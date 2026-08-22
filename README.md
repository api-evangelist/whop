# Whop (whop)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Whop is a marketplace and commerce platform for selling digital products, memberships, and access to online communities, courses, software, and other creator offerings. Sellers ("companies") list products (access passes) with pricing plans, take payments, and manage member access - frequently gating Discord or Telegram communities, apps, and content. Whop is free to start and monetizes through transaction fees rather than charging for API access.

Whop exposes a real, well-documented developer platform: a current **REST API (v1)** at `https://api.whop.com/api/v1` (with a sandbox at `https://sandbox-api.whop.com/api/v1`), a **GraphQL API** at `https://api.whop.com/public-graphql` positioned as the primary interface for building apps, JavaScript/TypeScript, Python, and Ruby SDKs, an app framework, OAuth, MCP servers, and a **realtime WebSocket** for apps.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/whop/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/whop/refs/heads/main/apis.yml)

## Access Model (honest notes)

- **Authentication is Bearer-token.** Two API key types - a Company/Account API key (your own account) and an App API key (companies that installed your app) - plus OAuth access tokens when acting on behalf of a signed-in Whop user. GraphQL requests may also carry `x-on-behalf-of` and `x-company-id` context headers. `company_id` is required on many REST list endpoints when using an API key.
- **No paid API tier.** Using the API is included with a Whop account. Whop's cost is transaction-based (payment processing, payouts, disputes, fraud, tax, affiliate) - see `plans/whop-plans-pricing.yml` and `finops/whop-finops.yml`, grounded against [docs.whop.com/fees](https://docs.whop.com/fees).
- **Multiple API generations.** The current surfaces are REST v1 and GraphQL. Older V5 and V2 REST generations remain for backward compatibility with different rate limits (see `rate-limits/whop-rate-limits.yml`).
- **Modeled vs. sourced.** Base URLs, the Bearer scheme, the `List memberships` / `List payments` parameters and response fields, the full resource/operation catalog, and the fee schedule are grounded in Whop's live docs (including its `llms.txt` index). Individual REST **action sub-paths** (for example membership cancel/pause/resume) and the object schemas beyond the two confirmed list responses are **modeled** from the documented operation names and flagged as such in the OpenAPI. The GraphQL `whop-schema.graphql` is a conceptual sketch, not Whop's generated schema. The WebSocket server URL is a **modeled placeholder** because Whop's docs connect via SDK rather than publishing a raw `wss://` endpoint.

## Tags

- Memberships
- Payments
- Creator Economy
- Marketplace
- Digital Products
- Access Control
- Commerce

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### Whop Memberships API

List, retrieve, and manage the lifecycle of memberships (a user's access to a product) - cancel, uncancel, pause, resume, add free days - plus membership webhooks.

- **Human URL:** [https://docs.whop.com/api-reference/memberships/list-memberships](https://docs.whop.com/api-reference/memberships/list-memberships)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Products API

Create, list, retrieve, update, and delete products (access passes) - the sellable offerings a company lists.

- **Human URL:** [https://docs.whop.com/api-reference/products/product](https://docs.whop.com/api-reference/products/product)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Plans API

Create, list, retrieve, update, and delete pricing plans attached to products, and calculate tax for a plan.

- **Human URL:** [https://docs.whop.com/api-reference/plans/plan](https://docs.whop.com/api-reference/plans/plan)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Payments API

List and retrieve payments with rich filtering, create off-session charges, list fees, and refund, retry, or void a payment, plus payment lifecycle webhooks.

- **Human URL:** [https://docs.whop.com/api-reference/payments/list-payments](https://docs.whop.com/api-reference/payments/list-payments)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Users API

Retrieve and list users, update the current user, and check whether a user has access to an access pass or experience.

- **Human URL:** [https://docs.whop.com/api-reference/users/user](https://docs.whop.com/api-reference/users/user)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Companies API

Create, list, retrieve, and update companies (whops), onboard sub-merchants, and mint child-company API keys.

- **Human URL:** [https://docs.whop.com/api-reference/companies/company](https://docs.whop.com/api-reference/companies/company)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Checkout Configurations API

Create, list, retrieve, and delete reusable checkout configurations for custom payment flows and off-session charging.

- **Human URL:** [https://docs.whop.com/api-reference/checkout-configurations/create-a-checkout-configuration](https://docs.whop.com/api-reference/checkout-configurations/create-a-checkout-configuration)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Transfers API

Programmatically pay out users and connected ledger accounts, and list and retrieve transfers.

- **Human URL:** [https://docs.whop.com/api-reference/transfers/create-transfer](https://docs.whop.com/api-reference/transfers/create-transfer)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Webhooks API

Register and manage webhook endpoints that receive platform events for memberships, payments, invoices, disputes, and more.

- **Human URL:** [https://docs.whop.com/api-reference/webhooks/webhook](https://docs.whop.com/api-reference/webhooks/webhook)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop Promo Codes API

Create, list, retrieve, update, and delete promo / discount codes applied at checkout.

- **Human URL:** [https://docs.whop.com/api-reference/promo-codes/promo-code](https://docs.whop.com/api-reference/promo-codes/promo-code)
- **Base URL:** `https://api.whop.com/api/v1`

### Whop GraphQL API

Whop's GraphQL API, positioned as the current primary interface for building apps - search/discovery, access passes, plans, memberships, users, and messaging.

- **Human URL:** [https://docs.whop.com/developer/api/getting-started](https://docs.whop.com/developer/api/getting-started)
- **Base URL:** `https://api.whop.com/public-graphql`

### Whop Realtime WebSocket API

Bidirectional realtime WebSocket for Whop apps - custom app messages and chat/feed updates - connected and authenticated through the `@whop/react` and `@whop/api` SDKs. No raw `wss://` endpoint URL is published; the base URL is a modeled placeholder (see the AsyncAPI document).

- **Human URL:** [https://docs.whop.com/apps/features/websocket-guide](https://docs.whop.com/apps/features/websocket-guide)
- **Base URL:** `wss://realtime.whop.com` (modeled placeholder)

## Common Properties

- [GitHub Organization](https://github.com/whopio)
- [LinkedIn](https://www.linkedin.com/company/whop)
- [Website](https://whop.com)
- [Documentation](https://docs.whop.com/developer/api/getting-started)
- [Plans](plans/whop-plans-pricing.yml)
- [Rate Limits](rate-limits/whop-rate-limits.yml)
- [Fin Ops](finops/whop-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
