---
title: "aaaVirtual 適用於 Linux 機器擴充功能和功能 |Microsoft 文件"
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
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="0bbf3-103">適用於 Linux 的虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="0bbf3-104">「Azure 虛擬機器」擴充功能是小型的應用程式，可在「Azure 虛擬機器」上提供部署後設定及自動化工作。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="0bbf3-105">例如，如果虛擬機器需要的軟體安裝、 防毒保護或 Docker 組態，VM 延伸模組可以是使用的 toocomplete 這些工作。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="0bbf3-106">Azure VM 延伸模組可以使用 hello Azure CLI、 PowerShell、 Azure 資源管理員範本，來執行，與 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="0bbf3-107">擴充功能可以與新的虛擬機器部署搭配，或是在任何現有的系統上執行。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="0bbf3-108">本文件概述的 VM 擴充功能，使用 Azure VM 擴充功能和指引 toodetect，如何管理和移除 VM 擴充功能上的必要條件。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="0bbf3-109">本文件提供通用的資訊，因為有許多可用的 VM 擴充功能，每個都有唯一可能的組態。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="0bbf3-110">在每個文件特定 toohello 個別擴充功能，可以找到延伸模組的特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="0bbf3-111">使用案例和範例</span><span class="sxs-lookup"><span data-stu-id="0bbf3-111">Use cases and samples</span></span>

<span data-ttu-id="0bbf3-112">有數個不同的 Azure VM 擴充功能可供使用，各有特定使用案例。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="0bbf3-113">部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="0bbf3-113">Some examples are:</span></span>

