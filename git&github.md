1.What is the difference between Git and GitHub?

Overall explanation
Git is a distributed version control system that helps track code changes locally.

GitHub is a cloud-based platform that hosts Git repositories, allowing developers to collaborate using pull requests, issue tracking, and CI/CD integrations.

2.What are Git tags, and how are they used in versioning?


Tags are markers used to label specific points in commit history, typically for releases or milestones.


Overall explanation
Tags are used to mark specific points in a project’s history (e.g., v1.0.0).

Example: git tag -a v1.0.0 -m "Release version 1.0.0" tags a commit with version v1.0.0.

3.What is the difference between git pull and git fetch?

git pull fetches and merges changes, while git fetch only downloads changes without merging them.

4.How do you remove a file from the Git repository but keep it locally?

git rm --cached <file>

5.What is the significance of GitHub Pull Requests in a CI/CD pipeline?

They ensure code changes are reviewed, discussed, and tested before merging.

Overall explanation
Pull Requests allow team members to review and discuss code changes before merging.

In a CI/CD pipeline, Pull Requests trigger automated tests and builds, ensuring that only validated code reaches production.

6. How do you set up GitHub Actions for automating workflows?
Overall explanation
GitHub Actions allow automation of builds, tests, and deployments.

To set up:

Create a .github/workflows directory.

Add a YAML file (e.g., ci.yml) defining triggers (push, PR) and actions (build, test).

GitHub will automatically execute the workflow based on defined events.

7.How do you handle large binary files in GitHub?

Overall explanation
Git LFS stores large files outside the main repository but tracks references to them.

This prevents the repository from becoming too large and speeds up cloning and fetching.

8.How do you configure GitHub to trigger Azure Pipelines automatically on a code push?

Set up a GitHub webhook and define triggers in azure-pipelines.yml.

Overall explanation
GitHub Webhooks allow Azure Pipelines to run automatically on code changes.

In azure-pipelines.yml, define triggers:

trigger:
  branches:
    include:
      - main
      - develop
This ensures automated builds and deployments.

9.How do you configure a multi-branch pipeline with a GitHub repository in Azure DevOps?

Define the trigger for specific branches in azure-pipelines.yml.

Overall explanation
In azure-pipelines.yml, you can define branch-specific triggers like:

trigger:
  branches:
    include:
      - main
      - develop
This ensures only selected branches trigger the pipeline.

10.How do you use GitHub secrets for secure token management in Azure Pipelines?

Store sensitive tokens in GitHub Secrets and reference them in Azure Pipelines using $(SECRET_NAME).

11.How do you trigger an Azure DevOps build pipeline when a pull request is created in GitHub?
Use the pr trigger in azure-pipelines.yml.

Overall explanation
In azure-pipelines.yml, use:

yaml
pr:
  branches:
    include:
      - main
      - develop
This automatically triggers a build when a PR is created in GitHub.

11.What is Git Submodule, and how is it used in real-world projects?

A Git repository embedded inside another Git repository.

Overall explanation
A Git Submodule is a repository inside another repository.

It helps manage dependencies or separate components like third-party libraries.

Example:

sh
git submodule add <repo-url> <path>

12. How do you perform a Git bisect to find a faulty commit?

Running git bisect start, marking commits as good or bad, and letting Git find the faulty commit.

Overall explanation
git bisect binary searches commit history to find the faulty commit efficiently.

Example:

sh
git bisect start
git bisect good <commit-hash>
git bisect bad <commit-hash>

13. How do you revert a specific commit in Git without affecting subsequent commits?

git revert <commit-hash>

14. Explain the concept of cherry-picking in Git. Provide an example.

Selecting specific commits from one branch and applying them to another.

Overall explanation
git cherry-pick applies a specific commit from one branch to another.

Example:

git cherry-pick abc1234

15. How do you handle and resolve detached HEAD state in Git?
git branch -b <new-branch>

Overall explanation
Detached HEAD means you're not on a branch.

Fix: Create a new branch and switch back:

git checkout -b my-branch

16. What strategies do you follow for branch naming and version control in GitHub?
Using consistent naming conventions like feature/, bugfix/, release/.

Overall explanation
Standard naming conventions improve clarity:

Feature branches: feature/new-ui

Bugfix branches: bugfix/login-issue

Release branches: release/v1.2

17.What is GitHub's Dependabot, and how does it help in project security?
A bot that automatically scans and updates dependencies.

18. How do you audit commit history to ensure compliance and security in GitHub?
Use GitHub Audit Logs to track repository activity.

19.Explain the concept of Signed Commits in GitHub.
Signed commits verify the authenticity of a commit using GPG or SSH keys.

20. Describe a situation where you used GitHub to manage a production issue.

Created a hotfix branch, applied the changes, tested in staging, and merged it into the main branch.

Overall explanation
The correct approach is to create a hotfix branch from the main branch, apply the fix, test it in a staging environment, and merge it back into the main branch via a pull request. This ensures controlled deployment without affecting ongoing development.

21. How have you handled a scenario where a deployment failed due to a bad commit in GitHub?
Overall explanation
When a bad commit causes a deployment failure, the best practice is to use git log or git bisect to find the faulty commit, then revert it using git revert. This ensures minimal disruption while maintaining a clean history.

22. Can you explain how you manage hotfixes in GitHub in a production pipeline?

Overall explanation
The best practice is to create a hotfix branch from main, implement the fix, test it thoroughly, and then merge it back into both main and develop. This keeps the fix tracked and synchronized with ongoing development.

23.How do you roll back a deployment using GitHub and Azure DevOps?

Overall explanation
The correct rollback process involves reverting the problematic changes in GitHub, committing the rollback, and triggering a redeployment using Azure DevOps by specifying the last stable commit.

24.Share an example of a custom GitHub Action you implemented for an Azure DevOps workflow.

Overall explanation
A GitHub Action can be used to automate deployments by triggering a CI/CD pipeline when changes are pushed. A common use case is building and pushing Docker images to Azure Container Registry and triggering an Azure DevOps pipeline.

25.How do you perform GitOps using GitHub repositories for infrastructure as code in Azure?

Overall explanation
GitOps is a declarative approach where infrastructure as code (IaC) is stored in GitHub. CI/CD pipelines deploy changes automatically, and tools like Flux or ArgoCD monitor repositories for infrastructure updates.

26.A developer accidentally pushed sensitive credentials to a public GitHub repository. What should they do immediately to mitigate the risk?

Change the credentials immediately and use GitHub's secret scanning feature


Deleting the repository does not remove the commit from GitHub’s history, and using git rm --cached only removes the file from tracking, not from history. The correct approach is to immediately revoke and rotate the credentials (e.g., API keys, passwords), as they may have already been exposed. GitHub’s secret scanning can help detect leaked credentials and notify the owner. If necessary, history rewriting can be done, but it should be handled carefully.


27.
A company follows a Git workflow where feature branches need to be merged into develop before going to main. However, a developer accidentally merged a feature branch directly into main. How should this be fixed?

Use git revert to undo the merge in main and reapply changes to develop

Overall explanation
The safest way to fix this is to use git revert <merge-commit-hash> to create a new commit that undoes the merge while preserving history. Then, the feature branch can be properly merged into develop. Using git reset --hard is risky because it can delete history, especially in a shared repository. Cherry-picking is not ideal for larger changes, and deleting the main branch is not a viable solution.