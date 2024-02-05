# Github create release

Github Action to create Github Release.

## Usage

### Example Pipeline

Create a new folder `workflows` and create yaml file example `myWorkflow.yml` in the repository you are trying to use this release action. Copy below yaml code in this file.

```yaml
name: Bump Version and Tag
on:
  push:
    branches:
      - 'master'
      - 'sit'
      - 'alpha'
      - 'sandbox'
jobs:
  build-and-push:
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    name: Bump and Tag
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@master
      - name: Bump and Tag
        id: bump_and_tag
        uses: bricklanetech/action.bump-version-and-tag@master
      - name: Release
        if: github.ref == 'refs/heads/master'
        uses: bricklanetech/action.create-release@master
        with:
          tag: ${{ steps.bump_and_tag.outputs.tag }}
```

## Environment Variables

- `GITHUB_TOKEN`: The token required to authenticate on Github.

## Arguments

- `tag`: New tag name to be released in Github.
