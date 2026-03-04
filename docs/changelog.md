# Changelog — Meridian: AI Meeting Intelligence

All notable changes to this feature are documented here.
This file follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

Versions reflect internal build milestones, not public releases.

---

## [Unreleased]

### In Progress
- Transcript editing interface — inline editing of AI-generated summaries before they are shared to the workspace
- Manual project assignment flow — fallback UI when automatic project matching fails or returns low confidence
- Host review notification improvements — reminder if a summary has been waiting more than 24 hours without approval

### Planned
- Searchable meeting archive within Meridian project workspaces
- Summary accuracy feedback mechanism (thumbs up/down per summary)

---

## [0.3.0] — 2026-01-30

### Added
- First working integration with Microsoft Teams transcription API — meetings linked to Meridian now generate a transcript automatically
- AI summarisation pipeline: post-meeting transcript is processed and a structured summary (discussion points, decisions, action items) is returned within 15 minutes
- Automated summary delivery to Meridian project workspace on host approval
- Slack notification to meeting host when summary is ready for review

### Fixed
- Meeting metadata (title, date, attendees) was not being passed correctly to the project matching service — now resolved
- Slack notifications were firing before the summary generation job had completed, sending hosts to an empty summary page — fixed by adding a completion check before notification dispatch

### Known issues
- Project matching confidence is low for meetings with generic titles (e.g. "Catch-up", "Weekly sync") — manual assignment fallback not yet built

---

## [0.2.0] — 2025-12-18

### Added
- Initial data model for meeting objects: meeting ID, title, timestamp, attendee list, transcript reference, summary reference
- API authentication flow for Microsoft Teams — Meridian can now request and store access tokens for transcription
- Project matching prototype — rule-based matching using meeting title keywords against Meridian project names

### Changed
- Switched from polling-based meeting detection to webhook-based event triggers — reduces detection latency from ~5 minutes to ~30 seconds after a meeting ends

### Removed
- Prototype Zoom connector removed from codebase — de-scoped from v1 following Decision 3 in the decisions log

---

## [0.1.0] — 2025-11-28

### Added
- Discovery spike completed: evaluated three AI summarisation vendors and produced a shortlist of two for further commercial and technical review
- Confirmed Microsoft Teams as the v1 integration target based on internal usage data
- Initial data schema drafted for meetings, transcripts, and summaries
- Project repository created and access configured for core team (Sarah Chen, Marcus Webb, Priya Nair)

### Notes
- This version marks the end of the discovery phase. No user-facing functionality exists yet. All entries from 0.2.0 onwards represent active development.
