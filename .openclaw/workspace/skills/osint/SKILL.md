---
name: "osint_graph"
description: "OSINT graph analysis and enrichment (Neo4j, entity linking)."
requires:
  - "python3"
  - "neo4j"
tools:
  - name: "osint_graph_build"
    description: "Build or update a Neo4j graph from OSINT data."
  - name: "osint_graph_query"
    description: "Run analysis (community detection, centrality, shortest path) over the OSINT graph."
---

OSINT Graph Analyzer

This skill lets the agent:
- Ingest CSV/JSON OSINT exports (from web_osint_scan, discord_intel, etc.) into Neo4j using:  
  `python3 scripts/osint-graph.py --ingest data/sources.csv`
- Run graph algorithms to find communities, central nodes, and paths:  
  `python3 scripts/osint-graph.py --community-detection`  
  `python3 scripts/osint-graph.py --centrality --top 20`  
  `python3 scripts/osint-graph.py --path "Entity A" "Entity B"`

Usage:
- Support complex investigations by mapping relationships between entities across platforms.
- Export graphs as JSON for visualization or archival:  
  `python3 scripts/osint-graph.py --export graph.json`
