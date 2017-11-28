---
title: "檢視 Azure 網路監看員拓撲 - REST API | Microsoft Docs"
description: "本文會說明如何使用 REST API 來查詢網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="f6c83-103">使用 REST API 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="f6c83-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f6c83-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6c83-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="f6c83-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f6c83-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="f6c83-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f6c83-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="f6c83-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f6c83-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="f6c83-108">網路監看員的拓撲功能可以視覺方式呈現訂用帳戶中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="f6c83-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="f6c83-109">在入口網站中，會自動向您呈現這個視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f6c83-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="f6c83-110">透過 PowerShell 即可擷取入口網站拓撲檢視背後的資訊。</span><span class="sxs-lookup"><span data-stu-id="f6c83-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="f6c83-111">這項功能可讓您活用拓撲資訊，因為資料可供其他工具取用以建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f6c83-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="f6c83-112">系統會根據兩項關聯性建立彼此間聯繫關係的模型。</span><span class="sxs-lookup"><span data-stu-id="f6c83-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="f6c83-113">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="f6c83-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="f6c83-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="f6c83-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="f6c83-115">下列清單是查詢拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="f6c83-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="f6c83-116">**名稱** - 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="f6c83-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="f6c83-117">**識別碼** - 資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="f6c83-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="f6c83-118">**位置** - 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="f6c83-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="f6c83-119">**關聯** - 與參考物件之關聯的清單。</span><span class="sxs-lookup"><span data-stu-id="f6c83-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="f6c83-120">**名稱** - 所參考資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6c83-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="f6c83-121">**resourceId** - resourceId 是關聯中所參考資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="f6c83-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="f6c83-122">**associationType** - 這個值會參考子物件與父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f6c83-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="f6c83-123">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="f6c83-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f6c83-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="f6c83-124">Before you begin</span></span>

<span data-ttu-id="f6c83-125">在此案例中，您會擷取拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="f6c83-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="f6c83-126">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="f6c83-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="f6c83-127">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="f6c83-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f6c83-128">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="f6c83-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="f6c83-129">案例</span><span class="sxs-lookup"><span data-stu-id="f6c83-129">Scenario</span></span>

<span data-ttu-id="f6c83-130">本文涵蓋的案例會擷取指定資源群組的拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="f6c83-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f6c83-131">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="f6c83-131">Log in with ARMClient</span></span>

<span data-ttu-id="f6c83-132">使用 Azure 認證登入 Armclient。</span><span class="sxs-lookup"><span data-stu-id="f6c83-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="f6c83-133">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="f6c83-133">Retrieve topology</span></span>

<span data-ttu-id="f6c83-134">下列範例會要求來自 REST API 的拓撲。</span><span class="sxs-lookup"><span data-stu-id="f6c83-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="f6c83-135">此範例中的參數會設定為允許彈性建立範例。</span><span class="sxs-lookup"><span data-stu-id="f6c83-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="f6c83-136">以它們周圍的 \< \> 取代所有值。</span><span class="sxs-lookup"><span data-stu-id="f6c83-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="f6c83-137">下列的回應是擷取資源群組的拓撲時所傳回的縮短回應之範例︰</span><span class="sxs-lookup"><span data-stu-id="f6c83-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="f6c83-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6c83-138">Next steps</span></span>

<span data-ttu-id="f6c83-139">若要了解如何利用 Power BI 將 NSG 流量記錄視覺化，請瀏覽[利用 Power BI 將 NSG 流量記錄視覺](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f6c83-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

