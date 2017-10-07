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
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="2e24d-104">傳送資料 tooLog 分析以 hello HTTP 資料收集器 API</span><span class="sxs-lookup"><span data-stu-id="2e24d-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="2e24d-105">本文章將示範如何 toouse hello HTTP 資料收集器 API toosend 資料 tooLog 分析從 REST API 用戶端。</span><span class="sxs-lookup"><span data-stu-id="2e24d-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="2e24d-106">它說明 tooformat 資料如何收集您的指令碼或應用程式，將它包含在要求中，並已獲授權的記錄分析該要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="2e24d-107">提供的範例適用於 PowerShell、C# 及 Python。</span><span class="sxs-lookup"><span data-stu-id="2e24d-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="2e24d-108">概念</span><span class="sxs-lookup"><span data-stu-id="2e24d-108">Concepts</span></span>
<span data-ttu-id="2e24d-109">您可以使用 hello HTTP 資料收集器 API toosend 資料 tooLog 分析來自任何用戶端可以呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="2e24d-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="2e24d-110">這可能是 runbook 會收集管理的 Azure 自動化中從 Azure 或其他雲端，或它的資料可能會使用記錄分析 tooconsolidate 替代的管理系統，並分析資料。</span><span class="sxs-lookup"><span data-stu-id="2e24d-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="2e24d-111">Hello 記錄分析儲存機制中的所有資料都會都儲存為特定記錄類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="2e24d-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="2e24d-112">您可以格式化您資料 toosend toohello HTTP 資料收集器 API 為 JSON 中的多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="2e24d-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="2e24d-113">當您送出 hello 資料時，個別的記錄會建立 hello hello 要求裝載中的每一筆記錄的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="2e24d-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![HTTP 資料收集器概觀](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="2e24d-115">建立要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-115">Create a request</span></span>
<span data-ttu-id="2e24d-116">toouse hello HTTP 資料收集器 API，您會建立包含 hello 資料 toosend JavaScript Object Notation (JSON) 的 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="2e24d-117">hello 接下來三個資料表 hello 屬性清單所需的每個要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="2e24d-118">我們將描述 hello 文章稍後的更多詳細資料中每個屬性。</span><span class="sxs-lookup"><span data-stu-id="2e24d-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="2e24d-119">要求 URI</span><span class="sxs-lookup"><span data-stu-id="2e24d-119">Request URI</span></span>
| <span data-ttu-id="2e24d-120">屬性</span><span class="sxs-lookup"><span data-stu-id="2e24d-120">Attribute</span></span> | <span data-ttu-id="2e24d-121">屬性</span><span class="sxs-lookup"><span data-stu-id="2e24d-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e24d-122">方法</span><span class="sxs-lookup"><span data-stu-id="2e24d-122">Method</span></span> |<span data-ttu-id="2e24d-123">POST</span><span class="sxs-lookup"><span data-stu-id="2e24d-123">POST</span></span> |
| <span data-ttu-id="2e24d-124">URI</span><span class="sxs-lookup"><span data-stu-id="2e24d-124">URI</span></span> |<span data-ttu-id="2e24d-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="2e24d-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="2e24d-126">內容類型</span><span class="sxs-lookup"><span data-stu-id="2e24d-126">Content type</span></span> |<span data-ttu-id="2e24d-127">application/json</span><span class="sxs-lookup"><span data-stu-id="2e24d-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="2e24d-128">要求 URI 參數</span><span class="sxs-lookup"><span data-stu-id="2e24d-128">Request URI parameters</span></span>
| <span data-ttu-id="2e24d-129">參數</span><span class="sxs-lookup"><span data-stu-id="2e24d-129">Parameter</span></span> | <span data-ttu-id="2e24d-130">說明</span><span class="sxs-lookup"><span data-stu-id="2e24d-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e24d-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="2e24d-131">CustomerID</span></span> |<span data-ttu-id="2e24d-132">hello hello Microsoft Operations Management Suite 工作區的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2e24d-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="2e24d-133">資源</span><span class="sxs-lookup"><span data-stu-id="2e24d-133">Resource</span></span> |<span data-ttu-id="2e24d-134">hello 應用程式開發介面資源名稱: / api/記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2e24d-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="2e24d-135">API 版本</span><span class="sxs-lookup"><span data-stu-id="2e24d-135">API Version</span></span> |<span data-ttu-id="2e24d-136">與此要求的 hello API toouse hello 版本。</span><span class="sxs-lookup"><span data-stu-id="2e24d-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="2e24d-137">目前是 2016-04-01。</span><span class="sxs-lookup"><span data-stu-id="2e24d-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e24d-138">要求標頭</span><span class="sxs-lookup"><span data-stu-id="2e24d-138">Request headers</span></span>
| <span data-ttu-id="2e24d-139">標頭</span><span class="sxs-lookup"><span data-stu-id="2e24d-139">Header</span></span> | <span data-ttu-id="2e24d-140">說明</span><span class="sxs-lookup"><span data-stu-id="2e24d-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e24d-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="2e24d-141">Authorization</span></span> |<span data-ttu-id="2e24d-142">hello 授權簽章。</span><span class="sxs-lookup"><span data-stu-id="2e24d-142">hello authorization signature.</span></span> <span data-ttu-id="2e24d-143">稍後在 hello 文章中，您可以了解 toocreate hmac-sha256 標頭。</span><span class="sxs-lookup"><span data-stu-id="2e24d-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="2e24d-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="2e24d-144">Log-Type</span></span> |<span data-ttu-id="2e24d-145">指定正在提交的 hello 資料 hello 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="2e24d-146">目前，hello 記錄類型支援只有英文字元。</span><span class="sxs-lookup"><span data-stu-id="2e24d-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="2e24d-147">不支援數值或特殊字元。</span><span class="sxs-lookup"><span data-stu-id="2e24d-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="2e24d-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="2e24d-148">x-ms-date</span></span> |<span data-ttu-id="2e24d-149">hello 日期該 hello 要求處理，以 RFC 1123 格式。</span><span class="sxs-lookup"><span data-stu-id="2e24d-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="2e24d-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="2e24d-150">time-generated-field</span></span> |<span data-ttu-id="2e24d-151">hello 包含時間戳記 hello hello 資料項目的 hello 資料中的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="2e24d-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="2e24d-152">如果您指定欄位，則其內容會用於 **TimeGenerated**。</span><span class="sxs-lookup"><span data-stu-id="2e24d-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="2e24d-153">如果未指定此欄位，hello 預設**TimeGenerated**為 hello 時間該 hello 訊息內嵌。</span><span class="sxs-lookup"><span data-stu-id="2e24d-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="2e24d-154">hello hello 訊息欄位內容應該遵循 hello ISO 8601 格式為 MM-DDThh:mm:ssZ。</span><span class="sxs-lookup"><span data-stu-id="2e24d-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="2e24d-155">Authorization</span><span class="sxs-lookup"><span data-stu-id="2e24d-155">Authorization</span></span>
<span data-ttu-id="2e24d-156">任何要求 toohello 記錄分析 HTTP 資料收集器 API 必須包含授權標頭。</span><span class="sxs-lookup"><span data-stu-id="2e24d-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="2e24d-157">tooauthenticate 要求，您必須登入 hello 要求主要 hello 或 hello 提出 hello 要求 hello 工作區的次要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2e24d-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="2e24d-158">接著，將該簽章為 hello 要求的一部分。</span><span class="sxs-lookup"><span data-stu-id="2e24d-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="2e24d-159">以下是 hello hello 授權標頭的格式：</span><span class="sxs-lookup"><span data-stu-id="2e24d-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="2e24d-160">*工作區識別碼*hello hello Operations Management Suite 工作區的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2e24d-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="2e24d-161">*簽章*是[雜湊式訊息驗證碼 (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) hello 要求從建構和使用 hello 然後計算該[SHA256 演算法](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e24d-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="2e24d-162">接下來，您可使用 Base64 編碼方式進行編碼。</span><span class="sxs-lookup"><span data-stu-id="2e24d-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="2e24d-163">使用此格式 tooencode hello **SharedKey**簽章字串：</span><span class="sxs-lookup"><span data-stu-id="2e24d-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="2e24d-164">以下是簽章字串的範例︰</span><span class="sxs-lookup"><span data-stu-id="2e24d-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="2e24d-165">當您擁有 hello 簽章字串，使用編碼 hello 上 hello UTF 8 編碼字串的 hmac-sha256 演算法，然後將編碼為 Base64 的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2e24d-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="2e24d-166">使用此格式︰</span><span class="sxs-lookup"><span data-stu-id="2e24d-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="2e24d-167">hello 下一節中的 hello 樣本的範例程式碼 toohelp 建立授權標頭。</span><span class="sxs-lookup"><span data-stu-id="2e24d-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="2e24d-168">Request body</span><span class="sxs-lookup"><span data-stu-id="2e24d-168">Request body</span></span>
<span data-ttu-id="2e24d-169">hello hello 訊息主體必須是 JSON。</span><span class="sxs-lookup"><span data-stu-id="2e24d-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="2e24d-170">它必須包含具有 hello 屬性名稱 / 值組的一個或多個記錄格式如下：</span><span class="sxs-lookup"><span data-stu-id="2e24d-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="2e24d-171">您可以使用下列格式的 hello 批次處理多個單一要求中一起記錄。</span><span class="sxs-lookup"><span data-stu-id="2e24d-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="2e24d-172">所有的 hello 記錄必須 hello 相同記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-172">All hello records must be hello same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="2e24d-173">記錄類型和屬性</span><span class="sxs-lookup"><span data-stu-id="2e24d-173">Record type and properties</span></span>
<span data-ttu-id="2e24d-174">當您送出 hello 記錄分析 HTTP 資料收集器 API 的資料，您可以定義自訂的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="2e24d-175">目前，您無法寫入資料 tooexisting 其他資料型別和解決方案所建立的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="2e24d-176">記錄分析會讀取 hello 內送資料，並接著會建立符合您輸入的 hello 值 hello 資料類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e24d-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="2e24d-177">記錄分析 API 必須包含每個要求 toohello**記錄類型**hello 記錄類型 hello 同名的標頭。</span><span class="sxs-lookup"><span data-stu-id="2e24d-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="2e24d-178">hello 尾碼**_CL**是自動附加的 toohello 輸入的 toodistinguish 它從其他記錄類型為自訂的記錄檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e24d-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="2e24d-179">例如，如果您輸入 hello 名稱**MyNewRecordType**，記錄分析會建立記錄與 hello 類型**MyNewRecordType_CL**。</span><span class="sxs-lookup"><span data-stu-id="2e24d-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="2e24d-180">這有助於確保使用者建立的類型名稱與目前或未來 Microsoft 解決方案隨附的類型名稱之間沒有衝突。</span><span class="sxs-lookup"><span data-stu-id="2e24d-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="2e24d-181">tooidentify 屬性的資料類型，記錄分析將後置詞 toohello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="2e24d-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="2e24d-182">如果屬性包含 null 值，hello 屬性不會包含在此記錄中。</span><span class="sxs-lookup"><span data-stu-id="2e24d-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="2e24d-183">下表列出 hello 屬性資料型別和對應的後置詞：</span><span class="sxs-lookup"><span data-stu-id="2e24d-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="2e24d-184">屬性資料類型</span><span class="sxs-lookup"><span data-stu-id="2e24d-184">Property data type</span></span> | <span data-ttu-id="2e24d-185">尾碼</span><span class="sxs-lookup"><span data-stu-id="2e24d-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e24d-186">String</span><span class="sxs-lookup"><span data-stu-id="2e24d-186">String</span></span> |<span data-ttu-id="2e24d-187">_s</span><span class="sxs-lookup"><span data-stu-id="2e24d-187">_s</span></span> |
| <span data-ttu-id="2e24d-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="2e24d-188">Boolean</span></span> |<span data-ttu-id="2e24d-189">_b</span><span class="sxs-lookup"><span data-stu-id="2e24d-189">_b</span></span> |
| <span data-ttu-id="2e24d-190">Double</span><span class="sxs-lookup"><span data-stu-id="2e24d-190">Double</span></span> |<span data-ttu-id="2e24d-191">_d</span><span class="sxs-lookup"><span data-stu-id="2e24d-191">_d</span></span> |
| <span data-ttu-id="2e24d-192">Date/time</span><span class="sxs-lookup"><span data-stu-id="2e24d-192">Date/time</span></span> |<span data-ttu-id="2e24d-193">_t</span><span class="sxs-lookup"><span data-stu-id="2e24d-193">_t</span></span> |
| <span data-ttu-id="2e24d-194">GUID</span><span class="sxs-lookup"><span data-stu-id="2e24d-194">GUID</span></span> |<span data-ttu-id="2e24d-195">_g</span><span class="sxs-lookup"><span data-stu-id="2e24d-195">_g</span></span> |

