---
title: "檢視 Azure 網路監看員拓撲 - PowerShell | Microsoft Docs"
description: "本文會說明如何使用 PowerShell 來查詢網路拓撲。"
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
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="90790-103">使用 PowerShell 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="90790-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="90790-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90790-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="90790-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90790-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="90790-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="90790-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="90790-107">REST API</span><span class="sxs-lookup"><span data-stu-id="90790-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="90790-108">網路監看員的拓撲功能可以視覺方式呈現訂用帳戶中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="90790-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="90790-109">在入口網站中，會自動向您呈現這個視覺效果。</span><span class="sxs-lookup"><span data-stu-id="90790-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="90790-110">透過 PowerShell 即可擷取入口網站拓撲檢視背後的資訊。</span><span class="sxs-lookup"><span data-stu-id="90790-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="90790-111">這項功能可讓您活用拓撲資訊，因為資料可供其他工具取用以建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="90790-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="90790-112">系統會根據兩項關聯性建立彼此間聯繫關係的模型。</span><span class="sxs-lookup"><span data-stu-id="90790-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="90790-113">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="90790-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="90790-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="90790-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="90790-115">下列清單是查詢拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="90790-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="90790-116">**名稱** - 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="90790-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="90790-117">**識別碼** - 資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="90790-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="90790-118">**位置** - 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="90790-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="90790-119">**關聯** - 與參考物件之關聯的清單。</span><span class="sxs-lookup"><span data-stu-id="90790-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="90790-120">**名稱** - 所參考資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="90790-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="90790-121">**resourceId** - resourceId 是關聯中所參考資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="90790-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="90790-122">**associationType** - 這個值會參考子物件與父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="90790-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="90790-123">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="90790-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90790-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="90790-124">Before you begin</span></span>

<span data-ttu-id="90790-125">在此案例中，您會使用 `Get-AzureRmNetworkWatcherTopology` Cmdlet 來擷取拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="90790-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="90790-126">另有一篇文章說明如何[使用 REST API 擷取網路拓撲](network-watcher-topology-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="90790-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="90790-127">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="90790-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="90790-128">案例</span><span class="sxs-lookup"><span data-stu-id="90790-128">Scenario</span></span>

<span data-ttu-id="90790-129">本文涵蓋的案例會擷取指定資源群組的拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="90790-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="90790-130">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="90790-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="90790-131">第一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="90790-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="90790-132">`$networkWatcher` 變數會傳遞至 `Get-AzureRmNetworkWatcherTopology` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="90790-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="90790-133">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="90790-133">Retrieve topology</span></span>

<span data-ttu-id="90790-134">`Get-AzureRmNetworkWatcherTopology` Cmdlet 會擷取指定資源群組的拓撲。</span><span class="sxs-lookup"><span data-stu-id="90790-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="90790-135">結果</span><span class="sxs-lookup"><span data-stu-id="90790-135">Results</span></span>

<span data-ttu-id="90790-136">所傳回的結果有屬性名稱「資源」，其中包含 `Get-AzureRmNetworkWatcherTopology` Cmdlet 的 json 回應主體。</span><span class="sxs-lookup"><span data-stu-id="90790-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="90790-137">回應包含網路安全性群組中的資源和其關聯 (也就是包含、相關聯)。</span><span class="sxs-lookup"><span data-stu-id="90790-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="90790-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90790-138">Next steps</span></span>

<span data-ttu-id="90790-139">若要了解如何利用 Power BI 將 NSG 流量記錄視覺化，請瀏覽[利用 Power BI 將 NSG 流量記錄視覺](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="90790-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


