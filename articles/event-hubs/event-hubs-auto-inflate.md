---
title: "自動相應增加 Azure 事件中樞輸送量單位 | Microsoft Docs"
description: "在命名空間上啟用自動擴充以自動相應增加輸送量單位"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="ee1e6-103">自動相應增加 Azure 事件中樞輸送量單位</span><span class="sxs-lookup"><span data-stu-id="ee1e6-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="ee1e6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ee1e6-104">Overview</span></span>

<span data-ttu-id="ee1e6-105">Azure 事件中樞為可高度擴充的資料串流平台。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="ee1e6-106">因此，事件中樞客戶通常會在上線至該服務之後提升他們的使用量。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="ee1e6-107">提升使用量必須提升預先設定的輸送量單位 (TU)，以調整事件中樞並處理較大的傳輸速率。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="ee1e6-108">事件中樞的「自動擴充」功能可以自動相應增加 TU 數目以符合使用量需求。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="ee1e6-109">提升 TU 能避免節流案例，在這些案例中：</span><span class="sxs-lookup"><span data-stu-id="ee1e6-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="ee1e6-110">資料輸入速率會超過所設定的 TU。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="ee1e6-111">資料輸出要求速率會超過所設定的 TU。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="ee1e6-112">自動擴充的運作方式</span><span class="sxs-lookup"><span data-stu-id="ee1e6-112">How Auto-inflate works</span></span>

<span data-ttu-id="ee1e6-113">事件中樞的流量會受到輸送量單位控制。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="ee1e6-114">單一 TU 可允許每秒 1 MB 的輸入，以及兩倍數量的輸出。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="ee1e6-115">標準事件中樞可以設定為 1-20 個輸送量單位。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="ee1e6-116">自動擴充可讓您於開始時使用最小的必要輸送量單位。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="ee1e6-117">該功能接著會根據流量的提升，自動擴充至您所需的輸送量單位上限。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="ee1e6-118">自動擴充提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ee1e6-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="ee1e6-119">能視需求進行相應增加的有效擴充機制。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="ee1e6-120">自動擴充至指定的上限，以避免產生節流問題。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="ee1e6-121">透過控制調整的時機和程度，來取得更多擴充上的控制。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="ee1e6-122">在命名空間上啟用自動擴充</span><span class="sxs-lookup"><span data-stu-id="ee1e6-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="ee1e6-123">您可以使用下列其中一種方法，在命名空間上啟用或停用自動擴充：</span><span class="sxs-lookup"><span data-stu-id="ee1e6-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="ee1e6-124">[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ee1e6-125">Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="ee1e6-126">透過入口網站啟用自動擴充</span><span class="sxs-lookup"><span data-stu-id="ee1e6-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="ee1e6-127">您可以在建立事件中樞命名空間時，在命名空間上啟用自動擴充功能：</span><span class="sxs-lookup"><span data-stu-id="ee1e6-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="ee1e6-128">啟用此選項時，您可以於開始時使用較小的輸送量單位，並隨著使用量需求的提升進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="ee1e6-129">擴充的上限並不會影響價格，因為價格是依每小時所使用的 TU 數目來計算。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="ee1e6-130">您也可以使用入口網站中 [設定] 刀鋒視窗上的 [調整] 選項來啟用自動擴充：</span><span class="sxs-lookup"><span data-stu-id="ee1e6-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="ee1e6-131">使用 Azure Resource Manager 範本啟用自動擴充</span><span class="sxs-lookup"><span data-stu-id="ee1e6-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="ee1e6-132">您可以在 Azure Resource Manager 範本部署期間啟用自動擴充。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="ee1e6-133">例如，將 `isAutoInflateEnabled` 屬性設定為 **true**，並將 `maximumThroughputUnits` 設定為 10。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="ee1e6-134">如需完整的範本，請參閱 GitHub 上的[建立事件中樞命名空間並啟用擴充](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) \(英文\) 範本。</span><span class="sxs-lookup"><span data-stu-id="ee1e6-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee1e6-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee1e6-135">Next steps</span></span>

<span data-ttu-id="ee1e6-136">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ee1e6-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ee1e6-137">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="ee1e6-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ee1e6-138">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="ee1e6-138">Create an Event Hub</span></span>](event-hubs-create.md)
