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

## Example

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: work-spaces/spaces-checkout-run@v1
        with:
          checkout: https://github.com/my-org/my-spaces --name=my-workspace
          run: //my-workspace:build
```

## How it works

1. Installs the `spaces` CLI using [work-spaces/install-spaces](https://github.com/work-spaces/install-spaces)
2. Runs `spaces checkout` with the provided arguments
3. Runs `spaces run` with the provided arguments
