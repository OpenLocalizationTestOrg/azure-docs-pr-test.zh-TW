---
title: "媒體服務作業 REST API 概觀 | Microsoft Docs"
description: "媒體服務 REST API 概觀"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-operations-rest-api-overview"></a>媒體服務作業 REST API 概觀
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

**媒體服務作業 REST** API 用於建立作業、資產、存取原則，以及媒體服務帳戶中物件上的其他作業。 如需詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。

Microsoft Azure 媒體服務會接受以 OData 為基礎的 HTTP 要求，而且可以使用詳細資訊 JSON 或 atom+pub 回應。 由於媒體服務符合 Azure 設計指導方針，因此在連線到媒體服務時，每個用戶端都必須使用一組必要的 HTTP 標頭，以及一組可以使用的選擇性標頭。 下列章節描述建立要求及接收來自媒體服務的回應時可以使用的標頭和 HTTP 指令動詞。

本主題提供如何使用 REST v2 搭配媒體服務的概觀。

## <a name="considerations"></a>考量

使用 REST 時須考量下列事項：

* 查詢項目時，有一次最多傳回 1000 個實體的限制，因為公用 REST v2 有 1000 個查詢結果數目的限制。 您需要使用 **Skip** 和 **Take** (.NET)/ **top** (REST)，如[此 .NET 範例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[此 REST API 範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)中所述。 
* 使用 JSON 並指定在要求中使用 **__metadata** 關鍵字時 (例如，為了參考連結的物件)，您「必須」將 **Accept** 標頭設為 [JSON Verbose 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (請參閱下列範例)。 Odata 並不了解要求中的 **__metadata** 屬性，除非您將它設為 verbose。  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>媒體服務支援的標準 HTTP 要求標頭
您對媒體服務每次呼叫，有一組必須在要求中包含的必要標頭，以及一組可能會想要包含的選擇性標頭。 下表列出必要標頭：

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| Authorization |Bearer |Bearer 是唯一接受的授權機制。 此值也必須包含 ACS 所提供的存取權杖。 |
| x-ms-version |十進位 |2.11 |
| DataServiceVersion |十進位 |3.0 |
| MaxDataServiceVersion |十進位 |3.0 |

> [!NOTE]
> 媒體服務使用 OData 來透過 REST API 公開其基礎資產中繼資料儲存機制，因此 DataServiceVersion 和 MaxDataServiceVersion 標頭應該包含在任何要求中。不過，如果沒有，則目前媒體服務會假設使用的 DataServiceVersion 值是 3.0。
> 
> 

以下是一組選擇性標頭：

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| Date |RFC 1123 日期 |要求的時間戳記 |
| Accept |內容類型 |如下所示的回應要求內容類型：<p> -application/json;odata=verbose<p> - application/atom+xml<p> 回應可能會有不同的內容類型，例如 Blob 擷取，成功的回應會在其中包含 Blob 資料流做為裝載。 |
| Accept-Encoding |Gzip、deflate |GZIP 和 DEFLATE 編碼 (適用時)。 注意：若是大型資源，媒體服務可能會忽略此標頭，並傳回未壓縮的資料。 |
| Accept-Language |"en"、"es" 等。 |指定回應的慣用語言。 |
| Accept-Charset |字元集類型，如 "UTF-8" |預設值為 UTF-8。 |
| X-HTTP-Method |HTTP 方法 |可讓不支援 PUT 或 DELETE 等 HTTP 方法的用戶端或防火牆，透過 GET 呼叫通道傳送使用這些方法。 |
| Content-Type |內容類型 |PUT 或 POST 要求中的要求主體內容類型。 |
| client-request-id |String |呼叫端定義的值，識別指定的要求。 如果指定，回應訊息中將包含此值以做為對應要求的方式。 <p><p>**重要**<p>值的上限應該為 2096b (2k)。 |

## <a name="standard-http-response-headers-supported-by-media-services"></a>媒體服務支援的標準 HTTP 回應標頭
以下是一組可能會根據您所要求的資源，以及您要執行的動作而傳回給您的標頭。

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| request-id |String |目前作業的唯一識別碼，由服務產生。 |
| client-request-id |String |在原始要求中，呼叫者所指定的識別碼 (如果有的話)。 |
| Date |RFC 1123 日期 |處理要求的日期。 |
| Content-Type |視情況而異 |回應主體的內容類型。 |
| Content-Encoding |視情況而異 |Gzip 或 deflate (視情況)。 |

## <a name="standard-http-verbs-supported-by-media-services"></a>媒體服務支援的標準 HTTP 指令動詞
以下是進行 HTTP 要求時，可以使用的 HTTP 指令動詞完整清單：

| 指令動詞 | 說明 |
| --- | --- |
| GET |傳回物件的目前值。 |
| POST |根據提供的資料建立物件或提交命令。 |
| PUT |取代物件，或建立具名的物件 (如果適用的話)。 |
| 刪除 |刪除物件。 |
| MERGE |以具名屬性變更來更新現有的物件。 |
| HEAD |傳回 GET 回應的物件中繼資料。 |

## <a name="discover-media-services-model"></a>探索媒體服務模型
若要讓使用者更容易找到媒體服務實體，可以使用 $metadata 作業。 它可讓您擷取所有有效的實體類型、實體屬性、關聯、函式、動作等等。 下列範例示範如何建構 URI：https://media.windows.net/API/$metadata。

如果您想要在瀏覽器檢視中繼資料，或是未在要求中包含 x-ms-version 標頭，您應該將 "?api-version=2.x" 附加到 URI 的結尾。

## <a name="connect-to-media-services"></a>連線到媒體服務

如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。 順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。 後續的呼叫必須送到新的 URI。

## <a name="next-steps"></a>後續步驟

若要使用 REST 存取 AMS API，請參閱[使用 Azure AD 驗證搭配 REST 存取 Azure 媒體服務 API](media-services-rest-connect-with-aad.md)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

