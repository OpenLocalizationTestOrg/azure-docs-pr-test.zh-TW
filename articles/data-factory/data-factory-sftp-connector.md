---
title: "從 SFTP 伺服器使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署或雲端 SFTP 伺服器使用 Azure Data Factory toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>使用 Azure Data Factory 從 SFTP 伺服器移動資料
本文概述如何在 Azure Data Factory toomove 資料從內部部署/雲端上的 SFTP 伺服器 tooa toouse hello 複製活動支援接收資料存放區。 這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。

資料處理站目前只支援移動資料從 SFTP 伺服器 tooother 資料存放區，但對於 tooan SFTP 伺服器會將資料從其他資料儲存。 它支援內部部署和雲端 SFTP 伺服器。

> [!NOTE]
> 複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。 如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。 

## <a name="supported-scenarios-and-authentication-types"></a>支援的案例和驗證類型
您可以使用此 SFTP 連接器 toocopy 資料從**這兩種雲端 SFTP 伺服器和內部部署 SFTP 伺服器**。 **基本**和**SshPublicKey** toohello SFTP 伺服器連線時支援驗證類型。

複製資料時從 SFTP 伺服器在內部部署，您需要在 hello 在內部部署環境/Azure VM 中安裝資料管理閘道器。 請參閱[資料管理閘道器](data-factory-data-management-gateway.md)如 hello 閘道的詳細資訊。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文件以取得逐步指示設定 hello 閘道並使用它。

