# Repogent - Multi-Agent GitHub Repository Assistant

🤖 **An intelligent multi-agent system for GitHub** that combines PR review, issue management, CI/CD monitoring, and community assistance - all orchestrated and running as GitHub Actions.

## 🏗️ Architecture

```
┌─────────────────────────────────────────┐
│      ORCHESTRATOR (Central Brain)       │
│  • Coordinates all agents               │
│  • Manages inter-agent communication    │
│  • Tracks context & decisions           │
└──────────────┬──────────────────────────┘
               │
    ┌──────────┼──────────┬──────────┐
    │          │          │          │
┌───▼────┐ ┌──▼──────┐ ┌─▼───────┐ ┌▼────────┐
│Community│ │ Issue   │ │   PR    │ │  CI/CD  │
│Assistant│ │ Manager │ │Reviewer │ │ Agent   │
└─────────┘ └─────────┘ └─────────┘ └─────────┘
```

## ✨ Features

### 🎭 Orchestrator (NEW!)
- **Central coordinator** for all sub-agents
- **Agent-to-agent communication** via message queue
- **Context management** across workflows
- **Decision logging** and pattern recognition
- **Event routing** to appropriate agents

### 🔍 PR Reviewer
- **Inline code comments** on specific lines
- **Severity levels**: 🔴 Critical, 🟡 Warning, 🟢 Suggestion  
- **Smart fix suggestions** for every issue
- **Build failure analysis** (receives from CI/CD Agent)
- **Lightning-fast** reviews powered by Groq

### 🎯 Issue Manager
- **Auto-triage & labeling** of new issues
- **AI-powered classification** (Bug, Enhancement, Question)
- **Intelligent responses** to issue comments
- **Context-aware** explanations

### 💬 Community Assistant
- **Ask questions about the codebase** using `@repogent`
- **Get code references** with highlighted permalinks
- **Navigate the repository** with AI guidance
- **Understand how features work** with code examples

### 🚨 CI/CD Agent (NEW!)
- **Monitors build failures** automatically
- **Analyzes error logs** with pattern recognition
- **Identifies root causes** (test failures, dependencies, etc.)
- **Notifies PR authors** with actionable fixes
- **Communicates with PR Reviewer** for context-aware analysis

## 🚀 Quick Start

**1. Create a workflow in your repository**

**Create a file:**

.github/workflows/repogent.yml

**2. Add this workflow code**
name: Repogent AI Automation

on:
  pull_request:
  issues:
  issue_comment:

permissions:
  contents: read
  issues: write
  pull-requests: write
  actions: read

jobs:
  repogent:
    runs-on: ubuntu-latest
    steps:
      - name: Run Repogent
        uses: harry1634/Repogent@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          groq-key: ${{ secrets.GROQ_API_KEY }}

**3. Add your Groq API key**

**Go to:**

**Settings → Secrets and variables → Actions**


**Add a new secret:**

Name: GROQ_API_KEY
Value: your_groq_api_key


**Get a key from:**

https://console.groq.com

**4. Enable workflow permissions**

**Go to:**

**Settings → Actions → General**


**Under Workflow permissions, select:**

**Read and write permissions**


Save the changes.

**5. Start using Repogent**

Now the automation works automatically.

**Open a Pull Request →** AI review comments appear

**Create an Issue →** Auto-classified and labeled

**Comment on issues →** AI responds
```markdown
## 🔴 CI/CD Build Failed

**Workflow:** Tests
**Failed Job:** Unit Tests
**Failure Type:** `test_failure`

### 🔍 Error Details:
```
FAIL src/auth.test.js
  ● Authentication › should validate token
    Expected status 200, got 401
```

### 💡 Suggested Fixes:
1. Review the failing test cases and fix the implementation
2. Check if recent code changes broke the test assertions
3. Run tests locally to reproduce: `npm test`

### 📊 Build Information:
- **Commit:** `abc1234`
- **Author:** @username
- **Job URL:** [View Logs](...)
```

### 🤖 Community Assistant Examples

Ask questions about the codebase by mentioning `@repogent`:

```
@repogent How does the diff parsing work?
@repogent Where is the severity emoji logic implemented?
@repogent Show me how to add a new label
@repogent What files handle GitHub API calls?
```

The bot will:
1. 🔍 Search the codebase for relevant code
2. 📍 Provide GitHub permalinks to specific lines
3. 💡 Explain how things work with context
4. 📝 Show code snippets with syntax highlighting

## � Agent Communication Flow

### Example: Build Failure → PR Notification

```
1. PR Merged
   ↓
2. CI/CD Agent monitors build
   ↓
3. Build Fails ❌
   ↓
4. CI/CD Agent analyzes logs
   - Detects: "Test failure in auth.test.js"
   - Root cause: Breaking change in PR #42
   ↓
5. CI/CD Agent → Orchestrator:
   {type: "build_failure", pr: 42, ...}
   ↓
6. Orchestrator → PR Reviewer:
   "Analyze PR #42 with build context"
   ↓
7. PR Reviewer generates targeted analysis
   ↓
8. Posts to PR: "@author, your changes broke auth tests..."
```

## �📂 Repository Structure

```
.github/workflows/
  ├── orchestrator.yml           # Central coordinator
  ├── cicd-monitor.yml           # CI/CD failure monitoring
  ├── pr-review.yml              # PR review automation
  ├── issue-triage.yml           # Issue management
  └── community-assistant.yml    # Community Q&A helper
scripts/
  ├── orchestrator.py            # Central agent coordinator
  ├── cicd_agent.py              # Build monitoring & analysis
  ├── pr_reviewer_enhanced.py    # Enhanced PR reviewer with CI/CD context
  ├── agent_comms.py             # Agent communication helpers
  ├── review_pr.py               # PR analysis
  ├── post_review_comments.py    # Post inline PR comments
  ├── triage_issue.py            # Issue classification
  ├── respond_to_comment.py      # Issue comment responses
  └── community_assistant.py     # Codebase Q&A with references
config/
  └── labels.json                # Label configuration
.repogent/
  ├── context/                   # Stored context data
  ├── queue/                     # Message queue
  └── logs/                      # Agent decision logs
```

## ⚙️ Configuration

Edit `config/labels.json`:
```json
{
  "labels": ["Bug", "Enhancement", "Question", "Documentation"],
  "default_label": "Question"
}
```

## 🔧 Models

- **PR Review**: llama-3.3-70b-versatile
- **Issue Triage**: llama-3.3-70b-versatile
- **Community Assistant**: llama-3.3-70b-versatile  

## 📄 License

Apache 2.0 License

## 👤 Author

P.Saiteja


GitHub user name : harry1634

---
**⚡ Powered by Groq**


