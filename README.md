# Command Drill

A practice playground for CLI commands — built because relying on AI autocomplete every day was starting to erode recall of commands I should just know cold.

It's a single static HTML file (`command-drill.html`) with no build step and no backend: open it in any browser, or open it directly as a file. Progress is tracked per-command in the browser's `localStorage`, so it's private to whichever browser you use it in.

## What's in it

95 hand-written command-recall drills across three sections:

- **Git** (23) — the basics (add, commit, push, pull, fetch) plus the ones worth actually remembering: rebase -i, cherry-pick, stash, reset (soft/hard) vs revert, bisect, blame, reflog, worktree, add -p, log --pretty=format.
- **Linux · EC2 · Docker** (40) — grep/find (recursive search, content search, time/size filters), permissions (chmod/chown), scp/rsync/ssh to and from EC2, Docker (ps/logs/exec/build/prune), disk/process inspection (du/df/lsof/ss), systemd + journalctl, tmux, and the `aws` CLI (ec2, s3, logs).
- **Dev basics · Vim · Python** (32) — file/directory creation, Vim editing *and* navigation (dd/yy/:%s, gg/0/$/w/b/%), venv/pip, env vars, tar, crontab, and everyday shell productivity (`cd -`, `pushd`, `!!`, Ctrl+R, `alias`).

Each question is tagged **basic / intermediate / advanced**.

## How it works

**Practice mode** shows one command prompt at a time. Type your answer and hit Check (or Enter):

- Checking isn't plain string-matching — most commands are validated structurally (which flags actually appear, in any order or bundling), so `grep -rni` and `grep -in -r` both pass while a missing flag fails.
- Stuck? Hints reveal progressively; "Show answer" reveals the canonical form plus a short explanation of what each flag does and why.
- Filter by **status** (All / Weak spots / Not yet tried) and **level** (Basic / Intermediate / Advanced) independently — combine them to drill just what a session calls for, e.g. "Weak spots" + "Advanced".
- Previous/Next navigate the current filtered queue; mastery per section and overall accuracy are tracked in the header.

**Learn mode** is a separate screen — no typing, no filters. It lists every command in the current section, grouped by difficulty, with its answer and explanation always visible. Use it to read through everything once before drilling.

## Running it

Just open `command-drill.html` in a browser — no server required. It's also published as a Claude Artifact for quick access from anywhere: ask Claude to pull up the "Command Drill" link if you've lost it.

## Adding more commands

The question bank is a plain JS array (`const Q = [...]`) near the top of the `<script>` block in `command-drill.html`. Each entry has a `prompt`, progressive `hints`, the canonical `answer`, an `explain` (what the flags mean / why), and a `check` object describing how to validate a typed answer (base command, required flags, required substrings, or acceptable alternatives). Add an entry, reload, and it shows up in both Practice and Learn mode automatically.
