---
title: "aaaWhat 是服務健全狀況通知 |Microsoft 文件"
description: "服務健全狀況通知可讓您 tooview 服務健全狀況訊息發行 Microsoft azure。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>服務健康狀態通知
## <a name="overview"></a>概觀

本文章將示範如何使用 tooview 服務健全狀況通知 hello Azure 入口網站。

服務健全狀況通知可讓您 tooview 服務健全狀況發佈訊息 hello Azure 團隊可能會影響您的訂用帳戶底下的 hello 資源。 這些通知是一種活動的子類別記錄事件，也可以找到 hello 活動記錄 刀鋒視窗。 服務健全狀況通知可以是參考用訊息還是 hello 類別而採取動作。

服務健康狀態通知有五種類別：  

- **必要的動作：**從時間 tootime 我們可能會注意到尋常會發生在您的帳戶。 我們可能需要與您 tooremedy toowork 此項。 我們會傳送通知給您或是詳述 hello 動作必須 tootake 或 toocontact Azure 工程與方式的詳細資訊或支援。  
- **協助復原︰**事件已發生，且工程師確認您仍受到影響。 需要與您 toowork 工程直接 toobring 服務 toorestoration。  
- **事件：**影響事件的服務目前會影響一個或多個訂用帳戶中的 hello 資源。  
- **維護：**這是通知，通知您可能會影響一個或多個訂用帳戶下的 hello 資源計劃的維護活動。  
- **資訊：**從時間 tootime 我們可能會傳送通知給您有關潛在的最佳化可能有助於傳達 tooyou 改善資源使用率。  
- **安全性︰**緊急的安全性相關資訊，關係到 Azure 上正在執行的解決方案。

每個服務健全狀況通知將 hello 範圍和影響 tooyour 資源上執行詳細資料。 詳細資料包括：

屬性名稱 | 說明
-------- | -----------
通道 | 是 hello 下列值之一: 「 系統管理 」、 「 作業 」
correlationId | 通常是 hello 字串格式的 GUID。 事件與屬於相同超級動作通常會共用的 toohello hello 相同的相互關聯識別碼。
eventDataId | Hello 唯一識別碼的事件
eventName | Hello 標題的 hello 事件
層級 | Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」
resourceProviderName | Hello hello 資源提供者的名稱會影響資源
resourceType| 資源的 hello hello 類型會影響資源
子狀態 | 通常 hello hello 對應 REST 呼叫的 HTTP 狀態碼，但也可能包含其他描述子狀態，例如這些常見的值的字串: [確定] (HTTP 狀態碼： 200)，建立 (HTTP 狀態碼： 201)、 接受 (HTTP 狀態碼： 202)，無內容 (HTTP狀態碼： 204)，不正確的要求 (HTTP 狀態碼： 400)、 找不到 (HTTP 狀態碼： 404)，衝突 (HTTP 狀態碼： 409)，內部伺服器錯誤 (HTTP 狀態碼： 500)，則 Service 無法使用 (HTTP 狀態碼： 503)，閘道逾時 (HTTP 狀態碼： 504)。
eventTimestamp | Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。
submissionTimestamp |   時間戳記 hello 事件變成可供查詢。
subscriptionId | hello 記錄這個事件的 Azure 訂用帳戶
status | 描述 hello hello 作業狀態的字串。 常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。
operationName | Hello 作業的名稱。
category | "ServiceHealth"
resourceId | 資源識別碼 hello 影響資源。
Properties.title | 此通訊的 hello 當地語系化標題。 英文是 hello 預設語言。
Properties.communication | hello 當地語系化 hello 通訊以 HTML 標記的詳細資料。 英文是 hello 預設值。
Properties.incidentType | 可能的值：AssistedRecovery、ActionRequired、Information、Incident、Maintenance、Security
Properties.trackingId | 識別此事件相關聯的 hello 事件。 使用此 toocorrelate hello 事件相關的 tooan 事件。
Properties.impactedServices | 逸出的 JSON blob hello 服務和區域 hello 事件受影響的描述。 Services 清單 (每一份都有 ServiceName) 和 ImpactedRegions 清單 (每一份都有 RegionName)。
Properties.defaultLanguageTitle | 英文版的 hello 通訊
Properties.defaultLanguageContent | 做為 html 標記或純文字的英文版的 hello 通訊
Properties.stage | AssistedRecovery、ActionRequired、Information、Incident、Security 的可能值：Active、Resolved。 Maintenance 的可能值︰Active、Planned、InProgress、Canceled、Rescheduled、Resolved、Complete
Properties.communicationId | hello 通訊此事件是相關聯。


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視您的服務健全狀況通知
1.  在 hello[入口網站](https://portal.azure.com)，瀏覽 toohello**監視器**服務

    ![監視](./media/monitoring-service-notifications/home-monitor.png)
2.  按一下 hello**監視器**選項 tooopen hello 監視器刀鋒視窗上的。 此刀鋒視窗會將您所有的監視設定和資料結合成一個彙總檢視。 它第一次開啟 toohello**活動記錄檔**> 一節。

3.  此時按一下 [服務通知] 區段

    ![監視](./media/monitoring-service-notifications/service-health-summary.png)
4.  按一下任何 hello 明細項目 tooview 更多詳細資料

5. 按一下 hello **+ 加入活動記錄警示**作業 tooreceive 通知 tooensure 就會通知您此類型的通知，未來的服務。 設定服務通知的警示會有更多的 toolearn[按一下這裡](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>後續步驟：
每當[發佈服務健康狀態通知時，即接收警示通知](monitoring-activity-log-alerts-on-service-notifications.md)  
深入了解[活動記錄警示](monitoring-activity-log-alerts.md)
