---

<div style="background-color:#f2f2f2; border:1px solid #ccc; padding:10px; border-radius:6px;">
  <h2><strong>Release Notes — Build {{buildDetails.buildNumber}}</strong></h2>
</div>


---

### Build Summary
| Field | Value |
|---|---|
| Build | {{buildDetails.buildNumber}} |
| Branch | {{buildDetails.sourceBranch}} |
| Tags | {{#if buildDetails.tags}}{{buildDetails.tags}}{{else}}{{#if (contains buildDetails.sourceBranch 'refs/tags/')}}{{replace buildDetails.sourceBranch 'refs/tags/' ''}}{{else}}{{buildDetails.sourceBranch}}{{/if}}{{/if}} |
| Triggered By | {{#if buildDetails.requestedFor}}{{buildDetails.requestedFor.displayName}}{{else}}N/A{{/if}} |

---

<details>
<summary><strong>Associated Pull Requests ({{pullRequests.length}})</strong></summary>

{{#if pullRequests}}
| PR | Title | Author | Work Items | Commits |
|---:|---|---|---:|---:|
{{#forEach (sort pullRequests "creationDate" "desc")}}
| [#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) | {{this.title}} | {{#if this.createdBy}}{{this.createdBy.displayName}}{{else}}Unknown{{/if}} | {{this.associatedWorkitems.length}} | {{this.associatedCommits.length}} |
{{/forEach}}
{{else}}
_No pull requests associated with this build._
{{/if}}

</details>

---

<details>
<summary><strong>Associated Work Items ({{this.workItems.length}})</strong></summary>

{{#if this.workItems}}
| ID | Title | Type | Assigned | Tags | PRs |
|---:|---|---|---|---|---|
{{#forEach (sort this.workItems "id" "desc")}}
| [#{{this.id}}]({{replace (replace (lookup this.fields 'System.Url') "_apis/wit/workItems" "_workitems/edit") "" ""}}) | {{lookup this.fields 'System.Title'}} | {{lookup this.fields 'System.WorkItemType'}} | {{#with (lookup this.fields 'System.AssignedTo')}}{{displayName}}{{else}}Unassigned{{/with}} | {{lookup this.fields 'System.Tags'}} | {{#forEach this.relations}}{{#if (contains this.attributes.name 'Pull Request')}}{{#with (lookup_a_pullrequest ../../pullRequests this.url)}}[#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) {{/with}}{{/if}}{{/forEach}} |
{{/forEach}}
{{else}}
_No work items found for this build._
{{/if}}

</details>

---

<details>
<summary><strong>Work Item Details</strong></summary>

{{#if this.workItems}}
{{#forEach (sort this.workItems "id" "desc")}}
### Work Item #{{this.id}} — {{lookup this.fields 'System.Title'}}

| Field | Value |
|---|---|
| ID | [#{{this.id}}]({{replace (replace (lookup this.fields 'System.Url') "_apis/wit/workItems" "_workitems/edit") "" ""}}) |
| Type | {{lookup this.fields 'System.WorkItemType'}} |
| State | {{lookup this.fields 'System.State'}} |
| Assigned To | {{#with (lookup this.fields 'System.AssignedTo')}}{{displayName}}{{else}}Unassigned{{/with}} |
| Tags | {{lookup this.fields 'System.Tags'}} |
| Feature | {{#each this.relations}}{{#if (contains this.attributes.name 'Parent')}}{{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}{{#if (contains (lookup this.fields 'System.WorkItemType') 'Feature')}}{{lookup this.fields 'System.Title'}}{{/if}}{{/with}}{{/if}}{{/each}} |
| Epic | {{#each this.relations}}{{#if (contains this.attributes.name 'Parent')}}{{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}{{#if (contains (lookup this.fields 'System.WorkItemType') 'Epic')}}{{lookup this.fields 'System.Title'}}{{else}}{{#each this.relations}}{{#if (contains this.attributes.name 'Parent')}}{{#with (lookup_a_work_item ../../../../relatedWorkItems this.url)}}{{#if (contains (lookup this.fields 'System.WorkItemType') 'Epic')}}{{lookup this.fields 'System.Title'}}{{/if}}{{/with}}{{/if}}{{/each}}{{/if}}{{/with}}{{/if}}{{/each}} |

<details>
<summary><strong>Description</strong></summary>

{{#if (lookup this.fields 'System.Description')}}
{{{lookup this.fields 'System.Description'}}}
{{else}}
_No description provided._
{{/if}}

</details>

<details>
<summary><strong>Related PRs</strong></summary>

{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Pull Request')}}
      {{#with (lookup_a_pullrequest ../../pullRequests this.url)}}
- [#{{this.pullRequestId}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}}) — {{this.title}}
      {{/with}}
   {{/if}}
{{/forEach}}

</details>

<details>
<summary><strong>Parents</strong></summary>

{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Parent')}}
      {{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}
- [#{{this.id}}]({{replace (replace this.url "_apis/wit/workItems" "_workitems/edit") "" ""}}) — {{lookup this.fields 'System.Title'}}
      {{/with}}
   {{/if}}
{{/forEach}}

</details>

<details>
<summary><strong>Children</strong></summary>

{{#forEach this.relations}}
   {{#if (contains this.attributes.name 'Child')}}
      {{#with (lookup_a_work_item ../../relatedWorkItems this.url)}}
- [#{{this.id}}]({{replace (replace this.url "_apis/wit/workItems" "_workitems/edit") "" ""}}) — {{lookup this.fields 'System.Title'}}
      {{/with}}
   {{/if}}
{{/forEach}}

</details>

---

{{/forEach}}
{{else}}
_No work item details to display._
{{/if}}

</details>
