---
title: "（水平資料分割） 的向外延展雲端資料庫之間的 aaaReport |Microsoft 文件"
description: "toouse 如何跨資料庫的資料庫查詢"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>跨相應放大雲端資料庫報告 (預覽)
您可以使用 [彈性查詢](sql-database-elastic-query-overview.md)，從單一連接點的多個 Azure SQL Database 建立報告。 hello 資料庫必須進行水平資料分割 （也稱為 「 分區 」）。

如果您有現有的資料庫，請參閱[移轉現有的資料庫 tooscaled 外資料庫](sql-database-elastic-convert-to-use-elastic-tools.md)。

需要 tooquery 的 toounderstand hello SQL 物件，請參閱[跨水平資料分割的資料庫查詢](sql-database-elastic-query-horizontal-partitioning.md)。

## <a name="prerequisites"></a>必要條件
下載並執行 hello[入門彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>建立分區對應管理員使用 hello 範例應用程式
這裡您將建立的分區對應管理員以及數個分區，後面接著插入資料至 hello 分區。 如果您遇到 tooalready 中有分區安裝過程中的使用分區化資料，您可以略過下列步驟的 hello 和移動 toohello 下一節。

1. 建置並執行 hello**彈性資料庫工具使用者入門**範例應用程式。 步驟 7 hello > 一節中的 hello 步驟[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)。 在步驟 7 hello 最後，您會看到下列命令提示字元中的 hello:

    ![命令提示字元][1]
2. 在 hello 命令視窗中，輸入"1"，然後按**Enter**。 這會建立 hello 分區對應管理員，並將這兩個分區 toohello 伺服器時。 然後輸入"3"，然後按**Enter**; 四次重複 hello 動作。 這會在您的分區中插入範例資料列。
3. hello [Azure 入口網站](https://portal.azure.com)中您的伺服器應該會顯示三個新的資料庫：

   ![Visual Studio 確認][2]

   此時，透過 hello 彈性資料庫用戶端程式庫支援跨資料庫查詢。 例如，使用選項 4 hello 命令視窗中。 hello 查詢結果的多個分區都**UNION ALL**的所有分區 hello 結果。

   Hello 下一節，我們會建立範例資料庫支援之端點的跨分區的 hello 資料更豐富查詢。

## <a name="create-an-elastic-query-database"></a>建立彈性的查詢資料庫
1. 開啟 hello [Azure 入口網站](https://portal.azure.com)並登入。
2. 在 hello 中建立新的 Azure SQL database 分區安裝相同的伺服器。 名稱 hello 資料庫 」 ElasticDBQuery。 」

    ![Azure 入口網站和定價層][3]

    > [!NOTE]
    > 您可以使用現有的資料庫。 如果您可以這樣做，它不得為您想要 tooexecute hello 分區的其中一個查詢。 這個資料庫會用於建立 hello 彈性資料庫查詢的中繼資料物件。
    >

## <a name="create-database-objects"></a>建立資料庫物件
### <a name="database-scoped-master-key-and-credentials"></a>資料庫範圍的主要金鑰和認證
這些是使用的 tooconnect toohello 分區對應管理員與 hello 分區：

1. 在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools
2. 連接 tooElasticDBQuery 資料庫，然後執行下列 T-SQL 命令 hello:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    「 使用者名稱 」 和 「 密碼 」 應該是 hello 相同的步驟 6 中所用的登入資訊為[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)中[彈性資料庫工具使用者入門](sql-database-elastic-scale-get-started.md)。

### <a name="external-data-sources"></a>外部資料來源
toocreate 外部資料來源，執行下列命令 hello ElasticDBQuery 資料庫上的 hello:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 「 CustomerIDShardMap 」 是 hello 分區對應，hello 名稱，如果您建立 hello 分區對應和分區對應管理員使用 hello 彈性資料庫工具範例。 不過，如果您使用您自訂的設定，此範例，它應該是您選擇在您的應用程式中的 hello 分區對應名稱。

### <a name="external-tables"></a>外部資料表
建立藉由執行下列命令 ElasticDBQuery 資料庫上的 hello 符合上 hello 分區 hello Customers 資料表的外部資料表：

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>執行範例彈性資料庫 T-SQL 查詢
一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。

Hello ElasticDBQuery 資料庫上執行下列查詢：

    select count(CustomerId) from [dbo].[Customers]

您會發現該 hello 查詢從所有 hello 分區彙總結果，並提供 hello 下列輸出：

![輸出詳細資料][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>匯入彈性資料庫查詢結果 tooExcel
 您可以匯入 hello 結果的查詢 tooan Excel 檔案。

1. 啟動 Excel 2013。
2. 瀏覽 toohello**資料**功能區。
3. 按一下 [從其他來源]，然後按一下 [從 SQL Server]。

   ![從其他來源的 Excel 匯入][5]
4. 在 hello**資料連線精靈**輸入 hello 伺服器名稱和登入認證。 然後按 [下一步] 。
5. 在 hello 對話方塊**選取 hello 資料庫包含您想要的 hello 資料**，選取 hello **ElasticDBQuery**資料庫。
6. 選取 hello**客戶**hello 清單檢視中資料表，並按一下**下一步**。 然後按一下 [ **完成**]。
7. 在 hello**匯入資料**底下形成**選取您要如何 tooview 這項資料在活頁簿中**，選取**資料表**按一下**[確定]**。

所有 hello 中的資料列**客戶**儲存在不同的分區中的資料表填入 hello Excel 工作表。

您現在可以使用 Excel 強大的資料視覺化功能。 您可以使用與您的伺服器名稱、 資料庫名稱的 hello 連接字串和認證 tooconnect BI 和資料整合工具 toohello 彈性查詢資料庫。 請確定 SQL Server 可支援做為您的工具的資料來源。 您可以參考 toohello 彈性查詢資料庫，就像任何其他 SQL Server 資料庫的外部資料表和連線 toowith 工具的 SQL Server 資料表。

### <a name="cost"></a>成本
沒有另收費用使用 hello 彈性資料庫查詢功能。

如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。

## <a name="next-steps"></a>後續步驟

* 如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。
* 若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。
* 如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)
* 如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)
* 如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
