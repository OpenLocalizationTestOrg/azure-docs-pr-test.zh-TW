---
title: "aaaDocumentDB API 效能層級 |Microsoft 文件"
description: "深入了解如何 DocumentDB API 效能層級可讓您以每個容器基礎 tooreserve 輸送量。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>淘汰 hello S1、 S2 和 S3 效能層級

> [!IMPORTANT] 
> hello S1、 S2 和 S3 效能層級本文所討論的淘汰過程，便無法再使用新的 DocumentDB API 帳戶。
>

本文提供 S1、 S2 和 S3 效能層級的概觀，並討論如何使用這些效能層級的 hello 集合時，會在 2017 年 8 月 1 日，是移轉的 toosingle 分割區集合。 閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題：

- [為何 hello S1、 S2 和 S3 效能層級停用嗎？](#why-retired)
- [如何單一分割區集合和資料分割的集合比較 toohello S1、 S2、 S3 效能層級？](#compare)
- [我要如何需要 toodo tooensure 不會中斷存取 toomy 資料嗎？](#uninterrupted-access)
- [Hello 移轉之後如何變更我的集合？](#collection-change)
- [如何將我的帳單之後變更我已移轉的 toosingle 分割區集合？](#billing-change)
- [如果我需要超過 10 GB 的儲存體會如何？](#more-storage-needed)
- [我可以變更 hello S1、 S2 和 S3 效能層級，2017 年 8 月 1 之前, 之間嗎？](#change-before)
- [如何得知我的收藏何時已移轉？](#when-migrated)
- [如何將從 hello S1、 S2 或 S3 效能層級 toosingle 分割區集合自己移轉？](#migrate-diy)
- [如果我是 EA 客戶會受到什麼影響？](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>為何 hello S1、 S2 和 S3 效能層級停用嗎？

hello S1、 S2 和 S3 效能層級執行無法提供 hello 彈性 DocumentDB API 集合所提供。 以 hello S1、 S2 或 S3 效能層級，這兩個 hello 輸送量與儲存體容量已預先設定，並不會提供彈性。 Azure Cosmos DB 現在提供 hello 能力 toocustomize 您輸送量與儲存體，提供您更大的彈性能力 tooscale 中隨著需求的變更。

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>如何單一分割區集合和資料分割的集合比較 toohello S1、 S2、 S3 效能層級？

下表中的 hello 比較 hello 輸送量與儲存體的可用選項中單一分割區集合、 資料分割的集合和 S1、 S2 或 S3 效能層級。 美國東部 2 區域的範例如下︰

|   |資料分割的集合|單一資料分割集合|S1|S2|S3|
|---|---|---|---|---|---|
|最大輸送量|無限制|10K RU/秒|250 RU/秒|1 K RU/秒|2.5 K RU/秒|
|輸送量下限|2.5K RU/秒|400 RU/秒|250 RU/秒|1 K RU/秒|2.5 K RU/秒|
|儲存體上限|無限制|10 GB|10 GB|10 GB|10 GB|
|價格 (每月)|輸送量：$6 / 100 RU/秒<br><br>儲存體：$0.25/GB|輸送量：$6 / 100 RU/秒<br><br>儲存體：$0.25/GB|$25 美元|$50 美元|$100 美元|

您是 EA 客戶嗎？ 如果是，請參閱[如果我是 EA 客戶會受到什麼影響？](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>我要如何需要 toodo tooensure 不會中斷存取 toomy 資料嗎？

Nothing，Cosmos DB 處理 hello 為您的移轉。 如果您擁有 S1、 S2 或 S3 的集合，您目前的集合將會移轉的 tooa 2017 年 7 月 31，單一資料分割集合。 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Hello 移轉之後如何變更我的集合？

如果您擁有 S1 集合，您將會移轉的 tooa 400 RU/秒的輸送量的單一資料分割集合。 400 RU/秒是 hello 最低輸送量適用於單一分割區集合。 不過，400 RU/秒中的單一資料分割集合為大約使用 S1 集合費用與您相同的 hello hello 和 250k RU/秒 – 讓您不支付 hello 成本 hello 額外 150 RU/秒可用 tooyou。

如果您擁有 S2 集合，您將會移轉的 tooa 單一資料分割集合，1 RU/秒。 您會看到不變更 tooyour 輸送量層級。

如果您擁有 S3 集合，您將會移轉的 tooa 單一資料分割集合 2.5 RU/秒。 您會看到不變更 tooyour 輸送量層級。

在每個這種情況下，移轉您的集合之後，您會無法 toocustomize 您輸送量層級，或它上下調整為所需的 tooprovide 低延遲存取 tooyour 使用者。 toochange hello 輸送量層級之後已移轉您的集合，只要 hello Azure 入口網站中開啟 Cosmos DB 帳戶、 按一下標尺、 選擇您的集合，和 hello 下列螢幕擷取畫面所示，然後調整 hello 輸送量層級：

![如何在 tooscale 輸送量 hello Azure 入口網站](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>如何將我的帳單之後變更我已移轉的 toohello 單一分割區集合？

假設您有 10 個 S1 集合，1 GB 的 hello 美國東部地區中的每個儲存體，而且您將移轉這些 10 S1 集合 too10 單一分割區集合在 400 RU/秒 （hello 最低層級）。 您的帳單將會看起來像這樣如果您維持完整月份 hello 10 的單一分割區集合：

![如何 S1 定價 10 集合比較 too10 集合使用的單一資料分割集合定價](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>如果我需要超過 10 GB 的儲存空間怎麼辦？

不論您具有使用 S1、 S2 或 S3 效能層級的集合，或具有單一資料分割集合，其中有 10 GB 的可用儲存體，您可以使用 hello Cosmos DB 的資料移轉工具 toomigrate 資料 tooa 幾乎分割集合無限制的儲存體。 資料分割的集合中的 hello 優點的相關資訊，請參閱[資料分割和 Azure Cosmos DB 中的縮放比例](documentdb-partition-data.md)。 如需有關資訊 toomigrate 您 S1、 S2、 S3 或單一資料分割集合 tooa 分割集合，請參閱[從單一資料分割 toopartitioned 集合移轉](documentdb-partition-data.md#migrating-from-single-partition)。 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>我可以變更 hello S1、 S2 和 S3 效能層級，2017 年 8 月 1 之前, 之間嗎？

唯一的現有帳戶使用 S1、 S2 和 S3 效能會無法 toochange 並變更效能層級層透過 hello 入口網站，或以程式設計的方式。 依年 8 月 1，2017，hello S1、 S2 和 S3 效能層級將不再可用。 如果您從 S1、 S3  S3 tooa 單一資料分割集合變更時，無法傳回 toohello S1、 S2 或 S3 效能層級。

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>如何得知我的收藏何時已移轉？

hello 移轉會發生在 2017 年 7 月 31。 如果您擁有的集合，其使用 hello S1、 S2 或 S3 效能層級，hello Cosmos DB 小組會與您連絡以電子郵件進行 hello 移轉之前。 Hello 移轉完成之後，在 8 月 1，2017，hello Azure 入口網站會顯示您的集合，使用標準定價。

![如何 tooconfirm 集合已移轉 toohello 標準定價層](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>如何將從 hello S1、 S2 或 S3 效能層級 toosingle 分割區集合自己移轉？

您可以從 hello S1、 S2、 移轉和 S3 效能層級 toosingle 分割區集合使用 hello Azure 入口網站或以程式設計的方式。 您可以在您自己之前年 8 月 1 toobenefit hello 彈性輸送量選項適用於單一資料分割的集合，或我們將會移轉您的集合，讓您在 2017 年 7 月 31。

**使用 Azure 入口網站 hello toomigrate toosingle 分割區集合**

1. 在 hello [ **Azure 入口網站**](https://portal.azure.com)，按一下 [ **Azure Cosmos DB**，然後選取 [hello Cosmos DB 帳戶 toomodify。 
 
    如果**Azure Cosmos DB**在 hello Jumpbar，請按一下 >，太捲動**資料庫**，選取**Azure Cosmos DB**，然後選取 hello DocumentDB 帳戶。  

2. Hello 資源在功能表上，在**容器**，按一下 **標尺**從 hello 下拉式清單中，選取 hello 集合 toomodify，然後按一下**定價層**。 使用預先定義的輸送量的帳戶具有 S1、S2 或 S3 定價層。  在 hello**選擇定價層**刀鋒視窗中，按一下 **標準**toochange toouser 定義輸送量，然後按一下**選取**toosave 您的變更。

    ![顯示其中 toochange hello 輸送量值 hello 設定 刀鋒視窗的螢幕擷取畫面](./media/performance-levels/change-performance-set-thoughput.png)

3. 在 hello**標尺**刀鋒視窗，hello**定價層**太變更**標準**和 hello**輸送量 （RU/秒）**方塊會顯示預設值為 400。 設定介於 400 到 10000 之間的 hello 輸送量[要求單位](request-units.md)數/秒 （RU/秒）。 hello**預估每月帳單**底部 hello hello 頁面會自動更新 tooprovide hello 每月成本估計。 

    >[!IMPORTANT] 
    > 一旦您儲存變更，並移動 toohello 標準定價層，您無法回復 toohello S1、 S2 或 S3 效能層級。

4. 按一下**儲存**toosave 您的變更。

    如果您判斷您需要更多輸送量 (大於 10,000 RU/秒) 或更多儲存體 (大於 10 GB)，您可以建立資料分割的集合。 toomigrate 單一資料分割集合 tooa 分割集合，請參閱[從單一資料分割 toopartitioned 集合移轉](documentdb-partition-data.md#migrating-from-single-partition)。

    > [!NOTE]
    > 從 S1、 S2 或 S3 tooStandard 變更可能會佔用 too2 分鐘。
    > 
    > 

**使用.NET SDK hello toomigrate toosingle 分割區集合**

變更集合的效能層級的另一個選項是透過我們的 SDK。 本節只涵蓋變更集合的效能層級使用我們[DocumentDB.NET API](documentdb-sdk-dotnet.md)，但我們其他 Sdk 類似 hello 處理程序。

以下是變更 hello 集合輸送量 too5，000 每秒的要求單位的程式碼片段：
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

請瀏覽[MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview 其他範例和深入了解我們提供的方法：

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>如果我是 EA 客戶會受到什麼影響？

EA 客戶將會受到保護，直到其目前合約的 hello 結尾的價格。

## <a name="next-steps"></a>後續步驟
進一步了解價格及使用 Azure Cosmos DB，管理資料 toolearn 瀏覽這些資源：

1.  [在 Cosmos DB 中分割資料](documentdb-partition-data.md)。 了解 hello 差異單一磁碟分割容器和資料分割的容器，以及順暢地實作資料分割的策略 tooscale 的秘訣。
2.  [Cosmos DB 定價](https://azure.microsoft.com/pricing/details/cosmos-db/)。 深入了解 hello 佈建輸送量和耗用儲存體的成本。
3.  [要求單位](request-units.md)。 了解 hello 耗用量的不同作業類型，例如讀取、 寫入、 查詢的輸送量。
