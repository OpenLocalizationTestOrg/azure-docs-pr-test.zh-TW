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
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="0a578-103">使用 Data Factory 將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="0a578-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="0a578-104">您可以使用 Azure Data Factory tooload 資料到 Azure SQL 資料倉儲，從任何 hello[支援來源資料存放區](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="0a578-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0a578-105">例如，您可以使用 Data Factory，將 Azure SQL Database 或 Oracle 資料庫中的資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="0a578-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="0a578-106">本文章中的教學課程會示範如何 tooload 資料從內部部署 SQL Server 資料庫到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="0a578-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="0a578-107">**估計時間**： 本教學課程，大約需要 10-15 分鐘 toocomplete 一旦符合 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="0a578-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a578-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a578-108">Prerequisites</span></span>

- <span data-ttu-id="0a578-109">您需要**SQL Server 資料庫**包含 hello 資料的資料表與 toobe 複製 toohello SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="0a578-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="0a578-110">您需要線上 **SQL 資料倉儲**。</span><span class="sxs-lookup"><span data-stu-id="0a578-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="0a578-111">如果您已經沒有資料倉儲，了解如何太[建立 Azure SQL 資料倉儲](sql-data-warehouse-get-started-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="0a578-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="0a578-112">您需要 **Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0a578-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="0a578-113">如果您已經沒有儲存體帳戶，了解如何太[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="0a578-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0a578-114">為了達到最佳效能，找出 hello 儲存體帳戶和 hello 資料倉儲中 hello 相同 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="0a578-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="0a578-115">設定 Data Factory</span><span class="sxs-lookup"><span data-stu-id="0a578-115">Configure a data factory</span></span>
1. <span data-ttu-id="0a578-116">登入 toohello [Azure 入口網站][]。</span><span class="sxs-lookup"><span data-stu-id="0a578-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="0a578-117">找出您的資料倉儲，並按一下 tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="0a578-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="0a578-118">在 hello 主要刀鋒視窗中，按一下 **將資料載入** > **Azure Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="0a578-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![啟動載入資料精靈](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="0a578-120">如果您的 Azure 訂用帳戶中沒有 data factory，您會看到**新的 Data Factory** hello 瀏覽器 對話方塊中的個別索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0a578-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="0a578-121">Hello 中的填入要求的詳細資訊，並按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="0a578-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="0a578-122">建立 hello 資料處理站之後，hello**新的 Data Factory**對話框會關閉，而且您看見 hello**選取 Data Factory**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0a578-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="0a578-123">如果您有一或多個 data factory 已在 hello Azure 訂用帳戶，請參閱 hello**選取 Data Factory**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0a578-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="0a578-124">在這個對話方塊中，您可以選取現有的 data factory，或按一下**建立新的 data factory** toocreate 新建一個。</span><span class="sxs-lookup"><span data-stu-id="0a578-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![設定 Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="0a578-126">在 hello**選取 Data Factory**對話方塊中，hello**載入資料**預設會選取選項。</span><span class="sxs-lookup"><span data-stu-id="0a578-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="0a578-127">按一下**下一步**toostart 建立資料載入工作。</span><span class="sxs-lookup"><span data-stu-id="0a578-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="0a578-128">設定 hello 資料 factory 屬性</span><span class="sxs-lookup"><span data-stu-id="0a578-128">Configure hello data factory properties</span></span>
<span data-ttu-id="0a578-129">現在您已經建立 data factory，hello 下一個步驟是 tooconfigure hello 資料載入排程。</span><span class="sxs-lookup"><span data-stu-id="0a578-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="0a578-130">針對 [工作名稱]，輸入 [DWLoadData fromSQLServer]。</span><span class="sxs-lookup"><span data-stu-id="0a578-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="0a578-131">使用預設的 hello**執行一次現在**選項，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0a578-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![設定負載排程](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="0a578-133">設定 hello 來源資料存放區和閘道</span><span class="sxs-lookup"><span data-stu-id="0a578-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="0a578-134">現在您要從中 tooload 資料 hello 在內部部署 SQL Server 資料庫的相關分辨 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="0a578-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="0a578-135">選擇**SQL Server** hello 支援來源資料存放區目錄，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0a578-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![選擇 SQL Server 來源](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="0a578-137">A**指定 hello 在內部部署 SQL Server 資料庫**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0a578-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="0a578-138">第一次 hello**連接名稱**欄位會自動填入。</span><span class="sxs-lookup"><span data-stu-id="0a578-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="0a578-139">hello 第二個欄位會要求輸入 hello hello 名稱**閘道**。</span><span class="sxs-lookup"><span data-stu-id="0a578-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="0a578-140">如果您使用現有的 data factory 已有閘道，您可以從 hello 下拉式清單中選取重複使用 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="0a578-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="0a578-141">按一下 hello**建立閘道**連結 toocreate 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="0a578-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="0a578-142">如果 hello 來源資料儲存在內部部署或在 Azure IaaS 虛擬機器，就需要資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0a578-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="0a578-143">閘道與 Data Factory 有 1 對 1 關聯性。</span><span class="sxs-lookup"><span data-stu-id="0a578-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="0a578-144">它不能從另一個 data factory，但是可供多個資料載入與 hello 中的工作相同的 data factory。</span><span class="sxs-lookup"><span data-stu-id="0a578-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="0a578-145">閘道可以是使用的 tooconnect toomultiple 資料存放區時執行資料載入工作。</span><span class="sxs-lookup"><span data-stu-id="0a578-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="0a578-146">如需 hello 閘道的詳細資訊，請參閱[資料管理閘道器](../data-factory/data-factory-data-management-gateway.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="0a578-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="0a578-147">隨即出現 [建立閘道] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0a578-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="0a578-148">針對名稱，輸入 **GatewayForDWLoading**，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0a578-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="0a578-149">隨即出現 [設定閘道] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0a578-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="0a578-150">按一下**啟動此電腦上的快速安裝**tooautomatically 下載、 安裝及註冊目前電腦上的資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="0a578-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="0a578-151">hello 進度會顯示快顯視窗中。</span><span class="sxs-lookup"><span data-stu-id="0a578-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="0a578-152">如果 hello 電腦無法連線 toohello 資料存放區，您可以手動[下載並安裝 hello 閘道](https://www.microsoft.com/download/details.aspx?id=39717)toohello 資料可以連接的電腦上儲存和使用 hello 金鑰 tooregister。</span><span class="sxs-lookup"><span data-stu-id="0a578-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="0a578-153">hello 快速安裝適用於原生 Microsoft Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="0a578-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="0a578-154">如果您使用 Google Chrome，先安裝 hello ClickOnce 延伸模組從 Chrome web 存放區。</span><span class="sxs-lookup"><span data-stu-id="0a578-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="0a578-156">等候 hello 閘道安裝程式 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="0a578-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="0a578-157">Hello 閘道註冊成功，且已上線，一旦 hello 快顯視窗關閉，而 hello 新的閘道會出現在 hello 閘道 欄位中。</span><span class="sxs-lookup"><span data-stu-id="0a578-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="0a578-158">然後在 hello 其餘部分填滿必要欄位，如下所示，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="0a578-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="0a578-159">**伺服器名稱**: hello 名稱內部部署 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="0a578-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="0a578-160">**資料庫名稱**：SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a578-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="0a578-161">**認證加密**: hello 預設使用 」 的網頁瀏覽器 」。</span><span class="sxs-lookup"><span data-stu-id="0a578-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="0a578-162">**驗證類型**： 選擇您要使用的驗證 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="0a578-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="0a578-163">**使用者名稱**和**密碼**: hello 使用者名稱和密碼輸入具有權限 toocopy hello 資料的使用者。</span><span class="sxs-lookup"><span data-stu-id="0a578-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="0a578-165">hello 下一個步驟就是從哪一個 toocopy hello 資料 toochoose hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="0a578-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="0a578-166">您可以使用關鍵字篩選 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="0a578-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="0a578-167">然後您可以預覽 hello 下方面板中的 hello 資料和資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="0a578-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="0a578-168">在完成您的選擇之後，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a578-168">After you finish your selection, click **Next**.</span></span>

    ![選取資料表](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="0a578-170">設定 hello 目的地，您的 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="0a578-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="0a578-171">現在您告訴 hello 目的地資訊 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="0a578-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="0a578-172">您的 SQL 資料倉儲連接資訊會自動填入。</span><span class="sxs-lookup"><span data-stu-id="0a578-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="0a578-173">輸入 hello 密碼 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0a578-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="0a578-174">然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a578-174">and click **Next**.</span></span>

    ![設定目的地](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="0a578-176">智慧型資料表對應會顯示對應來源 toodestination 資料表為基礎的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="0a578-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="0a578-177">如果 hello 資料表不存在於 hello 目的地中，依預設 ADF 會建立一個以 hello （這適用於 tooSQL 伺服器或 Azure SQL Database 當做來源） 相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a578-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="0a578-178">您也可以選擇 toomap tooan 現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="0a578-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="0a578-179">檢閱並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a578-179">Review and click **Next**.</span></span>

    ![對應資料表](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="0a578-181">檢閱 hello 結構描述對應，並找出錯誤或警告訊息。</span><span class="sxs-lookup"><span data-stu-id="0a578-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="0a578-182">智慧型對應是根據資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="0a578-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="0a578-183">如果沒有 hello 來源和目的地資料行之間的不支援的資料類型轉換，您會看到一則錯誤訊息一起 hello 對應資料表。</span><span class="sxs-lookup"><span data-stu-id="0a578-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="0a578-184">如果您選擇 toolet Data Factory 自動建立 hello 資料表，如果需要來源和目的地存放區之間 toofix hello 不相容，可能會發生適當的資料類型轉換。</span><span class="sxs-lookup"><span data-stu-id="0a578-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![對應結構描述](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="0a578-186">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0a578-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="0a578-187">設定 hello 效能設定</span><span class="sxs-lookup"><span data-stu-id="0a578-187">Configure hello performance settings</span></span>
<span data-ttu-id="0a578-188">您可以在 hello 效能組態中，設定用於暫存 hello 資料載入 SQL 資料倉儲 performantly 使用之前的 Azure 儲存體帳戶[PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly)。</span><span class="sxs-lookup"><span data-stu-id="0a578-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="0a578-189">Hello 複製完成之後，儲存體中的 hello 暫時資料將會自動清除。</span><span class="sxs-lookup"><span data-stu-id="0a578-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="0a578-190">選取現有的 Azure 儲存體帳戶，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a578-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![設定預備 blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="0a578-192">檢閱摘要資訊和部署 hello 管線</span><span class="sxs-lookup"><span data-stu-id="0a578-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="0a578-193">檢閱 hello 組態，然後按一下**完成**按鈕 toodeploy hello 管線。</span><span class="sxs-lookup"><span data-stu-id="0a578-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![部署 Data Factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="0a578-195">監視資料載入進度</span><span class="sxs-lookup"><span data-stu-id="0a578-195">Monitor data loading progress</span></span>

<span data-ttu-id="0a578-196">您可以看到 hello 部署進度和結果在 hello**部署**頁面。</span><span class="sxs-lookup"><span data-stu-id="0a578-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="0a578-197">一旦完成 hello 部署後，按一下 hello 連結**按一下這裡 toomonitor 複製管線**toomonitor 資料載入進度。</span><span class="sxs-lookup"><span data-stu-id="0a578-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![監視管線](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="0a578-199">新建立的 hello **DWLoadData fromSQLServer**資料載入管線是自動選取從左側的 hello**資源總管**。</span><span class="sxs-lookup"><span data-stu-id="0a578-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![檢視管線](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="0a578-201">按一下至 hello 管線 hello 中間面板 toosee hello 詳細的每個資料表都會對應 tooan 活動的狀態。</span><span class="sxs-lookup"><span data-stu-id="0a578-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![檢視資料表活動](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="0a578-203">進一步按到活動，而且您看見 hello 載入詳細資料，包括資料大小、 資料列、 輸送量等 hello 右面板中的資料。</span><span class="sxs-lookup"><span data-stu-id="0a578-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![檢視資料表活動詳細資料](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="0a578-205">此監視檢視更新，請移 tooyour SQL 資料倉儲中，按一下 toolaunch**載入資料 > Azure Data Factory**，選取您的 factory，然後選擇**監視現有載入工作**。</span><span class="sxs-lookup"><span data-stu-id="0a578-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a578-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a578-206">Next steps</span></span>

<span data-ttu-id="0a578-207">toomigrate 您資料庫 tooSQL 資料倉儲時，請參閱[移轉概觀](sql-data-warehouse-overview-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="0a578-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="0a578-208">toolearn 深入了解 Azure Data Factory 和它的資料移動的功能，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="0a578-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="0a578-209">簡介 tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0a578-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="0a578-210">使用複製活動來移動資料</span><span class="sxs-lookup"><span data-stu-id="0a578-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="0a578-211">從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand</span><span class="sxs-lookup"><span data-stu-id="0a578-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="0a578-212">tooexplore 資料在 SQL 資料倉儲中，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="0a578-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="0a578-213">與 Visual Studio 和 SSDT 連接 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="0a578-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="0a578-214">[採用 Power BI 的視覺化資料](sql-data-warehouse-get-started-visualize-with-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="0a578-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure 入口網站]: https://portal.azure.com
