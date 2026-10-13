# Lab Manual Manifest

Source of truth for which lab version is current and what changed between revisions.

**How this folder works:**

- **Current files sit at the top** of `lab-manual/` with stable, un-versioned filenames (`Lab 01 - Participant.docx`, `Lab 01 - Instructor Notes.docx`). These are what you open for delivery, smoke-testing, and sharing.
- **Every prior revision is preserved in** `lab-manual/archive/` with its full versioned filename intact.
- **This manifest is the single source of truth** for which revision each "current" file corresponds to and what changed between revisions.

Whenever a new revision is produced, the old current file moves to `archive/` with its versioned name, the new file takes the stable "current" name, and this manifest is updated.

---

## Current labs

| Lab | Participant guide | Instructor Notes | Current revision | Last updated | Status |
|-----|-------------------|------------------|------------------|--------------|--------|
| Lab 01 — Extend Case for Multi-Agency Intake | `Lab 01 - Participant.docx` | `Lab 01 - Instructor Notes.docx` | v0.7 r9 | 2026-10-09 | Round 9 cross-lab sweep + new Part 6.5 to clean up the Case Layout's Related Lists section |
| Lab 01.5 — Load MTA Sample Data | `Lab 01.5 - Participant.docx` | `Lab 01.5 - Instructor Notes.docx` | v0.7 r1 | 2026-10-13 | New 10-min mini-lab. Uses native Data Import Wizard to bulk-load 4 Accounts + 4 Contacts + 10 Cases. CSVs on workshop site. Fits between Lab 1 and Lab 2 in the Day 1 agenda. Addresses the concept doc's Data Ingestion session. |
| Lab 02 — Lightning App Builder & Dynamic Forms | `Lab 02 - Participant.docx` | `Lab 02 - Instructor Notes.docx` | v0.7 r6 | 2026-10-09 | Round 9 cross-lab sweep: Day 1 removed, API names → labels, "Where you should be" removed, em dashes swept |
| Lab 03 — Asset Hierarchy for MTA Infrastructure | `Lab 03 - Participant.docx` | `Lab 03 - Instructor Notes.docx` | v0.7 r3 | 2026-10-09 | Round 9: new Part 3.6 adds Work Orders related list to Asset Layout (Lab 4 prerequisite) + cross-lab sweep |
| Lab 04 — Field Service Foundations | `Lab 04 - Participant.docx` | `Lab 04 - Instructor Notes.docx` | v0.7 r3 | 2026-10-09 | Round 9 big restructure: Part 2.1 trims Work Type Layout, Part 3.2 removal list matches actual Pronto layout, Part 3.3 four-section target layout, Part 5.3 removed, cross-lab sweep applied |
| Lab 05 — Service Disruption Custom Object | `Lab 05 - Participant.docx` | `Lab 05 - Instructor Notes.docx` | v0.7 r3 | 2026-10-09 | Fields grew from 6 → 9: added Disruption Start Date/Time, Disruption Cleared Date/Time, Duration (Minutes) formula. Part 3 time 18 → 25 min; lab total 68 → 75 min. New Timing section in Part 5 layout. |
| Lab 06 — Platform Showcase | `Lab 06 - Participant.docx` | `Lab 06 - Instructor Notes.docx` | v0.7 r12 | 2026-10-11 | Round 19 big batch (25+ items): Part 3.4 h3 subsections + Public_Description__c + Record ID picker drill + new Confirmation Screen (3.4.6); Part 3.6 rewrote as Dynamic Actions upgrade flow; Part 4.1 switched to Confirm-field (Publish Status now built in Lab 5 r4); Part 4.2 keep "Add Submit for Approval button" layouts checkbox checked; Part 4.6 adds Submit for Approval as a Dynamic Action; Part 5.1 Category=All + Update Preview Auto + Service Disruption Number pre-populated; Part 5.2 Save As clone of Report 1; Part 5.3 Private Dashboards folder, Widget 2 = Vertical Bar. 110 → 115 min. |
| Lab 07 — Agentforce Dispatcher Assistant | `Lab 07 - Participant.docx` | `Lab 07 - Instructor Notes.docx` | v0.7 r2 | 2026-10-11 | Round 2 feedback (15+ UI corrections after smoke-test build in v3): Part 2 Flow Builder label/UI alignment; Part 3 restructured (no Clone, new agent create flow, Topics→Subagents, Reasoning Instructions, alphabetical input/output ordering); new Part 3.5 Grant Agent Access via Permission Set (the critical blocker). |
| **Day 2 Closing** — Executive Scenario Simulation | — | `Executive Scenario Simulation.docx` | v0.7 r1 | 2026-10-12 | Facilitator script for the 50-min Day 2 afternoon live-fire exercise. Four timed injects (Hudson Line signal fault, Case escalation, LIRR Jamaica P1, Hudson Line resolve). No Participant guide (narrated live). Addresses the concept doc's Executive Scenario Simulation session. |

Note on Instructor Notes addenda not in the versioning table:
- Lab 06 Instructor Notes r12 (same version as above) gained an optional 10-min "AI-assisted Flow development demo" opening in Part 2 on 2026-10-12. Addresses the concept doc gap on AI-as-developer-productivity-tool (vs. AI-as-feature only). See the "Optional opening: AI-assisted Flow development demo" section inside Part 2.

---

## Supporting files in this folder

- `lab-authoring-feedback.md` — living log of feedback Tim has given on lab content. Principles become inputs to future lab authoring; corrections become to-do items for revision passes.
- `.scratch/` — Python builder scripts used by Claude to generate the .docx files from code. Internal, not for sharing.

---

## Lab 07 revision history

