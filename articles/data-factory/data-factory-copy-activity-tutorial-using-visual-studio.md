---
title: "教學課程：使用 Visual Studio 建立具有複製活動的管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Visual Studio，建立具有複製活動的 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="2ddb1-103">教學課程：使用 Visual Studio 建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="2ddb1-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ddb1-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="2ddb1-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="2ddb1-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="2ddb1-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="2ddb1-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2ddb1-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="2ddb1-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ddb1-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="2ddb1-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ddb1-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="2ddb1-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="2ddb1-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="2ddb1-110">REST API</span><span class="sxs-lookup"><span data-stu-id="2ddb1-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="2ddb1-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="2ddb1-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="2ddb1-112">在本文中，您學會如何 toouse 會 hello Microsoft Visual Studio toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="2ddb1-113">如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="2ddb1-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="2ddb1-115">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="2ddb1-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2ddb1-117">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2ddb1-118">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="2ddb1-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2ddb1-120">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="2ddb1-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="2ddb1-122">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="2ddb1-123">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ddb1-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ddb1-124">Prerequisites</span></span>
1. <span data-ttu-id="2ddb1-125">閱讀[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="2ddb1-126">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="2ddb1-127">您必須擁有您電腦上安裝的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="2ddb1-128">Visual Studio 2013 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2ddb1-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="2ddb1-129">下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="2ddb1-130">瀏覽過[Azure 下載頁面](https://azure.microsoft.com/downloads/)按一下**VS 2013**或**VS 2015**在 hello **.NET** > 一節。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="2ddb1-131">下載最新 Azure Data Factory 外掛程式 hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5)或[VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="2ddb1-132">您也可以執行下列步驟的 hello 更新 hello 外掛程式： hello 功能表上，按一下**工具** -> **擴充功能和更新** -> **線上** ->  **Visual Studio 組件庫** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **更新**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="2ddb1-133">步驟</span><span class="sxs-lookup"><span data-stu-id="2ddb1-133">Steps</span></span>
<span data-ttu-id="2ddb1-134">以下是您執行本教學課程的一部分的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="2ddb1-135">建立**連結的服務**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="2ddb1-136">在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="2ddb1-137">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="2ddb1-138">您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="2ddb1-139">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="2ddb1-140">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="2ddb1-141">您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="2ddb1-142">建立輸入和輸出**資料集**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="2ddb1-143">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="2ddb1-144">此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="2ddb1-145">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="2ddb1-146">此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="2ddb1-147">建立**管線**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="2ddb1-148">在此步驟中，您會建立具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="2ddb1-149">hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="2ddb1-150">您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="2ddb1-151">如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="2ddb1-152">在部署 Data Factory 實體 (連結服務、資料集/資料表和管線) 時，建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="2ddb1-153">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="2ddb1-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="2ddb1-154">啟動 **Visual Studio 2015**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="2ddb1-155">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="2ddb1-156">您應該會看見 hello**新專案** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="2ddb1-157">在 hello**新專案**對話方塊中，選取 hello **DataFactory**範本，然後按一下**空白資料處理站專案**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![[新增專案] 對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="2ddb1-159">指定 hello 名稱 hello 專案、 hello 方案位置以及 hello 方案的名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="2ddb1-161">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="2ddb1-161">Create linked services</span></span>
<span data-ttu-id="2ddb1-162">您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="2ddb1-163">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="2ddb1-164">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="2ddb1-165">因此，您會建立兩種連結服務：AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="2ddb1-166">hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="2ddb1-167">這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="2ddb1-168">Azure SQL 連結服務連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="2ddb1-169">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="2ddb1-170">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="2ddb1-171">連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="2ddb1-172">請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="2ddb1-173">請參閱[計算連結的服務](data-factory-compute-linked-services.md)hello 的 Data Factory 支援的計算服務的清單。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="2ddb1-174">在本教學課程中，您不會使用任何計算服務。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="2ddb1-175">建立 hello Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="2ddb1-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="2ddb1-176">在**方案總管 中**，以滑鼠右鍵按一下**連結的服務**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="2ddb1-177">在 hello**加入新項目**對話方塊中，選取**Azure 儲存體連結服務**從 hello 清單，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![新的連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="2ddb1-179">取代`<accountname>`和`<accountkey>`* 與 hello 您 Azure 儲存體帳戶名稱和其索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Azure 儲存體連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="2ddb1-181">儲存 hello **AzureStorageLinkedService1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="2ddb1-182">如需在連結的 hello 服務定義中的 JSON 屬性的詳細資訊，請參閱[Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)發行項。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="2ddb1-183">建立 hello Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="2ddb1-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="2ddb1-184">以滑鼠右鍵按一下**連結的服務**hello 中的節點**方案總管 中**同樣地，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="2ddb1-185">這次，請選取 [Azure SQL 連結服務]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="2ddb1-186">在 hello **AzureSqlLinkedService1.json 檔案**，取代`<servername>`， `<databasename>`， `<username@servername>`，和`<password>`與您 Azure SQL server、 資料庫、 使用者帳戶和密碼的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="2ddb1-187">儲存 hello **AzureSqlLinkedService1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="2ddb1-188">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="2ddb1-189">建立資料集</span><span class="sxs-lookup"><span data-stu-id="2ddb1-189">Create datasets</span></span>
<span data-ttu-id="2ddb1-190">在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="2ddb1-191">在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService1 和 AzureSqlLinkedService1 所參考的資料存放區中的兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="2ddb1-192">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="2ddb1-193">此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="2ddb1-194">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="2ddb1-195">此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="2ddb1-196">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="2ddb1-196">Create input dataset</span></span>
<span data-ttu-id="2ddb1-197">在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService1 連結服務所代表的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="2ddb1-198">如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="2ddb1-199">在本教學課程中，您可以指定 hello 檔案名稱的值。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="2ddb1-200">在這裡，您可以使用 hello 詞彙"tables"而不是 「 資料集 」。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="2ddb1-201">資料表是矩形的資料集，並且是 hello 現在支援的資料集的唯一類型。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="2ddb1-202">以滑鼠右鍵按一下**資料表**在 hello**方案總管 中**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="2ddb1-203">在 hello**加入新項目**對話方塊中，選取**Azure Blob**，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="2ddb1-204">Hello JSON 文字取代成下列文字的 hello 和儲存 hello **AzureBlobLocation1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="2ddb1-205">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="2ddb1-206">屬性</span><span class="sxs-lookup"><span data-stu-id="2ddb1-206">Property</span></span> | <span data-ttu-id="2ddb1-207">說明</span><span class="sxs-lookup"><span data-stu-id="2ddb1-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2ddb1-208">類型</span><span class="sxs-lookup"><span data-stu-id="2ddb1-208">type</span></span> | <span data-ttu-id="2ddb1-209">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="2ddb1-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2ddb1-210">linkedServiceName</span></span> | <span data-ttu-id="2ddb1-211">是指 toohello **AzureStorageLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2ddb1-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="2ddb1-212">folderPath</span></span> | <span data-ttu-id="2ddb1-213">指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="2ddb1-214">在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="2ddb1-215">fileName</span><span class="sxs-lookup"><span data-stu-id="2ddb1-215">fileName</span></span> | <span data-ttu-id="2ddb1-216">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-216">This property is optional.</span></span> <span data-ttu-id="2ddb1-217">如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="2ddb1-218">在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="2ddb1-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="2ddb1-219">format -> type</span></span> |<span data-ttu-id="2ddb1-220">hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="2ddb1-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="2ddb1-221">columnDelimiter</span></span> | <span data-ttu-id="2ddb1-222">hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="2ddb1-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2ddb1-223">frequency/interval</span></span> | <span data-ttu-id="2ddb1-224">hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="2ddb1-225">換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="2ddb1-226">它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="2ddb1-227">external</span><span class="sxs-lookup"><span data-stu-id="2ddb1-227">external</span></span> | <span data-ttu-id="2ddb1-228">這個屬性設定太**true**如果 hello 資料不會產生此管線。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="2ddb1-229">在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="2ddb1-230">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="2ddb1-231">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="2ddb1-231">Create output dataset</span></span>
<span data-ttu-id="2ddb1-232">在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="2ddb1-233">此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService1**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="2ddb1-234">以滑鼠右鍵按一下**資料表**在 hello**方案總管 中**同樣地，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="2ddb1-235">在 hello**加入新項目**對話方塊中，選取**Azure SQL**，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="2ddb1-236">Hello JSON 文字取代成下列 JSON hello 和儲存 hello **AzureSqlTableLocation1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="2ddb1-237">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="2ddb1-238">屬性</span><span class="sxs-lookup"><span data-stu-id="2ddb1-238">Property</span></span> | <span data-ttu-id="2ddb1-239">說明</span><span class="sxs-lookup"><span data-stu-id="2ddb1-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2ddb1-240">類型</span><span class="sxs-lookup"><span data-stu-id="2ddb1-240">type</span></span> | <span data-ttu-id="2ddb1-241">hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="2ddb1-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2ddb1-242">linkedServiceName</span></span> | <span data-ttu-id="2ddb1-243">是指 toohello **AzureSqlLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2ddb1-244">tableName</span><span class="sxs-lookup"><span data-stu-id="2ddb1-244">tableName</span></span> | <span data-ttu-id="2ddb1-245">指定的 hello**資料表**toowhich hello 資料複製。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="2ddb1-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2ddb1-246">frequency/interval</span></span> | <span data-ttu-id="2ddb1-247">hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="2ddb1-248">有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="2ddb1-249">識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="2ddb1-250">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="2ddb1-251">建立管線</span><span class="sxs-lookup"><span data-stu-id="2ddb1-251">Create pipeline</span></span>
<span data-ttu-id="2ddb1-252">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="2ddb1-253">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="2ddb1-254">在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="2ddb1-255">hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="2ddb1-256">因此，hello 管線所產生的輸出資料集的 24 配量。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="2ddb1-257">以滑鼠右鍵按一下**管線**在 hello**方案總管 中**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="2ddb1-258">選取**複製資料管線**在 hello**加入新項目**對話方塊，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="2ddb1-259">取代下列 JSON hello hello JSON，並儲存 hello **CopyActivity1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="2ddb1-260">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="2ddb1-261">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2ddb1-262">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="2ddb1-263">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="2ddb1-264">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="2ddb1-265">支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2ddb1-266">toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="2ddb1-267">取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="2ddb1-268">您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="2ddb1-269">例如，"2016年-02-03"，這相當於太"2016年-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="2ddb1-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="2ddb1-270">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="2ddb1-271">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="2ddb1-272">hello**結束**時間是選擇性的但我們在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="2ddb1-273">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="2ddb1-274">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="2ddb1-275">在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="2ddb1-276">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2ddb1-277">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2ddb1-278">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="2ddb1-279">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="2ddb1-280">發佈/部署 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="2ddb1-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="2ddb1-281">在此步驟中，您會發佈稍早建立的 Data Factory 實體 (連結的服務、資料集和管線)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="2ddb1-282">您也可以指定新資料處理站 toobe hello hello 名稱建立 toohold 這些實體。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="2ddb1-283">以滑鼠右鍵按一下專案 hello 方案總管] 中的，按一下 [**發行**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="2ddb1-284">如果您看到**登入 Microsoft 帳戶 tooyour**對話方塊中，hello 擁有帳戶的 Azure 訂用帳戶中，輸入您的認證，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="2ddb1-285">您應該會看到下列對話方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ddb1-285">You should see hello following dialog box:</span></span>
   
   ![發佈對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="2ddb1-287">Hello 設定資料 factory 頁面上，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="2ddb1-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="2ddb1-288">選取 [建立新的 Data Factory]  選項。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="2ddb1-289">針對 [名稱] 輸入 **VSTutorialFactory**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="2ddb1-290">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="2ddb1-291">如果發行時，您會收到一個錯誤 hello 的 data factory 的名稱，，變更 hello 名稱 hello 資料處理站 (例如，yournameVSTutorialFactory) 並再試一次發行一次。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="2ddb1-292">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="2ddb1-293">選取您的 Azure 訂閱 hello**訂用帳戶**欄位。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="2ddb1-294">如果看不到任何訂用帳戶，請確定您登入是系統管理員或共同管理員的 hello 訂用帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="2ddb1-295">選取 hello**資源群組**hello 資料 factory toobe 建立的。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="2ddb1-296">選取 hello**區域**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="2ddb1-297">Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="2ddb1-298">按一下**下一步**tooswitch toohello**發行的項目**頁面。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![設定 Data Factory 頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="2ddb1-300">在 [hello**發行的項目**頁面上，確定所有 hello Data Factory 實體已選取，然後按一下**下一步]** tooswitch toohello**摘要**頁面。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![發佈項目頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="2ddb1-302">檢閱 hello 摘要，然後按一下**下一步**toostart hello 部署程序和檢視 hello**部署狀態**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![發佈摘要頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="2ddb1-304">在 [hello**部署狀態**] 頁面上，您應該會看到 hello hello 部署程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="2ddb1-305">Hello 部署完成之後，請按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-305">Click Finish after hello deployment is done.</span></span>
 
   ![部署狀態頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="2ddb1-307">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="2ddb1-307">Note hello following points:</span></span> 

* <span data-ttu-id="2ddb1-308">如果您收到 hello 錯誤: 「 此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory 」，請勿 hello 下列其中一種，再次嘗試重新發行：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="2ddb1-309">在 Azure PowerShell，執行下列命令 tooregister hello Data Factory 提供者的 hello。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="2ddb1-310">您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="2ddb1-311">登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="2ddb1-312">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="2ddb1-313">可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ddb1-314">toocreate Data Factory 執行個體，您需要 toobe hello Azure 訂用帳戶管理員/共同管理員</span><span class="sxs-lookup"><span data-stu-id="2ddb1-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="2ddb1-315">監視管線</span><span class="sxs-lookup"><span data-stu-id="2ddb1-315">Monitor pipeline</span></span>
<span data-ttu-id="2ddb1-316">瀏覽您的 data factory toohello 首頁：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="2ddb1-317">登入太[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ddb1-318">按一下**更多服務**hello 左的窗格中，且按一下**Data factory**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![瀏覽 Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="2ddb1-320">開始輸入 hello 的 data factory 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-320">Start typing hello name of your data factory.</span></span>

    ![資料處理站名稱](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="2ddb1-322">按一下您的 data factory 中 hello 結果清單 toosee hello 首頁，即可供您的 data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="2ddb1-324">請依照下列指示從[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)toomonitor hello 管線和資料集已建立本教學課程中。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="2ddb1-325">Visual Studio 目前不支援監視 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="2ddb1-326">摘要</span><span class="sxs-lookup"><span data-stu-id="2ddb1-326">Summary</span></span>
<span data-ttu-id="2ddb1-327">在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="2ddb1-328">您可以使用 Visual Studio toocreate hello 資料處理站、 連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="2ddb1-329">以下是您執行本教學課程中的 hello 高階步驟：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="2ddb1-330">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="2ddb1-331">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="2ddb1-332">**Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="2ddb1-333">**Azure SQL**連結服務 toolink hello 輸出資料會保存您 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="2ddb1-334">建立可描述管線輸入資料和輸出資料的 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="2ddb1-335">建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="2ddb1-336">如何 toouse HDInsight Hive 活動 tootransform 資料使用 Azure HDInsight 叢集，請參閱的 toosee[教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="2ddb1-337">您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="2ddb1-338">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="2ddb1-339">在 Server Explorer 中檢視所有資料處理站</span><span class="sxs-lookup"><span data-stu-id="2ddb1-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="2ddb1-340">本章節描述如何 toouse hello 伺服器總管，在 Visual Studio tooview 您 Azure 訂用帳戶中的所有都 hello data factory 及建立 Visual Studio 專案是根據現有的 data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="2ddb1-341">在**Visual Studio**，按一下 **檢視**在 hello 功能表，然後按一下**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="2ddb1-342">在 [hello 伺服器總管] 視窗中，展開**Azure**展開**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="2ddb1-343">如果您看到**登入 tooVisual Studio**，輸入 hello**帳戶**與您的 Azure 訂用帳戶，然後按一下相關聯**繼續**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="2ddb1-344">輸入**密碼**，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="2ddb1-345">Visual Studio 會嘗試 tooget 您訂用帳戶中的所有 Azure data factory 的資訊。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="2ddb1-346">您看到這項作業在 hello hello 狀態**資料 Factory 工作清單**視窗。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="2ddb1-348">建立現有資料處理站的 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="2ddb1-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="2ddb1-349">以滑鼠右鍵按一下伺服器總管中的資料處理站，然後選取**匯出 Data Factory tooNew 專案**toocreate Visual Studio 專案是根據現有的 data factory。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![匯出資料 factory tooa VS 專案](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="2ddb1-351">更新 Visual studio 的 Data Factory 工具</span><span class="sxs-lookup"><span data-stu-id="2ddb1-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="2ddb1-352">tooupdate Azure Data Factory tools for Visual Studio hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="2ddb1-353">按一下**工具**hello 功能表，然後選取**擴充功能和更新**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="2ddb1-354">選取**更新**在 hello 左的窗格，然後選取  **Visual Studio 組件庫**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="2ddb1-355">選取 [Visual Studio 的 Azure Data Factory 工具] 並按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="2ddb1-356">如果看不到此項目，您已經有 hello hello 工具最新版本。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="2ddb1-357">使用組態檔</span><span class="sxs-lookup"><span data-stu-id="2ddb1-357">Use configuration files</span></span>
<span data-ttu-id="2ddb1-358">您可以使用 Visual Studio tooconfigure 屬性中的組態檔的連結服務/資料表/管線以不同的方式為每個環境。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="2ddb1-359">請考慮下列 JSON 定義 Azure 儲存體連結服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="2ddb1-360">toospecify **connectionString** accountname 和 accountkey hello 環境 （開發/測試/生產環境） toowhich 所根據的值不同，您要部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="2ddb1-361">您可以針對每個環境使用個別的組態檔來達成此行為。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="2ddb1-362">新增組態檔</span><span class="sxs-lookup"><span data-stu-id="2ddb1-362">Add a configuration file</span></span>
<span data-ttu-id="2ddb1-363">執行下列步驟的 hello 加入每個環境的組態檔：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="2ddb1-364">Visual Studio 方案中的 hello Data Factory 專案上按一下滑鼠右鍵，指向太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="2ddb1-365">選取**Config**從已安裝的範本在 hello 左邊 hello 清單中選取**組態檔**，輸入**名稱**hello 組態檔案，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![新增組態檔](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="2ddb1-367">遵循格式 hello 中加入組態參數和值：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-367">Add configuration parameters and their values in hello following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="2ddb1-368">這個範例會設定 Azure 儲存體連結服務和 Azure SQL 連結服務的 connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="2ddb1-369">請注意，用來指定名稱的 hello 語法[JsonPath](http://goessner.net/articles/JsonPath/)。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="2ddb1-370">如果 JSON 屬性，其值的陣列，如 hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="2ddb1-371">設定屬性，如下列組態檔 （使用以零為起始的索引） 的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="2ddb1-372">包含空格的屬性名稱</span><span class="sxs-lookup"><span data-stu-id="2ddb1-372">Property names with spaces</span></span>
<span data-ttu-id="2ddb1-373">如果屬性名稱具有空格中的，使用方括號，如下列範例 （資料庫伺服器名稱） 的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="2ddb1-374">使用組態部署解決方案</span><span class="sxs-lookup"><span data-stu-id="2ddb1-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="2ddb1-375">當您發行 Azure Data Factory 實體在 VS 中時，您可以指定該發行作業需 toouse hello 組態。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="2ddb1-376">使用組態檔的 Azure Data Factory 專案中的 toopublish 實體：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="2ddb1-377">Data Factory 專案上按一下滑鼠右鍵，然後按一下**發行**toosee hello**發行的項目** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="2ddb1-378">選取現有的 data factory，或指定值的 data factory 建立 hello**設定資料 factory**頁面，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="2ddb1-379">在 hello**發行的項目**頁面： 您會看到與 hello 可用的組態下拉式清單**選取部署設定**欄位。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![選取組態檔](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="2ddb1-381">選取 hello**組態檔**您會想 toouse，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="2ddb1-382">確認您看到的 JSON 檔案中 hello hello 名稱**摘要**頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="2ddb1-383">按一下**完成**hello 部署作業完成之後。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="2ddb1-384">當您部署時，hello 設定檔中的 hello 值是使用的 tooset hello JSON 檔案中的屬性值在 hello 實體部署的 tooAzure Data Factory 服務之前。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="2ddb1-385">使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="2ddb1-385">Use Azure Key Vault</span></span>
<span data-ttu-id="2ddb1-386">它不建議您經常對等連接字串 toohello 程式碼儲存機制的安全性原則 toocommit 敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="2ddb1-387">請參閱[ADF 安全發佈](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)GitHub toolearn 有關在 Azure 金鑰保存庫中儲存機密資訊，並使用它時發行 Data Factory 實體上的範例。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="2ddb1-388">hello 安全發行 Visual Studio 擴充功能可讓儲存在金鑰保存庫中的 hello 密碼 toobe 和連結的服務中指定只參考 toothem / 部署組態。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="2ddb1-389">當您發行 Data Factory 實體 tooAzure 時，這些參考會解析。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="2ddb1-390">這些檔案接著可以認可的 toosource 儲存機制，而不公開任何秘密。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ddb1-391">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ddb1-391">Next steps</span></span>
<span data-ttu-id="2ddb1-392">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="2ddb1-393">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="2ddb1-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="2ddb1-394">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2ddb1-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
