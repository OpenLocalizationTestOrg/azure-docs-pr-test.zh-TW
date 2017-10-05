---
title: "Azure 資料處理站-常見問題集"
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
ms.openlocfilehash: 086e6b2fb9bd0ee8541401b6f0d65268926e45a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a><span data-ttu-id="6e361-103">Azure 資料處理站-常見問題集</span><span class="sxs-lookup"><span data-stu-id="6e361-103">Azure Data Factory - Frequently Asked Questions</span></span>
## <a name="general-questions"></a><span data-ttu-id="6e361-104">一般問題</span><span class="sxs-lookup"><span data-stu-id="6e361-104">General questions</span></span>
### <a name="what-is-azure-data-factory"></a><span data-ttu-id="6e361-105">Azure 資料處理站是什麼？</span><span class="sxs-lookup"><span data-stu-id="6e361-105">What is Azure Data Factory?</span></span>
<span data-ttu-id="6e361-106">Data Factory 是雲端架構資料整合服務，用來 **自動移動和轉換資料**。</span><span class="sxs-lookup"><span data-stu-id="6e361-106">Data Factory is a cloud-based data integration service that **automates the movement and transformation of data**.</span></span> <span data-ttu-id="6e361-107">就像會運轉設備以將原物料轉換成成品的工廠一樣，Data Factory 會協調現有的服務來收集未經處理資料，並將之轉換成隨時可用的資訊。</span><span class="sxs-lookup"><span data-stu-id="6e361-107">Just like a factory that runs equipment to take raw materials and transform them into finished goods, Data Factory orchestrates existing services that collect raw data and transform it into ready-to-use information.</span></span>

<span data-ttu-id="6e361-108">Data Factory 可讓您建立資料導向工作流程，不僅可透過計算服務 (例如 Azure HDInsight 和 Azure Data Lake Analytics) 來處理/轉換資料，還能在內部部署與雲端資料存放區之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="6e361-108">Data Factory allows you to create data-driven workflows to move data between both on-premises and cloud data stores as well as process/transform data using compute services such as Azure HDInsight and Azure Data Lake Analytics.</span></span> <span data-ttu-id="6e361-109">建立可執行您所需動作的管線之後，您可以排定讓它定期執行 (每小時、每天、每週等)。</span><span class="sxs-lookup"><span data-stu-id="6e361-109">After you create a pipeline that performs the action that you need, you can schedule it to run periodically (hourly, daily, weekly etc.).</span></span>   

