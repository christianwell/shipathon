<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the Shipathon SvelteKit landing page. The following changes were made:

- **`src/hooks.client.ts`** (new) — Initializes PostHog on the client via the `/ingest` reverse proxy. Also captures client-side exceptions automatically via `handleError`.
- **`src/hooks.server.ts`** (new) — Reverse proxy that routes `/ingest` requests to PostHog's EU servers, allowing analytics to bypass ad blockers.
- **`src/routes/+page.svelte`** (edited) — Added `posthog-js` import and five `posthog.capture()` calls for user actions on the landing page.
- **`svelte.config.js`** (edited) — Added `paths.relative: false`, required for PostHog session replay to work correctly with SSR.
- **`.env`** (created) — `PUBLIC_POSTHOG_PROJECT_TOKEN` and `PUBLIC_POSTHOG_HOST` added.

| Event | Description | File |
|---|---|---|
| `rsvp_clicked` | User clicks the RSVP button — primary conversion event | `src/routes/+page.svelte` |
| `faq_item_opened` | User expands a FAQ item (includes `question` and `index` properties) | `src/routes/+page.svelte` |
| `subathon_popup_opened` | User opens the "What's a subathon?" popup (`source: 'hero'`) | `src/routes/+page.svelte` |
| `faq_section_viewed` | FAQ section scrolls into view for the first time | `src/routes/+page.svelte` |
| `hackclub_tv_link_clicked` | User clicks the hackclub.tv link (`source: 'hero'`) | `src/routes/+page.svelte` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics:** https://eu.posthog.com/project/146500/dashboard/584235
- **RSVP Clicks Over Time:** https://eu.posthog.com/project/146500/insights/XAfCiLjO
- **FAQ Engagement: Views vs Opens:** https://eu.posthog.com/project/146500/insights/gGRcTc5l
- **Landing Page Conversion Funnel:** https://eu.posthog.com/project/146500/insights/qvpKR7Ws
- **Visitor Interest Signals:** https://eu.posthog.com/project/146500/insights/qZeQp2ZV
- **Most Opened FAQ Questions:** https://eu.posthog.com/project/146500/insights/EM06XP6k

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
