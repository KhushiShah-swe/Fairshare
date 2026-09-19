# Run FairShare locally

[Back to the project](../README.md) · [Testing](TESTING.md) · [API](API.md)

## Requirements

| Tool | Use |
| --- | --- |
| JDK 17 | Matches the Java target in `pom.xml` and the existing CI workflow |
| Maven 3.9.x | Backend build and startup; the documented build uses Maven |
| Node.js 22.12+ and npm | Compatible with the Vite 7 frontend; install dependencies from the lockfile |
| MySQL 8.x | Local application database |
| Git | Clone the repository |

The repository includes older Gradle files and generated reports. Follow the Maven commands below to match the current CI build. No application source changes are required for this setup.

Use disposable demo accounts and a local database. The current account model needs further security work before public hosting.

## 1. Prepare MySQL

Start MySQL. In an administrative MySQL session, create a database and a dedicated local user:

```sql
CREATE DATABASE IF NOT EXISTS fairshare;
CREATE USER 'fairshare'@'localhost' IDENTIFIED BY 'replace-with-a-unique-local-password';
GRANT ALL PRIVILEGES ON fairshare.* TO 'fairshare'@'localhost';
```

Replace the example password before executing it. If the user already exists, use that account's password instead of running `CREATE USER` again. The database account needs schema privileges because the current configuration uses Hibernate `ddl-auto=update`.

Do not paste database credentials into repository files. Spring Boot environment variables override the existing application properties.

## 2. Clone and start the API

```bash
git clone https://github.com/KhushiShah-swe/fairshare-app.git
cd fairshare-app/backend/fairshare-backend
```

### Windows PowerShell

```powershell
$env:SPRING_DATASOURCE_URL = 'jdbc:mysql://localhost:3306/fairshare?useSSL=false&serverTimezone=UTC'
$env:SPRING_DATASOURCE_USERNAME = 'fairshare'
$localDbCredential = Get-Credential -UserName 'fairshare' -Message 'Enter your local MySQL password'
$env:SPRING_DATASOURCE_PASSWORD = $localDbCredential.GetNetworkCredential().Password
mvn spring-boot:run
```

The password prompt is for your local MySQL account. `JAVA_HOME` should point to the JDK 17 installation; `java -version` and `mvn -version` should resolve to the expected JDK.

### macOS or Linux with Bash

```bash
export SPRING_DATASOURCE_URL='jdbc:mysql://localhost:3306/fairshare?useSSL=false&serverTimezone=UTC'
export SPRING_DATASOURCE_USERNAME='fairshare'
read -rsp 'Local MySQL password: ' SPRING_DATASOURCE_PASSWORD; echo
export SPRING_DATASOURCE_PASSWORD
mvn spring-boot:run
```

The API starts at `http://localhost:8080/api`. The local URL disables database TLS for loopback development only. Hibernate creates or updates the schema on startup; no migration tool is configured. Do not separately import the historical `schema.sql` unless you have reviewed its compatibility with the current entities.

## 3. Start the React application

Open a second terminal at the repository root:

```bash
cd frontend/fairshare-frontend
npm ci
npm run dev -- --host localhost --port 5173 --strictPort
```

Visit **http://localhost:5173**. Use `localhost`, because the current API client and allowed browser origin use that host. The frontend Axios client points directly to `http://localhost:8080/api` and sends credentials. Changing deployment addresses would require a separate application configuration change.

## 4. Walk through a demo

Use synthetic data and distinct browser profiles for different demo users.

1. Register Alex, then create a group such as **Weekend trip**.
2. Copy its invite code. Register Sam in another browser profile and join that group.
3. Add a $60 expense paid by Alex, split equally between Alex and Sam. Sam's share is $30.
4. Add another expense using selected participants and percentage allocation; ensure the percentages total 100.
5. Attach a synthetic image or PDF receipt and open its preview.
6. Review the group balances and consolidated settlement instructions. Export the CSV balance sheet.
7. Explore Zelle reference fields using demo information only. No banking credentials or actual transfers are needed.

The current **Clear All Debts** operation deletes the group's expense and split records, including receipt data attached to those expenses. Use a disposable group if demonstrating it. The individual dashboard settlement action is not a completed payment-recording flow.

## Configuration reference

| Environment variable | Purpose |
| --- | --- |
| `SPRING_DATASOURCE_URL` | Override the local MySQL JDBC URL |
| `SPRING_DATASOURCE_USERNAME` | Override the database username |
| `SPRING_DATASOURCE_PASSWORD` | Override the database password |
| `SERVER_PORT` | Spring Boot server port; the unchanged frontend expects 8080 |

These variables are consumed by Spring Boot. The current frontend does not implement a `VITE_API_URL` configuration option.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| `Access denied for user` | Verify the local MySQL user, password, host, and privileges. Set the environment variables in the same terminal that launches Maven. |
| Database connection refused | Start MySQL and confirm it listens on localhost port 3306. |
| Java compilation/version error | Check both `java -version` and `mvn -version`; confirm JDK 17 is selected. |
| npm engine/version error | Use Node 22.12+ and run `npm ci` again. Avoid replacing the lockfile as a workaround. |
| Vite cannot bind port 5173 | Stop the process using that port. The current CORS configuration expects 5173. |
| Browser cannot reach the API | Confirm the API started, use localhost in both URLs, and inspect the failed request in browser developer tools. |
| Root API URL returns 404 | There is no API landing page or configured Swagger UI. Use a documented route in [API.md](API.md). |

Stop each running service with `Ctrl+C`. MySQL records remain in the local database. Clear demo browser storage when finished; login responses are currently stored in `localStorage`.
