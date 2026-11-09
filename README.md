# LevelthanQ-DEV

Controller repo for the LevelthanQ multi-repository project. It holds no
application code — only the VS Code workspace, the setup script, and the
gitignore rules that keep the 7 real repos out of this one's history.

## Layout

```
LevelthanQ-DEV/
├── LevelthanQ.code-workspace   # multi-root workspace (relative paths, safe to move)
├── scripts/setup.ps1       # clone whichever child repos are missing + npm install
├── LevelthanQ-APP/
├── LevelthanQ-SDB/
├── LevelthanQ-TRX/
├── LevelthanQ-EXE/
├── LevelthanQ-PWA/
├── LevelthanQ-PKG/
├── LevelthanQ-WEB/
```

Each `LevelthanQ-*` folder is its own git repository (own `.git`, own GitHub
remote under `ZYDRAXYL/`). `.gitignore` excludes them entirely from this repo.

## Chained repositories

From [`LevelthanQ-APP/chain/chain.json`](https://github.com/ZYDRAXYL/LevelthanQ-APP/blob/main/chain/chain.json):

| Repo | Role | Owns | Releases | Visibility |
|---|---|---|---|---|
| [LevelthanQ-APP](https://github.com/ZYDRAXYL/LevelthanQ-APP) | hub | `.claude/`, `chain/`, `docs/`, `process/`, `tools/` | — | private |
| [LevelthanQ-SDB](https://github.com/ZYDRAXYL/LevelthanQ-SDB) | schema | `schema/`, `supabase/`, `assets/`, `generated/` | `sdb-v*` | public |
| [LevelthanQ-TRX](https://github.com/ZYDRAXYL/LevelthanQ-TRX) | service | `netlify/`, `public/`, `netlify.toml` | — | public |
| [LevelthanQ-EXE](https://github.com/ZYDRAXYL/LevelthanQ-EXE) | app | `electron/` | `v*` | private |
| [LevelthanQ-PWA](https://github.com/ZYDRAXYL/LevelthanQ-PWA) | build | `tools/`, `shim/`, `dist/` | — | public |
| [LevelthanQ-PKG](https://github.com/ZYDRAXYL/LevelthanQ-PKG) | content | `packages/`, `index.json` | `pkg-v*` | public |
| [LevelthanQ-WEB](https://github.com/ZYDRAXYL/LevelthanQ-WEB) | site | `*.html`, `assets/` | `mirror` | public |

Changes flow one way along the chain:

```
EXE    APP > SDB, TRX > EXE > PKG, WEB, PWA
PWA    APP > SDB, TRX > EXE > PWA > WEB
```

## First-time setup on a new device

Prerequisites: [Git](https://git-scm.com/) with access to the `ZYDRAXYL` org (APP, EXE are private), and [Node.js LTS](https://nodejs.org/).

```powershell
git clone https://github.com/ZYDRAXYL/LevelthanQ-DEV.git
cd LevelthanQ-DEV
./scripts/setup.ps1
```

Then open `LevelthanQ.code-workspace` in VS Code.

> If PowerShell refuses to run the script, run it once as:
> `powershell -ExecutionPolicy Bypass -File .scriptssetup.ps1`

## License

MIT — see [LICENSE](LICENSE). Created by LDKTC.
