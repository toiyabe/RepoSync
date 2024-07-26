# Azure DevOps Repository Synchronizer

This is an Azure DevOps pipeline script that keeps files in a source repository--known as the "upstream" repository--
synchronized with the files in another repository--known as the "downstream" repository.

## Install Pipeline Code

Upload the 'SyncPipeline.yml' YAML file to the __upstream__ Azure DevOps repository.

NOTE: This pipeline code will be run from the __downstream__ repository(ies), so there is no need to configure
it as a "pipeline" in the upstream repo.

## Choose the type of trigger

Next, choose what kind of [trigger](https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/azure-repos-git?view=azure-devops&tabs=yaml#ci-triggers) will be used to start the pipeline from the __downstream__ repository(s). Example triggers are found in the YAML file.

## Create "Downstream" Repository

After installing the pipeline, simply "clone" the upstream repository to create the "downstream" repository.
The downstream repository will contain a mirror copy of the upstream source--including a copy of the pipeline YAML file.

## Gather Environment Variable Values

The pipeline setup requires six environment variables to be set. It is best to gather those values now
before continuing.  The following shows the variable names their values:

| Variable        | Value           | Save as Secret   |
| --------------- | --------------- | ---------------- |
| UPSTREAMPATH    | Path to upstream repo     | No      |
| UPSTREAMUSER    | Git credentials username | No      |
| UPSTREAMKEY     | Git credentials password | Yes     |
| DOWNSTREAMPATH  | Path to downstream repo   | No      |
| DOWNSTREAMUSER  | Git credentials username | No      |
| DOWNSTREAMKEY   | Git credentials password | Yes     |

Notes:

* The username and password credentials can be obtained by clicking on "Files" under the "Repo" tab on left, then "Clone," then "Generate Credentials."
* The two "KEY" variables should be saved as "Secrets" so they are not visible as clear text.
* Example path:
  *  dev.azure.com/MoonriseSoftwareLLC/TestUpStream/_git/TestUpStream

NOTE: The path __DOES NOT__ start with "https://"

## Setup the "Downstream" Pipeline

Setup consists of two steps: (1) create the pipeline in the downstream
repo(s) then, (2) set the pipeline environment variables.

### Create Pipeline

From the __downstream__ Azure DevOps project home screen choose "Pipelines," then follow these steps:

1. Click "Create Pipeline."
2. Then it asks "Where is your code?"  Here select  "Azure Repos Git (YAML)."
3. On the next tab, select the current repo.
4. Now on the "Configure your pipeline" tab, scroll down and select "Existing Azure Pipelines YAML file."
5. When the popup dialog appears, select "/SyncPipeline.yml" file, then "Continue."

### Set Environment Variables

While in the "edit" mode for the pipeline, add the six environment variables above to your pipeline by clicking on the "Variables" button, and clicking the plus (+) button for each variable.

Remember to click on the __"Keep this value secret"__ check box for the two __"KEY"__ variables.

## Final Notes

* Test the pipeline by clicking "Run."
* You can modify the pipeline by editing the YAML file in the __upstream__ repo.
* Any changes to the YAML file in the __downstream__ repo will be overwritten by the current files in the __upstream__ repo.
