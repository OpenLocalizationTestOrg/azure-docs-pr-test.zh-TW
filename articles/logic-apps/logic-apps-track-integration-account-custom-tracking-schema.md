---
title: "追蹤結構描述 b2b aaaCustom 監視-Azure 邏輯應用程式 |Microsoft 文件"
description: "建立自訂追蹤結構描述 toomonitor B2B 訊息從您的 Azure 整合帳戶中的交易。"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>讓您完成的工作流程，端對端追蹤 toomonitor
有內建的追蹤可供您啟用您不同部分的企業對企業工作流程，例如追蹤 AS2 或 X12 訊息。 當您建立包含邏輯應用程式、 BizTalk Server、 SQL Server 或任何其他層級的工作流程時，您可以啟用自訂的追蹤記錄的事件，從您的工作流程 hello 開頭 toohello 結尾。 

本主題提供您可以使用 hello 層級中，外部應用程式邏輯的自訂程式碼。 

## <a name="custom-tracking-schema"></a>自訂追蹤結構描述
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| sourceType |   | Hello 執行來源的類型。 允許的值為 **Microsoft.Logic/workflows** 和 **custom**。 (必要) |
| 來源 |   | 如果 hello 來源類型為**Microsoft.Logic/workflows**，hello 來源資訊需要 toofollow 這個結構描述。 如果 hello 來源類型為**自訂**，hello 結構描述是 JToken。 (必要) |
| systemId | String | 邏輯應用程式系統識別碼。 (必要) |
| runId | String | 邏輯應用程式執行識別碼。 (必要) |
| operationName | String | Hello 作業 （例如，動作或觸發程序） 的名稱。 (必要) |
| repeatItemScopeName | String | 如果 hello 動作內重複項目名稱`foreach` / `until`迴圈。 (必要) |
| repeatItemIndex | Integer | Hello 動作是否內`foreach` / `until`迴圈。 指出 hello 重複的項目索引。 (必要) |
| trackingId | String | Toocorrelate hello 訊息追蹤識別碼。 (選用) |
| correlationId | String | Toocorrelate hello 訊息相互關聯識別碼。 (選用) |
| clientRequestId | String | 用戶端可以將它填入 toocorrelate 訊息。 (選用) |
| eventLevel |   | Hello 事件層級。 (必要) |
| eventTime |   | 以 UTC 格式 YYYY-MM-DDTHH:MM:SS.00000Z hello 事件的時間。 (必要) |
| recordType |   | Hello 追蹤記錄的類型。 允許的值為 **custom**。 (必要) |
| record |   | 自訂記錄類型。 允許的格式為 JToken。 (必要) |

## <a name="b2b-protocol-tracking-schemas"></a>B2B 通訊協定追蹤結構描述
如需 B2B 通訊協定追蹤結構描述的相關資訊，請參閱︰
* [AS2 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [X12 追蹤結構描述](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>後續步驟
* [深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。   
* 深入了解[追蹤 hello Operations Management Suite 入口網站中的 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。
* 深入了解 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。
