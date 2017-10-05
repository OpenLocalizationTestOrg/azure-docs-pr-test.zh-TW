---
title: "資料轉換︰處理和轉換資料 | Microsoft Docs"
description: "了解如何使用 Hadoop、Machine Learning 或 Azure Data Lake Analytics 在 Azure Data Factory 中轉換資料或處理資料。"
keywords: "資料轉換, 處理資料, 轉換資料, 轉換活動"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 7fc30f32b5038467b3474d89311dc51e182c6e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-in-azure-data-factory"></a><span data-ttu-id="4e249-104">Azure Data Factory 中的資料轉換</span><span class="sxs-lookup"><span data-stu-id="4e249-104">Transform data in Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e249-105">Hive</span><span class="sxs-lookup"><span data-stu-id="4e249-105">Hive</span></span>](data-factory-hive-activity.md)  
> * [<span data-ttu-id="4e249-106">Pig</span><span class="sxs-lookup"><span data-stu-id="4e249-106">Pig</span></span>](data-factory-pig-activity.md)  
> * [<span data-ttu-id="4e249-107">MapReduce</span><span class="sxs-lookup"><span data-stu-id="4e249-107">MapReduce</span></span>](data-factory-map-reduce.md)  
> * [<span data-ttu-id="4e249-108">Hadoop 串流</span><span class="sxs-lookup"><span data-stu-id="4e249-108">Hadoop Streaming</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4e249-109">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="4e249-109">Machine Learning</span></span>](data-factory-azure-ml-batch-execution-activity.md) 
> * [<span data-ttu-id="4e249-110">預存程序</span><span class="sxs-lookup"><span data-stu-id="4e249-110">Stored Procedure</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4e249-111">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e249-111">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4e249-112">.NET 自訂</span><span class="sxs-lookup"><span data-stu-id="4e249-112">.NET custom</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="4e249-113">概觀</span><span class="sxs-lookup"><span data-stu-id="4e249-113">Overview</span></span>
<span data-ttu-id="4e249-114">本文說明 Azure Data Factory 中的資料轉換活動，您可用來轉換未經處理資料，並將其處理為預測和見解。</span><span class="sxs-lookup"><span data-stu-id="4e249-114">This article explains data transformation activities in Azure Data Factory that you can use to transform and processes your raw data into predictions and insights.</span></span> <span data-ttu-id="4e249-115">轉換活動會在計算環境中執行，例如 Azure HDInsight 叢集或 Azure Batch。</span><span class="sxs-lookup"><span data-stu-id="4e249-115">A transformation activity executes in a computing environment such as Azure HDInsight cluster or an Azure Batch.</span></span> <span data-ttu-id="4e249-116">它會提供每個轉換活動的詳細資訊文章連結。</span><span class="sxs-lookup"><span data-stu-id="4e249-116">It provides links to articles with detailed information on each transformation activity.</span></span>

<span data-ttu-id="4e249-117">Data Factory 支援下列可個別或與其他活動鏈結而加入至 [管線](data-factory-create-pipelines.md) 的資料轉換活動。</span><span class="sxs-lookup"><span data-stu-id="4e249-117">Data Factory supports the following data transformation activities that can be added to [pipelines](data-factory-create-pipelines.md) either individually or chained with another activity.</span></span>

> [!NOTE]
> <span data-ttu-id="4e249-118">如需逐步解說，請參閱 [建立可 Hive 轉換的管線](data-factory-build-your-first-pipeline.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-118">For a walkthrough with step-by-step instructions, see [Create a pipeline with Hive transformation](data-factory-build-your-first-pipeline.md) article.</span></span>  
> 
> 

## <a name="hdinsight-hive-activity"></a><span data-ttu-id="4e249-119">HDInsight Hive 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-119">HDInsight Hive activity</span></span>
<span data-ttu-id="4e249-120">Data Factory 管線中的 HDInsight Hive 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="4e249-120">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4e249-121">如需此活動的詳細資訊，請參閱 [Hive 活動](data-factory-hive-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-121">See [Hive Activity](data-factory-hive-activity.md) article for details about this activity.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="4e249-122">HDInsight Pig 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-122">HDInsight Pig activity</span></span>
<span data-ttu-id="4e249-123">Data Factory 管線中的 HDInsight Pig 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Pig 查詢。</span><span class="sxs-lookup"><span data-stu-id="4e249-123">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4e249-124">如需此活動的詳細資訊，請參閱 [Pig 活動](data-factory-pig-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-124">See [Pig Activity](data-factory-pig-activity.md) article for details about this activity.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="4e249-125">HDInsight MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-125">HDInsight MapReduce activity</span></span>
<span data-ttu-id="4e249-126">Data Factory 管線中的 HDInsight MapReduce 活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="4e249-126">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4e249-127">如需此活動的詳細資訊，請參閱 [MapReduce 活動](data-factory-map-reduce.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-127">See [MapReduce Activity](data-factory-map-reduce.md) article for details about this activity.</span></span>

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="4e249-128">HDInsight 串流活動</span><span class="sxs-lookup"><span data-stu-id="4e249-128">HDInsight Streaming activity</span></span>
<span data-ttu-id="4e249-129">Data Factory 管線中的 HDInsight 串流活動會在您自己或隨選的 Windows/Linux 架構 HDInsight 叢集上執行 Hadoop 串流程式。</span><span class="sxs-lookup"><span data-stu-id="4e249-129">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4e249-130">如需此活動的詳細資訊，請參閱 [HDInsight 串流活動](data-factory-hadoop-streaming-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-130">See [HDInsight Streaming activity](data-factory-hadoop-streaming-activity.md) for details about this activity.</span></span>

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="4e249-131">HDInsight Spark 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-131">HDInsight Spark Activity</span></span>
<span data-ttu-id="4e249-132">Data Factory 管線中的 HDInsight Spark 活動會在您自己的 HDInsight 叢集上執行 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="4e249-132">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> <span data-ttu-id="4e249-133">如需詳細資訊，請參閱[從 Azure Data Factory 叫用 Spark 程式](data-factory-spark.md)。</span><span class="sxs-lookup"><span data-stu-id="4e249-133">For details, see [Invoke Spark programs from Azure Data Factory](data-factory-spark.md).</span></span> 

## <a name="machine-learning-activities"></a><span data-ttu-id="4e249-134">Machine Learning 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-134">Machine Learning activities</span></span>
<span data-ttu-id="4e249-135">Azure Data Factory 可讓您輕鬆地建立管線，使用已發佈的 Azure Machine Learning Web 服務進行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="4e249-135">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="4e249-136">在 Azure Data Factory 管線中使用 [批次執行活動](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) ，您可以叫用 Machine Learning Web 服務來對批次中的資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="4e249-136">Using the [Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span>

<span data-ttu-id="4e249-137">經過一段時間，必須使用新的輸入資料集重新訓練 Machine Learning 評分實驗中的預測模型。</span><span class="sxs-lookup"><span data-stu-id="4e249-137">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="4e249-138">完成重新訓練之後，您想要使用已重新訓練的 Machine Learning 模型來更新評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4e249-138">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="4e249-139">您可以使用 [更新資源活動](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) ，以新訓練的模型更新 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4e249-139">You can use the [Update Resource Activity](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) to update the web service with the newly trained model.</span></span>  

<span data-ttu-id="4e249-140">如需這些機器學習活動的詳細資料，請參閱 [使用 Machine Learning 活動](data-factory-azure-ml-batch-execution-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-140">See [Use Machine Learning activities](data-factory-azure-ml-batch-execution-activity.md) for details about these Machine Learning activities.</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="4e249-141">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="4e249-141">Stored procedure activity</span></span>
<span data-ttu-id="4e249-142">您可以在 Data Factory 管線中使用 SQL Server 的預存程序活動，以叫用下列其中一個資料存放區中的預存程序：您的企業或 Azure VM 中的 Azure SQL Database、Azure SQL 資料倉儲、SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4e249-142">You can use the SQL Server Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> <span data-ttu-id="4e249-143">如需詳細資料，請參閱 [預存程序活動](data-factory-stored-proc-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-143">See [Stored Procedure Activity](data-factory-stored-proc-activity.md) article for details.</span></span>  

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="4e249-144">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="4e249-144">Data Lake Analytics U-SQL activity</span></span>
<span data-ttu-id="4e249-145">Data Lake Analytics U-SQL 活動會在 Azure Data Lake Analytics 叢集上執行 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4e249-145">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span> <span data-ttu-id="4e249-146">如需詳細資料，請參閱 [U-SQL 活動](data-factory-usql-activity.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-146">See [Data Analytics U-SQL Activity](data-factory-usql-activity.md) article for details.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="4e249-147">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="4e249-147">.NET custom activity</span></span>
<span data-ttu-id="4e249-148">如果您需要以 Data Factory 不支援的方法轉換資料，可以利用自己的資料處理邏輯建立自訂活動，然後在管線中使用活動。</span><span class="sxs-lookup"><span data-stu-id="4e249-148">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="4e249-149">您可以將自訂 .NET 活動設定為使用 Azure Batch 服務或 Azure HDInsight 叢集來執行。</span><span class="sxs-lookup"><span data-stu-id="4e249-149">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> <span data-ttu-id="4e249-150">如需詳細資訊請參閱 [使用自訂活動](data-factory-use-custom-activities.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e249-150">See [Use custom activities](data-factory-use-custom-activities.md) article for details.</span></span> 

<span data-ttu-id="4e249-151">您可以建立自訂活動，以便在已安裝 R 的 HDInsight 叢集上執行 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4e249-151">You can create a custom activity to run R scripts on your HDInsight cluster with R installed.</span></span> <span data-ttu-id="4e249-152">請參閱 [使用 Azure Data Factory 執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。</span><span class="sxs-lookup"><span data-stu-id="4e249-152">See [Run R Script using Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="4e249-153">計算環境</span><span class="sxs-lookup"><span data-stu-id="4e249-153">Compute environments</span></span>
<span data-ttu-id="4e249-154">您需要為計算環境建立連結服務，然後在定義轉換活動時使用該連結服務。</span><span class="sxs-lookup"><span data-stu-id="4e249-154">You create a linked service for the compute environment and then use the linked service when defining a transformation activity.</span></span> <span data-ttu-id="4e249-155">Data Factory 支援兩種類型的資計算環境。</span><span class="sxs-lookup"><span data-stu-id="4e249-155">There are two types of compute environments supported by Data Factory.</span></span> 

1. <span data-ttu-id="4e249-156">**隨選**：在此情況下，運算環境完全由 Data Factory 進行管理。</span><span class="sxs-lookup"><span data-stu-id="4e249-156">**On-Demand**:  In this case, the computing environment is fully managed by Data Factory.</span></span> <span data-ttu-id="4e249-157">Data Factory 服務會在工作提交前自動建立運算環境以處理資料，而在工作完成時予以移除。</span><span class="sxs-lookup"><span data-stu-id="4e249-157">It is automatically created by the Data Factory service before a job is submitted to process data and removed when the job is completed.</span></span> <span data-ttu-id="4e249-158">您可以針對工作執行、叢集管理及啟動載入動作，設定和控制隨選計算環境的細微設定。</span><span class="sxs-lookup"><span data-stu-id="4e249-158">You can configure and control granular settings of the on-demand compute environment for job execution, cluster management, and bootstrapping actions.</span></span> 
2. <span data-ttu-id="4e249-159">**攜帶您自己的裝置**：在此情況下，您可以註冊自己的運算環境 (例如 HDInsight 叢集)，做為 Data Factory 中的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4e249-159">**Bring Your Own**: In this case, you can register your own computing environment (for example HDInsight cluster) as a linked service in Data Factory.</span></span> <span data-ttu-id="4e249-160">運算環境由您自行管理，而 Data Factory 會使用它來執行活動。</span><span class="sxs-lookup"><span data-stu-id="4e249-160">The computing environment is managed by you and the Data Factory service uses it to execute the activities.</span></span> 

<span data-ttu-id="4e249-161">如需了解 Data Factory 所支援的計算服務，請參閱 [計算連結服務](data-factory-compute-linked-services.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="4e249-161">See [Compute Linked Services](data-factory-compute-linked-services.md) article to learn about compute services supported by Data Factory.</span></span> 

## <a name="summary"></a><span data-ttu-id="4e249-162">摘要</span><span class="sxs-lookup"><span data-stu-id="4e249-162">Summary</span></span>
<span data-ttu-id="4e249-163">Azure Data Factory 支援下列資料轉換活動和活動計算環境。</span><span class="sxs-lookup"><span data-stu-id="4e249-163">Azure Data Factory supports the following data transformation activities and the compute environments for the activities.</span></span> <span data-ttu-id="4e249-164">可將轉換活動個別加入管線，或先與其他活動鏈結再加入管線。</span><span class="sxs-lookup"><span data-stu-id="4e249-164">The transformation activities can be added to pipelines either individually or chained with another activity.</span></span>

| <span data-ttu-id="4e249-165">資料轉換活動</span><span class="sxs-lookup"><span data-stu-id="4e249-165">Data transformation activity</span></span> | <span data-ttu-id="4e249-166">計算環境</span><span class="sxs-lookup"><span data-stu-id="4e249-166">Compute environment</span></span> |
|:--- |:--- |
| [<span data-ttu-id="4e249-167">Hive</span><span class="sxs-lookup"><span data-stu-id="4e249-167">Hive</span></span>](data-factory-hive-activity.md) |<span data-ttu-id="4e249-168">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="4e249-168">HDInsight [Hadoop]</span></span> |
| [<span data-ttu-id="4e249-169">Pig</span><span class="sxs-lookup"><span data-stu-id="4e249-169">Pig</span></span>](data-factory-pig-activity.md) |<span data-ttu-id="4e249-170">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="4e249-170">HDInsight [Hadoop]</span></span> |
| [<span data-ttu-id="4e249-171">MapReduce</span><span class="sxs-lookup"><span data-stu-id="4e249-171">MapReduce</span></span>](data-factory-map-reduce.md) |<span data-ttu-id="4e249-172">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="4e249-172">HDInsight [Hadoop]</span></span> |
| [<span data-ttu-id="4e249-173">Hadoop 串流</span><span class="sxs-lookup"><span data-stu-id="4e249-173">Hadoop Streaming</span></span>](data-factory-hadoop-streaming-activity.md) |<span data-ttu-id="4e249-174">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="4e249-174">HDInsight [Hadoop]</span></span> |
| [<span data-ttu-id="4e249-175">Machine Learning 活動︰批次執行和更新資源</span><span class="sxs-lookup"><span data-stu-id="4e249-175">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |<span data-ttu-id="4e249-176">Azure VM</span><span class="sxs-lookup"><span data-stu-id="4e249-176">Azure VM</span></span> |
| [<span data-ttu-id="4e249-177">預存程序</span><span class="sxs-lookup"><span data-stu-id="4e249-177">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |<span data-ttu-id="4e249-178">Azure SQL、Azure SQL 資料倉儲或 SQL Server</span><span class="sxs-lookup"><span data-stu-id="4e249-178">Azure SQL, Azure SQL Data Warehouse, or SQL Server</span></span> |
| [<span data-ttu-id="4e249-179">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e249-179">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |<span data-ttu-id="4e249-180">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4e249-180">Azure Data Lake Analytics</span></span> |
| [<span data-ttu-id="4e249-181">DotNet</span><span class="sxs-lookup"><span data-stu-id="4e249-181">DotNet</span></span>](data-factory-use-custom-activities.md) |<span data-ttu-id="4e249-182">HDInsight [Hadoop] 或 Azure Batch</span><span class="sxs-lookup"><span data-stu-id="4e249-182">HDInsight [Hadoop] or Azure Batch</span></span> |

