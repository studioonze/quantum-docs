---
title: Honeywell quickstart for Azure Quantum
description: This document provides a step-by-step guide to get you started with Honeywell on Azure Quantum
author: mblouin
ms.author: mblouin
ms.topic: quickstart
uid: microsoft.quantum.quickstarts.computing.honeywell
---

# Honeywell quickstart for Azure Quantum

Learn how to use Azure Quantum to run Q# problems against the Honeywell simulator or QPU.

## Prerequisites

- To complete this tutorial you need an Azure subscription. If you don't have
  an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
- In this guide we'll use [Visual Studio Code](https://code.visualstudio.com/download) which you can download and use for free.

## Install the Quantum Development Kit and other resources

Before you can write a Q# program and run it with Honeywell, you'll need a few resources installed:

1. Install the [Microsoft QDK for VS Code extension](https://marketplace.visualstudio.com/items?itemName=quantum.quantum-devkit-vscode).
1. Install the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).
1. Install the `quantum` CLI extension for the Azure CLI.

   ```bash
   az extension add --source https://msquantumpublic.blob.core.windows.net/az-quantum-cli/quantum-latest-py3-none-any.whl
   ```

## Create an Azure Quantum workspace

You use the Azure Quantum service by adding an Azure Quantum workspace resource to your Azure subscription in the Azure portal. An Azure Quantum workspace resource, or workspace for short, is a collection of assets associated with running quantum or optimization applications.

To open the Azure Portal, go to https://portal.azure.com and then follow these steps:

1. Click **Create a resource** and then search for **Azure Quantum**. On the results page, you should see a tile for the **Azure Quantum (preview)** service.

   ![Tile for the Azure Quantum (preview)
   service](./media/azure-quantum-preview-search.png)

1. Click **Azure Quantum (preview)** and then click  **Create**. This opens a form to create a workspace.

   ![Create resource for the Azure Quantum (preview)
   service](./media/azure-quantum-preview-create.png)

