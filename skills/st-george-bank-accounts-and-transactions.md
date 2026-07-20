---
name: Read consented accounts, balances and transactions (CDR ADR)
description: >-
  Read a customer's St.George accounts, balances and transactions through the
  Consumer Data Right data-sharing APIs. Requires a CDR-accredited Data
  Recipient (ADR) OAuth2 access token and an active consent/sharing arrangement
  — there is no public self-serve access.
api: openapi/st-george-bank-cds-banking-products-openapi.yml
operations: [listBankingAccounts, getBankingAccountDetail, listBankingBalancesBulk, getBankingBalance, listBankingTransactions, getBankingTransactionDetail]
---

# Read consented accounts, balances and transactions (CDR ADR)

These resources are **gated**: you must be a CDR-accredited Data Recipient with a
valid OAuth2 / FAPI access token bound to the customer's consent. Do not attempt
without accreditation — you will not obtain a token.

## Preconditions
- OAuth2 authorization-code flow through the CDR Register (PAR + PKCE, mutual-TLS or `private_key_jwt` client auth). See authentication/st-george-bank-authentication.yml.
- Scopes granted in the consent: `bank:accounts.basic:read` (+ `bank:accounts.detail:read` for detail), `bank:transactions:read`. See scopes/st-george-bank-scopes.yml.
- Send `x-v` on every call; include FAPI headers (`x-fapi-auth-date`, `x-fapi-customer-ip-address`, `x-cds-client-headers`) as required for customer-present calls.

## Steps
1. `listBankingAccounts` — `GET /banking/accounts`, paginate with `page`/`page-size`. Requires `bank:accounts.basic:read`.
2. `getBankingAccountDetail` — `GET /banking/accounts/{accountId}` for full account detail. Requires `bank:accounts.detail:read`.
3. Balances: `getBankingBalance` — `GET /banking/accounts/{accountId}/balance` for one account, or `listBankingBalancesBulk` — `GET /banking/accounts/balances` across all consented accounts.
4. Transactions: `listBankingTransactions` — `GET /banking/accounts/{accountId}/transactions` (supports `oldest-time`/`newest-time`/`min-amount`/`max-amount`/`text` filters); then `getBankingTransactionDetail` — `GET /banking/accounts/{accountId}/transactions/{transactionId}` for enriched detail.

## Errors & tracing
- `404 urn:au-cds:error:cds-all:Resource/NotFound` — unknown/unshared `accountId` or `transactionId`.
- `404 urn:au-cds:error:cds-banking:Authorisation/RevokedConsent` — the sharing arrangement was revoked; stop and re-consent.
- Correlate support requests with the `x-fapi-interaction-id` echoed on every response.
See errors/st-george-bank-problem-types.yml and conventions/st-george-bank-conventions.yml.
