---
title: "Application Insights 的發行註解 | Microsoft Docs"
description: "在 Application Insights 中對計量瀏覽器新增部署或建置標記。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="bc633-103">Application Insights 中度量圖表上的註解</span><span class="sxs-lookup"><span data-stu-id="bc633-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="bc633-104">[計量瀏覽器](app-insights-metrics-explorer.md)圖表上的註解會顯示您在哪裡部署了新的組建，或是其他重要事件。</span><span class="sxs-lookup"><span data-stu-id="bc633-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="bc633-105">註解可讓您輕鬆查看變更是否對應用程式的效能有任何影響。</span><span class="sxs-lookup"><span data-stu-id="bc633-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="bc633-106">[Visual Studio Team Services 建置系統](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)可以自動建立這些註解。</span><span class="sxs-lookup"><span data-stu-id="bc633-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="bc633-107">您也可以[從 PowerShell 建立註解](#create-annotations-from-powershell)來標幟您想要的任何事件。</span><span class="sxs-lookup"><span data-stu-id="bc633-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![註解範例，其會顯示與伺服器回應時間的相互關聯](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="bc633-109">與 VSTS 組建搭配的發行註解</span><span class="sxs-lookup"><span data-stu-id="bc633-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="bc633-110">發行註解是 Visual Studio Team Services 的雲端型組建和發行服務的功能。</span><span class="sxs-lookup"><span data-stu-id="bc633-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="bc633-111">安裝註解擴充功能 (一次)</span><span class="sxs-lookup"><span data-stu-id="bc633-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="bc633-112">若要能夠建立發行註解，必須安裝 Visual Studio Marketplace 中許多可用 Team Service 擴充功能的其中一個。</span><span class="sxs-lookup"><span data-stu-id="bc633-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="bc633-113">登入您的 [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) 專案。</span><span class="sxs-lookup"><span data-stu-id="bc633-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="bc633-114">在 Visual Studio Marketplace 中， [取得發行註解擴充功能](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)，並將其加入至 Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc633-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![在 Team Services 網頁右上角開啟 Marketplace。](./media/app-insights-annotations/10.png)

<span data-ttu-id="bc633-117">您只需要為 Visual Studio Team Services 帳戶執行一次。</span><span class="sxs-lookup"><span data-stu-id="bc633-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="bc633-118">現在就能為帳戶中的任何專案設定發行註解。</span><span class="sxs-lookup"><span data-stu-id="bc633-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="bc633-119">設定發行註解</span><span class="sxs-lookup"><span data-stu-id="bc633-119">Configure release annotations</span></span>

<span data-ttu-id="bc633-120">您必須為每個 VSTS 發行範本取得個別的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bc633-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="bc633-121">登入 [Microsoft Azure 入口網站](https://portal.azure.com)，然後開啟監視您應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="bc633-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="bc633-122">(或如果您尚未建立該資源，請[立即建立一個](app-insights-overview.md))。</span><span class="sxs-lookup"><span data-stu-id="bc633-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="bc633-123">開啟 [API 存取]、[Application Insights 識別碼]。</span><span class="sxs-lookup"><span data-stu-id="bc633-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![在 portal.azure.com 中，開啟您的 Application Insights 資源然後選擇 [設定]。](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="bc633-127">在另一個瀏覽器視窗中，開啟 (或建立) 可從 Visual Studio Team Services 管理部署的發行範本。</span><span class="sxs-lookup"><span data-stu-id="bc633-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="bc633-128">新增工作，然後從功能表中選取 Application Insights 發行註解工作。</span><span class="sxs-lookup"><span data-stu-id="bc633-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="bc633-129">將您從 [API 存取] 刀鋒視窗複製的應用程式識別碼  貼上。</span><span class="sxs-lookup"><span data-stu-id="bc633-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![在 Visual Studio Team Services 中，開啟 [發行]，選取一項發行定義，然後選擇 [編輯]。](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="bc633-133">將 [APIKey] 欄位設定為變數 `$(ApiKey)`。</span><span class="sxs-lookup"><span data-stu-id="bc633-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="bc633-134">回到 Azure 視窗，建立新的「API 金鑰」並複製它。</span><span class="sxs-lookup"><span data-stu-id="bc633-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![在 [Azure] 視窗的 [API 存取] 刀鋒視窗中，按一下 [建立 API 金鑰]。](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="bc633-138">開啟發行範本的 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bc633-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="bc633-139">建立 `ApiKey`的變數定義。</span><span class="sxs-lookup"><span data-stu-id="bc633-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="bc633-140">將您的 API 金鑰貼上至 ApiKey 變數定義。</span><span class="sxs-lookup"><span data-stu-id="bc633-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![在 [Team Services] 視窗中，選取 [設定] 索引標籤然後按一下 [新增變數]。](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="bc633-143">最後，儲存  發行定義。</span><span class="sxs-lookup"><span data-stu-id="bc633-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="bc633-144">檢視註解</span><span class="sxs-lookup"><span data-stu-id="bc633-144">View annotations</span></span>
<span data-ttu-id="bc633-145">現在，每當您使用發行範本來部署新的發行，就會將註解傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="bc633-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="bc633-146">註解將會出現在計量瀏覽器的圖表上。</span><span class="sxs-lookup"><span data-stu-id="bc633-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="bc633-147">按一下任一註解標記即可開啟版本的詳細資料，包括要求者、來源控制分支、版本定義、環境等。</span><span class="sxs-lookup"><span data-stu-id="bc633-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![按一下任一版本註解標記。](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="bc633-149">從 PowerShell 建立自訂註解</span><span class="sxs-lookup"><span data-stu-id="bc633-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="bc633-150">您也可以從任何您喜歡的處理程序建立註解 (不使用 VS Team System)。</span><span class="sxs-lookup"><span data-stu-id="bc633-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="bc633-151">建立一個[來自 GitHub 的 Powershell 指令碼](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)的本機複本。</span><span class="sxs-lookup"><span data-stu-id="bc633-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="bc633-152">從 [API 存取] 刀鋒視窗中取得「應用程式識別碼」並建立 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bc633-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="bc633-153">依下列方式呼叫指令碼：</span><span class="sxs-lookup"><span data-stu-id="bc633-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="bc633-154">修改指令碼很簡單，例如，修改成建立過去的註解。</span><span class="sxs-lookup"><span data-stu-id="bc633-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc633-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc633-155">Next steps</span></span>

* [<span data-ttu-id="bc633-156">建立工作項目</span><span class="sxs-lookup"><span data-stu-id="bc633-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="bc633-157">使用 PowerShell 進行自動化</span><span class="sxs-lookup"><span data-stu-id="bc633-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
