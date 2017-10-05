---
title: "Data Factory 教學課程︰第一個資料管線 | Microsoft Docs"
description: "此 Azure Data Factory 教學課程會示範如何使用 Hadoop 叢集上的 Hive 指令碼，建立和排程處理資料的 Data Factory。"
services: data-factory
keywords: "azure data factory 教學課程, hadoop 叢集, hadoop hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 08e2988d455cca21726162d9fb128e91fd51f463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-pipeline-to-transform-data-using-hadoop-cluster"></a><span data-ttu-id="70037-104">教學課程︰使用 Hadoop 叢集建置您的第一個管線來轉換資料</span><span class="sxs-lookup"><span data-stu-id="70037-104">Tutorial: Build your first pipeline to transform data using Hadoop cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70037-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="70037-105">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="70037-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70037-106">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="70037-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70037-107">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="70037-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70037-108">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="70037-109">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="70037-109">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="70037-110">REST API</span><span class="sxs-lookup"><span data-stu-id="70037-110">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="70037-111">在本教學課程中，您會使用資料管線建立您的第一個 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="70037-111">In this tutorial, you build your first Azure data factory with a data pipeline.</span></span> <span data-ttu-id="70037-112">管線藉由在 Azure HDInsight (Hadoop) 叢集上執行 Hive 指令碼，來將輸入資料轉換成輸出資料。</span><span class="sxs-lookup"><span data-stu-id="70037-112">The pipeline transforms input data by running Hive script on an Azure HDInsight (Hadoop) cluster to produce output data.</span></span>  

<span data-ttu-id="70037-113">本文提供教學課程的概觀與必要條件。</span><span class="sxs-lookup"><span data-stu-id="70037-113">This article provides overview and prerequisites for the tutorial.</span></span> <span data-ttu-id="70037-114">完成必要條件之後，您可以使用下列其中一個工具/SDK 來進行教學課程：Azure 入口網站、Visual Studio、PowerShell、Resource Manager 範本、REST API。</span><span class="sxs-lookup"><span data-stu-id="70037-114">After you complete the prerequisites, you can do the tutorial using one of the following tools/SDKs: Azure portal, Visual Studio, PowerShell, Resource Manager template, REST API.</span></span> <span data-ttu-id="70037-115">選取文章開頭下拉式清單中的選項，或是選取文章結尾的連結來進行教學課程。</span><span class="sxs-lookup"><span data-stu-id="70037-115">Select one of the options in the drop-down list at the beginning (or) links at the end of this article to do the tutorial using one of these options.</span></span>    

## <a name="tutorial-overview"></a><span data-ttu-id="70037-116">教學課程概觀</span><span class="sxs-lookup"><span data-stu-id="70037-116">Tutorial overview</span></span>
<span data-ttu-id="70037-117">在本教學課程中，您會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="70037-117">In this tutorial, you perform the following steps:</span></span>

1. <span data-ttu-id="70037-118">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="70037-118">Create a **data factory**.</span></span> <span data-ttu-id="70037-119">資料處理站可以包含一或多個資料管線，可移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="70037-119">A data factory can contain one or more data pipelines that move and transform data.</span></span> 

    <span data-ttu-id="70037-120">在本教學課程中，您會在資料處理站中建立一個管線。</span><span class="sxs-lookup"><span data-stu-id="70037-120">In this tutorial, you create one pipeline in the data factory.</span></span> 
2. <span data-ttu-id="70037-121">建立 **管線**。</span><span class="sxs-lookup"><span data-stu-id="70037-121">Create a **pipeline**.</span></span> <span data-ttu-id="70037-122">管線可以有一或多個活動 (範例︰複製活動、HDInsight Hive 活動)。</span><span class="sxs-lookup"><span data-stu-id="70037-122">A pipeline can have one or more activities (Examples: Copy Activity, HDInsight Hive Activity).</span></span> <span data-ttu-id="70037-123">本範例使用在 HDInsight Hadoop 叢集上執行 Hive 指令碼的 HDInsight Hive 活動。</span><span class="sxs-lookup"><span data-stu-id="70037-123">This sample uses the HDInsight Hive activity that runs a Hive script on a HDInsight Hadoop cluster.</span></span> <span data-ttu-id="70037-124">指令碼首先會建立一個參照儲存在 Azure Blob 儲存體中的原始 Web 記錄資料的資料表，再依年份或月份分割未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="70037-124">The script first creates a table that references the raw web log data stored in Azure blob storage and then partitions the raw data by year and month.</span></span>

    <span data-ttu-id="70037-125">在本教學課程中，管線使用 Hive 活動來轉換資料，方法是在 Azure HDInsight Hadoop 叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="70037-125">In this tutorial, the pipeline uses the Hive Activity to transform data by running a Hive query on an Azure HDInsight Hadoop cluster.</span></span> 
