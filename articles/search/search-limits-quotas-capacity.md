---
title: "在 Azure 搜尋 aaaService 限制 |Microsoft 文件"
description: "容量計劃中使用的服務限制，以及 Azure 搜尋服務要求和回應的最大限制。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Azure 搜尋中的服務限制
儲存體與工作負載的最大限制，以及索引、文件和其他物件的數量上限，皆取決於您是否在**免費**、**基本**，還是**標準**定價層中[佈建 Azure 搜尋服務](search-create-service-portal.md)。

* **免費** 的是 Azure 訂用帳戶隨附的多租用戶共用服務。 它是現有的訂閱者不需額外成本選項可讓您與 hello 服務 tooexperiment 之前註冊專用資源。
* **基本**會針對生產環境工作負載提供較小規模的專用計算資源。
* **標準** 是在專用的機器上執行，在各層級具有更多的儲存和處理容量。 標準共有四個等級︰S1、S2、S3 及 S3 高密度 (S3 HD)。

> [!NOTE]
> 服務會佈建在特定層。 如果您需要更多容量 toojump 層 tooget，您必須提供新的服務 （沒有任何就地升級）。 如需詳細資訊，請參閱[選擇 SKU 或階層](search-sku-tier.md)。 深入了解調整服務內的容量 toolearn 您已經已經佈建，請參閱[調整 查詢和索引的工作負載的資源層級](search-capacity-planning.md)。
>

## <a name="per-subscription-limits"></a>每一訂用帳戶限制
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>每一服務限制
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>每一索引限制
索引限制與索引子限制之間有一對一的對應關係。 指定的限制為 200 的索引，索引子的 hello 最大限制也是 200 hello 相同的服務。

| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 索引︰每個索引的欄位上限 |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| 索引：每個索引的評分設定檔上限 |100 |100 |100 |100 |100 |100 |
| 索引：每個設定檔的函式上限 |8 |8 |8 |8 |8 |8 |
| 索引子︰每次叫用的索引編製負載上限 |10,000 份文件 |僅限制文件上限 |僅限制文件上限 |僅限制文件上限 |僅限制文件上限 |N/A <sup>2</sup> |
| 索引子︰執行時間上限 | 1-3 分鐘 <sup>3</sup> |24 小時 |24 小時 |24 小時 |24 小時 |N/A <sup>2</sup> |
| Blob 索引子︰Blob 大小上限，MB |16 |16 |128 |256 |256 |N/A <sup>2</sup> |
| Blob 索引子︰從 Blob 擷取的內容字元數上限 |32,000 |64,000 |4 百萬 |4 百萬 |4 百萬 |N/A <sup>2</sup> |

<sup>1</sup>基本層是 hello 只 100 的欄位，每個索引的較低限制的 SKU。

<sup>2</sup> S3 HD 目前不支援索引子。 如果您對此功能有迫切的需求，請連絡 Azure 支援。

<sup>3</sup> hello 免費層的索引子最長執行時間為 3 分鐘，blob 來源和所有其他資料來源的 1 分鐘。

## <a name="document-size-limits"></a>文件大小限制
| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 每個索引 API 的文件大小 |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

呼叫索引 API 時，是指 toohello 最大的文件大小。 文件大小是 hello 的實際索引 API 要求主體的 hello 大小的限制。 您可以一次傳遞多個文件 toohello 索引 API 批次，因為 hello 大小上限實際上取決於多少文件 hello 批次中。 具有單一文件的批次，hello 最大的文件大小是 16 MB 的 JSON。

tookeep 文件大小，請從 hello 要求記住 tooexclude 非可查詢資料。 影像和其他二進位資料不可以直接查詢，而且不應該儲存在 hello 索引。 搜尋結果中，將 toointegrate 非可查詢資料定義儲存的 URL 參考 toohello 資源的非可搜尋欄位。

## <a name="workload-limits-queries-per-second"></a>工作負載限制 (每秒查詢次數)
| 資源 | 免費 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N/A  |~3/每個複本 |~15/每個複本 |~60/每個複本 |>60/每個複本 |>60/每個複本 |

每秒查詢數 (QPS) 是使用啟發學習法，使用模擬與實際客戶工作負載 tooderive 估計值為基礎的近似值。 確切的 QPS 輸送量 hello 查詢您的資料和 hello 性質而有所不同。

雖然上述提供概略估計，實際的速率是難以 toodetermine，尤其是在 hello 免費共用其中輸送量根據可用的頻寬和系統資源的服務。 在 hello 免費層次中，儲存和運算資源共用由多個訂閱者，所以解決方案的 QPS 會一律有所不同 hello 同時執行多少其他工作負載相同的時間。

在 hello 標準層級，您可以估計多個 QPS 密切因為您可以控制多個 hello 參數。 請參閱 hello 最佳作法 > 一節中的[管理您的搜尋解決方案](search-manage.md)的指引 toocalculate QPS 工作負載。

## <a name="api-request-limits"></a>API 要求限制
* 每個要求最多 16 MB <sup>1</sup>
* 最長 8 KB 的 URL 長度
* 每個索引上傳、合併、或刪除批次最多包含 1000 個文件
* $orderby 子句中最多 32 個欄位
* 最大搜尋詞彙的大小是 utf-8 編碼文字的 32,766 個位元組 (32 KB 減 2 個位元組)

<sup>1</sup>中 「 Azure 搜尋 hello 主體的要求主體 tooan 上限是 16 MB，意在 hello 或內容的個別欄位集合，否則不一定理論上的限制所實用的限制 (請參閱[支援資料型別](https://msdn.microsoft.com/library/azure/dn798938.aspx)如需有關欄位組合和限制)。

## <a name="api-response-limits"></a>API 回應限制
* 每一頁搜尋結果最多傳回 1000 個文件
* 每個建議 API 要求最多傳回 100 個建議

## <a name="api-key-limits"></a>API 金鑰限制
API 金鑰可用於服務驗證。 有兩種類型。 系統管理金鑰 hello 要求標頭中指定，並授與完全的讀寫存取 toohello 服務。 查詢索引鍵會是唯讀的指定 hello URL 和 tooclient 通常分散式應用程式。

* 每個服務最多 2 個系統管理金鑰
* 每個服務最多 50 個查詢金鑰
