# generate-changelog

Generate a structured `CHANGELOG.md` from Git history since the latest tag.

## Setup — 3 steps

1. Copy the `bounty-1` directory into your repository.
2. Run `chmod +x bounty-1/generate-changelog`.
3. Run `bounty-1/generate-changelog`.

That writes `CHANGELOG.md` in the target repository and preserves older
entries. Use `--stdout` to preview without writing.

## Examples

```bash
bounty-1/generate-changelog
bounty-1/generate-changelog --since v1.2.0
bounty-1/generate-changelog --since v1.2.0 --until v1.3.0 --heading v1.3.0
bounty-1/generate-changelog --stdout
```

The default range is `LATEST_TAG..HEAD`; if the repository has no tags, all
reachable commits are used.
## Categories

- `feat`, `add`, `new` → **Added**
- `fix`, `bug`, `patch` → **Fixed**
- `remove`, `delete`, `deprecate` → **Removed**
- `refactor`, `perf`, `docs`, `test`, `chore`, `ci`, `build`, and uncategorized → **Changed**

Conventional scopes such as `feat(api): ...` are supported. `!` or a
`BREAKING CHANGE:` footer adds a `BREAKING` marker without duplicating the
entry in a second section.

Git records use ASCII unit/record separators instead of printable delimiters,
so subjects containing pipes or other common punctuation do not corrupt
parsing.

## Verification

```bash
python3 -m unittest discover -s bounty-1/tests -v
python3 -m py_compile bounty-1/generate_changelog.py
```

A generated example from a real GitHub repository is included at
`samples/requests-changelog.md`.