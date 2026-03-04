# Decisions Log: AI Meeting Intelligence

This log captures key product decisions made during the discovery and planning phase for AI Meeting Intelligence. Entries are listed in reverse chronological order (most recent first).

For full feature context, see `docs/prd-template.md`.

---

## Decision 5 — Notification model: opt-out by default

**Decision made:** Meeting summaries will be pushed to project workspaces automatically once the host approves them. Consultants who do not want a summary shared to the workspace can suppress it on a per-meeting basis.

**Rationale:** Opt-out maximises coverage and reduces friction for the majority use case. The team agreed that the value of consistent, searchable documentation outweighs the overhead of requiring active opt-in for every meeting. Hosts retain control via an explicit suppress option before the summary is published.

**Date:** 2026-01-22
**Owner:** Sarah Chen
**Revisit trigger:** If adoption data shows high suppress rates (>20%), reconsider whether opt-out is creating resentment rather than coverage.

---

## Decision 4 — Audio data retention: 7 days

**Decision made:** Raw audio recordings will be retained for 7 days after a meeting ends, after which only the transcript text and AI-generated summary are stored. Audio is permanently deleted.

**Rationale:** Legal and compliance reviewed three retention windows (7 days, 30 days, 90 days). The 7-day window was selected to minimise data exposure risk while still allowing transcript correction disputes to be raised in the days immediately following a meeting. Longer retention was judged to be disproportionate given that the summary — not the raw audio — is the primary long-term artefact. This decision was signed off by the Legal team lead.

**Date:** 2025-12-10
**Owner:** Sarah Chen / Legal
**Revisit trigger:** If transcript accuracy issues require consultants to reference audio longer than 7 days post-meeting, reopen with Legal.

---

## Decision 3 — Meeting platform integration: Microsoft Teams only for v1

**Decision made:** Version 1 of the feature will support Microsoft Teams exclusively. Zoom integration is de-scoped and will be considered for v2.

**Rationale:** Internal usage data shows that 87% of client-facing meetings at Luminary take place on Teams. Building a robust, well-tested integration for one platform is preferable to a fragile integration for two. Engineering estimated that including Zoom in v1 would extend the timeline by 6 weeks and introduce disproportionate complexity in the transcription pipeline. The Teams-only scope allows the team to ship a polished experience faster and validate core assumptions before expanding.

**Date:** 2025-12-03
**Owner:** Marcus Webb
**Revisit trigger:** If client-facing Zoom usage increases materially, or if Zoom requests emerge strongly from v1 user feedback.

---

## Decision 2 — Target launch: Q2 2026

**Decision made:** The feature will target a Q2 2026 launch, timed to align with Luminary's annual client review season (April–June).

**Rationale:** Launching before the peak client review period gives consultants a full season to benefit from automated meeting capture during the highest-volume meeting period of the year. The team reviewed scope against available engineering capacity and confirmed Q2 is achievable provided compliance sign-off and vendor selection are finalised by end of January 2026. A Q2 launch also gives the product team a natural checkpoint at mid-year to evaluate adoption before committing to v2 scope.

**Date:** 2025-11-28
**Owner:** Sarah Chen
**Revisit trigger:** If Legal sign-off or vendor selection slips past end of January, timeline should be reviewed immediately.

---

## Decision 1 — AI summarisation: buy, not build

**Decision made:** Luminary will purchase a third-party AI summarisation API rather than building an in-house model.

**Rationale:** Building a proprietary summarisation model was estimated at 9–12 months of ML engineering time with no guarantee of output quality comparable to leading commercial providers. The team evaluated three vendors and produced a shortlist of two for detailed review (see vendor comparison document in Confluence). Purchasing an API allows the team to ship a working product significantly faster and redirect engineering effort toward the Meridian-specific integration work — project matching, workspace sync, and the host review interface.

**Date:** 2025-11-15
**Owner:** Marcus Webb / Sarah Chen
**Revisit trigger:** If vendor pricing becomes prohibitive at the scale of Luminary's meeting volume, or if in-house ML capability grows through future hiring.
