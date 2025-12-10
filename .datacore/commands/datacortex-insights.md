# /datacortex-insights

Analyze knowledge clusters and synthesize strategic insights.

## Model

Use **sonnet** model for this command (deeper analysis for cluster insights).

## Behavior

1. Run `datacortex insights` to generate cluster analysis for all spaces
2. Read the output file
3. Synthesize insights for each cluster
4. Generate a summary report with recommendations

## Synthesis Guidelines

For each cluster, generate:

### Cluster Name
Create a descriptive name (3-5 words) based on hub documents and dominant tags.

### Summary
2-3 sentences describing what the cluster covers and its primary focus.

### Key Themes
Identify 3-5 key themes or topics present in the cluster based on:
- Hub document titles
- Tag frequency
- Content samples

### Patterns
Analyze patterns you observe:
- What types of knowledge are grouped here?
- How well connected is the cluster internally (density)?
- What's the balance between mature documents and stubs?
- Are there dominant sources (literature references)?

### Connections
Note significant connections to other clusters:
- Which clusters is this most connected to?
- What might those connections represent?
- Are there unexpected bridges?

### Gaps
Identify potential gaps or missing elements:
- Topics that seem underrepresented
- Missing connections that would make sense
- Areas that need more depth
- Stubs or placeholders that should be expanded

### Recommendations
Suggest 2-4 actionable recommendations:
- Documents to link together
- Topics to research further
- Areas to expand or consolidate
- Tags to add for better organization

## Output Format

Generate a clean markdown report with:

```markdown
# Datacortex Cluster Insights
Generated: [timestamp]
Spaces: [space names]
Total Clusters: N
Total Documents: N

---

## Cluster [ID]: [Descriptive Name]
Size: N documents | Density: 0.XX | Avg Centrality: 0.XXX

### Summary
[2-3 sentence summary]

### Key Themes
- Theme 1
- Theme 2
- Theme 3

### Patterns
[Analysis paragraph]

### Connections
- Cluster X ([N links]): [What this represents]
- Cluster Y ([N links]): [What this represents]

### Gaps & Opportunities
[Analysis paragraph]

### Recommendations
1. [Actionable recommendation]
2. [Actionable recommendation]
3. [Actionable recommendation]

---

[Repeat for each cluster]

---

## Strategic Overview

### Strongest Clusters
[Analysis of well-connected, high-density clusters]

### Emerging Topics
[Clusters that are growing or gaining connections]

### Integration Opportunities
[Clusters that should be better connected]

### Priority Actions
[Top 5-10 actions to improve the knowledge graph]
```

## Options

You can run with options:
- `datacortex insights` - All clusters summary
- `datacortex insights --cluster 3` - Single cluster detail
- `datacortex insights --no-samples` - Skip content samples (faster)
- `datacortex insights --top 5` - Only top N clusters by size
- `datacortex insights --space datafund` - Single space only

## Tips

- Focus on actionable insights, not just description
- Look for cross-cluster patterns and opportunities
- Identify knowledge gaps where key connections are missing
- Suggest specific documents to create or link
- Consider the strategic value of each cluster to the organization
