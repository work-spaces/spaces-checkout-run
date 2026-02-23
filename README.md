# spaces-checkout-run

Github Action for executing a [spaces](https://github.com/work-spaces/spaces) checkout/spaces run sequence.

This action installs the `spaces` CLI, runs `spaces checkout` (or `spaces checkout-repo`) to create a workspace, then runs `spaces run` in that workspace.

## Usage

### Checkout a repository and run targets

```yaml
steps:
  - name: Checkout and Run with Spaces
    uses: work-spaces/spaces-checkout-run@v0.1.0
    with:
      checkout-url: https://github.com/my-org/my-repo
      checkout-rev: ${{ github.sha }}
      workspace: my-workspace
      run-target: //:test
```

### Checkout using starlark scripts and run targets

```yaml
steps:
  - name: Clone workflows
    run: git clone https://github.com/work-spaces/workflows.git

  - name: Checkout and Run with Spaces
    uses: work-spaces/spaces-checkout-run@v0.1.0
    with:
      checkout-scripts: |
        workflows/preload
        workflows/my-workflow
      workspace: my-workspace
      run-target: //:build
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `checkout-url` | URL of the repository to checkout (uses `spaces checkout-repo`; mutually exclusive with `checkout-scripts`) | No | `''` |
| `checkout-rev` | Revision (branch, tag, or SHA) when using `checkout-url` | No | `main` |
| `checkout-scripts` | Newline-separated list of checkout script paths (passed as `--script` arguments to `spaces checkout`) | No | `''` |
| `workspace` | Name of the workspace directory to create | **Yes** | — |
| `run-target` | Target to pass to `spaces run` (e.g. `//:test`). Leave empty to run all targets. | No | `''` |

## Related Actions

- [work-spaces/install-spaces](https://github.com/work-spaces/install-spaces) — Install the `spaces` CLI on its own
