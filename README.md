# Azure DevOps and GitHub Q&A

## Azure Policy and Azure Pipelines

### 1. Enforcing Azure Policy compliance in a deployment pipeline

**Question:** A pipeline that deploys resources must ensure that the resources comply with applied policies. When a resource fails to comply, the deployment must stop. What should you add to each pipeline?

**Options:** A check gate; a webhook; a CodeQL test; a Visual Studio test.

**Answer: A check gate.**

A check gate can evaluate Azure Policy compliance before deployment proceeds. If the resources are non-compliant, the gate fails and prevents the deployment from continuing.

### 2. Automatically enabling TDE on Azure SQL databases

**Question:** Which Azure Policy effect should you use to ensure automatic remediation if an Azure SQL database is created without Transparent Data Encryption (TDE)?

**Options:** `auditIfNotExists`; `deployIfNotExists`; `deny`; `modify`.

**Answer: `deployIfNotExists`.**

This effect can deploy a related resource or configuration when it is missing or non-compliant, such as the TDE configuration for a database. The policy assignment needs an appropriately authorized managed identity for remediation.

### 3. Grouping regulatory compliance requirements

**Question:** You need to audit unencrypted Azure SQL databases, monitor NSGs for specific ports, check whether vulnerability assessment solutions are installed on VMs, and group the requirements for easier administration. What should you include?

**Options:** Initiative definition; policy definition; policy remediation; policy scope.

**Answer: Initiative definition.**

An initiative definition (policy set) groups multiple policy definitions so they can be assigned and managed together.

## Azure Boards and GitHub

### 4. Connecting a GitHub repository to Azure Boards with least privilege

**Question:** You need to link a GitHub repository to an Azure DevOps project so GitHub commits, pull requests, and issues can be associated with Azure Boards work items, while following least privilege. What should you use?

**Options:** A GitHub app installed in the GitHub organization; a GitHub user account that is a member of the repository; a personal access token (PAT); your GitHub account credentials.

**Answer: A GitHub app installed in the GitHub organization.**

The Azure Boards GitHub app can be granted access only to selected repositories and the permissions it needs, avoiding a connection tied to an individual's broader account access.

### 5. Connecting an Azure Repos repository and a GitHub repository to Azure Boards

**Question:** Project1 already contains Azure Repos Repo1. You also need to track work items across GitHub Repo2. What should you do first?

**Options:** Add Repo2 to Project1's GitHub connections; add the GitHub SSH key to Project1; move Repo1 to GitHub; move Repo2 to Project1.

**Answer: Add Repo2 to Project1's GitHub connections.**

Connect the GitHub repository to the Azure DevOps project through its GitHub connections. This lets GitHub development activity link to the project's work items without moving either repository.

### 6. Requiring traceability from code changes to Azure Boards work items

**Question:** Which two actions help ensure each GitHub code change can be traced to an Azure Boards work item?

**Options:** Configure branch protection to require a passing status check; retain Azure Pipelines build artifacts indefinitely; create a GitHub Action that validates commit messages; configure GitHub Actions to assign PRs based on labels.

**Answers:**

1. Create a GitHub Action that validates commit messages for Azure Boards work-item references, such as `AB#123`.
2. Configure branch protection to require that action's status check before merging.

The validation action checks that changes include a work-item reference, and branch protection prevents merging when the check fails.

### 7. Automating feedback request handling

**Question:** Your Azure DevOps organization uses a manual feedback request workflow to gather and triage stakeholder feedback. What should you do first to automate it?

**Options:** Create a GitHub issue; create an Azure DevOps GitHub service connection; create a notification subscription; create a service hook subscription.

**Answer: Create a service hook subscription.**

A service hook subscription can publish Azure DevOps events to an external service or automation workflow, which can then route or process feedback automatically.

## GitHub Projects and Repository Workflows

### 8. Adding repository issues to a GitHub project

**Question:** You need to add Repo1 issues to GitHub Project1. Which two actions can you perform?

**Options:** Create a workflow and link it to Project1; open an issue and assign it to Project1; assign the issue to the Project1 milestone; open Project1's Iteration Plan, select **Add item**, and choose the issue.

**Answers:**

1. Open an issue and add it to Project1 from the issue's **Projects** control.
2. From Project1, select **Add item** and choose the issue.

Both approaches add the issue to the project. A repository milestone is separate and does not add an issue to a project.

