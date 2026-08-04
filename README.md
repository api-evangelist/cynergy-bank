# Cynergy Bank (cynergy-bank)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Cynergy Bank is an FCA- and PRA-authorised UK specialist bank (FCA reference 575105) serving the blended personal and business banking needs of business owners, property entrepreneurs, and family businesses. It was formed in December 2018 when Cynergy Capital acquired Bank of Cyprus UK for approximately £103m and rebranded the business as Cynergy Bank. As a UK ASPSP it complies with PSD2 and the UK Open Banking Standard, exposing the OBIE Read/Write APIs — Account & Transaction Information (AIS), Payment Initiation (PIS), and Confirmation of Funds (CBPII) — to FCA/EEA-regulated Third Party Providers through its Open Banking developer portal. It is not one of the nine CMA-mandated banks (CMA9).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cynergy-bank/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cynergy-bank/refs/heads/main/apis.yml)

## Tags

- Financial Services
- Banking
- Open Banking
- PSD2
- OBIE
- United Kingdom
- Payments
- Account Information
- Confirmation of Funds
- Specialist Lender

## Timestamps

- **Created:** 2026-07-23
- **Modified:** 2026-07-23

## APIs

### Cynergy Bank Account & Transaction Information API (AIS)

Cynergy Bank's implementation of the OBIE Read/Write Account & Transaction Information (AISP) API, allowing regulated Account Information Service Providers to retrieve customer account, balance, transaction, and product data with customer consent. FAPI-secured (OAuth2/OIDC, mTLS, PSD2 SCA).

- **Human URL:** [https://developer.openbanking.cynergybank.co.uk/](https://developer.openbanking.cynergybank.co.uk/)

#### Tags

- Account Information
- AISP
- Open Banking

#### Properties

- [OpenAPI](openapi/cynergy-bank-account-information-obie-standard-openapi.yaml) — shared OBIE Read/Write standard (Account & Transaction v4.0.1)
- [Documentation](https://developer.openbanking.cynergybank.co.uk/)
- [Documentation](https://www.cynergybank.co.uk/support/open-banking)

### Cynergy Bank Payment Initiation API (PIS)

Cynergy Bank's implementation of the OBIE Read/Write Payment Initiation (PISP) API, allowing regulated Payment Initiation Service Providers to initiate domestic and scheduled payments on behalf of customers with their consent. FAPI-secured (OAuth2/OIDC, mTLS, PSD2 SCA).

- **Human URL:** [https://developer.openbanking.cynergybank.co.uk/](https://developer.openbanking.cynergybank.co.uk/)

#### Tags

- Payment Initiation
- PISP
- Open Banking

#### Properties

- [OpenAPI](openapi/cynergy-bank-payment-initiation-obie-standard-openapi.yaml) — shared OBIE Read/Write standard (Payment Initiation v4.0.1)
- [Documentation](https://developer.openbanking.cynergybank.co.uk/)
- [Documentation](https://www.cynergybank.co.uk/support/open-banking)

### Cynergy Bank Confirmation of Funds API (CBPII)

Cynergy Bank's implementation of the OBIE Read/Write Confirmation of Funds (CBPII) API, allowing regulated Card Based Payment Instrument Issuers to confirm whether sufficient funds are available on a customer account with the customer's consent. FAPI-secured (OAuth2/OIDC, mTLS, PSD2 SCA).

- **Human URL:** [https://developer.openbanking.cynergybank.co.uk/](https://developer.openbanking.cynergybank.co.uk/)

#### Tags

- Confirmation of Funds
- CBPII
- Open Banking

#### Properties

- [OpenAPI](openapi/cynergy-bank-confirmation-of-funds-obie-standard-openapi.yaml) — shared OBIE Read/Write standard (Confirmation of Funds v4.0.1)
- [Documentation](https://developer.openbanking.cynergybank.co.uk/)
- [Documentation](https://www.cynergybank.co.uk/support/open-banking)

## Common Properties

- [Website](https://www.cynergybank.co.uk/)
- [Developer Portal](https://developer.openbanking.cynergybank.co.uk/)
- [Open Banking Documentation](https://www.cynergybank.co.uk/support/open-banking)
- [LinkedIn](https://uk.linkedin.com/company/cynergy-bank)
- [Support](https://www.cynergybank.co.uk/support/)
- [Privacy Policy](https://www.cynergybank.co.uk/privacy-policy)
- [Terms of Service](https://www.cynergybank.co.uk/privacy-policy/legal-cynergy-bank)
- [Document Library](https://www.cynergybank.co.uk/document-library)
- [Information Security](https://www.cynergybank.co.uk/support/security-and-fraud/information-security)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
