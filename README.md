# claude-plugins

A Claude Code plugin marketplace. I use these tools in my own practice at [herakles.dev](https://herakles.dev); this repo is how you install them without copying files by hand.

```bash
claude plugin marketplace add herakles-dev/claude-plugins
claude plugin install opensource-pipeline@herakles-plugins
claude plugin install typesafe-claude-kit@herakles-plugins
claude plugin install safexl@herakles-plugins
```

## What's in it

**[opensource-pipeline](https://github.com/herakles-dev/opensource-pipeline)** — forks a private repo, strips secrets and internal references, and generates the docs (README, LICENSE, CONTRIBUTING, issue templates) a public release needs. Three agents: one forks and sanitizes, a second independently audits the result against 21 detection patterns, a third packages it. I built this because I open-source my own projects often enough that doing it by hand got tedious. It's also the workflow behind a merged PR — [affaan-m/ECC#1036](https://github.com/affaan-m/ECC/pull/1036) — into a repo that's currently at 267k+ stars.

**[typesafe-claude-kit](https://github.com/herakles-dev/typesafe-claude-kit)** — a Claude Code kit for TypeSafe's Jev model: typed Choice/Score/Noul judgments with calibrated probabilities that your code can act on directly, instead of parsing free text. It's a cheap, fast decision layer that sits under an orchestrating LLM — good for routing, ranking, and screening; not a replacement for Claude on generation or reasoning tasks.

**[safexl](https://github.com/herakles-dev/safexl)** — a hook that watches your workbooks while Claude works. If another library, say openpyxl or pandas, re-saves one, the hook rebuilds it from the original and keeps the cell edits Claude made. When that can't be done, it puts the original back and tells Claude to redo the edit with safexl. No row deletion, no column inserts, no charts. Checked in LibreOffice, not Excel.

The hook calls the `safexl` command, so install that first: `pip install "git+https://github.com/herakles-dev/safexl#subdirectory=packages/safexl"`. The plugin sits in a subfolder of the safexl repo. The engine and my benchmark kit are in the same repo.

Each plugin is its own repo with its own README, versioning, and issue tracker. This marketplace only points at them — updates to any of them flow through automatically.

## Adding a plugin to your own project

The plugins install into `~/.claude/` by default (user scope). If you'd rather pin one to a specific project, see that plugin's own README for its manual-copy instructions.

## License

Each plugin carries its own license (all MIT — see their repos). This marketplace repo itself is MIT; see [LICENSE](LICENSE).
