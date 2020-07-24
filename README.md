# msa-devOps-2020
Deployed website URL: https://devops-caleb.azurewebsites.net/

# Build Pipeline
The build pipeline, defined by the "azure-pipelines" YAML script, carries out a series of tasks that are required to build a React app. The React app is built from code on the "msa-devOps-2020" GitHub repository which, in turn, is linked to an Azure Pipelines project. The "azure-pipelines" script has the following parts:
- Firstly, <b>push triggers</b> are defined using branch names. When commits are pushed to these branches, a continuous integration build is run. Here, I defined two triggers for the master and develop branches. Therefore, releases will be created when new commits are pushed to these two branches. 
- Next, <b>variables</b> are defined. These variables are assigned values that will be used multiple times throughout the script so that the code is easier to read and maintain. 
- The <b>pool</b> keyword is then used to define the operating system which will run on the virtual machine used, by the Microsoft-hosted build agent, to build the project.
- Finally, the <b>steps</b> section contains a number of tasks and a script which define how the project will be built on the virtual machine. These tasks and script have the following purposes:
  1. Download Node.js and add it to PATH
  2. Navigate to the root directory of the React app, install the packages required by the app, build the app and navigate back to the original directory
  3. Archive the latest build by compressing the contents of the "build" folder into a zipped folder 
  4. Publish the resulting arhive as a build artifact for the release pipeline to access
  
# Release Pipeline
The release pipeline has been configured in the Azure DevOps project. Using the latest build artifact that is created on completion of the build pipeline, the built React app is deployed to the given Azure App Service. However, the continuous deployment trigger has been enabled and set such that the release pipeline only runs when the React app is built from code commited and pushed to the "master" branch. 
