---
title: "高階 Azure Redis 快取的 aaaHow tooconfigure 資料持續性"
description: "深入了解如何 tooconfigure 和管理資料持續性 Premium 層 Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>如何 tooconfigure Premium Azure Redis 快取的資料持續性
Azure Redis 快取都有提供有彈性地 hello 選擇的快取大小和功能，包括 Premium 層功能，例如叢集、 持續性和虛擬網路支援不同的快取提供項目。 本文說明如何在 premium tooconfigure 持續性 Azure Redis 快取執行個體。

如需其他進階快取功能的資訊，請參閱[簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)。

## <a name="what-is-data-persistence"></a>資料永續性是什麼？
[Redis 持續性](https://redis.io/topics/persistence)可讓您儲存於 Redis toopersist 資料。 您也可以取得快照集及備份 hello 資料，您可以載入如果發生硬體故障。 這是龐大的優勢，透過基本或標準層，其中所有 hello 資料儲存在記憶體中，而且可以有其中快取節點為關閉故障的潛在資料遺失。 

Azure Redis 快取提供 Redis 持續性，使用下列模型 hello:

* **RDB 持續性**-設定當 RDB （Redis 資料庫） 的持續性，Azure Redis 快取保存於二進位格式 toodisk 根據可設定的備份頻率 Redis hello Redis 快取的快照集。 發生重大事件，會停用 hello 主要和複本快取，hello 快取重新建構使用 hello 最新的快照集。 深入了解 hello[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)RDB 持續性。
* **很少持續性**-設定時很少 （附加唯一的檔案） 的持續性，Azure Redis 快取會儲存在至少一次秒到 Azure 儲存體帳戶會儲存每個寫入作業 tooa 記錄檔。 發生重大事件，會停用 hello 主要和複本快取，hello 快取重新建構使用 hello 儲存寫入作業。 深入了解 hello[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)很少持續性。

持續性會設定 hello**新增 Redis 快取**刀鋒視窗中的快取建立期間和 hello**資源功能表**現有進階版快取。

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

選取進階定價層後，按一下 [Redis 永續性] 。

![Redis 永續性][redis-cache-persistence]

hello hello 下一節中的步驟說明如何 tooconfigure Redis 上新的高階快取的持續性。 一旦設定 Redis 持續性之後，按一下**建立**toocreate 您新 premium 快取，Redis 持續性。

## <a name="enable-redis-persistence"></a>啟用 Redis 持續性

Redis 在 hello 上已啟用持續性**Redis 資料持續性**刀鋒視窗中的選擇  **RDB**或**很少**持續性。 新的快取，此刀鋒視窗存取 hello 快取建立程序期間 hello 上一節中所述。 現有的快取，hello **Redis 資料持續性**刀鋒視窗存取從 hello**資源功能表**快取。

![Redis 設定][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>設定 RDB 持續性

tooenable RDB 持續性，按一下  **RDB**。 toodisable RDB 持續性上先前已啟用進階版快取中，按一下**已停用**。

![Redis RDB 持續性][redis-cache-rdb-persistence]

tooconfigure hello 備份間隔，選取**備份頻率**hello 下拉式清單中。 選項包括 [15 分鐘]、[30 分鐘]、[60 分鐘]、[6 小時]、[12 小時] 及 [24 小時]。 在此時間間隔開始 hello 先前的備份作業成功完成，並在它耗盡時起始新的備份之後，向下計數。

按一下**儲存體帳戶**tooselect hello 儲存體帳戶 toouse，並選擇其中一個 hello**主索引鍵**或**次要金鑰**從 hello toouse**儲存體索引鍵**下拉式清單。 您必須選擇儲存體帳戶中 hello 與 hello 快取中，相同的區域和**高階儲存體**因為進階儲存體具有較高的輸送量，建議使用帳戶。 

> [!IMPORTANT]
> 如果重新產生您的持續性帳戶 hello 儲存體金鑰時，您必須重新設定從 hello hello 所需的索引鍵**儲存體金鑰**下拉式清單。
> 
> 

按一下**確定**toosave hello 持續性組態。

一旦 hello 備份頻率間隔耗盡起始 hello 下一個備份 （或新的快取的第一次備份）。

## <a name="configure-aof-persistence"></a>設定 AOF 持續性

tooenable 很少持續性，按一下 **很少**。 toodisable 很少持續性上先前已啟用進階版快取中，按一下**已停用**。

![Redis AOF 持續性][redis-cache-aof-persistence]

tooconfigure 很少持續性，指定**第一個儲存體帳戶**。 這個儲存體帳戶必須在 hello 與 hello 快取中，相同的區域和**高階儲存體**因為進階儲存體具有較高的輸送量，建議使用帳戶。 您可以選擇性地設定額外的儲存體帳戶，並指定為 [第二個儲存體帳戶]。 如果第二個儲存體帳戶設定，hello 寫入 toohello 複本快取寫入 toothis 第二個儲存體帳戶。 針對每個設定的儲存體帳戶中，選擇其中一個 hello**主索引鍵**或**次要金鑰**從 hello toouse**儲存體金鑰**下拉式清單。 

> [!IMPORTANT]
> 如果重新產生您的持續性帳戶 hello 儲存體金鑰時，您必須重新設定從 hello hello 所需的索引鍵**儲存體金鑰**下拉式清單。
> 
> 

啟用很少持續性時，寫入作業 toohello 快取會儲存 toohello 指定儲存體帳戶 （或如果您已設定的第二個儲存體帳戶的帳戶）。 Hello 重大錯誤事件中，會同時向 hello 主要複本快取，hello 預存很少記錄會使用和 toorebuild hello 快取。

## <a name="persistence-faq"></a>永續性常見問題集
hello 下列清單包含 Azure Redis 快取持續性相關常見問題的解答 toocommonly。

* [可以對先前建立的快取啟用永續性嗎？](#can-i-enable-persistence-on-a-previously-created-cache)
* [啟用在 hello 很少和 RDB 持續性相同的時間？](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [我應該選擇哪一種持續性模型？](#which-persistence-model-should-i-choose)
* [如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份會怎樣？](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>RDB 持續性
* [在建立 hello 快取之後可以變更 hello RDB 備份頻率嗎？](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [新的備份進行時，怎樣 toohello 舊 RDB 備份？](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>AOF 持續性
* [何時應該使用第二個儲存體帳戶？](#when-should-i-use-a-second-storage-account)
* [AOF 持續性是否會影響快取的輸送量、延遲或效能？](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [我要如何移除 hello 第二個儲存體帳戶？](#how-can-i-remove-the-second-storage-account)
* [什麼是重寫，其對快取有何影響？](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [在啟用 AOF 下調整快取預期會發生什麼事？](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [我的 AOF 資料在儲存體中的組織方式為何？](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>可以對先前建立的快取啟用永續性嗎？
可以，可在建立快取時以及現有進階快取中設定 Redis 永續性。

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>啟用在 hello 很少和 RDB 持續性相同的時間？

否，您可以啟用僅 RDB 或很少，但不是能同時執行 hello 相同的時間。

### <a name="which-persistence-model-should-i-choose"></a>我應該選擇哪一種持續性模型？

很少持續性儲存每個寫入 tooa 記錄檔，會影響部分輸送量，相較於 RDB 持續性 hello 為基礎的備份需要以備份的時間間隔，以設定對效能的影響降到最低。 如果您的主要目標 toominimize 資料遺失，而且您可以處理輸送量降低快取，請選擇很少持續性。 如果您想在您的快取 toomaintain 最佳輸送量，但仍然想要進行資料復原的機制，請選擇 RDB 持續性。

* 深入了解 hello[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)RDB 持續性。
* 深入了解 hello[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)很少持續性。

如需使用 AOF 持續性時之效能的詳細資訊，請參閱 [AOF 持續性是否會影響快取的輸送量、延遲或效能？](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份會怎樣？

針對 RDB 和 AOF 持續性：

* 如果您有縮放 tooa 較大的大小，則不會影響。
* 如果您有調整 tooa 較小，而且您有自訂[資料庫](cache-configure.md#databases)設定大於 hello[資料庫限制](cache-configure.md#databases)對於新的大小，不還原那些資料庫中的資料。 如需詳細資訊，請參閱[我的自訂資料庫設定在調整期間會受到影響嗎？](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* 如果您有向 tooa 較小的大小，hello 所有 hello hello 最後一個備份，索引鍵的資料將會收回 hello 還原程序期間較小的大小 toohold 沒有足夠空間，通常會使用 hello [allkeys lru](http://redis.io/topics/lru-cache)收回原則。

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>在建立 hello 快取之後可以變更 hello RDB 備份頻率嗎？
是，您可以變更在 hello RDB 持續性的 hello 備份頻率**Redis 資料持續性**刀鋒視窗。 如需相關指示，請參閱 [設定 Redis 永續性](#configure-redis-persistence)。

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？
hello RDB 持續性備份頻率間隔會等到 hello 先前的備份程序已順利完成。 如果 hello 備份頻率為 60 分鐘，它會採用完成備份程序 15 分鐘 toosuccessfully hello 下一次備份無法啟動，直到之後 hello 的 75 分鐘開始 hello 先前備份的時間。

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>新的備份進行時，怎樣 toohello 舊 RDB 備份？
所有 RDB 持續性備份，hello 最新的一不會自動都刪除。 這項刪除作業可能不會立即發生，但較舊的備份不會無限期保存。


### <a name="when-should-i-use-a-second-storage-account"></a>何時應該使用第二個儲存體帳戶？

當您認為您有高於 hello 快取的預期的設定作業，您應該很少持續性使用第二個儲存體帳戶。  Hello 次要儲存體帳戶的設定可協助確保您的快取不會連線到儲存體頻寬限制。

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>AOF 持續性是否會影響快取的輸送量、延遲或效能？

很少持續性時，會影響輸送量的大約 15%-20 %hello 快取低於最大負載 (CPU 和伺服器負載兩者在 90%)。 不應該有延遲問題 hello 快取這些限制範圍內時。 不過，hello 快取會達到這些限制較早與啟用很少。

### <a name="how-can-i-remove-hello-second-storage-account"></a>我要如何移除 hello 第二個儲存體帳戶？

您可以藉由設定 hello toobe hello 相同 hello 第一個儲存體帳戶為第二個儲存體帳戶中移除 hello 很少持續性次要儲存體帳戶。 如需相關指示，請參閱[設定 AOF 持續性](#configure-aof-persistence)。

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>什麼是重寫，其對快取有何影響？

當 hello 很少檔案變得夠大時，重寫自動排入佇列 hello 快取上。 hello 重寫 hello 很少與最小的 hello 設定檔的作業需要 toocreate hello 目前資料集的調整大小。 在撰寫，預期 tooreach 效能限制更快地尤其是在處理大型資料集。 撰寫發生小於通常 hello 很少檔案變得更大，但需要大量的情況時的時間。

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>在啟用 AOF 下調整快取預期會發生什麼事？

如果縮放的 hello 次 hello 很少檔案相當龐大，則預期 hello 延展作業 tootake 時間超出預期行為，因為它將會重新載入 hello 檔案之後調整已完成。

如需有關調整的詳細資訊，請參閱[如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份，會發生什麼事？](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>我的 AOF 資料在儲存體中的組織方式為何？

很少檔案中儲存的資料會分成多個分頁 blob，每個儲存 hello 資料 toostorage 節點 tooincrease 效能。 hello 下表顯示針對每個定價層使用多少的分頁 blob:

| 高階層 | Blob |
|--------------|-------|
| P1           | 每個分區 4 個    |
| P2           | 每個分區 8 個    |
| P3           | 每個分區 16 個   |
| P4           | 每個分區 20 個   |

啟用叢集時，hello 快取中的每個分區會有它自己的分頁 blob 集 hello 上表所示。 例如，具有三個分區的 P2 快取會將其 AOF 檔案散發到 24 個分頁 Blob (3 個分區，所以每個分區 8 個 Blob)。

重寫後，儲存體中會有兩組 AOF 檔案。 撰寫 hello 背景中發生，並附加 toohello 第一組檔案，而傳送嗨重寫期間 toohello 快取的設定作業附加 toohello 第二個集合。 重寫期間會暫時儲存備份以備失敗之需，但在重寫完成之後則會立即刪除備份。


## <a name="next-steps"></a>後續步驟
了解如何更進階的 toouse 快取功能。

* [簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
