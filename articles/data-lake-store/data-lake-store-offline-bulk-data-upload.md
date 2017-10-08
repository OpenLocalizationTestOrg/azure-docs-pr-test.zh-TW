---
title: "aaaUpload 大量資料至資料湖存放區使用的離線方法 |Microsoft 文件"
description: "使用 hello AdlCopy 工具 toocopy 資料從 Azure 儲存體 blob tooData 湖存放區"
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
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="7594e-103">使用資料 tooData 湖存放區的離線複本的 hello Azure 匯入/匯出服務</span><span class="sxs-lookup"><span data-stu-id="7594e-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="7594e-104">在本文中，您將學習如何 toocopy 大量的資料設定 (> 200 GB) 到使用離線複製方法，例如 hello Azure Data Lake Store [Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="7594e-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="7594e-105">具體而言，用做為範例，本文章中的 hello 檔案是 339,420,860,416 位元組或約 319 GB 的磁碟上。</span><span class="sxs-lookup"><span data-stu-id="7594e-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="7594e-106">讓我將此檔案稱為 319GB.tsv。</span><span class="sxs-lookup"><span data-stu-id="7594e-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="7594e-107">hello Azure 匯入/匯出服務可協助您 tootransfer 大量的更多安全地 tooAzure Blob 儲存體傳送的硬碟磁碟機 tooan Azure 資料中心內的資料。</span><span class="sxs-lookup"><span data-stu-id="7594e-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7594e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7594e-108">Prerequisites</span></span>
<span data-ttu-id="7594e-109">在開始之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7594e-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="7594e-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7594e-110">**An Azure subscription**.</span></span> <span data-ttu-id="7594e-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7594e-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7594e-112">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7594e-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="7594e-113">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7594e-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="7594e-114">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7594e-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="7594e-115">準備 hello 資料</span><span class="sxs-lookup"><span data-stu-id="7594e-115">Preparing hello data</span></span>
<span data-ttu-id="7594e-116">在使用之前 hello 匯入/匯出服務，中斷 hello 資料檔案 toobe 傳輸**小於 200 gb 的複製**的大小。</span><span class="sxs-lookup"><span data-stu-id="7594e-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="7594e-117">hello 匯入工具不適用於檔案大於 200 GB。</span><span class="sxs-lookup"><span data-stu-id="7594e-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="7594e-118">在本教學課程中，我們必須 hello 檔案分割為 100 GB 的區塊中。</span><span class="sxs-lookup"><span data-stu-id="7594e-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="7594e-119">您可以使用 [Cygwin](https://cygwin.com/install.html) 來達成此目的。</span><span class="sxs-lookup"><span data-stu-id="7594e-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="7594e-120">Cygwin 支援 Linux 命令。</span><span class="sxs-lookup"><span data-stu-id="7594e-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="7594e-121">在此情況下，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7594e-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="7594e-122">hello split 作業會以下列名稱的 hello 建立檔案。</span><span class="sxs-lookup"><span data-stu-id="7594e-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="7594e-123">備妥資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7594e-123">Get disks ready with data</span></span>
<span data-ttu-id="7594e-124">請依照下列中的 hello 指示[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)(下 hello**準備磁碟機時**> 一節) tooprepare 硬碟機。</span><span class="sxs-lookup"><span data-stu-id="7594e-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="7594e-125">以下是 hello 整體順序：</span><span class="sxs-lookup"><span data-stu-id="7594e-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="7594e-126">取得符合 hello 需求 toobe hello Azure 匯入/匯出服務所使用的硬碟。</span><span class="sxs-lookup"><span data-stu-id="7594e-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="7594e-127">識別 Azure 儲存體帳戶之後已出貨的 toohello Azure 資料中心位置複製 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7594e-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="7594e-128">使用 hello [Azure 匯入/匯出工具](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409)，命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="7594e-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="7594e-129">以下是範例程式碼片段顯示如何 toouse hello 工具。</span><span class="sxs-lookup"><span data-stu-id="7594e-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="7594e-130">請參閱[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)for 詳細的範例程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="7594e-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="7594e-131">hello 前述的命令建立日誌檔案中的，於 hello 指定的位置。</span><span class="sxs-lookup"><span data-stu-id="7594e-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="7594e-132">使用這個日誌檔 toocreate 匯入工作從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="7594e-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="7594e-133">建立匯入作業</span><span class="sxs-lookup"><span data-stu-id="7594e-133">Create an import job</span></span>
<span data-ttu-id="7594e-134">您現在可以建立匯入工作使用中的 hello 指示[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)(下 hello**建立 hello 匯入工作**> 一節)。</span><span class="sxs-lookup"><span data-stu-id="7594e-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="7594e-135">這個匯入工作，與其他詳細資料，也提供 hello 準備 hello 磁碟機期間建立的日誌檔。</span><span class="sxs-lookup"><span data-stu-id="7594e-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="7594e-136">實際寄送 hello 磁碟機</span><span class="sxs-lookup"><span data-stu-id="7594e-136">Physically ship hello disks</span></span>
<span data-ttu-id="7594e-137">您可以現在實際送出 hello 磁碟 tooan Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="7594e-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="7594e-138">Hello 資料，複製 toohello 建立 hello 匯入工作時您所提供的 Azure 儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="7594e-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="7594e-139">此外，在建立 hello 作業時，如果您選擇 tooprovide hello 追蹤資訊之後，您現在可以移回 tooyour 匯入作業並更新 hello 追蹤號碼。</span><span class="sxs-lookup"><span data-stu-id="7594e-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="7594e-140">從 Azure 儲存體 blob tooAzure 資料湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="7594e-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="7594e-141">Hello hello 狀態之後匯入工作會顯示已完成，您可以確認是否已指定 hello Azure 儲存體 blob 中可用 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7594e-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="7594e-142">然後，您可以使用各種不同的方法 toomove hello 資料 blob tooAzure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="7594e-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="7594e-143">如需所有 hello 可用於將資料上傳選項，請參閱[擷取資料至資料湖存放區](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)。</span><span class="sxs-lookup"><span data-stu-id="7594e-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="7594e-144">在本節中，我們提供您 hello JSON 定義，您可以使用 toocreate Azure Data Factory 管線用來複製資料。</span><span class="sxs-lookup"><span data-stu-id="7594e-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="7594e-145">您可以使用這些 JSON 定義從 hello [Azure 入口網站](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md)，或[Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="7594e-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="7594e-146">來源連結服務 (Azure 儲存體 Blob)</span><span class="sxs-lookup"><span data-stu-id="7594e-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="7594e-147">目標連結服務 (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="7594e-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="7594e-148">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="7594e-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="7594e-149">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="7594e-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="7594e-150">管線 (複製活動)</span><span class="sxs-lookup"><span data-stu-id="7594e-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="7594e-151">如需詳細資訊，請參閱[移動資料從 Azure 儲存體 blob 使用 Azure Data Factory tooAzure Data Lake Store](../data-factory/data-factory-azure-datalake-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="7594e-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="7594e-152">重新建構 hello Azure 資料湖存放區中的資料檔案</span><span class="sxs-lookup"><span data-stu-id="7594e-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="7594e-153">我們已開始 319 gb，並進入它較小的大小的檔案，讓它無法使用傳送 hello Azure 匯入/匯出服務的檔案。</span><span class="sxs-lookup"><span data-stu-id="7594e-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="7594e-154">既然 hello 資料是在 Azure 資料湖存放區中，我們可以重新建構 hello 檔案 tooits 原始大小。</span><span class="sxs-lookup"><span data-stu-id="7594e-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="7594e-155">您可以使用下列 Azure PowerShell cmldts toodo 因此 hello。</span><span class="sxs-lookup"><span data-stu-id="7594e-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="7594e-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7594e-156">Next steps</span></span>
* [<span data-ttu-id="7594e-157">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="7594e-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7594e-158">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7594e-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7594e-159">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7594e-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
