# SmoovOps API

Everything you need to start calling the [SmoovOps](https://smoovops.com) REST API with a
Personal API Token (PAT).

## What's here

- **[`api-reference.md`](api-reference.md)** — every endpoint your token can call, with its
  request fields, mirrored from [smoovops.com/doc/api-reference](https://smoovops.com/doc/api-reference).
- **`smoovops-api.postman_collection.json`** + **`smoovops-api.postman_environment.json`** —
  the same endpoints as a ready-to-run Postman collection, grouped by resource with an
  example request body already filled in.

Both are auto-generated from SmoovOps' backend route definitions, so they always match what's
actually deployed.

## Quick start

1. Generate a token: sign in to SmoovOps (Starter or Pro plan) and go to
   [smoovops.com/doc/api-access](https://smoovops.com/doc/api-access) for the steps. You'll
   get a token (`smv_live_...`) and an API key — copy both, they're only shown once.
2. In Postman, select **Import** and add both JSON files from this repo.
3. Select the **SmoovOps API** environment (top right) and fill in `apiToken` and `apiKey`
   with the values from step 1.
4. Open any request and select **Send**.

That's it — token and key apply automatically to every request in the collection.

## Not included

Registration/login, newsletter, and webhook endpoints, plus token management itself, aren't
in the collection or the reference above — none of them accept a Personal API Token (they're
public, third-party-signed, or, for token management, deliberately blocked so a leaked token
can't mint or revoke tokens on its own).

## Found an issue?

Open an [issue](../../issues) — a wrong field or a missing endpoint is the fastest thing to
fix here.
