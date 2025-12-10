# /datacortex

Launch the knowledge graph visualization or run graph analysis commands.

## Usage

```
/datacortex                      # Start server and open visualization
/datacortex stats                # Show graph statistics
/datacortex embed [--force]      # Compute/update embeddings
/datacortex opportunities        # Find low-hanging fruit for research
/datacortex search "query"       # Q&A search
/datacortex insights [--cluster N]  # Cluster analysis
/datacortex digest               # Link suggestions
/datacortex gaps                 # Knowledge gap detection
/datacortex orphans              # Find unlinked documents
/datacortex pulse                # Generate pulse snapshot
/datacortex spaces               # List available spaces
```

## All Commands

### Graph & Visualization

| Command | Description |
|---------|-------------|
| `/datacortex` | Start server at localhost:8765 and open browser |
| `/datacortex stats` | Show node/edge counts, types, spaces |
| `/datacortex orphans [--min-words N]` | Find documents with no connections |
| `/datacortex spaces` | List spaces with knowledge databases |

### AI Extensions

| Command | Description |
|---------|-------------|
| `/datacortex embed [--force]` | Compute embeddings (incremental or forced) |
| `/datacortex search "query" [--top N]` | RAG search with full content |
| `/datacortex opportunities [--top N]` | Find stubs, orphans, gaps to fill |
| `/datacortex insights [--cluster N]` | Analyze clusters, find hubs and themes |
| `/datacortex digest [--threshold N]` | Find similar unlinked documents |
| `/datacortex gaps [--min-score N]` | Detect gaps between clusters |

### Temporal Snapshots

| Command | Description |
|---------|-------------|
| `/datacortex pulse` | Generate a new pulse snapshot |
| `/datacortex pulse list` | List available pulses |

## Behavior

### Default (no arguments)

1. Check if datacortex server is already running on port 8765
2. If not running, start the server in background
3. Open browser to http://localhost:8765

```bash
cd ~/Data/1-datafund/2-projects/datacortex
source .venv/bin/activate

if ! curl -s http://localhost:8765/api/health > /dev/null 2>&1; then
    echo "Starting datacortex server..."
    DATACORE_ROOT=~/Data datacortex serve &
    sleep 2
fi

open http://localhost:8765
```

### /datacortex stats

Show graph statistics:

```bash
DATACORE_ROOT=~/Data datacortex stats
```

### /datacortex embed

Compute semantic embeddings for all documents:

```bash
DATACORE_ROOT=~/Data datacortex embed           # Incremental (cache)
DATACORE_ROOT=~/Data datacortex embed --force   # Recompute all
DATACORE_ROOT=~/Data datacortex embed --space datafund  # Single space
```

### /datacortex opportunities

Find low-hanging fruit for research:

```bash
DATACORE_ROOT=~/Data datacortex opportunities --top 15
```

Output categories:
- **HIGH_VALUE_STUBS**: Concepts referenced but undefined
- **INTEGRATION_CANDIDATES**: Orphan docs worth connecting
- **UNDERLINKED_CONTENT**: Substantial docs with few links
- **STUB_HEAVY_CLUSTERS**: Topic areas needing research

### /datacortex search

RAG search with full content for Q&A:

```bash
DATACORE_ROOT=~/Data datacortex search "data tokenization" --top 10
DATACORE_ROOT=~/Data datacortex search "DMCC pilot" --no-expand
```

### /datacortex insights

Analyze knowledge clusters:

```bash
DATACORE_ROOT=~/Data datacortex insights              # All clusters
DATACORE_ROOT=~/Data datacortex insights --cluster 3  # Single cluster
DATACORE_ROOT=~/Data datacortex insights --top 5      # Top 5 by size
```

### /datacortex digest

Find similar documents that should be linked:

```bash
DATACORE_ROOT=~/Data datacortex digest --threshold 0.8 --top-n 20
```

### /datacortex gaps

Detect knowledge gaps between clusters:

```bash
DATACORE_ROOT=~/Data datacortex gaps --min-score 0.3
```

### /datacortex orphans

Find unconnected documents:

```bash
DATACORE_ROOT=~/Data datacortex orphans --min-words 100
```

### /datacortex pulse

Generate temporal snapshots:

```bash
DATACORE_ROOT=~/Data datacortex pulse generate
DATACORE_ROOT=~/Data datacortex pulse list
```

## Prerequisites

1. **Install datacortex**:
   ```bash
   cd ~/Data/1-datafund/2-projects/datacortex
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -e .
   ```

2. **Compute embeddings** (first time):
   ```bash
   DATACORE_ROOT=~/Data datacortex embed
   ```

3. **Sync database** (if stale):
   ```bash
   python ~/.datacore/lib/zettel_db.py sync
   ```

## Related Commands

For AI-synthesized insights, use the specialized commands:

| Command | Model | Purpose |
|---------|-------|---------|
| `/datacortex-digest` | haiku | Link suggestions with reasoning |
| `/datacortex-gaps` | haiku | Bridge suggestions between clusters |
| `/datacortex-insights` | sonnet | Deep cluster analysis |
| `/datacortex-ask [question]` | haiku | Answer questions from KB |
| `/datacortex-opportunities` | haiku | Research opportunities with follow-up |

## Web Interface Features

- **Interactive graph**: D3.js force-directed visualization
- **Filters**: Filter by space, node type, minimum connections
- **Search**: Find nodes by title or tag
- **Details panel**: Click node to see backlinks, outlinks, metadata
- **Pulse timeline**: View and compare historical snapshots
- **Statistics**: Live graph metrics

## Keyboard Shortcuts (Web UI)

- `/` - Focus search
- `Escape` - Close details panel
- `r` - Refresh graph
- Double-click background - Reset zoom

## Output

- Server runs at http://localhost:8765
- Pulses saved to `~/Data/1-datafund/2-projects/datacortex/pulses/`
- Search/insights/opportunities write to `/tmp/datacortex_*.txt`
