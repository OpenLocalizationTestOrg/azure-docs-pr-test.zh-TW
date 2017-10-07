---
title: "aaaCreate Azure 邏輯應用程式的部署範本 |Microsoft 文件"
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
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a><span data-ttu-id="18f1d-103">建立範本以進行邏輯應用程式部署和發行管理</span><span class="sxs-lookup"><span data-stu-id="18f1d-103">Create templates for logic apps deployment and release management</span></span>

<span data-ttu-id="18f1d-104">已建立邏輯應用程式之後，您可能會想 toocreate 它做為 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="18f1d-104">After a logic app has been created, you might want toocreate it as an Azure Resource Manager template.</span></span>
<span data-ttu-id="18f1d-105">如此一來，您可以輕鬆地部署 hello 邏輯應用程式 tooany 環境或，您可能需要的資源群組。</span><span class="sxs-lookup"><span data-stu-id="18f1d-105">This way, you can easily deploy hello logic app tooany environment or resource group where you might need it.</span></span>
<span data-ttu-id="18f1d-106">如需 Resource Manager 範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)和[使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-106">For more about Resource Manager templates, see [authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) and [deploying resources by using Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="logic-app-deployment-template"></a><span data-ttu-id="18f1d-107">邏輯應用程式部署範本</span><span class="sxs-lookup"><span data-stu-id="18f1d-107">Logic app deployment template</span></span>

<span data-ttu-id="18f1d-108">邏輯應用程式有三個基本元件：</span><span class="sxs-lookup"><span data-stu-id="18f1d-108">A logic app has three basic components:</span></span>

* <span data-ttu-id="18f1d-109">**邏輯應用程式資源**： 包含等定價計劃、 位置和 hello 工作流程定義的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="18f1d-109">**Logic app resource**: Contains information about things like pricing plan, location, and hello workflow definition.</span></span>
* <span data-ttu-id="18f1d-110">**工作流程定義**： 描述邏輯應用程式的工作流程的步驟和 hello Logic Apps 引擎應該如何執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="18f1d-110">**Workflow definition**: Describes your logic app's workflow steps and how hello Logic Apps engine should execute hello workflow.</span></span>
<span data-ttu-id="18f1d-111">您可以在邏輯應用程式的 [程式碼檢視] 視窗中檢視此定義。</span><span class="sxs-lookup"><span data-stu-id="18f1d-111">You can view this definition in your logic app's **Code View** window.</span></span>
<span data-ttu-id="18f1d-112">在 hello 邏輯應用程式資源中，您可以在 hello 中找到此定義`definition`屬性。</span><span class="sxs-lookup"><span data-stu-id="18f1d-112">In hello logic app resource, you can find this definition in hello `definition` property.</span></span>
* <span data-ttu-id="18f1d-113">**連線**： 參考 tooseparate 資源的安全地儲存任何連接器連接，例如連接字串和存取權杖的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="18f1d-113">**Connections**: Refers tooseparate resources that securely store metadata about any connector connections, such as a connection string and an access token.</span></span>
<span data-ttu-id="18f1d-114">Hello 邏輯應用程式資源，在邏輯應用程式會參考這些資源在 hello `parameters` > 一節。</span><span class="sxs-lookup"><span data-stu-id="18f1d-114">In hello logic app resource, your logic app references these resources in hello `parameters` section.</span></span>

<span data-ttu-id="18f1d-115">您可以使用 [Azure 資源總管](http://resources.azure.com)等工具，檢視現有邏輯應用程式的這些所有部分。</span><span class="sxs-lookup"><span data-stu-id="18f1d-115">You can view all these pieces of existing logic apps by using a tool like [Azure Resource Explorer](http://resources.azure.com).</span></span>

<span data-ttu-id="18f1d-116">toomake 範本的應用程式 toouse 邏輯與資源群組部署中，您必須定義 hello 資源，並視需要將參數化。</span><span class="sxs-lookup"><span data-stu-id="18f1d-116">toomake a template for a logic app toouse with resource group deployments, you must define hello resources and parameterize as needed.</span></span>
<span data-ttu-id="18f1d-117">例如，如果您要部署 tooa 開發、 測試和生產環境，您可能想 toouse 不同的連接字串 tooa SQL 資料庫中每個環境。</span><span class="sxs-lookup"><span data-stu-id="18f1d-117">For example, if you're deploying tooa development, test, and production environment, you likely want toouse different connection strings tooa SQL database in each environment.</span></span>
<span data-ttu-id="18f1d-118">或者，您可能會想 toodeploy 不同訂用帳戶或資源群組內。</span><span class="sxs-lookup"><span data-stu-id="18f1d-118">Or, you might want toodeploy within different subscriptions or resource groups.</span></span>  

## <a name="create-a-logic-app-deployment-template"></a><span data-ttu-id="18f1d-119">建立邏輯應用程式部署範本</span><span class="sxs-lookup"><span data-stu-id="18f1d-119">Create a logic app deployment template</span></span>

<span data-ttu-id="18f1d-120">最簡單方式 toohave hello 的有效邏輯應用程式部署範本是 toouse [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-120">hello easiest way toohave a valid logic app deployment template is toouse the [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md).</span></span>
<span data-ttu-id="18f1d-121">hello Visual Studio 工具會產生可用於任何訂閱或位置的有效的部署範本。</span><span class="sxs-lookup"><span data-stu-id="18f1d-121">hello Visual Studio tools generate a valid deployment template that can be used across any subscription or location.</span></span>

<span data-ttu-id="18f1d-122">有一些其他工具可在您建立邏輯應用程式部署範本時提供協助。</span><span class="sxs-lookup"><span data-stu-id="18f1d-122">A few other tools can assist you as you create a logic app deployment template.</span></span>
<span data-ttu-id="18f1d-123">您可以手動撰寫，也就是使用 hello 資源已經討論 toocreate 參數視。</span><span class="sxs-lookup"><span data-stu-id="18f1d-123">You can author by hand, that is, by using hello resources already discussed here toocreate parameters as needed.</span></span>
<span data-ttu-id="18f1d-124">另一個選項是 toouse[邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator)PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="18f1d-124">Another option is toouse a [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell module.</span></span> <span data-ttu-id="18f1d-125">此開放原始碼模組會先評估 hello 邏輯應用程式和任何連接它正在使用，並接著會產生與部署的 hello 必要參數的範本資源。</span><span class="sxs-lookup"><span data-stu-id="18f1d-125">This open-source module first evaluates hello logic app and any connections that it is using, and then generates template resources with hello necessary parameters for deployment.</span></span>
<span data-ttu-id="18f1d-126">比方說，如果您有邏輯應用程式，從 Azure 服務匯流排佇列接收訊息，並加入資料 tooan Azure SQL database，hello 工具可以保留所有 hello 協調流程邏輯，會參數化 hello SQL 和服務匯流排連接字串，讓他們可以設定在部署。</span><span class="sxs-lookup"><span data-stu-id="18f1d-126">For example, if you have a logic app that receives a message from an Azure Service Bus queue and adds data tooan Azure SQL database, hello tool preserves all hello orchestration logic and parameterizes hello SQL and Service Bus connection strings so that they can be set at deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="18f1d-127">連線必須位在 hello 與 hello 邏輯應用程式的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="18f1d-127">Connections must be within hello same resource group as hello logic app.</span></span>
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a><span data-ttu-id="18f1d-128">安裝 hello 邏輯應用程式範本 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="18f1d-128">Install hello logic app template PowerShell module</span></span>
<span data-ttu-id="18f1d-129">hello 最簡單方式 tooinstall hello 模組是透過 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1)，利用 hello 命令`Install-Module -Name LogicAppTemplate`。</span><span class="sxs-lookup"><span data-stu-id="18f1d-129">hello easiest way tooinstall hello module is via hello [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), by using hello command `Install-Module -Name LogicAppTemplate`.</span></span>  

<span data-ttu-id="18f1d-130">您也可以安裝 hello PowerShell 模組以手動方式：</span><span class="sxs-lookup"><span data-stu-id="18f1d-130">You also can install hello PowerShell module manually:</span></span>

1. <span data-ttu-id="18f1d-131">下載 hello 最新版本的 hello[邏輯應用程式範本建立者](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-131">Download hello latest release of hello [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).</span></span>  
2. <span data-ttu-id="18f1d-132">擷取您的 PowerShell 模組資料夾中的 hello 資料夾 (通常`%UserProfile%\Documents\WindowsPowerShell\Modules`)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-132">Extract hello folder in your PowerShell module folder (usually `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span></span>

<span data-ttu-id="18f1d-133">Hello 模組 toowork 具有任何租用戶和訂用帳戶的存取權的語彙基元，我們建議您的 hello 使用[ARMClient](https://github.com/projectkudu/ARMClient)命令列工具。</span><span class="sxs-lookup"><span data-stu-id="18f1d-133">For hello module toowork with any tenant and subscription access token, we recommend that you use it with hello [ARMClient](https://github.com/projectkudu/ARMClient) command-line tool.</span></span>  <span data-ttu-id="18f1d-134">這篇[部落格文章 (英文)](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) 會更詳細地討論 ARMClient。</span><span class="sxs-lookup"><span data-stu-id="18f1d-134">This [blog post](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) discusses ARMClient in more detail.</span></span>

### <a name="generate-a-logic-app-template-by-using-powershell"></a><span data-ttu-id="18f1d-135">使用 PowerShell 產生邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="18f1d-135">Generate a logic app template by using PowerShell</span></span>
<span data-ttu-id="18f1d-136">安裝 PowerShell 之後，您可以使用下列命令的 hello 產生範本：</span><span class="sxs-lookup"><span data-stu-id="18f1d-136">After PowerShell is installed, you can generate a template by using hello following command:</span></span>

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

<span data-ttu-id="18f1d-137">`$SubscriptionId`這是 hello Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="18f1d-137">`$SubscriptionId` is hello Azure subscription ID.</span></span> <span data-ttu-id="18f1d-138">這一行會先取得存取權杖透過 ARMClient，則管道透過 toohello PowerShell 指令碼，然後建立 JSON 檔案中的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18f1d-138">This line first gets an access token via ARMClient, then pipes it through toohello PowerShell script, and then creates hello template in a JSON file.</span></span>

## <a name="add-parameters-tooa-logic-app-template"></a><span data-ttu-id="18f1d-139">加入參數 tooa 邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="18f1d-139">Add parameters tooa logic app template</span></span>
<span data-ttu-id="18f1d-140">您建立邏輯應用程式範本之後，您可以繼續 tooadd 或修改您可能需要的參數。</span><span class="sxs-lookup"><span data-stu-id="18f1d-140">After you create your logic app template, you can continue tooadd or modify parameters that you might need.</span></span> <span data-ttu-id="18f1d-141">比方說，如果您定義包含的資源識別碼 tooan Azure 函式或您計劃在單一部署 toodeploy 巢狀工作流程，您可以新增更多資源 tooyour 範本，並視需要參數化識別碼。</span><span class="sxs-lookup"><span data-stu-id="18f1d-141">For example, if your definition includes a resource ID tooan Azure function or nested workflow that you plan toodeploy in a single deployment, you can add more resources tooyour template and parameterize IDs as needed.</span></span> <span data-ttu-id="18f1d-142">hello 一樣 tooany 參考 toocustom 應用程式開發介面或 Swagger 端點您預期 toodeploy 與每個資源群組。</span><span class="sxs-lookup"><span data-stu-id="18f1d-142">hello same applies tooany references toocustom APIs or Swagger endpoints you expect toodeploy with each resource group.</span></span>

## <a name="deploy-a-logic-app-template"></a><span data-ttu-id="18f1d-143">部署邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="18f1d-143">Deploy a logic app template</span></span>

<span data-ttu-id="18f1d-144">您可以使用 powershell、 REST API 的任何工具來部署您的範本[Visual Studio Team Services Release Management](#team-services)，並透過 hello Azure 入口網站的範本部署。</span><span class="sxs-lookup"><span data-stu-id="18f1d-144">You can deploy your template by using any tools like PowerShell, REST API, [Visual Studio Team Services Release Management](#team-services), and template deployment through hello Azure portal.</span></span>
<span data-ttu-id="18f1d-145">此外，toostore hello 參數的值，我們建議您建立[參數檔](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-145">Also, toostore hello values for parameters, we recommend that you create a [parameter file](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span></span>
<span data-ttu-id="18f1d-146">了解如何太[部署與 Azure 資源管理員範本和 PowerShell 資源](../azure-resource-manager/resource-group-template-deploy.md)或[部署 Azure 資源管理員範本的資源和 hello Azure 入口網站](../azure-resource-manager/resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="18f1d-146">Learn how too[deploy resources with Azure Resource Manager templates and PowerShell](../azure-resource-manager/resource-group-template-deploy.md) or [deploy resources with Azure Resource Manager templates and hello Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

### <a name="authorize-oauth-connections"></a><span data-ttu-id="18f1d-147">授權 OAuth 連接</span><span class="sxs-lookup"><span data-stu-id="18f1d-147">Authorize OAuth connections</span></span>

<span data-ttu-id="18f1d-148">部署之後，hello 邏輯應用程式運作順利端對端的有效參數。</span><span class="sxs-lookup"><span data-stu-id="18f1d-148">After deployment, hello logic app works end-to-end with valid parameters.</span></span>
<span data-ttu-id="18f1d-149">不過，您仍然必須授權 OAuth 連線 toogenerate 有效存取權杖。</span><span class="sxs-lookup"><span data-stu-id="18f1d-149">However, you must still authorize OAuth connections toogenerate a valid access token.</span></span>
<span data-ttu-id="18f1d-150">tooauthorize OAuth 連線，在 [hello 邏輯應用程式的設計工具] 中開啟 hello 邏輯應用程式，並授權這些連線。</span><span class="sxs-lookup"><span data-stu-id="18f1d-150">tooauthorize OAuth connections, open hello logic app in hello Logic Apps Designer, and authorize these connections.</span></span> <span data-ttu-id="18f1d-151">或用於自動化部署，您可以使用指令碼 tooconsent tooeach OAuth 連線。</span><span class="sxs-lookup"><span data-stu-id="18f1d-151">Or for automated deployment, you can use a script tooconsent tooeach OAuth connection.</span></span>
<span data-ttu-id="18f1d-152">在 GitHub 上的 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 專案下方有一個範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="18f1d-152">There's an example script on GitHub under the [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) project.</span></span>

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a><span data-ttu-id="18f1d-153">Visual Studio Team Services Release Management</span><span class="sxs-lookup"><span data-stu-id="18f1d-153">Visual Studio Team Services Release Management</span></span>

<span data-ttu-id="18f1d-154">部署及管理環境的常見案例是 toouse 這類工具 Visual Studio Team Services 中的發行管理使用邏輯應用程式的部署範本。</span><span class="sxs-lookup"><span data-stu-id="18f1d-154">A common scenario for deploying and managing an environment is toouse a tool like Release Management in Visual Studio Team Services, with a logic app deployment template.</span></span> <span data-ttu-id="18f1d-155">Visual Studio Team Services 包含[部署 Azure 資源群組](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup)工作，您可以新增 tooany 建置或發行管線。</span><span class="sxs-lookup"><span data-stu-id="18f1d-155">Visual Studio Team Services includes a [Deploy Azure Resource Group](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) task that you can add tooany build or release pipeline.</span></span> <span data-ttu-id="18f1d-156">您需要 toohave[服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)授權 toodeploy，然後您可以產生 hello 發行定義。</span><span class="sxs-lookup"><span data-stu-id="18f1d-156">You need toohave a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) for authorization toodeploy, and then you can generate hello release definition.</span></span>

1. <span data-ttu-id="18f1d-157">在 Release Management 中，選取 [空白]，如此就能建立空白的定義。</span><span class="sxs-lookup"><span data-stu-id="18f1d-157">In Release Management, select **Empty** so that you create an empty definition.</span></span>

    ![建立空白定義][1]

2. <span data-ttu-id="18f1d-159">選擇此，最有可能包括 hello 邏輯應用程式範本以手動方式或一部分 hello 產生所需的任何資源建置程序。</span><span class="sxs-lookup"><span data-stu-id="18f1d-159">Choose any resources you need for this, most likely including hello logic app template that is generated manually or as part of hello build process.</span></span>
3. <span data-ttu-id="18f1d-160">新增 [Azure 資源群組部署]  工作。</span><span class="sxs-lookup"><span data-stu-id="18f1d-160">Add an **Azure Resource Group Deployment** task.</span></span>
4. <span data-ttu-id="18f1d-161">使用設定[服務主體](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)，並參考 hello 範本和範本參數檔案。</span><span class="sxs-lookup"><span data-stu-id="18f1d-161">Configure with a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), and reference hello Template and Template Parameters files.</span></span>
5. <span data-ttu-id="18f1d-162">繼續 toobuild 步驟中的任何其他環境，自動化的測試或視需要的核准者 hello 發行程序。</span><span class="sxs-lookup"><span data-stu-id="18f1d-162">Continue toobuild out steps in hello release process for any other environment, automated test, or approvers as needed.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
