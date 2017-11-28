---
title: "教學課程： 使用 REST API toocreate Azure Data Factory 管線 |Microsoft 文件"
description: "在本教學課程中，您可以使用 REST API toocreate Azure Data Factory 管線複製活動 toocopy 資料從 Azure blob 儲存體 Azure SQL database。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="ea2ad-103">教學課程： 使用 REST API toocreate Azure Data Factory 管線 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="ea2ad-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea2ad-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="ea2ad-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ea2ad-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="ea2ad-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ea2ad-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ea2ad-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ea2ad-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea2ad-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ea2ad-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea2ad-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ea2ad-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ea2ad-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ea2ad-110">REST API</span><span class="sxs-lookup"><span data-stu-id="ea2ad-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ea2ad-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="ea2ad-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="ea2ad-112">在本文中，您學會如何 toouse 會 REST API toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="ea2ad-113">如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="ea2ad-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="ea2ad-115">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="ea2ad-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ea2ad-117">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ea2ad-118">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="ea2ad-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ea2ad-120">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ea2ad-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="ea2ad-122">本文並未涵蓋所有 hello Data Factory REST API。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="ea2ad-123">如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory REST API 參考](/rest/api/datafactory/) 。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="ea2ad-124">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="ea2ad-125">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea2ad-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="ea2ad-126">Prerequisites</span></span>
* <span data-ttu-id="ea2ad-127">透過移[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)和完整 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="ea2ad-128">在您的電腦上安裝 [Curl](https://curl.haxx.se/dlwiz/) 。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="ea2ad-129">您可以使用 hello Curl 工具與其他命令 toocreate data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="ea2ad-130">請依照 [本文](../azure-resource-manager/resource-group-create-service-principal-portal.md) 的指示：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="ea2ad-131">在 Azure Active Directory 中建立名為 **ADFCopyTutorialApp** 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="ea2ad-132">取得**用戶端識別碼**和**秘密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="ea2ad-133">取得 **租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="ea2ad-134">指派 hello **ADFCopyTutorialApp**應用程式 toohello**資料 Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="ea2ad-135">安裝 [Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="ea2ad-136">啟動**PowerShell**並執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="ea2ad-137">保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="ea2ad-138">如果您關閉並重新開啟，您需要 toorun hello 命令一次。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="ea2ad-139">執行下列命令的 hello，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="ea2ad-140">此帳戶的所有 hello 訂用帳戶都執行下列命令 tooview hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="ea2ad-141">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="ea2ad-142">取代 **&lt;NameOfAzureSubscription** &gt; hello 的 Azure 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="ea2ad-143">建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="ea2ad-144">如果已經存在 hello 資源群組，指定是否 tooupdate 它 (Y) 或保留為 (N)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="ea2ad-145">本教學課程中的 hello 步驟假設您使用名為 ADFTutorialResourceGroup hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="ea2ad-146">如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="ea2ad-147">建立 JSON 定義</span><span class="sxs-lookup"><span data-stu-id="ea2ad-147">Create JSON definitions</span></span>
<span data-ttu-id="ea2ad-148">建立下列 hello curl.exe 所在的資料夾中的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="ea2ad-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea2ad-150">名稱必須是全域唯一的因此您可能需要 tooprefix/後置詞 ADFCopyTutorialDF toomake 它唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="ea2ad-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea2ad-152">以 Azure 儲存體帳戶的名稱和金鑰取代 **accountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="ea2ad-153">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

<span data-ttu-id="ea2ad-154">如需 JSON 屬性的詳細資訊，請參閱 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="ea2ad-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea2ad-156">取代**servername**， **databasename**， **username**，和**密碼**名稱為您的 Azure SQL server，SQL 資料庫名稱的使用者帳戶和 hello 帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="ea2ad-157">如需 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="ea2ad-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="ea2ad-159">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="ea2ad-160">屬性</span><span class="sxs-lookup"><span data-stu-id="ea2ad-160">Property</span></span> | <span data-ttu-id="ea2ad-161">說明</span><span class="sxs-lookup"><span data-stu-id="ea2ad-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea2ad-162">類型</span><span class="sxs-lookup"><span data-stu-id="ea2ad-162">type</span></span> | <span data-ttu-id="ea2ad-163">hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="ea2ad-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ea2ad-164">linkedServiceName</span></span> | <span data-ttu-id="ea2ad-165">是指 toohello **AzureStorageLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="ea2ad-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="ea2ad-166">folderPath</span></span> | <span data-ttu-id="ea2ad-167">指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="ea2ad-168">在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="ea2ad-169">fileName</span><span class="sxs-lookup"><span data-stu-id="ea2ad-169">fileName</span></span> | <span data-ttu-id="ea2ad-170">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-170">This property is optional.</span></span> <span data-ttu-id="ea2ad-171">如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="ea2ad-172">在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="ea2ad-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="ea2ad-173">format -> type</span></span> |<span data-ttu-id="ea2ad-174">hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="ea2ad-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="ea2ad-175">columnDelimiter</span></span> | <span data-ttu-id="ea2ad-176">hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="ea2ad-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="ea2ad-177">frequency/interval</span></span> | <span data-ttu-id="ea2ad-178">hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="ea2ad-179">換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="ea2ad-180">它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="ea2ad-181">external</span><span class="sxs-lookup"><span data-stu-id="ea2ad-181">external</span></span> | <span data-ttu-id="ea2ad-182">這個屬性設定太**true**如果 hello 資料不會產生此管線。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="ea2ad-183">在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="ea2ad-184">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="ea2ad-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="ea2ad-186">hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="ea2ad-187">屬性</span><span class="sxs-lookup"><span data-stu-id="ea2ad-187">Property</span></span> | <span data-ttu-id="ea2ad-188">說明</span><span class="sxs-lookup"><span data-stu-id="ea2ad-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ea2ad-189">類型</span><span class="sxs-lookup"><span data-stu-id="ea2ad-189">type</span></span> | <span data-ttu-id="ea2ad-190">hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="ea2ad-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ea2ad-191">linkedServiceName</span></span> | <span data-ttu-id="ea2ad-192">是指 toohello **AzureSqlLinkedService**您稍早建立的。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="ea2ad-193">tableName</span><span class="sxs-lookup"><span data-stu-id="ea2ad-193">tableName</span></span> | <span data-ttu-id="ea2ad-194">指定的 hello**資料表**toowhich hello 資料複製。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="ea2ad-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="ea2ad-195">frequency/interval</span></span> | <span data-ttu-id="ea2ad-196">hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="ea2ad-197">有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="ea2ad-198">識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="ea2ad-199">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="ea2ad-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="ea2ad-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="ea2ad-201">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-201">Note hello following points:</span></span>

- <span data-ttu-id="ea2ad-202">在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="ea2ad-203">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ea2ad-204">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="ea2ad-205">輸入 hello 活動設定太**AzureBlobInput**和輸出 hello 活動設定太**AzureSqlOutput**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="ea2ad-206">在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="ea2ad-207">支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ea2ad-208">toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="ea2ad-209">取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="ea2ad-210">您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="ea2ad-211">例如，"2017年-02-03"，這相當於太"2017年-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="ea2ad-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="ea2ad-212">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ea2ad-213">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="ea2ad-214">hello**結束**時間是選擇性的但我們在本教學課程中使用它。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="ea2ad-215">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="ea2ad-216">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="ea2ad-217">在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="ea2ad-218">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ea2ad-219">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ea2ad-220">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="ea2ad-221">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="ea2ad-222">設定全域變數</span><span class="sxs-lookup"><span data-stu-id="ea2ad-222">Set global variables</span></span>
<span data-ttu-id="ea2ad-223">在 Azure PowerShell，執行下列命令以您自己取代 hello 值後的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea2ad-224">如需取得用戶端識別碼、用戶端密碼、租用戶識別碼及訂用帳戶識別碼的指示，請參閱 [必要條件](#prerequisites) 一節。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="ea2ad-225">您使用執行的 hello hello hello data factory 名稱在更新之後，下列命令：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="ea2ad-226">使用 AAD 驗證</span><span class="sxs-lookup"><span data-stu-id="ea2ad-226">Authenticate with AAD</span></span>
<span data-ttu-id="ea2ad-227">執行下列命令 tooauthenticate 與 Azure Active Directory (AAD) 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="ea2ad-228">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="ea2ad-228">Create data factory</span></span>
<span data-ttu-id="ea2ad-229">在此步驟中，您會建立名為 **ADFCopyTutorialDF**的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="ea2ad-230">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ea2ad-231">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ea2ad-232">例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="ea2ad-233">HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="ea2ad-234">執行下列命令 toocreate hello 資料處理站的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="ea2ad-235">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="ea2ad-236">確認您在此處指定 (ADFCopyTutorialDF) 相符項目 hello hello 中指定名稱的 hello data factory 名稱 hello **datafactory.json**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-237">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-238">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-238">View hello results.</span></span> <span data-ttu-id="ea2ad-239">如果 hello data factory 建立成功，您會看見 hello JSON hello data factory 中 hello**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="ea2ad-240">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-240">Note hello following points:</span></span>

* <span data-ttu-id="ea2ad-241">hello hello Azure Data Factory 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="ea2ad-242">如果您看到結果中的 hello 錯誤： **Data factory 名稱"ADFCopyTutorialDF"不是使用**，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="ea2ad-243">在 hello 變更 hello 名稱 (例如，yournameADFCopyTutorialDF) **datafactory.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="ea2ad-244">Hello 第一個命令中其中 hello **$cmd**值指派給變數，請取代 ADFCopyTutorialDF hello 新名稱，執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="ea2ad-245">執行 hello 下面兩個命令 tooinvoke hello REST API toocreate hello 資料處理站和列印 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="ea2ad-246">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="ea2ad-247">toocreate Data Factory 執行個體，您需要 toobe 參與者/系統管理員的 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ea2ad-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="ea2ad-248">可能會註冊為未來的 hello 中的 DNS 名稱，因此變得可見 hello hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="ea2ad-249">如果您收到 hello 錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**」，請勿 hello 下列其中一種，然後再試一次發行：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="ea2ad-250">在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea2ad-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="ea2ad-251">您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="ea2ad-252">登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="ea2ad-253">這個動作會自動註冊 hello 您的提供者。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="ea2ad-254">之前建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="ea2ad-255">您第一次建立連結的服務 toolink 來源和目的地資料存放區 tooyour 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="ea2ad-256">然後，定義輸入和輸出資料集 toorepresent 資料連結的資料存放區中。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="ea2ad-257">最後，建立 hello 管線與該活動會使用這些資料集。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="ea2ad-258">建立連結的服務</span><span class="sxs-lookup"><span data-stu-id="ea2ad-258">Create linked services</span></span>
<span data-ttu-id="ea2ad-259">您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="ea2ad-260">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="ea2ad-261">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="ea2ad-262">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="ea2ad-263">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="ea2ad-264">這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="ea2ad-265">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="ea2ad-266">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="ea2ad-267">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ea2ad-268">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="ea2ad-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="ea2ad-269">在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="ea2ad-270">您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="ea2ad-271">請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="ea2ad-272">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-273">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-274">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-274">View hello results.</span></span> <span data-ttu-id="ea2ad-275">如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="ea2ad-276">建立 Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="ea2ad-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="ea2ad-277">在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ea2ad-278">您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="ea2ad-279">請參閱[Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="ea2ad-280">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-281">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-282">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-282">View hello results.</span></span> <span data-ttu-id="ea2ad-283">如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="ea2ad-284">建立資料集</span><span class="sxs-lookup"><span data-stu-id="ea2ad-284">Create datasets</span></span>
<span data-ttu-id="ea2ad-285">在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ea2ad-286">在此步驟中，您可以定義名為 AzureBlobInput AzureSqlOutput 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="ea2ad-287">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ea2ad-288">此外，hello 輸入的 blob 資料集 (AzureBlobInput) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="ea2ad-289">同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="ea2ad-290">此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="ea2ad-291">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="ea2ad-291">Create input dataset</span></span>
<span data-ttu-id="ea2ad-292">在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) AzureBlobInput hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="ea2ad-293">如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="ea2ad-294">在本教學課程中，您可以指定 hello 檔案名稱的值。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="ea2ad-295">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-296">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-297">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-297">View hello results.</span></span> <span data-ttu-id="ea2ad-298">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="ea2ad-299">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="ea2ad-299">Create output dataset</span></span>
<span data-ttu-id="ea2ad-300">hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="ea2ad-301">hello 輸出 SQL 資料表的資料集 (OututDataset) 您在此步驟中建立指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="ea2ad-302">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-303">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-304">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-304">View hello results.</span></span> <span data-ttu-id="ea2ad-305">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="ea2ad-306">建立管線</span><span class="sxs-lookup"><span data-stu-id="ea2ad-306">Create pipeline</span></span>
<span data-ttu-id="ea2ad-307">在此步驟中，您會建立管線，其中含有使用 **AzureBlobInput** 作為輸入和使用 **AzureSqlOutput** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="ea2ad-308">目前，輸出資料集是哪些磁碟機 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="ea2ad-309">在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="ea2ad-310">hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="ea2ad-311">因此，hello 管線所產生的輸出資料集的 24 配量。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="ea2ad-312">指定名為 hello 命令 toovariable **cmd**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ea2ad-313">使用執行 hello 命令**Invoke-command**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ea2ad-314">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-314">View hello results.</span></span> <span data-ttu-id="ea2ad-315">如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="ea2ad-316">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="ea2ad-316">**Congratulations!**</span></span> <span data-ttu-id="ea2ad-317">您已成功建立 Azure data factory，，具有會將資料從 Azure Blob 儲存體 tooAzure SQL database 的管線。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="ea2ad-318">監視管線</span><span class="sxs-lookup"><span data-stu-id="ea2ad-318">Monitor pipeline</span></span>
<span data-ttu-id="ea2ad-319">在此步驟中，您可以使用 Data Factory REST API toomonitor 配量 hello 管線所產生。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="ea2ad-320">請確定 hello 開始和結束時間中指定下列的 hello 命令對 hello 開始和結束時間的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="ea2ad-321">執行 hello Invoke-command 和 hello 下一個直到您看到中的扇區**準備**狀態或**失敗**狀態。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="ea2ad-322">當 hello 配量處於就緒狀態時，請檢查 hello **emp**您 Azure SQL database 中的 hello 輸出資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="ea2ad-323">每個配量，兩個資料列的資料從 hello 原始程式檔是 hello Azure SQL database 中的複製的 toohello emp 資料表。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="ea2ad-324">因此，所有的 hello 配量已成功處理 （處於就緒狀態） 時看到 24 hello emp 資料表中的新記錄。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="ea2ad-325">摘要</span><span class="sxs-lookup"><span data-stu-id="ea2ad-325">Summary</span></span>
<span data-ttu-id="ea2ad-326">在此教學課程中，您可以使用 REST API toocreate 從 Azure blob tooan Azure SQL database 的 Azure data factory toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="ea2ad-327">以下是您執行本教學課程中的 hello 高階步驟：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="ea2ad-328">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="ea2ad-329">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="ea2ad-330">Azure 儲存體連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="ea2ad-331">Azure SQL 連結服務 toolink hello 輸出資料會保存您 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="ea2ad-332">建立可描述管線輸入資料和輸出資料的 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="ea2ad-333">建立具有複製活動的 **管線** ，以 BlobSource 做為來源並以 SqlSink 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ea2ad-334">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea2ad-334">Next steps</span></span>
<span data-ttu-id="ea2ad-335">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="ea2ad-336">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="ea2ad-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="ea2ad-337">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ea2ad-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
