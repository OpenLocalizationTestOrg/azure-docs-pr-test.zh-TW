---
title: "建立 Azure Logic Apps 的部署範本 | Microsoft Docs"
description: "建立 Azure Resource Manager 範本以進行邏輯應用程式部署和發行管理"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9cfbb294010d48deaf4b4c78c6a6bcd59a387d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a><span data-ttu-id="aa352-103">建立範本以進行邏輯應用程式部署和發行管理</span><span class="sxs-lookup"><span data-stu-id="aa352-103">Create templates for logic apps deployment and release management</span></span>

<span data-ttu-id="aa352-104">建立邏輯應用程式之後，您可能想要將其建立為 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="aa352-104">After a logic app has been created, you might want to create it as an Azure Resource Manager template.</span></span>
<span data-ttu-id="aa352-105">如此一來，您就可以輕鬆地將邏輯應用程式部署到您可能需要在其中用到它的任何環境或資源群組。</span><span class="sxs-lookup"><span data-stu-id="aa352-105">This way, you can easily deploy the logic app to any environment or resource group where you might need it.</span></span>
<span data-ttu-id="aa352-106">如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)和[使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="aa352-106">For more about Resource Manager templates, see [authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) and [deploying resources by using Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="logic-app-deployment-template"></a><span data-ttu-id="aa352-107">邏輯應用程式部署範本</span><span class="sxs-lookup"><span data-stu-id="aa352-107">Logic app deployment template</span></span>

<span data-ttu-id="aa352-108">邏輯應用程式有三個基本元件：</span><span class="sxs-lookup"><span data-stu-id="aa352-108">A logic app has three basic components:</span></span>

* <span data-ttu-id="aa352-109">**邏輯應用程式資源**：包含定價方案、位置和工作流程定義等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa352-109">**Logic app resource**: Contains information about things like pricing plan, location, and the workflow definition.</span></span>
* <span data-ttu-id="aa352-110">**工作流程定義**︰描述邏輯應用程式的工作流程步驟，以及 Logic Apps 引擎應該如何執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="aa352-110">**Workflow definition**: Describes your logic app's workflow steps and how the Logic Apps engine should execute the workflow.</span></span>
<span data-ttu-id="aa352-111">您可以在邏輯應用程式的 [程式碼檢視] 視窗中檢視此定義。</span><span class="sxs-lookup"><span data-stu-id="aa352-111">You can view this definition in your logic app's **Code View** window.</span></span>
<span data-ttu-id="aa352-112">在邏輯應用程式資源中，您可以在 `definition` 屬性中找到此定義。</span><span class="sxs-lookup"><span data-stu-id="aa352-112">In the logic app resource, you can find this definition in the `definition` property.</span></span>
* <span data-ttu-id="aa352-113">**連接**：參照到可安全儲存關於任何連接器連接之中繼資料的個別資源，例如連接字串和存取權杖。</span><span class="sxs-lookup"><span data-stu-id="aa352-113">**Connections**: Refers to separate resources that securely store metadata about any connector connections, such as a connection string and an access token.</span></span>
<span data-ttu-id="aa352-114">在邏輯應用程式資源中，您的邏輯應用程式會參考 `parameters` 區段中的這些資源。</span><span class="sxs-lookup"><span data-stu-id="aa352-114">In the logic app resource, your logic app references these resources in the `parameters` section.</span></span>

<span data-ttu-id="aa352-115">您可以使用 [Azure 資源總管](http://resources.azure.com)等工具，檢視現有邏輯應用程式的這些所有部分。</span><span class="sxs-lookup"><span data-stu-id="aa352-115">You can view all these pieces of existing logic apps by using a tool like [Azure Resource Explorer](http://resources.azure.com).</span></span>

<span data-ttu-id="aa352-116">若要讓邏輯應用程式的範本可與資源群組部署搭配使用，您必須定義資源並視需要參數化。</span><span class="sxs-lookup"><span data-stu-id="aa352-116">To make a template for a logic app to use with resource group deployments, you must define the resources and parameterize as needed.</span></span>
<span data-ttu-id="aa352-117">例如，如果要部署到開發、測試和生產環境，您可能想要在每個環境中使用不同連接字串連至 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="aa352-117">For example, if you're deploying to a development, test, and production environment, you likely want to use different connection strings to a SQL database in each environment.</span></span>
<span data-ttu-id="aa352-118">或者，您可能想要在不同訂用帳戶或資源群組內部署。</span><span class="sxs-lookup"><span data-stu-id="aa352-118">Or, you might want to deploy within different subscriptions or resource groups.</span></span>  

## <a name="create-a-logic-app-deployment-template"></a><span data-ttu-id="aa352-119">建立邏輯應用程式部署範本</span><span class="sxs-lookup"><span data-stu-id="aa352-119">Create a logic app deployment template</span></span>

<span data-ttu-id="aa352-120">具備有效的邏輯應用程式部署範本的最簡單方法是使用[適用於 Logic Apps 的 Visual Studio 工具](logic-apps-deploy-from-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="aa352-120">The easiest way to have a valid logic app deployment template is to use the [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md).</span></span>
<span data-ttu-id="aa352-121">Visual Studio 工具產生的有效部署範本，可以在任何訂用帳戶或位置。</span><span class="sxs-lookup"><span data-stu-id="aa352-121">The Visual Studio tools generate a valid deployment template that can be used across any subscription or location.</span></span>

<span data-ttu-id="aa352-122">有一些其他工具可在您建立邏輯應用程式部署範本時提供協助。</span><span class="sxs-lookup"><span data-stu-id="aa352-122">A few other tools can assist you as you create a logic app deployment template.</span></span>
<span data-ttu-id="aa352-123">您可以手動撰寫，也就是視需要使用此處已討論過的資源來建立參數。</span><span class="sxs-lookup"><span data-stu-id="aa352-123">You can author by hand, that is, by using the resources already discussed here to create parameters as needed.</span></span>
<span data-ttu-id="aa352-124">另一個選項是使用 [邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="aa352-124">Another option is to use a [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell module.</span></span> <span data-ttu-id="aa352-125">這個開放原始碼模組會先評估邏輯應用程式和它所使用的任何連接，然後以部署所需的參數產生範本資源。</span><span class="sxs-lookup"><span data-stu-id="aa352-125">This open-source module first evaluates the logic app and any connections that it is using, and then generates template resources with the necessary parameters for deployment.</span></span>
<span data-ttu-id="aa352-126">例如，如果您的邏輯應用程式會收到來自 Azure 服務匯流排佇列的訊息並將資料加入至 Azure SQL Database，則此工具會保留所有的協調流程邏輯並將 SQL 和服務匯流排連接字串參數化，如此便可在部署時進行設定。</span><span class="sxs-lookup"><span data-stu-id="aa352-126">For example, if you have a logic app that receives a message from an Azure Service Bus queue and adds data to an Azure SQL database, the tool preserves all the orchestration logic and parameterizes the SQL and Service Bus connection strings so that they can be set at deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="aa352-127">連接必須位於與邏輯應用程式相同的資源群組內。</span><span class="sxs-lookup"><span data-stu-id="aa352-127">Connections must be within the same resource group as the logic app.</span></span>
>
>

### <a name="install-the-logic-app-template-powershell-module"></a><span data-ttu-id="aa352-128">安裝邏輯應用程式範本 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="aa352-128">Install the logic app template PowerShell module</span></span>
<span data-ttu-id="aa352-129">最簡單的安裝方式是透過 [PowerShell 資源庫](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1)使用 `Install-Module -Name LogicAppTemplate` 命令。</span><span class="sxs-lookup"><span data-stu-id="aa352-129">The easiest way to install the module is via the [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), by using the command `Install-Module -Name LogicAppTemplate`.</span></span>  

<span data-ttu-id="aa352-130">您也可以手動安裝 PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="aa352-130">You also can install the PowerShell module manually:</span></span>

1. <span data-ttu-id="aa352-131">下載最新版的 [邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)。</span><span class="sxs-lookup"><span data-stu-id="aa352-131">Download the latest release of the [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).</span></span>  
2. <span data-ttu-id="aa352-132">將此資料夾解壓縮至您的 PowerShell 模組資料夾 (通常是 `%UserProfile%\Documents\WindowsPowerShell\Modules`)。</span><span class="sxs-lookup"><span data-stu-id="aa352-132">Extract the folder in your PowerShell module folder (usually `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span></span>

<span data-ttu-id="aa352-133">為了讓模組能使用任何租用戶和訂用帳戶存取權杖，我們建議您搭配 [ARMClient](https://github.com/projectkudu/ARMClient) 命令列工具使用。</span><span class="sxs-lookup"><span data-stu-id="aa352-133">For the module to work with any tenant and subscription access token, we recommend that you use it with the [ARMClient](https://github.com/projectkudu/ARMClient) command-line tool.</span></span>  <span data-ttu-id="aa352-134">這篇[部落格文章 (英文)](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) 會更詳細地討論 ARMClient。</span><span class="sxs-lookup"><span data-stu-id="aa352-134">This [blog post](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) discusses ARMClient in more detail.</span></span>

### <a name="generate-a-logic-app-template-by-using-powershell"></a><span data-ttu-id="aa352-135">使用 PowerShell 產生邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="aa352-135">Generate a logic app template by using PowerShell</span></span>
<span data-ttu-id="aa352-136">安裝 PowerShell 之後，您可以使用下列命令來產生範本：</span><span class="sxs-lookup"><span data-stu-id="aa352-136">After PowerShell is installed, you can generate a template by using the following command:</span></span>

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

<span data-ttu-id="aa352-137">`$SubscriptionId` 是 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa352-137">`$SubscriptionId` is the Azure subscription ID.</span></span> <span data-ttu-id="aa352-138">這行程式碼會先透過 ARMClient 取得存取權杖，然後透過管線將它傳送到 PowerShell 指令碼，接著在 JSON 檔案中建立範本。</span><span class="sxs-lookup"><span data-stu-id="aa352-138">This line first gets an access token via ARMClient, then pipes it through to the PowerShell script, and then creates the template in a JSON file.</span></span>

## <a name="add-parameters-to-a-logic-app-template"></a><span data-ttu-id="aa352-139">將參數加入至邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="aa352-139">Add parameters to a logic app template</span></span>
<span data-ttu-id="aa352-140">建立邏輯應用程式範本之後，您可以繼續加入或修改您可能需要的參數。</span><span class="sxs-lookup"><span data-stu-id="aa352-140">After you create your logic app template, you can continue to add or modify parameters that you might need.</span></span> <span data-ttu-id="aa352-141">例如，如果您的定義包含您打算在單一部署中部署的 Azure 函數或巢狀工作流程的資源識別碼，您可以將更多資源新增至範本，並視需要將識別碼參數化。</span><span class="sxs-lookup"><span data-stu-id="aa352-141">For example, if your definition includes a resource ID to an Azure function or nested workflow that you plan to deploy in a single deployment, you can add more resources to your template and parameterize IDs as needed.</span></span> <span data-ttu-id="aa352-142">相同情況亦適用於您預計要與各資源群組一起部署的自訂 API 或 Swagger 端點的任何參考。</span><span class="sxs-lookup"><span data-stu-id="aa352-142">The same applies to any references to custom APIs or Swagger endpoints you expect to deploy with each resource group.</span></span>

## <a name="deploy-a-logic-app-template"></a><span data-ttu-id="aa352-143">部署邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="aa352-143">Deploy a logic app template</span></span>

<span data-ttu-id="aa352-144">您可以使用任何工具部署範本，例如 PowerShell、REST API、[Visual Studio Team Services Release Management](#team-services)，以及透過 Azure 入口網站進行範本部署。</span><span class="sxs-lookup"><span data-stu-id="aa352-144">You can deploy your template by using any tools like PowerShell, REST API, [Visual Studio Team Services Release Management](#team-services), and template deployment through the Azure portal.</span></span>
<span data-ttu-id="aa352-145">此外，為了儲存參數的值，我們也建議您建立[參數檔](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)。</span><span class="sxs-lookup"><span data-stu-id="aa352-145">Also, to store the values for parameters, we recommend that you create a [parameter file](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span></span>
<span data-ttu-id="aa352-146">了解如何[使用 Azure Resource Manager 範本和 PowerShell 部署資源](../azure-resource-manager/resource-group-template-deploy.md)或[使用 Azure Resource Manager 範本和 Azure 入口網站部署資源](../azure-resource-manager/resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="aa352-146">Learn how to [deploy resources with Azure Resource Manager templates and PowerShell](../azure-resource-manager/resource-group-template-deploy.md) or [deploy resources with Azure Resource Manager templates and the Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

### <a name="authorize-oauth-connections"></a><span data-ttu-id="aa352-147">授權 OAuth 連接</span><span class="sxs-lookup"><span data-stu-id="aa352-147">Authorize OAuth connections</span></span>

<span data-ttu-id="aa352-148">部署之後，邏輯應用程式就能搭配有效參數端對端運作。</span><span class="sxs-lookup"><span data-stu-id="aa352-148">After deployment, the logic app works end-to-end with valid parameters.</span></span>
<span data-ttu-id="aa352-149">不過，您仍然必須授權 OAuth 連接，才能產生有效的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="aa352-149">However, you must still authorize OAuth connections to generate a valid access token.</span></span>
<span data-ttu-id="aa352-150">若要授權 OAuth 連接，請在 Logic Apps 設計工具中開啟邏輯應用程式，然後授權這些連接。</span><span class="sxs-lookup"><span data-stu-id="aa352-150">To authorize OAuth connections, open the logic app in the Logic Apps Designer, and authorize these connections.</span></span> <span data-ttu-id="aa352-151">或者，如果是自動化部署，您可以使用指令碼來同意每個 OAuth 連接。</span><span class="sxs-lookup"><span data-stu-id="aa352-151">Or for automated deployment, you can use a script to consent to each OAuth connection.</span></span>
<span data-ttu-id="aa352-152">在 GitHub 上的 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 專案下方有一個範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="aa352-152">There's an example script on GitHub under the [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) project.</span></span>

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a><span data-ttu-id="aa352-153">Visual Studio Team Services Release Management</span><span class="sxs-lookup"><span data-stu-id="aa352-153">Visual Studio Team Services Release Management</span></span>

<span data-ttu-id="aa352-154">有一個適用於部署和管理環境的常見案例是，搭配使用 Visual Studio Team Services 中 Release Management 之類的工具與邏輯應用程式部署範本。</span><span class="sxs-lookup"><span data-stu-id="aa352-154">A common scenario for deploying and managing an environment is to use a tool like Release Management in Visual Studio Team Services, with a logic app deployment template.</span></span> <span data-ttu-id="aa352-155">Visual Studio Team Services 包含可加入至任何組建或版本管線的 [部署 Azure 資源群組](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) 工作。</span><span class="sxs-lookup"><span data-stu-id="aa352-155">Visual Studio Team Services includes a [Deploy Azure Resource Group](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) task that you can add to any build or release pipeline.</span></span> <span data-ttu-id="aa352-156">您必須擁有 [服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) 才能授權部署，而後可以產生版本定義。</span><span class="sxs-lookup"><span data-stu-id="aa352-156">You need to have a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) for authorization to deploy, and then you can generate the release definition.</span></span>

1. <span data-ttu-id="aa352-157">在 Release Management 中，選取 [空白]，如此就能建立空白的定義。</span><span class="sxs-lookup"><span data-stu-id="aa352-157">In Release Management, select **Empty** so that you create an empty definition.</span></span>

    ![建立空白定義][1]

2. <span data-ttu-id="aa352-159">選擇此定義所需的任何資源，很可能會包含手動產生或在建置流程中產生的邏輯應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="aa352-159">Choose any resources you need for this, most likely including the logic app template that is generated manually or as part of the build process.</span></span>
3. <span data-ttu-id="aa352-160">新增 [Azure 資源群組部署]  工作。</span><span class="sxs-lookup"><span data-stu-id="aa352-160">Add an **Azure Resource Group Deployment** task.</span></span>
4. <span data-ttu-id="aa352-161">設定 [服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)並參考 [範本] 和 [範本參數] 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa352-161">Configure with a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), and reference the Template and Template Parameters files.</span></span>
5. <span data-ttu-id="aa352-162">視需要針對任何其他環境、自動化測試或核准者，繼續在發行程序中建置步驟。</span><span class="sxs-lookup"><span data-stu-id="aa352-162">Continue to build out steps in the release process for any other environment, automated test, or approvers as needed.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