<span data-ttu-id="2e24d-196">hello 記錄分析會使用每一個屬性的資料類型取決於是否 hello hello 新記錄的記錄類型已經存在。</span><span class="sxs-lookup"><span data-stu-id="2e24d-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="2e24d-197">如果 hello 記錄類型不存在，記錄分析就會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="2e24d-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="2e24d-198">記錄分析會使用 hello 新記錄的每一個屬性 hello JSON 型別推斷 toodetermine hello 資料類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="2e24d-199">如果存在 hello 記錄類型，記錄分析就會嘗試 toocreate 新的記錄，根據現有的屬性。</span><span class="sxs-lookup"><span data-stu-id="2e24d-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="2e24d-200">如果 hello hello 新記錄中的屬性資料類型不符合，無法轉換的 toohello 現有類型，或如果 hello 記錄包含不存在的屬性，記錄分析會建立新的屬性則 hello 相關的後置詞。</span><span class="sxs-lookup"><span data-stu-id="2e24d-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="2e24d-201">例如，此提交項目會建立具有三個屬性 (**number_d**、**boolean_b** 和 **string_s**) 的記錄︰</span><span class="sxs-lookup"><span data-stu-id="2e24d-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![範例記錄 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="2e24d-203">如果您送出這個下一個項目，格式化為字串的所有值，就不會變更 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="2e24d-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="2e24d-204">這些值可以是轉換的 tooexisting 資料類型：</span><span class="sxs-lookup"><span data-stu-id="2e24d-204">These values can be converted tooexisting data types:</span></span>

