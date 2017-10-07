---
title: "在 Azure 中的 Linux Vm 上的 aaaRun 自訂指令碼 |Microsoft 文件"
description: "使用 hello 自訂指令碼擴充自動化 Linux VM 組態工作"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="735bf-103">使用 Azure 自訂指令碼擴充的 hello 與 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="735bf-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="735bf-104">hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="735bf-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="735bf-105">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="735bf-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="735bf-106">可以下載自 Azure 儲存體或其他可存取網際網路的位置，或提供 toohello 延伸模組執行階段指令碼。</span><span class="sxs-lookup"><span data-stu-id="735bf-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="735bf-107">hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。</span><span class="sxs-lookup"><span data-stu-id="735bf-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="735bf-108">如何 toouse hello 自訂指令碼擴充，從本文件詳述 hello Azure CLI 和 Azure 資源管理員範本，以及詳細的疑難排解步驟，在 Linux 系統上。</span><span class="sxs-lookup"><span data-stu-id="735bf-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="735bf-109">擴充功能組態</span><span class="sxs-lookup"><span data-stu-id="735bf-109">Extension Configuration</span></span>
<span data-ttu-id="735bf-110">hello 自訂指令碼延伸模組組態會指定指令碼位置和執行 hello 命令 toobe 等。</span><span class="sxs-lookup"><span data-stu-id="735bf-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="735bf-111">此組態可以儲存在組態檔中指定 hello 命令列上，或在 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="735bf-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="735bf-112">可以在受保護組態中，其加密，並只能解密 hello 虛擬機器內儲存機密資料。</span><span class="sxs-lookup"><span data-stu-id="735bf-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="735bf-113">hello 受保護的組態時，hello 執行命令包含機密資料，例如密碼。</span><span class="sxs-lookup"><span data-stu-id="735bf-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="735bf-114">公用組態</span><span class="sxs-lookup"><span data-stu-id="735bf-114">Public Configuration</span></span>
<span data-ttu-id="735bf-115">結構描述：</span><span class="sxs-lookup"><span data-stu-id="735bf-115">Schema:</span></span>

<span data-ttu-id="735bf-116">**注意** - 屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="735bf-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="735bf-117">如下所示 tooavoid 部署問題，請使用 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="735bf-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="735bf-118">**commandToExecute**: (需要，string) hello 進入點指令碼 tooexecute</span><span class="sxs-lookup"><span data-stu-id="735bf-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="735bf-119">**fileUris**: （選擇性，字串陣列），檔案 toobe hello Url 的下載。</span><span class="sxs-lookup"><span data-stu-id="735bf-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="735bf-120">**時間戳記**（選擇性，整數） 使用此欄位只有 tootrigger hello 指令碼的重新執行，藉由變更這個欄位的值。</span><span class="sxs-lookup"><span data-stu-id="735bf-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="735bf-121">受保護的組態</span><span class="sxs-lookup"><span data-stu-id="735bf-121">Protected Configuration</span></span>
<span data-ttu-id="735bf-122">結構描述：</span><span class="sxs-lookup"><span data-stu-id="735bf-122">Schema:</span></span>

<span data-ttu-id="735bf-123">**注意** - 屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="735bf-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="735bf-124">如下所示 tooavoid 部署問題，請使用 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="735bf-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="735bf-125">**commandToExecute**: (選擇性，string) hello 進入點指令碼 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="735bf-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="735bf-126">如果您的命令包含機密資料 (例如密碼)，請改用此欄位。</span><span class="sxs-lookup"><span data-stu-id="735bf-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="735bf-127">**storageAccountName**: (選擇性，string) hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="735bf-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="735bf-128">如果您指定儲存體證明資料，則所有 fileUri 都必須是 Azure Blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="735bf-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="735bf-129">**storageAccountKey**: (選擇性，string) hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="735bf-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="735bf-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="735bf-130">Azure CLI</span></span>
<span data-ttu-id="735bf-131">當使用 hello Azure CLI toorun hello 自訂指令碼擴充，建立組態檔或檔案，其中包含在最小 hello 檔案 uri，以及 hello 指令碼執行命令。</span><span class="sxs-lookup"><span data-stu-id="735bf-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="735bf-132">選擇性地 hello 設定可以 hello 命令中指定，以 JSON 格式字串。</span><span class="sxs-lookup"><span data-stu-id="735bf-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="735bf-133">這可讓 hello 組態 toobe 指定在執行期間並不使用個別的組態檔案。</span><span class="sxs-lookup"><span data-stu-id="735bf-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="735bf-134">Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="735bf-134">Azure CLI Examples</span></span>

