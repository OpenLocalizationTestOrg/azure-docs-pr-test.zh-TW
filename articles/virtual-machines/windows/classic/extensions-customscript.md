---
title: "aaaCustom Windows VM 上的指令碼延伸 |Microsoft 文件"
description: "在遠端 Windows VM 上使用 hello 自訂指令碼延伸 toorun PowerShell 指令碼自動化 Azure VM 組態工作"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="f062d-103">自訂指令碼擴充功能的 Windows hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="f062d-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f062d-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f062d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f062d-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f062d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f062d-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="f062d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f062d-107">了解如何太[使用 hello 資源管理員的模型執行這些步驟](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f062d-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f062d-108">hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f062d-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="f062d-109">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="f062d-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f062d-110">可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f062d-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="f062d-111">hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。</span><span class="sxs-lookup"><span data-stu-id="f062d-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f062d-112">這份文件詳細說明如何使用自訂指令碼擴充 toouse hello hello Azure PowerShell 模組、 Azure 資源管理員範本及疑難排解在 Windows 系統上的步驟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f062d-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f062d-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f062d-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f062d-114">作業系統</span><span class="sxs-lookup"><span data-stu-id="f062d-114">Operating System</span></span>

<span data-ttu-id="f062d-115">hello 自訂指令碼擴充的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。</span><span class="sxs-lookup"><span data-stu-id="f062d-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="f062d-116">指令碼位置</span><span class="sxs-lookup"><span data-stu-id="f062d-116">Script Location</span></span>

<span data-ttu-id="f062d-117">hello 指令碼需要 toobe 儲存在 Azure 儲存體或可透過有效的 URL 存取的任何其他位置。</span><span class="sxs-lookup"><span data-stu-id="f062d-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f062d-118">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="f062d-118">Internet Connectivity</span></span>

<span data-ttu-id="f062d-119">hello 自訂指令碼擴充功能的 Windows 需要該 hello 目標虛擬機器已連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f062d-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="f062d-120">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="f062d-120">Extension schema</span></span>

<span data-ttu-id="f062d-121">hello 下列 JSON 顯示 hello hello 自訂指令碼擴充的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f062d-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="f062d-122">hello 延伸模組需要的指令碼位置 （Azure 儲存體或其他位置，以有效的 URL） 和命令 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="f062d-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="f062d-123">如果使用 Azure 儲存體做為 hello 指令碼來源，Azure 儲存體帳戶名稱和帳戶金鑰需要。</span><span class="sxs-lookup"><span data-stu-id="f062d-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="f062d-124">這些項目應該視為機密資料，並且在 hello 延伸的受保護的設定組態中指定。</span><span class="sxs-lookup"><span data-stu-id="f062d-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="f062d-125">Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="f062d-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="f062d-126">屬性值</span><span class="sxs-lookup"><span data-stu-id="f062d-126">Property values</span></span>

| <span data-ttu-id="f062d-127">名稱</span><span class="sxs-lookup"><span data-stu-id="f062d-127">Name</span></span> | <span data-ttu-id="f062d-128">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="f062d-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f062d-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f062d-129">apiVersion</span></span> | <span data-ttu-id="f062d-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f062d-130">2015-06-15</span></span> |
| <span data-ttu-id="f062d-131">publisher</span><span class="sxs-lookup"><span data-stu-id="f062d-131">publisher</span></span> | <span data-ttu-id="f062d-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="f062d-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="f062d-133">擴充功能</span><span class="sxs-lookup"><span data-stu-id="f062d-133">extension</span></span> | <span data-ttu-id="f062d-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="f062d-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="f062d-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f062d-135">typeHandlerVersion</span></span> | <span data-ttu-id="f062d-136">1.8</span><span class="sxs-lookup"><span data-stu-id="f062d-136">1.8</span></span> |
| <span data-ttu-id="f062d-137">fileUris (例如)</span><span class="sxs-lookup"><span data-stu-id="f062d-137">fileUris (e.g)</span></span> | <span data-ttu-id="f062d-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="f062d-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="f062d-139">commandToExecute (例如)</span><span class="sxs-lookup"><span data-stu-id="f062d-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="f062d-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="f062d-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="f062d-141">範本部署</span><span class="sxs-lookup"><span data-stu-id="f062d-141">Template deployment</span></span>

<span data-ttu-id="f062d-142">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f062d-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f062d-143">hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 自訂指令碼擴充，在 Azure 資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="f062d-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="f062d-144">包含自訂指令碼擴充功能可以在這裡，找到的 hello 的範例範本[GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="f062d-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="f062d-145">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="f062d-145">PowerShell deployment</span></span>

<span data-ttu-id="f062d-146">hello`Set-AzureVMCustomScriptExtension`命令可以是使用的 tooadd hello 自訂指令碼延伸 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f062d-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="f062d-147">如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。</span><span class="sxs-lookup"><span data-stu-id="f062d-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="f062d-148">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="f062d-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="f062d-149">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f062d-149">Troubleshoot</span></span>

<span data-ttu-id="f062d-150">從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="f062d-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="f062d-151">擴充功能，針對指定的 VM，並執行下列命令的 hello toosee hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="f062d-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="f062d-152">延伸模組執行輸出我們記錄 toofiles hello hello 目標虛擬機器上下列目錄中找到。</span><span class="sxs-lookup"><span data-stu-id="f062d-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="f062d-153">hello 指令碼本身會下載到 hello hello 目標虛擬機器上下列目錄。</span><span class="sxs-lookup"><span data-stu-id="f062d-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="f062d-154">支援</span><span class="sxs-lookup"><span data-stu-id="f062d-154">Support</span></span>

<span data-ttu-id="f062d-155">如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="f062d-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f062d-156">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="f062d-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f062d-157">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="f062d-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f062d-158">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="f062d-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
