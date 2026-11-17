# Project 02 – Automatic n8n Workflow Backup to GitHub

## 1. Project Overview

This project automates the process of backing up n8n workflows to a GitHub repository.

Instead of manually exporting workflows and uploading JSON files, this automation retrieves workflows through the n8n REST API, saves them locally, and uses Git to commit and push changes to GitHub.

The workflow is manually triggered, giving the user control over when backups happen.

## 2. Project Objectives

- Automatically retrieve workflows from a local n8n instance.
- Export workflows as JSON files.
- Save exported files to a local directory.
- Detect changes using Git.
- Automatically commit modified or newly created workflow files.
- Push backups to a GitHub repository.
- Avoid unnecessary commits when no changes are detected.

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation |
| n8n REST API | Retrieve workflow data |
| JavaScript | Process workflow JSON |
| Google Gemini | Used by Project 01, not required by this backup workflow |
| PowerShell | Execute Git backup commands |
| Git | Version control |
| GitHub | Remote backup storage |

## 4. Workflow Architecture

**Execution sequence:**

1. Manual Trigger
2. HTTP Request
3. Code (JavaScript)
4. Convert to File
5. Read/Write Files from Disk
6. Execute Command

### Node Responsibilities

**1. Manual Trigger**

Starts the backup process when the user clicks Execute Workflow.

**2. HTTP Request**

Sends a GET request to:

`http://localhost:5678/api/v1/workflows`

Authentication uses an n8n API key through Header Auth.

Header name: `X-N8N-API-KEY`

**3. Code (JavaScript)**

Processes the API response and prepares individual workflow items.

For each workflow, it generates:
- Workflow ID
- Workflow name
- A sanitized filename
- JSON content

**4. Convert to File**

Converts the JSON content into a binary file.

Configuration:
- Operation: Convert to Text File
- Text Input Field: `fileContent`
- Output Binary Field: `data`

**5. Read/Write Files from Disk**

Writes the generated JSON files to:

`D:\AI-Automation\n8n-Workflows`

The destination path is dynamically retrieved from the Code node.

**6. Execute Command**

Runs the PowerShell backup script:

`powershell -NoProfile -ExecutionPolicy Bypass -File "D:\AI-Automation\backup-git.ps1"`

## 5. Repository Structure

Current local project structure:

```text
D:\AI-Automation\
│
├── Learning-Notes\
│
├── n8n-Workflows\
│   ├── proj-01-my-first-ai-agent\
│   ├── 01-my-first-ai-personal-assistant.json
│   └── project-02-automatic-github-backup.json
│
├── backup-git.ps1
└── Start-n8n.bat
```

GitHub repository:

https://github.com/WoodRuff646562/ai-engineering-journey

## 6. GitHub Backup Automation

The PowerShell script performs the following operations:

1. Locates JSON files in the root of the `n8n-Workflows` directory.
2. Stages each JSON file individually.
3. Checks whether the staged files have changed.
4. Creates a Git commit if changes are detected.
5. Pushes the commit to the remote `main` branch.
6. Reports success or failure.

Commit message:

`Backup all n8n workflows`

If no changes are detected, the script skips the commit and proceeds to push.

## 7. Execution Instructions

1. Start the local n8n instance using `Start-n8n.bat`.
2. Open `http://localhost:5678`.
3. Open Project 02 – Automatic GitHub Backup.
4. Save any changes to the workflows you want backed up.
5. Click Execute Workflow.
6. Wait for all nodes to complete.
7. Check the GitHub repository for updated workflow JSON files.

## 8. Environment Configuration

**Operating System:** Windows

**Local n8n URL:** `http://localhost:5678`

**Backup directory:** `D:\AI-Automation\n8n-Workflows`

**Git repository:** `D:\AI-Automation`

**Remote branch:** `main`

The n8n launcher restricts filesystem access to the workflow backup directory using `N8N_RESTRICT_FILE_ACCESS_TO`.

The Execute Command node is enabled through the local n8n configuration.

API credentials are stored in n8n credentials rather than hardcoded in the workflow.

## 9. Current Limitations

- Backup execution requires manual triggering.
- The current API implementation has not yet been extended to handle pagination.
- JSON files are currently saved directly inside the `n8n-Workflows` directory.
- The PowerShell script currently handles root-level JSON files, not JSON files inside nested workflow folders.
- README documentation is currently maintained separately; automatic AI-generated documentation is planned as a future enhancement.

## 10. Future Improvements

- Automatically create a separate folder for each workflow.
- Integrate Google Gemini to analyze workflow JSON.
- Generate a README.md for each workflow using AI.
- Support nested folders and larger workflow collections.
- Improve error handling and backup reporting.
- Add scheduled automatic backups.
- Add backup history and recovery procedures.

## 11. Project Status

**Current status:** Working – initial universal backup implementation tested successfully.

The system has successfully:
- Retrieved multiple workflows from n8n.
- Generated individual JSON files.
- Saved them locally.
- Detected workflow modifications.
- Created Git commits.
- Pushed updated backups to GitHub.

The next development stage will introduce structured folders and AI-powered workflow documentation.

---

*Part of the AI Engineering Journey – Project 02.*