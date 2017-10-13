---
title: "建置可調整的雲端資料庫 | Microsoft Docs"
description: "使用彈性資料庫用戶端程式庫建置可調整的 .NET 資料庫應用程式"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 0128b333f04847ab646dcb0759fcef5f7e86ffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="building-scalable-cloud-databases"></a>建置可調整的雲端資料庫
使用 Azure SQL Database 的可調整工具和功能，可以輕鬆地相應放大資料庫。 特別是，您可以使用 **彈性資料庫用戶端程式庫** 來建立和管理相應放大的資料庫。 這項功能可讓您使用成百上千個 Azure SQL 資料庫，輕鬆地開發分區化應用程式。 [彈性工作](sql-database-elastic-jobs-powershell.md) 則可用來協助簡化管理這些資料庫。

若要安裝程式庫，請移至 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。 

## <a name="documentation"></a>文件
1. [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)
2. [彈性資料庫功能](sql-database-elastic-scale-introduction.md)
3. [分區對應管理](sql-database-elastic-scale-shard-map-management.md)
4. [轉換現有的資料庫以使用彈性資料庫工具](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)
6. [多分區查詢](sql-database-elastic-scale-multishard-querying.md)
7. [使用彈性資料庫工具加入分區](sql-database-elastic-scale-add-a-shard.md)
8. [使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [升級用戶端程式庫應用程式](sql-database-elastic-scale-upgrade-client-library.md) 
10. [彈性查詢概觀](sql-database-elastic-query-overview.md)
11. [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)
12. [搭配使用彈性資料庫用戶端程式庫與 Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [彈性資料庫用戶端程式庫與 Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)
15. [分區對應管理員的效能計數器](sql-database-elastic-database-client-library.md) 
16. [彈性資料庫工具常見問題集](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>用戶端功能
使用分區化  來相應放大應用程式，對開發人員和系統管理員而言都是一項挑戰。 用戶端程式庫藉由提供工具讓開發人員和系統管理員管理相應放大的資料庫，簡化了管理工作。 在典型的範例中，有許多稱為「分區」的資料庫要管理。 客戶共置於同一資料庫，而每位客戶 (單一租用戶配置) 一個資料庫。 用戶端程式庫包含下列功能：

- **分區對應管理**︰建立了稱為「分區對應管理員」的特殊資料庫。 分區對應管理可讓應用程式管理其分區的中繼資料。 開發人員可利用此功能將資料庫註冊為分區 (描述個別分區化索引鍵或索引鍵範圍至這些資料庫的對應)，並隨著資料庫的數量和組成發展來維護此中繼資料，以反映容量變更。 若沒有彈性資料庫用戶端程式庫，實作分區化時您必須花費大量時間撰寫管理程式碼。 如需詳細資訊，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。

- **資料相依路由**：想像有一個要求進入應用程式。 以要求的分區化索引鍵值為基礎，應用程式必須根據索引鍵值判斷正確的資料庫。 接著，它會開啟資料庫連線來處理要求。 資料相依路由可讓您輕鬆地呼叫一次應用程式的分區對應，就能開啟連接。 資料相依路由是基礎結構程式碼的另一個領域，現在由彈性資料庫用戶端程式庫中的功能所涵蓋。 如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。
- **多分區查詢 (MSQ)**：當要求牽涉到數個 (或所有) 分區時，多分區查詢就派上用場。 多分區查詢在所有分區或一組分區上執行相同的 T-SQL 程式碼。 使用 UNION ALL 語意可將參與分區的結果合併成整體的結果集。 經由用戶端程式庫公開的功能可處理許多工作，包括：連接管理、執行緒管理、錯誤處理和中繼結果處理。 MSQ 可以查詢多達數百個分區。 如需詳細資訊，請參閱 [多分區查詢](sql-database-elastic-scale-multishard-querying.md)。

一般而言，使用彈性資料庫工具的客戶在提交分區內作業，而不是有其本身語意的跨分區作業時，就可以獲得完整的 T-SQL 功能。

## <a name="next-steps"></a>後續步驟
請嘗試示範用戶端功能的 [範例應用程式](sql-database-elastic-scale-get-started.md) 。 

若要安裝文件庫，請移至 [彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。

如需有關使用分割合併工具的指示，請參閱 [分割合併工具概觀](sql-database-elastic-scale-overview-split-and-merge.md)。

[彈性資料庫用戶端程式庫現在已開放原始碼！](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

使用 [彈性查詢](sql-database-elastic-query-overview.md)。

[GitHub](https://github.com/Azure/elastic-db-tools)以開放原始碼軟體的形式提供程式庫。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

