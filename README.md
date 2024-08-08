# Azure DevOps Repository Synchronizer

This is an Azure DevOps pipeline script that keeps files in a source repository--known as the "upstream"
repository--synchronized with the files in another repository--known as the "downstream" repository.

## Install the Pipeline

Upload the 'azure-pipelines.yml' YAML file to the __upstream__ Azure DevOps repository. If you already have
a pipeline file by that same name, rename the file before uploading.

Once the YAML file is uploaded, select "__Pipelines__" on the DevOps project menu.

If the pipeline does not appear, you can load it as follows:

1. Click "Create Pipeline."
2. When asked, "Where is your code?" Select "Azure Repos Git (YAML)."
3. On the next tab, select the current repo.
4. Now on the "Configure your pipeline" tab, scroll down and select "Existing Azure Pipelines YAML file."
5. When the popup dialog appears, select "/azure-pipelines.yml" file (or what ever file name you used), then "Continue."

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

### Set Environment Variables

While in the "edit" mode for the pipeline, add the six environment variables above to your pipeline by clicking on the "Variables" button, and clicking the plus (+) button for each variable.

Remember to click on the __"Keep this value secret"__ check box for the two __"KEY"__ variables.

## Final Notes

* Test the pipeline by clicking "Run."
* You can modify the pipeline by editing the YAML file in the __upstream__ repo.
* Any changes to the YAML file in the __downstream__ repo will be overwritten by the current files in the __upstream__ repo.
