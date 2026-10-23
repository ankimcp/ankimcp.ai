---
title: "Privacy Policy"
description: "Privacy Policy for ankimcp.ai, the AnkiMCP open-source project, and the AnkiMCP SaaS cloud service."
sitemap_priority: 0.3
---

## Privacy Policy

**Effective Date:** October 24, 2026

{{< callout type="info" >}}
**The short version.** This summary is for convenience only — the full policy below is what applies.

- The main website uses anonymous, **cookieless** analytics and needs no account. If you arrive from an ad, a campaign, or a partner's referral link, we set a cookie that remembers where you came from, and save that to your account if you sign up.
- Your flashcards **only pass through** our tunnel servers — they are never stored, logged, or read.
- Two optional features are different. **Hosted Anki** runs a copy of Anki on our servers, so your collection and media **are stored there** while your instance exists and are permanently removed when you delete it. Your **AnkiWeb password is never stored** — you enter it yourself inside the remote desktop. The **media library** stores the files you upload or generate (text you submit for audio generation is processed by Microsoft Azure) until you delete them.
- The community forum and the cloud service each need their own account; the forum and the SaaS dashboard use cookies to keep you signed in.
- The **AnkiMCP app for Android** has no analytics or crash reporting. Your collection stays on your phone; only your AI's requests and the app's answers pass through our relay, and they're never stored.
- Our application logs do **not** record the IP addresses of normal tunnel or MCP traffic. Our request traces record the network address each request came from, for up to 14 days. If our systems detect possible abuse, we may keep additional technical data to investigate it. Service logs are kept for up to 14 days; performance metrics for 7 days.
- Email [support@ankimcp.ai](mailto:support@ankimcp.ai) to see or delete the data we hold about you.
{{< /callout >}}

This Privacy Policy describes how ankimcp.ai ("Website"), the AnkiMCP software ("Software", including the AnkiMCP app for Android), and the AnkiMCP SaaS cloud service ("SaaS Service") handle your information.

### 1. Information We Collect

