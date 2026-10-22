# vale-crossing-action

Security research lab. **Not production, not affiliated with Elastic.**

Stands exactly where `elastic/docs-actions/vale/lint@v1` stands in the composition under
test: a remote, pinned action whose own files a pull request to the caller cannot modify.

- The "Determine files to lint" step is copied byte for byte from
  `elastic/docs-actions` `vale/lint/action.yml` at `ee16641f`, including the
  `# zizmor: ignore[template-injection]` suppression and the E2BIG comment above it.
- The "Upload Vale results" step is copied from the same file.
- `vale_reporter.py` stands in for the generator the real action invokes at
  `action.yml:679` with `python3 ${{ github.action_path }}/vale_reporter.py`, after the
  sink has already run. Same contract: it writes `vale_results.json` and
  `issue_counts.txt` into the workspace.
