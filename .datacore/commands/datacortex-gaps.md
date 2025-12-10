# /datacortex-gaps

Detect knowledge gaps between semantically similar clusters that should be connected.

## Model

Use **haiku** model for this command (fast, cost-effective for bridge suggestions).

## Overview

This command analyzes the knowledge graph to find clusters of documents that are semantically related (similar topics/themes) but have few or no links between them. These gaps represent opportunities to strengthen the knowledge base by adding strategic connections.

## What is a Knowledge Gap?

A knowledge gap occurs when two clusters of documents:
1. Have high semantic similarity (their topics are related)
2. Have low link density (few actual connections)
3. The gap score = semantic similarity - link density

Higher gap scores indicate clusters that "should" be connected based on their content but currently aren't.

## Behavior

1. Run `datacortex gaps --space personal --min-score 0.3` (or without --space for all spaces)
2. Read the generated output file from /tmp/datacortex_gaps_*.txt
3. Synthesize bridge suggestions for the user
4. Present gaps in order of priority (highest gap_score first)

## Synthesis Guidelines

For each gap detected:

### 1. Name the Clusters
- Use the hub documents and top tags to create descriptive cluster names
- Example: "Cluster 3: Data Tokenization & Storage" and "Cluster 7: Trading & Risk Analytics"

### 2. Explain the Connection
- Why do these topics belong together?
- What shared themes or tags indicate relatedness?
- Example: "Both clusters deal with financial data processing - one focuses on storage/access, the other on analysis/application"

### 3. Suggest Bridge Actions

Prioritize in this order:

**A. Expand Boundary Nodes** (if any exist)
- These documents already link to both clusters
- Suggest expanding their content to strengthen the connection
- Example: "Expand 'Market Data Feed' to explicitly connect data tokenization with trading analytics"

**B. Create a Bridge Note**
- Suggest a new document that explicitly connects the themes
- Provide a suggested title and 2-3 key points it should cover
- Example: "Create 'From Data Tokenization to Trading Signals' covering: how tokenized data feeds trading models, access control for trading data, real-time data pipelines"

**C. Add Direct Links**
- Suggest specific wiki-links to add between existing documents
- Example: "Add link from 'Swarm Storage' to 'Trading Journal' explaining how to store trading data"

**D. Identify a Unifying Tag**
- If shared tags exist, recommend standardizing usage
- If no shared tags, suggest one that spans both topics
- Example: "Add #data-pipeline tag to documents in both clusters"

### 4. Prioritize by Impact

Consider:
- Gap score (higher = more important)
- Cluster sizes (larger clusters = more impact)
- Number of shared tags (more shared context = easier to connect)
- Existence of boundary nodes (easier to expand than create new)

## Output Format

Present gaps in a structured format:

```markdown
## Knowledge Gap Analysis

Found X gaps across Y clusters.

### Priority 1: [Cluster A Name] <-> [Cluster B Name]
**Gap Score:** 0.58 (semantic_sim: 0.72, link_density: 0.02)
**Sizes:** Cluster A (47 docs), Cluster B (23 docs)

**Why Connect:** [Your analysis of why these belong together]

**Recommendations:**
1. [Specific action with details]
2. [Specific action with details]
3. [Specific action with details]

**Quick Wins:**
- [If boundary nodes exist, list them]
- [If shared tags exist, suggest standardizing]

---

### Priority 2: [Next gap...]
...
```

## Important Notes

- Focus on actionable, specific suggestions
- Avoid generic advice like "add more links" - say WHICH links WHERE
- If a gap is unclear or clusters seem unrelated despite high similarity, say so
- Limit output to top 5-10 gaps to avoid overwhelming the user
- After presenting gaps, ask if user wants details on any specific gap

## Example Interaction

User: `/datacortex-gaps`