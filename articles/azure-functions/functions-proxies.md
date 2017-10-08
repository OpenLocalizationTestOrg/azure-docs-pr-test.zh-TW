---
title: "使用 Azure 功能中的 proxy aaaWork |Microsoft 文件"
description: "概觀 toouse Azure 函式的 Proxy"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>使用 Azure Functions Proxy (預覽)

> [!NOTE] 
> Azure Functions Proxy 目前為預覽版。 雖然在預覽中，但是標準函式計費適用於 tooproxy 執行，它是免費的。 如需詳細資訊，請參閱 [Azure Functions 價格](https://azure.microsoft.com/pricing/details/functions/)。

這篇文章說明如何 tooconfigure 地使用 Azure 函式的 Proxy。 這項功能可讓您在函式應用程式上指定由其他資源所實作的端點。 您可以使用到多個函式應用程式 （如所示的微服務架構），這些 proxy toobreak 大型的應用程式開發介面時，仍單一的 API 介面的用戶端。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>啟用 Azure Functions Proxy

預設不會啟用 Proxy。 Hello 功能已停用，但是它們不會執行，您可以建立 proxy。 tooenable proxy hello 遵循：

1. 開啟 hello [Azure 入口網站]，並前往 tooyour 函式應用程式。
2. 選取 [函式應用程式設定]。
3. 交換器**啟用 Azure 函式 Proxy （預覽）**太**上**。

您也可以傳回以下 tooupdate hello proxy 執行階段可用時的新功能。


## <a name="create"></a>建立 Proxy

本節說明如何 toocreate proxy 中的 hello 函式的入口網站。

1. 開啟 hello [Azure 入口網站]，並前往 tooyour 函式應用程式。
2. Hello 左窗格中，選取**新 proxy**。
3. 為您的 Proxy 提供名稱。
4. 此函式應用程式上設定 hello 端點所公開，藉由指定 hello**路由範本**和**HTTP 方法**。 這些參數的運作方式的相應 toohello 規則[HTTP 觸發程序]。
5. 設定 hello**後端 URL** tooanother 端點。 此端點可能是另一個函式應用程式中的函式，也可能是任何其他 API。 hello 值不需要 toobe 靜態，而且可以參考[應用程式設定]和[來自原始用戶端要求 hello 參數]。
6. 按一下 [建立] 。

您的 Proxy 現在會存在做為函式應用程式上的新端點。 用戶端的觀點而言，它是對等 tooan HttpTrigger Azure 函式中。 藉由複製 hello Proxy URL，並使用您最愛的 HTTP 用戶端來測試它，您可以試用新的 proxy。

## <a name="modify-requests-responses"></a>修改要求和回應

使用 Azure 函式的 Proxy，您可以修改要求 tooand 回應 hello 後端。 這些轉換可以利用[使用變數]中所定義的變數。

### <a name="modify-backend-request"></a>修改 hello 後端要求

根據預設，hello 後端要求會初始化為 hello 原始要求的複本。 此外 toosetting hello 後端 URL，您可以進行變更 toohello HTTP 方法、 標頭和查詢字串參數。 hello 修改的值可以參考[應用程式設定]和[來自原始用戶端要求 hello 參數]。

目前，尚無修改後端要求的入口網站體驗。 toolearn 如何 tooapply 這項功能，從 proxies.json，請參閱[定義 requestOverrides 物件]。

### <a name="modify-response"></a>修改 hello 回應

根據預設，hello 用戶端的回應會初始化為 hello 後端回應的複本。 您可以進行變更 toohello 回應的狀態碼、 原因片語、 標頭和主體。 hello 修改的值可以參考[應用程式設定]，[來自原始用戶端要求 hello 參數]，和[hello 後端回應來自參數]。

目前，尚無修改回應的入口網站體驗。 toolearn 如何 tooapply 這項功能，從 proxies.json，請參閱[定義 responseOverrides 物件]。

## <a name="using-variables"></a>使用變數

hello 組態 proxy 不需要 toobe 靜態。 您可以條件 toouse 變數從 hello 原始要求、 hello 後端回應或應用程式設定。

### <a name="request-parameters"></a>參考要求參數

輸入 toohello 後端 URL 屬性或修改要求和回應的一部分，您可以使用要求參數。 某些參數可以從 hello 路由範本中 hello 基底的 proxy 設定，指定繫結和其他人可以來自 hello 連入要求的屬性。

#### <a name="route-template-parameters"></a>路由範本參數
Hello 路由範本中使用的參數都是由名稱所參考的可用 toobe。 hello 參數名稱會放在大括號 （{}）。

例如，如果 proxy 有路由範本，例如`/pets/{petId}`，hello 後端 URL 可以包含 hello 值`{petId}`，如同在`https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`。 如果 hello 路由範本就會終止中使用萬用字元，例如`/api/{*restOfPath}`，hello 值`{restOfPath}`是 hello 剩餘 hello 連入要求來自路徑片段的字串表示法。

#### <a name="additional-request-parameters"></a>其他要求參數
此外 toohello 路由範本參數，hello 值可用於組態值：

* **{request.method}**: hello hello 原始要求使用的 HTTP 方法。
* **{request.headers。\<HeaderName\>}**： 可讀取 hello 原始要求的標頭。 取代 *\<HeaderName\>*  hello 想 tooread hello 標頭名稱。 如果 hello 標頭未包含在 hello 要求，hello 值會是 hello 空字串。
* **{request.querystring。\<ParameterName\>}**： 可讀取 hello 原始要求的查詢字串參數。 取代 *\<ParameterName\>*  hello 想 tooread hello 參數名稱。 如果在 hello 要求不包含 hello 參數，hello 值會是 hello 空字串。

### <a name="response-parameters"></a>參考後端回應參數

回應參數可修改 hello 回應 toohello 用戶端的一部分。 hello 值可以用於組態值：

* **{backend.response.statusCode}**: hello 傳回 hello 後端回應的 HTTP 狀態碼。
* **{backend.response.statusReason}**: hello HTTP 原因片語 hello 後端回應傳回。
* **{backend.response.headers。\<HeaderName\>}**： 可讀取 hello 後端回應標頭。 取代 *\<HeaderName\>* 想 tooread hello hello 標頭名稱。 如果 hello 標頭未包含在 hello 要求，hello 值會是 hello 空字串。

### <a name="use-appsettings"></a>參考應用程式設定

您也可以參考[hello 函式應用程式定義的應用程式設定](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop)住 hello 設定名稱，加上百分比符號 （%）。

例如後, 端的 URL *https://%ORDER_PROCESSING_HOST%/api/orders*會有"%order_processing_host%"hello ORDER_PROCESSING_HOST 設定 hello 值取代。

> [!TIP] 
> 當您有多個部署或測試環境時，請使用後端主機的應用程式設定。 這樣一來，您可以確保您永遠與對話 toohello 帶回結束該環境。

## <a name="advanced-configuration"></a>進階組態

您所設定的 hello proxy 會儲存在 proxies.json 檔案，位於 hello 的函式應用程式目錄的根目錄中。 您可以手動編輯此檔案並將其部署為應用程式的一部分，當您使用任何 hello[部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)支援的函式。 hello 功能必須為[啟用](#enable)的 hello 檔案 toobe 處理。 

> [!TIP] 
> 如果您還沒有將設定 hello 部署方法之一，您也可以使用 hello 入口網站中的 hello proxies.json 檔案。 移 tooyour 函式應用程式中，選取**平台功能**，然後選取**應用程式服務編輯器**。 如此一來，您可以檢視應用程式函式的 hello 整個檔案結構，並再進行變更。

Proxies.json 是由 Proxy 物件定義，該物件包含具名 Proxy 及其定義。 您可以選擇性地參考 [JSON 結構描述](http://json.schemastore.org/proxies)，以啟用程式碼自動完成 (如果編輯器支援的話)。 範例檔案可能看起來像下列 hello:

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

每個 proxy 都具有好記的名稱，例如*proxy1* hello 前面範例中。 hello 對應的 proxy 定義物件是由下列屬性的 hello 定義：

* **matchCondition**： 需要-定義這個 proxy hello 執行觸發程序的 hello 要求的物件。 它包含與 [HTTP 觸發程序]共用的兩個屬性：
    * _方法_： 回應 hello proxy 的 hello HTTP 方法的陣列。 如果未指定，hello proxy 會回應 tooall hello 路由上的 HTTP 方法。
    * _路由_： 需要-定義 hello 路由範本，控制其要求您的 proxy Url 回應。 不同於 HTTP 觸發程序，這個項目沒有預設值。
* **backendUri**: hello hello 後端資源 toowhich hello 要求 URL 應該代理。 這個值可以從原始用戶端要求 hello 參考應用程式設定和參數。 如果不包含這個屬性，Azure Functions 會回應 HTTP 200 OK。
* **requestOverrides**： 定義轉換 toohello 後端要求的物件。 請參閱[定義 requestOverrides 物件]。
* **responseOverrides**： 定義轉換 toohello 用戶端回應的物件。 請參閱[定義 responseOverrides 物件]。

> [!NOTE] 
> hello 路由屬性 Azure 函式的 Proxy 不接受 hello routePrefix hello 函式主機組態屬性。 如果您想 tooinclude /api 例如前置詞，則它必須包含在 hello 路由屬性。

### <a name="requestOverrides"></a>定義 requestOverrides 物件

hello requestOverrides 物件會定義呼叫 hello 後端資源時提出 toohello 要求的變更。 hello 物件是由下列屬性的 hello 定義：

* **backend.request.method**: hello toocall hello 後端使用的 HTTP 方法。
* **backend.request.querystring。\<ParameterName\>**： 您可以將 hello 呼叫 toohello 後端的查詢字串參數。 取代 *\<ParameterName\>*  hello 想 tooset hello 參數名稱。 如果提供 hello 空字串，則 hello 參數不會包含在 hello 後端要求。
* **backend.request.headers。\<HeaderName\>**： 您可以將 hello 呼叫 toohello 後端的標頭。 取代 *\<HeaderName\>*  hello 想 tooset hello 標頭名稱。 如果您提供 hello 空字串，hello 標頭未包含在 hello 後端要求。

值可以從原始用戶端要求 hello 參考應用程式設定和參數。

設定範例看起來可能類似下列 hello:

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

hello requestOverrides 物件定義進行 toohello 回應已通過後 toohello 用戶端的變更。 hello 物件是由下列屬性的 hello 定義：

* **response.statusCode**: hello HTTP 狀態碼 toobe 傳回 toohello 用戶端。
* **response.statusReason**: hello HTTP 原因片語 toobe 傳回 toohello 用戶端。
* **response.body**: hello 主體 toobe hello 字串表示法傳回 toohello 用戶端。
* **response.headers。\<HeaderName\>**: hello 回應 toohello 用戶端可設定的標頭。 取代 *\<HeaderName\>*  hello 想 tooset hello 標頭名稱。 如果您提供 hello 空字串，hello 回應不包含 hello 標頭。

值可以參考 hello 後端回應應用程式設定、 從原始用戶端要求 hello、 參數和參數。

設定範例看起來可能類似下列 hello:

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
> 在此範例中，hello 主體被設定直接等等`backendUri`需要屬性。 hello 範例示範如何使用 Azure 函式 Proxy 的模擬應用程式開發介面。

[Azure 入口網站]: https://portal.azure.com
[HTTP 觸發程序]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[定義 requestOverrides 物件]: #requestOverrides
[定義 responseOverrides 物件]: #responseOverrides
[應用程式設定]: #use-appsettings
[使用變數]: #using-variables
[來自原始用戶端要求 hello 參數]: #request-parameters
[hello 後端回應來自參數]: #response-parameters
