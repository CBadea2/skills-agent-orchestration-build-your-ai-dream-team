# Project Pulse implementation plan

## Summary

Build a lightweight static Project Pulse dashboard that shows project names, owners, status, recent activity, priority or risk, and contributor-friendly summaries. Use the brief’s fixed JSON schema, semantic accessible markup, and responsive project cards. Serve the app locally so it loads from `app/index.html`, not a directory listing. No framework or package installation is needed.

## Ordered implementation steps

1. **Agree on the UI contract — Designer, with Orchestrator.** Define the information hierarchy, card layout, accessible status and priority treatment, responsive behavior, and shared selectors before implementation. Keep visual guidance aligned with the brief and the exercise’s required `.dashboard` and `.project-card` hooks.
2. **Implement in parallel after the contract is agreed.**
   - **Designer — `app/styles.css`:** Create the polished, responsive visual treatment. Include `.dashboard`, `.project-card`, readable spacing and contrast, status/priority affordances, `border-radius`, and `box-shadow`.
   - **Coder — `app/index.html`:** Build the page with the exact title “Project Pulse”; reference `styles.css` and `project-data.json`; render project cards showing name, owner, status, recent activity, priority, and summary. Include accessible labels and clear empty/error states. Ensure the source references the required field names, including `recentActivity`.
   - **Coder — `app/project-data.json`:** Create valid JSON with a top-level `projects` array. Each entry must include `name`, `owner`, `status`, `recentActivity`, and `priority`, with useful contributor-friendly sample content.
   - **Coder — `.vscode/launch.json`:** Create strict JSON with a **Run Project Pulse Dashboard** configuration. Use `python3 -m http.server 5500`, set the working directory to `${workspaceFolder}/app`, and configure `serverReadyAction` to open `http://localhost:%s/index.html`.
3. **Integrate and review — Orchestrator, with Designer and Coder as needed.** Check that markup selectors match the stylesheet and that the page loads and renders the JSON data. Assign any fixes to the owner of the affected file; avoid overlapping edits.
4. **Validate the integrated result — Orchestrator.** Run the checks below and manually launch the dashboard in VS Code.

## Dependencies and parallel work

- Step 1 precedes implementation: Designer and Coder need a shared selector and layout contract.
- Once that contract is agreed, Designer’s stylesheet and Coder’s three files can be authored in parallel because ownership does not overlap.
- Coder owns both the HTML and JSON, so the data schema and rendering logic can be kept consistent. The page must be served over HTTP for JSON fetching; `file://` preview is not a valid runtime check.
- Integration, launch, and visual validation must happen sequentially after all four files are present.

## Edge cases and risks

- Malformed or unavailable JSON, an empty `projects` array, or missing/blank field values should not produce a broken or confusing page.
- Keep status and priority distinguishable without relying on color alone; check contrast, keyboard focus, and narrow-screen wrapping.
- A port already in use or a launch working-directory error can prevent preview. Confirm the configured server opens `index.html`, not the server root/directory listing.
- Use the repository’s specified Python server command and avoid introducing unnecessary runtime or build dependencies.

## Validation expectations

- Run `python3 -m json.tool app/project-data.json` and `python3 -m json.tool .vscode/launch.json`; both must pass.
- Run `bash scripts/validate-exercise.sh` from the repository root. This checks the repository’s existing exercise conventions and that learner output files are not tracked; leave git staging and commits to the learner.
- Confirm the dashboard source includes the exact title, stylesheet/data references, required field names, and `project-card` markup; confirm the stylesheet includes `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`.
- In VS Code, run **Run Project Pulse Dashboard**. Confirm the browser opens `http://localhost:5500/index.html`, project cards render from JSON, the page is not a directory listing, and the layout remains readable at narrow widths. Stop the server after checking.

## Open questions

- None blocking. The brief and exercise steps specify the data fields, launch command, port, working directory, and launch URL. Designer and Orchestrator should settle the visual details within those constraints.
