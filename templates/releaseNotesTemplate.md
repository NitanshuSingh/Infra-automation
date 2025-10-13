# 🚀 Release Notes - $(Build.BuildNumber)

**Release Date:** $(Date)  
**Triggered By:** $(Build.RequestedFor)

## 🧩 Features & Epics

{{#forEach workItems}}
### {{this.fields['System.Title']}}
**Type:** {{this.fields['System.WorkItemType']}}  
**Assigned To:** {{this.fields['System.AssignedTo']}}  
**Description:** {{this.fields['System.Description']}}

{{#if this.parents}}
#### 🔗 Parent (Feature / Epic)
{{#forEach this.parents}}
- **{{this.fields['System.WorkItemType']}}:** {{this.fields['System.Title']}}
{{/forEach}}
{{/if}}

---
{{/forEach}}


