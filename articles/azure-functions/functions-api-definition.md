---
title: "aaaOpenAPI Azure 函式中的中繼資料 |Microsoft 文件"
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="90e73-103">Azure Functions 中的 OpenAPI 2.0 中繼資料支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="90e73-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span></span>
<span data-ttu-id="90e73-104">OpenAPI 2.0 (先前稱為 Swagger) Azure 函式中的中繼資料支援是預覽功能，您可以使用 toowrite OpenAPI 2.0 定義函式應用程式內。</span><span class="sxs-lookup"><span data-stu-id="90e73-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use toowrite an OpenAPI 2.0 definition inside a function app.</span></span> <span data-ttu-id="90e73-105">您接著可以使用 hello 函式應用程式來裝載該檔案。</span><span class="sxs-lookup"><span data-stu-id="90e73-105">You can then host that file by using hello function app.</span></span>

<span data-ttu-id="90e73-106">[OpenAPI 中繼資料](http://swagger.io/)可讓主控 REST API toobe 函式供各種不同的其他軟體。</span><span class="sxs-lookup"><span data-stu-id="90e73-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="90e73-107">此軟體包含 Microsoft 供應項目，例如 PowerApps 和 hello [Azure App Service API 應用程式功能](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier)，例如協力廠商開發人員工具[郵差](https://www.getpostman.com/docs/importing_swagger)，和[許多更多封裝](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="90e73-107">This software includes Microsoft offerings like PowerApps and hello [API Apps feature of Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
><span data-ttu-id="90e73-108">我們建議您從 hello[快速入門教學課程](./functions-api-definition-getting-started.md)然後有關特定功能的詳細資訊傳回 toothis 文件 toolearn。</span><span class="sxs-lookup"><span data-stu-id="90e73-108">We recommend starting with hello [getting started tutorial](./functions-api-definition-getting-started.md) and then returning toothis document toolearn more about specific features.</span></span>

## <span data-ttu-id="90e73-109"><a name="enable"></a>啟用 OpenAPI 定義支援</span><span class="sxs-lookup"><span data-stu-id="90e73-109"><a name="enable"></a>Enable OpenAPI definition support</span></span>
<span data-ttu-id="90e73-110">您可以設定所有 OpenAPI 上 hello **API 定義**中函式應用程式的頁面**平台功能**。</span><span class="sxs-lookup"><span data-stu-id="90e73-110">You can configure all OpenAPI settings on hello **API Definition** page in your function app's **Platform features**.</span></span>

<span data-ttu-id="90e73-111">tooenable hello 產生託管的 OpenAPI 定義和快速入門的定義中，設定**API 定義來源**太**函式 （預覽）**。</span><span class="sxs-lookup"><span data-stu-id="90e73-111">tooenable hello generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** too**Function (Preview)**.</span></span> <span data-ttu-id="90e73-112">**外部 URL**允許函式 toouse OpenAPI 定義裝載存放在其他地方。</span><span class="sxs-lookup"><span data-stu-id="90e73-112">**External URL** allows your function toouse an OpenAPI definition that's hosted elsewhere.</span></span>

## <span data-ttu-id="90e73-113"><a name="generate-definition"></a> 從您的函式中繼資料產生 Swagger 基本架構</span><span class="sxs-lookup"><span data-stu-id="90e73-113"><a name="generate-definition"></a>Generate a Swagger skeleton from your function's metadata</span></span>
<span data-ttu-id="90e73-114">範本可協助您開始撰寫第一個 OpenAPI 定義。</span><span class="sxs-lookup"><span data-stu-id="90e73-114">A template can help you start writing your first OpenAPI definition.</span></span> <span data-ttu-id="90e73-115">hello 定義範本功能會建立疏鬆 OpenAPI 定義使用 hello function.json 檔案中的 hello 的所有中繼資料，每個 HTTP 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="90e73-115">hello definition template feature creates a sparse OpenAPI definition by using all hello metadata in hello function.json file for each of your HTTP trigger functions.</span></span> <span data-ttu-id="90e73-116">您將需要 toofill 中的詳細資訊，您的 API，從 hello 相關[OpenAPI 規格](http://swagger.io/specification/)，例如要求和回應的範本。</span><span class="sxs-lookup"><span data-stu-id="90e73-116">You'll need toofill in more information about your API from hello [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span></span>

<span data-ttu-id="90e73-117">如需逐步指示，請參閱 hello[快速入門教學課程](./functions-api-definition-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="90e73-117">For step-by-step instructions, see hello [getting started tutorial](./functions-api-definition-getting-started.md).</span></span>

### <span data-ttu-id="90e73-118"><a name="templates"></a>可用範本</span><span class="sxs-lookup"><span data-stu-id="90e73-118"><a name="templates"></a>Available templates</span></span>

|<span data-ttu-id="90e73-119">名稱</span><span class="sxs-lookup"><span data-stu-id="90e73-119">Name</span></span>| <span data-ttu-id="90e73-120">描述</span><span class="sxs-lookup"><span data-stu-id="90e73-120">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="90e73-121">已產生的定義</span><span class="sxs-lookup"><span data-stu-id="90e73-121">Generated Definition</span></span>|<span data-ttu-id="90e73-122">OpenAPI 具有定義 hello 最大數量來推斷從 hello 函式的現有中繼資料的資訊。</span><span class="sxs-lookup"><span data-stu-id="90e73-122">An OpenAPI definition with hello maximum amount of information that can be inferred from hello function's existing metadata.</span></span>|

### <span data-ttu-id="90e73-123"><a name="quickstart-details"></a>產生的 hello 定義中包含的中繼資料</span><span class="sxs-lookup"><span data-stu-id="90e73-123"><a name="quickstart-details"></a>Included metadata in hello generated definition</span></span>

<span data-ttu-id="90e73-124">下列表格代表 hello hello Azure 入口網站設定和 function.json 中的對應資料，所以產生的對應的 toohello Swagger 基本架構。</span><span class="sxs-lookup"><span data-stu-id="90e73-124">hello following table represents hello Azure portal settings and corresponding data in function.json as it is mapped toohello generated Swagger skeleton.</span></span>

|<span data-ttu-id="90e73-125">Swagger.json</span><span class="sxs-lookup"><span data-stu-id="90e73-125">Swagger.json</span></span>|<span data-ttu-id="90e73-126">入口網站 UI</span><span class="sxs-lookup"><span data-stu-id="90e73-126">Portal UI</span></span>|<span data-ttu-id="90e73-127">Function.json</span><span class="sxs-lookup"><span data-stu-id="90e73-127">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="90e73-128">Host</span><span class="sxs-lookup"><span data-stu-id="90e73-128">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|<span data-ttu-id="90e73-129">**函式應用程式設定** > **App Service 設定** > **概觀** > **URL**</span><span class="sxs-lookup"><span data-stu-id="90e73-129">**Function app settings** > **App Service settings** > **Overview** > **URL**</span></span>|<span data-ttu-id="90e73-130">不存在</span><span class="sxs-lookup"><span data-stu-id="90e73-130">*Not present*</span></span>
|[<span data-ttu-id="90e73-131">Paths</span><span class="sxs-lookup"><span data-stu-id="90e73-131">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|<span data-ttu-id="90e73-132">[整合] > [選取的 HTTP 方法]</span><span class="sxs-lookup"><span data-stu-id="90e73-132">**Integrate** > **Selected HTTP methods**</span></span>|<span data-ttu-id="90e73-133">繫結：路由</span><span class="sxs-lookup"><span data-stu-id="90e73-133">Bindings: Route</span></span>
|[<span data-ttu-id="90e73-134">Path Item</span><span class="sxs-lookup"><span data-stu-id="90e73-134">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|<span data-ttu-id="90e73-135">[整合] > [路由範本]</span><span class="sxs-lookup"><span data-stu-id="90e73-135">**Integrate** > **Route template**</span></span>|<span data-ttu-id="90e73-136">繫結：方法</span><span class="sxs-lookup"><span data-stu-id="90e73-136">Bindings: Methods</span></span>
|[<span data-ttu-id="90e73-137">安全性</span><span class="sxs-lookup"><span data-stu-id="90e73-137">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="90e73-138">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="90e73-138">**Keys**</span></span>|<span data-ttu-id="90e73-139">不存在</span><span class="sxs-lookup"><span data-stu-id="90e73-139">*Not present*</span></span>|
|<span data-ttu-id="90e73-140">operationID*</span><span class="sxs-lookup"><span data-stu-id="90e73-140">operationID*</span></span>|<span data-ttu-id="90e73-141">**路由 + 允許的動詞**</span><span class="sxs-lookup"><span data-stu-id="90e73-141">**Route + Allowed verbs**</span></span>|<span data-ttu-id="90e73-142">路由 + 允許的動詞</span><span class="sxs-lookup"><span data-stu-id="90e73-142">Route + Allowed Verbs</span></span>|

<span data-ttu-id="90e73-143">\*只需要整合與 PowerApps 和流程 hello 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="90e73-143">\*hello operation ID is required only for integrating with PowerApps and Flow.</span></span>
> [!NOTE]
> <span data-ttu-id="90e73-144">hello x ms 摘要延伸模組提供邏輯應用程式、 PowerApps，以及流程中的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="90e73-144">hello x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span></span>
>
> <span data-ttu-id="90e73-145">詳細資訊，請參閱 toolearn[自訂您的 Swagger 定義 powerapps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)。</span><span class="sxs-lookup"><span data-stu-id="90e73-145">toolearn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span></span>

## <span data-ttu-id="90e73-146"><a name="CICD"></a>使用 CI/CD tooset 應用程式開發介面定義</span><span class="sxs-lookup"><span data-stu-id="90e73-146"><a name="CICD"></a>Use CI/CD tooset an API definition</span></span>

 <span data-ttu-id="90e73-147">您必須啟用應用程式開發介面定義裝載 hello 入口網站中啟用原始檔控制 toomodify 您從原始檔控制的應用程式開發介面定義之前。</span><span class="sxs-lookup"><span data-stu-id="90e73-147">You must enable API definition hosting in hello portal before you enable source control toomodify your API definition from source control.</span></span> <span data-ttu-id="90e73-148">遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="90e73-148">Follow these instructions:</span></span>

1. <span data-ttu-id="90e73-149">瀏覽過**API 定義 （預覽）**函式應用程式設定中。</span><span class="sxs-lookup"><span data-stu-id="90e73-149">Browse too**API Definition (preview)** in your function app settings.</span></span>
  1. <span data-ttu-id="90e73-150">設定**API 定義來源**太**函式**。</span><span class="sxs-lookup"><span data-stu-id="90e73-150">Set **API definition source** too**Function**.</span></span>
  1. <span data-ttu-id="90e73-151">按一下**產生應用程式開發介面定義範本**然後**儲存**toocreate 稍後修改的範本定義。</span><span class="sxs-lookup"><span data-stu-id="90e73-151">Click **Generate API definition template** and then **Save** toocreate a template definition for modifying later.</span></span>
  1. <span data-ttu-id="90e73-152">請注意您的 API 定義 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="90e73-152">Note your API definition URL and key.</span></span>
1. <span data-ttu-id="90e73-153">[設定持續整合/持續部署 (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements)。</span><span class="sxs-lookup"><span data-stu-id="90e73-153">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span></span>
2. <span data-ttu-id="90e73-154">在原始檔控制中的 \site\wwwroot\.azurefunctions\swagger\swagger.json 修改 swagger.json。</span><span class="sxs-lookup"><span data-stu-id="90e73-154">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span></span>

<span data-ttu-id="90e73-155">現在，tooswagger.json 在您的儲存機制中所裝載的應用程式函式，在 hello API 定義 URL 的變更，並記下的索引鍵步驟 1.c。</span><span class="sxs-lookup"><span data-stu-id="90e73-155">Now, changes tooswagger.json in your repository are hosted by your function app at hello API definition URL and key that you noted in step 1.c.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90e73-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90e73-156">Next steps</span></span>
* <span data-ttu-id="90e73-157">[入門教學課程](functions-api-definition-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="90e73-157">[Getting started tutorial](functions-api-definition-getting-started.md).</span></span> <span data-ttu-id="90e73-158">請嘗試我們的逐步解說 toosee OpenAPI 中定義的動作。</span><span class="sxs-lookup"><span data-stu-id="90e73-158">Try our walkthrough toosee an OpenAPI definition in action.</span></span>
* <span data-ttu-id="90e73-159">[Azure Functions GitHub 存放庫](https://github.com/Azure/Azure-Functions/)。</span><span class="sxs-lookup"><span data-stu-id="90e73-159">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span></span> <span data-ttu-id="90e73-160">簽出 hello 函式儲存機制 toogive 我們 hello API 定義支援預覽的意見反應。</span><span class="sxs-lookup"><span data-stu-id="90e73-160">Check out hello Functions repository toogive us feedback on hello API definition support preview.</span></span> <span data-ttu-id="90e73-161">針對您想要更新的 toosee 的任何項目進行 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="90e73-161">Make a GitHub issue for anything you want toosee updated.</span></span>
* <span data-ttu-id="90e73-162">[Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="90e73-162">[Azure Functions developer reference](functions-reference.md).</span></span> <span data-ttu-id="90e73-163">深入了解如何撰寫函式程式碼及定義觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="90e73-163">Learn about coding functions and defining triggers and bindings.</span></span>
