---
title: "Data Factory 教學課程︰第一個資料管線 | Microsoft Docs"
description: "此 Azure Data Factory 教學課程會示範如何 toocreate 和排程處理使用 Hive 資料的資料處理站上的指令碼的 Hadoop 叢集。"
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
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a><span data-ttu-id="247db-104">教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="247db-104">Tutorial: Build your first pipeline tootransform data using Hadoop cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="247db-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="247db-105">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="247db-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="247db-106">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="247db-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="247db-107">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="247db-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="247db-108">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="247db-109">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="247db-109">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="247db-110">REST API</span><span class="sxs-lookup"><span data-stu-id="247db-110">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="247db-111">在本教學課程中，您會使用資料管線建立您的第一個 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="247db-111">In this tutorial, you build your first Azure data factory with a data pipeline.</span></span> <span data-ttu-id="247db-112">hello 管線的 Azure HDInsight (Hadoop) 叢集 tooproduce 輸出資料上執行 Hive 指令碼轉換輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="247db-112">hello pipeline transforms input data by running Hive script on an Azure HDInsight (Hadoop) cluster tooproduce output data.</span></span>  

<span data-ttu-id="247db-113">本文章提供概觀和 hello 教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="247db-113">This article provides overview and prerequisites for hello tutorial.</span></span> <span data-ttu-id="247db-114">完成 hello 必要條件之後，您可以使用其中一種下列 Sdk 工具/hello hello 教學課程： Azure 入口網站，Visual Studio、 PowerShell、 REST API 資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="247db-114">After you complete hello prerequisites, you can do hello tutorial using one of hello following tools/SDKs: Azure portal, Visual Studio, PowerShell, Resource Manager template, REST API.</span></span> <span data-ttu-id="247db-115">選取其中一個 hello 選項 hello hello 開頭 （或） 連結的下拉式清單中使用這些選項的其中一個本文章 toodo hello 教學課程的 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="247db-115">Select one of hello options in hello drop-down list at hello beginning (or) links at hello end of this article toodo hello tutorial using one of these options.</span></span>    

## <a name="tutorial-overview"></a><span data-ttu-id="247db-116">教學課程概觀</span><span class="sxs-lookup"><span data-stu-id="247db-116">Tutorial overview</span></span>
<span data-ttu-id="247db-117">在本教學課程中，您要執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="247db-117">In this tutorial, you perform hello following steps:</span></span>

1. <span data-ttu-id="247db-118">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="247db-118">Create a **data factory**.</span></span> <span data-ttu-id="247db-119">資料處理站可以包含一或多個資料管線，可移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="247db-119">A data factory can contain one or more data pipelines that move and transform data.</span></span> 

    <span data-ttu-id="247db-120">在本教學課程中，您可以建立 hello data factory 中的一個管線。</span><span class="sxs-lookup"><span data-stu-id="247db-120">In this tutorial, you create one pipeline in hello data factory.</span></span> 
2. <span data-ttu-id="247db-121">建立 **管線**。</span><span class="sxs-lookup"><span data-stu-id="247db-121">Create a **pipeline**.</span></span> <span data-ttu-id="247db-122">管線可以有一或多個活動 (範例︰複製活動、HDInsight Hive 活動)。</span><span class="sxs-lookup"><span data-stu-id="247db-122">A pipeline can have one or more activities (Examples: Copy Activity, HDInsight Hive Activity).</span></span> <span data-ttu-id="247db-123">這個範例會使用 hello HDInsight Hive 活動在 HDInsight Hadoop 叢集上執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="247db-123">This sample uses hello HDInsight Hive activity that runs a Hive script on a HDInsight Hadoop cluster.</span></span> <span data-ttu-id="247db-124">hello 指令碼會先建立參考 hello 原始 web 記錄資料儲存在 Azure blob 儲存體中的資料表和資料分割再依據年和月 hello 未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="247db-124">hello script first creates a table that references hello raw web log data stored in Azure blob storage and then partitions hello raw data by year and month.</span></span>

    <span data-ttu-id="247db-125">在本教學課程，hello 管線會使用 Azure HDInsight Hadoop 叢集上執行 Hive 查詢 hello Hive 活動 tootransform 資料。</span><span class="sxs-lookup"><span data-stu-id="247db-125">In this tutorial, hello pipeline uses hello Hive Activity tootransform data by running a Hive query on an Azure HDInsight Hadoop cluster.</span></span> 
