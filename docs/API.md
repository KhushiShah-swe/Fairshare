# API reference

[Back to the project](../README.md) · [Setup](SETUP.md) · [Architecture](ARCHITECTURE.md)

Local base URL: **`http://localhost:8080/api`**. This reference describes the controller mappings in the current source. There is no configured Swagger/OpenAPI UI.

The prototype accepts several user IDs in request parameters or bodies. These are part of its present interface, not proof of authorization. Evaluate with synthetic local data; consistent authenticated access is tracked in [#15](https://github.com/KhushiShah-swe/fairshare-app/issues/15).

## Accounts and payment references

| Method | Path | Input / purpose |
| --- | --- | --- |
| POST | `/auth/signup` | JSON `name`, `email`, `password`; create a demo account |
| POST | `/auth/login` | JSON `email`, `password`; login and set the HTTP session user |
| GET | `/auth/{userId}/zelle` | Get payment-reference metadata |
| PUT | `/auth/{userId}/zelle` | Optional query parameters `zelleEmail`, `zellePhone` |
| POST | `/auth/{userId}/zelle/qr` | Multipart `file`; upload or replace a QR image |
| GET | `/auth/{userId}/zelle/qr` | Retrieve QR bytes |
| DELETE | `/auth/{userId}/zelle/qr` | Remove QR data |

The account endpoints return a user entity in the current implementation. A safe response DTO and stronger account protection are future work. Payment-reference endpoints do not contact Zelle or perform banking operations.

## Groups

| Method | Path | Input / purpose |
| --- | --- | --- |
| POST | `/groups/create` | Query parameters `name`, `type`, `userId` |
| POST | `/groups/join` | Query parameters `code`, `userId` |
| GET | `/groups/user-groups/{userId}` | List a user's memberships |
| GET | `/groups/group-members/{groupId}` | List group memberships |
| PUT | `/groups/{groupId}/update-name` | Query parameters `newName`, `userId` |
| DELETE | `/groups/{groupId}/leave` | Query parameter `userId` |
| DELETE | `/groups/{groupId}/delete` | Query parameter `userId`; group deletion |

Group creation uses HTTP 201 on success. Rename and deletion contain ADMIN membership checks based on the supplied user ID; authentication and authorization still need to be enforced consistently at the API boundary.

## Expenses and receipts

| Method | Path | Input / purpose |
| --- | --- | --- |
| POST | `/expenses/add` | JSON expense request; HTTP 201 with `expenseId` on success |
| GET | `/expenses/{id}` | Get an expense |
| GET | `/expenses/{id}/splits` | Get participant allocation for editing |
| GET | `/expenses/group/{groupId}` | List expenses in a group |
| PUT | `/expenses/edit/{id}` | JSON expense request; replace expense details and splits |
| DELETE | `/expenses/delete/{id}` | Delete the expense and its split records |
| POST | `/expenses/{id}/receipt` | Multipart `file`; upload or replace a receipt |
| GET | `/expenses/{id}/receipt/info` | Get receipt filename/type/presence metadata |
| GET | `/expenses/{id}/receipt` | Retrieve receipt bytes |
| DELETE | `/expenses/{id}/receipt` | Remove receipt data |

### Example percentage expense

The following IDs are placeholders. Use the group, payer, and participant IDs from your local demo accounts.

```json
{
  "description": "Weekend groceries",
  "amount": 120.00,
  "paidBy": 1,
  "groupId": 1,
  "participants": [1, 2, 3],
  "category": "Food",
  "expenseDate": "2026-09-19",
  "notes": "Synthetic demo expense",
  "splitType": "PERCENTAGE",
  "percentages": {"1": 50, "2": 30, "3": 20}
}
```

For an equal split, use `"splitType": "EQUAL"` and omit `percentages`. Percentage-map keys must correspond to the selected participants and values must sum to 100 within the current tolerance. The current implementation allows zero percentage values; stricter rules and exact currency allocation are tracked in [#16](https://github.com/KhushiShah-swe/fairshare-app/issues/16).

Receipt service validation accepts a reported MIME type of `image/*` or `application/pdf`; QR validation accepts `image/*`. The multipart file and total request limits are each 5 MB. This is not a content-scanning guarantee, and multipart overhead can make a file near 5 MB exceed the total request limit.

## Balances, exports, and settlement

| Method | Path | Purpose |
| --- | --- | --- |
| GET | `/expenses/balance/{userId}` | Per-group user net balances |
| GET | `/expenses/activity/{userId}` | Recent expense activity |
| GET | `/expenses/group/{groupId}/settlement-plan` | Consolidated direct payment instructions |
| GET | `/expenses/group/{groupId}/balance-sheet` | Expense, balance, and instruction data |
| GET | `/expenses/group/{groupId}/export/csv` | Download `group_{groupId}_balance_sheet.csv` |
| POST | `/expenses/group/{groupId}/clear-debts` | **Deletes the group's expenses and split records** |

The CSV contains sections for expenses, balances, and settlement instructions. A PDF export endpoint is not implemented. The dashboard references `POST /expenses/settle`, but no corresponding controller route is present; completing that flow is tracked in [#17](https://github.com/KhushiShah-swe/fairshare-app/issues/17).

## Errors and integration notes

Response bodies vary by controller: some failures return plain text, others an `error` map or an empty response. Common statuses include 400 for selected validation errors, 403 for group role checks, 404 for missing records, and 500 for unhandled/service failures. Do not assume a unified Problem Details schema.

There is no API version prefix, pagination contract, or payment webhook integration. Application source and controller tests remain the authority for exact response behavior.
