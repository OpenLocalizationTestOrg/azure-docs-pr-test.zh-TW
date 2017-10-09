---
title: "aaaView Azure 網路監看員拓樸-Azure CLI 1.0 |Microsoft 文件"
description: "本文將說明如何 toouse Azure CLI 1.0 tooquery 網路拓撲。"
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
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="1ddfd-103">使用 Azure CLI 1.0 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="1ddfd-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1ddfd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ddfd-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="1ddfd-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1ddfd-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="1ddfd-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ddfd-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="1ddfd-107">REST API</span><span class="sxs-lookup"><span data-stu-id="1ddfd-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="1ddfd-108">網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="1ddfd-109">在 hello 入口網站，此視覺效果會自動顯示 tooyou。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="1ddfd-110">hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="1ddfd-111">這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="1ddfd-112">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="1ddfd-113">hello 互連的方式是在兩個關聯性模型化。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="1ddfd-114">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="1ddfd-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="1ddfd-115">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="1ddfd-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="1ddfd-116">hello 下列清單會查詢 hello 拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="1ddfd-117">**名稱**-hello hello 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="1ddfd-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="1ddfd-118">**識別碼**-hello hello 資源的 uri。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="1ddfd-119">**位置**-hello hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="1ddfd-120">**關聯**-一份關聯 toohello 參考物件。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="1ddfd-121">**名稱**-hello hello 名稱所參考的資源。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="1ddfd-122">**resourceId** -hello resourceId 為 hello 參考 hello 關聯中的 hello 資源 uri。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="1ddfd-123">**associationType** -這個值會參考 hello hello 子物件 hello 父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="1ddfd-124">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ddfd-125">開始之前</span><span class="sxs-lookup"><span data-stu-id="1ddfd-125">Before you begin</span></span>

<span data-ttu-id="1ddfd-126">在此案例中，您可以使用 hello `network watcher topology` cmdlet tooretrieve hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="1ddfd-127">另外還有發行項上如何太[擷取使用 REST API 的網路拓樸](network-watcher-topology-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="1ddfd-128">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="1ddfd-129">案例</span><span class="sxs-lookup"><span data-stu-id="1ddfd-129">Scenario</span></span>

<span data-ttu-id="1ddfd-130">hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="1ddfd-131">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="1ddfd-131">Retrieve topology</span></span>

<span data-ttu-id="1ddfd-132">hello`network watcher topology`指令程式會擷取指定的資源群組的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="1ddfd-133">加入 hello 引數 」-json"tooview hello oput json 格式</span><span class="sxs-lookup"><span data-stu-id="1ddfd-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="1ddfd-134">結果</span><span class="sxs-lookup"><span data-stu-id="1ddfd-134">Results</span></span>

<span data-ttu-id="1ddfd-135">hello 傳回的結果具有的屬性名稱 「 資源 」，其中包含 hello hello json 回應主體`network watcher topology`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="1ddfd-136">hello 回應包含 hello 網路安全性群組與它們關聯 （也就是包含、 相關聯） 中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="1ddfd-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1ddfd-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ddfd-137">Next steps</span></span>

<span data-ttu-id="1ddfd-138">深入了解 hello 安全性規則所套用的 tooyour 網路資源，造訪[安全性的群組檢視概觀](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1ddfd-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
