---
title: "aaaGet 入門彈性資料庫工具 |Microsoft 文件"
description: "基本的 hello 彈性資料庫工具功能的 Azure SQL Database，包括簡單執行範例應用程式的詳細說明。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>開始使用彈性資料庫工具
本文件介紹您 toohello 開發人員的體驗藉由協助您 toorun hello 範例應用程式。 hello 範例會建立簡單的分區化應用程式，並且瀏覽的彈性資料庫工具的主要功能。 hello 範例示範的 hello 函式[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。

tooinstall hello 程式庫，請移太[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。 hello 程式庫會隨 hello 之後 > 一節中所述的 hello 範例應用程式。

## <a name="prerequisites"></a>必要條件
* 含 C# 的 Visual Studio 2012 或更新版本。 請在 [Visual Studio 下載](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)上下載免費版本。
* NuGet 2.7 或更新版本。 tooget hello 最新版本，請參閱[安裝 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)。

## <a name="download-and-run-hello-sample-app"></a>下載並執行 hello 範例應用程式
hello**彈性的 DB Tools for Azure SQL-快速入門**範例應用程式說明 hello 最重要的 hello 使用彈性資料庫工具的分區化應用程式的開發經驗的觀點。 此範例應用程式著重在[分區對應管理](sql-database-elastic-scale-shard-map-management.md)、[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)和[多分區查詢](sql-database-elastic-scale-multishard-querying.md)的主要使用案例。 toodownload 和執行的 hello 範例，請遵循下列步驟： 

1. 下載 hello[彈性的 DB Tools for Azure SQL-快速入門範例](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6)從 MSDN。 解壓縮您選擇的 hello 範例 tooa 位置。

2. toocreate 專案中，開啟 hello **ElasticScaleStarterKit.sln**解決方案的 hello **C#**目錄。

3. 在 hello hello 範例專案的方案，開啟 hello **app.config**檔案。 您的 Azure SQL Database 伺服器名稱和登入資訊 （使用者名稱和密碼），然後遵循 hello 檔案 tooadd hello 指示進行。

4. 建置並執行 hello 應用程式。 出現提示時，讓 Visual Studio toorestore hello 的 hello 方案的 NuGet 封裝。 這會從 NuGet 下載 hello hello 彈性資料庫用戶端程式庫的最新版本。

5. 試驗 hello 不同選項 toolearn 進一步了解 hello 的用戶端程式庫功能。 請注意 hello 步驟 hello hello 主控台輸出中的應用程式會接受，但覺得 hello 幕後可用 tooexplore hello 程式碼。
   
    ![Progress][4]

恭喜 - 您已使用彈性資料庫工具，在 SQL Database 上成功建置並執行您的第一個分區化應用程式。 使用 Visual Studio 或 SQL Server Management Studio tooconnect tooyour SQL 資料庫，看看 hello 範例建立的 hello 分區快速。 您會注意到新的範例分區化資料庫和分區對應管理員資料庫已建立該 hello 範例。

> [!IMPORTANT]
> 我們建議您一律使用 hello 最新版本的 Management Studio，以便您保持同步更新 tooAzure 與 SQL 資料庫。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>關鍵的 hello 程式碼範例
* **管理分區和分區對應**: hello 程式碼說明如何與分區、 範圍和 hello 檔案中的對應 toowork **ShardManagementUtils.cs**。 如需詳細資訊，請參閱[hello 分區對應管理員與資料庫的延展](http://go.microsoft.com/?linkid=9862595)。  

* **資料依存路由**： 交易 toohello 右分區的路由，如下所示**DataDependentRoutingSample.cs**。 如需詳細資訊，請參閱[資料相依路由](http://go.microsoft.com/?linkid=9862596)。 

* **查詢透過多個分區**： 跨分區查詢如下所示 hello 檔案**MultiShardQuerySample.cs**。 如需詳細資訊，請參閱[多分區查詢](http://go.microsoft.com/?linkid=9862597)。

* **加入空白的分區**: hello hello 檔案中的程式碼所執行 hello 反覆加入新的空白分區**CreateShardSample.cs**。 如需詳細資訊，請參閱[hello 分區對應管理員與資料庫的延展](http://go.microsoft.com/?linkid=9862595)。

### <a name="other-elastic-scale-operations"></a>其他 Elastic Scale 作業
* **分割現有分區**: hello 功能 toosplit 分區係由 hello**分割合併工具**。 如需詳細資訊，請參閱[在向外延展的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)。

* **合併現有分區**： 分區合併也會執行使用 hello**分割合併工具**。 如需詳細資訊，請參閱[在向外延展的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)。   

## <a name="cost"></a>成本
hello 彈性資料庫工具是免費的。 當您使用彈性資料庫工具時，您沒有收到任何額外的費用，在您的 Azure 使用量 hello 成本之上。 

例如，hello 範例應用程式會建立新的資料庫。 這個 hello 成本取決於您選擇的 hello SQL Database 版本和 hello Azure 應用程式的使用量。

如需價格資訊，請參閱 [SQL Database 定價詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。

## <a name="next-steps"></a>後續步驟
如需彈性資料庫工具的詳細資訊，請參閱 hello 下列頁面：

* 程式碼範例： 
  * [適用於 Azure SQL 的彈性 DB 工具 - 開始使用 (英文)](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [適用於 Azure SQL 的彈性 DB 工具 - Entity Framework 整合 (英文)](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [指令碼中心的分區彈性](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* 部落格：[Elastic Scale 公告 (英文)](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy:[實作向外延展使用分區化以 hello 彈性資料庫用戶端程式庫視訊](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* 第 9 頻道：[Elastic Scale 概觀影片 (英文)](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* 討論論壇：[Azure SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* toomeasure 效能：[分區對應管理員的效能計數器](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

