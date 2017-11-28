---
title: "aaaOMS 適用於 Windows Azure 虛擬機器擴充功能 |Microsoft 文件"
description: "部署 Windows 虛擬機器使用虛擬機器擴充功能上的 hello OMS 代理程式。"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="81124-103">適用於 Windows 的 OMS 虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="81124-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="81124-104">Operations Management Suite (OMS) 可提供雲端和內部部署資產的監視、警示和警示補救功能。</span><span class="sxs-lookup"><span data-stu-id="81124-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="81124-105">發行 hello OMS Agent for Windows 的虛擬機器擴充功能和 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="81124-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="81124-106">hello 延伸模組會安裝 Azure 的虛擬機器上的 hello OMS 代理程式，並註冊到現有的 OMS 工作區的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81124-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="81124-107">此文件詳細資料 hello 支援平台、 組態和部署選項 hello OMS 虛擬機器擴充功能的 Windows。</span><span class="sxs-lookup"><span data-stu-id="81124-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81124-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="81124-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="81124-109">作業系統</span><span class="sxs-lookup"><span data-stu-id="81124-109">Operating system</span></span>
<span data-ttu-id="81124-110">hello OMS Agent 擴充功能的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。</span><span class="sxs-lookup"><span data-stu-id="81124-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="81124-111">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="81124-111">Internet connectivity</span></span>
<span data-ttu-id="81124-112">hello 適用於 Windows 的 OMS 代理程式延伸模組需要該 hello 目標虛擬機器已連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="81124-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="81124-113">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="81124-113">Extension schema</span></span>

<span data-ttu-id="81124-114">hello 下列 JSON 顯示 hello hello OMS 代理程式延伸結構描述。</span><span class="sxs-lookup"><span data-stu-id="81124-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="81124-115">hello 延伸模組需要 hello 工作區識別碼和工作區金鑰從 hello 目標 OMS 工作區，這些可以找到 hello OMS 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="81124-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="81124-116">Hello 工作區金鑰應該視為機密資料，因為它應該儲存在受保護的設定。</span><span class="sxs-lookup"><span data-stu-id="81124-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="81124-117">Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="81124-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="81124-118">請注意，**workspaceId** 和 **workspaceKey** 區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="81124-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="81124-119">屬性值</span><span class="sxs-lookup"><span data-stu-id="81124-119">Property values</span></span>

| <span data-ttu-id="81124-120">名稱</span><span class="sxs-lookup"><span data-stu-id="81124-120">Name</span></span> | <span data-ttu-id="81124-121">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="81124-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="81124-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="81124-122">apiVersion</span></span> | <span data-ttu-id="81124-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="81124-123">2015-06-15</span></span> |
| <span data-ttu-id="81124-124">publisher</span><span class="sxs-lookup"><span data-stu-id="81124-124">publisher</span></span> | <span data-ttu-id="81124-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="81124-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="81124-126">類型</span><span class="sxs-lookup"><span data-stu-id="81124-126">type</span></span> | <span data-ttu-id="81124-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="81124-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="81124-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="81124-128">typeHandlerVersion</span></span> | <span data-ttu-id="81124-129">1.0</span><span class="sxs-lookup"><span data-stu-id="81124-129">1.0</span></span> |
| <span data-ttu-id="81124-130">workspaceId (例如)</span><span class="sxs-lookup"><span data-stu-id="81124-130">workspaceId (e.g)</span></span> | <span data-ttu-id="81124-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="81124-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="81124-132">workspaceKey (例如)</span><span class="sxs-lookup"><span data-stu-id="81124-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="81124-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="81124-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="81124-134">範本部署</span><span class="sxs-lookup"><span data-stu-id="81124-134">Template deployment</span></span>

<span data-ttu-id="81124-135">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="81124-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="81124-136">hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello OMS Agent 擴充功能，在 Azure 資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="81124-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="81124-137">包含 hello OMS 代理程式 VM 擴充功能的範例範本可以找到上 hello [Azure 快速入門圖庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm)。</span><span class="sxs-lookup"><span data-stu-id="81124-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="81124-138">可以巢狀方式置於 hello 虛擬機器資源 hello JSON 的虛擬機器擴充功能，或將其放在 hello 根或資源管理員 JSON 範本的最上層。</span><span class="sxs-lookup"><span data-stu-id="81124-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="81124-139">hello JSON hello 位置會影響 hello hello 資源名稱和類型的值。</span><span class="sxs-lookup"><span data-stu-id="81124-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="81124-140">如需詳細資訊，請參閱[設定子資源的名稱和類型](../../azure-resource-manager/resource-manager-template-child-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="81124-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="81124-141">hello 下列範例假設 hello OMS 擴充功能位於 hello 虛擬機器資源。</span><span class="sxs-lookup"><span data-stu-id="81124-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="81124-142">巢狀 hello 延伸模組資源、 hello JSON 會放置於 hello `"resources": []` hello 虛擬機器的物件。</span><span class="sxs-lookup"><span data-stu-id="81124-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="81124-143">根目錄 hello hello 範本 hello 擴充 JSON 時，hello 資源名稱包含參考 toohello 父虛擬機器，並 hello 類型會反映 hello 巢狀的組態。</span><span class="sxs-lookup"><span data-stu-id="81124-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="81124-144">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="81124-144">PowerShell deployment</span></span>

<span data-ttu-id="81124-145">hello`Set-AzureRmVMExtension`命令可以是使用的 toodeploy hello OMS 代理程式的虛擬機器擴充功能 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81124-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="81124-146">在執行之前 hello 命令，hello 公用和私用組態需要 toobe PowerShell 雜湊表中儲存。</span><span class="sxs-lookup"><span data-stu-id="81124-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="81124-147">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="81124-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="81124-148">疑難排解</span><span class="sxs-lookup"><span data-stu-id="81124-148">Troubleshoot</span></span>

<span data-ttu-id="81124-149">從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="81124-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="81124-150">toosee hello 部署狀態的延伸模組指定的 vm 時，執行下列命令所使用的 hello hello Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="81124-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="81124-151">延伸模組執行輸出 hello 中找到的記錄的 toofiles 之後，目錄：</span><span class="sxs-lookup"><span data-stu-id="81124-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="81124-152">支援</span><span class="sxs-lookup"><span data-stu-id="81124-152">Support</span></span>

<span data-ttu-id="81124-153">如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="81124-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="81124-154">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="81124-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="81124-155">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="81124-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="81124-156">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="81124-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
