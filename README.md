# .github-workflows-
name: generate animation

on:
  schedule:
    - cron: "0 */24 * * *" # Runs every 24 hours
  workflow_dispatch:
  push:
    branches:
    - main

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - name: generate-snake-game-from-github-contribution-grid
        uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
      - name: push github-snake.svg to the output branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          ![Snake animation](https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-snake.svg)
