---
title: "aaaBuilding 可擴充的雲端資料庫 |Microsoft 文件"
description: "建置可延展資料庫應用程式的.NET 與 hello 彈性資料庫用戶端程式庫"
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
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>建置可調整的雲端資料庫
使用 Azure SQL Database 的可調整工具和功能，可以輕鬆地相應放大資料庫。 特別是，您可以使用 hello**彈性資料庫用戶端程式庫**toocreate 和管理向外延展資料庫。 這項功能可讓您使用成百上千個 Azure SQL 資料庫，輕鬆地開發分區化應用程式。 [彈性作業](sql-database-elastic-jobs-powershell.md)接著可以使用的 toohelp 方便管理這些資料庫。

tooinstall hello 程式庫，請移太[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。 

## <a name="documentation"></a>文件
1. [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)
2. [彈性資料庫功能](sql-database-elastic-scale-introduction.md)
3. [分區對應管理](sql-database-elastic-scale-shard-map-management.md)
4. [移轉現有的資料庫 tooscale 外](sql-database-elastic-convert-to-use-elastic-tools.md)
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
向外延展應用程式使用*分區化*hello 開發人員以及 hello 系統管理員的挑戰。 hello 用戶端程式庫會簡化 hello 管理工作所提供的工具，可讓這兩種開發人員和系統管理員管理向外延展資料庫。 在典型的範例中，有許多資料庫，又稱為 「 分區 」，toomanage。 客戶會共置於相同資料庫中的 hello 和一個資料庫，每個客戶 （單一租用戶配置）。 hello 用戶端程式庫包含下列功能：

- **分區對應管理**： 建立名為 hello"分區對應管理員 」 的特殊資料庫。 分區對應管理是其分區相關應用程式 toomanage 中繼資料的 hello 功能。 開發人員可以使用此功能 tooregister 資料庫作為分區、 描述對應的個別分區化索引鍵或索引鍵範圍 toothose 資料庫，並維護此中繼資料當做 hello 數字及組合的資料庫中發展 tooreflect 容量變更。 沒有 hello 彈性資料庫用戶端程式庫，您就必須 toospend 大量撰寫 hello 管理程式碼實作分區化時的時間。 如需詳細資訊，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。

- **資料依存路由**： 假設傳入 hello 應用程式的要求。 根據 hello 分區化索引鍵值的 hello 要求，必須正確資料庫根據 hello 索引鍵值 toodetermine hello hello 應用程式。 接著，它會開啟連接 toohello 資料庫 tooprocess hello 要求。 資料依存路由提供 hello 能力 tooopen 連線透過 hello 分區對應到單一輕鬆呼叫 hello 應用程式。 資料依存路由是現在 hello 彈性資料庫用戶端程式庫中的功能所涵蓋的基礎結構程式碼的其他區域。 如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。
- **多分區查詢 (MSQ)**：當要求牽涉到數個 (或所有) 分區時，多分區查詢就派上用場。 執行多個分區查詢 hello 所有分區或分區的一組相同的 T-SQL 程式碼。 從參與分區的 hello hello 結果會合併到整體的結果集使用 UNION ALL 的語意。 hello 所透過 hello 用戶端程式庫公開的功能會處理許多工作，包括： 連線管理、 執行緒管理、 錯誤處理和處理的中繼結果。 MSQ 可以向上 toohundreds 分區的查詢。 如需詳細資訊，請參閱 [多分區查詢](sql-database-elastic-scale-multishard-querying.md)。

一般情況下，使用彈性資料庫工具的客戶可以預期 tooget 完整 T-SQL 功能，做為有自己的語意，但不要的 toocross 分區作業提交分區本機作業時。

## <a name="next-steps"></a>後續步驟
再試一次 hello[範例應用程式](sql-database-elastic-scale-get-started.md)示範 hello 用戶端功能。 

tooinstall hello 程式庫，請移太[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。

如需使用 hello 分割合併工具的指示，請參閱 hello[分割合併工具概觀](sql-database-elastic-scale-overview-split-and-merge.md)。

[彈性資料庫用戶端程式庫現在已開放原始碼！](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

使用 [彈性查詢](sql-database-elastic-query-overview.md)。

hello 程式庫可做為開放原始碼軟體上[GitHub](https://github.com/Azure/elastic-db-tools)。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

