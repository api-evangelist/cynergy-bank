---
name: Initiate a domestic payment via Cynergy Bank
description: Create a domestic payment consent, get the PSU to authorise it, optionally check funds, then submit the payment through Cynergy Bank's OBIE Read/Write Payment Initiation API.
api: openapi/cynergy-bank-payment-initiation-obie-standard-openapi.yaml
operations:
  - CreateDomesticPaymentConsents
  - GetDomesticPaymentConsentsConsentId
  - GetDomesticPaymentConsentsConsentIdFundsConfirmation
  - CreateDomesticPayments
  - GetDomesticPaymentsDomesticPaymentId
---

# Initiate a domestic payment (PIS)

Cynergy Bank implements the UK Open Banking (OBIE) Read/Write Payment Initiation API.
Payment writes require a regulated PISP identity, request signing, and idempotency.

## Prerequisites
- FCA/EEA-regulated Payment Initiation Service Provider registered in the OBIE Directory.
- Mutual-TLS with an OBIE/eIDAS transport certificate.
- Client-credentials token (`TPPOAuth2Security`, scope `payments`) for consent creation.
- Every write MUST carry `x-idempotency-key` (required) and a detached `x-jws-signature` (required).

## Steps
1. **Create the payment consent** — `CreateDomesticPaymentConsents` (POST `/domestic-payment-consents`)
   with the `Initiation` block (debtor/creditor, `InstructedAmount`). Include `x-idempotency-key` and
   `x-jws-signature`. Returns a `ConsentId` in `AwaitingAuthorisation`.
2. **PSU authorises** — redirect the customer through the authorization-code flow (`PSUOAuth2Security`)
   with strong customer authentication; obtain a PSU access token.
3. **Confirm the consent** — `GetDomesticPaymentConsentsConsentId`
   (GET `/domestic-payment-consents/{ConsentId}`); proceed only when `Status` is `Authorised`.
4. **(Optional) Check funds** — `GetDomesticPaymentConsentsConsentIdFundsConfirmation`
   (GET `/domestic-payment-consents/{ConsentId}/funds-confirmation`).
5. **Submit the payment** — `CreateDomesticPayments` (POST `/domestic-payments`) with the same
   `Initiation` and the `ConsentId`, a fresh `x-idempotency-key`, and `x-jws-signature`. Returns a
   `DomesticPaymentId`.
6. **Track status** — `GetDomesticPaymentsDomesticPaymentId`
   (GET `/domestic-payments/{DomesticPaymentId}`) until it reaches a terminal status.

## Rules
- `x-idempotency-key` is valid for 24h; retrying with the same key + identical body returns the
  original resource instead of double-paying (see `conventions/`).
- The `Initiation` submitted at step 5 must match the consented `Initiation` exactly.
- Errors use the OBIE `OBErrorResponse1` envelope; a `409`/`UK.OBIE.Rules.DuplicateReference` is an
  idempotency/duplicate conflict, a `UK.OBIE.Signature.Invalid` means the JWS failed verification.
