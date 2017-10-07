---
title: "教學課程： 建立 Azure Data Factory 管線 toocopy 資料 （Azure 入口網站） |Microsoft 文件"
description: "在本教學課程中，您可以使用 Azure 入口網站 toocreate Azure Data Factory 管線複製活動 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。"
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
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="12a1e-103">教學課程： 使用 Azure 入口網站 toocreate Data Factory 管線 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="12a1e-103">Tutorial: Use Azure portal toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12a1e-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="12a1e-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="12a1e-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="12a1e-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="12a1e-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="12a1e-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="12a1e-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12a1e-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="12a1e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12a1e-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="12a1e-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="12a1e-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="12a1e-110">REST API</span><span class="sxs-lookup"><span data-stu-id="12a1e-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="12a1e-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="12a1e-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="12a1e-112">在本文中，您將學習如何 toouse [Azure 入口網站](https://portal.azure.com)toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="12a1e-112">In this article, you learn how toouse [Azure portal](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="12a1e-113">如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="12a1e-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="12a1e-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="12a1e-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="12a1e-115">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="12a1e-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="12a1e-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="12a1e-117">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="12a1e-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="12a1e-118">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="12a1e-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="12a1e-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="12a1e-120">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="12a1e-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="12a1e-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="12a1e-122">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="12a1e-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="12a1e-123">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12a1e-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="12a1e-124">Prerequisites</span></span>
<span data-ttu-id="12a1e-125">完成 hello 中所列必要條件[教學課程必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="12a1e-125">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="12a1e-126">步驟</span><span class="sxs-lookup"><span data-stu-id="12a1e-126">Steps</span></span>
<span data-ttu-id="12a1e-127">以下是您執行本教學課程的一部分的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="12a1e-127">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="12a1e-128">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-128">Create an Azure **data factory**.</span></span> <span data-ttu-id="12a1e-129">在此步驟中，您會建立名為 ADFTutorialDataFactory 的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="12a1e-129">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="12a1e-130">建立**連結的服務**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-130">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="12a1e-131">在此步驟中，您會建立兩種連結服務：Azure 儲存體和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="12a1e-131">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="12a1e-132">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-132">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="12a1e-133">您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-133">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="12a1e-134">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-134">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="12a1e-135">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-135">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="12a1e-136">您在此資料庫中建立了 SQL 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="12a1e-136">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="12a1e-137">建立輸入和輸出**資料集**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-137">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="12a1e-138">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="12a1e-138">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="12a1e-139">此外，hello 輸入的 blob 資料集會指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="12a1e-139">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="12a1e-140">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="12a1e-140">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="12a1e-141">此外，hello 輸出 SQL 資料表的資料集指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="12a1e-141">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="12a1e-142">建立**管線**hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-142">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="12a1e-143">在此步驟中，您會建立具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-143">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="12a1e-144">hello 複製活動會將資料從 hello Azure SQL database 中 hello Azure blob 儲存體 tooa 資料表中的 blob。</span><span class="sxs-lookup"><span data-stu-id="12a1e-144">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="12a1e-145">您可以從任何支援的來源支援 tooany 目的地管線 toocopy 資料中使用複製活動。</span><span class="sxs-lookup"><span data-stu-id="12a1e-145">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="12a1e-146">如需支援的資料存放區清單，請參閱[資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-146">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="12a1e-147">監視 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-147">Monitor hello pipeline.</span></span> <span data-ttu-id="12a1e-148">在此步驟中，您**監視器**hello 的輸入和輸出資料集配量，使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="12a1e-148">In this step, you **monitor** hello slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="12a1e-149">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="12a1e-149">Create data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12a1e-150">完成[hello 教學課程的必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如果您還沒有。</span><span class="sxs-lookup"><span data-stu-id="12a1e-150">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="12a1e-151">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-151">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="12a1e-152">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="12a1e-152">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="12a1e-153">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="12a1e-153">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="12a1e-154">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-154">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="12a1e-155">登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，按一下 **新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-155">After logging in toohello [Azure portal](https://portal.azure.com/), click **New** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![新增->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="12a1e-157">在 hello**新的 data factory**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="12a1e-157">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="12a1e-158">輸入**ADFTutorialDataFactory** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-158">Enter **ADFTutorialDataFactory** for hello **name**.</span></span> 
      
         ![新增 Data Factory 刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="12a1e-160">hello hello Azure data factory 的名稱必須是**全域唯一**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-160">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="12a1e-161">如果您收到下列錯誤 hello，變更 hello 名稱 hello 資料處理站 (例如，yournameADFTutorialDataFactory)，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="12a1e-161">If you receive hello following error, change hello name of hello data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="12a1e-162">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="12a1e-162">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="12a1e-164">選取您的 Azure**訂用帳戶**想 toocreate hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-164">Select your Azure **subscription** in which you want toocreate hello data factory.</span></span> 
   3. <span data-ttu-id="12a1e-165">Hello**資源群組**，執行下列步驟的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="12a1e-165">For hello **Resource Group**, do one of hello following steps:</span></span>
      
      - <span data-ttu-id="12a1e-166">選取**使用現有**，並從 hello 下拉式清單中選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="12a1e-166">Select **Use existing**, and select an existing resource group from hello drop-down list.</span></span> 
      - <span data-ttu-id="12a1e-167">選取**建立新**，然後輸入 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="12a1e-167">Select **Create new**, and enter hello name of a resource group.</span></span>   
         
          <span data-ttu-id="12a1e-168">部分 hello 步驟在本教學課程假設您使用 hello 名稱： **ADFTutorialResourceGroup** hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="12a1e-168">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="12a1e-169">toolearn 解資源群組，請參閱[資源使用您的 Azure 資源群組 toomanage](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-169">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="12a1e-170">選取 hello**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-170">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="12a1e-171">Hello 下拉式清單中會顯示 hello Data Factory 服務所支援的區域。</span><span class="sxs-lookup"><span data-stu-id="12a1e-171">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   5. <span data-ttu-id="12a1e-172">選取**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-172">Select **Pin toodashboard**.</span></span>     
   6. <span data-ttu-id="12a1e-173">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="12a1e-173">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="12a1e-174">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="12a1e-174">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
      > 
      > <span data-ttu-id="12a1e-175">可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="12a1e-175">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>                
      > 
      > 
3. <span data-ttu-id="12a1e-176">在 hello 儀表板，您會看到狀態磚的 hello 下列：**部署資料處理站**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-176">On hello dashboard, you see hello following tile with status: **Deploying data factory**.</span></span> 

    ![部署資料處理站圖格](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="12a1e-178">Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 影像所示。</span><span class="sxs-lookup"><span data-stu-id="12a1e-178">After hello creation is complete, you see hello **Data Factory** blade as shown in hello image.</span></span>
   
   ![Data Factory 首頁](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="12a1e-180">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="12a1e-180">Create linked services</span></span>
<span data-ttu-id="12a1e-181">您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-181">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="12a1e-182">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="12a1e-182">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="12a1e-183">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-183">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="12a1e-184">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="12a1e-184">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="12a1e-185">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-185">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="12a1e-186">這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-186">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="12a1e-187">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-187">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="12a1e-188">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-188">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="12a1e-189">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-189">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="12a1e-190">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="12a1e-190">Create Azure Storage linked service</span></span>
<span data-ttu-id="12a1e-191">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-191">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="12a1e-192">您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="12a1e-192">You specify hello name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="12a1e-193">在 hello **Data Factory**刀鋒視窗中，按一下 **作者及部署**磚。</span><span class="sxs-lookup"><span data-stu-id="12a1e-193">In hello **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![[製作和部署] 磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="12a1e-195">您會看到 hello **Data Factory 編輯器**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="12a1e-195">You see hello **Data Factory Editor** as shown in hello following image:</span></span> 

    ![Data Factory 編輯器](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="12a1e-197">在 hello 編輯器中，按一下 **新建資料存放區**hello 工具列，然後選取按鈕**Azure 儲存體**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-197">In hello editor, click **New data store** button on hello toolbar and select **Azure storage** from hello drop-down menu.</span></span> <span data-ttu-id="12a1e-198">您應該會看到 hello hello 右窗格中建立 Azure 儲存體連結服務的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="12a1e-198">You should see hello JSON template for creating an Azure storage linked service in hello right pane.</span></span> 
   
    ![編輯器 [新增資料存放區] 按鈕](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="12a1e-200">取代`<accountname>`和`<accountkey>`與 hello 帳戶名稱和帳戶金鑰值為您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12a1e-200">Replace `<accountname>` and `<accountkey>` with hello account name and account key values for your Azure storage account.</span></span> 
   
    ![編輯器 Blob 儲存體 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="12a1e-202">按一下**部署**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="12a1e-202">Click **Deploy** on hello toolbar.</span></span> <span data-ttu-id="12a1e-203">您應該會看到部署的 hello **AzureStorageLinkedService**現在在 hello 樹狀目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="12a1e-203">You should see hello deployed **AzureStorageLinkedService** in hello tree view now.</span></span> 
   
    ![編輯器 Blob 儲存體部署](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="12a1e-205">如需在連結的 hello 服務定義中的 JSON 屬性的詳細資訊，請參閱[Azure Blob 儲存體連接器](data-factory-azure-blob-connector.md#linked-service-properties)發行項。</span><span class="sxs-lookup"><span data-stu-id="12a1e-205">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a><span data-ttu-id="12a1e-206">建立連結的服務的 hello Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="12a1e-206">Create a linked service for hello Azure SQL Database</span></span>
<span data-ttu-id="12a1e-207">在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-207">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="12a1e-208">您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="12a1e-208">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="12a1e-209">在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**hello 工具列，然後選取按鈕**Azure SQL Database**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-209">In hello **Data Factory Editor**, click **New data store** button on hello toolbar and select **Azure SQL Database** from hello drop-down menu.</span></span> <span data-ttu-id="12a1e-210">您應該會看到 hello JSON 範本，用於建立 hello 右窗格中的 hello Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="12a1e-210">You should see hello JSON template for creating hello Azure SQL linked service in hello right pane.</span></span>
2. <span data-ttu-id="12a1e-211">以您的 Azure SQL Server 名稱、資料庫名稱、使用者帳戶名稱和密碼取代 `<servername>`、`<databasename>`、`<username>@<servername>` 和 `<password>`。</span><span class="sxs-lookup"><span data-stu-id="12a1e-211">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="12a1e-212">按一下**部署**hello 工具列 toocreate 且部署 hello **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-212">Click **Deploy** on hello toolbar toocreate and deploy hello **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="12a1e-213">確認您看到**AzureSqlLinkedService** hello 下的樹狀結構檢視中**連結的服務**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-213">Confirm that you see **AzureSqlLinkedService** in hello tree view under **Linked services**.</span></span>  

    <span data-ttu-id="12a1e-214">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-214">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="12a1e-215">建立資料集</span><span class="sxs-lookup"><span data-stu-id="12a1e-215">Create datasets</span></span>
<span data-ttu-id="12a1e-216">在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-216">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="12a1e-217">在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="12a1e-217">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="12a1e-218">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="12a1e-218">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="12a1e-219">此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="12a1e-219">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="12a1e-220">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="12a1e-220">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="12a1e-221">此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。</span><span class="sxs-lookup"><span data-stu-id="12a1e-221">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="12a1e-222">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="12a1e-222">Create input dataset</span></span>
<span data-ttu-id="12a1e-223">在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-223">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="12a1e-224">如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="12a1e-224">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="12a1e-225">在本教學課程中，您可以指定 hello 檔案名稱的值。</span><span class="sxs-lookup"><span data-stu-id="12a1e-225">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="12a1e-226">在 hello**編輯器**hello Data Factory 中，按一下  **...多個**，按一下**新的資料集**，然後按一下**Azure Blob 儲存體**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-226">In hello **Editor** for hello Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from hello drop-down menu.</span></span> 
   
    ![新增資料集功能表](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="12a1e-228">以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON:</span><span class="sxs-lookup"><span data-stu-id="12a1e-228">Replace JSON in hello right pane with hello following JSON snippet:</span></span> 
   
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

    <span data-ttu-id="12a1e-229">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="12a1e-229">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="12a1e-230">屬性</span><span class="sxs-lookup"><span data-stu-id="12a1e-230">Property</span></span> | <span data-ttu-id="12a1e-231">說明</span><span class="sxs-lookup"><span data-stu-id="12a1e-231">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="12a1e-232">類型</span><span class="sxs-lookup"><span data-stu-id="12a1e-232">type</span></span> | <span data-ttu-id="12a1e-233">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-233">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="12a1e-234">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="12a1e-234">linkedServiceName</span></span> | <span data-ttu-id="12a1e-235">是指 toohello **AzureStorageLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="12a1e-235">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="12a1e-236">folderPath</span><span class="sxs-lookup"><span data-stu-id="12a1e-236">folderPath</span></span> | <span data-ttu-id="12a1e-237">指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。</span><span class="sxs-lookup"><span data-stu-id="12a1e-237">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="12a1e-238">在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="12a1e-238">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="12a1e-239">fileName</span><span class="sxs-lookup"><span data-stu-id="12a1e-239">fileName</span></span> | <span data-ttu-id="12a1e-240">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="12a1e-240">This property is optional.</span></span> <span data-ttu-id="12a1e-241">如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="12a1e-241">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="12a1e-242">在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。</span><span class="sxs-lookup"><span data-stu-id="12a1e-242">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="12a1e-243">format -> type</span><span class="sxs-lookup"><span data-stu-id="12a1e-243">format -> type</span></span> |<span data-ttu-id="12a1e-244">hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-244">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="12a1e-245">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="12a1e-245">columnDelimiter</span></span> | <span data-ttu-id="12a1e-246">hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-246">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="12a1e-247">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="12a1e-247">frequency/interval</span></span> | <span data-ttu-id="12a1e-248">hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-248">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="12a1e-249">換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。</span><span class="sxs-lookup"><span data-stu-id="12a1e-249">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="12a1e-250">它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。</span><span class="sxs-lookup"><span data-stu-id="12a1e-250">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="12a1e-251">external</span><span class="sxs-lookup"><span data-stu-id="12a1e-251">external</span></span> | <span data-ttu-id="12a1e-252">這個屬性設定太**true**如果 hello 資料不會產生此管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-252">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="12a1e-253">在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。</span><span class="sxs-lookup"><span data-stu-id="12a1e-253">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="12a1e-254">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-254">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="12a1e-255">按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**資料集。</span><span class="sxs-lookup"><span data-stu-id="12a1e-255">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** dataset.</span></span> <span data-ttu-id="12a1e-256">確認您看到 hello **InputDataset** hello 樹狀檢視中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-256">Confirm that you see hello **InputDataset** in hello tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="12a1e-257">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="12a1e-257">Create output dataset</span></span>
<span data-ttu-id="12a1e-258">hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="12a1e-258">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="12a1e-259">hello 輸出 SQL 資料表的資料集 (OututDataset) 您在此步驟中建立指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="12a1e-259">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="12a1e-260">在 hello**編輯器**hello Data Factory 中，按一下  **...多個**，按一下**新的資料集**，然後按一下**Azure SQL**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-260">In hello **Editor** for hello Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from hello drop-down menu.</span></span> 
2. <span data-ttu-id="12a1e-261">以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON:</span><span class="sxs-lookup"><span data-stu-id="12a1e-261">Replace JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="12a1e-262">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="12a1e-262">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="12a1e-263">屬性</span><span class="sxs-lookup"><span data-stu-id="12a1e-263">Property</span></span> | <span data-ttu-id="12a1e-264">說明</span><span class="sxs-lookup"><span data-stu-id="12a1e-264">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="12a1e-265">類型</span><span class="sxs-lookup"><span data-stu-id="12a1e-265">type</span></span> | <span data-ttu-id="12a1e-266">hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="12a1e-266">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="12a1e-267">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="12a1e-267">linkedServiceName</span></span> | <span data-ttu-id="12a1e-268">是指 toohello **AzureSqlLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="12a1e-268">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="12a1e-269">tableName</span><span class="sxs-lookup"><span data-stu-id="12a1e-269">tableName</span></span> | <span data-ttu-id="12a1e-270">指定的 hello**資料表**toowhich hello 資料複製。</span><span class="sxs-lookup"><span data-stu-id="12a1e-270">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="12a1e-271">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="12a1e-271">frequency/interval</span></span> | <span data-ttu-id="12a1e-272">hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。</span><span class="sxs-lookup"><span data-stu-id="12a1e-272">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="12a1e-273">有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-273">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="12a1e-274">識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。</span><span class="sxs-lookup"><span data-stu-id="12a1e-274">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="12a1e-275">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-275">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="12a1e-276">按一下**部署**hello 工具列 toocreate 且部署 hello **OutputDataset**資料集。</span><span class="sxs-lookup"><span data-stu-id="12a1e-276">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset** dataset.</span></span> <span data-ttu-id="12a1e-277">確認您看到 hello **OutputDataset** hello 下的樹狀結構檢視中**資料集**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-277">Confirm that you see hello **OutputDataset** in hello tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="12a1e-278">建立管線</span><span class="sxs-lookup"><span data-stu-id="12a1e-278">Create pipeline</span></span>
<span data-ttu-id="12a1e-279">在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-279">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="12a1e-280">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="12a1e-280">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="12a1e-281">在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。</span><span class="sxs-lookup"><span data-stu-id="12a1e-281">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="12a1e-282">hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="12a1e-282">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="12a1e-283">因此，hello 管線所產生的輸出資料集的 24 配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-283">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="12a1e-284">在 hello**編輯器**hello Data Factory 中，按一下  **...更多** 和 新增管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-284">In hello **Editor** for hello Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="12a1e-285">或者，您可以以滑鼠右鍵按一下**管線**hello 樹狀檢視中按一下**新管線**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-285">Alternatively, you can right-click **Pipelines** in hello tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="12a1e-286">以 hello 下列 JSON 片段取代 hello 右窗格中的 JSON:</span><span class="sxs-lookup"><span data-stu-id="12a1e-286">Replace JSON in hello right pane with hello following JSON snippet:</span></span> 

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
    
    <span data-ttu-id="12a1e-287">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="12a1e-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="12a1e-288">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="12a1e-289">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="12a1e-290">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="12a1e-291">輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="12a1e-292">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="12a1e-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="12a1e-293">支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="12a1e-294">toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="12a1e-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>
    - <span data-ttu-id="12a1e-295">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-295">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="12a1e-296">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="12a1e-296">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="12a1e-297">hello**結束**時間是選擇性的但我們在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="12a1e-297">hello **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="12a1e-298">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。</span><span class="sxs-lookup"><span data-stu-id="12a1e-298">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="12a1e-299">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="12a1e-299">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="12a1e-300">在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="12a1e-300">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="12a1e-301">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-301">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="12a1e-302">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-302">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="12a1e-303">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-303">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="12a1e-304">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="12a1e-304">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="12a1e-305">按一下**部署**hello 工具列 toocreate 且部署 hello **ADFTutorialPipeline**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-305">Click **Deploy** on hello toolbar toocreate and deploy hello **ADFTutorialPipeline**.</span></span> <span data-ttu-id="12a1e-306">確認您看到 hello 樹狀檢視中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-306">Confirm that you see hello pipeline in hello tree view.</span></span> 
4. <span data-ttu-id="12a1e-307">現在，關閉 hello**編輯器**刀鋒視窗中的按一下**X**。按一下**X**再次 toosee hello **Data Factory** hello 首頁**ADFTutorialDataFactory**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-307">Now, close hello **Editor** blade by clicking **X**. Click **X** again toosee hello **Data Factory** home page for hello **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="12a1e-308">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="12a1e-308">**Congratulations!**</span></span> <span data-ttu-id="12a1e-309">您已成功建立管線 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="12a1e-309">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="12a1e-310">監視管線</span><span class="sxs-lookup"><span data-stu-id="12a1e-310">Monitor pipeline</span></span>
<span data-ttu-id="12a1e-311">在此步驟中，您可以使用 hello Azure 入口網站的 toomonitor Azure data factory 中運作。</span><span class="sxs-lookup"><span data-stu-id="12a1e-311">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="12a1e-312">使用監視及管理應用程式來監視管線</span><span class="sxs-lookup"><span data-stu-id="12a1e-312">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="12a1e-313">hello 下列步驟說明在您的 data factory toomonitor 管線 hello 監視和管理應用程式的使用方式：</span><span class="sxs-lookup"><span data-stu-id="12a1e-313">hello following steps show you how toomonitor pipelines in your data factory by using hello Monitor & Manage application:</span></span> 

1. <span data-ttu-id="12a1e-314">按一下**監視和管理**在您的 data factory 的 hello 首頁上並排顯示。</span><span class="sxs-lookup"><span data-stu-id="12a1e-314">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>
   
    ![監視及管理圖格](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="12a1e-316">您應該會在個別的索引標籤中看到 [監視及管理應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12a1e-316">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="12a1e-317">如果您看到該 hello 網頁瀏覽器卡在 [授權]，執行 hello 下列其中一種： 清除 hello**封鎖第三方 cookie 和站台資料**核取方塊 （或） 建立的例外狀況**login.microsoftonline.com**，然後再試一次 tooopen hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12a1e-317">If you see that hello web browser is stuck at "Authorizing...", do one of hello following: clear hello **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>

    ![監視及管理應用程式](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="12a1e-319">變更 hello**開始時間**和**結束時間**tooinclude 開始 (2017年-05-11)，並結束時間 (2017年-05-12) 您的管線，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-319">Change hello **Start time** and **End time** tooinclude start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>     
3. <span data-ttu-id="12a1e-320">您會看到 hello**活動 windows**聯管線開始和結束之間的每小時 hello 中間窗格中的 hello 清單中的時間。</span><span class="sxs-lookup"><span data-stu-id="12a1e-320">You see hello **activity windows** associated with each hour between pipeline start and end times in hello list in hello middle pane.</span></span> 
4. <span data-ttu-id="12a1e-321">toosee 詳細活動視窗選取 hello hello 中的活動視窗**活動 Windows**清單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-321">toosee details about an activity window, select hello activity window in hello **Activity Windows** list.</span></span> 
    <span data-ttu-id="12a1e-322">![活動時段詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="12a1e-322">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="12a1e-323">在活動 Windows 檔案總管 右邊的 hello 上，您會看到該 hello 配量執行 toohello 目前 UTC 時間 （下午 8:12） 會處理 （以綠色）。</span><span class="sxs-lookup"><span data-stu-id="12a1e-323">In Activity Window Explorer on hello right, you see that hello slices up toohello current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="12a1e-324">hello 8-9 PM，9-10 PM、 10 11 PM，晚上 11 點-12 AM 配量不會尚未處理。</span><span class="sxs-lookup"><span data-stu-id="12a1e-324">hello 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="12a1e-325">hello**嘗試**hello 右窗格會提供執行 hello 資料配量的 hello 活動的相關資訊 > 一節。</span><span class="sxs-lookup"><span data-stu-id="12a1e-325">hello **Attempts** section in hello right pane provides information about hello activity run for hello data slice.</span></span> <span data-ttu-id="12a1e-326">如果發生錯誤，它會提供 hello 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="12a1e-326">If there was an error, it provides details about hello error.</span></span> <span data-ttu-id="12a1e-327">例如，如果 hello 輸入資料夾或容器不存在，hello 配量處理失敗，您會看到錯誤訊息，說明該 hello 容器或資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="12a1e-327">For example, if hello input folder or container does not exist and hello slice processing fails, you see an error message stating that hello container or folder does not exist.</span></span>

    ![活動執行嘗試](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="12a1e-329">啟動**SQL Server Management Studio**、 連接 toohello Azure SQL Database，並確認 hello 資料列會插入在 toohello **emp** hello 資料庫資料表中的。</span><span class="sxs-lookup"><span data-stu-id="12a1e-329">Launch **SQL Server Management Studio**, connect toohello Azure SQL Database, and verify that hello rows are inserted in toohello **emp** table in hello database.</span></span>
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="12a1e-331">如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="12a1e-331">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="12a1e-332">使用圖表檢視監視管線</span><span class="sxs-lookup"><span data-stu-id="12a1e-332">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="12a1e-333">您也可以使用 hello 圖表檢視監視資料管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-333">You can also monitor data pipelines by using hello diagram view.</span></span>  

1. <span data-ttu-id="12a1e-334">在 hello **Data Factory**刀鋒視窗中，按一下 **圖表**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-334">In hello **Data Factory** blade, click **Diagram**.</span></span>
   
    ![Data Factory 刀鋒視窗：圖表磚](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="12a1e-336">您應該會看到 hello 圖表類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="12a1e-336">You should see hello diagram similar toohello following image:</span></span> 
   
    ![圖表檢視](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="12a1e-338">在 [hello] 圖表檢視中，按兩下**InputDataset** toosee hello 資料集配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-338">In hello diagram view, double-click **InputDataset** toosee slices for hello dataset.</span></span>  
   
    ![已選取 InputDataset 的資料集](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="12a1e-340">按一下**看到更多**連結 toosee 所有 hello 資料配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-340">Click **See more** link toosee all hello data slices.</span></span> <span data-ttu-id="12a1e-341">您會看到管線開始和結束時間之間的 24 個每小時配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-341">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![所有輸入資料配量](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="12a1e-343">請注意，所有 hello toohello 目前 UTC 時間的資料配量是**準備**因為 hello **emp.txt**檔案存在 hello world hello blob 容器中： **adftutorial\input**.</span><span class="sxs-lookup"><span data-stu-id="12a1e-343">Notice that all hello data slices up toohello current UTC time are **Ready** because hello **emp.txt** file exists all hello time in hello blob container: **adftutorial\input**.</span></span> <span data-ttu-id="12a1e-344">hello 配量的 hello 未來時間還未處於就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="12a1e-344">hello slices for hello future times are not in ready state yet.</span></span> <span data-ttu-id="12a1e-345">確認任何扇區顯示在 hello**最近失敗配量**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="12a1e-345">Confirm that no slices show up in hello **Recently failed slices** section at hello bottom.</span></span>
6. <span data-ttu-id="12a1e-346">Hello 檢視 （或） 捲動左的 toosee hello 圖表檢視，請參閱 < 直到您關閉 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="12a1e-346">Close hello blades until you see hello diagram view (or) scroll left toosee hello diagram view.</span></span> <span data-ttu-id="12a1e-347">然後，按兩下 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-347">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="12a1e-348">按一下**看到更多**hello 上的連結**資料表**刀鋒伺服器**OutputDataset** toosee 所有 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-348">Click **See more** link on hello **Table** blade for **OutputDataset** toosee all hello slices.</span></span>

    ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="12a1e-350">請注意，所有 hello toohello 目前 UTC 時間配量將從移**暫止執行**狀態 = >**正在** ==> **準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="12a1e-350">Notice that all hello slices up toohello current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="12a1e-351">hello 從 hello 過去的配量 （在目前的時間） 之前從最新 toooldest 預設來處理。</span><span class="sxs-lookup"><span data-stu-id="12a1e-351">hello slices from hello past (before current time) are processed from latest toooldest by default.</span></span> <span data-ttu-id="12a1e-352">例如，如果 hello 目前時間是下午 8:12 UTC，hello 處理配量的 7-8 下午前面 hello 6-7 下午配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-352">For example, if hello current time is 8:12 PM UTC, hello slice for 7 PM - 8 PM is processed ahead of hello 6 PM - 7 PM slice.</span></span> <span data-ttu-id="12a1e-353">根據預設，之後 9 PM 結尾 hello hello 時間間隔處理 hello 8-9 下午配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-353">hello 8 PM - 9 PM slice is processed at hello end of hello time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="12a1e-354">按一下 從 hello 清單的任何資料分割，您應該會看見 hello**資料配量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="12a1e-354">Click any data slice from hello list and you should see hello **Data slice** blade.</span></span> <span data-ttu-id="12a1e-355">與活動時段相關聯的資料稱為配量。</span><span class="sxs-lookup"><span data-stu-id="12a1e-355">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="12a1e-356">配量可以是一或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="12a1e-356">A slice can be one file or multiple files.</span></span>  
    
     ![資料配量刀鋒視窗](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="12a1e-358">如果 hello 配量不在 hello**準備**狀態，您可以看到未就緒，並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。</span><span class="sxs-lookup"><span data-stu-id="12a1e-358">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="12a1e-359">在 hello**資料配量**刀鋒視窗中，您應該會看到所有的活動執行 hello hello 底部的清單中。</span><span class="sxs-lookup"><span data-stu-id="12a1e-359">In hello **DATA SLICE** blade, you should see all activity runs in hello list at hello bottom.</span></span> <span data-ttu-id="12a1e-360">按一下**活動執行**toosee hello**活動執行詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="12a1e-360">Click an **activity run** toosee hello **Activity run details** blade.</span></span> 
    
    ![活動執行詳細資料](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="12a1e-362">在這個刀鋒視窗中，您會看到如何花了很長的 hello 複製作業，執行哪些輸送量時，多少個位元組的資料已讀取和寫入，請執行開始時間、 結束時間等。</span><span class="sxs-lookup"><span data-stu-id="12a1e-362">In this blade, you see how long hello copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="12a1e-363">按一下**X** tooclose 所有 hello 刀鋒視窗，直到您都回到 toohello 家用刀鋒視窗中的 hello **ADFTutorialDataFactory**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-363">Click **X** tooclose all hello blades until you get back toohello home blade for hello **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="12a1e-364">（選擇性） 按一下 hello**資料集**磚或**管線**磚 tooget hello 刀鋒視窗，您已經瞭解 hello 前面的步驟。</span><span class="sxs-lookup"><span data-stu-id="12a1e-364">(optional) click hello **Datasets** tile or **Pipelines** tile tooget hello blades you have seen hello preceding steps.</span></span> 
14. <span data-ttu-id="12a1e-365">啟動**SQL Server Management Studio**、 連接 toohello Azure SQL Database，並確認 hello 資料列會插入在 toohello **emp** hello 資料庫資料表中的。</span><span class="sxs-lookup"><span data-stu-id="12a1e-365">Launch **SQL Server Management Studio**, connect toohello Azure SQL Database, and verify that hello rows are inserted in toohello **emp** table in hello database.</span></span>
    
    ![SQL 查詢結果](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="12a1e-367">摘要</span><span class="sxs-lookup"><span data-stu-id="12a1e-367">Summary</span></span>
<span data-ttu-id="12a1e-368">在本教學課程中，您可以建立 Azure data factory toocopy 資料從 Azure blob tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="12a1e-368">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="12a1e-369">您已經使用 hello Azure 入口網站 toocreate hello 資料處理站、 連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="12a1e-369">You used hello Azure portal toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="12a1e-370">以下是您執行本教學課程中的 hello 高階步驟：</span><span class="sxs-lookup"><span data-stu-id="12a1e-370">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="12a1e-371">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="12a1e-371">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="12a1e-372">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="12a1e-372">Created **linked services**:</span></span>
   1. <span data-ttu-id="12a1e-373">**Azure 儲存體**連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12a1e-373">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="12a1e-374">**Azure SQL**連結服務 toolink hello 輸出資料會保存您 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="12a1e-374">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="12a1e-375">建立可描述管線輸入資料和輸出資料的 **資料集** 。</span><span class="sxs-lookup"><span data-stu-id="12a1e-375">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="12a1e-376">建立具有**複製活動**的**管線**，以 **BlobSource** 做為來源並以 **SqlSink** 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="12a1e-376">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="12a1e-377">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12a1e-377">Next steps</span></span>
<span data-ttu-id="12a1e-378">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="12a1e-378">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="12a1e-379">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="12a1e-379">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="12a1e-380">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="12a1e-380">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
