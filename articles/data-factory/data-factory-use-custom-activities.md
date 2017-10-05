---
title: "在 Azure 資料處理站管線中使用自訂活動"
description: "了解如何建立自訂活動，並在 Azure 資料處理站管線中使用這些活動。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="88d1a-103">在 Azure 資料處理站管線中使用自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="88d1a-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="88d1a-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="88d1a-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="88d1a-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="88d1a-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="88d1a-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="88d1a-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="88d1a-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="88d1a-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="88d1a-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="88d1a-114">您可以在 Azure Data Factory 管線中使用兩種活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="88d1a-115">[資料移動活動](data-factory-data-movement-activities.md)，可在[支援的來源與接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="88d1a-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="88d1a-116">使用 Azure HDInsight、Azure Batch 及 Azure Machine Learning 等計算服務來轉換資料的[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="88d1a-117">如果要移動資料至/自 Data Factory 不支援的資料存放區，利用自己的資料移動邏輯建立**自訂活動**，然後在管線中使用活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="88d1a-118">同樣地，若要以 Data Factory 不支援的方法轉換/處理資料，可以利用自己的資料轉換邏輯建立自訂活動，然後在管線中使用活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="88d1a-119">您可以將自訂活動設定為在虛擬機器的 **Azure Batch** 集區或 Windows 架構的 **Azure HDInsight** 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="88d1a-120">當使用 Azure Batch 時，您只可以使用現有的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="88d1a-121">然而，使用 HDInsight 時，您可以使用現有的 HDInsight 叢集或針對您在執行階段的隨選自動建立叢集。</span><span class="sxs-lookup"><span data-stu-id="88d1a-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="88d1a-122">下列逐步解說提供建立自訂 .NET 活動以及在管線中使用自訂活動的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="88d1a-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="88d1a-123">本逐步解說使用 **Azure Batch** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="88d1a-124">若要改用 Azure HDInsight 連結服務，建立型別 **HDInsight** 的連結服務 (您自己的 HDInsight 叢集) 或 **HDInsightOnDemand** (Data Factory 會隨選建立 HDInsight 叢集)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="88d1a-125">然後，設定自訂的活動以使用 HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="88d1a-126">如需使用 Azure HDInsight 來執行自訂活動的詳細資料，請參閱 [使用 Azure HDInsight 連結服務](#use-hdinsight-compute-service) 一節。</span><span class="sxs-lookup"><span data-stu-id="88d1a-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="88d1a-127">自訂的 .NET 活動只會在 Windows 架構的 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="88d1a-128">這項限制的因應措施是使用 Map Reduce 活動以在 Linux 架構的 HDInsight 叢集上執行自訂的 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="88d1a-129">另一個選項是使用 VM 的 Azure Batch 集區來執行自訂活動，而非使用 HDInsight 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="88d1a-130">您不能使用自訂活動中的資料管理閘道來存取內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="88d1a-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="88d1a-131">目前在 Data Factory 中，[資料管理閘道](data-factory-data-management-gateway.md)只支援複製活動和預存程序活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="88d1a-132">逐步解說：建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="88d1a-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="88d1a-133">Prerequisites</span></span>
* <span data-ttu-id="88d1a-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="88d1a-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="88d1a-135">下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="88d1a-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="88d1a-136">Azure Batch 的必要條件</span><span class="sxs-lookup"><span data-stu-id="88d1a-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="88d1a-137">在逐步解說中，您會將 Azure Batch 當作計算資源使用來執行自訂 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="88d1a-138">**Azure Batch** 是一項平台服務，可用於在雲端有效地執行大規模的平行和高效能運算 (HPC) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88d1a-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="88d1a-139">Azure Batch 可排程要在**一組受管理的虛擬機器**上執行的計算密集型工作，而且可以調整計算資源以符合工作的需求。</span><span class="sxs-lookup"><span data-stu-id="88d1a-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="88d1a-140">請參閱 [Azure Batch 基本知識][batch-technical-overview]文章，以取得 Azure Batch 服務的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="88d1a-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="88d1a-141">在教學課程中，建立含 VM 集區的 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="88d1a-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="88d1a-142">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="88d1a-142">Here are the steps:</span></span>

1. <span data-ttu-id="88d1a-143">使用 **Azure 入口網站** 建立 [Azure Batch 帳戶](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="88d1a-144">請參閱[建立和管理 Azure Batch 帳戶][batch-create-account]一文以取得指示。</span><span class="sxs-lookup"><span data-stu-id="88d1a-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="88d1a-145">記下 Azure Batch 帳戶名稱、帳戶金鑰、URI，以及集區名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="88d1a-146">您需要它們來建立 Azure Batch 連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="88d1a-147">在 Azure Batch 帳戶首頁上，您會看到一串 URL 為下列格式︰`https://myaccount.westus.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="88d1a-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="88d1a-148">在此範例中，**myaccount** 是 Azure Batch 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="88d1a-149">您在連結服務的定義中使用之 URI 是不含帳戶名稱的 URL。</span><span class="sxs-lookup"><span data-stu-id="88d1a-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="88d1a-150">例如： `https://<region>.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="88d1a-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="88d1a-151">在左窗格上按一下 [金鑰]，然後複製**主要存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="88d1a-152">若要使用現有的集區，在功能表上按一下 [集區]，記下集區的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="88d1a-153">如果您沒有現有的集區，請移至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="88d1a-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="88d1a-154">建立 **Azure Batch 集區**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="88d1a-155">在 [Azure 入口網站](https://portal.azure.com)中，按一下左側功能標中的 [瀏覽]，然後按一下 [Batch 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="88d1a-156">選取您的 Azure Batch 帳戶，以開啟 [Batch 帳戶]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88d1a-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="88d1a-157">按一下 [集區]  圖格。</span><span class="sxs-lookup"><span data-stu-id="88d1a-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="88d1a-158">在 [集區]  刀鋒視窗中，按一下工具列上的 [新增] 按鈕以新增集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="88d1a-159">輸入集區的識別碼 (集區識別碼)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="88d1a-160">請注意 **集區的識別碼**；您在建立 Data Factory 解決方案時需要它。</span><span class="sxs-lookup"><span data-stu-id="88d1a-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="88d1a-161">指定作業系統系列設定的 **Windows Server 2012 R2** 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="88d1a-162">選取 **節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="88d1a-163">輸入 **2** 做為 [目標專用] 設定的值。</span><span class="sxs-lookup"><span data-stu-id="88d1a-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="88d1a-164">輸入 **2** 做為 [每個節點的工作上限] 設定的值。</span><span class="sxs-lookup"><span data-stu-id="88d1a-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="88d1a-165">按一下 [確定]  以建立集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="88d1a-166">記下集區的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="88d1a-167">高階步驟</span><span class="sxs-lookup"><span data-stu-id="88d1a-167">High-level steps</span></span>
<span data-ttu-id="88d1a-168">以下是您在此逐步解說中執行的兩個高階步驟︰</span><span class="sxs-lookup"><span data-stu-id="88d1a-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="88d1a-169">建立包含簡單資料轉換/處理邏輯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="88d1a-170">透過使用自訂活動的管線建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="88d1a-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="88d1a-171">建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-171">Create a custom activity</span></span>
<span data-ttu-id="88d1a-172">若要建立 .NET 自訂活動，您必須利用實作 **IDotNetActivity** 介面的類別建立 **.NET 類別庫**專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="88d1a-173">這個介面只有一個方法： [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) ，其簽章為：</span><span class="sxs-lookup"><span data-stu-id="88d1a-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="88d1a-174">此方法會採用四個參數：</span><span class="sxs-lookup"><span data-stu-id="88d1a-174">The method takes four parameters:</span></span>

- <span data-ttu-id="88d1a-175">**linkedServices**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-175">**linkedServices**.</span></span> <span data-ttu-id="88d1a-176">這個屬性是活動之輸入/輸出資料集所參考的資料存放區連結服務的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="88d1a-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="88d1a-177">**資料集**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-177">**datasets**.</span></span> <span data-ttu-id="88d1a-178">這個屬性是活動之輸入/輸出資料集的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="88d1a-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="88d1a-179">您可以使用這個參數取得輸入和輸出資料集定義的位置和結構描述。</span><span class="sxs-lookup"><span data-stu-id="88d1a-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="88d1a-180">**活動**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-180">**activity**.</span></span> <span data-ttu-id="88d1a-181">這個屬性表示目前的活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-181">This property represents the current activity.</span></span> <span data-ttu-id="88d1a-182">它可以用來存取與自訂活動相關聯的延伸屬性。</span><span class="sxs-lookup"><span data-stu-id="88d1a-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="88d1a-183">如需詳細資訊，請參閱[存取延伸屬性](#access-extended-properties)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="88d1a-184">**記錄器**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-184">**logger**.</span></span> <span data-ttu-id="88d1a-185">此物件可讓您撰寫會呈現為管線的使用者記錄檔的偵錯註解。</span><span class="sxs-lookup"><span data-stu-id="88d1a-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="88d1a-186">此方法會傳回未來可用來將自訂活動鏈結在一起的字典。</span><span class="sxs-lookup"><span data-stu-id="88d1a-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="88d1a-187">尚未實作這項功能，因此會從方法傳回空的字典。</span><span class="sxs-lookup"><span data-stu-id="88d1a-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="88d1a-188">程序</span><span class="sxs-lookup"><span data-stu-id="88d1a-188">Procedure</span></span>
1. <span data-ttu-id="88d1a-189">建立 **.NET 類別庫** 專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="88d1a-190">啟動 <b>Visual Studio 2017</b> 或 <b>Visual Studio 2015</b> 或 <b>Visual Studio 2013</b> 或 <b>Visual Studio 2012</b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="88d1a-191">按一下 [檔案]<b></b>，指向 [新增]<b></b>，然後按一下 [專案]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="88d1a-192">展開 [範本]<b></b>，然後選取 [Visual C#]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="88d1a-193">在此逐步解說中，您使用 C# 中，但您可以使用任何 .NET 語言來開發自訂活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="88d1a-194">從右邊的專案類型清單中選取 [類別庫]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="88d1a-195">在 VS 2017 中，選擇 <b>類別庫 (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="88d1a-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="88d1a-196">在 [名稱]<b></b> 輸入 <b>MyDotNetActivity</b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="88d1a-197">在 [位置]<b></b> 選取 <b>C:\ADFGetStarted</b>。</span><span class="sxs-lookup"><span data-stu-id="88d1a-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="88d1a-198">按一下 [確定] <b></b> 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="88d1a-199">
2. 按一下 **[工具]** ，指向 **[NuGet 封裝管理員]** ，然後按一下 **[封裝管理員主控台]** 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="88d1a-200">3.</span><span class="sxs-lookup"><span data-stu-id="88d1a-200">3.</span></span> <span data-ttu-id="88d1a-201">在 [封裝管理員主控台] 中，執行下列命令以匯入 **Microsoft.Azure.Management.DataFactories**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="88d1a-202">將 **Azure 儲存體** NuGet 封裝匯入專案中。</span><span class="sxs-lookup"><span data-stu-id="88d1a-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="88d1a-203">Data Factory 服務啟動程式需要 4.3 版的 WindowsAzure.Storage。</span><span class="sxs-lookup"><span data-stu-id="88d1a-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="88d1a-204">如果您在自訂活動專案中新增新版的 Azure 儲存體組件的參考，當活動執行時會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="88d1a-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="88d1a-205">若要解決這個錯誤，請參閱[ Appdomain 隔離](#appdomain-isolation)小節。</span><span class="sxs-lookup"><span data-stu-id="88d1a-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="88d1a-206">將下列 **using** 陳述式加入至專案的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="88d1a-206">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="88d1a-207">將 **namespace** 的名稱變更為 **MyDotNetActivityNS**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="88d1a-208">將類別的名稱變更為 **MyDotNetActivity**，並從 **IDotNetActivity** 介面衍生它，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="88d1a-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="88d1a-209">對 **MyDotNetActivity** 類別實作 (新增) **IDotNetActivity** 介面的 **Execute** 方法，並將下列範例程式碼複製到方法。</span><span class="sxs-lookup"><span data-stu-id="88d1a-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="88d1a-210">下列範例會在每個與資料配量相關聯之 Blob 中計算搜尋詞彙 ("Microsoft") 的出現次數。</span><span class="sxs-lookup"><span data-stu-id="88d1a-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="88d1a-211">新增下列 Helper 方法：</span><span class="sxs-lookup"><span data-stu-id="88d1a-211">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="88d1a-212">GetFolderPath 方法會將路徑傳回資料集所指向的資料夾，而 GetFileName 方法會傳回資料集指向的 blob/檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="88d1a-213">如果您的 havefolderPath 定義使用如 {Year}、{Month}、{Day} 等變數，方法會以未將變數取代為執行階段值的形式傳回字串。</span><span class="sxs-lookup"><span data-stu-id="88d1a-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="88d1a-214">如需存取 SliceStart、SliceEnd 等的詳細資料，請參閱 [存取延伸屬性](#access-extended-properties) 一節。</span><span class="sxs-lookup"><span data-stu-id="88d1a-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="88d1a-215">Calculate 方法會在輸入檔案 (資料夾中的 blob) 計算關鍵字 Microsoft 的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="88d1a-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="88d1a-216">搜尋詞彙 ("Microsoft") 已在程式碼中硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="88d1a-217">編譯專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-217">Compile the project.</span></span> <span data-ttu-id="88d1a-218">按一下功能表中的 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="88d1a-219">將 .NET Framework 4.5.2 版設定為您專案的目標架構：在專案上按一下滑鼠右鍵，然後按一下 [屬性] 來設定目標架構。</span><span class="sxs-lookup"><span data-stu-id="88d1a-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="88d1a-220">Data Factory 不支援針對 .NET Framework 4.5.2 版之後的版本編譯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="88d1a-221">啟動 [Windows 檔案總管]，瀏覽至 **bin\debug** 或 **bin\release** 資料夾，視建置類型而定。</span><span class="sxs-lookup"><span data-stu-id="88d1a-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="88d1a-222">建立 zip 檔案 **MyDotNetActivity.zip**，檔案中包含 <project folder>\bin\Debug 資料夾中的所有二進位檔。</span><span class="sxs-lookup"><span data-stu-id="88d1a-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="88d1a-223">新增 **MyDotNetActivity.pdb** 檔案，讓您可以取得額外的詳細資訊，例如如果有失敗時，原始程式碼中引起問題的程式碼行號。</span><span class="sxs-lookup"><span data-stu-id="88d1a-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="88d1a-224">自訂活動之 zip 檔案中的所有檔案都必須位於 **最上層** 且不包含任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="88d1a-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![二進位輸出檔案](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="88d1a-226">如果名為 **customactivitycontainer** 的 Blob 容器不存在，請自行建立。</span><span class="sxs-lookup"><span data-stu-id="88d1a-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="88d1a-227">將 MyDotNetActivity.zip 作為 blob，上傳至 AzureStorageLinkedService 所參照之**一般用途** Azure Blob 儲存體 (而不是經常性/非經常性 Blob 儲存體) 中的 customactivitycontainer。</span><span class="sxs-lookup"><span data-stu-id="88d1a-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="88d1a-228">如果您將這個 .NET 活動專案加入 Visual Studio 中包含 Data Factory 專案的方案，並從 Data Factory 應用程式專案加入 .NET 活動的參考，您就不需要執行最後兩個步驟，也就是建立 zip 檔案，和手動上傳到一般用途 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="88d1a-229">當您使用 Visual Studio 發佈 Data Factory 實體時，發佈程序會自動完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="88d1a-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="88d1a-230">如需詳細資訊，請參閱[Visual Studio 中的 Data Factory 專案](#data-factory-project-in-visual-studio)一節。</span><span class="sxs-lookup"><span data-stu-id="88d1a-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="88d1a-231">建立具有自訂活動的管線</span><span class="sxs-lookup"><span data-stu-id="88d1a-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="88d1a-232">您已建立自訂活動，並將二進位檔的 zip 檔案上傳至**一般用途** Azure 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="88d1a-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="88d1a-233">在本節中，您將透過使用自訂活動的管線建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="88d1a-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="88d1a-234">自訂活動的輸入資料集代表 blob 儲存體中 adftutorial 容器之 customactivityinput 資料夾中的輸入 blob (檔案)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="88d1a-235">活動的輸出資料集代表 blob 儲存體中 adftutorial 容器之 customactivityinput 資料夾中的輸出 blob。</span><span class="sxs-lookup"><span data-stu-id="88d1a-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="88d1a-236">以下列內容建立 **file.txt** 檔案，然後將它上傳至 **adftutorial** 容器的 **customactivityinput** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="88d1a-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="88d1a-237">建立 adftutorial 容器 (如果尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="88d1a-238">即使資料夾有 2 個以上的檔案，輸入資料夾還是會對應至 Azure Data Factory 中的配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="88d1a-239">管線處理每個配量時，自訂活動會為該配量逐一查看輸入資料夾中的所有 blob。</span><span class="sxs-lookup"><span data-stu-id="88d1a-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="88d1a-240">您會看到 adftutorial\customactivityoutput 資料夾中的一個輸出檔案具有 1 行或更多行 (和輸入資料夾中的 blob 數目相同)：</span><span class="sxs-lookup"><span data-stu-id="88d1a-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="88d1a-241">以下是您會在此節中執行的步驟：</span><span class="sxs-lookup"><span data-stu-id="88d1a-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="88d1a-242">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="88d1a-243">建立自訂活動執行所在之 Azure Batch VM 集區的連結服務，以及容納輸入/輸出 Blob 之 Azure 儲存體的**連結服務**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="88d1a-244">建立輸入和輸出**資料集**，代表自訂活動的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="88d1a-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="88d1a-245">建立使用自訂活動的**管線**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="88d1a-246">建立 **file.txt** 並上傳到 Blob 容器 (如果您尚未完成)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="88d1a-247">請參閱上一節中的指示。</span><span class="sxs-lookup"><span data-stu-id="88d1a-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="88d1a-248">步驟 1：建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="88d1a-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="88d1a-249">登入 Azure 入口網站之後，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="88d1a-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="88d1a-250">按一下左側功能表上的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="88d1a-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="88d1a-251">按一下 [新增] 刀鋒視窗中的 [資料 + 分析]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="88d1a-252">按一下 [資料分析] 刀鋒視窗上的 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![新增 Azure Data Factory 功能表](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="88d1a-254">在 [新增 Data Factory] 刀鋒視窗中，輸入 **CustomActivityFactor** 做為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="88d1a-255">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="88d1a-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="88d1a-256">如果您收到錯誤：**Data Factory 名稱 “CustomActivityFactory” 無法使用**，請變更 Data Factory 名稱 (例如 **yournameCustomActivityFactory**)，然後試著重新建立。</span><span class="sxs-lookup"><span data-stu-id="88d1a-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![新增 Azure Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="88d1a-258">按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。</span><span class="sxs-lookup"><span data-stu-id="88d1a-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="88d1a-259">請確認您使用的是要在其中建立 Data Factory 的正確**訂用帳戶**和**區域**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="88d1a-260">按一下 [新增 Data Factory] 刀鋒視窗上的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="88d1a-261">您會看到 Data Factory 建立在 Azure 入口網站的 [儀表板]  中。</span><span class="sxs-lookup"><span data-stu-id="88d1a-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="88d1a-262">在 Data Factory 成功建立後，您會看到 Data Factory 刀鋒視窗，顯示 Data Factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="88d1a-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="88d1a-264">步驟 2：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="88d1a-264">Step 2: Create linked services</span></span>
<span data-ttu-id="88d1a-265">連結服務會將資料存放區或計算服務連結至 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="88d1a-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="88d1a-266">在此步驟中，您會將 Azure 儲存體帳戶和 Azure Batch 帳戶連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="88d1a-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="88d1a-267">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="88d1a-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="88d1a-268">按一下 **CustomActivityFactory** 的 [DATA FACTORY] 刀鋒視窗上的 [作者和部署] 圖格。</span><span class="sxs-lookup"><span data-stu-id="88d1a-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="88d1a-269">您會看到 [Data Factory 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="88d1a-270">在命令列上按一下 [新增資料儲存區]，然後選擇 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="88d1a-271">在編輯器中，您應該會看到用來建立 Azure 儲存體連結服務的 JSON 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![新增資料存放區 - Azure 儲存體](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="88d1a-273">以您的 Azure 儲存體帳戶名稱取代`<accountname>`，並以 Azure 儲存體帳戶的存取金鑰取代`<accountkey>`。</span><span class="sxs-lookup"><span data-stu-id="88d1a-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="88d1a-274">若要了解如何取得儲存體存取金鑰，請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="88d1a-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure 儲存體類型的連結服務](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="88d1a-276">按一下命令列的 [部署]  ，部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="88d1a-277">建立 Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="88d1a-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="88d1a-278">在 [Data Factory 編輯器] 中，按一下工具列上的 [...**其他]**，按一下 [新增計算]，然後從功能表選取 [Azure 批次]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![[新增計算]-[Azure 批次]](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="88d1a-280">對 JSON 指令碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="88d1a-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="88d1a-281">指定 **accountName** 屬性的 Azure Batch 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="88d1a-282">[Azure Batch 帳戶] 刀鋒視窗中的 **URL** 格式如下：`http://accountname.region.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="88d1a-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="88d1a-283">如果是 JSON 中的 **batchUri** 屬性，您需要移除 URL 中的 `accountname.`，並為 JSON 屬性使用 `accountname``accountName`。</span><span class="sxs-lookup"><span data-stu-id="88d1a-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="88d1a-284">指定 **accessKey** 屬性的 Azure Batch 帳戶金鑰 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="88d1a-285">針對為滿足 **poolName** 屬性之必要條件而建立的集區指定名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="88d1a-286">您也可以指定該集區的 ID，而非集區名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="88d1a-287">指定 **batchUri** 屬性的 Azure Batch URI。</span><span class="sxs-lookup"><span data-stu-id="88d1a-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="88d1a-288">範例：`https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="88d1a-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="88d1a-289">指定 **AzureStorageLinkedService** for the **linkedServiceName** 屬性的 Azure Batch 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="88d1a-290">針對 **poolName** 屬性，您也可以指定該集區的 ID，而非集區名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="88d1a-291">與支援 HDInsight 的情況不同，Data Factory 服務不支援 Azure Batch 的隨選選項。</span><span class="sxs-lookup"><span data-stu-id="88d1a-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="88d1a-292">您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="88d1a-293">步驟 3：建立資料集</span><span class="sxs-lookup"><span data-stu-id="88d1a-293">Step 3: Create datasets</span></span>
<span data-ttu-id="88d1a-294">在此步驟中，您會建立資料集來代表輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="88d1a-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="88d1a-295">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="88d1a-295">Create input dataset</span></span>
1. <span data-ttu-id="88d1a-296">在 Data Factory 的 [編輯器] 中，依序按一下下拉式功能表中的 **[...其他]**，按一下 [新增資料集]，然後從下拉式功能表選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="88d1a-297">使用下列 JSON 程式碼片段取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="88d1a-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="88d1a-298">您稍後會在本逐步解說建立管線，開始時間為：2016-11-16T00:00:00Z，而結束時間為：2016-11-16T05:00:00Z。</span><span class="sxs-lookup"><span data-stu-id="88d1a-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="88d1a-299">排程為每小時產生，因此會有 5 個輸入/輸出配量 (在 **00**:00:00 -> **05**:00:00 之間)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="88d1a-300">輸入資料集的 **frequency** 和 **interval** 設定為 **Hour** 和 **1**，這表示每小時皆可使用輸入配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="88d1a-301">在此範例中，它是 intputfolder 中的相同檔案 (file.txt)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="88d1a-302">以下是每個配量的開始時間，由上述 JSON 程式碼片段中的 SliceStart 系統變數代表。</span><span class="sxs-lookup"><span data-stu-id="88d1a-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="88d1a-303">按一下工具列的 [部署]，建立並部署 **InputDataset**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="88d1a-304">確認您在編輯器的標題列看到  [已成功建立資料表] 訊息。</span><span class="sxs-lookup"><span data-stu-id="88d1a-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="88d1a-305">建立輸出資料表</span><span class="sxs-lookup"><span data-stu-id="88d1a-305">Create an output dataset</span></span>
1. <span data-ttu-id="88d1a-306">在 [Data Factory 編輯器] 中，按一下命令列上的 [...**其他]**，按一下 [新增資料集]，然後選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="88d1a-307">使用下列 JSON 指令碼取代右窗格中的 JSON 指令碼：</span><span class="sxs-lookup"><span data-stu-id="88d1a-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="88d1a-308">輸出位置是 **adftutorial/customactivityoutput/** ，而輸出檔案名稱是 yyyy-MM-dd-HH.txt ，其中 yyyy-MM-dd-HH 是產生配量的年、月、日、時。</span><span class="sxs-lookup"><span data-stu-id="88d1a-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="88d1a-309">如需詳細資訊，請參閱[開發人員參考資料][adf-developer-reference]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="88d1a-310">為每個輸入配量產生輸出 blob/檔案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="88d1a-311">以下是為每個配量命名輸出檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="88d1a-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="88d1a-312">所有的輸出檔案會產生於一個輸出資料夾：**adftutorial\customactivityoutput**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="88d1a-313">配量</span><span class="sxs-lookup"><span data-stu-id="88d1a-313">Slice</span></span> | <span data-ttu-id="88d1a-314">開始時間</span><span class="sxs-lookup"><span data-stu-id="88d1a-314">Start time</span></span> | <span data-ttu-id="88d1a-315">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="88d1a-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="88d1a-316">1</span><span class="sxs-lookup"><span data-stu-id="88d1a-316">1</span></span> |<span data-ttu-id="88d1a-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="88d1a-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="88d1a-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="88d1a-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="88d1a-319">2</span><span class="sxs-lookup"><span data-stu-id="88d1a-319">2</span></span> |<span data-ttu-id="88d1a-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="88d1a-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="88d1a-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="88d1a-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="88d1a-322">3</span><span class="sxs-lookup"><span data-stu-id="88d1a-322">3</span></span> |<span data-ttu-id="88d1a-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="88d1a-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="88d1a-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="88d1a-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="88d1a-325">4</span><span class="sxs-lookup"><span data-stu-id="88d1a-325">4</span></span> |<span data-ttu-id="88d1a-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="88d1a-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="88d1a-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="88d1a-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="88d1a-328">5</span><span class="sxs-lookup"><span data-stu-id="88d1a-328">5</span></span> |<span data-ttu-id="88d1a-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="88d1a-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="88d1a-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="88d1a-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="88d1a-331">請記得輸入資料夾中的所有檔案都是包含上述開始時間之配量的一部分。</span><span class="sxs-lookup"><span data-stu-id="88d1a-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="88d1a-332">處理此配量時，自訂活動會掃描每個檔案，並利用搜尋詞彙 (“Microsoft”) 的出現次數在輸出檔案中產生資料行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="88d1a-333">如果 inputfolder 中有三個檔案，每小時的配量會有三行在輸出檔案中：2016-11-16-00.txt、2016-11-16:01:00:00.txt 等等。</span><span class="sxs-lookup"><span data-stu-id="88d1a-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="88d1a-334">若要部署 **OutputDataset**，按一下命令列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="88d1a-335">建立並執行使用自訂活動的管線</span><span class="sxs-lookup"><span data-stu-id="88d1a-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="88d1a-336">在 [Data Factory 編輯器] 中，按一下工具列上的 [...**其他]**，接著選擇命令列上的 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="88d1a-337">使用下列 JSON 指令碼取代右窗格中的 JSON︰</span><span class="sxs-lookup"><span data-stu-id="88d1a-337">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="88d1a-338">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="88d1a-338">Note the following points:</span></span>

   * <span data-ttu-id="88d1a-339">**Concurrency** 設定為 **2**，因此 Azure Batch 集區中會有 2 部 VM 以平行方式處理 2 個配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="88d1a-340">activities 區段中有一個活動，它的類型是： **DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="88d1a-341">**AssemblyName** 設定為 DLL 的名稱：**MyDotnetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="88d1a-342">**EntryPoint** 設定為 **MyDotNetActivityNS.MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="88d1a-343">**PackageLinkedService** 設定為 **AzureStorageLinkedService**，它會指向包含自訂活動 zip 檔案的 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="88d1a-344">如果您將不同的 Azure 儲存體帳戶用於輸入/輸出檔案和自訂活動 zip 檔案，您可以建立另一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="88d1a-345">本文假設您使用相同的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="88d1a-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="88d1a-346">**PackageFile** 設定為 **customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="88d1a-347">其格式為：containerforthezip/nameofthezip.zip。</span><span class="sxs-lookup"><span data-stu-id="88d1a-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="88d1a-348">自訂活動會採用 **InputDataset** 做為輸入和 **OutputDataset** 做為輸出。</span><span class="sxs-lookup"><span data-stu-id="88d1a-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="88d1a-349">自訂活動的 linkedServiceName 屬性會指向 **AzureBatchLinkedService**，這會告知 Azure Data Factory 自訂活動必須在 Azure Batch VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="88d1a-350">**isPaused** 屬性預設為 **false**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="88d1a-351">在此範例中，管線會立即執行，因為配量已在過去開始。</span><span class="sxs-lookup"><span data-stu-id="88d1a-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="88d1a-352">您可以將此屬性設為 true，以暫停管線，並將其設回 false，以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="88d1a-353">**start** 時間和 **end**時間相差 **5** 小時，而配量會每小時產生，因此管線會產生 5 個配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="88d1a-354">若要部署管線，按一下命令列上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="88d1a-355">監視管線</span><span class="sxs-lookup"><span data-stu-id="88d1a-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="88d1a-356">在 Azure 入口網站的 [Data Factory] 刀鋒視窗中，按一下 [圖表] 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![[圖表] 磚](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="88d1a-358">在 [圖表] 檢視中，現在按一下 [OutputDataset]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![圖表檢視](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="88d1a-360">您應該會看到這五個輸出配量都處於就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="88d1a-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="88d1a-361">如果沒有處於就緒狀態，則他們尚未產生。</span><span class="sxs-lookup"><span data-stu-id="88d1a-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![輸出配量](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="88d1a-363">確認 Blob 儲存體的 **adftutorial** 容器中已產生輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![自訂活動的輸出][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="88d1a-365">如果您開啟輸出檔，您應該會看到類似下面的輸出：</span><span class="sxs-lookup"><span data-stu-id="88d1a-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="88d1a-366">使用 [Azure 入口網站][azure-preview-portal]或 Azure PowerShell Cmdlet 來監視您的 Data Factory、管線和資料集。</span><span class="sxs-lookup"><span data-stu-id="88d1a-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="88d1a-367">在可從入口網站下載的記錄檔中 (尤其是 user-0.log)，您可以從程式碼中的 **ActivityLogger** ，或使用 Cmdlet，以查看自訂活動的訊息。</span><span class="sxs-lookup"><span data-stu-id="88d1a-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![從自訂活動下載記錄檔][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="88d1a-369">如需有關監視資料集和管線的詳細步驟，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md) 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="88d1a-370">Visual Studio 中的 Data Factory 專案</span><span class="sxs-lookup"><span data-stu-id="88d1a-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="88d1a-371">您可以使用 Visual Studio (而不是使用 Azure 入口網站) 來建立並發佈 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="88d1a-372">如需使用 Visual Studio 建立並發佈 Data Factory 實體的詳細資訊，請參閱[使用 Visual Studio 建置您的第一個管線](data-factory-build-your-first-pipeline-using-vs.md)和[從 Azure Blob 複製資料到 Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md)一文。</span><span class="sxs-lookup"><span data-stu-id="88d1a-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="88d1a-373">如果您在 Visual Studio 中建立 Data Factory 專案，請執行下列額外步驟︰</span><span class="sxs-lookup"><span data-stu-id="88d1a-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="88d1a-374">將 Data Factory 專案新增至包含自訂活動專案的 Visual Studio 解決方案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="88d1a-375">從 Data Factory 專案將參考新增至 .NET 活動專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="88d1a-376">以滑鼠右鍵按一下 Data Factory 專案，指向 [新增]，然後按一下 [參考]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="88d1a-377">在 [新增參考] 對話方塊中，選取 **MyDotNetActivity** 專案，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="88d1a-378">建置及發佈解決方案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="88d1a-379">當您發佈 Data Factory 實體時，系統會自動為您建立 zip 檔，並且上傳至 blob 容器：customactivitycontainer。</span><span class="sxs-lookup"><span data-stu-id="88d1a-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="88d1a-380">如果 blob 容器不存在，也會自動建立。</span><span class="sxs-lookup"><span data-stu-id="88d1a-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="88d1a-381">Data Factory 和 Batch 整合</span><span class="sxs-lookup"><span data-stu-id="88d1a-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="88d1a-382">Data Factory 服務會在 Azure Batch 中建立作業，其名為：**adf-poolname: job-xxx**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="88d1a-383">按一下左側功能表中的 [作業]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-383">Click **Jobs** from the left menu.</span></span> 

![Azure Data Factory - Batch 作業](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="88d1a-385">配量的每個活動執行都會建立一個作業。</span><span class="sxs-lookup"><span data-stu-id="88d1a-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="88d1a-386">如果有五個配量就緒可供處理，此作業中會建立五個作業。</span><span class="sxs-lookup"><span data-stu-id="88d1a-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="88d1a-387">如果 Batch 集區中有多個運算節點，可以平行執行兩個或多個配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="88d1a-388">如果每個計算結點的最大工作設為 > 1，您也可以在相同的計算中執行多個配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Azure Data Factory - Batch 作業工作](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="88d1a-390">下圖說明 Azure Data Factory 與 Batch 工作之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="88d1a-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory & Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="88d1a-392">疑難排解失敗</span><span class="sxs-lookup"><span data-stu-id="88d1a-392">Troubleshoot failures</span></span>
<span data-ttu-id="88d1a-393">疑難排解包含一些基本技術：</span><span class="sxs-lookup"><span data-stu-id="88d1a-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="88d1a-394">如果您看到下列錯誤，您可能正在使用經常性/非經常性 Blob 儲存體，而非使用一般用途的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="88d1a-395">將 zip 檔案上傳至**一般用途的 Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="88d1a-396">如果您看到下列錯誤，請確認 CS 檔案中的類別名稱符合您在管線 JSON 中為 **EntryPoint** 屬性指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="88d1a-397">在逐步解說中，類別的名稱是︰MyDotNetActivity，而 JSON 中的 EntryPoint 是︰MyDotNetActivityNS.**MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="88d1a-398">如果名稱相符，請確認所有二進位檔皆位於 zip 檔案的 **根資料夾** 中。</span><span class="sxs-lookup"><span data-stu-id="88d1a-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="88d1a-399">也就是說，當您開啟 zip 檔案，您應該會在根資料夾中看到所有檔案，而非在任何子資料夾中看到。</span><span class="sxs-lookup"><span data-stu-id="88d1a-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="88d1a-400">如果輸入配量不是設定為 [就緒] ，請確認輸入資料夾結構正確，且在於輸入資料夾中有 **file.txt**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="88d1a-401">在自訂活動的 **Execute** 方法中，使用可協助您針對問題進行疑難排解的 **IActivityLogger** 物件記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="88d1a-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="88d1a-402">記錄的訊息會顯示在使用者記錄檔 (一或多個名為 user-0.log、user-1.log、user-2.log 等的檔案) 中。</span><span class="sxs-lookup"><span data-stu-id="88d1a-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="88d1a-403">在 [OutputDataset] 刀鋒視窗中，按一下配量，以查看該配量的 [資料配量] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88d1a-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="88d1a-404">您會看到該配量的 [活動執行]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="88d1a-405">您會看到一個為該配量執行的活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="88d1a-406">如果您按一下命令列中的 [執行]，您可以為相同的配量啟動另一個活動執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="88d1a-407">當您按一下活動執行，您會看到包含記錄檔清單的 [活動執行詳細資料]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="88d1a-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="88d1a-408">您會在 user_0.log 檔案中看到記錄的訊息。</span><span class="sxs-lookup"><span data-stu-id="88d1a-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="88d1a-409">發生錯誤時，您會看到三個活動執行，因為管線/活動 JSON 中的重試計數設定為 3。</span><span class="sxs-lookup"><span data-stu-id="88d1a-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="88d1a-410">當您按一下活動執行，您會看到您可以檢閱的記錄檔來疑難排解錯誤。</span><span class="sxs-lookup"><span data-stu-id="88d1a-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="88d1a-411">在記錄檔清單中，按一下 [user-0.log] **IActivityLogger.Write**方法的結果。</span><span class="sxs-lookup"><span data-stu-id="88d1a-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="88d1a-412">在右窗格中的是使用 **IActivityLogger.Write** 方法的結果。</span><span class="sxs-lookup"><span data-stu-id="88d1a-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="88d1a-413">如果您無法看到所有訊息，請檢查是否有名為 user_1.log、user_2.log 等等多個記錄檔。否則，程式碼可能會在最後一個記錄的訊息之後失敗。</span><span class="sxs-lookup"><span data-stu-id="88d1a-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="88d1a-414">此外，檢查 **system-0.log** 是否有任何系統錯誤訊息和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="88d1a-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="88d1a-415">在 zip 檔案中包含 **PDB** 檔案，錯誤詳細資料才會在錯誤發生時包含**呼叫堆疊**等資訊。</span><span class="sxs-lookup"><span data-stu-id="88d1a-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="88d1a-416">自訂活動之 zip 檔案中的所有檔案都必須位於 **最上層** 且不包含任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="88d1a-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="88d1a-417">確認 **assemblyName** (MyDotNetActivity.dll)、**entryPoint** (MyDotNetActivityNS.MyDotNetActivity)、**packageFile** (customactivitycontainer/MyDotNetActivity.zip) 和 **packageLinkedService** (應指向包含 zip 檔案的**一般用途** Azure blob 儲存體) 都設為正確的值。</span><span class="sxs-lookup"><span data-stu-id="88d1a-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="88d1a-418">如果您修正錯誤，並想要重新處理配量，請以滑鼠右鍵按一下 [OutputDataset] 刀鋒視窗中的配量，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="88d1a-419">如果您看到下列錯誤，您使用的 Azure 儲存體封裝的版本即 > 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="88d1a-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="88d1a-420">Data Factory 服務啟動程式需要 4.3 版的 WindowsAzure.Storage。</span><span class="sxs-lookup"><span data-stu-id="88d1a-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="88d1a-421">若您必須使用更新版本的 Azure 儲存體組件，請參閱 [Appdomain 隔離](#appdomain-isolation)小節，以取得因應措施。</span><span class="sxs-lookup"><span data-stu-id="88d1a-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="88d1a-422">如果您可以使用版本 4.3.0 的 Azure 儲存體封裝，請移除對版本 > 4.3.0 Azure.Storage 封裝的現有參考。</span><span class="sxs-lookup"><span data-stu-id="88d1a-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="88d1a-423">接著，從 NuGet Package Manager Console 執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="88d1a-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="88d1a-424">建置專案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-424">Build the project.</span></span> <span data-ttu-id="88d1a-425">從 bin\Debug 資料夾刪除版本 > 4.3.0 的 Azure.Storage 組件。</span><span class="sxs-lookup"><span data-stu-id="88d1a-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="88d1a-426">以二進位檔和 PDB 檔案建立 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="88d1a-427">以 blob 容器 (customactivitycontainer) 中的 zip 檔案取代舊的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="88d1a-428">重新執行失敗的配量 (以滑鼠右鍵按一下配量並按一下 [執行])。</span><span class="sxs-lookup"><span data-stu-id="88d1a-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="88d1a-429">自訂活動不會使用來自您套件的 **app.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="88d1a-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="88d1a-430">因此，如果您的程式碼會從組態檔讀取任何連接字串，則在執行階段沒有作用。</span><span class="sxs-lookup"><span data-stu-id="88d1a-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="88d1a-431">最佳做法是使用 Azure Batch 將所有祕密存放在 **Azure KeyVault** 中、使用以憑證為基礎的服務主體來保護 **keyvault**，然後將憑證發佈至 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="88d1a-432">接著，.NET 自訂活動便可以在執行階段從 KeyVault 存取密碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="88d1a-433">這是一般解決方案，而且可以擴展至任何類型的密碼，不僅限於連接字串。</span><span class="sxs-lookup"><span data-stu-id="88d1a-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="88d1a-434">此外，也有較簡單的因應措施 (但並非最佳做法)︰您可以建立一個帶有連接字串設定的 **Azure SQL 連結服務** 、建立一個使用該連結服務的資料集，然後將該資料集以虛擬輸入資料集的形式鏈結至自訂 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="88d1a-435">接著，您便可以在自訂活動程式碼中存取連結服務的連接字串。</span><span class="sxs-lookup"><span data-stu-id="88d1a-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="88d1a-436">更新自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-436">Update custom activity</span></span>
<span data-ttu-id="88d1a-437">如果您更新自訂活動的程式碼，請建置它，並將包含新二進位檔案的 zip 檔案上傳至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="88d1a-438">Appdomain 隔離</span><span class="sxs-lookup"><span data-stu-id="88d1a-438">Appdomain isolation</span></span>
<span data-ttu-id="88d1a-439">請參閱 [跨 AppDomain 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample)，此範例示範如何建立不受 Data Factory 啟動器之組件版本 (例如：WindowsAzure.Storage v4.3.0、Newtonsoft.Json v6.0.x 等) 限制的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="88d1a-440">存取延伸屬性</span><span class="sxs-lookup"><span data-stu-id="88d1a-440">Access extended properties</span></span>
<span data-ttu-id="88d1a-441">您可以在活動 JSON 中宣告延伸屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="88d1a-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="88d1a-442">範例中有兩個延伸屬性：**SliceStart** 和 **DataFactoryName**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="88d1a-443">SliceStart 的值以 SliceStart 系統變數為基礎。</span><span class="sxs-lookup"><span data-stu-id="88d1a-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="88d1a-444">如需支援的系統變數清單，請參閱 [系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="88d1a-445">DataFactoryName 值為硬式編碼為 CustomActivityFactory。</span><span class="sxs-lookup"><span data-stu-id="88d1a-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="88d1a-446">若要以 **Execute** 方法存取這些延伸屬性，請使用類似以下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="88d1a-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="88d1a-447">Azure Batch 的自動調整</span><span class="sxs-lookup"><span data-stu-id="88d1a-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="88d1a-448">您也可以建立具有 **自動調整** 功能的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="88d1a-449">例如，您可以用 0 專用 VM 和依據暫止工作數目自動調整的公式，建立 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="88d1a-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="88d1a-450">這裡的範例公式會有下列行為：當集區一開始建立時，它會以 1 部 VM 啟動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="88d1a-451">$PendingTasks 計量會定義執行中 + 作用中 (已排入佇列) 狀態的工作數目。</span><span class="sxs-lookup"><span data-stu-id="88d1a-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="88d1a-452">公式會尋找過去 180 秒內的平均擱置中工作數目，並據以設定 TargetDedicated。</span><span class="sxs-lookup"><span data-stu-id="88d1a-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="88d1a-453">它會確保 TargetDedicated 一律不會超過 25 部 VM。</span><span class="sxs-lookup"><span data-stu-id="88d1a-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="88d1a-454">因此，當提交新工作時，集區會自動成長而且工作會完成，VM 會依序成為可用，而且自動調整規模功能會壓縮那些 VM。</span><span class="sxs-lookup"><span data-stu-id="88d1a-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="88d1a-455">您可以視需要調整 startingNumberOfVMs 及 maxNumberofVMs。</span><span class="sxs-lookup"><span data-stu-id="88d1a-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="88d1a-456">自動調整公式：</span><span class="sxs-lookup"><span data-stu-id="88d1a-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="88d1a-457">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](../batch/batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="88d1a-458">如果集區使用預設的 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)，Batch 服務在執行自訂活動之前，可能需要 15-30 分鐘的時間準備 VM。</span><span class="sxs-lookup"><span data-stu-id="88d1a-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="88d1a-459">如果集區使用不同的 autoScaleEvaluationInterval，Batch 服務可能需要 autoScaleEvaluationInterval + 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="88d1a-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="88d1a-460">使用 HDInsight 計算服務</span><span class="sxs-lookup"><span data-stu-id="88d1a-460">Use HDInsight compute service</span></span>
<span data-ttu-id="88d1a-461">在逐步解說中，您會使用 Azure Batch 計算來執行自訂活動。</span><span class="sxs-lookup"><span data-stu-id="88d1a-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="88d1a-462">您也可以使用自己的 Windows 架構 HDInsight 叢集，或讓 Data Factory 建立隨選 Windows 架構 HDInsight 叢集，然後讓自訂活動在 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="88d1a-463">以下是使用 HDInsight 叢集的高階步驟。</span><span class="sxs-lookup"><span data-stu-id="88d1a-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88d1a-464">自訂的 .NET 活動只會在 Windows 架構的 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="88d1a-465">這項限制的因應措施是使用 Map Reduce 活動以在 Linux 架構的 HDInsight 叢集上執行自訂的 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="88d1a-466">另一個選項是使用 VM 的 Azure Batch 集區來執行自訂活動，而非使用 HDInsight 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="88d1a-467">建立 Azure HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="88d1a-468">使用 HDInsight 連結服務來取代管線 JSON 中的 **AzureBatchLinkedService** 。</span><span class="sxs-lookup"><span data-stu-id="88d1a-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="88d1a-469">如果您要使用逐步解說測試它，變更管線的**開始**和**結束**時間，以便讓您能夠使用 Azure HDInsight 服務來測試案例。</span><span class="sxs-lookup"><span data-stu-id="88d1a-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="88d1a-470">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="88d1a-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="88d1a-471">Azure Data Factory 服務支援建立隨選叢集，並使用它處理輸入來產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="88d1a-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="88d1a-472">您也可以使用自己的叢集執行相同作業。</span><span class="sxs-lookup"><span data-stu-id="88d1a-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="88d1a-473">當您使用隨選 HDInsight 叢集時，系統會為每個配量建立叢集。</span><span class="sxs-lookup"><span data-stu-id="88d1a-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="88d1a-474">然而，如果您使用自己的 HDInsight 叢集，叢集已經準備好立即處理配量。</span><span class="sxs-lookup"><span data-stu-id="88d1a-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="88d1a-475">因此，在使用隨選叢集時，可能無法像使用自己的叢集那麼快看到輸出資料。</span><span class="sxs-lookup"><span data-stu-id="88d1a-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="88d1a-476">在執行階段，.NET 活動的執行個體只在 HDInsight 叢集的一個背景工作角色節點上執行，無法擴展到多個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="88d1a-477">.NET 活動的多個執行個體可以在 HDInsight 叢集的不同節點上平行執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="88d1a-478">若要使用隨選 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="88d1a-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="88d1a-479">在 **Azure 入口網站**中，按一下 Data Factory 首頁中的 [製作和部署]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="88d1a-480">在 [Data Factory 編輯器] 中，從命令列按一下 [新增計算]，然後從功能表選取 [隨選 HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="88d1a-481">對 JSON 指令碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="88d1a-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="88d1a-482">在 **clusterSize** 屬性中，指定 HDInsight 叢集的大小。</span><span class="sxs-lookup"><span data-stu-id="88d1a-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="88d1a-483">在 **timeToLive** 屬性中，指定客戶閒置多久之後會被刪除。</span><span class="sxs-lookup"><span data-stu-id="88d1a-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="88d1a-484">在 **version** 屬性中，指定您要使用的 HDInsight 版本。</span><span class="sxs-lookup"><span data-stu-id="88d1a-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="88d1a-485">如果您排除此屬性，則會使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="88d1a-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="88d1a-486">針對 **LinkedServiceName**，指定 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="88d1a-487">自訂的 .NET 活動只會在 Windows 架構的 HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="88d1a-488">這項限制的因應措施是使用 Map Reduce 活動以在 Linux 架構的 HDInsight 叢集上執行自訂的 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="88d1a-489">另一個選項是使用 VM 的 Azure Batch 集區來執行自訂活動，而非使用 HDInsight 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="88d1a-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="88d1a-490">按一下命令列的 [部署]  ，部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="88d1a-491">若要使用您自己的 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="88d1a-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="88d1a-492">在 **Azure 入口網站**中，按一下 Data Factory 首頁中的 [製作和部署]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="88d1a-493">在 [Data Factory 編輯器] 中，從命令列按一下 [新增計算]，然後從功能表選取 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="88d1a-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="88d1a-494">對 JSON 指令碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="88d1a-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="88d1a-495">在 **clusterUri** 屬性中，輸入您的 HDInsight 的 URL。</span><span class="sxs-lookup"><span data-stu-id="88d1a-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="88d1a-496">例如：https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="88d1a-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="88d1a-497">在 **UserName** 屬性中，輸入具有 HDInsight 叢集存取權的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="88d1a-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="88d1a-498">在 **Password** 屬性中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="88d1a-499">在 **LinkedServiceName** 屬性輸入 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="88d1a-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="88d1a-500">按一下命令列的 [部署]  ，部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="88d1a-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="88d1a-501">請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="88d1a-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="88d1a-502">在 **管線 JSON**中，使用 HDInsight (隨選或自有) 連結服務︰</span><span class="sxs-lookup"><span data-stu-id="88d1a-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="88d1a-503">使用 .NET SDK 建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="88d1a-504">在這篇文章的逐步解說中，您會使用 Azure 入口網站建立具有管線 (使用自訂活動) 的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="88d1a-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="88d1a-505">下列程式碼會示範如何改為使用 .NET SDK 建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="88d1a-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="88d1a-506">您可以在[使用 .NET API 建立具有複製活動的管線](data-factory-copy-activity-tutorial-using-dotnet-api.md)一文中找到使用 SDK 以程式設計方式建立管線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="88d1a-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="88d1a-507">在 Visual Studio 中針對自訂活動進行偵錯</span><span class="sxs-lookup"><span data-stu-id="88d1a-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="88d1a-508">GitHub 上的 [Azure Data Factory - 本機環境](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) 範例包含可讓您在 Visual Studio 內針對自訂 .NET 活動進行偵錯的工具。</span><span class="sxs-lookup"><span data-stu-id="88d1a-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="88d1a-509">GitHub 上的範例自訂活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="88d1a-510">範例</span><span class="sxs-lookup"><span data-stu-id="88d1a-510">Sample</span></span> | <span data-ttu-id="88d1a-511">自訂活動的工作內容</span><span class="sxs-lookup"><span data-stu-id="88d1a-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="88d1a-512">[HTTP 資料下載程式](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="88d1a-513">使用 Data Factory 的自訂 C# 活動，從 HTTP 端點將資料下載到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="88d1a-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="88d1a-514">Twitter 情感分析範例</span><span class="sxs-lookup"><span data-stu-id="88d1a-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="88d1a-515">叫用 Azure ML 模型，執行情感分析、評分、預測等等。</span><span class="sxs-lookup"><span data-stu-id="88d1a-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="88d1a-516">[執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。</span><span class="sxs-lookup"><span data-stu-id="88d1a-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="88d1a-517">在已安裝 R 的 HDInsight 叢集上執行 RScript.exe 來叫用 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="88d1a-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="88d1a-518">跨 AppDomain.NET 活動</span><span class="sxs-lookup"><span data-stu-id="88d1a-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="88d1a-519">使用非 Data Factory 啟動器所使用的組件版本</span><span class="sxs-lookup"><span data-stu-id="88d1a-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="88d1a-520">重新處理 Azure Analysis Services 中的模型</span><span class="sxs-lookup"><span data-stu-id="88d1a-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="88d1a-521">重新處理 Azure Analysis Services 中的模型。</span><span class="sxs-lookup"><span data-stu-id="88d1a-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
