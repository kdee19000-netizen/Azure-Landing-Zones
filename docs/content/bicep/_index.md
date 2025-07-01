---
title: Bicep
geekdocCollapseSection: true
weight: 20
---

This section provides guidance for performing common tasks once you have deployed the [ALZ Bicep Accelerator]({{< relref "accelerator" >}}) and is currently specific to the [ALZ-Bicep modules](https://github.com/Azure/ALZ-Bicep).

## Getting Started

If you're new to Bicep or to the ALZ Accelerator, consider starting with:

- [Overview of ALZ-Bicep modules](https://github.com/Azure/ALZ-Bicep)
- [Deploying the Accelerator framework]
- [Customizing parameters and structure for your environment]

## What to Do After Deploying the Accelerator

Once the ALZ Bicep Accelerator is deployed, your platform engineering team can begin customizing and extending the Bicep modules using a Git-based workflow. The following steps guide you through setting up your local environment and using Azure DevOps (ADO) to manage changes.

### 1. Clone the Repository

Clone the accelerator repository from ADO:

```bash
git clone https://dev.azure.com/<your-org>/<your-project>/_git/<your-repo>
cd <your-repo>
```

### 2. Create a Feature Branch

Create a new Git branch to isolate your changes. This helps keep your work separate from the main branch and supports collaborative review through pull requests.

```bash
git switch -c feature/<your-feature-name>
```

### 3. Make and Commit Your Changes

Make the necessary updates to the Bicep files or configuration. Once your changes are ready, stage and commit them locally:

```bash
git add .
git commit -m "Short summary of your changes"
```

### 4. Push Your Branch to ADO

Once you've committed your changes locally, push the feature branch to Azure DevOps:

```bash
git push origin feature/<your-feature-name>
```

### 5. Create a Pull Request

In Azure DevOps:

- Navigate to **Repos > Pull Requests**
- You should see your feature branch listed with an option to create a pull request
- Ensure the **target branch** is `main`
- Add a clear **title** and **description** of your changes
- Assign the required **reviewers** (if not defined in your branch policies)
- Click **Create Pull Request**

### 6. Continuous Integration (CI) Validation

Once the pull request is created, it will automatically trigger:

- **Pipeline 01 - Azure Landing Zones Continuous Integration**

This pipeline performs a **What-If analysis** to preview the impact of your changes without applying them.

{{< hint type=tip >}}
🔍 Review the What-If output carefully to ensure the planned changes align with your expectations. Look for any unintended modifications or deletions.
{{< /hint >}}

### 7. Approve and Complete the Pull Request

After reviewing the What-If output and confirming the changes look correct:

- Have the assigned **reviewer approve** the pull request
- Click **Complete** in the PR view
- In the completion dialog:
  - ✅ Select **Squash commit** to combine all commits into one or another approach that fits your commit history strategy
  - ✅ Select **Delete source branch** to clean up the feature branch (optional but recommended)

This will merge your changes into the `main` branch and finalize the development workflow.

{{< hint type=tip >}}
💡 Tip: Squashing commits keeps your main branch history clean and easier to follow.
{{< /hint >}}

### 8. Continuous Delivery Pipeline (CD)

After merging into the `main` branch, the following pipeline is triggered automatically by default:

- **Pipeline 02 - Azure Landing Zones Continuous Delivery**

This pipeline runs a second **What-If analysis** to preview changes before deployment.

{{< hint type=tip >}}
🔍 Review the What-If output to ensure the planned deployment matches your expectations.
{{< /hint >}}

### 9. Review the Final What-If Output

Once the delivery pipeline runs, it will produce a **What-If analysis** showing the exact changes that will be applied to your Azure environment.

- Review the output carefully to ensure all planned updates are correct
- Verify that no unexpected changes or deletions are included

{{< hint type=important >}}
✅ This is your final checkpoint before deployment. Confirm that the changes align with the intended infrastructure update.
{{< /hint >}}

### 10. Approve and Deploy

Once the What-If output has been reviewed and validated:

- A reviewer should approve the **Deploy** stage in Azure DevOps (if manual approval is required)
- After approval, the pipeline will proceed to apply the changes to the target environment

## Azure Verified Modules (AVM) Transition

The documentation will be updated as the **Bicep Azure Verified Modules (AVM) for Platform Landing Zone (ALZ)** moves into public preview.

{{< hint type=tip >}}
If you're interested in early guidance or background on this initiative, refer to the official blog post:
[An Update on Bicep Azure Verified Modules for Platform Landing Zone (ALZ)](https://techcommunity.microsoft.com/blog/AzureToolsBlog/an-update-on-bicep-azure-verified-modules-for-platform-landing-zone-alz/4407626).
{{< /hint >}}
