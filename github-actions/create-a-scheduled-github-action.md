# Create a Scheduled GitHub Action

GitHub Actions can be triggered by repository events such as opening a new pull request, merge a pull request into the master branch. But besides these standard GitHub webhooks, you can also trigger a workflow by scheduled times:

```yaml
name: Scheduled Report
on:
  schedule:
    - cron: 1 * * * * # Run this action every minute

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v2
      - run: npm install
      - run: npm run start
```

You can also create multiple cron jobs. Just place them under the schedule section:

```yaml
name: Scheduled Report
on:
  schedule:
    - cron: 00 05 * * * # Run this on every morning at 5 AM
    - cron: 00 07 * * * # Run this on every morning at 7 AM
    - cron: 30 20 * * * # Run this on every evening at 20:30 PM
  # ...
```

References:

- [Triggering a workflow](https://docs.github.com/en/actions/using-workflows/triggering-a-workflow)
- [About billing for GitHub Actions](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions)
