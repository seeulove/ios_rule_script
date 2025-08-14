# AI Rule Set

This directory contains rules for blocking and proxying traffic to various AI services.

## Sources

The domains in this list were compiled from the following official sources:

*   **OpenAI:** [Network recommendations for ChatGPT](https://help.openai.com/en/articles/9247338-network-recommendations-for-chatgpt-errors-on-web-and-apps)
*   **Google Gemini:** [Gemini app firewall settings](https://support.google.com/a/answer/15627649?hl=en)
*   **Microsoft Copilot:** [Microsoft 365 Copilot requirements](https://learn.microsoft.com/en-us/copilot/microsoft-365/microsoft-365-copilot-requirements)
*   **Anthropic Claude:** [Anthropic API Documentation](https://docs.anthropic.com/en/api/getting-started)

## Daily Updates

To keep this rule set up to date, you can use a GitHub Actions workflow. Create a file named `.github/workflows/update-ai-rules.yml` with the following content:

```yaml
name: Update AI Rules

on:
  schedule:
    - cron: '0 0 * * *' # Runs every day at midnight
  workflow_dispatch:

jobs:
  update-rules:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Update AI rules
        run: |
          # This is a placeholder for the actual script to update the rules.
          # A more complex script would be needed to fetch, parse, and update the rules from the sources.
          # For example, you could use curl and grep to extract domains from the official pages.
          echo "Updating AI rules..."
          # Example for OpenAI:
          # curl -s https://help.openai.com/en/articles/9247338-network-recommendations-for-chatgpt-errors-on-web-and-apps | grep -oE '[a-zA-Z0-9.-]+\.openai\.com' >> new_rules.txt
          # The full script would need to handle all sources and formats.
          echo "Update script not yet implemented."

      - name: Commit and push if changed
        run: |
          git config --global user.name 'github-actions[bot]'
          git config --global user.email 'github-actions[bot]@users.noreply.github.com'
          git add rule/Clash/AI/AI.list rule/Clash/AI/AI.yaml rule/Loon/AI/AI.list rule/QuantumultX/AI/AI.list rule/Shadowrocket/AI/AI.list rule/Surge/AI/AI.list
          git commit -m "Update AI rules" || echo "No changes to commit"
          git push || echo "No changes to push"
```

This workflow will run daily, and you can also trigger it manually. You will need to write a script that fetches the domains from the sources and updates the rule files accordingly. The placeholder in the `run` step should be replaced with your own script.
