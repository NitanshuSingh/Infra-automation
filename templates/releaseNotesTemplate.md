# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.startTime}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 📌 Work Items

| ID | Type | Title | Feature | Epic |
|----|------|-------|---------|------|
{{#forEach workItems}}
| {{id}} | {{lookup fields 'System.WorkItemType'}} | [{{lookup fields 'System.Title'}}]({{replace url "_apis/wit/workItems" "_workitems/edit"}}) | 
{{#with (lookup this 'parents')}}
  {{#each this}}
    {{#if (eq (lookup fields 'System.WorkItemType') 'Feature')}}
      [{{lookup fields 'System.Title'}}]({{replace url "_apis/wit/workItems" "_workitems/edit"}})
    {{/if}}
  {{/each}}
{{else}} - {{/with}} | 
{{#with (lookup this 'parents')}}
  {{#each this}}
    {{#if (eq (lookup fields 'System.WorkItemType') 'Epic')}}
      [{{lookup fields 'System.Title'}}]({{replace url "_apis/wit/workItem_)
