---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "使用 Azure Data Factory aaaLoad 資料 |Microsoft 文件"
description: "了解使用 Azure Data Factory tooload 資料"
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
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="baefa-103">使用 Azure Data Factory 載入資料</span><span class="sxs-lookup"><span data-stu-id="baefa-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="baefa-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="baefa-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="baefa-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="baefa-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="baefa-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="baefa-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="baefa-107">BCP</span><span class="sxs-lookup"><span data-stu-id="baefa-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="baefa-108">本教學課程示範如何 toocreate Azure Data Factory toomove 資料從 Azure 儲存體 Blob tooAzure SQL 資料倉儲中的管線。</span><span class="sxs-lookup"><span data-stu-id="baefa-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="baefa-109">以下列的步驟將會看到 hello:</span><span class="sxs-lookup"><span data-stu-id="baefa-109">With hello following steps you will:</span></span>

* <span data-ttu-id="baefa-110">在 Azure 儲存體 Blob 中設定範例資料。</span><span class="sxs-lookup"><span data-stu-id="baefa-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="baefa-111">連接資源 tooAzure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="baefa-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="baefa-112">從儲存體 Blob tooSQL 資料倉儲中建立管線 toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="baefa-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="baefa-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="baefa-113">Before you begin</span></span>
<span data-ttu-id="baefa-114">toofamiliarize 自己與 Azure Data Factory，請參閱[簡介 tooAzure Data Factory][Introduction tooAzure Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="baefa-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="baefa-115">建立或識別資源</span><span class="sxs-lookup"><span data-stu-id="baefa-115">Create or identify resources</span></span>
<span data-ttu-id="baefa-116">開始之前本教學課程，您需要 toohave hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="baefa-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="baefa-117">**Azure 儲存體 Blob**： 本教學課程使用 Azure 儲存體 Blob 做 hello 資料來源 hello Azure Data Factory 管線，並因此您需要 toohave 一個可用 toostore hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="baefa-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="baefa-118">如果您還沒有已經，了解如何太[建立儲存體帳戶][Create a storage account]。</span><span class="sxs-lookup"><span data-stu-id="baefa-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="baefa-119">**SQL 資料倉儲**： 此教學課程移 hello 資料從 Azure 儲存體 Blob 太 SQL 資料倉儲，因此需要 toohave 的資料倉儲線上 hello AdventureWorksDW 範例資料會載入。</span><span class="sxs-lookup"><span data-stu-id="baefa-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="baefa-120">如果您已經沒有資料倉儲，了解如何太[佈建一個][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="baefa-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="baefa-121">如果您有資料倉儲，但未以佈建它 hello 範例資料，您可以[手動載入][Load sample data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="baefa-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="baefa-122">**Azure Data Factory**: Azure Data Factory 完成 hello 實際負載，因此您需要 toohave 其中一個，您可以使用 toobuild hello 資料移動管線。</span><span class="sxs-lookup"><span data-stu-id="baefa-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="baefa-123">如果您還沒有已經，了解如何 toocreate 其中一個步驟 1 中的[開始使用 Azure Data Factory （Data Factory 編輯器）][Get started with Azure Data Factory (Data Factory Editor)]。</span><span class="sxs-lookup"><span data-stu-id="baefa-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="baefa-124">**AZCopy**： 您需要從您的本機用戶端 tooyour Azure 儲存體 Blob 的 AZCopy toocopy hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="baefa-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="baefa-125">安裝指示，請參閱 hello [AZCopy 文件][AZCopy documentation]。</span><span class="sxs-lookup"><span data-stu-id="baefa-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="baefa-126">步驟 1： 複製範例資料 tooAzure 儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="baefa-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="baefa-127">準備的所有 hello 片段之後，您就準備好 toocopy 範例資料 tooyour Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="baefa-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="baefa-128">[下載範例資料][Download sample data]。</span><span class="sxs-lookup"><span data-stu-id="baefa-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="baefa-129">這項資料將加入另一個的三年的銷售資料 tooyour AdventureWorksDW 範例資料。</span><span class="sxs-lookup"><span data-stu-id="baefa-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="baefa-130">使用此 AZCopy 命令 toocopy hello 三年的資料 tooyour Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="baefa-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="baefa-131">步驟 2： 連接資源 tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="baefa-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="baefa-132">現在已 hello 資料就地我們可以從 Azure blob 儲存體中建立 hello Azure Data Factory 管線 toomove hello 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="baefa-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="baefa-133">啟動 tooget，開啟 hello [Azure 入口網站][ Azure portal]從 hello 左側功能表中選取您的 data factory。</span><span class="sxs-lookup"><span data-stu-id="baefa-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="baefa-134">步驟 2.1：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="baefa-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="baefa-135">連結您的 Azure 儲存體帳戶和 SQL 資料倉儲 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="baefa-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="baefa-136">首先，您的 data factory hello '連結服務' 區段，即可開始 hello 註冊程序，然後按一下'新建資料存放區。'</span><span class="sxs-lookup"><span data-stu-id="baefa-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="baefa-137">選擇名稱 tooregister 下選取的 Azure 儲存體做為您的類型，您 azure 儲存體，然後輸入您的帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="baefa-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="baefa-138">tooregister SQL 資料倉儲瀏覽 toohello '作者及部署' 區段，選取 新增資料存放區，' 然後 ' Azure SQL 資料倉儲 '。</span><span class="sxs-lookup"><span data-stu-id="baefa-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="baefa-139">複製並貼上此範本，然後填入您的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="baefa-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="baefa-140">步驟 2.2： 定義 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="baefa-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="baefa-141">建立 hello 連結的服務之後，我們必須 toodefine hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="baefa-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="baefa-142">以下這表示定義 hello 已從您的儲存體 tooyour 資料倉儲移 hello 資料結構。</span><span class="sxs-lookup"><span data-stu-id="baefa-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="baefa-143">您可以閱讀如何建立的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="baefa-143">You can read more about creating</span></span>

1. <span data-ttu-id="baefa-144">開始此程序瀏覽的 data factory toohello 「 作者和部署 」 一節。</span><span class="sxs-lookup"><span data-stu-id="baefa-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="baefa-145">'新的資料集' 按一下，然後按一下Azure Blob 儲存體' toolink 您的儲存體 tooyour data factory。</span><span class="sxs-lookup"><span data-stu-id="baefa-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="baefa-146">您可以使用下列指令碼 toodefine hello 您的資料，在 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="baefa-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="baefa-147">現在，我們要對 SQL 資料倉儲定義我們的資料集。</span><span class="sxs-lookup"><span data-stu-id="baefa-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="baefa-148">我們一開始在 hello 同樣地，按一下 新的資料集' ' Azure SQL 資料倉儲 '。</span><span class="sxs-lookup"><span data-stu-id="baefa-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="baefa-149">步驟 3：建立和執行管線</span><span class="sxs-lookup"><span data-stu-id="baefa-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="baefa-150">最後，我們會設定並執行 Azure Data Factory 中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="baefa-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="baefa-151">這是完成 hello 實際的資料移動的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="baefa-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="baefa-152">您可以找到您可完成 SQL 資料倉儲與 Azure Data Factory 的 hello 作業的完整檢視[這裡][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="baefa-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="baefa-153">在 hello '作者與部署' 區段中，按一下 '更命令' 然後 ' 新管線 '。</span><span class="sxs-lookup"><span data-stu-id="baefa-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="baefa-154">建立 hello 管線之後，您可以使用下列程式碼 tootransfer hello 資料 tooyour 資料倉儲的 hello:</span><span class="sxs-lookup"><span data-stu-id="baefa-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="baefa-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="baefa-155">Next steps</span></span>
<span data-ttu-id="baefa-156">藉由檢視詳細資訊，開始 toolearn:</span><span class="sxs-lookup"><span data-stu-id="baefa-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="baefa-157">[Azure Data Factory 的學習路徑][Azure Data Factory learning path]。</span><span class="sxs-lookup"><span data-stu-id="baefa-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="baefa-158">[Azure SQL 資料倉儲連接器][Azure SQL Data Warehouse Connector]。</span><span class="sxs-lookup"><span data-stu-id="baefa-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="baefa-159">這是適用於使用 Azure SQL 資料倉儲中的 Azure Data Factory 的 hello 核心參考主題。</span><span class="sxs-lookup"><span data-stu-id="baefa-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="baefa-160">這些主題提供 Azure Data Factory 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="baefa-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="baefa-161">他們討論 Azure SQL Database 或 HDInsight，但 hello 資訊也適用於 tooAzure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="baefa-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="baefa-162">[教學課程： 開始使用 Azure Data Factory] [ Tutorial: Get started with Azure Data Factory]這是 hello 核心教學課程來處理資料與 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="baefa-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="baefa-163">在本教學課程中，您會建置您使用 HDInsight tootransform 的第一個管線，並分析每月為基礎的網站記錄檔。</span><span class="sxs-lookup"><span data-stu-id="baefa-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="baefa-164">請注意，本教學課程中沒有複製的活動。</span><span class="sxs-lookup"><span data-stu-id="baefa-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="baefa-165">[教學課程： 將資料從 Azure 儲存體 Blob tooAzure SQL Database 中複製][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="baefa-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="baefa-166">在本教學課程中，您可以建立在 Azure Data Factory toocopy 資料管線從 Azure 儲存體 Blob tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="baefa-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