- <span data-ttu-id="0bbf3-114">適用於使用 hello DSC 延伸模組，適用於 Linux 的 PowerShell 預期狀態設定 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="0bbf3-115">如需詳細資訊，請參閱 [Azure 期望狀態組態擴充功能簡介](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="0bbf3-116">設定虛擬機器以 hello Microsoft 監視代理程式 VM 擴充功能的監視。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="0bbf3-117">如需詳細資訊，請參閱[如何 toomonitor Linux VM](tutorial-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="0bbf3-118">設定監視 Azure 基礎結構以 hello Datadog 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="0bbf3-119">如需詳細資訊，請參閱 hello [Datadog 部落格](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="0bbf3-120">使用 hello Docker VM 擴充功能的 Azure 虛擬機器上設定 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="0bbf3-121">如需詳細資訊，請參閱 [Docker VM 擴充功能](dockerextension.md)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="0bbf3-122">此外 tooprocess 特定延伸項目，自訂指令碼延伸模組是適用於 Windows 和 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="0bbf3-123">hello 適用於 Linux 的自訂指令碼擴充功能可讓虛擬機器上執行任何 Bash 指令碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="0bbf3-124">自訂指令碼對於設計需要超過原生 Azure 工具可提供之設定的 Azure 部署很有用。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="0bbf3-125">如需詳細資訊，請參閱 [Linux VM 自訂指令碼延伸模組](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0bbf3-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="0bbf3-126">Prerequisites</span></span>

<span data-ttu-id="0bbf3-127">每個虛擬機器擴充功能可能有它自己的必要條件組。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="0bbf3-128">比方說，hello Docker VM 擴充功能包含受支援的 Linux 散發套件的必要的元件。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="0bbf3-129">Hello 延伸模組特定文件會詳細說明個別的擴充功能的需求。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="0bbf3-130">Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="0bbf3-130">Azure VM agent</span></span>

<span data-ttu-id="0bbf3-131">hello Azure VM 代理程式管理的 Azure 虛擬機器與 hello Azure 網狀架構控制器之間的互動。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="0bbf3-132">hello VM 代理程式會負責部署及管理 Azure 虛擬機器，包括執行 VM 擴充功能的許多功能層面。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="0bbf3-133">hello Azure VM 代理程式會預先安裝在 Azure Marketplace 映像，並手動安裝支援的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="0bbf3-134">如需有關支援的作業系統和安裝指示，請參閱 [Azure 虛擬機器代理程式](../windows/classic/agents-and-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="0bbf3-135">探索 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-135">Discover VM extensions</span></span>

<span data-ttu-id="0bbf3-136">有許多不同的 VM 擴充功能可供與「Azure 虛擬機器」搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="0bbf3-137">完整的清單中，執行下列命令以 hello Azure CLI、 hello 範例位置取代為您選擇的 hello 位置 hello toosee。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="0bbf3-138">執行 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="0bbf3-138">Run VM extensions</span></span>

<span data-ttu-id="0bbf3-139">Azure 虛擬機器擴充功能可以執行在現有的虛擬機器，您需要 toomake 組態變更或修復已部署的 VM 上的連線時很有用。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="0bbf3-140">VM 擴充功能也可以搭配 Azure Resource Manager 範本部署。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="0bbf3-141">使用具有 Resource Manager 範本中的擴充功能，可以部署及設定 Azure 虛擬機器而不需要部署後介入。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="0bbf3-142">hello 下列方法可以是使用的 toorun 針對現有的虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="0bbf3-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0bbf3-143">Azure CLI</span></span>

<span data-ttu-id="0bbf3-144">Azure 虛擬機器擴充功能可以針對現有的虛擬機器執行使用 hello`az vm extension set`命令。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="0bbf3-145">這個範例會針對虛擬機器執行 hello 自訂指令碼延伸。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="0bbf3-146">hello 指令碼會產生輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="0bbf3-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="0bbf3-147">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0bbf3-147">Azure portal</span></span>

<span data-ttu-id="0bbf3-148">VM 擴充功能可以透過 Azure 入口網站 hello 套用的 tooan 現有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="0bbf3-149">toodo，選取 hello 虛擬機器，選擇**延伸**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="0bbf3-150">選取您想要從 hello 可用延伸清單，並遵循 hello 精靈中的 hello 指示 「 hello 」 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="0bbf3-151">hello 下列影像顯示 hello hello Linux 自訂指令碼擴充功能，從 hello Azure 入口網站安裝。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![安裝自訂指令碼延伸模組](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="0bbf3-153">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="0bbf3-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="0bbf3-154">VM 擴充功能與 hello hello 範本部署執行，而且可以加入的 tooan Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="0bbf3-155">當您使用範本部署擴充功能時，可以建立完全設定的 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="0bbf3-156">例如，下列 JSON hello 取自 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="0bbf3-157">hello 範本將一組負載平衡虛擬機器和 Azure SQL database，部署，並在每個 VM 上安裝.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="0bbf3-158">hello VM 延伸模組會負責 hello 軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="0bbf3-159">如需詳細資訊，請參閱完整的 hello [Resource Manager 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="0bbf3-160">如需詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="0bbf3-161">安全的 VM 擴充功能資料</span><span class="sxs-lookup"><span data-stu-id="0bbf3-161">Secure VM extension data</span></span>

<span data-ttu-id="0bbf3-162">如果您執行的 VM 延伸模組，可能需要 tooinclude 機密資訊，例如認證、 儲存體帳戶名稱，以及儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="0bbf3-163">許多 VM 擴充功能包含受保護的組態加密資料，並只將它解密 hello 目標虛擬機器內。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="0bbf3-164">每個擴充功能有特定受保護的組態結構描述，並每個都會在擴充功能特定文件中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="0bbf3-165">hello 下列範例會顯示適用於 Linux 的 hello 自訂指令碼延伸執行個體。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="0bbf3-166">請注意該 hello 命令 tooexecute 包含一組認證。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="0bbf3-167">在此範例中，將不會加密 hello 命令 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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

<span data-ttu-id="0bbf3-168">移動 hello**命令 tooexecute**屬性 toohello**保護**組態保護 hello 執行字串。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="0bbf3-169">針對 VM 擴充功能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0bbf3-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="0bbf3-170">每個 VM 擴充功能可能會有疑難排解步驟特定 toohello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="0bbf3-171">例如，當您使用 hello 自訂指令碼擴充功能，指令碼執行詳細資料可以找到本機 hello hello 延伸模組執行所在的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="0bbf3-172">所有擴充功能特定的疑難排解步驟都會在擴充功能特定文件中詳述。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="0bbf3-173">下列疑難排解步驟的 hello 套用 tooall 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="0bbf3-174">檢視擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="0bbf3-174">View extension status</span></span>

<span data-ttu-id="0bbf3-175">已執行的虛擬機器的虛擬機器擴充功能之後，請使用下列 Azure CLI 命令 tooreturn 延伸模組狀態的 hello。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="0bbf3-176">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="0bbf3-177">hello 輸出看起來類似下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="0bbf3-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="0bbf3-178">也可以在 hello Azure 入口網站中找到延伸模組的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="0bbf3-179">tooview hello 狀態的延伸，選取 hello 虛擬機器，選擇**延伸**，並選取 hello 所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="0bbf3-180">重新執行 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-180">Rerun a VM extension</span></span>

<span data-ttu-id="0bbf3-181">可能是虛擬機器擴充功能必須 toobe 的情況下重新執行。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="0bbf3-182">您可以藉由移除它，然後重新執行您選擇的執行方法 hello 延伸模組執行擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="0bbf3-183">擴充功能，執行下列命令以 hello Azure CLI hello tooremove。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="0bbf3-184">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="0bbf3-185">您可以使用 hello hello Azure 入口網站中的步驟，以移除擴充功能：</span><span class="sxs-lookup"><span data-stu-id="0bbf3-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="0bbf3-186">選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="0bbf3-187">選擇**擴充功能**。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="0bbf3-188">選取所需的 hello 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="0bbf3-189">選擇**解除安裝**。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="0bbf3-190">常見的 VM 擴充功能參考</span><span class="sxs-lookup"><span data-stu-id="0bbf3-190">Common VM extension reference</span></span>
| <span data-ttu-id="0bbf3-191">擴充功能名稱</span><span class="sxs-lookup"><span data-stu-id="0bbf3-191">Extension name</span></span> | <span data-ttu-id="0bbf3-192">說明</span><span class="sxs-lookup"><span data-stu-id="0bbf3-192">Description</span></span> | <span data-ttu-id="0bbf3-193">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="0bbf3-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0bbf3-194">Linux 的自訂指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="0bbf3-195">對「Azure 虛擬機器」執行指令碼</span><span class="sxs-lookup"><span data-stu-id="0bbf3-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="0bbf3-196">Linux 的自訂指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="0bbf3-197">Docker 擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-197">Docker extension</span></span> |<span data-ttu-id="0bbf3-198">安裝 hello Docker daemon toosupport 遠端 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="0bbf3-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="0bbf3-199">Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="0bbf3-200">VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-200">VM Access extension</span></span> |<span data-ttu-id="0bbf3-201">重新取得存取 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0bbf3-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="0bbf3-202">VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="0bbf3-203">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="0bbf3-204">管理「Azure 診斷」</span><span class="sxs-lookup"><span data-stu-id="0bbf3-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="0bbf3-205">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="0bbf3-206">Azure VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-206">Azure VM Access extension</span></span> |<span data-ttu-id="0bbf3-207">管理使用者和認證</span><span class="sxs-lookup"><span data-stu-id="0bbf3-207">Manage users and credentials</span></span> |[<span data-ttu-id="0bbf3-208">適用於 Linux 的 VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="0bbf3-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
