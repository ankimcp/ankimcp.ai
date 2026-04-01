---
title: "Privacy Policy"
description: "Privacy Policy for ankimcp.ai and the Anki MCP open-source project."
sitemap_priority: 0.3
---

## Privacy Policy

**Effective Date:** April 1, 2026

This Privacy Policy describes how ankimcp.ai ("Website") and the Anki MCP software ("Software") handle your information.

### 1. Information We Collect

#### Website Analytics
We use [Umami](https://umami.is), a privacy-focused, self-hosted analytics platform. Umami collects:

- Page views and referrer URLs
- Browser type and operating system
- Country-level location (from IP, which is not stored)

Umami **does not use cookies**, does not track users across sites, and does not collect personal information. All data is aggregated and anonymous.

#### Newsletter
If you subscribe to our newsletter via [MailerLite](https://www.mailerlite.com), we collect your **email address**. MailerLite acts as our data processor and stores your email on their servers. You can unsubscribe at any time using the link in every email.

#### Hosting
This website is hosted on [GitHub Pages](https://pages.github.com). GitHub may collect technical information such as IP addresses in server logs according to their own [Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).

#### Community Forum (forum.ankimcp.ai)
We operate a self-hosted [Discourse](https://www.discourse.org) community forum. When you use the forum, we collect:

- **Account information:** email address, username, and display name. Accounts are created through our self-hosted [Keycloak](https://www.keycloak.org) identity provider, which supports Google and GitHub social login as well as email/password registration.
- **Posts and messages:** all content you publish, including topics, replies, and direct messages.
- **Uploaded files:** images and attachments you upload to posts.
- **IP addresses:** logged for security and anti-abuse purposes.
- **Activity data:** page views, read tracking, visit history, and notification preferences.
- **Cookies:** the forum sets `_t` (authentication token) and `_forum_session` (session) cookies, which are required for the forum to function.

All forum data is stored in a self-hosted PostgreSQL database on AnkiMCP infrastructure — no third-party SaaS is involved in data storage. Email notifications from the forum are delivered via [SMTP2GO](https://www.smtp2go.com), a third-party email delivery service.

### 2. Information We Do Not Collect

- **No cookies** are set by the main website (ankimcp.ai). The community forum (forum.ankimcp.ai) does use cookies for authentication — see the [Community Forum](#community-forum-forumankimcpai) section above.
- **No user accounts** exist on the main website. The community forum requires an account to participate — see above.
- **No personal data** is collected through website analytics
- **The Anki MCP software** runs entirely on your local machine and **does not send any data** to our servers or any third party. All communication happens locally between your AI assistant and your Anki installation.

### 3. Third-Party Services

We rely on the following third-party services:

| Service | Purpose | Their Privacy Policy |
|---------|---------|---------------------|
| GitHub Pages | Website hosting | [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) |
| Umami (self-hosted) | Anonymous analytics | [Umami Privacy](https://umami.is/privacy) |
| MailerLite | Newsletter delivery | [MailerLite Privacy Policy](https://www.mailerlite.com/legal/privacy-policy) |
| Discourse (self-hosted) | Community forum | [Discourse Privacy Policy](https://www.discourse.org/privacy) |
| Keycloak (self-hosted) | Forum authentication (SSO) | [Keycloak Privacy](https://www.keycloak.org/privacy) |
| SMTP2GO | Forum email notifications | [SMTP2GO Privacy Policy](https://www.smtp2go.com/privacy) |

### 4. Your Rights

You have the right to:

- **Unsubscribe** from the newsletter at any time via the unsubscribe link in emails
- **Request deletion** of your email from our newsletter list
- **Request information** about what data we hold about you

Since we use cookieless, anonymous analytics, there is no personal website analytics data to delete or export.

**Forum users** additionally have the right to:

- **Edit or delete** your own posts and direct messages
- **Export your data** via the Discourse profile settings (account data download)
- **Delete your account** via profile settings or by contacting us — this anonymizes your posts (see Data Retention below)
- **Control notifications** — manage email notification preferences in your forum profile

### 5. Data Retention

- **Newsletter emails** are retained until you unsubscribe or request deletion
- **Analytics data** is aggregated and anonymous — no individual user data is stored
- **Forum posts** are retained for as long as the forum operates. Soft-deleted posts are permanently purged after 30 days.
- **Forum IP addresses** are retained for security and anti-abuse purposes
- **Forum account deletion** anonymizes your posts (author replaced with a generic label) but does not remove the post content, as other users may have relied on or replied to it

### 6. Children's Privacy

This website and software are not directed at children under 13. We do not knowingly collect personal information from children.

### 7. Changes to This Policy

We may update this Privacy Policy from time to time. Changes will be posted on this page with an updated effective date.

### 8. Contact

For privacy-related questions or requests, contact us at [support@ankimcp.ai](mailto:support@ankimcp.ai).
