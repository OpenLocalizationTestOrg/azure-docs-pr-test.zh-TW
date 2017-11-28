---
title: "aaaBuild 您第一次的 data factory (Visual Studio) |Microsoft 文件"
description: "在本教學課程中，您會使用 Visual Studio，建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="a9888-103">教學課程：使用 Visual Studio 建立資料處理站</span><span class="sxs-lookup"><span data-stu-id="a9888-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="a9888-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="a9888-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="a9888-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a9888-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="a9888-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9888-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="a9888-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9888-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="a9888-108">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="a9888-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="a9888-109">REST API</span><span class="sxs-lookup"><span data-stu-id="a9888-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="a9888-110">本教學課程示範如何使用 Visual Studio Azure data factory toocreate。</span><span class="sxs-lookup"><span data-stu-id="a9888-110">This tutorial shows you how toocreate an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="a9888-111">您建立使用 hello Data Factory 的專案範本的 Visual Studio 專案、 定義以 JSON 格式的 Data Factory 實體 （連結的服務、 資料集和管線），然後發行/部署這些實體 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="a9888-111">You create a Visual Studio project using hello Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities toohello cloud.</span></span> 

<span data-ttu-id="a9888-112">在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="a9888-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="a9888-113">此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a9888-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="a9888-114">hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。</span><span class="sxs-lookup"><span data-stu-id="a9888-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9888-115">本教學課程不會顯示如何使用 Azure Data Factory 複製資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="a9888-116">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="a9888-117">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="a9888-118">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a9888-119">如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="a9888-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="a9888-120">逐步解說︰建立和發佈 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="a9888-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="a9888-121">以下是您執行此逐步解說中的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="a9888-121">Here are hello steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="a9888-122">建立兩個連結服務：**AzureStorageLinkedService1** 和 **HDInsightOnDemandLinkedService1**。</span><span class="sxs-lookup"><span data-stu-id="a9888-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="a9888-123">在本教學課程中，輸入和輸出資料中的 hello hive 活動 hello 相同的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9888-123">In this tutorial, both input and output data for hello hive activity are in hello same Azure Blob Storage.</span></span> <span data-ttu-id="a9888-124">您使用隨 HDInsight 叢集 tooprocess 現有輸入的資料 tooproduce 輸出的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-124">You use an on-demand HDInsight cluster tooprocess existing input data tooproduce output data.</span></span> <span data-ttu-id="a9888-125">hello 隨選 HDInsight 叢集會自動為您建立 Azure Data factory 在 hello 輸入的資料時處理的準備 toobe 的執行階段。</span><span class="sxs-lookup"><span data-stu-id="a9888-125">hello on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when hello input data is ready toobe processed.</span></span> <span data-ttu-id="a9888-126">您需要的 toolink 儲存您的資料，或計算 tooyour 資料處理站，以便讓 hello Data Factory 服務可以連線 toothem 在執行階段。</span><span class="sxs-lookup"><span data-stu-id="a9888-126">You need toolink your data stores or computes tooyour data factory so that hello Data Factory service can connect toothem at runtime.</span></span> <span data-ttu-id="a9888-127">因此，您會使用 hello AzureStorageLinkedService1，連結您的 Azure 儲存體帳戶 toohello data factory，並且使用 hello HDInsightOnDemandLinkedService1 連結隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-127">Therefore, you link your Azure Storage Account toohello data factory by using hello AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using hello HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="a9888-128">發行時，您可以指定建立 hello 資料 factory toobe hello 名稱或現有的 data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-128">When publishing, you specify hello name for hello data factory toobe created or an existing data factory.</span></span>  
2. <span data-ttu-id="a9888-129">建立兩個資料集： **InputDataset**和**OutputDataset**，代表儲存在 hello Azure blob 儲存體中的 hello 輸入/輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent hello input/output data that is stored in hello Azure blob storage.</span></span> 
   
    <span data-ttu-id="a9888-130">這些資料集定義，請參閱您在 hello 上一個步驟中建立的 toohello Azure 儲存體連結的服務。</span><span class="sxs-lookup"><span data-stu-id="a9888-130">These dataset definitions refer toohello Azure Storage linked service you created in hello previous step.</span></span> <span data-ttu-id="a9888-131">Hello InputDataset，您可以指定 hello blob 容器 (adfgetstarted)，然後 hello 所在的資料夾 (inptutdata) hello 輸入資料的 blob。</span><span class="sxs-lookup"><span data-stu-id="a9888-131">For hello InputDataset, you specify hello blob container (adfgetstarted) and hello folder (inptutdata) that contains a blob with hello input data.</span></span> <span data-ttu-id="a9888-132">Hello OutputDataset，您會指定 hello blob 容器 (adfgetstarted) 和 hello 資料夾 (partitioneddata)，其中保存 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-132">For hello OutputDataset, you specify hello blob container (adfgetstarted) and hello folder (partitioneddata) that holds hello output data.</span></span> <span data-ttu-id="a9888-133">您也會指定其他屬性，例如結構、可用性和原則。</span><span class="sxs-lookup"><span data-stu-id="a9888-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="a9888-134">建立名為 **MyFirstPipeline** 的管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="a9888-135">在本逐步解說，hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="a9888-135">In this walkthrough, hello pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="a9888-136">這個活動轉換輸入資料 tooproduce 輸出資料的隨選 HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a9888-136">This activity transform input data tooproduce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="a9888-137">toolearn hive 活動詳細資料請參閱[Hive 活動](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="a9888-137">toolearn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="a9888-138">建立名為 **DataFactoryUsingVS** 的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="a9888-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="a9888-139">部署 hello data factory 和所有的 Data Factory 實體 （連結的服務、 表格和 hello 管線）。</span><span class="sxs-lookup"><span data-stu-id="a9888-139">Deploy hello data factory and all Data Factory entities (linked services, tables, and hello pipeline).</span></span>
