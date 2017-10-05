---
title: "適用於 Linux 的虛擬機器擴充功能和功能 | Microsoft Docs"
description: "了解哪些擴充功能適用於 Azure 虛擬機器，並依它們提供或改善的內容來分組。"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 8a5b39351f665c51ae7d83f755329e54ff3cf786
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="992b2-103">適用於 Linux 的虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="992b2-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="992b2-104">「Azure 虛擬機器」擴充功能是小型的應用程式，可在「Azure 虛擬機器」上提供部署後設定及自動化工作。</span><span class="sxs-lookup"><span data-stu-id="992b2-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="992b2-105">例如，如果「虛擬機器」要求安裝軟體、防毒保護或 Docker 組態，便可使用 VM 擴充功能來完成這些工作。</span><span class="sxs-lookup"><span data-stu-id="992b2-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="992b2-106">您可以使用 Azure CLI、PowerShell、Azure Resource Manager 範本及 Azure 入口網站來執行 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="992b2-107">擴充功能可以與新的虛擬機器部署搭配，或是在任何現有的系統上執行。</span><span class="sxs-lookup"><span data-stu-id="992b2-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="992b2-108">本文件提供 VM 擴充功能概觀、使用 Azure VM 擴充功能的必要條件，以及如何偵測、管理和移除 VM 擴充功能的指引。</span><span class="sxs-lookup"><span data-stu-id="992b2-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="992b2-109">本文件提供通用的資訊，因為有許多可用的 VM 擴充功能，每個都有唯一可能的組態。</span><span class="sxs-lookup"><span data-stu-id="992b2-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="992b2-110">可以在每份個別擴充功能專用的文件中找到擴充功能特定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="992b2-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="992b2-111">使用案例和範例</span><span class="sxs-lookup"><span data-stu-id="992b2-111">Use cases and samples</span></span>

<span data-ttu-id="992b2-112">有數個不同的 Azure VM 擴充功能可供使用，各有特定使用案例。</span><span class="sxs-lookup"><span data-stu-id="992b2-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="992b2-113">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="992b2-113">Some examples are:</span></span>

