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
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>教學課程： 使用 REST API toocreate Azure Data Factory 管線 toocopy 資料 
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [複製精靈](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

在本文中，您學會如何 toouse 會 REST API toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。 如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。   

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。

> [!NOTE]
> 本文並未涵蓋所有 hello Data Factory REST API。 如需 Data Factory Cmdlet 的完整文件，請參閱 [Data Factory REST API 參考](/rest/api/datafactory/) 。
>  
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

## <a name="prerequisites"></a>必要條件
* 透過移[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)和完整 hello**必要條件**步驟。
* 在您的電腦上安裝 [Curl](https://curl.haxx.se/dlwiz/) 。 您可以使用 hello Curl 工具與其他命令 toocreate data factory。 
* 請依照 [本文](../azure-resource-manager/resource-group-create-service-principal-portal.md) 的指示： 
  1. 在 Azure Active Directory 中建立名為 **ADFCopyTutorialApp** 的 Web 應用程式。
  2. 取得**用戶端識別碼**和**秘密金鑰**。 
  3. 取得 **租用戶識別碼**。 
  4. 指派 hello **ADFCopyTutorialApp**應用程式 toohello**資料 Factory 參與者**角色。  
* 安裝 [Azure PowerShell](/powershell/azure/overview)。  
* 啟動**PowerShell**並執行下列步驟 hello。 保持開啟 Azure PowerShell 直到本教學課程中的 hello 結尾。 如果您關閉並重新開啟，您需要 toorun hello 命令一次。
  
  1. 執行下列命令的 hello，然後輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中：
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. 此帳戶的所有 hello 訂用帳戶都執行下列命令 tooview hello:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. 執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。 取代 **&lt;NameOfAzureSubscription** &gt; hello 的 Azure 訂用帳戶的名稱。 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. 建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      如果已經存在 hello 資源群組，指定是否 tooupdate 它 (Y) 或保留為 (N)。 
     
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
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> 以 Azure 儲存體帳戶的名稱和金鑰取代 **accountname** 和 **accountkey**。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。

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

如需 JSON 屬性的詳細資訊，請參閱 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)。

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> 取代**servername**， **databasename**， **username**，和**密碼**名稱為您的 Azure SQL server，SQL 資料庫名稱的使用者帳戶和 hello 帳戶密碼。  
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

如需 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)。

### <a name="inputdatasetjson"></a>inputdataset.json

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

hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

| 屬性 | 說明 |
|:--- |:--- |
| 類型 | hello type 屬性設定太**AzureBlob**因為資料常駐於 Azure blob 儲存體中。 |
| linkedServiceName | 是指 toohello **AzureStorageLinkedService**您稍早建立的。 |
| folderPath | 指定 hello blob**容器**和 hello**資料夾**，其中包含輸入的 blob。 在本教學課程，adftutorial hello blob 容器且資料夾是 hello 根資料夾。 | 
| fileName | 這是選用屬性。 如果您省略這個屬性時，會挑出 hello folderPath 中的所有檔案。 在本教學課程， **emp.txt**指定了 hello 檔名，因此只有該檔案所挑選的處理。 |
| format -> type |hello 輸入的檔為 hello 文字格式，因此我們使用**TextFormat**。 |
| columnDelimiter | hello hello 輸入檔中的資料行分隔**逗號字元 (`,`)**。 |
| frequency/interval | hello 頻率設定過**小時**和間隔設定得**1**，這表示該 hello 輸入配量可用**每小時**。 換句話說，hello Data Factory 服務會尋找輸入資料每小時的 blob 容器的 hello 根資料夾中 (**adftutorial**) 指定。 它會尋找 hello hello 管線開始和結束時間、 不之前或之後這段時間內的資料。  |
| external | 這個屬性設定太**true**如果 hello 資料不會產生此管線。 在此教學課程中的 hello 輸入的資料是在 hello emp.txt 檔案，不會產生這個管線，因此我們設定此屬性 tootrue。 |

如需這些 JSON 屬性的詳細資訊，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md#dataset-properties)一文。

### <a name="outputdatasetjson"></a>outputdataset.json

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
hello 下表提供 hello hello 程式碼片段中使用的 JSON 屬性的說明：

