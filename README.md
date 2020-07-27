# ArmTemplateForDemo
This is a public repo for Arm template testing.

# Add and configure the Azure Resource Group Deployment task.

- The task references both the artifact you built with the Copy Files task and your pipeline variables. Set these values when configuring your task.

	- Deployment scope (deploymentScope): Set the deployment scope to Resource Group. You can target your deployment to a management group, an Azure subscription, or a resource group.
	- Azure Resource Manager connection (azureResourceManagerConnection): Select your Azure Resource Manager service connection. To configure new service connection, select the Azure subscription from the list and click Authorize. See Connect to Microsoft Azure for more details
	- Subscription (subscriptionId): Select the subscription where the deployment should go.
	- Action (action): Set to Create or update resource group to create a new resource group or to update an existing one.
	- Resource group: Set toARMPipelinesLAMP-rg to name your new resource group. If this is an existing resource group, it will be updated.
	- Location(location): Location for deploying the resource group. Set to your closest location (for example, West US). If the resource group already exists in your subscription, this value will be ignored.
	- Template location (templateLocation): Set to Linked artifact. This is location of your template and the parameters files.
	- Template (cmsFile): Set to $(Build.ArtifactStagingDirectory)/azuredeploy.json. This is the path to the ARM template.
	- Template parameters (cmsParametersFile): Set to $(Build.ArtifactStagingDirectory)/azuredeploy.parameters.json. This is the path to the parameters file for your ARM template.
	- Override template parameters (overrideParameters): Set to -siteName $(siteName) -administratorLogin $(adminUser) -administratorLoginPassword $(ARM_PASS) to use the variables you created earlier. These values will replace the parameters set in your template parameters file.
	- Deployment mode (deploymentMode): The way resources should be deployed. Set to Incremental. Incremental keeps resources that are not in the ARM template and is faster than Complete. Validate mode lets you find problems with the template before deploying.


# Documentation on Azure Resource Manager (ARM) Template Deployment Task:

https://github.com/microsoft/azure-pipelines-tasks/tree/master/Tasks/AzureResourceManagerTemplateDeploymentV3
