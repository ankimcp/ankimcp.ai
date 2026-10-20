---
title: "Delete Your AnkiMCP Account"
description: "How to delete your AnkiMCP account and its data, from the dashboard or by email. Applies to the AnkiMCP app for Android, the web dashboard, and the tunnel."
sitemap_priority: 0.3
---

## Delete your AnkiMCP account

This page explains how to delete the account you use with **AnkiMCP** (the AnkiMCP app for Android, the web dashboard at web.ankimcp.ai, and the AnkiMCP tunnel), published by AnkiMCP. You don't need to be signed in to read this page.

### Delete your account in the dashboard

1. Sign in at [web.ankimcp.ai](https://web.ankimcp.ai/) with the account you want to delete.
2. Open **Settings**, then the **General** tab.
3. Click **Delete account** and confirm.

Direct link: [web.ankimcp.ai/settings#delete-account](https://web.ankimcp.ai/settings#delete-account) (sign in first).

Deletion is **immediate and irreversible**.

### Before you delete: two things that block deletion

The dashboard refuses to delete an account that still has an active subscription or a hosted Anki instance, and tells you which one is in the way. Clear them first:

- **Cancel your subscription.**
  - Bought in the Android app through Google Play: cancel it in the **Play Store** (Play Store → your profile → Payments & subscriptions → Subscriptions). AnkiMCP can't cancel a Google Play subscription for you.
  - Bought on the website: cancel it from the dashboard's **Billing** page, which opens the Polar billing portal.
- **Delete your hosted Anki instance**, if you have one, from the **Hosted Anki** page in the dashboard. This permanently removes the collection and media stored for it.

### Delete without the app or dashboard

If you can't sign in, email [support@ankimcp.ai](mailto:support@ankimcp.ai) **from the email address on the account** and ask for deletion. We'll confirm by replying to that address, then delete the account. Subscription and hosted-instance checks apply the same way; we'll tell you if something still needs cancelling.

### What is deleted

- Your login (our Keycloak identity) and the sign-in method linked to it (Google, GitHub, or email/password).
- Your user record: email, display name, avatar, and account identifiers.
- Your subscription record and its link to your account.
- The OAuth client registrations that connected AI assistants to your tunnel.
- Hosted Anki data (collection and media) and media library files, if any remain.
- The push token registered by the Android app, if any.

### What is kept

- Records we are legally required to retain for tax and accounting purposes (for example invoices), kept for the statutory period and then deleted.
- Google Play and Polar keep their own payment records under their privacy policies; we never hold your card details.

Nothing else is kept. Your flashcards on your own device or in AnkiWeb are not touched; AnkiMCP never stored them unless you used Hosted Anki.

For the full picture of what we collect and how long we keep it, see the [Privacy Policy](/privacy/). Questions: [support@ankimcp.ai](mailto:support@ankimcp.ai).

---

*"Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent project and is not affiliated with, endorsed by, or sponsored by Ankitects. Google Play is a trademark of Google LLC.*
