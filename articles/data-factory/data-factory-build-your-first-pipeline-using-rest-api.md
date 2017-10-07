---
title: "aaaBuild 您第一次的 data factory (REST) |Microsoft 文件"
description: "在本教學課程中，您會使用 Data Factory REST API 建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>教學課程：使用 Data Factory REST API 建置您的第一個 Azure Data Factory
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-build-your-first-pipeline.md)
> * [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


在本文中，您使用 Data Factory REST API toocreate 第一個 Azure data factory。 toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。

在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。 此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。 hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。

> [!NOTE]
> 本文並未涵蓋所有 hello REST API。 如需 REST API 的完整文件，請參閱 [Data Factory REST API 參考](/rest/api/datafactory/)。
> 
> 一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。


## <a name="prerequisites"></a>必要條件
* 閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。
* 在您的電腦上安裝 [Curl](https://curl.haxx.se/dlwiz/) 。 您可以使用 hello CURL 工具與其他命令 toocreate data factory。
* 請依照 [本文](../azure-resource-manager/resource-group-create-service-principal-portal.md) 的指示：
  1. 在 Azure Active Directory 中建立名為 **ADFGetStartedApp** 的 Web 應用程式。
  2. 取得**用戶端識別碼**和**秘密金鑰**。
  3. 取得 **租用戶識別碼**。
  4. 指派 hello **ADFGetStartedApp**應用程式 toohello**資料 Factory 參與者**角色。
* 安裝 [Azure PowerShell](/powershell/azure/overview)。
* 啟動**PowerShell**和 hello 執行下列命令。 保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。 如果您關閉並重新開啟，您需要 toorun hello 命令一次。
  1. 執行**登入 AzureRmAccount** ，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。
  2. 執行**Get AzureRmSubscription** tooview 所有 hello 這個帳戶的訂用帳戶。
  3. 執行**Get AzureRmSubscription-訂用帳戶名稱 NameOfAzureSubscription |設定 AzureRmContext** tooselect hello 訂用帳戶，您想要使用 toowork。 取代**NameOfAzureSubscription** hello 的 Azure 訂用帳戶的名稱。
* 建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   本教學課程中的 hello 步驟假設您使用名為 ADFTutorialResourceGroup hello 資源群組。 如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。

## <a name="create-json-definitions"></a>建立 JSON 定義
建立下列 hello curl.exe 所在的資料夾中的 JSON 檔案。

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> 名稱必須是全域唯一的因此您可能需要 tooprefix/後置詞 ADFCopyTutorialDF toomake 它唯一的名稱。
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> 以 Azure 儲存體帳戶的名稱和金鑰取代 **accountname** 和 **accountkey**。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱有關如何 tooview、 複製和重新產生儲存體存取金鑰中的 hello 資訊[管理您的儲存體帳戶](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。
>
>

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

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

| 屬性 | 說明 |
|:--- |:--- |
| ClusterSize |Hello HDInsight 叢集的大小。 |
| TimeToLive |於刪除之前，請指定 hello HDInsight 叢集，該 hello 閒置時間。 |
| linkedServiceName |指定 hello 是使用的 toostore hello 記錄 HDInsight 所產生的儲存體帳戶 |

請注意下列點 hello:

* hello Data Factory 建立**linux**上方 JSON hello 與您的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。
* 您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。
* hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 HDInsight 叢集隨 HDInsight 連結服務，以建立每一次，除非有現有的叢集即時處理配量 (**timeToLive**) 和 hello 處理完成時刪除。

    隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。

如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

hello JSON 定義名為資料集**AzureBlobInput**，代表 hello 管線中活動的輸入的資料。 此外，它會指定 hello 輸入的資料位於呼叫 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**inputdata**。

hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |hello 類型屬性是設定 tooAzureBlob，因為資料常駐於 Azure blob 儲存體中。 |
| linkedServiceName |是指您稍早建立的 StorageLinkedService toohello。 |
| fileName |這是選用屬性。 如果您省略這個屬性時，會挑出 hello folderPath 中的所有 hello 檔案。 在此情況下，只有 hello input.log 會進行處理。 |
| 類型 |hello 記錄檔是以文字格式，因此我們使用 TextFormat。 |
| columnDelimiter |hello 記錄檔中的資料行是以逗號 （，） 分隔 |
| frequency/interval |設定 tooMonth 頻率和間隔為 1，這表示的 hello 輸入配量可使用每個月。 |
| external |設定此屬性是 tootrue hello 輸入的資料不會產生 hello Data Factory 服務。 |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

hello JSON 定義名為資料集**AzureBlobOutput**，代表 hello 管線中活動的輸出資料。 此外，它會指定 hello 結果會儲存在稱為 hello blob 容器**adfgetstarted**和 hello 資料夾稱為**partitioneddata**。 hello**可用性**區段會指定該 hello 輸出資料集產生每月為基礎。

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> 以您的 Azure 儲存體帳戶名稱取代 **storageaccountname** 。
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

在 hello JSON 片段中，您要建立管線的 HDInsight 叢集使用 Hive tooprocess 資料的活動所組成。

hello Hive 指令碼檔案， **partitionweblogs.hql**，儲存在 hello Azure 儲存體帳戶 (由 hello scriptLinkedService，稱為**StorageLinkedService**)，然後在**指令碼** hello 容器中的資料夾**adfgetstarted**。

hello**定義**區段會指定 Hive 組態值會傳遞 toohello hive 指令碼的執行階段設定 (例如 ${hiveconf: inputtable}，{hiveconf:partitionedtable} $)。

hello**啟動**和**結束**hello 管線屬性指定 hello 之 hello 管線的作用期間。

在 hello 活動 JSON 中，您指定該 hello Hive 指令碼在上執行指定 hello hello 計算**linkedServiceName** – **HDInsightOnDemandLinkedService**。

> [!NOTE]
> 請參閱中的"管線 JSON"[管線和 Azure Data Factory 中的活動](data-factory-create-pipelines.md)hello 前面範例中使用的 JSON 內容的詳細資料。
>
>

## <a name="set-global-variables"></a>設定全域變數
在 Azure PowerShell，執行下列命令以您自己取代 hello 值後的 hello:

> [!IMPORTANT]
> 如需取得用戶端識別碼、用戶端密碼、租用戶識別碼及訂用帳戶識別碼的指示，請參閱 [必要條件](#prerequisites) 一節。
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>使用 AAD 驗證

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>建立 Data Factory
在此步驟中，您會建立名為 **FirstDataFactoryREST**的 Azure Data Factory。 資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 資料。 執行下列命令 toocreate hello 資料處理站的 hello:

1. 指定名為 hello 命令 toovariable **cmd**。

    確認您在此處指定 (ADFCopyTutorialDF) 相符項目 hello hello 中指定名稱的 hello data factory 名稱 hello **datafactory.json**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果 hello data factory 建立成功，您會看見 hello JSON hello data factory 中 hello**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```

請注意下列點 hello:

* hello hello Azure Data Factory 名稱必須是全域唯一的。 如果您看到結果中的 hello 錯誤： **Data factory 名稱"FirstDataFactoryREST"不是使用**，執行下列步驟 hello:
  1. 在 hello 變更 hello 名稱 (例如，yournameFirstDataFactoryREST) **datafactory.json**檔案。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
  2. Hello 第一個命令中其中 hello **$cmd**值指派給變數，請取代 FirstDataFactoryREST hello 新名稱，執行 hello 命令。
  3. 執行 hello 下面兩個命令 tooinvoke hello REST API toocreate hello 資料處理站和列印 hello hello 作業結果。
* toocreate Data Factory 執行個體，您需要 toobe 參與者/系統管理員的 hello Azure 訂用帳戶
* 可能會註冊為未來的 hello 中的 DNS 名稱，因此變得可見 hello hello data factory 名稱。
* 如果您收到 hello 錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**」，請勿 hello 下列其中一種，然後再試一次發行：

  * 在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      您可以執行下列命令 tooconfirm hello Data Factory 提供者註冊該 hello:
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * 登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。 這個動作會自動註冊 hello 您的提供者。

之前建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。 您第一次建立連結的服務 toolink 資料存放區/計算 tooyour 資料存放區，定義輸入和輸出連結的資料存放區中的資料集 toorepresent 資料。

## <a name="create-linked-services"></a>建立連結的服務
在此步驟中，您可以連結您的 Azure 儲存體帳戶和隨 Azure HDInsight 叢集 tooyour 資料處理站。 hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。 hello HDInsight 連結服務是使用的 toorun hello 管線，在此範例中的 hello 活動中指定的 Hive 指令碼。

### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。 本教學課程中，您使用 hello toostore 輸入/輸出資料與 hello HQL 指令碼檔案的相同 Azure 儲存體帳戶。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>建立 Azure HDInsight 連結服務
在此步驟中，您可以連結的隨選 HDInsight 叢集 tooyour 資料 factory。 自動在執行階段建立及刪除它為了處理和閒置 hello 指定的時間量之後 hello HDInsight 叢集。 您可以使用自己的 HDInsight 叢集，不必使用隨選的 HDInsight 叢集。 請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>建立資料集
在此步驟中，您可以建立資料集 toorepresent hello 輸入和輸出 Hive 處理的資料。 這些資料集，請參閱 toohello **StorageLinkedService**稍早在本教學課程中，您已建立。 hello 連結的服務點 tooan Azure 儲存體帳戶和資料集指定保留輸入 hello 儲存體中的容器、 資料夾、 檔案名稱和輸出資料。

### <a name="create-input-dataset"></a>建立輸入資料集
在此步驟中，您可以建立 hello 輸入資料集 toorepresent 輸入的資料儲存在 hello Azure Blob 儲存體。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>建立輸出資料集
在此步驟中，您可以建立 hello 輸出資料集 toorepresent 輸出資料儲存在 hello Azure Blob 儲存體中。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>建立管線
在此步驟中，您會建立第一個具有 **HDInsightHive** 活動的管線。 輸入的配量可每月 (頻率： Month、 interval: 1)、 每月產生輸出配量和 hello hello 活動的排程器屬性也設定 toomonthly。 hello 輸出資料集和 hello 活動排程器的 hello 設定必須相符。 目前，輸出資料集是哪些磁碟機 hello 排程，因此您必須建立輸出資料集，即使 hello 活動不會產生任何輸出。 如果 hello 活動不接受任何輸入，您可以略過建立 hello 輸入資料集。

確認您看到 hello **input.log**檔案在 hello **adfgetstarted/inputdata** hello Azure blob 儲存體，並執行下列命令 toodeploy hello 管線的 hello 中的資料夾。 因為 hello**啟動**和**結束**次數設定在過去的 hello 和**isPaused**是集 toofalse，hello 管線 （hello 管線中的活動） 執行您部署之後，立即。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果已成功建立 hello 資料集，您會看見 hello JSON hello hello 中的資料集**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell
    Write-Host $results
    ```
4. 恭喜，您已經成功使用 Azure PowerShell 建立您的第一個管線！

## <a name="monitor-pipeline"></a>監視管線
在此步驟中，您可以使用 Data Factory REST API toomonitor 配量 hello 管線所產生。

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> 建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。 因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。
>
>

執行 hello Invoke-command 和 hello 下一個直到您看到 hello 配量中的**準備**狀態或**失敗**狀態。 當 hello 配量處於就緒狀態時，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。  hello 建立隨選 HDInsight 叢集通常需要一些時間。

![輸出資料](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> 已成功處理 hello 配量時，取得刪除 hello 輸入的檔。 因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。
>
>

您也可以使用 Azure 入口網站 toomonitor 配量，以及疑難排解任何問題。 如需詳細，請參閱 [使用 Azure 入口網站監視管線](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 。

## <a name="summary"></a>摘要
在本教學課程中，您可以建立 Azure data factory tooprocess 資料在 HDInsight hadoop 叢集上執行 Hive 指令碼。 您使用 hello Data Factory 編輯器在 hello Azure 入口網站 toodo hello 下列步驟：

1. 建立 Azure **Data Factory**。
2. 建立兩個 **連結服務**：
   1. **Azure 儲存體**您保留輸入/輸出檔案 toohello 資料處理站的 Azure blob 儲存體連結服務 toolink。
   2. **Azure HDInsight**視連結的服務 toolink 隨 HDInsight Hadoop 叢集 toohello 資料 factory。 Azure Data Factory 建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料，並產生輸出資料。
3. 建立兩個**資料集**，其中描述輸入和輸出 HDInsight Hive 活動 hello 管線中的資料。
4. 建立具有 **HDInsight Hive** 活動的**管線**。

## <a name="next-steps"></a>後續步驟
在本文中，您已經建立可在隨選 Azure HDInsight 叢集上執行 Hive 指令碼，含有轉換活動 (HDInsight 活動) 的管線。 如何 toouse 複製活動 toocopy 資料從 Azure Blob tooAzure SQL，請參閱的 toosee[教學課程： 將資料從 Azure Blob tooAzure SQL 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。

## <a name="see-also"></a>另請參閱
| 主題 | 說明 |
|:--- |:--- |
| [Data Factory REST API 參考](/rest/api/datafactory/) |請參閱 Data Factory Cmdlet 中的完整文件 |
| [管線](data-factory-create-pipelines.md) |這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。 |
| [資料集](data-factory-create-datasets.md) |本文協助您了解 Azure Data Factory 中的資料集。 |
| [排程和執行](data-factory-scheduling-and-execution.md) |本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。 |
| [使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md) |本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。 |
