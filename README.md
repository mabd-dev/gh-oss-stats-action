# gh-oss-stats-action

> Automatically generate beautiful SVG badges for your GitHub open source contributions

Showcase your open source contributions with stunning, auto-updating badges on your GitHub profile. This action wraps the [gh-oss-stats](https://github.com/mabd-dev/gh-oss-stats) CLI tool to generate SVG badges that display your contributions to external repositories.


## ✨ Features

- **36 badge combinations**: 6 themes × 2 variants × 3 styles
- **Auto-commit**: Automatically updates your profile badge on schedule
- **Highly customizable**: Filter by stars, limit repos, exclude organizations
- **Zero configuration**: Works out-of-the-box with sensible defaults
- **Fast**: Efficient GitHub API usage with smart rate limit handling


## 🚀 Quick Start

**Step 1:** Create `.github/workflows/oss-badge.yml` in your profile repository:

```yaml
name: Generate OSS Badge

on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday at midnight
  workflow_dispatch:      # Manual trigger

jobs:
  update-badge:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Generate OSS Badge
        uses: mabd-dev/gh-oss-stats-action@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          badge-style: summary
          badge-theme: dark
```

**Step 2:** Add the badge to your `README.md`:

**That's it!** Your badge will auto-update weekly.

***

## 💡 Usage Examples

### Basic Usage (Minimal Configuration)

```yaml
- uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

### Custom Theme & Style

```yaml
- uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    badge-style: detailed
    badge-theme: nord
    badge-variant: text-based
    badge-limit: 10
```

### Filter High-Impact Contributions

```yaml
- uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    min-stars: 500          # Only repos with 500+ stars
    badge-sort: stars       # Sort by most popular
    badge-limit: 5          # Top 5 repos
```

### Exclude Work Organizations

```yaml
- uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    exclude-orgs: "my-company,client-org,acme-corp"
    badge-style: summary
```

### Multiple Badges (Different Themes)

```yaml
- name: Generate Dark Badge
  uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    badge-theme: dark
    output-path: oss-badge-dark.svg

- name: Generate Light Badge
  uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    badge-theme: light
    output-path: oss-badge-light.svg
```



### Manual Commit Control

```yaml
- uses: actions/checkout@v4

- name: Generate Badge
  uses: mabd-dev/gh-oss-stats-action@v1
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    auto-commit: false      # Don't auto-commit

- name: Custom Commit Logic
  run: |
    git config user.name "github-actions[bot]"
    git config user.email "github-actions[bot]@users.noreply.github.com"
    git add oss-badge.svg
    git commit -m "feat: update OSS badge [skip ci]"
    git push
```


---

## 🛠️ Troubleshooting

### Badge Not Updating

**Problem:** Workflow runs but badge doesn't change.

**Solution:**
1. Check if workflow has `contents: write` permission:
   ```yaml
   jobs:
     update-badge:
       runs-on: ubuntu-latest
       permissions:
         contents: write
   ```
2. Verify `commit-badge: true` (default)
3. Check GitHub Actions logs for errors

### Rate Limit Errors

**Problem:** `Error: API rate limit exceeded`

**Solution:**
1. Use a Personal Access Token instead of `GITHUB_TOKEN`:
   ```yaml
   github-token: ${{ secrets.PAT }}
   ```
2. Reduce `max-prs` or increase schedule interval
3. Enable `verbose: true` to see rate limit status

### Empty Badge / No Contributions

**Problem:** Badge shows "0 projects"

**Solution:**
1. Check if you have merged PRs to external repos
2. Verify `exclude-orgs` isn't too broad
3. Lower `min-stars` threshold
4. Ensure username is correct (defaults to `${{ github.actor }}`)

---

## ❓ FAQ

### Q: How often should I update my badge?

**A:** Weekly is recommended for most users. Daily updates may hit rate limits; monthly is fine for infrequent contributors.

```yaml
on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly (Sunday midnight)
    # - cron: '0 0 * * *'  # Daily
    # - cron: '0 0 1 * *'  # Monthly
```

### Q: Does this work with private repos?

**A:** The action itself runs fine in private repos, but it only tracks contributions to **public** repositories (GitHub API limitation).

### Q: Can I customize badge colors/fonts?

**A:** Currently, customization is limited to the 6 themes and 2 variants. Full custom styling requires forking and modifying the badge generation templates. Open an issue if you need specific customization.

### Q: What counts as an "external" contribution?

**A:** Any merged PR to a repository you don't own. Repos owned by excluded orgs (via `exclude-orgs`) are also filtered out.

### Q: How do I debug badge generation?

**A:** Set `verbose: true` to enable detailed logging:


```yaml
- uses: mabd-dev/gh-oss-stats-action@v1
  with:
    verbose: true
```

Check the Actions logs for detailed API calls and processing steps.

---

## 🔗 Related Links

- **Main Repository**: [github.com/mabd-dev/gh-oss-stats](https://github.com/mabd-dev/gh-oss-stats)
- **CLI Documentation**: [gh-oss-stats README](https://github.com/mabd-dev/gh-oss-stats#readme)
- **Issue Tracker**: [Report a bug](https://github.com/mabd-dev/gh-oss-stats-action/issues)
- **Changelog**: [Release notes](https://github.com/mabd-dev/gh-oss-stats-action/releases)

***

## 🤝 Contributing

Contributions are welcome! Here's how you can help:
