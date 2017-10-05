---
title: "從 Azure Data Factory 叫用 Spark 程式 | Microsoft Docs"
description: "了解如何從 Azure Data Factory 使用 MapReduce 活動叫用 Spark 程式。"
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
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="9bae9-103">從 Azure Data Factory 叫用 Spark 程式管線</span><span class="sxs-lookup"><span data-stu-id="9bae9-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9bae9-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="9bae9-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9bae9-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9bae9-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9bae9-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9bae9-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9bae9-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9bae9-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9bae9-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9bae9-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="9bae9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="9bae9-114">簡介</span><span class="sxs-lookup"><span data-stu-id="9bae9-114">Introduction</span></span>
<span data-ttu-id="9bae9-115">Spark 活動是 Azure Data Factory 所支援的其中一個[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="9bae9-116">此活動會在 Azure HDInsight 中 Apache Spark 叢集上執行指定的 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="9bae9-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="9bae9-117">Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="9bae9-118">Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="9bae9-119">它不支援隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="9bae9-120">逐步解說：使用 Spark 活動建立管線</span><span class="sxs-lookup"><span data-stu-id="9bae9-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="9bae9-121">以下是使用 Spark 活動建立 Data Factory 管線的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="9bae9-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="9bae9-122">建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9bae9-122">Create a data factory.</span></span>
2. <span data-ttu-id="9bae9-123">建立 Azure 儲存體連結服務，將與 HDInsight Spark 叢集相關聯的 Azure 儲存體連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="9bae9-124">建立 Azure HDInsight 連結服務，將 Azure HDInsight 中的 Apache Spark 叢集連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="9bae9-125">建立可參考 Azure 儲存體連結服務的資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="9bae9-126">目前，您必須指定活動的輸出資料集，即使沒有產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9bae9-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="9bae9-127">使用 Spark 活動建立管線，以參考 #2 中建立的 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="9bae9-128">此活動已使用您在上一個步驟中建立的資料集設定為輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="9bae9-129">輸出資料集可以驅動排程 (每小時、每天等)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="9bae9-130">因此，您必須指定輸出資料集，即使活動並未真的產生輸出。</span><span class="sxs-lookup"><span data-stu-id="9bae9-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9bae9-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="9bae9-131">Prerequisites</span></span>
1. <span data-ttu-id="9bae9-132">依照逐步解說：[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)中的指示，建立**一般用途的 Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="9bae9-133">依照教學課程：[在 Azure HDInsight 中建立 Apache Spark 叢集](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)中的指示**在 Azure HDInsight 中建立 Apache Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="9bae9-134">將您在步驟 1 中建立的 Azure 儲存體帳戶與此叢集產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9bae9-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="9bae9-135">下載並檢閱 python 指令碼檔案 **test.py**，該檔案位於：[https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="9bae9-136">將 **test.py** 上傳至您的Azure Blob 儲存體 **adfspark** 容器中的 **pyFiles** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="9bae9-137">建立容器和資料夾 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="9bae9-138">建立資料處理站</span><span class="sxs-lookup"><span data-stu-id="9bae9-138">Create data factory</span></span>
<span data-ttu-id="9bae9-139">讓我們在這個步驟中開始建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="9bae9-140">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9bae9-141">按一下左側功能表上的 [新增]、[資料 + 分析]，再按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="9bae9-142">在 [新增 Data Factory] 刀鋒視窗中，輸入 **SparkDF** 作為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9bae9-143">Azure Data Factory 的名稱必須是 **全域唯一的**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="9bae9-144">如果您看到此錯誤：**Data factory 名稱 "SparkDF" 無法使用**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="9bae9-145">請變更 Data Factory 名稱 (例如 yournameSparkDFdate)，然後嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="9bae9-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="9bae9-146">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="9bae9-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="9bae9-147">選取您想要建立 Data Factory 的 [Azure 訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="9bae9-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="9bae9-148">請選取現有的**資源群組**，或建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9bae9-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="9bae9-149">選取 [釘選到儀表板] 選項。</span><span class="sxs-lookup"><span data-stu-id="9bae9-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="9bae9-150">按一下 [新增 Data Factory] 刀鋒視窗上的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9bae9-151">若要建立 Data Factory 執行個體，您必須是訂用帳戶/資源群組層級的 [Data Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 角色成員。</span><span class="sxs-lookup"><span data-stu-id="9bae9-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="9bae9-152">您會看到 Data Factory 建立在 Azure 入口網站的「儀表板」中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bae9-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="9bae9-153">在 Data Factory 成功建立後，您會看到 Data Factory 頁面，顯示 Data Factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="9bae9-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="9bae9-154">如果看不到 Data Factory 頁面，請在儀表板上按一下您的 Data Factory 圖格。</span><span class="sxs-lookup"><span data-stu-id="9bae9-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Data Factory 刀鋒視窗](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="9bae9-156">建立連結服務</span><span class="sxs-lookup"><span data-stu-id="9bae9-156">Create linked services</span></span>
<span data-ttu-id="9bae9-157">在此步驟中，您可以建立兩個連結服務，一個用來將您的 Spark 叢集連結至 Data Factory，以及另一個用來將您的 Azure 儲存體連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9bae9-158">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="9bae9-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="9bae9-159">在此步驟中，您會將您的 Azure 儲存體帳戶連結到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="9bae9-160">您在本逐步解說稍後的步驟中建立的資料集會參考此連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="9bae9-161">您在下一個步驟中定義的 HDInsight 連結服務也會參考此連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="9bae9-162">在您的 Data Factory 的 [Data Factory] 刀鋒視窗上按一下 [製作和部署]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="9bae9-163">您應該會看到 Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="9bae9-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="9bae9-164">按一下 [新增資料存放區] 並選擇 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![新增資料存放區 - Azure 儲存體 - 功能表](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="9bae9-166">在編輯器中，您應該會看到用來建立 Azure 儲存體連結服務的 **JSON 指令碼**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure 儲存體連結服務](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="9bae9-168">將 **accountname** 和 **accountkey** 以 Azure 儲存體帳戶的名稱及存取金鑰來取代。</span><span class="sxs-lookup"><span data-stu-id="9bae9-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="9bae9-169">若要了解如何取得您的儲存體存取金鑰，請參閱[管理儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)中說明如何檢視、複製和重新產生儲存體存取金鑰的資訊。</span><span class="sxs-lookup"><span data-stu-id="9bae9-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="9bae9-170">若要部署連結服務，請按一下命令列的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="9bae9-171">成功部署連結的服務之後，應該會出現 **Draft-1** 視窗，而且您會在左側的樹狀檢視中看到 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="9bae9-172">建立 HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="9bae9-172">Create HDInsight linked service</span></span>
<span data-ttu-id="9bae9-173">在此步驟中，您會建立 Azure HDInsight 連結服務，將 HDInsight Spark 叢集連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="9bae9-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="9bae9-174">HDInsight 叢集是用來執行此範例管線的 Spark 活動中指定的 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="9bae9-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="9bae9-175">按一下**...其他** (工具列上)，按一下 [新增計算]，然後按一下 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![建立 HDInsight 連結服務](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="9bae9-177">複製下列程式碼片段並貼到 [Draft-1]  視窗。</span><span class="sxs-lookup"><span data-stu-id="9bae9-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="9bae9-178">在 [JSON 編輯器] 中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bae9-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="9bae9-179">指定 HDInsight Spark 叢集的 **URI**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="9bae9-180">例如： `https://<sparkclustername>.azurehdinsight.net/`。</span><span class="sxs-lookup"><span data-stu-id="9bae9-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="9bae9-181">指定具有 Spark 叢集存取權之**使用者**的名稱。</span><span class="sxs-lookup"><span data-stu-id="9bae9-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="9bae9-182">指定使用者的**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="9bae9-183">指定與 HDInsight Spark 叢集相關聯的 **Azure 儲存體連結服務**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="9bae9-184">在此範例中，它是：**AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="9bae9-185">Spark 活動不支援 Azure Data Lake Store 作為主要儲存體的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="9bae9-186">Spark 活動僅支援現有 (您自己的) HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="9bae9-187">它不支援隨選 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="9bae9-188">如需 HDInsight 連結服務的詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="9bae9-189">若要部署連結服務，請按一下命令列的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="9bae9-190">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="9bae9-190">Create output dataset</span></span>
<span data-ttu-id="9bae9-191">輸出資料集可以驅動排程 (每小時、每天等)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="9bae9-192">因此，您必須為管線中的 Spark 活動指定輸出資料集，即使活動並未真的產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9bae9-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="9bae9-193">為活動指定輸入資料集是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="9bae9-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="9bae9-194">在 [Data Factory 編輯器] 中，按一下命令列上的 [...其他]，按一下 [新增資料集]，然後選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="9bae9-195">複製下列程式碼片段並貼到 [Draft-1] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9bae9-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="9bae9-196">JSON 程式碼片段會定義名為 **OutputDataset** 的資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="9bae9-197">此外，指定將結果儲存在名為 **adfspark** 的 Blob 容器及名為 **pyFiles/output** 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9bae9-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="9bae9-198">如先前所述，此資料集是空的資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="9bae9-199">此範例中的 Spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9bae9-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="9bae9-200">**availability** 區段指定每日產生一次輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="9bae9-201">若要部署資料集，請按一下命令列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="9bae9-202">建立管線</span><span class="sxs-lookup"><span data-stu-id="9bae9-202">Create pipeline</span></span>
<span data-ttu-id="9bae9-203">在此步驟中，您會建立具有 **HDInsightSpark** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="9bae9-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="9bae9-204">目前，輸出資料集會影響排程，因此即使活動並未產生任何輸出，您都必須建立輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="9bae9-205">如果活動沒有任何輸入，您可以略過建立輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="9bae9-206">因此，在此範例中不會指定任何輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="9bae9-207">在 **Data Factory 編輯器**中，按一下工具列的 [... 更多]，然後按一下 [新增資料閘道]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="9bae9-208">使用下列指令碼取代 Draft-1 視窗中的指令碼：</span><span class="sxs-lookup"><span data-stu-id="9bae9-208">Replace the script in the Draft-1 window with the following script:</span></span>

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
    <span data-ttu-id="9bae9-209">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="9bae9-209">Note the following points:</span></span>
    - <span data-ttu-id="9bae9-210">**type** 屬性會設為 **HDInsightSpark**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="9bae9-211">**rootPath** 會設為 **adfspark\\pyFiles**，其中 adfspark 是 Azure Blob 容器，而 pyFiles 是該容器中的正常資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="9bae9-212">在此範例中，Azure Blob 儲存體是與 Spark 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9bae9-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="9bae9-213">您可以將檔案上傳至不同的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9bae9-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="9bae9-214">如果您這麼做，請建立 Azure 儲存體連結服務，以將該儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9bae9-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="9bae9-215">然後，將連結服務的名稱指定為 **sparkJobLinkedService** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="9bae9-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="9bae9-216">如需此屬性和 Spark 活動所支援的其他屬性詳細資訊，請參閱 [Spark 活動屬性](#spark-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="9bae9-217">**entryFilePath** 會設為 **test.py**，這就是 python 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bae9-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="9bae9-218">**getDebugInfo** 屬性會設為 **Always**，表示永遠產生記錄檔 (不論成功或失敗)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="9bae9-219">我們建議您不要在生產環境中將這個屬性設定為 `Always`，除非您要針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9bae9-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="9bae9-220">**outputs** 區段有一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="9bae9-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="9bae9-221">您必須指定輸出資料集，即使 Spark 程式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9bae9-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="9bae9-222">輸出資料集可以驅動管線的排程 (每小時、每天等)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="9bae9-223">如需 Spark 活動所支援之屬性的詳細資訊，請參閱 [Spark 活動屬性](#spark-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="9bae9-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="9bae9-224">若要部署管線，按一下命令列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="9bae9-225">監視管線</span><span class="sxs-lookup"><span data-stu-id="9bae9-225">Monitor pipeline</span></span>
1. <span data-ttu-id="9bae9-226">按一下 **X** 以關閉 [Data Factory 編輯器] 刀鋒視窗，以及瀏覽回 [Data Factory] 首頁。</span><span class="sxs-lookup"><span data-stu-id="9bae9-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="9bae9-227">按一下 [監視及管理] 在另一個索引標籤中啟動監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bae9-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![監視及管理圖格](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="9bae9-229">將頂端的 [開始時間] 篩選變更為 **2/1/2017**，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="9bae9-230">因為管線的開始 (2017-02-01) 與結束時間 (2017-02-02) 之間只有一天，您應該只會看到一個活動時段。</span><span class="sxs-lookup"><span data-stu-id="9bae9-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="9bae9-231">確認資料配量為 [就緒] 狀態。</span><span class="sxs-lookup"><span data-stu-id="9bae9-231">Confirm that the data slice is in **ready** state.</span></span>

    ![監視管線](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="9bae9-233">選取 [活動視窗] 以查看關於活動執行的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9bae9-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="9bae9-234">如果發生錯誤，您會在右窗格中看到它的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9bae9-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="9bae9-235">驗證結果</span><span class="sxs-lookup"><span data-stu-id="9bae9-235">Verify the results</span></span>

1. <span data-ttu-id="9bae9-236">瀏覽至 https://CLUSTERNAME.azurehdinsight.net/jupyter，啟動您的 HDInsight Spark 叢集的 **Jupyter Notebook**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="9bae9-237">您可以為 HDInsight Spark 叢集啟動叢集儀表板，然後啟動 **Jupyter Notebook**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="9bae9-238">按一下 [新增] -> [PySpark] 來啟動新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="9bae9-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Jupyter 新筆記本](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="9bae9-240">在第二個陳述式的結尾複製/貼上文字，並按下 **SHIFT + ENTER** 來執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="9bae9-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="9bae9-241">確認您看到來自 hvac 資料表的資料：</span><span class="sxs-lookup"><span data-stu-id="9bae9-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Jupyter 查詢結果](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="9bae9-243">如需詳細指示，請參閱[執行 Spark SQL 查詢](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql)區段。</span><span class="sxs-lookup"><span data-stu-id="9bae9-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="9bae9-244">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9bae9-244">Troubleshooting</span></span>
<span data-ttu-id="9bae9-245">因為您將 **getDebugInfo** 設定為 **Always**，您會在 Azure Blob 容器的 **pyFiles** 資料夾中看到一個 **log** 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="9bae9-246">log 資料夾中的記錄檔會提供其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9bae9-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="9bae9-247">發生錯誤時，此記錄檔特別有用。</span><span class="sxs-lookup"><span data-stu-id="9bae9-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="9bae9-248">在生產環境中，您可能想要將它設定為**失敗**。</span><span class="sxs-lookup"><span data-stu-id="9bae9-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="9bae9-249">如需進一步的疑難排解，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9bae9-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="9bae9-250">瀏覽至 `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`。</span><span class="sxs-lookup"><span data-stu-id="9bae9-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI 應用程式](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="9bae9-252">按一下其中一個執行嘗試的 [記錄]。</span><span class="sxs-lookup"><span data-stu-id="9bae9-252">Click **Logs** for one of the run attempts.</span></span>

    ![應用程式頁面](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="9bae9-254">您應該會在記錄頁面中看到其他的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="9bae9-254">You should see additional error information in the log page.</span></span>

    ![記錄錯誤](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="9bae9-256">下列各節提供 Data Factory 實體的相關資訊，以在您的資料處理站中使用 Apache Spark 叢集和 Spark 活動。</span><span class="sxs-lookup"><span data-stu-id="9bae9-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="9bae9-257">Spark 活動屬性</span><span class="sxs-lookup"><span data-stu-id="9bae9-257">Spark activity properties</span></span>
<span data-ttu-id="9bae9-258">以下是使用 Spark 活動之管線的 JSON 定義範例：</span><span class="sxs-lookup"><span data-stu-id="9bae9-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="9bae9-259">下表說明 JSON 定義中使用的 JSON 屬性：</span><span class="sxs-lookup"><span data-stu-id="9bae9-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="9bae9-260">屬性</span><span class="sxs-lookup"><span data-stu-id="9bae9-260">Property</span></span> | <span data-ttu-id="9bae9-261">說明</span><span class="sxs-lookup"><span data-stu-id="9bae9-261">Description</span></span> | <span data-ttu-id="9bae9-262">必要</span><span class="sxs-lookup"><span data-stu-id="9bae9-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="9bae9-263">名稱</span><span class="sxs-lookup"><span data-stu-id="9bae9-263">name</span></span> | <span data-ttu-id="9bae9-264">管線中的活動名稱。</span><span class="sxs-lookup"><span data-stu-id="9bae9-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="9bae9-265">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-265">Yes</span></span> |
| <span data-ttu-id="9bae9-266">說明</span><span class="sxs-lookup"><span data-stu-id="9bae9-266">description</span></span> | <span data-ttu-id="9bae9-267">說明活動用途的文字。</span><span class="sxs-lookup"><span data-stu-id="9bae9-267">Text describing what the activity does.</span></span> | <span data-ttu-id="9bae9-268">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-268">No</span></span> |
| <span data-ttu-id="9bae9-269">類型</span><span class="sxs-lookup"><span data-stu-id="9bae9-269">type</span></span> | <span data-ttu-id="9bae9-270">這個屬性必須設為 HDInsightSpark。</span><span class="sxs-lookup"><span data-stu-id="9bae9-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="9bae9-271">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-271">Yes</span></span> |
| <span data-ttu-id="9bae9-272">預設容器</span><span class="sxs-lookup"><span data-stu-id="9bae9-272">linkedServiceName</span></span> | <span data-ttu-id="9bae9-273">Spark 程式執行所在的 HDInsight 連結服務名稱。</span><span class="sxs-lookup"><span data-stu-id="9bae9-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="9bae9-274">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-274">Yes</span></span> |
| <span data-ttu-id="9bae9-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="9bae9-275">rootPath</span></span> | <span data-ttu-id="9bae9-276">Spark 檔案所在的 Azure Blob 容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="9bae9-277">檔案名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="9bae9-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="9bae9-278">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-278">Yes</span></span> |
| <span data-ttu-id="9bae9-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="9bae9-279">entryFilePath</span></span> | <span data-ttu-id="9bae9-280">Spark 程式碼/套件之根資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="9bae9-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="9bae9-281">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-281">Yes</span></span> |
| <span data-ttu-id="9bae9-282">className</span><span class="sxs-lookup"><span data-stu-id="9bae9-282">className</span></span> | <span data-ttu-id="9bae9-283">應用程式的 Java/Spark 主要類別</span><span class="sxs-lookup"><span data-stu-id="9bae9-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="9bae9-284">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-284">No</span></span> |
| <span data-ttu-id="9bae9-285">arguments</span><span class="sxs-lookup"><span data-stu-id="9bae9-285">arguments</span></span> | <span data-ttu-id="9bae9-286">Spark 程式的命令列引數清單。</span><span class="sxs-lookup"><span data-stu-id="9bae9-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="9bae9-287">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-287">No</span></span> |
| <span data-ttu-id="9bae9-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="9bae9-288">proxyUser</span></span> | <span data-ttu-id="9bae9-289">模擬來執行 Spark 程式的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="9bae9-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="9bae9-290">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-290">No</span></span> |
| <span data-ttu-id="9bae9-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="9bae9-291">sparkConfig</span></span> | <span data-ttu-id="9bae9-292">指定下列主題中所列的 Spark 組態屬性值：[Spark 組態 - 應用程式屬性](https://spark.apache.org/docs/latest/configuration.html#available-properties) (英文)。</span><span class="sxs-lookup"><span data-stu-id="9bae9-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="9bae9-293">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-293">No</span></span> |
| <span data-ttu-id="9bae9-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="9bae9-294">getDebugInfo</span></span> | <span data-ttu-id="9bae9-295">指定何時將 Spark 記錄檔複製到 HDInsight 叢集所使用 (或) sparkJobLinkedService 所指定的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9bae9-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="9bae9-296">允許的值︰None、Always 或 Failure。</span><span class="sxs-lookup"><span data-stu-id="9bae9-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="9bae9-297">預設值：None。</span><span class="sxs-lookup"><span data-stu-id="9bae9-297">Default value: None.</span></span> | <span data-ttu-id="9bae9-298">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-298">No</span></span> |
| <span data-ttu-id="9bae9-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="9bae9-299">sparkJobLinkedService</span></span> | <span data-ttu-id="9bae9-300">存放 Spark 作業檔案、相依性和記錄的 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="9bae9-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="9bae9-301">如果您未指定此屬性的值，則會使用與 HDInsight 叢集相關聯的儲存體。</span><span class="sxs-lookup"><span data-stu-id="9bae9-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="9bae9-302">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="9bae9-303">資料夾結構</span><span class="sxs-lookup"><span data-stu-id="9bae9-303">Folder structure</span></span>
<span data-ttu-id="9bae9-304">不同於 Pig 和 Hive 活動，Spark 活動不支援內嵌指令碼。</span><span class="sxs-lookup"><span data-stu-id="9bae9-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="9bae9-305">Spark 作業也比 Pig/Hive 作業更具擴充性。</span><span class="sxs-lookup"><span data-stu-id="9bae9-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="9bae9-306">對於 Spark 作業，您可以提供多個相依性，例如 jar 套件 (置於 java CLASSPATH)、python 檔案 (置於 PYTHONPATH) 和任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="9bae9-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="9bae9-307">在 HDInsight 連結服務所參考的 Azure Blob 儲存體中，建立下列資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="9bae9-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="9bae9-308">然後，將相依檔案上傳至根資料夾中以 **entryFilePath** 表示的適當子資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="9bae9-309">比方說，將 python 檔案上傳至根資料夾的 pyFiles 子資料夾，將 jar 檔案上傳至 jars 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bae9-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="9bae9-310">在執行階段，Data Factory 服務會預期 Azure Blob 儲存體中有下列資料夾結構︰</span><span class="sxs-lookup"><span data-stu-id="9bae9-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="9bae9-311">路徑</span><span class="sxs-lookup"><span data-stu-id="9bae9-311">Path</span></span> | <span data-ttu-id="9bae9-312">說明</span><span class="sxs-lookup"><span data-stu-id="9bae9-312">Description</span></span> | <span data-ttu-id="9bae9-313">必要</span><span class="sxs-lookup"><span data-stu-id="9bae9-313">Required</span></span> | <span data-ttu-id="9bae9-314">類型</span><span class="sxs-lookup"><span data-stu-id="9bae9-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="9bae9-315">。</span><span class="sxs-lookup"><span data-stu-id="9bae9-315">.</span></span> | <span data-ttu-id="9bae9-316">Spark 作業在儲存體連結服務中的根路徑</span><span class="sxs-lookup"><span data-stu-id="9bae9-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="9bae9-317">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-317">Yes</span></span> | <span data-ttu-id="9bae9-318">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-318">Folder</span></span> |
| <span data-ttu-id="9bae9-319">&lt;使用者定義&gt;</span><span class="sxs-lookup"><span data-stu-id="9bae9-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="9bae9-320">指向 Spark 作業輸入檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="9bae9-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="9bae9-321">是</span><span class="sxs-lookup"><span data-stu-id="9bae9-321">Yes</span></span> | <span data-ttu-id="9bae9-322">檔案</span><span class="sxs-lookup"><span data-stu-id="9bae9-322">File</span></span> |
| <span data-ttu-id="9bae9-323">./jars</span><span class="sxs-lookup"><span data-stu-id="9bae9-323">./jars</span></span> | <span data-ttu-id="9bae9-324">此資料夾下的所有檔案會上傳並放在叢集的 java 類別路徑</span><span class="sxs-lookup"><span data-stu-id="9bae9-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="9bae9-325">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-325">No</span></span> | <span data-ttu-id="9bae9-326">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-326">Folder</span></span> |
| <span data-ttu-id="9bae9-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="9bae9-327">./pyFiles</span></span> | <span data-ttu-id="9bae9-328">此資料夾下的所有檔案會上傳並放在叢集的 PYTHONPATH</span><span class="sxs-lookup"><span data-stu-id="9bae9-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="9bae9-329">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-329">No</span></span> | <span data-ttu-id="9bae9-330">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-330">Folder</span></span> |
| <span data-ttu-id="9bae9-331">./files</span><span class="sxs-lookup"><span data-stu-id="9bae9-331">./files</span></span> | <span data-ttu-id="9bae9-332">此資料夾下的所有檔案會上傳並放在執行程式工作目錄</span><span class="sxs-lookup"><span data-stu-id="9bae9-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="9bae9-333">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-333">No</span></span> | <span data-ttu-id="9bae9-334">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-334">Folder</span></span> |
| <span data-ttu-id="9bae9-335">./archives</span><span class="sxs-lookup"><span data-stu-id="9bae9-335">./archives</span></span> | <span data-ttu-id="9bae9-336">此資料夾下的所有檔案未壓縮</span><span class="sxs-lookup"><span data-stu-id="9bae9-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="9bae9-337">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-337">No</span></span> | <span data-ttu-id="9bae9-338">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-338">Folder</span></span> |
| <span data-ttu-id="9bae9-339">./logs</span><span class="sxs-lookup"><span data-stu-id="9bae9-339">./logs</span></span> | <span data-ttu-id="9bae9-340">此資料夾儲存來自 Spark 叢集的記錄。</span><span class="sxs-lookup"><span data-stu-id="9bae9-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="9bae9-341">否</span><span class="sxs-lookup"><span data-stu-id="9bae9-341">No</span></span> | <span data-ttu-id="9bae9-342">資料夾</span><span class="sxs-lookup"><span data-stu-id="9bae9-342">Folder</span></span> |

<span data-ttu-id="9bae9-343">以下是 HDInsight 連結服務所參考的 Azure Blob 儲存體中，含有兩個 Spark 作業檔案的儲存體範例。</span><span class="sxs-lookup"><span data-stu-id="9bae9-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

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
