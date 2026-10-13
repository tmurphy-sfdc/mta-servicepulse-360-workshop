# Workshop Lab Authoring Feedback Log

Living document capturing feedback Tim has given on hands-on Salesforce workshop lab content. Used to (a) correct specific labs, (b) shape future lab authoring, (c) eventually distill into a Claude Skill (`salesforce-workshop-lab` or similar) that ships the principles as instructions.

Each entry tags whether it's a **lab-specific correction**, a **generalizable principle**, or both. The latter category is what eventually becomes the Skill content.

---

## Standard-First Architecture

### #1 — Customize standard picklist values before adding parallel custom fields
**Source:** Lab 01 v0.7 review, 2026-06-09
**Tags:** generalizable principle, Lab 01 correction
**Feedback:** The justifications for creating custom Severity and Issue Type fields are arguable — those concerns can be addressed by customizing the standard Priority and Type picklist values while keeping the standard fields in play.

**Principle:** Customize before extending. A custom field is justified only when configuration of the standard field genuinely can't reach the goal — not when the default *values* are wrong, the default *label* is wrong, or the default *layout* is wrong (those are configuration changes, not custom-field justifications). The tighter test:

- ❌ Standard values don't match → customize the picklist values
- ❌ Standard label is wrong → rename the field
- ❌ Standard layout placement is wrong → edit the page layout
- ✅ Standard field is read-only and editable is required (e.g., Reported_DateTime__c vs. CreatedDate)
- ✅ No standard field captures the concept at all (e.g., Resolution_Notes__c)
- ✅ Standard field has the wrong data type (rare; typically forces custom)
- ✅ Standard field is locked to a platform process we can't avoid

**Impact on Lab 01:** Drop Severity__c and Issue_Type__c custom fields. Customize standard Priority picklist (replace High/Medium/Low with P1–P4) and standard Type picklist (replace defaults with the 13 transit values). Record Types still restrict standard Type per agency — the per-RT picklist restriction pattern works identically on standard and custom picklists. Reported_DateTime__c and Resolution_Notes__c remain custom.

**Impact on future labs:** Apply the tighter test before introducing any custom field. Surface the test explicitly in lab content so participants see the decision being made, not just the result.

**Status:** APPLIED 2026-06-09 evening. SFDX metadata, deployed Case configuration, Lab 01 participant guide, Lab 01 instructor notes, and v0.7 internal doc all updated. Lab 01 now applies the customize-before-extending test four times explicitly.

---

## Pre-Workshop Setup Burden

### #2 — Minimize per-org pre-workshop setup; participant-buildable in <3 min should be a lab step
**Source:** Lab 01 v0.7 review, 2026-06-11
**Tags:** generalizable principle, Lab 01 correction
**Feedback:** Lab 01 currently states "your instructor has pre-created an MTA Service Issue Process you can select." There's no clean operational answer for how to pre-create this in 10–15 individual participant orgs without either (a) running scripted deploys against every org with the OrgFarm patch dependency, or (b) 30 minutes of manual point-and-click instructor tedium per workshop.

**Principle:** Default any pre-workshop setup item that a participant can build themselves in under three minutes into a lab step instead. Pre-workshop setup is fragile — orgs get re-provisioned, patches need re-applying, instructor laptops need the right tools. Lab steps are robust. Every minute of setup moved into the lab is a minute of robustness gained.

**Test for whether something stays as instructor pre-work:**

- ❌ Building it takes <3 min and the concept is on-topic for the workshop → make it a lab step
- ❌ Building it takes <3 min and the concept is teachable as a passing aside → make it a lab step with a Why-this-matters callout
- ✅ Building it requires deploy-level access participants don't have (e.g., enabling features that require System Administrator + multiple cross-system toggles)
- ✅ Building it takes >10 min and isn't core to the lab's pedagogical arc
- ✅ Building it is a one-time per-org bootstrap that participants would never do in production (e.g., installing a managed package)

**Impact on Lab 01:** Add a new Part 5.5 (~2 min) that has participants create the MTA Service Issue Process themselves: Setup → Cases → Support Processes → New → name it → select New, On Hold, Escalated, Closed as the active status values → Save. This becomes a teaching moment about Case Support Processes (the standard Salesforce mechanism for per-Record-Type Status restrictions on Case/Lead/Opportunity), which fits cleanly under the standard-first / customize-before-extending umbrella. Drop the "pre-created by instructor" pre-req from instructor notes. Lab grows from 90 to 92 min; the existing buffer absorbs it.

**Impact on future labs:** Apply the test before declaring anything as instructor pre-work. When in doubt, make it a lab step.

**Status:** PENDING — batched with additional Lab 01 feedback round, will apply together.

---

## Round 2 — Lab 01 v0.7 Detailed Review (21 comments from Tim's annotated copy, 2026-06-17)

Source file: `lab-manual/Lab 01 v0.7 - Extend Case for Multi-Agency (Participant) with comments v1.docx`. All entries below derive from anchored Pages comments exported as Word; the anchor text is the span Tim's comment was attached to. **Round 2 batch APPLIED 2026-06-17 in Lab 01 r3, instructor notes r3, and v0.7 internal doc r3. Open question #16 (dedicated Lightning App at start) resolved: deferred to Lab 2 per the existing v0.7 11:30 Lightning App Builder slot — Lab 1 stays in the default app.**

### Lab-specific corrections

#### #3 — Use Field Labels, not API names, in field listings
**Tags:** generalizable principle, Lab 01 correction
**Source comments:** #1 (anchor: "CaseNumber, "), #3 (anchor: "ContactId")
**Feedback:** Both Part 1's Case-tour bullet list and Part 7's compact-layout field list use API/Field Names (e.g., `CaseNumber`, `ContactId`) rather than the user-facing Field Labels (e.g., "Case Number", "Contact"). Participants navigate the Setup UI by Label, not API Name.
**Principle:** Use Field Labels in lab content. The Field Name / API Name distinction is itself a teaching moment (covered in the rename-tab section), but participants find fields by Label.
**Impact on Lab 01:** Replace `CaseNumber` → "Case Number", `ContactId` → "Contact", and similar throughout. Apply the convention everywhere a field is referenced in lab text.

#### #4 — Disambiguate "New" buttons when multiple exist on a page
**Tags:** generalizable principle, Lab 01 correction
**Source comments:** #8 (anchor: "Click New")
**Feedback:** Part 2.1 (Priority customization) says "Click New" without specifying which New button. The Priority field detail page has multiple New buttons (one for the main toolbar and one inside the Case Type Picklist Values section).
**Principle:** When a page has multiple buttons with the same label, name the section context. "Click New" → "In the Case Priority Picklist Values section, click New."
**Impact on Lab 01:** Apply to Part 2.1, 2.2, and any other multi-New context.

#### #5 — Bulk deactivation of picklist values is tedious
**Tags:** Lab 01 correction (open question), instructor pre-work decision
**Source comments:** #4 (anchor: "(15 min)"), #9 (anchor: "Deactivate every existing value that isn't transit-specific. Click Deactivate next to each one in turn.")
**Feedback:** Part 2.2 asks participants to click Deactivate next to ~7 Pronto restaurant defaults on the Type field. With 10+ values across Priority and Type combined, this could blow the 15-minute Part 2 estimate. Tim suggested: "instead of deactivating, we add a step to specify which 'Type' values should be available for the MTA record types" — but that's already Part 6 (Record Types). The deactivation step is technically redundant for record-create UI (Record Types restrict per-agency) but DOES matter for reports, list-view filters, and master-picklist integrity.
**Resolution (2026-06-17):** Option D — Priority hands-on by the participant; Type pre-customized via instructor pre-deployed StandardValueSet metadata. Lab Part 2.1 retains the full hands-on customization (3 Priority value deactivations + 4 P1–P4 additions, ~3 min). Lab Part 2.2 becomes a guided tour of the pre-deployed Type customization with explicit framing: "we pre-deployed Type because the mechanic is identical to what you just did on Priority, applied at scale." Teaches the mechanic on a small instance; demonstrates the pattern at scale via instructor pre-work. Avoids ~10 tedious deactivation clicks.

