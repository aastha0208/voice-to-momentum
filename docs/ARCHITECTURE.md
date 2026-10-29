# Architecture

The application has no runtime package dependencies. `worker/index.js` embeds HTML/CSS/browser JavaScript and exports a Worker-compatible fetch handler. The Node adapter imports that same handler for local use.

## Browser

- Splits input on blank lines, preserving each paragraph as an excerpt.
- Builds four named questions per excerpt: `category_i`, `area_i`, `impact_i`, `followup_i`.
- Sends all excerpts as shared `state.excerpts`, instructing each question to evaluate its indexed excerpt.
- Uses custom categories/areas for choice options, plus fixed impact and follow-up instructions.
- Validates selected fields in returned answers, stores rows in memory, and applies routing.
- Stores only preferences in localStorage.

## Server

`POST /api/analyze` forwards model, state and questions to `https://api.typesafe.ai/v1/systemone`. The API key arrives from the current browser session and is used in the outbound Authorization header. The request has a 45-second upstream timeout. Input length/item/question limits are checked. Provider failures are returned to the UI. No automatic retries or cache are implemented.

## Routing

`needsReview(item, config)` checks approval, demo status, category confidence, unclear category and follow-up probability. `destination(item, config)` resolves a category's configured team or falls back to Human review. These are browser rules, not authorization controls for external actions.

## Design decisions

- Typed judgments are separate from routing policy.
- Missing impact is an explicit option.
- Low confidence is not the only reason for review.
- Demo provenance is visible and never passed off as live Jev.
- Human corrections preserve the original category and can be restored.

## Future engineering work

Before public multi-user hosting, assess authentication, rate limits, bounded request-body streaming, full upstream response validation and operational logging/retention. Extracting the embedded UI into modules would improve maintainability. Preserve evidence isolation when adding automated transcript extraction.
