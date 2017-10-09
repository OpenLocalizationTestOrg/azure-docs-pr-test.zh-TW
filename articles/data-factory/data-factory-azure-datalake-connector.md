---
title: "從 Azure Data Lake Store aaaCopy 資料 tooand |Microsoft 文件"
description: "深入了解如何從資料湖存放區使用 Azure Data Factory 的 toocopy 資料 tooand"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>複製資料湖存放區中的資料 tooand，使用 Data Factory
這篇文章說明如何在 Azure 資料湖存放區從 Azure Data Factory toomove 資料 tooand toouse 複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)發行項的資料移動，複製活動的概觀。

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 Azure Data Lake Store** toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooAzure Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> 先建立 Data Lake Store 帳戶，再使用「複製活動」建立管線。 如需詳細資訊，請參閱[開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)。

## <a name="supported-authentication-types"></a>支援的驗證類型
hello Data Lake Store 連接器支援這些驗證類型：
* 服務主體驗證
* 使用者認證 (OAuth) 驗證 

我們建議您使用服務主體驗證，特別是針對排程的資料複本。 權杖到期行為會連同使用者認證驗證發生。 設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。

## <a name="get-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Data Lake Store。

最簡單方式 toocreate hello 管線 toocopy 資料為 toouse hello**複製精靈**。 如需使用 hello 複製精靈建立管線的教學課程，請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您要從 Azure blob 儲存體 tooan Azure 資料湖存放區來複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure 資料湖存放區 tooyour 資料 factory。 連結的服務是特定 tooAzure 資料湖存放區的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。 
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。 而且，您保存 hello 資料從 hello blob 儲存體複製 hello 資料湖存放區中建立另一個資料集 toospecify hello 資料夾和檔案路徑。 資料集是特定 tooAzure 資料湖存放區的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 BlobSource 作為來源和 AzureDataLakeStoreSink 做為接收器 hello 複製活動。 同樣地，如果您要從 Azure Data Lake Store tooAzure Blob 儲存體複製，則使用 AzureDataLakeStoreSource 和 BlobSink 的 hello 複製活動。 特定 tooAzure 資料湖存放區複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。  

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料至 azure 或從 Azure Data Lake Store 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-data-lake-store)本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooData Lake Store 的 JSON 屬性的詳細資料。

## <a name="linked-service-properties"></a>連結服務屬性
連結的服務連結資料儲存區 tooa data factory。 您建立連結的服務型別的**AzureDataLakeStore** toolink 您 Data Lake Store 資料 tooyour 的 data factory。 hello 下表描述的 JSON 元素特定 tooData Lake Store 連結服務。 您可以在服務主體與使用者認證驗證之間選擇。

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **type** | hello type 屬性必須設定得**AzureDataLakeStore**。 | 是 |
| **dataLakeStoreUri** | Hello Azure Data Lake Store 帳戶的相關資訊。 這項資訊會使用其中一個 hello 下列格式：`https://[accountname].azuredatalakestore.net/webhdfs/v1`或`adl://[accountname].azuredatalakestore.net/`。 | 是 |
| **subscriptionId** | 所屬的 azure 訂用帳戶 ID toowhich hello Data Lake Store 帳戶。 | 接收 (Sink) 的必要項目 |
| **resourceGroupName** | 所屬的 azure 資源群組名稱 toowhich hello Data Lake Store 帳戶。 | 接收 (Sink) 的必要項目 |

### <a name="service-principal-authentication-recommended"></a>服務主體驗證 (建議)
服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。 如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。 請記下的下列值，您使用的 hello toodefine hello 連結服務：
* 應用程式識別碼
* 應用程式金鑰 
* 租用戶識別碼

> [!IMPORTANT]
> 如果您使用 hello 複製精靈 tooauthor 資料管線，請確定您授與 hello 服務主體至少**讀取器**hello Data Lake Store 帳戶的存取控制 （身分識別和存取管理） 中的角色。 此外，至少授與 hello 服務主體**讀取 + Execute**權限 tooyour Data Lake Store 根 （"/"） 和其子系。 否則，您可能會看到 hello 訊息"hello 提供的認證無效。"<br/><br/>
您建立或更新 Azure AD 中的服務主體之後，可能需要幾分鐘，讓 hello 變更 tootake 效果。 請檢查 hello 服務主體以及資料湖存放區的存取控制清單 (ACL) 設定。 如果您仍然看到 hello 訊息"提供的認證不正確的 hello"，請稍待片刻，然後再試。

您可以使用服務主體的驗證方法是指定 hello 下列屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **servicePrincipalId** | 指定 hello 應用程式的用戶端識別碼。 | 是 |
| **servicePrincipalKey** | 指定 hello 應用程式的金鑰。 | 是 |
| **tenant** | 指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。 您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。 | 是 |

