# Azure AI Starter Template

> [!IMPORTANT]
> This file provides guidelines to complete setup after scaffolding and to validate your codebase. Feel free to remove this file.

## Standards and conventions

For a complete set of standards and conventions that will guarantee successful template validation, [visit this repository](https://github.com/Azure-Samples/azd-template-artifacts)

## Getting started

Before you get started please make sure to have the [Azure Developer CLI](https://learn.microsoft.com/azure/developer/azure-developer-cli/overview) installed. You may also need to meet all requirements in the [readme.md](./README.md) file.

### Step 1 - Scaffolding

To proceed with scaffolding using the terminal, change local directory to the desired one, 

`cd [my-project-directory]`

and run

`azd init --template [name-of-template]`

in this case, `[name-of-template]` is `azd-ai-starter`. This will clone the repo files to your directory, including all those Infrastructure as Code files necessary for the [Azure Developer CLI](https://learn.microsoft.com/azure/developer/azure-developer-cli/overview) to provision, build, and deploy your application.

### Step 2 - Provisioning AI resources

Now you can provision the necessary Azure resources, by running

`azd provision`

You may need to be logged in to Azure. Follow instructions in the [Deploy to Azure](./README.md#quickstart) section of the [readme.md](./README.md) file.

> [!TIP]
> You may want to check available regions and quota by running the provided [script](#).

### Step 3 - Develop your application

Once your Azure OpenAI resources are provisioned, you may want to continue developing your application, as per your requirments and specifications. You may want to refer to our [operational guidelines](https://github.com/Azure-Samples/azd-template-artifacts/blob/main/docs/development-guidelines/operational-guidelines.md) that provide guidance to succeed when developing application samples.

Make sure to implement the right tools for local testing.

### Step 4 - Deploy your application to the cloud

Once your application development is complete and local testing has succeeded, add or update your Bicep files and the corresponding [azure.yaml](./azure.yaml) configuration to complete your application deployment to Azure. 

#### API Version Information

You can run the[listApiVersions](./scripts/listApiVersions.sh) or [listApiVersions](./scripts/listApiVersions.ps1) script, for your corresponding platform, to get a list of available Bicep APIs

When done, run

`azd up`

This will provision all required resources to host your application and run compute when necessary, and deploy all artifacts to Azure. You may be prompted to select again a region for those resources.

When the deployment is complete, you can test your application in the cloud.

### Step 5 - Validation and template publishing

Commit and push your code changes to your repository on [GitHub](https://github.com/), to run the `validation` workflow. The workflow will create a `Success criteria` issue in your repository, and check the passing criteria.

If it succeeds and all success criteria is met, you're ready to create a pull request to the [AI Gallery](https://azure.github.io/ai-apps/) following these guidelines [TBD](#)

If the validation fails, the system will create the corresponding in your repository. Before you open a PR, you will need to fix all issues and close them and mark the corresponding criteria passed, as well as run the validation worflow manually, again.

## Reporting Issues and Feedback

If you have any feature requests, issues, or areas for improvement, please [file an issue](https://github.com/Azure-Samples/azd-template-artifacts/issues), including the template you're reporting issues for.