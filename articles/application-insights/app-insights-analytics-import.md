---
title: "aaaImport Azure Application Insights 中的您資料 tooAnalytics |Microsoft 文件"
description: "匯入的應用程式遙測的靜態資料 toojoin 或匯入個別的資料流 tooquery 進行分析。"
services: application-insights
keywords: "開啟結構描述、匯入資料"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>將資料匯入分析

任何表格式資料匯入[分析](app-insights-analytics.md)，任一 toojoin 它與[Application Insights](app-insights-overview.md)從您的應用程式的遙測，或是讓您可以為不同的資料流分析。 分析是功能強大的查詢語言適合的 tooanalyzing 高容量加上資料流的遙測資料。

您可以使用自己的結構描述將資料匯入分析。 它沒有 toouse hello 標準 Application Insights 結構描述要求或追蹤等。

您可以匯入 JSON 或 DSV (以分隔符號分隔值 - 逗號、分號或定位字元) 檔案。

有三種情況下匯入 tooAnalytics 很有用：

* **加入應用程式遙測。** 例如，您可以匯入對應 Url 從您的網站 toomore 可讀取的頁面標題的資料表。 在分析，您可以建立儀表板圖表報表會顯示 hello 十個最受歡迎頁面中您的網站。 現在可以顯示 hello 而不是 hello Url 的頁面標題。
* **相互關聯應用程式遙測**與其他來源，例如網路流量、伺服器資料或 CDN 記錄檔。
* **適用於分析 tooa 不同的資料流。** Application Insights 分析是強大的工具，可搭配疏鬆、時間戳記資料流 - 在許多情況下遠優於 SQL。 如果您有來自其他來源的資料流，您可以使用分析進行分析。

傳送 tooyour 資料來源的資料很容易。 

1. （一次）定義 hello 結構描述，'data source' 中的資料。
2. （定期）上傳資料 tooAzure 儲存體，並呼叫 hello REST API toonotify 我們正在等待擷取新的資料。 在幾分鐘的時間內 hello 資料可在分析中的查詢。

hello 的 hello 上傳頻率由您定義和速度您希望您的資料 toobe 可供查詢。 它會更有效率的 tooupload 資料在較大的區塊，但不是會超過 1 GB。

