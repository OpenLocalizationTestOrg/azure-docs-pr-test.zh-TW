---
title: "使用複製活動 aaaMove 資料 |Microsoft 文件"
description: "了解 Data Factory 管線中的資料移動︰雲端存放區之間和內部部署與雲端之間的資料移轉。 使用「複製活動」。"
keywords: "複製資料, 資料移動, 資料移轉, 傳輸資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>使用複製活動來移動資料
## <a name="overview"></a>概觀
在 Azure Data Factory，您可以使用複製活動 toocopy 資料在內部部署和雲端之間的資料存放區。 複製 hello 資料之後，它可以進一步轉換及分析。 您也可以使用複製活動 toopublish 轉換和分析結果的商業智慧 (BI) 和應用程式使用。

![複製活動的角色](media/data-factory-data-movement-activities/copy-activity.png)

「複製活動」是由安全、可靠、可調整且 [全域可用的服務](#global)提供技術支援。 本文提供關於在 Data Factory 和複製活動中移動資料的詳細資訊。

首先，讓我們看看在兩個雲端資料存放區之間，以及在內部部署資料存放區與雲端資料存放區之間，如何進行資料移轉。

> [!NOTE]
> 一般情況下，請參閱有關活動 toolearn[了解管線和活動](data-factory-create-pipelines.md)。
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>在兩個雲端資料存放區之間複製資料
Hello 雲端來源和接收的資料存放區時，複製活動會經歷下列階段 toocopy 資料從 hello 來源 toohello 接收 hello。 hello 力量複製活動的服務：

1. 從 hello 來源資料存放區讀取資料。
2. 執行序列化/還原序列化、壓縮/解壓縮、資料行對應及類型轉換。 它會根據 hello 輸入資料集、 輸出資料集，以及複製活動的 hello 設定這些作業。
3. 寫入資料 toohello 目的地資料存放區。

hello 服務會自動選擇 hello 最佳區域 tooperform hello 資料移動。 此區域通常是 hello 一個最接近 toohello 接收資料存放區。

![從雲端複製到雲端](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>在內部部署資料存放區和雲端資料存放區之間複製資料
toosecurely 移動資料的內部部署資料存放區之間的雲端資料存放區中，您在內部部署的電腦上安裝資料管理閘道器。 「資料管理閘道」是一個能夠啟用混合式資料移動及處理的代理程式。 您可以安裝在相同機器 hello 資料存放區本身，因為 hello 或具有存取 toohello 資料儲存在不同電腦上。

在此案例中，資料管理閘道器會執行 hello 序列化/還原序列化、 壓縮/解壓縮、 資料行對應，及類型轉換。 資料不會流過 hello Azure Data Factory 服務透過。 相反地，資料管理閘道器會直接寫入 hello 資料 toohello 目的地存放區。

![從內部部署複製到雲端](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

如需簡介和逐步解說，請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。 如需有關此代理程式的詳細資訊，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 。

您也可以將資料從 / toosupported 資料存放區，使用資料管理閘道器裝載在 Azure IaaS 虛擬機器 (Vm) 上。 在此情況下，您可以在安裝資料管理閘道器 hello hello 資料存放區本身，或具有存取 toohello 資料儲存在個別 VM 上的相同的 VM。

## <a name="supported-data-stores-and-formats"></a>支援的資料存放區和格式
Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。 Data Factory 支援下列資料存放區的 hello。 從任何來源的資料可以寫入 tooany 接收。 按一下 資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。

> [!NOTE] 
> 如果您需要 toomove 資料複製活動不支援的資料存放區中，使用**自訂活動**您自己的邏輯複製/移動資料的 Data Factory 中。 如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 資料存放區使用 * 可在內部部署或 Azure IaaS 上，因此需要您 tooinstall[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署/Azure IaaS 電腦上。

### <a name="supported-file-formats"></a>支援的檔案格式
您也可以使用複製活動**複製檔做為-是**之間以檔案為基礎的兩個資料存放區，您可以略過 hello[格式化區段](data-factory-create-datasets.md)在 hello 輸入和輸出資料集定義。 hello 資料有效率地複製不含任何序列化/還原序列化。

複製活動也會讀取和寫入 toofiles 中指定的格式： **Text、 JSON、 Avro、 ORC 及 Parquet**，並壓縮轉碼器**GZip、 Deflate、 BZip2 和 ZipDeflate**支援。 如需詳細資訊，請參閱[支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。

例如，您可以執行 hello 下列複製的活動：

* 複製資料在內部部署 SQL Server 中，將 ORC 格式寫入 tooAzure 資料湖存放區。
* 將檔案從內部部署檔案系統複製文字 (CSV) 格式，並將 tooAzure Blob 寫入 Avro 格式。
* 從內部部署檔案系統複製 zip 的檔案解壓縮，然後登陸 tooAzure 資料湖存放區。
* 將資料從 Azure Blob 複製 GZip 壓縮的文字 (CSV) 格式，並將寫入 tooAzure SQL 資料庫。

## <a name="global"></a>全域可用的資料移動
Azure Data Factory 提供了只 hello 美國西部、 美國東部、 和北歐區域。 不過，可提供複製活動的 hello 服務位於全域 hello 下列區域和地理位置。 hello 全域可用的拓撲可確保通常可以避免跨地區躍點的高效率的資料移動。 如需了解某區域中是否有 Data Factory 和「資料移動」可供使用，請參閱 [依區域提供的服務](https://azure.microsoft.com/regions/#services) 。

### <a name="copy-data-between-cloud-data-stores"></a>在雲端資料存放區之間複製資料
Data Factory hello 雲端來源和接收的資料存放區時，會將服務部署使用 hello 中最接近的 toohello 接收 hello 區域中相同的地理位置 toomove hello 資料。 請參閱下表針對對應的 toohello:

| 地理位置的 hello 目的地資料存放區 | Hello 目的地資料存放區的區域 | 用於資料移動的區域 |
|:--- |:--- |:--- |
| 美國 | 美國東部 | 美國東部 |
| &nbsp; | 美國東部 2 | 美國東部 2 |
| &nbsp; | 美國中部 | 美國中部 |
| &nbsp; | 美國中北部 | 美國中北部 |
| &nbsp; | 美國中南部 | 美國中南部 |
| &nbsp; | 美國中西部 | 美國中西部 |
| &nbsp; | 美國西部 | 美國西部 |
| &nbsp; | 美國西部 2 | 美國西部 |
| 加拿大 | 加拿大東部 | 加拿大中部 |
| &nbsp; | 加拿大中部 | 加拿大中部 |
| 巴西 | 巴西南部 | 巴西南部 |
| 歐洲 | 北歐 | 北歐 |
| &nbsp; | 西歐 | 西歐 |
| 英國 | 英國西部 | 英國南部 |
| &nbsp; | 英國南部 | 英國南部 |
| 亞太地區 | 東南亞 | 東南亞 |
| &nbsp; | 東亞 | 東南亞 |
| 澳大利亞 | 澳洲東部 | 澳洲東部 |
| &nbsp; | 澳大利亞東南部 | 澳大利亞東南部 |
| 日本 | 日本東部 | 日本東部 |
| &nbsp; | 日本西部 | 日本東部 |
| 印度 | 印度中部 | 印度中部 |
| &nbsp; | 印度西部 | 印度中部 |
| &nbsp; | 印度南部 | 印度中部 |

或者，您可以明確指出的 Data Factory 服務 toobe hello 區域中，藉由指定使用 tooperform hello 複製`executionLocation`下複製活動的屬性`typeProperties`。 這個屬性支援的值詳列於上述**用於資料移動的區域**資料行。 請注意您的資料會通過該區域網路上 hello 傳輸進行複製時。 例如 toocopy Azure 之間會儲存在韓國，您可以指定`"executionLocation": "Japan East"`tooroute 透過日本地區 (請參閱[範例 JSON](#by-using-json-scripts)做為參考)。

> [!NOTE]
> 如果 hello 目的地資料存放區的 hello 區域不在上述清單中或無法偵測預設複製活動失敗而不是透過替代地區中，除非`executionLocation`指定。 經過一段時間，將會展開 hello 支援區域清單。
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>在內部部署資料存放區和雲端資料存放區之間複製資料
在內部部署存放區 (或 Azure 虛擬機器/IaaS) 與雲端存放區之間複製資料時， [資料管理閘道](data-factory-data-management-gateway.md) 會在內部部署機器或虛擬機器上執行資料移動。 hello 資料不流經 hello 服務在 hello 雲端中，除非您使用 hello[分段複製](data-factory-copy-activity-performance.md#staged-copy)功能。 在此情況下，資料流經 hello 寫入 hello 接收資料存放區之前，請執行 Azure Blob 儲存體。

## <a name="create-a-pipeline-with-copy-activity"></a>建立具有複製活動的管線
您可以使用幾個方式來建立具有「複製活動」的管線︰

### <a name="by-using-hello-copy-wizard"></a>使用 hello 複製精靈
hello 資料 Factory 複製精靈可協助您 toocreate 具有複製活動的管線。 這個管線可讓您從支援的來源 toodestinations toocopy 資料*而不需要撰寫 JSON*定義連結的服務、 資料集和管線。 請參閱[資料 Factory 複製精靈](data-factory-copy-wizard.md)hello 精靈的詳細資料。  

### <a name="by-using-json-scripts"></a>透過使用 JSON 指令碼
您可以使用 Data Factory 編輯器 hello Azure 入口網站、 Visual Studio 中或 Azure PowerShell toocreate JSON 定義中的管線 （透過使用複製活動）。 然後，您可以部署 toocreate Data Factory 中的 hello 管線。 如需含有逐步指示的教學課程，請參閱 [教學課程：在 Azure Data Factory 管線中使用複製活動](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 。    

JSON 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。 屬性可用在 hello `typeProperties` hello 活動的區段會隨每個活動類型。

複製活動 hello`typeProperties`區段有所不同 hello 類型的來源和接收。 按一下來源/接收器中 hello[支援來源與接收](#supported-data-stores-and-formats)區段 toolearn 有關針對該資料存放區的複製活動支援的型別屬性。

以下是範例 JSON 定義︰

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
hello 排程 hello 中定義的輸出資料集可讓您判斷 hello 活動執行時 (例如：**每日**，頻率，做為**天**，以及做為間隔**1**)。 hello 活動會將資料從輸入資料集 (**來源**) tooan 輸出資料集 (**接收**)。

您可以指定多個輸入資料集 tooCopy 活動。 Hello 活動開始執行前，它們是使用的 tooverify hello 相依性。 不過，只有 hello 從 hello 第一個資料集的資料是複製的 toohello 目的地資料集。 如需詳細資訊，請參閱 [排程和執行](data-factory-scheduling-and-execution.md)。  

## <a name="performance-and-tuning"></a>效能和微調
請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)，其中描述 Azure Data Factory 中的資料移動 （複製活動） 的 hello 效能影響的關鍵因素。 它也列出 hello 觀察到在內部測試期間的效能，並討論各種方式 toooptimize hello 複製活動的效能。

## <a name="fault-tolerance"></a>容錯
根據預設，複製活動將會停止複製資料以及傳回失敗時遇到不相容的資料來源與接收器; 之間雖然您可以明確地設定 tooskip 和記錄檔 hello 不相容的資料列只複製這些相容的資料 toomake hello 複製成功。 請參閱 hello[複製活動容錯](data-factory-copy-activity-fault-tolerance.md)上更多詳細資料。

## <a name="security-considerations"></a>安全性考量
請參閱 hello[安全性考量](data-factory-data-movement-security-considerations.md)，其中描述 Azure Data Factory 中的資料移動服務使用 toosecure 您資料的安全性基礎結構。

## <a name="scheduling-and-sequential-copy"></a>排程和循序複製
請參閱 [排程和執行](data-factory-scheduling-and-execution.md) ，以取得排程和執行在 Data Factory 中如何運作的詳細資訊。 它是可能 toorun 多項複製作業逐一循序/排序的方式。 請參閱 hello[循序複製](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)> 一節。

## <a name="type-conversions"></a>類型轉換
不同的資料存放區有不同的原生類型系統。 複製活動與 hello 下列兩種方法執行從來源類型 toosink 類型的自動類型轉換：

1. 從原生的來源類型 tooa.NET 型別轉換。
2. 從.NET 型別 tooa 原生接收類型轉換。

從資料存放區的原生型別系統 tooa.NET 型別 hello 對應是 hello 各自的資料存放區文件中。 (按一下 hello 特定連結在 hello[支援資料存放區](#supported-data-stores)資料表)。 以便複製活動會執行 hello 右邊轉換，您可以建立您的資料表時使用這些對應 toodetermine 適當類型。

## <a name="next-steps"></a>後續步驟
* toolearn 有關 hello 複製活動，請參閱[將資料從 Azure Blob 儲存體 tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
* toolearn 有關將資料從內部部署資料存放區 tooa 雲端資料儲存區，請參閱[將資料從內部部署 toocloud 資料存放區移](data-factory-move-data-between-onprem-and-cloud.md)。