3. <span data-ttu-id="70037-126">建立 **連結服務**。</span><span class="sxs-lookup"><span data-stu-id="70037-126">Create **linked services**.</span></span> <span data-ttu-id="70037-127">您會建立一個連結的服務，以將資料存放區或計算服務連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="70037-127">You create a linked service to link a data store or a compute service to the data factory.</span></span> <span data-ttu-id="70037-128">像是 Azure 儲存體的資料存放區會保留管線中的活動輸入/輸出資料。</span><span class="sxs-lookup"><span data-stu-id="70037-128">A data store such as Azure Storage holds input/output data of activities in the pipeline.</span></span> <span data-ttu-id="70037-129">計算服務 (例如 HDInsight Hadoop 叢集) 會處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="70037-129">A compute service such as HDInsight Hadoop cluster processes/transforms data.</span></span>

    <span data-ttu-id="70037-130">在本教學課程中，您會建立兩個「連結服務」：**Azure 儲存體** 和 **Azure HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="70037-130">In this tutorial, you create two linked services: **Azure Storage** and **Azure HDInsight**.</span></span> <span data-ttu-id="70037-131">Azure 儲存體已連結的服務會連結提供資料處理站輸入/輸出資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70037-131">The Azure Storage linked service links an Azure Storage Account that holds the input/output data to the data factory.</span></span> <span data-ttu-id="70037-132">Azure HDInsight 已連結的服務會連將資料轉換到資料處理站的 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="70037-132">Azure HDInsight linked service links an Azure HDInsight cluster that is used to transform data to the data factory.</span></span> 
3. <span data-ttu-id="70037-133">建立輸入和輸出 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="70037-133">Create input and output **datasets**.</span></span> <span data-ttu-id="70037-134">輸入資料集表示管線中的活動輸入，而輸出資料集表示活動的輸出。</span><span class="sxs-lookup"><span data-stu-id="70037-134">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span>

    <span data-ttu-id="70037-135">在本教學課程中，輸入和輸出資料集是指定 Azure Blob 儲存體中輸入和輸出資料的位置。</span><span class="sxs-lookup"><span data-stu-id="70037-135">In this tutorial, the input and output datasets specify locations of input and output data in the Azure Blob Storage.</span></span> <span data-ttu-id="70037-136">Azure 儲存體連結服務會指定要使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70037-136">The Azure Storage linked service specifies what Azure Storage Account is used.</span></span> <span data-ttu-id="70037-137">輸入資料集會指定輸入資料所在的位置，而輸出資料集則指定放置輸出資料的位置。</span><span class="sxs-lookup"><span data-stu-id="70037-137">An input dataset specifies where the input files are located and an output dataset specifies where the output files are placed.</span></span> 


