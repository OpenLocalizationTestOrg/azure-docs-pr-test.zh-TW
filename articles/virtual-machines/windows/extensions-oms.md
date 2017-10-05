---
title: "適用於 Windows 的 OMS Azure 虛擬機器擴充功能 | Microsoft Docs"
description: "使用虛擬機器擴充功能在 Windows 虛擬機器上部署 OMS 代理程式。"
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
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="5c66a-103">適用於 Windows 的 OMS 虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="5c66a-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="5c66a-104">Operations Management Suite (OMS) 可提供雲端和內部部署資產的監視、警示和警示補救功能。</span><span class="sxs-lookup"><span data-stu-id="5c66a-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="5c66a-105">Microsoft 已發佈和支援適用於 Windows 的 OMS 代理程式虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5c66a-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="5c66a-106">擴充功能會在 Azure 虛擬機器上安裝 OMS 代理程式，並且在現有的 OMS 工作區中註冊虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5c66a-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="5c66a-107">本文件詳述適用於 Windows 的 OMS 虛擬機器擴充功能所支援的平台、組態和部署選項。</span><span class="sxs-lookup"><span data-stu-id="5c66a-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c66a-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c66a-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="5c66a-109">作業系統</span><span class="sxs-lookup"><span data-stu-id="5c66a-109">Operating system</span></span>
<span data-ttu-id="5c66a-110">適用於 Windows 的 OMS 代理程式擴充功能可以在 Windows Server 2008 R2、2012、2012 R2 及 2016 版本上執行。</span><span class="sxs-lookup"><span data-stu-id="5c66a-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="5c66a-111">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="5c66a-111">Internet connectivity</span></span>
<span data-ttu-id="5c66a-112">適用於 Windows 的 OMS 代理程式擴充功能會要求目標虛擬機器連接到網際網路。</span><span class="sxs-lookup"><span data-stu-id="5c66a-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="5c66a-113">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="5c66a-113">Extension schema</span></span>

<span data-ttu-id="5c66a-114">下列 JSON 顯示 OMS 代理程式擴充功能的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5c66a-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="5c66a-115">此擴充功能需要來自目標 OMS 工作區的工作區識別碼和工作區金鑰，這些在 OMS 入口網站上皆有提供。</span><span class="sxs-lookup"><span data-stu-id="5c66a-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="5c66a-116">由於工作區金鑰應視為敏感性資料，因此應儲存在受保護的設定組態中。</span><span class="sxs-lookup"><span data-stu-id="5c66a-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="5c66a-117">Azure VM 擴充功能保護的設定資料會經過加密，只會在目標虛擬機器上解密。</span><span class="sxs-lookup"><span data-stu-id="5c66a-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="5c66a-118">請注意，**workspaceId** 和 **workspaceKey** 區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5c66a-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="5c66a-119">屬性值</span><span class="sxs-lookup"><span data-stu-id="5c66a-119">Property values</span></span>

| <span data-ttu-id="5c66a-120">名稱</span><span class="sxs-lookup"><span data-stu-id="5c66a-120">Name</span></span> | <span data-ttu-id="5c66a-121">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="5c66a-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="5c66a-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="5c66a-122">apiVersion</span></span> | <span data-ttu-id="5c66a-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="5c66a-123">2015-06-15</span></span> |
| <span data-ttu-id="5c66a-124">publisher</span><span class="sxs-lookup"><span data-stu-id="5c66a-124">publisher</span></span> | <span data-ttu-id="5c66a-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="5c66a-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="5c66a-126">類型</span><span class="sxs-lookup"><span data-stu-id="5c66a-126">type</span></span> | <span data-ttu-id="5c66a-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="5c66a-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="5c66a-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="5c66a-128">typeHandlerVersion</span></span> | <span data-ttu-id="5c66a-129">1.0</span><span class="sxs-lookup"><span data-stu-id="5c66a-129">1.0</span></span> |
| <span data-ttu-id="5c66a-130">workspaceId (例如)</span><span class="sxs-lookup"><span data-stu-id="5c66a-130">workspaceId (e.g)</span></span> | <span data-ttu-id="5c66a-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="5c66a-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="5c66a-132">workspaceKey (例如)</span><span class="sxs-lookup"><span data-stu-id="5c66a-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="5c66a-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="5c66a-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="5c66a-134">範本部署</span><span class="sxs-lookup"><span data-stu-id="5c66a-134">Template deployment</span></span>

<span data-ttu-id="5c66a-135">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5c66a-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="5c66a-136">上一節中詳述的 JSON 結構描述可在部署 Azure Resource Manager 範本時，在 Azure Resource Manager 範本中用來執行 OMS 代理程式擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5c66a-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="5c66a-137">在 [Azure 快速入門資源庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm)上可以找到包含 OMS 代理程式 VM 擴充功能的範例範本。</span><span class="sxs-lookup"><span data-stu-id="5c66a-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="5c66a-138">虛擬機器擴充功能的 JSON 可以巢狀方式置於虛擬機器資源內部，或放在 Resource Manager JSON 範本的根目錄或最上層。</span><span class="sxs-lookup"><span data-stu-id="5c66a-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="5c66a-139">JSON 的放置會影響資源名稱和類型的值。</span><span class="sxs-lookup"><span data-stu-id="5c66a-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="5c66a-140">如需詳細資訊，請參閱[設定子資源的名稱和類型](../../azure-resource-manager/resource-manager-template-child-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="5c66a-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="5c66a-141">下列範例假設 OMS 擴充功能以巢狀方式置於虛擬機器資源內部。</span><span class="sxs-lookup"><span data-stu-id="5c66a-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="5c66a-142">在巢狀處理擴充資源時，JSON 會放在虛擬機器的 `"resources": []` 物件中。</span><span class="sxs-lookup"><span data-stu-id="5c66a-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


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

<span data-ttu-id="5c66a-143">將擴充 JSON 置於範本的根目錄時，資源名稱包含父系虛擬機器的參考，而類型可反映巢狀的組態。</span><span class="sxs-lookup"><span data-stu-id="5c66a-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="5c66a-144">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="5c66a-144">PowerShell deployment</span></span>

<span data-ttu-id="5c66a-145">`Set-AzureRmVMExtension` 命令可以用來將 OMS 代理程式虛擬機器擴充功能部署到現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5c66a-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="5c66a-146">執行命令之前，必須將公用和私人組態儲存在 PowerShell 雜湊表中。</span><span class="sxs-lookup"><span data-stu-id="5c66a-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="5c66a-147">疑難排解與支援</span><span class="sxs-lookup"><span data-stu-id="5c66a-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="5c66a-148">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5c66a-148">Troubleshoot</span></span>

<span data-ttu-id="5c66a-149">從 Azure 入口網站及透過使用 Azure PowerShell 模組，都可擷取有關擴充功能部署狀態的資料。</span><span class="sxs-lookup"><span data-stu-id="5c66a-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="5c66a-150">若要查看所指定 VM 的擴充功能部署狀態，請使用 Azure PowerShell 模組來執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="5c66a-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="5c66a-151">擴充功能執行輸出會記錄至下列目錄中的檔案︰</span><span class="sxs-lookup"><span data-stu-id="5c66a-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="5c66a-152">支援</span><span class="sxs-lookup"><span data-stu-id="5c66a-152">Support</span></span>

<span data-ttu-id="5c66a-153">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/en-us/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="5c66a-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="5c66a-154">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="5c66a-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5c66a-155">請移至 [Azure 支援網站](https://azure.microsoft.com/en-us/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="5c66a-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="5c66a-156">如需使用 Azure 支援的資訊，請參閱 [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="5c66a-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
