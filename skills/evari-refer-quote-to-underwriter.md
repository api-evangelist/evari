---
name: Evari refer a quote to an underwriter
description: Move a quote out of straight-through processing into human underwriting on the Evari Quotes API — refer, review, note, override cover prices and return a decision.
api: openapi/evari-quotes-api-openapi.yml
generated: '2026-07-25'
method: generated
source: openapi/evari-quotes-api-openapi.yml
operations:
  - ReferredQuoteGetByQuoteId
  - ReferredQuoteReferQuoteToUnderwriter
  - ReferredQuoteGet
  - ReferredQuoteCreateNote
  - ReferredQuoteGetAllNotes
  - ReferredQuoteUpdate
  - ReferredQuoteSearch
  - ReferredQuoteGetAll
---

# Evari refer a quote to an underwriter

Referral is a first-class entity in the Evari quoting model, not a status flag. A
`ReferredQuote` wraps the underlying quote and carries its own notes and cover price
overrides.

## Before you start

- **Auth.** `Authorization` header apiKey on every operation.
- **Trigger.** A quote lands in referral when its `underwritingRules` say so — read
  them off the `Quote` after `QuoteValidate` / `QuoteGetPrice`. There is no separate
  "is referred" endpoint.
- **No documented failure responses.** Treat any non-2xx as unknown.

## Steps

1. **Check whether a referral already exists.** `ReferredQuoteGetByQuoteId` —
   `GET /api/quotes/quotes/{quoteId}/referred-quotes`. Do this first; referring twice
   is not idempotent and the API gives you no key to deduplicate on.
2. **Refer.** `ReferredQuoteReferQuoteToUnderwriter` —
   `POST /api/quotes/referred-quotes/{referredQuoteId}/refer-to-underwriter`. The
   public mirror of this is `PublicReferredQuoteReferQuoteToUnderwriter`, for a
   customer-initiated referral.
3. **Read the referral.** `ReferredQuoteGet` —
   `GET /api/quotes/referred-quotes/{id}`. Returns `ReferredQuoteResponse`, which
   embeds the full `QuoteResponse` plus `notes` and `coverPriceOverrides`.
4. **Work the queue.** `ReferredQuoteGetAll` (`GET /api/quotes/referred-quotes`),
   `ReferredQuoteGetAllByProduct`
   (`GET /api/quotes/products/{productId}/referred-quotes`) and `ReferredQuoteSearch`
   (`GET /api/quotes/search/referred-quotes`, free-text `q`). All take
   `offset`/`limit`/`sort`/`order`; `ReferredQuoteGetAll` also takes `status`.
5. **Add underwriter notes.** `ReferredQuoteCreateNote` —
   `POST /api/quotes/referred-quotes/{referredQuoteId}/notes`; read them back with
   `ReferredQuoteGetAllNotes` or a single note with `ReferredQuoteGetNote`. Notes are
   the audit trail of the underwriting decision — write one for every decision, not
   just declines.
6. **Return the decision.** `ReferredQuoteUpdate` —
   `PUT /api/quotes/referred-quotes/{id}` with a `ReferredQuoteUpdateRequest`. This is
   where `ReferredQuoteCoverPriceOverride` entries are applied — a per-cover price
   override, not a whole-quote adjustment.
7. **Hand back.** Re-read the quote with `QuoteGet` and re-run `QuoteGetPrice` so the
   broker sees the overridden price before confirmation.

## Notes

- **Agent-safety.** Steps 2, 5 and 6 are consequential writes against an underwriting
  decision. Treat `ReferredQuoteUpdate` (price override) as human-in-the-loop; see
  `agentic-access/evari-agentic-access.yml`.
- The customer-facing surface can only *read* a referral
  (`PublicReferredQuoteGet`, `PublicReferredQuoteGetByQuoteId`) and initiate one — it
  cannot update or note it.
