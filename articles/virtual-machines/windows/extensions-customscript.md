---
title: "aaaAzure 自訂指令碼延伸的視窗 |Microsoft 文件"
description: "使用 hello 自訂指令碼擴充自動化 Windows VM 組態工作"
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
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="11a49-103">Windows 的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="11a49-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="11a49-104">hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="11a49-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="11a49-105">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="11a49-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="11a49-106">可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="11a49-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="11a49-107">hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。</span><span class="sxs-lookup"><span data-stu-id="11a49-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="11a49-108">這份文件詳細說明如何使用自訂指令碼擴充 toouse hello hello Azure PowerShell 模組、 Azure 資源管理員範本及疑難排解在 Windows 系統上的步驟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="11a49-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11a49-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="11a49-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="11a49-110">作業系統</span><span class="sxs-lookup"><span data-stu-id="11a49-110">Operating System</span></span>

<span data-ttu-id="11a49-111">hello 自訂指令碼擴充的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。</span><span class="sxs-lookup"><span data-stu-id="11a49-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="11a49-112">指令碼位置</span><span class="sxs-lookup"><span data-stu-id="11a49-112">Script Location</span></span>

<span data-ttu-id="11a49-113">hello 指令碼需要 toobe 儲存在 Azure Blob 儲存體或可透過有效的 URL 存取的任何其他位置。</span><span class="sxs-lookup"><span data-stu-id="11a49-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="11a49-114">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="11a49-114">Internet Connectivity</span></span>

<span data-ttu-id="11a49-115">hello 自訂指令碼擴充功能的 Windows 需要該 hello 目標虛擬機器已連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="11a49-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="11a49-116">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="11a49-116">Extension schema</span></span>

<span data-ttu-id="11a49-117">hello 下列 JSON 顯示 hello hello 自訂指令碼擴充的結構描述。</span><span class="sxs-lookup"><span data-stu-id="11a49-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="11a49-118">hello 延伸模組需要的指令碼位置 （Azure 儲存體或其他位置，以有效的 URL） 和命令 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="11a49-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="11a49-119">如果使用 Azure 儲存體做為 hello 指令碼來源，Azure 儲存體帳戶名稱和帳戶金鑰需要。</span><span class="sxs-lookup"><span data-stu-id="11a49-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="11a49-120">這些項目應該視為機密資料，並且在 hello 延伸的受保護的設定組態中指定。</span><span class="sxs-lookup"><span data-stu-id="11a49-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="11a49-121">Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="11a49-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="11a49-122">屬性值</span><span class="sxs-lookup"><span data-stu-id="11a49-122">Property values</span></span>

| <span data-ttu-id="11a49-123">名稱</span><span class="sxs-lookup"><span data-stu-id="11a49-123">Name</span></span> | <span data-ttu-id="11a49-124">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="11a49-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="11a49-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11a49-125">apiVersion</span></span> | <span data-ttu-id="11a49-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="11a49-126">2015-06-15</span></span> |
| <span data-ttu-id="11a49-127">publisher</span><span class="sxs-lookup"><span data-stu-id="11a49-127">publisher</span></span> | <span data-ttu-id="11a49-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="11a49-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="11a49-129">類型</span><span class="sxs-lookup"><span data-stu-id="11a49-129">type</span></span> | <span data-ttu-id="11a49-130">擴充功能</span><span class="sxs-lookup"><span data-stu-id="11a49-130">extensions</span></span> |
| <span data-ttu-id="11a49-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="11a49-131">typeHandlerVersion</span></span> | <span data-ttu-id="11a49-132">1.9</span><span class="sxs-lookup"><span data-stu-id="11a49-132">1.9</span></span> |
| <span data-ttu-id="11a49-133">fileUris (例如)</span><span class="sxs-lookup"><span data-stu-id="11a49-133">fileUris (e.g)</span></span> | <span data-ttu-id="11a49-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="11a49-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="11a49-135">commandToExecute (例如)</span><span class="sxs-lookup"><span data-stu-id="11a49-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="11a49-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="11a49-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="11a49-137">storageAccountName (例如)</span><span class="sxs-lookup"><span data-stu-id="11a49-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="11a49-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="11a49-138">examplestorageacct</span></span> |
| <span data-ttu-id="11a49-139">storageAccountKey (例如)</span><span class="sxs-lookup"><span data-stu-id="11a49-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="11a49-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="11a49-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="11a49-141">**注意** - 屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="11a49-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="11a49-142">如上 tooavoid 部署問題，請使用 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="11a49-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="11a49-143">範本部署</span><span class="sxs-lookup"><span data-stu-id="11a49-143">Template deployment</span></span>

