# action-release

Example workflow step:

```
- name: Publish release
  uses: saucal/action-release@v1
  with:
    github_token: ${{ secrets.the_token }}
```

`github_token` is the only required input param.
And a more complete example workflow that is triggered when a tag is pushed,  builds, creates a zip, creates a release based on the tag, and attaches the created zip to that release:

```
name: "tagged-release"
on:
  push:
    tags:
      - "*"

jobs:
  tagged-release:
    name: "Build & Create a Tagged Release"
    runs-on: "ubuntu-latest"
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Install Dependencies
        run: npm ci

      - name: Build
        run: npm run build --if-present

      - name: Test
        run: npm run test --if-present

      - name: Publish release
        uses: saucal/action-release@v1

```
