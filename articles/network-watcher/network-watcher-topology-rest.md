---
title: "aaaView Azure 網路監看員拓樸-REST API |Microsoft 文件"
description: "本文將說明如何 toouse 會 REST API tooquery 網路拓撲。"
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="f4171-103">使用 REST API 檢視網路監看員拓撲</span><span class="sxs-lookup"><span data-stu-id="f4171-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f4171-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4171-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="f4171-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f4171-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="f4171-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f4171-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="f4171-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f4171-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="f4171-108">網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="f4171-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="f4171-109">在 hello 入口網站，此視覺效果會自動顯示 tooyou。</span><span class="sxs-lookup"><span data-stu-id="f4171-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="f4171-110">hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。</span><span class="sxs-lookup"><span data-stu-id="f4171-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="f4171-111">這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="f4171-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="f4171-112">hello 互連的方式是在兩個關聯性模型化。</span><span class="sxs-lookup"><span data-stu-id="f4171-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="f4171-113">**內含項目** - 範例︰VNet 包含子網路包含 NIC</span><span class="sxs-lookup"><span data-stu-id="f4171-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="f4171-114">**相關聯** - 範例︰NIC 與 VM 相關聯</span><span class="sxs-lookup"><span data-stu-id="f4171-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="f4171-115">hello 下列清單會查詢 hello 拓撲 REST API 時所傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="f4171-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="f4171-116">**名稱**-hello hello 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="f4171-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="f4171-117">**識別碼**-hello hello 資源的 uri。</span><span class="sxs-lookup"><span data-stu-id="f4171-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="f4171-118">**位置**-hello hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="f4171-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="f4171-119">**關聯**-一份關聯 toohello 參考物件。</span><span class="sxs-lookup"><span data-stu-id="f4171-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="f4171-120">**名稱**-hello hello 名稱所參考的資源。</span><span class="sxs-lookup"><span data-stu-id="f4171-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="f4171-121">**resourceId** -hello resourceId 為 hello 參考 hello 關聯中的 hello 資源 uri。</span><span class="sxs-lookup"><span data-stu-id="f4171-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="f4171-122">**associationType** -這個值會參考 hello hello 子物件 hello 父系之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f4171-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="f4171-123">有效值為 [包含] 或 [相關聯]。</span><span class="sxs-lookup"><span data-stu-id="f4171-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f4171-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="f4171-124">Before you begin</span></span>

<span data-ttu-id="f4171-125">在此案例中，您可以擷取 hello 拓撲資訊。</span><span class="sxs-lookup"><span data-stu-id="f4171-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="f4171-126">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="f4171-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="f4171-127">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="f4171-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f4171-128">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="f4171-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="f4171-129">案例</span><span class="sxs-lookup"><span data-stu-id="f4171-129">Scenario</span></span>

<span data-ttu-id="f4171-130">hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。</span><span class="sxs-lookup"><span data-stu-id="f4171-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f4171-131">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="f4171-131">Log in with ARMClient</span></span>

<span data-ttu-id="f4171-132">登入 tooarmclient 與您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="f4171-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="f4171-133">擷取拓撲</span><span class="sxs-lookup"><span data-stu-id="f4171-133">Retrieve topology</span></span>

<span data-ttu-id="f4171-134">hello hello REST API 中的下列範例要求 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4171-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="f4171-135">hello 範例是參數化的 tooallow 為建立範例的彈性。</span><span class="sxs-lookup"><span data-stu-id="f4171-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="f4171-136">以它們周圍的 \< \> 取代所有值。</span><span class="sxs-lookup"><span data-stu-id="f4171-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="f4171-137">下列回應 hello 是縮短回應時，會傳回的範例擷取的資源群組拓撲：</span><span class="sxs-lookup"><span data-stu-id="f4171-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f4171-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4171-138">Next steps</span></span>

<span data-ttu-id="f4171-139">了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f4171-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

