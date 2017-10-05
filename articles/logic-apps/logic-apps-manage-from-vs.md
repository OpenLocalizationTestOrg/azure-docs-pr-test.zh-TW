---
title: "在 Visual Studio 中管理邏輯應用程式 - Azure Logic Apps | Microsoft Docs"
description: "使用 Visual Studio Cloud Explorer 管理邏輯應用程式和其他 Azure 資產"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="b0970-103">使用 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b0970-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="b0970-104">雖然 [Azure 入口網站](https://portal.azure.com/)提供一種絕佳的方式讓您能夠設計和管理 Azure Logic Apps，但您可以使用 Visual Studio Cloud Explorer 來管理許多 Azure 資產 (包括 Logic Apps)。</span><span class="sxs-lookup"><span data-stu-id="b0970-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="b0970-105">Visual Studio Cloud Explorer 可讓您瀏覽、管理、編輯和下載已發佈的 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="b0970-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="b0970-106">管理工作包括啟用、停用及檢視執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="b0970-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="b0970-107">您必須先安裝和設定適用於 Azure Logic Apps 的 Visual Studio 工具，才能在 Visual Studio 中存取及管理 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="b0970-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b0970-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="b0970-108">Prerequisites</span></span>

* [<span data-ttu-id="b0970-109">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b0970-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="b0970-110">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="b0970-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="b0970-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="b0970-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="b0970-112">Web 的存取權 (若使用內嵌的設計工具)</span><span class="sxs-lookup"><span data-stu-id="b0970-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="b0970-113">安裝適用於 Logic Apps 的 Visual Studio 工具</span><span class="sxs-lookup"><span data-stu-id="b0970-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="b0970-114">安裝必要條件之後，請下載並安裝 Azure Logic Apps Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b0970-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="b0970-115">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b0970-115">Open Visual Studio.</span></span> <span data-ttu-id="b0970-116">在 [工具] 功能表上，選取 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="b0970-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="b0970-117">展開 [線上] 類別讓您可以在 Visual Studio 資源庫中進行線上搜尋。</span><span class="sxs-lookup"><span data-stu-id="b0970-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="b0970-118">瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="b0970-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="b0970-119">若要下載並安裝擴充功能，按一下 [下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0970-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="b0970-120">在安裝好之後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b0970-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="b0970-121">若要直接下載 Azure Logic Apps Tools for Visual Studio，請前往 [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)。</span><span class="sxs-lookup"><span data-stu-id="b0970-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="b0970-122">在 Cloud Explorer 中瀏覽邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b0970-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="b0970-123">若要開啟 Cloud Explorer，在 [檢視] 功能表上，選擇 [Cloud Explorer]。</span><span class="sxs-lookup"><span data-stu-id="b0970-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="b0970-124">依資源群組或資源類型瀏覽邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0970-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="b0970-125">如果您要依資源類型進行瀏覽，請選取您的 Azure 訂用帳戶、展開 [Logic Apps] 區段，然後選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0970-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="b0970-126">如果您要依資源群組進行瀏覽，請展開包含您邏輯應用程式的資源群組，然後選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0970-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="b0970-127">若要檢視您邏輯應用程式的命令，請以滑鼠右鍵按一下您的邏輯應用程式，或是在 Cloud Explorer 底部，從 [動作] 功能表進行選擇。</span><span class="sxs-lookup"><span data-stu-id="b0970-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![瀏覽邏輯應用程式](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="b0970-129">使用 Logic Apps 設計工具編輯邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b0970-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="b0970-130">您可以從 Cloud Explorer，以您在 Azure 入口網站中所使用的相同設計工具，來開啟目前部署的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0970-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="b0970-131">若要編輯您的邏輯應用程式，請在 Cloud Explorer 中，以滑鼠右鍵按一下您的邏輯應用程式，然後選取 [使用邏輯應用程式編輯器開啟]。</span><span class="sxs-lookup"><span data-stu-id="b0970-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="b0970-132">若要將您的更新發佈到雲端，請選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="b0970-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="b0970-133">若要啟動新的執行，請選擇 [執行觸發程序]。</span><span class="sxs-lookup"><span data-stu-id="b0970-133">To start a new run, choose **Run Trigger**.</span></span>

![Logic Apps 設計工具](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="b0970-135">您也可以從設計工具**下載**邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0970-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="b0970-136">此動作會自動參數化邏輯應用程式定義，並將定義儲存為 Azure Resource Manager 部署範本。</span><span class="sxs-lookup"><span data-stu-id="b0970-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="b0970-137">您可以將此部署範本新增至 Azure 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="b0970-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="b0970-138">瀏覽邏輯應用程式執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="b0970-138">Browse your logic app run history</span></span>

<span data-ttu-id="b0970-139">若要檢視邏輯應用程式的執行歷程記錄，在邏輯應用程式上按一下滑鼠右鍵，然後選取 [開啟執行歷程記錄]。</span><span class="sxs-lookup"><span data-stu-id="b0970-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="b0970-140">若要根據任何顯示的屬性重新排列您的執行歷程記錄，請選取該欄標頭。</span><span class="sxs-lookup"><span data-stu-id="b0970-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![執行記錄](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="b0970-142">若要顯示執行個體的執行歷程記錄，讓您可以檢閱該次執行的結果 (包括每個步驟的輸入和輸出)，請按兩下其中一個執行的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b0970-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![步驟所產生的執行歷程記錄結果、輸入和輸出](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="b0970-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0970-144">Next steps</span></span>

* [<span data-ttu-id="b0970-145">建立第一個邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b0970-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="b0970-146">在 Visual Studio 中設計、建置和部署 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b0970-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="b0970-147">檢視常見的範例和案例</span><span class="sxs-lookup"><span data-stu-id="b0970-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* <span data-ttu-id="b0970-148">[影片：Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (使用 Azure Logic Apps 自動化商業程序)</span><span class="sxs-lookup"><span data-stu-id="b0970-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)</span></span>
* <span data-ttu-id="b0970-149">[影片：Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (整合您的系統與 Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="b0970-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)</span></span>
