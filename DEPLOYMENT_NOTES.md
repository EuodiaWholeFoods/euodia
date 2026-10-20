# Company maintenance update

This branch is based on `EuodiaWholeFoods/euodia` at `2d674b9` and carries the
maintenance changes from the personal repository at `d8a70ae`. The repositories
have unrelated histories, so the source changes were applied on top of company
history. Files with only line-ending differences were preserved.

The company Google measurement ID is retained, using `GoogleAnalytics` rather
than passing a `G-` measurement ID to `GoogleTagManager`. The integration package
is pinned to 14.2.11, matching the installed Next.js version.

## Before merging or deploying

- Review the pull request and use a Vercel preview before changing production.
- Use Node.js 24.x. CI and `package.json` select this version.
- Configure server-only `SANITY_API_TOKEN` in the company Vercel project. Remove
  and rotate any write token previously exposed as `NEXT_PUBLIC_SANITY_TOKEN`.
- Check the JWT, Paystack, email, base URL, and Sanity project/dataset environment
  variables against `.env.example`. Actual credentials are not in this branch.
- Use test payment credentials for payment validation.

## Known release blockers

The initial maintenance work does not resolve every defect. The statistics API
still uses an invalid Sanity query. Checkout trusts client totals, payment/order
finalization is incomplete, several admin actions still write directly from the
browser, and sensitive data access and dependency vulnerabilities require further
work. See `PROJECT_REVIEW.md`. Keep this as a review branch until those issues and
the company environment are validated; do not treat a passing build as approval
to accept live orders.

## Validation of this branch

- Dependency installation and `npm run build` passed on Node 24.14.0, including
  lint/type validation and generation of 44 pages.
- HTTP checks passed for 12 pages, 20 login JS/CSS assets, manifest/icons, logo,
  dishes/categories APIs, and expected 400/401/403 authentication responses.
- The company analytics ID is present in each checked page. Browser event delivery
  and a real authenticated login redirect have not been verified.
- No credentials are tracked. No account, email, or payment mutations were made
  during these checks. The existing statistics query error remains confirmed.
