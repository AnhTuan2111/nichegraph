# Existing tools and the first search by hand

Date: 18 November 2026. Sources are web pages found by search; vendor pages were not tested and their claims are
marketing copy.

## The search by hand

The question was a cheap, well-liked homestay in Tam Đảo for one night.

- A web search for the question returned booking sites (Booking.com mirrors, Trip.com), listicles (mia.vn, MoMo blog)
  and posts by the homestays themselves on TikTok and Facebook. No independent review thread came up.
- `site:threads.com` search found individual Threads posts, mostly promotional, and none of their replies.
- Opening `https://www.threads.com/search?q=...` in a browser without a session redirected to an Instagram login page.
  Threads search shows nothing without an account.

## Tools that already do part of this

| Tool | Sources | Aimed at | Source |
| --- | --- | --- | --- |
| Reddinbox | Reddit, X, Bluesky, Hacker News, Facebook | audience research, with links to threads | [reddinbox.com](https://reddinbox.com/), [Facebook search](https://reddinbox.com/facebook-ai-search) |
| BuzzSearch | Reddit, TikTok with comments; mentions Facebook, YouTube | ecommerce and ad angles | [buzzsearch.ai](https://buzzsearch.ai/) |
| Adlicio | Reddit, TikTok and 30+ sources | marketing copy | [comparison](https://tryadlicio.com/blog/best-reddit-research-tools) |
| GummySearch | Reddit only | paid, from $49 a month per the comparison above | same comparison |
| Tavily social media agent | TikTok, Reddit, Instagram, X, Facebook, LinkedIn | an example agent in Tavily's docs | [docs](https://docs.tavily.com/examples/agent-toolkit/social-media-research) |
| Reddit AI search | Reddit | built into Reddit search since 26 May 2026 | [article](https://everything-pr.com/social-ai-search-engines) |
| Meta Forum | Facebook Groups | iOS app, US App Store, 22 May 2026 | same article |

## Gaps

- No tool found covers Threads.
- No tool found is aimed at Vietnamese sources: Vietnamese Facebook groups, Vietnamese Threads, Vietnamese TikTok.
- The tools above are paid services aimed at marketers, not people asking a practical question.

## Not yet studied

- Whether the official Threads API offers keyword search of public posts, and on what terms.
- Open-source scrapers and browser-automation projects for Threads, Facebook groups and TikTok, read in their code.
- Go libraries for driving a browser: `chromedp`, `go-rod`, `playwright-go`.
- Reading video sources (TikTok, YouTube): captions through `yt-dlp`, speech to text with Whisper (`whisper.cpp`),
  frames and audio cut with `ffmpeg`, and how well each handles Vietnamese.
- The browser work in [hypomnema](https://github.com/kl3inIT/hypomnema): `docs/research/2026-11-12-embedded-browser.md`
  and `deploy/browser/`.
