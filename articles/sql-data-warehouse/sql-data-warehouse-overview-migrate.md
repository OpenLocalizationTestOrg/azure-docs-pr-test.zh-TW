---
title: "aaaMigrate 您方案 tooSQL 資料倉儲 |Microsoft 文件"
description: "讓您的方案 tooAzure SQL 資料倉儲平台的移轉指導方針。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>移轉您的方案 tooAzure SQL 資料倉儲
移轉現有的資料庫方案 tooAzure SQL 資料倉儲相關資訊，請參閱。 

## <a name="profile-your-workload"></a>分析工作負載
然後再移轉，您會想 toobe 特定 SQL 資料倉儲是 hello 絕佳的解決方案，您的工作負載。 SQL 資料倉儲是針對大型資料進行分散式的系統設計 tooperform 分析。  移轉 tooSQL 資料倉儲需要一些不太難 toounderstand，但可能需要一些時間 tooimplement 的設計變更。 如果您的業務需求的企業級資料倉儲，hello 優點是值得 hello。 不過，如果您不需要的 SQL 資料倉儲的 hello 電源，則更多符合成本效益 toouse SQL Server 或 Azure SQL Database。

可考慮使用 SQL 資料倉儲的時機如下：
- 具有超過 1 TB 的資料
- 計劃 toorun 分析大量資料
- 需要 hello 能力 tooscale 運算和存放裝置 
- 想要暫停的成本 toosave 計算資源，您不需要它們時。

不要使用 SQL 資料倉儲進行具備以下條件的操作 (OLTP) 工作負載：
- 高頻率的讀取和寫入
- 大量的單一項目選取
- 大量的單一資料列插入
- 逐一處理資料列的需求
- 不相容的格式 (JSON、XML)


## <a name="plan-hello-migration"></a>計劃 hello 移轉

一旦您已決定 toomigrate 現有的方案 tooSQL 資料倉儲，就是開始使用之前的重要 tooplan hello 移轉。 

計劃的其中一個目標是 tooensure 您的資料，您的資料表結構描述，且您的程式碼與 SQL 資料倉儲相容。 有一些相容性的差異 toowork 周圍您目前的系統與 SQL 資料倉儲之間。 此外，移轉大量資料 tooAzure 花費的時間。 務必先謹慎規劃，可以加速取得資料 tooAzure。 

另一個計劃的目標是您的方案會利用 SQL 資料倉儲是 hello 高的查詢效能調整 tooensure 設計 tooprovide toomake 設計。 設計資料倉儲，標尺的介紹不同的設計模式，因此傳統方法不一定 hello 最佳。 雖然您可以在移轉之後進行一些設計調整，更快地 hello 程序中進行變更會儲存之後的時間。

您需要 toomigrate tooperform 移轉成功，您的資料表結構描述、 程式碼和您的資料。 如需這些移轉主題的指引，請參閱：

-  [移轉結構描述](sql-data-warehouse-migrate-schema.md)
-  [遷移程式碼](sql-data-warehouse-migrate-code.md)
-  [移轉資料](sql-data-warehouse-migrate-data.md)。 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>後續步驟
hello CAT （客戶諮詢小組） 也會有它們透過部落格發行一些很棒 SQL 資料倉儲指引。  看看他們的文件：[移轉資料 tooAzure SQL 資料倉儲實際上][ Migrating data tooAzure SQL Data Warehouse in practice]如需有關移轉的其他指引。

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
