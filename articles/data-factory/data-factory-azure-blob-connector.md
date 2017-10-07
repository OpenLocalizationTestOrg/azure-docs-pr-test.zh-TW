---
title: "aaaCopy 資料至 azure 或從 Azure Blob 儲存體 |Microsoft 文件"
description: "了解如何 toocopy blob 在 Azure Data Factory 中的資料。 使用我們的範例： 如何從 Azure Blob 儲存體和 Azure SQL Database toocopy 資料 tooand。"
keywords: "blob 資料, azure blob 複製"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>從 Azure Blob 儲存體，使用 Azure Data Factory 複製資料 tooor
本文說明如何 toouse hello Azure Data Factory toocopy 資料 tooand 從 Azure Blob 儲存體中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

## <a name="overview"></a>概觀
您可以從任何支援的來源資料儲存 tooAzure Blob 儲存體，或從 Azure Blob 儲存體支援 tooany 接收資料存放區來複製資料。 hello 下表提供一份資料存放區支援做為來源或接收 hello 複製活動。 例如，您可以將資料**從** SQL Server 資料庫或 Azure SQL Database 移**到** Azure Blob 儲存體。 而且，您可以將資料「從」 Azure Blob 儲存體複製「到」 Azure SQL 資料倉儲或 Azure Cosmos DB 集合。 

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 Azure Blob 儲存體**toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooAzure Blob 儲存體**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> 複製活動支援複製資料的 / tooboth 一般用途的 Azure 儲存體帳戶和熱/冷卻 Blob 儲存體。 hello 活動支援**讀取區塊、 附加、 或分頁 blob**，但支援**撰寫 tooonly 區塊 blob**。 不支援使用「Azure 進階儲存體」作為接收器，因為它是以分頁 Blob 為後盾。
> 
> 複製活動不會刪除資料來源 hello hello 資料已順利複製 toohello 目的地之後。 如果您需要 toodelete 來源資料複製成功之後，建立[自訂活動](data-factory-use-custom-activities.md)toodelete hello 資料，並使用 hello 管線中的 hello 活動。 如需範例，請參閱 hello [GitHub 上的刪除 blob 或資料夾範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)。 

## <a name="get-started"></a>開始使用
您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出 Azure Blob 儲存體。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 此發行項[逐步解說](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage)建立管線 toocopy 資料從 Azure Blob 儲存體位置 tooanother Azure Blob 儲存體位置。 如需建立管線 toocopy 資料從 Azure Blob 儲存體 tooAzure SQL Database 的教學課程，請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體 tooan Azure SQL database 中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 對於屬於特定 tooAzure Blob 儲存體連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。 
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。 而且，您保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL database 中建立另一個資料集 toospecify hello SQL 資料表。 如為特定 tooAzure Blob 儲存體的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 BlobSource 作為來源與 SqlSink 做為接收器 hello 複製活動。 同樣地，如果您要複製 Azure SQL Database tooAzure Blob 儲存體，您使用 SqlSource 和 BlobSink hello 複製活動中。 特定 tooAzure Blob 儲存體複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。  

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料至 azure 或從 Azure Blob 儲存體的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-blob-storage  )本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure Blob 儲存體的 JSON 屬性的詳細資料。

## <a name="linked-service-properties"></a>連結服務屬性
有兩種類型的連結服務中，您可以使用 toolink Azure 儲存體 tooan Azure data factory。 它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。 hello Azure 儲存體連結服務提供 hello 與全域存取 toohello Azure 儲存體的資料處理站。 而 hello Azure 儲存體 SAS （共用存取簽章） 連結的限制/時間繫結存取 toohello Azure 儲存體的 hello data factory 提供服務。 這兩個連結服務之間沒有其他差異。 選擇符合您需求的 hello 連結服務。 hello 下列各節提供更多詳細資料這兩個連結的服務。

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>資料集屬性
資料集 toorepresent toospecify Azure Blob 儲存體中的輸入或輸出資料，設定 hello hello 資料集的類型屬性： **AzureBlob**。 設定 hello **linkedServiceName**連結服務的 hello Azure 儲存體或 Azure 儲存體 SAS hello 資料集 toohello 名稱的內容。  hello hello 資料集的類型屬性指定 hello **blob 容器**和 hello**資料夾**hello blob 儲存體中。

如 JSON 區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

