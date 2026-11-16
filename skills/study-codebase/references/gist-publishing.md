# Publish the Study as a GitHub Gist

Load this only when the user explicitly requested Gist delivery. Upload the completed local study with its repository URL and commit SHA intact.

## Visibility, redaction, and auth check

Honor requested visibility; otherwise default to a **secret** Gist and state that choice explicitly (`secret` is unlisted, not access-controlled — anyone with the URL can read it). Never upload credentials or unauthorized proprietary source in either mode; if sensitive material is involved, keep the note local until disclosure scope is cleared.

Verify `gh auth status` (or the host's authenticated GitHub tool) before uploading. If Gist scope or auth is missing, keep the local artifact intact and report the exact capability gap without claiming publication.

## Idempotent upload and raw verification

Pass the exact Markdown file path (never a wildcard) so formatting survives intact, adding `--public` only when explicitly requested:

```bash
gh gist create /abs/path/project-study.md --desc "Codebase study: <project> @ <short-sha>"
```

Record the returned URL immediately, then fetch back the raw file and metadata to confirm byte-for-byte content and visibility before reporting success:

```bash
gh gist view <GIST_URL> --raw --filename project-study.md
```

If `gist create` times out or returns an ambiguous result, list recent Gists (`gh gist list --limit 5`) to check whether it landed before retrying so duplicate Gists are never left behind. Modify an existing Gist only when the user named that target Gist explicitly, preserving any sibling files and existing visibility.
