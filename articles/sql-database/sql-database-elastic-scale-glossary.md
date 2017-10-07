---
title: "aaaElastic 資料庫工具詞彙 |Microsoft 文件"
description: "彈性資料庫工具所用詞彙的解釋"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>彈性資料庫工具字彙
hello 下列所定義的詞彙 hello[彈性資料庫工具](sql-database-elastic-scale-introduction.md)，Azure SQL Database 的功能。 hello 工具會使用的 toomanage[分區對應](sql-database-elastic-scale-shard-map-management.md)，並包含 hello[用戶端程式庫](sql-database-elastic-database-client-library.md)，hello[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)，[彈性集區](sql-database-elastic-pool.md)，和[查詢](sql-database-elastic-query-overview.md)。 

這些授權條款會以[新增分區使用彈性資料庫工具](sql-database-elastic-scale-add-a-shard.md)和[使用 hello RecoveryManager 類別 toofix 分區對應問題](sql-database-elastic-database-recovery-manager.md)。

![彈性擴縮詞彙][1]

**資料庫**：Azure SQL 資料庫。 

**資料依存路由**: hello 功能，可提供特定的分區化索引鍵的應用程式 tooconnect tooa 分區。 請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。 比較太**[多分區查詢](sql-database-elastic-scale-multishard-querying.md)**。

**全域分區對應**: hello 之間分區化索引鍵和其各自的分區間進行對應**分區集**。 hello 全域分區對應會儲存在 hello**分區對應管理員**。 比較太**本機分區對應**。

**清單分區對應**：逐一對應分區化索引鍵的分區對應。 比較太**範圍分區對應**。   

**本機分區對應**： 儲存於分區，hello 本機分區對應包含 hello shardlet 位於 hello 分區對應。

**多個分區查詢**: hello 能力 tooissue 針對多個分區的查詢，則會傳回結果集，使用 UNION ALL 語意 （也稱為 「 展開傳送查詢 」）。 比較太**資料依存路由**。

**多租用戶**和**單一租用戶**︰這會顯示單一租用戶資料庫和多租用戶資料庫︰

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

以下是 **分區化** 單一和多租用戶資料庫的呈現。 

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**範圍分區對應**： 分區對應中的 hello 分區散發策略根據多個連續值的範圍。 

**參考資料表**：不分區化而是跨分區複寫的資料表。 例如，郵遞區號可以儲存參考資料表中。 

**分區**：儲存來自分區化資料集之資料的 Azure SQL 資料庫。 

**分區彈性**: hello 能力 tooperform**水平延展**和**垂直縮放比例**。

**分區化資料表**：分區化的資料表，亦即，資料根據其分區化索引鍵值而分佈至分區。 

**分區化索引鍵**：決定資料如何分佈至分區的資料行值。 hello 實值型別可以是 hello 下列其中一種： **int**， **bigint**， **varbinary**，或**uniqueidentifier**。 

**分區集**: hello 的屬性化的 toohello 的分區集合 hello 分區對應管理員中的相同分區對應。  

**Shardlet**： 所有 hello 與單一值的分區有分區化索引鍵相關聯的資料。 Shardlet 時轉散發分區化資料表的資料移動可能 hello 最小單位。 

**分區對應**: hello 的分區化索引鍵和其個別分區之間的對應集合。

**分區對應管理員**: hello 分區 map(s)、 分區位置，以及對應的一或多個分區集包含為管理物件和資料存放區。

![對應][2]

## <a name="verbs"></a>動詞
**水平延展**: hello act 的縮放比例外 （或） 的新增或移除分區 tooa 分區對應，如下所示的分區集合。

![水平和垂直縮放][3]

**合併**: hello 動作從兩個分區 tooone 分區移動 shardlet 並據以更新 hello 分區對應。

**Shardlet 移動**: hello 動作 tooa 不同單一 shardlet 的分區。 

**分區**： 跨多個資料庫分區化索引鍵為基礎的水平資料分割具有相同的 hello 動作結構化的資料。

**分割**: hello act 從一個分區 tooanother （通常是新的） 分區移幾個 shardlet。 分區化索引鍵是由 hello 使用者提供，如 hello 分割點。

**垂直縮放比例**: hello act 縮放 （上下） 的 hello 個別分區效能層級。 例如，變更分區從標準 tooPremium （這會導致更多運算資源）。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

