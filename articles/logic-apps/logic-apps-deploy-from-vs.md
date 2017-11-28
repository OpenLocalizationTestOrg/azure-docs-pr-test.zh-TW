---
title: "aaaCreate、 建置及部署 Visual Studio-Azure 邏輯應用程式中的 logic apps |Microsoft 文件"
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
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="ad85e-103">在 Visual Studio 中設計、建置和部署 Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ad85e-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="ad85e-104">雖然 hello [Azure 入口網站](https://portal.azure.com/)toocreate 為您提供絕佳的方式和管理 Azure 邏輯應用程式，您可以使用 Visual Studio 設計、 建置和部署您的 logic apps。</span><span class="sxs-lookup"><span data-stu-id="ad85e-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="ad85e-105">Visual Studio 提供豐富的工具，像是 hello 邏輯應用程式的設計工具為您 toocreate 邏輯應用程式、 設定部署和自動化範本和部署 tooany 環境。</span><span class="sxs-lookup"><span data-stu-id="ad85e-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="ad85e-106">Azure 邏輯應用程式，以啟動 tooget 深入了解[如何 toocreate hello Azure 入口網站中的第一個邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ad85e-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="ad85e-107">安裝步驟</span><span class="sxs-lookup"><span data-stu-id="ad85e-107">Installation steps</span></span>

<span data-ttu-id="ad85e-108">tooinstall 和設定 Visual Studio tools for Azure 邏輯應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ad85e-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ad85e-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ad85e-109">Prerequisites</span></span>

* <span data-ttu-id="ad85e-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 或 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ad85e-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="ad85e-111">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="ad85e-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="ad85e-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad85e-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="ad85e-113">使用 hello 內嵌設計工具時，存取 toohello web</span><span class="sxs-lookup"><span data-stu-id="ad85e-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="ad85e-114">安裝適用於 Azure Logic Apps 的 Visual Studio 工具</span><span class="sxs-lookup"><span data-stu-id="ad85e-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="ad85e-115">之後您安裝 hello 必要條件：</span><span class="sxs-lookup"><span data-stu-id="ad85e-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="ad85e-116">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ad85e-116">Open Visual Studio.</span></span> <span data-ttu-id="ad85e-117">在 hello**工具**功能表上，選取**擴充功能和更新**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="ad85e-118">展開 hello**線上**類別讓您可以在線上搜尋。</span><span class="sxs-lookup"><span data-stu-id="ad85e-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="ad85e-119">瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="ad85e-120">toodownload 和安裝 hello 副檔名，請按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="ad85e-121">在安裝好之後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ad85e-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="ad85e-122">您也可以下載[Azure 邏輯應用程式 Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)和 hello [Azure 邏輯應用程式 Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)直接從 Visual Studio Marketplace hello。</span><span class="sxs-lookup"><span data-stu-id="ad85e-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="ad85e-123">完成安裝之後，您可以使用邏輯應用程式的設計工具來 hello Azure 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="ad85e-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="ad85e-124">建立專案</span><span class="sxs-lookup"><span data-stu-id="ad85e-124">Create your project</span></span>

1. <span data-ttu-id="ad85e-125">在 hello**檔案**功能表上，移過**新增**，然後選取**專案**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="ad85e-126">或 tooadd 太現有方案中，移至您的專案 tooan**新增**，然後選取**新專案**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![[檔案] 功能表](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="ad85e-128">在 hello**新專案**視窗中，尋找**雲端**，並選取**Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="ad85e-129">將您的專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-129">Name your project, and click **OK**.</span></span>

    ![加入新的專案](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="ad85e-131">選取 hello**邏輯應用程式**toouse 為您建立空白的邏輯應用程式的部署範本的範本。</span><span class="sxs-lookup"><span data-stu-id="ad85e-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="ad85e-132">選取您的範本後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-132">After you select your template, click **OK**.</span></span>

    ![選取 [邏輯應用程式] 範本](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="ad85e-134">您現在已加入邏輯應用程式專案 tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="ad85e-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="ad85e-135">在 [hello 方案總管] 中，您部署的檔案應該會出現。</span><span class="sxs-lookup"><span data-stu-id="ad85e-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![部署檔案](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="ad85e-137">利用邏輯應用程式設計工具建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="ad85e-138">當您有 Azure 資源群組專案包含邏輯應用程式時，您可以 hello 邏輯應用程式的設計工具中開啟 Visual Studio toocreate 您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="ad85e-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad85e-139">hello 設計工具需要網際網路連線太查詢可用的屬性和資料的連接器。</span><span class="sxs-lookup"><span data-stu-id="ad85e-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="ad85e-140">例如，如果您使用 hello Dynamics CRM Online 連接器，hello 設計工具會查詢您的 CRM 執行個體 tooshow 可用自訂與預設屬性。</span><span class="sxs-lookup"><span data-stu-id="ad85e-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="ad85e-141">以滑鼠右鍵按一下 `<template>.json` 檔案，然後選取 [使用邏輯應用程式設計工具來開啟]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="ad85e-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="ad85e-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="ad85e-143">選擇部署範本的 Azure 訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="ad85e-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad85e-144">在設計邏輯應用程式時將會建立 API 連線資源，以在設計期間查詢屬性。</span><span class="sxs-lookup"><span data-stu-id="ad85e-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="ad85e-145">Visual Studio 在設計階段期間，這些連接將使用您選取的資源群組 toocreate。</span><span class="sxs-lookup"><span data-stu-id="ad85e-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="ad85e-146">tooview 或變更任何應用程式開發介面連接 toohello Azure 入口網站，請瀏覽**API 連線**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![訂用帳戶選擇器](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="ad85e-148">hello 設計工具會使用 hello 定義在 hello`<template>.json`轉譯的檔案。</span><span class="sxs-lookup"><span data-stu-id="ad85e-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="ad85e-149">建立並設計邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad85e-149">Create and design your logic app.</span></span> <span data-ttu-id="ad85e-150">會使用變更來更新部署範本。</span><span class="sxs-lookup"><span data-stu-id="ad85e-150">Your deployment template is updated with your changes.</span></span>

    ![Visual Studio 中的邏輯應用程式設計工具](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="ad85e-152">Visual Studio 會加入`Microsoft.Web/connections`資源過您的資源檔案的任何連線邏輯應用程式需要 toofunction。</span><span class="sxs-lookup"><span data-stu-id="ad85e-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="ad85e-153">這些連接屬性可以設定部署時，並在部署之後，管理**API 連線**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ad85e-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="ad85e-154">切換 tooJSON 程式碼檢視</span><span class="sxs-lookup"><span data-stu-id="ad85e-154">Switch tooJSON code view</span></span>

<span data-ttu-id="ad85e-155">tooshow hello 邏輯應用程式，選取 hello 的 JSON 表示法**程式碼檢視**在 hello hello 設計工具底部的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ad85e-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="ad85e-156">tooswitch 回 toohello 完整資源 JSON，以滑鼠右鍵按一下 hello`<template>.json`檔案，然後選取**開啟**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="ad85e-157">加入相依的資源 tooVisual Studio 部署範本的參考</span><span class="sxs-lookup"><span data-stu-id="ad85e-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="ad85e-158">當您希望邏輯應用程式 tooreference 相依資源時，您可以使用[Azure Resource Manager 範本函式](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions)在邏輯應用程式部署範本中。</span><span class="sxs-lookup"><span data-stu-id="ad85e-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="ad85e-159">比方說，您可能會想您邏輯應用程式 tooreference 您想要讓 toodeploy，隨應用程式邏輯一起 Azure 功能或整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad85e-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="ad85e-160">遵循這些指導方針，關於 toouse 參數，在您部署範本，因此，hello 邏輯應用程式的設計工具中正確轉譯的方式。</span><span class="sxs-lookup"><span data-stu-id="ad85e-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="ad85e-161">您可以在這些類型的觸發程序和動作中使用邏輯應用程式參數︰</span><span class="sxs-lookup"><span data-stu-id="ad85e-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="ad85e-162">子工作流程</span><span class="sxs-lookup"><span data-stu-id="ad85e-162">Child workflow</span></span>
*   <span data-ttu-id="ad85e-163">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-163">Function app</span></span>
*   <span data-ttu-id="ad85e-164">APIM 呼叫</span><span class="sxs-lookup"><span data-stu-id="ad85e-164">APIM call</span></span>
*   <span data-ttu-id="ad85e-165">API 連線執行階段 URL</span><span class="sxs-lookup"><span data-stu-id="ad85e-165">API connection runtime URL</span></span>
*   <span data-ttu-id="ad85e-166">API 連線路徑</span><span class="sxs-lookup"><span data-stu-id="ad85e-166">API connection path</span></span>

<span data-ttu-id="ad85e-167">您可以使用範本函式，例如 parameters、variables、resourceId、concat 等等。例如，以下是如何取代 hello Azure 函式的資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="ad85e-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="ad85e-168">以及您想使用參數的位置︰</span><span class="sxs-lookup"><span data-stu-id="ad85e-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="ad85e-169">另一個範例中，您可以參數化的 hello 服務匯流排傳送訊息作業：</span><span class="sxs-lookup"><span data-stu-id="ad85e-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

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
> <span data-ttu-id="ad85e-170">host.runtimeUrl 是選擇性的，如果存在的話，可以從您的範本中移除。</span><span class="sxs-lookup"><span data-stu-id="ad85e-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="ad85e-171">Hello 邏輯應用程式的設計工具 toowork 時使用參數，您必須提供預設值，例如：</span><span class="sxs-lookup"><span data-stu-id="ad85e-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="ad85e-172">儲存您的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-172">Save your logic app</span></span>

<span data-ttu-id="ad85e-173">toosave 在任何時候，應用程式邏輯移過**檔案** > **儲存**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="ad85e-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="ad85e-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="ad85e-175">如果應用程式邏輯會有任何錯誤，當您儲存您的應用程式時，它們會出現在 hello Visual Studio**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="ad85e-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="ad85e-176">從 Visual Studio 部署邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="ad85e-177">設定應用程式之後，只要幾個步驟，就能從 Visual Studio 直接部署。</span><span class="sxs-lookup"><span data-stu-id="ad85e-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="ad85e-178">在方案總管 中，以滑鼠右鍵按一下您的專案，並跳過**部署** > **新部署...**</span><span class="sxs-lookup"><span data-stu-id="ad85e-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![新增部署](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="ad85e-180">當提示您時，請登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad85e-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="ad85e-181">現在，您必須選取 hello hello 想 toodeploy 邏輯應用程式的資源群組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ad85e-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="ad85e-182">完成後，選取 [部署]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad85e-183">請確定您選取 hello 正確的範本和參數檔案 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ad85e-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="ad85e-184">例如，如果您想 toodeploy tooa 生產環境中，選擇 hello 生產參數檔案。</span><span class="sxs-lookup"><span data-stu-id="ad85e-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![部署 tooresource 群組](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="ad85e-186">hello 部署狀態會顯示在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="ad85e-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="ad85e-187">您可能必須 tooselect **Azure 佈建**在 hello**顯示輸出來源**清單。</span><span class="sxs-lookup"><span data-stu-id="ad85e-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![部署狀態輸出](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="ad85e-189">在 hello 未來，您可以編輯原始檔控制中的應用程式邏輯，並使用 Visual Studio toodeploy 新版本。</span><span class="sxs-lookup"><span data-stu-id="ad85e-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="ad85e-190">如果您直接變更 hello Azure 入口網站中的 hello 定義，當從 Visual Studio 部署下一次時，會覆寫這些變更。</span><span class="sxs-lookup"><span data-stu-id="ad85e-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="ad85e-191">新增邏輯應用程式 tooan 現有資源群組專案</span><span class="sxs-lookup"><span data-stu-id="ad85e-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="ad85e-192">如果您有現有的資源群組專案時，您可以加入邏輯應用程式 toothat 專案 hello [JSON 大綱] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="ad85e-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="ad85e-193">您也可以加入另一個邏輯應用程式，以及您先前建立的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad85e-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="ad85e-194">開啟 hello`<template>.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="ad85e-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="ad85e-195">tooopen hello JSON 大綱 視窗中，跳過**檢視** > **其他視窗** > **JSON 大綱**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="ad85e-196">tooadd 資源 toohello 範本檔，按一下**加入資源**在 hello hello [JSON 大綱] 視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="ad85e-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="ad85e-197">或在 hello [JSON 大綱] 視窗，以滑鼠右鍵按一下**資源**，然後選取**加入新的資源**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![[JSON 大綱] 視窗](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="ad85e-199">在 hello**加入資源**對話方塊中，尋找並選取**邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ad85e-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="ad85e-200">為您的邏輯應用程式命名，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ad85e-200">Name your logic app, and choose **Add**.</span></span>

    ![新增資源](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="ad85e-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad85e-202">Next Steps</span></span>

* [<span data-ttu-id="ad85e-203">使用 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="ad85e-204">檢視常見的範例和案例</span><span class="sxs-lookup"><span data-stu-id="ad85e-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="ad85e-205">了解如何 tooautomate 商務程序與 Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="ad85e-206">深入了解如何 toointegrate 系統與 Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ad85e-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
