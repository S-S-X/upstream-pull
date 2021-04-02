# upstream-pull
Keep stuff sync with upstream repo updates

```yaml
name: "Merge Upstream"

on:
  schedule:
    - cron: "30 20 * * *"
  workflow_dispatch:

jobs:
  pull:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - id: upstream-pull
      uses: S-S-X/upstream-pull@master
      with:
        repository: < UPSTREAM REPOSITORY URI >
    - uses: repo-sync/pull-request@v2
      with:
        source_branch: upstream
        destination_branch: master
        pr_title: "Merge upstream changes"
        pr_body: "${{ steps.upstream-pull.outputs.upstream-log }}"
        pr_label: "upstream"
        github_token: ${{ secrets.GITHUB_TOKEN }}
```
