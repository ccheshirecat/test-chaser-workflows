# Test Chaser Workflows

This repository benchmarks Chaser sandboxes as GitHub Actions runners.

## Run the Benchmark

1. Go to **Actions** tab
2. Select **Chaser Sandbox Runner Benchmark**
3. Click **Run workflow**
4. Select runner type (leave as `chaser` to test Chaser)

## Runner Labels

- `chaser` - Chaser sandbox runners
- `blacksmith` - Blacksmith runners (if configured)
- `depo` - Depo runners (if configured)

## Metrics Collected

- CPU/Memory/Disk info
- Git clone speed (Linux kernel)
- Node.js/npm performance
- Python performance
- Rust compilation time
- File I/O (read/write)
- Network speed

## Setup for Self-Hosted Chaser Runners

See [chaser-docs](https://github.com/ccheshirecat/chaser-docs) for runner setup instructions.