#### Website Analytics
We use [Umami](https://umami.is), a privacy-focused, self-hosted analytics platform. Umami collects:

- Page views and referrer URLs
- Browser type and operating system
- Country-level location (from IP, which is not stored)

Umami **does not use cookies**, does not track users across sites, and does not collect personal information. All data is aggregated and anonymous.

#### Marketing Attribution and Referrals
We want to know which campaigns and partners bring people to AnkiMCP. For that we use two cookies, set only in the cases below:

- **Attribution cookie (`ankimcp_attr`).** If you arrive at ankimcp.ai from an ad, a campaign link, or another website, we set a first-party cookie that records where you came from: campaign tags in the link (such as `utm_source`), an ad click identifier if the link has one, the referring website's domain, and the page you landed on. It lasts up to 180 days. If you sign up, we save the first of these records to your account. If you start a checkout on the web, we pass only the campaign source, medium, and name to our Payment Provider with the order. We do not send this data to advertising platforms, and we don't use it for anything but measuring where our users come from.
- **Referral cookie (Affonso).** While our affiliate program is running, ankimcp.ai and the dashboard load a script from [Affonso](https://affonso.io), our affiliate platform. Loading it lets Affonso receive technical data such as your IP address and browser details. If you arrive through a partner's referral link, the script sets a referral cookie that lasts up to 60 days. If you then start a checkout on the web, we save the referral to your account and pass it to our Payment Provider with the order, so the partner can be credited. Affonso receives the details of the referred purchase (such as your name, email address, amounts, refunds, and cancellations) from our Payment Provider, acting as our data processor. Partners see referred customers anonymously unless we choose otherwise. Purchases in the Android app are never attributed to a partner.

You can block or delete these cookies in your browser at any time; the site works the same without them.

#### Hosting
This website is served through a third-party hosting provider, which may collect technical information such as IP addresses in server logs as part of operating the infrastructure.

#### Community Forum (forum.ankimcp.ai)
We operate a self-hosted [Discourse](https://www.discourse.org) community forum. When you use the forum, we collect:

- **Account information:** email address, username, and display name. Accounts are created through our self-hosted [Keycloak](https://www.keycloak.org) identity provider, which supports Google and GitHub social login as well as email/password registration.
- **Posts and messages:** all content you publish, including topics, replies, and direct messages.
- **Uploaded files:** images and attachments you upload to posts.
- **IP addresses:** logged for security and anti-abuse purposes.
- **Activity data:** page views, read tracking, visit history, and notification preferences.
- **Cookies:** the forum sets `_t` (authentication token) and `_forum_session` (session) cookies, which are required for the forum to function.

All forum data is stored in a self-hosted PostgreSQL database on AnkiMCP infrastructure — no third-party SaaS is involved in data storage. Email notifications from the forum are delivered via a third-party email delivery service.

#### SaaS Cloud Service (AnkiMCP SaaS)

The AnkiMCP SaaS cloud service lets LLM clients (such as ChatGPT and Claude.ai) interact with your Anki — either your local installation via secure tunnels, or a copy of Anki we run for you on our servers (the **Hosted Anki** feature). When you use the SaaS Service, we collect and process the following information.

##### SaaS Account Information

When you create a SaaS account, we collect:

- **Authentication data:** your email address, display name, and Keycloak user ID. If you sign in via Google or GitHub, we also receive your avatar image URL from the social login provider.
- **Account identifiers:** a unique user ID assigned to your account.
- **Authentication method:** which social login provider you used, or that you registered with email/password.
- **Cookies:** when you sign in to the SaaS dashboard (web.ankimcp.ai), it sets httpOnly authentication and session cookies. These are required for sign-in and are not used for tracking.
- **Sign-in records:** our sign-in service records each sign-in attempt (sign-ins, failed sign-ins, registrations, sign-outs, and token exchanges), including the IP address, the time, the app you signed in to, and the result. We use these records for security and to investigate account problems.

SaaS accounts are managed through our self-hosted [Keycloak](https://www.keycloak.org) identity provider, which also handles forum authentication.

##### Tunnel Connection Data

When you connect your AnkiMCP client (the add-on, the CLI, or the Android app) to the SaaS tunnel server, we collect:

- **Connection metadata:** connect and disconnect times, your plan, your account email and ID, and which kind of client connected (the add-on or the Android app). During normal operation our application logs do **not** record the IP addresses of tunnel or MCP connections (see [Service Monitoring](#service-monitoring-opentelemetry) and [Security and Abuse Prevention](#security-and-abuse-prevention) below).
- **Connection state:** whether your client is currently connected, and while it is, the client's type and version, for display on your dashboard and to route LLM requests.

Connection state is short-lived routing data on the tunnel server and is not persisted to a database. Connection metadata appears in service logs, which are retained for up to **14 days**. Our network infrastructure provider (Cloudflare) may process connection metadata, including IP addresses, at the network edge under its own privacy policy.

##### LLM OAuth Data

When an LLM client connects to your tunnel, we process:

- **OAuth client registrations:** LLM clients register via Dynamic Client Registration with our self-hosted Keycloak identity provider. We store the client ID and associated metadata. We do **not** store OAuth access tokens or refresh tokens — those are managed by Keycloak and issued directly to the LLM client.

##### Authless Access

The tunnel is **authenticated by default**. You can optionally enable **Authless access** in your Tunnel Dashboard. When you do:

- We generate a **private URL containing a secret identifier** for your tunnel and store that identifier to route requests to you.
- Requests made through that URL are **not tied to a signed-in client or account**: anyone who knows the URL can access your Anki through your tunnel until you disable authless access or regenerate the URL. Treat the URL like a password and do not share or publish it.
- We process the same connection metadata (such as timestamps) for authless requests as for authenticated ones.

##### Subscription Data

We store:

- **Subscription tier:** your current plan (Free, Plus, or Pro).
- **Tier history:** an audit trail of tier changes (upgrades, downgrades) with timestamps.
- **Expiration date:** when your current subscription period ends (for paid plans).

Payments for paid tiers are handled by our third-party Payment Provider — see the [Terms of Service (Payments section)](/terms/#payments-refunds-and-cancellation) for the current status. Your payment details — card number, billing address, and related checkout information (which may include your IP address, collected for tax-location and fraud-prevention purposes) — are collected and processed by the Payment Provider on its own checkout pages, under its own privacy policy. Card numbers never reach our servers and we do not store them. Where the Payment Provider acts as merchant of record, it is the seller of record for your purchase and an independent controller of the payment data it collects.

{{< payment-provider >}}

Payments were processed by Paddle (merchant of record) until September 1, 2026. Paddle retains the payment data it collected under its own [privacy policy](https://www.paddle.com/legal/privacy).

##### Service Monitoring (OpenTelemetry)

We use [OpenTelemetry](https://opentelemetry.io) to collect service health metrics and request traces. This includes:

- **Performance metrics:** request latency, error rates, and service availability.
- **Request traces:** request paths, HTTP status codes, timing data across services, and the network address each request came from. For MCP requests this is usually your AI provider's server; for requests from the dashboard or the Android app it is your own device.
- **Service identifiers:** your user ID may appear in trace metadata for debugging purposes.

OpenTelemetry data is used exclusively for service reliability and debugging. It does **not** capture the content of your Anki flashcards or LLM conversations.

##### Security and Abuse Prevention

To protect the SaaS Service and its users, our systems monitor for signs of abuse, misuse, and violations of our [Terms of Service](/terms/). When they detect possible abuse, we may record additional technical data about the activity involved, such as IP addresses and request metadata, and use it to investigate, to block the activity, and to enforce our Terms. We don't publish the details of how detection works, because doing so would make it easier to get around.

This data is used only for security and enforcement. It is deleted together with our service logs, within **14 days**, unless we need it for longer for an ongoing investigation or to establish, exercise, or defend legal claims. It never includes the content of your flashcards.

##### Data Transit (Anki Flashcard Data)

This is important to understand: when you use the SaaS tunnel, your Anki flashcard data **passes through** our tunnel server on its way between the LLM client and your local Anki installation (or AnkiDroid on your phone). Here is how we handle it:

- **No persistent storage:** Anki data is relayed in real-time over WebSocket connections. It is temporarily present in server memory during transit but is **never written to disk, logged, or stored in any database**.
- **No inspection or analysis:** we do not read, index, analyze, or use the content of your flashcards or LLM requests/responses.
- **Encryption in transit:** connections between your AnkiMCP client (the add-on, the CLI, or the Android app) and our tunnel server, and between LLM clients and our tunnel server, use TLS encryption.
- **Your data stays yours:** all Anki data remains on your own computer or phone. The tunnel is a pass-through — we are a conduit, not a data controller, with respect to your flashcard content.

##### Hosted Anki Data

Hosted Anki is different from the tunnel. To run a copy of Anki on our servers, we store your Anki data rather than only relaying it. When you use Hosted Anki:

- **Stored collection and media:** your **Anki collection and media files are stored on persistent storage** on AnkiMCP infrastructure. We store this so your hosted instance can run and be reached by your AI (and by you through the remote desktop). We store it only to operate the feature — we do not read, index, analyze, or use its content for any other purpose.
- **Remote desktop sessions:** when you open your hosted Anki through the in-browser remote desktop, the session streams the running desktop to your browser. We may process operational data needed to run and route the session (such as session and connection state, timing, and IP address for the connection), but we do not record the contents of your screen or capture what you type.
- **AnkiWeb password is never stored:** if you sync your hosted instance with AnkiWeb, you enter your AnkiWeb credentials yourself, inside your remote desktop session, directly with AnkiWeb. Your AnkiWeb password is **never stored, transmitted to, or accessible by AnkiMCP.**
- **Retention:** your stored collection and media persist for as long as your hosted instance exists. When you delete the instance (or when it is removed after account deletion), that data is **permanently removed** and cannot be recovered. You are responsible for your own backups — see [Data Retention](#5-data-retention) below.

##### AnkiMCP App for Android (AnkiDroid)

The AnkiMCP app for Android connects AnkiDroid on your phone to the same AnkiMCP account, through a dedicated relay. In addition to the SaaS account data above, when you use the Android app we process:

- **Access to your AnkiDroid collection:** the app reads and edits your decks, notes, cards, tags, and note types through AnkiDroid's official API, using AnkiDroid's own permission, which you grant and can revoke in Android settings. It does this only when your AI client asks. The app never uploads your whole collection; your AI's requests and the app's answers pass through our relay between the app and your AI client (see Data Transit above).
- **Sign-in:** you sign in in your browser, so the app never sees your password. Your access and refresh tokens are stored on the phone, encrypted with a key held by Android's secure keystore. No password is stored.
- **Push token:** when you sign in with **Remote access** on (the default), the app registers its Firebase push token, together with the client type, platform, and app version, with our relay server. We use it only to wake the app when an AI assistant calls it. Push delivery is handled by **Google Firebase**, which uses an installation ID to issue the token and also receives technical data such as the device model, Android version, and library versions, under Google's privacy policy. The app doesn't request a push token until you sign in. The token is removed from our server when you turn Remote access off or sign out (signing out also deletes it with Firebase). A token that Firebase reports as no longer valid is deleted the next time we try to wake the app with it.
- **Google Play purchases:** if you buy a subscription inside the app, the app sends the Google Play purchase token to our server so we can verify the purchase with Google Play and activate your plan. We store the purchase token, your plan, its status, and when the paid period ends. To link a purchase to your account, the app gives Google Play a one-way scrambled form of your account ID, not your email. We keep the purchase notifications Google Play sends us; after 90 days their contents are erased, leaving only a record that each notification arrived and how it was handled. **Google Play is the payment processor** for in-app purchases; your card details are handled by Google and never reach the app or our servers.
- **No analytics or crash reporting:** the app contains no analytics, advertising, or crash-reporting libraries.
- **Logs stay on your phone:** the app keeps a diagnostic log in its private storage, with your email and tokens removed. It leaves the phone only if you tap **Share log**, **Share detailed log**, or **Copy** and choose where to send or paste it. A shared log includes the app version, Android version, and phone model.

The app's data is excluded from Android backups, and uninstalling the app removes it from your phone.

**Local Wi-Fi mode.** The app can also run a local server that a computer on the same Wi-Fi network talks to directly, without an AnkiMCP account. Requests served by the local server never go through AnkiMCP's servers. If you use only local mode and don't sign in, the app sends nothing to our servers. The connection is plain, unencrypted HTTP, and anyone on the same network can reach it unless you turn on **Require access token**.

### 2. Information We Do Not Collect

- **No tracking cookies** are set by the main website (ankimcp.ai) for ordinary visits. The only cookies it sets are the attribution and referral cookies described in [Marketing Attribution and Referrals](#marketing-attribution-and-referrals), and only when you arrive from an ad, a campaign, or a referral link. The community forum (forum.ankimcp.ai) and the SaaS dashboard (web.ankimcp.ai) use cookies for authentication — see the respective sections above.
- **No user accounts** are required on the main website (ankimcp.ai). The community forum and the SaaS cloud service each require separate accounts — see the respective sections above.
- **No personal data** is collected through website analytics.
- **The AnkiMCP software**, when used in local-only mode (without the SaaS tunnel), runs entirely on your machine and **does not send any data** to our servers or any third party. When used with the SaaS tunnel service, flashcard data passes through our servers in transit but is not stored — see [Data Transit](#data-transit-anki-flashcard-data) above. Cloud features you choose to use do store what you put into them: files in your media library are stored there, including audio generated by text-to-speech and the source text kept in that file's description.
- **The AnkiMCP app for Android:** requests served by its local Wi-Fi server go only to the computer on your network, never through our servers. If you use only local mode and don't sign in, the app **sends nothing** to our servers. The app contains no analytics or crash reporting in any mode.
- **No flashcard content** is stored, logged, or analyzed by the SaaS **tunnel**. We do not have access to the contents of your Anki decks when you use the tunnel. (Two features are exceptions, because storage is what they do: the **media library**, which keeps the files you upload or generate, and the optional **Hosted Anki** feature, which runs Anki on our servers and stores your collection and media there — see [Hosted Anki Data](#hosted-anki-data) above.)
- **No AnkiWeb password** is ever collected, stored, transmitted to, or accessible by AnkiMCP. If you sync Hosted Anki with AnkiWeb, you enter your AnkiWeb credentials yourself inside your remote desktop session, directly with AnkiWeb.

### 3. Third-Party Services

We rely on the following third-party services:


| Service | Purpose | Their Privacy Policy |
|---------|---------|---------------------|
| Hosting provider (third-party) | Website hosting | N/A |
| Cloudflare | Network edge for SaaS connections (TLS, DDoS protection) | [Cloudflare Privacy Policy](https://www.cloudflare.com/privacypolicy/) |
| Umami (self-hosted) | Anonymous analytics | [Umami Privacy](https://umami.is/privacy) |
| Affonso (ZASolution, Germany) | Affiliate referral tracking and partner commissions | [Affonso Privacy Policy](https://affonso.io/privacy) |
| Polar Software, Inc. (merchant of record) | Payment processing and checkout (since Sep 2026) | [Polar Privacy Policy](https://polar.sh/legal/privacy-policy) |
| Paddle (until Sep 1, 2026) | Payment processing (historical — retains past payment data) | [Paddle Privacy Policy](https://www.paddle.com/legal/privacy) |
| Google Play | Payment processing for subscriptions bought in the Android app | [Google Privacy Policy](https://policies.google.com/privacy) |
| Google Firebase (Cloud Messaging) | Push notifications that wake the Android app | [Firebase Privacy](https://firebase.google.com/support/privacy) |
| Microsoft Azure (AI Speech) | Speech synthesis — text you submit for audio generation is processed by Microsoft Azure | [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement) |
| Discourse (self-hosted) | Community forum | [Discourse Privacy Policy](https://www.discourse.org/privacy) |
| Keycloak (self-hosted) | Authentication for forum, SaaS accounts, and LLM OAuth | [Keycloak Privacy](https://www.keycloak.org/privacy) |
| Email delivery service (third-party) | Forum email notifications | N/A |
| PostgreSQL (self-hosted) | SaaS user data and subscription storage | N/A (self-hosted, no third-party access) |
| NATS (self-hosted) | Internal event streaming between SaaS services | N/A (self-hosted, no third-party access) |
| OpenTelemetry (self-hosted) | SaaS service health monitoring | N/A (self-hosted, no third-party access) |

**A note on self-hosted infrastructure:** PostgreSQL, NATS, Keycloak, and OpenTelemetry are all hosted on AnkiMCP-controlled infrastructure. Apart from the third-party services listed above — in particular our Payment Provider for payments and Microsoft Azure for speech synthesis — your SaaS data is stored and processed on that infrastructure. When you use text-to-speech, the text you submit is sent to Microsoft Azure to be turned into audio; the generated audio file is then stored in your media library, together with a description that records the text it was made from.

### 4. Your Rights

You have the right to:

- **Request information** about what data we hold about you

Since we use cookieless, anonymous analytics, there is no personal website analytics data to delete or export.

**Forum users** additionally have the right to:

- **Edit or delete** your own posts and direct messages
- **Export your data** via the Discourse profile settings (account data download)
- **Delete your account** via profile settings or by contacting us — this anonymizes your posts (see Data Retention below)
- **Control notifications** — manage email notification preferences in your forum profile

**SaaS users** additionally have the right to:

- **Access your data** — view your account information, connection history, and subscription status through the SaaS dashboard.
- **Delete your account** — delete your SaaS account yourself in the dashboard (**Settings → General → Delete account**), or by emailing [support@ankimcp.ai](mailto:support@ankimcp.ai) from the account's address. Delete any Hosted Anki instance first; account deletion is refused while one exists. Account deletion removes your login, user record, OAuth client registrations, subscription history, and push token, except records we are legally required to retain (for example for tax or accounting purposes). This action is irreversible.
- **Cancel your subscription** — downgrade from a paid tier to the free tier at any time through the dashboard. A subscription bought in the Android app is cancelled in the Google Play Store.
- **Disconnect your client** — disconnect your AnkiMCP add-on, CLI, or Android app from the tunnel at any time, immediately stopping all data transit through our servers. In the Android app, turning **Remote access** off also deletes your push token.
- **Delete Hosted Anki data** — if you use Hosted Anki, delete your hosted instance at any time to permanently remove the collection and media stored for it from our servers.
- **Request data export** — request a copy of all personal data we hold about your SaaS account by contacting [support@ankimcp.ai](mailto:support@ankimcp.ai).

### 5. Data Retention

- **Analytics data** is aggregated and anonymous — no individual user data is stored
- **Attribution and referral cookies** expire in your browser after up to **180 days** (attribution) and **60 days** (referral). Attribution and referral data saved to your account is retained for the lifetime of the account and deleted upon account deletion; copies passed to our Payment Provider with an order are kept with that order under its retention rules
- **Forum posts** are retained for as long as the forum operates. Soft-deleted posts are permanently purged after 30 days.
- **Forum IP addresses** are retained for security and anti-abuse purposes
- **Forum account deletion** anonymizes your posts (author replaced with a generic label) but does not remove the post content, as other users may have relied on or replied to it
- **SaaS account data** (email, name, avatar, Keycloak ID) is retained for the lifetime of your account and deleted upon account deletion
- **Service logs** are retained for up to **14 days** and then automatically purged. They don't record the IP addresses of normal tunnel and MCP traffic
- **Sign-in records** (including IP addresses) are deleted after **30 days**; copies in our daily backups are kept up to 7 days longer
- **Security and abuse data** is deleted with the service logs within **14 days**, unless needed for longer for an ongoing investigation or a legal claim (see [Security and Abuse Prevention](#security-and-abuse-prevention))
- **OAuth client registrations** are retained while your account is active. They are deleted when you delete your account
- **Android push tokens** are retained while remote access is on in the Android app. They are deleted when you turn remote access off, sign out, or delete your account. A token that Firebase reports as no longer valid is deleted the next time we try to use it
- **Google Play purchase records** (purchase token, plan, status, and period end) are retained for the lifetime of your account and deleted upon account deletion, except records we are legally required to retain
- **Subscription history and usage statistics** (tier changes, monthly request counts, timestamps) are retained for the lifetime of your account for audit purposes and deleted upon account deletion, except records we are legally required to retain (for example for tax or accounting purposes), which are kept for the statutory period and then deleted
- **Diagnostic traces** (including the network address each request came from) are retained for up to **14 days** and **performance metrics** for up to **7 days**, then automatically purged. This data does not contain flashcard content
- **Google Play purchase notifications** have their contents erased after **90 days**; the remaining record that each one arrived is deleted upon account deletion
- **In-memory tunnel state** (active connection data) exists only while your client is connected and is lost when the connection ends or the server restarts
- **Media library files** (uploaded files and generated audio, including the source text stored in a file's description) are retained until you delete them and are **permanently deleted upon account deletion**
- **Hosted Anki data** (your stored collection and media) is retained for as long as the hosted instance exists and is **permanently deleted** when you delete the instance or when it is removed following account deletion. Superseded backup versions are automatically removed within **7 days**. Deletion is irreversible, so you are responsible for maintaining your own backups (for example, via AnkiWeb sync or by exporting your collection)

### 6. Children's Privacy

This website and software are not directed at children under 13. We do not knowingly collect personal information from children.

### 7. Changes to This Policy

We may update this Privacy Policy from time to time. Changes will be posted on this page with an updated effective date.

### 8. Contact

For privacy-related questions or requests, contact us at [support@ankimcp.ai](mailto:support@ankimcp.ai).
