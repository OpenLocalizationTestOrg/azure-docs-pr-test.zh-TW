---
title: "將 SQL 資料倉儲資料的 aaaLoad tb |Microsoft 文件"
description: "示範如何使用 Azure Data Factory 在 15 分鐘內將 1 TB 的資料載入至 Azure SQL 資料倉儲"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>使用 Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲
[Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)是一種雲端架構、相應放大的資料庫，可處理巨量關聯式與非關聯式資料。  SQL 資料倉儲是以巨量平行處理 (MPP) 架構為基礎，最適用於企業資料倉儲工作負載。  它提供彈性與 hello 彈性 tooscale 存放裝置的雲端及獨立計算。

現在，使用 Azure SQL 資料倉儲比之前使用 **Azure Data Factory** 還要簡單。  Azure Data Factory 是完全受管理的雲端式資料的整合服務，它可以是使用的 toopopulate SQL 資料倉儲的 hello 資料，從您現有的系統，並節省您寶貴的時間時評估 SQL 資料倉儲和建置您的分析解決方案。 以下是 hello 的資料載入到 Azure SQL 資料倉儲使用 Azure Data Factory 的主要優點：

* **向上輕鬆 tooset**: 5 步驟直覺式精靈沒有需要的指令碼。
* **豐富的資料存放區支援**︰一組豐富內部部署和雲端架構資料存放區的內部支援。
* **安全且相容**： 資料經由 HTTPS 或 ExpressRoute，傳送和全域服務組態選項可確保您的資料永遠不會離開 hello 地理界限
* **前所未有的效能，使用 PolyBase** – 使用 Polybase 是 hello 最有效率的方式 toomove 資料到 Azure SQL 資料倉儲。 您可以使用 hello 暫存 blob 」 功能，來達到高負載速度從 hello Polybase 支援預設的 Azure Blob 儲存體，以外的資料存放區的所有類型。

本文章將示範如何 toouse 資料 Factory 複製精靈 tooload 1 TB 資料從 Azure Blob 儲存體到 Azure SQL 資料倉儲中在 15 分鐘，超過 1.2 GBps 輸送量。

本文章提供將資料移到 Azure SQL 資料倉儲中，使用 hello 複製精靈的逐步指示。

> [!NOTE]
>  一般功能相關資訊的 Data Factory 中將資料移至 azure 或從 Azure SQL 資料倉儲，請參閱[從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand](data-factory-azure-sql-data-warehouse-connector.md)發行項。
>
> 您也可以使用 Azure 入口網站、Visual Studio、PowerShell 等來建置管線。請參閱[教學課程： 將資料從 Azure Blob tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)快速逐步解說中，使用 Azure Data Factory 中的 hello 複製活動的逐步指示。  
>
>

