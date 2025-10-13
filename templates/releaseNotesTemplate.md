# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.buildDate}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 📦 User Stories in this Release

{{#if workItems.length}}
{{#forEach workItems}}
{{#if (eq this.fields['System.WorkItemType'] 'User Story')}}
### 📝 {{this.fields['System.Title']}}

**Description:**  
{{{this.fields['System.Description']}}}

**Assigned To:** {{#if this.fields['System.AssignedTo']}}{{this.fields['System.AssignedTo'].displayName}}{{else}}Unassigned{{/if}}

{{#if this.parents.length}}
#### 🔗 Parent Links
{{#forEach this.parents}}

- **{{this.fields['System.WorkItemType']}}**: {{this.fields['System.Title']}}

{{/forEach}}
{{/if}}

---

{{/if}}
{{/forEach}}
{{else}}
⚠️ No user stories found for this deployment.
{{/if}}

