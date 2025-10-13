# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.buildDate}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 🧩 User Stories

{{#if workItems.length}}
{{#forEach workItems}}
### 🔖 {{this.fields['System.Title']}}

**Type:** {{this.fields['System.WorkItemType']}}  
**Assigned To:** {{#if this.fields['System.AssignedTo']}}{{this.fields['System.AssignedTo'].displayName}}{{else}}Unassigned{{/if}}  

**Description:**  
{{{this.fields['System.Description']}}}

{{#if this.fields['System.Parent']}}
> 🔗 Parent Feature/Epic ID: **{{this.fields['System.Parent']}}**  
{{/if}}

{{/forEach}}
{{else}}
⚠️ No work items linked to this build.
{{/if}}
