# Graph interface references: bl00d.money, graph libraries, sci-fi UI kits

Date: 23 November 2026. The owner sent a screen recording of bl00d.money as the look wanted for showing research
results. The site was opened in a browser on this date; library figures come from the GitHub API on the same date.

## bl00d.money, read in the browser

What the page is built with, read from the loaded page: `d3.min.js`, one 2D `<canvas>` for the graph, two small SVGs,
the fonts Hanken Grotesk and IBM Plex Mono. No WebGL and no 3D.

Layout of the map screen:

- Top bar: name, a search box (`/` focuses it), and four pages: Map, Index, About, Submit.
- Left column: "Case files", fourteen stories that each pull one subset out of the database, and "Highlight a type",
  the node types with their counts (Companies 36, People 121, Countries 54, and so on).
- Centre: the graph on a black background. Every node is a record coloured by type; lines are coloured by what
  connects them. Toggles for names (off, key, all) and zoom buttons sit at the edges.
- Right column, nothing selected: title, question, totals (294 entities, 609 facts, 384 sources), a money breakdown,
  a legend in prose and "most connected" entities.
- Bottom: view switcher, Network, Orbit, Clusters, Flow, Holdings and Timeline (Timeline disabled, "next round").

Behaviour:

- Clicking an entity changes the URL to `#<entity-slug>` and switches to Orbit: the entity in the centre, its
  neighbours around it, each line labelled with the relation and a figure ("PROCURES FROM $400M").
- The right column becomes the entity's file: type and ID, headline figures, role, country, link counts, a profile,
  then every relationship as a row with direction, relation, date, one sentence and a mark.
- The mark is `●` "confirmed by primary source" or `○` "media / data provider only"; on the graph the first is a solid
  line and the second dashed. The About page says every fact is tied to at least one document, and reported facts
  "stay visibly marked until a primary record is found".
- Clusters groups nodes by type into separate clouds, with cross-type lines between them.
- Index is a plain table of all 294 records: type, name, ID, country, largest value, links, sorted by links; a row
  opens the entity on the map.

## Graph rendering libraries

| Library | Stars | Last push | Licence | Renders |
| --- | --- | --- | --- | --- |
| [d3-force](https://github.com/d3/d3-force) | 2014 | 2026-11-21 | ISC | layout only; bl00d.money draws it on canvas itself |
| [force-graph](https://github.com/vasturiano/force-graph) | 2173 | 2026-09-28 | MIT | 2D canvas |
| [3d-force-graph](https://github.com/vasturiano/3d-force-graph) | 6589 | 2026-11-05 | MIT | 3D, Three.js/WebGL |
| [react-force-graph](https://github.com/vasturiano/react-force-graph) | 3374 | 2026-09-29 | MIT | React wrapper for both, plus VR/AR |
| [sigma.js](https://github.com/jacomyal/sigma.js) | 12246 | 2026-11-10 | MIT | 2D WebGL, thousands of nodes; data in [graphology](https://github.com/graphology/graphology) |
| [cosmos](https://github.com/cosmosgl/graph) | 1309 | 2026-11-23 | MIT | 2D, layout and rendering on the GPU |
| [reagraph](https://github.com/reaviz/reagraph) | 1100 | 2026-06-25 | Apache-2.0 | 2D and 3D WebGL for React |
| [G6](https://github.com/antvis/G6) | 12400 | 2026-11-23 | MIT | 2D and 3D, many layouts |
| [Cytoscape.js](https://github.com/cytoscape/cytoscape.js) | 11302 | 2026-11-10 | MIT | 2D, graph analysis included |

Notes from the 3d-force-graph README: the 2D, VR and AR versions share one API, and `graphData()` accepts
incremental updates, so nodes can be added to a running graph.

## Sci-fi ("FUI") interface kits

| Kit | Stars | Last push | Licence | Status |
| --- | --- | --- | --- | --- |
| [Arwes](https://github.com/arwes/arwes) | 7576 | 2026-07-05 | MIT | README: "no longer maintained and currently outdated but it is still functional"; last release `v1.0.0-alpha.23`, 2023-08-13 |
| [augmented-ui](https://github.com/propjockey/augmented-ui) | 1413 | 2024-05-28 | BSD-2-Clause | CSS only: clipped corners and borders |

bl00d.money uses neither; its look comes from two fonts, a black background, one acid-yellow accent, monospace labels
in capitals and thin rules.

## Not yet studied

- Figma: how an agent can draw into a Figma file (the Figma MCP server and what it can write).
- How each graph library handles a few hundred nodes with readable labels, tested on real data.
