# /datacortex-ask [question]

Answer a question using your knowledge base.

## Model

Use **haiku** model for this command (fast, cost-effective for Q&A synthesis).

## Behavior

1. Run `datacortex search "[question]"` to retrieve relevant documents
2. Read the output file with full document content
3. Synthesize an answer based ONLY on the retrieved documents

## Synthesis Guidelines

- Answer based ONLY on the provided documents
- Cite sources using [[Document Title]] format
- If the answer isn't in the documents, say so clearly
- Be concise but complete
- Include a Sources section at the end listing the documents used

## Example Output

Based on your notes, here's what I found about **data tokenization**:

Your knowledge base describes data tokenization as transforming data ownership into tradeable assets through blockchain-based tokens. The key mechanism is the SPV (Special Purpose Vehicle) structure, which enables legal compliance while maintaining decentralized ownership records. [[Data Tokenization]]

The key components include:
- ERC-3643 token standard for compliant securities [[Verity Specification]]
- Revenue distribution waterfall for earnings flow [[Real World Assets]]
- Fractional ownership model that enables retail participation [[Data as RWA]]

**Sources:**
- [[Data Tokenization]] (92% relevance)
- [[Real World Assets]] (85% relevance)
- [[Verity Technical Specification]] (78% relevance)
