# Codex Session Viewer

A simple, private way to read back what an AI coding agent did during a session.

## What is this?

[OpenAI Codex CLI](https://github.com/openai/codex) is a command-line coding
assistant. As it works, it records everything it does — every message, shell
command, file edit, plan, and web search — into log files on your computer
(called "rollout" logs). Those raw logs are dense JSON and not pleasant to read.

**Codex Session Viewer** turns those logs into a clean, browsable transcript.
You get a readable, scrollable view of the whole conversation: what you asked,
what the agent replied, the commands it ran (with their output), the file
changes it made (shown as colorized diffs), its task plans, and any web
searches — all organized turn by turn with a navigation sidebar.

It's a single web page. There is no account, no server, and no upload. You open
the page, drop in your logs, and read.

### Your data stays on your machine

Even though the page calls it "upload," nothing is ever sent anywhere. The page
reads, unpacks, and displays your logs entirely inside your own browser. The
data lives only in the browser tab's memory while you're viewing it, and it's
gone the moment you close or refresh the tab. Nothing is written to disk and
nothing is transmitted over the internet.

## How to use it

1. **Open the viewer.** Open `index.html` in any modern web browser (just
   double-click the file, or host it as a static page).
2. **Create an archive of your Codex logs.** This is a `.tar.gz` file
   containing your session logs — see the next section for how to make one.
3. **Drop it in.** Drag the `.tar.gz` onto the page, or click to choose the
   file.
4. **Read.** If the archive contains a single session, it opens straight into
   the transcript. If it contains several, you get a list to pick from. Use the
   sidebar to jump between turns, and the toggles to show or hide the agent's
   reasoning, terminal output, and commentary.

The viewer expects the standard Codex layout inside the archive — session logs
named `rollout-*.jsonl` living under a `sessions/` folder (typically
`.codex/sessions/YYYY/MM/DD/`).

## How to create a log archive from a local Codex install

Codex stores its logs in a `.codex` folder in your home directory. You just
need to bundle the relevant pieces into a single `.tar.gz` file.

A general-purpose command that grabs your sessions (plus history and logs, if
present) looks like this:

```bash
tar -czf /tmp/codex_session_logs.tar.gz \
  ~/.codex/sessions ~/.codex/history* ~/.codex/log* 2>/dev/null
```

This creates `/tmp/codex_session_logs.tar.gz`, which is the file you then drop
into the viewer.

A few notes:

- The viewer only needs the `sessions` directory (`rollout-*.jsonl` files), so
  at minimum `tar -czf /tmp/codex_session_logs.tar.gz ~/.codex/sessions` is
  enough. Including `history*` and `log*` is harmless — the viewer ignores
  anything that isn't a session log.
- `2>/dev/null` just silences "no such file" warnings in case `history*` or
  `log*` don't exist on your system.
- If your Codex data lives somewhere other than `~/.codex`, point the paths at
  wherever your `sessions` folder actually is.

### If you run Codex inside a Docker container

If (like the author) you run Codex inside Docker containers, the logs live
inside the container's filesystem. Run the same `tar` command *inside* the
container to create the archive, then copy it out to your host machine so you
can open it in a browser:

```bash
# inside the container — create the archive
tar -czf /tmp/codex_session_logs.tar.gz \
  ~/.codex/sessions ~/.codex/history* ~/.codex/log* 2>/dev/null

# on your host — copy the archive out of the container
docker cp <container-name-or-id>:/tmp/codex_session_logs.tar.gz .
```

Then drop the copied `codex_session_logs.tar.gz` into the viewer.
