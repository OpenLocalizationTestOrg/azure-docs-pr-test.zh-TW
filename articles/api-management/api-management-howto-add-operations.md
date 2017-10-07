---
title: "aaaHow tooadd 作業 tooan API 在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何在 Azure API 管理 tooadd 作業 tooan 應用程式開發介面。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>如何在 Azure API 管理 tooadd 作業 tooan 應用程式開發介面
您必須先加入作業，才能夠使用 API 管理中的 API。 本指南適顯示如何 tooadd 及 API 管理中設定不同類型的作業 tooan 應用程式開發介面。

## <a name="add-operation"> </a>新增作業
作業可加入與 hello 發行者入口網站中設定 tooan API。 tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

Hello 發行者入口網站，然後選取 hello 中選取 hello 所需的應用程式開發介面**作業** 索引標籤。 

![作業][api-management-operations]

按一下**Add 作業**tooadd 新作業。 hello**新作業**將會顯示與 hello**簽章**預設會選取索引標籤。

![Add operation][api-management-add-operation]

指定 hello **HTTP 指令動詞**hello 下拉式清單中選擇。

![HTTP method][api-management-http-method]

<a name="url-template"></a>

URL 片段包含一或多個 URL 路徑區段和零個或多個查詢字串參數中輸入，藉以定義 hello URL 範本。 hello URL 範本，附加的 toohello hello 應用程式開發介面，基底 URL 會識別單一 HTTP 作業。 可能包含一或多個以大括弧識別的具名變數部分。 這些變數的組件稱為範本參數，而且會動態指派時正在處理 hello API 管理平台 hello 要求從 hello 要求 URL 中擷取的值。

> hello URL 範本可以包含萬用字元模式。 例如，指定`/*`會向前復原所有要求的 HTTP 方法 toohello 回都結束服務。

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

如有需要，指定 hello**重寫 URL 範本**。 這可讓您 toouse hello 標準 URL 範本為處理傳入要求 hello 前端上的，同時呼叫 hello 後端透過根據 toohello 轉換 URL 重寫範本。 來自 hello URL 範本的範本參數應該用於 hello 重寫成範本。 hello 下列範例顯示如何在內容編碼方式 hello hello 上一個範例的 web 服務中的路徑區段可供做為查詢參數，在 hello 發行 hello 透過 API 管理平台使用 hello URL 範本的應用程式開發介面的型別。

![URL template rewrite][api-management-url-template-rewrite]

呼叫端 toohello 作業將會使用 hello 格式`/customers?customerid=ALFKI`，這將會太對應`/Customers('ALFKI')`hello 後端服務會叫用。

**顯示**名稱和**描述**提供 hello 作業的描述，而且使用的 tooprovide 文件 toohello hello 開發人員入口網站中使用此 API 的開發人員。

![說明][api-management-description]

hello 作業描述中可以指定做為純文字或 HTML hello**描述**文字方塊。

## <a name="operation-caching"> </a>作業快取
回應快取可減少 hello API 取用者，降低頻寬耗用量看得見的延遲，並減少 hello 負載 hello HTTP web 服務實作 hello 應用程式開發介面。 

tooeasily 和快速啟用快取 hello 作業中，選取 hello**快取**索引標籤上，並檢查 hello**啟用**核取方塊。

![快取][api-management-caching-tab]

**持續時間**指定 hello 時哪些 hello 作業回應會保留在 hello 快取的時間週期。 hello 預設值為 3600 秒或 1 小時。

快取索引鍵是使用的 toodifferentiate 各次回應之間，如此 hello 回應對應 tooeach 不同的快取索引鍵，會在它自己個別快取的值。 （選擇性） 輸入 特定的查詢字串參數及/或計算快取索引鍵值在 hello 時使用的 HTTP 標頭 toobe**區分的查詢字串參數**和**Vary 標頭所**文字方塊分別。 當不會指定的完整要求 URL，而且下列 HTTP 標頭值的 hello 用於快取金鑰的產生：**接受**和**Accept-charset**。

> 如需有關快取和快取原則的詳細資訊，請參閱[toocache 作業會在 Azure API 管理如何產生][How toocache operation results in Azure API Management]。
> 
> 

## <a name="request-parameters"> </a>要求參數
作業參數是在 hello 參數 索引標籤上管理。指定在 hello 參數**URL 範本**上 hello**簽章** 索引標籤會自動新增，而且可以變更只是藉由編輯 hello URL 範本。 可手動輸入其他參數。

按一下新的查詢參數，tooadd**加入查詢參數**並輸入下列資訊的 hello:

* **名稱** - 參數名稱。
* **描述**-（選擇性） hello 參數的簡短描述。
* **型別**-hello 下拉式清單中選取的參數類型。
* **值**-可以指派 toothis 參數的值。 其中一個 hello 值可標示為預設值 （選擇性）。
* **需要**-藉由檢查 hello 核取方塊，讓 hello 參數成為強制。 

![要求參數][api-management-request-parameters]

## <a name="request-body"> </a>要求本文
如果允許 hello 作業 （例如 PUT、 POST） 和要求主體，您可能會提供一個範例，它在所有 hello 支援表示格式 (例如 json、 XML)。 

> hello 要求主體使用僅供文件，但不會驗證。
> 
> 

要求本文，tooenter 切換 toohello**主體** 索引標籤。

按一下**新增表示**，開始輸入所需的內容類型名稱 (例如應用程式/json)，則會在 [hello] 下拉式清單中選取它，並貼上 hello 預期 hello 文字方塊中的 hello 選格式的要求主體範例。 

![Request body][api-management-request-body]

在其他 toorepresentations，也可以指定選擇性的文字中描述 hello**描述**文字方塊。

## <a name="responses"> </a>回應
是很好的作法 tooprovide 範例的所有狀態碼，可能會產生 hello 作業的回應。 每個狀態碼可能有一個以上的回應主體範例，各供一個 hello 支援的內容類型。 

tooadd 回應時，按一下**新增**並開始輸入 hello 所需狀態碼。 在此範例 hello 狀態程式碼是**200 確定**。 一旦 hello 程式碼顯示在 [hello] 下拉式清單中，選取它，而且 hello 回應程式碼建立和加入 tooyour 作業。

![Response code][api-management-response-code]

按一下**新增表示**，開始輸入 hello 所需的內容類型名稱 (例如應用程式/json)，然後選取在 hello 下拉式清單。

![Body content type][api-management-response-body-content-type]

Hello 選取格式貼入 hello 文字方塊 hello 回應主體範例。 

![Response body][api-management-response-body]

如有需要，新增選用的描述成 hello**描述**文字方塊。

一旦設定 hello 作業之後，按一下**儲存**。

## <a name="next-steps"> </a>後續步驟
一旦 hello 作業加入 tooan API，hello 下一個步驟為 tooassociate hello API 與產品，並將它發行，可讓開發人員可以呼叫其作業。

* [如何 toocreate 及發佈產品][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