資料處理站都會支援下列基礎符合 CLS 標準的.NET 型別值提供 「 結構 」 的結構描述上讀取資料來源類似 Azure blob 中的類型資訊的 hello: Int16、 Int32、 Int64、 單一、 Double、 Decimal、 Byte []、 Bool、 字串、 Guid、 Datetime、Datetimeoffset、 Timespan。 Data Factory 會移動資料的來源資料的資料存放區 tooa 接收資料存放區時，會自動執行類型轉換。

hello **typeProperties**區段是不同的資料集的每個型別，並提供資訊 hello 位置相關格式等，hello hello 資料儲存區的資料。 hello typeProperties 區段類型的資料集**AzureBlob**資料集具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |路徑 toohello 容器，並且在 hello blob 儲存體中的資料夾。 範例：myblobcontainer\myblobfolder\ |是 |
| fileName |Hello blob 名稱。 fileName 是選擇性的，而且區分大小寫。<br/><br/>如果您在上指定的檔名、 hello 活動 （包括複製） 運作 hello 特定 Blob。<br/><br/>若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有 Blob。<br/><br/>當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱會在 hello 遵循此格式： 資料。<Guid>。txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |否 |
| partitionedBy |partitionedBy 是選擇性的屬性。 您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。 例如，folderPath 可針對每小時的資料進行參數化。 請參閱 hello[使用 partitionedBy 屬性區段](#using-partitionedBy-property)如需詳細資訊和範例。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

### <a name="using-partitionedby-property"></a>使用 partitionedBy 屬性
當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。

如需時間序列資料集、排程和配量的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)和[排程和執行](data-factory-scheduling-and-execution.md)等文章。

#### <a name="sample-1"></a>範例 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

在此範例中，指定在 hello 格式 (YYYYMMDDHH) 的 Data Factory 系統變數 SliceStart hello 值取代 {Slice}。 hello SliceStart 是指 toostart hello 配量時間。 hello folderPath 是不同的每個配量。 例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104

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

在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。 而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。 如果您要移動的資料從 Azure Blob 儲存體，您設定 hello 來源類型 hello 複製活動中太**BlobSource**。 同樣地，如果您要移動資料 tooan Azure Blob 儲存體，您設定 hello 接收器類型 hello 複製活動中太**BlobSink**。 本節提供 BlobSource 和 BlobSink 支援的屬性清單。

**BlobSource**支援下列屬性在 hello hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True (預設值)、False |否 |

**BlobSink**支援下列屬性的 hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| copyBehavior |Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。 |<b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。 hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。<br/><br/><b>FlattenHierarchy</b>: hello 來源資料夾中的所有檔案都位於 hello 第一次層級的目標資料夾。 hello 目標檔案已自動產生的名稱。 <br/><br/><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。 |否 |

**BlobSource** 也支援這兩個屬性以提供回溯相容性。

* **treatEmptyAsNull**： 指定是否 tootreat null 或空字串視為 null 值。
* **skipHeaderLineCount** - 指定需略過多少行。 僅適用於輸入資料集使用 TextFormat 時。

同樣地， **BlobSink**支援 hello 遵循回溯相容性的屬性。

* **blobWriterAddHeader**： 指定是否 tooadd 寫入 tooan 時的資料行定義的標頭輸出資料集。

下列實作的屬性的資料集現在支援 hello hello 相同的功能： **treatEmptyAsNull**， **skipLineCount**， **firstRowAsHeader**。

hello 下表提供使用指引來取代這些 blob 來源/接收器屬性 hello 新資料集屬性。

| 複製活動屬性 | 資料集屬性 |
|:--- |:--- |
| BlobSource 上的 skipHeaderLineCount |skipLineCount 和 firstRowAsHeader。 線條會略過第一次，然後做為標頭讀取 hello 第一個資料列。 |
| BlobSource 上的 treatEmptyAsNull |輸入資料集上的 treatEmptyAsNull |
| BlobSink 上的 blobWriterAddHeader |輸出資料集上的 firstRowAsHeader |

如需這些屬性的詳細資訊，請參閱 [指定 TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) 一節。    

### <a name="recursive-and-copybehavior-examples"></a>遞迴和 copyBehavior 範例
本章節描述 hello hello 複製作業，針對遞迴和 copyBehavior 值的不同組合產生的行為。

