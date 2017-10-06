---
title: "在 Azure Cosmos DB aaaRegional 容錯移轉 |Microsoft 文件"
description: "了解 Azure Cosmos DB 的手動和自動容錯移轉如何運作。"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Azure Cosmos DB 中商務持續性的自動區域性容錯移轉
Azure Cosmos DB hello 全域發佈的資料，藉以簡化供應項目完整進行管理，[多區域資料庫帳戶](distribute-data-globally.md)提供清楚的權衡取捨完全之間的一致性、 可用性和效能，所有的對應保證。 Cosmos DB 帳戶提供高可用性，單一位數毫秒的延遲，[妥善定義的一致性層級](consistency-levels.md)，透明區域的容錯移轉多路連接的應用程式開發介面，和 hello 能力 tooelastically 標尺輸送量與儲存體跨 hello 地球。 

Cosmos DB 明確同時支援和原則導向的容錯移轉可讓您 toocontrol hello 端對端的系統行為在 hello 事件中的失敗。 我們將在本文中說明：

* Cosmos DB 的手動容錯移轉如何運作？
* 自動容錯移轉在 Cosmos DB 中如何運作，以及當資料中心當機時會發生什麼情況？
* 如何在應用程式架構中使用手動容錯移轉？

您也可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解區域容錯移轉。

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>設定多區域應用程式
我們深入了解容錯移轉模式之前，我們探討您可以設定應用程式的多重區域可用性 tootake 優點和 hello 表面區域的容錯移轉中有彈性的方式。

* 首先，在多個區域中部署您的應用程式
* 從您的應用程式部署時，每個區域 tooensure 低延遲存取設定 hello 對應[慣用的區域清單](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations)透過其中一個 hello 各地區支援的 Sdk。

下列程式碼片段說明如何 hello tooinitialize 多區域應用程式。 在這裡，hello Azure Cosmos DB 帳戶`contoso.documents.azure.com`設有兩個區域-美國西部和北歐。 

* hello 應用程式被部署在 hello 美國西部地區 （例如，使用 Azure 應用程式服務） 
* 設定`West US`為 hello 第一個慣用的區域為低延遲讀取
* 設定`North Europe`為 hello 第二個慣用的區域 （適用於在地區失敗時的高可用性）

Hello DocumentDB API，在此組態看起來像下列程式碼片段的 hello:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

hello 應用程式也部署在 hello 北歐 hello 順序反轉的慣用區域的區域中。 也就是針對低度延遲讀取時先指定 hello 北歐區域。 然後，hello 美國西部地區 hello 第二個慣用的地區高可用性為期間指定地區的失敗。

hello 架構圖顯示多區域應用程式部署 Cosmos DB 與 hello 應用程式會設定的 toobe 可用在四個 Azure 地理區域中。  

![使用 Cosmos DB 部署全域分散式應用程式](./media/regional-failover/app-deployment.png)

現在，讓我們看看如何 hello Cosmos DB 服務處理地區透過自動容錯移轉失敗。 

## <a id="AutomaticFailovers"></a>自動容錯移轉
在 hello 罕見事件中的 Azure 地區中斷或資料中心完全停止運作，Cosmos DB 都會自動觸發容錯移轉的 hello 受影響區域中出現的所有 Cosmos DB 帳戶。 

**如果讀取區域中斷會發生什麼事？**

與唯讀區域中的其中一個受影響的 hello 區域 cosmos DB 帳戶自動中斷其寫入區域並標示為離線。 區域是使用重新導向讀取呼叫 toohello 下一個可用的地區 hello 慣用的地區清單中，偵測到 hello Cosmos DB Sdk 實作外面 tooautomatically 地區的探索通訊協定。 如果無 hello 中的 hello 區域偏好的地區清單為可用，呼叫會自動切換回 toohello 目前寫入區域。 您的應用程式程式碼 toohandle 地區容錯移轉，不需要任何變更。 在整個過程中，一致性保證會繼續接受 Cosmos DB toobe。

![Azure Cosmos DB 中的讀取區域失敗](./media/regional-failover/read-region-failures.png)

一旦從 hello 中斷復原受影響的 hello 區域，hello 區域中的所有受影響的 hello Cosmos DB 帳戶會自動回復 hello 服務。 Cosmos DB 帳戶 hello 受影響區域中已讀取的區域會自動同步目前寫入區域然後開啟線上。 hello Cosmos DB Sdk 探索 hello 的 hello 新區域的可用性，並評估是否應該為 hello 目前讀取區域 hello 應用程式所設定的 hello 慣用的地區清單為基礎選取 hello 區域。 後續的讀取會重新導向的 toohello 復原的區域，而不需要任何變更 tooyour 應用程式程式碼。

