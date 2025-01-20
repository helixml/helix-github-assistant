# Helix GitHub Assistant

A Helix-powered app that enables natural language interaction with GitHub Issues. Talk to your GitHub Issues using natural language!

## Quick Start

`bash`

Clone the repository

git clone https://github.com/helixml/helix-github-assistant.git

cd helix-github-assistant


Set up environment variables
`env`

export GITHUB_OWNER=your_github_username
export GITHUB_API_TOKEN=your_github_token
export HELIX_API_KEY=your_helix_api_key

`bash`

Deploy
./deploy.sh



## Installation

### Prerequisites
- GitHub Account
- Helix Account (sign up at app.tryhelix.ai)
- Terminal/Command Line access

### Access Tokens Setup
**GitHub Token:**
1. Go to GitHub.com → Settings → Developer Settings
2. Select "Personal Access Tokens" → "Tokens (classic)"
3. Generate new token with 'repo' permissions
4. Copy and save the token

**Helix API Key:**
1. Log into app.tryhelix.ai
2. Click on the three dots beside your name
3. Click on Account & API
4. Copy Helix API Key

## Configuration

### Environment Setup

`env`

Set environment variables

export GITHUB_OWNER=your_github_username
export GITHUB_API_TOKEN=your_github_token
export HELIX_API_KEY=your_helix_api_key

Verify they're set

echo $GITHUB_OWNER
echo $GITHUB_API_TOKEN
echo $HELIX_API_KEY


### Assistant Configuration

Copy this into helix.yaml:
`yaml`

piVersion: app.aispec.org/v1alpha1
kind: AIApp
metadata:
name: Github-issues-Assistant
spec:
assistants:
model: llama3.1:8b-instruct-q8_0
type: text
system_prompt: |
You are a GitHub Issues expert. Present issues clearly and include:
Issue title and number

Current status (open/closed)
Assignees and labels
apis:
name: GitHub Issues API
description: List repository issues
schema: |-
openapi: 3.0.0
info:
title: GitHub Issues API
description: List repository issues
version: "1.0.0"
servers:
url: https://api.github.com
paths:
/repos/{owner}/{repo}/issues:
get:
operationId: listIssues
parameters:
name: owner
in: path
required: true
schema:
type: string
name: repo
in: path
required: true
schema:
type: string
name: state
in: query
schema:
type: string
enum: [open, closed, all]
responses:
'200':
description: List of issues
url: https://api.github.com

### Testing Your Setup

`bash`

Test configuration

helix test -f helix.yaml

## Contributing

We welcome contributions! Here's how:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Troubleshooting
If you encounter issues:
1. Check environment variables are set correctly
2. Verify GitHub token has 'repo' access
3. Make sure repository names are correct
4. Check Helix API key is valid

## License

Apache 2.0 - See [LICENSE](LICENSE) for details.

