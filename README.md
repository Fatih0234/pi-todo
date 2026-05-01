# pi-todo

A file-based todo manager for [pi](https://pi.dev), with optional **GitHub issue integration**.

## Features

- **File-based storage** — Each todo is a standalone markdown file under `.pi/todos/`
- **Visual manager** — `/todos` command with fuzzy search, keyboard shortcuts, and a detail overlay
- **Session-safe** — Todos are tracked per working directory, so switching projects keeps them separate
- **GitHub issue export** — Convert any todo into a GitHub issue directly from the detail view or action menu. Todo tags are automatically mapped to GitHub labels (missing labels are auto-created)
- **Lock-based editing** — Prevents conflicts when multiple sessions edit the same todo

## Install

```bash
pi install git:github.com/Fatih0234/pi-todo
```

Or copy the extension directly:

```bash
cp extensions/todo.ts ~/.pi/agent/extensions/
```

## Usage

### LLM tool

The agent can manage todos naturally via the `todo` tool:

```
Create a todo titled "Refactor auth module"
```

Actions: `list`, `list-all`, `get`, `create`, `update`, `append`, `delete`, `claim`, `release`.

### Interactive `/todos` command

| Key | Action |
|-----|--------|
| `↑↓` | Navigate todos |
| `Enter` | Open detail view |
| `Ctrl+A` | Open action menu |
| `Ctrl+Shift+W` | Work on selected todo |
| `Ctrl+Shift+R` | Refine selected todo |
| `Esc` | Close |

### Detail view shortcuts

| Key | Action |
|-----|--------|
| `↵` | Work on todo |
| `r` | Refine todo |
| `v` | Select lines to comment |
| `g` | **Create GitHub issue** |
| `c` | Close / reopen todo |
| `d` | Delete todo |
| `Esc` | Back |

### GitHub issue integration

From the detail view, press **`g`** (or choose **"github issue"** from the action menu) to convert the todo into a GitHub issue.

Requirements:
- [GitHub CLI (`gh`)](https://cli.github.com/) installed
- Authenticated (`gh auth login`)
- Inside a git repository with a GitHub remote

The issue title and body are taken directly from the todo. **Todo tags are automatically mapped to GitHub labels** — if a label doesn't exist on the repo, it is auto-created with a sensible color. The issue URL is copied to your clipboard on success.

## Todo file format

Each todo lives at `.pi/todos/<id>.md`:

```json
{
  "id": "deadbeef",
  "title": "Add tests",
  "tags": ["qa"],
  "status": "open",
  "created_at": "2026-01-25T17:00:00.000Z",
  "assigned_to_session": "session.json"
}
```

Notes about the work go here (markdown body).

## License

MIT