## <a name="prerequisites"></a>必要條件
* Azure Blob 儲存體︰這項實驗使用 Azure Blob 儲存體 (GRS) 來儲存 TPC-H 測試資料集。  如果您沒有 Azure 儲存體帳戶，了解[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。
* [-](http://www.tpc.org/tpch/)資料： 我們 toouse-因為 hello 測試資料集內。  您需要 toouse toodo `dbgen` TPC H toolkit，這可協助您產生 hello 資料集。  您可以下載原始程式碼`dbgen`從[TPC 工具](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp)自己，或從下載 hello 編譯二進位檔進行編譯[GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools)。  執行的 dbgen.exe hello 下列命令為 toogenerate 1TB 一般檔案`lineitem`資料表散佈跨 10 個檔案：

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    目前複製 hello 產生檔案 tooAzure Blob。  參照太[使用 Azure Data Factory，從內部部署檔案系統移動資料 tooand](data-factory-onprem-file-system-connector.md)如何 toodo，使用 ADF 複製。    
* Azure SQL 資料倉儲︰這項實驗會將資料載入至使用 6,000 個 DWU 所建立的 Azure SQL 資料倉儲

    請參閱太[建立 Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)如詳細說明如何 toocreate SQL 資料倉儲資料庫。  tooget hello 最佳可能的負載效能到使用 Polybase 的 SQL 資料倉儲，我們選擇的資料倉儲單位 (Dwu) hello 效能設定，也就是 6000 的 Dwu 中允許的數目上限。

  > [!NOTE]
  > 載入時從 Azure Blob，hello 資料載入效能是與呈現直接正比 toohello Dwu hello SQL 資料倉儲設定的數目：
  >
  > 將 1 TB 載入至 1,000 個 DWU SQL 資料倉儲需要 87 分鐘 (~200MBps 輸送量) 將 1 TB 載入至 2,000 個 DWU SQL 資料倉儲需要 46 分鐘 (~380MBps 輸送量) 將 1 TB 載入至 6,000 個 DWU SQL 資料倉儲需要 14 分鐘 (~1.2GBps 輸送量)
  >
  >

    SQL 資料倉儲與 6000 的 Dwu toocreate hello 效能滑桿所有 hello 方式 toohello 向右移動：

    ![效能滑桿](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    針對未設定 6,000 個 DWU 的現有資料庫，您可以使用 Azure 入口網站相應進行增加。  瀏覽 toohello 在 Azure 入口網站的資料庫，而且沒有**標尺**按鈕在 hello**概觀**面板 hello 下列影像所示：

    ![[調整] 按鈕](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    按一下 hello**標尺**按鈕 tooopen hello 下列 面板，移動滑桿 toohello 最大值 hello，然後按一下**儲存** 按鈕。

    ![[調整] 對話方塊](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    這項實驗會將資料載入至使用 `xlargerc` 資源類別的 Azure SQL 資料倉儲。

    tooachieve 最佳可能輸送量，複本需要 toobe 執行使用 SQL 資料倉儲使用者屬於太`xlargerc`資源類別。  深入了解如何 toodo，依照[變更使用者資源類別範例](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。  
* 執行 DDL 陳述式之後的 hello Azure SQL 資料倉儲資料庫中建立目的地資料表的結構描述：

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
有了 hello 先決條件步驟完成，我們現在都會使用 hello 複製精靈 」 準備好 tooconfigure hello 複製活動。

## <a name="launch-copy-wizard"></a>啟動複製精靈
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**+ 新增**從 hello 左上角，按一下 **智慧 + 分析**，然後按一下**Data Factory**。
3. 在 hello**新的 data factory**刀鋒視窗中：

   1. 輸入**LoadIntoSQLDWDataFactory** hello**名稱**。
       hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： **Data factory 名稱"LoadIntoSQLDWDataFactory"不是使用**、 變更 hello hello data factory (例如，yournameLoadIntoSQLDWDataFactory) 名稱，然後再次嘗試重新建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。  
   2. 選取您的 Azure **訂用帳戶**。
   3. 資源群組，請執行步驟的 hello 其中一項：
      1. 選取**使用現有**tooselect 現有的資源群組。
      2. 選取**建立新**tooenter 資源群組的名稱。
   4. 選取**位置**hello data factory。
   5. 選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。  
   6. 按一下 [建立] 。
4. Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：

   ![Data Factory 首頁](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. 在 hello Data Factory 首頁上，按一下 hello**將資料複製**磚 toolaunch**複製精靈**。

   > [!NOTE]
   > 如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**設定 （或） 保留啟用它，並建立的例外狀況**login.microsoftonline.com**，然後再次嘗試重新啟動 hello 精靈。
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>步驟 1︰設定資料載入排程
hello 第一個步驟是 tooconfigure hello 資料載入排程。  

在 hello**屬性**頁面：

1. 輸入 **CopyFromBlobToAzureSqlDataWarehouse** 作為 [工作名稱]
2. 選取 [立即執行一次] 選項。   
3. 按一下 [下一步] 。  

    ![複製精靈 - 屬性頁面](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>步驟 2：設定來源
此區段會顯示 hello 步驟 tooconfigure hello 來源： Azure Blob 包含 hello 1 TB TPC-H 明細項目檔案。

1. 選取 hello **Azure Blob 儲存體**hello 資料存放區，並按一下**下一步**。

    ![複製精靈 - 選取來源頁面](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. 填寫 hello 連線資訊 hello Azure Blob 儲存體帳戶，然後按一下**下一步**。

    ![複製精靈 - 來源連接資訊](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. 選擇 hello**資料夾**包含 hello TPC H 行項目檔案並按一下**下一步**。

    ![複製精靈 - 選取輸入資料夾](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. 按一下後**下一步**，系統會自動偵測 hello 檔案格式設定。  請確定該資料行分隔符號是 toomake ' | '而不是 hello 預設逗號'，'。  按一下**下一步**預覽 hello 資料之後。

    ![複製精靈 - 檔案格式設定](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>步驟 3︰設定目的地
此區段會顯示您如何 tooconfigure hello 目的地： `lineitem` hello Azure SQL 資料倉儲資料庫中的資料表。

1. 選擇**Azure SQL 資料倉儲**做為 hello 目的地存放區，按一下**下一步**。

    ![複製精靈 - 選取目的地資料存放區](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. 填寫 hello Azure SQL 資料倉儲的連接資訊。  請確定您指定 hello 使用者 hello 角色的成員`xlargerc`(請參閱 hello**必要條件**一節以取得詳細指示)，然後按一下**下一步**。

    ![複製精靈 - 目的地連接資訊](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. 選擇 hello 目的地資料表，然後按一下**下一步**。

    ![複製精靈 - 資料表對應頁面](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. 在 [結構描述對應] 頁面中，將 [套用資料行對應] 選項保持不選取，然後按 [下一步]。

## <a name="step-4-performance-settings"></a>步驟 4：效能設定

預設會核取 [允許 Polybase]。  按一下 [下一步] 。

![複製精靈 - 結構描述對應頁面](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>步驟 5︰部署和監視載入結果
1. 按一下**完成**按鈕 toodeploy。

    ![複製精靈 - 摘要頁面](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Hello 部署完成後，按一下`Click here toomonitor copy pipeline`toomonitor hello 複製執行進度。 您建立在 hello 選取 hello 複製管線**活動 Windows**清單。

    ![複製精靈 - 摘要頁面](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    您可以檢視詳細資料以 hello hello 複製**活動視窗總管**在 hello 右面板中，包括 hello 資料磁碟區從來源讀取和寫入目的地、 期間與 hello hello 執行的平均輸送量。

    您可以從下列螢幕擷取畫面中，將 1 TB 從 Azure Blob 儲存體複製到 SQL 資料倉儲的 hello 看到花費了 14 分鐘，有效地達成需要 1.22 GBps 輸送量 ！

    ![複製精靈 - 成功對話方塊](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>最佳作法
以下是執行 Azure SQL 資料倉儲資料庫的一些最佳作法：

* 載入至 CLUSTERED COLUMNSTORE INDEX 時，請使用較大的資源類別。
* 對於更有效率的聯結，請考慮透過選取資料行使用雜湊散發，而不是預設循環配置資源散發。
* 若要更快的載入速度，請考慮使用暫時性資料的堆積。
* 在您完成載入 Azure SQL 資料倉儲之後，請建立統計資料。

如需詳細資料，請參閱 [Azure SQL 資料倉儲最佳作法](../sql-data-warehouse/sql-data-warehouse-best-practices.md)。

## <a name="next-steps"></a>後續步驟
* [資料處理站的複製精靈](data-factory-copy-wizard.md)-本文章提供有關 hello 複製精靈的詳細資料。
* [複製活動效能及微調指南](data-factory-copy-activity-performance.md)-本文章包含 hello 參考效能測量和微調指南。
