---
title: "aaaView Azure 網路監看員拓樸-PowerShell |Microsoft 文件"
description: "本文將說明如何 toouse PowerShell tooquery 網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="96a09-103">使用 PowerShell 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="96a09-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="96a09-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96a09-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="96a09-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="96a09-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="96a09-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="96a09-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="96a09-107">REST API</span><span class="sxs-lookup"><span data-stu-id="96a09-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="96a09-108">網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="96a09-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="96a09-109">在 hello 入口網站，此視覺效果會自動顯示 tooyou。</span><span class="sxs-lookup"><span data-stu-id="96a09-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="96a09-110">hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。</span><span class="sxs-lookup"><span data-stu-id="96a09-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="96a09-111">這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="96a09-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="96a09-112">hello 互連的方式是在兩個關聯性模型化。</span><span class="sxs-lookup"><span data-stu-id="96a09-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="96a09-113">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="96a09-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="96a09-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="96a09-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="96a09-115">hello 下列清單會查詢 hello 拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="96a09-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="96a09-116">**名稱**-hello hello 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="96a09-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="96a09-117">**識別碼**-hello hello 資源的 uri。</span><span class="sxs-lookup"><span data-stu-id="96a09-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="96a09-118">**位置**-hello hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="96a09-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="96a09-119">**關聯**-一份關聯 toohello 參考物件。</span><span class="sxs-lookup"><span data-stu-id="96a09-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="96a09-120">**名稱**-hello hello 名稱所參考的資源。</span><span class="sxs-lookup"><span data-stu-id="96a09-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="96a09-121">**resourceId** -hello resourceId 為 hello 參考 hello 關聯中的 hello 資源 uri。</span><span class="sxs-lookup"><span data-stu-id="96a09-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="96a09-122">**associationType** -這個值會參考 hello hello 子物件 hello 父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="96a09-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="96a09-123">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="96a09-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96a09-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="96a09-124">Before you begin</span></span>

<span data-ttu-id="96a09-125">在此案例中，您可以使用 hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="96a09-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="96a09-126">另外還有發行項上如何太[擷取使用 REST API 的網路拓樸](network-watcher-topology-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="96a09-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="96a09-127">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="96a09-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="96a09-128">案例</span><span class="sxs-lookup"><span data-stu-id="96a09-128">Scenario</span></span>

<span data-ttu-id="96a09-129">hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="96a09-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="96a09-130">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="96a09-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="96a09-131">hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="96a09-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="96a09-132">hello`$networkWatcher`變數傳遞 toohello `Get-AzureRmNetworkWatcherTopology` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="96a09-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="96a09-133">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="96a09-133">Retrieve topology</span></span>

<span data-ttu-id="96a09-134">hello`Get-AzureRmNetworkWatcherTopology`指令程式會擷取指定的資源群組的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="96a09-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="96a09-135">結果</span><span class="sxs-lookup"><span data-stu-id="96a09-135">Results</span></span>

<span data-ttu-id="96a09-136">hello 傳回的結果具有的屬性名稱 「 資源 」，其中包含 hello hello json 回應主體`Get-AzureRmNetworkWatcherTopology`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="96a09-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="96a09-137">hello 回應包含 hello 網路安全性群組與它們關聯 （也就是包含、 相關聯） 中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="96a09-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="96a09-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96a09-138">Next steps</span></span>

<span data-ttu-id="96a09-139">了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="96a09-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


