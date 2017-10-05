---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "使用 Azure Data Factory 載入資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 載入資料"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="8ca20-103">使用 Azure Data Factory 載入資料</span><span class="sxs-lookup"><span data-stu-id="8ca20-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ca20-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="8ca20-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="8ca20-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="8ca20-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="8ca20-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="8ca20-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="8ca20-107">BCP</span><span class="sxs-lookup"><span data-stu-id="8ca20-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="8ca20-108">本教學課程說明如何在 Azure Data Factory 中建立管線，將資料從 Azure 儲存體 Blob 移至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8ca20-108">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8ca20-109">使用下列步驟，您將：</span><span class="sxs-lookup"><span data-stu-id="8ca20-109">With the following steps you will:</span></span>

* <span data-ttu-id="8ca20-110">在 Azure 儲存體 Blob 中設定範例資料。</span><span class="sxs-lookup"><span data-stu-id="8ca20-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="8ca20-111">將資源連接到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="8ca20-111">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="8ca20-112">建立管線來將資料從儲存體 Blob 移至 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8ca20-112">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="8ca20-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="8ca20-113">Before you begin</span></span>
<span data-ttu-id="8ca20-114">若要熟悉 Azure Data Factory，請參閱 [Azure Data Factory 簡介][Introduction to Azure Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-114">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="8ca20-115">建立或識別資源</span><span class="sxs-lookup"><span data-stu-id="8ca20-115">Create or identify resources</span></span>
<span data-ttu-id="8ca20-116">開始進行本教學課程之前，您需要有下列資源：</span><span class="sxs-lookup"><span data-stu-id="8ca20-116">Before starting this tutorial, you need to have the following resources:</span></span>

* <span data-ttu-id="8ca20-117">**Azure 儲存體 Blob**：本教學課程使用 Azure 儲存體 Blob 做為 Azure Data Factory 管線的資料來源，因此您需要有此資源來儲存範例資料。</span><span class="sxs-lookup"><span data-stu-id="8ca20-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="8ca20-118">如果您沒有此資源，請了解如何[建立儲存體帳戶][Create a storage account]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-118">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="8ca20-119">**SQL 資料倉儲**：本教學課程會將資料從 Azure 儲存體 Blob 移至 SQL 資料倉儲，因此需要有線上的資料倉儲且已載入 AdventureWorksDW 範例資料。</span><span class="sxs-lookup"><span data-stu-id="8ca20-119">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="8ca20-120">如果您還沒有資料倉儲，請了解如何[佈建資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-120">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="8ca20-121">如果您已有資料倉儲，但未使用範例資料來進行佈建，您可以[手動載入它][Load sample data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-121">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="8ca20-122">**Azure Data Factory**：Azure Data Factory 會完成實際的負載，因此您必須擁有一個以便用來建置資料移動管線。</span><span class="sxs-lookup"><span data-stu-id="8ca20-122">**Azure Data Factory**: Azure Data Factory completes the actual load and so you need to have one that you can use to build the data movement pipeline.</span></span> <span data-ttu-id="8ca20-123">如果您還沒有資料倉儲，請在[開始使用 Azure Data Factory (Data Factory 編輯器)][Get started with Azure Data Factory (Data Factory Editor)] 的步驟 1 中了解如何建立一個。</span><span class="sxs-lookup"><span data-stu-id="8ca20-123">If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="8ca20-124">**AZCopy**：您需要有 AZCopy 將本機用戶端的範例資料複製到您的 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="8ca20-124">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="8ca20-125">如需安裝指示，請參閱 [AZCopy 文件][AZCopy documentation]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-125">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="8ca20-126">步驟 1：將範例資料複製到 Azure 儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="8ca20-126">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="8ca20-127">一切就緒時，您就可以開始將範例資料複製到您的 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="8ca20-127">Once you have all the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="8ca20-128">[下載範例資料][Download sample data]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="8ca20-129">這項資料會將另外三年份的銷售資料新增至 AdventureWorksDW 範例資料。</span><span class="sxs-lookup"><span data-stu-id="8ca20-129">This data adds another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="8ca20-130">使用此 AZCopy 命令，將三年份的資料複製到您的 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="8ca20-130">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="8ca20-131">步驟 2：將資源連接到 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8ca20-131">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="8ca20-132">既然已備妥資料，我們可以開始建立 Azure Data Factory 管線，將資料從 Azure Blob 儲存體移至 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8ca20-132">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="8ca20-133">首先，請開啟 [Azure 入口網站][Azure portal]，從左側功能表中選取您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="8ca20-133">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="8ca20-134">步驟 2.1：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="8ca20-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="8ca20-135">將您的 Azure 儲存體帳戶和 SQL 資料倉儲連結到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="8ca20-135">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="8ca20-136">首先，按一下 Data Factory 的 [連結服務] 區段來開始註冊程序，然後按一下 [新資料存放區]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-136">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="8ca20-137">選擇要用來註冊 Azure 儲存體的名稱、選取 Azure 儲存體做為類型，然後輸入您的帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="8ca20-137">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="8ca20-138">若要註冊 SQL 資料倉儲，請瀏覽至 [編寫及部署] 區段，選取 [新資料存放區]，然後選取 [Azure SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-138">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="8ca20-139">複製並貼上此範本，然後填入您的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="8ca20-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="8ca20-140">步驟 2.2：定義資料集</span><span class="sxs-lookup"><span data-stu-id="8ca20-140">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="8ca20-141">建立連結服務之後，我們必須定義資料集。</span><span class="sxs-lookup"><span data-stu-id="8ca20-141">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="8ca20-142">在這裡，此舉表示將定義要從儲存體移至資料倉儲的資料結構。</span><span class="sxs-lookup"><span data-stu-id="8ca20-142">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="8ca20-143">您可以閱讀如何建立的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8ca20-143">You can read more about creating</span></span>

1. <span data-ttu-id="8ca20-144">若要開始此程序，請瀏覽至 Data Factory 的 [作者與部署] 區段。</span><span class="sxs-lookup"><span data-stu-id="8ca20-144">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="8ca20-145">依序按一下 [新增資料集] 和 [Azure Blob 儲存體]，以將儲存體連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="8ca20-145">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="8ca20-146">您可以使用以下指令碼，在 Azure Blob 儲存體中定義您的資料：</span><span class="sxs-lookup"><span data-stu-id="8ca20-146">You can use the below script to define your data in Azure Blob storage:</span></span>
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. <span data-ttu-id="8ca20-147">現在，我們要對 SQL 資料倉儲定義我們的資料集。</span><span class="sxs-lookup"><span data-stu-id="8ca20-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="8ca20-148">我們以相同方式開始，即依序按一下 [新增資料集] 和 [Azure SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-148">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="8ca20-149">步驟 3：建立和執行管線</span><span class="sxs-lookup"><span data-stu-id="8ca20-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="8ca20-150">最後，我們要在 Azure Data Factory 中安裝並執行管線。</span><span class="sxs-lookup"><span data-stu-id="8ca20-150">Finally, we set up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="8ca20-151">這是會完成實際資料移動的作業。</span><span class="sxs-lookup"><span data-stu-id="8ca20-151">This is the operation that completes the actual data movement.</span></span>  <span data-ttu-id="8ca20-152">您可以在[這裡][Move data to and from Azure SQL Data Warehouse using Azure Data Factory]找到可以使用 SQL 資料倉儲和 Azure Data Factory 完成之作業的完整檢視。</span><span class="sxs-lookup"><span data-stu-id="8ca20-152">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="8ca20-153">在 [製作和部署] 區段中，依序按一下 [其他命令] 和 [新增管線]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-153">In the 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="8ca20-154">建立管線之後，您可以使用以下程式碼，將資料傳送到資料倉儲：</span><span class="sxs-lookup"><span data-stu-id="8ca20-154">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8ca20-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ca20-155">Next steps</span></span>
<span data-ttu-id="8ca20-156">若要深入了解，首先請檢視：</span><span class="sxs-lookup"><span data-stu-id="8ca20-156">To learn more, start by viewing:</span></span>

* <span data-ttu-id="8ca20-157">[Azure Data Factory 的學習路徑][Azure Data Factory learning path]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="8ca20-158">[Azure SQL 資料倉儲連接器][Azure SQL Data Warehouse Connector]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="8ca20-159">這是搭配使用 Azure Data Factory 與 Azure SQL 資料倉儲的核心參考主題。</span><span class="sxs-lookup"><span data-stu-id="8ca20-159">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="8ca20-160">這些主題提供 Azure Data Factory 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8ca20-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="8ca20-161">其中討論 Azure SQL Database 或 HDInsight，但資訊也適用於 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8ca20-161">They discuss Azure SQL Database or HDInsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="8ca20-162">[教學課程：開始使用 Azure Data Factory][Tutorial: Get started with Azure Data Factory]這是使用 Azure Data Factory 處理資料的核心教學課程。</span><span class="sxs-lookup"><span data-stu-id="8ca20-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="8ca20-163">在本教學課程中，您將建置第一個管線，在每個月使用 HDInsight 來轉換及分析 Web 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8ca20-163">In this tutorial, you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="8ca20-164">請注意，本教學課程中沒有複製的活動。</span><span class="sxs-lookup"><span data-stu-id="8ca20-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="8ca20-165">[教學課程：將資料從 Azure 儲存體 Blob 複製到 Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="8ca20-165">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="8ca20-166">在本教學課程中，您會在 Azure Data Factory 中建立管線，將資料從 Azure 儲存體 Blob 複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8ca20-166">In this tutorial, you create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
