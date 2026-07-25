---
name: Evari public quote to confirmation
description: Take an insurance buyer from a new quote through questions, pricing and SMS confirmation on the Evari Quotes public surface, then hand back the quote PDF.
api: openapi/evari-quotes-api-openapi.yml
generated: '2026-07-25'
method: generated
source: openapi/evari-quotes-api-openapi.yml
operations:
  - PublicQuotePost
  - QuestionGetPublicQuestionsByQuote
  - PublicQuotePatch
  - PublicQuoteValidate
  - PublicQuoteGetPrice
  - PublicQuoteConfirmSMS
  - PublicQuoteConfirmSMSCode
  - PublicQuoteConfirmed
  - PublicQuotePdf
---

# Evari public quote to confirmation

Operates the customer-facing mirror of the Evari Quotes API — every path under
`/api/quotes/public/**`. Use this surface for anything a buyer touches; use the
internal surface (`evari-broker-quote-lifecycle.md`) for broker and underwriter work.

## Before you start

- **Auth.** Every operation requires an `Authorization` header (apiKey scheme). The
  spec declares no bearer format and no scopes. See
  `authentication/evari-authentication.yml`.
- **Access reality.** This API is tenant-scoped and closed. The spec was published in
  Evari's own `evari-quotes-api` npm tarball; the only named API root
  (`https://api.cloudstream.evari.tech/api`) returns 404 unauthenticated. You need a
  tenant credential from Evari — there is no self-serve sign-up.
- **No error contract.** The spec documents only 200/202/204. Do not branch on
  documented error codes; treat any non-2xx as unknown and surface the raw response.
- **Not idempotent.** There is no `Idempotency-Key`. Never blind-retry
  `PublicQuotePost` or the confirm operations — re-read with `PublicQuoteGet` first.

## Steps

1. **Create the quote.** `PublicQuotePost` — `POST /api/quotes/public/quotes` with a
   `QuoteCreateRequest` body (product, customer, initial answers). Returns a
   `QuoteResponse`; keep `id`.
2. **Fetch the question set.** `QuestionGetPublicQuestionsByQuote` —
   `GET /api/quotes/public/quotes/{id}/questions`. Returns `QuestionResponseList`;
   these are the product questions the pricing engine consumes.
3. **Answer them.** `PublicQuotePatch` — `PATCH /api/quotes/public/quotes/{id}` with a
   `QuoteUpdateRequest`. Patch incrementally as answers arrive; each patch re-runs the
   underwriting rules server-side.
4. **Validate before pricing.** `PublicQuoteValidate` —
   `GET /api/quotes/public/quotes/{id}/validate`. Do this before showing a price; it
   is the cheap check that the answer set is complete and admissible.
5. **Price it.** `PublicQuoteGetPrice` — `GET /api/quotes/public/quotes/{id}/price`.
   Read `priceComponents`, `priceSummary` **and** `priceErrors` — pricing failure is
   modelled as data on the response, not as an HTTP error. A populated `priceErrors`
   means no valid price, even on a 200.
6. **Send the confirmation code.** `PublicQuoteConfirmSMS` —
   `POST /api/quotes/public/quotes/{id}/confirmSMS`. Returns a `requestId`.
7. **Verify the code.** `PublicQuoteConfirmSMSCode` —
   `POST /api/quotes/public/quotes/{id}/confirmSMS/{requestId}` with the code the
   buyer received.
8. **Confirm the state.** `PublicQuoteConfirmed` —
   `GET /api/quotes/public/quotes/{id}/confirmed`. Only treat the quote as confirmed
   when this says so; never infer it from step 7's status alone.
9. **Return the document.** `PublicQuotePdf` —
   `GET /api/quotes/public/quotes/{id}/pdf`.

## Notes

- `PublicQuoteReconfirm` (`POST .../reconfirm`) re-issues confirmation on a quote that
  has already been through the flow — use it instead of restarting at step 1.
- The SMS confirmation pair exists **only** on the public surface; the internal surface
  confirms by code via `QuoteConfirm`.
- If the product needs a document from the buyer, `AttachmentPost` is on the internal
  surface only (`POST /api/quotes/attachments`, `multipart/form-data`).
- Referral: if underwriting refers the quote out of straight-through processing, stop
  here and switch to `evari-refer-quote-to-underwriter.md`.
