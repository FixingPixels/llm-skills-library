---
title: Transcript Providers
load_at: on-demand
summary: Per-provider adapter notes (detection signals, list/fetch capability names, dedup keys, quirks) for Granola, Fireflies, Otter, Fathom, Read.ai, tl;dv, Grain, Zoom, Google Meet, and Microsoft Teams
---

# Transcript Providers

One short adapter section per known meeting transcription tool. Load this file **only when you actually need to wire a specific provider** — `source-ingestion.md` handles provider discovery and the overall ingestion flow without needing this detail.

Each section answers four questions in the same shape:

- **Detection** — how the skill recognizes the provider is available.
- **List** — capability or pattern for "list recent items since N."
- **Fetch** — capability or pattern for "give me the full transcript for id X."
- **Dedup key** — what to store in the profile's `sources[].id` to prevent re-ingest.
- **Notes** — quirks the skill should handle.

If a tool the user names is not listed here, treat it as unknown and ask the user how to reach it (MCP server name, API doc URL, or a folder of exports).

## Contents

1. [Granola](#granola)
2. [Fireflies.ai](#firefliesai)
3. [Otter.ai](#otterai)
4. [Fathom](#fathom)
5. [Read.ai](#readai)
6. [tl;dv](#tldv)
7. [Grain](#grain)
8. [Zoom](#zoom)
9. [Google Meet](#google-meet)
10. [Microsoft Teams](#microsoft-teams)
11. [Unknown provider](#unknown-provider)

---

## Granola

- **Detection** — MCP server / connector identifying as `granola` or surfacing Granola-shaped tool names (`list_notes`, `get_note`, etc.).
- **List** — usually `list_notes` / `list_meetings`. Many surfaces support a date filter; if not, list a recent window and filter client-side.
- **Fetch** — usually `get_note` / `get_transcript`.
- **Dedup key** — Granola note id.
- **Notes** — Per-call user approval may be required in some hosts; batch fetches where possible. Granola sometimes returns both a structured summary and a raw transcript — prefer the raw transcript for voice analysis.

## Fireflies.ai

- **Detection** — MCP server named `fireflies` / `fireflies-ai`, or `FIREFLIES_API_KEY` available in the environment.
- **List** — GraphQL `transcripts(fromDate: ..., toDate: ...)` query against `https://api.fireflies.ai/graphql`.
- **Fetch** — `transcript(id: ...)` returning `sentences[]` with speaker labels.
- **Dedup key** — Fireflies transcript id.
- **Notes** — Stitch `sentences[]` into a single string with speaker labels preserved before analysis. Apply paid-tier rate limits when listing many items at once.

## Otter.ai

- **Detection** — Otter MCP, an `OTTER_*` env token, or a folder of Otter exports (`.txt`/`.docx`).
- **List** — Otter exposes a Speech list API; the folder fallback is a directory of dated export filenames.
- **Fetch** — Speech detail endpoint, or read the exported file directly.
- **Dedup key** — Otter speech id when available, else the file path.
- **Notes** — Exports include speaker labels and a header block; keep them, they aid analysis. Strip Otter's "highlights" footer if present.

## Fathom

- **Detection** — Fathom MCP, a Fathom API token, or per-meeting `.txt` exports in a folder.
- **List** — Fathom's API; or list dated `.txt` files in the exports folder.
- **Fetch** — Fathom call detail; or read the file.
- **Dedup key** — Fathom call id when via API; else the file path.
- **Notes** — Fathom exports tend to be tidy plain text — no extra normalization required.

## Read.ai

- **Detection** — Read.ai MCP, an API token, or transcript exports (email or folder).
- **List** — Read.ai API; or scan the export folder.
- **Fetch** — Read.ai transcript endpoint; or read the export.
- **Dedup key** — Read.ai meeting id; else file path.
- **Notes** — Read.ai exports include a chapter/summary section before the transcript — skip it when isolating the raw transcript.

## tl;dv

- **Detection** — tl;dv MCP, API token, or `.txt`/`.srt` exports.
- **List** — tl;dv API; or list dated exports.
- **Fetch** — API; or read the export (strip `.srt` cue timing identically to `.vtt`).
- **Dedup key** — tl;dv meeting id; else file path.
- **Notes** — Treat `.srt` like `.vtt` (strip `00:14:32,000 --> 00:14:35,500` cues).

## Grain

- **Detection** — Grain MCP, API token, or shareable transcript URLs.
- **List** — Grain API.
- **Fetch** — Grain API; or WebFetch a shareable URL the user provided.
- **Dedup key** — Grain recording id; else canonical share URL.
- **Notes** — Grain often returns highlight clips and a full transcript; use the full transcript.

## Zoom

- **Detection** — Zoom MCP / Cloud Recording API token; OR a folder of `.vtt` files exported from Zoom; OR a folder name matching `cloud[_-]?recordings?` / `zoom`.
- **List** — Cloud Recording API; or list `.vtt`/`.txt` files in the folder.
- **Fetch** — Recording download via API; or read the file.
- **Dedup key** — Zoom meeting UUID (from the API or the VTT header); else file path.
- **Notes** — Strip the `WEBVTT` header and every `HH:MM:SS.mmm --> HH:MM:SS.mmm` cue timing line before analysis. Preserve speaker labels if Zoom included them.

## Google Meet

- **Detection** — A Drive MCP / Google Drive connector with access to a "Meet Recordings" folder OR a "Transcripts" folder; OR a local folder of Meet transcript exports (Docs converted to `.txt`/`.md`).
- **List** — Drive list of the relevant folder, filtered by mtime; or filesystem listing.
- **Fetch** — Drive file fetch returning Doc content as text; or read the local file.
- **Dedup key** — Drive file id when via Drive; else file path.
- **Notes** — Gemini-generated Meet transcripts are formatted as alternating speaker paragraphs without timecodes — they ingest cleanly with no normalization. Skip Meet recordings that are video-only (no transcript Doc).

## Microsoft Teams

- **Detection** — Microsoft Graph / Teams MCP with calendar + recording scopes; OR a folder of `.docx` transcript exports.
- **List** — Graph `/me/onlineMeetings` + `/transcripts`; or filesystem listing.
- **Fetch** — Graph transcript content endpoint; or read the `.docx` (use `python-docx`).
- **Dedup key** — Teams meeting id; else file path.
- **Notes** — Teams transcripts include speaker labels and timestamps — strip the timestamps but keep speaker labels.

## Unknown provider

If the user names a tool that isn't here:

1. Ask whether it's reachable via an MCP server, an API + token, or a folder of exports.
2. Capture the answer in `learnings.md` so the next run recognizes it.
3. If reachable, treat it as a generic provider: list-recent + fetch-by-id, dedup by whatever stable id the tool provides (falling back to file path).
4. If not reachable, ask the user to export transcripts to a folder and point the skill at it.
