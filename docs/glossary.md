# Glossary

One meaning per term. Use these words in code, documents, issues and messages. Agreed with the owner on 27 November
2026; the table format, with a "Not to be confused with" column, is learned from
[hypomnema's glossary](https://github.com/kl3inIT/hypomnema/blob/main/docs/glossary.md).

## Data

| Term | Meaning | Not to be confused with | From |
| --- | --- | --- | --- |
| **Topic** | One subject the owner researches, such as "homestays in Tam Đảo". A topic has one Graph that grows: later Runs add to it, edit it and remove from it | Session, a word kept out of NicheGraph because it already means a browser login or a chat | owner, 2026-11-23; GraphRAG incremental indexing |
| **Run** | One round of research on a Topic: a question typed in the Web app, Tools fetch Posts, the model groups them, and the Graph is changed | The Topic, which has many Runs | hypomnema's Run; GraphRAG incremental indexing |
| **Graph** | The Entities, Relationships and Claims of one Topic | A view of it (network, orbit, clusters), which is a way of drawing the same Graph | owner, 2026-11-23 |
| **Source** | A platform Posts are read from: Reddit first, then Facebook | A Post | [vision](vision.md) |
| **Post** | A post or a comment fetched from a Source, with its Author, text, link and date. A comment is a Post with a parent Post | A Claim: a Post is what was written, a Claim is the point taken from it | GraphRAG `Document`; [vision](vision.md) |
| **Author** | The account that wrote a Post. People are counted by Author, because one person can write several Posts | The owner of NicheGraph | [vision](vision.md): "how many people said each point" |
| **Entity** | A thing people talk about and a node in the Graph: a homestay, a place, a bus route. It has a type, which gives it a colour and an icon ([vision](vision.md)) | A Post | GraphRAG `Entity`; bl00d.money |
| **Relationship** | A link between two Entities, such as a homestay lying in Tam Đảo, with the Posts it was taken from | A Claim | GraphRAG `Relationship`; bl00d.money ties every fact to a source |
| **Claim** | A point people make about one Entity, such as "clean rooms", with the Posts that make it and the number of Authors. A Claim is a node in the Graph, linked to its Entity | A Relationship, which links two Entities rather than carrying an opinion | GraphRAG claim (`Covariate`); [vision](vision.md); node in the Graph: owner, 2026-11-27 |
| **Ad flag** | A mark on a Post that looks like advertising (a phone number, "inbox me"). The link from a Claim to its Entity is dashed when every Post behind the Claim is flagged, solid otherwise | | [vision](vision.md); solid and dashed lines of bl00d.money |

## System

| Term | Meaning | Not to be confused with | From |
| --- | --- | --- | --- |
| **Web app** | Where the owner types a question and looks at the Graph in 3D | | owner, 2026-11-23 |
| **Tool** | Code that does fixed work without a model: driving the browser, fetching Posts, filtering comments | A Skill | hypomnema's CLI and skill decision |
| **Skill** | A document that teaches the model the method: which Vietnamese phrasings to search, how to group points, how to flag advertising | A Tool | hypomnema's Skill |
| **Runtime** | How the model is reached: an agent CLI (Claude Code, Codex) using the subscription logged in on the machine, or an API key | The model itself, which one Runtime or another can reach | hypomnema's Runtime |
