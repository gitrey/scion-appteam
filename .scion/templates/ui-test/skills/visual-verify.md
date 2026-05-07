---
name: visual-verify
description: Perform visual and functional UI verification using Chrome DevTools
---

# /visual-verify — Visual and Functional UI Verification

## Trigger

User invokes `/visual-verify` with a target URL and a specification ID (e.g.,
`/visual-verify "http://localhost:3000" "F-0031"`).

## Instructions

1. **Launch Browser & Navigate** — Use the native Chrome DevTools MCP `navigate` tool to load the target URL, ensuring the `headless` parameter is explicitly set to `true` to avoid opening GUI windows:
   ```json
   {
     "url": "<target-url>",
     "headless": true
   }
   ```
2. **Audit Baseline State** — Check for initial rendering correctness:
   - Capture a baseline screenshot using the native `screenshot` tool.
   - Save the screenshot as `docs/screenshots/<spec-id>-baseline.png`.
3. **Simulate User Interactions** — Based on the spec's acceptance criteria in
   `docs/specs/<spec-id>-*.md`:
   - Use `click` or `hover` on target UI elements (buttons, dropdowns, toggles).
   - Use `fill` or `type` to enter test data into input fields.
4. **Verify State Transitions** — After interactions are complete:
   - Capture an updated state screenshot.
   - Save the screenshot as `docs/screenshots/<spec-id>-interaction-state.png`.
5. **Monitor Console & Network Logs:**
   - Review the page context for any failed network requests (4xx/5xx) or
     JavaScript runtime console errors.
   - Report any warning or error logs in the final summary.
6. **Groom & Commit Screenshots** — Stage and commit the captured verification
   screenshots:
   ```bash
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" add docs/screenshots/
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" commit -m "test(ui): add visual verification screenshots for <spec-id>"
   ```
7. **Verification Report Summary** — Present a concise visual QA report back to
   the user:
   - List verified acceptance criteria.
   - Provide markdown links to the saved screenshots.
   - Note any console errors or visual discrepancies found.

## Project Context

- **Project:** appteam
