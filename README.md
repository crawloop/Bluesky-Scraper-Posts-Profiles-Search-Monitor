# Bluesky Scraper — Posts, Profiles, Search & Monitor

[![Run on Apify](https://apify.com/actor-badge?actor=crawloop/bluesky-scraper)](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)
[![Apify Store](https://img.shields.io/badge/Apify-Bluesky%20Scraper-brightgreen?logo=apify)](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)
[![Crawloop](https://img.shields.io/badge/Crawloop-Social%20data-0A66C2)](https://apify.com/crawloop?fpr=guboir)

**Scrape Bluesky** — posts, profiles, keyword/hashtag search, reply threads, followers, likes, reposts, and custom feeds — into clean JSON on [Apify](https://apify.com/?fpr=guboir).

Built on the open **AT Protocol** public AppView API: no browser, no Cloudflare fight, and **no login for public data** (including post search). **Monitor mode** keeps watermarks across runs and returns only new posts — ideal for brand listening and scheduled tracking.

### Run the Actor

**→ [Bluesky Scraper on Apify Store](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)**

Free Apify account: [sign up](https://apify.com/?fpr=guboir) · All Crawloop actors: [apify.com/crawloop](https://apify.com/crawloop?fpr=guboir)

---

> **Disclaimer:** Unofficial tool for publicly accessible Bluesky / AT Protocol AppView data. Not affiliated with, sponsored by, or endorsed by Bluesky PBC. Trademarks belong to their respective owners. Provided for informational and research use only; you must comply with applicable laws and platform terms.

---

## Social & discovery suite

| Bluesky | Product Hunt |
| :--- | :--- |
| **[Bluesky Scraper](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)** ◄── this repo | [Product Hunt Scraper](https://apify.com/crawloop/producthunt-scraper?fpr=guboir) |
| Posts, profiles, search, threads, graph, monitor | Launches, reviews, comments, leaderboards |

---

## What you get

| Use case | Output |
| :--- | :--- |
| **Brand / hashtag listening** | Matching posts with text, engagement, media, facets |
| **Author feed export** | Posts (optional replies & reposts) for one or many handles |
| **Profile enrichment** | Bio, avatar, banner, followers / follows / posts counts |
| **Social graph** | Followers or following lists with profile fields |
| **Conversation research** | Flattened reply trees with depth |
| **Scheduled monitoring** | Only posts newer than the last run (KV watermarks) |

---

## Key features

- **AT Protocol XRPC** — fast async `httpx` client against public AppView endpoints
- **Dual-host search** — post search without Bluesky app password
- **11 modes** — user posts, profiles, search, search users, threads, followers, following, custom feed, likes, reposts, **monitor**
- **Incremental monitor** — named Apify KV store watermarks; optional baseline-only first run
- **Batch hydration** — `getProfiles` / `getPosts` (up to 25)
- **RateGate** — client RPS budget + 429 backoff; proxy optional
- **Flat dataset rows** — `type`: `post` | `profile` | `follower` | `following` | `like` | `repost`

---

## Quick start

1. Create a free [Apify account](https://apify.com/?fpr=guboir).
2. Open **[Bluesky Scraper](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)**.
3. Pick a mode, set handles or queries, set `maxItems`, run.
4. Export Dataset as JSON / CSV / Excel.

### Example — author feeds

```json
{
  "mode": "user_posts",
  "handles": ["jay.bsky.team", "bsky.app"],
  "maxItems": 100,
  "concurrency": 8,
  "maxRequestsPerSecond": 10,
  "includeReplies": true,
  "includeReposts": true,
  "proxyConfiguration": {
    "useApifyProxy": false
  }
}
```

### Example — hashtag / keyword search

```json
{
  "mode": "search",
  "searchQuery": "#ai",
  "searchSort": "latest",
  "maxItems": 200
}
```

### Example — monitor (schedule after baseline)

```json
{
  "mode": "monitor",
  "monitorSource": "search",
  "searchQueries": ["#ai", "bluesky"],
  "monitorStoreName": "bluesky-monitor-brand-x",
  "monitorBaselineOnly": true,
  "maxItems": 200,
  "maxRequestsPerSecond": 10
}
```

After the baseline run, set `monitorBaselineOnly` to `false` (or omit it) so later runs push only new posts.

Run on Apify: [crawloop/bluesky-scraper](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)

---

## Example output

```json
{
  "type": "post",
  "id": "at://did:plc:oky5czdrnfjpqslsw2a5iclo/app.bsky.feed.post/3mrdkahh4xk2r",
  "url": "https://bsky.app/profile/jay.bsky.team/post/3mrdkahh4xk2r",
  "text": "Example post text",
  "authorHandle": "jay.bsky.team",
  "authorDid": "did:plc:oky5czdrnfjpqslsw2a5iclo",
  "likeCount": 42,
  "repostCount": 3,
  "replyCount": 5,
  "hashtags": [],
  "media": [],
  "monitorTarget": "#ai",
  "monitorSource": "search"
}
```

Full docs and live console: **[Apify Store page](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)**

---

## Modes at a glance

| Mode | What it scrapes |
| :--- | :--- |
| `user_posts` | Author feed for handles / DIDs |
| `user_profiles` | Profile metadata |
| `search` | Posts by keyword / hashtag |
| `search_users` | User discovery |
| `post_threads` | Reply trees |
| `followers` / `following` | Social graph |
| `custom_feed` | Feed generator AT-URI / URL |
| `likes` / `reposts` | Engagement lists for posts |
| `monitor` | Incremental new posts only |

---

## API / automation

Trigger runs via the [Apify API](https://docs.apify.com/api/v2), Schedules, or webhooks. More: [Apify API docs](https://docs.apify.com/api/v2) · [Actor page](https://apify.com/crawloop/bluesky-scraper?fpr=guboir)

---

## Pricing

Pay-per-event on Apify (**$1.00 / 1,000** scraped items). Exact pricing is shown on the [Actor page](https://apify.com/crawloop/bluesky-scraper?fpr=guboir) before you run.

---

## Related Actors

| Actor | Role |
| :--- | :--- |
| [Bluesky Scraper](https://apify.com/crawloop/bluesky-scraper?fpr=guboir) | Bluesky / AT Protocol public data |
| [Product Hunt Scraper](https://apify.com/crawloop/producthunt-scraper?fpr=guboir) | Product launches, reviews, comments |
| [Crawloop on Apify](https://apify.com/crawloop?fpr=guboir) | Full actor portfolio |

---

## Links

| Link | Description |
| :--- | :--- |
| [Run Bluesky Scraper](https://apify.com/crawloop/bluesky-scraper?fpr=guboir) | Live Actor on Apify Store |
| [Product Hunt Scraper](https://apify.com/crawloop/producthunt-scraper?fpr=guboir) | Sibling Actor |
| [Crawloop Store](https://apify.com/crawloop?fpr=guboir) | All Crawloop Actors |
| [Sign up for Apify](https://apify.com/?fpr=guboir) | Free account |

Questions or custom enterprise runs: open an issue here or contact via the [Apify Store](https://apify.com/crawloop/bluesky-scraper?fpr=guboir) page.
