---
title: "aaaUse 自動調整規模動作 toosend 電子郵件和 webhook 警示通知。 | Microsoft Docs"
description: "請參閱 toouse 自動調整規模動作 toocall web Url 或 Azure 監視器中傳送電子郵件通知的方式。 "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>使用 Azure 監視器 」 中的自動調整規模動作 toosend 電子郵件和 webhook 警示通知
本文將告訴您如何設定觸發程序，讓您可以根據 Azure 中的自動調整動作呼叫特定的 Web URl 或傳送電子郵件。  

## <a name="webhooks"></a>Webhook
Webhook 允許 tooroute hello Azure 的警示通知 tooother 系統後置處理或自訂通知。 例如，可處理連入 web 要求 toosend SMS，記錄錯誤，路由 hello 警示 tooservices 通知小組使用聊天室訊息服務，等 hello webhook URI 必須是有效的 HTTP 或 HTTPS 端點。

## <a name="email"></a>電子郵件
可以 tooany 有效的電子郵件地址傳送電子郵件。 系統也會通知系統管理員和共同管理員的 hello hello 規則執行所在的訂用帳戶。

## <a name="cloud-services-and-web-apps"></a>雲端服務和 Web Apps
您可以在選擇 hello Azure 入口網站從雲端服務和伺服器陣列 （Web 應用程式）。

* 選擇 hello**縮放**度量。

![調整依據](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>虛擬機器擴展集
對於使用 Resource Manager 建立的較新虛擬機器 (虛擬機器擴展集)，您可以使用 REST API、Resource Manager 範本、PowerShell 和 CLI 設定此項目。 目前尚無入口網站介面。
使用 REST API hello 或資源管理員範本時，包含下列選項的 hello hello 通知項目。

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| 欄位 | 是否為強制？ | 說明 |
| --- | --- | --- |
| operation |yes |值必須是 [調整] |
| sendToSubscriptionAdministrator |yes |值必須是 "true" 或 "false" |
| sendToSubscriptionCoAdministrators |yes |值必須是 "true" 或 "false" |
| customEmails |yes |值可以是 null 或電子郵件的字串陣列 |
| Webhook |yes |值可以是 null 或有效的 Uri |
| serviceUri |yes |有效的 https Uri |
| properties |yes |值必須是空的 {}，或可以包含索引鍵-值組 |

## <a name="authentication-in-webhooks"></a>Webhook 中的驗證
hello webhook 可以驗證使用權杖型驗證，您將 hello webhook URI 儲存為查詢參數的權杖識別碼。 例如，https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>自動調整通知 Webhook 承載結構描述
當產生 hello 自動調整規模通知時，hello 下列中繼資料包含在 hello webhook 裝載：

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| 欄位 | 是否為強制？ | 說明 |
| --- | --- | --- |
| status |yes |表示所產生的自動調整規模動作 hello 狀態 |
| operation |yes |若執行個體增加，它會「相應放大」，若執行個體減少，它會「相應縮小」。 |
| context |yes |hello 自動調整規模動作內容 |
| timestamp |yes |觸發 hello 自動調整規模動作時的時間戳記 |
| id |是 |資源管理員識別碼 hello 自動調整規模設定 |
| 名稱 |是 |hello hello 自動調整規模設定名稱 |
| 詳細資料 |是 |Hello 自動調整規模服務的 hello 動作的說明，並 hello 變更 hello 執行個體計數 |
| subscriptionId |是 |已縮放的 hello 目標資源的訂用帳戶 ID |
| resourceGroupName |是 |已縮放的 hello 目標資源的資源群組名稱 |
| resourceName |是 |已縮放的 hello 目標資源的名稱 |
| resourceType |是 |hello 三個支援的值:"microsoft.classiccompute/domainnames/slots/roles"-雲端服務角色、 「 microsoft.compute/virtualmachinescalesets"-虛擬機器擴展集和 「 Microsoft.Web/serverfarms"-Web 應用程式 |
| resourceId |是 |已縮放的 hello 目標資源的資源管理員識別碼 |
| portalLink |是 |Azure 入口網站的連結 toohello 摘要 頁面上的 hello 目標資源 |
| oldCapacity |是 |hello 目前 （舊） 執行個體計數時自動調整規模所需的調整規模動作 |
| newCapacity |是 |hello 自動調整規模調整 hello 資源太新執行個體計數|
| 屬性 |否 |選用。 <索引鍵, 值> 組 (例如，字典 <字串, 字串>)。 hello 屬性欄位是選擇性的。 您可以在自訂使用者介面或邏輯基礎的應用程式工作流程中，輸入索引鍵和值，可使用 hello 裝載傳遞。 Toopass 自訂屬性 back toohello 外寄的 webhook 呼叫的替代方式是 toouse hello webhook URI 本身 （作為查詢參數） |
