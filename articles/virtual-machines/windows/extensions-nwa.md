---
title: "aaaAzure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能 |Microsoft 文件"
description: "部署 Windows 虛擬機器使用虛擬機器擴充功能上的 hello 網路監看員的代理程式。"
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="b9ecb-103">適用於 Windows 的網路監看員代理程式虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="b9ecb-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="b9ecb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b9ecb-104">Overview</span></span>

<span data-ttu-id="b9ecb-105">[Azure 網路監看員](https://review.docs.microsoft.com/en-us/azure/network-watcher/)是網路效能的監視、診斷和分析服務，可讓您監視 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="b9ecb-106">hello 網路監看員的代理程式的虛擬機器擴充功能是某些 hello Azure 虛擬機器上的網路監看員功能的需求。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="b9ecb-107">這包括擷取隨選網路流量和其他進階功能。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="b9ecb-108">此文件詳細資料 hello 支援平台和部署選項 hello 網路監看員的代理程式的虛擬機器擴充功能的 Windows。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ecb-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="b9ecb-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="b9ecb-110">作業系統</span><span class="sxs-lookup"><span data-stu-id="b9ecb-110">Operating system</span></span>

<span data-ttu-id="b9ecb-111">hello 網路監看員的代理程式擴充功能的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="b9ecb-112">請注意，hello Nano Server 不支援這一次。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="b9ecb-113">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="b9ecb-113">Internet connectivity</span></span>

<span data-ttu-id="b9ecb-114">某些 hello 網路監看員的代理程式的功能要求該 hello 目標虛擬機器必須連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="b9ecb-115">不使用 hello 能力 tooestablish 傳出連線的一些 hello 網路監看員的代理程式功能可能故障，或變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="b9ecb-116">如需詳細資訊，請參閱 hello[網路監看員文件](../../network-watcher/network-watcher-monitoring-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="b9ecb-117">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="b9ecb-117">Extension schema</span></span>

<span data-ttu-id="b9ecb-118">hello 下列 JSON 顯示 hello 網路監看員的代理程式延伸模組的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="b9ecb-119">hello 延伸模組都不需要也不支援任何使用者提供的設定，這次並依賴其預設設定。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="b9ecb-120">屬性值</span><span class="sxs-lookup"><span data-stu-id="b9ecb-120">Property values</span></span>

| <span data-ttu-id="b9ecb-121">名稱</span><span class="sxs-lookup"><span data-stu-id="b9ecb-121">Name</span></span> | <span data-ttu-id="b9ecb-122">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="b9ecb-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="b9ecb-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b9ecb-123">apiVersion</span></span> | <span data-ttu-id="b9ecb-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="b9ecb-124">2015-06-15</span></span> |
| <span data-ttu-id="b9ecb-125">publisher</span><span class="sxs-lookup"><span data-stu-id="b9ecb-125">publisher</span></span> | <span data-ttu-id="b9ecb-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="b9ecb-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="b9ecb-127">類型</span><span class="sxs-lookup"><span data-stu-id="b9ecb-127">type</span></span> | <span data-ttu-id="b9ecb-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="b9ecb-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="b9ecb-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="b9ecb-129">typeHandlerVersion</span></span> | <span data-ttu-id="b9ecb-130">1.4</span><span class="sxs-lookup"><span data-stu-id="b9ecb-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="b9ecb-131">範本部署</span><span class="sxs-lookup"><span data-stu-id="b9ecb-131">Template deployment</span></span>

<span data-ttu-id="b9ecb-132">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="b9ecb-133">hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 網路監看員的代理程式擴充功能，在 Azure 資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="b9ecb-134">PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="b9ecb-134">PowerShell deployment</span></span>

<span data-ttu-id="b9ecb-135">hello`Set-AzureRmVMExtension`命令可以是使用的 toodeploy hello 網路監看員的代理程式的虛擬機器擴充功能 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="b9ecb-136">疑難排解和支援</span><span class="sxs-lookup"><span data-stu-id="b9ecb-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="b9ecb-137">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b9ecb-137">Troubleshooting</span></span>

<span data-ttu-id="b9ecb-138">從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="b9ecb-139">toosee hello 部署狀態的延伸模組指定的 vm 時，執行下列命令所使用的 hello hello Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="b9ecb-140">延伸模組執行輸出 hello 中找到的記錄的 toofiles 之後，目錄：</span><span class="sxs-lookup"><span data-stu-id="b9ecb-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="b9ecb-141">支援</span><span class="sxs-lookup"><span data-stu-id="b9ecb-141">Support</span></span>

<span data-ttu-id="b9ecb-142">如果您需要更多說明，在本文中的任何時間點，您可以參閱 toohello 網路監看員使用者指南 》 文件，或連絡 hello Azure 專家發表 hello [MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="b9ecb-143">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b9ecb-144">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="b9ecb-145">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="b9ecb-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
