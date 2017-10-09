---
title: "aaaView Azure 網路監看員拓樸-Azure CLI |Microsoft 文件"
description: "本文將說明如何 toouse Azure CLI tooquery 網路拓撲。"
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
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="af076-103">使用 Azure CLI 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="af076-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="af076-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af076-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="af076-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af076-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="af076-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af076-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="af076-107">REST API</span><span class="sxs-lookup"><span data-stu-id="af076-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="af076-108">網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="af076-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="af076-109">在 hello 入口網站，此視覺效果會自動顯示 tooyou。</span><span class="sxs-lookup"><span data-stu-id="af076-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="af076-110">hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。</span><span class="sxs-lookup"><span data-stu-id="af076-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="af076-111">這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="af076-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="af076-112">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="af076-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="af076-113">網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。</span><span class="sxs-lookup"><span data-stu-id="af076-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="af076-114">hello 互連的方式是在兩個關聯性模型化。</span><span class="sxs-lookup"><span data-stu-id="af076-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="af076-115">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="af076-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="af076-116">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="af076-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="af076-117">hello 下列清單會查詢 hello 拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="af076-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="af076-118">**名稱**-hello hello 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="af076-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="af076-119">**識別碼**-hello hello 資源的 uri。</span><span class="sxs-lookup"><span data-stu-id="af076-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="af076-120">**位置**-hello hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="af076-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="af076-121">**關聯**-一份關聯 toohello 參考物件。</span><span class="sxs-lookup"><span data-stu-id="af076-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="af076-122">**名稱**-hello hello 名稱所參考的資源。</span><span class="sxs-lookup"><span data-stu-id="af076-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="af076-123">**resourceId** -hello resourceId 為 hello 參考 hello 關聯中的 hello 資源 uri。</span><span class="sxs-lookup"><span data-stu-id="af076-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="af076-124">**associationType** -這個值會參考 hello hello 子物件 hello 父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="af076-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="af076-125">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="af076-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="af076-126">開始之前</span><span class="sxs-lookup"><span data-stu-id="af076-126">Before you begin</span></span>

<span data-ttu-id="af076-127">在此案例中，您可以使用 hello `network watcher topology` cmdlet tooretrieve hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="af076-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="af076-128">另外還有發行項上如何太[擷取使用 REST API 的網路拓樸](network-watcher-topology-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="af076-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="af076-129">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="af076-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="af076-130">案例</span><span class="sxs-lookup"><span data-stu-id="af076-130">Scenario</span></span>

<span data-ttu-id="af076-131">hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="af076-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="af076-132">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="af076-132">Retrieve topology</span></span>

<span data-ttu-id="af076-133">hello`network watcher topology`指令程式會擷取指定的資源群組的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="af076-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="af076-134">加入 hello 引數 」-json"tooview hello oput json 格式</span><span class="sxs-lookup"><span data-stu-id="af076-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="af076-135">結果</span><span class="sxs-lookup"><span data-stu-id="af076-135">Results</span></span>

<span data-ttu-id="af076-136">hello 傳回的結果具有的屬性名稱 「 資源 」，其中包含 hello hello json 回應主體`network watcher topology`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="af076-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="af076-137">hello 回應包含 hello 網路安全性群組與它們關聯 （也就是包含、 相關聯） 中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="af076-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="af076-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af076-138">Next steps</span></span>

<span data-ttu-id="af076-139">深入了解 hello 安全性規則所套用的 tooyour 網路資源，造訪[安全性的群組檢視概觀](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="af076-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
