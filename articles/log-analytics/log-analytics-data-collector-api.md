---
title: "aaaLog 分析 HTTP 資料收集器 API |Microsoft 文件"
description: "您可以使用 hello 記錄分析 HTTP 資料收集器 API tooadd POST JSON 資料 toohello 記錄分析儲存機制從任何用戶端可以呼叫 hello REST API。 本文說明如何 toouse hello 應用程式開發介面，並具有方式的範例 toopublish 資料使用不同的程式語言。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>傳送資料 tooLog 分析以 hello HTTP 資料收集器 API
本文章將示範如何 toouse hello HTTP 資料收集器 API toosend 資料 tooLog 分析從 REST API 用戶端。  它說明 tooformat 資料如何收集您的指令碼或應用程式，將它包含在要求中，並已獲授權的記錄分析該要求。  提供的範例適用於 PowerShell、C# 及 Python。

## <a name="concepts"></a>概念
您可以使用 hello HTTP 資料收集器 API toosend 資料 tooLog 分析來自任何用戶端可以呼叫 REST API。  這可能是 runbook 會收集管理的 Azure 自動化中從 Azure 或其他雲端，或它的資料可能會使用記錄分析 tooconsolidate 替代的管理系統，並分析資料。

Hello 記錄分析儲存機制中的所有資料都會都儲存為特定記錄類型的記錄。  您可以格式化您資料 toosend toohello HTTP 資料收集器 API 為 JSON 中的多筆記錄。  當您送出 hello 資料時，個別的記錄會建立 hello hello 要求裝載中的每一筆記錄的儲存機制中。


