---
title: "aaaGetting Started with OpenAPI Azure 函式中的中繼資料 |Microsoft 文件"
description: "開始使用 Azure Functions 中的 OpenAPI 支援"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="fdb31-103">建立函數應用程式的 OpenAPI 2.0 (Swagger) 中繼資料 (預覽)</span><span class="sxs-lookup"><span data-stu-id="fdb31-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="fdb31-104">這份文件會引導您建立裝載於 Azure 函式上的簡單 api OpenAPI 定義的 hello 逐步程序。</span><span class="sxs-lookup"><span data-stu-id="fdb31-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="fdb31-105">OpenAPI (Swagger) 是什麼？</span><span class="sxs-lookup"><span data-stu-id="fdb31-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="fdb31-106">[Swagger 中繼資料](http://swagger.io/)是檔案，定義 hello 功能和作業模式的 API，可讓裝載各種不同的其他軟體所耗用的 REST API toobe 函式。</span><span class="sxs-lookup"><span data-stu-id="fdb31-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="fdb31-107">Microsoft 供應項目要 PowerApps 和[API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier)，以及第 3 個合作對象開發人員工具，例如[郵差](https://www.getpostman.com/docs/importing_swagger)和[許多更多封裝](http://swagger.io/tools/)全部允許使用與您 API toobeSwagger 定義。</span><span class="sxs-lookup"><span data-stu-id="fdb31-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="fdb31-108"><a name="prepare-function"></a>建立包含簡單 API 的函數</span><span class="sxs-lookup"><span data-stu-id="fdb31-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="fdb31-109">toocreate OpenAPI 定義，我們必須先 toocreate 具有簡單的應用程式開發介面的函式。</span><span class="sxs-lookup"><span data-stu-id="fdb31-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="fdb31-110">如果您已經有函式的應用程式上裝載的 API，您可以略過直線 toohello 下一節</span><span class="sxs-lookup"><span data-stu-id="fdb31-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="fdb31-111">建立新的函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb31-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="fdb31-112">[Azure 入口網站](https://portal.azure.com) > `+ New` > 搜尋「函數應用程式」</span><span class="sxs-lookup"><span data-stu-id="fdb31-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="fdb31-113">在新的函數應用程式中建立新的 HTTP 觸發程序函數</span><span class="sxs-lookup"><span data-stu-id="fdb31-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="fdb31-114">系統已經將定義非常簡單之 REST API 的程式碼，預先填入您的函數。</span><span class="sxs-lookup"><span data-stu-id="fdb31-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="fdb31-115">任何字串做為查詢參數，或在 hello 主體中傳遞 toohello 函式會傳回為"Hello {輸入}"</span><span class="sxs-lookup"><span data-stu-id="fdb31-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="fdb31-116">移 toohello `Integrate` ] 索引標籤的 [新的 HTTP 觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="fdb31-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="fdb31-117">切換`Allowed HTTP methods`太`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="fdb31-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="fdb31-118">在 `Selected HTTP methods` 中，取消選取除了 POST 之外的所有動詞。</span><span class="sxs-lookup"><span data-stu-id="fdb31-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="fdb31-119">![選取的 HTTP 方法](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="fdb31-120">此步驟日後會簡化您的 API 定義。</span><span class="sxs-lookup"><span data-stu-id="fdb31-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="fdb31-121"><a name="enable"></a>啟用 API 定義支援</span><span class="sxs-lookup"><span data-stu-id="fdb31-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="fdb31-122">瀏覽過`your function name` > `Platform Features` > `API Definition`
![定義索引標籤](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="fdb31-123">設定`API Definition Source`太`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="fdb31-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="fdb31-124">這個步驟可讓一套應用程式的函式，包括端點 toohost OpenAPI 檔案，從您的函式應用程式定義域，hello 的內嵌複本 OpenAPI 選項[OpenAPI 編輯器](http://editor.swagger.io)，和 快速入門定義產生器。</span><span class="sxs-lookup"><span data-stu-id="fdb31-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="fdb31-125">![已啟用的定義](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="fdb31-126"><a name="create-definition"></a>從範本建立 API 定義</span><span class="sxs-lookup"><span data-stu-id="fdb31-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="fdb31-127">按一下 `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="fdb31-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="fdb31-128">此步驟會掃描您 HTTP 觸發程序函式的函式應用程式，並使用 functions.json toogenerate OpenAPI 文件中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb31-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="fdb31-129">太加入作業物件`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="fdb31-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="fdb31-130">hello 快速入門 OpenAPI 文件是完整的 OpenAPI 文件大綱。它需要更多的中繼資料 toobe 完整 OpenAPI 定義，例如作業物件，以及回應範本。</span><span class="sxs-lookup"><span data-stu-id="fdb31-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="fdb31-131">hello 以下的範例作業物件已填滿/會產生取用區段、 參數物件，和回應物件。</span><span class="sxs-lookup"><span data-stu-id="fdb31-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="fdb31-132">x-ms-summary 提供 Logic Apps、Flow 和 PowerApps 中的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="fdb31-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="fdb31-133">簽出[自訂您的 Swagger 定義 powerapps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="fdb31-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="fdb31-134">按一下`save`toosave 變更![加入樣板定義](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="fdb31-135"><a name="use-definition"></a>使用 API 定義</span><span class="sxs-lookup"><span data-stu-id="fdb31-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="fdb31-136">複製您`API definition URL`並貼到新的瀏覽器索引標籤 tooview 原始 OpenAPI 文件。</span><span class="sxs-lookup"><span data-stu-id="fdb31-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="fdb31-137">您可以匯入您 OpenAPI 文件 tooany 許多工具進行測試和使用該 URL 的整合。</span><span class="sxs-lookup"><span data-stu-id="fdb31-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="fdb31-138">許多 Azure 資源都可以 tooautomatically 匯入使用您 OpenAPI doc hello 儲存函式應用程式設定中的 API 定義 URL。</span><span class="sxs-lookup"><span data-stu-id="fdb31-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="fdb31-139">Hello 的一部份`Function`API 定義的來源，我們為您更新該 url。</span><span class="sxs-lookup"><span data-stu-id="fdb31-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="fdb31-140"><a name="test-definition"></a>使用 hello Swagger UI tootest 您應用程式開發介面的定義</span><span class="sxs-lookup"><span data-stu-id="fdb31-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="fdb31-141">那里正在測試的 hello 內嵌應用程式開發介面定義編輯器 toohello UI 檢視內建的工具。</span><span class="sxs-lookup"><span data-stu-id="fdb31-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="fdb31-142">新增您的 API 金鑰，然後使用 hello`Try this operation`下的每個方法。</span><span class="sxs-lookup"><span data-stu-id="fdb31-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="fdb31-143">hello 工具會使用您的應用程式開發介面定義 tooformat hello 要求和成功的回應會指出您定義正確。</span><span class="sxs-lookup"><span data-stu-id="fdb31-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="fdb31-144">步驟：</span><span class="sxs-lookup"><span data-stu-id="fdb31-144">Steps:</span></span>

1. <span data-ttu-id="fdb31-145">複製函數 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="fdb31-145">Copy your function API key</span></span>
    1. <span data-ttu-id="fdb31-146">在 HTTP 觸發程序函式中可以找到 hello API 金鑰`function name` > `Keys` > `Function Keys` 
  ![功能鍵](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="fdb31-147">瀏覽 toohello`API Definition`頁面。</span><span class="sxs-lookup"><span data-stu-id="fdb31-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="fdb31-148">按一下`Authenticate`hello 頂端，將您函式的 API 金鑰 toohello 安全性物件。</span><span class="sxs-lookup"><span data-stu-id="fdb31-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="fdb31-149">![OpenAPI 金鑰](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="fdb31-150">選取 `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="fdb31-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="fdb31-151">按一下`Try it out`並輸入名稱 tootest</span><span class="sxs-lookup"><span data-stu-id="fdb31-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="fdb31-152">您應該會在 `Pretty` 下看到測試結果「成功」
![API 定義測試](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="fdb31-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdb31-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb31-153">Next steps</span></span>
* [<span data-ttu-id="fdb31-154">函數中的 OpenAPI 定義概觀</span><span class="sxs-lookup"><span data-stu-id="fdb31-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="fdb31-155">閱讀 hello OpenAPI 支援的詳細資訊的完整文件。</span><span class="sxs-lookup"><span data-stu-id="fdb31-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="fdb31-156">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="fdb31-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="fdb31-157">可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="fdb31-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="fdb31-158">Azure Functions GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="fdb31-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="fdb31-159">簽出 hello 函式 GitHub toogive 我們 hello API 定義支援預覽的意見 ！</span><span class="sxs-lookup"><span data-stu-id="fdb31-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="fdb31-160">針對您想要更新的 toosee 的任何項目進行 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="fdb31-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