5. <span data-ttu-id="a9888-140">發行之後，您可以使用 Azure 入口網站的刀鋒視窗，並監視和管理 App toomonitor hello 管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-140">After you publish, you use Azure portal blades and Monitoring & Management App toomonitor hello pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="a9888-141">必要條件</span><span class="sxs-lookup"><span data-stu-id="a9888-141">Prerequisites</span></span>
1. <span data-ttu-id="a9888-142">閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="a9888-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span> <span data-ttu-id="a9888-143">您也可以選取 hello**概觀和必要條件**hello 頂端 tooswitch toohello 文 hello 下拉式清單中的選項。</span><span class="sxs-lookup"><span data-stu-id="a9888-143">You can also select hello **Overview and prerequisites** option in hello drop-down list at hello top tooswitch toohello article.</span></span> <span data-ttu-id="a9888-144">完成 hello 必要條件之後，回復 toothis 文章選取切換**Visual Studio** hello 下拉式清單中的選項。</span><span class="sxs-lookup"><span data-stu-id="a9888-144">After you complete hello prerequisites, switch back toothis article by selecting **Visual Studio** option in hello drop-down list.</span></span>
2. <span data-ttu-id="a9888-145">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="a9888-145">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>  
3. <span data-ttu-id="a9888-146">您必須擁有您電腦上安裝的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a9888-146">You must have hello following installed on your computer:</span></span>
   * <span data-ttu-id="a9888-147">Visual Studio 2013 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a9888-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="a9888-148">下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="a9888-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="a9888-149">瀏覽過[Azure 下載頁面](https://azure.microsoft.com/downloads/)按一下**VS 2013**或**VS 2015**在 hello **.NET** > 一節。</span><span class="sxs-lookup"><span data-stu-id="a9888-149">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="a9888-150">下載最新 Azure Data Factory 外掛程式 hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5)或[VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。</span><span class="sxs-lookup"><span data-stu-id="a9888-150">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="a9888-151">您也可以執行下列步驟的 hello 更新 hello 外掛程式： hello 功能表上，按一下**工具** -> **擴充功能和更新** -> **線上** ->  **Visual Studio 組件庫** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **更新**。</span><span class="sxs-lookup"><span data-stu-id="a9888-151">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="a9888-152">現在，我們將使用 Visual Studio toocreate Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-152">Now, let's use Visual Studio toocreate an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="a9888-153">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="a9888-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="a9888-154">啟動 **Visual Studio 2013** 或 **Visual Studio 2015**。</span><span class="sxs-lookup"><span data-stu-id="a9888-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="a9888-155">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="a9888-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="a9888-156">您應該會看見 hello**新專案** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a9888-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="a9888-157">在 hello**新專案**對話方塊中，選取 hello **DataFactory**範本，然後按一下**空白資料處理站專案**。</span><span class="sxs-lookup"><span data-stu-id="a9888-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![[新增專案] 對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="a9888-159">輸入**名稱**hello 專案**位置**，hello 的名稱和**方案**，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a9888-159">Enter a **name** for hello project, **location**, and a name for hello **solution**, and click **OK**.</span></span>

    ![Solution Explorer](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="a9888-161">建立連結服務</span><span class="sxs-lookup"><span data-stu-id="a9888-161">Create linked services</span></span>
<span data-ttu-id="a9888-162">在此步驟中，您會建立兩個連結服務：**Azure 儲存體**和**隨選 HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="a9888-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="a9888-163">hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory 提供 hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="a9888-163">hello Azure Storage linked service links your Azure Storage account toohello data factory by providing hello connection information.</span></span> <span data-ttu-id="a9888-164">資料 Factory 服務會在執行階段使用 hello hello 連結的服務設定 tooconnect toohello Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="a9888-164">Data Factory service uses hello connection string from hello linked service setting tooconnect toohello Azure storage at runtime.</span></span> <span data-ttu-id="a9888-165">這個儲存體保存輸入] 和 [輸出資料 hello 管線和 hello hive hello hive 活動所使用的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-165">This storage holds input and output data for hello pipeline, and hello hive script file used by hello hive activity.</span></span> 

<span data-ttu-id="a9888-166">隨 HDInsight 連結服務，與 hello HDInsight 叢集會自動建立在執行階段準備 tooprocessed hello 輸入的資料時。</span><span class="sxs-lookup"><span data-stu-id="a9888-166">With on-demand HDInsight linked service, hello HDInsight cluster is automatically created at runtime when hello input data is ready tooprocessed.</span></span> <span data-ttu-id="a9888-167">它為了處理和閒置 hello 指定的時間量之後，會刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-167">hello cluster is deleted after it is done processing and idle for hello specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9888-168">您可以指定其名稱和設定發行您的 Data Factory 方案的 hello 次，以建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-168">You create a data factory by specifying its name and settings at hello time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="a9888-169">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="a9888-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="a9888-170">以滑鼠右鍵按一下**連結的服務**hello 方案總管中，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-170">Right-click **Linked Services** in hello solution explorer, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="a9888-171">在 hello**加入新項目**對話方塊中，選取**Azure 儲存體連結服務**從 hello 清單，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-171">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span>
    <span data-ttu-id="a9888-172">![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="a9888-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="a9888-173">取代`<accountname>`和`<accountkey>`與 hello 您 Azure 儲存體帳戶名稱和其索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a9888-173">Replace `<accountname>` and `<accountkey>` with hello name of your Azure storage account and its key.</span></span> <span data-ttu-id="a9888-174">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="a9888-174">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="a9888-175">![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="a9888-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="a9888-176">儲存 hello **AzureStorageLinkedService1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-176">Save hello **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="a9888-177">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="a9888-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="a9888-178">在 hello**方案總管 中**，以滑鼠右鍵按一下**連結的服務**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-178">In hello **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="a9888-179">選取 [HDInsight 隨選連結服務]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a9888-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="a9888-180">取代 hello **JSON**以下列 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="a9888-180">Replace hello **JSON** with hello following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="a9888-181">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="a9888-181">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="a9888-182">屬性</span><span class="sxs-lookup"><span data-stu-id="a9888-182">Property</span></span> | <span data-ttu-id="a9888-183">說明</span><span class="sxs-lookup"><span data-stu-id="a9888-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="a9888-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="a9888-184">ClusterSize</span></span> | <span data-ttu-id="a9888-185">指定 hello hello HDInsight Hadoop 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="a9888-185">Specifies hello size of hello HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="a9888-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="a9888-186">TimeToLive</span></span> | <span data-ttu-id="a9888-187">於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。</span><span class="sxs-lookup"><span data-stu-id="a9888-187">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="a9888-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="a9888-188">linkedServiceName</span></span> | <span data-ttu-id="a9888-189">指定 hello 是所產生的 HDInsight Hadoop 叢集中使用的 toostore hello 記錄檔的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9888-189">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="a9888-190">hello HDInsight 叢集建立**預設容器**hello hello JSON (linkedServiceName) 中所指定的 blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a9888-190">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="a9888-191">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-191">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="a9888-192">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="a9888-192">This behavior is by design.</span></span> <span data-ttu-id="a9888-193">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (timeToLive)，否則每次處理配量時，就會建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="a9888-194">hello 處理完成時，會自動刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-194">hello cluster is automatically deleted when hello processing is done.</span></span>
    > 
    > <span data-ttu-id="a9888-195">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="a9888-196">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="a9888-196">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="a9888-197">這些容器的 hello 名稱遵循模式： `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="a9888-197">hello names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="a9888-198">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9888-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="a9888-199">如需 JSON 屬性的詳細資訊，請參閱[計算已連結的服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)一文。</span><span class="sxs-lookup"><span data-stu-id="a9888-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="a9888-200">儲存 hello **HDInsightOnDemandLinkedService1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-200">Save hello **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="a9888-201">建立資料集</span><span class="sxs-lookup"><span data-stu-id="a9888-201">Create datasets</span></span>
<span data-ttu-id="a9888-202">在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-202">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="a9888-203">這些資料集，請參閱 toohello **AzureStorageLinkedService1**稍早在本教學課程中，您已建立。</span><span class="sxs-lookup"><span data-stu-id="a9888-203">These datasets refer toohello **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="a9888-204">hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-204">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="a9888-205">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="a9888-205">Create input dataset</span></span>
1. <span data-ttu-id="a9888-206">在 hello**方案總管 中**，以滑鼠右鍵按一下**資料表**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-206">In hello **Solution Explorer**, right-click **Tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="a9888-207">選取**Azure Blob** hello 清單中，從變更 hello hello 檔名太**InputDataSet.json**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-207">Select **Azure Blob** from hello list, change hello name of hello file too**InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="a9888-208">取代 hello **JSON** hello 編輯器 hello 下列 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="a9888-208">Replace hello **JSON** in hello editor with hello following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="a9888-209">此 JSON 片段會定義資料集稱為**AzureBlobInput**代表 hello 管線中的 hello hive 活動的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for hello hive activity in hello pipeline.</span></span> <span data-ttu-id="a9888-210">您指定 hello 輸入的資料位於呼叫 hello blob 容器`adfgetstarted`和 hello 資料夾稱為`inputdata`。</span><span class="sxs-lookup"><span data-stu-id="a9888-210">You specify that hello input data is located in hello blob container called `adfgetstarted` and hello folder called `inputdata`.</span></span>

    <span data-ttu-id="a9888-211">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="a9888-211">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="a9888-212">屬性</span><span class="sxs-lookup"><span data-stu-id="a9888-212">Property</span></span> | <span data-ttu-id="a9888-213">說明</span><span class="sxs-lookup"><span data-stu-id="a9888-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="a9888-214">類型</span><span class="sxs-lookup"><span data-stu-id="a9888-214">type</span></span> |<span data-ttu-id="a9888-215">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a9888-215">hello type property is set too**AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="a9888-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="a9888-216">linkedServiceName</span></span> | <span data-ttu-id="a9888-217">是指您稍早建立的 AzureStorageLinkedService1 toohello。</span><span class="sxs-lookup"><span data-stu-id="a9888-217">Refers toohello AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="a9888-218">fileName</span><span class="sxs-lookup"><span data-stu-id="a9888-218">fileName</span></span> |<span data-ttu-id="a9888-219">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="a9888-219">This property is optional.</span></span> <span data-ttu-id="a9888-220">如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-220">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="a9888-221">在此情況下，只有 hello input.log 會進行處理。</span><span class="sxs-lookup"><span data-stu-id="a9888-221">In this case, only hello input.log is processed.</span></span>
    <span data-ttu-id="a9888-222">類型</span><span class="sxs-lookup"><span data-stu-id="a9888-222">type</span></span> | <span data-ttu-id="a9888-223">hello 記錄檔是以文字格式，因此我們使用 TextFormat。</span><span class="sxs-lookup"><span data-stu-id="a9888-223">hello log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="a9888-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="a9888-224">columnDelimiter</span></span> | <span data-ttu-id="a9888-225">hello 記錄檔中的資料行以 hello 逗號字元分隔 (`,`)</span><span class="sxs-lookup"><span data-stu-id="a9888-225">columns in hello log files are delimited by hello comma character (`,`)</span></span>
    <span data-ttu-id="a9888-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="a9888-226">frequency/interval</span></span> | <span data-ttu-id="a9888-227">設定 tooMonth 頻率和間隔為 1，這表示的 hello 輸入配量可使用每個月。</span><span class="sxs-lookup"><span data-stu-id="a9888-227">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span>
    <span data-ttu-id="a9888-228">external</span><span class="sxs-lookup"><span data-stu-id="a9888-228">external</span></span> | <span data-ttu-id="a9888-229">設定此屬性是 tootrue hello hello 活動的輸入的資料不會產生 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-229">This property is set tootrue if hello input data for hello activity is not generated by hello pipeline.</span></span> <span data-ttu-id="a9888-230">此屬性只會指定於輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="a9888-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="a9888-231">Hello hello 第一個活動的輸入資料集，一定會設定它 tootrue。</span><span class="sxs-lookup"><span data-stu-id="a9888-231">For hello input dataset of hello first activity, always set it tootrue.</span></span>
4. <span data-ttu-id="a9888-232">儲存 hello **InputDataset.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-232">Save hello **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="a9888-233">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="a9888-233">Create output dataset</span></span>
<span data-ttu-id="a9888-234">現在，您可以建立 hello 輸出資料集 toorepresent 輸出資料儲存在 hello Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a9888-234">Now, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="a9888-235">在 hello**方案總管 中**，以滑鼠右鍵按一下**資料表**，點太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-235">In hello **Solution Explorer**, right-click **tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="a9888-236">選取**Azure Blob** hello 清單中，從變更 hello hello 檔名太**OutputDataset.json**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-236">Select **Azure Blob** from hello list, change hello name of hello file too**OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="a9888-237">取代 hello **JSON** hello hello 下列 JSON 編輯器：</span><span class="sxs-lookup"><span data-stu-id="a9888-237">Replace hello **JSON** in hello editor with hello following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    <span data-ttu-id="a9888-238">hello JSON 片段會定義資料集稱為**AzureBlobOutput**代表輸出 hello 管線中的 hello hive 活動所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-238">hello JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by hello hive activity in hello pipeline.</span></span> <span data-ttu-id="a9888-239">您指定 hello 輸出 hello hive 活動所產生的資料位於呼叫 hello blob 容器`adfgetstarted`和 hello 資料夾稱為`partitioneddata`。</span><span class="sxs-lookup"><span data-stu-id="a9888-239">You specify that hello output data is produced by hello hive activity is placed in hello blob container called `adfgetstarted` and hello folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="a9888-240">hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。</span><span class="sxs-lookup"><span data-stu-id="a9888-240">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="a9888-241">hello 輸出資料集的磁碟機 hello 排程的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-241">hello output dataset drives hello schedule of hello pipeline.</span></span> <span data-ttu-id="a9888-242">hello 管線會執行每個月之間其開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="a9888-242">hello pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="a9888-243">請參閱**建立 hello 輸入資料集**> 一節，如需這些屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="a9888-243">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="a9888-244">您未 hello 外部屬性上設定輸出資料集為 hello 資料集由 hello 管線所產生。</span><span class="sxs-lookup"><span data-stu-id="a9888-244">You do not set hello external property on an output dataset as hello dataset is produced by hello pipeline.</span></span>
4. <span data-ttu-id="a9888-245">儲存 hello **OutputDataset.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-245">Save hello **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="a9888-246">建立管線</span><span class="sxs-lookup"><span data-stu-id="a9888-246">Create pipeline</span></span>
<span data-ttu-id="a9888-247">您已建立 hello Azure 儲存體連結服務，以及輸入和輸出資料集為止。</span><span class="sxs-lookup"><span data-stu-id="a9888-247">You have created hello Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="a9888-248">現在，建立具有 **HDInsightHive** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="a9888-249">hello**輸入**hello hive 活動會設定太**AzureBlobInput**和**輸出**設定得**AzureBlobOutput**。</span><span class="sxs-lookup"><span data-stu-id="a9888-249">hello **input** for hello hive activity is set too**AzureBlobInput** and **output** is set too**AzureBlobOutput**.</span></span> <span data-ttu-id="a9888-250">每月是可用的輸入資料集配量 (頻率： Month、 interval: 1)，且 hello 輸出配量產生每月太。</span><span class="sxs-lookup"><span data-stu-id="a9888-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and hello output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="a9888-251">在 hello**方案總管 中**，以滑鼠右鍵按一下**管線**，點太**新增**，然後按一下**新項目。**</span><span class="sxs-lookup"><span data-stu-id="a9888-251">In hello **Solution Explorer**, right-click **Pipelines**, point too**Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="a9888-252">選取**Hive 轉換管線**從 hello 清單，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-252">Select **Hive Transformation Pipeline** from hello list, and click **Add**.</span></span>
3. <span data-ttu-id="a9888-253">取代 hello **JSON**以下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="a9888-253">Replace hello **JSON** with hello following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a9888-254">取代`<storageaccountname>`hello 的儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9888-254">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a9888-255">取代`<storageaccountname>`hello 的儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9888-255">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    <span data-ttu-id="a9888-256">hello JSON 片段會定義單一活動 （Hive 活動） 所組成的管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-256">hello JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="a9888-257">此活動視 HDInsight 叢集 tooproduce 輸出資料上執行 Hive 指令碼 tooprocess 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-257">This activity runs a Hive script tooprocess input data on an on-demand HDInsight cluster tooproduce output data.</span></span> <span data-ttu-id="a9888-258">在 hello 活動 區段中的 hello 管線 JSON，您會看到一個 hello 陣列中的活動類型設定太**HDInsightHive**。</span><span class="sxs-lookup"><span data-stu-id="a9888-258">In hello activities section of hello pipeline JSON, you see only one activity in hello array with type set too**HDInsightHive**.</span></span> 

    <span data-ttu-id="a9888-259">在特定 tooHDInsight Hive 活動 hello 類型屬性，您可以指定哪些 Azure 儲存體連結服務有 hello hive 指令碼檔案、 hello 路徑 toohello 指令碼檔和參數 toohello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-259">In hello type properties that are specific tooHDInsight Hive activity, you specify what Azure Storage linked service has hello hive script file, hello path toohello script file, and parameters toohello script file.</span></span> 

    <span data-ttu-id="a9888-260">hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 （由 hello scriptLinkedService 指定），和 hello `script` hello 容器中的資料夾`adfgetstarted`。</span><span class="sxs-lookup"><span data-stu-id="a9888-260">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService), and in hello `script` folder in hello container `adfgetstarted`.</span></span>

    <span data-ttu-id="a9888-261">hello`defines`區段是做為 Hive 組態值傳遞 toohello hive 指令碼使用的 toospecify hello 執行階段設定 (例如`${hiveconf:inputtable}`， `${hiveconf:partitionedtable})`。</span><span class="sxs-lookup"><span data-stu-id="a9888-261">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="a9888-262">hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。</span><span class="sxs-lookup"><span data-stu-id="a9888-262">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span> <span data-ttu-id="a9888-263">您已設定 hello 資料集 toobe 產生每月，因此，一次 （因為 hello 月份是相同的開始和結束日期） hello 管線產生配量。</span><span class="sxs-lookup"><span data-stu-id="a9888-263">You configured hello dataset toobe produced monthly, therefore, only once slice is produced by hello pipeline (because hello month is same in start and end dates).</span></span>

    <span data-ttu-id="a9888-264">在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="a9888-264">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="a9888-265">儲存 hello **HiveActivity1.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="a9888-265">Save hello **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="a9888-266">將 partitionweblogs.hql 新增為相依性</span><span class="sxs-lookup"><span data-stu-id="a9888-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="a9888-267">以滑鼠右鍵按一下**相依性**在 hello**方案總管 中**視窗中，點太**新增**，然後按一下**現有項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-267">Right-click **Dependencies** in hello **Solution Explorer** window, point too**Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="a9888-268">瀏覽 toohello **C:\ADFGettingStarted**選取**partitionweblogs.hql**， **input.log**檔案，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-268">Navigate toohello **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="a9888-269">您可以建立這兩個檔案從 hello 必要條件的一部分[教學課程概觀](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-269">You created these two files as part of prerequisites from hello [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="a9888-270">當您發行 hello 方案 hello 下一個步驟中時，hello **partitionweblogs.hql**檔案已上傳的 toohello**指令碼**資料夾中 hello `adfgetstarted` blob 容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-270">When you publish hello solution in hello next step, hello **partitionweblogs.hql** file is uploaded toohello **script** folder in hello `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="a9888-271">發佈/部署 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="a9888-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="a9888-272">在此步驟中，您會在您的專案 toohello Azure Data Factory 服務中發行 hello Data Factory 實體 （連結的服務、 資料集和管線）。</span><span class="sxs-lookup"><span data-stu-id="a9888-272">In this step, you publish hello Data Factory entities (linked services, datasets, and pipeline) in your project toohello Azure Data Factory service.</span></span> <span data-ttu-id="a9888-273">在發行的 hello 程序，您可以指定 hello data factory 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9888-273">In hello process of publishing, you specify hello name for your data factory.</span></span> 

1. <span data-ttu-id="a9888-274">以滑鼠右鍵按一下專案 hello 方案總管] 中的，按一下 [**發行**。</span><span class="sxs-lookup"><span data-stu-id="a9888-274">Right-click project in hello Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="a9888-275">如果您看到**登入 Microsoft 帳戶 tooyour**對話方塊中，hello 擁有帳戶的 Azure 訂用帳戶中，輸入您的認證，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="a9888-275">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="a9888-276">您應該會看到下列對話方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a9888-276">You should see hello following dialog box:</span></span>

   ![發佈對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="a9888-278">在 hello**設定資料 factory**頁面上，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="a9888-278">In hello **Configure data factory** page, do hello following steps:</span></span>

    ![發佈 - 新增資料處理站設定](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="a9888-280">選取 [建立新的 Data Factory]  選項。</span><span class="sxs-lookup"><span data-stu-id="a9888-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="a9888-281">輸入唯一**名稱**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-281">Enter a unique **name** for hello data factory.</span></span> <span data-ttu-id="a9888-282">例如：**DataFactoryUsingVS09152016**。</span><span class="sxs-lookup"><span data-stu-id="a9888-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="a9888-283">hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="a9888-283">hello name must be globally unique.</span></span>
   3. <span data-ttu-id="a9888-284">選取 hello 右訂用帳戶 hello**訂用帳戶**欄位。</span><span class="sxs-lookup"><span data-stu-id="a9888-284">Select hello right subscription for hello **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="a9888-285">如果看不到任何訂用帳戶，請確定您登入是系統管理員或共同管理員的 hello 訂用帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9888-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>
   4. <span data-ttu-id="a9888-286">選取 hello**資源群組**hello 資料 factory toobe 建立的。</span><span class="sxs-lookup"><span data-stu-id="a9888-286">Select hello **resource group** for hello data factory toobe created.</span></span>
   5. <span data-ttu-id="a9888-287">選取 hello**區域**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-287">Select hello **region** for hello data factory.</span></span>
   6. <span data-ttu-id="a9888-288">按一下**下一步**tooswitch toohello**發行的項目**頁面。</span><span class="sxs-lookup"><span data-stu-id="a9888-288">Click **Next** tooswitch toohello **Publish Items** page.</span></span> <span data-ttu-id="a9888-289">(按 **索引標籤**超出 hello 名稱欄位 tooif hello toomove**下一步**按鈕已停用。)</span><span class="sxs-lookup"><span data-stu-id="a9888-289">(Press **TAB** toomove out of hello Name field tooif hello **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a9888-290">如果您收到 hello 錯誤**Data factory 名稱"DataFactoryUsingVS"不是使用**發行時，請變更 hello 名稱 (例如，yournameDataFactoryUsingVS)。</span><span class="sxs-lookup"><span data-stu-id="a9888-290">If you receive hello error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change hello name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="a9888-291">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="a9888-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="a9888-292">在 [hello**發行的項目**頁面上，確定所有 hello Data Factory 實體已選取，然後按一下**下一步]** tooswitch toohello**摘要**頁面。</span><span class="sxs-lookup"><span data-stu-id="a9888-292">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>

    ![發佈項目頁面](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="a9888-294">檢閱 hello 摘要，然後按一下**下一步**toostart hello 部署程序和檢視 hello**部署狀態**。</span><span class="sxs-lookup"><span data-stu-id="a9888-294">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>

    ![摘要頁面](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="a9888-296">在 [hello**部署狀態**] 頁面上，您應該會看到 hello hello 部署程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="a9888-296">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="a9888-297">Hello 部署完成之後，請按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="a9888-297">Click Finish after hello deployment is done.</span></span>

<span data-ttu-id="a9888-298">重要事項 toonote:</span><span class="sxs-lookup"><span data-stu-id="a9888-298">Important points toonote:</span></span>

- <span data-ttu-id="a9888-299">如果您收到 hello 錯誤：**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**、 執行 hello 下列其中一項，然後再試一次發行：</span><span class="sxs-lookup"><span data-stu-id="a9888-299">If you receive hello error: **This subscription is not registered toouse namespace Microsoft.DataFactory**, do one of hello following and try publishing again:</span></span>
    - <span data-ttu-id="a9888-300">在 Azure PowerShell，執行下列命令 tooregister hello Data Factory 提供者的 hello。</span><span class="sxs-lookup"><span data-stu-id="a9888-300">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="a9888-301">您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="a9888-301">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="a9888-302">登入使用 hello Azure 訂用帳戶中 toohello [Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-302">Login using hello Azure subscription in toohello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="a9888-303">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="a9888-303">This action automatically registers hello provider for you.</span></span>
- <span data-ttu-id="a9888-304">可能會註冊為未來的 hello 中的 DNS 名稱，因此會變成可公開可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="a9888-304">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
- <span data-ttu-id="a9888-305">toocreate Data Factory 執行個體，您需要 toobe 為系統管理員或共同管理員的 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a9888-305">toocreate Data Factory instances, you need toobe an admin or co-admin of hello Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="a9888-306">監視管線</span><span class="sxs-lookup"><span data-stu-id="a9888-306">Monitor pipeline</span></span>
<span data-ttu-id="a9888-307">在此步驟中，您可以監視 hello 管線中使用圖表檢視的 hello data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-307">In this step, you monitor hello pipeline using Diagram View of hello data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="a9888-308">使用圖表檢視監視管線</span><span class="sxs-lookup"><span data-stu-id="a9888-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="a9888-309">登入 toohello [Azure 入口網站](https://portal.azure.com/)，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="a9888-309">Log in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>
   1. <span data-ttu-id="a9888-310">按一下 [更多服務]，然後按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="a9888-310">Click **More services** and click **Data factories**.</span></span>
       
        ![瀏覽 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="a9888-312">選取 hello 的 data factory 的名稱 (例如： **DataFactoryUsingVS09152016**) 從 data factory 的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="a9888-312">Select hello name of your data factory (for example: **DataFactoryUsingVS09152016**) from hello list of data factories.</span></span>
   
       ![選取您的 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="a9888-314">在 data factory 的 hello 首頁上，按一下 **圖表**。</span><span class="sxs-lookup"><span data-stu-id="a9888-314">In hello home page for your data factory, click **Diagram**.</span></span>

    ![[圖表] 磚](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="a9888-316">在 hello 圖表檢視，您會看到 hello 管線，以及此教學課程中使用的資料集的總覽。</span><span class="sxs-lookup"><span data-stu-id="a9888-316">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="a9888-318">tooview hello 管線，以滑鼠右鍵按一下管線，在 hello 中的所有活動圖表，然後按一下 開啟管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-318">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![開啟管線功能表](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="a9888-320">確認您看到 hello 管線中的 hello HDInsightHive 活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-320">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![開啟管線檢視](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="a9888-322">toonavigate 回 toohello 前一個檢視中，按一下  **Data factory** hello hello 上方的階層連結功能表中。</span><span class="sxs-lookup"><span data-stu-id="a9888-322">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
6. <span data-ttu-id="a9888-323">在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobInput**。</span><span class="sxs-lookup"><span data-stu-id="a9888-323">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="a9888-324">確認該 hello 扇區**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="a9888-324">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="a9888-325">它可能需要幾分鐘的 hello 配量 tooshow 以佔用就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="a9888-325">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="a9888-326">如果它不會發生您等候一段時間之後，查看是否有 hello 輸入的檔 (input.log) 放在 hello 右容器 (`adfgetstarted`) 和資料夾 (`inputdata`)。</span><span class="sxs-lookup"><span data-stu-id="a9888-326">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="a9888-327">並確定該 hello**外部**hello 輸入資料集上的屬性設定太**true**。</span><span class="sxs-lookup"><span data-stu-id="a9888-327">And, make sure that hello **external** property on hello input dataset is set too**true**.</span></span> 

   ![輸入配量處於就緒狀態](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="a9888-329">按一下**X** tooclose **AzureBlobInput**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a9888-329">Click **X** tooclose **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="a9888-330">在 hello**圖表檢視**，按兩下 hello 資料集**AzureBlobOutput**。</span><span class="sxs-lookup"><span data-stu-id="a9888-330">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="a9888-331">您會看到目前正在處理該 hello 扇區。</span><span class="sxs-lookup"><span data-stu-id="a9888-331">You see that hello slice that is currently being processed.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="a9888-333">當處理完成時，請參閱中的 hello 扇區**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="a9888-333">When processing is done, you see hello slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a9888-334">建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="a9888-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="a9888-335">因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="a9888-335">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>  
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="a9888-337">當 hello 配量處於**準備**狀態，請檢查 hello`partitioneddata`資料夾中 hello `adfgetstarted` hello 您 blob 儲存體容器中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-337">When hello slice is in **Ready** state, check hello `partitioneddata` folder in hello `adfgetstarted` container in your blob storage for hello output data.</span></span>  

    ![輸出資料](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="a9888-339">按一下 hello 配量 toosee 詳細資料 中，有關**資料配量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a9888-339">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

    ![資料配量詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="a9888-341">按一下在 hello 中執行的活動**活動執行清單**toosee 活動的詳細資料中執行 （在我們的案例的 Hive 活動）**活動執行詳細資料**視窗。</span><span class="sxs-lookup"><span data-stu-id="a9888-341">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![活動執行詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="a9888-343">從 hello 記錄檔，您可以查看上次執行所執行的 hello Hive 查詢和狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="a9888-343">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="a9888-344">這些記錄檔適合用來排解任何疑難問題。</span><span class="sxs-lookup"><span data-stu-id="a9888-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="a9888-345">請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)如需如何 toouse hello Azure 入口網站 toomonitor hello 管線和資料集您已建立本教學課程中的指示。</span><span class="sxs-lookup"><span data-stu-id="a9888-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="a9888-346">使用監視及管理應用程式來監視管線</span><span class="sxs-lookup"><span data-stu-id="a9888-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="a9888-347">您也可以使用監視和管理應用程式 toomonitor 您的管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-347">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="a9888-348">如需使用此應用程式的詳細資訊，請參閱 [使用監視及管理應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="a9888-349">按一下 [監視及管理] 圖格。</span><span class="sxs-lookup"><span data-stu-id="a9888-349">Click Monitor & Manage tile.</span></span>

    ![監視及管理圖格](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="a9888-351">您應該會看到 [監視及管理] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9888-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="a9888-352">變更 hello**開始時間**和**結束時間**toomatch 開始 (04-01-2016年上午 12:00) 和結束時間 (04-02-2016年上午 12:00) 您的管線，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="a9888-352">Change hello **Start time** and **End time** toomatch start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![監視及管理應用程式](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="a9888-354">toosee 詳細活動視窗，請在選取 hello**活動視窗清單**toosee 相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-354">toosee details about an activity window, select it in hello **Activity Windows list** toosee details about it.</span></span>
    <span data-ttu-id="a9888-355">![活動時段詳細資料](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="a9888-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9888-356">已成功處理 hello 配量時，取得刪除 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="a9888-356">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="a9888-357">因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello 輸入的檔 (input.log) toohello`inputdata`資料夾 hello`adfgetstarted`容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-357">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello `inputdata` folder of hello `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="a9888-358">其他注意事項</span><span class="sxs-lookup"><span data-stu-id="a9888-358">Additional notes</span></span>
- <span data-ttu-id="a9888-359">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="a9888-360">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="a9888-361">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-361">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="a9888-362">請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="a9888-363">請參閱[計算連結的服務](data-factory-compute-linked-services.md)hello 的 Data Factory 支援的計算服務的清單。</span><span class="sxs-lookup"><span data-stu-id="a9888-363">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="a9888-364">連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-364">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="a9888-365">請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)針對所有 hello 來源與接收支援 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="a9888-366">請參閱[計算連結的服務](data-factory-compute-linked-services.md)Data Factory 支援的計算服務的 hello 清單和[轉換活動](data-factory-data-transformation-activities.md)，可以在其上執行。</span><span class="sxs-lookup"><span data-stu-id="a9888-366">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="a9888-367">請參閱[移動的資料 / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性用於 hello Azure 儲存體連結服務定義。</span><span class="sxs-lookup"><span data-stu-id="a9888-367">See [Move data from/tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in hello Azure Storage linked service definition.</span></span>
- <span data-ttu-id="a9888-368">您可以使用自己的 HDInsight 叢集，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="a9888-369">請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="a9888-370">hello Data Factory 建立**linux**以 hello 前面 JSON 為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-370">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello preceding JSON.</span></span> <span data-ttu-id="a9888-371">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="a9888-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="a9888-372">hello HDInsight 叢集建立**預設容器**hello hello JSON (linkedServiceName) 中所指定的 blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a9888-372">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="a9888-373">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-373">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="a9888-374">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="a9888-374">This behavior is by design.</span></span> <span data-ttu-id="a9888-375">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (timeToLive)，否則每次處理配量時，就會建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="a9888-376">hello 處理完成時，會自動刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9888-376">hello cluster is automatically deleted when hello processing is done.</span></span>
    
    <span data-ttu-id="a9888-377">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="a9888-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="a9888-378">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="a9888-378">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="a9888-379">這些容器的 hello 名稱遵循模式： `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="a9888-379">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="a9888-380">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9888-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="a9888-381">目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="a9888-381">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="a9888-382">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="a9888-382">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 
- <span data-ttu-id="a9888-383">本教學課程不會顯示如何使用 Azure Data Factory 複製資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="a9888-384">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-384">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-tooview-data-factories"></a><span data-ttu-id="a9888-385">使用伺服器總管 tooview data factory</span><span class="sxs-lookup"><span data-stu-id="a9888-385">Use Server Explorer tooview data factories</span></span>
1. <span data-ttu-id="a9888-386">在**Visual Studio**，按一下 **檢視**在 hello 功能表，然後按一下**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="a9888-386">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="a9888-387">在 [hello 伺服器總管] 視窗中，展開**Azure**展開**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="a9888-387">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="a9888-388">如果您看到**登入 tooVisual Studio**，輸入 hello**帳戶**與您的 Azure 訂用帳戶，然後按一下相關聯**繼續**。</span><span class="sxs-lookup"><span data-stu-id="a9888-388">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="a9888-389">輸入**密碼**，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="a9888-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="a9888-390">Visual Studio 會嘗試 tooget 您訂用帳戶中的所有 Azure data factory 的資訊。</span><span class="sxs-lookup"><span data-stu-id="a9888-390">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="a9888-391">您看到這項作業在 hello hello 狀態**資料 Factory 工作清單**視窗。</span><span class="sxs-lookup"><span data-stu-id="a9888-391">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="a9888-393">您可以以滑鼠右鍵按一下 data factory，並選取**匯出 Data Factory tooNew 專案**toocreate Visual Studio 專案是根據現有的 data factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-393">You can right-click a data factory, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![匯出 Data Factory](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="a9888-395">更新 Visual studio 的 Data Factory 工具</span><span class="sxs-lookup"><span data-stu-id="a9888-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="a9888-396">tooupdate Azure Data Factory tools for Visual Studio hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9888-396">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="a9888-397">按一下**工具**hello 功能表，然後選取**擴充功能和更新**。</span><span class="sxs-lookup"><span data-stu-id="a9888-397">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="a9888-398">選取**更新**在 hello 左的窗格，然後選取  **Visual Studio 組件庫**。</span><span class="sxs-lookup"><span data-stu-id="a9888-398">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="a9888-399">選取 [Visual Studio 的 Azure Data Factory 工具] 並按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="a9888-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="a9888-400">如果看不到此項目，您已經有 hello hello 工具最新版本。</span><span class="sxs-lookup"><span data-stu-id="a9888-400">If you do not see this entry, you already have hello latest version of hello tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="a9888-401">使用組態檔</span><span class="sxs-lookup"><span data-stu-id="a9888-401">Use configuration files</span></span>
<span data-ttu-id="a9888-402">您可以使用 Visual Studio tooconfigure 屬性中的組態檔的連結服務/資料表/管線以不同的方式為每個環境。</span><span class="sxs-lookup"><span data-stu-id="a9888-402">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="a9888-403">請考慮下列 JSON 定義 Azure 儲存體連結服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="a9888-403">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="a9888-404">toospecify **connectionString** accountname 和 accountkey hello 環境 （開發/測試/生產環境） toowhich 所根據的值不同，您要部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="a9888-404">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="a9888-405">您可以針對每個環境使用個別的組態檔來達成此行為。</span><span class="sxs-lookup"><span data-stu-id="a9888-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="a9888-406">新增組態檔</span><span class="sxs-lookup"><span data-stu-id="a9888-406">Add a configuration file</span></span>
<span data-ttu-id="a9888-407">執行下列步驟的 hello 加入每個環境的組態檔：</span><span class="sxs-lookup"><span data-stu-id="a9888-407">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="a9888-408">Visual Studio 方案中的 hello Data Factory 專案上按一下滑鼠右鍵，指向太**新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="a9888-408">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="a9888-409">選取**Config**從已安裝的範本在 hello 左邊 hello 清單中選取**組態檔**，輸入**名稱**hello 組態檔案，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a9888-409">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![新增組態檔](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="a9888-411">遵循格式 hello 中加入組態參數和值：</span><span class="sxs-lookup"><span data-stu-id="a9888-411">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="a9888-412">這個範例會設定 Azure 儲存體連結服務和 Azure SQL 連結服務的 connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="a9888-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="a9888-413">請注意，用來指定名稱的 hello 語法[JsonPath](http://goessner.net/articles/JsonPath/)。</span><span class="sxs-lookup"><span data-stu-id="a9888-413">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="a9888-414">如果 JSON 屬性，其值的陣列，如 hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="a9888-414">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="a9888-415">設定屬性，如下列組態檔 （使用以零為起始的索引） 的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="a9888-415">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="a9888-416">包含空格的屬性名稱</span><span class="sxs-lookup"><span data-stu-id="a9888-416">Property names with spaces</span></span>
<span data-ttu-id="a9888-417">如果屬性名稱具有空格中的，使用方括號，如下列範例 （資料庫伺服器名稱） 的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="a9888-417">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="a9888-418">使用組態部署解決方案</span><span class="sxs-lookup"><span data-stu-id="a9888-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="a9888-419">當您發行 Azure Data Factory 實體在 VS 中時，您可以指定該發行作業需 toouse hello 組態。</span><span class="sxs-lookup"><span data-stu-id="a9888-419">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="a9888-420">使用組態檔的 Azure Data Factory 專案中的 toopublish 實體：</span><span class="sxs-lookup"><span data-stu-id="a9888-420">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="a9888-421">Data Factory 專案上按一下滑鼠右鍵，然後按一下**發行**toosee hello**發行的項目** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a9888-421">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="a9888-422">選取現有的 data factory，或指定值的 data factory 建立 hello**設定資料 factory**頁面，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9888-422">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="a9888-423">在 hello**發行的項目**頁面： 您會看到與 hello 可用的組態下拉式清單**選取部署設定**欄位。</span><span class="sxs-lookup"><span data-stu-id="a9888-423">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![選取組態檔](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="a9888-425">選取 hello**組態檔**您會想 toouse，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9888-425">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="a9888-426">確認您看到的 JSON 檔案中 hello hello 名稱**摘要**頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9888-426">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="a9888-427">按一下**完成**hello 部署作業完成之後。</span><span class="sxs-lookup"><span data-stu-id="a9888-427">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="a9888-428">當您部署時，hello 設定檔中的 hello 值是使用的 tooset hello JSON 檔案中的屬性值在 hello 實體部署的 tooAzure Data Factory 服務之前。</span><span class="sxs-lookup"><span data-stu-id="a9888-428">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="a9888-429">使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="a9888-429">Use Azure Key Vault</span></span>
<span data-ttu-id="a9888-430">它不建議您經常對等連接字串 toohello 程式碼儲存機制的安全性原則 toocommit 敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-430">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="a9888-431">請參閱[ADF 安全發佈](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)GitHub toolearn 有關在 Azure 金鑰保存庫中儲存機密資訊，並使用它時發行 Data Factory 實體上的範例。</span><span class="sxs-lookup"><span data-stu-id="a9888-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="a9888-432">hello 安全發行 Visual Studio 擴充功能可讓儲存在金鑰保存庫中的 hello 密碼 toobe 和連結的服務中指定只參考 toothem / 部署組態。</span><span class="sxs-lookup"><span data-stu-id="a9888-432">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="a9888-433">當您發行 Data Factory 實體 tooAzure 時，這些參考會解析。</span><span class="sxs-lookup"><span data-stu-id="a9888-433">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="a9888-434">這些檔案接著可以認可的 toosource 儲存機制，而不公開任何秘密。</span><span class="sxs-lookup"><span data-stu-id="a9888-434">These files can then be committed toosource repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="a9888-435">摘要</span><span class="sxs-lookup"><span data-stu-id="a9888-435">Summary</span></span>
<span data-ttu-id="a9888-436">在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a9888-436">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="a9888-437">您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9888-437">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="a9888-438">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="a9888-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="a9888-439">建立兩個 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="a9888-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="a9888-440">**Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。</span><span class="sxs-lookup"><span data-stu-id="a9888-440">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="a9888-441">**Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="a9888-441">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="a9888-442">Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="a9888-443">建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。</span><span class="sxs-lookup"><span data-stu-id="a9888-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="a9888-444">建立具有 **HDInsight Hive** 活動的**管線**。</span><span class="sxs-lookup"><span data-stu-id="a9888-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a9888-445">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9888-445">Next Steps</span></span>
<span data-ttu-id="a9888-446">在本文中，您已經建立可在隨選 HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。</span><span class="sxs-lookup"><span data-stu-id="a9888-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="a9888-447">如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-447">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="a9888-448">您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="a9888-448">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a9888-449">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="a9888-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="a9888-450">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9888-450">See Also</span></span>
| <span data-ttu-id="a9888-451">主題</span><span class="sxs-lookup"><span data-stu-id="a9888-451">Topic</span></span> | <span data-ttu-id="a9888-452">說明</span><span class="sxs-lookup"><span data-stu-id="a9888-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="a9888-453">管線</span><span class="sxs-lookup"><span data-stu-id="a9888-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="a9888-454">這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 資料驅動型工作流程或商務案例。</span><span class="sxs-lookup"><span data-stu-id="a9888-454">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="a9888-455">資料集</span><span class="sxs-lookup"><span data-stu-id="a9888-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="a9888-456">本文協助您了解 Azure Data Factory 中的資料集。</span><span class="sxs-lookup"><span data-stu-id="a9888-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="a9888-457">資料轉換活動</span><span class="sxs-lookup"><span data-stu-id="a9888-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="a9888-458">本文提供 Azure Data Factory 所支援的資料轉換活動清單 (例如您在本教學課程中使用的 HDInsight Hive 轉換)。</span><span class="sxs-lookup"><span data-stu-id="a9888-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="a9888-459">排程和執行</span><span class="sxs-lookup"><span data-stu-id="a9888-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="a9888-460">本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。</span><span class="sxs-lookup"><span data-stu-id="a9888-460">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="a9888-461">使用監視應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="a9888-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="a9888-462">本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9888-462">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
