

> Use this checklist to identify GraphQL attack surfaces such as sensitive fields, broken auth, enum abuse, introspection leaks, and more.

## Common Endpoints to Probe
- [ ] `/graphql`
- [ ] `/api/graphql`
- [ ] `/gql`
- [ ] `/graphiql`
- [ ] `/v1/graphql`
- [ ] `/graphql/console`
- [ ] `/playground`

## Discovery & Introspection
- [ ] Introspection query enabled (`__schema`, `__type`)
- [ ] Field listing via `{__schema{types{name,fields{name}}}}`
- [ ] Type enumeration (`__type(name: "User")`)
- [ ] Detect hidden queries via GraphQL error messages

## Authentication/Authorization Insertion Points
- [ ] `me`, `user`, `viewer` – self-data leak
- [ ] `getUser(id: X)` – IDOR
- [ ] `updateUser(id: X)` – IDOR/Privilege Escalation
- [ ] `deleteUser(id: X)` – destructive IDOR
- [ ] `role`, `isAdmin`, `isSuperuser` flags in mutation

## Sensitive Field Access
- [ ] `password`, `passwordHash`, `pwd`
- [ ] `ssn`, `socialSecurityNumber`
- [ ] `token`, `authToken`, `accessToken`
- [ ] `secret`, `privateKey`, `apiKey`, `licenseKey`
- [ ] `email`, `phone`, `address`, `dob`

## Injection Opportunities
- [ ] String-based arguments (`username: "admin'--"`)
- [ ] JSON-based filters (`filter: {name: {eq: "abc"}}`)
- [ ] Arguments with file paths (`path`, `url`, `file`)
- [ ] Object-type mutation input (`input: {data}` injection)
- [ ] Batching queries for race condition
- [ ] Overloading aliases to bypass rate limits

## Abusing GraphQL Features
- [ ] `__typename` leak for internal logic
- [ ] Query aliasing (`alias1: getUser(id:1)`)
- [ ] Deep query nesting → DoS
- [ ] Query fragments (`... on User`)
- [ ] Mutations without auth
- [ ] Unauthenticated access to `mutation { login(...) }`
- [ ] Multiple operation types in one query

## WAF/CDN & Logic Bypass
- [ ] Use `POST` instead of `GET`
- [ ] Non-standard `Content-Type` (`application/graphql`)
- [ ] Use `alias`, `fragment`, `__typename` to bypass wordlists
- [ ] Alternate spellings like `me`, `viewer`, `myProfile`, etc.

## Input Types for Logic Injection
- [ ] `orderBy`, `sortBy`, `filter` → logic tampering
- [ ] `status`, `role`, `type` → privilege escalation
- [ ] Boolean bypasses (`isActive: true`)
- [ ] `limit`, `offset`, `pagination` → enumeration

## Error & Response Leaks
- [ ] GraphQL stack trace reveals server internals
- [ ] Full DB error from malformed query
- [ ] Enum/type error leaks sensitive field names
- [ ] Rate limit or caching info in HTTP headers

## Automation Vectors
- [ ] Query batching for automation
- [ ] Duplicate queries with varied parameters
- [ ] Reuse of tokens in different contexts
- [ ] GraphQL subscription endpoints (`ws://...`)

## Advanced Insertion
- [ ] Use of `@skip`, `@include` directives
- [ ] Introspecting deprecated types (`isDeprecated`)
- [ ] GraphQL-to-SQLi or NoSQLi via user-controlled args
- [ ] Nested input injections (input → nested object injection)