**如果寫入區域中斷會發生什麼事？**

如果指定的 Cosmos DB 帳戶 hello 目前寫入區域 hello 受影響的區域，然後 hello 區域將會自動標示為離線。 然後，hello 撰寫區域每個受影響的 Cosmos DB 帳戶時，會升級替代地區。 您可以完全掌控 hello 地區選取項目順序的 Cosmos DB 帳戶透過 hello Azure 入口網站或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)。 

![Azure Cosmos DB 的容錯移轉優先順序](./media/regional-failover/failover-priorities.png)

自動的容錯移轉期間 Cosmos DB 自動選擇下一個寫入區域 hello 指定的 Cosmos db 指定優先順序根據 hello 的帳戶。 

![Azure Cosmos DB 中的寫入區域失敗](./media/regional-failover/write-region-failures.png)

一旦從 hello 中斷復原受影響的 hello 區域，hello 區域中的所有受影響的 hello Cosmos DB 帳戶會自動回復 hello 服務。 

* Cosmos DB 帳戶與他們 hello 受影響區域中的先前寫入區域停留在離線模式中讀取的可用性與 hello 區域 hello 復原後，即使。 
* 您可以查詢此區域 toocompute 任何未複寫的寫入 hello 中斷期間藉由比較與 hello hello 目前寫入區域中可用的資料。 根據應用程式的 hello 需求，您可以執行合併和/或衝突解析並撰寫 hello 最終組的變更回復 toohello 目前寫入區域。 
* 當您完成變更之後時，您可以讓受影響的 hello 區域重新上線藉由移除 hello 區域 tooyour Cosmos DB 帳戶正在重新加入。 一旦 hello 區域就會重新加入，您可以設定回為 hello 寫入區域執行透過 hello Azure 入口網站的手動容錯移轉或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)。

## <a id="ManualFailovers"></a>手動容錯移轉

此外 tooautomatic 容錯移轉，目前的 hello 寫入指定的 Cosmos DB 帳戶的區域中，您可以手動變更動態 tooone 的 hello 現有唯讀區域。 可透過 hello Azure 入口網站起始手動容錯移轉或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)。 

手動容錯移轉確保**零資料遺失**和**零可用性**遺失而且依正常程序從舊的 hello 傳輸寫入狀態撰寫區域 toohello 新 hello 指定 Cosmos DB 帳戶。 像是自動容錯移轉，hello Cosmos DB SDK 自動控制代碼會寫入區域手動容錯移轉期間變更，並確保呼叫不會自動重新導向的 toohello 新寫入的區域。 程式碼或組態不需要任何變更您的應用程式 toomanage 容錯移轉。 

![Azure Cosmos DB 中的手動容錯移轉](./media/regional-failover/manual-failovers.png)

Hello 很有用的手動容錯移轉的常見案例包括：

**遵循 hello 時鐘模型**： 如果您的應用程式有 hello hello 一天的時間為基礎的可預測的流量模式，您可以定期變更 hello 寫入狀態 toohello 最常使用地理區域的 hello 當日時間為基礎。

**服務更新**： 特定全域散發的應用程式部署可能會重設透過流量管理員流量 toodifferent 區域路徑在其計劃的服務更新。 這類應用程式部署現在可以使用手動容錯移轉 tookeep hello 寫入狀態 toohello 區域其中那里即將 toobe active 流量期間 hello 服務更新。

**商務持續性和災害復原 (BCDR) 及高可用性和災害復原 (HADR) 演練**︰大多數企業應用程式都會將商務持續性測試納入其開發和發行程序。 BCDR 和 HADR 測試通常是在相容性認證中的一個重要步驟和地區的中斷的 hello 萬一保證服務可用性。 您可以測試 hello BCDR 整備觸發 Cosmos DB 帳戶的手動容錯移轉和/或新增及移除區域以動態方式透過使用儲存體 Cosmos DB 的應用程式。

在本文中，我們已檢閱 Cosmos DB 中的方式手動和自動容錯移轉工作，您可以設定您 Cosmos DB 帳戶與應用程式 toobe 全域可用的方式。 使用 Cosmos DB 全域複寫支援，可以改進端對端延遲，並確保其高可用性，即使在 hello 的區域失敗的事件。 

## <a id="NextSteps"></a>後續步驟
* 了解 Cosmos DB 如何支援[全域散發](distribute-data-globally.md)
* 了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)
* 使用 Azure Cosmos DB 的 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md) 進行多區域開發
* 深入了解如何 toobuild[多區域寫入器架構](multi-region-writers.md)與 Azure DocumentDB