<span data-ttu-id="735bf-135">**範例 1** - 含指令檔的公用組態。</span><span class="sxs-lookup"><span data-stu-id="735bf-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="735bf-136">Azure CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="735bf-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="735bf-137">**範例 2** - 不含指令檔的公用組態。</span><span class="sxs-lookup"><span data-stu-id="735bf-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="735bf-138">Azure CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="735bf-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="735bf-139">**範例 3** -公用組態檔是使用的 toospecify hello 指令碼檔案的 URI，且受保護的組態檔是使用的 toospecify hello 命令 toobe 執行。</span><span class="sxs-lookup"><span data-stu-id="735bf-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="735bf-140">公用組態檔：</span><span class="sxs-lookup"><span data-stu-id="735bf-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="735bf-141">受保護的組態檔：</span><span class="sxs-lookup"><span data-stu-id="735bf-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="735bf-142">Azure CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="735bf-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="735bf-143">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="735bf-143">Resource Manager Template</span></span>
<span data-ttu-id="735bf-144">可以在虛擬機器部署時間使用資源管理員範本執行 hello Azure 自訂指令碼擴充。</span><span class="sxs-lookup"><span data-stu-id="735bf-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="735bf-145">因此，toodo 中加入格式正確的 JSON toohello 部署範本。</span><span class="sxs-lookup"><span data-stu-id="735bf-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="735bf-146">Resource Manager 範例</span><span class="sxs-lookup"><span data-stu-id="735bf-146">Resource Manager Examples</span></span>
<span data-ttu-id="735bf-147">**範例 1** - 公用組態。</span><span class="sxs-lookup"><span data-stu-id="735bf-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="735bf-148">**範例 2** - 受保護組態中的執行命令。</span><span class="sxs-lookup"><span data-stu-id="735bf-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="735bf-149">請參閱 hello.Net Core Music Store 示範如需完整的範例-[音樂存放區示範](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)。</span><span class="sxs-lookup"><span data-stu-id="735bf-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="735bf-150">疑難排解</span><span class="sxs-lookup"><span data-stu-id="735bf-150">Troubleshooting</span></span>
<span data-ttu-id="735bf-151">Hello 自訂指令碼延伸執行時，hello 指令碼建立，或下載到目錄類似 toohello，下列範例。</span><span class="sxs-lookup"><span data-stu-id="735bf-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="735bf-152">hello 命令輸出也會儲存到此目錄中`stdout`和`stderr`檔案。</span><span class="sxs-lookup"><span data-stu-id="735bf-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="735bf-153">hello Azure 指令碼延伸模組會產生記錄檔，可以在這裡找到。</span><span class="sxs-lookup"><span data-stu-id="735bf-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="735bf-154">hello hello 自訂指令碼延伸執行狀態也可以擷取與 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="735bf-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="735bf-155">hello 輸出看起來類似下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="735bf-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="735bf-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="735bf-156">Next Steps</span></span>
<span data-ttu-id="735bf-157">如需有關其他「VM 指令碼擴充功能」的資訊，請參閱 [適用於 Linux 的 Azure 指令碼擴充功能概觀](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="735bf-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

