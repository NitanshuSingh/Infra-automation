# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.startTime}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 📌 Work Items

| ID | Type | Title | Feature | Epic |
|----|------|-------|---------|------|
{{#forEach workItems}}
| {{id}} 
| {{lookup fields 'System.WorkItemType'}} 
| [{{lookup fields 'System.Title'}}]({{replace url '_apis/wit/workItems' '_workitems/edit'}}) 
| {{#each (lookup . 'parents')}}{{#if (eq (lookup fields 'System.WorkItemType') 'Feature')}}[{{lookup fields 'System.Title'}}]({{replace url '_apis/wit/workItems' '_workitems/edit'}}){{/if}}{{/each}} 
| {{#each (lookup . 'parents')}}{{#if (eq (lookup fields 'System.WorkItemType') 'Epic')}}[{{lookup fields 'System.Title'}}]({{replace url '_apis/wit/workItems' '_workitems/edit'}}){{/if}}{{/each}} |
{{/forEach}}

---

## 🔀 Pull Requests

{{#if pullRequests.length}}
{{#forEach pullRequests}}
* [{{title}}]({{replace (replace url '_apis/git/repositories' '_git') 'pullRequests' 'pullRequest'}})
{{/forEach}}
{{else}}
_No pull requests associated with this build._
{{/if}}
