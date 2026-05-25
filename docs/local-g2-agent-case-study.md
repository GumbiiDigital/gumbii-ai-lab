# Local-first G2 voice agent

Status: private daily-driver build; public case-study notes only.

## One-line summary

A voice-first local AI companion for Even Realities G2 glasses that keeps transcription, command handling, notes/lists, and local LLM responses on user-owned devices.

## Why this exists

Smart-glasses workflows are most useful when they are fast, private, and glanceable. The goal of this project is not a cloud chatbot on glasses; it is a local personal operations layer:

- glasses for capture and HUD output
- spare Android phone as the wearable bridge
- Mac Studio as the local reasoning server
- Ollama as the free local LLM runtime
- local files for notes, lists, and short context

No API keys, hosted LLMs, paid agent services, or external automation platforms are required.

## Architecture

```text
Even Realities G2
  ↓ voice / HUD
Spare Android phone
  ↓ local Wi-Fi
Mac Studio local bridge
  ↓ localhost / LAN
Ollama model
```

The working daily-driver path uses Even Terminal Mode as the wearable transport. A private Even Hub plugin build is also maintained for the official plugin path when QR/private loading is available.

## Design constraints

- HUD output must be glanceable: short lines, usually bullets, no long prose.
- Local-first means private data stays on user-owned hardware.
- Commands that should be deterministic, like notes and lists, should not depend on the LLM.
- Open-ended planning and summarization can go to the local Ollama model.
- The system should survive restarts, so the Mac bridge runs as a LaunchAgent.

## Current capabilities

- Take notes by voice.
- Create and update simple lists.
- Show saved lists and notes on the G2 HUD.
- Turn spoken input into short action lists.
- Plan/prioritize tasks through a local LLM.
- Summarize locally saved X/Twitter snippets without calling external APIs.
- Run health checks for bridge, Ollama, model availability, and dev server state.

## Privacy posture

The private implementation keeps runtime data out of git:

- local `.env` files are ignored
- generated Even Hub packages are ignored
- notes/lists/history are ignored
- build output and logs are ignored
- a privacy scan checks tracked files and generated packages for common secret patterns

## What I learned

The practical interface is not “chat on glasses.” It is a tiny command surface for capture, triage, and next actions. The strongest pattern so far is:

1. speak a short command
2. get a tiny HUD response
3. continue what I was doing without touching a keyboard

## Next iteration

The private v0.2 work will be driven by real usage notes:

- better correction commands like “undo last note”
- improved list editing
- local calendar/reminder integration
- more deterministic planning commands
- cleaner local X/feed import sources
- stricter HUD formatting tests

## Public release plan

The actual daily-driver repo remains private because it includes personal workflow assumptions and local runtime details. If released publicly, it should be as a separate sanitized template repo with placeholders, screenshots that reveal no personal data, and no generated device packages.
