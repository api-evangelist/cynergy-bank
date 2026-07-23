---
name: Confirm funds availability via Cynergy Bank (CBPII)
description: Create a funds-confirmation consent, get the PSU to authorise it, then make point-in-time funds availability checks through Cynergy Bank's OBIE Read/Write Confirmation of Funds API.
api: openapi/cynergy-bank-confirmation-of-funds-obie-standard-openapi.yaml
operations:
  - CreateFundsConfirmationConsents
  - GetFundsConfirmationConsentsConsentId
  - CreateFundsConfirmations
---

# Confirm funds availability (CBPII)

Cynergy Bank implements the UK Open Banking (OBIE) Read/Write Confirmation of Funds API,
letting a regulated Card Based Payment Instrument Issuer check funds availability.

## Prerequisites
- Regulated CBPII registered in the OBIE Directory.
- Mutual-TLS with an OBIE/eIDAS transport certificate.
- Client-credentials token (`TPPOAuth2Security`, scope `fundsconfirmations`).

## Steps
1. **Create the funds-confirmation consent** — `CreateFundsConfirmationConsents`
   (POST `/funds-confirmation-consents`) with the `DebtorAccount` to be checked. Returns a `ConsentId`.
2. **PSU authorises** — redirect the customer through the authorization-code flow (`PSUOAuth2Security`)
   with strong customer authentication; obtain a PSU access token.
3. **Confirm the consent** — `GetFundsConfirmationConsentsConsentId`
   (GET `/funds-confirmation-consents/{ConsentId}`); proceed only when `Status` is `Authorised`.
4. **Check funds** — `CreateFundsConfirmations` (POST `/funds-confirmations`) with the `ConsentId`
   and `InstructedAmount`. The response returns a boolean `FundsAvailable` (a point-in-time yes/no,
   not a reservation).

## Rules
- Payloads are wrapped in a top-level `Data` object; errors use the OBIE `OBErrorResponse1` envelope.
- A `403` / `UK.OBIE.Resource.InvalidConsentStatus` means the consent is not `Authorised`.