> [!NOTE]
> *有許多資料來源 tooanalyze 嗎？* [*請考慮使用*logstash *tooship Application Insights 資料。*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>開始之前

您需要：

1. Microsoft Azure 中的 Application Insights 資源。

 * 如果您希望 tooanalyze 分開其他遙測資料[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。
 * 如果您是聯結或比較與已設定使用 Application Insights 的應用程式的遙測資料，您可以針對該應用程式使用 hello 資源。
 * 參與者或擁有者存取 toothat 資源。
 
2. Azure 儲存體中的 Blob。 您上傳 tooAzure 存放裝置，並分析從該處取得您的資料。 

 * 我們建議您針對 blob 建立專用的儲存體帳戶。 如果您的 blob 會共用與其他處理序，會在我們的處理程序 tooread 較長時間您的 blob。


## <a name="define-your-schema"></a>定義結構描述

您可以匯入資料之前，您必須定義*資料來源，*指定 hello 結構描述的資料。
您可以在單一的 Application Insights 資源 too50 資料來源

1. 啟動 hello 資料來源精靈。 使用 [新增資料來源] 按鈕。 或者 - 按一下右上角的 [設定] 按鈕，然後在下拉式功能表中選擇 [資料來源]。

    ![新增資料來源](./media/app-insights-analytics-import/add-new-data-source.png)

    提供新資料來源的名稱。

2. 定義您要上傳的 hello 檔案格式。

    您可以手動定義 hello 格式，或上傳範例檔。

    如果 hello 資料是以 CSV 格式，hello hello 範例的第一個資料列可以是資料行標頭。 您可以變更 hello hello 下一個步驟中的欄位名稱。

    hello 範例應該包含至少 10 個資料列或資料的記錄。

    資料行或欄位名稱應包含英數字元名稱 (不含空格或標點符號)。

    ![上傳範例檔案](./media/app-insights-analytics-import/sample-data-file.png)


3. 有 hello 精靈的檢閱 hello 結構描述。 如果範例中的 hello 類型推斷，您可能需要 hello 資料行 tooadjust hello 推斷型別。

    ![檢閱 hello 推斷結構描述](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (選擇性。)上傳結構描述定義。 請參閱下面的 hello 格式。

 * 選取時間戳記。 分析中的所有資料都必須都有時間戳記欄位。 型別必須`datetime`，但不含 toobe 名為 'timestamp'。 如果您的資料包含的日期和時間以 ISO 格式的資料行，請選擇此選項為 hello 時間戳記資料行。 否則，請選擇 "做為資料抵達 」，並 hello 匯入程序，將時間戳記欄位。

5. 建立 hello 資料來源。

### <a name="schema-definition-file-format"></a>結構描述定義檔案格式

而不是編輯 UI 中的 hello 結構描述，您可以從檔案載入 hello 結構描述定義。 hello 結構描述定義格式如下所示： 

以符號分隔的格式 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

JSON 格式 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
每個資料行被識別 hello 位置、 名稱和類型。 

* 位置 – 分隔的檔案格式，它是 hello 對應值的 hello 位置。 JSON 格式，則是 hello jpath hello 對應索引鍵。
* 名稱 – hello 顯示 hello 資料行的名稱。
* 類型 – hello 該資料行資料類型。
 
如果使用範例資料分隔的檔案格式，必須將所有資料行對應 hello 結構描述定義，然後 hello 結尾處新增新的資料行。 

JSON 可讓 hello 資料的部分對應，因此 hello 的 JSON 格式的結構描述定義不具有 toomap 範例資料中找到的每個金鑰。 它也可以將對應資料行不是 hello 範例資料的一部分。 

## <a name="import-data"></a>匯入資料

tooimport 資料，您將它上傳 tooAzure 儲存體、 建立便捷鍵，以及然後進行 REST API 呼叫。

![新增資料來源](./media/app-insights-analytics-import/analytics-upload-process.png)

您可以執行 hello 程序之後，手動或自動化的系統 toodo 它固定間隔。 您需要 toofollow 依照您想要的 tooimport 每個資料區塊。

1. Hello 資料上傳太[Azure blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 

 * Blob 可以是任何向上 too1GB 未壓縮大小。 從效能觀點來看，數百 MB 的大型 blob 很適合。
 * 您可以將它壓縮 Gzip tooimprove 上傳時間與 hello 資料 toobe 可用於查詢的延遲。 使用 hello`.gz`檔案的副檔名。
 * 基於此目的，從不同的服務會讓效能變 tooavoid 呼叫是最佳 toouse 個別儲存體帳戶。
 * 傳送資料時在高頻率，每隔幾秒，建議您使用 toouse 多超過一個儲存體帳戶，基於效能的考量。

 
2. [建立 hello blob 的共用存取簽章金鑰](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)。 hello 金鑰應該具有一天的到期時間，並提供讀取權限。
3. 請等候資料的 Application Insights REST 呼叫 toonotify。

 * 端點：`https://dc.services.visualstudio.com/v2/track`
 * HTTP 方法：POST
 * 承載：

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

hello 預留位置是：

* `Blob URI with Shared Access Key`： 取得此從 hello 程序建立金鑰。 它是特定 toohello blob。
* `Schema ID`: hello 您定義的結構描述產生的結構描述識別碼。 此 blob 中的 hello 資料應該符合 toohello 結構描述。
* `DateTime`: hello 時間在哪一個 hello 提交要求，UTC。 我們接受這些格式︰ISO8601 (例如 "2016-01-01 13:45:01")；RFC822 ("Wed, 14 Dec 16 14:57:01 +0000")；RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC")；RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000")。
* 您 `Instrumentation key` 的 Application Insights 資源。

hello 資料可在分析後幾分鐘的時間。

## <a name="error-responses"></a>錯誤回應

* **400 要求錯誤**： 指出該 hello 要求裝載無效。 勾選：
 * 修正動態檢測金鑰。
 * 有效的時間值。 它應該是 hello 現在時間-UTC 時間。
 * JSON 的 hello 事件符合 toohello 結構描述。
* **403 禁止**： 不能存取您先前曾傳送嗨 blob。 請確定該 hello 共用的存取金鑰無效，而且尚未過期。
* **404 找不到**：
 * hello blob 不存在。
 * hello sourceId 是錯誤。

Hello 回應錯誤訊息中使用更詳細的資訊。


## <a name="sample-code"></a>範例程式碼

此程式碼使用 hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 封裝。

### <a name="classes"></a>類別

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>擷取資料

針對每個 blob 使用此程式碼。 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>後續步驟

* [教學課程的 hello 記錄分析查詢語言](app-insights-analytics-tour.md)
* [使用*Logstash* toosend 資料 tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