### v0.7 r2 — 2026-10-11
**Change:** Round 2 feedback batch (15+ items) applied after Tim's full smoke-test build in the v3 reference org. Mostly Agentforce Builder UI reality corrections.
- Part 2.1: removed non-existent "Start From Scratch" selection screen; pick Autolaunched Flow directly after New Flow.
- Part 2.3: field label `SObject Type Name` (not `SobjectType`); field label `Record Type Name` (not `DeveloperName`); no `Done` button at the end — close via the X on the element card or click + to continue.
- Part 2.4: when the Manually option is selected on `How to set record field values`, the `How Many Records to Create` option is hidden; step removed. Field label `Record Type ID` (not `Id`). The `$Flow.CurrentDateTime` resource picker drill goes through `Running Flow Interview > CurrentDateTime` (new wording spells this out).
- Part 2.7 and Part 2.9: picker drill labels use the space-form `Outputs from Generate Rider Message` (not the underscore-form `Outputs from Generate_Rider_Message`).
- Part 3 title: `Create the agent and add the File Service Disruption Action` (was `Clone the agent`). Clone is no longer available in current Builder UI.
- Part 3.3 Inputs: reordered alphabetically to match UI (`affectedLine, agencyRecordType, description, headline`).
- Part 3.3 Outputs: reordered alphabetically to match UI (`draftedMessage, newSDName`).
- Part 3.3 Save: removed non-existent `Save on the action detail view` step; saves on inputs/outputs happen automatically, final Save is at the Agent level.
- Part 5.1 stretch: `$Flow.CurrentDateTime` drill wording updated to match Part 2.4.
- Participant time unchanged (~70 min with stretch, 60 min without).
**Files archived:** `Lab 07 v0.7 r2 - Agentforce Dispatcher Assistant (Participant).docx`, `Lab 07 v0.7 r2 - Agentforce Dispatcher Assistant (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-11
**Change:** Initial build.
- Three design decisions anchor the lab: (1) MTA Dispatcher persona (not external riders), (2) agent completes the end-to-end disruption lifecycle as the "wow moment", (3) agent panel inside Salesforce as the delivery surface. Chose "one Flow Action does the whole lifecycle" over multi-action chaining, and "agent asks a follow-up question" (slot-filling) over inference-with-confirmation.
- Lab structure (~70 min with stretch, 60 without): Part 1 Agent panel prerequisites (5 min); Part 2 File Service Disruption autolaunched Flow — 7 elements including Get Agency Record Type, Create SD, Get Created SD, Generate Rider Message, Update Rider Message, Set Outputs, Submit for Approval core action (25 min); Part 3 Clone Pronto Merchant Management Agent to MTA Dispatcher Agent, create Service Disruption Management Topic with slot-filling + agency inference instructions, add File Service Disruption Action (20 min); Part 4 Test wow moment with full-sentence path then slot-filling path (15 min); Part 5 Stretch Resolve Disruption action (10 min, optional); Part 6 Where to go next tour of Summarize/Notify/Proactive patterns (5 min); Final Verification (5 min).
- Reuses Lab 6's Rider Facing Message Generator prompt template as the Action's AI step. Reuses Lab 6's Approval Process as the Submit for Approval target. Lab 7 is pure composition on top of what Labs 1-6 built.
- Not yet smoke-tested against v3 (MCP server allowlist constraint; `mta_workshop` not currently reachable from Claude). Tim will smoke-test the finished draft and feedback becomes r2.
**Files archived:** `Lab 07 v0.7 r1 - Agentforce Dispatcher Assistant (Participant).docx`, `Lab 07 v0.7 r1 - Agentforce Dispatcher Assistant (Instructor Notes).docx`.

## Lab 06 revision history

### v0.7 r12 — 2026-10-11
**Change:** Round 19 big batch (25+ items) from Tim's smoke test against v3.
- Part 2 (Flow): formula box wording fixed ("In the formula box where it says 'Enter formula...'"); added the "Only when a record is updated to meet the condition requirements" radio button; filter block clarified with explicit two conditions (Service_Disruption__c Equals + Status Does Not Equal Closed); Record ID picker drill spelled out (Quick Resources > Triggering Service Disruption > Record ID).
- Part 3.4 (Screen Flow): "Step N:" paragraphs converted to proper h3 subsections (3.4.1 through 3.4.7). Public_Description__c now used throughout (was Description__c). Update Records has a Label (Update Rider Message), field is "Record ID" not "Id", picker drill is spelled out. New 3.4.6 Confirmation Screen so users see "The Rider-Facing Message has been updated" before Finish. Tip callout relocated above the "For each of these four fields" step; "Click Save & Preview" → "Click Preview".
- Part 3.6: rewrote as a Dynamic Actions upgrade flow (Upgrade Now > Migrate > Service Disruption Layout > Finish > Add Action > Draft Rider Message > drag to top > Save). This is the real UX; previous r11 wording assumed static Highlights actions.
- Part 4.1: no longer creates Publish Status (that field is now built in Lab 5 r4). Lab 6 Part 4.1 is just a confirm-field pass.
- Part 4.2: added the step about keeping the "Add Submit for Approval button to all Service Disruption page layouts" checkbox checked after Save.
- Part 4.6: because the Highlights Panel is now Dynamic Actions, Submit for Approval must also be added as a Dynamic Action alongside Draft Rider Message. New steps spell this out.
- Part 5.1: added Category = All click (so Service Disruption Report Type appears); Update Preview Automatically toggle ON; noted Service Disruption Number is pre-populated.
- Part 5.2: switched to Save As clone of Report 1 (rather than New Report from scratch).
- Part 5.3: folder = Private Dashboards (was Public); Widget 2 chart type = Vertical Bar (was Horizontal).
- Participant time: 115 min (was 110). The confirmation screen in 3.4.6, the Dynamic Actions upgrade in 3.6, and the Submit for Approval Dynamic Action in 4.6 add roughly 5 min.
**Files archived:** `Lab 06 v0.7 r12 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r12 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r11 — 2026-10-11
**Change:** Final Verification Check 1 was stale from the r2→r3 Validation Rule swap. r11 corrects it.
- OLD Check 1: "Try to save a Service Disruption with Status = Cleared and Rider-Facing Message empty. Save should fail." That rule (Require_Rider_Message_When_Cleared) was removed in r3 and replaced with Cleared_After_Started.
- NEW Check 1: open SD-00001, edit, set Disruption Cleared Date/Time earlier than Disruption Start Date/Time, verify Save fails with the error message, correct the Cleared time, verify Save succeeds.
- Rest of Lab 6 was already consistent with the Cleared_After_Started rule; only Final Verification was out of sync.
**Files archived:** `Lab 06 v0.7 r11 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r11 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r10 — 2026-10-11
**Change:** Part 5.3 Dashboard builder rewritten to match the Add Widget UI shown in Tim's screenshot.
- Section renamed from "two components" to "two widgets" to match Lightning Dashboard terminology.
- Dashboard creation steps: open Dashboards tab, New Dashboard, name, Create. Empty grid canvas opens.
- Widget creation: click + Add Widget (not + Component), pick Chart or Table from the widget-type dropdown (not Text/Image/LWC), configure Source Report + Chart Type + Measure, click Add to place on canvas.
- Save flow: Save then Done (two separate buttons).
- New Watch Out callout: widget type dropdown has four options; Chart or Table is the one for report-sourced visualizations.
- Instructor Notes gain a teaching moment distinguishing widget types and clarifying that "widget" is modern Lightning dashboard terminology (not "component").
**Files archived:** `Lab 06 v0.7 r10 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r10 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r9 — 2026-10-11
**Change:** Part 5 Report Builder steps rewritten to match the Outline tab UI.
- Report 1 and Report 2 Group Rows and Columns steps now use explicit Outline tab navigation: GROUP ROWS "Add group..." search picker and Columns "Add column..." search picker. Each column added one at a time.
- Filter step references the Filters tab explicitly as a sibling tab to Outline.
- Instructor Notes gain a teaching moment distinguishing Outline (shape) from Filters (narrow) tabs.
**Files archived:** `Lab 06 v0.7 r9 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r9 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r8 — 2026-10-11
**Change:** Part 4.2 Step 7 (Approval Process Entry Criteria + Approver) rewritten to match the Jump Start Wizard UI shown in Tim's screenshot.
- Entry Criteria: explicit substeps for Field = Service Disruption: Rider-Facing Message, Operator = not equal to, Value = EMPTY (not the word "blank").
- New Watch Out callout: do not type the word "blank" into the Value field.
- Select Approver: explicit substeps for the "Automatically assign to approver(s)" radio, User dropdown default, self as approver via lookup icon, "FIRST response" default.
- Instructor Notes gain a teaching moment about the empty-Value idiom used throughout Salesforce filter builders ('not equal to + empty Value' means 'not blank'), plus a common error for typing "blank" into the Value field.
**Files archived:** `Lab 06 v0.7 r8 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r8 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r7 — 2026-10-11
**Change:** Part 3.4 Step 4 (Default Value on Draft Rider Message Long Text Area) refined with a picker drill.
- Old single step: "Default Value: {!Generate_Rider_Message.Prompt_Response}."
- New three sub-steps: (a) click into the Default Value resource picker, (b) under the Action section, click Outputs from Generate_Rider_Message, (c) click Prompt Response.
- Instructor Notes gain a teaching moment framing resource picker drills as a recurring pattern throughout Flow Builder, with the Entire Resource vs field drill (Step 3) and the Outputs from Action drill (Step 4) as the two canonical examples in Part 3.4.
**Files archived:** `Lab 06 v0.7 r7 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r7 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r6 — 2026-10-11
**Change:** Part 3.4 Step 3 (Action input mapping) refined to match the actual Flow Builder resource picker UI.
- Old single step: "map it to {!Get_Service_Disruption}."
- New three sub-steps: (a) click into the resource picker, (b) under the Get Records section, click Service Disruption from Get_Service_Disruption, (c) in the next picker view, click Entire Resource (not a single field drill).
- Instructor Notes gain a teaching moment distinguishing Entire Resource (whole record) from Relationship Fields (single field) in the picker, plus a Common error for drilling to a specific field by mistake.
**Files archived:** `Lab 06 v0.7 r6 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r6 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r5 — 2026-10-11
**Change:** Part 3.4 Screen Flow structure corrected. The old Step 9 told participants to map the Service Disruption input to {!$Record}, but Screen Flows don't have $Record (that's only available in Record-Triggered Flows).
- Part 3.4 restructured into six labeled sub-steps: (1) recordId input variable, (2) Get Records element to retrieve the Service Disruption using recordId, (3) Action element mapping Service Disruption input to {!Get_Service_Disruption}, (4) Screen element with Long Text Area pre-populated by AI output, (5) Update Records to write the final draft back, (6) Save and Activate.
- Misleading {!$Record} reference removed entirely.
- Instructor Notes add a teaching moment distinguishing Screen Flows from Record-Triggered Flows (the former has no $Record), plus a new Common error for the Action input mapping failing.
- Lab total time unchanged (110 min).
**Files archived:** `Lab 06 v0.7 r5 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r5 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r4 — 2026-10-11
**Change:** Part 3 Prompt Builder steps rewritten to match actual UI (per screenshots from Tim's smoke-test).
- **3.1** rewritten as a single-page New Prompt Template modal walkthrough. Flex type, Name, API Name, Description, then Inputs section where Service Disruption is attached with Require when template runs checked. Click Next (not Click Create).
- **3.2** rewritten to reflect three-pane editor (Template Details sidebar / Prompt pane / Resolved Prompt + Generated Response). Teaches Insert Resource button for merge fields instead of hand-typing. Four field inserts (Headline, Description, Affected Line, Severity). Model section explicitly left at defaults (Standard, GPT 5 Mini).
- **3.3** preview flow rewritten: Save & Preview button, right-sidebar panes activate, preview input panel asks for SD-00001.
- Instructor Notes gain three new teaching moments: Insert Resource button, three-pane editor mental model, and expanded error handling.
- Lab total time unchanged (110 min). Changes clarify click paths without adding steps.
**Files archived:** `Lab 06 v0.7 r4 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r4 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r3 — 2026-10-09
**Change:** Timestamp/Duration fields moved from Lab 6 to Lab 5's data model (per feedback). Lab 6 Part 1 shrinks accordingly.
- Removed Part 1.1 (Add Started/Cleared timestamp fields) — now in Lab 5 r3 Part 3.
- Removed Part 1.5 (Add Duration (Minutes) formula field) — now in Lab 5 r3 Part 3.
- Renumbered Part 1 subsections: old 1.2 → new 1.1 (Open Validation Rules), old 1.3 → new 1.2 (Build rule), old 1.4 → new 1.3 (Test).
- 1.1 nav preamble added with explicit "From Setup, Object Manager, Service Disruption, Validation Rules" guidance.
- All field name references updated throughout: Started DateTime → Disruption Start Date/Time, Cleared DateTime → Disruption Cleared Date/Time. API names updated to Disruption_Start_Date_Time__c and Disruption_Cleared_Date_Time__c.
- Lab total time: 120 min → 110 min.
**Files archived:** `Lab 06 v0.7 r3 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r3 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r2 — 2026-10-09
**Change:** Mid-build feedback from Tim: MTA Operations wants to measure disruption duration for responsiveness and process efficacy. Scope expanded.
- Part 1 Validation Rule changed from Require_Rider_Message_When_Cleared to Cleared_After_Started. The Rider-Facing Message governance moves fully to the Approval Process in Part 4.
- New Part 1.1 adds Started DateTime and Cleared DateTime fields on Service Disruption.
- New Part 1.5 adds Duration (Minutes) formula field computing (Cleared - Started) * 24 * 60.
- Part 5 adds Report 2 (Average Disruption Duration by Agency) grouped by Record Type with Duration summarized as Average.
- Part 5 Dashboard adds a second component (Average Duration by Agency).
- Final Verification Check 5 updated to reference both dashboard components.
- Estimated time: 115 min → 120 min.
**Files archived:** `Lab 06 v0.7 r2 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r2 - Platform Showcase (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-09
**Change:** First draft of Lab 06, built as the Platform Showcase per Option C from the Day 2 planning conversation.
**Scope (per Tim's decisions):** Validation Rule + Record-Triggered Flow + Quick Action-launched Screen Flow + Prompt Builder Template + Approval Process + Reports + Dashboard. No Agentforce agent itself in this lab (that's deferred to the Day 2 Where-to-go-next tour). No Agentforce Vibes (Decision 2b).
**Structure:**
- Part 1: Validation Rule (Require Rider Message when Cleared) — superseded in r2
- Part 2: Record-Triggered Flow (escalate related Cases when SD Status = Active)
- Part 3: Prompt Template + Screen Flow + Quick Action (Draft Rider Message)
- Part 4: Approval Process (Rider Message approval, gate on Publish Status)
- Part 5: Report + Dashboard
- Final Verification: 5 checks
**Estimated time:** 115 min.
**Pedagogical arc:** This is where the data model becomes a working platform. Six capabilities on top of Service Disruption: data integrity, automation, AI content generation, human-in-the-loop governance, operational visibility.
**Files archived:** `Lab 06 v0.7 r1 - Platform Showcase (Participant).docx`, `Lab 06 v0.7 r1 - Platform Showcase (Instructor Notes).docx`.

---

## Lab 05 revision history

### v0.7 r3 — 2026-10-09
**Change:** Three fields moved from Lab 6 into Service Disruption's data model.
- Field 7 (new): Disruption Start Date/Time (Date/Time) — when the disruption was declared.
- Field 8 (new): Disruption Cleared Date/Time (Date/Time) — when the disruption was fully cleared.
- Field 9 (new): Duration (Minutes) (Formula, Number, 0 decimals) — computes (Disruption Cleared Date/Time − Disruption Start Date/Time) × 24 × 60.
- Part 3 field count: 6 → 9. Part 3 time: 18 min → 25 min.
- Part 5 Service Disruption Layout: new Timing section (2-Column) added between Communication and System Information. The three new fields go there.
- Field creation FLS/Page Layouts step wording clarified: "For the 'establish field-level security' page, click Next to accept the defaults. For the 'add to page layouts' page, click Save & New (or Save for the last field) to accept the defaults."
- Lab total time: 68 min → 75 min.
**Files archived:** `Lab 05 v0.7 r3 - Service Disruption Custom Object (Participant).docx`, `Lab 05 v0.7 r3 - Service Disruption Custom Object (Instructor Notes).docx`.

### v0.7 r2 — 2026-10-09
**Change:** Round 10 feedback — 25-item batch from Tim's smoke-test of r1.
**Participant guide rewritten top to bottom.** Highlights:
- "walk through" phrasing throughout (replacing "walk").
- Standard-fit test headers: "Could the Case object...", "Could the Asset object...", "Could a Knowledge article...", "Could the Work Order object..."
- 1.5 header: Conclusion (not Conclude).
- Part 2.2 step 8 highlighted in orange so the "Launch New Custom Tab Wizard" checkbox doesn't get missed.
- Part 2.3 radio button and checkbox verbs spelled out explicitly.
- Part 3.1 opener rewritten: open ServicePulse 360 app → click Service Disruptions tab → gear icon → Edit Object. Natural positioning.
- Each field creation now has its own h3 subsection with every click spelled out (radio button for picklist values, Use first value as default, Un-check Restrict picklist, Required, Auto add to custom report type, Next on FLS, Save & New or Save on Page Layouts).
- Field 4 renamed from Public Description to Description. Field 4 type: Text Area (Long).
- Part 3.2 adds a Why for Record Types and guides the user to Object Manager first.
- Part 3.2 Make Available step softened: keep checked, scroll down to verify System Administrator.
- Part 3.2 B&T: Watch Out callout flags B_T vs BandT Name rendering (manually correct to BandT).
- Part 4.1 lookup Description simplified: "The service disruption this Case is a result of."
- Part 4.1 Dynamic Forms-enabled record page step added between FLS and Page Layouts (this step auto-places the field on the canvas, which previously required a separate Part 4.2).
- Part 4.1 Related List Label step simplified.
- Part 4.1 Verify uses object label ("Case object") instead of API name.
- OLD Part 4.2 (manual Dynamic Forms placement) REMOVED. Redundant with Part 4.1 Dynamic Forms step.
- NEW Part 5 added: Configure the Service Disruption Layout and Lightning record page BEFORE creating any records. Mirrors Labs 3 and 4 layout-first pattern.
- OLD Part 5 (Create disruption + link Golden Case) renumbered to Part 6.
- Part 6.1 field order reordered to Status, Severity, Headline, Description, Rider-Facing Message, Affected Line.
- "Verified? Great job!" callouts no longer have trailing colons.
- Common sticking points moved from a single multi-line callout to proper bullets.
- Estimated time: 60 min → 68 min with the new Part 5.
**Cross-lab sweep applied:** "walk" → "walk through", "Verified? Great job!:" colon removal, Verrazzano spelling. Labs 1-4 scanned clean (issues were new in Lab 5).
**Files archived:** `Lab 05 v0.7 r2 - Service Disruption Custom Object (Participant).docx`, `Lab 05 v0.7 r2 - Service Disruption Custom Object (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-09
**Change:** First draft of Lab 05 (Service Disruption custom object). The one deliberate custom object in the workshop.
**Scope (per Tim's decisions):**
- 6 bare-essential fields: Status, Severity, Headline, Public Description, Rider-Facing Message, Affected Line (Rider-Facing Message is empty by design; Lab 6 Prompt Builder fills it)
- 4 Record Types mirroring Case: NYCT, LIRR, MNR, B&T
- New lookup field on Case: Service_Disruption__c, with "Rider Cases" named related list on the disruption side
- Service Disruption field placed on the Case Dynamic Forms canvas in Part 4.2
**Structure:**
- Part 1: Walk the standard-fit test (Case, Asset, Knowledge, Work Order all fail; custom justified)
- Part 2: Create the custom object + tab (added to ServicePulse 360 app)
- Part 3: 6 fields + 4 Record Types
- Part 4: Case lookup + Dynamic Forms placement
- Part 5: Create a Service Disruption + link Golden Case to it
- Final Verification: 3 checks
**Estimated time:** 60 minutes.
**Pedagogical arc:** This is the lab's "custom is justified" teaching moment. Participants internalize the standard-fit test by walking it on four candidates, then build the custom object as a conscious decision rather than a reflex.
**Files archived:** `Lab 05 v0.7 r1 - Service Disruption Custom Object (Participant).docx`, `Lab 05 v0.7 r1 - Service Disruption Custom Object (Instructor Notes).docx`.

---

## Lab 04 revision history

### v0.7 r3 — 2026-10-09
**Change:** Round 9 feedback — big restructure based on actual Pronto template layout + cross-lab sweep.
- **New Part 2.1:** trim the Work Type Layout before participants create the Signal Repair record. Keep only Work Type Name, Description, Estimated Duration, Duration Type, Owner.
- **Part 2.2 (Create Signal Repair):** removed Timeframe Start/End steps; participants can save after Duration Type = Hours.
- **Part 3.2 (Remove fields):** removal list corrected to match actual Pronto standard layout — just Parent Work Order (temporarily), Service Contract, Contact, Entitlement.
- **Part 3.3 (Target structure):** four clear sections matching Tim's target screenshot. Information (Work Order Number, Priority, Status, Owner, Account, Case). Work Order Details new section (Start Date, End Date, Work Type, Asset). Description (Subject, Description). System Information (Created By, Last Modified By, Parent Work Order re-added here).
- **Part 5.3 removed** (from Work Type to all Work Orders of that type).
- Verify callouts updated to "Verified? Great job!" with exclamation.
- "Day 2 extends this" replaced with "The subsequent hands-on labs extend this."
- **Prerequisite dependency:** Lab 3 r3 adds Work Orders to the Asset Layout's Related Lists section.
- Cross-lab sweep applied: "Day 1" removed from title, object API names replaced with labels, "Where you should be" callouts removed, em dashes replaced with commas in prose.
**Files archived:** `Lab 04 v0.7 r3 - Field Service Foundations (Participant).docx`, `Lab 04 v0.7 r3 - Field Service Foundations (Instructor Notes).docx`.

### v0.7 r2 — 2026-10-08
**Change:** Round 8 smoke-test (Tim, 2026-10-08) found that the Cases related list is NOT available on the WorkOrder page layout. The Case-to-WorkOrder relationship is many-to-one from WorkOrder's side (each WorkOrder references one Case), so there's nothing to list as a child collection.
**Scope:**
- Part 3.4 (Add Cases related list) removed entirely.
- Replaced with a "Why no Cases related list?" callout teaching relationship cardinality: related lists are for one-to-many; the Case field hyperlink on the WorkOrder is the right surface for the many-to-one navigation direction.
- Part 3.5 (Save the layout) renumbered to Part 3.4.
- Instructor Notes gain a new teaching moment about related lists vs lookup hyperlinks and when each is pedagogically correct.
**Files archived:** `Lab 04 v0.7 r2 - Field Service Foundations (Participant).docx`, `Lab 04 v0.7 r2 - Field Service Foundations (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-08
**Change:** First draft of Lab 04 (Field Service Foundations).
**Scope (per Tim's decisions):**
- Tight scope: WorkType creation + minimal WorkOrder Layout + Case-to-WorkOrder escalation + three-way chain verification.
- Lightweight WorkOrder Layout: only required or load-bearing fields (Work Order Number, Subject, Status, Priority, Case, Asset, Work Type, Account, Description, Start Date, End Date, Owner). Everything else trimmed.
- Participant builds the WorkType themselves (Signal Repair).
- Golden Case thread continues: participants escalate their golden Case record into a WorkOrder that inherits the Case's Asset (NYCT Bus 4521) and Account.
- ServiceAppointment, ServiceResource, Skills, ServiceTerritory deferred to Day 2.
**Structure:**
- Part 1: Add Work Orders tab to the ServicePulse 360 app (with fallback)
- Part 2: Create the Signal Repair WorkType
- Part 3: Trim the WorkOrder Layout to the critical fields; add Cases related list
- Part 4: Escalate the golden Case into a WorkOrder (dispatch pattern)
- Part 5: Verify the chain (Case → WorkOrder → Asset → WorkType)
- Final Verification: 3 checks
**Estimated time:** 60 minutes.
**Files archived:** `Lab 04 v0.7 r1 - Field Service Foundations (Participant).docx`, `Lab 04 v0.7 r1 - Field Service Foundations (Instructor Notes).docx`.

---

## Lab 03 revision history

### v0.7 r3 — 2026-10-09
**Change:** Round 9 — new Part 3.6 (Work Orders related list on Asset Layout, Lab 4 prerequisite) + cross-lab sweep.
- **New Part 3.6:** add Work Orders related list to the Asset Layout with columns Work Order Number, Subject, Status, Priority, Start Date. Lab 4 Part 5.2 depends on this.
- Previous Part 3.6 (Save the layout) renumbered to Part 3.7.
- Cross-lab sweep applied: "Day 1" removed, API names → labels, "Where you should be" callouts removed, em dashes swept in prose.
- Estimated time 90 min → 92 min.
**Files archived:** `Lab 03 v0.7 r3 - Asset Hierarchy for MTA Infrastructure (Participant).docx`, `Lab 03 v0.7 r3 - Asset Hierarchy for MTA Infrastructure (Instructor Notes).docx`.

### v0.7 r2 — 2026-10-08
**Change:** Round 7 smoke-test feedback batch. 16 items applied.
**Structural changes:**
- **Part 1:** fallback instructions added for cases where App Manager changes don't propagate to the nav bar immediately. Participants can use the pencil icon to add Assets to the nav bar manually.
- **Part 2:** removed the "Standard Related Lists" instruction that wasn't observable in the UI.
- **Part 3 (new structure):** layout-first. Participants configure the Asset Layout before creating any Assets: add Parent Asset, remove unused fields (Price, Usage End Date, Contact, Competitor Asset, Purchase Date), add Child Assets related list with columns (Asset Name, Serial Number, Account Name, Status), add Related Assets related list with columns (Asset Relationship Number, Related Asset, Relationship Type).
- **Part 4:** just the parent Asset (NYCT Bus 4521).
- **Part 5 (new):** create the four children via the parent's Child Assets related list, which auto-populates Parent Asset. Uses Save & New between children. Each child includes an Install Date.
- **Part 6 (AssetRelationship):** UI label corrections — "Related Assets" (not "Primary Asset Relationships"), Relationship Type = "Replacement", "From Date" (not "Begin Date"). Added honest note that AssetRelationship is unidirectional in the data model.
- **Part 7:** navigate from the Case to the bus via the Asset hyperlink. References "your golden Case record" explicitly.
- **Part 8 (new):** Asset.Cases Related List - Single component drops into the Other related cases tab (created in Lab 2 r5). Previously this was Part 7's inline step.
- Verify callouts throughout replaced with "Verified? Great job. This means..." pattern, followed by Common sticking points where appropriate.
- "Why this matters" expanded to mention Maintenance Plan integration (Asset + WorkOrder auto-scheduling).
- Removed the Asset 02i URL prefix mention.
**Estimated time:** 85 min to 90 min.
**Files archived:** `Lab 03 v0.7 r2 - Asset Hierarchy for MTA Infrastructure (Participant).docx`, `Lab 03 v0.7 r2 - Asset Hierarchy for MTA Infrastructure (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-08
**Change:** First draft of Lab 03 (Asset Hierarchy for MTA Infrastructure).
**Scope:**
- Part 1: Add Assets tab to the ServicePulse 360 app navigation.
- Part 2: Tour the standard Asset object.
- Part 3: Create parent Asset (NYCT Bus 4521) tied to MTA New York City Transit.
- Part 4: Create four component Assets (Battery Pack, HVAC Unit, Drive Motor, Farebox) with Parent Asset = NYCT Bus 4521.
- Part 5: Build an AssetRelationship between Battery Pack and HVAC Unit to demonstrate peer relationships.
- Part 6: Connect the Golden Record (from Lab 1 Part 10) to NYCT Bus 4521 via the standard Asset lookup on Case.
- Part 7: Add a second Related List - Single component to the Case record page, pointing at Asset.Cases.
- Final Verification: 3 checks (hierarchy, Case-Asset link, Asset.Cases visible on Case page).
**Estimated time:** 85 minutes.
**Standard-first:** Zero custom fields, zero custom objects. Pattern: Parent Asset for ownership hierarchy, AssetRelationship for peer/qualified relationships, standard Case-Asset lookup for maintenance context.
**Files archived:** `Lab 03 v0.7 r1 - Asset Hierarchy for MTA Infrastructure (Participant).docx`, `Lab 03 v0.7 r1 - Asset Hierarchy for MTA Infrastructure (Instructor Notes).docx`.

---

## Lab 02 revision history

### v0.7 r6 — 2026-10-09
**Change:** Round 9 cross-lab sweep only.
- "Day 1" removed from title.
- Object API names replaced with labels in prose.
- "Where you should be" callouts removed throughout.
- Em dashes replaced with commas in prose body text.
- No scope or content changes beyond the sweep.
**Files archived:** `Lab 02 v0.7 r6 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r6 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

### v0.7 r5 — 2026-10-08
**Change:** Round 7 feedback — add a dedicated tab for related cases on the Case Lightning record page.
**Changes:**
- Part 3 restructured: now creates a new tab labeled "Other related cases" on the Case Lightning record page via the Tabs component. The tab goes alongside Feed, Details, and Related.
- The Related List - Single component (Contact.Cases) is placed inside the new Other related cases tab, not on the Details tab.
- Lab 3 r2 will add a second Related List - Single (Asset.Cases) to the same tab.
- Verify callout at end of Part 3 rewritten as "Verified? Great job. This means..." followed by "Common sticking points."
- Check 2 references the new tab explicitly.
- Estimated time increased from 55 min to 60 min.
**Files archived:** `Lab 02 v0.7 r5 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r5 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

### v0.7 r4 — 2026-10-08
**Change:** Round 5 feedback batch (Tim's smoke-test observations).
**Participant guide changes:**
- Intro text scrubbed of unverifiable assumptions about what Cassie admins do today. Replaced with factual framing of what Dynamic Forms does and why.
- Removed the confusing Priority/Type/Reported Date/Time preamble that previewed which fields would get visibility rules.
- Part 2.1 filter path replaced with the real Advanced-tab clicks: Record > Case Record Type > Name, Operator = Contains, Value = NYCT.
- Part 2.3 switched from "create a second Case of a different Record Type" to "change the Record Type field on the Golden Record itself." Depends on Lab 1 r7 Part 9.4 which adds Case Record Type to the Dynamic Forms canvas.
- Added Watch Out callout in Part 2.3 about Record Type changes triggering automation in production.
- Part 4 (optional second agency) removed entirely. Lab is now Parts 1 through 3 plus Final Verification.
- "After lunch" language removed from What's Next.
- Check 2 success criteria updated to "at least 1 case appears" (reflects the self-referential behavior).
- Opening Part 1 now explicitly directs participants to their Golden Record and confirms it's NYCT before proceeding.
- Estimated time dropped from 65 min to 55 min with Part 4 removal.
**Files archived:** `Lab 02 v0.7 r4 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r4 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

### v0.7 r3 — 2026-10-08
**Change:** Round 5 (Golden Record cross-lab anchor) applied, correcting the Case Comments issue found during smoke-test.
**Scope changes:**
- **Part 3 (Related List - Single):** Swapped from Case Comments to showing Cases related to the Golden Record's Contact (Parent Record = Contact Name, Related List = Cases). Case Comments isn't in the Case Layout's Related Lists section by default on the Pronto template, so the Related List - Single component couldn't pick it. Contact.Cases uses an already-visible relationship and benefits from the Golden Record's guaranteed Contact population.
- **Self-referential behavior:** The Golden Record shows up in its own related list because it IS one of its Contact's cases. This is now called out explicitly as a feature.
- **Prerequisite:** Lab 02 now requires the Golden Record from Lab 1 Part 10 to exist with a populated Contact.
- **All examples:** Lab 02 now consistently uses "your Golden Record" as the demo record rather than "any case."
**Files archived:** `Lab 02 v0.7 r3 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r3 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

### v0.7 r2 — 2026-10-08
**Change:** Round 4 smoke-test corrections. Two edits based on Tim's live testing against v3:
- **Part 2 (Dynamic Forms visibility rule):** Validated as working. No changes.
- **Part 3 (Related List - Single component):** Two corrections. (1) Component name corrected from "Related Record List" (nonexistent) to "Related List - Single" (the actual Lightning App Builder standard component). (2) Demo swapped from Account.Cases to Case Comments because Account.Cases requires every Case to have an Account populated, which isn't guaranteed in production, while Case Comments is bulletproof (every Case can have Case Comments regardless of how it was created). The Related List - Single configuration simplifies as a result: Parent Record stays "Use This Case" (no cross-object traversal), Related List = Case Comments.
- **Prerequisite update:** Lab 02 now explicitly states participants must have placed Reported Date/Time and Resolution Notes on the Case Lightning record page's canvas via Dynamic Forms (which comes from Lab 01 Part 9, pending Lab 01 r6).
- **Instructor Notes:** Added "What changed from r1" callout up top. Expanded Part 3 teaching moments to distinguish the five "related"-named components in the palette so participants don't fumble between them.
**Files archived:** `Lab 02 v0.7 r2 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r2 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

### v0.7 r1 — 2026-10-06
**Change:** Initial draft of Lab 02 (Lightning App Builder & Dynamic Forms).
**Scope (per Tim's decisions):**
- Light depth on Dynamic Forms: one worked visibility rule on one field, NYCT-only.
- Include a Related Records component (previews the Asset relationship pattern in Lab 03).
- Skip utility bar configuration.
- Walk through only one agency (NYCT); Part 4 optional second-agency extension.
- MTA-anchored intro referencing Cassie's form-heavy environment (FOIL, Feedback, CBDTP, TPA Surveys, LIRR Feedback).
**Structure:**
- Part 1: Open the Case record page in App Builder (3 min)
- Part 2: Add field-level visibility rule for NYCT on Reported Date/Time (12 min)
- Part 3: Add Related Record List component (Account.Cases) (10 min)
- Part 4 (optional): Extend to a second agency (8 min)
- Final Verification (5 min)
- Estimated time: 70 minutes
**Files archived:** `Lab 02 v0.7 r1 - Lightning App Builder & Dynamic Forms (Participant).docx`, `Lab 02 v0.7 r1 - Lightning App Builder & Dynamic Forms (Instructor Notes).docx`.

---

## Lab 01 revision history

### v0.7 r9 — 2026-10-09
**Change:** Round 9 cross-lab sweep + new Case Layout cleanup step.
- **New Part 6.5:** Clean up the Case Layout's Related Lists section. Keep Case Comments, Case History, Attachments, Work Orders. Remove the rest (Open Activities, Activity History, Milestones, Approval History, Case Teams, External Content, Content Deliveries).
- Previous Part 6.5 content (if any) renumbered.
- Cross-lab sweep: "Day 1" removed from title, API names → labels, "Where you should be" callouts removed throughout (13 removed from participant guide), em dashes replaced with commas in prose.
**Files archived:** `Lab 01 v0.7 r9 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r9 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r8 — 2026-10-08
**Change:** Lab 03 prerequisite — Asset field needs to be on the Case record page.
- **Part 6.2:** Asset added to the list of fields dragged into the Case Details section of the classic Case Layout.
- **Part 9.5 (new):** drag Asset from the Fields panel onto the Dynamic Forms canvas. Previous 9.5 (Save and activate) becomes 9.6.
- Part 9 header updated to mention all four fields placed on the canvas; estimated time 10 min to 12 min; total lab time 102 min to 104 min.
**Files archived:** `Lab 01 v0.7 r8 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r8 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r7 — 2026-10-08
**Change:** Minor Part 9 addition supporting Lab 02 r4.
- Part 9 now also drags Case Record Type onto the Dynamic Forms canvas (in addition to Reported Date/Time and Resolution Notes). This makes Case Record Type editable from the Lightning record page, which Lab 02 r4 Part 2.3 uses to switch Record Type on the Golden Record for the visibility rule test.
- Part 9 estimated time increased from 8 min to 10 min; total lab from 100 min to 102 min.
- Scaffolding updated with 10 seeded Cases and a Profile override that sets ServicePulse 360 as the default app on login for System Administrator. See `scaffolding-package/v07-case-extension/data/README.md`.
**Files archived:** `Lab 01 v0.7 r7 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r7 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r6 — 2026-10-08
**Change:** Three structural changes based on Round 4 smoke-test findings and the Round 5 Golden Record decision.
**Changes:**
- **Part 6 (classic page layout):** Added a "Why this matters" callout clarifying classic page layouts vs Lightning record pages are two different rendering systems. Added Part 6.3 ("Confirm Case Comments is in the Related Lists section") because later labs rely on this.
- **Part 9 (Lightning record page):** Rewritten entirely. r5's "migrate to Dynamic Forms" had nothing to do (Pronto template ships with Dynamic Forms already enabled). r6 teaches "add your custom fields to the Dynamic Forms canvas": participants switch to the Fields tab in the App Builder's left sidebar and drag Reported Date/Time and Resolution Notes onto the record page.
- **Part 10 (NEW — Golden Record):** Expanded from a simple "test case" verification into a dedicated "create your Golden Record" step. Participants create one well-populated Case (NYCT Record Type, P3 - Medium, Track Defect, Case Origin = Phone, Account = MTA New York City Transit, Contact populated) that will be the central example across every subsequent lab. Fallback instructions for creating the Account manually are included for orgs where the scaffolding didn't deploy agency Accounts.
**Scaffolding update:** Added `scaffolding-package/v07-case-extension/data/` folder with four MTA agency Accounts (NYCT, LIRR, MNR, B&T) and four Contacts (Marcus Chen, Priya Patel, Elena Rodriguez, James O'Brien). Loaded via `sf data tree import --plan data/plan.json`.
**Files archived:** `Lab 01 v0.7 r6 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r6 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r5 — 2026-10-06
**Change:** Per-section step numbering. Step numbers restart at 1 within each subsection, baked into the text (not relying on Word's auto-numbering) so numbering is stable across Word versions.
**Reason:** r4 used Word's auto-numbered list style, which produced continuous numbering across the whole document (step 54, 55, 56 ... 70). Tim flagged this as both a formatting issue and a signal of lab length.
**Files archived:** `Lab 01 v0.7 r5 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r5 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r4 — 2026-10-04
**Change:** Round 3 of detailed lab feedback applied. Two structural additions, plus 20+ edits.
**Structural additions:**
- Part 0: Create the ServicePulse 360 Lightning App at the very start.
- Part 9: Migrate the record page to Dynamic Forms at the end, so the classic page layout actually renders in Lightning.
**Terminology:** Service Issue rename reverted. MTA uses "Cases" directly. Every reference to Service Issue was updated back to Case (object name, tab, record type, support process, compact layout, list views).
**Content edits:** em dashes swept, fields alphabetized to match UI, Case Record Type field added to page layout, Page Layout Assignment step added (with Shift-click multi-select), System Administrator profile explicitly checked in Record Type creation, list view 8.2 uses Clone pattern, Final Verification reordered to on-screen field order, Case Origin included as required, "Done" references removed, "at least seven" language for Inactive Values.
**Files archived:** `Lab 01 v0.7 r4 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 r4 - Extend Case for Multi-Agency (Instructor Notes).docx`.

### v0.7 r3 — 2026-06-17
**Change:** Round 2 of detailed lab feedback applied (21 anchored comments from Tim's annotated copy).
**Highlights:**
- Priority is full hands-on; Type is pre-deployed via instructor scaffolding (eliminates about 10 tedious deactivation clicks while preserving the customize-before-extending lesson).
- Case Support Process moved from instructor pre-work to a 2-minute participant lab step.
- Field Labels used throughout (not API names).
- Navigation context blocks at the start of each Part.
- Verify callouts name explicit Setup paths.
- Pronto context callout introduced.
- Compact Layout Assignment Shift-click sequence documented.
- List view filter-by-owner step added.
**Files archived:** `Lab 01 v0.7 - Extend Case for Multi-Agency (Participant).docx`, `Lab 01 v0.7 - Extend Case for Multi-Agency (Instructor Notes).docx`.
Note: these files are labeled "v0.7" without an r3 suffix because r3 was authored directly over the prior "v0.7" filename. The archive preserves them as the de facto r3 artifacts.

### v0.7 r2 — 2026-06-09 evening
**Change:** Customize-before-extending principle applied. Standard Priority and Type picklists are now customized in place rather than replaced by parallel custom fields.
**Reason:** Tim's Round 1 feedback: the justifications for custom Severity and Issue Type fields were arguable. Those concerns can be addressed by configuring the standard picklist values.
**Impact:** Lab drops from four custom fields to two. Standard Priority and Type carry P1 through P4 and the 13 transit values respectively.
Note: this revision does not have a dedicated archived file. The r2 and r3 content lived in the same filename as r3 evolved on top of r2 directly. r3's archived file is the first discrete artifact after r2.

### v0.7 r1 — 2026-06-09 afternoon
**Change:** Standard-First architectural pivot. Case + Asset + Field Service replace Service_Issue__c as the primary workshop surface. Service_Disruption__c becomes the one deliberate custom object.
**Reason:** v0.5 and v0.6 anchored the workshop on a custom object (Service_Issue__c). The demo org inventory revealed the entire Service Cloud + Asset + Field Service stack was available; building a custom object when MTA's actual production org (Cassie) runs on these standard objects was teaching the wrong pattern.
Note: r1 content was superseded by r2 before being written to a stable file. The historical "r1 output" is the v0.6 artifact pre-standard-first.

### v0.6 — 2026-06-09 morning (pre-Standard-First)
**Change:** Service_Issue__c scaffolded as the workshop's primary custom object. Day 2 Agentforce upgraded to hands-on. Data Import Wizard replaces the seed-action flourish for data loading.
**Files archived:** `Lab 01 - Build Service_Issue (Participant).docx`, `Lab 01 - Build Service_Issue (Instructor Notes).docx` (older runs; may not be in the archive if they were deleted during earlier housekeeping).
**Historical note:** v0.6 is the pre-pivot design. Reference only; superseded by v0.7 r1 and beyond.

---

## Conventions

**Filename pattern for current files:**  `Lab NN - Participant.docx` and `Lab NN - Instructor Notes.docx`.

**Filename pattern for archived revisions:**  `Lab NN v<agenda-version> r<revision> - <short title> (Participant|Instructor Notes).docx`.

**When a new revision ships:**
1. Rename the previous current file to its versioned name and move it to `archive/`.
2. Save the new revision at the stable current filename AND as a copy in `archive/` with its versioned name.
3. Add a new entry to the top of this manifest's revision history for that lab.
4. Update the lab's row in the Current labs table (bump Current revision and Last updated).

**When a new lab ships (first revision):**
1. Save the new lab at `Lab NN - Participant.docx` and `Lab NN - Instructor Notes.docx`.
2. Also save a copy at `archive/Lab NN v0.7 r1 - <short title> (Participant|Instructor Notes).docx` so there's a stable rev-1 artifact.
3. Change the lab's row in the Current labs table from "not started" to the real version and date.
4. Add revision history entries for the new lab.
