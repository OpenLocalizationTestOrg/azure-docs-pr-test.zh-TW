---
title: "aaaMedia 服務作業的 REST API 概觀 |Microsoft 文件"
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
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>媒體服務作業 REST API 概觀
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

hello**媒體服務作業的 REST** API 用於建立媒體服務帳戶中的工作、 資產、 存取原則和其他物件上的作業。 如需詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。

Microsoft Azure 媒體服務會接受以 OData 為基礎的 HTTP 要求，而且可以使用詳細資訊 JSON 或 atom+pub 回應。 Media Services 符合 tooAzure 設計指導方針，因為沒有一組連接 tooMedia 服務時，必須使用每個用戶端的必要 HTTP 標頭，以及一組可用的選擇性標頭。 hello 下列各節說明 hello 標頭和建立要求時使用的 HTTP 動詞命令，以及從媒體服務接收回應。

本主題概要說明如何使用 Media Services toouse REST v2。

## <a name="considerations"></a>考量

使用 REST 時，適用下列考量 hello。

* 當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。 您需要 toouse**略過**和**採取**(.NET) /**頂端**(REST) 中所述[.NET 本例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[這個 REST API範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)。 
* 當使用 JSON，並指定 toouse hello **__metadata**關鍵字 hello 要求 (例如，tooreferences 連結物件)，您必須設定 hello**接受**標頭太[詳細資訊 JSON 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) （請參閱下列範例中的 hello）。 Odata 不了解 hello **__metadata** hello 屬性要求，除非 tooverbose 設定。  
  
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
您對 Media Services 的每個呼叫沒有必要的標頭，您必須在要求中包含一組與另一組選擇性標頭可能會想 tooinclude。 下列表格列出 hello hello 必要標頭：

| 標頭 | 類型 | 值 |
| --- | --- | --- |
| Authorization |Bearer |Bearer 是 hello 只接受的授權機制。 hello 值也必須包含 ACS 提供的 hello 存取權杖。 |
| x-ms-version |十進位 |2.11 |
| DataServiceVersion |十進位 |3.0 |
| MaxDataServiceVersion |十進位 |3.0 |

> [!NOTE]
> 因為媒體服務會使用 OData tooexpose 其基礎資產中繼資料儲存機制透過 REST Api，hello DataServiceVersion 與 MaxDataServiceVersion 標頭應該包含在任何要求。不過，如果沒有，然後目前 Media Services 假設使用中的 hello DataServiceVersion 值為 3.0。
> 
> 

hello 以下是一組選擇性標頭：

| 標頭 | 類型 | 值 |
| --- | --- | --- |
| Date |RFC 1123 日期 |Hello 要求的時間戳記 |
| Accept |內容類型 |hello 要求的內容類型 hello 回應 hello 如下：<p> -application/json;odata=verbose<p> - application/atom+xml<p> 回應可能會有不同的內容類型，如 blob 擷取，其中成功的回應將包含做為 hello 裝載 hello blob 資料流。 |
| Accept-Encoding |Gzip、deflate |GZIP 和 DEFLATE 編碼 (適用時)。 注意：若是大型資源，媒體服務可能會忽略此標頭，並傳回未壓縮的資料。 |
| Accept-Language |"en"、"es" 等。 |指定 hello 回應 hello 慣用語言。 |
| Accept-Charset |字元集類型，如 "UTF-8" |預設值為 UTF-8。 |
| X-HTTP-Method |HTTP 方法 |可讓用戶端或不支援 HTTP 方法，例如 PUT 或 DELETE toouse 防火牆這些方法，透過 GET 呼叫通道。 |
| Content-Type |內容類型 |內容的 PUT 或 POST 要求中的 hello 要求主體的類型。 |
| client-request-id |String |呼叫端定義的值，識別 hello 給定要求。 如果指定，將 hello 回應訊息中包含此值，做為方法 toomap hello 要求。 <p><p>**重要**<p>值的上限應該為 2096b (2k)。 |

## <a name="standard-http-response-headers-supported-by-media-services"></a>媒體服務支援的標準 HTTP 回應標頭
hello 以下是一組可能會傳回根據您所要求的 hello 資源 tooyou 和 hello 適合 tooperform 的動作標頭。

| 標頭 | 類型 | 值 |
| --- | --- | --- |
| request-id |String |Hello 目前的作業，服務產生的唯一識別碼。 |
| client-request-id |String |如果有的話，hello 呼叫端，在 hello 原始要求中，指定識別項。 |
| Date |RFC 1123 日期 |hello 日期該 hello 要求處理。 |
| Content-Type |視情況而異 |hello hello 回應主體的內容類型。 |
| Content-Encoding |視情況而異 |Gzip 或 deflate (視情況)。 |

## <a name="standard-http-verbs-supported-by-media-services"></a>媒體服務支援的標準 HTTP 指令動詞
hello 下列是可以在提出 HTTP 要求時使用的 HTTP 動詞命令的完整清單：

| 指令動詞 | 說明 |
| --- | --- |
| GET |傳回 hello 物件的目前值。 |
| POST |建立基礎提供，hello 資料的物件，或提交的命令。 |
| PUT |取代物件，或建立具名的物件 (如果適用的話)。 |
| 刪除 |刪除物件。 |
| MERGE |以具名屬性變更來更新現有的物件。 |
| HEAD |傳回 GET 回應的物件中繼資料。 |

## <a name="discover-media-services-model"></a>探索媒體服務模型
可以使用 toomake 媒體服務實體更容易找到 hello $metadata 作業。 它可讓您 tooretrieve 所有有效的實體類型、 實體屬性、 關聯、 函數、 動作和等等。 hello 下列範例示範如何 tooconstruct hello URI: https://media.windows.net/API/$ 中繼資料。

您應該附加"？ api version=2.x"toohello 結尾 hello URI，如果您想要在瀏覽器，tooview hello 中繼資料或不在要求中包含 hello x ms 版本標頭。

## <a name="connect-toomedia-services"></a>TooMedia 服務連接

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

## <a name="next-steps"></a>後續步驟

tooaccess AMS 應用程式開發介面與其他部分，請參閱[使用 Azure AD 驗證 tooaccess hello Azure 媒體服務 API 與其餘](media-services-rest-connect-with-aad.md)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

