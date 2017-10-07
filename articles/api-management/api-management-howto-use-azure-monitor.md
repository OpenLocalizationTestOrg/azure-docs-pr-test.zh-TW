---
title: "API 管理的 Azure 監視 aaaMonitor |Microsoft 文件"
description: "了解如何 toomonitor Azure API 管理服務使用 Azure 監視器。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>使用 Azure 監視器監視 API 管理
Azure 監視器是一項 Azure 服務，可提供單一來源來讓您監視所有 Azure 資源。 Azure 監視，您可以視覺化方式檢視、 查詢、 路由、 封存，並採取動作上 hello 衡量標準及來自 Azure API 管理等的資源記錄。 

hello 下列影片示範如何使用 Azure 監視的應用程式開發介面管理 toomonitor。 如需 Azure 監視器的詳細資訊，請參閱[開始使用 Azure 監視器]。 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>度量
API 管理目前發出五個度量，我們計劃 tooadd hello 未來在多個。 這些度量會發出每隔一分鐘，讓您附近 hello 狀態和您的應用程式開發介面的健全狀況的即時可視性。 以下是 hello 度量資訊的摘要：
* 閘道要求總數： hello 期間內要求的應用程式開發介面的 hello 數目。 
* 成功的閘道要求： hello API 的要求數目接收到成功的 HTTP 回應碼，包括 304、 307 和小於 301 (例如，200) 的任何項目。 
* 失敗的閘道要求： hello API 的要求數目收到錯誤的 HTTP 回應碼，包括 400 和 500 大於任何項目。
* 未經授權的閘道要求： hello API 的要求數目收到包括 401、 403 和 429 HTTP 回應碼。 
* 其他閘道要求： hello API 的要求數目收到不屬於 tooany hello 前面類別 (例如，418) 的 HTTP 回應碼。

您可以在 API 管理服務中存取計量，或在 Azure 監視器中存取所有 Azure 資源的計量。 在您的 API 管理服務 tooview 度量：
1. 開啟 hello Azure 入口網站。
2. 移 tooyour API 管理服務。
3. 按一下 [計量]。

![[計量] 刀鋒視窗][metrics-blade]

如需有關如何 toouse 度量資訊，請參閱[概觀的度量]。

## <a name="activity-logs"></a>活動記錄檔
活動記錄檔提供深入了解 API 管理服務執行的 hello 操作。 此記錄以前稱為「稽核記錄」或「作業記錄」。 使用活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 的 API 管理服務。 

> [!NOTE]
> 活動記錄檔不包括讀取 (GET) 作業或執行中作業 hello 傳統發行者入口網站，或使用 hello 原始的管理 Api。

您可以在 API 管理服務中存取活動記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。 tooview 活動記錄在您的 API 管理服務：
1. 開啟 hello Azure 入口網站。
2. 移 tooyour API 管理服務。
3. 按一下 [活動記錄]。

![[活動記錄] 刀鋒視窗][activity-logs-blade]

如需有關如何 toouse 度量資訊，請參閱[活動記錄概觀]。

## <a name="alerts"></a>Alerts
您可以設定 tooreceive 根據度量和活動記錄檔的警示。 Azure 監視器可讓您 tooconfigure 警示 toodo hello，下列情況觸發：

* 傳送電子郵件通知
* 呼叫 Webhook
* 叫用 Azure 邏輯應用程式

您可以在 API 管理服務或 Azure 監視器中設定警示規則。 tooconfigure API 管理中： 
1. 開啟 hello Azure 入口網站。
2. 移 tooyour API 管理服務。
3. 按一下 [警示規則]。

![警示規則刀鋒視窗][alert-rules-blade]

如需有關使用警示的詳細資訊，請參閱[警示概觀]。

## <a name="diagnostic-logs"></a>診斷記錄檔
診斷記錄可提供豐富的作業與錯誤資訊，這些資訊對於稽核和疑難排解用途來說很重要。 診斷記錄與活動記錄不同。 活動記錄檔提供深入了解您的 Azure 資源執行的 hello 操作。 診斷記錄能讓您了解資源自行執行的作業。

API 管理目前提供診斷與每個項目具有下列結構的 hello 要求個別應用程式開發介面的相關記錄 （每小時批次）：

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

您可以在 API 管理服務中存取診斷記錄，或在 Azure 監視器中存取所有 Azure 資源的記錄。 tooview API 管理服務中的診斷記錄：
1. 開啟 hello Azure 入口網站。
2. 移 tooyour API 管理服務。
3. 按一下 [診斷記錄]。

![診斷記錄檔刀鋒視窗][diagnostic-logs-blade]

如需有關如何 toouse 度量資訊，請參閱[診斷記錄概觀]。

## <a name="next-step"></a>後續步驟

* [開始使用 Azure 監視器]
* [概觀的度量]
* [活動記錄概觀]
* [診斷記錄概觀]
* [警示概觀]

[開始使用 Azure 監視器]: ../monitoring-and-diagnostics/monitoring-get-started.md
[概觀的度量]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[活動記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[診斷記錄概觀]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[警示概觀]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
