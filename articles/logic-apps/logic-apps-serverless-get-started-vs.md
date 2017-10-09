---
title: "aaaBuild Visual Studio 中的無伺服器應用程式 |Microsoft 文件"
description: "開始使用您建立、 部署和管理 Visual Studio 中的 hello 應用程式在本指南的第一個無伺服器應用程式。"
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
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a><span data-ttu-id="bff49-103">在 Visual Studio 中使用 Logic Apps 和 Functions 建置邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="bff49-103">Build a serverless app in Visual Studio with Logic Apps and Functions</span></span>

<span data-ttu-id="bff49-104">Azure 中的無伺服器工具和功能可讓您快速開發和部署雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="bff49-104">Serverless tools and capabilities in Azure allow for rapid development and deployment of cloud applications.</span></span>  <span data-ttu-id="bff49-105">本文件著重於如何 tooget 建立無伺服器的應用程式的 Visual Studio 中啟動。</span><span class="sxs-lookup"><span data-stu-id="bff49-105">This document focuses on how tooget started in Visual Studio building a serverless application.</span></span>  <span data-ttu-id="bff49-106">如需 Azure 中的無伺服器概觀，請參閱[這篇文章](logic-apps-serverless-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bff49-106">An overview of serverless in Azure [can be found in this article](logic-apps-serverless-overview.md).</span></span>

## <a name="getting-everything-ready"></a><span data-ttu-id="bff49-107">備妥一切</span><span class="sxs-lookup"><span data-stu-id="bff49-107">Getting everything ready</span></span>

<span data-ttu-id="bff49-108">以下是 hello 所需必要條件 toobuild 無伺服器的應用程式，從 Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bff49-108">Here are hello prerequisites needed toobuild a serverless application from Visual Studio:</span></span>

* <span data-ttu-id="bff49-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) 或 Visual Studio 2015 - Community、Professional 或 Enterprise</span><span class="sxs-lookup"><span data-stu-id="bff49-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span></span>
* [<span data-ttu-id="bff49-110">Logic Apps Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bff49-110">Logic Apps Tools for Visual Studio</span></span>](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* <span data-ttu-id="bff49-111">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="bff49-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="bff49-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff49-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="bff49-113">[Azure 功能的核心工具](https://www.npmjs.com/package/azure-functions-core-tools)toodebug 本機函式</span><span class="sxs-lookup"><span data-stu-id="bff49-113">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) toodebug Functions locally</span></span>
* <span data-ttu-id="bff49-114">當使用 hello 內嵌邏輯應用程式的設計工具時，存取 toohello web</span><span class="sxs-lookup"><span data-stu-id="bff49-114">Access toohello web when using hello embedded Logic App designer</span></span>

## <a name="getting-started-with-a-deployment-template"></a><span data-ttu-id="bff49-115">開始使用部署範本</span><span class="sxs-lookup"><span data-stu-id="bff49-115">Getting started with a deployment template</span></span>

<span data-ttu-id="bff49-116">Azure 中是在資源群組內管理資源。</span><span class="sxs-lookup"><span data-stu-id="bff49-116">Managing resources in Azure are done within a resource group.</span></span>  <span data-ttu-id="bff49-117">資源群組是資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="bff49-117">A resource group is a logical grouping of resources.</span></span>  <span data-ttu-id="bff49-118">資源群組可用來部署和管理資源集合。</span><span class="sxs-lookup"><span data-stu-id="bff49-118">Resource groups allow deployment and management of a collection of resources.</span></span>  <span data-ttu-id="bff49-119">對於 Azure 中的無伺服器應用程式，我們的資源群組包含 Azure Logic Apps 和 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="bff49-119">For a Serverless application in Azure, our resource group contains both Azure Logic Apps, and Azure Functions.</span></span>  <span data-ttu-id="bff49-120">藉由使用 Visual Studio 中的 hello 資源群組專案，我們目前無法 toodevelop、 管理及部署 hello 整個應用程式做為單一的資產。</span><span class="sxs-lookup"><span data-stu-id="bff49-120">By using hello Resource Group project within Visual Studio, we are able toodevelop, manage, and deploy hello entire application as a single asset.</span></span>

### <a name="create-a-resource-group-project-in-visual-studio"></a><span data-ttu-id="bff49-121">在 Visual Studio 中建立資源群組</span><span class="sxs-lookup"><span data-stu-id="bff49-121">Create a Resource Group project in Visual Studio</span></span>

1. <span data-ttu-id="bff49-122">在 Visual Studio 中，按一下 tooadd**新專案**</span><span class="sxs-lookup"><span data-stu-id="bff49-122">In Visual Studio, click tooadd a **New Project**</span></span>
1. <span data-ttu-id="bff49-123">在 hello**雲端**分類中，選取 toocreate Azure**資源群組**專案</span><span class="sxs-lookup"><span data-stu-id="bff49-123">In hello **Cloud** category, select toocreate an Azure **Resource Group** project</span></span>  
 * <span data-ttu-id="bff49-124">如果您看不 hello 類別或專案列出，請確定您擁有 hello Azure SDK for Visual Studio 安裝</span><span class="sxs-lookup"><span data-stu-id="bff49-124">If you do not see hello category or project listed, be sure you have hello Azure SDK installed for Visual Studio</span></span>
1. <span data-ttu-id="bff49-125">為 hello 專案的名稱和位置，然後選取**確定**toocreate Visual Studio 會提示 tooselect 範本。</span><span class="sxs-lookup"><span data-stu-id="bff49-125">Give hello project a name and location, and select **Ok** toocreate Visual Studio prompts tooselect a template.</span></span>  <span data-ttu-id="bff49-126">您可以選擇 toostart 空白、 邏輯應用程式的開頭或其他資源。</span><span class="sxs-lookup"><span data-stu-id="bff49-126">You could select toostart from Blank, start with a Logic App or other resource.</span></span>  <span data-ttu-id="bff49-127">不過，在此情況下我們使用我們的無伺服器的應用程式以啟動 Azure 快速入門範本 tooget。</span><span class="sxs-lookup"><span data-stu-id="bff49-127">However, in this case we use an Azure Quickstart Template tooget us started with a serverless app.</span></span>
1. <span data-ttu-id="bff49-128">選取從 tooshow 範本**Azure 快速入門**![選取 Azure 快速入門範本][1]</span><span class="sxs-lookup"><span data-stu-id="bff49-128">Select tooshow templates from **Azure Quickstart** ![Selecting Azure Quickstart templates][1]</span></span>
1. <span data-ttu-id="bff49-129">選取 hello 無伺服器快速入門範本： **101-logic-app-and-function-app**按一下**[確定]**</span><span class="sxs-lookup"><span data-stu-id="bff49-129">Select hello serverless quickstart template: **101-logic-app-and-function-app** and click **Ok**</span></span>

<span data-ttu-id="bff49-130">hello 快速入門範本建立資源群組專案中的部署範本。</span><span class="sxs-lookup"><span data-stu-id="bff49-130">hello quickstart template creates a deployment template in your resource group project.</span></span>  <span data-ttu-id="bff49-131">hello 範本包含簡單的邏輯應用程式呼叫 Azure 函式，並傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="bff49-131">hello template contains a simple Logic App that calls an Azure Functions, and returns hello result.</span></span>  <span data-ttu-id="bff49-132">如果您開啟 hello`azuredeploy.json`檔案中的 hello 方案總管 中，您會看到 hello hello 無伺服器應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="bff49-132">If you open hello `azuredeploy.json` file in hello Solution Explorer, you can see hello resources for hello serverless app.</span></span>

## <a name="deploying-hello-serverless-application"></a><span data-ttu-id="bff49-133">部署的 hello 無伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="bff49-133">Deploying hello serverless application</span></span>

<span data-ttu-id="bff49-134">您可以開啟 Visual Studio 中的 hello 邏輯應用程式的視覺化設計工具之前，需要 toobe 預先部署的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="bff49-134">Before you can open hello Logic App visual designer in Visual Studio, there needs toobe a pre-deployed Azure Resource Group.</span></span>  <span data-ttu-id="bff49-135">這可讓 hello 設計工具 toocreate 及使用連線 tooresources 服務 hello 邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bff49-135">This allows hello designer toocreate and use connections tooresources and services in hello logic app.</span></span>  <span data-ttu-id="bff49-136">啟動 tooget，我們只需要建立 toodeploy hello 方案。</span><span class="sxs-lookup"><span data-stu-id="bff49-136">tooget started, we simply need toodeploy hello solution created.</span></span>

1. <span data-ttu-id="bff49-137">以滑鼠右鍵按一下 hello 專案在 Visual Studio 中，選取**部署**，並建立**新增**部署![選取新的資源部署][2]</span><span class="sxs-lookup"><span data-stu-id="bff49-137">Right-click hello project in Visual Studio, select **Deploy**, and create a **New** deployment  ![Selecting new resource deployment][2]</span></span>
1. <span data-ttu-id="bff49-138">選取有效的 Azure 訂用帳戶和資源群組</span><span class="sxs-lookup"><span data-stu-id="bff49-138">Select a valid Azure subscription and Resource group</span></span>
1. <span data-ttu-id="bff49-139">選取太**部署**hello 方案</span><span class="sxs-lookup"><span data-stu-id="bff49-139">Select too**Deploy** hello solution</span></span>
1. <span data-ttu-id="bff49-140">輸入 hello hello 邏輯應用程式的名稱和 hello Azure 函式應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bff49-140">Enter in hello name for hello Logic App and hello Azure Function App.</span></span>  <span data-ttu-id="bff49-141">hello Azure 函式需要名稱 toobe 全域唯一</span><span class="sxs-lookup"><span data-stu-id="bff49-141">hello Azure Function name does need toobe globally unique</span></span>

<span data-ttu-id="bff49-142">hello 無伺服器方案部署到 hello 指定的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bff49-142">hello serverless solution deploys into hello specified resource group.</span></span>  <span data-ttu-id="bff49-143">如果您看一下 hello**輸出**在 Visual Studio 中，您可以看到 hello 部署的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="bff49-143">If you look at hello **Output** in Visual Studio you can see hello status of hello deployment.</span></span>

## <a name="editing-hello-logic-app-in-visual-studio"></a><span data-ttu-id="bff49-144">編輯 Visual Studio 中的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="bff49-144">Editing hello logic app in Visual Studio</span></span>

<span data-ttu-id="bff49-145">一旦 hello 方案已經部署到任何資源群組，可以是使用的 tooedit hello 視覺化設計工具，而且讓變更 toohello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="bff49-145">Once hello solution has been deployed into any resource group, hello visual designer can be used tooedit and make changes toohello logic app.</span></span>

1. <span data-ttu-id="bff49-146">以滑鼠右鍵按一下 hello `azuredeploy.json` hello 方案總管 中的檔案，然後選取**開啟使用邏輯應用程式設計師**</span><span class="sxs-lookup"><span data-stu-id="bff49-146">Right-click hello `azuredeploy.json` file in hello Solution Explorer and select **Open With Logic Apps Designer**</span></span>
1. <span data-ttu-id="bff49-147">選取 hello**資源群組**和**位置**hello 解決方案已部署 tooand 選取**[確定]**</span><span class="sxs-lookup"><span data-stu-id="bff49-147">Select hello **Resource Group** and **Location** hello solution has been deployed tooand select **OK**</span></span>

<span data-ttu-id="bff49-148">hello 邏輯應用程式的視覺化設計工具現在應該可以看到與 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bff49-148">hello Logic App visual designer should now be visible with Visual Studio.</span></span>  <span data-ttu-id="bff49-149">您可以繼續 tooadd 步驟中，修改 hello 工作流程，並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="bff49-149">You can continue tooadd steps, modify hello workflow, and save changes.</span></span>  <span data-ttu-id="bff49-150">您也可以從 Visual Studio 建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="bff49-150">You can also create logic apps from Visual Studio.</span></span>  <span data-ttu-id="bff49-151">如果您以滑鼠右鍵按一下 hello**資源**hello 範本在導覽中，您可以選擇 tooadd**邏輯應用程式**toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="bff49-151">If you right-click hello **Resources** in hello template navigator, you can choose tooadd a **Logic App** toohello project.</span></span>  <span data-ttu-id="bff49-152">Hello 沒有視覺化設計工具中載入的空白 logic apps 預先部署至資源群組。</span><span class="sxs-lookup"><span data-stu-id="bff49-152">Empty logic apps load in hello visual designer without a pre-deploy into a resource group.</span></span>

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a><span data-ttu-id="bff49-153">管理和檢視已部署之邏輯應用程式的執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="bff49-153">Managing and viewing run history for a deployed logic app</span></span>

<span data-ttu-id="bff49-154">您也可以管理，並檢視部署在 Azure 中的 logic apps hello 執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="bff49-154">You can also manage and view hello run history for logic apps deployed in Azure.</span></span>  <span data-ttu-id="bff49-155">如果您開啟 hello **Cloud Explorer**工具或在 Visual Studio 中，您可以以滑鼠右鍵按一下任何邏輯應用程式，並選擇 tooedit，停用，檢視內容中，檢視執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="bff49-155">If you open hello **Cloud Explorer** tool in Visual Studio, you can right-click any Logic App and choose tooedit, disable, view properties, or view run history.</span></span>  <span data-ttu-id="bff49-156">按一下 編輯也可讓您 toodownload 已發行的邏輯應用程式到 Visual Studio 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="bff49-156">Clicking edit also allows you toodownload a published logic app into a Visual Studio Resource Group project.</span></span>  <span data-ttu-id="bff49-157">這表示，即使您開始建置 hello Azure 入口網站中的應用程式邏輯，您仍可以將它匯入及管理從 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bff49-157">This means that even if you started building your logic app in hello Azure portal, you can still import it and manage it from Visual Studio.</span></span>

## <a name="developing-an-azure-function-in-visual-studio"></a><span data-ttu-id="bff49-158">在 Visual Studio 中開發 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="bff49-158">Developing an Azure Function in Visual Studio</span></span>

<span data-ttu-id="bff49-159">hello 部署範本部署 hello hello 中指定的 git 儲存機制的 hello 方案中所包含的任何 Azure 函式`azuredeploy.json`變數。</span><span class="sxs-lookup"><span data-stu-id="bff49-159">hello deployment template deploys any Azure Functions that are contained in hello solution for hello git repository specified in hello `azuredeploy.json` variables.</span></span>  <span data-ttu-id="bff49-160">如果您撰寫函式中的專案 hello 方案時，將它簽入原始檔控制 （GitHub、 Visual Studio Team Services 等），並更新 hello`repo`變數 hello 範本將會部署 hello Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="bff49-160">If you author a function project within hello solution, check it into source control (GitHub, Visual Studio Team Services, etc.), and update hello `repo` variable, hello template will deploy hello Azure Function.</span></span>

### <a name="creating-an-azure-function-project"></a><span data-ttu-id="bff49-161">建立 Azure 函式專案</span><span class="sxs-lookup"><span data-stu-id="bff49-161">Creating an Azure Function project</span></span>

<span data-ttu-id="bff49-162">如果使用 JavaScript、 Python、 F #、 Bash、 批次或 PowerShell，請遵循 hello [hello CLI 函式中的步驟](../azure-functions/functions-run-local.md)toocreate 專案。</span><span class="sxs-lookup"><span data-stu-id="bff49-162">If using JavaScript, Python, F#, Bash, Batch, or PowerShell, follow hello [steps in hello Functions CLI](../azure-functions/functions-run-local.md) toocreate a project.</span></span>  <span data-ttu-id="bff49-163">如果開發的函式，在 C# 中，您可以使用[C# 類別庫](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/)hello Azure 函式的 hello 目前方案中。</span><span class="sxs-lookup"><span data-stu-id="bff49-163">If developing a function in C#, you can use a [C# class library](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) in hello current solution for hello Azure Function.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bff49-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bff49-164">Next steps</span></span>

* [<span data-ttu-id="bff49-165">深入了解如何 toobuild 無伺服器的社交儀表板</span><span class="sxs-lookup"><span data-stu-id="bff49-165">Learn how toobuild a serverless social dashboard</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="bff49-166">從 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="bff49-166">Manage a logic app from Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="bff49-167">邏輯應用程式工作流程定義語言</span><span class="sxs-lookup"><span data-stu-id="bff49-167">Logic App workflow definition language</span></span>](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
