---
title: "aaaAS2 追蹤結構描述 B2B 監視-Azure 邏輯應用程式 |Microsoft 文件"
description: "使用 AS2 追蹤結構描述 toomonitor B2B 訊息從您的 Azure 整合帳戶中的交易。"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>啟動或啟用的 AS2 訊息和 Mdn toomonitor 成功、 錯誤和訊息屬性追蹤
您可以使用這些 AS2 追蹤結構描述您可以在您的 Azure 整合帳戶 toohelp 監視企業對企業 (B2B) 交易：

* AS2 訊息追蹤結構描述
* AS2 MDN 追蹤結構描述

## <a name="as2-message-tracking-schema"></a>AS2 訊息追蹤結構描述
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| senderPartnerName | String | AS2 訊息傳送者的夥伴名稱。 (選用) |
| receiverPartnerName | String | AS2 訊息接收者的夥伴名稱。 (選用) |
| as2To | String | AS2 訊息接收者的名稱，從 hello hello AS2 訊息標頭。 (必要) |
| as2From | String | AS2 訊息傳送者的名稱，從 hello hello AS2 訊息標頭。 (必要) |
| agreementName | String | 所解析的 hello AS2 協議 toowhich hello 訊息名稱。 (選用) |
| direction | String | 方向 hello 訊息流程、 接收或傳送。 (必要) |
| messageId | String | AS2 訊息識別碼，從 hello 標頭的 hello AS2 訊息 （選擇性） |
| dispositionType |String | 訊息處理通知 (MDN) 配置類型值。 (選用) |
| fileName | String | 檔案名稱，從 hello hello AS2 訊息標頭。 (選用) |
| isMessageFailed |Boolean | Hello AS2 訊息是否失敗。 (必要) |
| isMessageSigned | Boolean | Hello AS2 訊息是否簽署。 (必要) |
| isMessageEncrypted | Boolean | 是否已加密 hello AS2 訊息。 (必要) |
| isMessageCompressed |Boolean | 是否 hello AS2 訊息已壓縮。 (必要) |
| correlationMessageId | String | AS2 訊息識別碼、 toocorrelate Mdn 訊息。 (選用) |
| incomingHeaders |JToken 的字典 | 內送 AS2 訊息標頭詳細資料。 (選用) |
| outgoingHeaders |JToken 的字典 | 外寄 AS2 訊息標頭詳細資料。 (選用) |
| isNrrEnabled | Boolean | 如果不知道 hello 值，請使用預設值。 (必要) |
| isMdnExpected | Boolean | 如果不知道 hello 值，請使用預設值。 (必要) |
| mdnType | 例舉 | 允許的值為 **NotConfigured**、**Sync** 和 **Async**。 (必要) |

## <a name="as2-mdn-tracking-schema"></a>AS2 MDN 追蹤結構描述
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| senderPartnerName | String | AS2 訊息傳送者的夥伴名稱。 (選用) |
| receiverPartnerName | String | AS2 訊息接收者的夥伴名稱。 (選用) |
| as2To | String | 收到 hello AS2 訊息的夥伴名稱。 (必要) |
| as2From | String | 夥伴傳送嗨 AS2 訊息的人員名稱。 (必要) |
| agreementName | String | 所解析的 hello AS2 協議 toowhich hello 訊息名稱。 (選用) |
| direction |String | 方向 hello 訊息流程、 接收或傳送。 (必要) |
| messageId | String | AS2 訊息識別碼。 (選用) |
| originalMessageId |String | AS2 原始訊息識別碼。 (選用) |
| dispositionType | String | MDN 處置類型值。 (選用) |
| isMessageFailed |Boolean | Hello AS2 訊息是否失敗。 (必要) |
| isMessageSigned |Boolean | Hello AS2 訊息是否簽署。 (必要) |
| isNrrEnabled | Boolean | 如果不知道 hello 值，請使用預設值。 (必要) |
| StatusCode | 例舉 | 允許的值為 **Accepted**、**Rejected** 和 **AcceptedWithErrors**。 (必要) |
| micVerificationStatus | 例舉 | 允許的值為 **NotApplicable**、**Succeeded** 和 **Failed**。 (必要) |
| correlationMessageId | String | 相互關連識別碼。 原始的 hello 依現狀識別碼 (hello 為設定 MDN 的 hello 訊息的訊息識別碼)。 (選用) |
| incomingHeaders | JToken 的字典 | 指出內送訊息標頭詳細資料。 (選用) |
| outgoingHeaders |JToken 的字典 | 指出外寄訊息標頭詳細資料。 (選用) |

## <a name="next-steps"></a>後續步驟
* 深入了解 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。    
* [深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。   
* [深入了解 B2B 自訂追蹤結構描述](logic-apps-track-integration-account-custom-tracking-schema.md)。   
* 深入了解 [X12 追蹤結構描述](logic-apps-track-integration-account-x12-tracking-schema.md)。   
* 深入了解[追蹤 hello Operations Management Suite 入口網站中的 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。
