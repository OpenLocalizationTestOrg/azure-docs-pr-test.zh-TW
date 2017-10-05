---
title: "Azure Functions 中的 OpenAPI 中繼資料 | Microsoft Docs"
description: "Azure Functions 中的 OpenAPI 支援概觀"
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
ms.openlocfilehash: e426e56bcac30c740e86d620dadf291fe31e3e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="565ab-103">Azure Functions 中的 OpenAPI 2.0 中繼資料支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="565ab-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span></span>
<span data-ttu-id="565ab-104">Azure Functions 中的 OpenAPI 2.0 (先前稱為 Swagger) 中繼資料支援是預覽功能，可讓您用來撰寫函式應用程式內的 OpenAPI 2.0 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use to write an OpenAPI 2.0 definition inside a function app.</span></span> <span data-ttu-id="565ab-105">接著您可以使用函式應用程式裝載該檔案。</span><span class="sxs-lookup"><span data-stu-id="565ab-105">You can then host that file by using the function app.</span></span>

<span data-ttu-id="565ab-106">[OpenAPI 中繼資料](http://swagger.io/)可讓裝載 REST API 的函式供其他各種軟體使用。</span><span class="sxs-lookup"><span data-stu-id="565ab-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="565ab-107">此軟體包含諸如 PowerApps 和 [Azure App Service 的 API Apps 功能](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier)等 Microsoft 供應項目、諸如 [Postman](https://www.getpostman.com/docs/importing_swagger) 等第三方開發人員工具，以及[許多其他套件](http://swagger.io/tools/)。</span><span class="sxs-lookup"><span data-stu-id="565ab-107">This software includes Microsoft offerings like PowerApps and the [API Apps feature of Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
><span data-ttu-id="565ab-108">建議您從[入門教學課程](./functions-api-definition-getting-started.md)開始，然後再回到此文件學習更多特定的功能。</span><span class="sxs-lookup"><span data-stu-id="565ab-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span></span>

## <span data-ttu-id="565ab-109"><a name="enable"></a>啟用 OpenAPI 定義支援</span><span class="sxs-lookup"><span data-stu-id="565ab-109"><a name="enable"></a>Enable OpenAPI definition support</span></span>
<span data-ttu-id="565ab-110">您可以在函式應用程式設定的**平台功能**中的 **API 定義**頁面上，設定所有 OpenAPI 設定。</span><span class="sxs-lookup"><span data-stu-id="565ab-110">You can configure all OpenAPI settings on the **API Definition** page in your function app's **Platform features**.</span></span>

<span data-ttu-id="565ab-111">若要允許產生託管的 OpenAPI 定義和快速入門定義，請將 **API 定義來源** 設定為**函式 (預覽)**。</span><span class="sxs-lookup"><span data-stu-id="565ab-111">To enable the generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** to **Function (Preview)**.</span></span> <span data-ttu-id="565ab-112">**外部 URL** 可讓您的函式使用裝載在其他位置的 OpenAPI 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-112">**External URL** allows your function to use an OpenAPI definition that's hosted elsewhere.</span></span>

## <span data-ttu-id="565ab-113"><a name="generate-definition"></a> 從您的函式中繼資料產生 Swagger 基本架構</span><span class="sxs-lookup"><span data-stu-id="565ab-113"><a name="generate-definition"></a>Generate a Swagger skeleton from your function's metadata</span></span>
<span data-ttu-id="565ab-114">範本可協助您開始撰寫第一個 OpenAPI 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-114">A template can help you start writing your first OpenAPI definition.</span></span> <span data-ttu-id="565ab-115">定義範本功能會針對每個 HTTP 觸發程序函式，使用 function.json 中所有的中繼資料來建立鬆散的 OpenAPI 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-115">The definition template feature creates a sparse OpenAPI definition by using all the metadata in the function.json file for each of your HTTP trigger functions.</span></span> <span data-ttu-id="565ab-116">您會需要從 [OpenAPI 規格](http://swagger.io/specification/)填入 API 的更多相關資訊，例如要求和回應範本。</span><span class="sxs-lookup"><span data-stu-id="565ab-116">You'll need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span></span>

<span data-ttu-id="565ab-117">如需逐步指示，請參閱[快速入門教學課程](./functions-api-definition-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="565ab-117">For step-by-step instructions, see the [getting started tutorial](./functions-api-definition-getting-started.md).</span></span>

### <span data-ttu-id="565ab-118"><a name="templates"></a>可用範本</span><span class="sxs-lookup"><span data-stu-id="565ab-118"><a name="templates"></a>Available templates</span></span>

|<span data-ttu-id="565ab-119">名稱</span><span class="sxs-lookup"><span data-stu-id="565ab-119">Name</span></span>| <span data-ttu-id="565ab-120">描述</span><span class="sxs-lookup"><span data-stu-id="565ab-120">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="565ab-121">已產生的定義</span><span class="sxs-lookup"><span data-stu-id="565ab-121">Generated Definition</span></span>|<span data-ttu-id="565ab-122">具有可從函式現有中繼資料推斷之最大數量資訊的 OpenAPI 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-122">An OpenAPI definition with the maximum amount of information that can be inferred from the function's existing metadata.</span></span>|

### <span data-ttu-id="565ab-123"><a name="quickstart-details"></a>產生的定義中所包含之中繼資料</span><span class="sxs-lookup"><span data-stu-id="565ab-123"><a name="quickstart-details"></a>Included metadata in the generated definition</span></span>

<span data-ttu-id="565ab-124">下表顯示 Azure 入口網站設定和 function.json 中相對應的資料，如同對應到所產生的 Swagger 基本架構。</span><span class="sxs-lookup"><span data-stu-id="565ab-124">The following table represents the Azure portal settings and corresponding data in function.json as it is mapped to the generated Swagger skeleton.</span></span>

|<span data-ttu-id="565ab-125">Swagger.json</span><span class="sxs-lookup"><span data-stu-id="565ab-125">Swagger.json</span></span>|<span data-ttu-id="565ab-126">入口網站 UI</span><span class="sxs-lookup"><span data-stu-id="565ab-126">Portal UI</span></span>|<span data-ttu-id="565ab-127">Function.json</span><span class="sxs-lookup"><span data-stu-id="565ab-127">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="565ab-128">Host</span><span class="sxs-lookup"><span data-stu-id="565ab-128">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|<span data-ttu-id="565ab-129">**函式應用程式設定** > **App Service 設定** > **概觀** > **URL**</span><span class="sxs-lookup"><span data-stu-id="565ab-129">**Function app settings** > **App Service settings** > **Overview** > **URL**</span></span>|<span data-ttu-id="565ab-130">不存在</span><span class="sxs-lookup"><span data-stu-id="565ab-130">*Not present*</span></span>
|[<span data-ttu-id="565ab-131">Paths</span><span class="sxs-lookup"><span data-stu-id="565ab-131">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|<span data-ttu-id="565ab-132">[整合] > [選取的 HTTP 方法]</span><span class="sxs-lookup"><span data-stu-id="565ab-132">**Integrate** > **Selected HTTP methods**</span></span>|<span data-ttu-id="565ab-133">繫結：路由</span><span class="sxs-lookup"><span data-stu-id="565ab-133">Bindings: Route</span></span>
|[<span data-ttu-id="565ab-134">Path Item</span><span class="sxs-lookup"><span data-stu-id="565ab-134">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|<span data-ttu-id="565ab-135">[整合] > [路由範本]</span><span class="sxs-lookup"><span data-stu-id="565ab-135">**Integrate** > **Route template**</span></span>|<span data-ttu-id="565ab-136">繫結：方法</span><span class="sxs-lookup"><span data-stu-id="565ab-136">Bindings: Methods</span></span>
|[<span data-ttu-id="565ab-137">安全性</span><span class="sxs-lookup"><span data-stu-id="565ab-137">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="565ab-138">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="565ab-138">**Keys**</span></span>|<span data-ttu-id="565ab-139">不存在</span><span class="sxs-lookup"><span data-stu-id="565ab-139">*Not present*</span></span>|
|<span data-ttu-id="565ab-140">operationID*</span><span class="sxs-lookup"><span data-stu-id="565ab-140">operationID*</span></span>|<span data-ttu-id="565ab-141">**路由 + 允許的動詞**</span><span class="sxs-lookup"><span data-stu-id="565ab-141">**Route + Allowed verbs**</span></span>|<span data-ttu-id="565ab-142">路由 + 允許的動詞</span><span class="sxs-lookup"><span data-stu-id="565ab-142">Route + Allowed Verbs</span></span>|

<span data-ttu-id="565ab-143">\*只有與 PowerApps 和 Flow 整合才需要作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="565ab-143">\*The operation ID is required only for integrating with PowerApps and Flow.</span></span>
> [!NOTE]
> <span data-ttu-id="565ab-144">x-ms-summary 擴充提供 Logic Apps、Power 和 AppsFlow 中的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="565ab-144">The x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span></span>
>
> <span data-ttu-id="565ab-145">若要進一步了解，請參閱[為 PowerApps 自訂 Swagger 定義](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)。</span><span class="sxs-lookup"><span data-stu-id="565ab-145">To learn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span></span>

## <span data-ttu-id="565ab-146"><a name="CICD"></a>使用 CI/CD 設定 API 定義</span><span class="sxs-lookup"><span data-stu-id="565ab-146"><a name="CICD"></a>Use CI/CD to set an API definition</span></span>

 <span data-ttu-id="565ab-147">從原始檔控制啟用讓原始檔控制修改 API 定義之前，您必須先啟用裝載在入口網站中的 API 定義。</span><span class="sxs-lookup"><span data-stu-id="565ab-147">You must enable API definition hosting in the portal before you enable source control to modify your API definition from source control.</span></span> <span data-ttu-id="565ab-148">遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="565ab-148">Follow these instructions:</span></span>

1. <span data-ttu-id="565ab-149">瀏覽至函式應用程式設定中的 **API 定義 (預覽)**。</span><span class="sxs-lookup"><span data-stu-id="565ab-149">Browse to **API Definition (preview)** in your function app settings.</span></span>
  1. <span data-ttu-id="565ab-150">將 **API 定義來源**設定為 **Function**。</span><span class="sxs-lookup"><span data-stu-id="565ab-150">Set **API definition source** to **Function**.</span></span>
  1. <span data-ttu-id="565ab-151">依序按一下 [產生 API 定義範本]、[儲存] 可建立範本定義以供稍後修改。</span><span class="sxs-lookup"><span data-stu-id="565ab-151">Click **Generate API definition template** and then **Save** to create a template definition for modifying later.</span></span>
  1. <span data-ttu-id="565ab-152">請注意您的 API 定義 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="565ab-152">Note your API definition URL and key.</span></span>
1. <span data-ttu-id="565ab-153">[設定持續整合/持續部署 (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements)。</span><span class="sxs-lookup"><span data-stu-id="565ab-153">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span></span>
2. <span data-ttu-id="565ab-154">在原始檔控制中的 \site\wwwroot\.azurefunctions\swagger\swagger.json 修改 swagger.json。</span><span class="sxs-lookup"><span data-stu-id="565ab-154">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span></span>

<span data-ttu-id="565ab-155">現在，您對存放庫中的 swagger.json 所進行之變更，會由您在步驟 1.c 中記下的 API 定義 URL 及金鑰之函式應用程式進行裝載。</span><span class="sxs-lookup"><span data-stu-id="565ab-155">Now, changes to swagger.json in your repository are hosted by your function app at the API definition URL and key that you noted in step 1.c.</span></span>

## <a name="next-steps"></a><span data-ttu-id="565ab-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="565ab-156">Next steps</span></span>
* <span data-ttu-id="565ab-157">[入門教學課程](functions-api-definition-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="565ab-157">[Getting started tutorial](functions-api-definition-getting-started.md).</span></span> <span data-ttu-id="565ab-158">請嘗試我們的逐步解說，以查看 OpenAPI 定義實際運作。</span><span class="sxs-lookup"><span data-stu-id="565ab-158">Try our walkthrough to see an OpenAPI definition in action.</span></span>
* <span data-ttu-id="565ab-159">[Azure Functions GitHub 存放庫](https://github.com/Azure/Azure-Functions/)。</span><span class="sxs-lookup"><span data-stu-id="565ab-159">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span></span> <span data-ttu-id="565ab-160">查看 Functions 存放庫以提供我們 API 定義支援預覽的意見反應。</span><span class="sxs-lookup"><span data-stu-id="565ab-160">Check out the Functions repository to give us feedback on the API definition support preview.</span></span> <span data-ttu-id="565ab-161">針對您想在更新看到的任何功能提出 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="565ab-161">Make a GitHub issue for anything you want to see updated.</span></span>
* <span data-ttu-id="565ab-162">[Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="565ab-162">[Azure Functions developer reference](functions-reference.md).</span></span> <span data-ttu-id="565ab-163">深入了解如何撰寫函式程式碼及定義觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="565ab-163">Learn about coding functions and defining triggers and bindings.</span></span>