**範例：服務主體驗證**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>使用者認證驗證
或者，您可以使用從使用者認證驗證 toocopy 或 tooData 湖存放區，藉由指定下列屬性的 hello:

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **authorization** | 按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。 | 是 |
| **sessionId** | 從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。 每個工作階段識別碼都是唯一的，只能使用一次。 當您使用 hello Data Factory 編輯器時，此設定會自動產生。 | 是 |

**範例：使用者認證授權**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>權杖到期
hello 您使用 hello 產生的授權碼**授權**一段時間之後過期的按鈕。 hello 下訊息，表示該 hello 驗證權杖已過期：

認證作業錯誤：invalid_grant - AADSTS70002：驗證認證時發生錯誤。 AADSTS70008: hello 提供存取權限已過期或撤銷。 追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21-09-31Z。

hello 下表顯示 hello 逾期時間的不同類型的使用者帳戶：


| 使用者類型 | 到期時間 |
|:--- |:--- |
| 「不」受 Azure Active Directory 管理的使用者帳戶 (例如 @hotmail.com 或 @live.com) |12 小時 |
| 受 Azure Active Directory 管理的使用者帳戶 |14 天之後執行 hello 最後一個配量 <br/><br/>如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天 |

如果您變更您的密碼 hello 權杖到期時間之前，hello 語彙基元就會立即到期。 您會看見 hello 訊息本節先前所述。

