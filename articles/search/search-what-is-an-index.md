---
title: "Azure 搜尋索引 aaaCreate |Microsoft Azure |託管的雲端搜尋服務"
description: "Azure 搜尋服務中的索引是什麼？如何使用？"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>建立 Azure Search 索引
> [!div class="op_single_selector"]
> * [概觀](search-what-is-an-index.md)
> * [入口網站](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>什麼是索引？
索引是對 Azure 搜尋服務所使用的文件和其他建構所做的持續性儲存。 文件是索引中單一單位的可搜尋資料。 例如，電子商務零售商可能會有儲存了每個銷售項目的文件、新聞組織可能會有儲存了每篇文章的文件，類似情況不一而足。對應這些概念 toomore 熟悉資料庫對等項目：*索引*是概念上類似 tooa*資料表*，和*文件*相近太*列*資料表中。

當您新增/上傳文件和送出搜尋查詢 tooAzure 搜尋中，在您的搜尋服務提交要求 tooa 的特定索引。

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Azure 搜尋服務索引中的欄位類型和屬性
當您定義您的結構描述，您必須指定索引中的 hello 名稱、 類型和每個欄位的屬性。 hello 欄位型別會分類儲存在該欄位中的 hello 資料。 屬性會設定個別欄位 toospecify hello 欄位的使用方式。 hello 表列舉 hello 類型和您可以指定的屬性。

### <a name="field-types"></a>欄位類型
| 類型 | 說明 |
| --- | --- |
| *Edm.String* |可選擇性予以 Token 化以供進行全文檢索搜尋 (斷字、詞幹分析等) 的文字。 |
| *Collection(Edm.String)* |可選擇性予以 Token 化以供進行全文檢索搜尋的字串清單。 項目集合中的 hello 數目沒有理論上限，但 hello 16 MB 承載大小上限，適用於 toocollections。 |
| *Edm.Boolean* |包含 true/false 值。 |
| *Edm.Int32* |32 位元整數值。 |
| *Edm.Int64* |64 位元整數值。 |
| *Edm.Double* |雙精度數值資料。 |
| *Edm.DateTimeOffset* |日期時間值以 hello OData V4 格式表示 (例如`yyyy-MM-ddTHH:mm:ss.fffZ`或`yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`)。 |
| *Edm.GeographyPoint* |代表 hello 地球上的某個地理位置的點。 |

您可以在這裡找到有關 Azure 搜尋服務 [支援的資料類型](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types)的詳細資訊。

### <a name="field-attributes"></a>欄位屬性
| 屬性 | 說明 |
| --- | --- |
| *金鑰* |提供 hello 每份文件，用來查閱文件的唯一識別碼的字串。 每個索引必須有一個索引鍵。 只有一個欄位可以是 hello 金鑰，且其類型必須設定 tooEdm.String。 |
| *Retrievable* |指定搜尋結果中是否可傳回某欄位。 |
| *Filterable* |可讓 hello 欄位 toobe 篩選查詢中使用。 |
| *Sortable* |允許查詢 toosort 搜尋結果使用此欄位。 |
| *Facetable* |允許用於欄位 toobe[多面向導覽](search-faceted-navigation.md)使用者自我引導篩選的結構。 通常包含重複的值，您可以使用 toogroup 欄位多份文件放在一起 （例如，多個文件 底下的單一品牌或服務類別目錄） 最適合做為 facet。 |
| *Searchable* |標記 hello 做為全文檢索搜尋的欄位。 |

您可以在這裡找到有關 Azure 搜尋服務 [索引屬性](https://docs.microsoft.com/rest/api/searchservice/Create-Index)的詳細資訊。

## <a name="guidance-for-defining-an-index-schema"></a>適用於定義索引結構描述的指引
設計索引時，請在規劃階段 toothink 透過每個決策的 hello 需要您的時間。 很重要時，設計您的索引，因為每個欄位必須指派 hello 您搜尋的使用者經驗和商務需求謹記在心[適當屬性](https://docs.microsoft.com/rest/api/searchservice/Create-Index)。 部署後變更索引需要重建並重新載入 hello 資料。

如果資料儲存體需求在之後有所改變，您可以藉由新增或移除資料分割來增加或減少容量。 如需詳細資料，請參閱[在 Azure 中管理您的搜尋服務](search-manage.md)或[服務限制](search-limits-quotas-capacity.md)。

