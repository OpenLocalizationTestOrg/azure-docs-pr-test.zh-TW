---
title: "從 FTP 伺服器使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 FTP 伺服器使用 Azure Data Factory toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>使用 Azure Data Factory 從 FTP 伺服器移動資料
本文說明如何 toouse hello 複製在 Azure Data Factory toomove 資料從 FTP 伺服器活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從 FTP 伺服器支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 Data Factory 目前支援僅從 FTP 伺服器 tooother 資料移動的資料存放區，但不是將資料從其他資料會儲存 tooan FTP 伺服器。 它支援內部部署和雲端 FTP 伺服器。

> [!NOTE]
> hello 複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。 如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 活動 hello 管線中。 

## <a name="enable-connectivity"></a>啟用連線能力
如果您要移動的資料**內部**FTP 伺服器 tooa 雲端資料儲存區 (例如，tooAzure Blob 儲存體)，安裝和使用資料管理閘道器。 hello 資料管理閘道是安裝在您的內部部署電腦的用戶端代理程式，並可讓雲端服務 tooconnect tooan 在內部部署資源。 如需詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)文章。 如需設定 hello 閘道和使用的逐步指示，請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。 即使 hello 伺服器做為服務 (IaaS) 虛擬機器 (VM) 位於 Azure 的基礎結構，您可以使用 hello 閘道 tooconnect tooan FTP 伺服器。

它也是可能 tooinstall hello 閘道上 hello 相同內部電腦或 IaaS VM hello FTP 伺服器。 不過，我們建議您安裝 hello 閘道，在不同的電腦或 IaaS VM tooavoid 資源爭用，以及更佳的效能。 當您在不同電腦上安裝 hello 閘道時，hello 部應該能夠 tooaccess hello FTP 伺服器。

