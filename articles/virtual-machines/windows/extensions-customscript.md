---
title: "Windows 的 Azure 自訂指令碼延伸模組 | Microsoft Docs"
description: "使用「自訂指令碼擴充功能」來自動執行 Windows VM 組態工作"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: a6f417ea6575b81258998ae3b31c10e9df59b603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="bedbe-103">Windows 的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="bedbe-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="bedbe-104">「自訂指令碼擴充功能」會在 Azure 虛擬機器上下載並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="bedbe-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="bedbe-105">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="bedbe-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="bedbe-106">您可以從 Azure 儲存體或 GitHub 下載指令碼，或是在擴充功能執行階段將指令碼提供給 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bedbe-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="bedbe-107">「自訂指令碼擴充功能」會與 Azure Resource Manager 範本整合，您也可以使用 Azure CLI、PowerShell、Azure 入口網站或「Azure 虛擬機器 REST API」來執行它。</span><span class="sxs-lookup"><span data-stu-id="bedbe-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="bedbe-108">本文件詳細說明如何透過 Azure PowerShell 模組、Azure Resource Manager 範本使用自訂指令碼擴充功能，同時也詳細說明 Windows 系統上的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="bedbe-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bedbe-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="bedbe-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="bedbe-110">作業系統</span><span class="sxs-lookup"><span data-stu-id="bedbe-110">Operating System</span></span>

<span data-ttu-id="bedbe-111">可以對 Windows Server 2008 R2、2012、2012 R2 和 2016 版執行適用於 Windows 的自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="bedbe-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="bedbe-112">指令碼位置</span><span class="sxs-lookup"><span data-stu-id="bedbe-112">Script Location</span></span>

<span data-ttu-id="bedbe-113">指令碼必須儲存在 Azure Blob 儲存體或任何可透過有效 URL 存取的其他位置。</span><span class="sxs-lookup"><span data-stu-id="bedbe-113">The script needs to be stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="bedbe-114">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="bedbe-114">Internet Connectivity</span></span>

<span data-ttu-id="bedbe-115">適用於 Windows 的自訂指令碼擴充功能會要求目標虛擬機器連接到網際網路。</span><span class="sxs-lookup"><span data-stu-id="bedbe-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="bedbe-116">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="bedbe-116">Extension schema</span></span>

<span data-ttu-id="bedbe-117">下列 JSON 顯示自訂指令碼擴充功能的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bedbe-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="bedbe-118">擴充功能需要指令碼位置 (Azure 儲存體或其他具有有效 URL 的位置)，以及可供執行的命令。</span><span class="sxs-lookup"><span data-stu-id="bedbe-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="bedbe-119">如果使用 Azure 儲存體做為指令碼來源，則需要 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="bedbe-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="bedbe-120">這些項目應被視為敏感性資料，並在擴充功能保護的設定組態中指定。</span><span class="sxs-lookup"><span data-stu-id="bedbe-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="bedbe-121">Azure VM 擴充功能保護的設定資料會經過加密，只會在目標虛擬機器上解密。</span><span class="sxs-lookup"><span data-stu-id="bedbe-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="bedbe-122">屬性值</span><span class="sxs-lookup"><span data-stu-id="bedbe-122">Property values</span></span>

| <span data-ttu-id="bedbe-123">名稱</span><span class="sxs-lookup"><span data-stu-id="bedbe-123">Name</span></span> | <span data-ttu-id="bedbe-124">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="bedbe-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="bedbe-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="bedbe-125">apiVersion</span></span> | <span data-ttu-id="bedbe-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="bedbe-126">2015-06-15</span></span> |
| <span data-ttu-id="bedbe-127">publisher</span><span class="sxs-lookup"><span data-stu-id="bedbe-127">publisher</span></span> | <span data-ttu-id="bedbe-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="bedbe-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="bedbe-129">類型</span><span class="sxs-lookup"><span data-stu-id="bedbe-129">type</span></span> | <span data-ttu-id="bedbe-130">擴充功能</span><span class="sxs-lookup"><span data-stu-id="bedbe-130">extensions</span></span> |
| <span data-ttu-id="bedbe-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="bedbe-131">typeHandlerVersion</span></span> | <span data-ttu-id="bedbe-132">1.9</span><span class="sxs-lookup"><span data-stu-id="bedbe-132">1.9</span></span> |
| <span data-ttu-id="bedbe-133">fileUris (例如)</span><span class="sxs-lookup"><span data-stu-id="bedbe-133">fileUris (e.g)</span></span> | <span data-ttu-id="bedbe-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="bedbe-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="bedbe-135">commandToExecute (例如)</span><span class="sxs-lookup"><span data-stu-id="bedbe-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="bedbe-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="bedbe-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="bedbe-137">storageAccountName (例如)</span><span class="sxs-lookup"><span data-stu-id="bedbe-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="bedbe-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="bedbe-138">examplestorageacct</span></span> |
| <span data-ttu-id="bedbe-139">storageAccountKey (例如)</span><span class="sxs-lookup"><span data-stu-id="bedbe-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="bedbe-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="bedbe-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="bedbe-141">**注意** - 屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="bedbe-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="bedbe-142">使用如上所示的名稱以避免發生部署問題。</span><span class="sxs-lookup"><span data-stu-id="bedbe-142">Use the names as seen above to avoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="bedbe-143">範本部署</span><span class="sxs-lookup"><span data-stu-id="bedbe-143">Template deployment</span></span>

