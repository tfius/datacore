# /datacortex

Launch the knowledge graph visualization or run graph analysis commands.

## Usage

```
/datacortex              # Start server and open visualization
/datacortex stats        # Show graph statistics
/datacortex pulse        # Generate a new pulse snapshot
/datacortex orphans      # Find unlinked documents
```

## Behavior

### Default (no arguments)

1. Check if datacortex server is already running on port 8765
2. If not running, start the server in background
3. Open browser to http://localhost:8765

```bash
cd ~/Data/1-datafund/2-projects/datacortex

# Check if server running
if ! curl -s http://localhost:8765/api/health > /dev/null 2>&1; then
    echo "Starting datacortex server..."
    python -m datacortex serve &
    sleep 2
fi

open http://localhost:8765
```

### /datacortex stats

Show graph statistics without starting the server:

```bash
cd ~/Data/1-datafund/2-projects/datacortex
python -m datacortex stats
```

Output:
```
==================================================
  DATACORTEX GRAPH STATISTICS
==================================================
  Spaces: personal, datafund
  Generated: 2025-01-15 14:30
==================================================

  Nodes: 1,234
  Edges: 3,456
    - Resolved: 3,200
    - Unresolved: 256
  Avg Degree: 5.6
  Max Degree: 42
  Orphans: 89

  By Type:
    page: 456
    zettel: 389
    journal: 234
    literature: 89
    stub: 66

  By Space:
    datafund: 789
    personal: 445
```

### /datacortex pulse

Generate a new pulse snapshot:

```bash
cd ~/Data/1-datafund/2-projects/datacortex
python -m datacortex pulse generate
```

Output:
```
Generating pulse for spaces: personal, datafund
Pulse saved: pulses/2025-01-15-1430.json
  ID: 2025-01-15-1430
  Nodes: 1,234
  Edges: 3,456
```

### /datacortex orphans

Find documents with no connections:

```bash
cd ~/Data/1-datafund/2-projects/datacortex
python -m datacortex orphans --min-words 100
```

## Prerequisites

1. **Install datacortex**:
   ```bash
   pip install -e ~/Data/1-datafund/2-projects/datacortex
   ```

2. **Sync database** (if stale):
   ```bash
   python ~/.datacore/lib/zettel_db.py sync
   ```

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
