# Reusable github workflows

- [Go CI](.github/workflows/go-ci.yaml)

_This workflow is indended for Go libraries, ie. projects that don't produce binaries_

in caller repo

```yaml
name: CI
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
    types:
      - opened
      - synchronize
      - reopened
  workflow_dispatch:

permissions:
  contents: read

jobs:
  ci:
    uses: rkosegi/github-workflows/.github/workflows/go-ci.yaml@6b051e22fcf9056ff77e553d6307a6d9b361b438 # v0.0.7
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

Used by [tuya-proto](https://github.com/rkosegi/tuya-proto/actions/workflows/ci.yaml)

- [Dependency review](.github/workflows/dependency-review.yaml)

_This workflow scans project dependencies on PR event_

in caller repo

```yaml
name: Dependency Review
on:
  pull_request:

permissions:
  contents: read

jobs:
  dependency-review:
    uses: rkosegi/github-workflows/.github/workflows/dependency-review.yaml@6b051e22fcf9056ff77e553d6307a6d9b361b438 # v0.0.7
```

Used by [yaml-pipeline](https://github.com/rkosegi/yaml-pipeline/actions/workflows/dependency-review.yaml)

- [GH pages](.github/workflows/gh-pages.yaml)

_Use this workflow to publish content, such as documentation to the GitHub pages_.

in caller repo

```yaml
name: Deploy docs to gh pages
on:
  push:
    branches:
      - main

  workflow_dispatch:

permissions:
  contents: read

jobs:
  pages:
    permissions:
      contents: read
      pages: write
      pull-requests: write
      issues: write
      id-token: write
    uses: rkosegi/github-workflows/.github/workflows/gh-pages.yaml@6b051e22fcf9056ff77e553d6307a6d9b361b438 # v0.0.7
```

- [labeler](.github/workflows/labeler.yaml)

_This workflow adds labels to the PR, based on configuration in caller repository._

in caller repo

```yaml
name: Pull Request Labeler
on:
  pull_request_target:
    types:
      - opened
      - synchronize

permissions:
  contents: read

jobs:
  label-pr:
    permissions:
      pull-requests: write
      issues: write
    uses: rkosegi/github-workflows/.github/workflows/labeler.yaml@6b051e22fcf9056ff77e553d6307a6d9b361b438 # v0.0.7
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

Used by [yaml-pipeline](https://github.com/rkosegi/yaml-pipeline/actions/workflows/labeler.yaml)

- [release on tag](.github/workflows/release-on-tag.yaml)

_This workflow creates release, whenever tag with pattern `v*` is pushed to git._

in caller repo

```yaml
name: Create release on tag push
on:
  push:
    tags:
      - v*

permissions:
  contents: read

jobs:
  release:
    permissions:
      contents: write
    uses: rkosegi/github-workflows/.github/workflows/release-on-tag.yaml@6b051e22fcf9056ff77e553d6307a6d9b361b438 # v0.0.7
```

Used by [slog-config](https://github.com/rkosegi/slog-config/actions/workflows/release-on-tag.yaml)