您可以重新 hello 帳戶授權使用 hello**授權**按鈕時 hello 權杖到期 tooredeploy hello 連結服務。 您也可以產生值 hello **sessionId**和**授權**屬性以程式設計方式利用 hello 下列程式碼：


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
如需 hello 程式碼中使用的 hello Data Factory 類別的詳細資訊，請參閱 hello [AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題。 新增參考 tooversion`2.9.10826.1824`的`Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll`hello `WindowsFormsWebAuthenticationDialog` hello 程式碼中使用的類別。

## <a name="dataset-properties"></a>資料集屬性
toospecify 資料湖存放區中的資料集 toorepresent 輸入資料，設定 hello**類型**hello 資料集的屬性太**AzureDataLakeStore**。 設定 hello **linkedServiceName** hello Data Lake Store 的 hello 資料集 toohello 名稱的屬性連結服務。 如需 JSON 區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 所有資料集類型 (例如 Azure SQL 資料庫、Azure Blob 及 Azure 資料表) 其 JSON 中如結構、可用性及原則等資料集區段都相似。 hello **typeProperties**章節是不同的資料集的每個型別，並提供資訊，例如位置和 hello 資料存放區中的 hello 資料格式。 

hello **typeProperties**類型的資料集區段**AzureDataLakeStore**包含下列屬性的 hello:

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **folderPath** |路徑 toohello 容器，並在資料湖存放區中的資料夾。 |是 |
| **fileName** |在 Azure 資料湖存放區中的 hello 檔案的名稱。 hello **fileName**屬性是選擇性的區分大小寫。 <br/><br/>如果您指定**fileName**，hello 活動 （包括複製） 的運作方式 hello 特定檔案。<br/><br/>當**fileName**未指定，複本會包含中的所有檔案**folderPath** hello 輸入資料集。<br/><br/>當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱的資料格式 hello。_Guid_.txt'。 例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt。 |否 |
| **partitionedBy** |hello **partitionedBy**是選擇性屬性。 Toospecify 動態的路徑和檔名，時間序列資料，您可以使用它。 例如，folderPath 可針對每小時的資料進行參數化。 如需詳細資訊和範例，請參閱[hello partitionedBy 屬性](#using-partitionedby-property)。 |否 |
| **format** | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**，和**ParquetFormat**。 設定 hello**類型**下的屬性**格式**tooone 這些值。 如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [ORC 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節 hello [Azure Data Factory 支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)發行項。 <br><br> 如果您想要 toocopy 檔案 」 做為-是 「 檔案型存放區之間 （二進位複製），略過 hello`format`這兩個輸入和輸出資料集定義中的區段。 |否 |
| **compression** | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：GZip、Deflate、BZip2 及 ZipDeflate。 支援的層級為 **Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 支援的檔案與壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

### <a name="hello-partitionedby-property"></a>hello partitionedBy 屬性
您可以指定動態**folderPath**和**fileName**屬性時間序列資料以 hello **partitionedBy**屬性、 Data Factory 函數和系統變數。 如需詳細資訊，請參閱 hello [Azure Data Factory-函式和系統變數](data-factory-functions-variables.md)發行項。


在下列範例，hello `{Slice}` hello hello Data Factory 系統變數值會取代`SliceStart`hello 格式指定 (`yyyyMMddHH`)。 hello 名稱`SliceStart`參考 toohello hello 配量的開始時間。 hello`folderPath`屬性是不同的每個配量，如下所示`wikidatagateway/wikisampledataout/2014100103`或`wikidatagateway/wikisampledataout/2014100104`。

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

在下列範例、 hello 年、 月、 日和時間的 hello`SliceStart`會擷取至不同的變數所使用的 hello`folderPath`和`fileName`屬性：
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
如需有關時間序列資料集的詳細資訊，排程，以及配量，請參閱 hello [Azure Data Factory 中的資料集](data-factory-create-datasets.md)和[Data Factory 排程和執行](data-factory-scheduling-and-execution.md)文件。 


## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

hello hello 中可用屬性**typeProperties** > 一節的活動會隨每個活動類型。 複製活動，它們而異的來源與接收的 hello 類型。

**AzureDataLakeStoreSource**支援下列屬性在 hello hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| **recursive** |指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。 |True (預設值)、False |否 |


**AzureDataLakeStoreSink**支援下列屬性在 hello hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| **copyBehavior** |指定 hello 複製行為。 |<b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。 hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。<br/><br/><b>FlattenHierarchy</b>: hello 第一個層級的 hello 目標資料夾中建立 hello 來源資料夾中的所有檔案。 會使用自動產生名稱建立 hello 目標檔案。<br/><br/><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。 如果 hello 檔案或 blob 名稱指定，則 hello 合併的檔案名稱是 hello 指定的名稱。 否則，hello 檔案名稱是自動產生。 |否 |

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

## <a name="supported-file-and-compression-formats"></a>支援的檔案和壓縮格式
如需詳細資訊，請參閱 hello [Azure Data Factory 中的檔案及壓縮格式](data-factory-supported-file-and-compression-formats.md)發行項。

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>從資料湖存放區複製資料 tooand JSON 範例
下列範例中的 hello 提供範例 JSON 定義。 您可以使用這些範例定義 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 hello 範例顯示如何從資料湖存放區和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，資料可以複製_直接_從任何支援的 hello 接收的 hello 來源 tooany。 如需詳細資訊，請參閱"支援資料存放區和格式 」 的 hello 一節中 hello[使用複製活動移動資料](data-factory-data-movement-activities.md)發行項。  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>範例： 將資料從 Azure Blob 儲存體 tooAzure 資料湖存放區複製
本節中的 hello 範例程式碼顯示：

* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [AzureDataLakeStore](#linked-service-properties)類型的連結服務。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureDataLakeStore](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [AzureDataLakeStoreSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例顯示時間序列資料從 Azure Blob 儲存體的方式複製 tooData 湖存放區的每個小時。 

**Azure 儲存體連結服務**

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

**Azure Data Lake Store 已連結的服務**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> 設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。
>

**Azure Blob 輸入資料集**

在下列範例的 hello，資料從挑選新的 blob 每小時 (`"frequency": "Hour", "interval": 1`)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 年、 月和日數部分的 hello 開始時間，則會使用 hello 資料夾路徑。 hello 檔案名稱會使用 hello hello 部分開始時間的小時。 hello `"external": true` hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時，設定會通知 hello Data Factory 服務。

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

**Azure Data Lake Store 輸出資料集**

下列範例複製資料 tooData 湖存放區的 hello。 會複製新的資料湖存放區 tooData 每小時。

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**具有 Blob 來源和 Data Lake Store 接收器的管線中的複製活動**

在下列範例的 hello，hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集。 hello 複製活動會排定的 toorun 每小時。 在 hello 管線 JSON 定義中，hello`source`類型設定得`BlobSource`，和 hello`sink`類型設定得`AzureDataLakeStoreSink`。

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>範例： 將資料從 Azure Data Lake Store tooan Azure blob 複製
本節中的 hello 範例程式碼顯示：

* [AzureDataLakeStore](#linked-service-properties)類型的連結服務。
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [AzureDataLakeStore](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [AzureDataLakeStoreSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 程式碼會複製時間序列資料從 Azure blob 的資料湖存放區 tooan 每小時。 

**Azure Data Lake Store 已連結的服務**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> 設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。
>

**Azure 儲存體連結服務**

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
**Azure Data Lake 輸入資料集**

在此範例中，設定`"external"`太`true`hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
**Azure Blob 輸出資料集**

在下列範例的 hello，資料會寫入 tooa 新 blob 的每個小時 (`"frequency": "Hour", "interval": 1`)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 年、 月、 日和 hello 開始時間的小時部分，則會使用 hello 資料夾路徑。

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**具有 Azure Data Lake Store 來源和 Blob 接收器的管線中的複製活動**

在下列範例的 hello，hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集。 hello 複製活動會排定的 toorun 每小時。 在 hello 管線 JSON 定義中，hello`source`類型設定得`AzureDataLakeStoreSource`，和 hello`sink`類型設定得`BlobSink`。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

您也可以在 hello 複製活動定義中，對應 hello 來源資料集 toocolumns hello 接收資料集中的資料行。 如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
toolearn 有關 hello 因素會影響複製活動效能以及如何 toooptimize，請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)發行項。
