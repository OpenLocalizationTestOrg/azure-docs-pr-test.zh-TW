---
title: "將資料從 Blob 儲存體複製到 SQL Database - Azure | Microsoft Docs"
description: "本教學課程向您說明如何使用 Azure Data Factory 管線中的複製活動，將資料從 Blob 儲存體複製到 SQL Database。"
keywords: "blob sql, blob 儲存體, 資料複製"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="9f6b5-104">教學課程：使用 Data Factory 將資料從 Blob 儲存體複製到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="9f6b5-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f6b5-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="9f6b5-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9f6b5-106">複製精靈</span><span class="sxs-lookup"><span data-stu-id="9f6b5-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9f6b5-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f6b5-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9f6b5-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f6b5-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9f6b5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f6b5-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9f6b5-110">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9f6b5-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9f6b5-111">REST API</span><span class="sxs-lookup"><span data-stu-id="9f6b5-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9f6b5-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="9f6b5-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="9f6b5-113">在本教學課程中，您會建立 Data Factory 與管線，以將資料從 Blob 儲存體複製到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="9f6b5-114">複製活動會在 Azure Data Factory 中執行資料移動。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="9f6b5-115">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9f6b5-116">如需複製活動的詳細資訊，請參閱 [資料移動活動](data-factory-data-movement-activities.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="9f6b5-117">如需 Data Factory 服務的詳細概觀，請參閱 [Azure Data Factory 簡介](data-factory-introduction.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="9f6b5-118">教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="9f6b5-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="9f6b5-119">開始進行本教學課程之前，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="9f6b5-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="9f6b5-120">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-120">**Azure subscription**.</span></span>  <span data-ttu-id="9f6b5-121">如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9f6b5-122">如需詳細資料，請參閱 [免費試用](http://azure.microsoft.com/pricing/free-trial/) 一文。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="9f6b5-123">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-123">**Azure Storage Account**.</span></span> <span data-ttu-id="9f6b5-124">在本教學課程中，您會使用 Blob 儲存體做為 **來源** 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="9f6b5-125">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) 一文以取得建立步驟。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="9f6b5-126">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-126">**Azure SQL Database**.</span></span> <span data-ttu-id="9f6b5-127">在本教學課程中，您會使用 Azure SQL Database 做為 **目的地** 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="9f6b5-128">如果您沒有可在教學課程中使用的 Azure SQL Database，請參閱 [如何建立和設定 Azure SQL Database](../sql-database/sql-database-get-started.md) 建立一個。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="9f6b5-129">**SQL Server 2012/2014 或 Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="9f6b5-130">您會使用 SQL Server Management Studio 或 Visual Studio，建立範例資料庫以及檢視資料庫中的結果資料。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="9f6b5-131">收集 Blob 儲存體帳戶名稱和金鑰</span><span class="sxs-lookup"><span data-stu-id="9f6b5-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="9f6b5-132">您需要有 Azure 儲存體帳戶的帳戶名稱和帳戶金鑰，才能進行這個教學課程。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="9f6b5-133">記下 Azure 儲存體帳戶的**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="9f6b5-134">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f6b5-135">按一下左側功能表中的 [更多服務]，然後選取 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![瀏覽 - 儲存體帳戶](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="9f6b5-137">在 [儲存體帳戶] 刀鋒視窗中，選取您想要在本教學課程中使用的 [Azure 儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="9f6b5-138">選取 [設定] 底下的 [存取金鑰] 連結。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="9f6b5-139">按一下 [儲存體帳戶名稱] 文字方塊旁的 [複製 (影像)] 按鈕，然後將它儲存/貼到某個位置 (例如：在文字檔中)。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="9f6b5-140">重複上述步驟，複製或記下 **key1**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![儲存體存取金鑰](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="9f6b5-142">按一下 **X**，關閉所有刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="9f6b5-143">收集 SQL Server、資料庫、使用者名稱</span><span class="sxs-lookup"><span data-stu-id="9f6b5-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="9f6b5-144">您需要有 Azure SQL 伺服器、資料庫和使用者的名稱，才能進行這個教學課程。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="9f6b5-145">記下 Azure SQL Database 的**伺服器**、**資料庫**和**使用者**名稱。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="9f6b5-146">在 **Azure 入口網站**中，按一下左邊的 [更多服務]，然後選取 [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="9f6b5-147">在 [SQL Database] 刀鋒視窗中，選取您想要在本教學課程中使用的**資料庫**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="9f6b5-148">記下 **資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="9f6b5-149">在 [SQL Database] 刀鋒視窗中，按一下 [設定] 下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="9f6b5-150">記下 [伺服器名稱] 和 [伺服器系統管理員登入] 的值。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="9f6b5-151">按一下 **X**，關閉所有刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="9f6b5-152">允許 Azure 服務存取 SQL Server</span><span class="sxs-lookup"><span data-stu-id="9f6b5-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="9f6b5-153">確定**開啟** Azure SQL 伺服器的 [允許存取 Azure 服務] 設定，讓 Data Factory 服務可以存取您的 Azure SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="9f6b5-154">若要確認並開啟此設定，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9f6b5-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="9f6b5-155">按一下左邊的 [更多服務] 中樞，然後按一下 [SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="9f6b5-156">選取您的伺服器，然後按一下 [設定] 下的 [防火牆]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="9f6b5-157">在 [防火牆設定] 刀鋒視窗中，對 [允許存取 Azure 服務] 按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="9f6b5-158">按一下 **X**，關閉所有刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="9f6b5-159">準備 Blob 儲存體和 SQL Database</span><span class="sxs-lookup"><span data-stu-id="9f6b5-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="9f6b5-160">現在，請執行下列步驟，準備本教學課程中的 Azure Blob 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="9f6b5-161">啟動 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-161">Launch Notepad.</span></span> <span data-ttu-id="9f6b5-162">複製以下文字，並命名為 **emp.txt**，然後儲存至您硬碟上的 **C:\ADFGetStarted** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="9f6b5-163">使用 [Azure 儲存體總管](http://storageexplorer.com/)這類的工具建立 **adftutorial** 容器，以及將 **emp.txt** 檔案上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure 儲存體總管。](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="9f6b5-166">使用以下 SQL 指令碼，在您的 Azure SQL Database 中建立 **emp** 資料表。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="9f6b5-167">**如果您的電腦上已安裝 SQL Server 2012/2014：**請遵循[使用 SQL Server Management Studio 管理 Azure SQL Database](../sql-database/sql-database-manage-azure-ssms.md) 中的指示，連線到您的 Azure SQL Server，並執行 SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="9f6b5-168">本文使用[傳統 Azure 入口網站](http://manage.windowsazure.com) (而非[新的 Azure 入口網站](https://portal.azure.com)) 來設定 Azure SQL Server 的防火牆。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="9f6b5-169">如果不允許您的用戶端存取 Azure SQL Server，則必須將 Azure SQL Server 的防火牆設定成允許從您的電腦 (IP 位址) 存取。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="9f6b5-170">請參閱 [本文](../sql-database/sql-database-configure-firewall-settings.md) 的步驟，為 Azure SQL Server 設定防火牆。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="9f6b5-171">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="9f6b5-171">Create a data factory</span></span>
<span data-ttu-id="9f6b5-172">您已完成必要條件。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-172">You have completed the prerequisites.</span></span> <span data-ttu-id="9f6b5-173">您可以使用下列其中一個方式建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="9f6b5-174">按一下頂端下拉式清單中的其中一個選項，或按一下下列連結以執行教學課程。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="9f6b5-175">複製精靈</span><span class="sxs-lookup"><span data-stu-id="9f6b5-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="9f6b5-176">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f6b5-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="9f6b5-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f6b5-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="9f6b5-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f6b5-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="9f6b5-179">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9f6b5-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="9f6b5-180">REST API</span><span class="sxs-lookup"><span data-stu-id="9f6b5-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="9f6b5-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="9f6b5-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="9f6b5-182">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="9f6b5-183">它不會轉換輸入資料來產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="9f6b5-184">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置第一個管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="9f6b5-185">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="9f6b5-186">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="9f6b5-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
