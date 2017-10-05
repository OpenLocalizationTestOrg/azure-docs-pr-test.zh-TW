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
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="9cd34-103">教學課程：使用 Visual Studio 建立具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="9cd34-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cd34-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="9cd34-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9cd34-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="9cd34-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9cd34-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9cd34-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9cd34-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cd34-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9cd34-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cd34-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9cd34-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9cd34-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9cd34-110">REST API</span><span class="sxs-lookup"><span data-stu-id="9cd34-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9cd34-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="9cd34-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="9cd34-112">在本文中，您會了解如何使用 Microsoft Visual Studio 建立資料處理站，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9cd34-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="9cd34-113">如果您不熟悉 Azure Data Factory，請先詳閱 [Azure Data Factory 簡介](data-factory-introduction.md)一文，再進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="9cd34-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="9cd34-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="9cd34-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="9cd34-115">複製活動會將資料從支援的資料存放區複製到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9cd34-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="9cd34-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9cd34-117">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="9cd34-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9cd34-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="9cd34-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="9cd34-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9cd34-120">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="9cd34-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="9cd34-122">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9cd34-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="9cd34-123">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cd34-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="9cd34-124">Prerequisites</span></span>
1. <span data-ttu-id="9cd34-125">詳讀 [教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 一文並完成 **必要** 步驟。</span><span class="sxs-lookup"><span data-stu-id="9cd34-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="9cd34-126">若要建立 Data Factory 執行個體，您必須是訂用帳戶/資源群組層級的 [Data Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 角色成員。</span><span class="sxs-lookup"><span data-stu-id="9cd34-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="9cd34-127">您必須已在電腦上安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="9cd34-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="9cd34-128">Visual Studio 2013 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9cd34-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="9cd34-129">下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="9cd34-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="9cd34-130">瀏覽至 [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後按一下 [.NET] 區段中的 [VS 2013] 或 [VS 2015]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="9cd34-131">下載適用於 Visual Studio 的最新 Azure Data Factory 外掛程式：[VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 或 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="9cd34-132">您也可以執行下列步驟來更新外掛程式：在功能表中按一下 [工具] -> [擴充功能和更新] -> [線上] -> [Visual Studio 組件庫] -> [Microsoft Azure Data Factory Tools for Visual Studio] -> [更新]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="9cd34-133">步驟</span><span class="sxs-lookup"><span data-stu-id="9cd34-133">Steps</span></span>
<span data-ttu-id="9cd34-134">以下是您會在本教學課程中執行的步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd34-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="9cd34-135">此資料處理站中建立**連結服務**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="9cd34-136">在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9cd34-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="9cd34-137">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9cd34-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="9cd34-138">您已建立容器並將資料上傳到此儲存體帳戶，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cd34-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="9cd34-139">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9cd34-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="9cd34-140">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="9cd34-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="9cd34-141">您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cd34-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="9cd34-142">在資料處理站中建立輸入和輸出**資料集**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="9cd34-143">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9cd34-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="9cd34-144">而且，輸入 Blob 資料集會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="9cd34-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="9cd34-145">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9cd34-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="9cd34-146">而且，輸出 SQL 資料表資料集會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="9cd34-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="9cd34-147">在資料處理站中建立**管線**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="9cd34-148">在此步驟中，您會建立具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="9cd34-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="9cd34-149">複製活動會將資料從 Azure Blob 儲存體中的 Blob 複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="9cd34-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="9cd34-150">您可以在管線中使用複製活動，將資料從任何支援的來源複製到任何支援的目的地。</span><span class="sxs-lookup"><span data-stu-id="9cd34-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="9cd34-151">如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="9cd34-152">在部署 Data Factory 實體 (連結服務、資料集/資料表和管線) 時，建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="9cd34-153">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="9cd34-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="9cd34-154">啟動 **Visual Studio 2015**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="9cd34-155">按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="9cd34-156">您應該會看到 [新增專案]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9cd34-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="9cd34-157">在 [新增專案] 對話方塊中，選取 **DataFactory** 範本，然後按一下 [空白 Data Factory 專案]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![[新增專案] 對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="9cd34-159">指定專案名稱、方案位置和方案名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="9cd34-161">建立連結服務</span><span class="sxs-lookup"><span data-stu-id="9cd34-161">Create linked services</span></span>
<span data-ttu-id="9cd34-162">您在資料處理站中建立的連結服務會將您的資料存放區和計算服務連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9cd34-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="9cd34-163">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="9cd34-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="9cd34-164">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="9cd34-165">因此，您會建立兩種連結服務：AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="9cd34-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="9cd34-166">Azure 儲存體已連結的服務會連結 Azure 儲存體帳戶至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9cd34-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="9cd34-167">此儲存體帳戶是您在其中建立容器並將資料上傳為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)一部分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cd34-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="9cd34-168">Azure SQL 連結服務可將 Azure SQL Database 連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9cd34-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="9cd34-169">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="9cd34-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="9cd34-170">您在此資料庫中建立了 emp 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cd34-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="9cd34-171">連結服務會將資料存放區或計算服務連結至 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9cd34-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="9cd34-172">如需複製活動支援的所有來源和接收，請參閱 [支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 。</span><span class="sxs-lookup"><span data-stu-id="9cd34-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="9cd34-173">如需 Data Factory 支援的計算服務清單，請參閱 [計算連結服務](data-factory-compute-linked-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="9cd34-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="9cd34-174">在本教學課程中，您不會使用任何計算服務。</span><span class="sxs-lookup"><span data-stu-id="9cd34-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="9cd34-175">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="9cd34-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="9cd34-176">以滑鼠右鍵按一下 [方案總管] 中的 [連結服務]，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="9cd34-177">在 [新增新項目] 對話方塊中，從清單選取 [Azure 儲存體連結服務]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![新的連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="9cd34-179">使用 Azure 儲存體帳戶的名稱及其金鑰來取代 `<accountname>` 和 `<accountkey>`。</span><span class="sxs-lookup"><span data-stu-id="9cd34-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Azure 儲存體連結服務](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="9cd34-181">儲存 **AzureStorageLinkedService1.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="9cd34-182">如需連結服務定義中 JSON 屬性的詳細資訊，請參閱 [Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="9cd34-183">建立 Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9cd34-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="9cd34-184">再次以滑鼠右鍵按一下 [方案總管] 中的 [連結服務] 節點，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="9cd34-185">這次，請選取 [Azure SQL 連結服務]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="9cd34-186">在 **AzureSqlLinkedService1.json 檔案**中，以您的 Azure SQL Server 名稱、資料庫名稱、使用者帳戶名稱和密碼取代 `<servername>`、`<databasename>`、`<username@servername>` 和 `<password>`。</span><span class="sxs-lookup"><span data-stu-id="9cd34-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="9cd34-187">儲存 **AzureSqlLinkedService1.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="9cd34-188">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="9cd34-189">建立資料集</span><span class="sxs-lookup"><span data-stu-id="9cd34-189">Create datasets</span></span>
<span data-ttu-id="9cd34-190">在上一個步驟中，您已建立可將 Azure 儲存體帳戶和 Azure SQL Database 連結至資料處理站的連結服務。</span><span class="sxs-lookup"><span data-stu-id="9cd34-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="9cd34-191">在此步驟中，您會定義名為 InputDataset 和 OutputDataset 的兩個資料集，它們分別代表 AzureStorageLinkedService1 和 AzureSqlLinkedService1 所參照資料存放區中儲存的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9cd34-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="9cd34-192">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9cd34-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="9cd34-193">而且，輸入 Blob 資料集 (InputDataset) 會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="9cd34-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="9cd34-194">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9cd34-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="9cd34-195">而且，輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="9cd34-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="9cd34-196">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="9cd34-196">Create input dataset</span></span>
<span data-ttu-id="9cd34-197">在此步驟中，您將在 AzureStorageLinkedService1 連結服務所代表的 Azure 儲存體中，建立名為 InputDataset 的資料集，該資料集會指向 Blob 容器 (adftutorial) 根資料夾中的 Blob 檔案 (emp.txt)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="9cd34-198">如果您未指定 (或跳過) fileName 的值，則輸入資料夾中所有 Blob 資料都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="9cd34-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="9cd34-199">在本教學課程中，您可指定 fileName 的值。</span><span class="sxs-lookup"><span data-stu-id="9cd34-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="9cd34-200">在此，您會使用「資料表」一詞，而不是「資料集」。</span><span class="sxs-lookup"><span data-stu-id="9cd34-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="9cd34-201">資料表是矩形的資料集，而且是目前唯一受支援的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="9cd34-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="9cd34-202">以滑鼠右鍵按一下 [方案總管] 中的 [資料表]，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="9cd34-203">在 [新增新項目] 對話方塊中，選取 [Azure Blob]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="9cd34-204">將 JSON 文字取代為下列文字並儲存 **AzureBlobLocation1.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="9cd34-205">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="9cd34-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="9cd34-206">屬性</span><span class="sxs-lookup"><span data-stu-id="9cd34-206">Property</span></span> | <span data-ttu-id="9cd34-207">說明</span><span class="sxs-lookup"><span data-stu-id="9cd34-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9cd34-208">類型</span><span class="sxs-lookup"><span data-stu-id="9cd34-208">type</span></span> | <span data-ttu-id="9cd34-209">type 屬性會設為 **AzureBlob**，因為資料位於 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="9cd34-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="9cd34-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9cd34-210">linkedServiceName</span></span> | <span data-ttu-id="9cd34-211">表示您稍早建立的 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="9cd34-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="9cd34-212">folderPath</span></span> | <span data-ttu-id="9cd34-213">指定包含輸入 Blob 的 Blob **容器**和**資料夾**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="9cd34-214">在本教學課程中，adftutorial 是 blob 容器，而資料夾是根資料夾。</span><span class="sxs-lookup"><span data-stu-id="9cd34-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="9cd34-215">fileName</span><span class="sxs-lookup"><span data-stu-id="9cd34-215">fileName</span></span> | <span data-ttu-id="9cd34-216">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="9cd34-216">This property is optional.</span></span> <span data-ttu-id="9cd34-217">如果您省略此屬性，則會挑選 folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="9cd34-218">在本教學課程中，會針對 fileName 指定 **emp.txt**，因此只會挑選該檔案進行處理。</span><span class="sxs-lookup"><span data-stu-id="9cd34-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="9cd34-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="9cd34-219">format -> type</span></span> |<span data-ttu-id="9cd34-220">輸入檔為文字格式，因此我們會使用 **TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="9cd34-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9cd34-221">columnDelimiter</span></span> | <span data-ttu-id="9cd34-222">輸入檔案中的資料行會以**逗號字元 (`,`)** 分隔。</span><span class="sxs-lookup"><span data-stu-id="9cd34-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="9cd34-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9cd34-223">frequency/interval</span></span> | <span data-ttu-id="9cd34-224">frequency 會設為 **Hour** 且 interval 會設為 **1**，表示**每小時**都可取得輸入配量。</span><span class="sxs-lookup"><span data-stu-id="9cd34-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="9cd34-225">換句話說，Data Factory 服務會每小時都在您指定之 Blob 容器 (**adftutorial**) 的根資料夾中尋找輸入資料。</span><span class="sxs-lookup"><span data-stu-id="9cd34-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="9cd34-226">它會尋找管線開始和結束時間內 (而非這些時間之前或之後) 的資料。</span><span class="sxs-lookup"><span data-stu-id="9cd34-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="9cd34-227">external</span><span class="sxs-lookup"><span data-stu-id="9cd34-227">external</span></span> | <span data-ttu-id="9cd34-228">如果資料不是由此管線產生，此屬性會設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="9cd34-229">本教學課程中的輸入資料位於 emp.txt 檔案中，該檔案不是由此管線產生，因此我們會將此屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="9cd34-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="9cd34-230">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="9cd34-231">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="9cd34-231">Create output dataset</span></span>
<span data-ttu-id="9cd34-232">在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9cd34-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="9cd34-233">此資料集指向 Azure SQL Database 中 **AzureSqlLinkedService1**所代表的 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="9cd34-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="9cd34-234">再次以滑鼠右鍵按一下 [方案總管] 中的 [資料表]，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="9cd34-235">在 [新增新項目] 對話方塊中，選取 [Azure SQL]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="9cd34-236">將 JSON 文字取代成下列 JSON 並儲存 **AzureSqlTableLocation1.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="9cd34-237">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="9cd34-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="9cd34-238">屬性</span><span class="sxs-lookup"><span data-stu-id="9cd34-238">Property</span></span> | <span data-ttu-id="9cd34-239">說明</span><span class="sxs-lookup"><span data-stu-id="9cd34-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9cd34-240">類型</span><span class="sxs-lookup"><span data-stu-id="9cd34-240">type</span></span> | <span data-ttu-id="9cd34-241">type 屬性會設為 **AzureSqlTable**，因為資料已複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="9cd34-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="9cd34-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9cd34-242">linkedServiceName</span></span> | <span data-ttu-id="9cd34-243">表示您稍早建立的 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="9cd34-244">tableName</span><span class="sxs-lookup"><span data-stu-id="9cd34-244">tableName</span></span> | <span data-ttu-id="9cd34-245">指定作為資料複製目的地的**資料表**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="9cd34-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9cd34-246">frequency/interval</span></span> | <span data-ttu-id="9cd34-247">frequency 會設為**Hour** 且 interval 為**1**，這表示會在管線開始和結束時間之間 (而非這些時間之前或之後) **每小時**產生輸出配量。</span><span class="sxs-lookup"><span data-stu-id="9cd34-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="9cd34-248">資料庫的 emp 資料表中有三個資料行 – **ID**、**FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="9cd34-249">ID 是識別資料行，所以您只需在此指定 **FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="9cd34-250">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="9cd34-251">建立管線</span><span class="sxs-lookup"><span data-stu-id="9cd34-251">Create pipeline</span></span>
<span data-ttu-id="9cd34-252">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="9cd34-253">目前，驅動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9cd34-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="9cd34-254">在本教學課程中，輸出資料集設定成一小時產生一次配量。</span><span class="sxs-lookup"><span data-stu-id="9cd34-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="9cd34-255">管線具有相隔一天 (也就是 24 小時) 的開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="9cd34-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="9cd34-256">因此，管線會產生輸出資料集的 24 個配量。</span><span class="sxs-lookup"><span data-stu-id="9cd34-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="9cd34-257">以滑鼠右鍵按一下 [方案總管] 中的 [管線]，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="9cd34-258">選取 [新增新項目] 對話方塊中的 [複製資料管線]，並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="9cd34-259">將 JSON 取代為下列 JSON 並儲存 **CopyActivity1.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob to Azure SQL table",
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
    - <span data-ttu-id="9cd34-260">在活動區段中，只會有一個 **type** 設為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="9cd34-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="9cd34-261">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9cd34-262">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="9cd34-263">活動的輸入設定為 **InputDataset**，活動的輸出則設定為 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="9cd34-264">在 **typeProperties** 區段中，來源類型指定為 **BlobSource**，接收類型指定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="9cd34-265">如需複製活動作為來源和接收器支援的資料存放區完整清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9cd34-266">若要了解如何使用特定支援的資料存放區作為來源/接收器，請按一下資料表中的連結。</span><span class="sxs-lookup"><span data-stu-id="9cd34-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="9cd34-267">將 **start** 屬性的值替換為目前日期，並將 **end**值替換為隔天的日期。</span><span class="sxs-lookup"><span data-stu-id="9cd34-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="9cd34-268">在日期時間中，您只指定日期部分，並略過時間部分。</span><span class="sxs-lookup"><span data-stu-id="9cd34-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="9cd34-269">例如，"2016-02-03"，這相當於 "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="9cd34-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="9cd34-270">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9cd34-271">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="9cd34-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="9cd34-272">**end** 時間為選擇性項目，但在本教學課程中會用到。</span><span class="sxs-lookup"><span data-stu-id="9cd34-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="9cd34-273">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="9cd34-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="9cd34-274">若要無限期地執行管線，請指定 **9999-09-09** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="9cd34-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="9cd34-275">在上述範例中，由於每小時即產生一個資料配量，共會有 24 個資料配量。</span><span class="sxs-lookup"><span data-stu-id="9cd34-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="9cd34-276">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9cd34-277">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9cd34-278">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="9cd34-279">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="9cd34-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="9cd34-280">發佈/部署 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="9cd34-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="9cd34-281">在此步驟中，您會發佈稍早建立的 Data Factory 實體 (連結的服務、資料集和管線)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="9cd34-282">您也可以指定要建立來保存這些實體的新 Data Factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="9cd34-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="9cd34-283">在 [方案總管] 中，以滑鼠右鍵按一下專案，再按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="9cd34-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="9cd34-284">如果您看到 [登入您的 Microsoft 帳戶] 對話方塊，請輸入具有 Azure 訂用帳戶的帳戶認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="9cd34-285">您應該會看到下列對話方塊：</span><span class="sxs-lookup"><span data-stu-id="9cd34-285">You should see the following dialog box:</span></span>
   
   ![發佈對話方塊](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="9cd34-287">在 [設定 Data Factory] 頁面中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd34-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="9cd34-288">選取 [建立新的 Data Factory]  選項。</span><span class="sxs-lookup"><span data-stu-id="9cd34-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="9cd34-289">針對 [名稱] 輸入 **VSTutorialFactory**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="9cd34-290">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9cd34-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="9cd34-291">如果您在發佈時收到與 Data Factory 名稱有關的錯誤，請變更 Data Factory 的名稱 (例如 yournameVSTutorialFactory) 並嘗試再發佈一次。</span><span class="sxs-lookup"><span data-stu-id="9cd34-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="9cd34-292">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="9cd34-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="9cd34-293">針對 [訂用帳戶]  欄位選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cd34-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="9cd34-294">如果看不到任何訂用帳戶，請確定您是使用訂用帳戶的管理員或共同管理員的帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="9cd34-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="9cd34-295">針對要建立的 Data Factory 選取 [資源群組]  。</span><span class="sxs-lookup"><span data-stu-id="9cd34-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="9cd34-296">選取 Data Factory 的 [區域]  。</span><span class="sxs-lookup"><span data-stu-id="9cd34-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="9cd34-297">下拉式清單中只會顯示 Data Factory 服務支援的區域。</span><span class="sxs-lookup"><span data-stu-id="9cd34-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="9cd34-298">按 [下一步]，切換至 [發佈項目] 頁面。</span><span class="sxs-lookup"><span data-stu-id="9cd34-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![設定 Data Factory 頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="9cd34-300">在 [發佈項目] 頁面上，確認所有 Data Factory 實體都已選取，並按 [下一步] 切換至 [摘要] 頁面。</span><span class="sxs-lookup"><span data-stu-id="9cd34-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![發佈項目頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="9cd34-302">檢閱摘要，然後按 [下一步] 開始部署程序，並檢視 [部署狀態]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![發佈摘要頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="9cd34-304">在 [部署狀態]  頁面上，您應該會看到部署程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="9cd34-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="9cd34-305">部署完成後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-305">Click Finish after the deployment is done.</span></span>
 
   ![部署狀態頁面](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="9cd34-307">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="9cd34-307">Note the following points:</span></span> 

* <span data-ttu-id="9cd34-308">如果您收到錯誤：「此訂用帳戶未註冊為使用命名空間 Microsoft.DataFactory」，請執行下列其中一項，然後嘗試再次發佈︰</span><span class="sxs-lookup"><span data-stu-id="9cd34-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="9cd34-309">在 Azure PowerShell 中，執行下列命令以註冊 Data Factory 提供者。</span><span class="sxs-lookup"><span data-stu-id="9cd34-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="9cd34-310">您可以執行下列命令來確認已註冊 Data Factory 提供者。</span><span class="sxs-lookup"><span data-stu-id="9cd34-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="9cd34-311">使用 Azure 訂用帳戶登入 [Azure 入口網站](https://portal.azure.com) 並瀏覽至 [Data Factory] 刀鋒視窗 (或) 在 Azure 入口網站中建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9cd34-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="9cd34-312">此動作會自動為您註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="9cd34-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="9cd34-313">Data Factory 的名稱未來可能會註冊為 DNS 名稱，因此會變成公開可見的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cd34-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cd34-314">若要建立 Data Factory 執行個體，您必須是 Azure 訂用帳戶的管理員/共同管理員</span><span class="sxs-lookup"><span data-stu-id="9cd34-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="9cd34-315">監視管線</span><span class="sxs-lookup"><span data-stu-id="9cd34-315">Monitor pipeline</span></span>
<span data-ttu-id="9cd34-316">瀏覽至您的資料處理站首頁：</span><span class="sxs-lookup"><span data-stu-id="9cd34-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="9cd34-317">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cd34-318">按一下左側功能表上的 [更多服務]，然後按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![瀏覽 Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="9cd34-320">開始輸入您的資料處理站名稱。</span><span class="sxs-lookup"><span data-stu-id="9cd34-320">Start typing the name of your data factory.</span></span>

    ![資料處理站名稱](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="9cd34-322">按一下結果清單中您的資料處理站，以查看您的資料處理站首頁。</span><span class="sxs-lookup"><span data-stu-id="9cd34-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="9cd34-324">請遵循[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)中的指示，監視您在本教學課程中建立的管線和資料集。</span><span class="sxs-lookup"><span data-stu-id="9cd34-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="9cd34-325">Visual Studio 目前不支援監視 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="9cd34-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="9cd34-326">摘要</span><span class="sxs-lookup"><span data-stu-id="9cd34-326">Summary</span></span>
<span data-ttu-id="9cd34-327">在本教學課程中，您已建立要將資料從 Azure Blob 複製到 Azure SQL 資料庫的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9cd34-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="9cd34-328">您已使用 Visual Studio 建立 Data Factory、連結服務、資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="9cd34-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="9cd34-329">以下是您在本教學課程中執行的高階步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd34-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="9cd34-330">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="9cd34-331">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="9cd34-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="9cd34-332">**Azure 儲存體** 連結服務可連結保留輸入資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cd34-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="9cd34-333">**Azure SQL** 連結服務可連結保留輸出資料的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9cd34-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="9cd34-334">建立可描述管線輸入資料和輸出資料的 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="9cd34-335">建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="9cd34-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="9cd34-336">若要了解如何使用 HDInsight Hive 活動以利用 Azure HDInsight 叢集轉換資料，請參閱[教學課程︰使用 Hadoop 叢集建置第一個管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="9cd34-337">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="9cd34-338">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="9cd34-339">在 Server Explorer 中檢視所有資料處理站</span><span class="sxs-lookup"><span data-stu-id="9cd34-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="9cd34-340">本節說明如何使用 Visual Studio 中的 Server Explorer，檢視 Azure 訂用帳戶中的所有資料處理站並根據現有的資料處理站建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="9cd34-341">在 **Visual Studio** 中，按一下功能表上的 [檢視]，然後按一下 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="9cd34-342">在 [伺服器總管] 視窗中，依序展開 **Azure** 和 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="9cd34-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="9cd34-343">如果您看到 [登入 Visual Studio]，請輸入和 Azure 訂用帳戶相關聯的**帳戶**，然後按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="9cd34-344">輸入**密碼**，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="9cd34-345">Visual Studio 會嘗試取得訂用帳戶中所有 Azure Data Factory 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9cd34-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="9cd34-346">您會在 [Data Factory 工作清單] 視窗中看到這項作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="9cd34-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="9cd34-348">建立現有資料處理站的 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="9cd34-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="9cd34-349">在 Server Explorer 中的資料處理站上按一下滑鼠右鍵，並選取 [將 Data Factory 匯出至新的專案]，以便根據現有的資料處理站建立 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="9cd34-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![匯出 Data Factory 至 VS 專案](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="9cd34-351">更新 Visual studio 的 Data Factory 工具</span><span class="sxs-lookup"><span data-stu-id="9cd34-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="9cd34-352">若要更新 Visual Studio 的 Azure Data Factory 工具，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd34-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="9cd34-353">按一下功能表上的 [工具]，然後選取 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="9cd34-354">選取左窗格中的 [更新]，然後選取 [Visual Studio 組件庫]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="9cd34-355">選取 [Visual Studio 的 Azure Data Factory 工具] 並按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="9cd34-356">如果您看不到此項目，代表您已經有最新版本的工具。</span><span class="sxs-lookup"><span data-stu-id="9cd34-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="9cd34-357">使用組態檔</span><span class="sxs-lookup"><span data-stu-id="9cd34-357">Use configuration files</span></span>
<span data-ttu-id="9cd34-358">您可以在 Visual Studio 中使用組態檔，針對各個環境分別設定連結服務/資料表/管線的屬性。</span><span class="sxs-lookup"><span data-stu-id="9cd34-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="9cd34-359">請針對 Azure 儲存體連結服務考量下列 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="9cd34-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="9cd34-360">根據您部署 Data Factory 實體的環境 (開發/測試/生產)，針對 accountname 和 accountkey 指定具有不同值的 **connectionString** 。</span><span class="sxs-lookup"><span data-stu-id="9cd34-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="9cd34-361">您可以針對每個環境使用個別的組態檔來達成此行為。</span><span class="sxs-lookup"><span data-stu-id="9cd34-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="9cd34-362">新增組態檔</span><span class="sxs-lookup"><span data-stu-id="9cd34-362">Add a configuration file</span></span>
<span data-ttu-id="9cd34-363">藉由執行下列步驟來新增每個環境的組態檔：</span><span class="sxs-lookup"><span data-stu-id="9cd34-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="9cd34-364">在 Visual Studio 解決方案中以滑鼠右鍵按一下 Data Factory 專案，指向 [新增]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="9cd34-365">從左側的已安裝範本清單中選取 [設定]、選取 [設定檔]、輸入設定檔的 [名稱]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![新增組態檔](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="9cd34-367">以下列格式新增設定參數和其值：</span><span class="sxs-lookup"><span data-stu-id="9cd34-367">Add configuration parameters and their values in the following format:</span></span>

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

    <span data-ttu-id="9cd34-368">這個範例會設定 Azure 儲存體連結服務和 Azure SQL 連結服務的 connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="9cd34-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="9cd34-369">請注意，指定名稱的語法是 [JsonPath](http://goessner.net/articles/JsonPath/)。</span><span class="sxs-lookup"><span data-stu-id="9cd34-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="9cd34-370">如果 JSON 具有屬性，該屬性具有如下列程式碼所示的值陣列：</span><span class="sxs-lookup"><span data-stu-id="9cd34-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

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

    <span data-ttu-id="9cd34-371">設定如下列組態檔所示的屬性 (使用以零為起始的索引)︰</span><span class="sxs-lookup"><span data-stu-id="9cd34-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="9cd34-372">包含空格的屬性名稱</span><span class="sxs-lookup"><span data-stu-id="9cd34-372">Property names with spaces</span></span>
<span data-ttu-id="9cd34-373">如果屬性名稱內含空格，請使用如下列範例 (資料庫伺服器名稱) 中所示的方括號：</span><span class="sxs-lookup"><span data-stu-id="9cd34-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="9cd34-374">使用組態部署解決方案</span><span class="sxs-lookup"><span data-stu-id="9cd34-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="9cd34-375">當您在 VS 中發佈 Azure Data Factory 實體時，您可以指定想要用於該發佈作業的組態。</span><span class="sxs-lookup"><span data-stu-id="9cd34-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="9cd34-376">若要使用組態檔在 Azure Data Factory 專案中發佈實體：</span><span class="sxs-lookup"><span data-stu-id="9cd34-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="9cd34-377">以滑鼠右鍵按一下 Data Factory 專案，然後按一下 [發佈] 以查看 [發佈項目] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9cd34-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="9cd34-378">選取現有的 Data Factory，或指定值以在 [設定 Data Factory] 頁面上建立 Data Factory，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="9cd34-379">在 [發佈項目] 頁面：您會看到下拉式清單，其中具有 [選取部署設定] 欄位的可用設定。</span><span class="sxs-lookup"><span data-stu-id="9cd34-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![選取組態檔](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="9cd34-381">選取您想要使用的**設定檔**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="9cd34-382">確認您在 [摘要] 頁面上看到 JSON 檔案的名稱，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9cd34-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="9cd34-383">部署作業完成後按一下 [完成]  。</span><span class="sxs-lookup"><span data-stu-id="9cd34-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="9cd34-384">部署時，在將實體部署至 Azure Data Factory 服務之前，會使用組態檔的值來設定 JSON 檔案中的屬性值。</span><span class="sxs-lookup"><span data-stu-id="9cd34-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="9cd34-385">使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9cd34-385">Use Azure Key Vault</span></span>
<span data-ttu-id="9cd34-386">不建議認可機密資料 (例如將字串連線至程式碼存放庫)，且通常會違反安全性原則。</span><span class="sxs-lookup"><span data-stu-id="9cd34-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="9cd34-387">請參閱 GitHub 上的 [ADF 安全發佈](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)範例，了解在 Azure Key Vault 中儲存機密資訊和在發行 Data Factory 實體時使用它。</span><span class="sxs-lookup"><span data-stu-id="9cd34-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="9cd34-388">Visual Studio 的安全發佈擴充功能可在 Key Vault 中儲存機密資料，且僅在連結服務 / 部署組態中指定時才予以參考。</span><span class="sxs-lookup"><span data-stu-id="9cd34-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="9cd34-389">當您將 Data Factory 實體發佈至 Azure 時，會解析這些參考。</span><span class="sxs-lookup"><span data-stu-id="9cd34-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="9cd34-390">接著這些檔案可以認可至來源存放庫而不公開任何機密資訊。</span><span class="sxs-lookup"><span data-stu-id="9cd34-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9cd34-391">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cd34-391">Next steps</span></span>
<span data-ttu-id="9cd34-392">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9cd34-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9cd34-393">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="9cd34-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9cd34-394">若要深入了解如何從資料存放區雙向複製資料，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="9cd34-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>