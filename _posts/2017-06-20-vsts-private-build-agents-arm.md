---
layout: default
title: "VSTS Private Agents with ARM"
date: 2017-06-20
categories: Azure
excerpt: Coming soon...
---

## {{page.title}}

My customers love to use [VSTS](https://www.visualstudio.com/team-services/) to enable their DevOps capabilities, however in some cases due to security requirements they are not able to use the Hosted Agents.  In that case the other alternative is to use Private Agents, for detailed description on differences between the two configurations checkout the [blog](https://www.visualstudio.com/en-us/docs/build/concepts/agents/agents).

In this blog we’ll see on how to automagically deploy a VSTS Private Agent with [Azure Resource Manager](https://docs.microsoft.com/en-ca/azure/azure-resource-manager/resource-group-overview) (ARM) and some PowerShell.

The example does the following:
-	Creates an azure VM based on a galley image
-	Using a custom script extension via PowerShell it downloads latest VSTS extension to the VM
-	Installs and configures the VSTS extension
-	Registers the Private Agent with an existing VSTS Agent Pool

The scripts referenced below are based on [A Visual Studio based Visual Studio Team Services (VSTS) Build Agent Vm](https://github.com/Azure/azure-quickstart-templates/tree/master/visual-studio-vstsbuildagent-vm), however I’ve made improvements and simplifications to make it more enterprise ready.

Some of the improvements/modification are:
-	Removed public IP from VM template
-	Used the latest Azure gallery image for Windows Server 2016 gallery with VS 2017 community edition
-	Updated ARM APIs to use latest versions
-	Updated the template to use an existing vNet and subnet (private address space)
-	Updated the VM to use managed disk (no storage account required)

### Prerequisites
-	Azure Subscription and permissions to create Azure VMs
-	Existing vNet and subnet in your Azure Subscription (private address space)
-	VSTS Account
-	[Personal Access Token](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to register the Private Agent with VSTS
-	Existing VSTS [Agent Pool](https://www.visualstudio.com/en-us/docs/build/concepts/agents/pools-queues) to register your Private Agent

### Step 1 – Configure Parameters for the ARM Template
All the required scripts can be found in [this GitHub repo](https://github.com/mariuszdotnet/vsts-hosted-agents).  Start by cloning or forking the repo.  The first file you need to modify is the “azuredeploy.parameters.json” file.

 
![ARM Parameters]({{ site.url }}/assets/images/vsts-agent-fig1.png)

### Step 2 – Execute the PowerShell Script to run the ARM Template
Open your favorite editor and run the “deploy.ps1” script.  The script does few basic things:
-	Sets required variables
-	Login to Azure
-	Select the right Azure Subscription
-	Create the Resource Group for your VM
-	Tests the ARM Template
-	Executes the ARM Template
 
![ARM Template]({{ site.url }}/assets/images/vsts-agent-fig2.png)

The ARM Template “azuredeploy.json” file does the following:
-	Creates the Azure VM and deploys it into the existing vNet and subnet you provided
-	Executes the custom script extension with calls the “installvstsagent.ps1” file that does all the heavy lifting.  It downloads the latest agent, installs the agent, configures the agent and registers it with the existing VSTS Pool you have specified in the ARM Template parameters file.

Note: the script currently downloads the “installvstsagent.ps1” from public GitHub URL.  To make it more secure you could get the file from an Azure Storage Account.  Also, all the parameters/secrets could be tokenized into the configuration file and/or retrieved from Azure Key Vault.
Assuming everything goes according to plan in 5 to 10 minutes you should be able to see the registered Private Agent in your VSTS Agent Pool.
 
![Agent Pool with Private Agent]({{ site.url }}/assets/images/vsts-agent-fig3.png)


[back]({{ site.baseurl }}{% link index.md %})