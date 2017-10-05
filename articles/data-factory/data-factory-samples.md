---
title: "Azure Data Factory - 範例"
description: "提供 Azure Data Factory 服務隨附範例的詳細資料。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3013607e62a3ac532cb0c035130fe35e503a345c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---samples"></a><span data-ttu-id="44b4a-103">Azure Data Factory - 範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-103">Azure Data Factory - Samples</span></span>
## <a name="samples-on-github"></a><span data-ttu-id="44b4a-104">GitHub 上的範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-104">Samples on GitHub</span></span>
<span data-ttu-id="44b4a-105">[GitHub Azure-DataFactory 儲存機制](https://github.com/azure/azure-datafactory) 包含數個範例，可協助您快速運用 Azure Data Factory 服務，或修改指令碼並用在您自己的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="44b4a-105">The [GitHub Azure-DataFactory repository](https://github.com/azure/azure-datafactory) contains several samples that help you quickly ramp up with Azure Data Factory service (or) modify the scripts and use it in own application.</span></span> <span data-ttu-id="44b4a-106">Samples\JSON 資料夾包含常見案例的 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="44b4a-106">The Samples\JSON folder contains JSON snippets for common scenarios.</span></span>

| <span data-ttu-id="44b4a-107">範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-107">Sample</span></span> | <span data-ttu-id="44b4a-108">說明</span><span class="sxs-lookup"><span data-stu-id="44b4a-108">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="44b4a-109">ADF 逐步解說</span><span class="sxs-lookup"><span data-stu-id="44b4a-109">ADF Walkthrough</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |<span data-ttu-id="44b4a-110">此範例提供一個端對端逐步解說，說明如何使用 Azure Data Factory 來處理記錄檔，以將來自記錄檔的資料轉換成深入解析。</span><span class="sxs-lookup"><span data-stu-id="44b4a-110">This sample provides an end-to-end walkthrough for processing log files using Azure Data Factory to turn data from log files in to insights.</span></span> <br/><br/><span data-ttu-id="44b4a-111">在此逐步解說中，Data Factory 管線會收集範例記錄檔、處理這些記錄檔並以參考資料充實記錄檔資料，然後轉換資料以評估最近展開之行銷活動的成效。</span><span class="sxs-lookup"><span data-stu-id="44b4a-111">In this walkthrough, the Data Factory pipeline collects sample logs, processes and enriches the data from logs with reference data, and transforms the data to evaluate the effectiveness of a marketing campaign that was recently launched.</span></span> |
| [<span data-ttu-id="44b4a-112">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-112">JSON samples</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |<span data-ttu-id="44b4a-113">此範例提供常見案例的 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="44b4a-113">This sample provides JSON examples for common scenarios.</span></span> |
| [<span data-ttu-id="44b4a-114">Http 資料下載程式範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-114">Http Data Downloader Sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |<span data-ttu-id="44b4a-115">此範例展示如何使用自訂的 .NET 活動，從 HTTP 端點將資料下載到「Azure Blob 儲存體」。</span><span class="sxs-lookup"><span data-stu-id="44b4a-115">This sample showcases downloading of data from an HTTP endpoint to Azure Blob Storage using custom .NET activity.</span></span> |
| [<span data-ttu-id="44b4a-116">跨 AppDomain .NET 活動範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-116">Cross AppDomain Dot Net Activity Sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="44b4a-117">此範例可讓您撰寫不受 ADF 啟動器所使用之組件版本 (例如 WindowsAzure.Storage v4.3.0、Newtonsoft.Json v6.0.x 等) 限制的自訂 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="44b4a-117">This sample allows you to author a custom .NET activity that is not constrained to assembly versions used by the ADF launcher (For example, WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span> |
| [<span data-ttu-id="44b4a-118">執行 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="44b4a-118">Run R script</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |<span data-ttu-id="44b4a-119">此範例包含可用來叫用 RScript.exe 的 Data Factory 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="44b4a-119">This sample includes the Data Factory custom activity that can be used to invoke RScript.exe.</span></span> <span data-ttu-id="44b4a-120">此範例只能與您自己的 (非隨選) 且已安裝 R 的 HDInsight 叢集搭配運作。</span><span class="sxs-lookup"><span data-stu-id="44b4a-120">This sample works only with your own (not on-demand) HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="44b4a-121">在 HDInsight Hadoop 叢集上叫用 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="44b4a-121">Invoke Spark jobs on HDInsight Hadoop cluster</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |<span data-ttu-id="44b4a-122">此範例示範如何使用 MapReduce 活動來叫用 Spark 程式。</span><span class="sxs-lookup"><span data-stu-id="44b4a-122">This sample shows how to use MapReduce activity to invoke a Spark program.</span></span> <span data-ttu-id="44b4a-123">Spark 程式只是將資料從一個 Azure Blob 容器複製到另一個。</span><span class="sxs-lookup"><span data-stu-id="44b4a-123">The spark program just copies data from one Azure Blob container to another.</span></span> |
| [<span data-ttu-id="44b4a-124">使用 Azure Machine Learning 批次評分活動進行的 Twitter 分析</span><span class="sxs-lookup"><span data-stu-id="44b4a-124">Twitter Analysis using Azure Machine Learning Batch Scoring Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |<span data-ttu-id="44b4a-125">此範例示範如何使用 AzureMLBatchScoringActivity 來叫用執行 Twitter 情緒分析、評分、預測等的 Azure Machine Learning 模型。</span><span class="sxs-lookup"><span data-stu-id="44b4a-125">This sample shows how to use AzureMLBatchScoringActivity to invoke an Azure Machine Learning model that performs twitter sentiment analysis, scoring, prediction etc.</span></span> |
| [<span data-ttu-id="44b4a-126">使用自訂活動進行的 Twitter 分析</span><span class="sxs-lookup"><span data-stu-id="44b4a-126">Twitter Analysis using custom activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="44b4a-127">此範例示範如何使用自訂的 .NET 活動來叫用執行 Twitter 情緒分析、評分、預測等的 Azure Machine Learning 模型。</span><span class="sxs-lookup"><span data-stu-id="44b4a-127">This sample shows how to use a custom .NET activity to invoke an Azure Machine Learning model that performs twitter sentiment analysis, scoring, prediction etc.</span></span> |
| [<span data-ttu-id="44b4a-128">Azure Machine Learning 的參數化管線</span><span class="sxs-lookup"><span data-stu-id="44b4a-128">Parameterized Pipelines for Azure Machine Learning</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |<span data-ttu-id="44b4a-129">此範例提供一個端對端 C# 程式碼來部署 N 條管線，為的是以不同的區域參數來評分和重新訓練每條管線，其中區域清單是來自此檔案隨附的 parameters.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="44b4a-129">The sample provides an end-to-end C# code to deploy N pipelines for scoring and retraining each with a different region parameter where the list of regions is coming from a parameters.txt file, which is included with this sample.</span></span> |
| [<span data-ttu-id="44b4a-130">Azure 串流分析作業的參考資料重新整理</span><span class="sxs-lookup"><span data-stu-id="44b4a-130">Reference Data Refresh for Azure Stream Analytics jobs</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |<span data-ttu-id="44b4a-131">此範例示範如何使用 Azure Data Factory 搭配「Azure 串流分析」來以參考資料執行查詢，並在排程上設定參考資料重新整理。</span><span class="sxs-lookup"><span data-stu-id="44b4a-131">This sample shows how to use Azure Data Factory and Azure Stream Analytics together to run the queries with reference data and setup the refresh for reference data on a schedule.</span></span> |
| [<span data-ttu-id="44b4a-132">搭配內部部署 Hortonworks Hadoop 的混合式管線</span><span class="sxs-lookup"><span data-stu-id="44b4a-132">Hybrid Pipeline with On-premises Hortonworks Hadoop</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |<span data-ttu-id="44b4a-133">此範例使用內部部署 Hadoop 叢集做為在 Data Factory 中執行作業的運算目標，就像您會在雲端新增其他運算目標 (例如以 HDInsight 為基礎的 Hadoop 叢集) 一樣。</span><span class="sxs-lookup"><span data-stu-id="44b4a-133">The sample uses an on-premises Hadoop cluster as a compute target for running jobs in Data Factory just like you would add other compute targets like an HDInsight based Hadoop cluster in cloud.</span></span> |
| [<span data-ttu-id="44b4a-134">JSON 轉換工具</span><span class="sxs-lookup"><span data-stu-id="44b4a-134">JSON Conversion Tool</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |<span data-ttu-id="44b4a-135">此工具可讓您將 2015-07-01-preview 之前的 JSON 版本轉換成最新版本或 2015-07-01-preview (預設)。</span><span class="sxs-lookup"><span data-stu-id="44b4a-135">This tool allows you to convert JSONs from version prior to 2015-07-01-preview to latest or 2015-07-01-preview (default).</span></span> |
| [<span data-ttu-id="44b4a-136">U-SQL 範例輸入檔</span><span class="sxs-lookup"><span data-stu-id="44b4a-136">U-SQL sample input file</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |<span data-ttu-id="44b4a-137">此檔案是 U-SQL 活動所使用的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="44b4a-137">This file is a sample file used by an U-SQL activity.</span></span> |
| [<span data-ttu-id="44b4a-138">刪除 blob 檔案</span><span class="sxs-lookup"><span data-stu-id="44b4a-138">Delete blob file</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | <span data-ttu-id="44b4a-139">本範例將示範 C# 檔案，該檔案可以作為 ADF 自訂 .net 活動的一部分，以在複製檔案之後從來源 Azure Blob 位置刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="44b4a-139">This sample showcases a C# file which can be used as part of ADF custom .net activity to delete files from the source Azure Blob location once the files have been copied.</span></span>|

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="44b4a-140">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="44b4a-140">Azure Resource Manager templates</span></span>
<span data-ttu-id="44b4a-141">您可以在 GitHub 上找到下列適用於 Data Factory 的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="44b4a-141">You can find the following Azure Resource Manager templates for Data Factory on GitHub.</span></span>

| <span data-ttu-id="44b4a-142">範本</span><span class="sxs-lookup"><span data-stu-id="44b4a-142">Template</span></span> | <span data-ttu-id="44b4a-143">說明</span><span class="sxs-lookup"><span data-stu-id="44b4a-143">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="44b4a-144">從 Azure Blob 儲存體複製到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="44b4a-144">Copy from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |<span data-ttu-id="44b4a-145">部署此範本會建立 Azure Data Factory，其中有管線可將資料從指定的 Azure Blob 儲存體複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="44b4a-145">Deploying this template creates an Azure data factory with a pipeline that copies data from the specified Azure blob storage to the Azure SQL database</span></span> |
| [<span data-ttu-id="44b4a-146">從 Salesforce 複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="44b4a-146">Copy from Salesforce to Azure Blob Storage</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |<span data-ttu-id="44b4a-147">部署此範本會建立 Azure Data Factory，其中有管線可將資料從指定的 Salesforce 帳戶複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="44b4a-147">Deploying this template creates an Azure data factory with a pipeline that copies data from the specified Salesforce account to the Azure blob storage.</span></span> |
| [<span data-ttu-id="44b4a-148">在 Azure HDInsight 叢集上執行 Hive 指令碼來轉換資料</span><span class="sxs-lookup"><span data-stu-id="44b4a-148">Transform data by running Hive script on an Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |<span data-ttu-id="44b4a-149">部署此範本會建立 Azure Data Factory，其中有管線可透過在 Azure HDInsight Hadoop 叢集上執行範例 Hive 指令碼來轉換資料。</span><span class="sxs-lookup"><span data-stu-id="44b4a-149">Deploying this template creates an Azure data factory with a pipeline that transforms data by running the sample Hive script on an Azure HDInsight Hadoop cluster.</span></span> |

## <a name="samples-in-azure-portal"></a><span data-ttu-id="44b4a-150">Azure 入口網站中的範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-150">Samples in Azure portal</span></span>
<span data-ttu-id="44b4a-151">您可以使用您 Data Factory 首頁上的 [範例管線] 磚，將範例管線及其相關實體 (資料集和連結的服務) 部署到您的 Data Factory 中。</span><span class="sxs-lookup"><span data-stu-id="44b4a-151">You can use the **Sample pipelines** tile on the home page of your data factory to deploy sample pipelines and their associated entities (datasets and linked services) in to your data factory.</span></span>

1. <span data-ttu-id="44b4a-152">建立 Data Factory 或開啟現有的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="44b4a-152">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="44b4a-153">請參閱[使用 Data Factory 將資料從 Blob 儲存體複製到 SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)，以取得建立 Data Factory 的步驟。</span><span class="sxs-lookup"><span data-stu-id="44b4a-153">See [Copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps to create a data factory.</span></span>
2. <span data-ttu-id="44b4a-154">在 Data Factory 的 [DATA FACTORY] 刀鋒視窗中，按一下 [範例管線] 磚。</span><span class="sxs-lookup"><span data-stu-id="44b4a-154">In the **DATA FACTORY** blade for the data factory, click the **Sample pipelines** tile.</span></span>

    ![範例管線圖格](./media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="44b4a-156">在 [範例管線] 刀鋒視窗中，按一下您想要部署的「範例」。</span><span class="sxs-lookup"><span data-stu-id="44b4a-156">In the **Sample pipelines** blade, click the **sample** that you want to deploy.</span></span>

    ![範例管線刀鋒視窗](./media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="44b4a-158">指定範例的組態設定。</span><span class="sxs-lookup"><span data-stu-id="44b4a-158">Specify configuration settings for the sample.</span></span> <span data-ttu-id="44b4a-159">例如，您的 Azure 儲存體帳戶名稱和帳戶金鑰、Azure SQL 伺服器名稱、資料庫、使用者 ID 和密碼等。</span><span class="sxs-lookup"><span data-stu-id="44b4a-159">For example, your Azure storage account name and account key, Azure SQL server name, database, User ID, and password, etc.</span></span>

    ![範例刀鋒視窗](./media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="44b4a-161">完成指定組態設定之後，請按一下 [建立]  ，以建立/部署範例管線，以及管線所使用的連結服務/資料表。</span><span class="sxs-lookup"><span data-stu-id="44b4a-161">After you are done with specifying the configuration settings, click **Create** to create/deploy the sample pipelines and linked services/tables used by the pipelines.</span></span>
6. <span data-ttu-id="44b4a-162">您會在之前於 [範例管線]  刀鋒視窗上按下的範例磚上，看到部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="44b4a-162">You see the status of deployment on the sample tile you clicked earlier on the **Sample pipelines** blade.</span></span>

    ![部署狀態](./media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="44b4a-164">當您在範例磚上看到 [部署成功] 訊息時，請關閉 [範例管線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="44b4a-164">When you see the **Deployment succeeded** message on the tile for the sample, close the **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="44b4a-165">在 [DATA FACTORY]  刀鋒視窗上，您會看到連結的服務、資料集及管線已新增到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="44b4a-165">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added to your data factory.</span></span>  

    ![Data Factory 刀鋒視窗](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a><span data-ttu-id="44b4a-167">Visual Studio 中的範例</span><span class="sxs-lookup"><span data-stu-id="44b4a-167">Samples in Visual Studio</span></span>
### <a name="prerequisites"></a><span data-ttu-id="44b4a-168">必要條件</span><span class="sxs-lookup"><span data-stu-id="44b4a-168">Prerequisites</span></span>
<span data-ttu-id="44b4a-169">您必須已在電腦上安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="44b4a-169">You must have the following installed on your computer:</span></span>

* <span data-ttu-id="44b4a-170">Visual Studio 2013 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="44b4a-170">Visual Studio 2013 or Visual Studio 2015</span></span>
* <span data-ttu-id="44b4a-171">下載 Azure SDK for Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="44b4a-171">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="44b4a-172">瀏覽至 [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後按一下 [.NET] 區段中的 [VS 2013] 或 [VS 2015]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-172">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
* <span data-ttu-id="44b4a-173">下載適用於 Visual Studio 的最新 Azure Data Factory 外掛程式：[VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 或 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)。</span><span class="sxs-lookup"><span data-stu-id="44b4a-173">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="44b4a-174">如果您使用的是 Visual Studio 2013，您也可以執行下列步驟來更新外掛程式：在功能表上，按一下 [工具] -> [擴充功能和更新] -> [線上] -> [Visual Studio 組件庫] -> [Microsoft Azure Data Factory Tools for Visual Studio] -> [更新]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-174">If you are using Visual Studio 2013, you can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

### <a name="use-data-factory-templates"></a><span data-ttu-id="44b4a-175">使用 Data Factory 範本</span><span class="sxs-lookup"><span data-stu-id="44b4a-175">Use Data Factory Templates</span></span>
1. <span data-ttu-id="44b4a-176">在功能表上按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-176">Click **File** on the menu, point to **New**, and click **Project**.</span></span>
2. <span data-ttu-id="44b4a-177">在 [新增專案] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="44b4a-177">In the **New Project** dialog box, do the following steps:</span></span>

   1. <span data-ttu-id="44b4a-178">在 [範本] 底下選取 [DataFactory]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-178">Select **DataFactory** under **Templates**.</span></span>
   2. <span data-ttu-id="44b4a-179">在右窗格中選取 [Data Factory 範本]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-179">Select **Data Factory Templates** in the right pane.</span></span>
   3. <span data-ttu-id="44b4a-180">輸入專案的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-180">Enter a **name** for the project.</span></span>
   4. <span data-ttu-id="44b4a-181">選取專案的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-181">Select a **location** for the project.</span></span>
   5. <span data-ttu-id="44b4a-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="44b4a-182">Click **OK**.</span></span>

      ![[新增專案] 對話方塊](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. <span data-ttu-id="44b4a-184">在 [Data Factory 範本] 對話方塊中，從 [使用案例範本] 區段選取範例範本，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-184">In the **Data Factory Templates** dialog box, select the sample template from the **Use-Case Templates** section, and click **Next**.</span></span> <span data-ttu-id="44b4a-185">以下步驟將引導您完成 [客戶分析]  範本的使用。</span><span class="sxs-lookup"><span data-stu-id="44b4a-185">The following steps walk you through using the **Customer Profiling** template.</span></span> <span data-ttu-id="44b4a-186">其他範例的步驟均相去不遠。</span><span class="sxs-lookup"><span data-stu-id="44b4a-186">Steps are similar for the other samples.</span></span>

    ![Data Factory 範本對話方塊](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. <span data-ttu-id="44b4a-188">在 [Data Factory 組態] 對話方塊中，於 [Data Factory 基本] 頁面上按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-188">In the **Data Factory Configuration** dialog, click **Next** on the **Data Factory Basics** page.</span></span>
5. <span data-ttu-id="44b4a-189">在 [設定 Data Factory] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="44b4a-189">On the **Configure data factory** page, do the following steps:</span></span>
   1. <span data-ttu-id="44b4a-190">選取 [建立新的 Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-190">Select **Create New Data Factory**.</span></span> <span data-ttu-id="44b4a-191">您也可以選取 [使用現有的 Data Factory] 。</span><span class="sxs-lookup"><span data-stu-id="44b4a-191">You can also select **Use existing data factory**.</span></span>
   2. <span data-ttu-id="44b4a-192">輸入 Data Factory 的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-192">Enter a **name** for the data factory.</span></span>
   3. <span data-ttu-id="44b4a-193">選取您要在其中建立 Data Factory 的 [Azure 訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-193">Select the **Azure subscription** in which you want the data factory to be created.</span></span>
   4. <span data-ttu-id="44b4a-194">選取 Data Factory 的 [資源群組]  。</span><span class="sxs-lookup"><span data-stu-id="44b4a-194">Select the **resource group** for the data factory.</span></span>
   5. <span data-ttu-id="44b4a-195">針對 [區域]，選取 [美國西部]、[美國東部] 或 [北歐]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-195">Select the **West US**, **East US**, or **North Europe** for the **region**.</span></span>
   6. <span data-ttu-id="44b4a-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="44b4a-196">Click **Next**.</span></span>
6. <span data-ttu-id="44b4a-197">在 [設定資料存放區] 頁面中，指定現有的 [Azure SQL Database] 和 [Azure 儲存體帳戶]，或建立資料庫/儲存體，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-197">In the **Configure data stores** page, specify an existing **Azure SQL database** and **Azure storage account** (or) create database/storage, and click Next.</span></span>
7. <span data-ttu-id="44b4a-198">在 [設定計算] 頁面中，選取預設值，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-198">In the **Configure compute** page, select defaults, and click **Next**.</span></span>
8. <span data-ttu-id="44b4a-199">在 [摘要] 頁面中，檢閱所有設定，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-199">In the **Summary** page, review all settings, and click **Next**.</span></span>
9. <span data-ttu-id="44b4a-200">在 [部署狀態] 頁面中，等候部署完成，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-200">In the **Deployment Status** page, wait until the deployment is finished, and click **Finish**.</span></span>
10. <span data-ttu-id="44b4a-201">在 [方案總管] 中，以滑鼠右鍵按一下專案，再按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="44b4a-201">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
11. <span data-ttu-id="44b4a-202">如果您看到 [登入您的 Microsoft 帳戶] 對話方塊，請輸入具有 Azure 訂用帳戶的帳戶認證，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-202">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
12. <span data-ttu-id="44b4a-203">您應該會看到下列對話方塊：</span><span class="sxs-lookup"><span data-stu-id="44b4a-203">You should see the following dialog box:</span></span>

    ![發佈對話方塊](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. <span data-ttu-id="44b4a-205">在 [設定 Data Factory] 頁面中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="44b4a-205">In the **Configure data factory** page, do the following steps:</span></span>

    1. <span data-ttu-id="44b4a-206">確認 [使用現有的 Data Factory]  選項。</span><span class="sxs-lookup"><span data-stu-id="44b4a-206">Confirm that **Use existing data factory** option.</span></span>
    2. <span data-ttu-id="44b4a-207">選取您在使用範本時已選取的 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="44b4a-207">Select the **data factory** you had select when using the template.</span></span>
    3. <span data-ttu-id="44b4a-208">按 [下一步]，切換至 [發佈項目] 頁面。</span><span class="sxs-lookup"><span data-stu-id="44b4a-208">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="44b4a-209">(如果 [下一步] 按鈕已停用，請按 **TAB** 來移出 [名稱] 欄位)。</span><span class="sxs-lookup"><span data-stu-id="44b4a-209">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>
14. <span data-ttu-id="44b4a-210">在 [發佈項目] 頁面上，確認所有 Data Factory 實體都已選取，並按 [下一步] 切換至 [摘要] 頁面。</span><span class="sxs-lookup"><span data-stu-id="44b4a-210">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>     
15. <span data-ttu-id="44b4a-211">檢閱摘要，然後按 [下一步] 開始部署程序，並檢視 [部署狀態]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-211">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
16. <span data-ttu-id="44b4a-212">在 [部署狀態]  頁面上，您應該會看到部署程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="44b4a-212">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="44b4a-213">部署完成後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="44b4a-213">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="44b4a-214">如需有關使用 Visual Studio 來撰寫 Data Factory 實體並將其發行至 Azure 的詳細資料，請參閱 [建置您的第一個 Data Factory (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) 。</span><span class="sxs-lookup"><span data-stu-id="44b4a-214">See [Build your first data factory (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) for details about using Visual Studio to author Data Factory entities and publishing them to Azure.</span></span>          