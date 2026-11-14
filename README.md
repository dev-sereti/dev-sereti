name: GitHub Metrics

on:
  schedule:
    - cron: "0 0 * * *"      # daily at midnight UTC
  workflow_dispatch:          # manual run button
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: dev-sereti
          filename: github-metrics.svg
          committer_branch: main

          # Layout / look (dark, classic template like your screenshot)
          template: classic
          base: header, activity, community, repositories, metadata
          base_indepth: yes
          config_timezone: Africa/Nairobi
          config_display: large
          config_padding: 0, 8 + 11%

          # Contributions calendar (3D isometric)
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year

          # Coding habits: commit time of day, per day, language activity
          plugin_habits: yes
          plugin_habits_from: 250
          plugin_habits_days: 14
          plugin_habits_facts: yes
          plugin_habits_charts: yes
          plugin_habits_charts_type: classic
          plugin_habits_languages_limit: 8

          # Most used languages
          plugin_languages: yes
          plugin_languages_indepth: yes
          plugin_languages_sections: most-used
          plugin_languages_details: bytes-size, percentage

          # Lines added / removed
          plugin_lines: yes
          plugin_lines_history_limit: 1

          # Mastered technologies and topics (icon grid)
          plugin_topics: yes
          plugin_topics_mode: icons
          plugin_topics_sort: mastered
          plugin_topics_limit: 0

          # PageSpeed Insights for your portfolio
          plugin_pagespeed: yes
          plugin_pagespeed_url: https://dev-sereti.netlify.app
          plugin_pagespeed_detailed: yes

          # Followers / contribution streak style info
          plugin_followup: yes
          plugin_stargazers: yes
          plugin_stargazers_charts: yes

          # Optional: Suggested tracks (needs a public Apple Music playlist)
          # plugin_music: yes
          # plugin_music_provider: apple
          # plugin_music_playlist: https://music.apple.com/ke/playlist/YOUR_PLAYLIST
          # plugin_music_limit: 2

          # Optional: Roadmap project card (needs a GitHub Project)
          # plugin_projects: yes
          # plugin_projects_repositories: dev-sereti/dev-sereti/1