![HTTP 資料收集器概觀](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>建立要求
toouse hello HTTP 資料收集器 API，您會建立包含 hello 資料 toosend JavaScript Object Notation (JSON) 的 POST 要求。  hello 接下來三個資料表 hello 屬性清單所需的每個要求。 我們將描述 hello 文章稍後的更多詳細資料中每個屬性。

### <a name="request-uri"></a>要求 URI
| 屬性 | 屬性 |
|:--- |:--- |
| 方法 |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| 內容類型 |application/json |

### <a name="request-uri-parameters"></a>要求 URI 參數
| 參數 | 說明 |
|:--- |:--- |
| CustomerID |hello hello Microsoft Operations Management Suite 工作區的唯一識別碼。 |
| 資源 |hello 應用程式開發介面資源名稱: / api/記錄檔。 |
| API 版本 |與此要求的 hello API toouse hello 版本。 目前是 2016-04-01。 |

### <a name="request-headers"></a>要求標頭
| 標頭 | 說明 |
|:--- |:--- |
| Authorization |hello 授權簽章。 稍後在 hello 文章中，您可以了解 toocreate hmac-sha256 標頭。 |
| Log-Type |指定正在提交的 hello 資料 hello 記錄類型。 目前，hello 記錄類型支援只有英文字元。 不支援數值或特殊字元。 |
| x-ms-date |hello 日期該 hello 要求處理，以 RFC 1123 格式。 |
| time-generated-field |hello 包含時間戳記 hello hello 資料項目的 hello 資料中的欄位名稱。 如果您指定欄位，則其內容會用於 **TimeGenerated**。 如果未指定此欄位，hello 預設**TimeGenerated**為 hello 時間該 hello 訊息內嵌。 hello hello 訊息欄位內容應該遵循 hello ISO 8601 格式為 MM-DDThh:mm:ssZ。 |

## <a name="authorization"></a>Authorization
任何要求 toohello 記錄分析 HTTP 資料收集器 API 必須包含授權標頭。 tooauthenticate 要求，您必須登入 hello 要求主要 hello 或 hello 提出 hello 要求 hello 工作區的次要索引鍵。 接著，將該簽章為 hello 要求的一部分。   

以下是 hello hello 授權標頭的格式：

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*工作區識別碼*hello hello Operations Management Suite 工作區的唯一識別碼。 *簽章*是[雜湊式訊息驗證碼 (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) hello 要求從建構和使用 hello 然後計算該[SHA256 演算法](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx)。 接下來，您可使用 Base64 編碼方式進行編碼。

使用此格式 tooencode hello **SharedKey**簽章字串：

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

以下是簽章字串的範例︰

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

當您擁有 hello 簽章字串，使用編碼 hello 上 hello UTF 8 編碼字串的 hmac-sha256 演算法，然後將編碼為 Base64 的 hello 結果。 使用此格式︰

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

hello 下一節中的 hello 樣本的範例程式碼 toohelp 建立授權標頭。

## <a name="request-body"></a>Request body
hello hello 訊息主體必須是 JSON。 它必須包含具有 hello 屬性名稱 / 值組的一個或多個記錄格式如下：

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

您可以使用下列格式的 hello 批次處理多個單一要求中一起記錄。 所有的 hello 記錄必須 hello 相同記錄類型。

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>記錄類型和屬性
當您送出 hello 記錄分析 HTTP 資料收集器 API 的資料，您可以定義自訂的記錄類型。 目前，您無法寫入資料 tooexisting 其他資料型別和解決方案所建立的記錄類型。 記錄分析會讀取 hello 內送資料，並接著會建立符合您輸入的 hello 值 hello 資料類型的屬性。

記錄分析 API 必須包含每個要求 toohello**記錄類型**hello 記錄類型 hello 同名的標頭。 hello 尾碼**_CL**是自動附加的 toohello 輸入的 toodistinguish 它從其他記錄類型為自訂的記錄檔的名稱。 例如，如果您輸入 hello 名稱**MyNewRecordType**，記錄分析會建立記錄與 hello 類型**MyNewRecordType_CL**。 這有助於確保使用者建立的類型名稱與目前或未來 Microsoft 解決方案隨附的類型名稱之間沒有衝突。

tooidentify 屬性的資料類型，記錄分析將後置詞 toohello 屬性名稱。 如果屬性包含 null 值，hello 屬性不會包含在此記錄中。 下表列出 hello 屬性資料型別和對應的後置詞：

| 屬性資料類型 | 尾碼 |
|:--- |:--- |
| String |_s |
| Boolean |_b |
| Double |_d |
| Date/time |_t |
| GUID |_g |

hello 記錄分析會使用每一個屬性的資料類型取決於是否 hello hello 新記錄的記錄類型已經存在。

* 如果 hello 記錄類型不存在，記錄分析就會建立一個新。 記錄分析會使用 hello 新記錄的每一個屬性 hello JSON 型別推斷 toodetermine hello 資料類型。
* 如果存在 hello 記錄類型，記錄分析就會嘗試 toocreate 新的記錄，根據現有的屬性。 如果 hello hello 新記錄中的屬性資料類型不符合，無法轉換的 toohello 現有類型，或如果 hello 記錄包含不存在的屬性，記錄分析會建立新的屬性則 hello 相關的後置詞。

例如，此提交項目會建立具有三個屬性 (**number_d**、**boolean_b** 和 **string_s**) 的記錄︰

![範例記錄 1](media/log-analytics-data-collector-api/record-01.png)

如果您送出這個下一個項目，格式化為字串的所有值，就不會變更 hello 屬性。 這些值可以是轉換的 tooexisting 資料類型：

![範例記錄 2](media/log-analytics-data-collector-api/record-02.png)

但假設再進行傳送下一步，記錄分析就必須建立 hello 新屬性**boolean_d**和**string_d**。 無法轉換這些值︰

![範例記錄 3](media/log-analytics-data-collector-api/record-03.png)

如果您再送出 hello 下列項目，建立 hello 記錄類型之前，記錄分析會使用三個屬性，建立記錄**number_s**， **boolean_s**，和**string_s**. 在此項目，每個 hello 初始值被格式化為字串：

![範例記錄 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>資料限制
有一些限制住 hello 資料張貼 toohello 記錄分析資料收集應用程式開發介面。

* 30 MB 的每個最大 post tooLog 分析資料收集器 API。 這是單一張貼項目的大小限制。 如果超過 30 MB 的單一文章中的 hello 資料，您應該先分割的 hello toosmaller 調整大小資料區塊，並同時傳送。
* 欄位值的大小上限為 32 KB。 Hello 欄位值是否大於 32 KB，hello 資料會被截斷。
* 指定類型欄位的建議數目上限為 50。 對於使用性和搜尋體驗觀點而言，這是一個實際的限制。  

## <a name="return-codes"></a>傳回碼
hello HTTP 狀態碼 200 表示已收到 hello 要求進行處理。 這表示該 hello 操作已順利完成。

下表列出 hello 整組 hello 服務可能會傳回狀態碼：

| 代碼 | 狀態 | 錯誤碼 | 說明 |
|:--- |:--- |:--- |:--- |
| 200 |OK | |已成功接受 hello 要求。 |
| 400 |不正確的要求 |InactiveCustomer |hello 工作區已關閉。 |
| 400 |不正確的要求 |InvalidApiVersion |hello 服務無法辨識您所指定的 hello API 版本。 |
| 400 |不正確的要求 |InvalidCustomerId |指定的 hello 工作區識別碼無效。 |
| 400 |不正確的要求 |InvalidDataFormat |提交的 JSON 無效。 hello 回應主體可能會包含如何 tooresolve hello 錯誤的詳細資訊。 |
| 400 |不正確的要求 |InvalidLogType |所包含的特殊字元或數字，就會指定 hello 記錄類型。 |
| 400 |不正確的要求 |MissingApiVersion |未指定 hello API 版本。 |
| 400 |不正確的要求 |MissingContentType |未指定 hello 內容類型。 |
| 400 |不正確的要求 |MissingLogType |hello 需要在未指定值的記錄類型。 |
| 400 |不正確的要求 |UnsupportedContentType |hello 內容類型未設定太**應用程式 /json**。 |
| 403 |禁止 |InvalidAuthorization |hello 服務無法 tooauthenticate hello 要求。 請確認該 hello 工作區識別碼和連線金鑰正確。 |
| 404 |找不到 | | 提供的 hello URL 不正確，或是 hello 要求太大。 |
| 429 |太多要求 | | hello 服務正遇到大量的資料從您的帳戶。 請稍後再試 hello 要求。 |
| 500 |內部伺服器錯誤 |UnspecifiedError |hello 服務發生內部錯誤。 請重試 hello 要求。 |
| 503 |服務無法使用 |ServiceUnavailable |hello 服務目前已無法使用 tooreceive 要求。 請重試您的要求。 |

## <a name="query-data"></a>查詢資料
hello 記錄分析 HTTP 資料收集器 API，使用記錄搜尋所提交的 tooquery 資料**類型**也就是等於 toohello **LogType**加上您所指定的值**_CL**. 例如，如果您使用 **MyCustomLog**，則會傳回 **Type=MyCustomLog_CL** 的所有記錄。

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> `MyCustomLog_CL`

## <a name="sample-requests"></a>範例要求
在 hello 下一步 區段中，您可以找到如何的範例使用不同的程式語言的 toosubmit 資料 toohello 記錄分析 HTTP 資料收集器 API。

如需每個範例中，執行下列步驟 hello 授權標頭的 tooset hello 變數：

1. 在 hello Operations Management Suite 入口網站中，選取 hello**設定**磚，，然後選取 hello**連線來源** 索引標籤。
2. 右側 toohello**工作區識別碼**、 選取 hello 複製圖示，並做為 hello hello 值貼 hello 識別碼**客戶 ID**變數。
3. 右側 toohello**主索引鍵**、 選取 hello 複製圖示，並做為 hello hello 值貼 hello 識別碼**共用金鑰**變數。

或者，您可以變更 hello 記錄類型和 JSON 資料的 hello 變數。

### <a name="powershell-sample"></a>PowerShell 範例
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>C# 範例
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Python 範例
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>後續步驟
- 使用 hello [Log Search API](log-analytics-log-search-api.md) tooretrieve hello 記錄分析儲存機制中的資料。
