# PRD: AI Meeting Intelligence

**Product:** Meridian
**Feature:** AI Meeting Intelligence
**Author:** Sarah Chen
**Status:** Draft — In Review
**Last Updated:** 2026-01-14
**Target Launch:** Q3 2026

---

## 1. Problem Statement

Consultants at Luminary Group spend an estimated [X hours per week] on meeting admin — writing up notes, extracting action items, and sharing summaries with project teams. This work is repetitive, inconsistently done, and often delayed by days after meetings end. Key decisions and commitments made in client calls are frequently lost or buried in email threads, creating risk for project delivery and client relationships.

Meridian is already the place where project knowledge lives. This feature will make it the place where meeting intelligence lives too — so consultants can walk out of a meeting and get back to the work that actually matters.

---

## 2. Goals

### Primary goal

Reduce the time consultants spend on post-meeting documentation by at least 50%.

### Secondary goals

- Ensure key decisions and action items from client meetings are captured and searchable within 15 minutes of a meeting ending.
- Improve handover quality when consultants rotate off projects.
- Reduce instances of missed or contested action items in client engagements.

### What success looks like (metrics)

| Metric | Baseline | Target |
|---|---|---|
| Time spent on meeting notes per consultant per week | [to be measured] | < 30 minutes |
| % of meetings with captured action items in Meridian | ~30% (estimated) | > 80% |
| User adoption (Meridian DAU from meeting feature) | 0 | [TBD — agree with Marcus] |
| Summary accuracy rating (user-submitted feedback) | N/A | > 4.0 / 5.0 |

---

## 3. Who This Is For

**Primary user:** Mid-level to senior consultants (Manager and above) at Luminary Group who regularly run or attend client meetings.

**Secondary user:** Project Leads who need visibility into meeting outcomes across multiple workstreams without attending every call.

**Out of scope for v1:** External clients, contractors, and anyone outside Luminary's Google Workspace domain.

---

## 4. User Stories

**As a consultant, I want to...**

- Join a meeting and have it automatically transcribed, so I don't have to take notes while trying to be present in the conversation.
- Receive a structured summary of the meeting with action items highlighted, so I can send a follow-up to the client within minutes of hanging up.
- Search past meeting summaries by project, client, or topic, so I can quickly find context when picking up work or preparing for a follow-up call.

**As a Project Lead, I want to...**

- See a feed of recent meeting summaries across my project, so I stay informed about progress and commitments without needing to attend every call.
- [Add user story here]

---

## 5. Functional Requirements

### 5.1 Meeting capture

- The system shall support automatic transcription of meetings held in **Microsoft Teams** and **Zoom**.
- Transcription shall begin automatically when a Meridian-linked meeting starts, without requiring manual action from the host.
- Participants shall receive a visible notification at the start of the meeting that it is being transcribed.
- Audio shall be retained for **30 days** after a meeting, after which only the transcript and summary are stored.

### 5.2 AI summarisation

- After a meeting ends, the system shall generate a structured summary including:
  - Key discussion points (3–5 bullet points)
  - Decisions made during the meeting
  - Action items, with owner name and due date where stated aloud
- Summaries shall be available within 15 minutes of meeting end.
- The meeting host shall be able to review and edit the generated summary before it is shared to the project workspace.

### 5.3 Workspace sync

- Meeting summaries shall be automatically added to the relevant Meridian project workspace upon host approval.
- Project matching shall use the meeting title and calendar invite metadata (e.g. project tags, attendee lists).
- [Define fallback behaviour when no project match can be determined]

### 5.4 Notifications

- The meeting host shall receive a Slack notification when the summary is ready for review.
- [Define notification preferences — opt-in vs opt-out? Confirm with Priya re: UX implications]

---

## 6. Out of Scope (v1)

- Real-time transcription displayed during the meeting itself
- Speaker identification (attributing specific quotes to named individuals)
- Integration with client-side tools (e.g. a client's own Confluence, Jira, or SharePoint instance)
- Mobile app support
- Support for phone-based dial-in calls where no digital audio stream is available

---

## 7. Open Questions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | What is the legal and compliance position on recording client calls without explicit consent in each jurisdiction? | Sarah Chen / Legal | Open |
| 2 | Which meeting platforms should we prioritise in v1 — Teams or Zoom, or both? | Sarah Chen / Marcus Webb | Open |
| 3 | How should the system handle meetings where some participants are outside Luminary's Google Workspace domain? | Marcus Webb | Open |
| 4 | [Add your question here] | | |

---

## 8. Assumptions & Dependencies

- Luminary Group's primary meeting platform is Microsoft Teams, with some Zoom usage for specific client accounts.
- The AI summarisation capability will be provided by a third-party API (vendor shortlist under evaluation — see Decision 1 in decisions log).
- Meridian's project workspace structure is stable enough to support automated meeting assignment without frequent schema changes.
- Legal sign-off on the recording consent approach is obtained before any user testing with real client meetings.

---

## 9. Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Low consultant adoption due to discomfort with being recorded | Medium | High | [To be defined] |
| AI summaries inaccurate enough to damage trust with clients | Medium | High | [To be defined] |
| [Add risk here] | | | |

---

*This document is a working draft. Feedback and edits welcome — please leave a comment or reach out to Sarah Chen directly.*
