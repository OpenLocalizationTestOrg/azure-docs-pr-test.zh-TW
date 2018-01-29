---
title: "選擇 Azure 搜尋服務的 SKU 或定價層 | Microsoft Docs"
description: "「Azure 搜尋服務」可以在這些 SKU 佈建︰「免費」、「基本」及「標準」，其中「標準」在各種資源組態和容量層級都有提供。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: 781683f27c943e25d5629dd846da357f51c9d4f9
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>選擇 Azure 搜尋服務的 SKU 或定價層
在 Azure 搜尋服務中，會在特定定價層或 SKU [佈建服務](search-create-service-portal.md)。 選項包括**免費**、**基本**或**標準**，其中**標準**在多個組態和容量都有提供。

本文的目的是協助您選擇定價層。 如果就結果來說某個定價層的容量太低，您就必須在更高的定價層佈建新服務，然後重新載入您的索引。 無法從某個 SKU 就地升級到另一個 SKU 的相同服務。

> [!NOTE]
> 選擇定價層並[佈建搜尋服務](search-create-service-portal.md)之後，您可以增加服務內的複本和分割計數。 如需指引，請參閱[調整適用於查詢和編製索引工作負載的資源等級](search-capacity-planning.md)。
>
>

## <a name="how-to-approach-a-pricing-tier-decision"></a>如何進行定價層決策
在 Azure 搜尋服務中，定價層決定容量，而不是功能可用性。 一般來說，每個定價層都可使用各項功能，包括預覽功能。 唯一的例外是不支援 S3 HD 中的索引子。

> [!TIP]
> 我們建議您一律佈建「免費」  服務 (每個訂用帳戶一個，沒有到期日)，以便隨時可供輕量專案使用。 使用**免費**服務進行測試與評估；針對生產或更大的測試工作負載，於**基本**或**標準**層建立第二個計費服務。
>
>

容量與執行服務的費用密切相關。 本文中的資訊可協助您判斷哪個 SKU 可提供適當的平衡，但若要讓任何資訊發揮作用，您至少需要下列項目的粗略預估：

* 您打算建立的索引的數目和大小
* 要上傳的文件的數目和大小
* 查詢量的一些概念，也就是每秒查詢次數 (QPS)。 如需指引，請參閱 [Azure 搜尋服務的效能與最佳化](search-performance-optimization.md)。

大小和數目很重要，因為會透過服務中索引的計數固定限制，或服務所使用的資源 (儲存體或複本) 上索引的計數固定限制，達到最大值限制。 服務的實際限制是看下列何者會先耗盡：資源或物件。

有了預估值之後，下列步驟應該能簡化程序：

* **步驟 1** 檢閱下面的 SKU 描述來了解可用的選項。
* **步驟 2** 回答下列問題來達成初步決策。
* **步驟 3** 檢閱對儲存體的固定限制和價格來完成您的決定。

## <a name="sku-descriptions"></a>SKU 描述
下表提供每個層的描述。

| 層 | 主要案例 |
| --- | --- |
| **免費** |共用服務 (不收費)，用於評估、調查或小量工作負載。 由於是與其他訂閱者共用，因此查詢輸送量和索引會因還有誰在使用該服務而異。 容量很小 (50 MB 或各具有最多 10000 份文件的 3 個索引)。 |
| **基本** |專用硬體上的小量生產環境工作負載。 具有高可用性。 容量最多 3 個複本和 1 個分割區 (2 GB)。 |
| **S1** |標準 1 支援彈性的分割區 (12 個) 和複本 (12 個) 組合，用於專用硬體上的中量生產環境工作負載。 您可以根據計費搜尋單位數目上限 (36 個) 所支援的組合來配置分割區和複本。 在此層級，分割區各為 25 GB。 |
| **S2** |標準 2 使用與 S1 相同的 36 個搜尋單位來執行較大的生產環境工作負載，但搭配較大的分割區和複本。 在此層級，分割區各為 100 GB。 |
| **S3** |標準 3 以 36 個搜尋單位底下最高可達 12 個分割區或 12 個複本的組態，在較高階的系統上執行相應較大的生產環境工作負載。 在此層級，分割區各為 100 GB。 |
| **S3 HD** |標準 3 高密度是設計用於大量的較小型索引。 您最多可以有 3 個分割區，每個 200 GB。|

> [!NOTE]
> 複本和分割區的最大值會以搜尋單位計費 (每個服務最多 36 個單位)，這會強制施行比上限面值所暗示之限制還低的有效限制。 例如，若要使用上限 12 個複本，您最多可以有 3 個分割區 (12 * 3 = 36 個單位)。 同樣地，若要使用分割區數目上限，則須將複本數目降低成 3 個。 如需有關所允許之組合的圖表，請參閱 [在 Azure 搜尋服務中調整查詢和索引工作負載的資源等級](search-capacity-planning.md) 。
>
>

## <a name="review-limits-per-tier"></a>檢閱每一層的限制
下列圖表是來自 [Azure 搜尋服務中的服務限制](search-limits-quotas-capacity.md)的限制子集。 它會列出最有可能會影響 SKU 決策的因素。 您可以在檢閱下列問題時參考這個圖表。

| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 服務等級協定 (SLA) |否 <sup>1</sup> |是 |是 |是 |是 |是 |
| 索引限制 |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| 文件限制 |總計 10,000 |每項服務 100 萬 |每個分割區 1500 萬 |每個分割區 6000 萬 |每個分割區 1 億 2000 萬 |每個索引 100 萬 |
| 分割區上限 |N/A |1 |12 |12 |12 |3 <sup>2</sup> |
| 分割區大小 |總計 50 MB |每項服務 2 GB |每個分割區 25 GB |每個分割區 100 GB (每項服務最多 1.2 TB) |每個分割區 200 GB (每項服務最多 2.4 TB) |200 GB (每項服務最多 600 GB) |
| 複本上限 |N/A |3 |12 |12 |12 |12 |

<sup>1</sup> 免費和預覽功能並未隨附服務等級協定 (SLA)。 在所有可計費層中，SLA 會在您為您的服務佈建足夠的備援性時生效。 查詢 (讀取) SLA 時需要兩個 (含) 以上的複本。 查詢和檢索 (讀寫) SLA 時需要三個 (含) 以上的複本。 分割區數目不是 SLA 考量。 

<sup>2</sup> S3 和 S3 HD 都由相同的高容量基礎結構支援，但各自會以不同方式達到最大限制。 S3 的目標是較少量的極大型索引。 因此，其最大限制是資源限制 (每項服務 2.4 TB)。 S3 HD 的目標是大量極小型索引。 到達 1,000 個索引時，S3 HD 就達到其索引條件約束形式的限制。 如果您是需要 1,000 個以上索引的 S3 HD 客戶，請連絡 Microsoft 支援以了解如何繼續進行。

## <a name="eliminate-skus-that-dont-meet-requirements"></a>排除不符合需求的 SKU
下列問題可協助您決定適合您工作負載的正確 SKU。

1. 您是否有 **服務等級協定 (SLA)** 需求？ 您可以使用任何的可計費層 (「基本」以上)，但必須為服務設定備援。 查詢 (讀取) SLA 時需要兩個 (含) 以上的複本。 查詢和檢索 (讀寫) SLA 時需要三個 (含) 以上的複本。 分割區數目不是 SLA 考量。
2. **多少索引** ？ 其中一個會納入 SKU 決策因素的最大變數就是每個 SKU 所支援的索引數目。 索引支援在較低的定價層中明顯屬於不同層級。 索引數目需求可能會是 SKU 決策的主要因素。
3. **多少文件** 載入每個索引？ 文件的數目和大小將決定索引的最終大小。 假設您可以估算出預計的索引大小，您可以將該數字與每個 SKU 的分割區大小做比較，再依存放該大小的索引所需的分割區數目加以擴充。
4. **什麼是預期的查詢負載**？ 了解儲存體需求之後，請考量查詢工作負載。 S2 及兩個 S3 SKU 提供幾乎相等的輸送量，但 SLA 需求會排除任何預覽版 SKU。
5. 如果您考慮使用 S2 或 S3 定價層，請判斷您是否需要[索引子](search-indexer-overview.md)。 S3 HD 定價層還無法使用索引子。 替代方法是使用索引更新推送模型，您可在其中撰寫應用程式程式碼將資料集推送至索引。

大多數客戶可以根據他們對上述問題的答案來納入或排除特定 SKU。 如果您仍不確定要使用哪一個 SKU，您可以將問題張貼到 MSDN 或 StackOverflow 論壇，或連絡 Azure 支援以尋求進一步的指導。

## <a name="decision-validation-does-the-sku-offer-sufficient-storage-and-qps"></a>決策驗證︰SKU 是否提供足夠的儲存體和 QPS？
最後一個步驟是再次瀏覽[定價頁面](https://azure.microsoft.com/pricing/details/search/)和[服務限制中的每一服務和每一索引小節](search-limits-quotas-capacity.md)，以仔細確認您對訂用帳戶與服務限制的預估值。

如果價格或儲存體需求超出範圍，您可能會想要將多個較小服務之間的工作負載重構 (舉例來說)。 在更細微的層級上，您可以將索引重新設計成更小，或使用篩選來讓查詢更有效率。

> [!NOTE]
> 如果文件包含無關的資料，儲存體需求可能會過度膨脹。 在理想情況下，文件只包含可搜尋的資料或中繼資料。 二進位資料不可搜尋，應該分開存放 (或許存放在 Azure 資料表或 Blob 儲存體中)，並且在索引中要有一個欄位用來保存外部資料的 URL 參考。 個別文件的大小上限是 16 MB (如果您在單一要求中大量上傳多個文件，則會小於 16 MB)。 如需詳細資訊，請參閱 [Azure 搜尋服務中的服務限制](search-limits-quotas-capacity.md) 。
>
>

## <a name="next-step"></a>後續步驟
在您了解哪個 SKU 是正確選擇之後，請繼續進行下列步驟：

* [在入口網站中建立搜尋服務](search-create-service-portal.md)
* [變更分割區和複本的配置以調整您的服務](search-capacity-planning.md)