![範例記錄 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="2e24d-206">但假設再進行傳送下一步，記錄分析就必須建立 hello 新屬性**boolean_d**和**string_d**。</span><span class="sxs-lookup"><span data-stu-id="2e24d-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="2e24d-207">無法轉換這些值︰</span><span class="sxs-lookup"><span data-stu-id="2e24d-207">These values can't be converted:</span></span>

![範例記錄 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="2e24d-209">如果您再送出 hello 下列項目，建立 hello 記錄類型之前，記錄分析會使用三個屬性，建立記錄**number_s**， **boolean_s**，和**string_s**.</span><span class="sxs-lookup"><span data-stu-id="2e24d-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="2e24d-210">在此項目，每個 hello 初始值被格式化為字串：</span><span class="sxs-lookup"><span data-stu-id="2e24d-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![範例記錄 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="2e24d-212">資料限制</span><span class="sxs-lookup"><span data-stu-id="2e24d-212">Data limits</span></span>
<span data-ttu-id="2e24d-213">有一些限制住 hello 資料張貼 toohello 記錄分析資料收集應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2e24d-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="2e24d-214">30 MB 的每個最大 post tooLog 分析資料收集器 API。</span><span class="sxs-lookup"><span data-stu-id="2e24d-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="2e24d-215">這是單一張貼項目的大小限制。</span><span class="sxs-lookup"><span data-stu-id="2e24d-215">This is a size limit for a single post.</span></span> <span data-ttu-id="2e24d-216">如果超過 30 MB 的單一文章中的 hello 資料，您應該先分割的 hello toosmaller 調整大小資料區塊，並同時傳送。</span><span class="sxs-lookup"><span data-stu-id="2e24d-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="2e24d-217">欄位值的大小上限為 32 KB。</span><span class="sxs-lookup"><span data-stu-id="2e24d-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="2e24d-218">Hello 欄位值是否大於 32 KB，hello 資料會被截斷。</span><span class="sxs-lookup"><span data-stu-id="2e24d-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="2e24d-219">指定類型欄位的建議數目上限為 50。</span><span class="sxs-lookup"><span data-stu-id="2e24d-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="2e24d-220">對於使用性和搜尋體驗觀點而言，這是一個實際的限制。</span><span class="sxs-lookup"><span data-stu-id="2e24d-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="2e24d-221">傳回碼</span><span class="sxs-lookup"><span data-stu-id="2e24d-221">Return codes</span></span>
<span data-ttu-id="2e24d-222">hello HTTP 狀態碼 200 表示已收到 hello 要求進行處理。</span><span class="sxs-lookup"><span data-stu-id="2e24d-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="2e24d-223">這表示該 hello 操作已順利完成。</span><span class="sxs-lookup"><span data-stu-id="2e24d-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="2e24d-224">下表列出 hello 整組 hello 服務可能會傳回狀態碼：</span><span class="sxs-lookup"><span data-stu-id="2e24d-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="2e24d-225">代碼</span><span class="sxs-lookup"><span data-stu-id="2e24d-225">Code</span></span> | <span data-ttu-id="2e24d-226">狀態</span><span class="sxs-lookup"><span data-stu-id="2e24d-226">Status</span></span> | <span data-ttu-id="2e24d-227">錯誤碼</span><span class="sxs-lookup"><span data-stu-id="2e24d-227">Error code</span></span> | <span data-ttu-id="2e24d-228">說明</span><span class="sxs-lookup"><span data-stu-id="2e24d-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2e24d-229">200</span><span class="sxs-lookup"><span data-stu-id="2e24d-229">200</span></span> |<span data-ttu-id="2e24d-230">OK</span><span class="sxs-lookup"><span data-stu-id="2e24d-230">OK</span></span> | |<span data-ttu-id="2e24d-231">已成功接受 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="2e24d-232">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-232">400</span></span> |<span data-ttu-id="2e24d-233">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-233">Bad request</span></span> |<span data-ttu-id="2e24d-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="2e24d-234">InactiveCustomer</span></span> |<span data-ttu-id="2e24d-235">hello 工作區已關閉。</span><span class="sxs-lookup"><span data-stu-id="2e24d-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="2e24d-236">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-236">400</span></span> |<span data-ttu-id="2e24d-237">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-237">Bad request</span></span> |<span data-ttu-id="2e24d-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="2e24d-238">InvalidApiVersion</span></span> |<span data-ttu-id="2e24d-239">hello 服務無法辨識您所指定的 hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="2e24d-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="2e24d-240">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-240">400</span></span> |<span data-ttu-id="2e24d-241">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-241">Bad request</span></span> |<span data-ttu-id="2e24d-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="2e24d-242">InvalidCustomerId</span></span> |<span data-ttu-id="2e24d-243">指定的 hello 工作區識別碼無效。</span><span class="sxs-lookup"><span data-stu-id="2e24d-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="2e24d-244">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-244">400</span></span> |<span data-ttu-id="2e24d-245">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-245">Bad request</span></span> |<span data-ttu-id="2e24d-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="2e24d-246">InvalidDataFormat</span></span> |<span data-ttu-id="2e24d-247">提交的 JSON 無效。</span><span class="sxs-lookup"><span data-stu-id="2e24d-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="2e24d-248">hello 回應主體可能會包含如何 tooresolve hello 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2e24d-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="2e24d-249">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-249">400</span></span> |<span data-ttu-id="2e24d-250">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-250">Bad request</span></span> |<span data-ttu-id="2e24d-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="2e24d-251">InvalidLogType</span></span> |<span data-ttu-id="2e24d-252">所包含的特殊字元或數字，就會指定 hello 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="2e24d-253">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-253">400</span></span> |<span data-ttu-id="2e24d-254">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-254">Bad request</span></span> |<span data-ttu-id="2e24d-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="2e24d-255">MissingApiVersion</span></span> |<span data-ttu-id="2e24d-256">未指定 hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="2e24d-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="2e24d-257">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-257">400</span></span> |<span data-ttu-id="2e24d-258">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-258">Bad request</span></span> |<span data-ttu-id="2e24d-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="2e24d-259">MissingContentType</span></span> |<span data-ttu-id="2e24d-260">未指定 hello 內容類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="2e24d-261">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-261">400</span></span> |<span data-ttu-id="2e24d-262">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-262">Bad request</span></span> |<span data-ttu-id="2e24d-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="2e24d-263">MissingLogType</span></span> |<span data-ttu-id="2e24d-264">hello 需要在未指定值的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="2e24d-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="2e24d-265">400</span><span class="sxs-lookup"><span data-stu-id="2e24d-265">400</span></span> |<span data-ttu-id="2e24d-266">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-266">Bad request</span></span> |<span data-ttu-id="2e24d-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="2e24d-267">UnsupportedContentType</span></span> |<span data-ttu-id="2e24d-268">hello 內容類型未設定太**應用程式 /json**。</span><span class="sxs-lookup"><span data-stu-id="2e24d-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="2e24d-269">403</span><span class="sxs-lookup"><span data-stu-id="2e24d-269">403</span></span> |<span data-ttu-id="2e24d-270">禁止</span><span class="sxs-lookup"><span data-stu-id="2e24d-270">Forbidden</span></span> |<span data-ttu-id="2e24d-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="2e24d-271">InvalidAuthorization</span></span> |<span data-ttu-id="2e24d-272">hello 服務無法 tooauthenticate hello 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="2e24d-273">請確認該 hello 工作區識別碼和連線金鑰正確。</span><span class="sxs-lookup"><span data-stu-id="2e24d-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="2e24d-274">404</span><span class="sxs-lookup"><span data-stu-id="2e24d-274">404</span></span> |<span data-ttu-id="2e24d-275">找不到</span><span class="sxs-lookup"><span data-stu-id="2e24d-275">Not Found</span></span> | | <span data-ttu-id="2e24d-276">提供的 hello URL 不正確，或是 hello 要求太大。</span><span class="sxs-lookup"><span data-stu-id="2e24d-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="2e24d-277">429</span><span class="sxs-lookup"><span data-stu-id="2e24d-277">429</span></span> |<span data-ttu-id="2e24d-278">太多要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-278">Too Many Requests</span></span> | | <span data-ttu-id="2e24d-279">hello 服務正遇到大量的資料從您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e24d-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="2e24d-280">請稍後再試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="2e24d-281">500</span><span class="sxs-lookup"><span data-stu-id="2e24d-281">500</span></span> |<span data-ttu-id="2e24d-282">內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="2e24d-282">Internal Server Error</span></span> |<span data-ttu-id="2e24d-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="2e24d-283">UnspecifiedError</span></span> |<span data-ttu-id="2e24d-284">hello 服務發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="2e24d-284">hello service encountered an internal error.</span></span> <span data-ttu-id="2e24d-285">請重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-285">Please retry hello request.</span></span> |
| <span data-ttu-id="2e24d-286">503</span><span class="sxs-lookup"><span data-stu-id="2e24d-286">503</span></span> |<span data-ttu-id="2e24d-287">服務無法使用</span><span class="sxs-lookup"><span data-stu-id="2e24d-287">Service Unavailable</span></span> |<span data-ttu-id="2e24d-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="2e24d-288">ServiceUnavailable</span></span> |<span data-ttu-id="2e24d-289">hello 服務目前已無法使用 tooreceive 要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="2e24d-290">請重試您的要求。</span><span class="sxs-lookup"><span data-stu-id="2e24d-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="2e24d-291">查詢資料</span><span class="sxs-lookup"><span data-stu-id="2e24d-291">Query data</span></span>
<span data-ttu-id="2e24d-292">hello 記錄分析 HTTP 資料收集器 API，使用記錄搜尋所提交的 tooquery 資料**類型**也就是等於 toohello **LogType**加上您所指定的值**_CL**.</span><span class="sxs-lookup"><span data-stu-id="2e24d-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="2e24d-293">例如，如果您使用 **MyCustomLog**，則會傳回 **Type=MyCustomLog_CL** 的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="2e24d-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="2e24d-294">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="2e24d-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="2e24d-295">範例要求</span><span class="sxs-lookup"><span data-stu-id="2e24d-295">Sample requests</span></span>
<span data-ttu-id="2e24d-296">在 hello 下一步 區段中，您可以找到如何的範例使用不同的程式語言的 toosubmit 資料 toohello 記錄分析 HTTP 資料收集器 API。</span><span class="sxs-lookup"><span data-stu-id="2e24d-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="2e24d-297">如需每個範例中，執行下列步驟 hello 授權標頭的 tooset hello 變數：</span><span class="sxs-lookup"><span data-stu-id="2e24d-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="2e24d-298">在 hello Operations Management Suite 入口網站中，選取 hello**設定**磚，，然後選取 hello**連線來源** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2e24d-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="2e24d-299">右側 toohello**工作區識別碼**、 選取 hello 複製圖示，並做為 hello hello 值貼 hello 識別碼**客戶 ID**變數。</span><span class="sxs-lookup"><span data-stu-id="2e24d-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="2e24d-300">右側 toohello**主索引鍵**、 選取 hello 複製圖示，並做為 hello hello 值貼 hello 識別碼**共用金鑰**變數。</span><span class="sxs-lookup"><span data-stu-id="2e24d-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="2e24d-301">或者，您可以變更 hello 記錄類型和 JSON 資料的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="2e24d-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="2e24d-302">PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="2e24d-302">PowerShell sample</span></span>
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

### <a name="c-sample"></a><span data-ttu-id="2e24d-303">C# 範例</span><span class="sxs-lookup"><span data-stu-id="2e24d-303">C# sample</span></span>
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

### <a name="python-sample"></a><span data-ttu-id="2e24d-304">Python 範例</span><span class="sxs-lookup"><span data-stu-id="2e24d-304">Python sample</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="2e24d-305">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e24d-305">Next steps</span></span>
- <span data-ttu-id="2e24d-306">使用 hello [Log Search API](log-analytics-log-search-api.md) tooretrieve hello 記錄分析儲存機制中的資料。</span><span class="sxs-lookup"><span data-stu-id="2e24d-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
