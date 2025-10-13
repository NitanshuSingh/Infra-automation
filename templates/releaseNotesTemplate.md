# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.buildDate}}  
**Triggered By:** {{buildDetails.requestedFor}}

---

## 🧩 Features & Epics

{{#forEach workItems}}
### 🔖 {{this.fields.System.Title}}

**Type:** {{this.fields.System.WorkItemType}}  
**Assigned To:** {{this.fields.System.AssignedTo.displayName}}  
**Description:**  
{{{this.fields.System.Description}}}

{{#if this.parents}}
#### 🔗 Parent (Feature / Epic)
{{#forEach this.parents}}
- **{{this.fields.System.WorkItemType}}**: {{this.fields.System.Title}}
{{/forEach}}
{{/if}}

---

{{/forEach}}
