---
name: Evari broker quote lifecycle
description: Create, answer, validate, price, compare and confirm an insurance quote on the internal broker/underwriter surface of the Evari Quotes API.
api: openapi/evari-quotes-api-openapi.yml
generated: '2026-07-25'
method: generated
source: openapi/evari-quotes-api-openapi.yml
operations:
  - QuotePost
  - QuestionGetByQuote
  - QuotePatch
  - QuotePatchByInternalKey
  - QuoteValidate
  - QuoteGetPrice
  - QuoteGetQuoteOptions
  - QuoteConfirm
  - QuoteConfirmed
  - QuotePdf
  - QuoteSearch
  - QuoteGetAllForCustomer
---

# Evari broker quote lifecycle

The internal (broker and underwriter) surface — everything under `/api/quotes/**` that
is not `/public/`. Same entities as the public mirror, more operations.

## Before you start

- **Auth.** `Authorization` header apiKey on every operation; no scopes are declared.
- **Pagination.** Collection operations take `offset`, `limit`, `sort` and `order` as
  query parameters and return `{items, total}`. See
  `conventions/evari-conventions.yml`.
- **No idempotency, no documented errors.** See the conventions artifact — the spec
  documents only 200/202/204 and there is no `Idempotency-Key`.

## Steps

1. **Create.** `QuotePost` — `POST /api/quotes/quotes` with a `QuoteCreateRequest`.
   Returns `QuoteResponse` with `id`, `customer`, `product`, `agentId`, `teamId` and
   `duplicateGroupId`.
2. **Load the question set.** `QuestionGetByQuote` —
   `GET /api/quotes/quotes/{id}/questions`.
3. **Answer.** Two routes, pick deliberately:
   - `QuotePatch` — `PATCH /api/quotes/quotes/{id}` with a `QuoteUpdateRequest`,
     addressing answers by answer id. Use this from a UI that already holds the
     question set.
   - `QuotePatchByInternalKey` — `PATCH /api/quotes/quotes/{id}/updatebyinternalkey`
     with a list of `QuoteItemToUpdateByInternalKey`. Use this when mapping in from
     another system (a policy admin system, a submission email, a spreadsheet) where
     you know the product's internal key but not Evari's answer ids. This is the
     integration-friendly route.
4. **Validate.** `QuoteValidate` — `GET /api/quotes/quotes/{id}/validate`.
5. **Price.** `QuoteGetPrice` — `GET /api/quotes/quotes/{id}/price`. Always read
   `priceErrors` alongside `priceComponents` and `priceSummary`; a 200 with populated
   `priceErrors` is a failed price, not a price.
6. **Compare options.** `QuoteGetQuoteOptions` —
   `GET /api/quotes/quote-options/{duplicateGroupId}`. Quote options are sibling
   quotes sharing a `duplicateGroupId`; this is how you present alternative
   limits/excesses side by side.
7. **Confirm.** `QuoteConfirm` — `GET /api/quotes/quotes/confirm/{code}`, then check
   `QuoteConfirmed` — `GET /api/quotes/quotes/{id}/confirmed`. `QuoteReconfirm`
   re-issues confirmation.
8. **Document.** `QuotePdf` — `GET /api/quotes/quotes/{id}/pdf`.

## Finding quotes

- `QuoteSearch` — `GET /api/quotes/search/quotes` with `q`, `offset`, `limit`, `sort`,
  `order`.
- `QuoteGetAllForCustomer` — `GET /api/quotes/customers/{id}/quotes`.
- `QuoteGetByProduct` and `QuoteCount` scope to a `productId`.

## Notes

- **Underwriting rules** come back on the `Quote` entity as `underwritingRules`; that
  is where a decline or a referral trigger shows up.
- **Date rules** are per product: `QuoteDateConfigGet` /
  `QuoteDateConfigPatch` on `/api/quotes/products/{id}/quote-date-config` govern
  allowable quote and inception date periods — check them before you set dates in a
  patch, not after.
- **Attachments.** `AttachmentPost` (`multipart/form-data`: `attachment` +
  `description`) and `AttachmentGet`.
- **Health.** `HealthHealthCheck` and `HealthDiagnostics` — the latter returns
  per-dependency status, useful before a batch run.
