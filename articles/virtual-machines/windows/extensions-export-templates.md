---
title: "包含 VM 擴充功能的 Azure 資源群組 aaaExporting |Microsoft 文件"
description: "匯出包含虛擬機器擴充功能的 Resource Manager 範本。"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="3c716-103">匯出包含 VM 擴充功能的資源群組</span><span class="sxs-lookup"><span data-stu-id="3c716-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="3c716-104">Azure 資源群組可以匯出到之後會重新部署的新 Resource Manager 範本中。</span><span class="sxs-lookup"><span data-stu-id="3c716-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="3c716-105">hello 匯出程序會解譯現有的資源，並建立 Resource Manager 範本的部署時導致類似的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3c716-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="3c716-106">使用 hello 資源群組匯出選項，針對包含虛擬機器擴充功能的資源群組時，數個項目需要 toobe 視為例如擴充功能的相容性，而且保護設定。</span><span class="sxs-lookup"><span data-stu-id="3c716-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="3c716-107">關於虛擬機器擴充功能，包括一份 hello 資源群組匯出程序的運作方式本文件詳述支援的延伸模組，並以處理的詳細資訊保護的資料。</span><span class="sxs-lookup"><span data-stu-id="3c716-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="3c716-108">支援的虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="3c716-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="3c716-109">有許多虛擬機器擴充功能可以使用。</span><span class="sxs-lookup"><span data-stu-id="3c716-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="3c716-110">並非所有擴充功能可以匯出成資源管理員範本使用 hello"自動化指令碼 」 功能。</span><span class="sxs-lookup"><span data-stu-id="3c716-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="3c716-111">如果不支援虛擬機器擴充功能，它會需要 toobe 手動放回 hello 匯出的範本。</span><span class="sxs-lookup"><span data-stu-id="3c716-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="3c716-112">hello 下列延伸項目可以匯出與 hello 自動化指令碼功能。</span><span class="sxs-lookup"><span data-stu-id="3c716-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="3c716-113">分機</span><span class="sxs-lookup"><span data-stu-id="3c716-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="3c716-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="3c716-114">Acronis Backup</span></span> | <span data-ttu-id="3c716-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="3c716-115">Datadog Windows Agent</span></span> | <span data-ttu-id="3c716-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-116">OS Patching For Linux</span></span> | <span data-ttu-id="3c716-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="3c716-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-118">Acronis Backup Linux</span></span> | <span data-ttu-id="3c716-119">Docker 延伸模組</span><span class="sxs-lookup"><span data-stu-id="3c716-119">Docker Extension</span></span> | <span data-ttu-id="3c716-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="3c716-120">Puppet Agent</span></span> |
| <span data-ttu-id="3c716-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="3c716-121">Bg Info</span></span> | <span data-ttu-id="3c716-122">DSC 延伸模組</span><span class="sxs-lookup"><span data-stu-id="3c716-122">DSC Extension</span></span> | <span data-ttu-id="3c716-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="3c716-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="3c716-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="3c716-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-125">Dynatrace Linux</span></span> | <span data-ttu-id="3c716-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="3c716-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="3c716-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="3c716-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="3c716-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="3c716-128">Dynatrace Windows</span></span> | <span data-ttu-id="3c716-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="3c716-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="3c716-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="3c716-130">Chef Client</span></span> | <span data-ttu-id="3c716-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="3c716-131">HPE Security Application Defender</span></span> | <span data-ttu-id="3c716-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="3c716-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="3c716-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="3c716-133">Custom Script</span></span> | <span data-ttu-id="3c716-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="3c716-134">IaaS Antimalware</span></span> | <span data-ttu-id="3c716-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="3c716-136">自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="3c716-136">Custom Script Extension</span></span> | <span data-ttu-id="3c716-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="3c716-137">IaaS Diagnostics</span></span> | <span data-ttu-id="3c716-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-138">VM Access For Linux</span></span> |
| <span data-ttu-id="3c716-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-139">Custom Script for Linux</span></span> | <span data-ttu-id="3c716-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="3c716-140">Linux Chef Client</span></span> | <span data-ttu-id="3c716-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="3c716-141">VM Access For Linux</span></span> |
| <span data-ttu-id="3c716-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="3c716-142">Datadog Linux Agent</span></span> | <span data-ttu-id="3c716-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="3c716-143">Linux Diagnostic</span></span> | <span data-ttu-id="3c716-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="3c716-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="3c716-145">匯出 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="3c716-145">Export hello Resource Group</span></span>

