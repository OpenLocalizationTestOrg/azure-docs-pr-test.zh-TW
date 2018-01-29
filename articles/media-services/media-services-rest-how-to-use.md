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
ms.date: 12/05/2017
ms.author: juliako;johndeu
ms.openlocfilehash: 066959058576af830103aa98a12f0c36acfdbb14
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="media-services-operations-rest-api-overview"></a>媒體服務作業 REST API 概觀
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

**媒體服務作業的 REST** API 用來建立 Media Services 帳戶中的工作、 資產、 即時通道和其他資源。 如需詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。

Media Services 提供 REST API 可接受 JSON 或 atom + pub XML 格式。 媒體服務 REST API 需要連接到 Media Services，以及一組選擇性標頭時，每個用戶端必須傳送的特定 HTTP 標頭。 下列章節描述建立要求及接收來自媒體服務的回應時可以使用的標頭和 HTTP 指令動詞。

媒體 serivces 為 REST API 的驗證透過 Azure Active Directory 驗證文件中所述[存取 Azure Media Services API，與其他使用 Azure AD 驗證](media-services-rest-connect-with-aad.md)

## <a name="considerations"></a>注意事項

使用 REST 時須考量下列事項：

* 查詢項目時，有一次最多傳回 1000 個實體的限制，因為公用 REST v2 有 1000 個查詢結果數目的限制。 您需要使用 **Skip** 和 **Take** (.NET)/ **top** (REST)，如[此 .NET 範例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[此 REST API 範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)中所述。 
* 當使用 JSON，並指定要使用**__metadata**關鍵字 （例如，若要參考連結物件） 要求中，您必須設定**接受**標頭[詳細資訊 JSON 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)（請參閱下列範例）。 Odata 並不了解要求中的 **__metadata** 屬性，除非您將它設為 verbose。  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.17
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>媒體服務支援的標準 HTTP 要求標頭
您對媒體服務每次呼叫，有一組必須在要求中包含的必要標頭，以及一組可能會想要包含的選擇性標頭。 下表列出必要的標頭：

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| Authorization |Bearer |Bearer 是唯一接受的授權機制。 此值也必須包含 Azure Active Directory 所提供的存取權杖。 |
| x-ms-version |十進位 |2.17 （或最新版本）|
| DataServiceVersion |十進位 |3.0 |
| MaxDataServiceVersion |十進位 |3.0 |

> [!NOTE]
> Media Services 會使用 OData 來公開其 REST Api，因為 DataServiceVersion 與 MaxDataServiceVersion 標頭應該包含在所有的要求。不過，如果沒有，然後目前 Media Services 會假設使用中的 DataServiceVersion 值為 3.0。
> 
> 

以下是一組選擇性標頭：

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| 日期 |RFC 1123 日期 |要求的時間戳記 |
| Accept |內容類型 |如下所示的回應要求內容類型：<p> -application/json;odata=verbose<p> - application/atom+xml<p> 回應可能會有不同的內容類型，如 blob 擷取，成功的回應包含 blob 資料流，做為裝載的位置。 |
| Accept-Encoding |Gzip、deflate |GZIP 和 DEFLATE 編碼 (適用時)。 注意：若是大型資源，媒體服務可能會忽略此標頭，並傳回未壓縮的資料。 |
| Accept-Language |"en"、"es" 等。 |指定回應的慣用語言。 |
| Accept-Charset |字元集類型，如 "UTF-8" |預設值為 UTF-8。 |
| X-HTTP-Method |HTTP 方法 |可讓不支援 PUT 或 DELETE 等 HTTP 方法的用戶端或防火牆，透過 GET 呼叫通道傳送使用這些方法。 |
| Content-Type |內容類型 |PUT 或 POST 要求中的要求主體內容類型。 |
| client-request-id |字串 |呼叫端定義的值，識別指定的要求。 如果指定，回應訊息中將包含此值以做為對應要求的方式。 <p><p>**重要**<p>值的上限應該為 2096b (2k)。 |

## <a name="standard-http-response-headers-supported-by-media-services"></a>媒體服務支援的標準 HTTP 回應標頭
以下是一組可能會根據您所要求的資源，以及您要執行的動作而傳回給您的標頭。

| 頁首 | 類型 | 值 |
| --- | --- | --- |
| request-id |字串 |目前作業的唯一識別碼，由服務產生。 |
| client-request-id |字串 |在原始要求中，呼叫者所指定的識別碼 (如果有的話)。 |
| 日期 |RFC 1123 日期 |日期/時間處理要求。 |
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

## <a name="discover-and-browse-the-media-services-entity-model"></a>探索並瀏覽媒體服務實體模型
若要讓使用者更容易找到媒體服務實體，可以使用 $metadata 作業。 它可讓您擷取所有有效的實體類型、實體屬性、關聯、函式、動作等等。 將 $metadata 作業加入至您的媒體服務 REST API 端點的結尾，您可以存取這項探索服務。

 /api/$ 中繼資料。

如果您想要在瀏覽器檢視中繼資料，或是未在要求中包含 x-ms-version 標頭，您應該將 "?api-version=2.x" 附加到 URI 的結尾。

## <a name="authenticate-with-media-services-rest-using-azure-active-directory"></a>使用媒體服務 REST 使用 Azure Active Directory 進行驗證

REST API 上的驗證是透過 Azure Active Directory(AAD)。
如需有關如何為您的 Media Services 帳戶取得必要的驗證詳細資料，從 Azure 入口網站的詳細資訊，請參閱[存取 Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。

如需撰寫程式碼連接至使用 Azure AD 驗證的 REST API 的詳細資訊，請參閱發行項[存取 Azure Media Services API，與其他使用 Azure AD 驗證](media-services-rest-connect-with-aad.md)。

## <a name="next-steps"></a>後續步驟
若要深入了解如何使用媒體服務 REST API 與 Azure AD 驗證，請參閱[存取 Azure Media Services API，與其他使用 Azure AD 驗證](media-services-rest-connect-with-aad.md)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

