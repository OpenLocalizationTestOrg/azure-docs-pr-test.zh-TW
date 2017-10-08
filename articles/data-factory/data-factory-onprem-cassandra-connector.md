---
title: "使用 Data Factory Cassandra aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署 Cassandra toomove 資料資料庫使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>使用 Azure Data Factory 從內部部署的 Cassandra 資料庫移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Cassandra 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從內部部署 Cassandra 資料存放區支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 目前資料處理站都會支援只移動資料的 Cassandra 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooa Cassandra 資料存放區。 

## <a name="supported-versions"></a>支援的版本
hello Cassandra 連接器支援下列版本的 Cassandra hello: 2.X。

## <a name="prerequisites"></a>必要條件
Hello Azure Data Factory 服務 toobe 無法 tooconnect tooyour 內部 Cassandra 資料庫中，您必須安裝資料管理閘道器上 hello 相同機器該主機 hello 資料庫或不同的機器 tooavoid 競用資源以 hello資料庫。 資料管理閘道器是安全、 受管理的方式連接到內部部署資料來源 toocloud 服務。 如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。 請參閱[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得有關設定 hello 閘道資料管線 toomove 資料的逐步指示。

即使 hello 資料庫裝載於 hello 雲端，例如，在 Azure IaaS VM 上，您必須使用 hello 閘道 tooconnect tooa Cassandra 資料庫。 您可以在擁有 hello 閘道的 Y hello 相同的 VM 主機 hello 資料庫或個別 VM 只要 hello 閘道上可以連接 toohello 資料庫。  

當您安裝 hello 閘道時，它會自動安裝 Microsoft Cassandra ODBC 驅動程式使用 tooconnect tooCassandra 資料庫。 因此，您不需要 toomanually hello 閘道機器上安裝任何驅動程式從 hello Cassandra 資料庫複製資料。 

> [!NOTE]
> 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。 

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。 
- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從內部部署 Cassandra 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Cassandra tooAzure Blob 複製](#json-example-copy-data-from-cassandra-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Cassandra 資料存放區的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooCassandra 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesCassandra** |是 |
| 主機 |一或多個 Cassandra 伺服器 IP 位址或主機名稱。<br/><br/>同時指定以逗號分隔的 IP 位址或主機名稱 tooconnect tooall 伺服器清單。 |是 |
| 連接埠 |hello hello Cassandra 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。 |否，預設值：9042 |
| authenticationType |基本或匿名 |是 |
| username |指定 hello 使用者帳戶的使用者名稱。 |是，如果設定 tooBasic authenticationType。 |
| password |指定 hello 使用者帳戶的密碼。 |是，如果設定 tooBasic authenticationType。 |
| gatewayName |hello hello 閘道所使用的 tooconnect toohello 內部 Cassandra 資料庫名稱。 |是 |
| encryptedCredential |加密的 hello 閘道的認證。 |否 |

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**CassandraTable**具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| keyspace |Hello keyspace 或 Cassandra 資料庫中的結構描述的名稱。 |是 (如果未定義 **CassandraSource** 的**查詢**)。 |
| tableName |Cassandra 資料庫中的 hello 資料表的名稱。 |是 (如果未定義 **CassandraSource** 的**查詢**)。 |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

當來源屬於型別**CassandraSource**，typeProperties 節中會使用下列屬性的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢或 CQL 查詢。 請參閱 [CQL 參考資料](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)。 <br/><br/>當使用 SQL 查詢，指定**keyspace name.table 名稱**想 tooquery toorepresent hello 資料表。 |否 (如果已定義資料集上的 tableName 和 keyspace)。 |
| consistencyLevel |hello 一致性層級指定幾個複本必須回應 tooa 讀取的要求傳回資料 toohello 用戶端應用程式之前。 Cassandra 檢查 hello 複本的指定的數目的資料 toosatisfy hello 讀取的要求。 |ONE、TWO、THREE、QUORUM、ALL、LOCAL_QUORUM、EACH_QUORUM、LOCAL_ONE。 如需詳細資訊，請參閱 [設定資料一致性](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 。 |否。 預設值為 ONE。 |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>JSON 範例： 從 Cassandra tooAzure Blob 複製資料
此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它會顯示如何從內部部署 Cassandra toocopy 資料資料庫 tooan Azure Blob 儲存體。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

> [!IMPORTANT]
> 此範例提供 JSON 程式碼片段。 它不包含建立 hello 資料處理站的逐步指示。 如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

hello 範例具有下列資料 factory 實體的 hello:

* [OnPremisesCassandra](#linked-service-properties)類型的連結服務。
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [CassandraTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [CassandraSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

**Cassandra 已連結的服務：**

這個範例會使用 hello **Cassandra**連結服務。 請參閱[Cassandra 連結服務](#linked-service-properties)支援這項連結服務的 hello 屬性區段。  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure 儲存體連結服務：**

```json
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

**Cassandra 輸入資料集：**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**具有 Cassandra 來源和 Blob 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**CassandraSource**和**接收**類型設定得**BlobSink**。

請參閱[RelationalSource 類型屬性](#copy-activity-properties)hello hello RelationalSource 支援之屬性的清單。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]    
    }
}
```

### <a name="type-mapping-for-cassandra"></a>Cassandra 的類型對應
| Cassandra 類型 | 以 .Net 為基礎的類型 |
| --- | --- |
| ASCII |String |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |單一 |
| INET |String |
| INT |Int32 |
| TEXT |String |
| 時間戳記 |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |String |
| VARINT |十進位 |

> [!NOTE]
> 集合型別 （地圖、 設定、 清單、 等等），請參閱太[使用 Cassandra 集合類型使用的虛擬資料表](#work-with-collections-using-virtual-table)> 一節。
>
> 不支援使用者定義的類型。
>
> hello 長度的 Binary 資料行和字串資料行的長度不能大於 4000。
>
>

## <a name="work-with-collections-using-virtual-table"></a>使用虛擬資料表處理集合
Azure Data Factory 會使用內建 ODBC 驅動程式 tooconnect tooand 複製的資料從 Cassandra 資料庫。 包括地圖、 集合和清單的集合類型，hello 驅動程式會重新 hello 資料正規化成對應的虛擬資料表。 具體來說，如果資料表包含集合中的任何資料行，hello 驅動程式會產生下列虛擬資料表中的 hello:

* A**基底資料表**，其中包含 hello 與 hello hello 集合的資料行除外真正的資料表相同的資料。 hello 基底資料表使用名稱相同的 hello 為 hello 它所代表的實際資料表。
* A**虛擬資料表**針對每個集合的資料行，這樣會將巢狀的 hello 資料。 代表集合的 hello 虛擬資料表使用 hello 真正的資料表，來區隔 hello 名稱來命名"*vt*」 以及 hello hello 資料行名稱。

虛擬資料表，請參閱 toohello hello 真正的資料表中的資料，啟用 hello 驅動程式 tooaccess hello 非正規化的資料。 如需詳細資訊，請參閱＜範例＞一節。 您可以存取 Cassandra 集合 hello 的內容查詢及聯結 hello 虛擬資料表。

您可以使用 hello[複製精靈](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity)toointuitively 檢視 hello Cassandra 資料庫包括 hello 虛擬資料表中的資料表清單，並預覽 hello 內的資料。 您也可以建構 hello 複製精靈中的查詢，並驗證 toosee hello 結果。

### <a name="example"></a>範例
例如，hello 下列"ExampleTable 」 是 Cassandra 資料庫資料表，其中包含名為"pk_int 」、 名為值的文字資料行、 清單資料行，對應資料行和集資料行 （名為"StringSet 」） 整數主索引鍵資料行。

| pk_int | 值 | 列出 | 對應 | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"sample value 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"sample value 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

hello 驅動程式會產生多個虛擬資料表 toorepresent 這個單一資料表。 hello hello 虛擬資料表中的外部索引鍵資料行參考 hello 主索引鍵資料行中 hello 真正的資料表，並指出哪些真實資料表資料列 hello 虛擬資料表資料列對應至。

hello 的第一個虛擬資料表是 hello 下表會顯示名為"ExampleTable"hello 基底資料表。 hello 基底資料表包含 hello 與 hello 原始資料庫的資料表除外 hello 集合，也就是省略這個資料表中，然後其他虛擬資料表中，展開節點相同的資料。

| pk_int | 值 |
| --- | --- |
| 1 |"sample value 1" |
| 3 |"sample value 3" |

hello 下列表格顯示 hello renormalize hello hello 清單、 地圖和 StringSet 資料行資料的虛擬資料表。 名稱結尾是"_index"或"（_k） 」 的 hello 資料行會指出 hello hello 原始清單或地圖中的 hello 資料位置。 名稱結尾是"_value"hello 資料行包含 hello 展開資料 hello 集合。

#### <a name="table-exampletablevtlist"></a>資料表「ExampleTable_vt_List」：
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>資料表「ExampleTable_vt_Map」：
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |具有使用  |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>資料表「ExampleTable_vt_StringSet」：
| pk_int | StringSet_value |
| --- | --- |
| 1 |具有使用  |
| 1 |b |
| 1 |C |
| 3 |具有使用  |
| 3 |E |

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
