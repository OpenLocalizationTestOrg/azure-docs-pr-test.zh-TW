---
title: "aaaUse Redgate tooload 資料 tooyour Azure 資料倉儲 |Microsoft 文件"
description: "深入了解如何針對資料倉儲案例 toouse Redgate 資料平台 Studio。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>使用 Redgate 資料平台 Studio 載入資料
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

本教學課程示範如何 toouse [Redgate 的資料平台 Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP) toomove 資料從內部部署 SQL Server tooAzure SQL 資料倉儲。 資料平台 Studio 套用 hello 最適當的相容性修正程式，並最佳化，所以其 quickest hello 方式 tooget 開始使用 SQL 資料倉儲。

> [!NOTE]
> [Redgate](http://www.red-gate.com) 是長期的 Microsoft 合作夥伴，提供各種 SQL Server 工具。 在資料平台 Studio 中的這項功能已免費提供商業和非商業使用。
> 
> 

## <a name="before-you-begin"></a>開始之前
### <a name="create-or-identify-resources"></a>建立或識別資源
開始之前本教學課程，您需要 toohave:

* **在內部部署 SQL Server 資料庫**: hello 想 tooimport tooSQL 資料倉儲需要從內部部署 SQL Server toocome 資料 (版本 2008 r2 或更新版本)。 資料平台 Studio 無法直接從 Azure SQL Database 或文字檔匯入資料。
* **Azure 儲存體帳戶**： 資料平台 Studio 設置 hello Azure Blob 儲存體中的資料載入到 SQL 資料倉儲之前。 hello 儲存體帳戶都必須使用 hello 「 資源管理員 」 部署模型 （hello 預設值） 而不 hello 「 傳統 」 部署模型。 如果您沒有儲存體帳戶，了解如何 tooCreate 儲存體帳戶。 
* **SQL 資料倉儲**： 本教學課程移動 hello 資料從內部部署 SQL Server tooSQL 資料倉儲，因此您需要 toohave 資料倉儲線上。 如果您已經沒有資料倉儲，了解如何 tooCreate Azure SQL 資料倉儲。

> [!NOTE]
> 如果 hello 儲存體帳戶和 hello 資料倉儲中建立 hello 相同提升的效能區域。
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>步驟 1： 登入 tooData Studio 平台與 Azure 帳戶
開啟網頁瀏覽器並瀏覽 toohello[資料平台 Studio](https://www.dataplatformstudio.com/)網站。 登入與 hello 相同 Azure 帳戶，您使用的 toocreate hello 儲存體帳戶和資料倉儲。 如果您的電子郵件地址是工作或學校帳戶和 Microsoft 帳戶相關聯，是確定 toochoose hello 帳戶具有存取 tooyour 資源。

> [!NOTE]
> 這是您第一次使用的資料平台 Studio 時，如果您是系統 toogrant hello 應用程式的權限 toomanage 要求您的 Azure 資源。
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>步驟 2： 開始 hello 匯入精靈
在 hello DP 主畫面上，選取 [hello 匯入 tooAzure SQL 資料倉儲連結 toostart hello 匯入精靈]。

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>步驟 3： 安裝 hello 資料平台 Studio 閘道
tooconnect tooyour 在內部部署 SQL Server 資料庫，您必須 tooinstall hello DP 閘道。 hello 閘道是用戶端代理程式，提供存取 tooyour 在內部部署環境中，擷取 hello 資料，然後將它上載 tooyour 儲存體帳戶。 您的資料永遠不會通過 Redgate 的伺服器。 tooinstall hello 閘道：

1. 按一下 hello**建立閘道**連結
2. 下載並安裝 hello 閘道使用 hello 提供安裝程式

![][2]

> [!NOTE]
> hello 閘道可以安裝在與網路存取 toohello 來源 SQL Server 資料庫的任何電腦上。 它會存取 hello hello hello 目前使用者的認證搭配使用 Windows 驗證的 SQL Server 資料庫。
> 
> 

安裝之後，hello 閘道狀態變更 tooConnected，您可以選取 [下一步]。

## <a name="step-4-identify-hello-source-database"></a>步驟 4： 識別 hello 來源資料庫
在 hello*輸入伺服器名稱*文字方塊中，輸入 hello hello 伺服器裝載您的資料庫名稱，然後選取**下一步**。 然後，從 hello 下拉式選單，選取您想要從 tooimport 資料 hello 資料庫。

![][3]

DP 會檢查資料表 tooimport hello 選取的資料庫。 根據預設，DP 匯入 hello 資料庫中的所有 hello 資料表。 您可以選取或取消選取資料表，方法是展開的 hello 所有資料表的都連結。 選取 hello 下一步 按鈕 toomove 向前復原。

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>步驟 5： 選擇儲存體帳戶 toostage hello 資料
DP 會提示您輸入位置 toostage hello 資料。 從您的訂用帳戶選擇現有的儲存體帳戶，並選取 [下一步]。

> [!NOTE]
> DP 會在 hello 選擇儲存體帳戶中建立新的 blob 容器，並使用每個匯入不同的資料夾。
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>步驟 6：建立資料倉儲
接下來，選取線上[Azure SQL 資料倉儲](http://aka.ms/sqldw)資料庫 tooimport hello 資料。 一旦您已選取您的資料庫，您需要 tooenter hello 認證 tooconnect toohello 資料庫，並選取**下一步**。

![][5]

> [!NOTE]
> DP 合併到 hello 資料倉儲的 hello 來源資料的資料表。 DP 會警告您如果 hello 資料表名稱需要 toooverwrite hello 資料倉儲中現有的資料表。 您可以選擇性地刪除 hello 資料倉儲中的任何現有物件的計時刪除之前匯入所有現有的物件。
> 
> 

## <a name="step-7-import-hello-data"></a>步驟 7: Hello 資料匯入
DP 確認您想要 tooimport hello 資料。 只要按一下 hello 開始匯入 按鈕 toobegin hello 資料匯入。

![][6]

DP 顯示視覺效果顯示 hello 進行擷取，並上傳 hello hello 在內部部署 SQL Server 和 hello 的進度 hello 匯入至 SQL 資料倉儲的資料。

![][7]

Hello 匯入完成之後，DP 顯示 hello 資料匯入的摘要以及變更報表已執行之 hello 相容性修正程式。

![][8]

## <a name="next-steps"></a>後續步驟
tooexplore 藉由檢視啟動 SQL 資料倉儲中的資料：

* [查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [使用 Power BI 視覺化資料][Visualize data with Power BI]

深入了解 Redgate 的資料平台 Studio toolearn:

* [請瀏覽 hello DP 首頁](http://www.dataplatformstudio.com/)
* [在 Channel9 上觀看 DPS 的示範](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

如需的其他方式 toomigrate 和負載概觀請參閱 SQL 資料倉儲中的資料：

* [移轉您的方案 tooSQL 資料倉儲][Migrate your solution tooSQL Data Warehouse]
* [將資料載入 Azure SQL 資料倉儲](sql-data-warehouse-overview-load.md)

如需開發秘訣，請參閱 hello [SQL 資料倉儲開發概觀](sql-data-warehouse-overview-develop.md)。

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
