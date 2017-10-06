---
title: "aaaApp Service API 應用程式中繼資料 API 探索和程式碼產生 |Microsoft 文件"
description: "了解如何在 Azure App Service API 應用程式使用 Swagger 中繼資料 toofacilitate API 探索和程式碼產生。"
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
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a><span data-ttu-id="a62fd-103">適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料</span><span class="sxs-lookup"><span data-stu-id="a62fd-103">App Service API Apps metadata for API discovery and code generation</span></span>
<span data-ttu-id="a62fd-104">App Service API Apps 內建支援 [Swagger 2.0](http://swagger.io/) API 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a62fd-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span></span> <span data-ttu-id="a62fd-105">您不需要 toouse Swagger，但如果您使用它，您可以利用 API 應用程式功能，讓探索和耗用更容易。</span><span class="sxs-lookup"><span data-stu-id="a62fd-105">You don't have toouse Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span></span>   

## <a name="swagger-endpoint"></a><span data-ttu-id="a62fd-106">Swagger 端點</span><span class="sxs-lookup"><span data-stu-id="a62fd-106">Swagger endpoint</span></span>
<span data-ttu-id="a62fd-107">您可以指定應用程式開發介面應用程式中的 hello API 應用程式的屬性會提供 Swagger 2.0 JSON 中繼資料端點。</span><span class="sxs-lookup"><span data-stu-id="a62fd-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of hello API app.</span></span> <span data-ttu-id="a62fd-108">hello 端點可以是相對 toohello hello API 應用程式基底 URL 或絕對 URL。</span><span class="sxs-lookup"><span data-stu-id="a62fd-108">hello endpoint can be relative toohello base URL of hello API app or an absolute URL.</span></span> <span data-ttu-id="a62fd-109">絕對 Url 可以指向外部 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a62fd-109">Absolute URLs can point outside hello API app.</span></span> 

<span data-ttu-id="a62fd-110">許多下游的用戶端 （例如 Visual Studio 程式碼產生和 PowerApps 「 新增應用程式開發介面 」 流程），hello URL 必須可公開存取 （不是由使用者或服務驗證保護）。</span><span class="sxs-lookup"><span data-stu-id="a62fd-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), hello URL must be publicly accessible (not protected by user or service authentication).</span></span> <span data-ttu-id="a62fd-111">這表示如果您使用的應用程式服務驗證，並想從 tooexpose hello API 定義本身的應用程式中，您需要您的 API 可讓匿名流量 tooreach toouse 驗證選項。</span><span class="sxs-lookup"><span data-stu-id="a62fd-111">This means that if you're using App Service authentication and want tooexpose hello API definition from within your app itself, you need toouse authentication option that allows anonymous traffic tooreach your API.</span></span> <span data-ttu-id="a62fd-112">如需詳細資訊，請參閱 [App Service API Apps 的驗證和授權](app-service-api-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span></span>

### <a name="portal-blade"></a><span data-ttu-id="a62fd-113">入口網站刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a62fd-113">Portal blade</span></span>
<span data-ttu-id="a62fd-114">在 hello [Azure 入口網站](https://portal.azure.com/)hello 的端點 URL 可以看到和 hello 上變更**API 定義**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a62fd-114">In hello [Azure portal](https://portal.azure.com/) hello endpoint URL can be seen and changed on hello **API Definition** blade.</span></span>

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a><span data-ttu-id="a62fd-115">Azure Resource Manager 屬性</span><span class="sxs-lookup"><span data-stu-id="a62fd-115">Azure Resource Manager property</span></span>
<span data-ttu-id="a62fd-116">您也可以藉由設定 API 應用程式的 hello API 定義 URL[資源總管](https://resources.azure.com/)或[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)在命令列工具，像是[Azure PowerShell](/powershell/azureps-cmdlets-docs)和 hello [Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-116">You can also configure hello API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="a62fd-117">在**資源總管**，跳過**訂用帳戶 > {訂用帳戶} > resourceGroups > {您的資源群組} > 提供者 > Microsoft.Web > 網站 > {您的站台} > 組態 > web**，您會看見 hello`apiDefinition`屬性：</span><span class="sxs-lookup"><span data-stu-id="a62fd-117">In **Resource Explorer**, go too**subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see hello `apiDefinition` property:</span></span>

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

<span data-ttu-id="a62fd-118">如需設定 hello Azure Resource Manager 範本的範例`apiDefinition`屬性，此時會開啟 hello [hello 待辦事項清單範例應用程式中的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-118">For an example of an Azure Resource Manager template that sets hello `apiDefinition` property, open hello [azuredeploy.json file in hello To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="a62fd-119">尋找看起來像 hello JSON 範例如上所示的 hello 範本的 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="a62fd-119">Find hello section of hello template that looks like hello JSON sample shown above.</span></span>

### <a name="default-value"></a><span data-ttu-id="a62fd-120">預設值</span><span class="sxs-lookup"><span data-stu-id="a62fd-120">Default value</span></span>
<span data-ttu-id="a62fd-121">當您使用 Visual Studio toocreate API 應用程式時，hello API 定義的端點會自動設定 toohello 加號 hello API 應用程式基底 URL `/swagger/docs/v1`。</span><span class="sxs-lookup"><span data-stu-id="a62fd-121">When you use Visual Studio toocreate an API app, hello API definition endpoint is automatically set toohello base URL of hello API app plus `/swagger/docs/v1`.</span></span> <span data-ttu-id="a62fd-122">這是 hello 預設 URL 的 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 套件的 ASP.NET Web API 專案使用 tooserve 動態產生的 Swagger 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a62fd-122">This is hello default URL that hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses tooserve dynamically generated Swagger metadata for an ASP.NET Web API project.</span></span> 

## <a name="code-generation"></a><span data-ttu-id="a62fd-123">產生程式碼</span><span class="sxs-lookup"><span data-stu-id="a62fd-123">Code generation</span></span>
<span data-ttu-id="a62fd-124">Azure API 應用程式中整合 Swagger hello 優點的其中一個是自動產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="a62fd-124">One of hello benefits of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="a62fd-125">產生的用戶端類別會讓它更容易 toowrite 程式碼呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a62fd-125">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="a62fd-126">您可以使用 Visual Studio，或從 hello 命令列，產生 API 應用程式的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="a62fd-126">You can generate client code for an API app by using Visual Studio or from hello command line.</span></span> <span data-ttu-id="a62fd-127">如需 Visual Studio 中 toogenerate 用戶端類別的 ASP.NET Web API 專案的如何資訊，請參閱[開始使用應用程式開發介面應用程式和 ASP.NET](app-service-api-dotnet-get-started.md#codegen)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-127">For information about how toogenerate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span></span> <span data-ttu-id="a62fd-128">如需如何 toodo 從 hello 命令列的所有支援的語言資訊，請參閱 hello 讀我檔案的 hello [Azure/autorest](https://github.com/azure/autorest) GitHub.com 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a62fd-128">For information about how toodo it from hello command line for all supported languages, see hello readme file of hello [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a62fd-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a62fd-129">Next steps</span></span>
<span data-ttu-id="a62fd-130">如需逐步解說的教學課程來引導您建立、部署及使用 API 應用程式，請參閱 [開始使用 Azure App Service 中的 API Apps](app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span></span>

<span data-ttu-id="a62fd-131">如果您使用 Azure API 管理 API 應用程式時，您可以使用 Swagger 中繼資料 tooimport 您的 API 到 API 管理。</span><span class="sxs-lookup"><span data-stu-id="a62fd-131">If you use Azure API Management with API Apps, you can use Swagger metadata tooimport your API into API Management.</span></span> <span data-ttu-id="a62fd-132">如需詳細資訊，請參閱[tooimport hello 的 Azure API 管理中的作業 API 定義的方式](../api-management/api-management-howto-import-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a62fd-132">For more information, see [How tooimport hello definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span></span> 

