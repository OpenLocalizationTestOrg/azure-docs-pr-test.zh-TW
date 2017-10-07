---
title: "從 Blob 儲存體 tooSQL 資料庫-Azure aaaCopy 資料 |Microsoft 文件"
description: "本教學課程會示範如何 toouse 複製活動中的 Azure Data Factory 管線 toocopy 從 Blob 儲存體 tooSQL 資料庫的資料。"
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
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="052ce-104">教學課程： 將資料從 Blob 儲存體 tooSQL 使用 Data Factory 的資料庫複製</span><span class="sxs-lookup"><span data-stu-id="052ce-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="052ce-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="052ce-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="052ce-106">複製精靈</span><span class="sxs-lookup"><span data-stu-id="052ce-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="052ce-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="052ce-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="052ce-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="052ce-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="052ce-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="052ce-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="052ce-110">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="052ce-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="052ce-111">REST API</span><span class="sxs-lookup"><span data-stu-id="052ce-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="052ce-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="052ce-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="052ce-113">在本教學課程中，您可以建立 data factory 管線 toocopy 資料從 Blob 儲存體 tooSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="052ce-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="052ce-114">hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="052ce-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="052ce-115">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="052ce-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="052ce-116">請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。</span><span class="sxs-lookup"><span data-stu-id="052ce-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="052ce-117">Hello Data Factory 服務的詳細概觀，請參閱 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="052ce-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="052ce-118">Hello 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="052ce-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="052ce-119">開始本教學課程之前，您必須具備下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="052ce-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="052ce-120">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="052ce-120">**Azure subscription**.</span></span>  <span data-ttu-id="052ce-121">如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="052ce-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="052ce-122">請參閱 hello[免費試用版](http://azure.microsoft.com/pricing/free-trial/)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="052ce-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="052ce-123">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="052ce-123">**Azure Storage Account**.</span></span> <span data-ttu-id="052ce-124">您使用做為 hello blob 儲存體**來源**資料儲存在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="052ce-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="052ce-125">如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。</span><span class="sxs-lookup"><span data-stu-id="052ce-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="052ce-126">**Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="052ce-126">**Azure SQL Database**.</span></span> <span data-ttu-id="052ce-127">在本教學課程中，您會使用 Azure SQL Database 做為 **目的地** 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="052ce-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="052ce-128">如果您沒有 Azure SQL database 可讓您在 hello 教學課程，請參閱[如何 toocreate 及設定 Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="052ce-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="052ce-129">**SQL Server 2012/2014 或 Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="052ce-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="052ce-130">您可以使用 SQL Server Management Studio 或 Visual Studio toocreate 範例資料庫和 tooview hello 結果資料 hello 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="052ce-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="052ce-131">收集 Blob 儲存體帳戶名稱和金鑰</span><span class="sxs-lookup"><span data-stu-id="052ce-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="052ce-132">您需要 hello 帳戶名稱和帳戶金鑰，您的 Azure 儲存體帳戶 toodo 本教學課程。</span><span class="sxs-lookup"><span data-stu-id="052ce-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="052ce-133">記下 Azure 儲存體帳戶的**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="052ce-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="052ce-134">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="052ce-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="052ce-135">按一下**更多服務**上 hello 功能表，然後選取左**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="052ce-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![瀏覽 - 儲存體帳戶](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="052ce-137">在 [hello**儲存體帳戶**刀鋒視窗中，選取 hello **Azure 儲存體帳戶**的 toouse 在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="052ce-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="052ce-138">選取 [設定] 底下的 [存取金鑰] 連結。</span><span class="sxs-lookup"><span data-stu-id="052ce-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="052ce-139">按一下**複製**（圖像） 下一步按鈕太**儲存體帳戶名稱**文字並儲存/貼上它某處 (例如： 文字檔案中)。</span><span class="sxs-lookup"><span data-stu-id="052ce-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="052ce-140">重複上一個步驟 toocopy hello 」 或 「 記下 hello **key1**。</span><span class="sxs-lookup"><span data-stu-id="052ce-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![儲存體存取金鑰](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="052ce-142">按一下 [關閉所有 hello 刀鋒視窗**X**。</span><span class="sxs-lookup"><span data-stu-id="052ce-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="052ce-143">收集 SQL Server、資料庫、使用者名稱</span><span class="sxs-lookup"><span data-stu-id="052ce-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="052ce-144">本教學課程需要的 Azure SQL server、 資料庫和使用者 toodo hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="052ce-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="052ce-145">記下 Azure SQL Database 的**伺服器**、**資料庫**和**使用者**名稱。</span><span class="sxs-lookup"><span data-stu-id="052ce-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="052ce-146">在 [hello **Azure 入口網站**，按一下 [**更多服務**上 hello，然後選取**SQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="052ce-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="052ce-147">在 [hello **SQL 資料庫刀鋒視窗**，選取 hello**資料庫**的 toouse 在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="052ce-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="052ce-148">記下 hello**資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="052ce-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="052ce-149">在 [hello **SQL database**刀鋒視窗中，按一下 [**屬性**下**設定**。</span><span class="sxs-lookup"><span data-stu-id="052ce-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="052ce-150">記下 hello 值**伺服器名稱**和**SERVER 系統管理員登入**。</span><span class="sxs-lookup"><span data-stu-id="052ce-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="052ce-151">按一下 [關閉所有 hello 刀鋒視窗**X**。</span><span class="sxs-lookup"><span data-stu-id="052ce-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="052ce-152">允許 Azure 服務 tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="052ce-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="052ce-153">請確認**tooAzure 服務允許存取**設定**ON** Azure SQL server 讓該 hello Data Factory 服務能夠存取您的 Azure SQL server。</span><span class="sxs-lookup"><span data-stu-id="052ce-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="052ce-154">tooverify 並開啟此設定，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="052ce-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="052ce-155">按一下**更多服務**hello 左側，按一下中樞**SQL 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="052ce-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="052ce-156">選取您的伺服器，然後按一下 [設定] 下的 [防火牆]。</span><span class="sxs-lookup"><span data-stu-id="052ce-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="052ce-157">在 [hello**防火牆設定**刀鋒視窗中，按一下**ON**如**tooAzure 服務允許存取**。</span><span class="sxs-lookup"><span data-stu-id="052ce-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="052ce-158">按一下 [關閉所有 hello 刀鋒視窗**X**。</span><span class="sxs-lookup"><span data-stu-id="052ce-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="052ce-159">準備 Blob 儲存體和 SQL Database</span><span class="sxs-lookup"><span data-stu-id="052ce-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="052ce-160">現在，執行備妥您的 Azure blob 儲存體和 Azure SQL database hello 教學課程步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="052ce-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="052ce-161">啟動 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="052ce-161">Launch Notepad.</span></span> <span data-ttu-id="052ce-162">複製下列文字的 hello，並將它儲存成**emp.txt**太**C:\ADFGetStarted**硬碟機上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="052ce-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="052ce-163">使用工具，例如[Azure 儲存體總管](http://storageexplorer.com/)toocreate hello **adftutorial**容器和 tooupload hello **emp.txt**檔案 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="052ce-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Azure 儲存體總管。](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="052ce-166">使用下列 SQL 指令碼 toocreate hello 的 hello **emp**您 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="052ce-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="052ce-167">**如果您有 SQL Server 2012/2014 安裝在電腦上：**遵循指示從[管理 Azure SQL Database 使用 SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour SQL Azure 伺服器，然後執行 hello SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="052ce-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="052ce-168">本文使用 hello[傳統 Azure 入口網站](http://manage.windowsazure.com)，不 hello[新版 Azure 入口網站](https://portal.azure.com)，Azure SQL 伺服器的 tooconfigure 防火牆。</span><span class="sxs-lookup"><span data-stu-id="052ce-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="052ce-169">如果您的用戶端不允許 tooaccess hello Azure SQL server，您需要 tooconfigure 防火牆 tooallow 存取您 Azure SQL server 從您的電腦 （IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="052ce-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="052ce-170">請參閱[本文](../sql-database/sql-database-configure-firewall-settings.md)步驟 tooconfigure hello 防火牆 Azure SQL server。</span><span class="sxs-lookup"><span data-stu-id="052ce-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="052ce-171">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="052ce-171">Create a data factory</span></span>
<span data-ttu-id="052ce-172">您已完成 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="052ce-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="052ce-173">您可以建立使用下列方式 hello 其中的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="052ce-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="052ce-174">按一下其中一個 hello 頂端或 hello 連結 tooperform hello 教學課程的 hello 下拉式清單中的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="052ce-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="052ce-175">複製精靈</span><span class="sxs-lookup"><span data-stu-id="052ce-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="052ce-176">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="052ce-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="052ce-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="052ce-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="052ce-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="052ce-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="052ce-179">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="052ce-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="052ce-180">REST API</span><span class="sxs-lookup"><span data-stu-id="052ce-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="052ce-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="052ce-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="052ce-182">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="052ce-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="052ce-183">它不會轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="052ce-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="052ce-184">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="052ce-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="052ce-185">您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="052ce-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="052ce-186">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="052ce-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
