# NDB-CAREER — GitHub Setup Sequence

**Task Code:** NDB-CAREER-INFRA-001
**Author:** Nicolette Martine Langendam — NikiDigitals
**Run this after:** 9 July 2026

This document contains every command and configuration step required to go from zero to a fully operational NDB-Career repository with GitFlow, branch protection, and Conventional Commits in place.

---

## Prerequisites

- Git installed and configured (`git config --global user.name` and `user.email` set to NikiDigitals)
- GitHub CLI installed (`gh --version` to confirm) — or use GitHub UI for repo creation step
- Repository files already prepared (this infrastructure build)

---

## Step 1 — Create the Repository

### Option A: GitHub CLI

```bash
gh repo create NikiDigitals/NDB-Career \
  --public \
  --description "NDB-CAREER — Business Analyst career readiness programme — NikiDigitals" \
  --clone
```

### Option B: GitHub UI

1. Go to github.com/new
2. Repository name: `NDB-Career`
3. Owner: `NikiDigitals`
4. Visibility: **Public**
5. Description: `NDB-CAREER — Business Analyst career readiness programme — NikiDigitals`
6. Do NOT initialise with README (we're pushing our own)
7. Click **Create repository**

---

## Step 2 — Initialise Local Repository

```bash
# Navigate to your projects folder
cd C:\Projects

# Create the NDB-Career folder (if not already cloned)
mkdir NDB-Career
cd NDB-Career

# Initialise git
git init

# Add remote origin
git remote add origin https://github.com/NikiDigitals/NDB-Career.git
```

---

## Step 3 — Create Folder Structure

```bash
# Windows (PowerShell)
New-Item -ItemType Directory -Force -Path `
  _context, `
  docs\roadmap, `
  docs\decisions, `
  docs\reviews, `
  portfolio\financial-analysis, `
  portfolio\case-studies, `
  portfolio\bpmn, `
  portfolio\governance, `
  certifications, `
  research

# Add .gitkeep to empty folders so Git tracks them
$folders = @(
  "docs/reviews",
  "portfolio/financial-analysis",
  "portfolio/case-studies",
  "portfolio/bpmn",
  "portfolio/governance",
  "certifications",
  "research"
)
foreach ($folder in $folders) {
  New-Item -ItemType File -Force -Path "$folder/.gitkeep"
}
```

```bash
# Mac/Linux equivalent
mkdir -p _context docs/roadmap docs/decisions docs/reviews \
  portfolio/financial-analysis portfolio/case-studies \
  portfolio/bpmn portfolio/governance \
  certifications research

touch docs/reviews/.gitkeep \
  portfolio/financial-analysis/.gitkeep \
  portfolio/case-studies/.gitkeep \
  portfolio/bpmn/.gitkeep \
  portfolio/governance/.gitkeep \
  certifications/.gitkeep \
  research/.gitkeep
```

---

## Step 4 — Copy Prepared Files

Copy all files from this infrastructure build into the correct locations:

```
README.md                          → /README.md
NDB-CAREER-CONTEXT.md              → /_context/NDB-CAREER-CONTEXT.md
docs/roadmap/BA-Roadmap-v1.0.md    → /docs/roadmap/BA-Roadmap-v1.0.md
docs/decisions/DECISIONS.md        → /docs/decisions/DECISIONS.md
```

---

## Step 5 — First Commit to Main

```bash
git add .
git commit -m "chore: initialise NDB-Career repository"
git branch -M main
git push -u origin main
```

---

## Step 6 — Create and Push Develop Branch (GitFlow)

```bash
git checkout -b develop
git push -u origin develop
```

---

## Step 7 — Branch Protection on Main

### Via GitHub CLI

```bash
gh api repos/NikiDigitals/NDB-Career/branches/main/protection \
  --method PUT \
  --field required_status_checks=null \
  --field enforce_admins=true \
  --field required_pull_request_reviews='{"required_approving_review_count":0,"dismiss_stale_reviews":true}' \
  --field restrictions=null
```

### Via GitHub UI (recommended — more control)

1. Go to: github.com/NikiDigitals/NDB-Career/settings/branches
2. Click **Add branch protection rule**
3. Branch name pattern: `main`
4. Enable:
   - ✅ **Require a pull request before merging**
   - ✅ **Dismiss stale pull request approvals when new commits are pushed**
   - ✅ **Do not allow bypassing the above settings**
5. Click **Create**

---

## Step 8 — Confirm GitFlow is Active

```bash
# Verify both branches exist
git branch -a

# Expected output:
# * develop
#   main
#   remotes/origin/develop
#   remotes/origin/main
```

---

## Step 9 — Set Default Branch to Develop

All active work happens on feature branches merging to `develop`. `main` is stable only.

### Via GitHub UI:
1. Settings → General → Default branch
2. Change to `develop`
3. Confirm

---

## Step 10 — Conventional Commits — Verify Format

Test that your first feature branch follows the format:

```bash
# Create a feature branch for the first real task
git checkout -b feature/NDB-CAREER-INFRA-001

# Example commit messages:
git commit -m "docs(_context): add NDB-CAREER-CONTEXT.md"
git commit -m "docs(roadmap): add BA-Roadmap-v1.0"
git commit -m "docs(decisions): initialise decisions log"
```

---

## Step 11 — Merge Feature Branch to Develop

```bash
git checkout develop
git merge --no-ff feature/NDB-CAREER-INFRA-001 \
  -m "feat: complete NDB-CAREER-INFRA-001 infrastructure setup"
git push origin develop
```

---

## Step 12 — Acceptance Criteria Check

Run through the full acceptance criteria before closing NDB-CAREER-INFRA-001:

- [ ] Repo live at github.com/NikiDigitals/NDB-Career
- [ ] README visible on repo landing page
- [ ] NDB-CAREER-CONTEXT.md visible in `_context/`
- [ ] BA-Roadmap-v1.0.md visible in `docs/roadmap/`
- [ ] DECISIONS.md visible in `docs/decisions/`
- [ ] All portfolio and docs subfolders present
- [ ] GitFlow active — `main` and `develop` both pushed
- [ ] Branch protection on `main` confirmed
- [ ] First commit message: `chore: initialise NDB-Career repository`
- [ ] Obsidian vault opens and all folders in place
- [ ] Zotero NDB-CAREER collection visible with all sub-collections
- [ ] Zotero → Obsidian pipeline tested — one test literature note created
- [ ] Zero documentation debt at session close

---

## Obsidian Vault Setup

### Create the vault

1. Open Obsidian
2. **Open another vault** → **Create new vault**
3. Vault name: `NDB-Career`
4. Location: `C:\Projects\NDB-Career\vault\`

### Create folder structure

Create these folders inside Obsidian (right-click in file explorer):

```
00 Inbox
01 Role Research
02 Industry Knowledge
02 Industry Knowledge/Data Governance
02 Industry Knowledge/Financial Services
02 Industry Knowledge/BA Practice
03 Certifications
03 Certifications/PSM-I
03 Certifications/BCS BA Foundation
03 Certifications/PL-300
03 Certifications/CDMP
04 Portfolio Projects
05 Application Tracking
06 Interview Prep
Templates
```

### Copy vault files

Copy from this infrastructure build:
- `vault/README.md` → vault root
- `vault/Templates/Literature Note.md` → `Templates/`
- `vault/Templates/Role Research.md` → `Templates/`
- `vault/Templates/Application.md` → `Templates/`

### Configure Core Plugins

Settings → Core plugins:
- ✅ Templates — enable. Set templates folder: `Templates`
- ✅ Backlinks — enable
- ✅ Tags — enable
- ❌ Daily Notes — disable

### Install Community Plugins

Settings → Community plugins → Browse:

1. **Zotero Integration** — search "Zotero Integration" by mgmeyers
   - After install: configure import format pointing to NDB-CAREER Zotero collection
2. **Templater** — search "Templater" by SilentVoid
   - Configure template folder: `Templates`
3. **Dataview** — search "Dataview" by blacksmithgu
   - Enable JavaScript queries: yes

---

## Zotero Setup

### Create NDB-CAREER collection

1. Open Zotero
2. Right-click in left panel → **New Collection**
3. Name: `NDB-CAREER`

### Create sub-collections

Right-click `NDB-CAREER` → **New Subcollection** for each:
- `Data Governance`
- `Financial Services`
- `BA Practice`
- `Certifications`
- `Industry Reports`

### Connect to Obsidian

1. Install **Better BibTeX** Zotero plugin (if not already installed)
2. In Obsidian Zotero Integration settings:
   - Database: Zotero
   - Template for literature notes: point to `Templates/Literature Note.md`
3. **Test:** Import one entry from NDB-CAREER collection as a literature note into `00 Inbox/`

---

*Document Code: NDB-CAREER*
*Task: NDB-CAREER-INFRA-001*
*Author: Nicolette Martine Langendam — NikiDigitals*
