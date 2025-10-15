# 🚀 Release Automation in Azure DevOps (ADO)

## 📌 Purpose

This repository outlines the procedure for automating the generation and publication of release notes in **Azure DevOps (ADO)**. The goal is to streamline the release documentation process by integrating CI/CD pipelines with an ADO Wiki.

---

## 📍 Scope

This guide applies to all **DevOps engineers** and **team members** responsible for managing **build and release pipelines** in Azure DevOps projects, particularly those requiring automated release note generation and publication.

---

## ⚙️ Prerequisites

Before setting up the release automation pipeline, ensure the following prerequisites are in place:

### 1. Azure DevOps Wiki Repository
- Your ADO Wiki must be backed by a Git repository.
- Example:  
```

[https://dev.azure.com/{organization}/{project}/_git/wiki](https://dev.azure.com/{organization}/{project}/_git/wiki)

````

### 2. Personal Access Token (PAT)
Create a **PAT** with the necessary permissions:
- ✅ **Code** → Read & Write  
- ✅ **Wiki** → Read & Write (optional, for REST API access)

> 💡 **Note**:  
> Store the PAT securely as a **secret variable** in your pipeline or configure a **service connection**.

---

## 🛠️ Pipeline Overview

The automation pipeline consists of the following stages:

1. **GenerateReleaseNotes**  
 Generates release notes in Markdown using a predefined template (`ReleaseTemplate.md`).

2. **PublishPipelineArtifact** *(Optional)*  
 Publishes the generated release notes as a pipeline artifact for archival.

3. **WikiUpdaterTask**  
 Pushes the generated release notes to the ADO Wiki repository.

> 🔐 Ensure the build agent has **push access** to the Wiki repo using the PAT for authentication.

---

## 🔗 Linking Work Items in ADO Pipelines

You can link ADO work items to commits or PRs using the following methods:

### 1. In Commit Messages
```bash
git commit -m "Fix login bug [AB#123]"
````

### 2. In Pull Request Title or Description

* **PR Title Example**:
  `Resolve signup issue [AB#456]`

* **PR Description Example**:
  `This PR addresses issue #456. Related work item: [AB#456]`

---

## 🔒 Security Considerations

* Store all **PATs and secrets** securely using Azure DevOps secret variables.
* Restrict access to pipeline triggers and modifications to **authorized users** only.
* **Never expose PATs** in logs, scripts, or console output.

---

## 📚 References

* [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)
* [WikiUpdaterTask GitHub Repo](https://github.com/jessehouwing/azure-pipelines-wiki-updater-task)

---

## 🕒 Revision History

| Version | Date       | Author         | Description          |
| ------- | ---------- | -------------- | -------------------- |
| 1.0     | 2025-10-15 | Nitanshu Singh | Initial SOP creation |

---

## 📁 Project Structure (Optional)

You can include this if your repo has scripts or templates:

```
/
├── .azure-pipelines/
│   └── release-automation.yml
├── templates/
│   └── ReleaseTemplate.md
├── README.md
```