## <a name="get-started"></a>開始使用
您可以藉由使用不同的工具 或 API，建立內含複製活動的管線，以便從 FTP 來源移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**資料 Factory 複製精靈**。 如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用工具或 Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。 如需使用 FTP 資料存放區中的使用的 toocopy 資料的 Data Factory 實體的 JSON 定義的範例，請參閱 hello [JSON 範例： 將資料從 FTP 伺服器 tooAzure blob 複製](#json-example-copy-data-from-ftp-server-to-azure-blob)本文一節。

> [!NOTE]
> 如需支援的檔案和壓縮格式 toouse 的詳細資訊，請參閱[Azure Data Factory 中的檔案及壓縮格式](data-factory-supported-file-and-compression-formats.md)。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooFTP 的 JSON 屬性的詳細資料。

## <a name="linked-service-properties"></a>連結服務屬性
hello 下表描述 JSON 項目特定 tooan FTP 連結服務。

| 屬性 | 說明 | 必要 | 預設值 |
| --- | --- | --- | --- |
| 類型 |設定此 tooFtpServer。 |是 |&nbsp; |
| 主機 |指定 hello 名稱或 IP 位址的 hello FTP 伺服器。 |是 |&nbsp; |
| authenticationType |指定 hello 的驗證類型。 |是 |基本或匿名 |
| username |指定具有存取 toohello FTP 伺服器 hello 使用者。 |否 |&nbsp; |
| password |指定 hello hello 使用者 （使用者名稱） 的密碼。 |否 |&nbsp; |
| encryptedCredential |指定加密的 hello 認證 tooaccess hello FTP 伺服器。 |否 |&nbsp; |
| gatewayName |指定資料管理閘道器 tooconnect tooan 內部 FTP 伺服器中的 hello hello 閘道名稱。 |否 |&nbsp; |
| 連接埠 |指定 hello 的 hello FTP 伺服器正在接聽的通訊埠。 |否 |21 |
| enableSsl |指定是否 toouse FTP over SSL/TLS 通道。 |否 |true |
| enableServerCertificateValidation |指定是否 tooenable 伺服器 SSL 憑證驗證，當您使用 FTP over SSL/TLS 通道。 |否 |true |

### <a name="use-anonymous-authentication"></a>使用匿名驗證

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>使用純文字的使用者名稱和密碼進行基本驗證

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>使用連接埠、enableSsl、enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>針對驗證和閘道器使用 encryptedCredential

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>資料集屬性
如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。

hello **typeProperties**區段是不同的資料集的每個型別。 它提供特定 toohello 資料集類型的資訊。 hello **typeProperties**類型的資料集區段**FileShare**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |子路徑 toohello 資料夾。 使用逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始和結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>當**fileName**未指定輸出資料集 hello hello 產生檔案名稱是以下列格式的 hello: <br/><br/>Data<Guid>.txt (範例：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |在 hello 中指定的檔案子集篩選使用 toobe tooselect **folderPath**，而非所有檔案。<br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1：`"fileFilter": "*.log"`<br/>範例 2：`"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter 適用於輸入 FileShare 資料集。 這個屬性不支援 Hadoop 分散式檔案系統 (HDFS)。 |否 |
| partitionedBy |使用動態 toospecify **folderPath**和**fileName**時間序列資料的。 例如，您可以指定每小時資料參數化的 **folderPath**。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)區段。 <br><br> 如果您想 toocopy 檔案，因為它們是以檔案為基礎的存放區 （二進位複製） 之間，略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：GZip、Deflate、BZip2 和 ZipDeflate，而支援的層級為：最佳和最快。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |
| useBinaryTransfer |指定是否 toouse hello 二進位傳輸模式。 hello 值會針對二進位模式 （這是 hello 預設值），則為 true 和 false 的 ASCII。 這個屬性只可用時 hello 相關聯的連結的服務類型的型別： FtpServer。 |否 |

> [!NOTE]
> 無法同時使用 fileName 和 fileFilter。

### <a name="use-hello-partionedby-property"></a>使用 hello partionedBy 屬性
如 hello 前一節中所述，您可以指定動態**folderPath**和**fileName**以 hello 時間序列資料的**partitionedBy**屬性。

toolearn 有關時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程與執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)。

#### <a name="sample-1"></a>範例 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
在此範例中，Data Factory 系統變數 SliceStart hello 值取代 {Slice} 是，在 hello 格式指定 (YYYYMMDDHH)。 hello SliceStart 是指 toostart hello 配量時間。 hello 資料夾路徑是不同的每個配量。 (例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。)

#### <a name="sample-2"></a>範例 2

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
在此範例中，hello 年、 月、 日和時間的 SliceStart 會擷取至不同的變數所使用的 hello **folderPath**和**fileName**屬性。

## <a name="copy-activity-properties"></a>複製活動屬性
如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

屬性用於 hello **typeProperties**區段 hello hello 上的活動，換句話說，每個活動類型而有所不同。 Hello 複製活動，根據 hello 類型的來源與接收 hello 類型屬性而有所不同。

複製活動中，當 hello 來源的類型為**FileSystemSource**，hello 下列屬性可用於**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>JSON 範例： 從 FTP 伺服器 tooAzure Blob 複製資料
這個範例示範如何從 FTP 伺服器 tooAzure Blob 儲存體 toocopy 資料。 不過，資料可以複製直接的 hello tooany 接收器中所述的 hello[支援資料存放區和格式](data-factory-data-movement-activities.md#supported-data-stores-and-formats)，使用 Data Factory 中的 hello 複製活動。  

hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* [FtpServer](#linked-service-properties) 類型的連結服務
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務
* [FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)
* 具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)

hello 範例將資料從 FTP 伺服器 tooan Azure blob 的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

### <a name="ftp-linked-service"></a>FTP 連結服務

這個範例會使用基本驗證，以 hello 使用者名稱和密碼以純文字。 您也可以使用下列方式 hello:

* 匿名驗證
* 基本驗證與加密認證
* 透過 SSL/TLS 的 FTP (FTPS)

請參閱 hello [FTP 連結服務](#linked-service-properties)不同類型的驗證，您可以使用的區段。

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務

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
### <a name="ftp-input-dataset"></a>FTP 輸入資料集

此資料集是指 toohello FTP 資料夾`mysharedfolder`和檔案`test.csv`。 hello 管線複製 hello 檔案 toohello 目的地。

設定**外部**太**true**該 hello 資料集是外部 toohello 資料處理站，並不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估，依據 hello 正在處理的 hello 配量的開始時間。 hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>具有檔案系統來源和 blob 接收器的管線中複製活動

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和 hello**接收**類型設定得**BlobSink**。

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
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
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="next-steps"></a>後續步驟
請參閱下列文章 hello:

* 關於金鑰 toolearn 因素影響效能的 Data Factory 中的資料移動 （複製活動） 和各種方式 toooptimize 的請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。

* 複製活動與建立管線的逐步指示，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