| 屬性 | 說明 |
|:--- |:--- |
| 類型 | hello type 屬性設定太**AzureSqlTable**因為資料是在 Azure SQL database 中的複製的 tooa 資料表。 |
| linkedServiceName | 是指 toohello **AzureSqlLinkedService**您稍早建立的。 |
| tableName | 指定的 hello**資料表**toowhich hello 資料複製。 | 
| frequency/interval | hello 頻率設定過**小時**和間隔是**1**，這表示 hello 輸出配量所產生**每小時**之間 hello 管線開始和結束時間，不是在之前或之後這段時間。  |

有三個資料行 –**識別碼**， **FirstName**，和**LastName** – hello 資料庫中的 hello emp 資料表中。 識別碼是識別資料行，所以您必須只 toospecify **FirstName**和**LastName**這裡。

如需這些 JSON 屬性的詳細資訊，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md#dataset-properties)一文。

### <a name="pipelinejson"></a>pipeline.json

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

請注意下列點 hello:

- 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。
- 輸入 hello 活動設定太**AzureBlobInput**和輸出 hello 活動設定太**AzureSqlOutput**。 
- 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。 支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。  
 
取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。 您可以指定 hello 日期部分，並略過 hello hello 時間部分日期時間。 例如，"2017年-02-03"，這相當於太"2017年-02-03T00:00:00Z"
 
開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2016-10-14T16:32:41Z。 hello**結束**時間是選擇性的但我們在本教學課程中使用它。 
 
如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。 無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。
 
在上述範例中的 hello，有 24 資料配量每小時產生每個資料分割。

如需管線定義中 JSON 屬性的說明，請參閱[建立管線](data-factory-create-pipelines.md)一文。 如需複製活動定義中 JSON 屬性的說明，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 如需 BlobSource 所支援 JSON 屬性的說明，請參閱 [Azure Blob 連接器](data-factory-azure-blob-connector.md)一文。 如需 SqlSink 支援的 JSON 屬性說明，請參閱 [Azure SQL Database 連接器](data-factory-azure-sql-connector.md)一文。

## <a name="set-global-variables"></a>設定全域變數
在 Azure PowerShell，執行下列命令以您自己取代 hello 值後的 hello:

