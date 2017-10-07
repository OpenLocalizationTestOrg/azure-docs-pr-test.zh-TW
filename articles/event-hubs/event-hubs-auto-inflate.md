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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>自動相應增加 Azure 事件中樞輸送量單位

## <a name="overview"></a>概觀

Azure 事件中樞為可高度擴充的資料串流平台。 因此，事件中心的客戶通常會增加其用法上架 toohello 服務之後。 這類量增加時需要增加 hello 預定的輸送量單位 (TUs) tooscale 事件中心，和處理較大傳送速率。 hello*自動擴大*事件中心的功能會自動依據 hello TUs toomeet 使用需要的數目。 提升 TU 能避免節流案例，在這些案例中：

* 資料輸入速率會超過所設定的 TU。
* 資料輸出要求速率會超過所設定的 TU。

## <a name="how-auto-inflate-works"></a>自動擴充的運作方式

事件中樞的流量會受到輸送量單位控制。 單一 TU 可允許每秒 1 MB 的輸入，以及兩倍數量的輸出。 標準事件中樞可以設定為 1-20 個輸送量單位。 自動擴大可讓您 toostart hello 最小必要的輸送量單位的小型。 然後 hello 功能自動縮放 toohello 的需要根據您的流量 hello 增加輸送量單位的最大限制。 自動擴大提供下列優點 hello:

- 有效率地調整機制 toostart 小型和為您的向上延展成長。
- 自動縮放表單 toohello 指定時間的上限而不會節流的問題。
- 多個控制縮放比例，因為您負責控制何時和多少 tooscale。

## <a name="enable-auto-inflate-on-a-namespace"></a>在命名空間上啟用自動擴充

您可以啟用或停用 使用下列方法 hello 命名空間上的 自動擴大：

1. hello [Azure 入口網站](https://portal.azure.com)。
2. Azure Resource Manager 範本。

### <a name="enable-auto-inflate-through-hello-portal"></a>透過 hello 入口網站中啟用 自動擴大

建立事件中樞命名空間時，您可以啟用命名空間上的 hello 自動增加功能：
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

啟用此選項時，您可以於開始時使用較小的輸送量單位，並隨著使用量需求的提升進行相應增加。 hello 擴大上限不會影響定價，會視 hello TUs 每小時使用的數目。

您也可以啟用自動擴大使用 hello**標尺**hello hello 入口網站中 [設定] 刀鋒視窗上的選項：
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本啟用自動擴充

您可以在 Azure Resource Manager 範本部署期間啟用自動擴充。 比方說，集 hello`isAutoInflateEnabled`屬性太**true**並設定`maximumThroughputUnits`too10。

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

Hello 完成範本，請參閱 hello[建立事件中樞命名空間，並啟用擴大](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate)GitHub 上的範本。

## <a name="next-steps"></a>後續步驟

您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
