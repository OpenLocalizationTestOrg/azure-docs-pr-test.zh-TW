---
title: "從 Azure Data Factory 程式 aaaInvoke Spark |Microsoft 文件"
description: "了解如何從 Azure data factory 使用 tooinvoke Spark 程式 hello MapReduce 活動。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="2e84b-103">從 Azure Data Factory 叫用 Spark 程式管線</span><span class="sxs-lookup"><span data-stu-id="2e84b-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2e84b-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="2e84b-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2e84b-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2e84b-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2e84b-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2e84b-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2e84b-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2e84b-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2e84b-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2e84b-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="2e84b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="2e84b-114">簡介</span><span class="sxs-lookup"><span data-stu-id="2e84b-114">Introduction</span></span>
<span data-ttu-id="2e84b-115">Spark 活動是其中一個 hello[資料轉換活動](data-factory-data-transformation-activities.md)受到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="2e84b-116">此活動可執行 hello 指定您的 Apache Spark 叢集，在 Azure HDInsight 上的 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="2e84b-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="2e84b-117">Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="2e84b-118">Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="2e84b-119">它不支援隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="2e84b-120">逐步解說：使用 Spark 活動建立管線</span><span class="sxs-lookup"><span data-stu-id="2e84b-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="2e84b-121">以下是 hello 的一般步驟 toocreate Data Factory 管線與 Spark 活動。</span><span class="sxs-lookup"><span data-stu-id="2e84b-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="2e84b-122">建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="2e84b-122">Create a data factory.</span></span>
2. <span data-ttu-id="2e84b-123">建立 Azure 儲存體連結服務 toolink 您與您的 HDInsight Spark 叢集 toohello data factory 相關聯的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e84b-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="2e84b-124">Azure HDInsight toohello data factory 中建立 Azure HDInsight 連結服務 toolink Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="2e84b-125">建立資料集，是指 toohello Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="2e84b-126">目前，您必須指定活動的輸出資料集，即使沒有產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="2e84b-127">是指在 #2 中建立的 toohello HDInsight 連結服務的 Spark 活動建立的管線。</span><span class="sxs-lookup"><span data-stu-id="2e84b-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="2e84b-128">hello 活動與 hello hello 做為輸出資料集的上一個步驟中建立的資料集設定。</span><span class="sxs-lookup"><span data-stu-id="2e84b-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="2e84b-129">hello 輸出資料集是哪些磁碟機 hello 排程 （每小時、 每天、 等等）。</span><span class="sxs-lookup"><span data-stu-id="2e84b-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2e84b-130">因此，您必須指定 hello 輸出資料集，即使 hello 活動實際上也不會產生輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2e84b-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="2e84b-131">Prerequisites</span></span>
1. <span data-ttu-id="2e84b-132">建立**一般用途的 Azure 儲存體帳戶**依照 hello 逐步解說中的指示：[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="2e84b-133">建立**Azure HDInsight 中的 Apache Spark 叢集**依照 hello 教學課程中的指示： [Azure HDInsight 中建立的 Apache Spark 叢集](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="2e84b-134">將您建立與此叢集的步驟 1 中的 hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e84b-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="2e84b-135">下載並檢閱 hello python 指令碼檔案**test.py**位於： [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="2e84b-136">上傳**test.py** toohello **pyFiles**資料夾中 hello **adfspark**您的 Azure Blob 儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="2e84b-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="2e84b-137">如果它們尚不存在，請建立 hello 容器和 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="2e84b-138">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="2e84b-138">Create data factory</span></span>
<span data-ttu-id="2e84b-139">讓我們開始在此步驟中建立 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="2e84b-140">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2e84b-141">按一下**新增**hello 左窗格中，按一下 **資料 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="2e84b-142">在 hello**新的 data factory**刀鋒視窗中，輸入**SparkDF** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2e84b-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2e84b-143">hello hello Azure data factory 的名稱必須是**全域唯一**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="2e84b-144">如果您看到 hello 錯誤： **Data factory 名稱"SparkDF"不是使用**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="2e84b-145">變更 hello 名稱 hello 資料處理站 （例如，yournameSparkDFdate，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="2e84b-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="2e84b-146">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="2e84b-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="2e84b-147">選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。</span><span class="sxs-lookup"><span data-stu-id="2e84b-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="2e84b-148">請選取現有的**資源群組**，或建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e84b-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="2e84b-149">選取**Pin toodashboard**選項。</span><span class="sxs-lookup"><span data-stu-id="2e84b-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="2e84b-150">按一下**建立**上 hello**新的 data factory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2e84b-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2e84b-151">toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。</span><span class="sxs-lookup"><span data-stu-id="2e84b-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="2e84b-152">您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e84b-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="2e84b-153">已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="2e84b-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="2e84b-154">如果看不到 hello 資料 factory 頁面上，按一下您 hello 儀表板上的 data factory 的 hello 磚。</span><span class="sxs-lookup"><span data-stu-id="2e84b-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Data Factory 刀鋒視窗](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="2e84b-156">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="2e84b-156">Create linked services</span></span>
<span data-ttu-id="2e84b-157">在此步驟中，您可以建立兩個連結的服務，一個 toolink 您的 Spark 叢集 tooyour 的 data factory，，和 hello 其他 toolink 您 Azure 儲存體 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="2e84b-158">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="2e84b-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="2e84b-159">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="2e84b-160">您稍後在本逐步解說步驟中建立資料集是指 toothis 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="2e84b-161">您在 hello 下一個步驟中定義 HDInsight 連結服務的 hello 太參考 toothis 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="2e84b-162">按一下**作者及部署**上 hello **Data Factory** data factory 的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2e84b-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="2e84b-163">您應該會看到 hello Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="2e84b-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="2e84b-164">按一下 [新增資料存放區] 並選擇 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="2e84b-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![新增資料存放區 - Azure 儲存體 - 功能表](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="2e84b-166">您應該會看見 hello **JSON 指令碼**建立 Azure 儲存體已連結的 hello 編輯器中的服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="2e84b-168">取代**帳戶名稱**和**帳戶金鑰**與 hello Azure 儲存體帳戶名稱和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e84b-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="2e84b-169">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="2e84b-170">toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="2e84b-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="2e84b-171">Hello 連結的服務已成功部署之後，hello **Draft 1**視窗應該就會消失，而且您會看到**AzureStorageLinkedService** hello hello 左側的樹狀檢視中。</span><span class="sxs-lookup"><span data-stu-id="2e84b-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="2e84b-172">建立 HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="2e84b-172">Create HDInsight linked service</span></span>
<span data-ttu-id="2e84b-173">在此步驟中，您建立 Azure HDInsight 連結服務 toolink 您 HDInsight Spark 叢集 toohello 的 data factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="2e84b-174">hello HDInsight 叢集是使用的 toorun hello Spark 程式 hello 管線，在此範例中的 hello Spark 活動中指定。</span><span class="sxs-lookup"><span data-stu-id="2e84b-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="2e84b-175">按一下**...多個**hello 工具列上，按一下**新計算**，然後按一下 **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![建立 HDInsight 連結服務](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="2e84b-177">複製並貼上下列程式碼片段 toohello hello **Draft 1**視窗。</span><span class="sxs-lookup"><span data-stu-id="2e84b-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="2e84b-178">在 hello JSON 編輯器中，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2e84b-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="2e84b-179">指定 hello **URI** hello HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2e84b-180">例如： `https://<sparkclustername>.azurehdinsight.net/`。</span><span class="sxs-lookup"><span data-stu-id="2e84b-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="2e84b-181">指定的 hello hello 名稱**使用者**誰存取 toohello Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="2e84b-182">指定 hello**密碼**使用者。</span><span class="sxs-lookup"><span data-stu-id="2e84b-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="2e84b-183">指定 hello **Azure 儲存體連結服務**與 hello HDInsight Spark 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="2e84b-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2e84b-184">在此範例中，它是：**AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="2e84b-185">Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="2e84b-186">Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="2e84b-187">它不支援隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="2e84b-188">請參閱[HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)如需詳細資訊 hello HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e84b-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="2e84b-189">toodeploy hello 連結的服務中，按一下**部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="2e84b-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="2e84b-190">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="2e84b-190">Create output dataset</span></span>
<span data-ttu-id="2e84b-191">hello 輸出資料集是哪些磁碟機 hello 排程 （每小時、 每天、 等等）。</span><span class="sxs-lookup"><span data-stu-id="2e84b-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2e84b-192">因此，您必須指定 hello spark 活動的輸出資料集 hello 管線中，即使 hello 活動不會真的產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="2e84b-193">指定 hello 活動的輸入資料集是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="2e84b-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="2e84b-194">在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="2e84b-195">複製並貼上下列程式碼片段 toohello Draft 1 視窗 hello。</span><span class="sxs-lookup"><span data-stu-id="2e84b-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="2e84b-196">hello JSON 片段會定義資料集稱為**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="2e84b-197">此外，您可以指定 hello 結果會儲存在稱為 hello blob 容器**adfspark**和 hello 資料夾稱為**pyFiles/輸出**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="2e84b-198">如先前所述，此資料集是空的資料集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="2e84b-199">在此範例中的 hello Spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="2e84b-200">hello**可用性**區段會指定每天產生該 hello 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="2e84b-201">toodeploy hello 資料集，請按一下**部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="2e84b-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="2e84b-202">建立管線</span><span class="sxs-lookup"><span data-stu-id="2e84b-202">Create pipeline</span></span>
<span data-ttu-id="2e84b-203">在此步驟中，您會建立具有 **HDInsightSpark** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="2e84b-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="2e84b-204">目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="2e84b-205">如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="2e84b-206">因此，在此範例中不會指定任何輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="2e84b-207">在 hello **Data Factory 編輯器**，按一下  **...多個**在 hello 命令列，然後按一下**新管線**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="2e84b-208">取代下列指令碼的 hello hello Draft 1 視窗中的 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="2e84b-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="2e84b-209">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="2e84b-209">Note hello following points:</span></span>
    - <span data-ttu-id="2e84b-210">hello**類型**屬性設定太**HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="2e84b-211">hello **rootPath**設定得**adfspark\\pyFiles** adfspark 所在 hello Azure Blob 容器和 pyFiles 是正常的資料夾，該容器中。</span><span class="sxs-lookup"><span data-stu-id="2e84b-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="2e84b-212">在此範例中，hello Azure Blob 儲存體是 hello 與 hello Spark 叢集相關聯的其中一個。</span><span class="sxs-lookup"><span data-stu-id="2e84b-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="2e84b-213">您可以上傳 hello 檔案 tooa 不同的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e84b-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="2e84b-214">如果您這樣做，請建立 Azure 儲存體連結服務 toolink 該儲存體帳戶 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2e84b-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="2e84b-215">然後，指定 hello hello 連結服務名稱做為 hello 值**sparkJobLinkedService**屬性。</span><span class="sxs-lookup"><span data-stu-id="2e84b-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="2e84b-216">請參閱[Spark 活動屬性](#spark-activity-properties)如需詳細資訊，這個屬性，而且支援 hello Spark 活動的其他內容。</span><span class="sxs-lookup"><span data-stu-id="2e84b-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="2e84b-217">hello **entryFilePath**設定 toohello **test.py**，這是 hello python 檔案。</span><span class="sxs-lookup"><span data-stu-id="2e84b-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="2e84b-218">hello **getDebugInfo**屬性設定太**永遠**，這表示 hello 記錄檔一律會產生 （成功或失敗）。</span><span class="sxs-lookup"><span data-stu-id="2e84b-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="2e84b-219">我們建議您不要設定此屬性太`Always`實際執行環境中除非您疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="2e84b-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="2e84b-220">hello**輸出**區段具有一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="2e84b-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="2e84b-221">您必須指定輸出資料集，即使 hello spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="2e84b-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="2e84b-222">hello 輸出資料集的磁碟機 hello 排程 hello 管線 （每小時、 每天、 等等）。</span><span class="sxs-lookup"><span data-stu-id="2e84b-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="2e84b-223">如需支援的 Spark 活動 hello 屬性的詳細資訊，請參閱[二手活動屬性](#spark-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2e84b-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="2e84b-224">toodeploy hello 管線中，按一下 **部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="2e84b-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="2e84b-225">監視管線</span><span class="sxs-lookup"><span data-stu-id="2e84b-225">Monitor pipeline</span></span>
1. <span data-ttu-id="2e84b-226">按一下**X** tooclose Data Factory 編輯器刀鋒 toonavigate 回 toohello Data Factory 的首頁。</span><span class="sxs-lookup"><span data-stu-id="2e84b-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="2e84b-227">按一下**監視和管理**toolaunch hello 監視另一個索引標籤中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e84b-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![監視及管理圖格](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="2e84b-229">變更 hello**開始時間**太篩選 hello 頂端**2/1/2017年**，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="2e84b-230">因為沒有 hello 之間只有一天開始 (2017年-02-01) 和結束時間 (2017年-02-02) 的 hello 管線，您應該看到只有一個活動視窗。</span><span class="sxs-lookup"><span data-stu-id="2e84b-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="2e84b-231">確認該 hello 資料配量處於**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="2e84b-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![監視 hello 管線](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="2e84b-233">選取 hello**活動視窗**toosee hello 活動執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e84b-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="2e84b-234">如果沒有發生錯誤，您會看到資訊，請參閱 hello 右窗格中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e84b-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="2e84b-235">請確認 hello 結果</span><span class="sxs-lookup"><span data-stu-id="2e84b-235">Verify hello results</span></span>

1. <span data-ttu-id="2e84b-236">瀏覽至 https://CLUSTERNAME.azurehdinsight.net/jupyter，啟動您的 HDInsight Spark 叢集的 **Jupyter Notebook**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="2e84b-237">您可以為 HDInsight Spark 叢集啟動叢集儀表板，然後啟動 **Jupyter Notebook**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="2e84b-238">按一下**新增** -> **PySpark** toostart 新的記事本。</span><span class="sxs-lookup"><span data-stu-id="2e84b-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Jupyter 新筆記本](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="2e84b-240">執行 hello 下列命令複製/貼上的 hello 文字，然後按**SHIFT + ENTER** hello hello 第二個陳述式結尾處。</span><span class="sxs-lookup"><span data-stu-id="2e84b-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="2e84b-241">確認您看到 hello hello hvac 資料表的資料：</span><span class="sxs-lookup"><span data-stu-id="2e84b-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Jupyter 查詢結果](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="2e84b-243">如需詳細指示，請參閱[執行 Spark SQL 查詢](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql)區段。</span><span class="sxs-lookup"><span data-stu-id="2e84b-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="2e84b-244">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2e84b-244">Troubleshooting</span></span>
<span data-ttu-id="2e84b-245">因為您設定**getDebugInfo**太**永遠**，您會看到**記錄**子資料夾中 hello **pyFiles** Azure Blob 容器中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="2e84b-246">hello hello 記錄檔資料夾中的記錄檔會提供其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e84b-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="2e84b-247">發生錯誤時，此記錄檔特別有用。</span><span class="sxs-lookup"><span data-stu-id="2e84b-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="2e84b-248">在實際執行環境中，您可能會想 tooset 它太**失敗**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="2e84b-249">如需進一步疑難排解，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2e84b-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="2e84b-250">瀏覽過`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`。</span><span class="sxs-lookup"><span data-stu-id="2e84b-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI 應用程式](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="2e84b-252">按一下**記錄**hello 其中執行的嘗試。</span><span class="sxs-lookup"><span data-stu-id="2e84b-252">Click **Logs** for one of hello run attempts.</span></span>

    ![應用程式頁面](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="2e84b-254">您應該會看到 hello 記錄 頁面中的其他錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="2e84b-254">You should see additional error information in hello log page.</span></span>

    ![記錄錯誤](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="2e84b-256">hello 下列各節提供有關 Data Factory 實體 toouse Apache Spark 叢集以及您的 data factory 中的 Spark 活動資訊。</span><span class="sxs-lookup"><span data-stu-id="2e84b-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="2e84b-257">Spark 活動屬性</span><span class="sxs-lookup"><span data-stu-id="2e84b-257">Spark activity properties</span></span>
<span data-ttu-id="2e84b-258">以下是管線 Spark 活動與 hello 範例 JSON 定義：</span><span class="sxs-lookup"><span data-stu-id="2e84b-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="2e84b-259">hello 下表描述 hello hello JSON 定義中使用的 JSON 屬性：</span><span class="sxs-lookup"><span data-stu-id="2e84b-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="2e84b-260">屬性</span><span class="sxs-lookup"><span data-stu-id="2e84b-260">Property</span></span> | <span data-ttu-id="2e84b-261">說明</span><span class="sxs-lookup"><span data-stu-id="2e84b-261">Description</span></span> | <span data-ttu-id="2e84b-262">必要</span><span class="sxs-lookup"><span data-stu-id="2e84b-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2e84b-263">名稱</span><span class="sxs-lookup"><span data-stu-id="2e84b-263">name</span></span> | <span data-ttu-id="2e84b-264">Hello 管線中的 hello 活動名稱。</span><span class="sxs-lookup"><span data-stu-id="2e84b-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="2e84b-265">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-265">Yes</span></span> |
| <span data-ttu-id="2e84b-266">說明</span><span class="sxs-lookup"><span data-stu-id="2e84b-266">description</span></span> | <span data-ttu-id="2e84b-267">會描述 hello 活動的文字。</span><span class="sxs-lookup"><span data-stu-id="2e84b-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="2e84b-268">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-268">No</span></span> |
| <span data-ttu-id="2e84b-269">類型</span><span class="sxs-lookup"><span data-stu-id="2e84b-269">type</span></span> | <span data-ttu-id="2e84b-270">這個屬性必須設定 tooHDInsightSpark。</span><span class="sxs-lookup"><span data-stu-id="2e84b-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="2e84b-271">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-271">Yes</span></span> |
| <span data-ttu-id="2e84b-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2e84b-272">linkedServiceName</span></span> | <span data-ttu-id="2e84b-273">名稱 hello HDInsight 連結的服務的 hello Spark 執行程式。</span><span class="sxs-lookup"><span data-stu-id="2e84b-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="2e84b-274">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-274">Yes</span></span> |
| <span data-ttu-id="2e84b-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="2e84b-275">rootPath</span></span> | <span data-ttu-id="2e84b-276">hello Azure Blob 容器，並包含 hello Spark 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="2e84b-277">hello 檔案名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="2e84b-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="2e84b-278">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-278">Yes</span></span> |
| <span data-ttu-id="2e84b-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="2e84b-279">entryFilePath</span></span> | <span data-ttu-id="2e84b-280">相對路徑 toohello 的 hello Spark 程式碼/封裝的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="2e84b-281">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-281">Yes</span></span> |
| <span data-ttu-id="2e84b-282">className</span><span class="sxs-lookup"><span data-stu-id="2e84b-282">className</span></span> | <span data-ttu-id="2e84b-283">應用程式的 Java/Spark 主要類別</span><span class="sxs-lookup"><span data-stu-id="2e84b-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="2e84b-284">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-284">No</span></span> |
| <span data-ttu-id="2e84b-285">arguments</span><span class="sxs-lookup"><span data-stu-id="2e84b-285">arguments</span></span> | <span data-ttu-id="2e84b-286">命令列引數 toohello Spark 程式的清單。</span><span class="sxs-lookup"><span data-stu-id="2e84b-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="2e84b-287">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-287">No</span></span> |
| <span data-ttu-id="2e84b-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="2e84b-288">proxyUser</span></span> | <span data-ttu-id="2e84b-289">hello 使用者帳戶 tooimpersonate tooexecute hello Spark 程式</span><span class="sxs-lookup"><span data-stu-id="2e84b-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="2e84b-290">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-290">No</span></span> |
| <span data-ttu-id="2e84b-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="2e84b-291">sparkConfig</span></span> | <span data-ttu-id="2e84b-292">指定的 Spark hello 主題中列出的組態屬性值： [Spark 設定-應用程式屬性](https://spark.apache.org/docs/latest/configuration.html#available-properties)。</span><span class="sxs-lookup"><span data-stu-id="2e84b-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="2e84b-293">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-293">No</span></span> |
| <span data-ttu-id="2e84b-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="2e84b-294">getDebugInfo</span></span> | <span data-ttu-id="2e84b-295">指定當 hello Spark 記錄檔會複製的 toohello HDInsight 叢集所使用的 Azure 儲存體 （或） sparkJobLinkedService 所指定。</span><span class="sxs-lookup"><span data-stu-id="2e84b-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="2e84b-296">允許的值︰None、Always 或 Failure。</span><span class="sxs-lookup"><span data-stu-id="2e84b-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="2e84b-297">預設值：None。</span><span class="sxs-lookup"><span data-stu-id="2e84b-297">Default value: None.</span></span> | <span data-ttu-id="2e84b-298">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-298">No</span></span> |
| <span data-ttu-id="2e84b-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="2e84b-299">sparkJobLinkedService</span></span> | <span data-ttu-id="2e84b-300">hello Azure 儲存體連結服務的 hello Spark 工作檔案、 相依性，以及記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2e84b-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="2e84b-301">如果您未指定此屬性的值，則會使用 hello 與 HDInsight 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e84b-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="2e84b-302">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="2e84b-303">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="2e84b-303">Folder structure</span></span>
<span data-ttu-id="2e84b-304">hello Spark 活動不支援內嵌指令碼，成為 Pig 和 Hive 活動執行。</span><span class="sxs-lookup"><span data-stu-id="2e84b-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="2e84b-305">Spark 作業也比 Pig/Hive 作業更具擴充性。</span><span class="sxs-lookup"><span data-stu-id="2e84b-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="2e84b-306">Spark 工作，您可以提供多個相依性例如 jar 封裝 （hello java CLASSPATH 中放置）、 python 檔案 （置於 hello PYTHONPATH 上），以及任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="2e84b-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="2e84b-307">建立下列資料夾結構 hello hello HDInsight 連結服務所參考的 Azure Blob 儲存體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2e84b-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="2e84b-308">然後上, 傳所代表的 hello 根資料夾中的相依檔案 toohello 適當的子資料夾**entryFilePath**。</span><span class="sxs-lookup"><span data-stu-id="2e84b-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="2e84b-309">例如上, 傳 python 檔案 toohello pyFiles 子資料夾和 jar 檔案 toohello （每瓶） 的子資料夾 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="2e84b-310">在執行階段，Data Factory 服務預期具備下列資料夾結構 hello Azure Blob 儲存體中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e84b-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="2e84b-311">Path</span><span class="sxs-lookup"><span data-stu-id="2e84b-311">Path</span></span> | <span data-ttu-id="2e84b-312">說明</span><span class="sxs-lookup"><span data-stu-id="2e84b-312">Description</span></span> | <span data-ttu-id="2e84b-313">必要</span><span class="sxs-lookup"><span data-stu-id="2e84b-313">Required</span></span> | <span data-ttu-id="2e84b-314">類型</span><span class="sxs-lookup"><span data-stu-id="2e84b-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="2e84b-315">.</span><span class="sxs-lookup"><span data-stu-id="2e84b-315">.</span></span> | <span data-ttu-id="2e84b-316">hello 儲存體連結服務中的 hello Spark 作業 hello 根路徑</span><span class="sxs-lookup"><span data-stu-id="2e84b-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="2e84b-317">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-317">Yes</span></span> | <span data-ttu-id="2e84b-318">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-318">Folder</span></span> |
| <span data-ttu-id="2e84b-319">&lt;使用者定義&gt;</span><span class="sxs-lookup"><span data-stu-id="2e84b-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="2e84b-320">hello 指向 toohello hello Spark 工作項目檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="2e84b-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="2e84b-321">是</span><span class="sxs-lookup"><span data-stu-id="2e84b-321">Yes</span></span> | <span data-ttu-id="2e84b-322">檔案</span><span class="sxs-lookup"><span data-stu-id="2e84b-322">File</span></span> |
| <span data-ttu-id="2e84b-323">./jars</span><span class="sxs-lookup"><span data-stu-id="2e84b-323">./jars</span></span> | <span data-ttu-id="2e84b-324">在這個資料夾底下的所有檔案會上傳並放在 hello 叢集的 hello java classpath</span><span class="sxs-lookup"><span data-stu-id="2e84b-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="2e84b-325">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-325">No</span></span> | <span data-ttu-id="2e84b-326">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-326">Folder</span></span> |
| <span data-ttu-id="2e84b-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="2e84b-327">./pyFiles</span></span> | <span data-ttu-id="2e84b-328">在這個資料夾底下的所有檔案會上傳並放在 hello PYTHONPATH hello 叢集的</span><span class="sxs-lookup"><span data-stu-id="2e84b-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="2e84b-329">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-329">No</span></span> | <span data-ttu-id="2e84b-330">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-330">Folder</span></span> |
| <span data-ttu-id="2e84b-331">./files</span><span class="sxs-lookup"><span data-stu-id="2e84b-331">./files</span></span> | <span data-ttu-id="2e84b-332">此資料夾下的所有檔案會上傳並放在執行程式工作目錄</span><span class="sxs-lookup"><span data-stu-id="2e84b-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="2e84b-333">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-333">No</span></span> | <span data-ttu-id="2e84b-334">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-334">Folder</span></span> |
| <span data-ttu-id="2e84b-335">./archives</span><span class="sxs-lookup"><span data-stu-id="2e84b-335">./archives</span></span> | <span data-ttu-id="2e84b-336">此資料夾下的所有檔案未壓縮</span><span class="sxs-lookup"><span data-stu-id="2e84b-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="2e84b-337">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-337">No</span></span> | <span data-ttu-id="2e84b-338">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-338">Folder</span></span> |
| <span data-ttu-id="2e84b-339">./logs</span><span class="sxs-lookup"><span data-stu-id="2e84b-339">./logs</span></span> | <span data-ttu-id="2e84b-340">hello 儲存來自 hello Spark 叢集記錄檔的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e84b-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="2e84b-341">否</span><span class="sxs-lookup"><span data-stu-id="2e84b-341">No</span></span> | <span data-ttu-id="2e84b-342">資料夾</span><span class="sxs-lookup"><span data-stu-id="2e84b-342">Folder</span></span> |

<span data-ttu-id="2e84b-343">以下是包含兩個 hello hello HDInsight 連結服務所參考的 Azure Blob 儲存體中的 Spark 工作檔案的儲存體的範例。</span><span class="sxs-lookup"><span data-stu-id="2e84b-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
