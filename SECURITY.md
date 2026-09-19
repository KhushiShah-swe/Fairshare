# Security policy

FairShare is an educational portfolio application intended for local demonstrations with synthetic data. The current authentication and authorization model requires further work before a public deployment with real users or financial records. See the [engineering roadmap](docs/ROADMAP.md).

## Report a concern privately

Contact the repository maintainer, **Khushi Shah**, at **khushishah.r.009@gmail.com** with the subject `FairShare security report`.

Include the affected commit, relevant component, impact, and minimal reproduction using test accounts. Do not send real passwords, banking information, production receipts, or personal records. Avoid public issue comments containing exploitable details or credentials.

There is no guaranteed response time or supported production release series. Security improvements are tracked against `main` as development work.

## Local evaluation

Use a disposable local database, unique demo credentials, and synthetic receipts. Supply database credentials through environment overrides described in [SETUP.md](docs/SETUP.md). Keep the app local while evaluating it. Zelle information in the interface is a payment reference; FairShare does not initiate or verify bank transfers.
