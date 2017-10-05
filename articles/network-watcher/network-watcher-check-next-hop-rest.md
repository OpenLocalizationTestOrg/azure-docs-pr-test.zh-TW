---
title: "使用 Azure 網路監看員下一個躍點來尋找下一個躍點 - REST | Microsoft Docs"
description: "本文會說明如何使用 Azure REST API，利用下一個躍點功能來得知下一個躍點類型和 IP 位址"
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
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="58465-103">使用 Azure REST API，利用 Azure 網路監看員的下一個躍點功能找出下一個躍點類型</span><span class="sxs-lookup"><span data-stu-id="58465-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="58465-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="58465-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="58465-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58465-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="58465-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="58465-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="58465-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="58465-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="58465-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="58465-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="58465-109">下一個躍點是網路監看員的一項功能，可根據指定的虛擬機器取得下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="58465-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="58465-110">這項功能可用於判斷離開虛擬機器的流量是否會周遊閘道、網際網路或虛擬網路，以抵達其目的地。</span><span class="sxs-lookup"><span data-stu-id="58465-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="58465-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="58465-111">Before you begin</span></span>

<span data-ttu-id="58465-112">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="58465-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="58465-113">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="58465-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="58465-114">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="58465-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="58465-115">案例</span><span class="sxs-lookup"><span data-stu-id="58465-115">Scenario</span></span>

<span data-ttu-id="58465-116">本文涵蓋的案例會使用網路監看員的下一個躍點功能，以找出資源的下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="58465-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="58465-117">若要深入了解下一個躍點，請造訪[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="58465-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="58465-118">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="58465-118">In this scenario, you will:</span></span>

* <span data-ttu-id="58465-119">擷取虛擬機器的下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="58465-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="58465-120">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="58465-120">Log in with ARMClient</span></span>

<span data-ttu-id="58465-121">使用 Azure 認證登入 Armclient。</span><span class="sxs-lookup"><span data-stu-id="58465-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="58465-122">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="58465-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="58465-123">執行下列指令碼，以傳回虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="58465-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="58465-124">執行下一個躍點需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="58465-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="58465-125">下列程式碼需要下列變數的值︰</span><span class="sxs-lookup"><span data-stu-id="58465-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="58465-126">**subscriptionId** - 要使用的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="58465-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="58465-127">**resourceGroupName** - 包含虛擬機器的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="58465-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="58465-128">從下列的輸出，會在下列範例中使用虛擬機器的識別碼︰</span><span class="sxs-lookup"><span data-stu-id="58465-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="58465-129">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="58465-129">Get Next Hop</span></span>

<span data-ttu-id="58465-130">一旦建立授權標頭後，就可以從虛擬機器擷取下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="58465-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="58465-131">必須取代下列程式碼範例的值才可運作。</span><span class="sxs-lookup"><span data-stu-id="58465-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="58465-132">針對網路監看員 REST API 呼叫，要求 URI 中的資源群組名稱是包含網路監看員的資源群組，而非您要執行診斷動作的資源。</span><span class="sxs-lookup"><span data-stu-id="58465-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

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
> <span data-ttu-id="58465-133">下一個躍點需要配置 VM 資源以供執行。</span><span class="sxs-lookup"><span data-stu-id="58465-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="58465-134">結果</span><span class="sxs-lookup"><span data-stu-id="58465-134">Results</span></span>

<span data-ttu-id="58465-135">以下程式碼片段是所接收輸出的範例。</span><span class="sxs-lookup"><span data-stu-id="58465-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="58465-136">結果包含下列值：</span><span class="sxs-lookup"><span data-stu-id="58465-136">The results contain the following values:</span></span>

* <span data-ttu-id="58465-137">**nextHopType** - 這個值可以是下列值之一︰Internet、VirtualAppliance、VirtualNetworkGateway、VnetLocal、HyperNetGateway 或 None。</span><span class="sxs-lookup"><span data-stu-id="58465-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="58465-138">**nextHopIpAddress** - 下一個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="58465-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="58465-139">**routeTableId** - 值是與路由相關聯的路由資料表的 URI，或者如果沒有定義使用者定義的路由，會傳回系統路由的值。</span><span class="sxs-lookup"><span data-stu-id="58465-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="58465-140">以下是 json 格式的結果。</span><span class="sxs-lookup"><span data-stu-id="58465-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="58465-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58465-141">Next steps</span></span>

<span data-ttu-id="58465-142">一旦您已能夠找出虛擬機器的下一個躍點，就可以檢視您網路資源的安全性，請造訪[安全性檢視概觀](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="58465-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














