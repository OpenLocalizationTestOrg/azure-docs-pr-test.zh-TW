---
title: "aaaAzure 網路監看員的代理程式適用於 Linux 的虛擬機器擴充功能 |Microsoft 文件"
description: "部署使用虛擬機器擴充功能的 Linux 虛擬機器上的 hello 網路監看員的代理程式。"
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="84f70-103">適用於 Linux 的網路監看員代理程式虛擬機器擴充功能</span><span class="sxs-lookup"><span data-stu-id="84f70-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="84f70-104">概觀</span><span class="sxs-lookup"><span data-stu-id="84f70-104">Overview</span></span>

<span data-ttu-id="84f70-105">[Azure 網路監看員](https://review.docs.microsoft.com/en-us/azure/network-watcher/)是網路效能的監視、診斷和分析服務，可讓您監視 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="84f70-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="84f70-106">hello 網路監看員的代理程式的虛擬機器擴充功能是某些 hello Azure 虛擬機器上的網路監看員功能的需求。</span><span class="sxs-lookup"><span data-stu-id="84f70-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="84f70-107">這包括擷取隨選網路流量和其他進階功能。</span><span class="sxs-lookup"><span data-stu-id="84f70-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="84f70-108">此文件詳細資料 hello 支援平台和部署選項 hello 網路監看員的代理程式的虛擬機器擴充功能適用於 Linux。</span><span class="sxs-lookup"><span data-stu-id="84f70-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84f70-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="84f70-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="84f70-110">作業系統</span><span class="sxs-lookup"><span data-stu-id="84f70-110">Operating system</span></span>

<span data-ttu-id="84f70-111">hello 網路監看員的代理程式延伸模組可以執行這些 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="84f70-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="84f70-112">配送映像</span><span class="sxs-lookup"><span data-stu-id="84f70-112">Distribution</span></span> | <span data-ttu-id="84f70-113">版本</span><span class="sxs-lookup"><span data-stu-id="84f70-113">Version</span></span> |
|---|---|
| <span data-ttu-id="84f70-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="84f70-114">Ubuntu</span></span> | <span data-ttu-id="84f70-115">16.04 LTS、14.04 LTS 和 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="84f70-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="84f70-116">Debian</span><span class="sxs-lookup"><span data-stu-id="84f70-116">Debian</span></span> | <span data-ttu-id="84f70-117">7 和 8</span><span class="sxs-lookup"><span data-stu-id="84f70-117">7 and 8</span></span> |
| <span data-ttu-id="84f70-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="84f70-118">RedHat</span></span> | <span data-ttu-id="84f70-119">6.x 和 7.x</span><span class="sxs-lookup"><span data-stu-id="84f70-119">6.x and 7.x</span></span> |
| <span data-ttu-id="84f70-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="84f70-120">Oracle Linux</span></span> | <span data-ttu-id="84f70-121">7x</span><span class="sxs-lookup"><span data-stu-id="84f70-121">7x</span></span> |
| <span data-ttu-id="84f70-122">Suse</span><span class="sxs-lookup"><span data-stu-id="84f70-122">Suse</span></span> | <span data-ttu-id="84f70-123">11 和 12</span><span class="sxs-lookup"><span data-stu-id="84f70-123">11 and 12</span></span> |
| <span data-ttu-id="84f70-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="84f70-124">OpenSuse</span></span> | <span data-ttu-id="84f70-125">7.0</span><span class="sxs-lookup"><span data-stu-id="84f70-125">7.0</span></span> |
| <span data-ttu-id="84f70-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="84f70-126">CentOS</span></span> | <span data-ttu-id="84f70-127">7.0</span><span class="sxs-lookup"><span data-stu-id="84f70-127">7.0</span></span> |

<span data-ttu-id="84f70-128">請注意，目前不支援 CoreOS。</span><span class="sxs-lookup"><span data-stu-id="84f70-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="84f70-129">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="84f70-129">Internet connectivity</span></span>

<span data-ttu-id="84f70-130">某些 hello 網路監看員的代理程式的功能要求該 hello 目標虛擬機器必須連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="84f70-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="84f70-131">不使用 hello 能力 tooestablish 傳出連線的一些 hello 網路監看員的代理程式功能可能故障，或變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="84f70-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="84f70-132">如需詳細資訊，請參閱 hello[網路監看員文件](https://review.docs.microsoft.com/en-us/azure/network-watcher/)。</span><span class="sxs-lookup"><span data-stu-id="84f70-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="84f70-133">擴充功能結構描述</span><span class="sxs-lookup"><span data-stu-id="84f70-133">Extension schema</span></span>

<span data-ttu-id="84f70-134">hello 下列 JSON 顯示 hello 網路監看員的代理程式延伸模組的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="84f70-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="84f70-135">hello 延伸模組都不需要也不支援任何使用者提供的設定，這次並依賴其預設設定。</span><span class="sxs-lookup"><span data-stu-id="84f70-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="84f70-136">屬性值</span><span class="sxs-lookup"><span data-stu-id="84f70-136">Property values</span></span>

| <span data-ttu-id="84f70-137">名稱</span><span class="sxs-lookup"><span data-stu-id="84f70-137">Name</span></span> | <span data-ttu-id="84f70-138">值 / 範例</span><span class="sxs-lookup"><span data-stu-id="84f70-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="84f70-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="84f70-139">apiVersion</span></span> | <span data-ttu-id="84f70-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="84f70-140">2015-06-15</span></span> |
| <span data-ttu-id="84f70-141">publisher</span><span class="sxs-lookup"><span data-stu-id="84f70-141">publisher</span></span> | <span data-ttu-id="84f70-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="84f70-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="84f70-143">類型</span><span class="sxs-lookup"><span data-stu-id="84f70-143">type</span></span> | <span data-ttu-id="84f70-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="84f70-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="84f70-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="84f70-145">typeHandlerVersion</span></span> | <span data-ttu-id="84f70-146">1.4</span><span class="sxs-lookup"><span data-stu-id="84f70-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="84f70-147">範本部署</span><span class="sxs-lookup"><span data-stu-id="84f70-147">Template deployment</span></span>

<span data-ttu-id="84f70-148">也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="84f70-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="84f70-149">hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 網路監看員的代理程式擴充功能，在 Azure 資源管理員範本部署期間。</span><span class="sxs-lookup"><span data-stu-id="84f70-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="84f70-150">Azure CLI 部署</span><span class="sxs-lookup"><span data-stu-id="84f70-150">Azure CLI deployment</span></span>

<span data-ttu-id="84f70-151">hello Azure CLI 可以是使用的 toodeploy hello 網路監看員的代理程式 VM 延伸模組 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="84f70-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="84f70-152">疑難排解和支援</span><span class="sxs-lookup"><span data-stu-id="84f70-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="84f70-153">疑難排解</span><span class="sxs-lookup"><span data-stu-id="84f70-153">Troubleshooting</span></span>

<span data-ttu-id="84f70-154">從 hello Azure 入口網站，也可以使用 Azure CLI hello，可以擷取有關 hello 部署狀態的延伸模組的資料。</span><span class="sxs-lookup"><span data-stu-id="84f70-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="84f70-155">toosee hello 部署狀態的延伸模組指定的 vm，執行下列命令使用 hello hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="84f70-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="84f70-156">延伸模組執行輸出 hello 中找到的記錄的 toofiles 之後，目錄：</span><span class="sxs-lookup"><span data-stu-id="84f70-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="84f70-157">支援</span><span class="sxs-lookup"><span data-stu-id="84f70-157">Support</span></span>

<span data-ttu-id="84f70-158">如果您需要更多說明，在本文中的任何時間點，您可以參閱 toohello 網路監看員文件，或連絡 hello Azure 專家發表 hello [MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="84f70-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="84f70-159">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="84f70-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="84f70-160">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。</span><span class="sxs-lookup"><span data-stu-id="84f70-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="84f70-161">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="84f70-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