| 遞迴 | copyBehavior | 產生的行為 |
| --- | --- | --- |
| true |preserveHierarchy |來源資料夾 Folder1 以 hello 下列結構： <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 目標資料夾 Folder1 建立以相同結構為 hello 來源 hello<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| true |flattenHierarchy |來源資料夾 Folder1 以 hello 下列結構： <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標 Folder1: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱 |
| true |mergeFiles |來源資料夾 Folder1 以 hello 下列結構： <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標 Folder1: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱 |
| false |preserveHierarchy |來源資料夾 Folder1 以 hello 下列結構： <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。 |
| false |flattenHierarchy |來源資料夾 Folder1 以 hello 下列結構：<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱<br/><br/><br/>系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。 |
| false |mergeFiles |來源資料夾 Folder1 以 hello 下列結構：<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。 File1 有自動產生的名稱<br/><br/>系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。 |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>逐步解說： 使用複製精靈 toocopy 資料，從 Blob 儲存體
讓我們看看如何 tooquickly 複製資料，從 Azure blob 儲存體。 在這個逐步解說中，來源和目的地資料存放區的類型都是：Azure Blob 儲存體。 hello 管線，在此逐步解說中的資料複製 tooanother 資料夾 hello 中相同的 blob 容器。 這個逐步解說是刻意簡單 tooshow 您的設定或使用 Blob 儲存體做為來源或接收器的屬性。 

