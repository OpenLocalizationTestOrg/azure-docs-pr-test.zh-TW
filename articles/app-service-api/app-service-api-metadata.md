---
title: "適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料 | Microsoft Docs"
description: "了解 Azure App Service 中的 API 應用程式如何使用 Swagger 中繼資料來協助 API 探索和產生程式碼。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: 800bb9df9b957bec2c80abb3edefbaf354b549ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a><span data-ttu-id="e420e-103">適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料</span><span class="sxs-lookup"><span data-stu-id="e420e-103">App Service API Apps metadata for API discovery and code generation</span></span>
<span data-ttu-id="e420e-104">App Service API Apps 內建支援 [Swagger 2.0](http://swagger.io/) API 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e420e-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span></span> <span data-ttu-id="e420e-105">您不需要使用 Swagger，但如果您使用 Swagger，就能利用可讓探索和使用變得更加容易的 API Apps 功能。</span><span class="sxs-lookup"><span data-stu-id="e420e-105">You don't have to use Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span></span>   

## <a name="swagger-endpoint"></a><span data-ttu-id="e420e-106">Swagger 端點</span><span class="sxs-lookup"><span data-stu-id="e420e-106">Swagger endpoint</span></span>
<span data-ttu-id="e420e-107">您可以指定端點來為 API 應用程式提供 Swagger 2.0 JSON 中繼資料，做為該 API 應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="e420e-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of the API app.</span></span> <span data-ttu-id="e420e-108">端點可以與 API 應用程式的基底 URL 或絕對 URL 相關。</span><span class="sxs-lookup"><span data-stu-id="e420e-108">The endpoint can be relative to the base URL of the API app or an absolute URL.</span></span> <span data-ttu-id="e420e-109">絕對 URL 可以指向 API 應用程式以外的地方。</span><span class="sxs-lookup"><span data-stu-id="e420e-109">Absolute URLs can point outside the API app.</span></span> 

<span data-ttu-id="e420e-110">許多下游的用戶端 (例如，Visual Studio 程式碼產生和 PowerApps 的「新增 API」流程)，此 URL 必須可公開存取 (未受使用者或服務驗證所保護)。</span><span class="sxs-lookup"><span data-stu-id="e420e-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), the URL must be publicly accessible (not protected by user or service authentication).</span></span> <span data-ttu-id="e420e-111">這表示如果您是使用 App Service 驗證，而且想要從應用程式本身之中公開 API 定義，您就需要使用驗證選項，來允許匿名流量進入您的 API。</span><span class="sxs-lookup"><span data-stu-id="e420e-111">This means that if you're using App Service authentication and want to expose the API definition from within your app itself, you need to use authentication option that allows anonymous traffic to reach your API.</span></span> <span data-ttu-id="e420e-112">如需詳細資訊，請參閱 [App Service API Apps 的驗證和授權](app-service-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="e420e-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span></span>

### <a name="portal-blade"></a><span data-ttu-id="e420e-113">入口網站刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e420e-113">Portal blade</span></span>
<span data-ttu-id="e420e-114">在 [Azure 入口網站](https://portal.azure.com/)中，您可以在 [API 定義] 刀鋒視窗看到及變更端點 URL。</span><span class="sxs-lookup"><span data-stu-id="e420e-114">In the [Azure portal](https://portal.azure.com/) the endpoint URL can be seen and changed on the **API Definition** blade.</span></span>

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a><span data-ttu-id="e420e-115">Azure Resource Manager 屬性</span><span class="sxs-lookup"><span data-stu-id="e420e-115">Azure Resource Manager property</span></span>
<span data-ttu-id="e420e-116">您也可以使用 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 和 [Azure CLI](../cli-install-nodejs.md) 等命令列工具中的[資源總管](https://resources.azure.com/)或 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)，設定 API 應用程式的 API 定義。</span><span class="sxs-lookup"><span data-stu-id="e420e-116">You can also configure the API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="e420e-117">例如，在**資源總管**中移至 [訂用帳戶] > {您的訂用帳戶} > [resourceGroups] > {您的資源群組} > [提供者] > [Microsoft.Web] > [網站] > {您的網站} > [組態] > [web]，您就會看到 `apiDefinition` 屬性：</span><span class="sxs-lookup"><span data-stu-id="e420e-117">In **Resource Explorer**, go to **subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see the `apiDefinition` property:</span></span>

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

<span data-ttu-id="e420e-118">如需可設定 `apiDefinition` 屬性之 Azure Resource Manager 範本的範例，請開啟 [待辦事項清單範例應用程式中的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="e420e-118">For an example of an Azure Resource Manager template that sets the `apiDefinition` property, open the [azuredeploy.json file in the To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="e420e-119">尋找看起來如以上 JSON 範例的範本區段。</span><span class="sxs-lookup"><span data-stu-id="e420e-119">Find the section of the template that looks like the JSON sample shown above.</span></span>

### <a name="default-value"></a><span data-ttu-id="e420e-120">預設值</span><span class="sxs-lookup"><span data-stu-id="e420e-120">Default value</span></span>
<span data-ttu-id="e420e-121">當您使用 Visual Studio 建立 API 應用程式時，API 定義端點會自動設為 API 應用程式的基底 URL，加上 `/swagger/docs/v1`。</span><span class="sxs-lookup"><span data-stu-id="e420e-121">When you use Visual Studio to create an API app, the API definition endpoint is automatically set to the base URL of the API app plus `/swagger/docs/v1`.</span></span> <span data-ttu-id="e420e-122">這是 [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 封裝用來為 ASP.NET Web API 專案提供動態產生的 Swagger 中繼資料的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="e420e-122">This is the default URL that the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses to serve dynamically generated Swagger metadata for an ASP.NET Web API project.</span></span> 

## <a name="code-generation"></a><span data-ttu-id="e420e-123">產生程式碼</span><span class="sxs-lookup"><span data-stu-id="e420e-123">Code generation</span></span>
<span data-ttu-id="e420e-124">將 Swagger 整合到 Azure API 應用程式的好處之一，就是自動產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="e420e-124">One of the benefits of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="e420e-125">產生的用戶端類別讓您能更容易地撰寫會呼叫 API 應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e420e-125">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="e420e-126">您可以利用 Visual Studio，或從命令列來為 API 應用程式產生用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="e420e-126">You can generate client code for an API app by using Visual Studio or from the command line.</span></span> <span data-ttu-id="e420e-127">如需如何在 Visual Studio 中為 ASP.NET Web API 專案產生用戶端類別的相關資訊，請參閱 [開始使用 API Apps 和 ASP.NET](app-service-api-dotnet-get-started.md#codegen)。</span><span class="sxs-lookup"><span data-stu-id="e420e-127">For information about how to generate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span></span> <span data-ttu-id="e420e-128">如需如何為所有支援的語言從命令列進行這項作業的相關資訊，請參閱 GitHub.com 上 [Azure/autorest](https://github.com/azure/autorest) 儲存機制的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="e420e-128">For information about how to do it from the command line for all supported languages, see the readme file of the [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e420e-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e420e-129">Next steps</span></span>
<span data-ttu-id="e420e-130">如需逐步解說的教學課程來引導您建立、部署及使用 API 應用程式，請參閱 [開始使用 Azure App Service 中的 API Apps](app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e420e-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span></span>

<span data-ttu-id="e420e-131">如果您搭配使用 Azure API 管理與 API Apps，您可以使用 Swagger 元資料將 API 匯入 API 管理。</span><span class="sxs-lookup"><span data-stu-id="e420e-131">If you use Azure API Management with API Apps, you can use Swagger metadata to import your API into API Management.</span></span> <span data-ttu-id="e420e-132">如需詳細資訊，請參閱 [如何在 Azure API 管理中連同操作一起匯入 API 的定義](../api-management/api-management-howto-import-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e420e-132">For more information, see [How to import the definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span></span> 

