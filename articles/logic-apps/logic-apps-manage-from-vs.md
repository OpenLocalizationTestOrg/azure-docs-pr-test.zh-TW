---
title: "在 Visual Studio-Azure 邏輯應用程式中的 aaaManage logic apps |Microsoft 文件"
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="25537-103">使用 Visual Studio Cloud Explorer 管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="25537-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="25537-104">雖然 hello [Azure 入口網站](https://portal.azure.com/)toodesign 為您提供絕佳的方式和管理 Azure 邏輯應用程式，您可以使用 Visual Studio Cloud Explorer 管理許多 Azure 資產，包括邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="25537-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="25537-105">Visual Studio Cloud Explorer 可讓您瀏覽、管理、編輯和下載已發佈的 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="25537-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="25537-106">管理工作包括啟用、停用及檢視執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="25537-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="25537-107">您必須先安裝和設定適用於 Azure Logic Apps 的 Visual Studio 工具，才能在 Visual Studio 中存取及管理 Logic Apps。</span><span class="sxs-lookup"><span data-stu-id="25537-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="25537-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="25537-108">Prerequisites</span></span>

* [<span data-ttu-id="25537-109">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="25537-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="25537-110">[最新的 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="25537-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="25537-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="25537-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="25537-112">使用 hello 內嵌設計工具時，存取 toohello web</span><span class="sxs-lookup"><span data-stu-id="25537-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="25537-113">安裝適用於 Logic Apps 的 Visual Studio 工具</span><span class="sxs-lookup"><span data-stu-id="25537-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="25537-114">安裝 hello 必要條件之後，請下載並安裝適用於 Visual Studio hello Azure 邏輯應用程式工具。</span><span class="sxs-lookup"><span data-stu-id="25537-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="25537-115">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25537-115">Open Visual Studio.</span></span> <span data-ttu-id="25537-116">在 hello**工具**功能表上，選取**擴充功能和更新**。</span><span class="sxs-lookup"><span data-stu-id="25537-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="25537-117">展開 hello**線上**類別讓您可以搜尋線上 hello Visual Studio 組件庫中。</span><span class="sxs-lookup"><span data-stu-id="25537-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="25537-118">瀏覽或搜尋 [Logic Apps]，直到您找出 [Azure Logic Apps Tools for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="25537-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="25537-119">toodownload 和安裝 hello 副檔名，請按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="25537-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="25537-120">在安裝好之後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25537-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="25537-121">toodownload hello Azure 邏輯應用程式 Tools for Visual Studio 會直接移 toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)。</span><span class="sxs-lookup"><span data-stu-id="25537-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="25537-122">在 Cloud Explorer 中瀏覽邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="25537-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="25537-123">在 hello tooopen Cloud Explorer**檢視**功能表上，選擇**Cloud Explorer**。</span><span class="sxs-lookup"><span data-stu-id="25537-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="25537-124">依資源群組或資源類型瀏覽邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="25537-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="25537-125">如果您瀏覽資源類型，選取您的 Azure 訂用帳戶中，展開 hello **Logic Apps**區段，然後選取 應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="25537-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="25537-126">如果您瀏覽資源群組，展開具有應用程式邏輯，hello 資源群組，並選取邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="25537-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="25537-127">tooview 命令邏輯應用程式中，請以滑鼠右鍵按一下應用程式邏輯，或在 Cloud Explorer hello 下方，選擇從 hello**動作**功能表。</span><span class="sxs-lookup"><span data-stu-id="25537-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![瀏覽邏輯應用程式](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="25537-129">使用 Logic Apps 設計工具編輯邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="25537-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="25537-130">您可以從雲端總管 中，開啟目前部署的邏輯應用程式在 hello hello Azure 入口網站中使用相同的設計工具。</span><span class="sxs-lookup"><span data-stu-id="25537-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="25537-131">tooedit 邏輯應用程式，在 Cloud Explorer 中的以滑鼠右鍵按一下應用程式邏輯，並選取**使用邏輯應用程式編輯器開啟**。</span><span class="sxs-lookup"><span data-stu-id="25537-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="25537-132">toopublish 更新 toohello 雲端選擇**發行**。</span><span class="sxs-lookup"><span data-stu-id="25537-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="25537-133">toostart 新的執行中，選擇**執行觸發程序**。</span><span class="sxs-lookup"><span data-stu-id="25537-133">toostart a new run, choose **Run Trigger**.</span></span>

![Logic Apps 設計工具](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="25537-135">Hello 設計工具中，您也可以**下載**邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="25537-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="25537-136">此動作自動參數化 hello 邏輯應用程式定義，並將 hello 定義儲存為 Azure Resource Manager 部署範本。</span><span class="sxs-lookup"><span data-stu-id="25537-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="25537-137">您可以加入這個部署範本 tooyour Azure 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="25537-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="25537-138">瀏覽邏輯應用程式執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="25537-138">Browse your logic app run history</span></span>

<span data-ttu-id="25537-139">tooview hello 執行歷程記錄的應用程式邏輯，以滑鼠右鍵按一下應用程式邏輯，並選取**開啟執行歷程記錄**。</span><span class="sxs-lookup"><span data-stu-id="25537-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="25537-140">tooreorder 程式執行歷程記錄，根據任何 hello 屬性顯示，請選取 hello 資料行標頭。</span><span class="sxs-lookup"><span data-stu-id="25537-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![執行記錄](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="25537-142">tooshow hello 執行歷程記錄執行個體，因此您可以檢閱 hello 執行的結果，包括 hello 輸入和輸出來自每個步驟中，按兩下其中一個 hello 執行執行個體。</span><span class="sxs-lookup"><span data-stu-id="25537-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![步驟所產生的執行歷程記錄結果、輸入和輸出](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="25537-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25537-144">Next steps</span></span>

* [<span data-ttu-id="25537-145">建立第一個邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="25537-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="25537-146">在 Visual Studio 中設計、建置和部署 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="25537-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="25537-147">檢視常見的範例和案例</span><span class="sxs-lookup"><span data-stu-id="25537-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* <span data-ttu-id="25537-148">[影片：Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (使用 Azure Logic Apps 自動化商業程序)</span><span class="sxs-lookup"><span data-stu-id="25537-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)</span></span>
* <span data-ttu-id="25537-149">[影片：Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (整合您的系統與 Azure Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="25537-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)</span></span>
