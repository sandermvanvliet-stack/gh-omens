# github-crystal-ball

A joke script that checks `githubstatus.com` and gives you a wildly unqualified prediction about whether GitHub is likely to fall over in the next hour.

## Usage

```bash
chmod +x ./github-crystal-ball
./github-crystal-ball
```

Example output:

```text
nah she'll be right
risk score: 0
because: githubstatus.com says everything is operational
```

## Requirements

It is now a Bash script.

You just need:

- `bash`
- either `curl` or `wget`
- standard shell tools like `grep`, `sed`, `awk`, and `tr`

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

This is a gimmick, not a predictor. Please do not use this as the basis for life decisions, trading strategies, or release trains.
