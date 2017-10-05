---
title: "使用離線方法將大量資料上傳到 Data Lake Store | Microsoft Docs"
description: "使用 AdlCopy 工具將資料從 Azure 儲存體 Blob 複製到 Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="1c77f-103">使用 Azure 匯入/匯出服務將資料離線複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1c77f-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="1c77f-104">在本文中，您將深入了解如何使用離線複製方法 (例如 [Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)) 將大型資料集 (>200 GB) 複製到 Azure Data Lake Store 中。</span><span class="sxs-lookup"><span data-stu-id="1c77f-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="1c77f-105">具體來說，作為本文中範例的檔案是 339,420,860,416 個位元組，或在磁碟上大約是 319 GB。</span><span class="sxs-lookup"><span data-stu-id="1c77f-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="1c77f-106">讓我將此檔案稱為 319GB.tsv。</span><span class="sxs-lookup"><span data-stu-id="1c77f-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="1c77f-107">Azure 匯入/匯出服務可讓您將硬碟運送到 Azure 資料中心，更安全地傳輸大量資料至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c77f-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c77f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c77f-108">Prerequisites</span></span>
<span data-ttu-id="1c77f-109">開始之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="1c77f-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="1c77f-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1c77f-110">**An Azure subscription**.</span></span> <span data-ttu-id="1c77f-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1c77f-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1c77f-112">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1c77f-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="1c77f-113">**Azure 資料湖儲存區帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1c77f-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="1c77f-114">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure 資料湖儲存區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1c77f-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="1c77f-115">準備資料</span><span class="sxs-lookup"><span data-stu-id="1c77f-115">Preparing the data</span></span>
<span data-ttu-id="1c77f-116">開始使用「匯入/匯出服務」之前，請將要傳輸的資料檔分割成大小**小於 200 GB 的複本**。</span><span class="sxs-lookup"><span data-stu-id="1c77f-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="1c77f-117">匯入工具不適用於大於 200 GB 的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c77f-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="1c77f-118">在本教學課程中，我們將檔案分割成每個 100 GB 的區塊。</span><span class="sxs-lookup"><span data-stu-id="1c77f-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="1c77f-119">您可以使用 [Cygwin](https://cygwin.com/install.html) 來達成此目的。</span><span class="sxs-lookup"><span data-stu-id="1c77f-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="1c77f-120">Cygwin 支援 Linux 命令。</span><span class="sxs-lookup"><span data-stu-id="1c77f-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="1c77f-121">在此情況下，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1c77f-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="1c77f-122">分割作業會建立帶有以下名稱的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c77f-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="1c77f-123">備妥資料磁碟</span><span class="sxs-lookup"><span data-stu-id="1c77f-123">Get disks ready with data</span></span>
<span data-ttu-id="1c77f-124">依照[使用 Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)的指示 (在**準備磁碟機**一節底下) 來準備您的硬碟。</span><span class="sxs-lookup"><span data-stu-id="1c77f-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="1c77f-125">以下是整體順序︰</span><span class="sxs-lookup"><span data-stu-id="1c77f-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="1c77f-126">取得符合 Auzre 匯入/匯出服務使用需求的硬碟。</span><span class="sxs-lookup"><span data-stu-id="1c77f-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="1c77f-127">識別當資料被送至 Azure 資料中心時，將用來複製資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c77f-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="1c77f-128">使用 [Azure 匯入/匯出工具](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409)，這是一個命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="1c77f-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="1c77f-129">以下是一個有關如何使用該工具的簡單程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="1c77f-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="1c77f-130">如需更多範例程式碼片段，請參閱[使用 Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="1c77f-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="1c77f-131">前述命令會在指定的位置建立日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="1c77f-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="1c77f-132">使用此日誌檔案從 [Azure 傳統入口網站](https://manage.windowsazure.com)建立匯入作業。</span><span class="sxs-lookup"><span data-stu-id="1c77f-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="1c77f-133">建立匯入作業</span><span class="sxs-lookup"><span data-stu-id="1c77f-133">Create an import job</span></span>
<span data-ttu-id="1c77f-134">您現在可以依照[使用 Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)的指示 (在**準備磁碟機**一節底下) 來建立匯入作業。</span><span class="sxs-lookup"><span data-stu-id="1c77f-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="1c77f-135">針對此匯入作業，除了其他詳細資料之外，也請提供在準備磁碟機時建立的日誌檔。</span><span class="sxs-lookup"><span data-stu-id="1c77f-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="1c77f-136">實際寄送磁碟</span><span class="sxs-lookup"><span data-stu-id="1c77f-136">Physically ship the disks</span></span>
<span data-ttu-id="1c77f-137">您現在可以將磁碟實際寄送至 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="1c77f-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="1c77f-138">在此，資料將在這裡複製到您建立匯入作業時所提供的 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="1c77f-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="1c77f-139">此外，如果您在建立作業時選擇了稍後提供追蹤資訊，您現在便可返回您的匯入作業並更新追蹤號碼。</span><span class="sxs-lookup"><span data-stu-id="1c77f-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="1c77f-140">將資料從 Azure 儲存體 Blob 複製到 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1c77f-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="1c77f-141">匯入作業的狀態顯示為完成之後，您可以確認您指定的 Azure 儲存體 Blob 中是否有該資料。</span><span class="sxs-lookup"><span data-stu-id="1c77f-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="1c77f-142">接下來，您可以使用各種方法將該資料從 Blob 移至 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="1c77f-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="1c77f-143">如需所有可用的上傳資料選項，請參閱[將資料內嵌到 Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)。</span><span class="sxs-lookup"><span data-stu-id="1c77f-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="1c77f-144">在本節中，我們會提供您可用來建立 Azure Data Factory 管線以供複製資料的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="1c77f-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="1c77f-145">您可以從 [Azure 入口網站](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md) 使用這些 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="1c77f-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="1c77f-146">來源連結服務 (Azure 儲存體 Blob)</span><span class="sxs-lookup"><span data-stu-id="1c77f-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="1c77f-147">目標連結服務 (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="1c77f-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="1c77f-148">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="1c77f-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="1c77f-149">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="1c77f-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="1c77f-150">管線 (複製活動)</span><span class="sxs-lookup"><span data-stu-id="1c77f-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="1c77f-151">如需詳細資訊，請參閱[使用 Azure Data Factory 將資料從 Azure 儲存體 Blob 移到 Azure Data Lake Store](../data-factory/data-factory-azure-datalake-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="1c77f-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="1c77f-152">在 Azure Data Lake Store 中重新建構資料檔</span><span class="sxs-lookup"><span data-stu-id="1c77f-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="1c77f-153">我們從 319 GB 的檔案開始著手並將它分割成數個較小的檔案，以便使用 Azure 匯入/匯出服務來傳輸它。</span><span class="sxs-lookup"><span data-stu-id="1c77f-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="1c77f-154">現在，該資料在 Azure Data Lake Store 中，我們可以將檔案重新建構成其原始大小。</span><span class="sxs-lookup"><span data-stu-id="1c77f-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="1c77f-155">您可以使用下列 Azure PowerShell Cmdlet 來這麼做。</span><span class="sxs-lookup"><span data-stu-id="1c77f-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="1c77f-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c77f-156">Next steps</span></span>
* [<span data-ttu-id="1c77f-157">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="1c77f-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1c77f-158">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1c77f-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1c77f-159">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c77f-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