### 9. Accepting external contributions safely

**Question:** External contributors should be able to submit changes without affecting the main repository, while maintainers control integration. Which workflow should you recommend?

**Options:** Centralized; feature branch; forking; GitFlow.

**Answer: Forking.**

Contributors work in their own forks and submit pull requests to the main repository. Maintainers review and decide whether to merge the changes.

### 10. Marking a release point in repository history

**Question:** You need to mark a specific point in a GitHub repository's history as releases are created. What should you use?

**Options:** Actions; environment variables; tags; webhooks.

**Answer: Tags.**

A tag identifies a specific commit, commonly using a version such as `v1.0.0`. GitHub releases are associated with tags.

### 11. Preventing merge commits on a protected GitHub branch

**Question:** You need to ensure future commits to `main` do not use a merge strategy that creates merge commits. Which branch protection rule should you apply?

**Options:** Require a pull request before merging; require linear history; require signed commits; require status checks to pass before merging.

**Answer: Require linear history.**

This rule prevents merge commits on the protected branch. Pull requests must use a linear-history-compatible merge method, such as squash or rebase.

### 12. Isolating release-ready changes in Azure Repos

**Question:** You need a branching strategy that isolates changes ready for a release in one branch, manages changes for a future release separately, and keeps `main` production-ready. Which strategy should you recommend?

**Options:** Development isolation; feature isolation; main only; release isolation.

**Answer: Release isolation.**

Release isolation uses a release branch to stabilize the changes intended for a release, while work for a future release remains separate. `main` is reserved for production-ready code.

### 13. Viewing GitHub repository activity with minimal setup

**Question:** You need to monitor open issues, pull request frequency, and contributor activity over time, minimizing configuration. What should you use?

**Options:** GitHub Actions; GitHub Insights; GitHub webhooks; GitHub workflows.

**Answer: GitHub Insights.**

The repository's built-in Insights pages provide activity and contributor data without requiring custom automation.

## Pipeline Performance and Monitoring

### 14. Reducing pipeline build time while minimizing cost

**Question:** A pipeline build takes longer than expected. You need to reduce build time while minimizing costs. What should you recommend?

**Options:** Add an agent pool; configure multiple jobs to run in parallel; create a deployment group; upgrade the agent to a higher CPU.

**Answer: Configure multiple jobs to run in parallel.**

Splitting independent work into parallel jobs can reduce elapsed build time without upgrading to a more expensive agent. This works best when parallel-job capacity is already available.

### 15. Building a pipeline metrics dashboard from Log Analytics

**Question:** You have a Log Analytics workspace and need a custom dashboard for Azure DevOps pipeline duration and failure rate, with minimal engineering effort. What should you configure?

**Options:** A GitHub Actions insight; a Power BI semantic model; an Azure dashboard; an Azure Monitor workbook.

**Answer: An Azure Monitor workbook.**

Workbooks can query Log Analytics data and present it in charts, tables, and other visualizations, making them suitable for a low-effort custom monitoring dashboard.

### 16. Checking whether an application issue is region-specific

**Question:** Application Insights reports exceptions whenever users in Singapore open a specific page. You need to verify whether the issue is limited to specific regions. What should you do?

**Options:** Configure availability tests; configure user flows; modify Smart Detection rules; update Application Map components.

**Answer: Configure availability tests.**

Run availability tests against the affected page from multiple geographic locations. Comparing the results helps determine whether failures are limited to particular regions.

### 17. Investigating slow calls to an external service

**Question:** Users report slow page loads, and you suspect an external web service is responding slowly. What should you do first to validate the cause?

**Options:** Add an alert to an Azure Monitor performance metric; migrate the service to another region; set up availability tests; set up dependency tracking.

**Answer: Set up dependency tracking.**

Application Insights dependency tracking records outgoing calls and their duration and result. This lets you compare external-service latency with the application's performance.

### 18. Investigating exceptions with Application Insights

**Question:** Application Insights Smart Detection reports exceptions in an app connected to Azure SQL Database. Which tool can you use to investigate the exceptions?

**Options:** .NET Reflector; Fiddler; Snapshot Debugger; Extended Events.

**Answer: Snapshot Debugger.**

For supported applications and configurations, Snapshot Debugger captures diagnostic snapshots when exceptions occur. The snapshots can help inspect the call stack and relevant variable values.
