# Iran Data — Twitter Follower Network Analysis

## Overview
This notebook analyses shared Twitter followers between accounts to detect communities using graph algorithms.

## Data
- `mega_scrape_1/2/3/e.json` — Raw scraped Twitter follower data
- `mega_df_simple.csv` — Cleaned combined dataset
- `shared_followers.csv` — Pairs of accounts with ≥3 shared followers

## Workflow

1. **Load & clean data** — Merges four JSON scrape files into a single DataFrame, keeping key fields (`screen_name`, `followers_count`, `created_at`, etc.)
2. **Compute shared followers** — For every pair of target accounts, counts how many followers they share. Pairs with fewer than 3 shared followers are dropped.
3. **Build graph** — Constructs a directed Raphtory graph (`g`) where nodes are accounts and edges represent shared-follower relationships.
4. **Graph metrics** — Computes PageRank, directed graph density, and global clustering coefficient on the full graph.
5. **Community detection** — Runs the Louvain algorithm to assign nodes to one of two communities (`Team_1` / `Team_2`).
6. **Subgraph analysis** — Builds separate subgraphs (`g0`, `g1`) for each community and computes their individual clustering coefficients.
7. **GraphQL server** — Serves graphs via a local Raphtory GraphQL server for UI exploration.

## Requirements
- Python 3.x
- `pandas`
- `raphtory`

## Output Files
- `mega_df_simple.csv` — Cleaned node metadata
- `shared_followers.csv` — Edge list with shared follower counts
- `cluster_0_edges.csv` — Edge list for Community 0
- `graphs_3/new_graph` — Saved Raphtory graph file
