# Mini Issue Tracker — approved low-fidelity design brief v1.1 (updated 2026-11-24; v1.0 approved 2026-10-22)

**Status:** APPROVED (Consolidated implementation contract based on S1 requirements and approved human decisions D-01–D-10; D-09 and D-10 added 2026-11-24).  
**Source Baseline:** `SD_Spec.docx` (§1–§8), `01_Input_Pack_v1.0.md`, `Decision_Log.md` (D-01–D-08 approved 2026-10-22; D-09, D-10 approved 2026-11-24).  
**Target Environment:** Figma Design (Starter Plan, Figma Agent launcher, editable native layers).  

---

## Purpose and scope
Internal desktop web issue tracker for one small team. Include US-01–US-08 only: create, view, assign, prioritize, track status, comment and view important non-closed issues. Use three sample users: Member A, Member B and Lead. They are fictional. Assignee is an issue-specific relationship, not a separate system role.

## Design and output
Create editable native Figma layers on one page. Grayscale, low-fidelity, readable hierarchy, reusable local controls and rows, Auto Layout where practical. Preserve Screen IDs in frame names. Reviewer notes and source references stay OUTSIDE product frames in REF-01. No decorative page icons or empty square placeholders.

Create canonical frames plus compact state examples, not a full screen for every role/status combination. Prototype navigation is annotated only; do not wire interactions or implement an application.

## S-01 — Authentication boundary [BR-01; D-02]
A neutral boundary block labeled “Authentication entry — mechanism TBD”. No login method, fields or social-login controls. This is not working authentication. The demo starts from S-02 as an already authenticated user.

## S-02 — Issues List [US-02; US-05; US-08; D-01]
Header: Issues List and Create Issue action. Tabs: All Issues / Important Issues. Rows show ID, Title, Status, Priority, Assignee if assigned. Title opens details. No row-selection checkboxes.

Show S-02-A All Issues, S-02-B Important Issues and S-02-C Empty. These are states of ONE product screen. They may use separate frames for demonstration. Empty All Issues means zero registered issues (demonstration copy: "No issues yet."). Empty Important means issues exist but none matches the Important rule (demonstration copy: "No important issues found."); it is the same S-02 list state, not a new screen.

Important = (priority is High or Critical) AND status != Closed. Resolved High/Critical issues stay included. Low, Normal, unset priority and every Closed issue are excluded. Reuse the same issue IDs/data across list states.

Sample rows (v1.1 — the fixture set actually used in the Figma mockup and prototype):
- ISS-101 Resolved / High / Member A
- ISS-102 Closed / Critical / Member B
- ISS-103 Open / Not Set / unassigned
- ISS-104 In Progress / Normal / Member A
- ISS-105 Open / Low / Member B
- ISS-106 Open / Not Set / unassigned — prepared new-issue result after Create [D-10]
- ISS-107 Open / Critical / Member B

Important contains ISS-101 and ISS-107 only (ISS-106 is shown only as the post-create result).

> v1.0 of this brief listed an illustrative set ISS-001…ISS-008. The mockup was built with ISS-101…ISS-105 and extended on 2026-11-24 with ISS-106 (Create result, D-10) and ISS-107 (Critical + Open, so that the Critical branch of the Important rule is visible). The Important rule itself is unchanged.

## M-01 — Create Issue overlay [US-01; D-01/04]
Inputs: Title, required; Description, required multiline. Actions: Create and Cancel. Only these two issue fields are editable here.

After success: generated ID, Open status, absent priority shown as Not Set, unassigned assignee, current authenticated author, generated creation time. Do not expose these defaults as inputs.

Show default, missing-Title and missing-Description examples. Invalid submission does not create an issue. Preserve the source example “Title is required”; other working validation copy is a design choice, not a new source requirement.

## S-03 — Issue Details [US-02–US-07]
Show ID, Title, Description, Status, Priority, Assignee, Author, Created at. Unassigned/Not Set are empty-value display states, not extra metadata. Provide Return to Issues List.

Keep Assignee, Priority and Status controls together without a decorative “Control Actions Area” heading. Do not duplicate editable and read-only versions of the same value unnecessarily. Canonical examples: Lead viewing unassigned ISS-103 — assignment and priority enabled, each with an Apply action (`Reference · Permissions and controls`); Lead who is not the assignee viewing ISS-105 — status controls disabled (`S-03 · Team Lead non-assignee`).

Only Lead can assign/reassign one team member and set/change priority [US-03; BR-06; D-04]. Member controls are disabled [D-05]. Selection is applied with an Apply action adjacent to that control; the visible result remains on S-03 [D-06].

Priority display: Not Set, Low, Normal, High, Critical. Selectable levels: Low, Normal, High, Critical only. Not Set represents absence, not a selectable level or a reset action [BR-04/05; D-03].

Only the current assignee can change status, including for Lead [AC-07.4]. Allowed transitions only: Open -> In Progress; In Progress -> Resolved; Resolved -> In Progress; Resolved -> Closed [BR-08.1]. In Closed there is no next status action. Show current status but do not offer it as a new transition. Resolved is resolved but not closed [BR-09.1]. Do not infer that Closed disables unrelated features.

Comments: Comment input, Add Comment action, saved entries with text, author and creation date/time. Empty submission shows validation and creates nothing. Save failure shows an error and no saved comment. Include ready, validation, saved and failure examples [AC-06.1–AC-06.5].

## REF-01 — state reference outside product frames
Show all four contexts: Member non-assignee; Member assignee; Lead non-assignee; Lead assignee. Represent assignment/priority/status control availability for each. Also show all four status examples including In Progress, with valid destinations only. No assignee means no user can change status before assignment.

Use compact components or annotated examples; do not create 16 complete detail screens. Visible annotations specify the test actor, issue ID and current status; they are not product controls or a role-switcher feature.

## Navigation intent [D-01/02/07/08]
S-02 tabs switch list states; issue Title opens its S-03; Create Issue opens M-01; Cancel returns to the calling state; successful Create shows the prepared new issue S-03; Return restores the prior list state (prototype limitation allowed by D-07: Return may go to S-02-A). Assignment, priority, status and comments remain on S-03 after success. Invalid operations do not show a success state. These are design intentions, not working persistence.

## Exclusions
No title/description editing after creation, deletion, attachments, AI features, dashboards, analytics, notifications, search, sorting, pagination, user administration, user-visible history, extra issue metadata, multi-assignee, extra status/priority values or transitions, invented login method, row selection, bulk actions, branding or decorative imagery. No separate product screens for assignment, priority, status, comments or Important Issues.

## Completion report
In the same Agent response report created frames, actual reusable components and unrepresented rules/states. State uncertainty instead of claiming full compliance. A static wireframe does not prove authentication, server permissions, saved data, response time, HTTPS or backup.
