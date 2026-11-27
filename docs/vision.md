# Vision

This file states intent, not fact. What exists is in [ARCHITECTURE.md](../ARCHITECTURE.md).

## The problem

Practical questions, such as which bus to take, which homestay is cheap and liked, or which shop overcharges, are
answered best by ordinary people in small places: Threads replies, Facebook groups, TikTok comments, Reddit. A web
search returns booking sites and paid articles instead, and the small places need a login, scrolling and time to read.
On 18 November 2026 a search for a homestay in Tam Đảo showed both: the search engine returned listings and
promotional posts, and Threads search asked for a login before showing anything
([research](research/2026-11-18-existing-tools.md)).

## The outcome

A person types one question and gets back, from several of those places at once:

- what people said, grouped by point, with how many people said each point;
- a link and a date for every post the answer rests on;
- a mark on posts that look like advertising (a phone number, "inbox me").

Answers are opinions, not verified facts. People disagree, and the tool shows the disagreement instead of hiding it.

Once searching works well, the collected posts may also be shown as a graph: who said what about which place
(owner, 2026-11-18).

## Principles

- Vietnamese sources and Vietnamese questions first; no tool found so far covers them
  ([research](research/2026-11-18-existing-tools.md)).
- Free and open source. It runs on the user's own machine with the user's own accounts and keys; there is no hosted
  service to pay for.
- Every claim in an answer links to its post.

## Direction agreed with the owner

Agreed in conversation on 18 November 2026, before any research or code. Each point becomes an ADR once its
implementation starts, and may change if research shows it is wrong.

- **Shape: a CLI and a skill.** A Go command line program fetches posts and prints them as JSON (author, text, link,
  date, comments). A skill teaches an agent (Claude Code, Codex) the method: which Vietnamese phrasings to search,
  which sources, how to group points, count people and mark advertising. The agent is the model, paid by the user's
  own subscription. Learned from hypomnema's
  [CLI and skill](https://github.com/kl3inIT/hypomnema/blob/main/docs/decisions/2026-11-09-coordinator-cli-and-skill.md)
  and [one tool for every agent](https://github.com/kl3inIT/hypomnema/blob/main/docs/decisions/2026-11-15-one-tool-for-every-agent.md)
  decisions: a tool is code the agent calls, a skill is a document on method. A web page may come later and reuse the
  same fetching code.
- **Reading sources: a browser, not official APIs.** The CLI drives a browser profile the user has logged in to,
  because Threads search shows nothing without an account. It therefore runs on the user's machine.
- **Video sources, in tiers.** The first version reads a video's description, comments and existing captions.
  Speech to text and text on screen come later as options, because they need `ffmpeg` and Whisper installed.

Agreed on 23 November 2026, changing the shape above:

- **A web app on top of the CLI and the skill.** The question is typed in the web app. The core stays a CLI, tools and
  a skill: tools do the fixed work (driving the browser, fetching posts, filtering comments) without a model, and a
  model only groups and analyses what was fetched. The model is reached through an agent, an API key or the
  subscription already logged in on the machine (owner, 2026-11-23).
- **One topic, one growing graph.** Each topic has its own graph. Later research on the same topic adds to it, or
  edits and removes from it, instead of starting over (owner, 2026-11-23).
- **The look of bl00d.money.** Results are shown as a graph in the style of [bl00d.money](https://bl00d.money)
  ([research](research/2026-11-23-graph-ui-references.md)) (owner, 2026-11-23).
- **Sources in order:** Reddit first, then Facebook; video platforms (TikTok, YouTube) after those (owner, 2026-11-23).
- **A 3D graph drawn with [3d-force-graph](https://github.com/vasturiano/3d-force-graph).** Chosen over 2D by the
  owner; the library's `graphData()` adds nodes to a running graph, which fits a topic that grows
  ([research](research/2026-11-23-graph-ui-references.md)) (owner, 2026-11-23).
- **Interface drafts in Figma, through [Figwright](https://github.com/awdr74100/figwright).** Motion and the 3D graph,
  which Figma cannot show, are drafted as HTML instead (owner, 2026-11-23).
- **The words for the parts of the system** are in the [glossary](glossary.md) (owner, 2026-11-27).

## Open questions

Each is decided with the owner, one at a time, and recorded in an issue.

1. Which Go library drives the browser, and whether Reddit needs a browser at all.
