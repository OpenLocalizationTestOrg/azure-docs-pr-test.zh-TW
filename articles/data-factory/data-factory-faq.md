---
title: "aaaAzure Data Factory-常見問題集"
description: "關於 Azure Data Factory 的常見問題。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a><span data-ttu-id="3c2a3-103">Azure 資料處理站-常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c2a3-103">Azure Data Factory - Frequently Asked Questions</span></span>
## <a name="general-questions"></a><span data-ttu-id="3c2a3-104">一般問題</span><span class="sxs-lookup"><span data-stu-id="3c2a3-104">General questions</span></span>
### <a name="what-is-azure-data-factory"></a><span data-ttu-id="3c2a3-105">Azure 資料處理站是什麼？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-105">What is Azure Data Factory?</span></span>
<span data-ttu-id="3c2a3-106">Data Factory 是以雲端為基礎的資料整合服務， **hello 移動和轉換資料會自動執行**。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-106">Data Factory is a cloud-based data integration service that **automates hello movement and transformation of data**.</span></span> <span data-ttu-id="3c2a3-107">就像處理站執行設備 tootake 原料，並將它們轉換成已完成的貨物，Data Factory 會協調現有的服務來收集未經處理資料，並將它轉換為已備妥要使用的資訊。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-107">Just like a factory that runs equipment tootake raw materials and transform them into finished goods, Data Factory orchestrates existing services that collect raw data and transform it into ready-to-use information.</span></span>

<span data-ttu-id="3c2a3-108">Data Factory 可讓您在內部部署和雲端資料存放區以及使用 Azure HDInsight 等 Azure Data Lake Analytics 計算服務的程序/轉換資料之間的 toocreate 資料驅動型工作流程 toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-108">Data Factory allows you toocreate data-driven workflows toomove data between both on-premises and cloud data stores as well as process/transform data using compute services such as Azure HDInsight and Azure Data Lake Analytics.</span></span> <span data-ttu-id="3c2a3-109">建立管線，以執行您所需要的 hello 動作之後，您可以將它排程 toorun 定期 （每小時、 每天、 每週等）。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-109">After you create a pipeline that performs hello action that you need, you can schedule it toorun periodically (hourly, daily, weekly etc.).</span></span>   

