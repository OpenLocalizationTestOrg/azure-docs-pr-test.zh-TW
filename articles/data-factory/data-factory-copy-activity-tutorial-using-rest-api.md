---
title: "教學課程︰使用 REST API 建立 Azure Data Factory 管線 |Microsoft Docs"
description: "在本教學課程中，您會使用 REST API 建立具有複製活動的 Azure Data Factory 管線，以將資料從 Azure Blob 儲存體複製到 Azure SQL Database。"
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
ms.openlocfilehash: 6663774497aa18aa98e7e8c5aed6183c599b2172
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="616ab-103">教學課程︰使用 REST API 建立 Azure Data Factory 管線來複製資料</span><span class="sxs-lookup"><span data-stu-id="616ab-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="616ab-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="616ab-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="616ab-105">複製精靈</span><span class="sxs-lookup"><span data-stu-id="616ab-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="616ab-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="616ab-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="616ab-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="616ab-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="616ab-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="616ab-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="616ab-109">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="616ab-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="616ab-110">REST API</span><span class="sxs-lookup"><span data-stu-id="616ab-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="616ab-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="616ab-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="616ab-112">在本文中，您會了解如何使用 REST API 建立資料處理站，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="616ab-112">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="616ab-113">如果您不熟悉 Azure Data Factory，請先詳閱 [Azure Data Factory 簡介](data-factory-introduction.md)一文，再進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="616ab-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="616ab-114">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="616ab-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="616ab-115">複製活動會將資料從支援的資料存放區複製到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="616ab-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="616ab-116">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="616ab-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="616ab-117">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="616ab-118">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="616ab-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="616ab-119">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="616ab-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="616ab-120">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="616ab-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="616ab-121">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="616ab-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="616ab-122">這篇文章並未涵蓋所有的 Data Factory REST API。</span><span class="sxs-lookup"><span data-stu-id="616ab-122">This article does not cover all the Data Factory REST API.</span></span> <span data-ttu-id="616ab-123">如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory REST API 參考](/rest/api/datafactory/) 。</span><span class="sxs-lookup"><span data-stu-id="616ab-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="616ab-124">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="616ab-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="616ab-125">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="616ab-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="616ab-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="616ab-126">Prerequisites</span></span>
* <span data-ttu-id="616ab-127">請檢閱 [教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 並完成 **必要** 步驟。</span><span class="sxs-lookup"><span data-stu-id="616ab-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="616ab-128">在您的電腦上安裝 [Curl](https://curl.haxx.se/dlwiz/) 。</span><span class="sxs-lookup"><span data-stu-id="616ab-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="616ab-129">您可搭配使用 Curl 工具與 REST 命令來建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="616ab-129">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="616ab-130">請依照 [本文](../azure-resource-manager/resource-group-create-service-principal-portal.md) 的指示：</span><span class="sxs-lookup"><span data-stu-id="616ab-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="616ab-131">在 Azure Active Directory 中建立名為 **ADFCopyTutorialApp** 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="616ab-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="616ab-132">取得**用戶端識別碼**和**秘密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="616ab-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="616ab-133">取得 **租用戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="616ab-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="616ab-134">將 **ADFCopyTutorialApp** 應用程式指派給 **Data Factory 參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="616ab-134">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="616ab-135">安裝 [Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="616ab-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="616ab-136">啟動 **PowerShell** 並執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="616ab-136">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="616ab-137">將 Azure PowerShell 維持在開啟狀態，直到本教學課程結束為止。</span><span class="sxs-lookup"><span data-stu-id="616ab-137">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="616ab-138">如果您關閉並重新開啟，則需要再次執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-138">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="616ab-139">執行下列命令並輸入您用來登入 Azure 入口網站的使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="616ab-139">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="616ab-140">執行下列命令以檢視此帳戶的所有訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="616ab-140">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="616ab-141">執行下列命令以選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="616ab-141">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="616ab-142">以您的 Azure 訂用帳戶名稱取代 **&lt;NameOfAzureSubscription**&gt;。</span><span class="sxs-lookup"><span data-stu-id="616ab-142">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="616ab-143">在 PowerShell 中執行以下命令，建立名為 **ADFTutorialResourceGroup** 的 Azure 資源群組：</span><span class="sxs-lookup"><span data-stu-id="616ab-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="616ab-144">如果資源群組已存在，您可指定是否要更新 (Y) 或予以保留 (N)。</span><span class="sxs-lookup"><span data-stu-id="616ab-144">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="616ab-145">本教學課程的某些步驟假設您使用名為 ADFTutorialResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="616ab-145">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="616ab-146">如果使用不同的資源群組，您必須以資源群組的名稱取代本教學課程中的 ADFTutorialResourceGroup。</span><span class="sxs-lookup"><span data-stu-id="616ab-146">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="616ab-147">建立 JSON 定義</span><span class="sxs-lookup"><span data-stu-id="616ab-147">Create JSON definitions</span></span>
<span data-ttu-id="616ab-148">在 curl.exe 所在的資料夾中建立下列 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="616ab-148">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="616ab-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="616ab-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="616ab-150">名稱必須是全域唯一的，所以建議您使用 ADFCopyTutorialDF 做為前置詞/後置詞，使其成為唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="616ab-150">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="616ab-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="616ab-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="616ab-152">以 Azure 儲存體帳戶的名稱和金鑰取代 **accountname** 和 **accountkey**。</span><span class="sxs-lookup"><span data-stu-id="616ab-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="616ab-153">若要了解如何取得儲存體存取金鑰，請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)</span><span class="sxs-lookup"><span data-stu-id="616ab-153">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="616ab-154">如需 JSON 屬性的詳細資訊，請參閱 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="616ab-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="616ab-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="616ab-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="616ab-156">將 **servername**、**databasename**、**username** 和 **password** 替換為您的 Azure SQL Server 名稱、SQL Database 名稱、使用者帳戶及帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="616ab-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.</span></span>  
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

<span data-ttu-id="616ab-157">如需 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="616ab-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="616ab-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="616ab-158">inputdataset.json</span></span>

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

<span data-ttu-id="616ab-159">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="616ab-159">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="616ab-160">屬性</span><span class="sxs-lookup"><span data-stu-id="616ab-160">Property</span></span> | <span data-ttu-id="616ab-161">說明</span><span class="sxs-lookup"><span data-stu-id="616ab-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="616ab-162">類型</span><span class="sxs-lookup"><span data-stu-id="616ab-162">type</span></span> | <span data-ttu-id="616ab-163">type 屬性會設為 **AzureBlob**，因為資料位於 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="616ab-163">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="616ab-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="616ab-164">linkedServiceName</span></span> | <span data-ttu-id="616ab-165">表示您稍早建立的 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="616ab-165">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="616ab-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="616ab-166">folderPath</span></span> | <span data-ttu-id="616ab-167">指定包含輸入 Blob 的 Blob **容器**和**資料夾**。</span><span class="sxs-lookup"><span data-stu-id="616ab-167">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="616ab-168">在本教學課程中，adftutorial 是 blob 容器，而資料夾是根資料夾。</span><span class="sxs-lookup"><span data-stu-id="616ab-168">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="616ab-169">fileName</span><span class="sxs-lookup"><span data-stu-id="616ab-169">fileName</span></span> | <span data-ttu-id="616ab-170">這是選用屬性。</span><span class="sxs-lookup"><span data-stu-id="616ab-170">This property is optional.</span></span> <span data-ttu-id="616ab-171">如果您省略此屬性，則會挑選 folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="616ab-171">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="616ab-172">在本教學課程中，會針對 fileName 指定 **emp.txt**，因此只會挑選該檔案進行處理。</span><span class="sxs-lookup"><span data-stu-id="616ab-172">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="616ab-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="616ab-173">format -> type</span></span> |<span data-ttu-id="616ab-174">輸入檔為文字格式，因此我們會使用 **TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="616ab-174">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="616ab-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="616ab-175">columnDelimiter</span></span> | <span data-ttu-id="616ab-176">輸入檔案中的資料行會以**逗號字元 (`,`)** 分隔。</span><span class="sxs-lookup"><span data-stu-id="616ab-176">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="616ab-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="616ab-177">frequency/interval</span></span> | <span data-ttu-id="616ab-178">frequency 會設為 **Hour** 且 interval 會設為 **1**，表示**每小時**都可取得輸入配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-178">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="616ab-179">換句話說，Data Factory 服務會每小時都在您指定之 Blob 容器 (**adftutorial**) 的根資料夾中尋找輸入資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-179">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="616ab-180">它會尋找管線開始和結束時間內 (而非這些時間之前或之後) 的資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-180">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="616ab-181">external</span><span class="sxs-lookup"><span data-stu-id="616ab-181">external</span></span> | <span data-ttu-id="616ab-182">如果資料不是由此管線產生，此屬性會設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="616ab-182">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="616ab-183">本教學課程中的輸入資料位於 emp.txt 檔案中，該檔案不是由此管線產生，因此我們會將此屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="616ab-183">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="616ab-184">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="616ab-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="616ab-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="616ab-185">outputdataset.json</span></span>

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
<span data-ttu-id="616ab-186">下表提供程式碼片段中所使用之 JSON 屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="616ab-186">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="616ab-187">屬性</span><span class="sxs-lookup"><span data-stu-id="616ab-187">Property</span></span> | <span data-ttu-id="616ab-188">說明</span><span class="sxs-lookup"><span data-stu-id="616ab-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="616ab-189">類型</span><span class="sxs-lookup"><span data-stu-id="616ab-189">type</span></span> | <span data-ttu-id="616ab-190">type 屬性會設為 **AzureSqlTable**，因為資料已複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="616ab-190">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="616ab-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="616ab-191">linkedServiceName</span></span> | <span data-ttu-id="616ab-192">表示您稍早建立的 **AzureSqlLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="616ab-192">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="616ab-193">tableName</span><span class="sxs-lookup"><span data-stu-id="616ab-193">tableName</span></span> | <span data-ttu-id="616ab-194">指定作為資料複製目的地的**資料表**。</span><span class="sxs-lookup"><span data-stu-id="616ab-194">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="616ab-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="616ab-195">frequency/interval</span></span> | <span data-ttu-id="616ab-196">frequency 會設為**Hour** 且 interval 為**1**，這表示會在管線開始和結束時間之間 (而非這些時間之前或之後) **每小時**產生輸出配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-196">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="616ab-197">資料庫的 emp 資料表中有三個資料行 – **ID**、**FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="616ab-197">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="616ab-198">ID 是識別資料行，所以您只需在此指定 **FirstName** 和 **LastName**。</span><span class="sxs-lookup"><span data-stu-id="616ab-198">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="616ab-199">如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。</span><span class="sxs-lookup"><span data-stu-id="616ab-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="616ab-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="616ab-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

<span data-ttu-id="616ab-201">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="616ab-201">Note the following points:</span></span>

- <span data-ttu-id="616ab-202">在活動區段中，只會有一個 **type** 設為 **Copy** 的活動。</span><span class="sxs-lookup"><span data-stu-id="616ab-202">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="616ab-203">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="616ab-203">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="616ab-204">在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="616ab-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="616ab-205">活動的輸入設為 **AzureBlobInput**，活動的輸出則設為 **AzureSqlOutput**。</span><span class="sxs-lookup"><span data-stu-id="616ab-205">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="616ab-206">在 **typeProperties** 區段中，來源類型指定為 **BlobSource**，接收類型指定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="616ab-206">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="616ab-207">如需複製活動作為來源和接收器支援的資料存放區完整清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="616ab-207">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="616ab-208">若要了解如何使用特定支援的資料存放區作為來源/接收器，請按一下資料表中的連結。</span><span class="sxs-lookup"><span data-stu-id="616ab-208">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="616ab-209">將 **start** 屬性的值替換為目前日期，並將 **end**值替換為隔天的日期。</span><span class="sxs-lookup"><span data-stu-id="616ab-209">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="616ab-210">在日期時間中，您只指定日期部分，並略過時間部分。</span><span class="sxs-lookup"><span data-stu-id="616ab-210">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="616ab-211">例如，"2017-02-03"，這相當於 "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="616ab-211">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="616ab-212">開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="616ab-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="616ab-213">例如：2016-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="616ab-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="616ab-214">**end** 時間為選擇性項目，但在本教學課程中會用到。</span><span class="sxs-lookup"><span data-stu-id="616ab-214">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="616ab-215">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="616ab-215">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="616ab-216">若要無限期地執行管線，請指定 **9999-09-09** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="616ab-216">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="616ab-217">在上述範例中，由於每小時即產生一個資料配量，共會有 24 個資料配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-217">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="616ab-218">如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="616ab-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="616ab-219">如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="616ab-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="616ab-220">如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="616ab-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="616ab-221">如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。</span><span class="sxs-lookup"><span data-stu-id="616ab-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="616ab-222">設定全域變數</span><span class="sxs-lookup"><span data-stu-id="616ab-222">Set global variables</span></span>
<span data-ttu-id="616ab-223">在 Azure PowerShell 中，將值取代為您自己的值之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="616ab-223">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="616ab-224">如需取得用戶端識別碼、用戶端密碼、租用戶識別碼及訂用帳戶識別碼的指示，請參閱 [必要條件](#prerequisites) 一節。</span><span class="sxs-lookup"><span data-stu-id="616ab-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="616ab-225">更新您正在使用的資料處理站名稱之後，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="616ab-225">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="616ab-226">使用 AAD 驗證</span><span class="sxs-lookup"><span data-stu-id="616ab-226">Authenticate with AAD</span></span>
<span data-ttu-id="616ab-227">執行下列命令以驗證 Azure Active Directory (AAD)：</span><span class="sxs-lookup"><span data-stu-id="616ab-227">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="616ab-228">建立資料處理站</span><span class="sxs-lookup"><span data-stu-id="616ab-228">Create data factory</span></span>
<span data-ttu-id="616ab-229">在此步驟中，您會建立名為 **ADFCopyTutorialDF**的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="616ab-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="616ab-230">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="616ab-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="616ab-231">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="616ab-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="616ab-232">例如，「複製活動」會從來源複製資料到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="616ab-232">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="616ab-233">HDInsight Hive 活動會執行 Hive 指令碼來轉換輸入資料，以產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-233">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="616ab-234">執行以下命令以建立 Data Factory：</span><span class="sxs-lookup"><span data-stu-id="616ab-234">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="616ab-235">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-235">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="616ab-236">確認您在此指定的名稱 (ADFCopyTutorialDF) 符合在 **datafactory.json**指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="616ab-236">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-237">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-237">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-238">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-238">View the results.</span></span> <span data-ttu-id="616ab-239">如果已成功建立 Data Factory，您會在 **結果**中看到 Data Factory 的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-239">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="616ab-240">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="616ab-240">Note the following points:</span></span>

* <span data-ttu-id="616ab-241">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="616ab-241">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="616ab-242">如果您在結果中看到錯誤︰「Data factory 名稱 "ADFCopyTutorialDF" 無法使用」 ，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="616ab-242">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="616ab-243">在 **datafactory.json** 檔案中變更名稱 (例如，yournameADFCopyTutorialDF)。</span><span class="sxs-lookup"><span data-stu-id="616ab-243">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="616ab-244">在指派 **$cmd** 變數值的第一個命令中，以新的名稱取代 ADFCopyTutorialDF 並執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-244">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="616ab-245">執行下面兩個命令來叫用 REST API，以建立 Data Factory 和列印作業的結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-245">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="616ab-246">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="616ab-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="616ab-247">若要建立 Data Factory 執行個體，您必須是 Azure 訂用帳戶的參與者/系統管理員</span><span class="sxs-lookup"><span data-stu-id="616ab-247">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="616ab-248">Data Factory 的名稱未來可能會註冊為 DNS 名稱，因此會變成公開可見的名稱。</span><span class="sxs-lookup"><span data-stu-id="616ab-248">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="616ab-249">如果您收到錯誤：「此訂用帳戶未註冊為使用命名空間 Microsoft.DataFactory」，請執行下列其中一項，然後嘗試再次發佈︰</span><span class="sxs-lookup"><span data-stu-id="616ab-249">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="616ab-250">在 Azure PowerShell 中，執行下列命令以註冊 Data Factory 提供者：</span><span class="sxs-lookup"><span data-stu-id="616ab-250">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="616ab-251">您可以執行下列命令來確認已註冊 Data Factory 提供者。</span><span class="sxs-lookup"><span data-stu-id="616ab-251">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="616ab-252">使用 Azure 訂用帳戶登入 [Azure 入口網站](https://portal.azure.com) 並瀏覽至 [Data Factory] 刀鋒視窗 (或) 在 Azure 入口網站中建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="616ab-252">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="616ab-253">此動作會自動為您註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="616ab-253">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="616ab-254">建立管線之前，您必須先建立一些 Data Factory 項目。</span><span class="sxs-lookup"><span data-stu-id="616ab-254">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="616ab-255">您會先建立連結服務，將來源和目的地資料存放區連結至您的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="616ab-255">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="616ab-256">然後，定義輸入和輸出資料集，以表示連結資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-256">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="616ab-257">最後，建立會使用這些資料集之活動的管線。</span><span class="sxs-lookup"><span data-stu-id="616ab-257">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="616ab-258">建立連結服務</span><span class="sxs-lookup"><span data-stu-id="616ab-258">Create linked services</span></span>
<span data-ttu-id="616ab-259">您在資料處理站中建立的連結服務會將您的資料存放區和計算服務連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="616ab-259">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="616ab-260">在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="616ab-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="616ab-261">您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。</span><span class="sxs-lookup"><span data-stu-id="616ab-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="616ab-262">因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。</span><span class="sxs-lookup"><span data-stu-id="616ab-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="616ab-263">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="616ab-263">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="616ab-264">此儲存體帳戶是您在其中建立容器並將資料上傳為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)一部分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="616ab-264">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="616ab-265">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="616ab-265">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="616ab-266">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="616ab-266">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="616ab-267">您在此資料庫中建立了 emp 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="616ab-267">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="616ab-268">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="616ab-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="616ab-269">在此步驟中，您會將您的 Azure 儲存體帳戶連結到您的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="616ab-269">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="616ab-270">在此區段中指定您 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="616ab-270">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="616ab-271">如需用來定義 Azure 儲存體連結服務之 JSON 屬性的詳細資料，請參閱 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="616ab-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="616ab-272">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-272">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-273">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-273">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-274">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-274">View the results.</span></span> <span data-ttu-id="616ab-275">如果已成功建立連結服務，您會在 **結果**中看到連結服務的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-275">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="616ab-276">建立 Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="616ab-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="616ab-277">在此步驟中，您會將您的 Azure SQL Database 連結到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="616ab-277">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="616ab-278">在此區段中指定 Azure SQL 伺服器名稱、資料庫名稱、使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="616ab-278">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="616ab-279">如需用來定義 Azure SQL 連結服務之 JSON 屬性的詳細資料，請參閱 [Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="616ab-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="616ab-280">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-280">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-281">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-281">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-282">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-282">View the results.</span></span> <span data-ttu-id="616ab-283">如果已成功建立連結服務，您會在 **結果**中看到連結服務的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-283">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="616ab-284">建立資料集</span><span class="sxs-lookup"><span data-stu-id="616ab-284">Create datasets</span></span>
<span data-ttu-id="616ab-285">在上一個步驟中，您已建立可將 Azure 儲存體帳戶和 Azure SQL Database 連結至資料處理站的連結服務。</span><span class="sxs-lookup"><span data-stu-id="616ab-285">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="616ab-286">在此步驟中，您會定義名為 AzureBlobInput 和 AzureSqlOutput 的兩個資料集，它們分別代表 AzureStorageLinkedService 和 AzureSqlLinkedService 所參照資料存放區中儲存的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="616ab-287">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="616ab-287">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="616ab-288">而且，輸入 Blob 資料集 (AzureBlobInput) 會指定包含輸入資料的容器和資料夾。</span><span class="sxs-lookup"><span data-stu-id="616ab-288">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="616ab-289">同樣第，Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="616ab-289">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="616ab-290">而且，輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="616ab-290">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="616ab-291">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="616ab-291">Create input dataset</span></span>
<span data-ttu-id="616ab-292">在此步驟中，您將在 AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中，建立名為 AzureBlobInput 的資料集，該資料集會指向 Blob 容器 (adftutorial) 根資料夾中的 Blob 檔案 (emp.txt)。</span><span class="sxs-lookup"><span data-stu-id="616ab-292">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="616ab-293">如果您未指定 (或跳過) fileName 的值，則輸入資料夾中所有 Blob 資料都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="616ab-293">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="616ab-294">在本教學課程中，您可指定 fileName 的值。</span><span class="sxs-lookup"><span data-stu-id="616ab-294">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="616ab-295">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-295">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-296">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-296">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-297">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-297">View the results.</span></span> <span data-ttu-id="616ab-298">如果已成功建立資料集，您會在 **結果**中看到資料集的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-298">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="616ab-299">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="616ab-299">Create output dataset</span></span>
<span data-ttu-id="616ab-300">Azure SQL Database 連結服務會指定 Data Factory 在執行階段用來連線到 Azure SQL Database 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="616ab-300">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="616ab-301">您在此步驟中建立的輸出 SQL 資料表資料集 (OututDataset) 會指定資料庫中作為 Blob 儲存體資料複製目的地的資料表。</span><span class="sxs-lookup"><span data-stu-id="616ab-301">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="616ab-302">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-302">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-303">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-303">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-304">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-304">View the results.</span></span> <span data-ttu-id="616ab-305">如果已成功建立資料集，您會在 **結果**中看到資料集的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-305">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="616ab-306">建立管線</span><span class="sxs-lookup"><span data-stu-id="616ab-306">Create pipeline</span></span>
<span data-ttu-id="616ab-307">在此步驟中，您會建立管線，其中含有使用 **AzureBlobInput** 作為輸入和使用 **AzureSqlOutput** 作為輸出的**複製活動**。</span><span class="sxs-lookup"><span data-stu-id="616ab-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="616ab-308">目前，驅動排程的是輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="616ab-308">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="616ab-309">在本教學課程中，輸出資料集設定成一小時產生一次配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-309">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="616ab-310">管線具有相隔一天 (也就是 24 小時) 的開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="616ab-310">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="616ab-311">因此，管線會產生輸出資料集的 24 個配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-311">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="616ab-312">將命令指派給名為 **cmd**的變數。</span><span class="sxs-lookup"><span data-stu-id="616ab-312">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="616ab-313">使用 **Invoke-Command**執行命令。</span><span class="sxs-lookup"><span data-stu-id="616ab-313">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="616ab-314">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="616ab-314">View the results.</span></span> <span data-ttu-id="616ab-315">如果已成功建立資料集，您會在 **結果**中看到資料集的 JSON；不然，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="616ab-315">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="616ab-316">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="616ab-316">**Congratulations!**</span></span> <span data-ttu-id="616ab-317">您已成功建立 Azure Data Factory，其中有管線可將資料從 Azure Blob 儲存體複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="616ab-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="616ab-318">監視管線</span><span class="sxs-lookup"><span data-stu-id="616ab-318">Monitor pipeline</span></span>
<span data-ttu-id="616ab-319">在此步驟中，您會使用 Data Factory REST API 來監視管線所產生的配量。</span><span class="sxs-lookup"><span data-stu-id="616ab-319">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="616ab-320">請確定在下列命令中指定的開始和結束時間符合管線的開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="616ab-320">Make sure that the start and end times specified in the following command match the start and end times of the pipeline.</span></span> 

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

<span data-ttu-id="616ab-321">執行 Invoke-Command 和下一個命令，直到您看到配量處於 [就緒] 狀態或 [失敗] 狀態。</span><span class="sxs-lookup"><span data-stu-id="616ab-321">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="616ab-322">當配量處於 [就緒] 狀態時，請檢查您的 Azure SQL Database 的 **emp** 資料表中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="616ab-322">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="616ab-323">對於每個配量，來源檔案中有兩個資料列會複製到 Azure SQL Database 中的 emp 資料表。</span><span class="sxs-lookup"><span data-stu-id="616ab-323">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="616ab-324">因此，成功處理所有配量 (處於 [就緒] 狀態) 後，您會在 emp 資料表中看到 24 筆新記錄。</span><span class="sxs-lookup"><span data-stu-id="616ab-324">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="616ab-325">摘要</span><span class="sxs-lookup"><span data-stu-id="616ab-325">Summary</span></span>
<span data-ttu-id="616ab-326">在本教學課程中，您已使用 REST API 建立要將資料從 Azure Blob 複製到 Azure SQL 資料庫的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="616ab-326">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="616ab-327">以下是您在本教學課程中執行的高階步驟：</span><span class="sxs-lookup"><span data-stu-id="616ab-327">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="616ab-328">建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="616ab-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="616ab-329">建立 **連結服務**：</span><span class="sxs-lookup"><span data-stu-id="616ab-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="616ab-330">Azure 儲存體連結服務可連結保留輸入資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="616ab-330">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="616ab-331">Azure SQL 連結服務可連結保留輸出資料的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="616ab-331">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="616ab-332">建立可描述管線輸入資料和輸出資料的 **資料集**。</span><span class="sxs-lookup"><span data-stu-id="616ab-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="616ab-333">建立具有複製活動的 **管線** ，以 BlobSource 做為來源並以 SqlSink 做為接收器。</span><span class="sxs-lookup"><span data-stu-id="616ab-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="616ab-334">後續步驟</span><span class="sxs-lookup"><span data-stu-id="616ab-334">Next steps</span></span>
<span data-ttu-id="616ab-335">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="616ab-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="616ab-336">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="616ab-336">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="616ab-337">若要深入了解如何從資料存放區雙向複製資料，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="616ab-337">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>