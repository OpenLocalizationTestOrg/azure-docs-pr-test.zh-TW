---
title: "Windows VM 上的自訂指令碼擴充功能 | Microsoft Docs"
description: "使用自訂指令碼擴充功能，在遠端 Windows VM 上執行 PowerShell 指令碼，將 Azure VM 組態工作自動化"
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
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="7853f-103">使用傳統部署模型自訂適用於 Windows 的指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="7853f-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7853f-104">Azure 建立和處理資源的部署模型有兩種： [Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="7853f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7853f-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="7853f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7853f-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="7853f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7853f-107">了解如何[使用 Resource Manager 模型執行這些步驟](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7853f-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7853f-108">「自訂指令碼擴充功能」會在 Azure 虛擬機器上下載並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="7853f-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="7853f-109">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="7853f-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="7853f-110">您可以從 Azure 儲存體或 GitHub 下載指令碼，或是在擴充功能執行階段將指令碼提供給 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7853f-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="7853f-111">「自訂指令碼擴充功能」會與 Azure Resource Manager 範本整合，您也可以使用 Azure CLI、PowerShell、Azure 入口網站或「Azure 虛擬機器 REST API」來執行它。</span><span class="sxs-lookup"><span data-stu-id="7853f-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="7853f-112">本文件詳細說明如何透過 Azure PowerShell 模組、Azure Resource Manager 範本使用自訂指令碼擴充功能，同時也詳細說明 Windows 系統上的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="7853f-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7853f-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7853f-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="7853f-114">作業系統</span><span class="sxs-lookup"><span data-stu-id="7853f-114">Operating System</span></span>

<span data-ttu-id="7853f-115">可以對 Windows Server 2008 R2、2012、2012 R2 和 2016 版執行適用於 Windows 的自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7853f-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="7853f-116">指令碼位置</span><span class="sxs-lookup"><span data-stu-id="7853f-116">Script Location</span></span>

<span data-ttu-id="7853f-117">指令碼必須儲存在 Azure 儲存體或任何可透過有效 URL 存取的其他位置。</span><span class="sxs-lookup"><span data-stu-id="7853f-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="7853f-118">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="7853f-118">Internet Connectivity</span></span>

<span data-ttu-id="7853f-119">適用於 Windows 的自訂指令碼擴充功能會要求目標虛擬機器連接到網際網路。</span><span class="sxs-lookup"><span data-stu-id="7853f-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="7853f-120">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="7853f-120">Extension schema</span></span>

<span data-ttu-id="7853f-121">下列 JSON 顯示自訂指令碼擴充功能的結構描述。</span><span class="sxs-lookup"><span data-stu-id="7853f-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="7853f-122">擴充功能需要指令碼位置 (Azure 儲存體或其他具有有效 URL 的位置)，以及可供執行的命令。</span><span class="sxs-lookup"><span data-stu-id="7853f-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="7853f-123">如果使用 Azure 儲存體做為指令碼來源，則需要 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="7853f-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="7853f-124">這些項目應被視為敏感性資料，並在擴充功能保護的設定組態中指定。</span><span class="sxs-lookup"><span data-stu-id="7853f-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="7853f-125">Azure VM 擴充功能保護的設定資料會經過加密，只會在目標虛擬機器上解密。</span><span class="sxs-lookup"><span data-stu-id="7853f-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="7853f-126">屬性值</span><span class="sxs-lookup"><span data-stu-id="7853f-126">Property values</span></span>

| <span data-ttu-id="7853f-127">名稱</span><span class="sxs-lookup"><span data-stu-id="7853f-127">Name</span></span> | <span data-ttu-id="7853f-128">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="7853f-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="7853f-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7853f-129">apiVersion</span></span> | <span data-ttu-id="7853f-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="7853f-130">2015-06-15</span></span> |
| <span data-ttu-id="7853f-131">publisher</span><span class="sxs-lookup"><span data-stu-id="7853f-131">publisher</span></span> | <span data-ttu-id="7853f-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7853f-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="7853f-133">擴充功能</span><span class="sxs-lookup"><span data-stu-id="7853f-133">extension</span></span> | <span data-ttu-id="7853f-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="7853f-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="7853f-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="7853f-135">typeHandlerVersion</span></span> | <span data-ttu-id="7853f-136">1.8</span><span class="sxs-lookup"><span data-stu-id="7853f-136">1.8</span></span> |
| <span data-ttu-id="7853f-137">fileUris (例如)</span><span class="sxs-lookup"><span data-stu-id="7853f-137">fileUris (e.g)</span></span> | <span data-ttu-id="7853f-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="7853f-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="7853f-139">commandToExecute (例如)</span><span class="sxs-lookup"><span data-stu-id="7853f-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="7853f-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="7853f-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="7853f-141">範本部署</span><span class="sxs-lookup"><span data-stu-id="7853f-141">Template deployment</span></span>

<span data-ttu-id="7853f-142">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7853f-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="7853f-143">上一節詳述的 JSON 結構描述可以用於 Azure Resource Manager 範本，以在 Azure Resource Manager 範本部署期間執行自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7853f-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="7853f-144">在 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows) 可以找到包含自訂指令碼擴充功能的範例範本。</span><span class="sxs-lookup"><span data-stu-id="7853f-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="7853f-145">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="7853f-145">PowerShell deployment</span></span>

<span data-ttu-id="7853f-146">`Set-AzureVMCustomScriptExtension` 命令可以用來將自訂指令碼擴充功能新增至現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7853f-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="7853f-147">如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。</span><span class="sxs-lookup"><span data-stu-id="7853f-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="7853f-148">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="7853f-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="7853f-149">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7853f-149">Troubleshoot</span></span>

<span data-ttu-id="7853f-150">使用 Azure PowerShell 模組，就可以從 Azure 入口網站擷取有關擴充功能部署狀態的資料。</span><span class="sxs-lookup"><span data-stu-id="7853f-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="7853f-151">若要查看指定 VM 的擴充功能部署狀態，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="7853f-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="7853f-152">擴充功能執行輸出會記錄至目標虛擬機器上下列目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7853f-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="7853f-153">指令碼本身會下載到目標虛擬機器上的下列目錄。</span><span class="sxs-lookup"><span data-stu-id="7853f-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="7853f-154">支援</span><span class="sxs-lookup"><span data-stu-id="7853f-154">Support</span></span>

<span data-ttu-id="7853f-155">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/en-us/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="7853f-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="7853f-156">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="7853f-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="7853f-157">請移至 [Azure 支援網站](https://azure.microsoft.com/en-us/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="7853f-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="7853f-158">如需使用 Azure 支援的資訊，請參閱 [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="7853f-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>