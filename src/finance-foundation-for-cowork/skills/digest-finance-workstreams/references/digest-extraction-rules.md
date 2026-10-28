# Digest extraction rules and template

## Workstream definition card

Before searching, fix one definition per workstream. Reuse it on every run of a recurring digest and show it in the About section.

| Field | Example |
|---|---|
| Workstream name | FY27 Q3 close |
| Keywords and codes | "Q3 close", "P09", "WD3", "flux", "recs", project code FIN-221 |
| People | Owners and regular participants by name and role (work identities only) |
| Mail scope | Folders, distribution lists, subjects |
| Teams scope | Named chats and channels (team and channel names) |
| Calendar scope | Meeting series titles, organizers |
| Related files | Close tracker, PBC list, budget tracker, deal tracker locations (for linking, not for re-analysis) |
| Window | Start and end date-time with time zone; recurring digests use "since the previous digest" |
| Exclusions | Personal, HR, legal-privileged threads the user names |

## Item types

| Type | Definition | Evidence required |
|---|---|---|
| Decision | A choice stated as made by someone with authority to make it ("approved", "agreed", "we will", "go with option B") | Message or meeting where it was stated; who stated it |
| Open item | A task, question or issue raised and not shown as completed | The message raising it; latest message about it |
| Deadline | A dated commitment or due date | Explicit date, or a relative date resolved against the message's sent date |
| Risk | A stated concern that could delay or change an outcome ("may slip", "auditor not comfortable", "system cutover at risk") | The message stating it; who raised it |
| Awaiting you | A direct question, request or approval addressed to the user and not answered by the user in the window | The message; the time it has been waiting |
| Update | A notable status change without a decision (e.g. "recs 80% complete") | The message |

## Status labels

| Label | Rule |
|---|---|
| Decided | Decision recorded; no later message reverses it |
| Reopened | A later message questions or reverses an earlier decision; both cited |
| Open | Raised, not shown as done |
| Done | A later message, tracker update or meeting note shows it completed |
| Overdue | Open and the deadline is before the digest end date-time |
| Due soon | Open and the deadline falls within the next 5 business days after the digest end, unless the user sets another horizon |
| At risk | Open with a stated risk, a slipped interim date, or no owner and a deadline inside the horizon |
| Awaiting you | Addressed to the user and unanswered by the user |
| Unclear | Evidence is contradictory or insufficient; both sources cited |

## Owner rules

- **Stated** — a person accepted it ("I'll take this") or was assigned by someone with authority ("Priya to own").
- **Inferred** — the person most recently asked to act, without acceptance; shown as "Inferred — <name>".
- **No owner** — no assignment found; this alone makes an item with a deadline At risk.

## Deduplication and recency

- Group messages by thread, chat, channel thread and meeting; one item may appear in several places — merge them and cite every location.
- The latest dated evidence governs the status; earlier evidence is retained in the citation list.
- A forwarded or quoted message is cited once, at its original source.
- Meeting invitations alone are not decisions; meeting notes, recaps or transcripts may be.

## Relative date resolution

Resolve phrases against the message's sent date and the user's time zone: "tomorrow", "EOD Friday", "by WD3" (using the Finance Profile workday convention and close calendar), "next week" (the Monday-to-Friday week following the sent date). If the phrase cannot be resolved with certainty, show the phrase as written and mark the deadline "Unresolved".

## Digest template (per workstream)

```
<Workstream name> — digest for <start> to <end> (<time zone>)
Sources read: <n> emails, <n> chat messages, <n> channel posts, <n> meetings

Headline: <one sentence on state of the workstream, evidence-based>

Awaiting you
| Item | From | Since | Due | Link |

Decisions
| Decision | Made by | When | Source |

Open items
| Item | Owner (Stated / Inferred / No owner) | Due | Status | Source |

Deadlines next <horizon>
| Date | What | Owner | Status |

Risks
| Risk | Raised by | Impact stated | Source |

Changes since last digest (recurring only)
- New, closed, reopened, slipped items

Coverage and gaps
- Sources not accessible, channels excluded, items marked Unclear
```

Each Source cell carries the sender, date and a link or locator (mail subject and date; chat or channel name and date; meeting title and date).
