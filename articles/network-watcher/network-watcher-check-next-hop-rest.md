---
title: "與 Azure 網路監看員下個躍點-REST 下個躍點 aaaFind |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型，且使用下一個躍點使用的 ip 位址 hello Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="89d37-103">找出 hello 下一個躍點類型會使用 Aure 網路監看員使用 Azure REST API 中的 hello 下一個躍點功能</span><span class="sxs-lookup"><span data-stu-id="89d37-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="89d37-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="89d37-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="89d37-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89d37-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="89d37-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="89d37-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="89d37-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="89d37-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="89d37-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="89d37-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="89d37-109">下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="89d37-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="89d37-110">這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="89d37-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="89d37-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="89d37-111">Before you begin</span></span>

<span data-ttu-id="89d37-112">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="89d37-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="89d37-113">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="89d37-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="89d37-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="89d37-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="89d37-115">案例</span><span class="sxs-lookup"><span data-stu-id="89d37-115">Scenario</span></span>

<span data-ttu-id="89d37-116">在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。</span><span class="sxs-lookup"><span data-stu-id="89d37-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="89d37-117">toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="89d37-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="89d37-118">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="89d37-118">In this scenario, you will:</span></span>

* <span data-ttu-id="89d37-119">擷取虛擬機器的 hello 下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="89d37-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="89d37-120">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="89d37-120">Log in with ARMClient</span></span>

<span data-ttu-id="89d37-121">登入 tooarmclient 與您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="89d37-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="89d37-122">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="89d37-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="89d37-123">執行下列指令碼 tooreturn hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89d37-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="89d37-124">執行下一個躍點需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="89d37-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="89d37-125">下列程式碼的 hello hello 下列變數需要值：</span><span class="sxs-lookup"><span data-stu-id="89d37-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="89d37-126">**subscriptionId** -hello 訂用帳戶 Id toouse。</span><span class="sxs-lookup"><span data-stu-id="89d37-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="89d37-127">**resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="89d37-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="89d37-128">從 hello 下列輸出，hello hello 虛擬機器識別碼 hello 下列範例中使用：</span><span class="sxs-lookup"><span data-stu-id="89d37-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="89d37-129">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="89d37-129">Get Next Hop</span></span>

<span data-ttu-id="89d37-130">一旦建立 hello 授權標頭，就可以擷取 hello 從虛擬機器的下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="89d37-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="89d37-131">hello 下列的值必須取代的 hello 程式碼範例 toowork。</span><span class="sxs-lookup"><span data-stu-id="89d37-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="89d37-132">網路監看員 REST api 呼叫 hello hello 要求 URI 是 hello 包含 hello 網路監看員，您執行的 hello 診斷動作不 hello 資源的資源群組中的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="89d37-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="89d37-133">下一個躍點需要 hello VM 資源配置 toorun。</span><span class="sxs-lookup"><span data-stu-id="89d37-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="89d37-134">結果</span><span class="sxs-lookup"><span data-stu-id="89d37-134">Results</span></span>

<span data-ttu-id="89d37-135">hello 下列程式碼片段是收到 hello 輸出的範例。</span><span class="sxs-lookup"><span data-stu-id="89d37-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="89d37-136">hello 結果包含下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="89d37-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="89d37-137">**nextHopType** -這個值可以是下列值的 hello 的其中一個： 網際網路、 VirtualAppliance、 VirtualNetworkGateway、 VnetLocal、 HyperNetGateway，或 None。</span><span class="sxs-lookup"><span data-stu-id="89d37-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="89d37-138">**nextHopIpAddress** -hello hello 下一個躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="89d37-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="89d37-139">**routeTableId** -hello 值為 hello 與 hello 路由相關聯的路由表的 uri，或如果不是使用者定義路由是定義的 hello 值*系統路由*傳回。</span><span class="sxs-lookup"><span data-stu-id="89d37-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="89d37-140">hello 以下是 json 格式的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="89d37-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="89d37-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89d37-141">Next steps</span></span>

<span data-ttu-id="89d37-142">後無法 toofind 出 hello 虛擬機器的下一個躍點後，您可以檢視您的網路資源的 hello 安全性造訪[安全性檢視概觀](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="89d37-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














