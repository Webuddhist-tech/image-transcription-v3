# Image Transcription V3 (TextAlign)

A React web app for collaborative image-text transcription correction using the
`imagetranscriptionv3` backend workflow: three double-blind annotators, then one
reviewer. Teams correct OCR text against source images with role-gated submit,
approve, reject, and trash actions.

## Features

- **Double-blind annotation** — Annotators A, B, and C start from baseline OCR, never each other's work
- **Reviewer workspace** — Compare all three annotations, approve, or reject any combination of slots
- **Role-based access** — Admin, Annotator, Reviewer; users without a role stay on Pending Approval
- **Workspace editor** — Pan/zoom/TIFF image viewer, Tibetan text editor, local drafts
- **Admin panel** — Users, groups, batches, task listing/search, restore, CSV export, contribution reports
- **Internationalization** — English and Tibetan (Bodic)
- **Theme support** — Light, dark, and system
- **Keyboard shortcuts** — `Ctrl/Cmd +/-/0` zoom, `Ctrl/Cmd+S` save draft

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Vite 7 + React 19 + TypeScript 5.9 |
| Styling | Tailwind CSS 4 + shadcn/ui (Radix UI) |
| Routing | React Router v7 |
| Server state | TanStack Query v5 |
| UI state | Zustand v5 |
| Auth | Auth0 (`@auth0/auth0-react`) |
| Image handling | react-zoom-pan-pinch, utif2 (TIFF) |
| i18n | i18next + react-i18next |
| HTTP | Axios |

## Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Create environment file
cp .env.example .env   # then fill in values (see docs/getting-started.md)

# 3. Start development server at http://localhost:3000
npm run dev
```

See [docs/getting-started.md](docs/getting-started.md) for full environment variable and Auth0 setup.

## Documentation

| Document | Description |
|---|---|
| [Getting Started](docs/getting-started.md) | Local setup, env vars, Auth0 configuration |
| [Architecture](docs/architecture.md) | Folder structure, data flow, state management |
| [Workflows](docs/workflows.md) | User roles, task state machine, QA pipeline |
| [Contributing](CONTRIBUTING.md) | Branching strategy, PR process, code conventions |

## Task State Machine

```text
pending
  -> annotating -> annotated_a
  -> annotating_b -> annotated_b
  -> annotating_c -> annotated
  -> reviewing -> reviewed
```

`reviewed` is the completed state. `trashed` is also terminal (Annotator A only).

Full workflow details: [docs/workflows.md](docs/workflows.md)

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl/Cmd + +` | Zoom in |
| `Ctrl/Cmd + -` | Zoom out |
| `Ctrl/Cmd + 0` | Reset zoom |
| `Ctrl/Cmd + S` | Save draft |

## License

MIT
