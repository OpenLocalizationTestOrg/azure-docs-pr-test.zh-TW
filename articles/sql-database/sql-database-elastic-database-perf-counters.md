---
title: "分區對應管理員 aaaPerformance 計數器"
description: "ShardMapManager 類別與資料相依路由效能計數器"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>分區對應管理員的效能計數器
您可以擷取的 hello 效能[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)，特別是在使用[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)。 計數器會建立與 hello Microsoft.Azure.SqlDatabase.ElasticScale.Client 類別的方法。  

計數器是使用的 tootrack hello 效能[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)作業。 這些計數器是在 hello 效能監視之下 hello 「 彈性資料庫:: 分區管理 」 類別目錄中存取。

**如需最新版本的 hello:**太移[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。 另請參閱[升級應用程式 toouse hello 最彈性資料庫用戶端程式庫](sql-database-elastic-scale-upgrade-client-library.md)。

## <a name="prerequisites"></a>必要條件
* hello toocreate hello 效能分類和計數器，使用者必須屬於 hello 本機**管理員**hello 裝載 hello 應用程式的電腦上的群組。  
* toocreate 效能計數器執行個體，然後更新 hello 計數器、 hello 使用者必須屬於其中一個 hello**管理員**或**Performance Monitor Users**群組。 

## <a name="create-performance-category-and-counters"></a>建立效能類別和計數器
toocreate hello 計數器，請呼叫 hello hello CreatePeformanceCategoryAndCounters 方法[ShardMapManagmentFactory 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)。 只有系統管理員可以執行 hello 方法： 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

您也可以使用[這](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283)PowerShell 指令碼 tooexecute hello 方法。 hello 方法會建立下列效能計數器的 hello:  

* **快取對應**: hello 分區對應快取對應的數目。
* **DDR 作業數/秒**： 資料依存路由作業 hello 分區對應的速率。 當呼叫時，會更新這個計數器太[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)導致連線成功 toohello 目的地分區。 
* **對應查閱快取點擊/秒**: hello 分區對應中對應的成功的快取查閱作業的速率。 
* **對應查閱快取遺漏數/秒**: hello 分區對應中對應的失敗的快取查閱作業的速率。
* **對應中新增或更新快取/sec**： 正在加入的對應或 hello 分區對應中更新之快取的速率。 
* **從快取每秒移除的對應**： 會從快取中的 hello 分區對應移除對應的速率。 

效能計數器會在每個程序針對每個快取的分區對應建立。  

## <a name="notes"></a>注意事項
hello 下列事件觸發程序建立 hello hello 效能計數器：  

* 初始化 hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)與[積極式載入](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)，如果 hello ShardMapManager 包含任何分區對應。 這些包括 hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29)和 hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)方法。
* 成功查閱分區對應 (使用 [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx)、[GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 或 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx))。 
* 使用 CreateShardMap() 成功建立分區對應。

hello 分區對應與對應上執行的所有快取作業就會更新 hello 效能計數器。 成功移除刪除的 hello 效能計數器執行個體使用 DeleteShardMap （) reults hello 分區對應。  

## <a name="best-practices"></a>最佳作法
* 建立 hello 效能分類和計數器，應執行一次 hello ShardMapManager 物件建立之前。 每次執行 hello 命令 CreatePerformanceCategoryAndCounters() 清除 hello 先前計數器 （遺失所有執行個體所報告的資料），並建立新的。  
* 每個程序都會建立效能計數器執行個體。 任何應用程式損毀或移除分區對應從 hello 快取會導致刪除 hello 效能計數器執行個體。  

### <a name="see-also"></a>另請參閱
[彈性資料庫功能概觀](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

