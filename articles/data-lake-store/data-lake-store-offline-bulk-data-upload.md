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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>使用資料 tooData 湖存放區的離線複本的 hello Azure 匯入/匯出服務
在本文中，您將學習如何 toocopy 大量的資料設定 (> 200 GB) 到使用離線複製方法，例如 hello Azure Data Lake Store [Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)。 具體而言，用做為範例，本文章中的 hello 檔案是 339,420,860,416 位元組或約 319 GB 的磁碟上。 讓我將此檔案稱為 319GB.tsv。

hello Azure 匯入/匯出服務可協助您 tootransfer 大量的更多安全地 tooAzure Blob 儲存體傳送的硬碟磁碟機 tooan Azure 資料中心內的資料。

## <a name="prerequisites"></a>必要條件
在開始之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure 儲存體帳戶**。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>準備 hello 資料
在使用之前 hello 匯入/匯出服務，中斷 hello 資料檔案 toobe 傳輸**小於 200 gb 的複製**的大小。 hello 匯入工具不適用於檔案大於 200 GB。 在本教學課程中，我們必須 hello 檔案分割為 100 GB 的區塊中。 您可以使用 [Cygwin](https://cygwin.com/install.html) 來達成此目的。 Cygwin 支援 Linux 命令。 在此情況下，使用下列命令的 hello:

    split -b 100m 319GB.tsv

hello split 作業會以下列名稱的 hello 建立檔案。

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>備妥資料磁碟
請依照下列中的 hello 指示[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)(下 hello**準備磁碟機時**> 一節) tooprepare 硬碟機。 以下是 hello 整體順序：

1. 取得符合 hello 需求 toobe hello Azure 匯入/匯出服務所使用的硬碟。
2. 識別 Azure 儲存體帳戶之後已出貨的 toohello Azure 資料中心位置複製 hello 資料。
3. 使用 hello [Azure 匯入/匯出工具](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409)，命令列公用程式。 以下是範例程式碼片段顯示如何 toouse hello 工具。

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    請參閱[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)for 詳細的範例程式碼片段。
4. hello 前述的命令建立日誌檔案中的，於 hello 指定的位置。 使用這個日誌檔 toocreate 匯入工作從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。

## <a name="create-an-import-job"></a>建立匯入作業
您現在可以建立匯入工作使用中的 hello 指示[使用 hello Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)(下 hello**建立 hello 匯入工作**> 一節)。 這個匯入工作，與其他詳細資料，也提供 hello 準備 hello 磁碟機期間建立的日誌檔。

## <a name="physically-ship-hello-disks"></a>實際寄送 hello 磁碟機
您可以現在實際送出 hello 磁碟 tooan Azure 資料中心。 Hello 資料，複製 toohello 建立 hello 匯入工作時您所提供的 Azure 儲存體 blob。 此外，在建立 hello 作業時，如果您選擇 tooprovide hello 追蹤資訊之後，您現在可以移回 tooyour 匯入作業並更新 hello 追蹤號碼。

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>從 Azure 儲存體 blob tooAzure 資料湖存放區複製資料
Hello hello 狀態之後匯入工作會顯示已完成，您可以確認是否已指定 hello Azure 儲存體 blob 中可用 hello 資料。 然後，您可以使用各種不同的方法 toomove hello 資料 blob tooAzure 資料湖存放區。 如需所有 hello 可用於將資料上傳選項，請參閱[擷取資料至資料湖存放區](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)。

在本節中，我們提供您 hello JSON 定義，您可以使用 toocreate Azure Data Factory 管線用來複製資料。 您可以使用這些 JSON 定義從 hello [Azure 入口網站](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md)，或[Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md)。

### <a name="source-linked-service-azure-storage-blob"></a>來源連結服務 (Azure 儲存體 Blob)
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

### <a name="target-linked-service-azure-data-lake-store"></a>目標連結服務 (Azure Data Lake Store)
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
### <a name="input-data-set"></a>輸入資料集
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
### <a name="output-data-set"></a>輸出資料集
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
### <a name="pipeline-copy-activity"></a>管線 (複製活動)
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
如需詳細資訊，請參閱[移動資料從 Azure 儲存體 blob 使用 Azure Data Factory tooAzure Data Lake Store](../data-factory/data-factory-azure-datalake-connector.md)。

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>重新建構 hello Azure 資料湖存放區中的資料檔案
我們已開始 319 gb，並進入它較小的大小的檔案，讓它無法使用傳送 hello Azure 匯入/匯出服務的檔案。 既然 hello 資料是在 Azure 資料湖存放區中，我們可以重新建構 hello 檔案 tooits 原始大小。 您可以使用下列 Azure PowerShell cmldts toodo 因此 hello。

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

## <a name="next-steps"></a>後續步驟
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
