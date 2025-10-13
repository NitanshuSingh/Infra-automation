## 🚀 Release Notes — Build {{buildDetails.buildNumber}}

> **Completed:** {{buildDetails.finishTime}} &nbsp;&nbsp;|&nbsp;&nbsp; **Branch:** {{buildDetails.sourceBranch}} &nbsp;&nbsp;|&nbsp;&nbsp; **Tags:** {{buildDetails.tags}}

### Build Summary
| Field | Value |
|---|---|
| Build | {{buildDetails.buildNumber}} |
| Completed | {{buildDetails.finishTime}} |
| Branch | {{buildDetails.sourceBranch}} |
| Tags | {{buildDetails.tags}} |
| Triggered By | {{#if buildDetails.requestedFor}}{{buildDetails.requestedFor.displayName}}{{else}}N/A{{/if}} |
| Previous Build | {{compareBuildDetails.buildNumber}} |

---

### Associated Pull Requests ({{pullRequests.length}})
{{#if pullRequests}}
| PR | Title | Author | Work Items | Commits |
|---:|---|---|---:|---:|
{{#forEach pullRequests}}
| [#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) | {{this.title}} | {{#if this.createdBy}}{{this.createdBy.displayName}}{{else}}Unknown{{/if}} | {{this.associatedWorkitems.length}} | {{this.associatedCommits.length}} |
{{/forEach}}
{{else}}
No pull requests associated with this build.
{{/if}}

---

### Associated Work Items ({{this.workItems.length}})
{{#if this.workItems}}
| ID | Title | Type | Assigned | Tags | PRs |
|---:|---|---|---|---|---|
{{#forEach this.workItems}}
| [#{{this.id}}]({{replace (replace (lookup this.fields 'System.Url') "_apis/wit/workItems" "_workitems/edit") "" ""}}) | {{lookup this.fields 'System.Title'}} | {{lookup this.fields 'System.WorkItemType'}} | {{#with (lookup this.fields 'System.AssignedTo')}}{{displayName}}{{else}}Unassigned{{/with}} | {{lookup this.fields 'System.Tags'}} | {{#forEach this.relations}}{{#if (contains this.attributes.name 'Pull Request')}}{{#with (lookup_a_pullrequest ../../pullRequests this.url)}}[#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) {{/with}}{{/if}}{{/forEach}} |
| ID | Title | Type | Assigned | Tags | Epic | PRs |
|---:|---|---|---|---|---|---|
| [#{{this.id}}]({{replace (replace (lookup this.fields 'System.Url') "_apis/wit/workItems" "_workitems/edit") "" ""}}) | {{lookup this.fields 'System.Title'}} | {{lookup this.fields 'System.WorkItemType'}} | {{#with (lookup this.fields 'System.AssignedTo')}}{{displayName}}{{else}}Unassigned{{/with}} | {{lookup this.fields 'System.Tags'}} | {{!-- Epic lookup: check parent then grandparent --}}
{{#with (lookup this.fields 'System.Url') }}{{/with}}
{{#if this.relations}}
   {{#forEach this.relations}}
      {{#if (contains this.attributes.name 'Parent')}}
         {{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}
            {{#if (contains (lookup this.fields 'System.WorkItemType') 'Epic')}}{{lookup this.fields 'System.Title'}}{{else}}
               {{!-- check grandparent --}}
               {{#forEach this.relations}}
                  {{#if (contains this.attributes.name 'Parent')}}
                     {{#with (lookup_a_work_item ../../../../relatedWorkItems this.url)}}
                        {{#if (contains (lookup this.fields 'System.WorkItemType') 'Epic')}}{{lookup this.fields 'System.Title'}}{{/if}}
                     {{/with}}
                  {{/if}}
               {{/forEach}}
            {{/if}}
         {{/with}}
      {{/if}}
   {{/forEach}}
{{/if}} |
{{/forEach}}
{{else}}
No work items found for this build.
{{/if}}

---

### Commits (from associated PRs and standalone)
{{#if pullRequests}}
| Commit | Message | Author |
|---|---|---|
{{#forEach pullRequests}}
   {{#forEach this.associatedCommits}}
| [{{this.commitId}}]({{this.remoteUrl}}) | {{this.comment}} | {{#if this.author}}{{this.author.name}}{{else}}Unknown{{/if}} |
   {{/forEach}}
{{/forEach}}
{{else}}
No commits associated with pull requests for this build.
{{/if}}

---

## Work Item Details
{{#if this.workItems}}
{{#forEach this.workItems}}
### Work Item #{{this.id}} — {{lookup this.fields 'System.Title'}}

| Field | Value |
|---|---|
| ID | [#{{this.id}}]({{replace (replace (lookup this.fields 'System.Url') "_apis/wit/workItems" "_workitems/edit") "" ""}}) |
| Type | {{lookup this.fields 'System.WorkItemType'}} |
| State | {{lookup this.fields 'System.State'}} |
| Assigned To | {{#with (lookup this.fields 'System.AssignedTo')}}{{displayName}}{{else}}Unassigned{{/with}} |
| Tags | {{lookup this.fields 'System.Tags'}} |

**Description**

{{#if (lookup this.fields 'System.Description')}}
{{{lookup this.fields 'System.Description'}}}
{{else}}
_No description provided._
{{/if}}

**Related PRs**
{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Pull Request')}}
      {{#with (lookup_a_pullrequest ../../pullRequests this.url)}}
- [#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) — {{this.title}}
      {{/with}}
   {{/if}}
{{/forEach}}

**Parents**
{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Parent')}}
      {{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}
- [#{{this.id}}]({{replace (replace this.url "_apis/wit/workItems" "_workitems/edit") "" ""}}) — {{lookup this.fields 'System.Title'}}
      {{/with}}
   {{/if}}
{{/forEach}}

**Children**
{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Child')}}
      {{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}
- [#{{this.id}}]({{replace (replace this.url "_apis/wit/workItems" "_workitems/edit") "" ""}}) — {{lookup this.fields 'System.Title'}}
      {{/with}}
   {{/if}}
{{/forEach}}

---
{{/forEach}}
{{else}}
No work item details to display.
{{/if}}