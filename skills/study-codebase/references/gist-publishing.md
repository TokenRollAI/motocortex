# Publish the study as a GitHub Gist

Use this guide only when Gist delivery is requested. Publish the completed study file, keeping its source attribution and revision information intact.

## Resolve publication scope

Honor the requested visibility. When unspecified, use a secret Gist and state that choice in the delivery. Secret means unlisted, not private: anyone with its URL can read it. Keep credentials and private source material out of either visibility mode unless disclosure of that material has been explicitly authorized. If the study contains such material, prepare the local note first and resolve its disclosure scope before uploading.

Use the available authenticated GitHub connector or CLI. With the CLI, check `gh auth status` and the installed `gh gist create --help` before publishing. If authentication or Gist access is missing, retain the complete artifact and report what is needed without exposing credentials or claiming publication.

## Create and verify

Pass the prepared Markdown file directly so multiline content is preserved. For example:

```bash
gh gist create /path/to/project-study.md --desc 'Project codebase study'
```

Add `--public` only for requested public visibility. Use the exact study file, not a directory wildcard. Treat the returned URL as the publication identifier and retain it immediately.

Retrieve the published file with the connector or CLI and compare it to the local note:

```bash
gh gist view GIST_URL --raw --filename project-study.md
```

Verify visibility through the returned Gist metadata or page, and report the URL only as verified after checking the file and visibility. If a create request has an ambiguous outcome, inspect recent Gists for the matching file and content before retrying; repeated creates can leave duplicate publications. A verification failure calls for checking the existing Gist, not creating another one. Updating an existing Gist requires a user-specified target and update intent; preserve its unrelated files and visibility.

## Official references

- [Creating Gists and visibility semantics](https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/creating-gists)
- [GitHub CLI: gist create](https://cli.github.com/manual/gh_gist_create)
- [GitHub CLI: gist view](https://cli.github.com/manual/gh_gist_view)
