# Volopay Assignment — Revenue Intelligence Inbox

## What is included
- `index.html`: working local-first web app; no build step or API key required.
- `data/01_initial.json`, `data/02_update.json`: original supplied batches.
- `exports/manifest.json` and `exports/manifest.csv`: record-level output manifest.
- `exports/outputs/{call,meeting}/`: one JSON analysis/output per source record.
- `Revenue_Intelligence_Decisions.pptx`: five-slide decision deck.
- `College_Event_Plan_TNWISE_Next_Edition.docx`: proposed event plan; verify event facts before submitting.
- `Revenue_Inbox_3min_Demo_Script.txt`, `College_Event_5to8min_Video_Script.txt`: narration guides.

## Run the app
1. Extract this ZIP folder.
2. Open `index.html` in an up-to-date Chrome or Edge browser.
3. It loads the post-update demo state in browser local storage. No server or credentials are needed.
4. Use the buttons at the top to replay the import test:
   - Click **Reset demo** to start clean.
   - Click **Import initial batch**; unique records should be 44.
   - Click **Repeat initial import**; count should remain 44 and records should not duplicate.
   - Select M07 and choose a manual route (for example Product / integration); save it.
   - Click **Apply late update (M07)**. The newer transcript should appear; unique count remains 44 and the manual route is retained.
   - Click **Reset demo** then apply update to start over if needed.
5. Click **Export current state** to download a JSON bundle and CSV manifest from the live app.

## Metrics and definitions
- Selected records: unique identities keyed by `(source_type, source_id)`. The package has 30 calls and 14 meetings.
- Usable text coverage: nonblank call transcript or at least one nonblank meeting turn. 17 texts are available initially; 18 after the update. Coverage does not prove recording or attendance.
- Source-reported connection rate: calls with `is_connected=true` divided by calls where `is_connected` is not null. Unknown flags are excluded and counted separately.
- Activity date: call `started_at`; meeting `starts_at`, interpreted in Asia/Kolkata.
- Person grouping: calls use rep name; meetings use organiser email. Organiser is not assumed to be salesperson or attendee.
- Suggested routes are deterministic keyword-assisted triage and should be reviewed by a human. No live AI model is called. The output keeps evidence, route rationale, and next-step guidance visible.
- M07 has a manual Product / integration override in the pre-generated export example and is marked `Needs review` because the late transcript changes the evidence.

## Exports
Each manifest `output_path` is relative to `exports/` and points to an actual JSON output. Outputs preserve the source payload and supplied transcript, plus route(s), review state, manual override, analysis freshness, reason and next step. Export paths are not links to a developer machine.

## Three important findings
1. **M07 — workaround does not equal resolution.** Meeting M07, turns 12–14: uploading from the invoice inbox works, but the direct Recreate payment path remains an issue. Product / integration route and a visible review state make this distinction explicit.
2. **M01 — eligibility boundary matters.** Meeting M01, turn 2: the discussion says the service is for registered businesses, not personal accounts. Partnership route should validate eligibility before a referral or promise.
3. **M02 — market requirement is unconfirmed.** Meeting M02, turn 5: the speaker says they need to check a specific customer requirement. Do not claim coverage or compliance until validated; route to partnership/product follow-up.

## Deliberately rejected decision
A rep leaderboard based on connection rate was considered and rejected. The data is a selected sample, not a representative team-day dataset; connection flags can be unknown or conflict with text; meeting organisers are not confirmed sales owners; and there is no authoritative opportunity table. The product therefore shows carefully denominated activity/coverage and avoids ranking people or inventing pipeline value.

## Known limitations / AI use
- Analyses are pre-generated, deterministic keyword-assisted suggestions, not live AI. A source update marks analysis for review instead of pretending old analysis is fresh.
- No CRM join, verified account history, staff directory, audio/video, or reliable deal value is supplied.
- The web app is local-first. To submit a public/private deployed URL, host `index.html` using a static hosting service and ensure the reviewer can open it. I cannot create a hosted deployment without your hosting account/access.
- Approximate effort: fill in your actual time spent before submitting.
- AI assistance was used to scaffold the UI and draft the explanatory materials. Review and personalise all findings and event assumptions before submission.