## <a name="getting-started"></a>開始使用
您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 SFTP 來源。

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 如 JSON 範例 toocopy 從 SFTP 伺服器 tooAzure Blob 儲存體的資料，請參閱 < [JSON 範例： 將資料從 SFTP 伺服器 tooAzure blob 複製](#json-example-copy-data-from-sftp-server-to-azure-blob)本文一節。

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooFTP 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| 類型 | hello type 屬性必須設定得`Sftp`。 |是 |
| 主機 | Hello SFTP 伺服器的名稱或 IP 位址。 |是 |
| 連接埠 |哪些 hello SFTP 伺服器正在接聽連接埠。 hello 預設值是： 21 |否 |
| authenticationType |指定驗證類型。 允許的值︰**Basic**、**SshPublicKey**。 <br><br> 請參閱太[使用基本驗證](#using-basic-authentication)和[使用 SSH 公開金鑰驗證](#using-ssh-public-key-authentication)分別區段上多個屬性和 JSON 範例。 |是 |
| skipHostKeyValidation | 指定是否 tooskip 主機金鑰的驗證。 | 否。 hello 預設值： false |
| hostKeyFingerprint | 指定 hello 指紋 hello 主索引鍵。 | 是如果 hello `skipHostKeyValidation` toofalse 設定。  |
| gatewayName |名稱的 hello 資料管理閘道器 tooconnect tooan 內部 SFTP 伺服器。 | 如果從內部部署 SFTP 伺服器複製資料，則為 [是]。 |
| encryptedCredential | 加密的認證 tooaccess hello SFTP 伺服器。 自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊中指定基本驗證 （使用者名稱 + 密碼） 或 SshPublicKey 驗證 （使用者名稱 + 私用金鑰的路徑或內容） 時。 | 否。 僅當從內部部署 SFTP 伺服器複製資料時才套用。 |

### <a name="using-basic-authentication"></a>使用基本驗證

toouse 基本驗證時，設定`authenticationType`為`Basic`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| username | 具有存取 toohello SFTP 伺服器的使用者。 |是 |
| password | Hello 使用者 （使用者名稱） 的密碼。 | 是 |

#### <a name="example-basic-authentication"></a>範例：基本驗證
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>範例：採用加密認證的基本驗證

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>使用 SSH 公用金鑰驗證

toouse SSH 公開金鑰驗證、 設定`authenticationType`為`SshPublicKey`，並指定下列屬性，除了 hello SFTP 連接器 hello 最後一節中導入的泛型的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- | --- |
| username |使用者具有存取 toohello SFTP 伺服器 |是 |
| privateKeyPath | 指定絕對路徑 toohello 私密金鑰檔案可以存取該閘道。 | 指定任一個 hello`privateKeyPath`或`privateKeyContent`。 <br><br> 僅當從內部部署 SFTP 伺服器複製資料時才套用。 |
| privateKeyContent | Hello 私用的索引鍵內容的序列化的字串。 hello 複製精靈可以讀取 hello 私密金鑰檔案，並自動擷取 hello 私用的索引鍵內容。 如果您使用任何其他工具/SDK，請改為使用 hello privateKeyPath 屬性。 | 指定任一個 hello`privateKeyPath`或`privateKeyContent`。 |
| passPhrase | 指定 hello 傳遞片語/密碼 toodecrypt hello 私密金鑰如果 hello 金鑰檔受複雜密碼。 | [是] 如果 hello 私密金鑰檔案受複雜密碼。 |

> [!NOTE]
> SFTP 連接器僅支援 OpenSSH 金鑰。 請確定您的金鑰檔 hello 正確的格式。 您可以使用 Putty 工具 tooconvert 從.ppk tooOpenSSH 格式。

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>範例︰使用私密金鑰 filePath 的 SshPublicKey 驗證

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>範例︰使用私密金鑰內容的 SshPublicKey 驗證

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。

hello **typeProperties**區段是不同的資料集的每個型別。 它提供特定 toohello 資料集類型的資訊。 hello typeProperties 區段類型的資料集**FileShare**資料集具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |子路徑 toohello 資料夾。 使用逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式： <br/><br/>Data.<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。<br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1：`"fileFilter": "*.log"`<br/>範例 2：`"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter 適用於輸入 FileShare 資料集。 這個屬性不支援使用 HDFS。 |否 |
| partitionedBy |partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |
| useBinaryTransfer |指定是否使用二進位傳輸模式。 二進位模式為 true，ASCII 則為 false。 預設值：True。 只有在相關聯的連結服務類型的類型為 FtpServer 時，才可以使用這個屬性。 |否 |

> [!NOTE]
> 無法同時使用檔名和 fileFilter。

### <a name="using-partionedby-property"></a>使用 partionedBy 屬性
如 hello 前一節中所述，您可以指定動態 folderPath，與 partitionedBy 時間序列資料的檔案名稱。 您可以使用 hello Data Factory 巨集和 hello 系統變數 SliceStart，顯示 hello 給定的資料配量的邏輯時間期間的 SliceEnd。

toolearn 有關時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程及執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)文件。

#### <a name="sample-1"></a>範例 1：

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
在此範例與 hello 指定 hello 格式 (YYYYMMDDHH) 中的 Data Factory 系統變數 SliceStart 的值取代 {Slice}。 hello SliceStart 是指 toostart hello 配量時間。 hello folderPath 是不同的每個配量。 範例：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。

#### <a name="sample-2"></a>範例 2：

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動，根據 hello 類型的來源與接收 hello 類型屬性而有所不同。

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>支援的檔案和壓縮格式
請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>JSON 範例： 從 SFTP 伺服器 tooAzure blob 複製資料
hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何 toocopy 資料從 SFTP 來源 tooAzure Blob 儲存體。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

> [!IMPORTANT]
> 此範例提供 JSON 程式碼片段。 它不包含建立 hello 資料處理站的逐步指示。 如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

hello 範例具有下列資料 factory 實體的 hello:

* [sftp](#linked-service-properties) 類型的已連結服務。
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從 Azure blob 的 SFTP 伺服器 tooan 每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**SFTP 連結服務**

這個範例會使用 hello 基本驗證的使用者名稱和密碼以純文字。 您也可以使用下列方式 hello:

* 基本驗證與加密認證
* SSH 公用金鑰驗證

請參閱 [FTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Azure 儲存體連結服務**

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
**SFTP 輸入資料集**

此資料集是指 toohello SFTP 資料夾`mysharedfolder`和檔案`test.csv`。 hello 管線複製 hello 檔案 toohello 目的地。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Blob 輸出資料集**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**具有複製活動的管線**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**和**接收**類型設定得**BlobSink**。

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。

## <a name="next-steps"></a>後續步驟
請參閱下列文章 hello:

* [複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。
