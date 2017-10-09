---
title: "從內部部署 HDFS aaaMove 資料 |Microsoft 文件"
description: "深入了解如何 toomove 資料從內部部署 HDFS 使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>使用 Azure Data Factory 從內部部署的 HDFS 移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 HDFS 中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從 HDFS tooany 支援接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 資料處理站目前支援從內部部署 HDFS tooother 資料存放區，只有移動資料，但不適用於將資料從其他資料存放區 tooan 內部部署 HDFS。

> [!NOTE]
> 複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。 如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。 

## <a name="enabling-connectivity"></a>啟用連線
資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 HDFS。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。 使用 hello 閘道 tooconnect tooHDFS，即使它裝載於 Azure IaaS VM。

> [!NOTE]
> 請確定 hello 資料管理閘道器可以存取太**所有**hello [節點名稱伺服器]: [name] 節點的連接埠] 和 [資料節點的伺服器]: [資料節點連接埠] hello Hadoop 叢集。 預設 [名稱節點連接埠] 是 50070，而預設 [資料節點連接埠] 是 50075。

雖然您可以在 hello 上安裝閘道相同內部電腦或 hello Azure VM hello HDFS，我們建議您在個別機器/Azure IaaS VM 上安裝 hello 閘道。 在個別機器上安裝閘道器可減少資源爭用並改善效能。 當您在不同電腦上安裝 hello 閘道時，hello 部應該以 hello HDFS 無法 tooaccess hello 機器。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 HDFS 來源移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  使用 Data Factory 實體的 HDFS 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從內部部署 HDFS tooAzure Blob 複製](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob)本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooHDFS 的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
連結的服務連結資料儲存區 tooa data factory。 您建立連結的服務型別的**Hdfs** toolink 在內部部署 HDFS tooyour 資料處理站。 下表中的 hello 提供 JSON 項目特定 tooHDFS 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **Hdfs** |是 |
| Url |URL toohello HDFS |是 |
| authenticationType |匿名或 Windows。 <br><br> toouse **Kerberos 驗證**HDFS 連接器，請參閱太[本節](#use-kerberos-authentication-for-hdfs-connector)在內部部署環境 tooset 據此。 |是 |
| userName |Windows 驗證的使用者名稱。 |是 (適用於 Windows 驗證) |
| password |Windows 驗證的密碼。 |是 (適用於 Windows 驗證) |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello HDFS。 |是 |
| encryptedCredential |[新 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 存取認證的輸出。 |否 |

### <a name="using-anonymous-authentication"></a>使用匿名驗證

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>使用 Windows 驗證

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**FileShare** （包括 HDFS 資料集） 具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |路徑 toohello 資料夾。 範例： `myfolder`<br/><br/>使用逸出字元 '\' hello 字串中的特殊字元。 例如︰若為 folder\subfolder，請指定 folder\\\\subfolder；若為 d:\samplefolder，請指定 d:\\\\samplefolder。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>檔案名稱未指定輸出資料集，hello hello 產生檔案名稱會在 hello 遵循此格式： <br/><br/>Data<Guid>.txt (例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| partitionedBy |partitionedBy 可以是使用的 toospecify 動態 folderPath，時間序列資料的檔案名稱。 範例：folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

> [!NOTE]
> 無法同時使用檔名和 fileFilter。

### <a name="using-partionedby-property"></a>使用 partionedBy 屬性
當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。

toolearn 深入了解時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程及執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)文件。

#### <a name="sample-1"></a>範例 1：

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
在此範例與 hello 指定 hello 格式 (YYYYMMDDHH) 中的 Data Factory 系統變數 SliceStart 的值取代 {Slice}。 hello SliceStart 是指 toostart hello 配量時間。 hello folderPath 是不同的每個配量。 例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。

#### <a name="sample-2"></a>範例 2：

```JSON
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

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

複製活動時，來源是類型為**FileSystemSource** typeProperties 節中會使用下列屬性的 hello:

**FileSystemSource**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

## <a name="supported-file-and-compression-formats"></a>支援的檔案和壓縮格式
請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>JSON 範例： 將資料從內部部署 HDFS tooAzure Blob 複製
這個範例示範如何從 Blob 儲存體的內部部署 HDFS tooAzure toocopy 資料。 不過，資料可以複製**直接**hello 接收所述的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。  

hello 範例提供下列 Data Factory 實體的 hello 的 JSON 定義。 您可以使用這些定義 toocreate 管線 toocopy 資料從 HDFS tooAzure Blob 儲存體使用[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。

1. [OnPremisesHdfs](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從內部部署 HDFS tooan Azure blob 的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，設定 hello 資料管理閘道器。 hello hello 中的指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**HDFS 連結服務：**本例使用 hello Windows 驗證。 請參閱 [HDFS 連結服務](#linked-service-properties) 章節以了解您可以使用的各種不同類型的驗證。

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure 儲存體連結服務：**

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

**HDFS 的輸入資料集：**此資料集是指 toohello HDFS 資料夾 DataTransfer/支援 UnitTest /。 hello 管線會將所有的 hello 檔案複製此資料夾 toohello 目的地中。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**具有檔案系統來源和 Blob 接收器的管線中複製活動：**

hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>對 HDFS 連接器使用 Kerberos 驗證
以在 HDFS 連接器 toouse Kerberos 驗證有兩個選項 tooset hello 在內部部署環境。 您可以選擇其中一個 hello 更適合您的案例。
* 選項 1：[將閘道電腦加入 Kerberos 領域](#kerberos-join-realm)
* 選項 2：[啟用 Windows 網域和 Kerberos 領域之間的相互信任](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>選項 1：將閘道電腦加入 Kerberos 領域

#### <a name="requirement"></a>需求：

* hello 閘道電腦必須 toojoin hello Kerberos 領域，且無法再加入任何 Windows 網域。

#### <a name="how-tooconfigure"></a>如何 tooconfigure:

**在閘道電腦上︰**

1.  執行 hello **Ksetup**公用程式 tooconfigure hello Kerberos KDC 伺服器和領域。

    hello 機器必須設定為工作群組的成員，因為 Kerberos 領域是從 Windows 網域不同。 這可藉由設定 hello Kerberos 領域及新增 KDC 伺服器，如下所示。 視需要以您自己的個別領域取代 *REALM.COM*。

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **重新啟動**hello 機器後立即執行這些 2 命令。

2.  確認 hello 組態**Ksetup**命令。 hello 輸出應該類似：

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**在 Azure Data Factory 中：**

* 設定 hello HDFS 連接器使用**Windows 驗證**搭配 Kerberos 主體名稱和密碼 tooconnect toohello HDFS 資料來源。 檢查組態詳細資料上的 [HDFS 連結服務屬性](#linked-service-properties)區段。

### <a name="kerberos-mutual-trust"></a>選項 2：啟用 Windows 網域和 Kerberos 領域之間的相互信任

#### <a name="requirement"></a>需求：
*   hello 閘道電腦必須加入 Windows 網域。
*   您需要的權限 tooupdate hello 網域控制站的設定。

#### <a name="how-tooconfigure"></a>如何 tooconfigure:

> [!NOTE]
> 取代 REALM.COM 和 AD.COM hello 視下列教學課程使用您自己的個別領域和網域控制站中。

**在 KDC 伺服器上︰**

1.  編輯中的 hello KDC 組態**krb5.conf**檔案 toolet KDC 信任參考 toohello 遵循組態範本的 Windows 網域。 根據預設，hello 組態是位於**/etc/krb5.conf**。

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **重新啟動**hello KDC 服務組態之後。

2.  準備名為主體 **krbtgt/REALM.COM@AD.COM**  KDC 伺服器以 hello 下列命令：

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  在 **hadoop.security.auth_to_local** HDFS 服務組態檔中，新增 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`。

**在網域控制站上：**

1.  執行下列 hello **Ksetup**命令 tooadd 領域項目：

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  建立從 Windows 網域 tooKerberos 領域的信任關係。 [密碼] 是 hello 主體 hello 密碼 **krbtgt/REALM.COM@AD.COM** 。

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  選取 Kerberos 所使用的加密演算法。

    1. 移 tooServer 管理員 > 群組原則管理 > 網域 > 群組原則物件 > 預設使用中的網域原則或編輯。

    2. 在 hello**群組原則管理編輯器**快顯視窗中，移 tooComputer 組態 > 原則 > Windows 設定 > 安全性設定 > 本機原則 > 安全性選項和設定**網路安全性： 設定加密類型的 Kerberos 允許**。

    3. 您想要 toouse 選取 hello 加密演算法時連接 tooKDC。 通常，您只需選取所有 hello 選項。

        ![設定 Kerberos 的加密類型](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. 使用**Ksetup**命令 toospecify hello 加密演算法 toobe hello 上使用特定的領域。

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Hello 之間建立對應 hello 網域帳戶和 Kerberos 主體順序 toouse Kerberos 主體中的 Windows 網域中。

    1. 啟動 hello 系統管理工具 > **Active Directory 使用者和電腦**。

    2. 按一下 [檢視] > [進階功能] 來設定進階功能。

    3. 找出您想 toocreate 對應，以滑鼠右鍵按一下 tooview hello 帳戶 toowhich**名稱對應**> 按一下**Kerberos 名稱** 索引標籤。

    4. 將主體加入從 hello 領域。

        ![對應安全性身分識別](media/data-factory-hdfs-connector/map-security-identity.png)

**在閘道電腦上︰**

* 執行下列 hello **Ksetup**命令 tooadd 領域項目。

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**在 Azure Data Factory 中：**

* 設定 hello HDFS 連接器使用**Windows 驗證**連同您的網域帳戶或 Kerberos 主體 tooconnect toohello HDFS 資料來源。 檢查組態詳細資料上的 [HDFS 連結服務屬性](#linked-service-properties)區段。

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。


## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
