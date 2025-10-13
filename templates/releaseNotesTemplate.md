    # {{buildDetails.buildNumber}}
    {{buildDetails.startTime}}

    **Work Items**
    |Id|Type|Title|
    |-|-|-|
    {{#forEach this.workItems}}
    |{{this.id}}|{{lookup this.fields 'System.WorkItemType'}}|[{{lookup this.fields 'System.Title'}}]({{replace this.url "_apis/wit/workItems" "_workitems/edit"}})|
    {{/forEach}}

    **Pull Requests**
    {{#forEach pullRequests}}
    * [{{this.title}}]({{replace (replace this.url "_apis/git/repositories" "_git") "pullRequests" "pullRequest"}})
    {{/forEach}}
    
    checkStage: true
    replaceFile: false
    getParentsAndChildren: false
    getAllParents: false
    getIndirectPullRequests: false
    stopOnError: false
    considerPartiallySuccessfulReleases: false
    checkForManuallyLinkedWI: false
    wiqlFromTarget: 'WorkItems'