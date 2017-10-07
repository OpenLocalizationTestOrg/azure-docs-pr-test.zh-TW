---
title: "Azure 事件中樞輸送量單位 aaaAutomatically 調整 |Microsoft 文件"
description: "命名空間 tooautomatically 標尺總輸送量單位上啟用 自動擴大"
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
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="d02ef-103">自動相應增加 Azure 事件中樞輸送量單位</span><span class="sxs-lookup"><span data-stu-id="d02ef-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="d02ef-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d02ef-104">Overview</span></span>

<span data-ttu-id="d02ef-105">Azure 事件中樞為可高度擴充的資料串流平台。</span><span class="sxs-lookup"><span data-stu-id="d02ef-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="d02ef-106">因此，事件中心的客戶通常會增加其用法上架 toohello 服務之後。</span><span class="sxs-lookup"><span data-stu-id="d02ef-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="d02ef-107">這類量增加時需要增加 hello 預定的輸送量單位 (TUs) tooscale 事件中心，和處理較大傳送速率。</span><span class="sxs-lookup"><span data-stu-id="d02ef-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="d02ef-108">hello*自動擴大*事件中心的功能會自動依據 hello TUs toomeet 使用需要的數目。</span><span class="sxs-lookup"><span data-stu-id="d02ef-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="d02ef-109">提升 TU 能避免節流案例，在這些案例中：</span><span class="sxs-lookup"><span data-stu-id="d02ef-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="d02ef-110">資料輸入速率會超過所設定的 TU。</span><span class="sxs-lookup"><span data-stu-id="d02ef-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="d02ef-111">資料輸出要求速率會超過所設定的 TU。</span><span class="sxs-lookup"><span data-stu-id="d02ef-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="d02ef-112">自動擴充的運作方式</span><span class="sxs-lookup"><span data-stu-id="d02ef-112">How Auto-inflate works</span></span>

<span data-ttu-id="d02ef-113">事件中樞的流量會受到輸送量單位控制。</span><span class="sxs-lookup"><span data-stu-id="d02ef-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="d02ef-114">單一 TU 可允許每秒 1 MB 的輸入，以及兩倍數量的輸出。</span><span class="sxs-lookup"><span data-stu-id="d02ef-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="d02ef-115">標準事件中樞可以設定為 1-20 個輸送量單位。</span><span class="sxs-lookup"><span data-stu-id="d02ef-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="d02ef-116">自動擴大可讓您 toostart hello 最小必要的輸送量單位的小型。</span><span class="sxs-lookup"><span data-stu-id="d02ef-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="d02ef-117">然後 hello 功能自動縮放 toohello 的需要根據您的流量 hello 增加輸送量單位的最大限制。</span><span class="sxs-lookup"><span data-stu-id="d02ef-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="d02ef-118">自動擴大提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d02ef-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="d02ef-119">有效率地調整機制 toostart 小型和為您的向上延展成長。</span><span class="sxs-lookup"><span data-stu-id="d02ef-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="d02ef-120">自動縮放表單 toohello 指定時間的上限而不會節流的問題。</span><span class="sxs-lookup"><span data-stu-id="d02ef-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="d02ef-121">多個控制縮放比例，因為您負責控制何時和多少 tooscale。</span><span class="sxs-lookup"><span data-stu-id="d02ef-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="d02ef-122">在命名空間上啟用自動擴充</span><span class="sxs-lookup"><span data-stu-id="d02ef-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="d02ef-123">您可以啟用或停用 使用下列方法 hello 命名空間上的 自動擴大：</span><span class="sxs-lookup"><span data-stu-id="d02ef-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="d02ef-124">hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d02ef-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d02ef-125">Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d02ef-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="d02ef-126">透過 hello 入口網站中啟用 自動擴大</span><span class="sxs-lookup"><span data-stu-id="d02ef-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="d02ef-127">建立事件中樞命名空間時，您可以啟用命名空間上的 hello 自動增加功能：</span><span class="sxs-lookup"><span data-stu-id="d02ef-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="d02ef-128">啟用此選項時，您可以於開始時使用較小的輸送量單位，並隨著使用量需求的提升進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="d02ef-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="d02ef-129">hello 擴大上限不會影響定價，會視 hello TUs 每小時使用的數目。</span><span class="sxs-lookup"><span data-stu-id="d02ef-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="d02ef-130">您也可以啟用自動擴大使用 hello**標尺**hello hello 入口網站中 [設定] 刀鋒視窗上的選項：</span><span class="sxs-lookup"><span data-stu-id="d02ef-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="d02ef-131">使用 Azure Resource Manager 範本啟用自動擴充</span><span class="sxs-lookup"><span data-stu-id="d02ef-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="d02ef-132">您可以在 Azure Resource Manager 範本部署期間啟用自動擴充。</span><span class="sxs-lookup"><span data-stu-id="d02ef-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="d02ef-133">比方說，集 hello`isAutoInflateEnabled`屬性太**true**並設定`maximumThroughputUnits`too10。</span><span class="sxs-lookup"><span data-stu-id="d02ef-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="d02ef-134">Hello 完成範本，請參閱 hello[建立事件中樞命名空間，並啟用擴大](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate)GitHub 上的範本。</span><span class="sxs-lookup"><span data-stu-id="d02ef-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d02ef-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d02ef-135">Next steps</span></span>

<span data-ttu-id="d02ef-136">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="d02ef-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="d02ef-137">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="d02ef-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d02ef-138">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="d02ef-138">Create an Event Hub</span></span>](event-hubs-create.md)
