---
title: "在 Azure Functions 中使用 Proxy | Microsoft Docs"
description: "如何使用 Azure Functions Proxy 的概觀"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: cfowler
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: alkarche
ms.openlocfilehash: dd022b189783f2d8c6209a6cd656704ff144bfd6
ms.sourcegitcommit: 4256ebfe683b08fedd1a63937328931a5d35b157
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/23/2017
---
# <a name="work-with-azure-functions-proxies"></a>使用 Azure Functions Proxy

這篇文章說明如何設定與使用 Azure Functions Proxy。 這項功能可讓您在函式應用程式上指定由其他資源所實作的端點。 您可以使用這些 Proxy 將大型 API 細分為多個函式應用程式 (如同在微服務架構中)，同時仍為用戶端呈現單一的 API 介面。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE] 
> 標準 Functions 計費會套用至 Proxy 執行。 如需詳細資訊，請參閱 [Azure Functions 價格](https://azure.microsoft.com/pricing/details/functions/)。

## <a name="create"></a>建立 Proxy

本節將示範如何在 Functions 入口網站中建立 Proxy。

1. 開啟 [Azure 入口網站]，然後移至您的函式應用程式。
2. 在左側窗格中，選取 [新增 Proxy]。
3. 為您的 Proxy 提供名稱。
4. 指定 [路由範本] 和 [HTTP 方法]，以設定此函式應用程式上公開的端點。 這些參數的行為會根據 [HTTP 觸發程序]的規則。
5. 將**後端 URL** 設定為其他端點。 此端點可能是另一個函式應用程式中的函式，也可能是任何其他 API。 值不需要是靜態，且可以參考[應用程式設定]和[來自原始用戶端要求的參數]。
6. 按一下頁面底部的 [新增] 。

您的 Proxy 現在會存在做為函式應用程式上的新端點。 從用戶端的觀點而言，它相當於 Azure Functions 中的 HttpTrigger。 您可以藉由複製 Proxy URL 並使用最愛的 HTTP 用戶端來測試它，以嘗試您的新 Proxy。

## <a name="modify-requests-responses"></a>修改要求和回應

使用 Azure 函式的 Proxy，您可以修改要求與回應從後端。 這些轉換可以利用[使用變數]中所定義的變數。

### <a name="modify-backend-request"></a>修改後端要求

根據預設，後端要求會初始化為原始要求的複本。 除了設定後端 URL 之外，您也可以變更 HTTP 方法、標頭及查詢字串參數。 修改過的值可以參考[應用程式設定]和[來自原始用戶端要求的參數]。

目前，尚無修改後端要求的入口網站體驗。 若要了解如何套用這項功能，從*proxies.json*，請參閱[定義 requestOverrides 物件]。

### <a name="modify-response"></a>修改回應

根據預設，用戶端回應會初始化為後端回應的複本。 您可以對回應的狀態碼、原因說明、標頭及本文做出變更。 修改過的值可以參考[應用程式設定]、[來自原始用戶端要求的參數]，以及[來自後端回應的參數]。

目前，尚無修改回應的入口網站體驗。 若要了解如何套用這項功能，從*proxies.json*，請參閱[定義 responseOverrides 物件]。

## <a name="using-variables"></a>使用變數

Proxy 的設定不需要是靜態。 您可以使用變數從原始用戶端要求、 後端回應或應用程式設定條件。

### <a name="request-parameters"></a>參考要求參數

您可以使用要求參數作為後端 URL 屬性的輸入，或在修改要求和回應時使用。 某些參數可能繫結自基底 Proxy 設定中指定的路由範本，而其他參數可能來自連入要求的屬性。

#### <a name="route-template-parameters"></a>路由範本參數
路由範本中使用的參數可依名稱參考。 參數名稱以大括號 ("{}") 括住。

例如，如果 Proxy 的路由範本是 `/pets/{petId}`，則後端 URL 可以包含 `{petId}` 的值，如 `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}` 中所示。 如果路由範本的結尾是萬用字元，例如 `/api/{*restOfPath}`，則值 `{restOfPath}` 是連入要求之其餘路徑區段的字串表示。

#### <a name="additional-request-parameters"></a>其他要求參數
除了路由範本參數之外，設定值中也可以使用下列值：

* **{request.method}**：用於原始要求的 HTTP 方法。
* **{request.headers.\<HeaderName\>}**：可以從原始要求讀取的標頭。 以您想要讀取之標頭的名稱取代 *\<HeaderName\>*。 如果標頭沒有包含在要求之上，值將會是空字串。
* **{request.querystring.\<ParameterName\>}**：可以從原始要求讀取的查詢字串參數。 以您想要讀取之參數的名稱取代 *\<ParameterName\>*。 如果參數沒有包含在要求之上，值將會是空字串。

### <a name="response-parameters"></a>參考後端回應參數

修改對用戶端的回應時可以使用回應參數。 設定值中可以使用下列值：

* **{backend.response.statusCode}**：後端回應上所傳回的 HTTP 狀態碼。
* **{backend.response.statusReason}**：後端回應上所傳回的 HTTP 原因說明。
* **{backend.response.headers.\<HeaderName\>}**：可以從後端回應讀取的標頭。 以您想要讀取之標頭的名稱取代 *\<HeaderName\>*。 如果標頭未包含在回應中，值會是空的字串。

### <a name="use-appsettings"></a>參考應用程式設定

您也可以參考[針對函式應用程式定義的應用程式設定](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop)，只要以百分比符號 (%) 括住設定名稱即可。

例如，後端 URL *https://%ORDER_PROCESSING_HOST%/api/orders* 中會以 ORDER_PROCESSING_HOST 設定的值取代 "%ORDER_PROCESSING_HOST%"。

> [!TIP] 
> 當您有多個部署或測試環境時，請使用後端主機的應用程式設定。 這樣一來，您可以確保您一律指到右該環境的後端。

## <a name="advanced-configuration"></a>進階組態

您所設定的 proxy 會儲存在*proxies.json*位於函式應用程式目錄的根目錄中的檔案。 當您使用Functions 支援的任何[部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)時，您可以手動編輯此檔案，並部署為應用程式的一部分。 必須是 Azure 函式 Proxy 功能[啟用](#enable)来處理的檔案。 

> [!TIP] 
> 如果您有未設定其中一種部署方法，您也可使用*proxies.json*入口網站中的檔案。 移至您的函式應用程式，選取 [平台功能]，然後選取 [App Service 編輯器]。 如此一來，您可以查看函式應用程式的整個檔案結構，然後做出變更。

*Proxies.json*定義具名的 proxy 和其定義組成的 proxy 物件。 您可以選擇性地參考 [JSON 結構描述](http://json.schemastore.org/proxies)，以啟用程式碼自動完成 (如果編輯器支援的話)。 範例檔案如下所示：

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

在上述範例中，每個 Proxy 都有好記的名稱，例如 *proxy1*。 對應的 Proxy 定義物件是由下列屬性定義︰

* **matchCondition**︰必要 -- 此物件定義要求以觸發執行此 Proxy。 它包含與 [HTTP 觸發程序]共用的兩個屬性：
    * _method_：Proxy 回應的 HTTP 方法陣列。 如果未指定，Proxy 會回應路由上的所有 HTTP 方法。
    * _route_：必要 - 定義路由範本，控制 Proxy 回應哪些要求 URL。 不同於 HTTP 觸發程序，這個項目沒有預設值。
* **backendUri**︰後端資源的 URL，而其要求應該透過代理。 此值可以參考應用程式設定和來自原始用戶端要求的參數。 如果不包含這個屬性，Azure Functions 會回應 HTTP 200 OK。
* **requestOverrides**：此物件定義後端要求的轉換。 請參閱[定義 requestOverrides 物件]。
* **responseOverrides**：此物件定義用戶端回應的轉換。 請參閱[定義 responseOverrides 物件]。

> [!NOTE] 
> *路由*Azure 函式 Proxy 中的屬性就不會接受*routePrefix*函式應用程式主機組態屬性。 如果您想要包含前置詞，例如`/api`，它必須包含在*路由*屬性。

### <a name="requestOverrides"></a>定義 requestOverrides 物件

requestOverrides 物件定義呼叫後端資源時針對要求所做的變更。 該物件是由下列屬性所定義：

* **backend.request.method**： 用來呼叫後端的 HTTP 方法。
* **backend.request.querystring。\<ParameterName\>**： 您可以將呼叫後端的查詢字串參數。 以您想要設定之參數的名稱取代 *\<ParameterName\>*。 若提供空字串，則後端要求不會包含該參數。
* **backend.request.headers。\<HeaderName\>**： 您可以將呼叫後端的標頭。 以您想要設定之標頭的名稱取代 *\<HeaderName\>*。 如果您提供空字串，則後端要求不會包含該標頭。

值可以參考應用程式設定和來自原始用戶端要求的參數。

範例設定看起來可能如下：

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>定義 responseOverrides 物件

requestOverrides 物件定義針對傳回給用戶端之回應所做的變更。 該物件是由下列屬性所定義：

* **response.statusCode**：要傳回給用戶端的 HTTP 狀態碼。
* **response.statusReason**：要傳回給用戶端的 HTTP 原因說明。
* **response.body**：要傳回給用戶端之本文的字串表示。
* **response.headers.\<HeaderName\>**：在回應用戶端時可以設定的標頭。 以您想要設定之標頭的名稱取代 *\<HeaderName\>*。 如果您提供空字串，則回應不會包含該標頭。

值可以參考應用程式設定、來自原始用戶端要求的參數，以及來自後端回應的參數。

範例設定看起來可能如下：

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> 在此範例中，回應主體會直接設定，等等`backendUri`需要屬性。 此範例示範如何使用 Azure Functions Proxy 來模擬 API。

## <a name="enable"></a>啟用 Azure Functions Proxy

現在預設會啟用 Proxy！ 如果您使用較舊的 Proxy 預覽版本並已停用 Proxy，您必須手動啟用 Proxy 一次，這些 Proxy 才會執行。

1. 開啟 [Azure 入口網站]，然後移至您的函式應用程式。
2. 選取 [函式應用程式設定]。
3. 將 [啟用 Azure Functions Proxy (預覽)] 切換為 [開啟]。

您也可以在新功能可供使用時，返回這裡以更新 Proxy 執行階段。

[Azure 入口網站]: https://portal.azure.com
[HTTP 觸發程序]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
[定義 requestOverrides 物件]: #requestOverrides
[定義 responseOverrides 物件]: #responseOverrides
[應用程式設定]: #use-appsettings
[使用變數]: #using-variables
[來自原始用戶端要求的參數]: #request-parameters
[來自後端回應的參數]: #response-parameters
