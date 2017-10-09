---
title: "Azure SQL 資料倉儲 Data Factory aaaLoad 資料 |Microsoft 文件"
description: "本教學課程使用 Azure Data Factory，將資料載入 Azure SQL 資料倉儲和當做 hello 資料來源會使用 SQL Server 資料庫。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>使用 Data Factory 將資料載入 SQL 資料倉儲

您可以使用 Azure Data Factory tooload 資料到 Azure SQL 資料倉儲，從任何 hello[支援來源資料存放區](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 例如，您可以使用 Data Factory，將 Azure SQL Database 或 Oracle 資料庫中的資料載入 SQL 資料倉儲。 本文章中的教學課程會示範如何 tooload 資料從內部部署 SQL Server 資料庫到 SQL 資料倉儲。

**估計時間**： 本教學課程，大約需要 10-15 分鐘 toocomplete 一旦符合 hello 必要條件。

## <a name="prerequisites"></a>必要條件

- 您需要**SQL Server 資料庫**包含 hello 資料的資料表與 toobe 複製 toohello SQL 資料倉儲。  

- 您需要線上 **SQL 資料倉儲**。 如果您已經沒有資料倉儲，了解如何太[建立 Azure SQL 資料倉儲](sql-data-warehouse-get-started-provision.md)。

- 您需要 **Azure 儲存體帳戶**。 如果您已經沒有儲存體帳戶，了解如何太[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)。 為了達到最佳效能，找出 hello 儲存體帳戶和 hello 資料倉儲中 hello 相同 Azure 區域。

## <a name="configure-a-data-factory"></a>設定 Data Factory
1. 登入 toohello [Azure 入口網站][]。
2. 找出您的資料倉儲，並按一下 tooopen 它。
3. 在 hello 主要刀鋒視窗中，按一下 **將資料載入** > **Azure Data Factory**。

    ![啟動載入資料精靈](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. 如果您的 Azure 訂用帳戶中沒有 data factory，您會看到**新的 Data Factory** hello 瀏覽器 對話方塊中的個別索引標籤。 Hello 中的填入要求的詳細資訊，並按一下**建立**。 建立 hello 資料處理站之後，hello**新的 Data Factory**對話框會關閉，而且您看見 hello**選取 Data Factory**  對話方塊。

    如果您有一或多個 data factory 已在 hello Azure 訂用帳戶，請參閱 hello**選取 Data Factory**  對話方塊。 在這個對話方塊中，您可以選取現有的 data factory，或按一下**建立新的 data factory** toocreate 新建一個。

    ![設定 Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. 在 hello**選取 Data Factory**對話方塊中，hello**載入資料**預設會選取選項。 按一下**下一步**toostart 建立資料載入工作。

## <a name="configure-hello-data-factory-properties"></a>設定 hello 資料 factory 屬性
現在您已經建立 data factory，hello 下一個步驟是 tooconfigure hello 資料載入排程。

1. 針對 [工作名稱]，輸入 [DWLoadData fromSQLServer]。
2. 使用預設的 hello**執行一次現在**選項，請按一下**下一步**。

    ![設定負載排程](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>設定 hello 來源資料存放區和閘道
現在您要從中 tooload 資料 hello 在內部部署 SQL Server 資料庫的相關分辨 Data Factory。

1. 選擇**SQL Server** hello 支援來源資料存放區目錄，然後按一下**下一步**。

    ![選擇 SQL Server 來源](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A**指定 hello 在內部部署 SQL Server 資料庫**對話方塊隨即出現。 第一次 hello**連接名稱**欄位會自動填入。 hello 第二個欄位會要求輸入 hello hello 名稱**閘道**。 如果您使用現有的 data factory 已有閘道，您可以從 hello 下拉式清單中選取重複使用 hello 閘道。 按一下 hello**建立閘道**連結 toocreate 資料管理閘道器。  

    > [!NOTE]
    > 如果 hello 來源資料儲存在內部部署或在 Azure IaaS 虛擬機器，就需要資料管理閘道。 閘道與 Data Factory 有 1 對 1 關聯性。 它不能從另一個 data factory，但是可供多個資料載入與 hello 中的工作相同的 data factory。 閘道可以是使用的 tooconnect toomultiple 資料存放區時執行資料載入工作。
    >
    > 如需 hello 閘道的詳細資訊，請參閱[資料管理閘道器](../data-factory/data-factory-data-management-gateway.md)發行項。

3. 隨即出現 [建立閘道] 對話方塊。 針對名稱，輸入 **GatewayForDWLoading**，然後按一下 [建立]。

4. 隨即出現 [設定閘道] 對話方塊。 按一下**啟動此電腦上的快速安裝**tooautomatically 下載、 安裝及註冊目前電腦上的資料管理閘道器。 hello 進度會顯示快顯視窗中。 如果 hello 電腦無法連線 toohello 資料存放區，您可以手動[下載並安裝 hello 閘道](https://www.microsoft.com/download/details.aspx?id=39717)toohello 資料可以連接的電腦上儲存和使用 hello 金鑰 tooregister。
    > [!NOTE]
    > hello 快速安裝適用於原生 Microsoft Edge 及 Internet Explorer。 如果您使用 Google Chrome，先安裝 hello ClickOnce 延伸模組從 Chrome web 存放區。

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. 等候 hello 閘道安裝程式 toocomplete。 Hello 閘道註冊成功，且已上線，一旦 hello 快顯視窗關閉，而 hello 新的閘道會出現在 hello 閘道 欄位中。 然後在 hello 其餘部分填滿必要欄位，如下所示，然後按一下 **下一步**。
    - **伺服器名稱**: hello 名稱內部部署 SQL Server。
    - **資料庫名稱**：SQL Server 資料庫。
    - **認證加密**: hello 預設使用 」 的網頁瀏覽器 」。
    - **驗證類型**： 選擇您要使用的驗證 hello 類型。
    - **使用者名稱**和**密碼**: hello 使用者名稱和密碼輸入具有權限 toocopy hello 資料的使用者。

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. hello 下一個步驟就是從哪一個 toocopy hello 資料 toochoose hello 資料表。 您可以使用關鍵字篩選 hello 資料表。 然後您可以預覽 hello 下方面板中的 hello 資料和資料表結構描述。 在完成您的選擇之後，按 [下一步]。

    ![選取資料表](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>設定 hello 目的地，您的 SQL 資料倉儲

現在您告訴 hello 目的地資訊 Data Factory。

1. 您的 SQL 資料倉儲連接資訊會自動填入。 輸入 hello 密碼 hello 使用者名稱。 然後按 [下一步]。

    ![設定目的地](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. 智慧型資料表對應會顯示對應來源 toodestination 資料表為基礎的資料表名稱。 如果 hello 資料表不存在於 hello 目的地中，依預設 ADF 會建立一個以 hello （這適用於 tooSQL 伺服器或 Azure SQL Database 當做來源） 相同的名稱。 您也可以選擇 toomap tooan 現有的資料表。 檢閱並按 [下一步]。

    ![對應資料表](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. 檢閱 hello 結構描述對應，並找出錯誤或警告訊息。 智慧型對應是根據資料行名稱。 如果沒有 hello 來源和目的地資料行之間的不支援的資料類型轉換，您會看到一則錯誤訊息一起 hello 對應資料表。 如果您選擇 toolet Data Factory 自動建立 hello 資料表，如果需要來源和目的地存放區之間 toofix hello 不相容，可能會發生適當的資料類型轉換。

    ![對應結構描述](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. 按一下 [下一步] 。

## <a name="configure-hello-performance-settings"></a>設定 hello 效能設定
您可以在 hello 效能組態中，設定用於暫存 hello 資料載入 SQL 資料倉儲 performantly 使用之前的 Azure 儲存體帳戶[PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly)。 Hello 複製完成之後，儲存體中的 hello 暫時資料將會自動清除。

選取現有的 Azure 儲存體帳戶，然後按一下 [下一步]。

![設定預備 blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>檢閱摘要資訊和部署 hello 管線

檢閱 hello 組態，然後按一下**完成**按鈕 toodeploy hello 管線。

![部署 Data Factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>監視資料載入進度

您可以看到 hello 部署進度和結果在 hello**部署**頁面。

1. 一旦完成 hello 部署後，按一下 hello 連結**按一下這裡 toomonitor 複製管線**toomonitor 資料載入進度。

    ![監視管線](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. 新建立的 hello **DWLoadData fromSQLServer**資料載入管線是自動選取從左側的 hello**資源總管**。

    ![檢視管線](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. 按一下至 hello 管線 hello 中間面板 toosee hello 詳細的每個資料表都會對應 tooan 活動的狀態。

    ![檢視資料表活動](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. 進一步按到活動，而且您看見 hello 載入詳細資料，包括資料大小、 資料列、 輸送量等 hello 右面板中的資料。

    ![檢視資料表活動詳細資料](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. 此監視檢視更新，請移 tooyour SQL 資料倉儲中，按一下 toolaunch**載入資料 > Azure Data Factory**，選取您的 factory，然後選擇**監視現有載入工作**。

## <a name="next-steps"></a>後續步驟

toomigrate 您資料庫 tooSQL 資料倉儲時，請參閱[移轉概觀](sql-data-warehouse-overview-migrate.md)。

toolearn 深入了解 Azure Data Factory 和它的資料移動的功能，請參閱下列文章 hello:

- [簡介 tooAzure Data Factory](../data-factory/data-factory-introduction.md)
- [使用複製活動來移動資料](../data-factory/data-factory-data-movement-activities.md)
- [從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore 資料在 SQL 資料倉儲中，請參閱下列文章 hello:

- [與 Visual Studio 和 SSDT 連接 tooSQL 資料倉儲](sql-data-warehouse-query-visual-studio.md)
- [採用 Power BI 的視覺化資料](sql-data-warehouse-get-started-visualize-with-power-bi.md)。

<!-- Azure references -->
[Azure 入口網站]: https://portal.azure.com
