# ✈️ Molt.bot plane-skill 🦞

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Plane.so skill for [Clawdbot](https://github.com/Jinko-LLC/clawdbot) / [Moltbot](https://github.com/Jinko-LLC/moltbot) agents** — manage projects, work items, cycles, modules, comments, and members via a zero-dependency Python CLI.

## Features

- **Projects** — list, get, create
- **Work Items** — list, get, create, update, assign, delete, search
- **Comments** — list activity, add comments to work items
- **Cycles** — list, get, create sprints
- **Modules** — list, get, create feature modules
- **Members** — list workspace members (for finding assignee IDs)
- **States & Labels** — list for reference
- Zero dependencies — Python 3.8+ stdlib only
- Color output with graceful degradation
- Table and JSON output formats

## Installation

### Via MoltHub (recommended)

```bash
npx molthub install plane
```

### Manual

Copy `SKILL.md` and `scripts/plane` into your agent's skill directory:

```bash
mkdir -p ~/.clawdbot/skills/plane/scripts
cp SKILL.md ~/.clawdbot/skills/plane/
cp scripts/plane ~/.clawdbot/skills/plane/scripts/
chmod +x ~/.clawdbot/skills/plane/scripts/plane
```

## Setup

You need two environment variables:

| Variable | Description | Where to get it |
|---|---|---|
| `PLANE_API_KEY` | Personal access token | Plane → Profile → Personal Access Tokens |
| `PLANE_WORKSPACE` | Workspace slug | The URL path segment (e.g., `my-team` from `app.plane.so/my-team/`) |

```bash
export PLANE_API_KEY="your-api-key-here"
export PLANE_WORKSPACE="your-workspace-slug"
```

Optionally, set `PLANE_BASE_URL` if you're self-hosting Plane (default: `https://api.plane.so`).

## Usage

```bash
# Who am I?
plane me

# List workspace members
plane members

# List all projects
plane projects list

# Create a work item
plane issues create -p PROJECT_ID --name "Fix login bug" --priority high

# Assign it to someone
plane issues assign -p PROJECT_ID ISSUE_ID USER_ID

# Add a comment
plane comments add -p PROJECT_ID -i ISSUE_ID "Working on this now"

# Search across workspace
plane issues search "login bug"

# List cycles in a project
plane cycles list -p PROJECT_ID

# JSON output
plane projects list -f json
```

### All Commands

| Command | Description |
|---|---|
| `plane me` | Show current user |
| `plane members` | List workspace members |
| `plane projects list` | List all projects |
| `plane projects get ID` | Get project details |
| `plane projects create --name N --identifier I` | Create project |
| `plane issues list -p ID` | List work items |
| `plane issues get -p ID ISSUE` | Get work item details |
| `plane issues create -p ID --name N` | Create work item |
| `plane issues update -p ID ISSUE [--fields]` | Update work item |
| `plane issues assign -p ID ISSUE USER...` | Assign work item |
| `plane issues delete -p ID ISSUE` | Delete work item |
| `plane issues search QUERY` | Search work items |
| `plane comments list -p ID -i ISSUE` | List comments/activity |
| `plane comments add -p ID -i ISSUE "text"` | Add comment |
| `plane cycles list -p ID` | List cycles |
| `plane cycles get -p ID CYCLE` | Get cycle details |
| `plane cycles create -p ID --name N` | Create cycle |
| `plane modules list -p ID` | List modules |
| `plane modules get -p ID MODULE` | Get module details |
| `plane modules create -p ID --name N` | Create module |
| `plane states -p ID` | List workflow states |
| `plane labels -p ID` | List labels |

### Filters

Work item listing supports filters:

```bash
plane issues list -p PROJECT_ID --state STATE_ID
plane issues list -p PROJECT_ID --priority high
plane issues list -p PROJECT_ID --assignee USER_ID
```

## How It Works

The CLI is a single Python script (`scripts/plane`) that wraps the [Plane.so REST API v1](https://developers.plane.so/). It uses only Python standard library modules (`urllib`, `json`, `argparse`) — no pip installs needed.

## License

[MIT](LICENSE) © 2026 [Jinko LLC](https://github.com/JinkoLLC)
