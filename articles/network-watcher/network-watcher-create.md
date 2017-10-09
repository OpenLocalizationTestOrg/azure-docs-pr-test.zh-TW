---
title: "aaaCreate Azure 網路監看員執行個體 |Microsoft 文件"
description: "本頁面提供的 hello 步驟 toocreate 網路監看員的執行個體使用 hello 入口網站和 Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="cae11-103">建立 Azure 網路監看員執行個體</span><span class="sxs-lookup"><span data-stu-id="cae11-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="cae11-104">網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。</span><span class="sxs-lookup"><span data-stu-id="cae11-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="cae11-105">案例層級的監視可讓您在結束 tooend 網路層級檢視 toodiagnose 問題。</span><span class="sxs-lookup"><span data-stu-id="cae11-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="cae11-106">網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。</span><span class="sxs-lookup"><span data-stu-id="cae11-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cae11-107">因為網路監看員時，目前只支援 CLI 1.0，hello 指示 toocreate 的新網路監看員執行個體提供 CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="cae11-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="cae11-108">在 hello 入口網站中建立網路監看員</span><span class="sxs-lookup"><span data-stu-id="cae11-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="cae11-109">瀏覽過**更服務** > **網路** > **網路監看員**。</span><span class="sxs-lookup"><span data-stu-id="cae11-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="cae11-110">您可以選取所有您想 tooenable 網路監看員的 hello 訂閱的。</span><span class="sxs-lookup"><span data-stu-id="cae11-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="cae11-111">此動作會在每個可用區域建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="cae11-111">This action creates a Network Watcher in every region that is available.</span></span>

![建立網路監看員][1]

<span data-ttu-id="cae11-113">當您啟用網路監看員使用 hello 入口網站時，hello hello 網路監看員執行個體名稱將會自動設定 tooNetworkWatcher_region_name region_name 其中對應 toohello hello 執行個體已啟用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="cae11-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="cae11-114">例如，在美國中西部區域啟用的網路監看員，名稱將會是 NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="cae11-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="cae11-115">此外，會自動加入 hello 網路監看員執行個體，稱為 NetworkWatcherRG 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cae11-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="cae11-116">如果該資源群組不存在，系統將會建立它。</span><span class="sxs-lookup"><span data-stu-id="cae11-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="cae11-117">如果您想將網路監看員執行個體和 hello toocustomize hello 名稱就放到的資源群組，您可以使用 Powershell、 REST API hello 或 ARMClient 如下所述的方法。</span><span class="sxs-lookup"><span data-stu-id="cae11-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="cae11-118">在每個選項中，hello 資源群組必須先放置到其中的 hello 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="cae11-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="cae11-119">使用 PowerShell 建立網路監看員</span><span class="sxs-lookup"><span data-stu-id="cae11-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="cae11-120">toocreate 網路監看員，執行下列範例中的 hello 的執行個體：</span><span class="sxs-lookup"><span data-stu-id="cae11-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="cae11-121">以 hello REST API 建立網路監看員</span><span class="sxs-lookup"><span data-stu-id="cae11-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="cae11-122">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="cae11-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="cae11-123">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="cae11-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="cae11-124">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="cae11-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="cae11-125">建立 hello 網路監看員</span><span class="sxs-lookup"><span data-stu-id="cae11-125">Create hello network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="cae11-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cae11-126">Next steps</span></span>

<span data-ttu-id="cae11-127">現在，您有網路監看員的執行個體，深入了解可用的 hello 功能：</span><span class="sxs-lookup"><span data-stu-id="cae11-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="cae11-128">拓撲</span><span class="sxs-lookup"><span data-stu-id="cae11-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="cae11-129">封包擷取</span><span class="sxs-lookup"><span data-stu-id="cae11-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="cae11-130">IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="cae11-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="cae11-131">下一個躍點</span><span class="sxs-lookup"><span data-stu-id="cae11-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="cae11-132">安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="cae11-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="cae11-133">NSG 流量記錄</span><span class="sxs-lookup"><span data-stu-id="cae11-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="cae11-134">虛擬網路閘道疑難排解</span><span class="sxs-lookup"><span data-stu-id="cae11-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="cae11-135">一旦建立網路監看員執行個體之後，可以設定下列 hello 文章封裝擷取：[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="cae11-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