**Principle (generalizable):** Teach the mechanic on a small instance; demonstrate the pattern at scale via instructor pre-work. Don't make participants rehearse the same skill 10 times.

**Status:** APPLIED 2026-06-17.

#### #6 — Verify wording reads like it needs a Case record but doesn't
**Tags:** generalizable principle, Lab 01 correction
**Source comments:** #7 (anchor: "Verify")
**Feedback:** The Part 2.1 Verify callout reads "Active Values shows P1 - Critical... P3 - Medium (default, indicated by ★)..." — the wording sounds like the participant needs a Case record to confirm a default value, but the indicator is actually visible on the Priority field detail page in Setup. Confirmed with Tim 2026-06-17: the issue is wording, not reachability.
**Principle:** Every Verify callout must (a) be reachable at the moment it appears in the lab, and (b) tell the participant *exactly where to look* — name the Setup path or screen explicitly so there's no ambiguity about where the verification happens.
**Impact on Lab 01:** Tighten every Verify callout to include the Setup path. Example for Part 2.1: "On Object Manager → Case → Priority → Case Priority Picklist Values section: the Active Values list shows P1 - Critical, P2 - High, P3 - Medium (default — has a checkmark in the Default column), P4 - Low. The Inactive Values list below shows High, Medium, Low."

#### #7 — Confusing transition in Part 3
**Tags:** Lab 01 correction
**Source comments:** #10 (anchor: "Now apply the test in the other direction: cases where standard genuinely can't reach the goal.")
**Feedback:** Sentence is too abstract for the audience. Reword or remove.
**Impact on Lab 01:** Replace with something concrete like: "Now we add the two custom fields. For each one, we'll see why standard couldn't fit."

#### #8 — Add navigation context at the start of each Part
**Tags:** generalizable principle, Lab 01 correction
**Source comments:** #11 (anchor: "Fields & Relationships → New."), #5 (anchor: "Object Manager")
**Feedback:** Part 3.1 starts with "Fields & Relationships → New" without restating that the participant should still be on the Case object. Setup nav state is easy to lose. Earlier instruction in the lab uses "Object Manager" without prefixing "Setup →".
**Principle:** At the start of every Part (and every numbered sub-step that resumes from a possible context shift), restate the navigation path. Early in the workshop especially, prefix Setup destinations with "Setup → ..."
**Impact on Lab 01:** Add "Setup → Object Manager → Case" navigation reminders at the start of Parts 3, 6, 7, 8, and any sub-step where context could be lost. Add "Setup →" prefix to Object Manager references in early Parts.

#### #9 — Remind that picklist values go on separate lines
**Tags:** Lab 01 correction
**Source comments:** #6 (anchor: "to add MTA's value")
**Feedback:** Add an explicit reminder when participants paste picklist values into Salesforce.
**Impact on Lab 01:** Add a one-line tip after the values code block: "Each value goes on its own line — this is how Salesforce parses them."

#### #10 — Remove "→ OK" after Check Syntax
**Tags:** Lab 01 correction
**Source comments:** #12 (anchor: "→ OK")
**Feedback:** The Check Syntax button doesn't trigger a dialog with an OK; it just renders a green or red status message. The instruction "Check Syntax → OK" describes UI that doesn't exist.
**Impact on Lab 01:** Replace "→ Check Syntax (you should see "No syntax errors in formula") → OK" with "→ Check Syntax → confirm you see the green "No syntax errors in formula" message."
**Generalizable lesson:** Don't describe UI interactions that haven't been verified against the actual screen.

#### #11 — "Find Case" → "Find Cases"
**Tags:** Lab 01 correction
**Source comments:** #14 (anchor: "Find Case")
**Feedback:** Part 4 (rename tab) says "Find Case in the list" but the Rename Tabs and Labels page lists tabs by their plural label ("Cases").
**Impact on Lab 01:** Change "Find Case" → "Find Cases".

#### #12 — Reorder LIRR Record Type instructions to match UI field order
**Tags:** generalizable principle, Lab 01 correction
**Source comments:** #15 (anchor: "Description: Long Island Rail Road. Active: ✅")
**Feedback:** The fields in the LIRR Record Type creation flow are described in the wrong order. In the Setup UI, the field order is: Existing Record Type → Record Type Label → Record Type Name → Support Process → Description → Active. The lab currently reads "Description... Active... Business Process" — wrong order. Fix: place Description and Active AFTER Business Process.
**Principle:** Lab instructions for filling out a Setup form should match the on-screen field order top-to-bottom.
**Impact on Lab 01:** Reorder the LIRR (Part 6.2), MNR (Part 6.3), and B&T (Part 6.4) Record Type instructions. Verify NYCT (Part 6.1) follows the same order.

#### #13 — Compact Layout Assignment requires shift-click for multi-RT assignment
**Tags:** Lab 01 correction
**Source comments:** #17 (anchor: "Choose Service Issue Compact ")
**Feedback:** The current instruction implies a single dropdown selection. The actual UI: "In the 'Compact Layout to Use' dropdown, select 'Service Issue Compact', then while holding down the Shift key, click into each of the 4 Record Types (you'll see each row highlight in purple), then click Save."
**Principle:** When a multi-step UI flow involves modifier keys (Shift, Ctrl, Cmd), document the exact key sequence and the visual confirmation participants should see (purple highlight, etc.).
**Impact on Lab 01:** Replace Part 8 Compact Layout Assignment instruction with the shift-click sequence above.

#### #14 — List view gear icon location is wrong
**Tags:** Lab 01 correction
**Source comments:** #18 (anchor: "next to the list view dropdown")
**Feedback:** The gear icon is to the right of the "Search this list" search box, not next to the list view dropdown. Fix: "Click the gear icon to the right of the 'Search this list' search box."
**Impact on Lab 01:** Update Part 9.1 and 9.2.

#### #15 — List view filter needs "Filter by Owner" set to All
**Tags:** Lab 01 correction
**Source comments:** #19 (anchor: "Add Filter: Status not equal to Closed → Done → Save.")
**Feedback:** The lab is missing a step: when creating a list view, the default Filter by Owner is "My Service Issues" — the participant won't see records they didn't create. Need to change Filter by Owner to "All Service Issues" before adding the Status filter.
**Impact on Lab 01:** Insert a step before the Status filter: "In the Filter by Owner section, click on 'My Service Issues' and change to 'All Service Issues' → Done."

### Open architectural questions

#### #16 — Should the workshop create a dedicated Lightning App at the start?
**Tags:** generalizable principle, architectural decision
**Source comments:** #20 (anchor: "App Launcher")
**Feedback:** Lab 01's verification step assumes participants navigate via App Launcher → Service Issues → click. But which App they're currently in determines the page layout, navigation tabs, and tab styling. Tim suggested creating a dedicated workshop Lightning App early so all subsequent instructions can assume that navigation context.
**Principle:** Establish navigation context (a dedicated Lightning App) at the very start of a multi-lab workshop. Reference it in every subsequent navigation instruction. Avoids the "which app am I in" failure mode for any lab beyond the first.
**Impact on Lab 01:** Open question — should we add an even earlier Part 0 ("Create the ServicePulse 360 App") before Part 1 (Tour the standard Case object)? Or carry the existing v0.7 agenda's 11:30 Lightning App Builder slot as the moment we establish the App, and have Lab 01's references be "App Launcher → Service Issues" with a tip "any standard app works for this; we'll build the dedicated app in the next session"?