> [!IMPORTANT]
> 如需取得用戶端識別碼、用戶端密碼、租用戶識別碼及訂用帳戶識別碼的指示，請參閱 [必要條件](#prerequisites) 一節。   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

您使用執行的 hello hello hello data factory 名稱在更新之後，下列命令： 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>使用 AAD 驗證
執行下列命令 tooauthenticate 與 Azure Active Directory (AAD) 的 hello: 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>建立 Data Factory
在此步驟中，您會建立名為 **ADFCopyTutorialDF**的 Azure Data Factory。 資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區。 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。 執行下列命令 toocreate hello 資料處理站的 hello: 

1. 指定名為 hello 命令 toovariable **cmd**。 
   
    > [!IMPORTANT]
    > 確認您在此處指定 (ADFCopyTutorialDF) 相符項目 hello hello 中指定名稱的 hello data factory 名稱 hello **datafactory.json**。 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果 hello data factory 建立成功，您會看見 hello JSON hello data factory 中 hello**結果**; 否則您會看到一則錯誤訊息。  
   
    ```
    Write-Host $results
    ```

請注意下列點 hello:

* hello hello Azure Data Factory 名稱必須是全域唯一的。 如果您看到結果中的 hello 錯誤： **Data factory 名稱"ADFCopyTutorialDF"不是使用**，執行下列步驟 hello:  
  
  1. 在 hello 變更 hello 名稱 (例如，yournameADFCopyTutorialDF) **datafactory.json**檔案。
  2. Hello 第一個命令中其中 hello **$cmd**值指派給變數，請取代 ADFCopyTutorialDF hello 新名稱，執行 hello 命令。 
  3. 執行 hello 下面兩個命令 tooinvoke hello REST API toocreate hello 資料處理站和列印 hello hello 作業結果。 
     
     請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
* toocreate Data Factory 執行個體，您需要 toobe 參與者/系統管理員的 hello Azure 訂用帳戶
* 可能會註冊為未來的 hello 中的 DNS 名稱，因此變得可見 hello hello data factory 名稱。
* 如果您收到 hello 錯誤:"**此訂用帳戶不是已註冊的 toouse 命名空間 Microsoft.DataFactory**」，請勿 hello 下列其中一種，然後再試一次發行： 
  
  * 在 Azure PowerShell 中執行下列命令 tooregister hello Data Factory 提供者的 hello: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    您可以執行下列命令 tooconfirm hello 該 hello Data Factory 提供者註冊。 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * 登入使用 hello hello 到 Azure 訂用帳戶[Azure 入口網站](https://portal.azure.com)並瀏覽 tooa Data Factory 刀鋒視窗 （或） 在 hello Azure 入口網站中建立 data factory。 這個動作會自動註冊 hello 您的提供者。

之前建立管線，您必須 toocreate 幾個 Data Factory 實體第一次。 您第一次建立連結的服務 toolink 來源和目的地資料存放區 tooyour 資料存放區。 然後，定義輸入和輸出資料集 toorepresent 資料連結的資料存放區中。 最後，建立 hello 管線與該活動會使用這些資料集。

## <a name="create-linked-services"></a>建立連結的服務
您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。 在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。 您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。 因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。  

hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。   

AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。  

### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
在此步驟中，您必須連結您的 Azure 儲存體帳戶 tooyour data factory。 您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。 請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。  

1. 指定名為 hello 命令 toovariable **cmd**。 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. 使用執行 hello 命令**Invoke-command**。

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. 檢視 hello 結果。 如果 hello 連結已成功建立服務，您會看到 hello 中的 hello 連結服務的 hello JSON**結果**; 否則您會看到一則錯誤訊息。

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>建立 Azure SQL 連結服務
在此步驟中，您可以連結您的 Azure SQL database tooyour data factory。 您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。 請參閱[Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 連結服務。

1. 指定名為 hello 命令 toovariable **cmd**。 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
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
在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 在此步驟中，您可以定義名為 AzureBlobInput AzureSqlOutput 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。

hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集 (AzureBlobInput) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。 

### <a name="create-input-dataset"></a>建立輸入資料集
在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) AzureBlobInput hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。 如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。 在本教學課程中，您可以指定 hello 檔案名稱的值。 

1. 指定名為 hello 命令 toovariable **cmd**。 

    ```PowerSHell   
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
hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 hello 輸出 SQL 資料表的資料集 (OututDataset) 您在此步驟中建立指定複製 hello hello 資料庫 toowhich hello 資料從 hello blob 儲存體中的資料表。

1. 指定名為 hello 命令 toovariable **cmd**。

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
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
在此步驟中，您會建立管線，其中含有使用 **AzureBlobInput** 作為輸入和使用 **AzureSqlOutput** 作為輸出的**複製活動**。

目前，輸出資料集是哪些磁碟機 hello 排程。 在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。 hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。 因此，hello 管線所產生的輸出資料集的 24 配量。 

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

**恭喜！** 您已成功建立 Azure data factory，，具有會將資料從 Azure Blob 儲存體 tooAzure SQL database 的管線。

## <a name="monitor-pipeline"></a>監視管線
在此步驟中，您可以使用 Data Factory REST API toomonitor 配量 hello 管線所產生。

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> 請確定 hello 開始和結束時間中指定下列的 hello 命令對 hello 開始和結束時間的 hello 管線。 

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

執行 hello Invoke-command 和 hello 下一個直到您看到中的扇區**準備**狀態或**失敗**狀態。 當 hello 配量處於就緒狀態時，請檢查 hello **emp**您 Azure SQL database 中的 hello 輸出資料的資料表。 

每個配量，兩個資料列的資料從 hello 原始程式檔是 hello Azure SQL database 中的複製的 toohello emp 資料表。 因此，所有的 hello 配量已成功處理 （處於就緒狀態） 時看到 24 hello emp 資料表中的新記錄。 

## <a name="summary"></a>摘要
在此教學課程中，您可以使用 REST API toocreate 從 Azure blob tooan Azure SQL database 的 Azure data factory toocopy 資料。 以下是您執行本教學課程中的 hello 高階步驟：  

1. 建立 Azure **Data Factory**。
2. 建立 **連結服務**：
   1. Azure 儲存體連結服務 toolink 您保留輸入的資料的 Azure 儲存體帳戶。     
   2. Azure SQL 連結服務 toolink hello 輸出資料會保存您 Azure SQL database。 
3. 建立可描述管線輸入資料和輸出資料的 **資料集**。
4. 建立具有複製活動的 **管線** ，以 BlobSource 做為來源並以 SqlSink 做為接收器。 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。