- <span data-ttu-id="992b2-114">使用適用於 Linux 的 DSC 擴充功能將 PowerShell 預期狀態設定套用至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="992b2-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="992b2-115">如需詳細資訊，請參閱 [Azure 期望狀態組態擴充功能簡介](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)。</span><span class="sxs-lookup"><span data-stu-id="992b2-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="992b2-116">使用 Microsoft 監視代理程式 VM 擴充功能設定虛擬機器的監視。</span><span class="sxs-lookup"><span data-stu-id="992b2-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="992b2-117">如需詳細資訊，請參閱[如何監視 Linux 虛擬機器](tutorial-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="992b2-117">For more information, see [How to monitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="992b2-118">使用 Datadog 擴充功能設定監視您的 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="992b2-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="992b2-119">如需詳細資訊，請參閱 [Datadog 部落格](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)。</span><span class="sxs-lookup"><span data-stu-id="992b2-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="992b2-120">使用 Docker VM 擴充功能設定 Azure 虛擬機器上的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="992b2-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="992b2-121">如需詳細資訊，請參閱 [Docker VM 擴充功能](dockerextension.md)。</span><span class="sxs-lookup"><span data-stu-id="992b2-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="992b2-122">除了處理序特定擴充功能，自訂指令碼延伸模組適用於 Windows 和 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="992b2-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="992b2-123">適用於 Linux 的自訂指令碼延伸模組可讓任何 Bash 指令碼在虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="992b2-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="992b2-124">自訂指令碼對於設計需要超過原生 Azure 工具可提供之設定的 Azure 部署很有用。</span><span class="sxs-lookup"><span data-stu-id="992b2-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="992b2-125">如需詳細資訊，請參閱 [Linux VM 自訂指令碼延伸模組](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="992b2-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="992b2-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="992b2-126">Prerequisites</span></span>

<span data-ttu-id="992b2-127">每個虛擬機器擴充功能可能有它自己的必要條件組。</span><span class="sxs-lookup"><span data-stu-id="992b2-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="992b2-128">比方說，Docker VM 擴充功能有受支援 Linux 散發套件的必要條件。</span><span class="sxs-lookup"><span data-stu-id="992b2-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="992b2-129">擴充功能特定文件中詳述的個別擴充功能的需求。</span><span class="sxs-lookup"><span data-stu-id="992b2-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="992b2-130">Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="992b2-130">Azure VM agent</span></span>

<span data-ttu-id="992b2-131">「Azure VM 代理程式」可管理「Azure 虛擬機器」與「Azure 網狀架構控制器」之間的互動。</span><span class="sxs-lookup"><span data-stu-id="992b2-131">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="992b2-132">VM 代理程式負責部署和管理「Azure 虛擬機器」的許多功能層面，包括執行「VM 擴充功能」。</span><span class="sxs-lookup"><span data-stu-id="992b2-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="992b2-133">「Azure VM 代理程式」會預先安裝在「Azure Marketplace 映像」上，並可手動安裝在支援的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="992b2-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="992b2-134">如需有關支援的作業系統和安裝指示，請參閱 [Azure 虛擬機器代理程式](../windows/classic/agents-and-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="992b2-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="992b2-135">探索 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-135">Discover VM extensions</span></span>

<span data-ttu-id="992b2-136">有許多不同的 VM 擴充功能可供與「Azure 虛擬機器」搭配使用。</span><span class="sxs-lookup"><span data-stu-id="992b2-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="992b2-137">若要查看完整清單，請使用 Azure CLI 來執行下列命令，其中將範例位置取代成所選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="992b2-137">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="992b2-138">執行 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="992b2-138">Run VM extensions</span></span>

<span data-ttu-id="992b2-139">Azure 虛擬機器延伸模組可以在現有的虛擬機器上執行，這在需要進行組態變更或復原已部署之 VM 上的連線時很有用。</span><span class="sxs-lookup"><span data-stu-id="992b2-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="992b2-140">VM 擴充功能也可以搭配 Azure Resource Manager 範本部署。</span><span class="sxs-lookup"><span data-stu-id="992b2-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="992b2-141">使用具有 Resource Manager 範本中的擴充功能，可以部署及設定 Azure 虛擬機器而不需要部署後介入。</span><span class="sxs-lookup"><span data-stu-id="992b2-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="992b2-142">下列方法可用來針對現有的虛擬機器執行擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-142">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="992b2-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="992b2-143">Azure CLI</span></span>

<span data-ttu-id="992b2-144">Azure 虛擬機器擴充功能可以使用 `az vm extension set` 命令對現有的虛擬機器執行。</span><span class="sxs-lookup"><span data-stu-id="992b2-144">Azure virtual machine extensions can be run against an existing virtual machine by using the `az vm extension set` command.</span></span> <span data-ttu-id="992b2-145">這個範例會針對虛擬機器執行自訂指令碼延伸模組。</span><span class="sxs-lookup"><span data-stu-id="992b2-145">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="992b2-146">指令碼會產生類似下列文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="992b2-146">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="992b2-147">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="992b2-147">Azure portal</span></span>

<span data-ttu-id="992b2-148">VM 擴充功能可以透過 Azure 入口網站套用至現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="992b2-148">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="992b2-149">若要這樣做，請選取虛擬機器，選擇 [擴充功能]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="992b2-149">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="992b2-150">從可用延伸模組清單選取您想要的延伸模組，並遵循精靈中的指示。</span><span class="sxs-lookup"><span data-stu-id="992b2-150">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="992b2-151">下圖顯示從 Azure 入口網站安裝 Linux 自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-151">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![安裝自訂指令碼延伸模組](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="992b2-153">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="992b2-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="992b2-154">VM 擴充功能可以新增至 Azure Resource Manager 範本，並使用範本的部署執行。</span><span class="sxs-lookup"><span data-stu-id="992b2-154">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="992b2-155">當您使用範本部署擴充功能時，可以建立完全設定的 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="992b2-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="992b2-156">例如，下列 JSON 取自 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="992b2-156">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="992b2-157">此範本會部署一組負載平衡虛擬機器和 Azure SQL Database，並在每個 VM 上安裝 .NET 核心應用程式。</span><span class="sxs-lookup"><span data-stu-id="992b2-157">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="992b2-158">VM 擴充功能會處理軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="992b2-158">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="992b2-159">如需詳細資訊，請參閱完整的 [Resource Manager 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="992b2-159">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="992b2-160">如需詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)。</span><span class="sxs-lookup"><span data-stu-id="992b2-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="992b2-161">安全的 VM 擴充功能資料</span><span class="sxs-lookup"><span data-stu-id="992b2-161">Secure VM extension data</span></span>

<span data-ttu-id="992b2-162">當您執行 VM 擴充功能時，可能需要包含機密資訊，例如認證、儲存體帳戶名稱和儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="992b2-162">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="992b2-163">許多 VM 擴充功能包含受保護的組態，其會加密資料並只在目標虛擬機器內加以解密。</span><span class="sxs-lookup"><span data-stu-id="992b2-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="992b2-164">每個擴充功能有特定受保護的組態結構描述，並每個都會在擴充功能特定文件中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="992b2-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="992b2-165">下列範例會顯示適用於 Linux 的自訂指令碼延伸模組執行個體。</span><span class="sxs-lookup"><span data-stu-id="992b2-165">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="992b2-166">請注意，要執行的命令包含一組認證。</span><span class="sxs-lookup"><span data-stu-id="992b2-166">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="992b2-167">在此範例中，要執行的命令不會加密。</span><span class="sxs-lookup"><span data-stu-id="992b2-167">In this example, the command to execute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="992b2-168">將 **command to execute**屬性移至 **protected**組態可保護執行字串。</span><span class="sxs-lookup"><span data-stu-id="992b2-168">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="992b2-169">針對 VM 擴充功能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="992b2-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="992b2-170">每個 VM 擴充功能可能會有擴充功能特定的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="992b2-170">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="992b2-171">例如，當您使用自訂指令碼延伸模組時，指令碼執行詳細資料可以在擴充功能執行所在的虛擬機器上本機找到。</span><span class="sxs-lookup"><span data-stu-id="992b2-171">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="992b2-172">所有擴充功能特定疑難排解步驟都會在擴充功能特定文件中詳述。</span><span class="sxs-lookup"><span data-stu-id="992b2-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="992b2-173">下列疑難排解步驟適用於所有虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-173">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="992b2-174">檢視擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="992b2-174">View extension status</span></span>

<span data-ttu-id="992b2-175">在虛擬機器擴充功能都已針對虛擬機器執行後，請使用下列 Azure CLI 命令傳回擴充功能的狀態。</span><span class="sxs-lookup"><span data-stu-id="992b2-175">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="992b2-176">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="992b2-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="992b2-177">輸出看起來會像下列文字：</span><span class="sxs-lookup"><span data-stu-id="992b2-177">The output looks like the following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="992b2-178">也可以在 Azure 入口網站中找到擴充功能的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="992b2-178">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="992b2-179">若要檢視擴充功能的狀態，請選取虛擬機器中，選擇 [擴充功能]，然後選取所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-179">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="992b2-180">重新執行 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-180">Rerun a VM extension</span></span>

<span data-ttu-id="992b2-181">可能會發生必須重新執行虛擬機器擴充功能的情況。</span><span class="sxs-lookup"><span data-stu-id="992b2-181">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="992b2-182">您可以藉由移除延伸模組，然後使用您所選的執行方法重新執行延伸模組，來重新執行延伸模組。</span><span class="sxs-lookup"><span data-stu-id="992b2-182">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="992b2-183">若要移除擴充功能，請使用 Azure CLI 執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="992b2-183">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="992b2-184">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="992b2-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="992b2-185">您可以在 Azure 入口網站中使用下列步驟來移除擴充功能：</span><span class="sxs-lookup"><span data-stu-id="992b2-185">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="992b2-186">選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="992b2-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="992b2-187">選擇**擴充功能**。</span><span class="sxs-lookup"><span data-stu-id="992b2-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="992b2-188">選取所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="992b2-188">Select the desired extension.</span></span>
4. <span data-ttu-id="992b2-189">選擇**解除安裝**。</span><span class="sxs-lookup"><span data-stu-id="992b2-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="992b2-190">常見的 VM 擴充功能參考</span><span class="sxs-lookup"><span data-stu-id="992b2-190">Common VM extension reference</span></span>
| <span data-ttu-id="992b2-191">擴充功能名稱</span><span class="sxs-lookup"><span data-stu-id="992b2-191">Extension name</span></span> | <span data-ttu-id="992b2-192">說明</span><span class="sxs-lookup"><span data-stu-id="992b2-192">Description</span></span> | <span data-ttu-id="992b2-193">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="992b2-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="992b2-194">Linux 的自訂指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="992b2-195">對「Azure 虛擬機器」執行指令碼</span><span class="sxs-lookup"><span data-stu-id="992b2-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="992b2-196">Linux 的自訂指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="992b2-197">Docker 擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-197">Docker extension</span></span> |<span data-ttu-id="992b2-198">安裝 Docker 背景程式以支援遠端 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="992b2-198">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="992b2-199">Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="992b2-200">VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-200">VM Access extension</span></span> |<span data-ttu-id="992b2-201">重新取得對「Azure 虛擬機器」的存取權</span><span class="sxs-lookup"><span data-stu-id="992b2-201">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="992b2-202">VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="992b2-203">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="992b2-204">管理「Azure 診斷」</span><span class="sxs-lookup"><span data-stu-id="992b2-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="992b2-205">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="992b2-206">Azure VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-206">Azure VM Access extension</span></span> |<span data-ttu-id="992b2-207">管理使用者和認證</span><span class="sxs-lookup"><span data-stu-id="992b2-207">Manage users and credentials</span></span> |[<span data-ttu-id="992b2-208">適用於 Linux 的 VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="992b2-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
