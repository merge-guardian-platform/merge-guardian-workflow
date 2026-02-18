# Merge Guardian Workflow

This repository provides a GitHub Action to integrate **Merge Guardian AI** into your CI/CD pipeline. It uses AI-powered analysis to predict potential merge conflicts and calculate risk scores for your Pull Requests.

## Usage

Add the following step to your GitHub Actions workflow:

```yaml
- name: Merge Guardian Analysis
  uses: merge-guardian-platform/merge-guardian-workflow@main
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    ai-api-key: ${{ secrets.AI_API_KEY }}
    ai-provider: 'openai' # or 'gemini', 'anthropic'
```

## Inputs

| Name | Description | Required | Default |
| :--- | :--- | :--- | :--- |
| `owner` | GitHub repository owner | Yes | `${{ github.repository_owner }}` |
| `repo` | GitHub repository name | Yes | `${{ github.event.repository.name }}` |
| `pr-number` | Pull Request number | Yes | `${{ github.event.pull_request.number }}` |
| `github-token` | GitHub Personal Access Token | Yes | N/A |
| `ai-provider` | AI Service Provider (openai, gemini, anthropic) | Yes | `openai` |
| `ai-api-key` | API Key for the chosen AI Service Provider | Yes | N/A |

## Example Workflow

```yaml
name: AI Conflict Analysis
on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.25'

      - name: Run Merge Guardian
        uses: merge-guardian-platform/merge-guardian-workflow@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          ai-api-key: ${{ secrets.OPENAI_API_KEY }}
          ai-provider: 'openai'
```
