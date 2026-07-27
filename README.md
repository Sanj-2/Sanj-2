name: Generate Dragon Snake

on:
  schedule:
    - cron: "0 0 * * *" # runs once a day
  workflow_dispatch: {} # lets you trigger it manually from the Actions tab
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    steps:
      - name: Generate snake animation
        uses: Platane/snk@v3
        with:
          github_user_name: Sanj-2
          outputs: |
            dist/dragon-snake.svg
            dist/dragon-snake-dark.svg?palette=github-dark

      - name: Push snake to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