<span data-ttu-id="6e361-110">如需詳細資訊，請參閱[概觀與重要概念](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6e361-110">For more information, see [Overview & Key Concepts](data-factory-introduction.md).</span></span>

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a><span data-ttu-id="6e361-111">哪裡可以找到 Azure 資料處理站的定價詳細資料？</span><span class="sxs-lookup"><span data-stu-id="6e361-111">Where can I find pricing details for Azure Data Factory?</span></span>
<span data-ttu-id="6e361-112">請參閱 [Data Factory 定價詳細資料頁面][adf-pricing-details]，以了解 Azure Data Factory 的定價詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6e361-112">See [Data Factory Pricing Details page][adf-pricing-details] for the pricing details for the Azure Data Factory.</span></span>  

### <a name="how-do-i-get-started-with-azure-data-factory"></a><span data-ttu-id="6e361-113">如何開始使用 Azure Data Factory？</span><span class="sxs-lookup"><span data-stu-id="6e361-113">How do I get started with Azure Data Factory?</span></span>
* <span data-ttu-id="6e361-114">如需 Azure Data Factory 的概觀，請參閱 [Azure Data Factory 簡介](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6e361-114">For an overview of Azure Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md).</span></span>
* <span data-ttu-id="6e361-115">如需說明如何使用複製活動 **複製/移動資料** 的教學課程，請參閱 [將資料從 Azure Blob 儲存體複製到 Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="6e361-115">For a tutorial on how to **copy/move data** using Copy Activity, see [Copy data from Azure Blob Storage to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="6e361-116">如需說明如何使用 HDInsight Hive 活動 **轉換資料** 的教學課程。</span><span class="sxs-lookup"><span data-stu-id="6e361-116">For a tutorial on how to **transform data** using HDInsight Hive Activity.</span></span> <span data-ttu-id="6e361-117">請參閱 [在 Hadoop 叢集上執行 Hive 指令碼來處理資料](data-factory-build-your-first-pipeline.md)</span><span class="sxs-lookup"><span data-stu-id="6e361-117">See [Process data by running Hive script on Hadoop cluster](data-factory-build-your-first-pipeline.md)</span></span>

### <a name="what-is-the-data-factorys-region-availability"></a><span data-ttu-id="6e361-118">什麼是資料處理站的區域可用性？</span><span class="sxs-lookup"><span data-stu-id="6e361-118">What is the Data Factory’s region availability?</span></span>
<span data-ttu-id="6e361-119">Data Factory 可在**美國西部**和**北歐**地區使用。</span><span class="sxs-lookup"><span data-stu-id="6e361-119">Data Factory is available in **US West** and **North Europe**.</span></span> <span data-ttu-id="6e361-120">資料處理站所使用的計算服務和儲存體服務可以在其他區域使用。</span><span class="sxs-lookup"><span data-stu-id="6e361-120">The compute and storage services used by data factories can be in other regions.</span></span> <span data-ttu-id="6e361-121">請參閱 [支援的區域](data-factory-introduction.md#supported-regions)。</span><span class="sxs-lookup"><span data-stu-id="6e361-121">See [Supported regions](data-factory-introduction.md#supported-regions).</span></span>

### <a name="what-are-the-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a><span data-ttu-id="6e361-122">資料處理站/管線/活動/資料集的數量有什麼限制？</span><span class="sxs-lookup"><span data-stu-id="6e361-122">What are the limits on number of data factories/pipelines/activities/datasets?</span></span>
<span data-ttu-id="6e361-123">請參閱〈 **Azure 訂用帳戶和服務限制、配額及條件約束** 〉中的〈 [Azure Data Factory 限制](../azure-subscription-service-limits.md#data-factory-limits) 〉章節。</span><span class="sxs-lookup"><span data-stu-id="6e361-123">See **Azure Data Factory Limits** section of the [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md#data-factory-limits) article.</span></span>

### <a name="what-is-the-authoringdeveloper-experience-with-azure-data-factory-service"></a><span data-ttu-id="6e361-124">Azure Data Factory 服務的撰寫/開發人員經驗為何？</span><span class="sxs-lookup"><span data-stu-id="6e361-124">What is the authoring/developer experience with Azure Data Factory service?</span></span>
<span data-ttu-id="6e361-125">您可以使用下列其中一個工具/SDK 來製作/建立資料處理站：</span><span class="sxs-lookup"><span data-stu-id="6e361-125">You can author/create data factories using one of the following tools/SDKs:</span></span>

* <span data-ttu-id="6e361-126">**Azure 入口網站** Azure 入口網站中的 Data Factory 刀鋒視窗提供豐富的使用者介面，可讓您建立 Data Factory 和連結的服務。</span><span class="sxs-lookup"><span data-stu-id="6e361-126">**Azure portal** The Data Factory blades in the Azure portal provide rich user interface for you to create data factories ad linked services.</span></span> <span data-ttu-id="6e361-127">**Data Factory 編輯器**也是入口網站的一部分，讓您透過指定成品的 JSON 定義，輕鬆建立連結服務、資料表、資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="6e361-127">The **Data Factory Editor**, which is also part of the portal, allows you to easily create linked services, tables, data sets, and pipelines by specifying JSON definitions for these artifacts.</span></span> <span data-ttu-id="6e361-128">如需使用入口網站/編輯器來建立和部署 Data Factory 的範例，請參閱 [使用 Azure 入口網站建置您的第一個資料管線](data-factory-build-your-first-pipeline-using-editor.md) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-128">See [Build your first data pipeline using Azure portal](data-factory-build-your-first-pipeline-using-editor.md) for an example of using the portal/editor to create and deploy a data factory.</span></span>
* <span data-ttu-id="6e361-129">**Visual Studio** 您可以使用 Visual Studio 建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6e361-129">**Visual Studio** You can use Visual Studio to create an Azure data factory.</span></span> <span data-ttu-id="6e361-130">如需詳細資料，請參閱 [使用 Visual Studio 建置您的第一個資料管線](data-factory-build-your-first-pipeline-using-vs.md) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-130">See [Build your first data pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) for details.</span></span>
* <span data-ttu-id="6e361-131">**Azure PowerShell** 如需使用 PowerShell 來建立 Data Factory 的教學課程/逐步解說，請參閱 [使用 Azure PowerShell 建立和監視 Azure Data Factory](data-factory-build-your-first-pipeline-using-powershell.md) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-131">**Azure PowerShell** See [Create and monitor Azure Data Factory using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) for a tutorial/walkthrough for creating a data factory using PowerShell.</span></span> <span data-ttu-id="6e361-132">如需 Data Factory Cmdlet 的完整文件，請參閱 MSDN Library 上的 [Data Factory Cmdlet 參考][adf-powershell-reference]內容。</span><span class="sxs-lookup"><span data-stu-id="6e361-132">See [Data Factory Cmdlet Reference][adf-powershell-reference] content on MSDN Library for a comprehensive documentation of Data Factory cmdlets.</span></span>
* <span data-ttu-id="6e361-133">**.NET 類別庫** 您可以使用 Data Factory .NET SDK，透過程式設計方式建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6e361-133">**.NET Class Library** You can programmatically create data factories by using Data Factory .NET SDK.</span></span> <span data-ttu-id="6e361-134">如需使用 .NET SDK 建立 Data Factory 的逐步解說，請參閱 [使用 .NET SDK 建立、監視和管理 Data Factory](data-factory-create-data-factories-programmatically.md) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-134">See [Create, monitor, and manage data factories using .NET SDK](data-factory-create-data-factories-programmatically.md) for a walkthrough of creating a data factory using .NET SDK.</span></span> <span data-ttu-id="6e361-135">如需 Data Factory .NET SDK 的完整文件，請參閱 [Data Factory 類別庫參考][msdn-class-library-reference]。</span><span class="sxs-lookup"><span data-stu-id="6e361-135">See [Data Factory Class Library Reference][msdn-class-library-reference] for a comprehensive documentation of Data Factory .NET SDK.</span></span>
* <span data-ttu-id="6e361-136">**REST API** 您也可以使用 Azure Data Factory 服務所公開的 REST API 來建立和部署 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6e361-136">**REST API** You can also use the REST API exposed by the Azure Data Factory service to create and deploy data factories.</span></span> <span data-ttu-id="6e361-137">如需 Data Factory REST API 的完整文件，請參閱 [Data Factory REST API 參考][msdn-rest-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="6e361-137">See [Data Factory REST API Reference][msdn-rest-api-reference] for a comprehensive documentation of Data Factory REST API.</span></span>
* <span data-ttu-id="6e361-138">**Azure Resource Manager 範本** 請參閱 [教學課程：使用 Azure Resource Manager 範本建置您的第一個 Azure Data Factory](data-factory-build-your-first-pipeline-using-arm.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6e361-138">**Azure Resource Manager Template** See [Tutorial: Build your first Azure data factory using Azure Resource Manager template](data-factory-build-your-first-pipeline-using-arm.md) fo details.</span></span>

### <a name="can-i-rename-a-data-factory"></a><span data-ttu-id="6e361-139">我是否可以重新命名資料處理站？</span><span class="sxs-lookup"><span data-stu-id="6e361-139">Can I rename a data factory?</span></span>
<span data-ttu-id="6e361-140">否。</span><span class="sxs-lookup"><span data-stu-id="6e361-140">No.</span></span> <span data-ttu-id="6e361-141">和其他 Azure 資源一樣，您無法變更 Azure Data Factory 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6e361-141">Like other Azure resources, the name of an Azure data factory cannot be changed.</span></span>

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-to-another"></a><span data-ttu-id="6e361-142">我是否可以將 Data Factory 從一個 Azure 訂用帳戶移至另一個訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="6e361-142">Can I move a data factory from one Azure subscription to another?</span></span>
<span data-ttu-id="6e361-143">是。</span><span class="sxs-lookup"><span data-stu-id="6e361-143">Yes.</span></span> <span data-ttu-id="6e361-144">請使用您資料處理站刀鋒視窗上的 [移動] 按鈕，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="6e361-144">Use the **Move** button on your data factory blade as shown in the following diagram:</span></span>

![移動 Data Factory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-the-compute-environments-supported-by-data-factory"></a><span data-ttu-id="6e361-146">Data Factory 支援什麼計算環境?</span><span class="sxs-lookup"><span data-stu-id="6e361-146">What are the compute environments supported by Data Factory?</span></span>
<span data-ttu-id="6e361-147">下表列出 Data Factory 支援的計算環境以及可在環境上執行的活動。</span><span class="sxs-lookup"><span data-stu-id="6e361-147">The following table provides a list of compute environments supported by Data Factory and the activities that can run on them.</span></span>

| <span data-ttu-id="6e361-148">計算環境</span><span class="sxs-lookup"><span data-stu-id="6e361-148">Compute environment</span></span> | <span data-ttu-id="6e361-149">活動</span><span class="sxs-lookup"><span data-stu-id="6e361-149">activities</span></span> |
| --- | --- |
| <span data-ttu-id="6e361-150">[隨選 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)或[您自己的 HDInsight 叢集](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="6e361-150">[On-demand HDInsight cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="6e361-151">[DotNet](data-factory-use-custom-activities.md)、[Hive](data-factory-hive-activity.md)、[Pig](data-factory-pig-activity.md)、[MapReduce](data-factory-map-reduce.md)、[Hadoop 串流](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="6e361-151">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="6e361-152">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="6e361-152">Azure Batch</span></span>](data-factory-compute-linked-services.md#azure-batch-linked-service) |[<span data-ttu-id="6e361-153">DotNet</span><span class="sxs-lookup"><span data-stu-id="6e361-153">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="6e361-154">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6e361-154">Azure Machine Learning</span></span>](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[<span data-ttu-id="6e361-155">Machine Learning 活動︰批次執行和更新資源</span><span class="sxs-lookup"><span data-stu-id="6e361-155">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="6e361-156">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6e361-156">Azure Data Lake Analytics</span></span>](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="6e361-157">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="6e361-157">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="6e361-158">[Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service)、[Azure SQL 資料倉儲](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service)、[SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="6e361-158">[Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service)</span></span> |[<span data-ttu-id="6e361-159">預存程序</span><span class="sxs-lookup"><span data-stu-id="6e361-159">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a><span data-ttu-id="6e361-160">Azure Data Factory 相較於 SQL Server Integration Services (SSIS) 有何異同？</span><span class="sxs-lookup"><span data-stu-id="6e361-160">How does Azure Data Factory compare with SQL Server Integration Services (SSIS)?</span></span> 
<span data-ttu-id="6e361-161">請參閱由我們的 MVP (最有價值專家) Reza Rad 所撰寫的 [Azure Data Factory 與SSIS 的比較 (英文)](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS)。</span><span class="sxs-lookup"><span data-stu-id="6e361-161">See the [Azure Data Factory vs. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) presentation from one of our MVPs (Most Valued Professionals): Reza Rad.</span></span> <span data-ttu-id="6e361-162">Data Factory 中的某些最近變更可能未列於投影片組中。</span><span class="sxs-lookup"><span data-stu-id="6e361-162">Some of the recent changes in Data Factory may not be listed in the slide deck.</span></span> <span data-ttu-id="6e361-163">我們會持續新增更多功能到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6e361-163">We are continuously adding more capabilities to Azure Data Factory.</span></span> <span data-ttu-id="6e361-164">我們會持續新增更多功能到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="6e361-164">We are continuously adding more capabilities to Azure Data Factory.</span></span> <span data-ttu-id="6e361-165">我們會在今年將這些更新整合到 Microsoft 的資料整合技術比較中。</span><span class="sxs-lookup"><span data-stu-id="6e361-165">We will incorporate these updates into the comparison of data integration technologies from Microsoft sometime later this year.</span></span>   

## <a name="activities---faq"></a><span data-ttu-id="6e361-166">活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6e361-166">Activities - FAQ</span></span>
### <a name="what-are-the-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a><span data-ttu-id="6e361-167">您可以在 Data Factory 管線中使用的不同類型活動有哪些？</span><span class="sxs-lookup"><span data-stu-id="6e361-167">What are the different types of activities you can use in a Data Factory pipeline?</span></span>
* <span data-ttu-id="6e361-168">[資料移動活動](data-factory-data-movement-activities.md) 以移動資料。</span><span class="sxs-lookup"><span data-stu-id="6e361-168">[Data Movement Activities](data-factory-data-movement-activities.md) to move data.</span></span>
* <span data-ttu-id="6e361-169">[資料轉換活動](data-factory-data-transformation-activities.md) 以處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="6e361-169">[Data Transformation Activities](data-factory-data-transformation-activities.md) to process/transform data.</span></span>

### <a name="when-does-an-activity-run"></a><span data-ttu-id="6e361-170">何時執行活動？</span><span class="sxs-lookup"><span data-stu-id="6e361-170">When does an activity run?</span></span>
<span data-ttu-id="6e361-171">輸出資料表中的 **可用性** 組態設定決定何時執行活動。</span><span class="sxs-lookup"><span data-stu-id="6e361-171">The **availability** configuration setting in the output data table determines when the activity is run.</span></span> <span data-ttu-id="6e361-172">如果已指定輸入資料集，活動會在開始執行之前，先檢查是否滿足所有輸入資料相依性 (即「就緒」  狀態)。</span><span class="sxs-lookup"><span data-stu-id="6e361-172">If input datasets are specified, the activity checks whether all the input data dependencies are satisfied (that is, **Ready** state) before it starts running.</span></span>

## <a name="copy-activity---faq"></a><span data-ttu-id="6e361-173">複製活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6e361-173">Copy Activity - FAQ</span></span>
### <a name="is-it-better-to-have-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a><span data-ttu-id="6e361-174">最好是一個管線有多個活動，還是每個活動都有不同的管線？</span><span class="sxs-lookup"><span data-stu-id="6e361-174">Is it better to have a pipeline with multiple activities or a separate pipeline for each activity?</span></span>
<span data-ttu-id="6e361-175">管線依例應該有配套的相關活動。</span><span class="sxs-lookup"><span data-stu-id="6e361-175">Pipelines are supposed to bundle related activities.</span></span> <span data-ttu-id="6e361-176">如果管線外的任何其他活動都未使用連接它們的資料集，則您可以將活動保留在一個管線中。</span><span class="sxs-lookup"><span data-stu-id="6e361-176">If the datasets that connect them are not consumed by any other activity outside the pipeline, you can keep the activities in one pipeline.</span></span> <span data-ttu-id="6e361-177">如此一來，您就不需要鏈結管線作用期間，使其彼此一致。</span><span class="sxs-lookup"><span data-stu-id="6e361-177">This way, you would not need to chain pipeline active periods so that they align with each other.</span></span> <span data-ttu-id="6e361-178">此外，更新管線時，也會更適當地保留管線內部資料表中的資料完整性。</span><span class="sxs-lookup"><span data-stu-id="6e361-178">Also, the data integrity in the tables internal to the pipeline is better preserved when updating the pipeline.</span></span> <span data-ttu-id="6e361-179">管線更新基本上會停止、移除並重新建立管線內的所有活動。</span><span class="sxs-lookup"><span data-stu-id="6e361-179">Pipeline update essentially stops all the activities within the pipeline, removes them, and creates them again.</span></span> <span data-ttu-id="6e361-180">從撰寫觀點來看，可能也較容易看出管線的某個 JSON 檔案中相關活動內的資料流程。</span><span class="sxs-lookup"><span data-stu-id="6e361-180">From authoring perspective, it might also be easier to see the flow of data within the related activities in one JSON file for the pipeline.</span></span>

### <a name="what-are-the-supported-data-stores"></a><span data-ttu-id="6e361-181">支援哪些資料存放區？</span><span class="sxs-lookup"><span data-stu-id="6e361-181">What are the supported data stores?</span></span>
<span data-ttu-id="6e361-182">Data Factory 中的複製活動會將資料從來源資料存放區複製到接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="6e361-182">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span></span> <span data-ttu-id="6e361-183">Data Factory 支援下列資料存放區。</span><span class="sxs-lookup"><span data-stu-id="6e361-183">Data Factory supports the following data stores.</span></span> <span data-ttu-id="6e361-184">可將來自任何來源的資料寫入任何接收器。</span><span class="sxs-lookup"><span data-stu-id="6e361-184">Data from any source can be written to any sink.</span></span> <span data-ttu-id="6e361-185">按一下資料存放區，即可了解如何將資料複製到該存放區，以及從該存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="6e361-185">Click a data store to learn how to copy data to and from that store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="6e361-186">具有 * 的資料存放區可以在內部部署環境或 Azure IaaS 上，並且需要您在內部部署/Azure IaaS 機器上安裝 [資料管理閘道](data-factory-data-management-gateway.md) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-186">Data stores with * can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="what-are-the-supported-file-formats"></a><span data-ttu-id="6e361-187">支援什麼檔案格式？</span><span class="sxs-lookup"><span data-stu-id="6e361-187">What are the supported file formats?</span></span>
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-the-copy-operation-performed"></a><span data-ttu-id="6e361-188">會在哪裡執行複製作業？</span><span class="sxs-lookup"><span data-stu-id="6e361-188">Where is the copy operation performed?</span></span>
<span data-ttu-id="6e361-189">如需詳細資料，請參閱 [全域可用的資料移動](data-factory-data-movement-activities.md#global) 一節。</span><span class="sxs-lookup"><span data-stu-id="6e361-189">See [Globally available data movement](data-factory-data-movement-activities.md#global) section for details.</span></span> <span data-ttu-id="6e361-190">簡單地說，當涉及內部部署資料存放區時，複製作業是由「資料管理閘道」在內部部署環境中執行。</span><span class="sxs-lookup"><span data-stu-id="6e361-190">In short, when an on-premises data store is involved, the copy operation is performed by the Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="6e361-191">而在兩個雲端存放區之間移動資料時，複製作業是在最接近相同地理位置內接收位置的區域中執行。</span><span class="sxs-lookup"><span data-stu-id="6e361-191">And, when the data movement is between two cloud stores, the copy operation is performed in the region closest to the sink location in the same geography.</span></span>

## <a name="hdinsight-activity---faq"></a><span data-ttu-id="6e361-192">HDInsight 活動 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6e361-192">HDInsight Activity - FAQ</span></span>
### <a name="what-regions-are-supported-by-hdinsight"></a><span data-ttu-id="6e361-193">HDInsight 支援哪些區域？</span><span class="sxs-lookup"><span data-stu-id="6e361-193">What regions are supported by HDInsight?</span></span>
<span data-ttu-id="6e361-194">請參閱下列文章中的＜各地區上市情況＞一節：或 [HDInsight 定價詳細資料][hdinsight-supported-regions]。</span><span class="sxs-lookup"><span data-stu-id="6e361-194">See the Geographic Availability section in the following article: or [HDInsight Pricing Details][hdinsight-supported-regions].</span></span>

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="6e361-195">隨選 HDInsight 叢集使用哪一個區域？</span><span class="sxs-lookup"><span data-stu-id="6e361-195">What region is used by an on-demand HDInsight cluster?</span></span>
<span data-ttu-id="6e361-196">隨選 HDInsight 叢集會建立在存有您指定用來使用叢集之儲存體的位置。</span><span class="sxs-lookup"><span data-stu-id="6e361-196">The on-demand HDInsight cluster is created in the same region where the storage you specified to be used with the cluster exists.</span></span>    

### <a name="how-to-associate-additional-storage-accounts-to-your-hdinsight-cluster"></a><span data-ttu-id="6e361-197">如何讓其他儲存體帳戶與 HDInsight 叢集產生關聯？</span><span class="sxs-lookup"><span data-stu-id="6e361-197">How to associate additional storage accounts to your HDInsight cluster?</span></span>
<span data-ttu-id="6e361-198">如果您使用的是自己的「HDInsight 叢集」(BYOC - 自攜叢集)，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="6e361-198">If you are using your own HDInsight Cluster (BYOC - Bring Your Own Cluster), see the following topics:</span></span>

* <span data-ttu-id="6e361-199">[搭配使用 HDInsight 叢集與替代儲存體帳戶和中繼存放區][hdinsight-alternate-storage]</span><span class="sxs-lookup"><span data-stu-id="6e361-199">[Using an HDInsight Cluster with Alternate Storage Accounts and Metastores][hdinsight-alternate-storage]</span></span>
* <span data-ttu-id="6e361-200">[搭配使用其他儲存體帳戶與 HDInsight Hive][hdinsight-alternate-storage-2]</span><span class="sxs-lookup"><span data-stu-id="6e361-200">[Use Additional Storage Accounts with HDInsight Hive][hdinsight-alternate-storage-2]</span></span>

<span data-ttu-id="6e361-201">如果您使用的是 Data Factory 服務所建立的隨選叢集，請為 HDInsight 連結服務指定額外的儲存體帳戶，以便讓 Data Factory 服務代表您註冊它們。</span><span class="sxs-lookup"><span data-stu-id="6e361-201">If you are using an on-demand cluster that is created by the Data Factory service, specify additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="6e361-202">在隨選連結服務的 JSON 定義中，請使用 **additionalLinkedServiceNames** 屬性指定替代的儲存體帳戶，如下列 JSON 片段所示：</span><span class="sxs-lookup"><span data-stu-id="6e361-202">In the JSON definition for the on-demand linked service, use **additionalLinkedServiceNames** property to specify alternate storage accounts as shown in the following JSON snippet:</span></span>

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
<span data-ttu-id="6e361-203">在上述範例中，otherLinkedServiceName1 和 otherLinkedServiceName2 連結服務的定義，包含 HDInsight 叢集存取替代儲存體帳戶所需的認證。</span><span class="sxs-lookup"><span data-stu-id="6e361-203">In the example above, otherLinkedServiceName1 and otherLinkedServiceName2 represent linked services whose definitions contain credentials that the HDInsight cluster needs to access alternate storage accounts.</span></span>

## <a name="slices---faq"></a><span data-ttu-id="6e361-204">配量 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6e361-204">Slices - FAQ</span></span>
### <a name="why-are-my-input-slices-not-in-ready-state"></a><span data-ttu-id="6e361-205">為什麼我的輸入配量不是處於「就緒」狀態？</span><span class="sxs-lookup"><span data-stu-id="6e361-205">Why are my input slices not in Ready state?</span></span>
<span data-ttu-id="6e361-206">常見的錯誤是當輸入資料是 Data Factory 的外部資料 (不是由 Data Factory 產生) 時，未將輸入資料集上的 **external** 屬性設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="6e361-206">A common mistake is not setting **external** property to **true** on the input dataset when the input data is external to the data factory (not produced by the data factory).</span></span>

<span data-ttu-id="6e361-207">在下列範例中，您只需要將 **dataset1** 上的 **external** 設定為 true 即可。</span><span class="sxs-lookup"><span data-stu-id="6e361-207">In the following example, you only need to set **external** to true on **dataset1**.</span></span>  

<span data-ttu-id="6e361-208">**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4</span><span class="sxs-lookup"><span data-stu-id="6e361-208">**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4</span></span>

<span data-ttu-id="6e361-209">如果您有另一個 Data Factory，其管線會接受 dataset4 (由 Data Factory 1 中的 pipeline 2 產生)，請將 dataset4 標示為外部資料集，因為該資料集是由不同的 Data Factory (DataFactory1，而非 DataFactory2) 產生。</span><span class="sxs-lookup"><span data-stu-id="6e361-209">If you have another data factory with a pipeline that takes dataset4 (produced by pipeline 2 in data factory 1), mark dataset4 as an external dataset because the dataset is produced by a different data factory (DataFactory1, not DataFactory2).</span></span>  

<span data-ttu-id="6e361-210">**DataFactory2**  </span><span class="sxs-lookup"><span data-stu-id="6e361-210">**DataFactory2**  </span></span>  
<span data-ttu-id="6e361-211">Pipeline 1: dataset4->activity4->dataset5</span><span class="sxs-lookup"><span data-stu-id="6e361-211">Pipeline 1: dataset4->activity4->dataset5</span></span>

<span data-ttu-id="6e361-212">如果 external 屬性的設定正確，請確認輸入資料是否存在於輸入資料集定義中指定的位置。</span><span class="sxs-lookup"><span data-stu-id="6e361-212">If the external property is properly set, verify whether the input data exists in the location specified in the input dataset definition.</span></span>

### <a name="how-to-run-a-slice-at-another-time-than-midnight-when-the-slice-is-being-produced-daily"></a><span data-ttu-id="6e361-213">每日產生配量時，如何在午夜以外的其他時間執行配量？</span><span class="sxs-lookup"><span data-stu-id="6e361-213">How to run a slice at another time than midnight when the slice is being produced daily?</span></span>
<span data-ttu-id="6e361-214">請使用 **offset** 屬性來指定要產生配量的時間。</span><span class="sxs-lookup"><span data-stu-id="6e361-214">Use the **offset** property to specify the time at which you want the slice to be produced.</span></span> <span data-ttu-id="6e361-215">如需有關此屬性的詳細資料，請參閱 [資料集可用性](data-factory-create-datasets.md#dataset-availability) 一節。</span><span class="sxs-lookup"><span data-stu-id="6e361-215">See [Dataset availability](data-factory-create-datasets.md#dataset-availability) section for details about this property.</span></span> <span data-ttu-id="6e361-216">以下是一個簡短的範例：</span><span class="sxs-lookup"><span data-stu-id="6e361-216">Here is a quick example:</span></span>

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
<span data-ttu-id="6e361-217">每日配量於 **上午 6 點** (而非預設的午夜) 開始。</span><span class="sxs-lookup"><span data-stu-id="6e361-217">Daily slices start at **6 AM** instead of the default midnight.</span></span>     

### <a name="how-can-i-rerun-a-slice"></a><span data-ttu-id="6e361-218">如何重新執行配量？</span><span class="sxs-lookup"><span data-stu-id="6e361-218">How can I rerun a slice?</span></span>
<span data-ttu-id="6e361-219">您可以利用下列方式之一來重新執行配量：</span><span class="sxs-lookup"><span data-stu-id="6e361-219">You can rerun a slice in one of the following ways:</span></span>

* <span data-ttu-id="6e361-220">使用「監視及管理應用程式」來重新執行活動時段或配量。</span><span class="sxs-lookup"><span data-stu-id="6e361-220">Use Monitor and Manage App to rerun an activity window or slice.</span></span> <span data-ttu-id="6e361-221">如需相關指示，請參閱 [重新執行已選取的活動時段](data-factory-monitor-manage-app.md#perform-batch-actions) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-221">See [Rerun selected activity windows](data-factory-monitor-manage-app.md#perform-batch-actions) for instructions.</span></span>   
* <span data-ttu-id="6e361-222">在 Azure 入口網站中，於該配量的 [資料配量] 刀鋒視窗上，按一下命令列中的 [執行]。</span><span class="sxs-lookup"><span data-stu-id="6e361-222">Click **Run** in the command bar on the **DATA SLICE** blade for the slice in the Azure portal.</span></span>
* <span data-ttu-id="6e361-223">在配量的 Status 設定為 **Waiting** 的情況下，執行 **Set-AzureRmDataFactorySliceStatus** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e361-223">Run **Set-AzureRmDataFactorySliceStatus** cmdlet with Status set to **Waiting** for the slice.</span></span>   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
<span data-ttu-id="6e361-224">如需 Cmdlet 的詳細資料，請參閱 [Set-AzureRmDataFactorySliceStatus][set-azure-datafactory-slice-status]。</span><span class="sxs-lookup"><span data-stu-id="6e361-224">See [Set-AzureRmDataFactorySliceStatus][set-azure-datafactory-slice-status] for details about the cmdlet.</span></span>

### <a name="how-long-did-it-take-to-process-a-slice"></a><span data-ttu-id="6e361-225">處理配量需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="6e361-225">How long did it take to process a slice?</span></span>
<span data-ttu-id="6e361-226">使用「監視及管理應用程式」中的「活動時段總管」來了解處理一個資料配量所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="6e361-226">Use Activity Window Explorer in Monitor & Manage App to know how long it took to process a data slice.</span></span> <span data-ttu-id="6e361-227">如需詳細資料，請參閱 [活動時段總管](data-factory-monitor-manage-app.md#activity-window-explorer) 。</span><span class="sxs-lookup"><span data-stu-id="6e361-227">See [Activity Window Explorer](data-factory-monitor-manage-app.md#activity-window-explorer) for details.</span></span>

<span data-ttu-id="6e361-228">您也可以在 Azure 入口網站中執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="6e361-228">You can also do the following in the Azure portal:</span></span>  

1. <span data-ttu-id="6e361-229">在您 Data Factory 的 [DATA FACTORY] 刀鋒視窗中，按一下 [資料集] 圖格。</span><span class="sxs-lookup"><span data-stu-id="6e361-229">Click **Datasets** tile on the **DATA FACTORY** blade for your data factory.</span></span>
2. <span data-ttu-id="6e361-230">在 [ **資料集** ] 刀鋒視窗中，按一下特定資料集。</span><span class="sxs-lookup"><span data-stu-id="6e361-230">Click the specific dataset on the **Datasets** blade.</span></span>
3. <span data-ttu-id="6e361-231">從 [資料表] 刀鋒視窗的 [最近配量] 清單中，選取您感興趣的配量。</span><span class="sxs-lookup"><span data-stu-id="6e361-231">Select the slice that you are interested in from the **Recent slices** list on the **TABLE** blade.</span></span>
4. <span data-ttu-id="6e361-232">從 [資料配量] 刀鋒視窗的 [活動執行] 清單中，按一下活動執行。</span><span class="sxs-lookup"><span data-stu-id="6e361-232">Click the activity run from the **Activity Runs** list on the **DATA SLICE** blade.</span></span>
5. <span data-ttu-id="6e361-233">在 [活動執行詳細資料] 刀鋒視窗中，按一下 [屬性] 圖格。</span><span class="sxs-lookup"><span data-stu-id="6e361-233">Click **Properties** tile on the **ACTIVITY RUN DETAILS** blade.</span></span>
6. <span data-ttu-id="6e361-234">您應該會看到 [持續時間]  欄位與值。</span><span class="sxs-lookup"><span data-stu-id="6e361-234">You should see the **DURATION** field with a value.</span></span> <span data-ttu-id="6e361-235">這個值是處理配量所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="6e361-235">This value is the time taken to process the slice.</span></span>   

### <a name="how-to-stop-a-running-slice"></a><span data-ttu-id="6e361-236">如何停止執行中配量？</span><span class="sxs-lookup"><span data-stu-id="6e361-236">How to stop a running slice?</span></span>
<span data-ttu-id="6e361-237">如果需要停止執行管線，可以使用 [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e361-237">If you need to stop the pipeline from executing, you can use [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet.</span></span> <span data-ttu-id="6e361-238">目前，擱置管線並不會停止正在進行的配量執行。</span><span class="sxs-lookup"><span data-stu-id="6e361-238">Currently, suspending the pipeline does not stop the slice executions that are in progress.</span></span> <span data-ttu-id="6e361-239">一旦進行中的執行完成，就不會再挑選任何額外的配量。</span><span class="sxs-lookup"><span data-stu-id="6e361-239">Once the in-progress executions finish, no extra slice is picked up.</span></span>

<span data-ttu-id="6e361-240">如果真的想要立即停止所有執行作業，唯一的方法就是刪除管線，然後再重新建立。</span><span class="sxs-lookup"><span data-stu-id="6e361-240">If you really want to stop all the executions immediately, the only way would be to delete the pipeline and create it again.</span></span> <span data-ttu-id="6e361-241">如果您選擇刪除管線，則「不」需要刪除管線所使用的資料表和連結服務。</span><span class="sxs-lookup"><span data-stu-id="6e361-241">If you choose to delete the pipeline, you do NOT need to delete tables and linked services used by the pipeline.</span></span>

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