<span data-ttu-id="bedbe-144">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="bedbe-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="bedbe-145">上一節詳述的 JSON 結構描述可以用於 Azure Resource Manager 範本，以在 Azure Resource Manager 範本部署期間執行自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="bedbe-145">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="bedbe-146">在 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows) 可以找到包含自訂指令碼擴充功能的範例範本。</span><span class="sxs-lookup"><span data-stu-id="bedbe-146">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="bedbe-147">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="bedbe-147">PowerShell deployment</span></span>

<span data-ttu-id="bedbe-148">`Set-AzureRmVMCustomScriptExtension` 命令可以用來將自訂指令碼擴充功能新增至現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bedbe-148">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="bedbe-149">如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。</span><span class="sxs-lookup"><span data-stu-id="bedbe-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="bedbe-150">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="bedbe-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="bedbe-151">疑難排解</span><span class="sxs-lookup"><span data-stu-id="bedbe-151">Troubleshoot</span></span>

<span data-ttu-id="bedbe-152">使用 Azure PowerShell 模組，就可以從 Azure 入口網站擷取有關擴充功能部署狀態的資料。</span><span class="sxs-lookup"><span data-stu-id="bedbe-152">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="bedbe-153">若要查看指定 VM 的擴充功能部署狀態，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="bedbe-153">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="bedbe-154">擴充功能執行輸出會記錄至目標虛擬機器上下列目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="bedbe-154">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="bedbe-155">指定檔案會下載至目標虛擬機器上的下列目錄之中。</span><span class="sxs-lookup"><span data-stu-id="bedbe-155">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="bedbe-156">其中 `<n>` 是十進位整數，可能會在擴充功能的執行之間變更。</span><span class="sxs-lookup"><span data-stu-id="bedbe-156">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="bedbe-157">`1.*` 值符合擴充功能目前實際的 `typeHandlerVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="bedbe-157">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="bedbe-158">例如，實際的目錄可能是 `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`。</span><span class="sxs-lookup"><span data-stu-id="bedbe-158">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="bedbe-159">執行 `commandToExecute` 命令時，擴充功能會將此目錄 (例如 `...\Downloads\2`) 設定為目前的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="bedbe-159">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="bedbe-160">這可讓您使用相對路徑找出透過 `fileURIs` 屬性下載的檔案位置。</span><span class="sxs-lookup"><span data-stu-id="bedbe-160">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="bedbe-161">如需範例，請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="bedbe-161">See the table below for examples.</span></span>

<span data-ttu-id="bedbe-162">由於絕對下載路徑會隨時間而改變，最好盡可能在 `commandToExecute` 字串中選擇相對的指令碼/檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="bedbe-162">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="bedbe-163">例如：</span><span class="sxs-lookup"><span data-stu-id="bedbe-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="bedbe-164">第一個 URI 區段後的路徑資訊會為透過 `fileUris` 屬性清單下載的檔案而保留。</span><span class="sxs-lookup"><span data-stu-id="bedbe-164">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="bedbe-165">如下表所示，下載的檔案會對應到下載的子目錄，以反映 `fileUris` 值結構。</span><span class="sxs-lookup"><span data-stu-id="bedbe-165">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="bedbe-166">下載檔案的範例</span><span class="sxs-lookup"><span data-stu-id="bedbe-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="bedbe-167">fileUris 中的 URI</span><span class="sxs-lookup"><span data-stu-id="bedbe-167">URI in fileUris</span></span> | <span data-ttu-id="bedbe-168">相對下載位置</span><span class="sxs-lookup"><span data-stu-id="bedbe-168">Relative downloaded location</span></span> | <span data-ttu-id="bedbe-169">絕對下載位置 *</span><span class="sxs-lookup"><span data-stu-id="bedbe-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="bedbe-170">\* 如同上述，絕對目錄路徑會隨 VM 生命週期而變更，但不會在 CustomScript 擴充的單次執行期間。</span><span class="sxs-lookup"><span data-stu-id="bedbe-170">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="bedbe-171">支援</span><span class="sxs-lookup"><span data-stu-id="bedbe-171">Support</span></span>

<span data-ttu-id="bedbe-172">如果關於本文有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇] 上的 Azure 專家 (https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="bedbe-172">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="bedbe-173">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="bedbe-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bedbe-174">請移至 [Azure 支援網站](https://azure.microsoft.com/en-us/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="bedbe-174">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="bedbe-175">如需使用 Azure 支援的資訊，請參閱 [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="bedbe-175">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
