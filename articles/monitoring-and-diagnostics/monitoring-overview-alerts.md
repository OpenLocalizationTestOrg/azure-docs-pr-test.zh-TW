---
title: "Microsoft Azure 和 Azure 監視器中的警示 aaaOverview |Microsoft 文件"
description: "警示 toomonitor Azure 資源度量、 事件或記錄檔可讓您和您指定的條件符合時收到通知。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Microsoft Azure 中的警示是什麼？
本文說明的 hello 各種來源的警示，在 Microsoft Azure 中，有哪些 hello 這些警示、 其優點和 tooget 如何開始使用它們的用途。 它特別適用於 tooAzure 監視器，但 tooother 服務提供的指標，以及警示。 警示提供監視在 Azure 中，透過資料 tooconfigure 條件允許您和變成收到 hello 條件符合 hello 最新監視資料的通知的方法。

## <a name="taxonomy-of-azure-alerts"></a>Azure 警示的分類
Azure 會使用 hello 下列條款 toodescribe 警示和它們的函式：
* **警示** - 符合時會啟動之準則 (一或多個規則或條件) 的定義。
* **Active** -hello 狀態時 hello 符合警示定義的準則。
* **解決**-hello 狀態時 hello 之後先前有已經符合不再符合警示定義的準則。
* **通知**-hello 點根據開成為作用中警示的動作。
* **動作**-傳送的特定呼叫 tooa 接收者 （例如，以電子郵件傳送地址或張貼 tooa webhook URL） 的通知。 通知通常可觸發多個動作。

## <a name="alerts-in-different-azure-services"></a>不同 Azure 服務中的警示
警示可跨數個 Azure 監視服務使用。 如需有關如何及何時 toouse 這些服務、 詳細[請參閱本文章](./monitoring-overview.md)。 以下是 hello 警示類型的分析提供跨 Azure:

| 服務 | 警示類型 | 支援的服務 | 說明 |
|---|---|---|---|
| Azure 監視器 | [度量警示](./insights-alerts-portal.md) | [Azure 監視器支援的度量](./monitoring-supported-metrics.md) | 任何平台層級度量符合特定條件時收到通知 （例如，在 VM 上的 CPU %大於 90 hello 過去 5 分鐘）。 |
| Azure 監視器 | [活動記錄警示](./monitoring-activity-log-alerts.md) | Azure Resource Manager 中可用的所有資源類型 | 收到通知時，任何新事件中 hello [Azure 活動記錄檔](./monitoring-overview-activity-logs.md)符合特定條件，（比方說，「 刪除 VM 」 作業中發生 myProductionResourceGroup 或新的服務健全狀況事件，以做為 「 作用中 」 時hello 狀態會出現）。 |
| Application Insights | [度量警示](../application-insights/app-insights-alerts.md) | 任何應用程式檢測 toosend 資料 tooApplication Insights | 當任何應用程式層級度量符合特定條件時收到通知 (例如伺服器回應時間大於 2 秒)。 |
| Application Insights | [Web 測試警示](../application-insights/app-insights-monitor-web-app-availability.md) | 任何網站檢測 toosend 資料 tooApplication Insights | 當網站的可用性或回應能力低於預期時收到通知。 |
| Log Analytics | [Log Analytics 警示](../log-analytics/log-analytics-alerts.md) | 任何服務中記錄分析設定 toosend 資料 | 當 Log Analytics 搜尋查詢高於度量及/或事件資料符合特定準則時收到通知。 |

## <a name="alerts-on-azure-monitor-data"></a>Azure 監視器資料的相關警示
Azure 監視器中可用資料的警示類型有兩種：度量警示和活動記錄警示。

* **度量的警示**-當 hello 值，指定的度量超出您所指定的臨界值時，此警示觸發程序。 hello 警示產生通知，當 hello 警示 「 啟動 」 （當跨越 hello 臨界值，且符合 hello 警示條件），以及當它 「 已解決 」 （當 hello 閾值已超過一次，且不再符合 hello 條件）。 Azure 監視器所支援的可用度量清單會不斷成長，如需此清單，請參閱 [Azure 監視器上支援的度量清單](monitoring-supported-metrics.md)。
* **活動記錄警示** - 當產生符合您已指派之篩選準則的活動記錄事件時會觸發資料流記錄警示。 這些警示會有一個狀態，「 啟動，」 因為 hello 警示引擎只會套用 hello 篩選準則 tooany 新事件。 這些警示可以新的服務健全狀況事件發生時，會使用的 toobecome 收到通知，或當使用者或應用程式執行的作業，在您的訂閱，例如，「 刪除虛擬機器 」。

可透過 Azure 監視的診斷記錄資料，建議路由 hello 資料到記錄分析，並使用記錄分析警示。 hello 圖摘要說明和中資料的 Azure 監視，在概念上，如何您可以從該資料警示的來源。

![警示的說明](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>如何收到 Azure 監視器警示的通知？
在過去，Azure 的警示來自不同的服務，各自使用其專屬的內建通知方法。 從現在開始，Azure 監視器提供可重複使用的通知群組，稱為動作群組。 動作群組會指定一組接收者通知-任意數目的電子郵件地址、 電話號碼 （如 SMS) 或 webhook Url--及任何參考 hello 動作群組啟動警示的時間所有接收者都接收該通知。 這可讓您 tooreuse 接收者 （例如，您在呼叫工程師清單） 的群組跨多個警示的物件。 目前，只有活動記錄警示可以使用動作群組，但未來將有數個其他 Azure 警示類型也可以使用動作群組。

動作群組支援藉由公佈 tooa webhook URL 中加入 tooemail 位址和 SMS 數字的通知。 如此即可啟用自動化和修復，例如使用：
    - Azure 自動化 Runbook
    - Azure Function
    - Azure 邏輯應用程式
    - 第三方服務

度量警示尚無法使用動作群組。 在個別度量警示上，您可以設定通知：
* 傳送電子郵件通知 toohello 服務系統管理員、 tooco 系統管理員或 tooadditional 電子郵件地址所指定。
* 呼叫可讓您 webhook toolaunch 其他自動化動作。

## <a name="next-steps"></a>後續步驟
使用下列項目取得有關警示規則和設定這些規則的資訊：

* 深入了解[計量](monitoring-overview-metrics.md)
* [透過 Azure 入口網站設定計量警示](insights-alerts-portal.md)
* [透過 PowerShell 設定計量警示](insights-alerts-powershell.md)
* [透過命令列介面 (CLI) 設定計量警示](insights-alerts-command-line-interface.md)
* [透過 Azure 監視器 REST API 設定計量警示](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* 深入了解[活動記錄](monitoring-overview-activity-logs.md)
* [透過 Azure 入口網站設定活動記錄警示](monitoring-activity-log-alerts.md)
* [透過 Resource Manager 設定活動記錄警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* 檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)
* 深入了解[服務通知](monitoring-service-notifications.md)
* 深入了解[動作群組](monitoring-action-groups.md)
