---
title: "在 Visual Studio 中建置無伺服器應用程式 | Microsoft Docs"
description: "根據本指南，在 Visual Studio 中開始打造您的第一個無伺服器應用程式，包括建立、部署和管理應用程式。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 3672beda8a502e5fe2c8182076a8edef7ee9ebf6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a><span data-ttu-id="0b303-103">在 Visual Studio 中使用 Logic Apps 和 Functions 建置邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0b303-103">Build a serverless app in Visual Studio with Logic Apps and Functions</span></span>

<span data-ttu-id="0b303-104">Azure 中的無伺服器工具和功能可讓您快速開發和部署雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b303-104">Serverless tools and capabilities in Azure allow for rapid development and deployment of cloud applications.</span></span>  <span data-ttu-id="0b303-105">本文件著重於如何開始在 Visual Studio 中建置無伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b303-105">This document focuses on how to get started in Visual Studio building a serverless application.</span></span>  <span data-ttu-id="0b303-106">如需 Azure 中的無伺服器概觀，請參閱[這篇文章](logic-apps-serverless-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0b303-106">An overview of serverless in Azure [can be found in this article](logic-apps-serverless-overview.md).</span></span>

## <a name="getting-everything-ready"></a><span data-ttu-id="0b303-107">備妥一切</span><span class="sxs-lookup"><span data-stu-id="0b303-107">Getting everything ready</span></span>

<span data-ttu-id="0b303-108">以下是從 Visual Studio 建立無伺服器應用程式所需的必要條件︰</span><span class="sxs-lookup"><span data-stu-id="0b303-108">Here are the prerequisites needed to build a serverless application from Visual Studio:</span></span>

* <span data-ttu-id="0b303-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) 或 Visual Studio 2015 - Community、Professional 或 Enterprise</span><span class="sxs-lookup"><span data-stu-id="0b303-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span></span>
* [<span data-ttu-id="0b303-110">Logic Apps Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b303-110">Logic Apps Tools for Visual Studio</span></span>](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* <span data-ttu-id="0b303-111">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="0b303-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="0b303-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b303-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="0b303-113">[Azure Functions 核心工具](https://www.npmjs.com/package/azure-functions-core-tools)，在本機對函式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="0b303-113">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) to debug Functions locally</span></span>
* <span data-ttu-id="0b303-114">使用內嵌的邏輯應用程式設計工具時能夠存取 Web</span><span class="sxs-lookup"><span data-stu-id="0b303-114">Access to the web when using the embedded Logic App designer</span></span>

## <a name="getting-started-with-a-deployment-template"></a><span data-ttu-id="0b303-115">開始使用部署範本</span><span class="sxs-lookup"><span data-stu-id="0b303-115">Getting started with a deployment template</span></span>

<span data-ttu-id="0b303-116">Azure 中是在資源群組內管理資源。</span><span class="sxs-lookup"><span data-stu-id="0b303-116">Managing resources in Azure are done within a resource group.</span></span>  <span data-ttu-id="0b303-117">資源群組是資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="0b303-117">A resource group is a logical grouping of resources.</span></span>  <span data-ttu-id="0b303-118">資源群組可用來部署和管理資源集合。</span><span class="sxs-lookup"><span data-stu-id="0b303-118">Resource groups allow deployment and management of a collection of resources.</span></span>  <span data-ttu-id="0b303-119">對於 Azure 中的無伺服器應用程式，我們的資源群組包含 Azure Logic Apps 和 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="0b303-119">For a Serverless application in Azure, our resource group contains both Azure Logic Apps, and Azure Functions.</span></span>  <span data-ttu-id="0b303-120">我們在 Visual Studio 內使用資源群組專案，能夠將整個應用程式當作單一資產來開發、管理和部署。</span><span class="sxs-lookup"><span data-stu-id="0b303-120">By using the Resource Group project within Visual Studio, we are able to develop, manage, and deploy the entire application as a single asset.</span></span>

### <a name="create-a-resource-group-project-in-visual-studio"></a><span data-ttu-id="0b303-121">在 Visual Studio 中建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0b303-121">Create a Resource Group project in Visual Studio</span></span>

1. <span data-ttu-id="0b303-122">在 Visual Studio 中，按一下以新增 [新專案]。</span><span class="sxs-lookup"><span data-stu-id="0b303-122">In Visual Studio, click to add a **New Project**</span></span>
1. <span data-ttu-id="0b303-123">在 [雲端] 分類中，選擇建立 Azure [資源群組] 專案</span><span class="sxs-lookup"><span data-stu-id="0b303-123">In the **Cloud** category, select to create an Azure **Resource Group** project</span></span>  
 * <span data-ttu-id="0b303-124">如果您沒看到分類或專案列出，請確定您已經為 Visual Studio 安裝 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="0b303-124">If you do not see the category or project listed, be sure you have the Azure SDK installed for Visual Studio</span></span>
1. <span data-ttu-id="0b303-125">指定專案的名稱和位置，然後選取 [確定] 開始建立。Visual Studio 會提示您選取範本。</span><span class="sxs-lookup"><span data-stu-id="0b303-125">Give the project a name and location, and select **Ok** to create Visual Studio prompts to select a template.</span></span>  <span data-ttu-id="0b303-126">您可以選擇從 [空白]、邏輯應用程式或其他資源開始。</span><span class="sxs-lookup"><span data-stu-id="0b303-126">You could select to start from Blank, start with a Logic App or other resource.</span></span>  <span data-ttu-id="0b303-127">但在此案例中，我們使用 [Azure 快速入門範本] 開始打造無伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b303-127">However, in this case we use an Azure Quickstart Template to get us started with a serverless app.</span></span>
1. <span data-ttu-id="0b303-128">選取即可顯示從範本**Azure 快速入門**![選取 Azure 快速入門範本][1]</span><span class="sxs-lookup"><span data-stu-id="0b303-128">Select to show templates from **Azure Quickstart** ![Selecting Azure Quickstart templates][1]</span></span>
1. <span data-ttu-id="0b303-129">選取無伺服器快速入門範本︰**101-logic-app-and-function-app**，然後按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="0b303-129">Select the serverless quickstart template: **101-logic-app-and-function-app** and click **Ok**</span></span>

<span data-ttu-id="0b303-130">快速入門範本會在您的資源群組專案中建立部署範本。</span><span class="sxs-lookup"><span data-stu-id="0b303-130">The quickstart template creates a deployment template in your resource group project.</span></span>  <span data-ttu-id="0b303-131">此範本包含一個簡單的邏輯應用程式，它會呼叫 Azure Functions，然後傳回結果。</span><span class="sxs-lookup"><span data-stu-id="0b303-131">The template contains a simple Logic App that calls an Azure Functions, and returns the result.</span></span>  <span data-ttu-id="0b303-132">如果您在 [方案總管] 中開啟 `azuredeploy.json` 檔案，您可以看到無伺服器應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="0b303-132">If you open the `azuredeploy.json` file in the Solution Explorer, you can see the resources for the serverless app.</span></span>

## <a name="deploying-the-serverless-application"></a><span data-ttu-id="0b303-133">部署無伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="0b303-133">Deploying the serverless application</span></span>

<span data-ttu-id="0b303-134">需要有預先部署的 Azure 資源群組，您才能在 Visual Studio 中開啟邏輯應用程式視覺化設計工具。</span><span class="sxs-lookup"><span data-stu-id="0b303-134">Before you can open the Logic App visual designer in Visual Studio, there needs to be a pre-deployed Azure Resource Group.</span></span>  <span data-ttu-id="0b303-135">這樣可讓設計師在邏輯應用程式中建立和使用資源和服務的連線。</span><span class="sxs-lookup"><span data-stu-id="0b303-135">This allows the designer to create and use connections to resources and services in the logic app.</span></span>  <span data-ttu-id="0b303-136">首先，我們只需要部署已建立的方案。</span><span class="sxs-lookup"><span data-stu-id="0b303-136">To get started, we simply need to deploy the solution created.</span></span>

1. <span data-ttu-id="0b303-137">以滑鼠右鍵按一下 Visual Studio 專案中，選取**部署**，並建立**新增**部署![選取新的資源部署][2]</span><span class="sxs-lookup"><span data-stu-id="0b303-137">Right-click the project in Visual Studio, select **Deploy**, and create a **New** deployment  ![Selecting new resource deployment][2]</span></span>
1. <span data-ttu-id="0b303-138">選取有效的 Azure 訂用帳戶和資源群組</span><span class="sxs-lookup"><span data-stu-id="0b303-138">Select a valid Azure subscription and Resource group</span></span>
1. <span data-ttu-id="0b303-139">選擇**部署**方案</span><span class="sxs-lookup"><span data-stu-id="0b303-139">Select to **Deploy** the solution</span></span>
1. <span data-ttu-id="0b303-140">輸入邏輯應用程式和 Azure 函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b303-140">Enter in the name for the Logic App and the Azure Function App.</span></span>  <span data-ttu-id="0b303-141">Azure 函式名稱不必是全域唯一</span><span class="sxs-lookup"><span data-stu-id="0b303-141">The Azure Function name does need to be globally unique</span></span>

<span data-ttu-id="0b303-142">無伺服器方案會部署到指定的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0b303-142">The serverless solution deploys into the specified resource group.</span></span>  <span data-ttu-id="0b303-143">如果您在 Visual Studio 中查看 [輸出]，您可以看到部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="0b303-143">If you look at the **Output** in Visual Studio you can see the status of the deployment.</span></span>

## <a name="editing-the-logic-app-in-visual-studio"></a><span data-ttu-id="0b303-144">在 Visual Studio 中編輯邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0b303-144">Editing the logic app in Visual Studio</span></span>

<span data-ttu-id="0b303-145">當方案部署到任何資源群組之後，就可以使用視覺化設計工具來編輯和變更邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b303-145">Once the solution has been deployed into any resource group, the visual designer can be used to edit and make changes to the logic app.</span></span>

1. <span data-ttu-id="0b303-146">以滑鼠右鍵按一下 [方案總管] 中的 `azuredeploy.json` 檔案，然後選取 [使用 Logic Apps 設計工具開啟]</span><span class="sxs-lookup"><span data-stu-id="0b303-146">Right-click the `azuredeploy.json` file in the Solution Explorer and select **Open With Logic Apps Designer**</span></span>
1. <span data-ttu-id="0b303-147">選取方案已部署到的 [資源群組] 和 [位置]，然後選取 [確定]</span><span class="sxs-lookup"><span data-stu-id="0b303-147">Select the **Resource Group** and **Location** the solution has been deployed to and select **OK**</span></span>

<span data-ttu-id="0b303-148">現在應該可以在 Visual Studio 中看到邏輯應用程式視覺化設計工具。</span><span class="sxs-lookup"><span data-stu-id="0b303-148">The Logic App visual designer should now be visible with Visual Studio.</span></span>  <span data-ttu-id="0b303-149">您可以繼續新增步驟、修改工作流程，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="0b303-149">You can continue to add steps, modify the workflow, and save changes.</span></span>  <span data-ttu-id="0b303-150">您也可以從 Visual Studio 建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b303-150">You can also create logic apps from Visual Studio.</span></span>  <span data-ttu-id="0b303-151">如果您以滑鼠右鍵按一下範本巡覽器中的 [資源]，您可以選擇將 [邏輯應用程式] 資源至專案。</span><span class="sxs-lookup"><span data-stu-id="0b303-151">If you right-click the **Resources** in the template navigator, you can choose to add a **Logic App** to the project.</span></span>  <span data-ttu-id="0b303-152">空的邏輯應用程式會載入視覺化設計工具中，而不會預先部署至資源群組。</span><span class="sxs-lookup"><span data-stu-id="0b303-152">Empty logic apps load in the visual designer without a pre-deploy into a resource group.</span></span>

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a><span data-ttu-id="0b303-153">管理和檢視已部署之邏輯應用程式的執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0b303-153">Managing and viewing run history for a deployed logic app</span></span>

<span data-ttu-id="0b303-154">您也可以管理和檢視已部署在 Azure 中之邏輯應用程式的執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0b303-154">You can also manage and view the run history for logic apps deployed in Azure.</span></span>  <span data-ttu-id="0b303-155">如果您在 Visual Studio 中開啟 [Cloud Explorer] 工具，您可以用滑鼠右鍵按一下任何邏輯應用程式，然後選擇編輯、停用、檢視屬性，或檢視執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0b303-155">If you open the **Cloud Explorer** tool in Visual Studio, you can right-click any Logic App and choose to edit, disable, view properties, or view run history.</span></span>  <span data-ttu-id="0b303-156">按一下編輯也可讓您將已發佈的邏輯應用程式下載到 Visual Studio 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="0b303-156">Clicking edit also allows you to download a published logic app into a Visual Studio Resource Group project.</span></span>  <span data-ttu-id="0b303-157">這表示即使是在 Azure 入口網站中開始建置邏輯應用程式，您仍可在 Visual Studio 中匯入和管理它。</span><span class="sxs-lookup"><span data-stu-id="0b303-157">This means that even if you started building your logic app in the Azure portal, you can still import it and manage it from Visual Studio.</span></span>

## <a name="developing-an-azure-function-in-visual-studio"></a><span data-ttu-id="0b303-158">在 Visual Studio 中開發 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="0b303-158">Developing an Azure Function in Visual Studio</span></span>

<span data-ttu-id="0b303-159">部署範本會將方案中包含的任何 Azure Functions，部署至 `azuredeploy.json` 變數中指定的 git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="0b303-159">The deployment template deploys any Azure Functions that are contained in the solution for the git repository specified in the `azuredeploy.json` variables.</span></span>  <span data-ttu-id="0b303-160">如果您在方案內撰寫函式專案、將它簽入原始檔控制 (GitHub、Visual Studio Team Services 等)，然後更新 `repo` 變數，此範本將會部署 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="0b303-160">If you author a function project within the solution, check it into source control (GitHub, Visual Studio Team Services, etc.), and update the `repo` variable, the template will deploy the Azure Function.</span></span>

### <a name="creating-an-azure-function-project"></a><span data-ttu-id="0b303-161">建立 Azure 函式專案</span><span class="sxs-lookup"><span data-stu-id="0b303-161">Creating an Azure Function project</span></span>

<span data-ttu-id="0b303-162">如果使用 JavaScript、Python、F#、Bash、Batch 或 PowerShell，請遵循 [Functions CLI 中的步驟](../azure-functions/functions-run-local.md)建立專案。</span><span class="sxs-lookup"><span data-stu-id="0b303-162">If using JavaScript, Python, F#, Bash, Batch, or PowerShell, follow the [steps in the Functions CLI](../azure-functions/functions-run-local.md) to create a project.</span></span>  <span data-ttu-id="0b303-163">如果以 C# 開發函式，您可以在 Azure 函式的目前方案中使用 [C# 類別庫](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/)。</span><span class="sxs-lookup"><span data-stu-id="0b303-163">If developing a function in C#, you can use a [C# class library](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) in the current solution for the Azure Function.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b303-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b303-164">Next steps</span></span>

* [<span data-ttu-id="0b303-165">了解如何建置無伺服器社交儀表板</span><span class="sxs-lookup"><span data-stu-id="0b303-165">Learn how to build a serverless social dashboard</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="0b303-166">從 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0b303-166">Manage a logic app from Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="0b303-167">邏輯應用程式工作流程定義語言</span><span class="sxs-lookup"><span data-stu-id="0b303-167">Logic App workflow definition language</span></span>](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
