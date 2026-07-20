# St.George Bank (st-george-bank)

St.George Bank is one of Australia's largest retail and business banks and a division of Westpac Banking Corporation (ASX:WBC), one of the country's "Big Four" banks. Originally a New South Wales building society that grew into an independent ADI, St.George merged into the Westpac Group in 2008 and today operates as a Westpac brand alongside BankSA, Bank of Melbourne and RAMS. As an authorised deposit-taking institution it is a designated Data Holder under Australia's Consumer Data Right (CDR / Open Banking), and therefore exposes a public, unauthenticated Product Reference Data (PRD) API conforming to the DSB Consumer Data Standards, alongside the consented, ADR-gated CDR data-sharing APIs. St.George does not operate a broad public developer portal beyond its CDR Open Banking surface.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/st-george-bank/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/st-george-bank/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- Product Reference Data
- Westpac Group

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### St.George Bank CDR Product Reference Data API

Public, unauthenticated Consumer Data Right Product Reference Data (PRD) API exposing St.George's openly available banking product catalogue (transaction and savings accounts, credit cards, loans, term deposits) under the standard CDS path `/cds-au/v1/banking/products`. Confirmed live returning HTTP 200 with a `data.products` array; supports `x-v` versions 4 and 5. Conforms to the DSB Consumer Data Standards Banking API contract.

- **Human URL:** [https://www.stgeorge.com.au/online-services/open-banking](https://www.stgeorge.com.au/online-services/open-banking)
- **Base URL:** `https://digital-api.stgeorge.com.au/cds-au/v1`

#### Tags

- Open Banking
- CDR
- Product Reference Data
- Banking
- Australia

#### Properties

- [Documentation](https://www.stgeorge.com.au/online-services/open-banking)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_get-products)
- [OpenAPI](openapi/st-george-bank-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.stgeorge.com.au/)
- [Portal](https://www.stgeorge.com.au/online-services/open-banking)
- [Documentation](https://www.stgeorge.com.au/online-services/open-banking/error-mapping)
- [Privacy Policy](https://www.stgeorge.com.au/privacy/privacy-statement)
- [Terms of Service](https://www.stgeorge.com.au/help/terms-conditions)
- [Support](https://www.stgeorge.com.au/online-services/security-centre)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
