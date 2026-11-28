# Reading Reddit

Date: 28 November 2026. Requests sent from the owner's machine; Reddit's own policy pages read through the Help Center
API (`support.reddithelp.com/api/v2/help_center/en-us/articles/<id>.json`) and Devvit's documentation.

## What Reddit announced in 2026

From Reddit's Help Center changelogs of
[8 October](https://support.reddithelp.com/hc/en-us/articles/54353370049684) and
[10 November 2026](https://support.reddithelp.com/hc/en-us/articles/55472297340308):

- "public Data API apps and bots are moving to Reddit's Developer Platform as part of efforts to reduce scraping and
  automated abuse".
- "October 31, 2026: New requests for public API access will no longer be accepted."
- "January 12, 2027: API access removal begins for apps and users that haven't registered or responded to Reddit's
  outreach." "March 2027: Remaining public API access ends."
- RSS feed support ended on 13 November 2026: "If you use RSS for feeds outside of a community you moderate, there is
  no replacement."
- "In November we'll be starting to test a logged-in only experience on Reddit in select markets."

The Data API is therefore closed to a new project such as NicheGraph, whatever the use.

## Without logging in

| Request | Result |
| --- | --- |
| `www.reddit.com/search.json`, `/r/VietNam/about.json`, `/r/VietNam/new.json` | HTTP 403, "blocked by network security" |
| `api.reddit.com/r/VietNam/new`, `oauth.reddit.com/r/VietNam/new` | HTTP 403, same page |
| `old.reddit.com/r/VietNam/about.json` | HTTP 302 to the login page |
| `www.reddit.com/r/VietNam/.rss` | HTTP 404 |
| `www.reddit.com/r/VietNam/search.rss?q=...` | HTTP 429 |
| `www.reddit.com/r/VietNam/` with a browser User-Agent | HTTP 200, but the page is a JavaScript proof-of-work challenge, no posts |
| `www.reddit.com/robots.txt` | `User-agent: *` / `Disallow: /` |
| `www.reddit.com/oembed?url=<post>` | HTTP 200, embed HTML of one post (no comments) |
| Reddit search in a browser driven by chrome-devtools | "You've been blocked by network security" |

## Reddit's rules

- [User Agreement](https://redditinc.com/policies/user-agreement) (effective 1 July 2026): users may not "Access,
  search, or collect data from the Services by any means (automated or otherwise) except as permitted in these Terms
  or in a separate agreement with Reddit (...scraping the Services without Reddit's prior written consent is
  prohibited)".
- [Responsible Builder Policy](https://support.reddithelp.com/hc/en-us/articles/42728983564564) (updated 27 November
  2026): approval before any API access; apps "including bots, AI agents, or non-human operated accounts" must register
  and carry an App label; no "commercial and non-commercial mining, scraping" without written approval. Enforcement
  includes "Suspending your app or account" and "associated accounts".
- [Developer Platform & Accessing Reddit Data](https://support.reddithelp.com/hc/en-us/articles/14945211791892):
  research is allowed only through Reddit for Researchers; "Using developer tools, APIs, or unauthorized third-party
  tools for academic research is a violation of our policies."
- [Data API Wiki](https://support.reddithelp.com/hc/en-us/articles/16160319875092): content deleted on Reddit must be
  deleted by the holder; Reddit recommends deleting stored user data within 48 hours.

## Routes

| Route | Works today | Allowed by Reddit | Notes |
| --- | --- | --- | --- |
| Data API (OAuth) | no, for new apps | yes, but closed | intake closed 31 Oct 2026; all public access ends March 2027 |
| Reddit for Researchers | needs application | yes, for research | [requires](https://support.reddithelp.com/hc/en-us/articles/49381918834964) a university affiliation, ethics approval, a sponsor; access for one year; no redistribution |
| Devvit app | yes | yes | can search all of Reddit (`reddit.searchPosts`, [docs](https://developers.reddit.com/docs/capabilities/server/reddit-api)); runs on Reddit's servers; [HTTP Fetch](https://developers.reddit.com/docs/capabilities/http-fetch) to personal domains "Will not be approved", AI limited to OpenAI and Gemini; results stay inside Reddit |
| Logged-in browser of the user | yes | no | breaks the User Agreement clause above; the account can be suspended |
| Arctic Shift API | yes | not by Reddit | see below |
| PullPush API | no | not by Reddit | answered "This website does not provide free scraping resources for agents" |
| Paid scraping services (Apify, Bright Data, ScrapeCreators) | per vendor claims | no | vendor blogs quote about 1-4 USD per 1,000 results; Reddit sued SerpApi, Oxylabs, AWMProxy and Perplexity for scraping in October 2025 ([Search Engine Land](https://searchengineland.com/reddit-sues-perplexity-serpapi-scraping-google-463681)) |
| Redlib (private Reddit front end) | only forks, with a logged-in session cookie | no | upstream blocked; [issue 609](https://github.com/redlib-org/redlib/issues/609) |
| Search engine APIs (`site:reddit.com`) | partly | n/a | give links and snippets only; Google Custom Search JSON API is closed to new customers and ends 1 January 2027; Brave Search API is paid |

## Arctic Shift

[Arctic Shift](https://github.com/ArthurHeitmann/arctic_shift) is a free archive run by one person: "All data is
retrieved through the official reddit API." It has an [API](https://github.com/ArthurHeitmann/arctic_shift/tree/master/api)
with no account and no key. Tried on this date:

- The newest r/VietNam post it returned was created at 05:49 UTC the same morning.
- Keyword search works within one subreddit or one author (`subreddit=VietNam&title=Tam Đảo` returned "Tam Đảo illegal
  racing", 15 comments, and two promotional posts with addresses and phone numbers).
- `comments/tree?link_id=t3_<id>` returns a post's comments with author and score.
- About half of the searches answered "Timeout. Maybe slow down a bit"; the README states there are no guarantees and
  rate limits depend on server load.
- It re-reads content after 36 hours and can restore deleted text (`_meta.was_initially_deleted`), which Reddit's rules
  say a holder must not keep.

Inferred, not checked: Arctic Shift collects through the Data API, so it may stop when public API access ends in March
2027.

## Vietnamese content

A Google search for `site:reddit.com "Tam Đảo"` gave about 1,490 results. Most of the first ten are English posts from
r/VietNam and r/hanoi shown with Reddit's machine translation (`?tl=vi`); posts written in Vietnamese come from
r/vozforums and r/VietNam.

## Legal background (United States, from press coverage)

- Meta v. Bright Data (January 2024): Meta's terms "do not apply to and prohibit Bright Data's scraping of publicly
  available data while logged off" ([TechCrunch](https://techcrunch.com/2024/01/24/court-rules-in-favor-of-a-web-scraper-bright-data-which-meta-had-used-and-then-sued)).
  A logged-in user has accepted the terms, so the reasoning does not cover a logged-in browser.
- X Corp v. Bright Data (May 2024): dismissed ([CNBC](https://www.cnbc.com/2024/05/10/elon-musks-x-loses-lawsuit-against-bright-data-over-data-scraping.html)).
