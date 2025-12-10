# /datacortex-digest

Generate daily digest of link suggestions based on content similarity.

## Model

Use **haiku** model for this command (fast, cost-effective for link suggestions).

## Behavior

1. Run `datacortex digest` to generate compact output
2. Read the output file path from stderr
3. Read the output file contents
4. Synthesize natural language suggestions for the user

## Output Interpretation

The digest contains two sections:

### SIMILAR_PAIRS
Documents that have high semantic similarity but are NOT currently linked.

Format: `doc_a | doc_b | similarity | recency | centrality | score`

- **similarity**: Cosine similarity of embeddings (0-1)
- **recency**: How recently the documents were updated (0-1, higher = more recent)
- **centrality**: Average graph centrality of the pair (0-1, higher = more connected)
- **score**: Final weighted score (similarity * 0.5 + recency * 0.3 + centrality * 0.2)

### ORPHANS
Documents with no incoming links (may be forgotten or isolated).

Format: `title | words | created_at | path`

## Synthesis Guidelines

### For Similar Pairs

For each pair, explain:
1. **Why they should be linked**: Based on titles and semantic similarity score
2. **Directional suggestion**: Which document should link to which (consider context and maturity)
3. **Reasoning**: Brief explanation of the connection

Example:
> "Data Tokenization" and "Real World Assets" have 0.87 similarity. These concepts are closely related - RWAs are often implemented through tokenization. Consider adding a link from "Real World Assets" to "Data Tokenization" to explain the underlying mechanism.

### For Orphans

For each orphan:
1. **Note the isolation**: Explain that it has no incoming links
2. **Suggest integration**: Propose which existing documents could link to it
3. **Context**: Use word count and creation date to assess importance

Example:
> "Autonomous AI Legal Entity" (278 words, created 2025-12-09) has no incoming links. This is a substantial document that should be connected. Consider linking from "AI Agent Architecture" or "Legal Framework" to integrate it into the knowledge graph.

## Output Format

Present your suggestions in a clear, actionable format:

### Link Suggestions

1. **[Doc A] → [Doc B]** (similarity: X.XX)
   - Reasoning: ...

### Orphan Integration

1. **[Orphan Title]** (XXX words)
   - Suggested parents: ...
   - Reasoning: ...

## Notes

- Prioritize high-scoring pairs (top 10-15 are most valuable)
- For orphans, focus on recent or substantial documents (high word count)
- Consider the broader knowledge graph structure when suggesting connections
- Be specific about which document should link to which
