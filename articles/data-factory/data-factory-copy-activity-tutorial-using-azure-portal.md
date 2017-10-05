---
title: "教學課程︰建立 Azure Data Factory 管線來複製資料 (Azure 入口網站) |Microsoft 文件"
description: "在本教學課程中，您會使用 Azure 入口網站建立具有複製活動的 Azure Data Factory 管線，以將資料從 Azure Blob 儲存體複製到 Azure SQL Database。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8072a863fab0b304ccbbba639aa56b403e8f37c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-portal-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="1f504-103">本教學課程︰使用 Azure 入口網站建立 Data Factory 管線來複製資料</span><span class="sxs-lookup"><span data-stu-id="1f504-103">Tutorial: Use Azure portal to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f504-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="1f504-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1f504-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="1f504-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1f504-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1f504-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1f504-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f504-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1f504-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f504-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1f504-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1f504-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1f504-110">REST API</span><span class="sxs-lookup"><span data-stu-id="1f504-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1f504-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="1f504-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="1f504-112">在本文中，您會了解如何使用 [Azure 入口網站](https://portal.azure.com)建立資料處理站，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f504-112">In this article, you learn how to use [Azure portal](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="1f504-113">如果您不熟悉 Azure Data Factory，請先詳閱 [Azure Data Factory 簡介](data-factory-introduction.md)一文，再進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="1f504-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="1f504-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="1f504-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="1f504-115">複製活動會將資料從支援的資料存放區複製到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="1f504-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="1f504-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="1f504-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1f504-117">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="1f504-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1f504-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="1f504-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="1f504-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1f504-120">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="1f504-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1f504-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="1f504-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="1f504-122">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="1f504-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="1f504-123">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f504-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="1f504-124">Prerequisites</span></span>
<span data-ttu-id="1f504-125">請先完成[教學課程必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)一文中所列的必要條件，再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="1f504-125">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="1f504-126">步驟</span><span class="sxs-lookup"><span data-stu-id="1f504-126">Steps</span></span>
<span data-ttu-id="1f504-127">以下是您會在本教學課程中執行的步驟：</span><span class="sxs-lookup"><span data-stu-id="1f504-127">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="1f504-128">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="1f504-128">Create an Azure **data factory**.</span></span> <span data-ttu-id="1f504-129">在此步驟中，您會建立名為 ADFTutorialDataFactory 的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-129">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="1f504-130">此資料處理站中建立**連結服務**。</span><span class="sxs-lookup"><span data-stu-id="1f504-130">Create **linked services** in the data factory.</span></span> <span data-ttu-id="1f504-131">在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="1f504-131">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="1f504-132">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-132">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="1f504-133">您已建立容器並將資料上傳到此儲存體帳戶，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="1f504-133">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="1f504-134">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-134">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1f504-135">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="1f504-135">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="1f504-136">您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="1f504-136">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="1f504-137">在資料處理站中建立輸入和輸出**資料集**。</span><span class="sxs-lookup"><span data-stu-id="1f504-137">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="1f504-138">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1f504-138">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="1f504-139">而且，輸入 Blob 資料集會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="1f504-139">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="1f504-140">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1f504-140">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1f504-141">而且，輸出 SQL 資料表資料集會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f504-141">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="1f504-142">在資料處理站中建立**管線**。</span><span class="sxs-lookup"><span data-stu-id="1f504-142">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="1f504-143">在此步驟中，您會建立具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-143">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="1f504-144">複製活動會將資料從 Azure Blob 儲存體中的 Blob 複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f504-144">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="1f504-145">您可以在管線中使用複製活動，將資料從任何支援的來源複製到任何支援的目的地。</span><span class="sxs-lookup"><span data-stu-id="1f504-145">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="1f504-146">如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-146">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="1f504-147">監視管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-147">Monitor the pipeline.</span></span> <span data-ttu-id="1f504-148">在此步驟中，您會使用 Azure 入口網站來**監視**輸入和輸出資料集的配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-148">In this step, you **monitor** the slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="1f504-149">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f504-149">Create data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f504-150">如果您尚未完成[教學課程的必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)，請先這麼做。</span><span class="sxs-lookup"><span data-stu-id="1f504-150">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="1f504-151">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-151">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1f504-152">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="1f504-152">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1f504-153">例如，「複製活動」會從來源將資料複製到目的地資料存放區，HDInsight Hive 活動則是執行 Hive 指令碼來轉換輸入資料，以產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="1f504-153">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="1f504-154">讓我們在這個步驟中開始建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="1f504-154">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="1f504-155">登入 [Azure 入口網站](https://portal.azure.com/)之後，按一下左功能表上的 [新增]，按一下 [資料 + 分析]，然後按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="1f504-155">After logging in to the [Azure portal](https://portal.azure.com/), click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![新增->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="1f504-157">在 [ **新增 Data Factory** ] 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="1f504-157">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="1f504-158">輸入 **ADFTutorialDataFactory** 做為**名稱**。</span><span class="sxs-lookup"><span data-stu-id="1f504-158">Enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
         ![新增 Data Factory 刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="1f504-160">Azure Data Factory 的名稱必須是 **全域唯一的**。</span><span class="sxs-lookup"><span data-stu-id="1f504-160">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="1f504-161">如果您收到錯誤，請變更 Data Factory 名稱 (例如 yournameADFTutorialDataFactory)，然後試著重新建立。</span><span class="sxs-lookup"><span data-stu-id="1f504-161">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="1f504-162">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="1f504-162">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="1f504-164">選取您要在其中建立資料處理站的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1f504-164">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
   3. <span data-ttu-id="1f504-165">針對 [資源群組]，請執行下列其中一個步驟︰</span><span class="sxs-lookup"><span data-stu-id="1f504-165">For the **Resource Group**, do one of the following steps:</span></span>
      
      - <span data-ttu-id="1f504-166">選取 [使用現有的] ，然後從下拉式清單選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1f504-166">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="1f504-167">選取 [建立新的] ，然後輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="1f504-167">Select **Create new**, and enter the name of a resource group.</span></span>   
         
          <span data-ttu-id="1f504-168">本教學課程的某些步驟是假設您使用 **ADFTutorialResourceGroup** 做為資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1f504-168">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="1f504-169">若要了解資源群組，請參閱 [使用資源群組管理您的 Azure 資源](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-169">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="1f504-170">選取 Data Factory 的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="1f504-170">Select the **location** for the data factory.</span></span> <span data-ttu-id="1f504-171">下拉式清單中只會顯示 Data Factory 服務支援的區域。</span><span class="sxs-lookup"><span data-stu-id="1f504-171">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   5. <span data-ttu-id="1f504-172">選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="1f504-172">Select **Pin to dashboard**.</span></span>     
   6. <span data-ttu-id="1f504-173">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1f504-173">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="1f504-174">若要建立 Data Factory 執行個體，您必須是訂用帳戶/資源群組層級的 [Data Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 角色成員。</span><span class="sxs-lookup"><span data-stu-id="1f504-174">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
      > 
      > <span data-ttu-id="1f504-175">Data Factory 的名稱未來可能會註冊為 DNS 名稱，因此會變成公開可見的名稱。</span><span class="sxs-lookup"><span data-stu-id="1f504-175">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>                
      > 
      > 
3. <span data-ttu-id="1f504-176">在儀表板上，您會看到狀態如下的下列圖格︰**正在部署資料處理站**。</span><span class="sxs-lookup"><span data-stu-id="1f504-176">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![部署資料處理站圖格](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="1f504-178">建立完成之後，您會看到如圖所示的 [Data Factory]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1f504-178">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span></span>
   
   ![Data Factory 首頁](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="1f504-180">建立連結服務</span><span class="sxs-lookup"><span data-stu-id="1f504-180">Create linked services</span></span>
<span data-ttu-id="1f504-181">您在資料處理站中建立的連結服務會將您的資料存放區和計算服務連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-181">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="1f504-182">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="1f504-182">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="1f504-183">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="1f504-183">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="1f504-184">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="1f504-184">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="1f504-185">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-185">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="1f504-186">此儲存體帳戶是您在其中建立容器並將資料上傳為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)一部分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1f504-186">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="1f504-187">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-187">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1f504-188">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="1f504-188">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="1f504-189">您在此資料庫中建立了 emp 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="1f504-189">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="1f504-190">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="1f504-190">Create Azure Storage linked service</span></span>
<span data-ttu-id="1f504-191">在此步驟中，您會將您的 Azure 儲存體帳戶連結到您的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1f504-191">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="1f504-192">在此區段中指定您 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="1f504-192">You specify the name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="1f504-193">在 [Data Factory] 刀鋒視窗中，按一下 [製作和部署] 圖格。</span><span class="sxs-lookup"><span data-stu-id="1f504-193">In the **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![[製作和部署] 磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="1f504-195">您會看到如下圖所示的 [Data Factory 編輯器]：</span><span class="sxs-lookup"><span data-stu-id="1f504-195">You see the **Data Factory Editor** as shown in the following image:</span></span> 

    ![Data Factory 編輯器](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="1f504-197">在編輯器中，按一下工具列上的 [新增資料存放區] 按鈕，然後從下拉式功能表中選取 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="1f504-197">In the editor, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span></span> <span data-ttu-id="1f504-198">在右窗格中，您應該會看到用來建立 Azure 儲存體連結服務的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="1f504-198">You should see the JSON template for creating an Azure storage linked service in the right pane.</span></span> 
   
    ![編輯器 [新增資料存放區] 按鈕](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="1f504-200">將 `<accountname>` 和 `<accountkey>` 取代為 Azure 儲存體帳戶的帳戶名稱和帳戶金鑰值。</span><span class="sxs-lookup"><span data-stu-id="1f504-200">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span></span> 
   
    ![編輯器 Blob 儲存體 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="1f504-202">按一下工具列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="1f504-202">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="1f504-203">您現在應該會在樹狀檢視中看到已部署的 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="1f504-203">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span></span> 
   
    ![編輯器 Blob 儲存體部署](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="1f504-205">如需連結服務定義中 JSON 屬性的詳細資訊，請參閱 [Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-205">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-the-azure-sql-database"></a><span data-ttu-id="1f504-206">建立 Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="1f504-206">Create a linked service for the Azure SQL Database</span></span>
<span data-ttu-id="1f504-207">在此步驟中，您會將您的 Azure SQL Database 連結到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="1f504-207">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="1f504-208">在此區段中指定 Azure SQL 伺服器名稱、資料庫名稱、使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1f504-208">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="1f504-209">在 [Data Factory 編輯器] 中，按一下工具列上的 [新增資料存放區] 按鈕，然後從下拉式功能表中選取 [Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="1f504-209">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span></span> <span data-ttu-id="1f504-210">在右窗格中，您應該會看到用來建立 Azure SQL 連結服務的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="1f504-210">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span></span>
2. <span data-ttu-id="1f504-211">以您的 Azure SQL Server 名稱、資料庫名稱、使用者帳戶名稱和密碼取代 `<servername>`、`<databasename>`、`<username>@<servername>` 和 `<password>`。</span><span class="sxs-lookup"><span data-stu-id="1f504-211">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="1f504-212">按一下工具列上的 [部署]，以建立並部署 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="1f504-212">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="1f504-213">確認您已在 [連結服務] 下的樹狀檢視中看到 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="1f504-213">Confirm that you see **AzureSqlLinkedService** in the tree view under **Linked services**.</span></span>  

    <span data-ttu-id="1f504-214">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="1f504-214">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="1f504-215">建立資料集</span><span class="sxs-lookup"><span data-stu-id="1f504-215">Create datasets</span></span>
<span data-ttu-id="1f504-216">在上一個步驟中，您已建立可將 Azure 儲存體帳戶和 Azure SQL Database 連結至資料處理站的連結服務。</span><span class="sxs-lookup"><span data-stu-id="1f504-216">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="1f504-217">在此步驟中，您會定義名為 InputDataset 和 OutputDataset 的兩個資料集，它們分別代表 AzureStorageLinkedService 和 AzureSqlLinkedService 所參照資料存放區中儲存的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="1f504-217">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="1f504-218">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1f504-218">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="1f504-219">而且，輸入 Blob 資料集 (InputDataset) 會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="1f504-219">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="1f504-220">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1f504-220">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1f504-221">而且，輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f504-221">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="1f504-222">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="1f504-222">Create input dataset</span></span>
<span data-ttu-id="1f504-223">在此步驟中，您將在 AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中，建立名為 InputDataset 的資料集，該資料集會指向 Blob 容器 (adftutorial) 根資料夾中的 Blob 檔案 (emp.txt)。</span><span class="sxs-lookup"><span data-stu-id="1f504-223">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="1f504-224">如果您未指定 (或跳過) fileName 的值，則輸入資料夾中所有 Blob 資料都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="1f504-224">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="1f504-225">在本教學課程中，您可指定 fileName 的值。</span><span class="sxs-lookup"><span data-stu-id="1f504-225">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="1f504-226">在 Data Factory 的 [編輯器] 中，依序按一下下拉式功能表中的 **[...更多]**、[新增資料集] 和 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="1f504-226">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span></span> 
   
    ![新增資料集功能表](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="1f504-228">將右窗格中的 JSON 替換為以下 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="1f504-228">Replace JSON in the right pane with the following JSON snippet:</span></span> 
   
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
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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

    <span data-ttu-id="1f504-229">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="1f504-229">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="1f504-230">屬性</span><span class="sxs-lookup"><span data-stu-id="1f504-230">Property</span></span> | <span data-ttu-id="1f504-231">說明</span><span class="sxs-lookup"><span data-stu-id="1f504-231">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="1f504-232">類型</span><span class="sxs-lookup"><span data-stu-id="1f504-232">type</span></span> | <span data-ttu-id="1f504-233">type 屬性會設為 **AzureBlob**，因為資料位於 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="1f504-233">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="1f504-234">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1f504-234">linkedServiceName</span></span> | <span data-ttu-id="1f504-235">表示您稍早建立的 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="1f504-235">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="1f504-236">folderPath</span><span class="sxs-lookup"><span data-stu-id="1f504-236">folderPath</span></span> | <span data-ttu-id="1f504-237">指定包含輸入 Blob 的 Blob **容器**和**資料夾**。</span><span class="sxs-lookup"><span data-stu-id="1f504-237">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="1f504-238">在本教學課程中，adftutorial 是 blob 容器，而資料夾是根資料夾。</span><span class="sxs-lookup"><span data-stu-id="1f504-238">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="1f504-239">fileName</span><span class="sxs-lookup"><span data-stu-id="1f504-239">fileName</span></span> | <span data-ttu-id="1f504-240">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="1f504-240">This property is optional.</span></span> <span data-ttu-id="1f504-241">如果您省略此屬性，則會挑選 folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="1f504-241">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="1f504-242">在本教學課程中，會針對 fileName 指定 **emp.txt**，因此只會挑選該檔案進行處理。</span><span class="sxs-lookup"><span data-stu-id="1f504-242">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="1f504-243">format -> type</span><span class="sxs-lookup"><span data-stu-id="1f504-243">format -> type</span></span> |<span data-ttu-id="1f504-244">輸入檔為文字格式，因此我們會使用 **TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="1f504-244">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="1f504-245">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="1f504-245">columnDelimiter</span></span> | <span data-ttu-id="1f504-246">輸入檔案中的資料行會以**逗號字元 (`,`)** 分隔。</span><span class="sxs-lookup"><span data-stu-id="1f504-246">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="1f504-247">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1f504-247">frequency/interval</span></span> | <span data-ttu-id="1f504-248">frequency 會設為 **Hour** 且 interval 會設為 **1**，表示**每小時**都可取得輸入配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-248">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="1f504-249">換句話說，Data Factory 服務會每小時都在您指定之 Blob 容器 (**adftutorial**) 的根資料夾中尋找輸入資料。</span><span class="sxs-lookup"><span data-stu-id="1f504-249">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="1f504-250">它會尋找管線開始和結束時間內 (而非這些時間之前或之後) 的資料。</span><span class="sxs-lookup"><span data-stu-id="1f504-250">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="1f504-251">external</span><span class="sxs-lookup"><span data-stu-id="1f504-251">external</span></span> | <span data-ttu-id="1f504-252">如果資料不是由此管線產生，此屬性會設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="1f504-252">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="1f504-253">本教學課程中的輸入資料位於 emp.txt 檔案中，該檔案不是由此管線產生，因此我們會將此屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="1f504-253">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="1f504-254">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-254">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="1f504-255">按一下工具列上的 [部署]，以建立並部署 **InputDataset** 資料集。</span><span class="sxs-lookup"><span data-stu-id="1f504-255">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span></span> <span data-ttu-id="1f504-256">確認您已在樹狀檢視中看到 **InputDataset** 。</span><span class="sxs-lookup"><span data-stu-id="1f504-256">Confirm that you see the **InputDataset** in the tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="1f504-257">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="1f504-257">Create output dataset</span></span>
<span data-ttu-id="1f504-258">Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1f504-258">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1f504-259">您在此步驟中建立的輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f504-259">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="1f504-260">在 Data Factory 的 [編輯器] 中，依序按一下下拉式功能表中的 **[...更多]**、[新增資料集] 和 [Azure SQL]。</span><span class="sxs-lookup"><span data-stu-id="1f504-260">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span></span> 
2. <span data-ttu-id="1f504-261">將右窗格中的 JSON 替換為以下 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="1f504-261">Replace JSON in the right pane with the following JSON snippet:</span></span>

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
        "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="1f504-262">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="1f504-262">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="1f504-263">屬性</span><span class="sxs-lookup"><span data-stu-id="1f504-263">Property</span></span> | <span data-ttu-id="1f504-264">說明</span><span class="sxs-lookup"><span data-stu-id="1f504-264">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="1f504-265">類型</span><span class="sxs-lookup"><span data-stu-id="1f504-265">type</span></span> | <span data-ttu-id="1f504-266">type 屬性會設為 **AzureSqlTable**，因為資料已複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="1f504-266">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="1f504-267">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1f504-267">linkedServiceName</span></span> | <span data-ttu-id="1f504-268">表示您稍早建立的 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="1f504-268">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="1f504-269">tableName</span><span class="sxs-lookup"><span data-stu-id="1f504-269">tableName</span></span> | <span data-ttu-id="1f504-270">指定作為資料複製目的地的**資料表**。</span><span class="sxs-lookup"><span data-stu-id="1f504-270">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="1f504-271">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1f504-271">frequency/interval</span></span> | <span data-ttu-id="1f504-272">frequency 會設為**Hour** 且 interval 為**1**，這表示會在管線開始和結束時間之間 (而非這些時間之前或之後) **每小時**產生輸出配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-272">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="1f504-273">資料庫的 emp 資料表中有三個資料行 – **ID**、**FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="1f504-273">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="1f504-274">ID 是識別資料行，所以您只需在此指定 **FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="1f504-274">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="1f504-275">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-275">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="1f504-276">按一下工具列上的 [部署]，以建立並部署 **OutputDataset** 資料集。</span><span class="sxs-lookup"><span data-stu-id="1f504-276">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span></span> <span data-ttu-id="1f504-277">確認您已在 **Datasets** 之下的樹狀檢視中看到 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="1f504-277">Confirm that you see the **OutputDataset** in the tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="1f504-278">建立管線</span><span class="sxs-lookup"><span data-stu-id="1f504-278">Create pipeline</span></span>
<span data-ttu-id="1f504-279">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="1f504-279">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="1f504-280">目前，驅動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="1f504-280">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="1f504-281">在本教學課程中，輸出資料集設定成一小時產生一次配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-281">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="1f504-282">管線具有相隔一天 (也就是 24 小時) 的開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="1f504-282">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="1f504-283">因此，管線會產生輸出資料集的 24 個配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-283">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="1f504-284">在 Data Factory 的 [編輯器] 中，依序按一下下拉式功能表中的 **[...更多]** 和 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="1f504-284">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="1f504-285">或者，您也可以在樹狀檢視中，以滑鼠右鍵按一下 [管線]，再按一下 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="1f504-285">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="1f504-286">將右窗格中的 JSON 替換為以下 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="1f504-286">Replace JSON in the right pane with the following JSON snippet:</span></span> 

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    <span data-ttu-id="1f504-287">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="1f504-287">Note the following points:</span></span>
   
    - <span data-ttu-id="1f504-288">在活動區段中，只會有一個 **type** 設為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="1f504-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="1f504-289">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="1f504-290">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="1f504-291">活動的輸入設定為 **InputDataset**，活動的輸出則設定為 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="1f504-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="1f504-292">在 **typeProperties** 區段中，來源類型指定為 **BlobSource**，接收類型指定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="1f504-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="1f504-293">如需複製活動作為來源和接收器支援的資料存放區完整清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="1f504-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1f504-294">若要了解如何使用特定支援的資料存放區作為來源/接收器，請按一下資料表中的連結。</span><span class="sxs-lookup"><span data-stu-id="1f504-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>
    - <span data-ttu-id="1f504-295">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="1f504-295">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="1f504-296">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="1f504-296">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="1f504-297">**end** 時間為選擇性項目，但在本教學課程中會用到。</span><span class="sxs-lookup"><span data-stu-id="1f504-297">The **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="1f504-298">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="1f504-298">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="1f504-299">若要無限期地執行管線，請指定 **9999-09-09** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1f504-299">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="1f504-300">在上述範例中，由於每小時即產生一個資料配量，共會有 24 個資料配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-300">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="1f504-301">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-301">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1f504-302">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-302">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="1f504-303">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-303">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="1f504-304">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="1f504-304">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="1f504-305">按一下工具列上的 [部署]，建立並部署 **ADFTutorialPipeline**。</span><span class="sxs-lookup"><span data-stu-id="1f504-305">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span></span> <span data-ttu-id="1f504-306">確認您在樹狀檢視中看到管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-306">Confirm that you see the pipeline in the tree view.</span></span> 
4. <span data-ttu-id="1f504-307">現在，按一下 **X** 關閉 [編輯器] 刀鋒視窗。再次按一下 **X**，以查看 **ADFTutorialDataFactory** 的 **Data Factory** 首頁。</span><span class="sxs-lookup"><span data-stu-id="1f504-307">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="1f504-308">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="1f504-308">**Congratulations!**</span></span> <span data-ttu-id="1f504-309">您已成功建立 Azure Data Factory，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="1f504-309">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="1f504-310">監視管線</span><span class="sxs-lookup"><span data-stu-id="1f504-310">Monitor pipeline</span></span>
<span data-ttu-id="1f504-311">在此步驟中，您會使用 Azure 入口網站來監視 Azure Data Factory 的運作情形。</span><span class="sxs-lookup"><span data-stu-id="1f504-311">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="1f504-312">使用監視及管理應用程式來監視管線</span><span class="sxs-lookup"><span data-stu-id="1f504-312">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="1f504-313">下列步驟顯示如何使用「監視及管理」應用程式來監視資料處理站中的管線︰</span><span class="sxs-lookup"><span data-stu-id="1f504-313">The following steps show you how to monitor pipelines in your data factory by using the Monitor & Manage application:</span></span> 

1. <span data-ttu-id="1f504-314">在 Data Factory 首頁上按一下 [監視及管理] 圖格。</span><span class="sxs-lookup"><span data-stu-id="1f504-314">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>
   
    ![監視及管理圖格](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="1f504-316">您應該會在個別的索引標籤中看到 [監視及管理應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1f504-316">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="1f504-317">如果您看到網頁瀏覽器停滯在「授權中...」，請執行下列其中一個動作：清除 [封鎖第三方 Cookie 和網站資料] 核取方塊，或建立 **login.microsoftonline.com** 的例外狀況，然後再試一次開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f504-317">If you see that the web browser is stuck at "Authorizing...", do one of the following: clear the **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>

    ![監視及管理應用程式](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="1f504-319">變更 [開始時間] 和 [結束時間] 以包含您管線的開始 (2017-05-11) 和結束時間 (2017-05-12)，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="1f504-319">Change the **Start time** and **End time** to include start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>       
3. <span data-ttu-id="1f504-320">您會在中間窗格的清單中看到與管線開始和結束時間之間的每小時相關聯的**活動時段**。</span><span class="sxs-lookup"><span data-stu-id="1f504-320">You see the **activity windows** associated with each hour between pipeline start and end times in the list in the middle pane.</span></span> 
4. <span data-ttu-id="1f504-321">若要查看活動時段的詳細資訊，請選取 [活動時段] 清單中的活動時段。</span><span class="sxs-lookup"><span data-stu-id="1f504-321">To see details about an activity window, select the activity window in the **Activity Windows** list.</span></span> 
    <span data-ttu-id="1f504-322">![活動時段詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="1f504-322">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="1f504-323">在右邊的 [活動時段總管] 中，您會看到截至目前 UTC 時間 (下午 8:12) 為止的所有配量都已處理 (綠色)。</span><span class="sxs-lookup"><span data-stu-id="1f504-323">In Activity Window Explorer on the right, you see that the slices up to the current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="1f504-324">尚未處理 8-9 PM、9-10 PM、10-11 PM、11 PM-12 AM 配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-324">The 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="1f504-325">右窗格中的 [嘗試] 區段會提供資料配量的活動執行相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1f504-325">The **Attempts** section in the right pane provides information about the activity run for the data slice.</span></span> <span data-ttu-id="1f504-326">如果發生錯誤，它會提供有關錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1f504-326">If there was an error, it provides details about the error.</span></span> <span data-ttu-id="1f504-327">例如，如果輸入資料夾或容器不存在，而且配量處理失敗，您看到錯誤訊息，說明容器或資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="1f504-327">For example, if the input folder or container does not exist and the slice processing fails, you see an error message stating that the container or folder does not exist.</span></span>

    ![活動執行嘗試](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="1f504-329">啟動 **SQL Server Management Studio**，並連接到 Azure SQL Database，然後確認資料列已插入資料庫的 **emp** 資料表中。</span><span class="sxs-lookup"><span data-stu-id="1f504-329">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="1f504-331">如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="1f504-331">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="1f504-332">使用圖表檢視監視管線</span><span class="sxs-lookup"><span data-stu-id="1f504-332">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="1f504-333">您也可以使用 [圖表] 檢視來監視資料管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-333">You can also monitor data pipelines by using the diagram view.</span></span>  

1. <span data-ttu-id="1f504-334">在 [Data Factory] 刀鋒視窗中，按一下 [圖表]。</span><span class="sxs-lookup"><span data-stu-id="1f504-334">In the **Data Factory** blade, click **Diagram**.</span></span>
   
    ![Data Factory 刀鋒視窗：圖表磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="1f504-336">您應該會看到如下圖所示的圖表：</span><span class="sxs-lookup"><span data-stu-id="1f504-336">You should see the diagram similar to the following image:</span></span> 
   
    ![圖表檢視](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="1f504-338">在 [圖表] 檢視中，按兩下 **InputDataset** 以查看資料集的配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-338">In the diagram view, double-click **InputDataset** to see slices for the dataset.</span></span>  
   
    ![已選取 InputDataset 的資料集](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="1f504-340">按一下 [更多資訊] 連結來查看所有資料配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-340">Click **See more** link to see all the data slices.</span></span> <span data-ttu-id="1f504-341">您會看到管線開始和結束時間之間的 24 個每小時配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-341">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![所有輸入資料配量](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="1f504-343">請注意，截至目前 UTC 時間為止的所有資料配量都已 [就緒]，因為 **emp.txt** 檔案一直都存在於 Blob 容器中：**adftutorial\input**。</span><span class="sxs-lookup"><span data-stu-id="1f504-343">Notice that all the data slices up to the current UTC time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span></span> <span data-ttu-id="1f504-344">未來時間的配量還不是就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="1f504-344">The slices for the future times are not in ready state yet.</span></span> <span data-ttu-id="1f504-345">確認下方的 [最近失敗的配量]  區段中沒有任何配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-345">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span></span>
6. <span data-ttu-id="1f504-346">關閉刀鋒視窗，直到您看到 [圖表] 檢視 (或) 向左捲動來查看 [圖表] 檢視。</span><span class="sxs-lookup"><span data-stu-id="1f504-346">Close the blades until you see the diagram view (or) scroll left to see the diagram view.</span></span> <span data-ttu-id="1f504-347">然後，按兩下 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="1f504-347">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="1f504-348">按一下 **OutputDataset** 的 [資料表] 刀鋒視窗上的 [更多資訊] 連結，以查看所有配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-348">Click **See more** link on the **Table** blade for **OutputDataset** to see all the slices.</span></span>

    ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="1f504-350">請注意，截至目前 UTC 時間為止的所有配量都會從 [暫止執行] 狀態 => [進行中] ==> [就緒] 狀態移動。</span><span class="sxs-lookup"><span data-stu-id="1f504-350">Notice that all the slices up to the current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="1f504-351">過去 (目前時間之前) 的配量預設會從最新到最舊的順序處理。</span><span class="sxs-lookup"><span data-stu-id="1f504-351">The slices from the past (before current time) are processed from latest to oldest by default.</span></span> <span data-ttu-id="1f504-352">比方說，如果目前時間為 8:12 PM UTC，則會在 6 PM - 7 PM 配量之前處理 7 PM - 8 PM 配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-352">For example, if the current time is 8:12 PM UTC, the slice for 7 PM - 8 PM is processed ahead of the 6 PM - 7 PM slice.</span></span> <span data-ttu-id="1f504-353">8 PM - 9 PM 配量預設會在時間間隔結束時 (也就是 9 PM 之後) 處理。</span><span class="sxs-lookup"><span data-stu-id="1f504-353">The 8 PM - 9 PM slice is processed at the end of the time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="1f504-354">按一下清單中的任何資料配量，您應該會看到 [資料配量]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1f504-354">Click any data slice from the list and you should see the **Data slice** blade.</span></span> <span data-ttu-id="1f504-355">與活動時段相關聯的資料稱為配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-355">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="1f504-356">配量可以是一或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="1f504-356">A slice can be one file or multiple files.</span></span>  
    
     ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="1f504-358">若配量不是處於 [就緒] 狀態，您可以在 [未就緒的上游配量] 清單中看到未就緒且阻礙目前配量執行的上游配量。</span><span class="sxs-lookup"><span data-stu-id="1f504-358">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="1f504-359">在 [資料配量]  刀鋒視窗中，您應該會看到底部清單中的所有活動執行。</span><span class="sxs-lookup"><span data-stu-id="1f504-359">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span></span> <span data-ttu-id="1f504-360">按一下 [活動執行] 查看 [活動執行詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1f504-360">Click an **activity run** to see the **Activity run details** blade.</span></span> 
    
    ![活動執行詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="1f504-362">在此刀鋒視窗中，您會看到複製作業花費多少時間、輸送量為何、已讀取和寫入多少個位元組的資料、執行開始時間、執行結束時間等。</span><span class="sxs-lookup"><span data-stu-id="1f504-362">In this blade, you see how long the copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="1f504-363">按一下 **X** 關閉所有刀鋒視窗，直到您回到 **ADFTutorialDataFactory** 的起始刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1f504-363">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="1f504-364">(選擇性) 按一下 [資料集] 圖格或 [管線] 圖格，以取得您在上述步驟所見的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1f504-364">(optional) click the **Datasets** tile or **Pipelines** tile to get the blades you have seen the preceding steps.</span></span> 
14. <span data-ttu-id="1f504-365">啟動 **SQL Server Management Studio**，並連接到 Azure SQL Database，然後確認資料列已插入資料庫的 **emp** 資料表中。</span><span class="sxs-lookup"><span data-stu-id="1f504-365">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="1f504-367">摘要</span><span class="sxs-lookup"><span data-stu-id="1f504-367">Summary</span></span>
<span data-ttu-id="1f504-368">在本教學課程中，您已建立要將資料從 Azure Blob 複製到 Azure SQL 資料庫的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="1f504-368">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="1f504-369">您已使用 Azure 入口網站建立 Data Factory、連結服務、資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="1f504-369">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="1f504-370">以下是您在本教學課程中執行的高階步驟：</span><span class="sxs-lookup"><span data-stu-id="1f504-370">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="1f504-371">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="1f504-371">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="1f504-372">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="1f504-372">Created **linked services**:</span></span>
   1. <span data-ttu-id="1f504-373">**Azure 儲存體** 連結服務可連結保留輸入資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1f504-373">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="1f504-374">**Azure SQL** 連結服務可連結保留輸出資料的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="1f504-374">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="1f504-375">建立可描述管線輸入資料和輸出資料的 **資料集** 。</span><span class="sxs-lookup"><span data-stu-id="1f504-375">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="1f504-376">建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="1f504-376">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1f504-377">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f504-377">Next steps</span></span>
<span data-ttu-id="1f504-378">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="1f504-378">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="1f504-379">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="1f504-379">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="1f504-380">若要深入了解如何從資料存放區雙向複製資料，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="1f504-380">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>