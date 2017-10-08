---
title: "aaaUse Azure Data Factory 管線中的自訂活動"
description: "深入了解如何 toocreate 自訂活動和在 Azure Data Factory 管線中使用它們。"
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
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="40792-103">在 Azure 資料處理站管線中使用自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="40792-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="40792-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="40792-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="40792-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="40792-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="40792-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="40792-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="40792-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="40792-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="40792-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="40792-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="40792-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="40792-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="40792-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="40792-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="40792-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="40792-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="40792-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="40792-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="40792-114">您可以在 Azure Data Factory 管線中使用兩種活動。</span><span class="sxs-lookup"><span data-stu-id="40792-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="40792-115">[資料移動活動](data-factory-data-movement-activities.md)toomove 資料之間[支援來源和接收的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="40792-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="40792-116">[資料轉換活動](data-factory-data-transformation-activities.md)tootransform 資料使用 compute 的 Azure HDInsight、 Azure Batch 和 Azure Machine Learning 等服務。</span><span class="sxs-lookup"><span data-stu-id="40792-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="40792-117">toomove 資料，從 Data Factory 不支援，資料存放區建立**自訂活動**您自己的資料移動邏輯和使用 hello 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="40792-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="40792-118">同樣地，tootransform/處理的方式不支援的 Data Factory 中的資料建立您自己的資料轉換邏輯的自訂活動，並在管線中使用 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="40792-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="40792-119">您可以設定自訂活動 toorun **Azure Batch**的虛擬機器，或以 Windows 為基礎的集區**Azure HDInsight**叢集。</span><span class="sxs-lookup"><span data-stu-id="40792-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="40792-120">當使用 Azure Batch 時，您只可以使用現有的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="40792-121">然而，使用 HDInsight 時，您可以使用現有的 HDInsight 叢集或針對您在執行階段的隨選自動建立叢集。</span><span class="sxs-lookup"><span data-stu-id="40792-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="40792-122">hello 下列逐步解說提供逐步指示，建立自訂的.NET 活動和管線中使用 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="40792-123">hello 逐步解說會使用**Azure Batch**連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="40792-124">請改用 toouse Azure HDInsight 連結服務，您可以建立連結的服務型別的**HDInsight** （您自己的 HDInsight 叢集） 或**HDInsightOnDemand** （Data Factory 建立的 HDInsight 叢集依需求）。</span><span class="sxs-lookup"><span data-stu-id="40792-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="40792-125">然後，設定自訂活動 toouse hello HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="40792-126">請參閱[使用 Azure HDInsight 連結服務](#use-hdinsight-compute-service)一節以取得有關使用 Azure HDInsight toorun hello 自訂活動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40792-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="40792-127">只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="40792-128">這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="40792-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="40792-129">另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="40792-130">不可能 toouse 從自訂活動 tooaccess 在內部部署資料來源的資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="40792-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="40792-131">目前，[資料管理閘道器](data-factory-data-management-gateway.md)僅支援 hello 複製活動和預存程序活動 Data Factory 中。</span><span class="sxs-lookup"><span data-stu-id="40792-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="40792-132">逐步解說：建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="40792-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="40792-133">Prerequisites</span></span>
* <span data-ttu-id="40792-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="40792-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="40792-135">下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="40792-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="40792-136">Azure Batch 的必要條件</span><span class="sxs-lookup"><span data-stu-id="40792-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="40792-137">Hello 逐步解說中，您可以執行您使用 Azure Batch 計算資源做的自訂.NET 活動。</span><span class="sxs-lookup"><span data-stu-id="40792-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="40792-138">**Azure 批次**是平台服務的執行大規模的平行和高效能運算 (HPC) 應用程式有效率地在 hello 雲端中的。</span><span class="sxs-lookup"><span data-stu-id="40792-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="40792-139">Azure 批次排程需要大量計算工作 toorun 上 managed**的虛擬機器集合**，並可自動調整計算資源 toomeet hello 需求的工作。</span><span class="sxs-lookup"><span data-stu-id="40792-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="40792-140">請參閱[Azure Batch 基本概念][ batch-technical-overview] hello Azure 批次服務的發行項的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="40792-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="40792-141">Hello 教學課程中，建立 Azure 批次帳戶與 Vm 的集區。</span><span class="sxs-lookup"><span data-stu-id="40792-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="40792-142">Hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="40792-142">Here are hello steps:</span></span>

1. <span data-ttu-id="40792-143">建立**Azure Batch 帳戶**使用 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="40792-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="40792-144">請參閱[建立和管理 Azure Batch 帳戶][batch-create-account]一文以取得指示。</span><span class="sxs-lookup"><span data-stu-id="40792-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="40792-145">記下 hello Azure Batch 帳戶名稱、 帳戶金鑰，URI 和集區名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="40792-146">您需要它們 toocreate Azure Batch 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="40792-147">在 Azure Batch 帳戶的 hello 首頁上，您會看到**URL**在 hello 下列格式： `https://myaccount.westus.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="40792-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="40792-148">在此範例中， **myaccount** hello hello Azure Batch 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="40792-149">您在連結的 hello 服務定義中使用的 URI 是 hello 的 URL 不 hello hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="40792-150">例如： `https://<region>.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="40792-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="40792-151">按一下**金鑰**hello 左的窗格中，以及複製 hello**主要存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="40792-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="40792-152">toouse 現有集區，按一下**集區**上 hello 功能表上，並記下 hello**識別碼**hello 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="40792-153">如果您沒有現有的集區，移動 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="40792-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="40792-154">建立 **Azure Batch 集區**。</span><span class="sxs-lookup"><span data-stu-id="40792-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="40792-155">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **瀏覽**在 hello 左的窗格中，然後按一下**批次帳戶**。</span><span class="sxs-lookup"><span data-stu-id="40792-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="40792-156">選取您的 Azure Batch 帳戶 tooopen hello**批次帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="40792-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="40792-157">按一下 [集區]  圖格。</span><span class="sxs-lookup"><span data-stu-id="40792-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="40792-158">在 hello**集區**刀鋒視窗中，按一下 hello 工具列 tooadd 集區中的 新增 按鈕。</span><span class="sxs-lookup"><span data-stu-id="40792-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="40792-159">請輸入 hello 集區 （集區識別碼） 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="40792-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="40792-160">請注意 hello **hello 集區的識別碼**; 時，您需要它建立 hello Data Factory 方案。</span><span class="sxs-lookup"><span data-stu-id="40792-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="40792-161">指定**Windows Server 2012 R2** hello 作業系統系列設定。</span><span class="sxs-lookup"><span data-stu-id="40792-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="40792-162">選取 **節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="40792-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="40792-163">輸入**2**做為 hello 值**目標專用**設定。</span><span class="sxs-lookup"><span data-stu-id="40792-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="40792-164">輸入**2**做為 hello 值**每個節點的最大工作**設定。</span><span class="sxs-lookup"><span data-stu-id="40792-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="40792-165">按一下**確定**toocreate hello 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="40792-166">記下 hello**識別碼**hello 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="40792-167">高階步驟</span><span class="sxs-lookup"><span data-stu-id="40792-167">High-level steps</span></span>
<span data-ttu-id="40792-168">以下是兩個 hello 您執行本逐步解說中為概要步驟：</span><span class="sxs-lookup"><span data-stu-id="40792-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="40792-169">建立包含簡單資料轉換/處理邏輯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="40792-170">建立 Azure data factory 管線，使用 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="40792-171">建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-171">Create a custom activity</span></span>
<span data-ttu-id="40792-172">toocreate.NET 自訂活動，建立**.NET 類別庫**所實作的類別具有專案**IDotNetActivity**介面。</span><span class="sxs-lookup"><span data-stu-id="40792-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="40792-173">這個介面只有一個方法： [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) ，其簽章為：</span><span class="sxs-lookup"><span data-stu-id="40792-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="40792-174">hello 方法會採用四個參數：</span><span class="sxs-lookup"><span data-stu-id="40792-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="40792-175">**linkedServices**。</span><span class="sxs-lookup"><span data-stu-id="40792-175">**linkedServices**.</span></span> <span data-ttu-id="40792-176">這個屬性是 hello 活動的輸入/輸出資料集所參考的資料存放區連結服務的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="40792-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="40792-177">**資料集**。</span><span class="sxs-lookup"><span data-stu-id="40792-177">**datasets**.</span></span> <span data-ttu-id="40792-178">這個屬性是 hello 活動的輸入/輸出資料集的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="40792-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="40792-179">您可以使用此參數 tooget hello 位置以及輸入和輸出資料集所定義的結構描述。</span><span class="sxs-lookup"><span data-stu-id="40792-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="40792-180">**活動**。</span><span class="sxs-lookup"><span data-stu-id="40792-180">**activity**.</span></span> <span data-ttu-id="40792-181">這個屬性代表 hello 目前活動。</span><span class="sxs-lookup"><span data-stu-id="40792-181">This property represents hello current activity.</span></span> <span data-ttu-id="40792-182">它可以是使用的 tooaccess 擴充 hello 自訂活動相關聯的屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="40792-183">如需詳細資訊，請參閱[存取延伸屬性](#access-extended-properties)。</span><span class="sxs-lookup"><span data-stu-id="40792-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="40792-184">**記錄器**。</span><span class="sxs-lookup"><span data-stu-id="40792-184">**logger**.</span></span> <span data-ttu-id="40792-185">此物件可讓您撰寫偵錯註解的設定，該介面 hello 使用者記錄檔中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="40792-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="40792-186">hello 方法會傳回可使用的 toochain 自訂活動運算子 hello 未來的字典。</span><span class="sxs-lookup"><span data-stu-id="40792-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="40792-187">尚未實作這項功能，因此從 hello 方法會傳回空的字典。</span><span class="sxs-lookup"><span data-stu-id="40792-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="40792-188">程序</span><span class="sxs-lookup"><span data-stu-id="40792-188">Procedure</span></span>
1. <span data-ttu-id="40792-189">建立 **.NET 類別庫** 專案。</span><span class="sxs-lookup"><span data-stu-id="40792-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="40792-190">啟動 <b>Visual Studio 2017</b> 或 <b>Visual Studio 2015</b> 或 <b>Visual Studio 2013</b> 或 <b>Visual Studio 2012</b>。</span><span class="sxs-lookup"><span data-stu-id="40792-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="40792-191">按一下<b>檔案</b>，點太<b>新增</b>，然後按一下<b>專案</b>。</span><span class="sxs-lookup"><span data-stu-id="40792-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="40792-192">展開 [範本]<b></b>，然後選取 [Visual C#]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="40792-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="40792-193">在本逐步解說，您使用 C# 中，但您可以使用任何.NET 語言 toodevelop hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="40792-194">選取<b>類別庫</b>從 hello hello 右上的專案類型清單。</span><span class="sxs-lookup"><span data-stu-id="40792-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="40792-195">在 VS 2017 中，選擇 <b>類別庫 (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="40792-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="40792-196">輸入<b>MyDotNetActivity</b> hello<b>名稱</b>。</span><span class="sxs-lookup"><span data-stu-id="40792-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="40792-197">選取<b>C:\ADFGetStarted</b> hello<b>位置</b>。</span><span class="sxs-lookup"><span data-stu-id="40792-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="40792-198">按一下<b>確定</b>toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="40792-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="40792-199">
2.按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="40792-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="40792-200">3.</span><span class="sxs-lookup"><span data-stu-id="40792-200">3.</span></span> <span data-ttu-id="40792-201">在 hello Package Manager Console 中，執行下列命令 tooimport hello **Microsoft.Azure.Management.DataFactories**。</span><span class="sxs-lookup"><span data-stu-id="40792-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="40792-202">匯入 hello **Azure 儲存體**toohello 專案中的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="40792-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="40792-203">資料處理站服務啟動器需要 WindowsAzure.Storage hello 4.3 版本。</span><span class="sxs-lookup"><span data-stu-id="40792-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="40792-204">如果您加入參考 tooa 更新您的自訂活動專案中的 Azure 儲存體組件的版本，您看到錯誤 hello 活動執行時。</span><span class="sxs-lookup"><span data-stu-id="40792-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="40792-205">tooresolve hello 錯誤，請參閱[Appdomain 隔離](#appdomain-isolation)> 一節。</span><span class="sxs-lookup"><span data-stu-id="40792-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="40792-206">新增下列 hello**使用**hello 專案中的陳述式 toohello 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-206">Add hello following **using** statements toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="40792-207">變更 hello 名稱的 hello**命名空間**太**MyDotNetActivityNS**。</span><span class="sxs-lookup"><span data-stu-id="40792-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="40792-208">變更 hello hello 類別名稱太**MyDotNetActivity**從其中 hello **IDotNetActivity**介面 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="40792-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="40792-209">實作 （加入） hello **Execute**方法 hello **IDotNetActivity**介面 toohello **MyDotNetActivity**類別，並複製下列範例程式碼 toohello 方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="40792-210">hello 下列範例會計算 hello 次數 hello 搜尋詞彙 ("Microsoft") 中相關聯的資料配量每個 blob。</span><span class="sxs-lookup"><span data-stu-id="40792-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
        // toolog information, use hello logger object
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

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="40792-211">新增下列 helper 方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="40792-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="40792-212">hello GetFolderPath 方法傳回 hello 路徑 toohello 資料夾 hello 資料集點 tooand hello GetFileName 方法傳回 hello hello blob 檔案的名稱/的 hello 指向資料集。</span><span class="sxs-lookup"><span data-stu-id="40792-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="40792-213">如果您 havefolderPath 定義使用變數，例如 {Year}，{Month}，{Day} 等等 hello 方法傳回 hello 字串，因為它是不使用執行階段值來取代它們。</span><span class="sxs-lookup"><span data-stu-id="40792-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="40792-214">如需存取 SliceStart、SliceEnd 等的詳細資料，請參閱 [存取延伸屬性](#access-extended-properties) 一節。</span><span class="sxs-lookup"><span data-stu-id="40792-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="40792-215">hello Calculate 方法計算 hello 關鍵字 Microsoft hello 輸入檔 (hello 資料夾中的 blob) 中的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="40792-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="40792-216">hello 搜尋詞彙 ("Microsoft") 是硬式編碼 hello 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="40792-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="40792-217">編譯 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="40792-217">Compile hello project.</span></span> <span data-ttu-id="40792-218">按一下**建置**從 hello 功能表，然後按一下**建置方案**。</span><span class="sxs-lookup"><span data-stu-id="40792-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="40792-219">集合 4.5.2 做 hello 專案的目標 framework 的.NET Framework 版本： hello 專案上按一下滑鼠右鍵，然後按一下**屬性**tooset hello 目標架構。</span><span class="sxs-lookup"><span data-stu-id="40792-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="40792-220">Data Factory 不支援針對 .NET Framework 4.5.2 版之後的版本編譯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="40792-221">啟動**Windows 檔案總管**，並瀏覽過**bin\debug**或**bin\release**資料夾視 hello 組建類型而定。</span><span class="sxs-lookup"><span data-stu-id="40792-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="40792-222">建立 zip 檔案**MyDotNetActivity.zip** ，其中包含所有的 hello 二進位碼檔案中 hello <project folder>\bin\Debug 資料夾。</span><span class="sxs-lookup"><span data-stu-id="40792-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="40792-223">包含 hello **MyDotNetActivity.pdb**檔案，以便您在 hello hello 問題的原因，如果發生失敗的程式碼中取得其他詳細資料，例如行號。</span><span class="sxs-lookup"><span data-stu-id="40792-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="40792-224">所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**與任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="40792-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![二進位輸出檔案](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="40792-226">如果名為 **customactivitycontainer** 的 Blob 容器不存在，請自行建立。</span><span class="sxs-lookup"><span data-stu-id="40792-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="40792-227">以 blob toohello customactivitycontainer 中上傳 MyDotNetActivity.zip**一般用途**稱為 AzureStorageLinkedService 的 Azure blob 儲存體 （不熱/cool Blob 儲存）。</span><span class="sxs-lookup"><span data-stu-id="40792-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="40792-228">如果您將.NET 活動專案 tooa 方案加入包含 Data Factory 專案的 Visual Studio 中，並新增參考 too.NET activity 專案從 hello Data Factory 應用程式專案，您不需要手動建立 tooperform hello 最後兩個的步驟hello zip 檔案，並將它上傳 toohello 一般用途的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="40792-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="40792-229">當您發佈使用 Visual Studio 的 Data Factory 實體時，會自動由 hello 發佈程序完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="40792-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="40792-230">如需詳細資訊，請參閱[Visual Studio 中的 Data Factory 專案](#data-factory-project-in-visual-studio)一節。</span><span class="sxs-lookup"><span data-stu-id="40792-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="40792-231">建立具有自訂活動的管線</span><span class="sxs-lookup"><span data-stu-id="40792-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="40792-232">您已建立的自訂活動，並上傳與二進位檔 tooa blob 容器中的 hello zip 檔案**一般用途**Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="40792-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="40792-233">本節中，在中，您可以建立 Azure data factory 管線，使用 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="40792-234">hello hello 自訂活動的輸入資料集代表 adftutorial hello blob 儲存體容器中的 hello customactivityinput 資料夾中的 blob （檔案）。</span><span class="sxs-lookup"><span data-stu-id="40792-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="40792-235">hello hello 活動的輸出資料集代表 adftutorial hello blob 儲存體容器中的 hello customactivityoutput 資料夾中輸出 blob。</span><span class="sxs-lookup"><span data-stu-id="40792-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="40792-236">建立**file.txt**檔案以下列內容，並將它上傳太 hello**customactivityinput**資料夾 hello **adftutorial**容器。</span><span class="sxs-lookup"><span data-stu-id="40792-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="40792-237">如果它已不存在，請建立 hello adftutorial 容器。</span><span class="sxs-lookup"><span data-stu-id="40792-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="40792-238">hello 輸入的資料夾對應 tooa Azure Data Factory 中的配量，即使 hello 資料夾有兩個或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="40792-239">Hello 管線處理每個配量時，該配量的 hello 輸入資料夾中的所有 hello blob 會都重複 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="40792-240">您會看到一個輸出與 hello adftutorial\customactivityoutput 資料夾中的檔案與一或多行 （與 hello 輸入資料夾中的 blob 數目相同）：</span><span class="sxs-lookup"><span data-stu-id="40792-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="40792-241">執行本節中的 hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="40792-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="40792-242">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="40792-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="40792-243">建立**連結的服務**hello Azure Batch 集區的 Vm 上的 hello 自訂活動會執行並 hello 保存 hello 輸入/輸出 blob 的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="40792-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="40792-244">建立輸入和輸出**資料集**代表輸入和輸出 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="40792-245">建立**管線**使用 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="40792-246">建立 hello **file.txt**並將它上載 tooa blob 容器，如果您還沒有。</span><span class="sxs-lookup"><span data-stu-id="40792-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="40792-247">請參閱 hello 前面一節中的指示。</span><span class="sxs-lookup"><span data-stu-id="40792-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="40792-248">步驟 1： 建立 hello 資料處理站</span><span class="sxs-lookup"><span data-stu-id="40792-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="40792-249">登入之後 toohello Azure 入口網站，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="40792-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="40792-250">按一下**新增**hello 左側功能表上。</span><span class="sxs-lookup"><span data-stu-id="40792-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="40792-251">按一下**資料 + 分析**在 hello**新增**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="40792-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="40792-252">按一下**Data Factory**上 hello**資料分析**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="40792-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![新增 Azure Data Factory 功能表](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="40792-254">在 hello**新的 data factory**刀鋒視窗中，輸入**CustomActivityFactory** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="40792-255">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="40792-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="40792-256">如果您收到 hello 錯誤： **Data factory 名稱"CustomActivityFactory"不是使用**，變更 hello hello data factory 名稱 (例如， **yournameCustomActivityFactory**)，然後再次嘗試建立一次。</span><span class="sxs-lookup"><span data-stu-id="40792-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![新增 Azure Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="40792-258">按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。</span><span class="sxs-lookup"><span data-stu-id="40792-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="40792-259">確認您是否使用正確的 hello**訂用帳戶**和**區域**您想要建立 hello 資料 factory toobe。</span><span class="sxs-lookup"><span data-stu-id="40792-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="40792-260">按一下**建立**上 hello**新的 data factory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="40792-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="40792-261">您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="40792-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="40792-262">已成功建立 hello 資料處理站之後，您會看到 hello Data Factory 刀鋒視窗中，它會顯示 hello hello data factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="40792-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="40792-264">步驟 2：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="40792-264">Step 2: Create linked services</span></span>
<span data-ttu-id="40792-265">連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="40792-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="40792-266">在此步驟中，您必須連結您的 Azure 儲存體帳戶和 Azure Batch 帳戶 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="40792-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="40792-267">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="40792-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="40792-268">按一下 hello**作者及部署**磚 hello **DATA FACTORY**刀鋒伺服器**CustomActivityFactory**。</span><span class="sxs-lookup"><span data-stu-id="40792-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="40792-269">您會看到 hello Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="40792-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="40792-270">按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="40792-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="40792-271">您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。</span><span class="sxs-lookup"><span data-stu-id="40792-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![新增資料存放區 - Azure 儲存體](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="40792-273">取代`<accountname>`與您的 Azure 儲存體帳戶名稱和`<accountkey>`hello Azure 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="40792-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="40792-274">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="40792-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure 儲存體類型的連結服務](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="40792-276">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="40792-277">建立 Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="40792-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="40792-278">在 hello Data Factory 編輯器中，按一下  **...多個**hello 命令列上，按一下**新計算**，然後選取**Azure Batch** hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="40792-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![[新增計算]-[Azure 批次]](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="40792-280">進行下列變更 toohello JSON 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="40792-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="40792-281">指定 Azure Batch 帳戶名稱 hello **accountName**屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="40792-282">hello **URL**從 hello **Azure Batch 帳戶 刀鋒視窗**處於 hello 下列格式： `http://accountname.region.batch.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="40792-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="40792-283">Hello **batchUri**屬性在 hello JSON，您需要 tooremove`accountname.`從 hello URL 和使用 hello `accountname` hello `accountName` JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="40792-284">指定 hello hello Azure Batch 帳戶金鑰**accessKey**屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="40792-285">Hello hello 您所建立的集區名稱指定為組件的必要條件 hello **poolName**屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="40792-286">您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="40792-287">指定 Azure 批次 URI hello **batchUri**屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="40792-288">範例：`https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="40792-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="40792-289">指定 hello **AzureStorageLinkedService** hello **linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

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

       <span data-ttu-id="40792-290">Hello **poolName**屬性，您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="40792-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="40792-291">hello Data Factory 服務不支援隨選項 Azure 批次的 HDInsight 的一樣。</span><span class="sxs-lookup"><span data-stu-id="40792-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="40792-292">您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="40792-293">步驟 3：建立資料集</span><span class="sxs-lookup"><span data-stu-id="40792-293">Step 3: Create datasets</span></span>
<span data-ttu-id="40792-294">在此步驟中，您可以建立資料集 toorepresent 輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="40792-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="40792-295">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="40792-295">Create input dataset</span></span>
1. <span data-ttu-id="40792-296">在 hello**編輯器**hello Data Factory 中，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="40792-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="40792-297">取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="40792-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

   <span data-ttu-id="40792-298">您稍後會在本逐步解說建立管線，開始時間為：2016-11-16T00:00:00Z，而結束時間為：2016-11-16T05:00:00Z。</span><span class="sxs-lookup"><span data-stu-id="40792-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="40792-299">它是排程的 tooproduce 資料每小時，因此有五個輸入/輸出配量 (之間**00**: 00:00]-> [ **05**: 00:00)。</span><span class="sxs-lookup"><span data-stu-id="40792-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="40792-300">hello**頻率**和**間隔**hello 輸入資料集設定太**小時**和**1**，這表示該 hello 輸入配量是可用每小時。</span><span class="sxs-lookup"><span data-stu-id="40792-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="40792-301">在此範例中，它是相同的 hello hello intputfolder 中的檔案 (.txt)。</span><span class="sxs-lookup"><span data-stu-id="40792-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="40792-302">以下是 hello SliceStart hello 上方 JSON 片段中的系統變數由每個配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="40792-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="40792-303">按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**。</span><span class="sxs-lookup"><span data-stu-id="40792-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="40792-304">確認您看到 hello**資料表成功建立**hello 編輯器 hello 標題列上的訊息。</span><span class="sxs-lookup"><span data-stu-id="40792-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="40792-305">建立輸出資料表</span><span class="sxs-lookup"><span data-stu-id="40792-305">Create an output dataset</span></span>
1. <span data-ttu-id="40792-306">在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="40792-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="40792-307">取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON 指令碼：</span><span class="sxs-lookup"><span data-stu-id="40792-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

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

     <span data-ttu-id="40792-308">輸出位置是**adftutorial/customactivityoutput/**和輸出檔名稱是 yyyy 公釐-dd HH.txt，其中 yyyy 公釐-dd HH 是 hello 年、 月、 日、 小時 hello 配量所產生。</span><span class="sxs-lookup"><span data-stu-id="40792-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="40792-309">如需詳細資訊，請參閱[開發人員參考資料][adf-developer-reference]。</span><span class="sxs-lookup"><span data-stu-id="40792-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="40792-310">為每個輸入配量產生輸出 blob/檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="40792-311">以下是為每個配量命名輸出檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="40792-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="40792-312">所有的 hello 輸出檔案產生一個輸出資料夾中： **adftutorial\customactivityoutput**。</span><span class="sxs-lookup"><span data-stu-id="40792-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="40792-313">配量</span><span class="sxs-lookup"><span data-stu-id="40792-313">Slice</span></span> | <span data-ttu-id="40792-314">開始時間</span><span class="sxs-lookup"><span data-stu-id="40792-314">Start time</span></span> | <span data-ttu-id="40792-315">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="40792-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="40792-316">1</span><span class="sxs-lookup"><span data-stu-id="40792-316">1</span></span> |<span data-ttu-id="40792-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="40792-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="40792-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="40792-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="40792-319">2</span><span class="sxs-lookup"><span data-stu-id="40792-319">2</span></span> |<span data-ttu-id="40792-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="40792-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="40792-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="40792-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="40792-322">3</span><span class="sxs-lookup"><span data-stu-id="40792-322">3</span></span> |<span data-ttu-id="40792-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="40792-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="40792-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="40792-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="40792-325">4</span><span class="sxs-lookup"><span data-stu-id="40792-325">4</span></span> |<span data-ttu-id="40792-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="40792-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="40792-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="40792-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="40792-328">5</span><span class="sxs-lookup"><span data-stu-id="40792-328">5</span></span> |<span data-ttu-id="40792-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="40792-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="40792-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="40792-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="40792-331">請記住，所有輸入的資料夾中的 hello 檔案會與上面提到的 hello 開始時間配量的一部分。</span><span class="sxs-lookup"><span data-stu-id="40792-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="40792-332">此配量處理時，hello 自訂活動會掃描每個檔案，並產生 hello 與 hello 發生次數的搜尋詞彙 ("Microsoft") 的輸出檔中的資料行。</span><span class="sxs-lookup"><span data-stu-id="40792-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="40792-333">每個每小時的配量的 hello 輸出檔 hello inputfolder 中有三個檔案，如果有三個行： 2016年-11-16-00.txt，2016年-11-16:01:00:00.txt，等等。</span><span class="sxs-lookup"><span data-stu-id="40792-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="40792-334">toodeploy hello **OutputDataset**，按一下 **部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="40792-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="40792-335">建立並執行管線的使用 hello 自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="40792-336">在 hello Data Factory 編輯器中，按一下  **...多個**，然後選取**新管線**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="40792-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="40792-337">取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="40792-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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

    <span data-ttu-id="40792-338">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="40792-338">Note hello following points:</span></span>

   * <span data-ttu-id="40792-339">**並行**設定得**2**以便由 2 個 Vm hello Azure Batch 集區中，兩個配量會平行處理。</span><span class="sxs-lookup"><span data-stu-id="40792-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="40792-340">Hello 活動 > 一節中一個活動，而且它是型別： **DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="40792-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="40792-341">**AssemblyName**設定 toohello hello DLL 名稱： **MyDotnetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="40792-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="40792-342">**EntryPoint**設定得**MyDotNetActivityNS.MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="40792-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="40792-343">**PackageLinkedService**設定得**AzureStorageLinkedService** ，以指 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="40792-344">如果您使用不同的 Azure 儲存體帳戶，來輸入/輸出檔案而且 hello 自訂活動 zip 檔，您建立另一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="40792-345">本文假設您使用 hello 相同的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="40792-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="40792-346">**PackageFile**設定得**customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="40792-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="40792-347">其為 hello 格式： containerforthezip/nameofthezip.zip。</span><span class="sxs-lookup"><span data-stu-id="40792-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="40792-348">hello 自訂活動會採用**InputDataset**做為輸入和**OutputDataset**做為輸出。</span><span class="sxs-lookup"><span data-stu-id="40792-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="40792-349">hello 自訂活動的 hello linkedServiceName 屬性指向 toohello **AzureBatchLinkedService**，它會告訴 Azure Data Factory 的 hello 自訂活動必須 toorun Azure 批次 Vm 上的。</span><span class="sxs-lookup"><span data-stu-id="40792-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="40792-350">**isPaused**屬性設定太**false**預設。</span><span class="sxs-lookup"><span data-stu-id="40792-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="40792-351">hello 管線執行立即在此範例中，因為 hello 配量開始在過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="40792-352">您可以設定這個屬性 tootrue toopause hello 管線，並將它回復 toofalse toorestart。</span><span class="sxs-lookup"><span data-stu-id="40792-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="40792-353">hello**啟動**時間和**結束**時間**五個**相距的時數和配量所產生每小時，因此 hello 管線所產生五個配量。</span><span class="sxs-lookup"><span data-stu-id="40792-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="40792-354">toodeploy hello 管線中，按一下 **部署**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="40792-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="40792-355">監視 hello 管線</span><span class="sxs-lookup"><span data-stu-id="40792-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="40792-356">在 hello Data Factory 刀鋒視窗中 hello Azure 入口網站中，按一下 **圖表**。</span><span class="sxs-lookup"><span data-stu-id="40792-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![[圖表] 磚](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="40792-358">在 hello 圖表檢視，現在按一下 hello OutputDataset。</span><span class="sxs-lookup"><span data-stu-id="40792-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![圖表檢視](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="40792-360">您應該會看到五個輸出配量 hello 位於 hello 就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="40792-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="40792-361">如果它們不是在 hello 就緒狀態，它們沒有被尚未產生。</span><span class="sxs-lookup"><span data-stu-id="40792-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![輸出配量](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="40792-363">確認 hello 輸出檔會產生在 hello blob 儲存體中 hello **adftutorial**容器。</span><span class="sxs-lookup"><span data-stu-id="40792-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![自訂活動的輸出][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="40792-365">如果您開啟 hello 輸出檔，您應該會看到 hello 輸出類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="40792-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="40792-366">使用 hello [Azure 入口網站][ azure-preview-portal]或 Azure PowerShell cmdlet toomonitor 您的資料處理站、 管線和資料集。</span><span class="sxs-lookup"><span data-stu-id="40792-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="40792-367">您可以查看來自 hello 訊息**ActivityLogger**在 hello hello hello 記錄檔 (特別是 0.log 使用者)，您可以下載從 hello 入口網站或使用 cmdlet 的自訂活動的程式碼。</span><span class="sxs-lookup"><span data-stu-id="40792-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![從自訂活動下載記錄檔][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="40792-369">如需有關監視資料集和管線的詳細步驟，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md) 。</span><span class="sxs-lookup"><span data-stu-id="40792-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="40792-370">Visual Studio 中的 Data Factory 專案</span><span class="sxs-lookup"><span data-stu-id="40792-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="40792-371">您可以使用 Visual Studio (而不是使用 Azure 入口網站) 來建立並發佈 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="40792-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="40792-372">詳細的資訊建立和使用 Visual Studio 發行 Data Factory 實體，請參閱[建置您使用 Visual Studio 的第一個管線](data-factory-build-your-first-pipeline-using-vs.md)和[資料複製到 Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md)文件。</span><span class="sxs-lookup"><span data-stu-id="40792-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="40792-373">請勿 hello 下列其他步驟，如果您要在 Visual Studio 中建立 Data Factory 專案：</span><span class="sxs-lookup"><span data-stu-id="40792-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="40792-374">新增 hello Data Factory 專案 toohello 包含 hello 自訂活動專案的 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="40792-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="40792-375">將 hello Data Factory 專案參考 toohello.NET 活動專案。</span><span class="sxs-lookup"><span data-stu-id="40792-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="40792-376">Data Factory 專案上按一下滑鼠右鍵，指向太**新增**，然後按一下**參考**。</span><span class="sxs-lookup"><span data-stu-id="40792-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="40792-377">在 hello**加入參考**對話方塊中，選取 hello **MyDotNetActivity**專案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="40792-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="40792-378">建置並發行 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="40792-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="40792-379">當您發行 Data Factory 實體時，zip 檔案會自動為您建立和上傳的 toohello blob 容器： customactivitycontainer。</span><span class="sxs-lookup"><span data-stu-id="40792-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="40792-380">如果 hello blob 容器不存在，它會自動建立太。</span><span class="sxs-lookup"><span data-stu-id="40792-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="40792-381">Data Factory 和 Batch 整合</span><span class="sxs-lookup"><span data-stu-id="40792-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="40792-382">hello Data Factory 服務 Azure 批次中建立工作以 hello 名稱： **adf poolname： 工作 xxx**。</span><span class="sxs-lookup"><span data-stu-id="40792-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="40792-383">按一下**作業**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="40792-383">Click **Jobs** from hello left menu.</span></span> 

![Azure Data Factory - Batch 作業](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="40792-385">配量的每個活動執行都會建立一個作業。</span><span class="sxs-lookup"><span data-stu-id="40792-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="40792-386">如果有五個處理的配量準備 toobe，有五個工作會建立此作業中。</span><span class="sxs-lookup"><span data-stu-id="40792-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="40792-387">Hello 批次集區中有多個計算節點，如果兩個或多個配量可以平行執行。</span><span class="sxs-lookup"><span data-stu-id="40792-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="40792-388">如果 hello 最大的工作，每個計算節點集太 > 1，您也可以有多個配量上 hello 執行相同的計算。</span><span class="sxs-lookup"><span data-stu-id="40792-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Azure Data Factory - Batch 作業工作](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="40792-390">hello 下列圖表說明 hello Azure Data Factory 和批次工作之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="40792-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory & Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="40792-392">疑難排解失敗</span><span class="sxs-lookup"><span data-stu-id="40792-392">Troubleshoot failures</span></span>
<span data-ttu-id="40792-393">疑難排解包含一些基本技術：</span><span class="sxs-lookup"><span data-stu-id="40792-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="40792-394">如果您看到下列錯誤 hello，您可能正在使用的作用/Cool blob 儲存體而不使用一般用途的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="40792-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="40792-395">上傳 hello zip 檔案 tooa**一般用途的 Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="40792-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="40792-396">如果您看到下列錯誤 hello，確認您指定 hello CS 檔案相符項目 hello 名稱中的 hello 類別 hello 名稱**EntryPoint** hello 管線 JSON 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="40792-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="40792-397">Hello 逐步解說中，在 hello 類別名稱是： MyDotNetActivity，並在 hello JSON 中的 hello 進入點是： MyDotNetActivityNS。**MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="40792-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="40792-398">如果 hello 名稱相符，確認所有 hello 二進位檔都位於 hello**根資料夾**hello zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="40792-399">也就是說，當您開啟 hello zip 檔案，您應該會看到所有的 hello 檔案 hello 根資料夾中，在任何子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="40792-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="40792-400">如果未設定 hello 輸入配量太**準備**，確認 hello 輸入的資料夾結構是否正確和**file.txt**存在 hello 輸入資料夾中。</span><span class="sxs-lookup"><span data-stu-id="40792-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="40792-401">在 hello **Execute**方法的自訂活動，使用 hello **IActivityLogger**物件 toolog 資訊可協助您疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="40792-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="40792-402">記錄的 hello 訊息顯示在 hello 使用者記錄檔 (名為的一個或多個檔案： 使用者 0.log、 使用者 1.log、 使用者 2.log 等。)。</span><span class="sxs-lookup"><span data-stu-id="40792-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="40792-403">在 hello **OutputDataset**刀鋒視窗中，按一下 hello 配量 toosee hello**資料配量**刀鋒視窗，該配量。</span><span class="sxs-lookup"><span data-stu-id="40792-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="40792-404">您會看到該配量的 [活動執行]。</span><span class="sxs-lookup"><span data-stu-id="40792-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="40792-405">您應該會看到一個 hello 配量執行的活動。</span><span class="sxs-lookup"><span data-stu-id="40792-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="40792-406">如果您按一下 執行 hello 命令列中，您可以啟動另一個活動執行 hello 相同配量。</span><span class="sxs-lookup"><span data-stu-id="40792-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="40792-407">當您按一下 hello 活動執行時，請參閱 hello**活動執行詳細資料**刀鋒視窗的記錄檔的清單。</span><span class="sxs-lookup"><span data-stu-id="40792-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="40792-408">您會看到 hello user_0.log 檔中記錄的訊息。</span><span class="sxs-lookup"><span data-stu-id="40792-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="40792-409">當發生錯誤時，因為 hello 重試計數設定 too3 hello 管線/活動 JSON 中會看到三個活動執行。</span><span class="sxs-lookup"><span data-stu-id="40792-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="40792-410">當您按一下 hello 活動執行時，您會看到 hello 記錄檔，您可以檢閱 tootroubleshoot hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="40792-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="40792-411">在 hello 清單中的記錄檔，按一下 hello**使用者 0.log**。</span><span class="sxs-lookup"><span data-stu-id="40792-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="40792-412">Hello 右面板中會使用 hello 的 hello 結果**IActivityLogger.Write**方法。</span><span class="sxs-lookup"><span data-stu-id="40792-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="40792-413">如果您無法看到所有訊息，請檢查是否有名為 user_1.log、user_2.log 等等多個記錄檔。否則，hello 一次登入訊息之後，可能會失敗 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="40792-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="40792-414">此外，檢查 **system-0.log** 是否有任何系統錯誤訊息和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="40792-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="40792-415">包含 hello **PDB**檔案 hello zip 檔案中，所以 hello 錯誤詳細資料會有這類資訊**呼叫堆疊**發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="40792-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="40792-416">所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**與任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="40792-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="40792-417">請確定該 hello **assemblyName** (MyDotNetActivity.dll)， **entryPoint**(MyDotNetActivityNS.MyDotNetActivity)， **packageFile** (customactivitycontainer /MyDotNetActivity.zip) 和**packageLinkedService** (應該指向 toohello**一般用途**包含 hello zip 檔案的 Azure blob 儲存體) 會設定 toocorrect 值。</span><span class="sxs-lookup"><span data-stu-id="40792-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="40792-418">如果您修正錯誤，且想 tooreprocess hello 配量，以滑鼠右鍵按一下 hello 配量在 hello **OutputDataset**刀鋒視窗，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="40792-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="40792-419">如果您看到下列錯誤 hello，您使用版本 > 4.3.0 hello Azure 儲存體的封裝。</span><span class="sxs-lookup"><span data-stu-id="40792-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="40792-420">資料處理站服務啟動器需要 WindowsAzure.Storage hello 4.3 版本。</span><span class="sxs-lookup"><span data-stu-id="40792-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="40792-421">請參閱[Appdomain 隔離](#appdomain-isolation)區段的解決方法是，如果您必須使用 hello 新版的 Azure 儲存體組件。</span><span class="sxs-lookup"><span data-stu-id="40792-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="40792-422">如果您可以使用 Azure 儲存體套件 hello 4.3.0 版，移除 hello 現有參考 tooAzure 儲存封裝的版本 > 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="40792-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="40792-423">然後，執行下列命令，NuGet Package Manager Console 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="40792-424">建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="40792-424">Build hello project.</span></span> <span data-ttu-id="40792-425">刪除版本 > 4.3.0 Azure.Storage 組件從 hello bin\Debug 資料夾。</span><span class="sxs-lookup"><span data-stu-id="40792-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="40792-426">建立 zip 檔案與二進位檔和 hello PDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="40792-427">取代這一個 hello blob 容器 (customactivitycontainer) 中的 hello 舊的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="40792-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="40792-428">重新執行 hello 配量失敗 （配量，以滑鼠右鍵按一下並按一下 [執行]）。</span><span class="sxs-lookup"><span data-stu-id="40792-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="40792-429">hello 自訂活動不會使用 hello **app.config**檔案從您的封裝。</span><span class="sxs-lookup"><span data-stu-id="40792-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="40792-430">因此，如果您的程式碼會讀取 hello 組態檔中的任何連接字串，因此無法在執行階段。</span><span class="sxs-lookup"><span data-stu-id="40792-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="40792-431">hello 最佳作法是當使用 Azure Batch toohold 中的秘密**Azure KeyVault**，使用憑證為基礎的服務主體 tooprotect hello **keyvault**，並散佈 hello 憑證tooAzure 批次集區。</span><span class="sxs-lookup"><span data-stu-id="40792-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="40792-432">hello.NET 自訂活動，則可以從 hello KeyVault 在執行階段存取機密資料。</span><span class="sxs-lookup"><span data-stu-id="40792-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="40792-433">這個解決方案是一般的解決方案，而且可以延展 tooany 類型的密碼，而不只是連接字串。</span><span class="sxs-lookup"><span data-stu-id="40792-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="40792-434">沒有簡單的因應措施 （但不是最佳作法）： 您可以建立**Azure SQL 連結服務**與連接字串設定，建立使用 hello 連結的服務，以及鏈結 hello 資料集做為虛擬輸入資料集的資料集自訂.NET 活動 toohello。</span><span class="sxs-lookup"><span data-stu-id="40792-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="40792-435">接著，您可以存取 hello 連結服務的連接字串 hello 自訂活動程式碼中。</span><span class="sxs-lookup"><span data-stu-id="40792-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="40792-436">更新自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-436">Update custom activity</span></span>
<span data-ttu-id="40792-437">如果您更新 hello hello 自訂活動的程式碼時，建置它，並上傳 hello zip 檔案包含新的二進位檔 toohello blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="40792-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="40792-438">Appdomain 隔離</span><span class="sxs-lookup"><span data-stu-id="40792-438">Appdomain isolation</span></span>
<span data-ttu-id="40792-439">請參閱[跨 AppDomain 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample)會示範如何 toocreate 的自訂活動不是，限制 hello Data Factory 啟動器所使用的 tooassembly 版本 (範例： WindowsAzure.Storage v4.3.0、 Newtonsoft.Json v6.0.x 等。)。</span><span class="sxs-lookup"><span data-stu-id="40792-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="40792-440">存取延伸屬性</span><span class="sxs-lookup"><span data-stu-id="40792-440">Access extended properties</span></span>
<span data-ttu-id="40792-441">Hello 下列範例所示，您可以在 hello 活動 JSON 中宣告擴充的屬性：</span><span class="sxs-lookup"><span data-stu-id="40792-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

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


<span data-ttu-id="40792-442">在 hello 範例中，有兩個的擴充的屬性： **SliceStart**和**DataFactoryName**。</span><span class="sxs-lookup"><span data-stu-id="40792-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="40792-443">hello SliceStart 的值根據 hello SliceStart 系統變數。</span><span class="sxs-lookup"><span data-stu-id="40792-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="40792-444">如需支援的系統變數清單，請參閱 [系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="40792-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="40792-445">DataFactoryName hello 值為硬式編碼 tooCustomActivityFactory。</span><span class="sxs-lookup"><span data-stu-id="40792-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="40792-446">這些擴充屬性中 hello tooaccess **Execute**方法，下列程式碼使用程式碼類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="40792-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="40792-447">Azure Batch 的自動調整</span><span class="sxs-lookup"><span data-stu-id="40792-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="40792-448">您也可以建立具有 **自動調整** 功能的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="40792-449">例如，您可以建立 azure 批次集區 0 專用的 Vm 與 hello 數字的暫止工作為基礎的自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="40792-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="40792-450">hello 範例公式會達到 hello 下列行為： 一開始建立 hello 集區時，開始的 1 的 VM。</span><span class="sxs-lookup"><span data-stu-id="40792-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="40792-451">$PendingTasks 度量定義 hello 數項工作中執行 + （佇列） 的作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="40792-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="40792-452">hello 公式中 hello 過去 180 秒尋找 hello 的平均數目暫止的工作，並據此設定 TargetDedicated。</span><span class="sxs-lookup"><span data-stu-id="40792-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="40792-453">它會確保 TargetDedicated 一律不會超過 25 部 VM。</span><span class="sxs-lookup"><span data-stu-id="40792-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="40792-454">因此，提交新的工作，因為集區自動成長和做為工作完成，Vm 會變成可用逐一和 hello 自動調整壓縮這些 Vm。</span><span class="sxs-lookup"><span data-stu-id="40792-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="40792-455">startingNumberOfVMs 和 maxNumberofVMs 可以調整的 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="40792-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="40792-456">自動調整公式：</span><span class="sxs-lookup"><span data-stu-id="40792-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="40792-457">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](../batch/batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="40792-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="40792-458">如果 hello 集區使用 hello 預設[autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)，hello 批次服務可能需要 15 到 30 分鐘 tooprepare hello VM，然後再執行 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="40792-459">如果 hello 集區使用不同的 autoScaleEvaluationInterval，hello 批次服務可能需要 autoScaleEvaluationInterval + 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="40792-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="40792-460">使用 HDInsight 計算服務</span><span class="sxs-lookup"><span data-stu-id="40792-460">Use HDInsight compute service</span></span>
<span data-ttu-id="40792-461">在 hello 逐步解說中，您可以使用 Azure Batch 計算 toorun hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="40792-462">您也可以使用 Windows 為基礎的 HDInsight 叢集，或已建立隨 Windows 為基礎的 HDInsight 叢集，並以 hello hello HDInsight 叢集上執行的自訂活動的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="40792-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="40792-463">以下是使用的 HDInsight 叢集的 hello 高層級步驟。</span><span class="sxs-lookup"><span data-stu-id="40792-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40792-464">只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="40792-465">這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="40792-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="40792-466">另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="40792-467">建立 Azure HDInsight 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="40792-468">使用 HDInsight 連結服務取代**AzureBatchLinkedService** hello 在管線 JSON。</span><span class="sxs-lookup"><span data-stu-id="40792-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="40792-469">如果您想 tootest hello 逐步解說中，變更與**啟動**和**結束**時間 hello 管線，讓您可以測試以 hello Azure HDInsight 服務的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="40792-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="40792-470">建立 Azure HDInsight 連結服務</span><span class="sxs-lookup"><span data-stu-id="40792-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="40792-471">hello Azure Data Factory 服務支援建立隨叢集，並將它 tooprocess 輸入的 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="40792-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="40792-472">您也可以使用自己的叢集 tooperform hello 相同。</span><span class="sxs-lookup"><span data-stu-id="40792-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="40792-473">當您使用隨選 HDInsight 叢集時，系統會為每個配量建立叢集。</span><span class="sxs-lookup"><span data-stu-id="40792-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="40792-474">而如果您使用 HDInsight 叢集，hello 叢集已準備好 tooprocess hello 立即配量。</span><span class="sxs-lookup"><span data-stu-id="40792-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="40792-475">因此，當您使用隨叢集，您可能無法看見 hello 輸出資料做為當您使用自己的叢集快速。</span><span class="sxs-lookup"><span data-stu-id="40792-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="40792-476">在執行階段，.NET 活動的執行個體只會在執行一個背景工作節點在 hello HDInsight 叢集。它不能在多個節點上的縮放的 toorun。</span><span class="sxs-lookup"><span data-stu-id="40792-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="40792-477">多個執行個體的.NET 活動可以平行執行 hello HDInsight 叢集的不同節點上。</span><span class="sxs-lookup"><span data-stu-id="40792-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="40792-478">toouse 隨選 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="40792-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="40792-479">在 hello **Azure 入口網站**，按一下 **作者及部署**hello Data Factory 首頁中。</span><span class="sxs-lookup"><span data-stu-id="40792-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="40792-480">在 hello Data Factory 編輯器中，按一下 **新計算**hello 命令列，並選取從**-隨選 HDInsight 叢集**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="40792-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="40792-481">進行下列變更 toohello JSON 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="40792-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="40792-482">Hello **clusterSize**屬性，指定 hello hello HDInsight 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="40792-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="40792-483">Hello **timeToLive**屬性，指定時間於刪除之前 hello 客戶可處於閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="40792-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="40792-484">Hello**版本**屬性，指定您想要 toouse hello HDInsight 版本。</span><span class="sxs-lookup"><span data-stu-id="40792-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="40792-485">如果您排除這個屬性時，會使用 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="40792-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="40792-486">Hello **linkedServiceName**，指定**AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="40792-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

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
    > <span data-ttu-id="40792-487">只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="40792-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="40792-488">這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="40792-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="40792-489">另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="40792-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="40792-490">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="40792-491">toouse HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="40792-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="40792-492">在 hello **Azure 入口網站**，按一下 **作者及部署**hello Data Factory 首頁中。</span><span class="sxs-lookup"><span data-stu-id="40792-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="40792-493">在 hello **Data Factory 編輯器**，按一下**新計算**hello 命令列，並選取從**HDInsight 叢集**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="40792-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="40792-494">進行下列變更 toohello JSON 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="40792-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="40792-495">Hello **clusterUri**屬性中，輸入您的 HDInsight hello URL。</span><span class="sxs-lookup"><span data-stu-id="40792-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="40792-496">例如：https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="40792-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="40792-497">Hello **UserName**屬性中，輸入 hello 使用者名稱擁有存取 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="40792-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="40792-498">Hello**密碼**屬性中，輸入 hello 使用者 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="40792-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="40792-499">Hello **LinkedServiceName**屬性中，輸入**AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="40792-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="40792-500">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="40792-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="40792-501">請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40792-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="40792-502">在 hello**管線 JSON**，使用 HDInsight (點播或您自己) 連結服務：</span><span class="sxs-lookup"><span data-stu-id="40792-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

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

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="40792-503">使用 .NET SDK 建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="40792-504">在本文中的 hello 逐步解說，您可以建立 data factory 管線，藉由使用 hello Azure 入口網站使用 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="40792-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="40792-505">下列程式碼的 hello 顯示 toocreate 改為使用.NET SDK hello 資料處理站的方式。</span><span class="sxs-lookup"><span data-stu-id="40792-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="40792-506">您可以找到更多詳細使用 SDK tooprogrammatically hello 中建立管線[建立與複製活動的管線，使用.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="40792-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

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

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="40792-507">在 Visual Studio 中針對自訂活動進行偵錯</span><span class="sxs-lookup"><span data-stu-id="40792-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="40792-508">hello [Azure Data Factory 的本機環境](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment)GitHub 上的範例包含一個工具，可讓您在 Visual Studio 內 toodebug 自訂.NET 活動。</span><span class="sxs-lookup"><span data-stu-id="40792-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="40792-509">GitHub 上的範例自訂活動</span><span class="sxs-lookup"><span data-stu-id="40792-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="40792-510">範例</span><span class="sxs-lookup"><span data-stu-id="40792-510">Sample</span></span> | <span data-ttu-id="40792-511">自訂活動的工作內容</span><span class="sxs-lookup"><span data-stu-id="40792-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="40792-512">[HTTP 資料下載程式](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)。</span><span class="sxs-lookup"><span data-stu-id="40792-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="40792-513">從 HTTP 端點 tooAzure Data Factory 中使用 C# 自訂活動的 Blob 儲存體下載資料。</span><span class="sxs-lookup"><span data-stu-id="40792-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="40792-514">Twitter 情感分析範例</span><span class="sxs-lookup"><span data-stu-id="40792-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="40792-515">叫用 Azure ML 模型，執行情感分析、評分、預測等等。</span><span class="sxs-lookup"><span data-stu-id="40792-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="40792-516">[執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。</span><span class="sxs-lookup"><span data-stu-id="40792-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="40792-517">在已安裝 R 的 HDInsight 叢集上執行 RScript.exe 來叫用 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="40792-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="40792-518">跨 AppDomain.NET 活動</span><span class="sxs-lookup"><span data-stu-id="40792-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="40792-519">使用從 hello Data Factory 啟動器所使用的不同組件版本</span><span class="sxs-lookup"><span data-stu-id="40792-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="40792-520">重新處理 Azure Analysis Services 中的模型</span><span class="sxs-lookup"><span data-stu-id="40792-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="40792-521">重新處理 Azure Analysis Services 中的模型。</span><span class="sxs-lookup"><span data-stu-id="40792-521">Reprocesses a model in Azure Analysis Services.</span></span> |

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