<span data-ttu-id="70037-138">如需 Azure Data Factory 的詳細概觀，請參閱 [Azure Data Factory 簡介](data-factory-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="70037-138">See [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of Azure Data Factory.</span></span>
  
<span data-ttu-id="70037-139">以下是您在本教學課程中建置的範例 Data Factory 的 **圖表檢視** 。</span><span class="sxs-lookup"><span data-stu-id="70037-139">Here is the **diagram view** of the sample data factory you build in this tutorial.</span></span> <span data-ttu-id="70037-140">**MyFirstPipeline** 有一個 Hive 類型的活動，可接收 **AzureBlobInput** 資料集做為輸入，並輸出 **AzureBlobOutput** 資料集。</span><span class="sxs-lookup"><span data-stu-id="70037-140">**MyFirstPipeline** has one activity of type Hive that consumes **AzureBlobInput** dataset as an input and produces **AzureBlobOutput** dataset as an output.</span></span> 

![Data Factory 教學課程中的圖表檢視](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


<span data-ttu-id="70037-142">在本教學課程中，**adfgetstarted** Azure Blob 容器的 **inputdata** 資料夾包含一個名為 input.log 的檔案。</span><span class="sxs-lookup"><span data-stu-id="70037-142">In this tutorial, **inputdata** folder of the **adfgetstarted** Azure blob container contains one file named input.log.</span></span> <span data-ttu-id="70037-143">此記錄檔包含三個月的項目，分別是：2016 年 1 月、2 月和 3 月。</span><span class="sxs-lookup"><span data-stu-id="70037-143">This log file has entries from three months: January, February, and March of 2016.</span></span> <span data-ttu-id="70037-144">這裡是輸入檔中每個月份的資料列範例。</span><span class="sxs-lookup"><span data-stu-id="70037-144">Here are the sample rows for each month in the input file.</span></span> 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="70037-145">當管線使用 HDInsight Hive 活動處理檔案時，活動會在依年份和月份分割輸入資料的 HDInsight 叢集中執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="70037-145">When the file is processed by the pipeline with HDInsight Hive Activity, the activity runs a Hive script on the HDInsight cluster that partitions input data by year and month.</span></span> <span data-ttu-id="70037-146">指令碼會建立三個輸出資料夾，包含每個月份項目的檔案。</span><span class="sxs-lookup"><span data-stu-id="70037-146">The script creates three output folders that contain a file with entries from each month.</span></span>  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

<span data-ttu-id="70037-147">如上所示的範例行中，第一行 (標有 2016-01-01) 會寫入 month=1 資料夾中的 000000_0 檔案。</span><span class="sxs-lookup"><span data-stu-id="70037-147">From the sample lines shown above, the first one (with 2016-01-01) is written to the 000000_0 file in the month=1 folder.</span></span> <span data-ttu-id="70037-148">同樣地，第二行會寫入 month=2 資料夾中的檔案；而第三行會寫入 month=3 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="70037-148">Similarly, the second one is written to the file in the month=2 folder and the third one is written to the file in the month=3 folder.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="70037-149">必要條件</span><span class="sxs-lookup"><span data-stu-id="70037-149">Prerequisites</span></span>
<span data-ttu-id="70037-150">開始進行本教學課程之前，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="70037-150">Before you begin this tutorial, you must have the following prerequisites:</span></span>

1. <span data-ttu-id="70037-151">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70037-151">**Azure subscription** - If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="70037-152">請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/) 一文了解如何取得免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70037-152">See the [Free Trial](https://azure.microsoft.com/pricing/free-trial/) article on how you can obtain a free trial account.</span></span>
2. <span data-ttu-id="70037-153">**Azure 儲存體** - 在本教學課程中，您會使用一般目的標準 Azure 儲存體帳戶來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="70037-153">**Azure Storage** – You use a general-purpose standard Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="70037-154">如果您沒有一般目的標準 Azure 儲存體帳戶，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)一文。</span><span class="sxs-lookup"><span data-stu-id="70037-154">If you don't have a general-purpose standard Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="70037-155">建立儲存體帳戶之後，請記下**帳戶名稱**和**存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="70037-155">After you have created the storage account, note down the **account name** and **access key**.</span></span> <span data-ttu-id="70037-156">請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="70037-156">See [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>
3. <span data-ttu-id="70037-157">下載並檢閱 Hive 查詢檔案 (**HQL**)，檔案位在：[https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql)。</span><span class="sxs-lookup"><span data-stu-id="70037-157">Download and review the Hive query file (**HQL**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span></span> <span data-ttu-id="70037-158">這個查詢會轉換輸入資料並產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="70037-158">This query transforms input data to produce output data.</span></span> 
4. <span data-ttu-id="70037-159">下載並檢閱範例輸入檔案 (**input.log**)，檔案位在：[https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span><span class="sxs-lookup"><span data-stu-id="70037-159">Download and review the sample input file (**input.log**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span></span>
5. <span data-ttu-id="70037-160">在您的 Azure Blob 儲存體中建立名為 **adfgetstarted** 的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="70037-160">Create a blob container named **adfgetstarted** in your Azure Blob Storage.</span></span> 
6. <span data-ttu-id="70037-161">將 **partitionweblogs.hql** 檔案上傳到 **adfgetstarted** 容器的 [script] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="70037-161">Upload **partitionweblogs.hql** file to the **script** folder in the **adfgetstarted** container.</span></span> <span data-ttu-id="70037-162">使用類似 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)的工具。</span><span class="sxs-lookup"><span data-stu-id="70037-162">Use tools such as [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 
7. <span data-ttu-id="70037-163">將 **input.log** 檔案上傳到 **adfgetstarted** 容器中的 [inputdata] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="70037-163">Upload **input.log** file to the **inputdata** folder in the **adfgetstarted** container.</span></span> 

<span data-ttu-id="70037-164">完成必要條件之後，選取下列其中一個工具/SDK 來進行教學課程：</span><span class="sxs-lookup"><span data-stu-id="70037-164">After you complete the prerequisites, select one of the following tools/SDKs to do the tutorial:</span></span> 

- [<span data-ttu-id="70037-165">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70037-165">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
- [<span data-ttu-id="70037-166">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70037-166">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
- [<span data-ttu-id="70037-167">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70037-167">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
- [<span data-ttu-id="70037-168">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="70037-168">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
- [<span data-ttu-id="70037-169">REST API</span><span class="sxs-lookup"><span data-stu-id="70037-169">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="70037-170">Azure 入口網站和 Visual Studio 可讓您透過 GUI 建置資料處理站。</span><span class="sxs-lookup"><span data-stu-id="70037-170">Azure portal and Visual Studio provide GUI way of building your data factories.</span></span> <span data-ttu-id="70037-171">而 PowerShell、Resource Manager 範本和 REST API，則可讓您選擇以撰寫指令碼/程式碼的方式來建置資料處理站。</span><span class="sxs-lookup"><span data-stu-id="70037-171">Whereas, PowerShell, Resource Manager Template, and REST API options provides scripting/programming way of building your data factories.</span></span>

> [!NOTE]
> <span data-ttu-id="70037-172">本教學課程中的資料管線會轉換輸入資料來產生輸出資料，</span><span class="sxs-lookup"><span data-stu-id="70037-172">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="70037-173">它不是將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="70037-173">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="70037-174">如需說明如何使用 Azure Data Factory 複製資料的教學課程，請參閱[教學課程：將資料從 Blob 儲存體複製到 SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="70037-174">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="70037-175">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="70037-175">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="70037-176">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="70037-176">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 





  
