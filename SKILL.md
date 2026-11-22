---
name: kdp-workflow-orchestrator-addon
description: Coordinate the numbered 28-skill KDP ebook workflow, maintain its project manifest and handoffs, and resolve legacy numbering/path conflicts without editing legacy skill files. Use at project start, stage transitions, or when a required artifact or approval is unclear.
---
# KDP Workflow Orchestrator Add-on

Use `WORKFLOW_INDEX.md` as the canonical order and `COMPATIBILITY_MAP.md` as the input/output crosswalk. These bundle-level files control routing and path reconciliation only. They do not rewrite the legacy cards' procedures or decisions.

## Immutable-source rules
- Preserve all 23 legacy skill cards and source ZIPs byte-for-byte. Do not rename, edit, delete, or silently rewrite them.
- Create project artifacts only in the active project. Never publish, upload, spend money, or change an account.
- Do not treat filename existence as proof of content, approval, or quality. Verify project identity, version, evidence, and gate status.
- If original cards conflict on substantive policy or rights, stop with `BLOCKED — Error / Tried / Next`. The index resolves canonical order only; it cannot invent a substantive resolution.

## Start the project
1. Inventory source archives and project files. Record filenames, SHA-256 where available, and which materials are originals versus add-ons.
2. Record project ID, title, author/pen name, genre, reader, language, marketplace, territories/rights, selected formats, target date, budget, AI-use status, and decision owner. Unknowns remain `UNKNOWN`.
3. Create a dated manifest, artifact register, decision log, source ledger, and initial risk list. Use the templates bundled in `templates/`.
4. Map each canonical stage 01–28 to exact required inputs, outputs, owner, evidence, status, and gate. Use `COMPATIBILITY_MAP.md` to record legacy path aliases; never change an original card to normalize a path.
5. Confirm the required prior gates before starting a stage. For the ebook path, print and audiobook branches are optional and must be selected explicitly.
6. Run `scripts/verify_bundle_integrity.py` on the delivered bundle when available. A successful integrity check verifies packaging, not KDP compliance or a real-book pilot.

## Resolve a legacy path mismatch
1. Record the source artifact path, expected downstream path, stage numbers, title/version, and mismatch in the artifact register.
2. Prefer a register alias that points to the original file. If downstream tooling requires a physical path, make a byte-identical copy only; record source and copy hashes and verify them.
3. If different status fields or formats must be reconciled, create a separate adapter note that links to the source evidence, quotes the exact verdict, maps fields transparently, and identifies the reviewer. Never manufacture a PASS, add approval not present in the source, or conceal that it is an adapter.
4. If semantics differ or evidence is missing, block the handoff for human decision.

## At every handoff
Check that required inputs exist, open correctly, match project title/language/edition, and carry a version/date. Confirm explicit human decisions. Pass the artifact link/path, status, evidence, open issues, and next canonical number. `DRAFT`, `REVISE`, `BLOCKED`, or pending approval cannot advance as `PASS`.

Use only these statuses: `NOT STARTED`, `IN PROGRESS`, `DRAFT`, `AWAITING HUMAN APPROVAL`, `PASS`, `REVISE`, `BLOCKED`, or `NOT APPLICABLE` with a reason. A PASS requires all stage acceptance checks, not just a generated file.

## Required control artifacts
- `00_Project_Control/project_manifest_<shortname>_<yyyymmdd>.md`
- `00_Project_Control/artifact_register_<shortname>_<yyyymmdd>.csv`
- `00_Project_Control/decision_log_<shortname>_<yyyymmdd>.md`
- `00_Project_Control/source_ledger_<shortname>_<yyyymmdd>.csv`
- `00_Project_Control/risk_register_<shortname>_<yyyymmdd>.md`

Before calling the workflow operationally validated, complete `PILOT_ACCEPTANCE_TEST.md` with one real project. Until that evidence exists, label the workflow `DESIGN-READY; PILOT NOT RUN`—never claim a 10/10 operational rating.