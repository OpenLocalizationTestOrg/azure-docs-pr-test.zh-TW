---
title: "由於在 Azure 搜尋 aaaModeling |Microsoft 文件"
description: "了解使用「Azure 搜尋服務」時常見的多租用戶 SaaS 應用程式設計模式。"
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>多租用戶 SaaS 應用程式與 Azure 搜尋服務的設計模式
多租用戶應用程式是一個範本提供 hello 相同服務和功能，tooany 數目的租用戶將無法檢視或共用的任何其他租用戶的 hello 資料。 本文件將討論以「Azure 搜尋服務」建置的多租用戶應用程式的租用戶隔離策略。

## <a name="azure-search-concepts"></a>Azure 搜尋服務概念
為搜尋做為服務方案，Azure 搜尋可讓開發人員 tooadd 豐富的搜尋體驗 tooapplications 而不需要管理任何基礎結構，或成為中搜尋的專家。 資料上傳 toohello 服務，然後儲存在 hello 雲端。 使用簡單要求 toohello Azure 搜尋 API，hello 資料可以然後修改並搜尋。 Hello 服務的概觀位於[本文](http://aka.ms/whatisazsearch)。 之前討論的設計模式時，它是重要的 toounderstand 一些概念，在 Azure 搜尋。

### <a name="search-services-indexes-fields-and-documents"></a>搜尋服務、索引、欄位及文件
當使用 Azure Search，其中一個訂閱 tooa*搜尋服務*。 資料上傳的 tooAzure 搜尋，它會儲存在*索引*hello 搜尋服務中。 單一服務內可能會有好幾個索引。 toouse hello 熟悉的概念的資料庫，hello 搜尋服務可以比擬 tooa 資料庫時在服務中的 hello 索引可以比擬 tootables 資料庫內。

搜尋服務內的每個索引都有自己的結構描述，此結構描述是由一些可自訂的「欄位」 所定義。 資料在個別的 hello 表單中加入 tooan Azure 搜尋索引*文件*。 每份文件必須上傳的 tooa 特定的索引，而且必須符合該索引的結構描述。 搜尋時使用 Azure 搜尋資料，來發出 hello 全文檢索搜尋查詢，針對特定的索引。  toocompare 資料庫的這些概念 toothose，欄位可以比擬 toocolumns 資料表中的，而且文件可以比擬 toorows。

### <a name="scalability"></a>延展性
Azure 搜尋中的任何服務 hello 標準[定價層](https://azure.microsoft.com/pricing/details/search/)可以調整以兩個維度： 儲存體和可用性。

* *資料分割*可以加入 tooincrease hello 儲存的搜尋服務。
* *複本*可以加入 tooa 服務 tooincrease hello 輸送量搜尋服務可以處理的要求。

加入和移除資料分割和複本，在將允許 hello 容量 hello 搜尋服務 toogrow hello 需要編寫小量的資料和流量 hello 應用程式需求。 中的順序搜尋服務 tooachieve 讀取[SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/)，它需要兩個複本。 若要為服務 tooachieve 讀寫[SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/)，它需要三個複本。

### <a name="service-and-index-limits-in-azure-search"></a>Azure 搜尋服務中的服務和索引限制
有幾個不同[定價層](https://azure.microsoft.com/pricing/details/search/)在 Azure 搜尋中，每個 hello 層都有不同[限制和配額](search-limits-quotas-capacity.md)。 部分這些限制是在 hello 服務層級，有些在 hello 索引層級，而有些是在 hello 資料分割層級。

|  | 基本 | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| 每項服務的複本數目上限 |3 |12 |12 |12 |12 |
| 每項服務的資料分割數目上限 |1 |12 |12 |12 |1 |
| 每項服務的搜尋單位數目上限 (複本數*資料分割數) |3 |36 |36 |36 |36 (最多 3 個資料分割) |
| 每項服務的文件數目上限 |100 萬 |1 億 8000 萬 |7 億 2000 萬 |140 億 |6 億 |
| 每項服務的儲存體上限 |2 GB |300 GB |1.2 TB |2.4 TB |600 GB |
| 每個資料分割的文件數目上限 |100 萬 |1500 萬 |6000 萬 |1 億 2000 萬 |2 億 |
| 每個資料分割的儲存體上限 |2 GB |25 GB |100 GB |200 GB |200 GB |
| 每項服務的索引數目上限 |5 |50 |200 |200 |3000 (最多 1000 個索引/資料分割) |

#### <a name="s3-high-density"></a>S3 高密度
在 Azure 搜尋 S3 定價層中，沒有特別針對多租用戶案例而設計的 hello 高密度 (HD) 模式的選項。 在許多情況下，就需要 toosupport 大量的較小的租用戶的簡單和成本效益的單一服務 tooachieve hello 權益下。

S3 HD 允許的 hello 許多小型索引 toobe hello 能力 tooscale hello 能力 toohost 的單一服務中的多個索引使用資料分割索引時，您可以壓縮單一搜尋服務的 hello 管理下。

具體而言，S3 服務可能會有介於 1 到 200 一起可能裝載 too1.4 100 億文件的索引。 S3 HD 另一方面上 hello 可讓個別索引 tooonly 向上 too1 百萬個文件，但它可以處理上每個資料分割 （向上 too3000 每個服務) 為 200 萬，每個資料分割的總文件計數 too1000 索引 (向上 too600 百萬個，每個服務)。

## <a name="considerations-for-multitenant-applications"></a>多租用戶應用程式的考量
多租用戶應用程式必須有效地發佈間 hello 租用戶的資源時保留某種程度的隱私權之間 hello 各種租用戶。 設計這類應用程式的 hello 架構時，有一些考量：

* *隔離租用戶：*應用程式開發人員需要 tootake 適當措施 tooensure 沒有租用戶有未經授權或不想要存取 toohello 資料的其他租用戶。 以外的資料隱私權的 hello 觀點而言，租用戶隔離策略需要有效的管理共用的資源，並防止在含有雜訊的鄰近項目。
* *雲端資源成本︰* 與任何其他應用程式一樣，軟體解決方案作為多租用戶應用程式的元件，必須保有成本競爭力。
* *容易的作業：*開發多租用戶的架構時, hello hello 應用程式的營運影響和複雜度是重要的考量。 Azure 搜尋服務具有 [99.9% 的 SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。
* *全域的足跡：*多租用戶應用程式可能需要分散至各 hello 地球 tooeffectively serve 租用戶。
* *延展性：*應用程式開發人員需要的 tooconsider 之間維護夠低層級的應用程式的複雜性和租用戶數目與設計 hello 應用程式 tooscale 如何先協調和 hello 租用戶資料的大小和工作負載。

Azure Search 提供了幾個可以使用的 tooisolate 租用戶資料和工作負載的界限。

## <a name="modeling-multitenancy-with-azure-search"></a>使用 Azure 搜尋服務來建立多租用戶模型
在多租用戶案例的 hello 情況下，hello 應用程式開發人員使用一或多個搜尋服務，並將其租用戶之間服務、 索引或兩者。 建立多租用戶案例模型時，「Azure 搜尋服務」有幾個常見的模式︰

1. *每個租用戶都使用專屬索引︰* 每個租用戶在與其他租用戶共用的搜尋服務內都有自己的索引。
2. *每個租用戶都使用專屬服務︰* 每個租用戶都有自己的專用「Azure 搜尋服務」服務，可提供最高層級的資料和工作負載分隔。
3. *兩者混合︰* 針對較大且較活躍的租用戶會指派專用服務，而針對較小的租用戶則會在共用服務內指派個別的索引。

## <a name="1-index-per-tenant"></a>1.每個租用戶都使用專屬索引
![Hello 索引每個租用戶模型的 portrayal](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

在「每個租用戶都使用專屬索引」模型中，多個租用戶會佔用單一的「Azure 搜尋服務」，其中每個租用戶都有自己的索引。

租用戶可達到資料隔離的目的，因為所有搜尋要求和文件作業都是在「Azure 搜尋服務」的索引層級發出。 Hello 應用程式層，在沒有 hello 需要感知 toodirect hello 各種租用戶流量 toohello 適當的索引，同時也在所有租用戶之間管理 hello 服務層級的資源。

Hello 索引每個租用戶模型的索引鍵屬性是 hello 應用程式開發人員 toooversubscribe hello 容量 hello 應用程式的租用戶之間搜尋服務的 hello 功能。 如果 hello 租用戶有分散工作負載的分配、 hello 最佳組合的租用戶可以搜尋服務編製索引 tooaccommodate 數目高作用中的大量資源的租用戶時同時處理冗長的較不活躍的租用戶。 hello 代價是 hello 無法 hello 模型 toohandle 的情況下每個租用戶同時高度使用中。

hello 索引每個租用戶模型提供了變數成本模型，在整個 Azure 搜尋服務購買前期 hello 基礎以及後續填入與租用戶。 這可讓您未使用的容量 toobe 指定試用和可用的帳戶。

對於具有通用的使用量應用程式，hello 索引每個租用戶模型可能不是最有效率的 hello。 如果應用程式的租用戶已分配給 hello 地球，則可能需要針對每個區域，而可能重複的成本透過每個個別的服務。

Azure 搜尋可讓您的 hello 個別索引和索引 toogrow 的 hello 總數 hello 小數位數。 如果適當的定價層選擇，資料分割和複本可以加入 toohello 整個搜尋服務時 hello 服務內的個別索引成長至過大儲存體或流量。

如果 hello 總數索引變得太大的單一服務，另一個服務已佈建 toobe tooaccommodate hello 新租用戶。 如果索引有 toobe 加入新的服務時，搜尋服務之間移動，hello hello 索引資料已 toobe 手動複製從一個索引 toohello 其他 Azure 搜尋不允許移動索引 toobe 如下。

## <a name="2-service-per-tenant"></a>2.每個租用戶都使用專屬服務
![Hello 服務每個租用戶模型的 portrayal](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

在「每個租用戶都使用專屬服務」架構中，每個租用戶都有自己的搜尋服務。

在此模型中，hello 應用程式會在達到 hello 其租用戶隔離的最大層級。 每項服務除了有個別的 API 金鑰之外，還有專用的儲存體和輸送量來處理搜尋要求。

針對其中每個租用戶中有較大的耗用量或 hello 工作負載從租用戶 tootenant 小變化性的應用程式，hello 每個租用戶的服務模型會是有效的選擇，因為資源不會跨各種租用戶工作負載共用。

每個租用戶模型的服務也提供可預測的固定成本模型的 hello 優點。 沒有任何整個搜尋服務中的前期投資租用戶 toofill 之前，不過 hello 成本的各個租用戶高於索引每個租用戶模型。

hello 服務每個租用戶模型是有效率的選擇有通用的耗用量的應用程式。 分散的租用戶，很容易 toohave 中的每個租用戶的服務 hello 適當區域。

個別租用戶 outgrow 其服務時會調整此模式中的 hello 挑戰。 Azure 搜尋目前不支援升級 hello 定價層的搜尋服務，因此必須手動複製 toobe tooa 新服務的所有資料。

## <a name="3-mixing-both-models"></a>3.混合兩種模型
建立多租用戶模型的另一種模式是將「每個租用戶都使用專屬索引」與「每個租用戶都使用專屬服務」策略混合。

混合 hello 兩個模式，應用程式的最大的租用戶可以佔用專用的服務，而 hello 長尾的作用中的較小的租用戶小於可佔用索引中的共用服務。 此模型可確保 hello 最大的租用戶有一直居高效能從 hello 服務，同時又能夠協助 tooprotect hello 較小的租用戶，從任何有很多雜訊的鄰近項目。

不過，實作此策略需要有遠見來預測哪些租用戶需要的是專用服務，而哪些租用戶需要的是共用服務中的索引。 應用程式的複雜度增加 hello 需要 toomanage 這兩個的這些多的模型。

## <a name="achieving-even-finer-granularity"></a>達到更精細的細微度
Azure 搜尋中的設計模式 toomodel 多租用戶案例上方 hello 假設統一範圍，其中每個租用戶是應用程式的整個執行個體。 不過，應用程式有時可能是處理許多較小的範圍。

如果服務每個租用戶和租用戶索引每個模型不是不夠小的範圍，則可能 toomodel 索引 tooachieve 資料粒度更細微程度。

toohave 單一索引不同的用戶端端點行為不同，欄位可以是針對每個可能的用戶端指定某個值加入的 tooan 索引。 每次用戶端會呼叫 Azure 搜尋 tooquery 或修改索引、 hello hello 用戶端應用程式程式碼指定 hello 適當的值，該欄位使用 Azure Search[篩選](https://msdn.microsoft.com/library/azure/dn798921.aspx)在查詢階段的功能。

這個方法可以是不同的使用者帳戶、 個別的權限層級，以及甚至完全不同的應用程式使用的 tooachieve 功能。

> [!NOTE]
> 使用 hello 方法上述 tooconfigure 單一索引 tooserve 多個租用戶會影響 hello 搜尋結果的相關性。 搜尋相關性分數計算索引層級範圍，而不是租用戶層級範圍，讓所有租用戶的資料併入 hello 相關性分數的基礎統計資料，例如 「 詞彙頻率。
> 
> 

## <a name="next-steps"></a>後續步驟
Azure 搜尋是令人信服的選擇對於許多應用程式，[深入了解有關 hello 服務的強大功能](http://aka.ms/whatisazsearch)。 當評估 hello 各種設計多租用戶應用程式的模式，請考慮 hello[各種不同的定價層](https://azure.microsoft.com/pricing/details/search/)和個別的 hello[服務限制](search-limits-quotas-capacity.md)toobest 量身訂做的 Azure 搜尋 toofit應用程式工作負載和架構的所有大小。

Azure 搜尋和多租用戶案例相關的任何問題可以導向tooazuresearch_contact@microsoft.com。

