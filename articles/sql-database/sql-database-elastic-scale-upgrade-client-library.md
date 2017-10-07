---
title: "aaaUpgrade toohello 最彈性資料庫用戶端程式庫 |Microsoft 文件"
description: "使用 Nuget 升級應用程式和程式庫"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>升級應用程式 toouse hello 最彈性資料庫用戶端程式庫
新版本的 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)可以透過 Visual Studio 中的 NuGetand hello NuGetPackage 管理員介面。 升級包含 bug 修正，並支援 hello 用戶端程式庫的新功能。

**如需最新版本的 hello:**太移[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。

重建您的應用程式與 hello 新媒體櫃，以及變更現有分區對應管理員中繼資料儲存在 Azure SQL Database toosupport 的新功能。

為了執行這些步驟可確保 hello 用戶端程式庫的舊版時，都是不會再出現在您的環境後，更新中繼資料物件，這表示舊版本的中繼資料物件將不會建立升級之後。   

## <a name="upgrade-steps"></a>升級步驟
**1.升級您的應用程式。** 在 Visual Studio、 下載和參考 hello 最新用戶端程式庫版本對所有使用 hello 程式庫; 您開發專案然後重新建置並部署。 

* 在您的 Visual Studio 解決方案中，依序選取 [工具] -->  [NuGet 套件管理員]  -->  [管理解決方案的 NuGet 套件]。 
* (Visual Studio 2013)在 hello 左面板中，選取**更新**，然後選取 hello**更新**hello 封裝上的按鈕**Azure SQL Database 彈性延展用戶端程式庫**，會出現在 hello視窗。
* (Visual Studio 2015)設定得 hello 篩選方塊**升級可用**。 選取 hello 封裝 tooupdate，然後按一下 [hello**更新**] 按鈕。
* (Visual Studio 2017)在 hello hello 對話方塊頂端，選取**更新**。 選取 hello 封裝 tooupdate，然後按一下 [hello**更新**] 按鈕。
* 建置並部署。 

**2.升級您的指令碼。** 如果您使用**PowerShell**指令碼 toomanage 分區[下載新程式庫版本 hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)並將它複製到您要從中執行指令碼的 hello 目錄。 

**3.升級您的分割合併服務。** 如果您使用 hello 彈性資料庫分割合併工具 tooreorganize 分區化資料，[下載和部署 hello 最新版 hello 工具](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)。 升級的詳細步驟可找到服務的 hello[這裡](sql-database-elastic-scale-overview-split-and-merge.md)。 

**4.升級您的分區對應管理員資料庫**。 升級支援分區對應 Azure SQL Database 中的 hello 中繼資料。  您可以使用 PowerShell 或 C# 來完成此作業。 下面會說明這兩個選項。

***選項 1：使用 PowerShell 升級中繼資料***

1. 從 nuget 下載 hello 最新命令列公用程式[這裡](http://nuget.org/nuget.exe)和 tooa 資料夾會儲存。 
2. 開啟命令提示字元，瀏覽 toohello 相同的資料夾和問題 hello 命令：`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. 瀏覽 toohello 子資料夾包含 hello 新用戶端的 DLL 版本您剛才下載，例如：`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. 從 hello 下載 hello 彈性資料庫用戶端升級程式碼片段[指令碼中心](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)，並儲存到 hello 同一個資料夾包含 hello DLL。
5. 從該資料夾中 hello 命令提示字元執行"PowerShell.\upgrade.ps1 」，並遵循 hello 提示。

***選項 2：使用 C# 升級中繼資料***

或者，建立 Visual Studio 應用程式，開啟您 ShardMapManager、 逐一查看所有分區，以及藉由呼叫 hello 方法執行 hello 中繼資料升級[UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx)和[UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx)如此範例所示： 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

這些中繼資料升級技巧可以套用多次且不會造成損害。 例如，如果較舊的用戶端版本不小心建立分區，您已更新之後，您可以執行升級一次跨所有分區 tooensure 該 hello 最新的中繼資料版本，則整個基礎結構。 

**注意：** hello 用戶端程式庫的新版本發行日期來繼續 toowork 與前一版的 hello 分區對應管理員中繼資料，在 Azure SQL DB，反之亦然。   不過 tootake 利用一些 hello hello 最新用戶端，中繼資料中的新功能需要使用 toobe 升級。   請注意，中繼資料升級不會影響任何使用者資料或應用程式特定資料，只有 hello 分區對應管理員所建立和使用的物件。  而且應用程式繼續 toooperate 透過 hello 上面所述的升級順序。 

## <a name="elastic-database-client-version-history"></a>彈性資料庫用戶端版本歷程記錄
版本歷程記錄，到太[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