<span data-ttu-id="3c2a3-110">如需詳細資訊，請參閱[概觀與重要概念](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-110">For more information, see [Overview & Key Concepts](data-factory-introduction.md).</span></span>

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a><span data-ttu-id="3c2a3-111">哪裡可以找到 Azure 資料處理站的定價詳細資料？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-111">Where can I find pricing details for Azure Data Factory?</span></span>
<span data-ttu-id="3c2a3-112">請參閱[資料 Factory 定價詳細資料頁面][ adf-pricing-details] hello 定價 hello Azure Data Factory 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-112">See [Data Factory Pricing Details page][adf-pricing-details] for hello pricing details for hello Azure Data Factory.</span></span>  

### <a name="how-do-i-get-started-with-azure-data-factory"></a><span data-ttu-id="3c2a3-113">如何開始使用 Azure Data Factory？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-113">How do I get started with Azure Data Factory?</span></span>
* <span data-ttu-id="3c2a3-114">如需 Azure Data Factory 的概觀，請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-114">For an overview of Azure Data Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md).</span></span>
* <span data-ttu-id="3c2a3-115">如需如何太**複製/移動資料**使用複製活動，請參閱[將資料從 Azure Blob 儲存體 tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-115">For a tutorial on how too**copy/move data** using Copy Activity, see [Copy data from Azure Blob Storage tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="3c2a3-116">如需如何太**轉換資料**使用 HDInsight Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-116">For a tutorial on how too**transform data** using HDInsight Hive Activity.</span></span> <span data-ttu-id="3c2a3-117">請參閱 [在 Hadoop 叢集上執行 Hive 指令碼來處理資料](data-factory-build-your-first-pipeline.md)</span><span class="sxs-lookup"><span data-stu-id="3c2a3-117">See [Process data by running Hive script on Hadoop cluster](data-factory-build-your-first-pipeline.md)</span></span>

### <a name="what-is-hello-data-factorys-region-availability"></a><span data-ttu-id="3c2a3-118">Hello Data Factory 的區域可用性是什麼？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-118">What is hello Data Factory’s region availability?</span></span>
<span data-ttu-id="3c2a3-119">Data Factory 可在**美國西部**和**北歐**地區使用。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-119">Data Factory is available in **US West** and **North Europe**.</span></span> <span data-ttu-id="3c2a3-120">hello 計算和資料處理站所使用的儲存體服務可位於其他區域。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-120">hello compute and storage services used by data factories can be in other regions.</span></span> <span data-ttu-id="3c2a3-121">請參閱 [支援的區域](data-factory-introduction.md#supported-regions)。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-121">See [Supported regions](data-factory-introduction.md#supported-regions).</span></span>

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a><span data-ttu-id="3c2a3-122">Hello 限制數目的資料處理站/管線/活動/資料集上有哪些？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-122">What are hello limits on number of data factories/pipelines/activities/datasets?</span></span>
<span data-ttu-id="3c2a3-123">請參閱**Azure 資料 Factory 限制**區段 hello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md#data-factory-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-123">See **Azure Data Factory Limits** section of hello [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md#data-factory-limits) article.</span></span>

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a><span data-ttu-id="3c2a3-124">什麼是 Azure Data Factory 服務的 hello 撰寫/開發人員經驗？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-124">What is hello authoring/developer experience with Azure Data Factory service?</span></span>
<span data-ttu-id="3c2a3-125">您可以撰寫/建立 data factory 使用其中一種下列 Sdk 工具/hello:</span><span class="sxs-lookup"><span data-stu-id="3c2a3-125">You can author/create data factories using one of hello following tools/SDKs:</span></span>

* <span data-ttu-id="3c2a3-126">**Azure 入口網站**hello Azure 入口網站中的 hello Data Factory 刀鋒提供豐富的使用者介面的 toocreate 資料 factory ad 連結服務。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-126">**Azure portal** hello Data Factory blades in hello Azure portal provide rich user interface for you toocreate data factories ad linked services.</span></span> <span data-ttu-id="3c2a3-127">hello **Data Factory 編輯器**，這也是 hello 入口網站的一部分，可讓您藉由指定這些成品的 JSON 定義 tooeasily 建立連結的服務、 資料表、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-127">hello **Data Factory Editor**, which is also part of hello portal, allows you tooeasily create linked services, tables, data sets, and pipelines by specifying JSON definitions for these artifacts.</span></span> <span data-ttu-id="3c2a3-128">請參閱[建置您使用 Azure 入口網站的第一個資料管線](data-factory-build-your-first-pipeline-using-editor.md)hello 入口網站/編輯器 toocreate 使用的範例，以及部署 data factory。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-128">See [Build your first data pipeline using Azure portal](data-factory-build-your-first-pipeline-using-editor.md) for an example of using hello portal/editor toocreate and deploy a data factory.</span></span>
* <span data-ttu-id="3c2a3-129">**Visual Studio**您可以使用 Visual Studio toocreate Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-129">**Visual Studio** You can use Visual Studio toocreate an Azure data factory.</span></span> <span data-ttu-id="3c2a3-130">如需詳細資料，請參閱 [使用 Visual Studio 建置您的第一個資料管線](data-factory-build-your-first-pipeline-using-vs.md) 。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-130">See [Build your first data pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) for details.</span></span>
* <span data-ttu-id="3c2a3-131">**Azure PowerShell** 如需使用 PowerShell 來建立 Data Factory 的教學課程/逐步解說，請參閱 [使用 Azure PowerShell 建立和監視 Azure Data Factory](data-factory-build-your-first-pipeline-using-powershell.md) 。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-131">**Azure PowerShell** See [Create and monitor Azure Data Factory using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) for a tutorial/walkthrough for creating a data factory using PowerShell.</span></span> <span data-ttu-id="3c2a3-132">如需 Data Factory Cmdlet 的完整文件，請參閱 MSDN Library 上的 [Data Factory Cmdlet 參考][adf-powershell-reference]內容。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-132">See [Data Factory Cmdlet Reference][adf-powershell-reference] content on MSDN Library for a comprehensive documentation of Data Factory cmdlets.</span></span>
* <span data-ttu-id="3c2a3-133">**.NET 類別庫** 您可以使用 Data Factory .NET SDK，透過程式設計方式建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-133">**.NET Class Library** You can programmatically create data factories by using Data Factory .NET SDK.</span></span> <span data-ttu-id="3c2a3-134">如需使用 .NET SDK 建立 Data Factory 的逐步解說，請參閱 [使用 .NET SDK 建立、監視和管理 Data Factory](data-factory-create-data-factories-programmatically.md) 。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-134">See [Create, monitor, and manage data factories using .NET SDK](data-factory-create-data-factories-programmatically.md) for a walkthrough of creating a data factory using .NET SDK.</span></span> <span data-ttu-id="3c2a3-135">如需 Data Factory .NET SDK 的完整文件，請參閱 [Data Factory 類別庫參考][msdn-class-library-reference]。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-135">See [Data Factory Class Library Reference][msdn-class-library-reference] for a comprehensive documentation of Data Factory .NET SDK.</span></span>
* <span data-ttu-id="3c2a3-136">**REST API**您也可以使用 hello hello Azure Data Factory 服務 toocreate 所公開的 REST API 和部署資料處理站。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-136">**REST API** You can also use hello REST API exposed by hello Azure Data Factory service toocreate and deploy data factories.</span></span> <span data-ttu-id="3c2a3-137">如需 Data Factory REST API 的完整文件，請參閱 [Data Factory REST API 參考][msdn-rest-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-137">See [Data Factory REST API Reference][msdn-rest-api-reference] for a comprehensive documentation of Data Factory REST API.</span></span>
* <span data-ttu-id="3c2a3-138">**Azure Resource Manager 範本** 請參閱 [教學課程：使用 Azure Resource Manager 範本建置您的第一個 Azure Data Factory](data-factory-build-your-first-pipeline-using-arm.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-138">**Azure Resource Manager Template** See [Tutorial: Build your first Azure data factory using Azure Resource Manager template](data-factory-build-your-first-pipeline-using-arm.md) fo details.</span></span>

### <a name="can-i-rename-a-data-factory"></a><span data-ttu-id="3c2a3-139">我是否可以重新命名資料處理站？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-139">Can I rename a data factory?</span></span>
<span data-ttu-id="3c2a3-140">否。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-140">No.</span></span> <span data-ttu-id="3c2a3-141">如同其他 Azure 資源，就無法變更 hello Azure data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-141">Like other Azure resources, hello name of an Azure data factory cannot be changed.</span></span>

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a><span data-ttu-id="3c2a3-142">可以從一個 Azure 訂用帳戶 tooanother 移動 data factory 嗎？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-142">Can I move a data factory from one Azure subscription tooanother?</span></span>
<span data-ttu-id="3c2a3-143">是。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-143">Yes.</span></span> <span data-ttu-id="3c2a3-144">使用 hello**移動**hello 下列圖表所示，您的資料處理站刀鋒視窗上按鈕：</span><span class="sxs-lookup"><span data-stu-id="3c2a3-144">Use hello **Move** button on your data factory blade as shown in hello following diagram:</span></span>

![移動 Data Factory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a><span data-ttu-id="3c2a3-146">支援的 Data Factory 的 hello 計算環境有哪些？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-146">What are hello compute environments supported by Data Factory?</span></span>
<span data-ttu-id="3c2a3-147">hello 下表提供支援的 Data Factory 和 hello 的活動可以在其上執行的運算環境的清單。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-147">hello following table provides a list of compute environments supported by Data Factory and hello activities that can run on them.</span></span>

| <span data-ttu-id="3c2a3-148">計算環境</span><span class="sxs-lookup"><span data-stu-id="3c2a3-148">Compute environment</span></span> | <span data-ttu-id="3c2a3-149">活動</span><span class="sxs-lookup"><span data-stu-id="3c2a3-149">activities</span></span> |
| --- | --- |
| <span data-ttu-id="3c2a3-150">[隨選 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="3c2a3-150">[On-demand HDInsight cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="3c2a3-151">[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="3c2a3-151">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="3c2a3-152">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="3c2a3-152">Azure Batch</span></span>](data-factory-compute-linked-services.md#azure-batch-linked-service) |[<span data-ttu-id="3c2a3-153">DotNet</span><span class="sxs-lookup"><span data-stu-id="3c2a3-153">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="3c2a3-154">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c2a3-154">Azure Machine Learning</span></span>](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[<span data-ttu-id="3c2a3-155">Machine Learning 活動︰批次執行和更新資源</span><span class="sxs-lookup"><span data-stu-id="3c2a3-155">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="3c2a3-156">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3c2a3-156">Azure Data Lake Analytics</span></span>](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="3c2a3-157">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="3c2a3-157">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="3c2a3-158">[Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service)、[Azure SQL 資料倉儲](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service)、[SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="3c2a3-158">[Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service)</span></span> |[<span data-ttu-id="3c2a3-159">預存程序</span><span class="sxs-lookup"><span data-stu-id="3c2a3-159">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a><span data-ttu-id="3c2a3-160">Azure Data Factory 相較於 SQL Server Integration Services (SSIS) 有何異同？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-160">How does Azure Data Factory compare with SQL Server Integration Services (SSIS)?</span></span> 
<span data-ttu-id="3c2a3-161">請參閱 hello [vs Azure Data Factory。SSIS 的比較 (英文)](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS)。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-161">See hello [Azure Data Factory vs. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) presentation from one of our MVPs (Most Valued Professionals): Reza Rad.</span></span> <span data-ttu-id="3c2a3-162">某些 hello Data Factory 中最近的變更可能不會列在 hello powerpoint 投影片中。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-162">Some of hello recent changes in Data Factory may not be listed in hello slide deck.</span></span> <span data-ttu-id="3c2a3-163">我們會持續新增更多的功能 tooAzure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-163">We are continuously adding more capabilities tooAzure Data Factory.</span></span> <span data-ttu-id="3c2a3-164">我們會持續新增更多的功能 tooAzure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-164">We are continuously adding more capabilities tooAzure Data Factory.</span></span> <span data-ttu-id="3c2a3-165">我們將會併入這些更新的資料整合技術，來自 Microsoft 的 hello 比較今年一段時間。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-165">We will incorporate these updates into hello comparison of data integration technologies from Microsoft sometime later this year.</span></span>   

## <a name="activities---faq"></a><span data-ttu-id="3c2a3-166">活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c2a3-166">Activities - FAQ</span></span>
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a><span data-ttu-id="3c2a3-167">Hello 不同類型的活動，您可以使用 Data Factory 管線中有哪些？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-167">What are hello different types of activities you can use in a Data Factory pipeline?</span></span>
* <span data-ttu-id="3c2a3-168">[資料移動活動](data-factory-data-movement-activities.md)toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-168">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data.</span></span>
* <span data-ttu-id="3c2a3-169">[資料轉換活動](data-factory-data-transformation-activities.md)tooprocess/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-169">[Data Transformation Activities](data-factory-data-transformation-activities.md) tooprocess/transform data.</span></span>

### <a name="when-does-an-activity-run"></a><span data-ttu-id="3c2a3-170">何時執行活動？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-170">When does an activity run?</span></span>
<span data-ttu-id="3c2a3-171">hello**可用性**hello 中的組態設定輸出資料表格決定 hello 活動執行時。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-171">hello **availability** configuration setting in hello output data table determines when hello activity is run.</span></span> <span data-ttu-id="3c2a3-172">如果未指定輸入資料集，hello 活動會檢查是否可滿足所有 hello 輸入的資料的相依性 (也就是**準備**狀態) 開始執行之前。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-172">If input datasets are specified, hello activity checks whether all hello input data dependencies are satisfied (that is, **Ready** state) before it starts running.</span></span>

## <a name="copy-activity---faq"></a><span data-ttu-id="3c2a3-173">複製活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c2a3-173">Copy Activity - FAQ</span></span>
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a><span data-ttu-id="3c2a3-174">它是較佳 toohave 具有多個活動的管線或不同的管線的每個活動嗎？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-174">Is it better toohave a pipeline with multiple activities or a separate pipeline for each activity?</span></span>
<span data-ttu-id="3c2a3-175">管線應該 toobundle 相關活動。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-175">Pipelines are supposed toobundle related activities.</span></span> <span data-ttu-id="3c2a3-176">如果 hello 管線外的任何其他活動不到連接它們的 hello 資料集，則可以在一個管保留 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-176">If hello datasets that connect them are not consumed by any other activity outside hello pipeline, you can keep hello activities in one pipeline.</span></span> <span data-ttu-id="3c2a3-177">如此一來，您不需要 toochain 管線作用期，讓它們彼此對齊。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-177">This way, you would not need toochain pipeline active periods so that they align with each other.</span></span> <span data-ttu-id="3c2a3-178">此外，更新 hello 管線時，會進一步保留 hello hello 資料表內部 toohello 管線中的資料完整性。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-178">Also, hello data integrity in hello tables internal toohello pipeline is better preserved when updating hello pipeline.</span></span> <span data-ttu-id="3c2a3-179">管線更新基本上停止 hello 管線中的所有 hello 活動，並移除並重新建立它們。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-179">Pipeline update essentially stops all hello activities within hello pipeline, removes them, and creates them again.</span></span> <span data-ttu-id="3c2a3-180">從撰寫觀點來看，它可能也會更容易 toosee hello 資料流程內 hello 相關的活動，在一個 JSON 檔案 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-180">From authoring perspective, it might also be easier toosee hello flow of data within hello related activities in one JSON file for hello pipeline.</span></span>

### <a name="what-are-hello-supported-data-stores"></a><span data-ttu-id="3c2a3-181">什麼是 hello 支援資料存放區？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-181">What are hello supported data stores?</span></span>
<span data-ttu-id="3c2a3-182">Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-182">Copy Activity in Data Factory copies data from a source data store tooa sink data store.</span></span> <span data-ttu-id="3c2a3-183">Data Factory 支援下列資料存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-183">Data Factory supports hello following data stores.</span></span> <span data-ttu-id="3c2a3-184">從任何來源的資料可以寫入 tooany 接收。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-184">Data from any source can be written tooany sink.</span></span> <span data-ttu-id="3c2a3-185">按一下 資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-185">Click a data store toolearn how toocopy data tooand from that store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="3c2a3-186">資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-186">Data stores with * can be on-premises or on Azure IaaS, and require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="what-are-hello-supported-file-formats"></a><span data-ttu-id="3c2a3-187">什麼是 hello 支援的檔案格式？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-187">What are hello supported file formats?</span></span>
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a><span data-ttu-id="3c2a3-188">Hello 複製作業在執行？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-188">Where is hello copy operation performed?</span></span>
<span data-ttu-id="3c2a3-189">如需詳細資料，請參閱 [全域可用的資料移動](data-factory-data-movement-activities.md#global) 一節。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-189">See [Globally available data movement](data-factory-data-movement-activities.md#global) section for details.</span></span> <span data-ttu-id="3c2a3-190">簡單地說，如果包含在內部部署資料存放區，hello 複製作業是由 hello 資料管理閘道器在內部部署環境中執行。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-190">In short, when an on-premises data store is involved, hello copy operation is performed by hello Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="3c2a3-191">與兩個 cloud 商店之間 hello 資料移動時，會在 hello 區域最接近 toohello 接收位置在 hello 執行 hello 複製作業相同的地理位置。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-191">And, when hello data movement is between two cloud stores, hello copy operation is performed in hello region closest toohello sink location in hello same geography.</span></span>

## <a name="hdinsight-activity---faq"></a><span data-ttu-id="3c2a3-192">HDInsight 活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c2a3-192">HDInsight Activity - FAQ</span></span>
### <a name="what-regions-are-supported-by-hdinsight"></a><span data-ttu-id="3c2a3-193">HDInsight 支援哪些區域？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-193">What regions are supported by HDInsight?</span></span>
<span data-ttu-id="3c2a3-194">請參閱 hello hello 下列文章中的各地區上市區段： 或[HDInsight 定價詳細資料][hdinsight-supported-regions]。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-194">See hello Geographic Availability section in hello following article: or [HDInsight Pricing Details][hdinsight-supported-regions].</span></span>

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="3c2a3-195">隨選 HDInsight 叢集使用哪一個區域？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-195">What region is used by an on-demand HDInsight cluster?</span></span>
<span data-ttu-id="3c2a3-196">hello 隨選 HDInsight 叢集建立在 hello 相同 hello 指定 toobe hello 叢集搭配使用的儲存體所在的區域。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-196">hello on-demand HDInsight cluster is created in hello same region where hello storage you specified toobe used with hello cluster exists.</span></span>    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a><span data-ttu-id="3c2a3-197">如何 tooassociate 額外的儲存體帳戶 tooyour HDInsight 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-197">How tooassociate additional storage accounts tooyour HDInsight cluster?</span></span>
<span data-ttu-id="3c2a3-198">如果您使用您自己的 HDInsight 叢集 (BYOC-攜帶您自己的叢集)，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c2a3-198">If you are using your own HDInsight Cluster (BYOC - Bring Your Own Cluster), see hello following topics:</span></span>

* <span data-ttu-id="3c2a3-199">[搭配使用 HDInsight 叢集與替代儲存體帳戶和中繼存放區][hdinsight-alternate-storage]</span><span class="sxs-lookup"><span data-stu-id="3c2a3-199">[Using an HDInsight Cluster with Alternate Storage Accounts and Metastores][hdinsight-alternate-storage]</span></span>
* <span data-ttu-id="3c2a3-200">[搭配使用其他儲存體帳戶與 HDInsight Hive][hdinsight-alternate-storage-2]</span><span class="sxs-lookup"><span data-stu-id="3c2a3-200">[Use Additional Storage Accounts with HDInsight Hive][hdinsight-alternate-storage-2]</span></span>

<span data-ttu-id="3c2a3-201">如果您使用隨叢集所建立的 hello Data Factory 服務，指定額外的儲存體帳戶的 hello HDInsight 連結服務，以便 hello Data Factory 服務可以代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-201">If you are using an on-demand cluster that is created by hello Data Factory service, specify additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="3c2a3-202">在 hello hello 視連結服務的 JSON 定義中，使用**additionalLinkedServiceNames**屬性 toospecify 替代儲存體帳戶中 hello 下列 JSON 片段所示：</span><span class="sxs-lookup"><span data-stu-id="3c2a3-202">In hello JSON definition for hello on-demand linked service, use **additionalLinkedServiceNames** property toospecify alternate storage accounts as shown in hello following JSON snippet:</span></span>

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
<span data-ttu-id="3c2a3-203">在 hello 上述範例中，otherLinkedServiceName1 和 otherLinkedServiceName2 表示連結的服務，其定義包含 hello HDInsight 叢集的需求 tooaccess 替代儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-203">In hello example above, otherLinkedServiceName1 and otherLinkedServiceName2 represent linked services whose definitions contain credentials that hello HDInsight cluster needs tooaccess alternate storage accounts.</span></span>

## <a name="slices---faq"></a><span data-ttu-id="3c2a3-204">配量 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="3c2a3-204">Slices - FAQ</span></span>
### <a name="why-are-my-input-slices-not-in-ready-state"></a><span data-ttu-id="3c2a3-205">為什麼我的輸入配量不是處於「就緒」狀態？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-205">Why are my input slices not in Ready state?</span></span>
<span data-ttu-id="3c2a3-206">常見的錯誤不設定**外部**屬性太**true** hello hello 輸入資料時，輸入資料集是外部 toohello 資料處理站 （未 hello 資料處理站所產生）。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-206">A common mistake is not setting **external** property too**true** on hello input dataset when hello input data is external toohello data factory (not produced by hello data factory).</span></span>

<span data-ttu-id="3c2a3-207">在下列範例的 hello，因此您只需要 tooset**外部**上的 tootrue **dataset1**。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-207">In hello following example, you only need tooset **external** tootrue on **dataset1**.</span></span>  

<span data-ttu-id="3c2a3-208">**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4</span><span class="sxs-lookup"><span data-stu-id="3c2a3-208">**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4</span></span>

<span data-ttu-id="3c2a3-209">如果您有與管線採用 dataset4 （管線 1 的 data factory 中的 2 所產生） 的另一個資料處理站時，將 dataset4 標示為外部資料集因為 hello 資料集由不同的資料處理站產生 （DataFactory1、 不 DataFactory2）。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-209">If you have another data factory with a pipeline that takes dataset4 (produced by pipeline 2 in data factory 1), mark dataset4 as an external dataset because hello dataset is produced by a different data factory (DataFactory1, not DataFactory2).</span></span>  

<span data-ttu-id="3c2a3-210">**DataFactory2**  </span><span class="sxs-lookup"><span data-stu-id="3c2a3-210">**DataFactory2**  </span></span>  
<span data-ttu-id="3c2a3-211">Pipeline 1: dataset4->activity4->dataset5</span><span class="sxs-lookup"><span data-stu-id="3c2a3-211">Pipeline 1: dataset4->activity4->dataset5</span></span>

<span data-ttu-id="3c2a3-212">如果 hello 外部屬性的設定正確，請確認 hello 輸入的資料是否存在於 hello hello 輸入資料集定義中指定的位置。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-212">If hello external property is properly set, verify whether hello input data exists in hello location specified in hello input dataset definition.</span></span>

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a><span data-ttu-id="3c2a3-213">如何在其他時間比午夜當 hello 配量每天產生配量 toorun 嗎？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-213">How toorun a slice at another time than midnight when hello slice is being produced daily?</span></span>
<span data-ttu-id="3c2a3-214">使用 hello**位移**想 hello 配量 toobe 屬性 toospecify hello 時間所產生。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-214">Use hello **offset** property toospecify hello time at which you want hello slice toobe produced.</span></span> <span data-ttu-id="3c2a3-215">如需有關此屬性的詳細資料，請參閱 [資料集可用性](data-factory-create-datasets.md#dataset-availability) 一節。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-215">See [Dataset availability](data-factory-create-datasets.md#dataset-availability) section for details about this property.</span></span> <span data-ttu-id="3c2a3-216">以下是一個簡短的範例：</span><span class="sxs-lookup"><span data-stu-id="3c2a3-216">Here is a quick example:</span></span>

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
<span data-ttu-id="3c2a3-217">每日的配量開始**上午 6 點**而不是 hello 預設午夜。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-217">Daily slices start at **6 AM** instead of hello default midnight.</span></span>     

### <a name="how-can-i-rerun-a-slice"></a><span data-ttu-id="3c2a3-218">如何重新執行配量？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-218">How can I rerun a slice?</span></span>
<span data-ttu-id="3c2a3-219">您可以重新執行配量 hello 下列方式之一：</span><span class="sxs-lookup"><span data-stu-id="3c2a3-219">You can rerun a slice in one of hello following ways:</span></span>

* <span data-ttu-id="3c2a3-220">使用監視和管理應用程式 toorerun 活動視窗或配量。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-220">Use Monitor and Manage App toorerun an activity window or slice.</span></span> <span data-ttu-id="3c2a3-221">如需相關指示，請參閱 [重新執行已選取的活動時段](data-factory-monitor-manage-app.md#perform-batch-actions) 。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-221">See [Rerun selected activity windows](data-factory-monitor-manage-app.md#perform-batch-actions) for instructions.</span></span>   
* <span data-ttu-id="3c2a3-222">按一下**執行**hello 命令列上 hello**資料配量**hello Azure 入口網站中的 hello 配量的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-222">Click **Run** in hello command bar on hello **DATA SLICE** blade for hello slice in hello Azure portal.</span></span>
* <span data-ttu-id="3c2a3-223">執行**組 AzureRmDataFactorySliceStatus**狀態的 cmdlet 設定得**等候**hello 配量。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-223">Run **Set-AzureRmDataFactorySliceStatus** cmdlet with Status set too**Waiting** for hello slice.</span></span>   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
<span data-ttu-id="3c2a3-224">請參閱[組 AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] hello cmdlet 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-224">See [Set-AzureRmDataFactorySliceStatus][set-azure-datafactory-slice-status] for details about hello cmdlet.</span></span>

### <a name="how-long-did-it-take-tooprocess-a-slice"></a><span data-ttu-id="3c2a3-225">時間長度沒有花費 tooprocess 配量？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-225">How long did it take tooprocess a slice?</span></span>
<span data-ttu-id="3c2a3-226">您可以使用活動 Windows 檔案總管 中監視和管理 App tooknow 多久花費 tooprocess 資料配量。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-226">Use Activity Window Explorer in Monitor & Manage App tooknow how long it took tooprocess a data slice.</span></span> <span data-ttu-id="3c2a3-227">如需詳細資料，請參閱 [活動時段總管](data-factory-monitor-manage-app.md#activity-window-explorer) 。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-227">See [Activity Window Explorer](data-factory-monitor-manage-app.md#activity-window-explorer) for details.</span></span>

<span data-ttu-id="3c2a3-228">您也可以執行下列 hello Azure 入口網站中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c2a3-228">You can also do hello following in hello Azure portal:</span></span>  

1. <span data-ttu-id="3c2a3-229">按一下**資料集**磚 hello **DATA FACTORY** data factory 的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-229">Click **Datasets** tile on hello **DATA FACTORY** blade for your data factory.</span></span>
2. <span data-ttu-id="3c2a3-230">按一下特定的資料集 hello 上 hello**資料集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-230">Click hello specific dataset on hello **Datasets** blade.</span></span>
3. <span data-ttu-id="3c2a3-231">選取 hello 配量您感興趣的 hello**最近配量**清單上 hello**資料表**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-231">Select hello slice that you are interested in from hello **Recent slices** list on hello **TABLE** blade.</span></span>
4. <span data-ttu-id="3c2a3-232">按一下從 hello 執行 hello 活動**活動執行**清單上 hello**資料配量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-232">Click hello activity run from hello **Activity Runs** list on hello **DATA SLICE** blade.</span></span>
5. <span data-ttu-id="3c2a3-233">按一下**屬性**磚 hello**活動執行詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-233">Click **Properties** tile on hello **ACTIVITY RUN DETAILS** blade.</span></span>
6. <span data-ttu-id="3c2a3-234">您應該會看見 hello**持續時間**欄位的值。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-234">You should see hello **DURATION** field with a value.</span></span> <span data-ttu-id="3c2a3-235">此值為 hello 時間 tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-235">This value is hello time taken tooprocess hello slice.</span></span>   

### <a name="how-toostop-a-running-slice"></a><span data-ttu-id="3c2a3-236">如何執行配量 toostop 嗎？</span><span class="sxs-lookup"><span data-stu-id="3c2a3-236">How toostop a running slice?</span></span>
<span data-ttu-id="3c2a3-237">如果您需要 toostop hello 管線執行時，您可以使用[暫停 AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-237">If you need toostop hello pipeline from executing, you can use [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet.</span></span> <span data-ttu-id="3c2a3-238">目前，暫停 hello 管線不會停止進行中的 hello 配量執行。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-238">Currently, suspending hello pipeline does not stop hello slice executions that are in progress.</span></span> <span data-ttu-id="3c2a3-239">完成 hello 進行中執行時，任何額外的配量所不挑選。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-239">Once hello in-progress executions finish, no extra slice is picked up.</span></span>

<span data-ttu-id="3c2a3-240">如果您真的想 toostop 所有 hello 執行立即，hello 方式只會 toodelete hello 管線，再重新建立。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-240">If you really want toostop all hello executions immediately, hello only way would be toodelete hello pipeline and create it again.</span></span> <span data-ttu-id="3c2a3-241">如果您選擇 toodelete hello 管線，您不需要 toodelete 資料表及連結的 hello 管線所使用的服務。</span><span class="sxs-lookup"><span data-stu-id="3c2a3-241">If you choose toodelete hello pipeline, you do NOT need toodelete tables and linked services used by hello pipeline.</span></span>

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
