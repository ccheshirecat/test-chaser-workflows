# Test Chaser Workflows

This repository benchmarks Chaser sandboxes as GitHub Actions runners.

## Workflows

### 1. Chaser Runner Test (`test-runner.yml`)
Simple test to verify Chaser sandbox runners work.

**Trigger:** Actions → Chaser Runner Test → Run workflow

```yaml
runs-on: [self-hosted, chaser]
```

### 2. Chaser Benchmark (`chaser-benchmark.yml`)
Comprehensive benchmark comparing:
- Chaser sandbox runners
- Standard GitHub runners
- Blacksmith runners
- Depo runners

**Trigger:** Actions → Chaser Sandbox Runner Benchmark → Run workflow → Select runner type

### 3. Standard Runner Test (`test-standard.yml`)
Baseline test on standard GitHub runners for comparison.

## Setting Up Chaser as Self-Hosted Runner

### Option 1: GitHub App (Recommended for Organizations)

1. Create a GitHub App in your organization settings
2. Set the following permissions:
   - `actions: write` - Register/unregister runners
   - `contents: read` - Clone repos
   - `workflows: write` - Update workflow runs

3. Subscribe to events:
   - `workflow_job`

4. Install the app on your organization/repository

5. The app should call GitHub API to register runners when jobs come in:

```python
# Example registration
POST /repos/{owner}/{repo}/actions/runners
{
  "name": "chaser-runner-{session_id}",
  "labels": ["chaser", "self-hosted"]
}
```

### Option 2: Personal Access Token

For testing, create a PAT with `repo` and `workflow` scopes.

### Runner Registration Flow

1. Chaser sandbox starts
2. Runner registers with GitHub via API
3. GitHub dispatches `workflow_job` event
4. Runner picks up job
5. Runner executes job steps
6. Runner unregisters when done

## Runner Labels

| Label | Description |
|-------|-------------|
| `chaser` | Chaser sandbox runners |
| `self-hosted` | Standard self-hosted label |

## Troubleshooting

### Jobs stuck in queue
- Check runner is registered: Settings → Actions → Runners
- Check GitHub App is installed and has correct permissions
- Check runner is online and can reach GitHub API

### Runner not picking up jobs
- Verify labels match in workflow and registration
- Check runner logs for registration errors

## Benchmark Results

See [Wiki](https://github.com/ccheshirecat/test-chaser-workflows/wiki) for benchmark results.

## Quick Test

1. Fork this repo
2. Go to Actions tab
3. Run "Chaser Runner Test" workflow
4. Watch the Chaser sandbox pick up and execute the job
