# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.buildDate}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 🧩 Work Items

{{#if workItems.length}}
{{#forEach workItems}}
### 🔖 {{this.fields.System.Title}}

**Type:** {{this.fields.System.WorkItemType}}  
**Assigned To:** {{#if this.fields.System.AssignedTo}}{{this.fields.System.AssignedTo.displayName}}{{else}}Unassigned{{/if}}  

**Description:**  
{{{this.fields.System.Description}}}

{{#if this.parents.length}}
#### 🔗 Parent Work Items

{{#forEach this.parents}}
- **{{this.fields.System.WorkItemType}}**: {{this.fields.System.Title}}
{{/forEach}}
{{/if}}

---
{{/forEach}}
{{else}}
⚠️ No work items linked to this build.
{{/if}}
