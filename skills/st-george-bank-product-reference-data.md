---
name: Browse St.George banking products (public CDR PRD)
description: >-
  Retrieve St.George Bank's publicly available banking product catalogue via the
  Consumer Data Right Product Reference Data (PRD) API. No authentication or
  consent is required — this is the one publicly callable St.George CDR surface.
api: openapi/st-george-bank-cds-banking-products-openapi.yml
operations: [listBankingProducts, getBankingProductDetail]
---

# Browse St.George banking products (public CDR PRD)

The Product Reference Data endpoints are **public and unauthenticated**. Base URL:
`https://digital-api.stgeorge.com.au/cds-au/v1`.

## Rules
- Always send the `x-v` request header (endpoint version). Products supports `x-v: 4` and `x-v: 5`; `x-v: 3` returns `406 Unsupported Version`. Prefer the highest you support.
- Optionally send `x-min-v` to accept a range, and `x-fapi-interaction-id` (an RFC 4122 UUID) for correlation — the response echoes it.
- Pagination is page-number: `page` (default 1) and `page-size` (default 25). Read `meta.totalPages` / `meta.totalRecords` and follow `links.next`.

## Steps
1. `listBankingProducts` — `GET /banking/products` with `x-v: 5`. Optional filters include `product-category` (a `BankingProductCategoryV2` value such as `TRANS_AND_SAVINGS_ACCOUNTS`, `CRED_AND_CHRG_CARDS`, `TERM_DEPOSITS`, `RESIDENTIAL_MORTGAGES`), `effective`, and `updated-since`. Iterate pages until `links.next` is absent.
2. For any product of interest, take its `productId` and call `getBankingProductDetail` — `GET /banking/products/{productId}` with `x-v: 5` — to read full features, rates, fees and eligibility.

## Errors
- `400 urn:au-cds:error:cds-all:Field/InvalidPageSize` — `page-size` out of range.
- `400 urn:au-cds:error:cds-all:Header/Missing` — `x-v` header omitted.
- `406 urn:au-cds:error:cds-all:Header/UnsupportedVersion` — requested version not supported.
- `404 urn:au-cds:error:cds-all:Resource/NotFound` — unknown `productId`.
See errors/st-george-bank-problem-types.yml and conventions/st-george-bank-conventions.yml.
