# Whop GraphQL API

Whop exposes a public GraphQL API alongside its REST v1 API. GraphQL is
positioned as the current primary interface for building Whop apps, while the
REST APIs are maintained for backward compatibility.

**Endpoint:** `https://api.whop.com/public-graphql`
**Method:** `POST` with a JSON body `{ "query": "...", "variables": { ... } }`
**Documentation:** https://docs.whop.com/developer/api/getting-started

## Authentication

Requests are authenticated with a Bearer token and (when acting on behalf of a
user or company) additional context headers:

- `Authorization: Bearer <API_KEY_OR_OAUTH_TOKEN>`
- `x-on-behalf-of: <USER_ID>` (optional; act as a specific user)
- `x-company-id: <COMPANY_ID>` (optional; scope to a company)
- `Content-Type: application/json`

## Representative operations

The following operations are documented in Whop's GraphQL examples. This is a
conceptual summary, not the full generated schema; the authoritative schema is
served from the endpoint via introspection.

- **Query `discoverySearch`** — search discoverable access passes / products,
  returning fields such as `title`, `route`, `headline`, and `logo`.
- **Query `publicUser`** — fetch a user's public profile.
- **Query `company` / `accessPass` / `plan`** — read company, access pass
  (product), and plan detail.
- **Mutation `dmsFeedData` / DM + forum operations** — fetch and post direct
  messages and forum content.
- **Membership / access queries** — check a user's access to an experience or
  access pass.

## Notes

- The `whop-schema.graphql` file in this directory is a **conceptual, modeled**
  SDL sketch of the core types (Company, AccessPass/Product, Plan, Membership,
  User, Payment) for discovery indexing. It is not Whop's authoritative
  generated schema — introspect the live endpoint for that.
- Rate limits on GraphQL are documented as 10 requests / 10 seconds, max query
  complexity 1000, max depth 10.

- Reference: https://docs.whop.com/developer/api/getting-started
- Schema (this repo): https://github.com/api-evangelist/whop