<span data-ttu-id="11a49-144">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="11a49-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="11a49-145">hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 自訂指令碼擴充，在 Azure 資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="11a49-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="11a49-146">包含自訂指令碼擴充功能可以在這裡，找到的 hello 的範例範本[GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="11a49-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="11a49-147">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="11a49-147">PowerShell deployment</span></span>

<span data-ttu-id="11a49-148">hello`Set-AzureRmVMCustomScriptExtension`命令可以是使用的 tooadd hello 自訂指令碼延伸 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="11a49-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="11a49-149">如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。</span><span class="sxs-lookup"><span data-stu-id="11a49-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="11a49-150">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="11a49-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="11a49-151">疑難排解</span><span class="sxs-lookup"><span data-stu-id="11a49-151">Troubleshoot</span></span>

<span data-ttu-id="11a49-152">從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="11a49-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="11a49-153">擴充功能，針對指定的 VM，並執行下列命令的 hello toosee hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="11a49-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="11a49-154">延伸模組執行輸出 hello 下找到的記錄的 toofiles 之後，目錄 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="11a49-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="11a49-155">hello 指定成 hello hello 目標虛擬機器上下列目錄下載檔案。</span><span class="sxs-lookup"><span data-stu-id="11a49-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="11a49-156">其中`<n>`是可能會改變 hello 延伸模組的執行之間的十進位整數。</span><span class="sxs-lookup"><span data-stu-id="11a49-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="11a49-157">hello`1.*`值符合 hello 實際目前`typeHandlerVersion`hello 延伸的值。</span><span class="sxs-lookup"><span data-stu-id="11a49-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="11a49-158">例如，可能是 hello 實際目錄`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`。</span><span class="sxs-lookup"><span data-stu-id="11a49-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="11a49-159">當執行 hello`commandToExecute`命令 hello 延伸模組會將這個目錄 (例如`...\Downloads\2`) 為 hello 目前工作目錄。</span><span class="sxs-lookup"><span data-stu-id="11a49-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="11a49-160">這可讓 hello 使用的相對路徑 toolocate hello 檔案下載透過 hello`fileURIs`屬性。</span><span class="sxs-lookup"><span data-stu-id="11a49-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="11a49-161">請參閱 hello 表中的範例。</span><span class="sxs-lookup"><span data-stu-id="11a49-161">See hello table below for examples.</span></span>

<span data-ttu-id="11a49-162">Hello 絕對下載路徑可能會隨著時間，因為它是較佳的相對的指令碼檔案路徑的 hello tooopt`commandToExecute`盡可能字串。</span><span class="sxs-lookup"><span data-stu-id="11a49-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="11a49-163">例如：</span><span class="sxs-lookup"><span data-stu-id="11a49-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="11a49-164">透過 hello 下載路徑資訊之後，檔案會保留第一個 URI 區段 hello`fileUris`屬性清單。</span><span class="sxs-lookup"><span data-stu-id="11a49-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="11a49-165">Hello 下表所示，將下載的檔案對應到下載子目錄 tooreflect hello 結構 hello`fileUris`值。</span><span class="sxs-lookup"><span data-stu-id="11a49-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="11a49-166">下載檔案的範例</span><span class="sxs-lookup"><span data-stu-id="11a49-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="11a49-167">fileUris 中的 URI</span><span class="sxs-lookup"><span data-stu-id="11a49-167">URI in fileUris</span></span> | <span data-ttu-id="11a49-168">相對下載位置</span><span class="sxs-lookup"><span data-stu-id="11a49-168">Relative downloaded location</span></span> | <span data-ttu-id="11a49-169">絕對下載位置 *</span><span class="sxs-lookup"><span data-stu-id="11a49-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="11a49-170">\*做為上述 hello 絕對目錄路徑將會變更 hello 存留期的 hello VM，但不是會在單一 hello CustomScript 延伸模組的執行。</span><span class="sxs-lookup"><span data-stu-id="11a49-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="11a49-171">支援</span><span class="sxs-lookup"><span data-stu-id="11a49-171">Support</span></span>

<span data-ttu-id="11a49-172">如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello hello [MSDN Azure 和堆疊溢位論壇] 上的 Azure 專家 (https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="11a49-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="11a49-173">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="11a49-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="11a49-174">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="11a49-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="11a49-175">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="11a49-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
