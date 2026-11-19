# Project 02 — Automatic n8n Workflow Backup to GitHub

<text>**Project Type:** Workflow Automation  
**Platform:** n8n  
**Language:** JavaScript, PowerShell  
**Version:** 1.0  
**Status:** Completed and Tested</text>

## 1. Overview

This project automates the backup of n8n workflows to a GitHub repository.

Instead of manually exporting workflows and uploading JSON files, this automation retrieves workflows through the n8n API, prepares their JSON files, saves them into their respective project folders, and automatically commits and pushes the changes to GitHub.

The entire process can be started with one click using the n8n Manual Trigger.

## 2. Project Objectives

- Automatically retrieve workflows from a local n8n instance.
- Export workflow configurations as JSON files.
- Organize backups into individual project directories.
- Save workflow files to the local filesystem.
- Automatically detect file changes using Git.
- Commit and push updated backups to GitHub.
- Avoid unnecessary commits when no workflow changes are detected.

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow orchestration |
| n8n REST API | Retrieve workflow configurations |
| JavaScript | Process workflow data |
| PowerShell | Execute local Git operations |
| Git | Version control |
| GitHub | Remote backup storage |
| Windows | Local execution environment |

## 4. System Architecture

The automation follows this process:

```text
Manual Trigger
      |
      v
HTTP Request
      |
      v
JavaScript Code
      |
      +----------------------+
      |                      |
      v                      v
Convert to File        Create Folders
      |                      |
      +----------+-----------+
                 |
                 v
               Merge
                 |
                 v
       Write Files to Disk
                 |
                 v
        Execute PowerShell
                 |
                 v
           Git Add
                 |
                 v
         Git Commit
                 |
                 v
          Git Push
                 |
                 v
             GitHub
```

## 5. Workflow Node Explanation

### 5.1 Manual Trigger
Starts the backup process when the user clicks **Execute Workflow**.

### 5.2 HTTP Request
Sends a GET request to the local n8n API:

```http
GET http://localhost:5678/api/v1/workflows
```

Authentication uses an n8n API key through a Header Auth credential.

### 5.3 Code in JavaScript
Processes the API response and prepares the backup information for each workflow:

- Workflow ID
- Workflow name
- Destination folder
- JSON filename
- JSON file content

It also generates consistent folder names from workflow names.

### 5.4 Convert to File
Converts the workflow JSON content into binary file data.

### 5