3. <span data-ttu-id="247db-126">建立 **連結服務**。</span><span class="sxs-lookup"><span data-stu-id="247db-126">Create **linked services**.</span></span> <span data-ttu-id="247db-127">您可以建立連結的服務 toolink 資料存放區或計算服務 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="247db-127">You create a linked service toolink a data store or a compute service toohello data factory.</span></span> <span data-ttu-id="247db-128">資料存放區，例如 Azure 儲存體保存 hello 管線中的輸入/輸出資料的活動。</span><span class="sxs-lookup"><span data-stu-id="247db-128">A data store such as Azure Storage holds input/output data of activities in hello pipeline.</span></span> <span data-ttu-id="247db-129">計算服務 (例如 HDInsight Hadoop 叢集) 會處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="247db-129">A compute service such as HDInsight Hadoop cluster processes/transforms data.</span></span>

    <span data-ttu-id="247db-130">在本教學課程中，您會建立兩個「連結服務」：**Azure 儲存體** 和 **Azure HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="247db-130">In this tutorial, you create two linked services: **Azure Storage** and **Azure HDInsight**.</span></span> <span data-ttu-id="247db-131">hello Azure 儲存體連結服務連結保存 hello 輸入/輸出資料 toohello 資料處理站的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="247db-131">hello Azure Storage linked service links an Azure Storage Account that holds hello input/output data toohello data factory.</span></span> <span data-ttu-id="247db-132">Azure HDInsight 連結服務連結是使用的 tootransform 資料 toohello 資料處理站的 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="247db-132">Azure HDInsight linked service links an Azure HDInsight cluster that is used tootransform data toohello data factory.</span></span> 
3. <span data-ttu-id="247db-133">建立輸入和輸出 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="247db-133">Create input and output **datasets**.</span></span> <span data-ttu-id="247db-134">輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。</span><span class="sxs-lookup"><span data-stu-id="247db-134">An input dataset represents hello input for an activity in hello pipeline and an output dataset represents hello output for hello activity.</span></span>

    <span data-ttu-id="247db-135">在此教學課程、 hello 輸入和輸出資料集指定位置的輸入和輸出資料中的 hello Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="247db-135">In this tutorial, hello input and output datasets specify locations of input and output data in hello Azure Blob Storage.</span></span> <span data-ttu-id="247db-136">hello Azure 儲存體連結服務指定 Azure 儲存體帳戶使用。</span><span class="sxs-lookup"><span data-stu-id="247db-136">hello Azure Storage linked service specifies what Azure Storage Account is used.</span></span> <span data-ttu-id="247db-137">輸入資料集指定 hello 輸入的檔案的位置而輸出資料集指定 hello 輸出檔案會放置於其中。</span><span class="sxs-lookup"><span data-stu-id="247db-137">An input dataset specifies where hello input files are located and an output dataset specifies where hello output files are placed.</span></span> 


