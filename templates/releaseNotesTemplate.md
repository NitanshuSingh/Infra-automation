# 🚀 Release Notes - {{buildDetails.buildNumber}}

**Release Date:** {{buildDetails.startTime}}  
**Triggered By:** {{buildDetails.requestedFor.displayName}}

---

## 📌 Work Items

| ID | Type | Title | Feature | Epic |
|----|------|-------|---------|------|
{{#each workItems}}
| {{this.id}} 
| {{lookup this.fields 'System.WorkItemType'}} 
| [{{lookup this.fields 'System.Title'}}]({{replace this.url "_apis/wit/workItems" "_workitems/edit"}}) 
| {{#with (lookup this 'parents')}}
  {{#each this}}
    {{#if (eq (lookup this.fields 'System.WorkItemType') 'Feature')}}
      [{{lookup this.fields 'System.Title'}}]({{replace this.url "_apis/wit/workItems" "_workitems/edit"}})
    {{/if}}
  {{/each}}
{{/with}} 
| {{#with (lookup this 'parents')}}
  {{#each this}}
    {{#if (eq (lookup this.fields 'System.WorkItemType') 'Epic')}}
      [{{lookup this.fields 'System.Title'}}]({{replace this.url "_apis/wit/workItems" "_workitems/edit"}})
    {{/if}}
  {{/each}}
{{/with}} |
{{/each}}

---

## 🔀 Pull Requests

{{#if pullRequests.length}}
{{#each pullRequests}}
- [{{this.title}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}})
{{/each}}
{{else}}
_No pull requests associated with this build._
{{/if}}
