# gh-omens

A joke script and GitHub CLI extension that checks `githubstatus.com` and reads the omens on whether GitHub is likely to fall over in the next hour.

## Standalone usage

```bash
chmod +x ./gh-omens ./omens
./omens
```

or run the main script directly:

```bash
./gh-omens
```

Example output:

```text
nah she'll be right
risk score: 0
because: githubstatus.com says everything is operational
```

## GitHub CLI extension usage

The extension executable is:

- `gh-omens`

When installed as a GitHub CLI extension, you run it as:

```bash
gh omens
```

Install it from GitHub with:

```bash
gh extension install sandermvanvliet-stack/gh-omens
```

For local testing, use a clone or directory named `gh-omens`:

```bash
git clone git@github.com:sandermvanvliet-stack/gh-omens.git gh-omens
cd gh-omens
gh extension install .
gh omens
```

### Reinstall note

If you installed an earlier version of the extension and see this error:

```text
env: bash\r: No such file or directory
```

remove and reinstall the extension:

```bash
gh extension remove gh-omens
gh extension install sandermvanvliet-stack/gh-omens
```

The repo now includes `.gitattributes` to force LF line endings for the shell scripts, which avoids that issue on systems with Git `core.autocrlf=true`.

## Requirements

You just need:

- `bash`
- either `curl` or `wget`
- standard shell tools like `grep`, `sed`, `awk`, and `tr`
- optionally `gh` if you want to run it as an extension

## How it works

It pulls data from these GitHub Status API endpoints:

- `https://www.githubstatus.com/api/v2/status.json`
- `https://www.githubstatus.com/api/v2/incidents/unresolved.json`
- `https://www.githubstatus.com/api/v2/components.json`
- `https://www.githubstatus.com/api/v2/scheduled-maintenances/active.json`
- `https://www.githubstatus.com/api/v2/scheduled-maintenances/upcoming.json`

Then it adds up a silly little risk score based on:

- overall status indicator
- unresolved incidents
- non-operational components
- active or upcoming maintenance

If the score is `4` or higher, it declares that GitHub is likely to tank.

It also picks a random response from a pool of normal and extra-chaotic Aussie lines.

This is a gimmick, not a predictor. Please do not use this as the basis for life decisions, trading strategies, release trains, or spiritual guidance.
