---
title: "Application Insights aaaRelease 註釋 |Microsoft 文件"
description: "新增部署或建置 tooyour 度量總管圖表 Application Insights 中的標記。"
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="30b58-103">Application Insights 中度量圖表上的註解</span><span class="sxs-lookup"><span data-stu-id="30b58-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="30b58-104">[計量瀏覽器](app-insights-metrics-explorer.md)圖表上的註解會顯示您在哪裡部署了新的組建，或是其他重要事件。</span><span class="sxs-lookup"><span data-stu-id="30b58-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="30b58-105">這個選項讓您輕鬆 toosee 是否變更沒有任何作用，對您的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="30b58-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="30b58-106">它們可以自動建立 hello[建置系統，Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)。</span><span class="sxs-lookup"><span data-stu-id="30b58-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="30b58-107">您也可以建立註解 tooflag 您喜歡的任何事件[建立它們從 PowerShell](#create-annotations-from-powershell)。</span><span class="sxs-lookup"><span data-stu-id="30b58-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![註解範例，其會顯示與伺服器回應時間的相互關聯](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="30b58-109">與 VSTS 組建搭配的發行註解</span><span class="sxs-lookup"><span data-stu-id="30b58-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="30b58-110">版本註解是 hello 以雲端為基礎建置的功能和版本的 Visual Studio Team Services 的服務。</span><span class="sxs-lookup"><span data-stu-id="30b58-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="30b58-111">安裝 hello 註解延伸模組 （一次）</span><span class="sxs-lookup"><span data-stu-id="30b58-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="30b58-112">toobe 無法 toocreate 版本註解，您將需要一個 tooinstall hello 的許多小組服務延伸模組用於 hello Visual Studio Marketplace。</span><span class="sxs-lookup"><span data-stu-id="30b58-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="30b58-113">登入 tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online)專案。</span><span class="sxs-lookup"><span data-stu-id="30b58-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="30b58-114">在 Visual Studio Marketplace， [hello 的版本註解延伸](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)，並將它加入 tooyour Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30b58-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![在 Team Services 網頁右上角開啟 Marketplace。](./media/app-insights-annotations/10.png)

<span data-ttu-id="30b58-117">您只需要 toodo 這一次為您的 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30b58-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="30b58-118">現在就能為帳戶中的任何專案設定發行註解。</span><span class="sxs-lookup"><span data-stu-id="30b58-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="30b58-119">設定發行註解</span><span class="sxs-lookup"><span data-stu-id="30b58-119">Configure release annotations</span></span>

<span data-ttu-id="30b58-120">您為每個 VSTS 發行範本需要 tooget 的個別 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="30b58-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="30b58-121">登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)並開啟 hello 監視您的應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="30b58-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="30b58-122">(或如果您尚未建立該資源，請[立即建立一個](app-insights-overview.md))。</span><span class="sxs-lookup"><span data-stu-id="30b58-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="30b58-123">開啟 [API 存取]、[Application Insights 識別碼]。</span><span class="sxs-lookup"><span data-stu-id="30b58-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![在 portal.azure.com 中，開啟您的 Application Insights 資源然後選擇 [設定]。](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="30b58-127">在另一個瀏覽器視窗中，開啟 （或建立） 從 Visual Studio Team Services 中管理您的部署的 hello 發行範本。</span><span class="sxs-lookup"><span data-stu-id="30b58-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="30b58-128">將工作，並從 hello 功能表選取 hello 應用程式 Insights 版本註解工作。</span><span class="sxs-lookup"><span data-stu-id="30b58-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="30b58-129">貼上 hello**應用程式識別碼**從 hello API 存取 刀鋒視窗中複製。</span><span class="sxs-lookup"><span data-stu-id="30b58-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![在 Visual Studio Team Services 中，開啟 [發行]，選取一項發行定義，然後選擇 [編輯]。](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="30b58-133">設定 hello **APIKey**欄位 tooa 變數`$(ApiKey)`。</span><span class="sxs-lookup"><span data-stu-id="30b58-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="30b58-134">回到 hello Azure 的視窗，建立新的 API 金鑰，需要一份。</span><span class="sxs-lookup"><span data-stu-id="30b58-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![在 hello hello Azure 視窗中的應用程式開發介面存取刀鋒視窗中，按一下 建立 API 金鑰。](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="30b58-138">開啟 hello hello 發行範本的 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="30b58-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="30b58-139">建立 `ApiKey`的變數定義。</span><span class="sxs-lookup"><span data-stu-id="30b58-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="30b58-140">貼上您的 API 金鑰 toohello ApiKey 變數定義。</span><span class="sxs-lookup"><span data-stu-id="30b58-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Hello Team Services 在視窗中，請選取 hello 組態] 索引標籤，然後按一下 [加入變數。](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="30b58-143">最後，**儲存**hello 發行定義。</span><span class="sxs-lookup"><span data-stu-id="30b58-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="30b58-144">檢視註解</span><span class="sxs-lookup"><span data-stu-id="30b58-144">View annotations</span></span>
<span data-ttu-id="30b58-145">現在，當您使用 hello 發行範本 toodeploy 新版本，註解將會傳送 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="30b58-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="30b58-146">hello 註解會顯示在計量瀏覽器中的圖表。</span><span class="sxs-lookup"><span data-stu-id="30b58-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="30b58-147">按一下任何註解標記 tooopen 詳細 hello 版本中，包括要求者、 原始檔控制分支、 發行定義、 環境、 等等。</span><span class="sxs-lookup"><span data-stu-id="30b58-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![按一下任一版本註解標記。](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="30b58-149">從 PowerShell 建立自訂註解</span><span class="sxs-lookup"><span data-stu-id="30b58-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="30b58-150">您也可以從任何您喜歡的處理程序建立註解 (不使用 VS Team System)。</span><span class="sxs-lookup"><span data-stu-id="30b58-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="30b58-151">建立的本機副本 hello [Powershell 指令碼從 GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)。</span><span class="sxs-lookup"><span data-stu-id="30b58-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="30b58-152">取得 hello 應用程式識別碼，並建立 API 金鑰從 hello API 存取 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="30b58-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="30b58-153">呼叫 hello 指令碼，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="30b58-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="30b58-154">它是簡單 toomodify hello 指令碼，例如 hello 過去 toocreate 註解。</span><span class="sxs-lookup"><span data-stu-id="30b58-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30b58-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30b58-155">Next steps</span></span>

* [<span data-ttu-id="30b58-156">建立工作項目</span><span class="sxs-lookup"><span data-stu-id="30b58-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="30b58-157">使用 PowerShell 進行自動化</span><span class="sxs-lookup"><span data-stu-id="30b58-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