1. Fill out the details of your workspace:
   - **Subscription:** The subscription that you want to associate with this
     workspace. 
   - **Resource group:** The resource group that you want to assign this workspace to.
   - **Name:** The name of your workspace.
   - **Region:** The region for the workspace.
   - **Storage Account**: The Azure storage account to store your jobs and results. If you don't have an existing storage account, click **Create a new storage account** and complete the necessary fields. For this preview, we recommend using the default values.

   ![Properties for the Azure Quantum workspace](./media/azure-quantum-preview-properties.png)


   > [!NOTE]
   > You must be an Owner of the selected resource group to create a new storage account. For more information about how resource groups work in Azure, see [Control and organize Azure resources with Azure Resource Manager](https://docs.microsoft.com/learn/modules/control-and-organize-with-azure-resource-manager/).

1. After completing the information, click the **Providers** tab to add providers to your workspace. A provider gives you access to a quantum service, which can be quantum hardware, a quantum simulator, or an optimization service.

   > [!NOTE]
   > If you do not see the Honeywell provider, you may not have access to their
   > preview yet. If you have received an email welcoming you to the Honeywell Preview
   > but you can't see their provider, please [create a ticket with Azure Support](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request).

   ![Providers for Azure Quantum](./media/azure-quantum-preview-providers.png)

   > [!NOTE]
   > By default, the Azure Quantum service adds the Microsoft QIO provider to every workspace.

1. Add at least the Honeywell provider, then click **Review + create**.

1. Review the settings and approve the *Terms and Conditions of Use* of
   the selected providers. If everything is correct, click **Create** to create your workspace.

   ![Review and create the workspace](./media/azure-quantum-preview-terms-honeywell.png)

> [!NOTE] 
> While we are not charging for usage of Azure Quantum during this
> preview, your jobs will be uploaded to the Azure storage account created above and will be subject to storage charges.

## Setup your project and write your program

Next, we'll open up Visual Studio Code and get create a Q# Project.

1. In VS Code open the **View** menu, and select **Command Palette**.

1. Type **Q#: Create New Project**.

1. Select **Standalone console application**.

1. Select a directory to hold your project, such as your home directory. Enter **QuantumRNG** as the project name, then select ***Create Project***.

1. From the window that appears at the bottom, select **Open new project**.

1. You should see two files: the project file and **Program.qs**, which contains starter code. Open **Program.qs**.

1. Start by opening the **QuantumRNG.csproj** file and adding the `ExecutionTarget` property, which will give you design-time feedback on the compatibility of your program for Honeywell's hardware.

```xml
<Project Sdk="Microsoft.Quantum.Sdk/0.14.2011120240">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <ExecutionTarget>honeywell.hqs-lt-1.0</ExecutionTarget>
  </PropertyGroup>
</Project>
```

1. Replace the contents of `Program.qs` with the program:

```qsharp
namespace QuantumRNG {
    open Microsoft.Quantum.Intrinsic;
    open Microsoft.Quantum.Measurement;
    open Microsoft.Quantum.Canon;

    @EntryPoint()
    operation GenerateRandomBits() : Result[] {
        use qubits = Qubit[4];
        ApplyToEach(H, qubits);
        return MultiM(qubits);
    }
}
```

> [!NOTE] 
> If you would like to learn more about this program code, we recommend checking out how to [Create your first Q# program by using the Quantum Development Kit](https://docs.microsoft.com/learn/modules/qsharp-create-first-quantum-development-kit/).

## Prepare the AZ CLI

Next, we'll prepare your environment to run the program against the workspace you created.

1. Use `quantum workspace set` to select the workspace you created above
   as the default workspace. Note that you also need to specify the resource
   group you created it in, for example:

   ```dotnetcli
   az quantum workspace set -g MyResourceGroup -w MyWorkspace -o table

   Location     Name                               ResourceGroup
   -----------  ---------------------------------  --------------------------------
   westus       ws-yyyyyy                          rg-yyyyyyyyy

   ```

1. In your workspace, there are different targets available from the
   providers that you added when you created the workspace. You can display a list of all
   the available targets with the command `az quantum target list -o table`:

   ```dotnetcli
   az quantum target list -o table

   Provider    Target-id                                       Status     Average Queue Time
   ----------  ----------------------------------------------  ---------  --------------------
   honeywell   honeywell.hqs-lt-1.0                            Available  0
   honeywell   honeywell.hqs-lt-1.0-apival                     Available  0
   ```

    > [!NOTE]
    > When you submit a job in Azure Quantum it will wait in a queue until the
    > provider is ready to run your program. The **Average Queue Time** column of
    > the target list command shows you how long recently run jobs had to wait in the queue. This can give you an idea of how long you
    > might have to wait.

## Run the program on hardware

To run the program on hardware, we'll use the asynchronous job submission command `az quantum job submit`. Like the `execute` command this will compile and submit your program, but it won't wait until the execution 
is complete. We recommend this pattern for running against hardware, because you may need to wait a while for your job to finish. To get an idea of how long you can run `az quantum target list -o table` as described above.

   ```dotnetcli
   az quantum job submit --target-id honeywell.hqs-lt-1.0 -o table

   Name        Id                                    Status    Target                Submission time
   ----------  ------------------------------------  --------  --------              ---------------------------------
   QuantumRNG  b4d17c63-2119-4d92-91d9-c18d1a07e08f  Waiting   honeywell.hqs-lt-1.0  2020-01-12T22:41:27.8855301+00:00
   ```

The table above shows that your job has been submitted and is waiting for its turn to run. To check on the status, use the `az quantum job show` command, being sure to replace the `job-id` parameter with the Id output by the previous command:

   ```dotnetcli
    az quantum job show -o table --job-id b4d17c63-2119-4d92-91d9-c18d1a07e08f 

   Name        Id                                    Status    Target    Submission time
   ----------  ------------------------------------  --------  --------  ---------------------------------
   QuantumRNG  b4d17c63-2119-4d92-91d9-c18d1a07e08f  Waiting   honeywell.hqs-lt-1.0  2020-10-22T22:41:27.8855301+00:00 
   ```

Eventually, you will see the `Status` in the above table change to `Succeeded`. Once that's done you can get the results from the job by running `az quantum job output`:

   ```dotnetcli
   az quantum job output -o table --job-id b4d17c63-2119-4d92-91d9-c18d1a07e08f 

   Result     Frequency
   ---------  -----------  -------------------------
   [0,0,0,0]  0.05200000   ▐█                      |
   [1,0,0,0]  0.07200000   ▐█                      |
   [0,1,0,0]  0.05000000   ▐█                      |
   [1,1,0,0]  0.06800000   ▐█                      |
   [0,0,1,0]  0.04600000   ▐█                      |
   [1,0,1,0]  0.06000000   ▐█                      |
   [0,1,1,0]  0.06400000   ▐█                      |
   [1,1,1,0]  0.07600000   ▐██                     |
   [0,0,0,1]  0.04800000   ▐█                      |
   [1,0,0,1]  0.06200000   ▐█                      |
   [0,1,0,1]  0.07400000   ▐█                      |
   [1,1,0,1]  0.08000000   ▐██                     |
   [0,0,1,1]  0.05800000   ▐█                      |
   [1,0,1,1]  0.06800000   ▐█                      |
   [0,1,1,1]  0.05200000   ▐█                      |
   [1,1,1,1]  0.07000000   ▐█                      |
   ```

The histogram you receive may be slightly different than the one above, but you should find that the states generally are observed with equal frequency.

## Next steps

This quickstart guide demonstrated how to get started running Q# programs against Honeywell's simulator and QPU. For more information on Honeywell's offerings, please see the [Honeywell Provider](xref:microsoft.quantum.providers.honeywell) documentation.

We recommend you continue your journey by learning more about the [different types of targets in Azure Quantum](xref:microsoft.quantum.concepts.targets), which will dictate which Q# programs you may run against a given provider. You might also be interested in learning how to submit Q# jobs with [Jupyter Notebooks](xref:microsoft.quantum.submit-jobs.jupyter) or with [Python](xref:microsoft.quantum.submit-jobs.python).

Looking for more samples to run? Check out the [samples directory](https://github.com/microsoft/qio-samples).

Lastly, if you would like to learn more about writing Q# programs please see the [Microsoft Quantum Documentation](xref:microsoft.quantum.overview.qdk-overview).