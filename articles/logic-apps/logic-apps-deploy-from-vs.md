---
title: "在 Visual Studio 中建立、建置和部署邏輯應用程式 - Azure Logic Apps | Microsoft Docs"
description: "建立 Visual Studio 專案，讓您能夠設計、建置和部署 Azure Logic Apps。"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="325d7-103">在 Visual Studio 中設計、建置和部署 Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="325d7-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="325d7-104">雖然 [Azure 入口網站](https://portal.azure.com/)提供一種絕佳的方式讓您能夠建立和管理 Azure Logic Apps，但您可以使用 Visual Studio 來設計、建置和部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="325d7-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="325d7-105">Visual Studio 提供豐富的工具 (例如邏輯應用程式設計工具)，讓您能夠用來建立邏輯應用程式、設定部署和自動化範本，並部署至任何環境。</span><span class="sxs-lookup"><span data-stu-id="325d7-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="325d7-106">若要開始使用 Azure Logic Apps，請先了解[如何在 Azure 入口網站中建立第一個邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="325d7-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="325d7-107">安裝步驟</span><span class="sxs-lookup"><span data-stu-id="325d7-107">Installation steps</span></span>

<span data-ttu-id="325d7-108">若要安裝和設定適用於 Azure Logic Apps 的 Visual Studio 工具，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="325d7-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="325d7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="325d7-109">Prerequisites</span></span>

* <span data-ttu-id="325d7-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="325d7-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="325d7-111">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="325d7-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="325d7-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="325d7-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="325d7-113">Web 的存取權 (若使用內嵌的設計工具)</span><span class="sxs-lookup"><span data-stu-id="325d7-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="325d7-114">安裝適用於 Azure Logic Apps 的 Visual Studio 工具</span><span class="sxs-lookup"><span data-stu-id="325d7-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="325d7-115">在您安裝必要條件之後︰</span><span class="sxs-lookup"><span data-stu-id="325d7-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="325d7-116">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="325d7-116">Open Visual Studio.</span></span> <span data-ttu-id="325d7-117">在 [工具] 功能表上，選取 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="325d7-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="325d7-118">展開 [線上] 類別讓您可以在線上搜尋。</span><span class="sxs-lookup"><span data-stu-id="325d7-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="325d7-119">瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="325d7-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="325d7-120">若要下載並安裝擴充功能，按一下 [下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="325d7-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="325d7-121">在安裝好之後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="325d7-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="325d7-122">您也可以直接從 Visual Studio Marketplace 下載 [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) 與 [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)。</span><span class="sxs-lookup"><span data-stu-id="325d7-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="325d7-123">完成安裝之後，您就可以搭配使用 Azure 資源群組專案與邏輯應用程式設計工具。</span><span class="sxs-lookup"><span data-stu-id="325d7-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="325d7-124">建立專案</span><span class="sxs-lookup"><span data-stu-id="325d7-124">Create your project</span></span>

