# /datacortex-opportunities

Find "low hanging fruit" research opportunities in your knowledge base - stubs to fill, gaps to bridge, orphans to integrate.

## Model

Use **haiku** model for this command (fast, cost-effective for opportunity analysis).

## Behavior

1. Run `datacortex opportunities` CLI command
2. Read the output file
3. Present prioritized opportunities to user
4. Ask if they want Claude Code to research and fill any items
5. If yes, execute research for selected items

## CLI Command

```bash
cd ~/Data/1-datafund/2-projects/datacortex
source .venv/bin/activate
DATACORE_ROOT=~/Data datacortex opportunities
```

## Output Format

The CLI outputs a prioritized list in three categories:

### HIGH_VALUE_STUBS
Stub notes with high centrality (many references but no content).

Format: `title | centrality | references | tags`

These are concepts your knowledge base expects but hasn't defined. High centrality = many documents link to this stub.

### KNOWLEDGE_GAPS
Cluster pairs with semantic similarity but poor linking.

Format: `cluster_a | cluster_b | gap_score | shared_tags | bridge_suggestion`

These represent opportunities to create bridge notes connecting related but isolated topic areas.

### INTEGRATION_CANDIDATES
Orphan documents with substantial content but no incoming links.

Format: `title | words | centrality | suggested_parents`

Real content that's disconnected from the knowledge graph.

## Synthesis Guidelines

### Prioritization

Rank opportunities by:
1. **Impact**: High centrality stubs affect many documents
2. **Effort**: Word count indicates research depth needed
3. **Value**: Bridging large clusters has multiplicative effect

### For Each Opportunity

Present:
- **What**: The specific item (stub title, gap, orphan)
- **Why it matters**: Impact on knowledge graph
- **Suggested action**: What research/writing would help
- **Estimated effort**: Quick (5 min), Medium (15 min), Deep (30+ min)

## User Interaction

After presenting the top 10-15 opportunities, ask:

> "Would you like me to research and fill any of these? I can:
> 1. Fill a specific stub with researched content
> 2. Create a bridge note connecting two clusters
> 3. Integrate an orphan by finding and adding links
>
> Enter numbers (e.g., '1, 3, 5') or 'all' for top 5, or 'skip' to just see the list."

## Research Execution

When user selects items:

### For Stubs
1. Search knowledge base for context: `datacortex search "[stub title]"`
2. Read related documents to understand expected content
3. Write stub content that fits the knowledge graph context
4. Present draft for user approval

### For Knowledge Gaps
1. Analyze both clusters via `datacortex insights --cluster N`
2. Identify common themes and connection points
3. Propose bridge note title and outline
4. Draft bridge note content
5. Present for approval

### For Orphan Integration
1. Read the orphan document
2. Search for semantically similar docs: `datacortex search "[orphan title]"`
3. Identify 2-3 documents that should link to the orphan
4. Propose specific link locations (which paragraph, what anchor text)
5. Present for approval

## Example Output

```
## Knowledge Base Opportunities

### High-Value Stubs (concepts needed but undefined)

1. **Data Sovereignty** (centrality: 0.15, 12 references)
   - Referenced by: Datafund, Fair Data Society, Privacy Framework...
   - Effort: Medium (15 min)
   - Action: Define concept, explain relationship to data ownership

2. **Privacy-Preserving Computation** (centrality: 0.12, 8 references)
   - Referenced by: Secure Enclave, Differential Privacy...
   - Effort: Medium (15 min)
   - Action: Explain techniques (MPC, TEE, ZK)

### Knowledge Gaps (clusters needing bridges)

3. **Tokenization ↔ Compliance** (gap: 0.72)
   - Clusters are semantically related but only 2 cross-links
   - Bridge suggestion: "Regulatory Compliance for Data Tokenization"
   - Effort: Deep (30 min)

### Integration Candidates (orphans worth connecting)

4. **Autonomous AI Legal Entity** (523 words, 0 incoming links)
   - Suggested parents: AI Agent Architecture, Legal Framework
   - Effort: Quick (5 min) - just add links

---

Would you like me to research and fill any of these?
```

## Notes

- Focus on actionable items (skip stubs with <3 references)
- Prioritize recent orphans over old ones
- For gaps, suggest specific bridge note titles
- Always present draft content for approval before writing files