### <a name="prerequisites"></a>必要條件
1. 建立一個一般用途的「Azure 儲存體帳戶」(如果您還沒有此帳戶)。 您同時使用 hello blob 儲存體**來源**和**目的地**資料儲存在這個逐步解說。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。
2. 建立名為的 blob 容器**adfblobconnector** hello 儲存體帳戶中。 
4. 建立名為的資料夾**輸入**在 hello **adfblobconnector**容器。
5. 建立名為**emp.txt**以 hello 下列內容，並將它上傳 toohello**輸入**資料夾使用工具，像是[Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>建立 hello 資料處理站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**+ 新增**從 hello 左上角，按一下 **智慧 + 分析**，然後按一下**Data Factory**。
3. 在 hello**新的 data factory**刀鋒視窗中：   
    1. 輸入**ADFBlobConnectorDF** hello**名稱**。 hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： `*Data factory name “ADFBlobConnectorDF” is not available`、 變更 hello hello data factory (例如，yournameADFBlobConnectorDF) 名稱，然後再次嘗試重新建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
    2. 選取您的 Azure **訂用帳戶**。
    3. 資源群組，請選取**使用現有**tooselect 現有資源群組 （或） 選取**建立新**tooenter 資源群組的名稱。
    4. 選取**位置**hello data factory。
    5. 選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。
    6. 按一下 [建立] 。
3. Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：![資料 factory 首頁](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>複製精靈
1. 在 hello Data Factory 首頁上，按一下 hello**複製資料 [預覽]**磚 toolaunch**複製資料精靈**個別索引標籤中。    
    
    > [!NOTE]
    >    如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**設定 （或） 保留啟用它，並建立的例外狀況**login.microsoftonline.com**，然後再次嘗試重新啟動 hello 精靈。
2. 在 hello**屬性**頁面：
    1. 針對 [工作名稱]，輸入 **CopyPipeline**。 hello 工作名稱是您的 data factory 中的 hello 管線 hello 名稱。
    2. 輸入**描述**hello 工作 （選擇性）。
    3. 如**工作韻律或工作排程**，保留 hello**排程定期執行**選項。 如果您想的 toorun 排程重複執行此工作一次，而不是，選取**執行一次，就**。 如果您選取 [立即執行一次] 選項，系統就會建立一個[單次管線](data-factory-create-pipelines.md#onetime-pipeline)。 
    4. 保留 hello 設定**週期性模式**。 這項工作執行每日之間 hello 的開始和結束時間您指定 hello 下一個步驟中。
    5. 變更 hello**的開始日期時間**太**04/21/2017年**。 
    6. 變更 hello**結束日期時間**太**04/25/2017年**。 您可能想 tootype hello 日期，而不是瀏覽 hello 行事曆。     
    8. 按一下 [下一步] 。
      ![複製工具 - 屬性頁面](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. 在 hello**來源資料存放區**頁面上，按一下**Azure Blob 儲存體**磚。 您可以使用這個頁面 toospecify hello 來源資料存放區 hello 複製工作。 您可以使用現有的資料存放區連結服務或指定新的資料存放區。 toouse 現有連結服務，您就必須選取**從現有連結的服務**和選取 hello 右邊的連結的服務。 
    ![複製工具 - 來源資料存放區頁面](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. 在 hello**指定 hello Azure Blob 儲存體帳戶**頁面：
   1. 保留 hello 自動產生名稱為**連接名稱**。 hello 連接名稱是 hello hello 連結服務類型的名稱： Azure 儲存體。 
   2. 確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。
   3. 針對 [Azure 訂用帳戶]，選取您的 Azure 訂用帳戶或保留 [全選]。   
   4. 選取**Azure 儲存體帳戶**從 hello hello 選取訂用帳戶中可使用的清單中的 Azure 儲存體帳戶。 您也可以選擇 tooenter 儲存體帳戶設定手動選取**手動輸入**選項 hello**帳戶選取方法**。
   5. 按一下 [下一步] 。 
      ![複製工具-指定 hello Azure Blob 儲存體帳戶](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. 在**選擇 hello 輸入的檔案或資料夾**頁面：
   1. 按兩下 [adfblobcontainer]。
   2. 選取 [input]，然後按一下 [選擇]。 在本逐步解說，您可以選取 hello 輸入的資料夾。 您也可以改為選取 hello 資料夾 hello emp.txt 檔案。 
      ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. 在 hello**選擇 hello 輸入的檔案或資料夾**頁面：
    1. 確認該 hello**檔案或資料夾**設定得**adfblobconnector/輸入**。 如果 hello 檔案子資料夾中，比方說，2017年/04/01、 2017年/04/02 等等，請輸入 adfblobconnector/輸入 / {year} / {month} / {day} 檔案或資料夾。 當您按下 TAB 鍵超出 hello 文字方塊中時，您會看到三個下拉式清單 tooselect 格式的年份 (yyyy)、 month (MM) 和一天 (dd)。 
    2. 請勿設定 [以遞迴方式複製檔案]。 選取此選項 toorecursively 周遊，透過檔案 toobe 複製的 toohello 目的地的資料夾。 
    3. 不執行 hello**二進位複製**選項。 選取此選項 tooperform 二進位的來源檔案 toohello 目的複本。 未選取此逐步解說中，讓您可以查看更多的 hello 接下來的頁面選項。 
    4. 確認該 hello**壓縮類型**設定得**無**。 如果您的來源檔案會壓縮其中一種支援的 hello 格式，請選取這個選項的值。 
    5. 按一下 [下一步] 。
    ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. 在 hello**檔案格式設定** 頁面上，您會看到 hello 分隔符號和是藉由剖析 hello 檔案的 自動偵測到的 hello 精靈的 hello 結構描述。 
    1. 確認 hello 下列選項：。 hello**檔案格式**設定得**文字格式**。 您可以查看所有支援的 hello 格式 hello 下拉式清單中。 例如：JSON、Avro、ORC、Parquet。
        b. hello**資料行分隔符號**設定得`Comma (,)`。 您可以看到 hello hello 下拉式清單中的 Data Factory 支援其他資料行分隔符號。 您也可以指定自訂的分隔符號。
        c. hello**資料列分隔符號**設定得`Carriage Return + Line feed (\r\n)`。 您可以看到 hello hello 下拉式清單中的 Data Factory 支援其他資料列分隔符號。 您也可以指定自訂的分隔符號。
        d. hello**略過行數**設定得**0**。 如果您想略過在 hello hello 檔案最上方的幾行 toobe，輸入 hello 數字。
        e.  hello**第一個資料列包含資料行名稱**未設定。 如果 hello 原始程式檔包含 hello 第一個資料列中的資料行名稱，請選取此選項。
        f. hello**空的資料行值視為 null**選項設定。
    2. 展開**進階設定**toosee 進階可用的選項。
    3. 在 hello hello 頁面底部，請參閱 hello**預覽**的 hello emp.txt 檔中的資料。
    4. 按一下**結構描述**hello 底部 toosee hello 結構描述推斷藉由在 hello 資料 hello 原始程式檔中查看該 hello 複製精靈 」 索引標籤。
    5. 按一下**下一步**在檢閱 hello 分隔符號和預覽資料。
    ![複製工具 - 檔案格式設定](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. 在 hello**目的地資料存放區頁面**，選取**Azure Blob 儲存體**，然後按一下**下一步**。 您正在使用 hello Azure Blob 儲存體，以在此逐步解說中這兩個 hello 來源和目的地資料存放區。    
    ![複製精靈 - 選取目的地資料存放區](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. 在**指定 hello Azure Blob 儲存體帳戶**頁面：
   1. 輸入**AzureStorageLinkedService** hello**連接名稱**欄位。
   2. 確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。
   3. 選取您的 Azure **訂用帳戶**。  
   4. 選取您的 Azure 儲存體帳戶。 
   5. 按一下 [下一步] 。     
10. 在 hello**選擇 hello 輸出檔案或資料夾**頁面： 
    6. 將 [資料夾路徑] 指定為 **adfblobconnector/output/{year}/{month}/{day}**。 輸入 **TAB**。
    7. Hello**年**，選取**yyyy**。
    8. Hello**月份**，確認已設定太**公釐**。
    9. Hello**天**，確認已設定太**dd**。
    10. 確認該 hello**壓縮類型**設定得**無**。
    11. 確認該 hello**複製行為**設定得**合併檔案**。 如果 hello 輸出檔案具有相同的名稱已存在的 hello，hello 新內容也會加入的 toohello 相同檔案 hello 結尾。
    12. 按一下 [下一步] 。
    ![複製工具 - 選擇輸出檔案或資料夾](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. 在 hello**檔案格式設定**頁面上，檢閱 hello 設定，然後按一下**下一步**。 這裡 hello 其他選項的其中一個是 tooadd 標頭 toohello 輸出檔。 如果您選取該選項時，標頭資料列會加入與 hello 資料行的名稱，從 hello hello 來源結構描述。 檢視 hello hello 來源結構描述時，您可以重新命名 hello 預設資料行名稱。 例如，您可以變更第一個資料行 tooFirst hello 名稱和第二個資料行 tooLast 名稱。 然後，hello 產生輸出檔案具有標頭，與這些名稱當做資料行名稱。 
    ![複製工具 - 目的地的檔案格式設定](media/data-factory-azure-blob-connector/file-format-destination.png)
12. 在 hello**效能設定**頁面上，確認**雲端單位**和**平行複製**設定得**自動**，然後按一下 [下一步]。 如需有關這些設定的詳細資料，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md#parallel-copy)。
    ![複製工具 - 效能設定](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. 在 hello**摘要**頁面上，檢閱所有設定 （工作內容、 設定來源和目的地，並複製設定值），然後按一下**下一步**。
    ![複製工具 - 摘要頁面](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. 檢閱資訊在 hello**摘要**頁面，然後按一下**完成**。 hello 精靈會建立兩個連結的服務、 兩個資料集 （輸入與輸出），以及一個管線 （從啟動 hello 複製精靈 」 的位置） 的 hello data factory 中。
    ![複製工具 - 部署頁面](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>監視 hello 管線 （複製工作）

1. 按一下 hello 連結`Click here toomonitor copy pipeline`上 hello**部署**頁面。 
2. 您應該會看見 hello**監視和管理應用程式**個別索引標籤中。![監視及管理應用程式](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. 變更 hello**啟動**太時間 hello 頂端`04/19/2017`和**結束**時間太`04/27/2017`，然後按一下**套用**。 
4. 您應該會看到五個活動 windows hello 中的**活動 WINDOWS**清單。 hello **WindowStart**時間應該涵蓋所有日從管線開始 toopipeline 結束時間。 
5. 按一下**重新整理**按鈕 hello**活動 WINDOWS** tooReady 設定幾次，直到您看到所有的 hello 活動 windows hello 狀態的清單。 
6. 現在，確認 hello 輸出檔會產生 adfblobconnector 容器 hello 輸出資料夾中。 您應該會看到下列資料夾結構 hello 輸出資料夾中的 hello: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
如需有關監視及管理 Data Factory 的詳細資訊，請參閱[監視和管理 Data Factory 管線](data-factory-monitor-manage-app.md)一文。 
 
### <a name="data-factory-entities"></a>Data Factory 實體
現在，請切換後 toohello hello Data Factory 首頁索引標籤。 請注意，您的 Data Factory 現在有兩個已連結的服務、兩個資料集，以及一條管線。 

![含有實體的 Data Factory 首頁](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

按一下**作者及部署**toolaunch Data Factory 編輯器。 

![Data Factory 編輯器](media/data-factory-azure-blob-connector/data-factory-editor.png)

您應該會看到下列 data factory 中的 Data Factory 實體的 hello: 

 - 兩個已連結的服務。 其中一個 hello 來源和目的地 hello hello 另一個。 這兩個 hello 連結服務，請參閱 toohello 在本逐步解說的相同 Azure 儲存體帳戶。 
 - 兩個資料集。 一個輸入資料集和一個輸出資料集。 在本逐步解說中，都使用 hello 相同 blob 容器，但是參考 toodifferent 資料夾 （輸入與輸出）。
 - 一條管線。 hello 管線包含複製活動會使用 blob 來源和 blob 接收 toocopy 資料從 Azure blob 位置 tooanother Azure blob 的位置。 

hello 下列各節提供有關這些實體的詳細資訊。 

#### <a name="linked-services"></a>連結的服務
您應該會看到兩個已連結的服務。 其中一個 hello 來源和目的地 hello hello 另一個。 在本逐步解說中，這兩個定義外觀 hello 相同 hello 名稱除外。 hello**類型**hello 連結的服務已設定太**AzureStorage**。 Hello 連結服務定義的最重要的屬性為 hello **connectionString**，這由 Data Factory tooconnect tooyour 在執行階段的 Azure 儲存體帳戶。 忽略 hello 定義中的 hello hubName 屬性。 

##### <a name="source-blob-storage-linked-service"></a>來源 Blob 儲存體連結服務
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>目的地 Blob 儲存體連結服務

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

如需有關「Azure 儲存體」連結服務的詳細資訊，請參閱[連結服務屬性](#linked-service-properties)一節。 

#### <a name="datasets"></a>資料集
有兩個資料集：一個輸入資料集和一個輸出資料集。 hello 資料集的 hello 類型設定得**AzureBlob**兩者。 

輸入資料集 hello 點 toohello**輸入**資料夾 hello **adfblobconnector** blob 容器。 hello**外部**屬性設定太**true** hello 為此資料集的資料就不會產生 hello 管線與 hello 複製活動會做為輸入此資料集。 

hello 輸出資料集點 toohello**輸出**hello 資料夾相同的 blob 容器。 hello 輸出資料集也會使用 hello 年、 月和日的 hello **SliceStart**系統變數 toodynamically 評估 hello hello 輸出檔的路徑。 如需 Data Factory 所支援的函式與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。 hello**外部**屬性設定太**false** （預設值） 因為此資料集由 hello 管線所產生。 

如需有關 Azure Blob 資料集所支援屬性的詳細資訊，請參閱[資料集屬性](#dataset-properties)一節。

##### <a name="input-dataset"></a>輸入資料集

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>輸出資料集

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>管線
hello 管線有一個活動。 hello**類型**hello 活動已設定太**複製**。  在 hello hello 活動的類型屬性，有兩個區段，另一個用於來源和接收另一個 hello。 hello 來源類型會設定太**BlobSource**為 hello 活動正在將資料複製從 blob 儲存體。 hello 接收器類型會設定太**BlobSink**作為複製資料 tooa blob 儲存體的 hello 活動。 hello 複製活動採用 InputDataset z4y hello 和當做輸入 OutputDataset-z4y 做為 hello 輸出。 

如需有關 BlobSource 和 BlobSink 所支援屬性的詳細資訊，請參閱[複製活動屬性](#copy-activity-properties)一節。 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>從 Blob 儲存體複製資料 tooand JSON 範例  
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Azure Blob 儲存體和 Azure SQL Database toocopy 資料 tooand。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>JSON 範例： 從 Blob 儲存體 tooSQL 資料庫複製資料
下列範例會示範 hello:

1. [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](#linked-service-properties)類型的連結服務。
3. [AzureBlob](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [BlobSource](#copy-activity-properties) 和 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從 Azure blob tooan Azure SQL 資料表複製時間序列資料的每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure SQL 連結服務：**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure 儲存體連結服務：**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。 如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。 請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。  

**Azure Blob 輸入資料集：**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在該 hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時通知 Data Factory。

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
**Azure SQL 輸出資料集：**

hello 範例複製 Azure SQL database 中名為"MyTable"的資料 tooa 資料表。 在與您 Azure SQL database 中建立 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**具有 Blob 來源和 SQL 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
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
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>JSON 範例： 將資料複製 Azure SQL tooAzure Blob
下列範例會示範 hello:

1. [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](#linked-service-properties)類型的連結服務。
3. [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 和 [BlobSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從 Azure SQL 資料表 tooan Azure blob 複製時間序列資料的每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure SQL 連結服務：**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure 儲存體連結服務：**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。 如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。 請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。  

**Azure SQL 輸入資料集：**

hello 範例假設您已建立資料表"MyTable"Azure SQL 中，而且包含稱為 「 timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**具有 SQL 來源和 Blob 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
