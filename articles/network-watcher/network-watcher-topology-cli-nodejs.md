---
title: "檢視 Azure 網路監看員拓撲 - Azure CLI 1.0 | Microsoft Docs"
description: "本文將描述如何使用 Azure CLI 1.0 來查詢網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9178c485a92e04564c95dae8073f045b5c639bb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="257f1-103">使用 Azure CLI 1.0 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="257f1-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="257f1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="257f1-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="257f1-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="257f1-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="257f1-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="257f1-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="257f1-107">REST API</span><span class="sxs-lookup"><span data-stu-id="257f1-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="257f1-108">網路監看員的拓撲功能可以視覺方式呈現訂用帳戶中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="257f1-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="257f1-109">在入口網站中，會自動向您呈現這個視覺效果。</span><span class="sxs-lookup"><span data-stu-id="257f1-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="257f1-110">透過 PowerShell 即可擷取入口網站拓撲檢視背後的資訊。</span><span class="sxs-lookup"><span data-stu-id="257f1-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="257f1-111">這項功能可讓您活用拓撲資訊，因為資料可供其他工具取用以建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="257f1-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="257f1-112">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="257f1-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="257f1-113">系統會根據兩項關聯性建立彼此間聯繫關係的模型。</span><span class="sxs-lookup"><span data-stu-id="257f1-113">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="257f1-114">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="257f1-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="257f1-115">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="257f1-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="257f1-116">下列清單是查詢拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="257f1-116">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="257f1-117">**名稱** - 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="257f1-117">**name** - The name of the resource</span></span>
* <span data-ttu-id="257f1-118">**識別碼** - 資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="257f1-118">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="257f1-119">**位置** - 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="257f1-119">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="257f1-120">**關聯** - 與參考物件之關聯的清單。</span><span class="sxs-lookup"><span data-stu-id="257f1-120">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="257f1-121">**名稱** - 所參考資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="257f1-121">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="257f1-122">**resourceId** - resourceId 是關聯中所參考資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="257f1-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="257f1-123">**associationType** - 這個值會參考子物件與父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="257f1-123">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="257f1-124">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="257f1-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="257f1-125">開始之前</span><span class="sxs-lookup"><span data-stu-id="257f1-125">Before you begin</span></span>

<span data-ttu-id="257f1-126">在此案例中，您會使用 `network watcher topology` Cmdlet 來擷取拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="257f1-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="257f1-127">另有一篇文章說明如何[使用 REST API 擷取網路拓撲](network-watcher-topology-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="257f1-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="257f1-128">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="257f1-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="257f1-129">案例</span><span class="sxs-lookup"><span data-stu-id="257f1-129">Scenario</span></span>

<span data-ttu-id="257f1-130">本文涵蓋的案例會擷取指定資源群組的拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="257f1-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="257f1-131">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="257f1-131">Retrieve topology</span></span>

<span data-ttu-id="257f1-132">`network watcher topology` Cmdlet 會擷取指定資源群組的拓撲。</span><span class="sxs-lookup"><span data-stu-id="257f1-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="257f1-133">新增引數 "--json" 即可以 json 格式檢視輸出</span><span class="sxs-lookup"><span data-stu-id="257f1-133">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="257f1-134">結果</span><span class="sxs-lookup"><span data-stu-id="257f1-134">Results</span></span>

<span data-ttu-id="257f1-135">所傳回的結果有屬性名稱「資源」，其中包含 `network watcher topology` Cmdlet 的 json 回應主體。</span><span class="sxs-lookup"><span data-stu-id="257f1-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="257f1-136">回應包含網路安全性群組中的資源和其關聯 (也就是包含、相關聯)。</span><span class="sxs-lookup"><span data-stu-id="257f1-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="257f1-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="257f1-137">Next steps</span></span>

<span data-ttu-id="257f1-138">請瀏覽[安全性群組檢視概觀](network-watcher-security-group-view-overview.md)以深入了解套用到網路資源的安全性規則</span><span class="sxs-lookup"><span data-stu-id="257f1-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
