# 1. Contents of extension
## 1.1. Tasks
### 1.1.1. Notify build status to Bitbucket
Click this link to go to the source: [./notifyBuildStatusToBitbucketRestApi](./notifyBuildStatusToBitbucketRestApi).  
Invoke a Bitbucket REST API as a part of your pipeline to update the build status for the currently git commit being built. This is a server-based (agentless) task and can therefore only be used in an agentless job.

# 2. How to use
1. Create a generic service connection in the project settings of your Azure DevOps project. The server url should be your Bitbucket base url and could for example be `https://yourorganization.televic.com`. The task then adds the following path `/rest/build-status/1.0/commits/<commit-hash>` to the configured url to perform the REST API call. The configured url should therefore not end with a slash `"/"`. Also enter a username and password for the service connection.
2. Install the extension with name "Notify build status to Bitbucket" in your Azure DevOps organization. This extension can be found here: https://marketplace.visualstudio.com/items?itemName=SwintDC.notify-build-status-to-bitbucket.
3. In your pipeline, inside a server-based (agentless) job, search the marketplace for the task with name "Notify build status to Bitbucket" and insert it in your pipeline.
4. Fill in all parameters. In the parameter "Generic service connection", pick the previously created generic service connection.

# 3. How to contribute
1. git clone this git repository
2. execute the command `npm install -g tfx-cli`  
   > **Note:** The version of tfx-cli originally used to develop this extension was v0.8.3.
3. execute the command `npm ci` in the root folder of this git repository
4. make your changes
5. execute the command `npx tfx-cli extension create` to create a .vsix file
6. upload the .vsix file to the Azure DevOps Marketplace
7. test the extension
8. create a pull request for your changes

# 4. Sources used when developing this extension
- https://developer.atlassian.com/server/bitbucket/how-tos/updating-build-status-for-commits/  
  This documentation of bitbucket explains how to update the build status in bitbucket using a REST API call.
- https://github.com/microsoft/azure-pipelines-tasks/blob/master/Tasks/InvokeRestApiV1/task.json  
  This is an example of another task which also performs a REST API call 
- https://github.com/jikuma/AzureDevOpsGithubRestApi/blob/master/githubrestapitask/task.json  
  This is an example of another extension containing  1 task.
- https://docs.microsoft.com/en-us/azure/devops/extend/get-started/node?view=azure-devops  
  This page explains how to create a Azure DevOps extension.
- https://docs.microsoft.com/en-us/azure/devops/extend/develop/integrate-build-task?view=azure-devops  
  This documentation gives a little information in general on how to create a custom build task in a Azure DevOps extension. It also references other interesting articles.
- https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-build-task?view=azure-devops  
  This documentation explains how to create an agent-based nodejs task.
- https://github.com/microsoft/azure-pipelines-tasks/blob/master/docs/authoring/servertaskauthoring.md  
  This documentation explains the differences between an agent-based task and a server-based (agentless) task on Azure DevOps. For example the "RunsOn" and "Execution" properties of the task.json.