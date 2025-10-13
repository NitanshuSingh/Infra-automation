🚀 Release Notes - {{buildDetails.buildNumber}}
Release Date: {{buildDetails.buildDate}}
Triggered By: {{buildDetails.requestedFor.displayName}}

🧩 Work Items
{{#if workItems}}
{{#each workItems}}

🔖 {{this.fields['System.Title']}}
Type: {{this.fields['System.WorkItemType']}}
Assigned To: {{#if this.fields['System.AssignedTo.displayName']}}{{this.fields['System.AssignedTo.displayName']}}{{else}}Unassigned{{/if}}

Description:
{{#if this.fields['System.Description']}}
{{this.fields['System.Description']}}
{{else}}
No description provided.
{{/if}}

🔗 Parent Feature/Epic
{{#if this.parents}}
{{#each this.parents}}

{{this.fields['System.WorkItemType']}}: {{this.fields['System.Title']}}
{{/each}}
{{else}}
No parent feature or epic linked.
{{/if}}

{{/each}}
{{else}}
⚠️ No work items linked to this build.
{{/if}}