<span data-ttu-id="247db-138">請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)的 Azure Data Factory 的發行項的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="247db-138">See [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of Azure Data Factory.</span></span>
  
<span data-ttu-id="247db-139">以下是 hello**圖表檢視**您在本教學課程中建立的 hello 範例資料處理站。</span><span class="sxs-lookup"><span data-stu-id="247db-139">Here is hello **diagram view** of hello sample data factory you build in this tutorial.</span></span> <span data-ttu-id="247db-140">**MyFirstPipeline** 有一個 Hive 類型的活動，可接收 **AzureBlobInput** 資料集做為輸入，並輸出 **AzureBlobOutput** 資料集。</span><span class="sxs-lookup"><span data-stu-id="247db-140">**MyFirstPipeline** has one activity of type Hive that consumes **AzureBlobInput** dataset as an input and produces **AzureBlobOutput** dataset as an output.</span></span> 

![Data Factory 教學課程中的圖表檢視](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


<span data-ttu-id="247db-142">在本教學課程， **inputdata**資料夾 hello **adfgetstarted** Azure blob 容器包含一個名為 input.log 的檔案。</span><span class="sxs-lookup"><span data-stu-id="247db-142">In this tutorial, **inputdata** folder of hello **adfgetstarted** Azure blob container contains one file named input.log.</span></span> <span data-ttu-id="247db-143">此記錄檔包含三個月的項目，分別是：2016 年 1 月、2 月和 3 月。</span><span class="sxs-lookup"><span data-stu-id="247db-143">This log file has entries from three months: January, February, and March of 2016.</span></span> <span data-ttu-id="247db-144">以下是每個月 hello 範例資料列 hello 輸入檔中。</span><span class="sxs-lookup"><span data-stu-id="247db-144">Here are hello sample rows for each month in hello input file.</span></span> 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="247db-145">HDInsight Hive 活動與 hello 管線處理 hello 檔案時，hello 活動執行 Hive 指令碼 hello HDInsight 叢集上的資料分割輸入資料，依年份和月份。</span><span class="sxs-lookup"><span data-stu-id="247db-145">When hello file is processed by hello pipeline with HDInsight Hive Activity, hello activity runs a Hive script on hello HDInsight cluster that partitions input data by year and month.</span></span> <span data-ttu-id="247db-146">hello 指令碼會建立三個包含每個月中的項目與檔案的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="247db-146">hello script creates three output folders that contain a file with entries from each month.</span></span>  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

<span data-ttu-id="247db-147">Hello 範例列如上所示，從 hello 第一次一個 （具有 2016年-01-01) toohello 000000_0 檔案以寫入 hello 月 = 1 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="247db-147">From hello sample lines shown above, hello first one (with 2016-01-01) is written toohello 000000_0 file in hello month=1 folder.</span></span> <span data-ttu-id="247db-148">同樣地，hello 第二個 toohello 檔案以寫入 hello 月 = 2 的資料夾和 hello 其中一個第三個撰寫 toohello 檔案的 hello 月 = 3 資料夾。</span><span class="sxs-lookup"><span data-stu-id="247db-148">Similarly, hello second one is written toohello file in hello month=2 folder and hello third one is written toohello file in hello month=3 folder.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="247db-149">必要條件</span><span class="sxs-lookup"><span data-stu-id="247db-149">Prerequisites</span></span>
<span data-ttu-id="247db-150">開始本教學課程之前，您必須具備下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="247db-150">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

1. <span data-ttu-id="247db-151">**Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="247db-151">**Azure subscription** - If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="247db-152">請參閱 hello[免費試用](https://azure.microsoft.com/pricing/free-trial/)如何取得免費的試用帳戶上的發行項。</span><span class="sxs-lookup"><span data-stu-id="247db-152">See hello [Free Trial](https://azure.microsoft.com/pricing/free-trial/) article on how you can obtain a free trial account.</span></span>
2. <span data-ttu-id="247db-153">**Azure 儲存體**– 您將 hello 資料儲存在本教學課程使用一般用途的標準 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="247db-153">**Azure Storage** – You use a general-purpose standard Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="247db-154">如果您沒有通用標準的 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。</span><span class="sxs-lookup"><span data-stu-id="247db-154">If you don't have a general-purpose standard Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="247db-155">建立 hello 儲存體帳戶之後，記下 hello**帳戶名稱**和**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="247db-155">After you have created hello storage account, note down hello **account name** and **access key**.</span></span> <span data-ttu-id="247db-156">請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="247db-156">See [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>
3. <span data-ttu-id="247db-157">下載並檢閱 hello Hive 查詢檔案 (**HQL**) 位於： [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql)。</span><span class="sxs-lookup"><span data-stu-id="247db-157">Download and review hello Hive query file (**HQL**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span></span> <span data-ttu-id="247db-158">此查詢來轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="247db-158">This query transforms input data tooproduce output data.</span></span> 
4. <span data-ttu-id="247db-159">下載並檢閱 hello 範例輸入的檔 (**input.log**) 位於： [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span><span class="sxs-lookup"><span data-stu-id="247db-159">Download and review hello sample input file (**input.log**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span></span>
5. <span data-ttu-id="247db-160">在您的 Azure Blob 儲存體中建立名為 **adfgetstarted** 的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="247db-160">Create a blob container named **adfgetstarted** in your Azure Blob Storage.</span></span> 
6. <span data-ttu-id="247db-161">上傳**partitionweblogs.hql**檔案 toohello**指令碼**資料夾中 hello **adfgetstarted**容器。</span><span class="sxs-lookup"><span data-stu-id="247db-161">Upload **partitionweblogs.hql** file toohello **script** folder in hello **adfgetstarted** container.</span></span> <span data-ttu-id="247db-162">使用類似 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)的工具。</span><span class="sxs-lookup"><span data-stu-id="247db-162">Use tools such as [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 
7. <span data-ttu-id="247db-163">上傳**input.log**檔案 toohello **inputdata**資料夾中 hello **adfgetstarted**容器。</span><span class="sxs-lookup"><span data-stu-id="247db-163">Upload **input.log** file toohello **inputdata** folder in hello **adfgetstarted** container.</span></span> 

<span data-ttu-id="247db-164">完成 hello 必要條件之後，選取其中一個 hello Sdk 工具/toodo hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="247db-164">After you complete hello prerequisites, select one of hello following tools/SDKs toodo hello tutorial:</span></span> 

- [<span data-ttu-id="247db-165">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="247db-165">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
- [<span data-ttu-id="247db-166">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="247db-166">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
- [<span data-ttu-id="247db-167">PowerShell</span><span class="sxs-lookup"><span data-stu-id="247db-167">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
- [<span data-ttu-id="247db-168">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="247db-168">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
- [<span data-ttu-id="247db-169">REST API</span><span class="sxs-lookup"><span data-stu-id="247db-169">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="247db-170">Azure 入口網站和 Visual Studio 可讓您透過 GUI 建置資料處理站。</span><span class="sxs-lookup"><span data-stu-id="247db-170">Azure portal and Visual Studio provide GUI way of building your data factories.</span></span> <span data-ttu-id="247db-171">而 PowerShell、Resource Manager 範本和 REST API，則可讓您選擇以撰寫指令碼/程式碼的方式來建置資料處理站。</span><span class="sxs-lookup"><span data-stu-id="247db-171">Whereas, PowerShell, Resource Manager Template, and REST API options provides scripting/programming way of building your data factories.</span></span>

> [!NOTE]
> <span data-ttu-id="247db-172">在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="247db-172">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="247db-173">它不會複製資料來源建立資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="247db-173">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="247db-174">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="247db-174">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="247db-175">您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="247db-175">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="247db-176">如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="247db-176">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 





  
