---
title: "將資料載入 Azure SQL 資料倉儲 – Data Factory | Microsoft Docs"
description: "本教學課程使用 Azure Data Factory 將資料載入 Azure SQL 資料倉儲，並使用 SQL Server 資料庫作為資料來源。"
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
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="64868-103">使用 Data Factory 將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="64868-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="64868-104">您可以從任何[支援來源資料存放區](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)，使用 Azure Data Factory 將資料載入至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="64868-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="64868-105">例如，您可以使用 Data Factory，將 Azure SQL Database 或 Oracle 資料庫中的資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="64868-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="64868-106">本文中的教學課程會示範如何從內部部署 SQL Server 資料庫將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="64868-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="64868-107">**預估時間**︰一旦符合先決條件後，本教學課程需要大約 10-15 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="64868-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64868-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="64868-108">Prerequisites</span></span>

- <span data-ttu-id="64868-109">您需要 **SQL Server 資料庫**，其中的資料表含有要複製到 SQL 資料倉儲的資料。</span><span class="sxs-lookup"><span data-stu-id="64868-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="64868-110">您需要線上 **SQL 資料倉儲**。</span><span class="sxs-lookup"><span data-stu-id="64868-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="64868-111">如果您還沒有資料倉儲，請了解如何[建立 Azure SQL 資料倉儲](sql-data-warehouse-get-started-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="64868-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="64868-112">您需要 **Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="64868-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="64868-113">如果您還沒有儲存體帳戶，請了解如何[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="64868-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="64868-114">為了達到最佳效能，在相同的 Azure 區域中找出儲存體帳戶和資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="64868-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="64868-115">設定 Data Factory</span><span class="sxs-lookup"><span data-stu-id="64868-115">Configure a data factory</span></span>
1. <span data-ttu-id="64868-116">登入 [Azure 入口網站][]。</span><span class="sxs-lookup"><span data-stu-id="64868-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="64868-117">找出您的資料倉儲，並按一下以開啟它。</span><span class="sxs-lookup"><span data-stu-id="64868-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="64868-118">在主要刀鋒視窗中，按一下 [載入資料] > [Azure Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="64868-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![啟動載入資料精靈](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="64868-120">如果您在 Azure 訂用帳戶中沒有 Data Factory，您會在瀏覽器的個別索引標籤中看到 [新增 Data Factory]對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="64868-121">填入必要的資訊，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="64868-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="64868-122">建立 Data Factory 之後，[新增 Data Factory] 對話方塊隨即關閉，而且您會看到 [選取 Data Factory] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="64868-123">如果您在 Azure 訂用帳戶中已有一或多個 Data Factory，您會看到[選取 Data Factory] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="64868-124">在這個對話方塊中，您可以選取現有的 Data Factory，或按一下[建立新的 Data Factory] 來建立新的。</span><span class="sxs-lookup"><span data-stu-id="64868-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![設定 Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="64868-126">在 [選取 Data Factory] 對話方塊中，預設會選取 [載入資料] 選項。</span><span class="sxs-lookup"><span data-stu-id="64868-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="64868-127">按 [下一步] 以開始建立資料載入工作。</span><span class="sxs-lookup"><span data-stu-id="64868-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="64868-128">設定 Data Factory 屬性</span><span class="sxs-lookup"><span data-stu-id="64868-128">Configure the data factory properties</span></span>
<span data-ttu-id="64868-129">現在您已建立 Data Factory，下一個步驟是設定資料載入排程。</span><span class="sxs-lookup"><span data-stu-id="64868-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="64868-130">針對 [工作名稱]，輸入 [DWLoadData fromSQLServer]。</span><span class="sxs-lookup"><span data-stu-id="64868-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="64868-131">使用預設的 [立即執行一次] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![設定負載排程](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="64868-133">設定來源資料存放區和閘道器</span><span class="sxs-lookup"><span data-stu-id="64868-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="64868-134">現在您要通知 Data Factory 關於您要載入資料的內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64868-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="64868-135">從支援的來源資料儲存類別目錄選擇 **SQL Server**，並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![選擇 SQL Server 來源](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="64868-137">隨即出現 [指定內部部署 SQL Server 資料庫] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="64868-138">第一個 [連接名稱] 欄位會自動填入。</span><span class="sxs-lookup"><span data-stu-id="64868-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="64868-139">第二個欄位會詢問 [閘道器] 的名稱。</span><span class="sxs-lookup"><span data-stu-id="64868-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="64868-140">如果您使用的現有 Data Factory 已有一個閘道，您可以藉由從下拉式清單中選取它來重複使用閘道。</span><span class="sxs-lookup"><span data-stu-id="64868-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="64868-141">按一下 [建立閘道] 連結以建立資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="64868-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="64868-142">如果來源資料存放區是在內部部署或在 Azure IaaS 虛擬機器中，資料管理閘道是必要的。</span><span class="sxs-lookup"><span data-stu-id="64868-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="64868-143">閘道與 Data Factory 有 1 對 1 關聯性。</span><span class="sxs-lookup"><span data-stu-id="64868-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="64868-144">它不能從另一個 Data Factory 使用，但可供相同 Data Factory 中的多個資料載入工作使用。</span><span class="sxs-lookup"><span data-stu-id="64868-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="64868-145">閘道可以用來在執行資料載入工作時連接至多個資料存放區。</span><span class="sxs-lookup"><span data-stu-id="64868-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="64868-146">如需閘道的詳細資訊，請參閱[資料管理閘道](../data-factory/data-factory-data-management-gateway.md)文章。</span><span class="sxs-lookup"><span data-stu-id="64868-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="64868-147">隨即出現 [建立閘道] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="64868-148">針對名稱，輸入 **GatewayForDWLoading**，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="64868-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="64868-149">隨即出現 [設定閘道] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="64868-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="64868-150">按一下 [在這台電腦上啟動快速安裝]，在目前電腦上自動下載、安裝及註冊資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="64868-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="64868-151">進度會顯示在快顯視窗中。</span><span class="sxs-lookup"><span data-stu-id="64868-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="64868-152">如果電腦無法連線到資料存放區，您可以手動在電腦上[下載並安裝閘道](https://www.microsoft.com/download/details.aspx?id=39717)，可以連接到資料存放區，然後使用金鑰進行註冊。</span><span class="sxs-lookup"><span data-stu-id="64868-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="64868-153">快速安裝適用於原生 Microsoft Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="64868-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="64868-154">如果您是使用 Google Chrome，先從 Chrome 線上應用程式商店安裝 ClickOnce 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="64868-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="64868-156">等候閘道安裝程式完成。</span><span class="sxs-lookup"><span data-stu-id="64868-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="64868-157">一旦閘道成功註冊且上線後，快顯視窗會關閉，且新的閘道會出現在 [閘道] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="64868-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="64868-158">接著，填寫其餘必要欄位，如下所示，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="64868-159">**伺服器名稱**︰內部部署 SQL Server 的名稱。</span><span class="sxs-lookup"><span data-stu-id="64868-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="64868-160">**資料庫名稱**：SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64868-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="64868-161">**認證加密**：使用預設的「透過網頁瀏覽器」。</span><span class="sxs-lookup"><span data-stu-id="64868-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="64868-162">**驗證類型**︰選擇您所使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="64868-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="64868-163">**使用者名稱**和**密碼**︰輸入擁有複製資料權限之使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="64868-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![啟動快速安裝](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="64868-165">下一步是選擇要從中複製資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="64868-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="64868-166">您可以使用關鍵字篩選資料表。</span><span class="sxs-lookup"><span data-stu-id="64868-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="64868-167">然後您可以預覽底部面板中的資料和資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="64868-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="64868-168">在完成您的選擇之後，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-168">After you finish your selection, click **Next**.</span></span>

    ![選取資料表](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="64868-170">設定目的地，您的 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="64868-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="64868-171">現在，您需要提供目的地資訊給 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="64868-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="64868-172">您的 SQL 資料倉儲連接資訊會自動填入。</span><span class="sxs-lookup"><span data-stu-id="64868-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="64868-173">輸入使用者名稱的密碼。</span><span class="sxs-lookup"><span data-stu-id="64868-173">Enter the password for the user name.</span></span> <span data-ttu-id="64868-174">然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-174">and click **Next**.</span></span>

    ![設定目的地](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="64868-176">出現智慧型資料表對應，它會根據資料表名稱將來源對應至目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="64868-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="64868-177">如果資料表不存在於目的地，依預設，ADF 會建立一個同名的資料表 (這適用於以 SQL Server 或 Azure SQL 資料庫作為來源的情形)。</span><span class="sxs-lookup"><span data-stu-id="64868-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="64868-178">您也可以選擇對應至現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="64868-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="64868-179">檢閱並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-179">Review and click **Next**.</span></span>

    ![對應資料表](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="64868-181">檢閱結構描述對應，並尋找錯誤或警告訊息。</span><span class="sxs-lookup"><span data-stu-id="64868-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="64868-182">智慧型對應是根據資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="64868-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="64868-183">如果在來源和目的地資料行之間有不支援的資料類型轉換，您會看到一則錯誤訊息與對應的資料表。</span><span class="sxs-lookup"><span data-stu-id="64868-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="64868-184">如果您選擇讓 Data Factory 自動建立資料表，則必要時會進行適當的資料類型轉換，以修正來源和目的地存放區之間的不相容性。</span><span class="sxs-lookup"><span data-stu-id="64868-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![對應結構描述](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="64868-186">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="64868-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="64868-187">設定效能設定</span><span class="sxs-lookup"><span data-stu-id="64868-187">Configure the performance settings</span></span>
<span data-ttu-id="64868-188">在 [效能] 設定中，您可以設定 Azure 儲存體帳戶，在資料載入至 SQL 資料倉儲之前用來暫存資料 (使用 [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly) 會有較高的效能)。</span><span class="sxs-lookup"><span data-stu-id="64868-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="64868-189">複製完成之後，將會自動清除儲存體中的暫時資料。</span><span class="sxs-lookup"><span data-stu-id="64868-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="64868-190">選取現有的 Azure 儲存體帳戶，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="64868-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![設定預備 blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="64868-192">檢閱摘要資訊和部署管線</span><span class="sxs-lookup"><span data-stu-id="64868-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="64868-193">檢閱設定，然後按一下 [完成] 按鈕部署管線。</span><span class="sxs-lookup"><span data-stu-id="64868-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![部署 Data Factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="64868-195">監視資料載入進度</span><span class="sxs-lookup"><span data-stu-id="64868-195">Monitor data loading progress</span></span>

<span data-ttu-id="64868-196">您可以在 [部署] 頁面查看部署進度和結果。</span><span class="sxs-lookup"><span data-stu-id="64868-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="64868-197">部署完成之後，按一下 [按一下這裡以監視複製管線] 連結，以監視資料載入進度。</span><span class="sxs-lookup"><span data-stu-id="64868-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![監視管線](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="64868-199">自動會從左邊的 [資源總管] 選取新建立的 **DWLoadData fromSQLServer** 資料載入管線。</span><span class="sxs-lookup"><span data-stu-id="64868-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![檢視管線](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="64868-201">按一下中間窗格中的管線，以查看對應至活動之每個資料表的詳細狀態。</span><span class="sxs-lookup"><span data-stu-id="64868-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![檢視資料表活動](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="64868-203">進一步按一下進入活動，您會在右窗格中看到資料載入詳細資料，包括資料大小、資料列、輸送量等。</span><span class="sxs-lookup"><span data-stu-id="64868-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![檢視資料表活動詳細資料](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="64868-205">若要啟動此更新，請移至您的 SQL 資料倉儲，按一下 [資料載入] > [Azure Data Factory]，選取您的 Factory，然後選擇 [監視現有的載入工作]。</span><span class="sxs-lookup"><span data-stu-id="64868-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64868-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64868-206">Next steps</span></span>

<span data-ttu-id="64868-207">若要將資料庫移轉至 SQL 資料倉儲，請參閱[移轉概觀](sql-data-warehouse-overview-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="64868-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="64868-208">若要深入了解 Azure Data Factory 和其資料移動功能，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="64868-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="64868-209">Azure Data Factory 簡介</span><span class="sxs-lookup"><span data-stu-id="64868-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="64868-210">使用複製活動來移動資料</span><span class="sxs-lookup"><span data-stu-id="64868-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="64868-211">使用 Azure Data Factory 從 Azure SQL 資料倉儲來回移動資料</span><span class="sxs-lookup"><span data-stu-id="64868-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="64868-212">若要瀏覽 SQL 資料倉儲中的資料，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="64868-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="64868-213">使用 Visual Studio 和 SSDT 連接到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="64868-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="64868-214">[採用 Power BI 的視覺化資料](sql-data-warehouse-get-started-visualize-with-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="64868-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure 入口網站]: https://portal.azure.com
