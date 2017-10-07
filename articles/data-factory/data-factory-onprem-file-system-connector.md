---
title: "aaaCopy 資料，從檔案系統，使用 Azure Data Factory |Microsoft 文件"
description: "深入了解如何從內部部署檔案系統使用 Azure Data Factory toocopy 資料 tooand。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>從內部部署檔案系統複製資料 tooand，使用 Azure Data Factory
本文說明如何 toouse hello Azure Data Factory toocopy 資料從內部部署檔案系統中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從內部部署檔案系統**toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooan 內部檔案系統**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> 複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。 如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。 

## <a name="enabling-connectivity"></a>啟用連線
Data Factory 支援透過在內部部署檔案系統中的連接 tooand**資料管理閘道器**。 您必須安裝 hello 資料管理閘道器在內部部署環境的 hello Data Factory 服務 tooconnect tooany 支援在內部部署資料存放區包括檔案系統中。 請參閱 toolearn 有關資料管理閘道器以及如需 hello 閘道設定的逐步指示[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。 資料管理閘道器，除了其他二進位檔案需要安裝 toobe toocommunicate tooand 從內部部署檔案系統。 您必須安裝並使用 hello 資料管理閘道，即使是在 Azure IaaS VM 的 hello 檔案系統。 如需 hello 閘道的詳細資訊，請參閱[資料管理閘道器](data-factory-data-management-gateway.md)。

安裝 Linux 檔案共用，toouse [Samba](https://www.samba.org/) Linux 伺服器和 Windows server 上的安裝資料管理閘道器上。 不支援在 Linux 伺服器上安裝資料管理閘道。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出檔案系統。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體 tooan 在內部部署檔案系統複製資料，您建立兩個連結的服務 toolink 在內部部署檔案系統與 Azure 儲存體帳戶 tooyour 資料 factory。 對於特定 tooan 在內部部署檔案系統連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。
3. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。 此外，您會建立另一個資料集 toospecify hello 資料夾和檔案名稱 （選擇性） 在檔案系統。 為特定 tooon 內部的資料集屬性的檔案系統，請參閱[資料集屬性](#dataset-properties)> 一節。
4. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 BlobSource 作為來源和使用 FileSystemSink 做為接收器 hello 複製活動。 同樣地，如果您要從內部部署檔案系統 tooAzure Blob 儲存體複製，則使用 FileSystemSource 和 BlobSink 的 hello 複製活動。 複製活動內容特定 tooon 內部檔案系統，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 [工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料，從檔案系統的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-file-system)本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 toofile 系統的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
您可以連結在內部部署檔案系統 tooan Azure data factory 以 hello**在內部部署檔案伺服器**連結服務。 hello 下表提供說明屬於特定 toohello 連結在內部部署檔案伺服器服務的 JSON 元素。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |請確定 hello type 屬性設定太**OnPremisesFileServer**。 |是 |
| 主機 |指定您想 toocopy hello 資料夾 hello 根路徑。 使用 hello 逸出字元 '\' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。 |是 |
| userid |指定具有存取 toohello 伺服器 hello 使用者識別碼 hello。 |否 (如果您選擇 encryptedCredential) |
| password |指定 hello hello 使用者 (userid) 的密碼。 |否 (如果您選擇 encryptedCredential) |
| encryptedCredential |指定您可以藉由執行 hello 新增 AzureRmDataFactoryEncryptValue cmdlet 取得的 hello 加密認證。 |否 （如果您選擇 toospecify 使用者識別碼和密碼以純文字） |
| gatewayName |指定 hello hello 閘道的 Data Factory 應該使用 tooconnect toohello 在內部部署檔案伺服器名稱。 |是 |


### <a name="sample-linked-service-and-dataset-definitions"></a>範例連結服務和資料集定義
| 案例 | 連結服務定義中的主機 | 資料集定義中的 folderPath |
| --- | --- | --- |
| 資料管理閘道電腦上的本機資料夾︰ <br/><br/>範例：D:\\\* 或 D:\folder\subfolder\\* |D:\\\\ (適用於資料管理閘道 2.0 和更新版本) <br/><br/> localhost (適用於比資料管理閘道 2.0 更早的版本) |.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本) <br/><br/>D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本) |
| 遠端共用資料夾︰ <br/><br/>範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\share |.\\\\ 或 folder\\\\subfolder |


### <a name="example-using-username-and-password-in-plain-text"></a>範例：使用純文字的使用者名稱和密碼

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>範例：使用 encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>資料集屬性
如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。

hello typeProperties 區段是不同的資料集的每個型別。 它提供資訊，例如 hello 位置和 hello 資料存放區中的 hello 資料格式。 hello typeProperties 區段 hello 資料集型別的**FileShare**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| folderPath |指定 hello 子路徑 toohello 資料夾。 使用 hello 逸出字元 ' \' hello 字串中的特殊字元。 如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。<br/><br/>您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。 |是 |
| fileName |在 [hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。 如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。<br/><br/>當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱是以下列格式的 hello: <br/><br/>`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |否 |
| fileFilter |指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。 <br/><br/>允許的值為︰`*` (多個字元) 和 `?` (單一字元)。<br/><br/>範例 1："fileFilter": "*.log"<br/>範例 2："fileFilter": 2014-1-?.txt"<br/><br/>請注意，fileFilter 適用於輸入 FileShare 資料集。 |否 |
| partitionedBy |您可以使用 partitionedBy toospecify 動態 folderPath/檔名，時間序列資料。 例如，folderPath 可針對每小時的資料進行參數化。 |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 <br><br> 如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

> [!NOTE]
> 無法同時使用 fileName 和 fileFilter。

### <a name="using-partitionedby-property"></a>使用 partitionedBy 屬性
當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。

toounderstand 更多詳細資料，在時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程與執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)。

#### <a name="sample-1"></a>範例 1：

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

在此範例中，hello hello Data Factory 系統變數 SliceStart hello 格式 (YYYYMMDDHH) 值會取代 {Slice}。 SliceStart 是指配 toostart hello 配量時間。 hello folderPath 是不同的每個配量。 例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。

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

在此範例中，年、 月、 日和時間的 SliceStart 會擷取到個別 hello folderPath 和 fileName 屬性所使用的變數。

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。 而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。

複製活動它們而異的來源與接收的 hello 類型。 如果您要從內部部署檔案系統中移動資料，您設定 hello 來源類型 hello 複製活動中太**FileSystemSource**。 同樣地，如果您要移動資料 tooan 在內部部署檔案系統，hello 接收器類型中設定 hello 複製活動太**使用 FileSystemSink**。 本節提供 FileSystemSource 和 FileSystemSink 所支援的屬性清單。

**FileSystemSource**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True/False (預設值為 False) |否 |

**使用 FileSystemSink**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| copyBehavior |Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。 |**PreserveHierarchy:**保留 hello hello 目標資料夾中的檔案階層。 也就是說，hello hello 來源檔案 toohello 來源資料夾的相對路徑是 hello 與 hello 相對路徑的 hello 目標檔案 toohello 目標資料夾相同。<br/><br/>**FlattenHierarchy:** hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。 會使用自動產生名稱建立 hello 目標檔案。<br/><br/>**MergeFiles:**合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果指定 hello 檔案名稱/blob 名稱，則 hello 合併的檔案名稱是 hello 指定的名稱。 否則，就會是自動產生的檔案名稱。 |否 |

### <a name="recursive-and-copybehavior-examples"></a>遞迴和 copyBehavior 範例
本章節描述 hello 產生不同的值為 hello 遞迴和 copyBehavior 屬性組合的 hello 複製作業的行為。

| recursive 值 | copyBehavior 值 | 產生的行為 |
| --- | --- | --- |
| true |preserveHierarchy |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>建立 hello 目標資料夾 Folder1 hello 相同結構為 hello 來源：<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| true |flattenHierarchy |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標 Folder1: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱 |
| true |mergeFiles |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標 Folder1: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱。 |
| false |preserveHierarchy |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>系統不會挑選含有 File3、File4、File5 的 Subfolder1。 |
| false |flattenHierarchy |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱<br/><br/>系統不會挑選含有 File3、File4、File5 的 Subfolder1。 |
| false |mergeFiles |來源資料夾 Folder1 以 hello 下列結構，<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>使用下列結構的 hello 建立 hello 目標資料夾 Folder1:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱<br/><br/>系統不會挑選含有 File3、File4、File5 的 Subfolder1。 |

## <a name="supported-file-and-compression-formats"></a>支援的檔案和壓縮格式
請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>從檔案系統複製資料 tooand JSON 範例
hello 下列範例會提供範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從內部部署檔案系統和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，您可以將資料複製*直接*從 hello 來源 tooany hello 接收中列出的任一[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)Azure Data Factory 中使用複製活動。

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>範例： 將資料從內部部署檔案系統 tooAzure Blob 儲存體複製
這個範例示範如何從內部部署檔案系統 tooAzure Blob 儲存體 toocopy 資料。 hello 範例有下列 Data Factory 實體的 hello:

* [OnPremisesFileServer](#linked-service-properties)類型的連結服務。
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

下列範例中的 hello 複製時間序列資料從內部部署檔案系統 tooAzure Blob 儲存體每小時。 這些範例中所使用的 hello JSON 屬性 hello 各節所述之後 hello 範例。

第一個步驟中，設定資料管理閘道器中的 hello 指示根據[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。

**內部部署檔案伺服器連結服務：**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

我們建議您使用 hello **encryptedCredential**屬性改為 hello **userid**和**密碼**屬性。 如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。

**Azure 儲存體連結服務：**

```JSON
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

**內部部署檔案系統輸入資料集：**

每小時從新的檔案挑選資料。 hello folderPath 和 fileName 屬性由決定依據 hello hello 配量的開始時間。  

設定`"external": "true"`該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 Data Factory。

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Azure Blob 儲存體資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**具有檔案系統來源和 Blob 接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和**接收**類型設定得**BlobSink**。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>範例： 將資料從 Azure SQL Database tooan 在內部部署檔案系統複製
下列範例會示範 hello:

* [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 類型的已連結服務。
* [OnPremisesFileServer](#linked-service-properties)類型的連結服務。
* [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入資料集。
* [FileShare](#dataset-properties) 類型的輸出資料集。
* 具有使用 [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 和 [FileSystemSink](#copy-activity-properties) 之複製活動的管線。

hello 範例將時間序列資料從 Azure SQL 資料表 tooan 在內部部署檔案系統每小時。 這些範例中所使用的 hello JSON 屬性各節所述之後 hello 範例。

**Azure SQL Database 已連結的服務：**

```JSON
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

**內部部署檔案伺服器連結服務：**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

我們建議您使用 hello **encryptedCredential**屬性，而不要使用 hello **userid**和**密碼**屬性。 如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。

**Azure SQL 輸入資料集：**

hello 範例假設您已建立資料表"MyTable"Azure SQL 中和它包含稱為"timestampcolumn 「 時間序列資料的資料行。

設定``“external”: ”true”``該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 Data Factory。

```JSON
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

**內部部署檔案系統輸出資料集：**

資料是每小時的複製的 tooa 新檔案。 hello folderPath 和 fileName hello blob 決定依據 hello hello 配量的開始時間。

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**具有 SQL 來源和檔案系統接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**，和 hello**接收**類型設定得**使用 FileSystemSink**。 hello SQL 查詢，以指定的 hello **SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。 如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
 關於金鑰 toolearn 因素影響 hello 效能的 Azure Data Factory 和各種方式 toooptimize 中的資料移動 （複製活動），請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。
