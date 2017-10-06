---
title: "aaaChoose SKU Azure Search 的定價層或 |Microsoft 文件"
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
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>選擇 Azure 搜尋服務的 SKU 或定價層
在 Azure 搜尋服務中，會在特定定價層或 SKU [佈建服務](search-create-service-portal.md)。 選項包括**免費**、**基本**或**標準**，其中**標準**在多個組態和容量都有提供。

hello 本文的目的是 toohelp 選擇層。 如果層的容量證明 toobe 太低，您將需要 tooprovision hello 較高層的新服務並再重新載入您的索引。 不含就地升級的相同服務從某個 SKU tooanother hello。

> [!NOTE]
> 選擇層之後和[佈建搜尋服務](search-create-service-portal.md)，您可以增加複本和資料分割計數 hello 服務中。 如需指引，請參閱[調整適用於查詢和編製索引工作負載的資源等級](search-capacity-planning.md)。
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>如何 tooapproach 定價層決策
在 Azure 搜尋 hello 層會決定不功能可用性的容量。 一般來說，每個定價層都可使用各項功能，包括預覽功能。 hello 一個例外狀況是 S3 HD 中的索引子不支援。

> [!TIP]
> 我們建議您一律佈建「免費」  服務 (每個訂用帳戶一個，沒有到期日)，以便隨時可供輕量專案使用。 使用 hello**免費**服務進行測試和評估; 在 hello 建立第二個計費服務**基本**或**標準**層生產或測試工作負載越大。
>
>

容量和執行 hello 服務成本的移手狀手中。 本文章中的資訊可協助您決定哪一個 SKU 傳送 hello 平衡點，但它的任何 toobe 很有用，您需要至少粗略的估計值上 hello 下列：

* 數量和大小的索引您計劃 toocreate
* 文件 tooupload 的數量和大小
* 查詢量的一些概念，也就是每秒查詢次數 (QPS)

數量和大小很重要，因為最大限制透過 hello 計數的索引或在服務中，文件或資源 （儲存體或複本） hello 服務所使用的固定限制。 hello 實際限制為您的服務會先使用較： 資源或物件。

手邊的預估，遵循步驟 hello 應該簡化 hello 程序：

* **步驟 1**檢閱 hello SKU 描述 toolearn 需可用選項如下。
* **步驟 2** hello 回答以下 tooarrive 初步的決策。
* **步驟 3** 檢閱對儲存體的固定限制和價格來完成您的決定。

## <a name="sku-descriptions"></a>SKU 描述
hello 下表提供每一層的描述。

| 層 | 主要案例 |
| --- | --- |
| **免費** |共用服務 (不收費)，用於評估、調查或小量工作負載。 因為它共用與其他訂閱者，查詢輸送量和索引異使用 hello 服務的其他人。 容量很小 (50 MB 或各具有最多 10000 份文件的 3 個索引)。 |
| **基本** |專用硬體上的小量生產環境工作負載。 具有高可用性。 容量是總 too3 複本和 1 的資料分割 (2 GB)。 |
| **S1** |標準 1 支援彈性的分割區 (12 個) 和複本 (12 個) 組合，用於專用硬體上的中量生產環境工作負載。 您可以根據計費搜尋單位數目上限 (36 個) 所支援的組合來配置分割區和複本。 在此層級，分割區各為 25 GB，而 QPS 是大約每秒 15 個查詢。 |
| **S2** |標準的 2 會執行較大的生產工作負載使用 S1 為但具有較大的可調整大小資料分割和複本的 hello 相同 36 搜尋單位。 在此層級，分割區各為 100 GB，而 QPS 是大約每秒 60 個查詢。 |
| **S3** |標準 3 比例較大的生產工作負載上執行更高階的系統 too12 磁碟分割或 12 複本的組態下 36 個搜尋單位。 在此層級，分割區各為 200 GB，而 QPS 是每秒 60 個查詢以上。 |
| **S3 HD** |標準 3 高密度是設計用於大量的較小型索引。 您可以讓 too3 資料分割，在 200 GB。 QPS 超過每秒 60 個查詢。 |

> [!NOTE]
> 複本和資料分割的最大值會出計費，做為搜尋單位 （36 單位每個服務的最大值），但會比從表面，表示哪些 hello 最大值較低的有效限制。 例如 toouse hello 最多 12 複本，您可能會有最多 3 的資料分割 (12 * 3 = 36 單位)。 同樣地，toouse 最大分割區，減少複本 too3。 如需有關所允許之組合的圖表，請參閱 [在 Azure 搜尋服務中調整查詢和索引工作負載的資源等級](search-capacity-planning.md) 。
>
>

## <a name="review-limits-per-tier"></a>檢閱每一層的限制
hello 下列圖表是子集 hello 限制從[在 Azure 搜尋服務限制](search-limits-quotas-capacity.md)。 它會列出 hello 因素最有可能 tooimpact SKU 決策。 檢閱下方的 hello 問題時，您可以參考 toothis 圖表。

| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 服務等級協定 (SLA) |否 <sup>1</sup> |是 |是 |是 |是 |是 |
| 索引限制 |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| 文件限制 |總計 10,000 |每項服務 100 萬 |每個分割區 1500 萬 |每個分割區 6000 萬 |每個分割區 1 億 2000 萬 |每個索引 100 萬 |
| 分割區上限 |N/A |1 |12 |12 |12 |3 <sup>2</sup> |
| 分割區大小 |總計 50 MB |每項服務 2 GB |每個分割區 25 GB |100 GB，每個資料分割 （向上 tooa 最大為 1.2 TB 每個服務) |200 GB，每個資料分割 （向上 tooa 上限 2.4 TB 的每個服務） |200 GB （向上 tooa 最多 600 GB 每個服務） |
| 複本上限 |N/A |3 |12 |12 |12 |12 |
| 每秒查詢數目 |N/A |~3/每個複本 |~15/每個複本 |~60/每個複本 |>60/每個複本 |>60/每個複本 |

<sup>1</sup> 免費和預覽功能並未隨附服務等級協定 (SLA)。 在所有可計費層中，SLA 會在您為您的服務佈建足夠的備援性時生效。 查詢 (讀取) SLA 時需要兩個 (含) 以上的複本。 查詢和檢索 (讀寫) SLA 時需要三個 (含) 以上的複本。 hello 資料分割數目不是一項 SLA 的考量。 

<sup>2</sup> S3 和 S3 HD 都由相同的高容量基礎結構支援，但各自會以不同方式達到最大限制。 S3 的目標是較少量的極大型索引。 因此，其最大限制是資源限制 (每項服務 2.4 TB)。 S3 HD 的目標是大量極小型索引。 1,000 的索引處 S3 HD 達到其限制 hello 形式索引條件約束。 如果您需要超過 1,000 個索引的 S3 HD 客戶，請連絡 Microsoft 支援服務如需詳細資訊 tooproceed。

## <a name="eliminate-skus-that-dont-meet-requirements"></a>排除不符合需求的 SKU
hello 下列問題可協助您到達您的工作負載 hello 右 SKU 決策。

1. 您是否有 **服務等級協定 (SLA)** 需求？ 您可以使用任何的可計費層 (「基本」以上)，但必須為服務設定備援。 查詢 (讀取) SLA 時需要兩個 (含) 以上的複本。 查詢和檢索 (讀寫) SLA 時需要三個 (含) 以上的複本。 hello 資料分割數目不是一項 SLA 的考量。
2. **多少索引** ？ 索引支援的每個 SKU 的 hello 數目其中一個 hello if-then-throw SKU 決定最大的變數。 索引支援中較低的 hello 相當不同層級定價層。 索引數目需求可能會是 SKU 決策的主要因素。
3. **多少文件**會載入至每個索引？ 文件的 hello 數量和大小會決定 hello 索引的 hello 最終大小。 假設您可以估計 hello hello 索引的預估的大小，您可以比較針對每個 SKU，擴充該大小的索引資料分割需要 toostore 的 hello 數目 hello 磁碟分割大小該數字。
4. **什麼是 hello 預期的查詢負載**？ 了解儲存體需求之後，請考量查詢工作負載。 S2 及兩個 S3 SKU 提供幾乎相等的輸送量，但 SLA 需求會排除任何預覽版 SKU。
5. 如果您考慮 hello S2 或 S3 層，判定您是否需要[索引子](search-indexer-overview.md)。 索引子尚無法使用 hello S3 HD 層。 替代方法是 toouse 索引更新發送模型，您在其中寫入應用程式程式碼 toopush 資料集 tooan 索引。

大部分的客戶可排除特定的 SKU in 或 out 根據上述問題的答案 toohello。 如果您仍不確定使用的 SKU toogo，您可以張貼問題 tooMSDN 或 StackOverflow 論壇，或連絡 Azure 支援以尋求進一步指引。

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>決策驗證： hello SKU 提供足夠的儲存體和 QPS 嗎？
最後一個步驟中，再次瀏覽 hello[定價頁面](https://azure.microsoft.com/pricing/details/search/)和 hello[服務限制中的每個服務和每個索引章節](search-limits-quotas-capacity.md)toodouble 核取您評估與訂用帳戶和服務限制。

如果任一個 hello 價格或儲存體需求超出範圍，您可以在多個較小的服務之間的 toorefactor hello 工作負載 （例如）。 在更細微的層級，您無法重新設計索引 toobe 較小，或使用篩選 toomake 查詢更有效率。

> [!NOTE]
> 如果文件包含無關的資料，儲存體需求可能會過度膨脹。 在理想情況下，文件只包含可搜尋的資料或中繼資料。 二進位資料是不可搜尋，而且應該儲存分開 （也許是在 Azure 資料表或 blob 儲存體） 與 hello 索引 toohold URL 參考 toohello 外部資料中的欄位。 hello 個別文件的大小上限是 16 MB （或小於如果您是大量上傳一個要求中的多個文件）。 如需詳細資訊，請參閱 [Azure 搜尋服務中的服務限制](search-limits-quotas-capacity.md) 。
>
>

## <a name="next-step"></a>後續步驟
一旦您知道其 SKU 為 hello 右符合，繼續進行這些步驟：

* [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)
* [變更的資料分割和複本 tooscale hello 配置您的服務](search-capacity-planning.md)
