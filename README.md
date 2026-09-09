# nalgo-legal

The public legal pages for the Nalgo app: terms, community guidelines, and
privacy policy. Plain static HTML, no build step.

## Publishing on GitHub Pages

1. Repo → **Settings → Pages** → Source: **Deploy from a branch**, branch
   `main`, folder `/ (root)`.
2. The pages appear at <https://etoushek-max.github.io/nalgo-legal/>.

## Then wire the URLs back into the app

In the Nalgo app repo, `lib/legal.ts`:

```ts
export const PRIVACY_POLICY_URL = 'https://etoushek-max.github.io/nalgo-legal/privacy.html';
export const TERMS_OF_SERVICE_URL = 'https://etoushek-max.github.io/nalgo-legal/terms.html';
```

Both URLs also go into the store listings: App Store Connect wants a privacy
policy URL (and a EULA/terms URL if you are not using Apple's standard EULA),
and Google Play wants a privacy policy URL in the Data Safety section.

## Before you publish

Every placeholder is highlighted in yellow on the rendered page — search the
HTML for `class="todo"` to find them all. They cover:

- the operating name and address behind Nalgo
- governing law and venue
- where Supabase hosts your data (needed for GDPR transfer disclosures)
- GDPR legal bases, data-subject response time, and retention periods
- whether Sentry is configured to attach user IDs to crash reports

`nalgosupport@gmail.com` appears throughout as the contact address. It must be a
mailbox someone actually reads — app reviewers sometimes test it.

These are drafts to review, not legal advice. Have someone qualified read them
for your jurisdiction before you rely on them.

## Keeping the app in step

The app carries its own copy of the terms, so the sign-up gate can show them on
a cold first launch with nothing hosted yet. It lives in `TERMS_SECTIONS` in
`lib/legal.ts` in the Nalgo app repo. If you change the terms here, change them there
too, and bump `TERMS_VERSION` — that version is recorded against every account
at sign-up.
