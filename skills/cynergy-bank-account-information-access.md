---
name: Access Cynergy Bank account & transaction information
description: Set up an AIS access consent, get the PSU to authorise it, then read accounts, balances, and transactions from Cynergy Bank's OBIE Read/Write Account Information API.
api: openapi/cynergy-bank-account-information-obie-standard-openapi.yaml
operations:
  - CreateAccountAccessConsents
  - GetAccountAccessConsentsConsentId
  - GetAccounts
  - GetAccountsAccountIdBalances
  - GetAccountsAccountIdTransactions
---

# Access Cynergy Bank account & transaction information (AIS)

Cynergy Bank implements the UK Open Banking (OBIE) Read/Write Account & Transaction
Information API. Every read is consent-gated and requires a regulated AISP identity.

## Prerequisites
- You are an FCA/EEA-regulated Account Information Service Provider registered in the OBIE Directory.
- Mutual-TLS with an OBIE/eIDAS transport certificate (QWAC).
- A client-credentials access token (`TPPOAuth2Security`, scope `accounts`) for app-level calls.
- Send FAPI headers: `Authorization`, `x-fapi-interaction-id`, `x-fapi-auth-date` where applicable.

## Steps
1. **Create the access consent** — `CreateAccountAccessConsents` (POST `/account-access-consents`)
   with a client-credentials token. Request the `Permissions` you need (e.g. `ReadAccountsDetail`,
   `ReadBalances`, `ReadTransactionsDetail`). The response returns a `ConsentId` in status `AwaitingAuthorisation`.
2. **Redirect the PSU to authorise** — send the customer through the bank's authorization-code flow
   (`PSUOAuth2Security`) with strong customer authentication. On return you hold a PSU access token.
3. **Confirm the consent is authorised** — `GetAccountAccessConsentsConsentId`
   (GET `/account-access-consents/{ConsentId}`); proceed only when `Status` is `Authorised`.
4. **List the accounts** — `GetAccounts` (GET `/accounts`) with the PSU token to get `AccountId`s.
5. **Read balances** — `GetAccountsAccountIdBalances` (GET `/accounts/{AccountId}/balances`).
6. **Read transactions** — `GetAccountsAccountIdTransactions` (GET `/accounts/{AccountId}/transactions`),
   paging via the `Links.Next` cursor and filtering with `fromBookingDateTime`/`toBookingDateTime`.

## Rules
- Payloads are wrapped in a top-level `Data` object with `Links` + `Meta` siblings.
- Errors use the OBIE `OBErrorResponse1` envelope with `UK.OBIE.*` codes (see `errors/`).
- A `403` means the consent/token lacks the requested permission; a `429` means back off and retry.