1. <span data-ttu-id="325d7-125">在 [檔案] 功能表上，移至 [新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="325d7-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="325d7-126">或者如果要將您的專案新增至現有的方案，請移至 [新增]，然後選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="325d7-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![[檔案] 功能表](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="325d7-128">在 [新增專案] 視窗中，尋找 [雲端]，然後選取 [Azure 資源群組]。</span><span class="sxs-lookup"><span data-stu-id="325d7-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="325d7-129">將您的專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="325d7-129">Name your project, and click **OK**.</span></span>

    ![加入新的專案](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="325d7-131">選取**邏輯應用程式**範本，其可建立空白的邏輯應用程式部署範本以供您使用。</span><span class="sxs-lookup"><span data-stu-id="325d7-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="325d7-132">選取您的範本後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="325d7-132">After you select your template, click **OK**.</span></span>

    ![選取 [邏輯應用程式] 範本](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="325d7-134">現在您已將邏輯應用程式新增至方案。</span><span class="sxs-lookup"><span data-stu-id="325d7-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="325d7-135">在 [方案總管] 中，您的部署檔案應該會出現。</span><span class="sxs-lookup"><span data-stu-id="325d7-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![部署檔案](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="325d7-137">利用邏輯應用程式設計工具建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="325d7-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="325d7-138">擁有包含邏輯應用程式的 Azure 資源群組專案時，您可以在 Visual Studio 內開啟邏輯應用程式設計工具以建立您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="325d7-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="325d7-139">設計工具需要網際網路連線，才能查詢連接器的可用屬性和資料。</span><span class="sxs-lookup"><span data-stu-id="325d7-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="325d7-140">例如，如果您使用 Dynamics CRM Online 連接器，設計工具會查詢您的 CRM 執行個體，以顯示可用的自訂與預設屬性。</span><span class="sxs-lookup"><span data-stu-id="325d7-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="325d7-141">以滑鼠右鍵按一下 `<template>.json` 檔案，然後選取 [使用邏輯應用程式設計工具來開啟]。</span><span class="sxs-lookup"><span data-stu-id="325d7-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="325d7-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="325d7-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="325d7-143">選擇部署範本的 Azure 訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="325d7-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="325d7-144">在設計邏輯應用程式時將會建立 API 連線資源，以在設計期間查詢屬性。</span><span class="sxs-lookup"><span data-stu-id="325d7-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="325d7-145">Visual Studio 會使用所選取的資源群組，在設計期間建立這些連線。</span><span class="sxs-lookup"><span data-stu-id="325d7-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="325d7-146">若要檢視或變更任何 API 連線，可前往 Azure 入口網站並瀏覽 **API 連線**。</span><span class="sxs-lookup"><span data-stu-id="325d7-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![訂用帳戶選擇器](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="325d7-148">設計工具會使用 `<template>.json` 檔案中的定義進行轉譯。</span><span class="sxs-lookup"><span data-stu-id="325d7-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="325d7-149">建立並設計邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="325d7-149">Create and design your logic app.</span></span> <span data-ttu-id="325d7-150">會使用變更來更新部署範本。</span><span class="sxs-lookup"><span data-stu-id="325d7-150">Your deployment template is updated with your changes.</span></span>

    ![Visual Studio 中的邏輯應用程式設計工具](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="325d7-152">Visual Studio 會針對您的邏輯應用程式需要函式的任何連線，將 `Microsoft.Web/connections` 資源新增至您的資源檔。</span><span class="sxs-lookup"><span data-stu-id="325d7-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="325d7-153">這些連線屬性可以在您部署時設定，並在您於 Azure 入口網站的 [API 連線] 中部署之後進行管理。</span><span class="sxs-lookup"><span data-stu-id="325d7-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="325d7-154">切換到 JSON 程式碼檢視</span><span class="sxs-lookup"><span data-stu-id="325d7-154">Switch to JSON code view</span></span>

<span data-ttu-id="325d7-155">若要顯示以 JSON 格式表示的邏輯應用程式，選取設計工具底部的 [程式碼檢視] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="325d7-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="325d7-156">若要切換回完整資源的 JSON，請以滑鼠右鍵按一下 `<template>.json` 檔案，然後選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="325d7-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="325d7-157">將相依資源的參考新增至 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="325d7-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="325d7-158">當您想要邏輯應用程式參考相依的資源時，您可以在邏輯應用程式部署範本中使用 [Azure Resource Manager 範本函式](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions)。</span><span class="sxs-lookup"><span data-stu-id="325d7-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="325d7-159">例如，您可能想要邏輯應用程式參考您要與邏輯應用程式一起部署的 Azure 函式或整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="325d7-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="325d7-160">遵循這些有關如何在部署範本中使用參數的指導方針，以便邏輯應用程式設計工具可正確轉譯。</span><span class="sxs-lookup"><span data-stu-id="325d7-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="325d7-161">您可以在這些類型的觸發程序和動作中使用邏輯應用程式參數︰</span><span class="sxs-lookup"><span data-stu-id="325d7-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="325d7-162">子工作流程</span><span class="sxs-lookup"><span data-stu-id="325d7-162">Child workflow</span></span>
*   <span data-ttu-id="325d7-163">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="325d7-163">Function app</span></span>
*   <span data-ttu-id="325d7-164">APIM 呼叫</span><span class="sxs-lookup"><span data-stu-id="325d7-164">APIM call</span></span>
*   <span data-ttu-id="325d7-165">API 連線執行階段 URL</span><span class="sxs-lookup"><span data-stu-id="325d7-165">API connection runtime URL</span></span>
*   <span data-ttu-id="325d7-166">API 連線路徑</span><span class="sxs-lookup"><span data-stu-id="325d7-166">API connection path</span></span>

<span data-ttu-id="325d7-167">您可以使用範本函式，例如 parameters、variables、resourceId、concat 等等。例如，以下是取代 Azure 函式資源識別碼的方式︰</span><span class="sxs-lookup"><span data-stu-id="325d7-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="325d7-168">以及您想使用參數的位置︰</span><span class="sxs-lookup"><span data-stu-id="325d7-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="325d7-169">另一個範例是您可以參數化服務匯流排傳送訊息作業：</span><span class="sxs-lookup"><span data-stu-id="325d7-169">As another example you can parameterize the Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="325d7-170">host.runtimeUrl 是選擇性的，如果存在的話，可以從您的範本中移除。</span><span class="sxs-lookup"><span data-stu-id="325d7-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="325d7-171">針對您在使用參數時要運作的邏輯應用程式設計工具，您必須提供預設值，例如︰</span><span class="sxs-lookup"><span data-stu-id="325d7-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="325d7-172">儲存您的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="325d7-172">Save your logic app</span></span>

<span data-ttu-id="325d7-173">若要隨時儲存邏輯應用程式，請移至 [檔案] > [儲存]。</span><span class="sxs-lookup"><span data-stu-id="325d7-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="325d7-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="325d7-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="325d7-175">如果當您儲存應用程式時邏輯應用程式有任何錯誤，它們會出現在 Visual Studio [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="325d7-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="325d7-176">從 Visual Studio 部署邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="325d7-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="325d7-177">設定應用程式之後，只要幾個步驟，就能從 Visual Studio 直接部署。</span><span class="sxs-lookup"><span data-stu-id="325d7-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="325d7-178">在 [方案總管] 中，以滑鼠右鍵按一下您的專案，並移至 [部署] > [新增部署...]</span><span class="sxs-lookup"><span data-stu-id="325d7-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![新增部署](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="325d7-180">當系統提示您時，登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="325d7-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="325d7-181">現在，您必須選取您要在其中部署邏輯應用程式的資源群組詳細資料。</span><span class="sxs-lookup"><span data-stu-id="325d7-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="325d7-182">完成後，選取 [部署]。</span><span class="sxs-lookup"><span data-stu-id="325d7-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="325d7-183">請確定您選取正確的資源群組範本和參數檔案。</span><span class="sxs-lookup"><span data-stu-id="325d7-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="325d7-184">例如，如果您想要部署到生產環境中，選擇生產參數檔。</span><span class="sxs-lookup"><span data-stu-id="325d7-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![部署到資源群組](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="325d7-186">部署狀態會出現在 [輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="325d7-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="325d7-187">您可能需要選取 [顯示輸出來源] 清單中的 [Azure 佈建]。</span><span class="sxs-lookup"><span data-stu-id="325d7-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![部署狀態輸出](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="325d7-189">未來，您可以在原始檔控制中編輯邏輯應用程式，並利用 Visual Studio 來部署新的版本。</span><span class="sxs-lookup"><span data-stu-id="325d7-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="325d7-190">如果您直接在 Azure 入口網站中變更定義，則下次從 Visual Studio 部署時會覆寫那些變更。</span><span class="sxs-lookup"><span data-stu-id="325d7-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="325d7-191">將邏輯應用程式新增到現有的資源群組專案</span><span class="sxs-lookup"><span data-stu-id="325d7-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="325d7-192">如果您有現有的資源群組專案，可以在 [JSON 大綱] 視窗中將邏輯應用程式新增至該專案。</span><span class="sxs-lookup"><span data-stu-id="325d7-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="325d7-193">您也可以您先前建立的應用程式共同新增另一個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="325d7-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="325d7-194">開啟 `<template>.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="325d7-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="325d7-195">若要開啟 [JSON 大綱] 視窗，請前往 [檢視] > [其他視窗] > [JSON 大綱]。</span><span class="sxs-lookup"><span data-stu-id="325d7-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="325d7-196">若要將資源新增至範本檔案，按一下 [JSON 大綱] 視窗頂端的 [新增資源]。</span><span class="sxs-lookup"><span data-stu-id="325d7-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="325d7-197">或在 [JSON 大綱] 視窗中，以滑鼠右鍵按一下 [資源]，然後選取 [新增資源]。</span><span class="sxs-lookup"><span data-stu-id="325d7-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![[JSON 大綱] 視窗](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="325d7-199">在 [新增資源] 對話方塊中，尋找並選取 [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="325d7-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="325d7-200">為您的邏輯應用程式命名，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="325d7-200">Name your logic app, and choose **Add**.</span></span>

    ![新增資源](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="325d7-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="325d7-202">Next Steps</span></span>

* [<span data-ttu-id="325d7-203">使用 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="325d7-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="325d7-204">檢視常見的範例和案例</span><span class="sxs-lookup"><span data-stu-id="325d7-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="325d7-205">了解如何使用 Azure Logic Apps 自動化商務程序</span><span class="sxs-lookup"><span data-stu-id="325d7-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="325d7-206">了解如何整合您的系統與 Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="325d7-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
