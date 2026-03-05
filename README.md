# spaces-checkout-run

GitHub Action for executing a `spaces checkout` / `spaces run` sequence using the [spaces](https://github.com/work-spaces/spaces) CLI.

## Usage

```yaml
- uses: work-spaces/spaces-checkout-run@v1
  with:
    checkout: <arguments to pass to spaces checkout>
    run: <arguments to pass to spaces run>
```

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `checkout` | Yes | Arguments to pass to `spaces checkout` |
| `run` | Yes | Arguments to pass to `spaces run` |
| `github-token` | No | GitHub token for authorizing access to GitHub repositories. Defaults to an empty string |

## Example

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: work-spaces/spaces-checkout-run@v1
        with:
          checkout: checkout-repo --url=https://github.com/my-org/my-spaces --rev=main
          run: //my-workspace:build
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## How it works

1. Installs the `spaces` CLI using [work-spaces/install-spaces](https://github.com/work-spaces/install-spaces)
2. Runs `spaces checkout` with the provided arguments
3. Runs `spaces run` with the provided arguments