<span data-ttu-id="3c716-146">tooexport 成可重複使用範本，請完成下列步驟的 hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="3c716-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="3c716-147">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3c716-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="3c716-148">在 hello 中樞功能表中，按一下 資源群組</span><span class="sxs-lookup"><span data-stu-id="3c716-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="3c716-149">從 hello 清單中選取 hello 目標資源群組</span><span class="sxs-lookup"><span data-stu-id="3c716-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="3c716-150">在 hello 資源群組刀鋒視窗中，按一下 自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="3c716-150">In hello Resource Group blade, click Automation Script</span></span>

![匯出範本](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="3c716-152">hello Azure Resource Manager 不僅指令碼會產生資源管理員範本、 參數檔案，以及數個範例部署指令碼，例如 PowerShell 和 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3c716-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="3c716-153">此時，hello 匯出的範本可以使用下載 hello 下載 按鈕，為新範本 toohello 範本程式庫，加入或重新部署使用 hello 部署按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c716-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="3c716-154">設定受保護的設定</span><span class="sxs-lookup"><span data-stu-id="3c716-154">Configure protected settings</span></span>

<span data-ttu-id="3c716-155">許多 Azure 虛擬機器擴充功能都包含受保護的設定組態，以加密敏感性資料，例如認證及組態字串。</span><span class="sxs-lookup"><span data-stu-id="3c716-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="3c716-156">受保護的設定不會匯出與 hello 自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="3c716-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="3c716-157">如果需要，受保護的設定需要重新插入 hello toobe 匯出樣板化。</span><span class="sxs-lookup"><span data-stu-id="3c716-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="3c716-158">步驟 1 - 移除範本參數</span><span class="sxs-lookup"><span data-stu-id="3c716-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="3c716-159">Hello 匯出資源群組時，單一的樣板參數建立 tooprovide 時值 toohello 匯出受保護的設定。</span><span class="sxs-lookup"><span data-stu-id="3c716-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="3c716-160">您可移除此參數。</span><span class="sxs-lookup"><span data-stu-id="3c716-160">This parameter can be removed.</span></span> <span data-ttu-id="3c716-161">tooremove hello 參數，查看 hello 參數清單，並刪除 hello 參數，看起來類似 toothis JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="3c716-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="3c716-162">步驟 2 - 取得受保護的設定屬性</span><span class="sxs-lookup"><span data-stu-id="3c716-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="3c716-163">因為每個受保護的設定有一組必要的屬性，這些屬性的清單需要 toobe 蒐集。</span><span class="sxs-lookup"><span data-stu-id="3c716-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="3c716-164">Hello 受保護的設定組態的每個參數可以在 hello [GitHub 上的 Azure 資源管理員結構描述](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json)。</span><span class="sxs-lookup"><span data-stu-id="3c716-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="3c716-165">這個結構描述僅包含 hello hello 延伸模組這份文件 hello 概觀 > 中列出的參數集。</span><span class="sxs-lookup"><span data-stu-id="3c716-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="3c716-166">從內 hello 結構描述儲存機制中，搜尋所需的 hello 延伸模組，此範例中`IaaSDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="3c716-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="3c716-167">一次 hello 延伸`protectedSettings`已找到物件，請注意，每個參數。</span><span class="sxs-lookup"><span data-stu-id="3c716-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="3c716-168">在 hello 範例中的 hello`IaasDiagnostic`延伸模組，hello 需要參數`storageAccountName`， `storageAccountKey`，和`storageAccountEndPoint`。</span><span class="sxs-lookup"><span data-stu-id="3c716-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="3c716-169">步驟 3-重新建立受保護的 hello 組態</span><span class="sxs-lookup"><span data-stu-id="3c716-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="3c716-170">Hello 匯出的範本，搜尋`protectedSettings`並取代，其中包含所需的 hello 延伸模組參數和值，針對每個新的 hello 匯出受保護的設定物件。</span><span class="sxs-lookup"><span data-stu-id="3c716-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="3c716-171">在 hello 範例中的 hello`IaasDiagnostic`延伸模組，hello 新的受保護的設定組態看起來會像下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c716-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="3c716-172">hello 最終的擴充資源看起來類似 toohello 下列 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="3c716-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="3c716-173">如果使用範本參數 tooprovide 屬性值，這些會需要建立 toobe。</span><span class="sxs-lookup"><span data-stu-id="3c716-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="3c716-174">當受保護的設定值，請建立範本參數，請確定 toouse hello`SecureString`參數型別，以便保護機密值。</span><span class="sxs-lookup"><span data-stu-id="3c716-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="3c716-175">如需使用參數的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3c716-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3c716-176">在 hello 範例中的 hello`IaasDiagnostic`延伸模組，會在 hello Resource Manager 範本 hello 參數 區段中建立 hello 下列參數。</span><span class="sxs-lookup"><span data-stu-id="3c716-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="3c716-177">此時，您可以使用範本部署的任何方法來部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3c716-177">At this point, hello template can be deployed using any template deployment method.</span></span>