### Tonal / framing corrections

#### #17 — Add Pronto-org context for participants who don't know it
**Tags:** Lab 01 correction
**Source comments:** #2 (anchor: "in this Pronto-derived org, restaurant-themed")
**Feedback:** The lab references the Pronto context casually but never introduces what Pronto is. Workshop participants need a one-paragraph explanation: the workshop org is built on a fictitious food-delivery business that uses Salesforce to manage operations; we're customizing it for MTA's reality.
**Impact on Lab 01:** Add a "Why does my org have restaurant data?" callout near the top of Part 1 (or in the Workshop intro) explaining Pronto.

### Affirmations (preserve in design)

#### #18 — Time estimates are accurate; conservative is good
**Tags:** generalizable principle (validated)
**Source comments:** #13 (anchor: "(2 min)" — Part 4 tab rename), #16 (anchor: "Part 7 — Configure the page layout (10 min)" — "conservative, which I'd prefer")
**Feedback:** Tim affirmed two specific time estimates as good or appropriately conservative.
**Principle:** Time estimates should be conservative. Better to finish a Part 5 minutes early than blow a Part 5 minutes late and cascade-fail the rest of the day.

### Operational / logistics (cross-cutting concerns)

#### #20 — How do we get access to 20 participant orgs for pre-workshop setup?
**Tags:** open operational problem, cross-cutting (affects every lab with pre-workshop setup)
**Source:** Tim, 2026-06-17, raised when committing to Option D for feedback #5
**Concern:** v0.7 already has multiple per-org pre-workshop setup items (the AgentActionsTest patch for the OrgFarm template defect, the Service_Issue Process Business Process — now relocated to a participant lab step per #2, the Type StandardValueSet pre-deploy per #5). More are likely as labs evolve. Without a strategy, we're looking at potentially 20+ × N-items of manual click-through or sf CLI login work.
**Possible approaches (to evaluate when we come back to this):**
- OrgFarm bulk-provisioning typically returns sfdx-auth-urls or username/password pairs. If sfdx-auth-urls: a single bash loop with `sf org login sfdx-url --sfdx-url-file ...` can import all 20 in one go.
- Once authenticated, a single bash loop iterating over the org aliases can apply the AgentActionsTest patch and deploy the v0.7 scaffolding package per org. ~1–2 min per org × 20 ≈ 30 min total instructor effort, scriptable.
- Alternative: a one-time JWT bearer flow setup per org enables fully automated runs, but requires a Connected App in each org — additional setup overhead that may not be worth it for 20 orgs.
- Alternative: ask OrgFarm if their bulk provisioning supports a "post-provision script" hook that runs against each org as it's created. If yes, we hand them the script once.
**Status:** OPEN — to be solved before workshop delivery; not blocking lab content design. Logging here so it's tracked alongside the per-lab feedback rather than lost as a side comment.

---

### Optional / informational

#### #19 — Mention Object Manager tab as alternative navigation
**Tags:** Lab 01 correction (low-priority)
**Source comments:** #0 (anchor: ".")
**Feedback:** Tim noted that participants could also click the Object Manager tab next to Home in Setup, but acknowledged the current click-through (gear → Setup → Quick Find: Object Manager) is probably easier for novices. No action required unless we want to mention the shortcut as a tip later.
**Impact on Lab 01:** Optional — add a Tip callout late in Lab 01 for participants who are getting comfortable: "Setup tip — once Setup is open, you can click the Object Manager tab next to Home for faster access."

---

---

## Round 3 — Lab 01 v0.7 Detailed Review (Tim's 2026-10-04 review of r3 output)

Source: Tim's chat review of Lab 01 v0.7 r3 after smoke-testing against v3 (org 00Daj00001AMEPVEA5). This batch becomes Lab 01 r4 and establishes principles applied to all subsequent labs.

### Generalizable principles (apply to every subsequent lab)

#### #21 — No em dashes in lab content
**Tags:** generalizable principle, writing style
**Feedback:** Em dashes are banned per Tim's standing style guidance (see [[feedback-no-em-dashes]] memory).
**Principle:** Rewrite with parens, colons, commas, or split sentences. Applies to all workshop materials, not just Lab 01.
**Status:** PENDING — Lab 01 r3 contains em dashes that need to be swept.

#### #22 — Instruct in the order fields appear on the screen
**Tags:** generalizable principle, Lab 01 correction (page 15 check 1)
**Feedback:** Final Verification walkthrough asks the user to populate Priority before Type, but Type is first on the page layout. Lab instructions should follow the on-screen order the user will encounter, not the semantic order the author had in mind.
**Principle:** When directing a user to click or populate fields on a page, order the instructions to match the on-screen top-to-bottom order. Reduces the "where is that field again?" moment.

#### #23 — Required-field completeness in verification walkthroughs
**Tags:** generalizable principle, Lab 01 correction (page 15 check 1)
**Feedback:** Service Issue Origin is a required field (either field-level required or page-layout-level required) but the lab's Final Verification doesn't include it. User would get a validation error and get stuck.
**Principle:** For any lab that ends with a "create a sample record" verification, enumerate every required field (both field-level and page-layout-level required) and include a populating step for each. Audit the page layout before writing the verification step. Applies to every lab that walks the user through creating a record.

#### #24 — Alphabetize field listings when the UI alphabetizes
**Tags:** generalizable principle, Lab 01 correction (page 3 #4)
**Feedback:** The Fields & Relationships screen alphabetizes fields. The lab's bulleted field list on page 3 is not alphabetical, so a participant scanning down the actual Salesforce list is working against an unordered reference.
**Principle:** When referencing fields on an alphabetized Setup screen, list them alphabetically in the lab text. Reduces cognitive load.

#### #25 — Pre-deployed values require either an all-org deploy or user hands-on instructions
**Tags:** operational / cross-cutting (affects every lab with pre-deployed metadata), Lab 01 correction (page 3 #6)
**Feedback:** Tim: "page 3, #6: this would require us to modify all of the orgs we're assigning to the participants (about 20 orgs) so we'll need to align on how we accomplish that OR build out instructions for doing it themselves."
**Principle:** Every item declared as "pre-deployed by the instructor" is a 20-org operational dependency. Either (a) commit to an automated bootstrap script that deploys the scaffolding to every participant org, or (b) convert the lab step to a hands-on build. Don't straddle. Related: feedback entry #20.
**Status:** Depends on resolution of 20-org bootstrap script decision.

#### #26 — When the UI alphabetizes a custom field, use its full custom-field name in instructions
**Tags:** generalizable principle, Lab 01 correction (page 14 instruction 93)
**Feedback:** Instruction says "Record Type" when the actual field in the Fields panel is "Service Issue Record Type" (post-rename). Participants will scroll the R section for Record Type and never find it; they need to scroll to S for Service Issue Record Type.
**Principle:** After a Case → Service Issue tab rename, every reference to a field that includes the object label (Case Number, Case Record Type, etc.) also renames (Service Issue Number, Service Issue Record Type). Audit the lab for any field reference that implicitly depends on the pre-rename object label.

#### #27 — Verify "Done" / "Save" button names against actual UI
**Tags:** generalizable principle, Lab 01 corrections (pages 14 #92, 10 — remove "Done" references)
**Feedback:** Instruction 92: "Closed > Done > Save" but there is no Done button in that UI. Instruction 93: "Save" is mentioned ambiguously as if it were a field.
**Principle:** Every button name in a lab instruction must be verified against the actual Setup UI. The pattern Field → Action → Save → OK is common but doesn't apply everywhere. Related: feedback entry #10 (same issue with Check Syntax).

#### #28 — When content is "subject to UI change" (picklist defaults, inactive values), use ranges / lower-bound language
**Tags:** generalizable principle, Lab 01 correction (page 5 #16 and "Verify" box)
**Feedback:** Lab says "7 inactive values" in the Type picklist, but Tim's screenshot shows 16 inactive values. The number varies by org provisioning date (different Pronto template versions ship different values).
**Principle:** For verification steps that reference content that varies by org state, use "at least X" language rather than "exactly X." Pattern: "your Inactive Values list should include at least [list of 7 restaurant-themed values]; it may include additional Pronto defaults depending on when your org was provisioned."

#### #29 — Record Type creation must include profile assignment
**Tags:** generalizable principle, Lab 01 correction (page 10 part 6)
**Feedback:** Current lab creates Record Types but doesn't instruct the user to grant any profiles access. Default is zero profiles. Participants will complete the Record Type creation and then be unable to use the Record Type anywhere.
**Principle:** Record Type creation lab steps must always include an explicit profile-assignment step. At minimum: grant System Administrator access. For workshop context, that's the only profile that matters since participants are all logged in as SysAdmins.

#### #30 — Page Layout assignment must include per-RT + per-profile assignment
**Tags:** generalizable principle, Lab 01 correction (page 12 part 8)
**Feedback:** After creating a page layout, the lab doesn't assign it to the correct profile × Record Type combinations. Participants will see the default layout instead of what they just built.
**Principle:** Page layout creation requires a Page Layout Assignment step. The pattern: Setup → Object → Page Layouts → Page Layout Assignment → Edit Assignment → for each row (profile × Record Type), select the correct layout → Save. Multi-select via Shift-click where possible. Include this step in every lab that creates a page layout.

#### #31 — Classic page layouts vs Lightning record pages — Dynamic Forms is required for the layout to actually render
**Tags:** generalizable principle, Lab 01 correction (general issue)
**Feedback:** The Lightning record page for Case uses field sections (Lightning record page components), not the classic page layout. So modifying the classic page layout has no visible effect for the user unless Dynamic Forms is enabled on the record page. Either (a) default the record page to use Dynamic Forms via the scaffolding, or (b) teach the user to migrate the record page to Dynamic Forms.
**Principle:** Any workshop lab that modifies a classic page layout must either (a) establish Dynamic Forms before the page-layout work so changes are visible, or (b) use the classic UI exclusively for the layout verification. "Edit the page layout and go to the record" is incomplete without one of those.

### Lab 01 specific corrections (apply to r4)

#### #32 — Em dash sweep
**Status:** PENDING — sweep all em dashes from Lab 01 Participant and Instructor Notes.

#### #33 — Cassie casing
**Feedback:** Should Cassie be mixed case or all caps (CASSIE)? Tim's memory notes use mixed case. Needs MTA confirmation before mass replace.
**Status:** OPEN — defaulting to "Cassie" per existing memory.

#### #34 — Terminology verification: "case" vs "ticket"
**Feedback:** Does MTA use the word "case" or "ticket" or something else? Needs MTA confirmation.
**Status:** OPEN — defaulting to "case" (and "Service Issue" after tab rename) until MTA confirms.

#### #35 — ServicePulse 360 Lightning App creation timing
**Feedback:** Should Lab 01 start by creating the ServicePulse 360 app? Related to open question #16 from Round 2.
**Status:** OPEN — needs decision.

#### #36 — Page 3 #5 wording
**Current:** "Click Priority. Notice the existing picklist values (likely High, Medium, Low). We'll change these in Part 2.1."
**New:** "Click Priority. Scroll down to the 'Case Priority Picklist Values' section. Notice the existing picklist values (likely High, Medium, Low). We'll change these in Part 2.1."
**Status:** PENDING for r4.

#### #37 — "Why this matters" sentence on Contact Name
**New:** "Contact Name creates a relationship between the case and the contact record within Cassie."
**Status:** PENDING for r4.

#### #38 — Page 5 #15 opening
**New opening:** "Look at the Case Type Picklist Values list."
**Status:** PENDING for r4.

#### #39 — Page 6 "Verify" box — remove phantom "Custom indicator"
**Feedback:** "or the 'Custom' indicator in the Type column" — no such indicator exists.
**Status:** PENDING for r4.

#### #40 — Page 9 part 5.5 — remove Lead/Opportunity mention
**Feedback:** The Case Support Process lab currently mentions Lead and Opportunity objects as other objects that use Support Processes. Remove that; keep the lab focused on Case.
**Status:** PENDING for r4.

#### #41 — Page 12 part 7 — target the "Case Layout" specifically
**Current:** "From the palette at the top, drag Section onto the canvas just above the Description section."
**New:** First instruction specifies the user clicks the layout named "Case Layout." Then: "From the palette at the top, drag Section onto the canvas just above the Description Information section."
**Status:** PENDING for r4.

#### #42 — Page 12 part 7 — add Quick Find tip for fields already on page
**New callout (colored tip):** "Users can locate where fields are already on the page layout by using the Quick Find tool in the palette. If a field is already on the page layout, it will show up in a light gray color; when you click the field name, the system will show you its location on the layout and will highlight it in yellow."
**Status:** PENDING for r4.

#### #43 — Page 12 part 8 — assign new page layout to profiles, add Service Issue Record Type field to layout
**Feedback:** After creating the page layout, assign it to the correct profiles × Record Types (see principle #30). Also add the field "Service Issue Record Type" to the page layout (presumably so participants can see which Record Type a given record is).
**Status:** PENDING for r4.

#### #44 — Page 14 instruction 93 — multiple fixes
- "Record Type" → "Service Issue Record Type" (see principle #26)
- "Case Number" → "Service Issue Number" (post-rename)
- End the instruction with "Click Save" (not implying Save is a field)
**Status:** PENDING for r4.

#### #45 — Page 14 section 9.2 — second list view via clone
**Feedback:** Simplify second list view creation by cloning the first one and modifying.
**Status:** PENDING for r4.

#### #46 — Page 15 check 1 reorder + required-field completion
See principles #22 and #23.
**Status:** PENDING for r4.


---

## Round 4 — Lab 01 + Lab 02 r1 smoke-test findings (Tim's 2026-10-06 to 2026-10-08 testing against v3)

Source: Tim's live smoke-testing of Lab 01 r5 and Lab 02 r1 in the v3 Pronto Agentforce Reference org. These findings reshape both labs and establish a generalizable principle about relying on standard-object relationships.

### Generalizable principles

#### #47 — Pronto template's Lightning record page for Case ships with Dynamic Forms already enabled
**Tags:** generalizable principle, Lab 01 correction (Part 9), org-template reality
**Finding:** The Pronto Agentforce Reference template's Case record page is already using Dynamic Forms when the org is provisioned. The "migrate to Dynamic Forms" operation that Lab 01 r4/r5 Part 9 teaches has nothing to do — there's no "Upgrade Now" button because the page is past that state. The template ships with pre-populated field sections (Case Details with Type/Subject/Description, Case Status with Status/Priority/Case Reason/Case Origin, Related Storefront with Business Account/Storefront).
**Principle:** When a workshop runs on a specific demo template, verify every "configure this feature from scratch" step actually produces work. If the template already configured the feature, the lab step must change from "configure" to either "customize what's there" or "replace with your own."
**Impact on Lab 01:** Part 9 must be rewritten for r6. New teaching: not "migrate to Dynamic Forms" but "add your custom fields to the Dynamic Forms canvas." Participants drag Reported Date/Time and Resolution Notes from the Fields panel in the left sidebar onto the canvas (into existing sections or new ones they create). Classic Case Layout work from Part 6 is a reference artifact, not something that auto-renders in Lightning on this template.

#### #48 — Component name correction: "Related List - Single" (not "Related Record List")
**Tags:** Lab 02 correction (Part 3), terminology accuracy
**Finding:** Lab 02 r1 referred to a "Related Record List" component. No such component exists in the standard component palette. The correct name for showing one specific related list is "Related List - Single" (not plural, singular, with the hyphen).
**Principle:** Component names in the Lightning App Builder palette must be verified against the actual palette, not inferred from Salesforce's documentation (which sometimes uses different names across releases). Standard components with "related" in the name in the current org include: Dynamic Related List - Single, Related List - Single, Related List Quick Links, Related Lists, Related Record.
**Impact on Lab 02:** r2 corrects every reference from "Related Record List" to "Related List - Single".

#### #49 — Don't demo relationships that aren't guaranteed to exist
**Tags:** generalizable principle, Lab 02 Part 3 correction
**Finding:** Lab 02 r1 demoed showing Account.Cases on a Case page via Related List - Single. In production, Cases don't always have an Account populated. Web-to-case anonymous intake, support orgs that allow anonymous cases, Contact-only cases — all break the demo. A pedagogical demo whose data assumption fails intermittently is worse than one with a less interesting but reliable data source.
**Principle:** When teaching a pattern that depends on a related record, choose a relationship that's guaranteed to exist. For Case, that means Case Comments or Case History (both auto-attached). For other objects, pick the most reliable relationship, not the most interesting-sounding one.
**Impact on Lab 02:** r2 swaps Account.Cases for Case Comments. The Related List - Single component is configured with Parent Record = "Use This Case" (no cross-object traversal), Related List = Case Comments. Simpler config, bulletproof data assumption, same portable teaching: "surface one specific related list prominently so users don't have to switch tabs."

### Lab 01 specific corrections (apply to r6)

#### #50 — Part 9 rewrite: "add your custom fields to the Dynamic Forms canvas"
**Previous (r4/r5):** Part 9 teaches migrating from Record Detail component to Dynamic Forms via the Upgrade Now wizard. Doesn't apply because the template already migrated.
**New (r6):** Part 9 teaches adding Reported Date/Time and Resolution Notes to the Dynamic Forms canvas. Participants open the Case record page in App Builder, click the Fields tab in the left sidebar, locate Reported Date/Time and Resolution Notes, drag each onto the canvas into an existing field section (Case Details is natural), Save → Activate.
**Secondary teaching:** The classic Case Layout participants built in Part 6 is a documented reference artifact but does not auto-render in Lightning on this template. Lightning record page field placement is a separate concern that must be explicitly configured via Dynamic Forms. This is the "classic layouts and Lightning record pages are two different systems" teaching, reframed with the Pronto template reality in mind.

### Lab 02 specific corrections (apply to r2)

#### #51 — Part 3 rewrite: Related List - Single showing Case Comments
**Previous (r1):** Part 3 taught Related Record List (wrong name) showing Account.Cases (unreliable).
**New (r2):**
- Component: Related List - Single
- Parent Record: "Use This Case" (default, no change needed)
- Related List: Case Comments
- Related List Type: Default (or Basic List)
- Placement: on the Case Details canvas, below existing content, so Case Comments is visible without clicking the Related tab
**Pre-prerequisite:** Case Comments must be in the Case page layout's Related Lists section. Standard Case Layout includes it by default on this template (visible as "Case Comments (0)" on the Related tab in the smoke-test screenshots).

### Lab-level implications

- Lab 01 r6 and Lab 02 r2 are both triggered by this smoke-test batch. Produce both.
- The Lab 02 r2 Part 2 (Dynamic Forms visibility rule on Reported Date/Time) was validated as working in Tim's smoke-test. r2 doesn't change Part 2.
- The Lab 01 r6 Part 6 (classic Case Layout) stays as-is for reference and SOQL/API consistency, but the Part 9 rewrite acknowledges that it's not what makes the Lightning UI render.

---

## Round 5 — Golden Record cross-lab anchor (Tim's 2026-10-08 design decision)

Source: Tim's smoke-test of Lab 02 r2 against v3 revealed Case Comments wasn't pickable in Related List - Single because it wasn't in the Case Layout's Related Lists section on the Pronto template. Rather than try to make Case Comments work, Tim proposed a stronger pattern: create a single "Golden Record" at the end of Lab 1 that every subsequent lab references.

### Generalizable principles

#### #52 — Create a Golden Record at Lab 1 to anchor every subsequent lab
**Tags:** generalizable principle, cross-lab architecture
**Rationale:** Multi-lab workshops suffer when each lab assumes its own ad-hoc test data. A dedicated, well-populated Golden Record at the end of Lab 1 solves four problems: (1) later labs don't have to re-create test data, (2) smoke-testing is deterministic, (3) participants internalize what a "complete" record looks like, (4) narrative continuity across labs reinforces the workshop story.
**Principle:** When a workshop spans multiple labs that share data concerns, create a dedicated Golden Record step at the end of the first lab. Spec every field explicitly (Record Type, Priority, Status, Type, Contact, Account, Origin). Every subsequent lab references "your Golden Record" rather than "create a test case."

#### #53 — Narrative coherence: pick one agency's story and thread it through
**Tags:** generalizable principle, cross-lab architecture
**Rationale:** With four MTA agencies (NYCT, LIRR, MNR, B&T), the workshop could demo any of them. Tim chose NYCT because the v0.7 agenda already specifies an NYCT bus for the Lab 3 Asset hierarchy, and Lab 5's Executive Scenario is an F line (NYCT subway) disruption. Picking one coherent agency narrative keeps the workshop story simple and makes "did I do this right?" easier to diagnose.
**Principle:** When a workshop has multiple parallel options (agencies, product lines, use cases), pick one as the primary story thread. Other options stay available for optional/alternate paths but aren't the demonstrator.

#### #54 — Pre-populate scaffolding with records referenced by Lab 1's Golden Record step
**Tags:** generalizable principle, operational / scaffolding
**Rationale:** Lab 1's Golden Record needs an Account (MTA New York City Transit) that doesn't exist in the Pronto starter data. Rather than have 20 participants each create the Account manually (30 seconds x 20 = 10 minutes of workshop time, plus the risk of inconsistent naming), pre-populate four MTA agency Accounts via `sf data tree import` as part of scaffolding.
**Principle:** Any specific-named record that Lab 1 asks participants to pick (not create) should be pre-loaded via scaffolding. Keep participant-facing creation steps for records whose existence is a lesson, not a prerequisite.
**Fallback:** The participant guide must include create-this-record instructions in case the scaffolding wasn't deployed for a given participant org. Fallbacks are robustness, not laziness.

### Lab 01 r6 specific decisions

#### #55 — "MTA New York City Transit" as the Golden Record Account
**Rationale:** NYCT aligns with Lab 3's bus-with-components narrative, Lab 5's F line example, and the Day 2 Executive Scenario Simulation.

#### #56 — Participants pick any contact; MTA-aligned contacts available as a nice-to-have
**Rationale:** Avoids forcing participants into a specific name-finding step while making MTA-coherent choices available if they want. The four MTA-aligned contacts (Marcus Chen, Priya Patel, Elena Rodriguez, James O'Brien) are pre-populated by scaffolding but Lab 1 says "pick any contact" with the MTA names mentioned as suggested options.

#### #57 — Golden Record Subject = "Golden Record: Workshop reference case"
**Rationale:** Makes the record easy to find in a list view and clearly signals its role to any instructor assisting a participant.

### Lab 02 r3 specific decisions

#### #58 — Contact.Cases is the Related List - Single demonstrator
**Rationale:** Case Comments isn't in the Pronto template's Case Layout Related Lists section, so the Related List - Single component couldn't pick it. Case History is bulletproof but passive. Contact.Cases uses the Golden Record's Contact (guaranteed populated by Lab 1 Part 10), is already a Related List on Contact's layout, and benefits from the self-referential behavior (the Golden Record appears in its own list because it IS one of its Contact's cases). This turns a workaround into a teaching moment.

#### #59 — Self-referential behavior is a feature, not a bug
**Principle:** When teaching related-list patterns via a self-referential demo (the current record appearing in its own related list), call it out explicitly. Participants who notice it will wonder if it's a mistake; participants who don't notice it miss the pattern. Teach the pattern directly.

---

## Round 6 — Lab 02 r3 smoke-test feedback (Tim, 2026-10-08)

Source: Tim's targeted smoke-test of Lab 02 r3 against v3. This batch triggered Lab 02 r4 and Lab 01 r7, plus a scaffolding update.

### Generalizable principles

#### #60 — Scrub assumption-laden intro text; prefer factual framing
**Tags:** generalizable principle, writing style
**Finding:** Lab 02 r3 intro included "In production, a NYCT dispatcher triaging a Signal Issue cares about different information than a B&T toll operator." Tim: "We don't know if that's what admins do today."
**Principle:** Avoid making claims about what customer admins or users do today unless there's firsthand customer validation. Replace confident operational narration with factual descriptions of what the Salesforce feature does and why it exists.

#### #61 — Don't preview field choices that aren't representative of the lab's actual depth
**Tags:** generalizable principle, writing style
**Finding:** Lab 02 r3 Part 2 had a confusing preamble listing Priority ("shown for every Record Type"), Type ("shown for every Record Type"), and Reported Date/Time ("we'll make this NYCT-only as the demonstrator"). Reviewer confusion: are we applying rules to all three or one? Answer was one, but the preamble implied three.
**Principle:** For a lab that applies a technique to one specific field as a worked example, don't preview the other fields with aside-explanations unless the lab actually touches them. State the one thing you're doing and do it.

#### #62 — Filter paths must match the real UI, not a simplified mental model
**Tags:** generalizable principle, Lab 02 Part 2.1 correction
**Finding:** Lab 02 r3 Part 2.1 said "Field: Case > Case Record Type, Operator: Equal, Value: NYCT." The actual UI requires clicking Advanced, then navigating Record > Case Record Type > Name, using Contains, with Value = NYCT. The simplified mental-model instructions didn't match any clicks the participant could actually make.
**Principle:** For UI-navigation instructions, always use the actual click path, not a conceptual summary of what the clicks accomplish. If the UI has a tab called "Advanced" that participants need to click, say "click Advanced." If the field picker is a multi-step dropdown, enumerate every step.

#### #63 — Prefer editing an existing record over creating a second one when demonstrating UI-conditional behavior
**Tags:** generalizable principle, Lab 02 Part 2.3 correction
**Finding:** Lab 02 r3 asked participants to create a second Case with a different Record Type to verify the visibility rule. Tim: cleaner to change the Record Type on the Golden Record itself, which requires Case Record Type to be editable on the Lightning record page.
**Principle:** When a lab needs to demonstrate how UI responds to a field change, prefer editing that field on an existing record over creating a parallel record. Fewer steps, less data clutter, same pedagogical outcome. Requires the field to be editable on the record page (which may require a prior lab step to place it on the Dynamic Forms canvas).

#### #64 — Avoid time-of-day language in cross-lab references
**Tags:** generalizable principle, writing style
**Finding:** Lab 02 r3 "What's next" said "After lunch, Lab 3 models MTA infrastructure." Risk: workshop schedule can slip, lunch may be at a different time, or the lab may run on a different day.
**Principle:** In cross-lab references, use "In Lab X" or "The next lab" rather than time-of-day anchors. Keeps the lab reusable across schedule variations.

#### #65 — Success criteria should express the minimum verifiable outcome
**Tags:** generalizable principle, Lab 02 Check 2 correction
**Finding:** Lab 02 r3 Check 2 verified "the Related List component shows up on the record page." Tim: the stronger criterion is "the related list displays at least 1 case."
**Principle:** Success criteria for a Verify step should express the minimum thing that proves the lab's technique worked, not just that the component is present. A component with zero data looks like a bug to participants; a component with at least one record proves the plumbing is wired correctly.

#### #66 — Pre-seed data for environmental richness without making it participant-facing
**Tags:** generalizable principle, scaffolding
**Finding:** Lab 02's related-list demo would look sparse with only the Golden Record. Pre-seeding Cases makes the list demos feel real without changing lab instructions.
**Principle:** Scaffolding seeded data serves two purposes: (a) make lab demos look realistic, (b) smoke-test real-data behaviors. Lab text should NOT instruct participants to interact with seeded data directly; keep participant actions focused on the records they create themselves (Golden Record and later labs' built records). Seeded data is environmental.

#### #67 — Set admin-settable workshop defaults via scaffolding, not via lab steps
**Tags:** generalizable principle, scaffolding / workshop UX
**Finding:** Tim: "Should we add a step to place the ServicePulse 360 App as the top choice in the App Picker?" Analyzed: user-side App Launcher reordering isn't admin-forceable, but Default App on login is. Right answer: scaffold the Default App via Profile metadata, don't ask 20 participants to do it manually.
**Principle:** For any admin-settable workshop UX default (default app, default record page, default list view), configure it in the scaffolding rather than adding a lab step. Reduces per-participant setup burden and ensures consistency.

### Lab 02 r4 specific decisions

#### #68 — Opening Part 1 explicitly directs participants to their Golden Record
**Rationale:** r3's "Click your Golden Record from Lab 1" was easy to skip. r4 adds a Watch Out callout: "Open your Golden Record specifically. Opening a case with a different Record Type will make Part 2 harder to verify."

#### #69 — Watch Out callout about Record Type changes in production
**Rationale:** r4 Part 2.3 asks participants to switch Record Type on the Golden Record. In production, Record Type changes can trigger automation. The callout acknowledges this real-world concern while making clear the workshop context is safe.

#### #70 — Part 4 (optional second agency) dropped entirely
**Rationale:** Tim: "Let's remove this." The pattern is already demonstrated once in Part 2; a second agency extension adds length without new teaching.

---

## Round 7 — Lab 03 r1 smoke-test feedback (Tim, 2026-10-08)

Source: Tim's smoke-test of Lab 03 r1 against v3. 16 items captured, resulting in Lab 01 r8, Lab 02 r5, and Lab 03 r2.

### Generalizable principles

#### #71 — Setup UI changes can lag; provide fallback paths for navigation setup
**Tags:** generalizable principle, Lab 03 Part 1 correction
**Finding:** Adding Assets to the ServicePulse 360 app via App Manager didn't immediately reflect in the nav bar.
**Principle:** For any lab step that depends on Setup UI changes propagating to the Lightning UI (navigation items, record page activations, profile assignments), provide a manual UI-side fallback. For nav bar: pencil icon on the far right of the nav bar then Add More Items.

#### #72 — Instruct on things that exist in the UI; delete speculative "if present" instructions
**Tags:** generalizable principle, Lab 03 Part 2 correction
**Finding:** Lab 03 r1 Part 2 said "Click the Standard Related Lists link (if present) or look at the related lists panel." Nothing by that name exists in the current Setup UI.
**Principle:** Lab instructions should direct participants to concrete, verifiable things in the UI. If something's existence depends on org state or Salesforce release, call that out explicitly or remove the instruction. "If present" language is a smell.

#### #73 — Configure object layouts BEFORE creating records when the lab depends on the configured layout
**Tags:** generalizable principle, Lab 03 Part 3 restructure
**Finding:** Lab 03 r1 had participants create the parent Asset in Part 3, then create children in Part 4, then wrestle with missing fields and empty related lists. Tim: better to configure the Asset Layout first, so every record created inherits the configured layout.
**Principle:** When a lab needs specific fields or related lists visible during record creation (e.g., Parent Asset to make hierarchy explicit, Child Assets related list to drive subsequent creates), configure the layout before creating any records. One upfront setup block beats repeated back-and-forth.

#### #74 — Prefer creating child records from the parent's related list (auto-populates the parent lookup)
**Tags:** generalizable principle, Lab 03 Part 5 pattern
**Finding:** Lab 03 r1 had participants navigate back to the Assets tab for each child creation, then manually populate Parent Asset. Tim: use the parent's Child Assets related list, which auto-populates Parent Asset.
**Principle:** For hierarchy or lookup-driven relationships, prefer creating related records from the parent's related list rather than from the related object's main tab. Saves clicks, prevents mistakes, mirrors how admins actually work in production.

#### #75 — Use Save & New for repetitive record creation
**Tags:** generalizable principle, Lab 03 Part 5 pattern
**Finding:** Creating 4 Assets with the same pattern — Save & New keeps the user in the creation flow instead of landing on the detail page each time.
**Principle:** For labs that create 2+ similar records in sequence, use Save & New for all but the last.

#### #76 — Verify callouts should affirm success + guide troubleshooting, not just state the end state
**Tags:** generalizable principle, Lab 03 Verify format change
**Finding:** r1 ended sections with "Verify: [observable state]." Tim: better format is "Verified? Great job. This means [what the user has accomplished]" followed by "Common sticking points" callout with troubleshooting for that specific checkpoint.
**Principle:** Verify callouts have two jobs: (1) confirm success, (2) catch failures with specific recovery steps. A good Verify callout does both at the right level of specificity for the just-completed section. "Common sticking points" belongs AFTER the verify, scoped to the same checkpoint.

#### #77 — AssetRelationship is unidirectional; teach the directionality honestly
**Tags:** generalizable principle, standard object teaching
**Finding:** Lab 03 r1 said "The inverse appears on the related Asset's related list." Not true. AssetRelationship records only appear on the Primary Asset's Related Assets list.
**Principle:** When teaching a standard object relationship, be honest about directionality. If a record appears on only one side by default, say so. If participants want bidirectionality, teach them it requires two records. Don't hand-wave data-model details.

### Lab 03 r2 specific decisions

#### #78 — "Why this matters" expanded to mention Maintenance Plan + WorkOrder auto-generation
**Rationale:** Tim: real admins should know Asset's integration with Maintenance Plans. Not demonstrated in Lab 3 but worth mentioning as a value proposition for using standard Asset.

#### #79 — Golden Case record references throughout, not "Golden Record"
**Rationale:** Tim: clearer naming. "Your golden Case record" is more specific than "the Golden Record" when later labs may introduce other Golden-anything records.

#### #80 — Navigate Case to Asset via the Asset hyperlink, not via App Launcher
**Rationale:** Tim: cleaner workflow. Shows the natural way a user traverses relationships in Lightning.

### Lab 02 r5 and Lab 01 r8 (cascading dependencies)

#### #81 — Dedicate a tab on the Case record page for cross-cutting related data
**Tags:** generalizable principle, record page UX
**Finding:** Lab 2 r4 placed Related List - Single on the Details tab. Lab 3 would add another, cluttering Details. Tim: create a dedicated Other related cases tab for both, keeping Details clean.
**Principle:** For record pages that accumulate multiple cross-cutting related lists through a workshop (or in production over time), reserve a dedicated tab for them. Prevents the Details tab from becoming a scroll-fest.

#### #82 — Lab 01 r8 pre-stages dependencies for Lab 03
**Rationale:** The Asset field on Case was needed in Lab 03 but wasn't in Lab 01's Case Layout. Lab 01 r8 adds Asset to Part 6.2 (classic layout) and Part 9.5 (Dynamic Forms canvas) so Lab 03 Part 7 doesn't need workarounds. Earlier labs should pre-stage every dependency later labs rely on.

---

## Round 8 — Lab 04 r1 smoke-test (Tim, 2026-10-08)

Source: Tim's smoke-test of Lab 04 r1 against v3.

#### #83 — Verify related list availability against the actual object before instructing to add it
**Tags:** generalizable principle, Lab 04 Part 3 correction
**Finding:** Lab 04 r1 Part 3.4 asked participants to add a Cases related list to the WorkOrder Layout. The Cases related list isn't available on WorkOrder because the relationship is many-to-one from WorkOrder's side: each WorkOrder references at most one Case via a lookup field. Related lists only make sense on the one-side of one-to-many relationships.
**Principle:** Before instructing participants to add a related list to a page layout, verify the relationship exists in the correct direction. Lookups create related lists on the parent (lookup target) side, not on the many-side (lookup source). WorkOrder.CaseId makes Work Orders a related list on Case, but Cases is NOT a related list on WorkOrder.

#### #84 — Teach relationship cardinality when the natural participant assumption is wrong
**Tags:** generalizable principle, pedagogy
**Finding:** Participants coming from "every object has a Related tab, so I can related-list anything" need to see cardinality explicitly. The right UX for many-to-one is the hyperlinked lookup field, not a one-row related list.
**Principle:** When a lab's natural flow would have participants adding a related list that doesn't exist (or that would only ever contain one row), surface the cardinality explicitly in a Why callout. The lesson is pedagogically richer than the fix.

---

## Round 9 — Lab 04 r2 smoke-test + cross-lab sweep (Tim, 2026-10-09)

Source: Tim's smoke-test of Lab 04 r2 against v3. 14 items captured, resulting in Lab 01 r9, Lab 02 r6, Lab 03 r3, and Lab 04 r3 — the first cross-lab sweep.

### Generalizable principles

#### #85 — Remove schedule-dependent language from lab titles and references
**Tags:** generalizable principle, writing style, cross-lab
**Finding:** Lab titles like "Day 1 Lab 4" and references like "Day 2 extends this" lock the workshop to a specific schedule. If timing slips (deliver Day 1 content on a different day, run a half-day workshop, split delivery), the labels break.
**Principle:** Lab titles use "Lab N" not "Day X Lab N." Cross-lab references use "In Lab N" or "The subsequent hands-on labs" rather than "Day 2 content." Keeps the material reusable across schedule variations.

#### #86 — Use object Labels, not API names, in all prose
**Tags:** generalizable principle, writing style, cross-lab
**Finding:** Lab prose referenced "WorkOrder," "AssetRelationship," "ServiceAppointment" in body text. These are API names (concatenated, PascalCase). Participants see the Label versions in the UI: "Work Order," "Asset Relationship," "Service Appointment." Mismatch is confusing.
**Principle:** Prose uses the Label (as seen in the UI). API names appear only when discussing SOQL, Apex, or metadata explicitly. Standard object API names to Label mapping includes: WorkOrder → Work Order, WorkType → Work Type, ServiceAppointment → Service Appointment, AssetRelationship → Asset Relationship, AssetStatePeriod → Asset State Period. Keep custom object API names as-is (Service_Disruption__c appears with its API suffix because that's how participants will see it after building the object).

#### #87 — "Where you should be" callouts were inconsistent with lab style
**Tags:** generalizable principle, writing style, cross-lab
**Finding:** Lab 01 through Lab 04 r2 used blue NAV_COLOR callouts labeled "Where you should be" to preface Setup navigation steps. Tim: these feel out of place alongside the other callouts (Why/Verify/Watch out/Tip). The instructions that follow are already clear.
**Principle:** Don't use navigation-breadcrumb callouts before every Setup section. Let the first step of each section carry the Setup navigation inline. Reduces visual noise. Keep callouts for signal (teaching, verification, pitfalls, tips), not for breadcrumbs.

#### #88 — Em dashes stay in section headers, swept from prose body
**Tags:** generalizable principle, writing style, cross-lab
**Finding:** Em dashes keep slipping into prose despite the standing rule. The sweep targets prose body (b.bullet, b.para, b.step, b.substep, b.callout) but leaves em dashes in section headers (b.h1, b.h2, b.h3) because those serve as structural separators.
**Principle:** Em dashes in headers are OK as "Section Title - Content Description" separators. Em dashes in prose body text should be replaced with commas, parentheses, or sentence splits per the standing [[feedback-no-em-dashes]] rule.

#### #89 — Trim object page layouts BEFORE participants interact with them
**Tags:** generalizable principle, UX pattern, cross-lab
**Finding:** Tim: "Before section 2.2, I wouldn't mind stepping through a quick update of the page layout so users don't have to even see all of the fields that we're leaving blank. It feels messy." Applied to Work Type Layout in Lab 4; same principle applies to Case Layout and Asset Layout (already done in Labs 1 and 3).
**Principle:** When a lab creates records of a specific type, trim the record's page layout first (even if the only cleanup is removing fields participants won't populate). Participants shouldn't see fields they'll leave blank. Layout-first is a workshop UX principle.

#### #90 — Pre-stage related-list prerequisites in earlier labs rather than mid-lab setup
**Tags:** generalizable principle, cross-lab coherence
**Finding:** Lab 4 Part 5.2 depends on the Work Orders related list being on the Asset Layout. Tim: add this to an earlier lab (Lab 3 r3 Part 3.6) rather than making Lab 4 do the setup.
**Principle:** When a later lab needs a prerequisite related list, page layout field, or configuration, add it to the earliest lab that already touches the relevant object's layout. Keeps individual labs focused and avoids participants doing the same object's layout work twice.

---

## Round 10 — Lab 05 r1 smoke-test (Tim, 2026-10-09)

Source: Tim's smoke-test of Lab 05 r1 against v3. 25-item batch triggering Lab 05 r2.

### Generalizable principles

#### #91 — "Walk" vs "walk through"
**Tags:** generalizable principle, writing style
**Finding:** "Walk the standard-fit test" and "Walk the four candidates" read as terse. The instructional phrasing is "walk through."
**Principle:** When directing participants through a sequence (checks, candidates, steps), use "walk through." Reserve bare "walk" for literal physical motion (which doesn't appear in these labs anyway).

#### #92 — Standard-fit test phrasing uses "Could the X object..."
**Tags:** generalizable principle, writing style, pedagogy
**Finding:** Lab 05 r1 phrased test candidates as "Could Case model..." Tim: better as "Could the Case object model..." Explicit noun phrasing is clearer for newer admins who may not instantly map "Case" as a shorthand for "the Case object."
**Principle:** First mentions of a standard object in prose use "the X object" rather than bare "X." Subsequent mentions in the same paragraph can shorten to just the object name. Knowledge is the exception: "a Knowledge article" (lowercase, article as the noun).

#### #93 — Spelled-out click sequences for every form field
**Tags:** generalizable principle, lab authoring
**Finding:** Lab 05 r1 batched "for each field, click New, choose type, Next, fill properties, Save & New." Participants need every intermediate click spelled out including: radio button for picklist entry, "Use first value as default" checkbox, "Restrict picklist to the values" un-check, Required checkbox, Auto add to custom report type checkbox, Next (FLS), Save & New (Page Layouts).
**Principle:** For form flows with multiple screens (field wizard, record type wizard, Flow Builder), spell out each screen's required action, even if the pattern is identical across fields. "Click Next" is a real step, not an implicit one.

#### #94 — Record Type Make Available step soft phrasing
**Tags:** generalizable principle, writing style
**Finding:** Lab 05 r1 said "check System Administrator" as a hard instruction. Softer phrasing: "keep it checked, we just want to make sure System Administrator has access."
**Principle:** For checkbox-defaults steps where the lab's goal is to confirm (rather than change) the state, phrasing should be "keep X checked" or "verify X is checked" rather than "check X." Softer, less likely to lead a participant into double-clicking or confusion.

#### #95 — Watch Out callouts for API name edge cases
**Tags:** generalizable principle, lab authoring
**Finding:** B&T Record Type Name may render as B_T (not BandT) when the Label is B&T. Lab 05 r1 said "BandT" without warning participants about the render.
**Principle:** When an object name or API name has edge-case rendering (ampersand, slash, parentheses, non-ASCII), add a Watch Out callout explaining what the UI will show and what to correct it to. Observed behavior varies by Salesforce release.

#### #96 — Field creation adds to Dynamic Forms-enabled page in the wizard
**Tags:** generalizable principle, lab authoring, Lightning behavior
**Finding:** Lab 05 r1 had a redundant Part 4.2 that manually dragged the Service Disruption field onto the Case Lightning page. The lookup wizard itself has a Dynamic Forms-enabled record page step that places the field automatically.
**Principle:** When creating a lookup or custom field on an object with a Dynamic Forms Lightning page, the wizard offers an in-flow step to add the field to the Dynamic Forms canvas. Teach this step as part of the field creation flow, not as a separate manual-drag step afterward.

#### #97 — Layout-first before record creation, applied to custom objects too
**Tags:** generalizable principle (from Round 7, reinforced)
**Finding:** Lab 05 r1 jumped from creating fields to creating records. Tim: insert a Part that configures the Service Disruption Layout and Lightning record page BEFORE creating the first record, same as Labs 3 (Asset Layout) and 4 (Work Type Layout, Work Order Layout).
**Principle:** The layout-first pattern applies to custom objects as rigorously as to standard objects. Configure the record's layout once up front; every record created afterwards inherits a clean view.

#### #98 — "Verified? Great job!" with no trailing colon
**Tags:** generalizable principle, writing style
**Finding:** The pattern was "Verified? Great job!: [content]" with a trailing colon after the exclamation. Tim: exclamation mark alone, no colon.
**Principle:** Verify callouts use "Verified? Great job!" followed by the content as the next sentence of the callout. No colon.

#### #99 — Common sticking points use bullets, not multi-line single callout
**Tags:** generalizable principle, formatting
**Finding:** Lab 05 r1 used a single callout with "\n\n" separators between sticking points. Word rendered these as paragraph breaks but not visible bullets.
**Principle:** For enumerated troubleshooting content, use separate b.bullet() calls under a dedicated h2 "Common sticking points" section, not a single multi-line callout.

#### #100 — Verrazzano spelling verification
**Tags:** generalizable principle, factual accuracy
**Finding:** Tim: "Verrazano spelling needs to be corrected on Field 6 and possibly in other spots." Correct spelling: Verrazzano (two Zs).
**Principle:** Audit MTA proper nouns against official sources. For named infrastructure: Verrazzano-Narrows Bridge (preferred), Hugh L. Carey Tunnel, Robert F. Kennedy Bridge, Grand Central Terminal.
