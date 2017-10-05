---
title: "整合 Azure 雲端服務與 Azure CDN | Microsoft Docs"
description: "了解如何部署可提供整合式 Azure CDN 端點內容的雲端服務"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="55d0f-103"><a name="intro"></a> 整合雲端服務與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="55d0f-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="55d0f-104">雲端服務可以與 Azure CDN 整合，從雲端服務的位置提供任何內容。</span><span class="sxs-lookup"><span data-stu-id="55d0f-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="55d0f-105">此方法提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="55d0f-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="55d0f-106">輕鬆地在雲端服務的專案目錄中部署和更新影像、指令碼和樣式表</span><span class="sxs-lookup"><span data-stu-id="55d0f-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="55d0f-107">輕鬆地升級雲端服務中的 NuGet 套件，例如 jQuery 或 Bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="55d0f-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="55d0f-108">完全從相同的 Visual Studio 介面來管理 Web 應用程式和 CDN 提供的內容</span><span class="sxs-lookup"><span data-stu-id="55d0f-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="55d0f-109">Web 應用程式和 CDN 提供的內容採用統一的部署工作流程</span><span class="sxs-lookup"><span data-stu-id="55d0f-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="55d0f-110">整合 ASP.NET 統合和縮製與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="55d0f-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55d0f-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="55d0f-111">What you will learn</span></span>
<span data-ttu-id="55d0f-112">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="55d0f-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="55d0f-113">整合 Azure CDN 端點與雲端服務，並從 Azure CDN 提供網頁的靜態內容</span><span class="sxs-lookup"><span data-stu-id="55d0f-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="55d0f-114">在雲端服務中為靜態內容設定快取設定</span><span class="sxs-lookup"><span data-stu-id="55d0f-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="55d0f-115">透過 Azure CDN 使用控制器動作提供內容</span><span class="sxs-lookup"><span data-stu-id="55d0f-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="55d0f-116">透過 Azure CDN 提供統合和縮製的內容，同時保持良好的 Visual Studio 指令碼偵錯體驗</span><span class="sxs-lookup"><span data-stu-id="55d0f-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="55d0f-117">設定 Azure CDN 離線時的後援指令碼和 CSS</span><span class="sxs-lookup"><span data-stu-id="55d0f-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="55d0f-118">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="55d0f-118">What you will build</span></span>
<span data-ttu-id="55d0f-119">您將使用預設 ASP.NET MVC 範本來部署雲端服務 Web 角色、加入程式碼從整合式 Azure CDN 提供內容，例如影像、控制器動作結果及預設 JavaScript 和 CSS 檔案，也會撰寫程式碼來為 CDN 離線時提供的套件組合設定後援機制。</span><span class="sxs-lookup"><span data-stu-id="55d0f-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="55d0f-120">必要元件</span><span class="sxs-lookup"><span data-stu-id="55d0f-120">What you will need</span></span>
<span data-ttu-id="55d0f-121">本教學課程有下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="55d0f-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="55d0f-122">使用中的 [Microsoft Azure 帳戶](/account/)</span><span class="sxs-lookup"><span data-stu-id="55d0f-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="55d0f-123">Visual Studio 2015 (含 [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="55d0f-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="55d0f-124">要完成此教學課程，您必須要有 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="55d0f-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="55d0f-125">您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/) - 您將取得可試用付費 Azure 服務的額度，且即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務，例如「網站」。</span><span class="sxs-lookup"><span data-stu-id="55d0f-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="55d0f-126">您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - 您的 MSDN 訂閱每月會提供您額度，您可以用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="55d0f-127">部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="55d0f-127">Deploy a cloud service</span></span>
<span data-ttu-id="55d0f-128">在本節中，您將在 Visual Studio 2015 中將預設 ASP.NET MVC 應用程式範本部署至雲端服務 Web 角色，然後將其與新的 CDN 端點整合。</span><span class="sxs-lookup"><span data-stu-id="55d0f-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="55d0f-129">請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="55d0f-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="55d0f-130">在 Visual Studio 2015 中，從功能表列前往 [檔案] > [新增] > [專案] > [雲端] > [Azure 雲端服務]，建立新的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="55d0f-131">命名並按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="55d0f-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="55d0f-132">選取 [ASP.NET Web 角色]，然後按一下 **>** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55d0f-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="55d0f-133">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="55d0f-134">選取 [MVC]，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="55d0f-135">現在，將此 Web 角色發行至 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="55d0f-136">以滑鼠右鍵按一下雲端服務專案，選取 [ **發行**]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="55d0f-137">若您尚未登入 Microsoft Azure，按一下 [新增帳戶...] 下拉式清單，然後按一下 [新增帳戶] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="55d0f-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="55d0f-138">在登入頁面中，使用您用來啟用 Azure 帳戶的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="55d0f-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="55d0f-139">登入後，按一下 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="55d0f-140">如果您未建立雲端服務或儲存體帳戶，Visual Studio 會協助您建立兩者。</span><span class="sxs-lookup"><span data-stu-id="55d0f-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="55d0f-141">在 [ **建立雲端服務與帳戶** ] 對話方塊中，輸入想要的服務名稱，並選取需要的區域。</span><span class="sxs-lookup"><span data-stu-id="55d0f-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="55d0f-142">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="55d0f-143">在發行設定頁面中，驗證設定並按一下 [ **發行**]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="55d0f-144">雲端服務的發行程序會花費很長時間。</span><span class="sxs-lookup"><span data-stu-id="55d0f-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="55d0f-145">[啟用所有 Web 角色的 Web Deploy] 選項可快速 (但暫時) 提供更新給 Web 角色，加速偵測您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="55d0f-146">如需此選項的詳細資訊，請參閱 [使用 Azure Tools 發行雲端服務](http://msdn.microsoft.com/library/ff683672.aspx)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="55d0f-147">當 [Microsoft Azure 活動記錄檔] 的發佈狀態為 [已完成] 時，您就能建立與此雲端服務整合的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="55d0f-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="55d0f-148">若在發佈後部署的雲端服務顯示錯誤畫面，原因可能在於您已部署的雲端服務使用 [不含 .NET 4.5.2 的客體 OS](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="55d0f-149">您可 [將 .NET 4.5.2 部署為啟動工作](../cloud-services/cloud-services-dotnet-install-dotnet.md)，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="55d0f-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="55d0f-150">建立新的 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="55d0f-150">Create a new CDN profile</span></span>
<span data-ttu-id="55d0f-151">CDN 設定檔就是 CDN 端點的集合。</span><span class="sxs-lookup"><span data-stu-id="55d0f-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="55d0f-152">每個設定檔皆包含一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="55d0f-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="55d0f-153">您可能會想要使用多個設定檔，依網際網路網域、Web 應用程式或其他準則來組織您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="55d0f-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="55d0f-154">若您已有您想要用於本教學課程的 CDN 設定檔，請繼續參閱「 [建立新的 CDN 端點](#create-a-new-cdn-endpoint)」。</span><span class="sxs-lookup"><span data-stu-id="55d0f-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="55d0f-155">建立新的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="55d0f-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="55d0f-156">**為儲存體帳戶建立新的 CDN 端點**</span><span class="sxs-lookup"><span data-stu-id="55d0f-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="55d0f-157">在 [Azure 管理入口網站](https://portal.azure.com)中，巡覽至您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="55d0f-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="55d0f-158">您可能已在先前步驟中將其釘選至儀表板。</span><span class="sxs-lookup"><span data-stu-id="55d0f-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="55d0f-159">若否，則您可依序按一下 [瀏覽]、[CDN 設定檔] 尋找該設定檔，然後再按一下您要在其中新增端點的設定檔。</span><span class="sxs-lookup"><span data-stu-id="55d0f-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="55d0f-160">此時會顯示 [CDN 設定檔] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55d0f-160">The CDN profile blade appears.</span></span>
   
    ![CDN 設定檔][cdn-profile-settings]
2. <span data-ttu-id="55d0f-162">按一下 [新增端點]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="55d0f-162">Click the **Add Endpoint** button.</span></span>
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    <span data-ttu-id="55d0f-164">此時會顯示 [加入端點]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="55d0f-164">The **Add an endpoint** blade appears.</span></span>
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. <span data-ttu-id="55d0f-166">輸入這個 CDN 端點的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="55d0f-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="55d0f-167">此名稱會用於存取位於網域 `<EndpointName>.azureedge.net`的快取資源。</span><span class="sxs-lookup"><span data-stu-id="55d0f-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="55d0f-168">在 [ **原始類型** ] 下拉式清單中，選取 [ *雲端服務*]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="55d0f-169">在 [ **原始主機名稱** ] 下拉式清單中，選取您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="55d0f-170">針對以下項目保留預設值：[原始路徑]、[原始主機標頭] 和 [通訊協定/原始連接埠]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="55d0f-171">您至少必須指定一個通訊協定 (HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="55d0f-172">按一下 [ **新增** ] 按鈕，以建立新的端點。</span><span class="sxs-lookup"><span data-stu-id="55d0f-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="55d0f-173">端點建立完畢之後，即會出現在設定檔的端點清單中。</span><span class="sxs-lookup"><span data-stu-id="55d0f-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="55d0f-174">此清單檢視會顯示用來存取所快取內容的 URL 以及原始網域。</span><span class="sxs-lookup"><span data-stu-id="55d0f-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN 端點][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="55d0f-176">端點將無法立即可用。</span><span class="sxs-lookup"><span data-stu-id="55d0f-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="55d0f-177">註冊可能需要 90 分鐘的處理時間，以透過 CDN 網路傳播。</span><span class="sxs-lookup"><span data-stu-id="55d0f-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="55d0f-178">若使用者嘗試立即使用 CDN 網域名稱，則可能會顯示狀態碼 404，直到可透過 CDN 使用內容為止。</span><span class="sxs-lookup"><span data-stu-id="55d0f-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="55d0f-179">測試 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="55d0f-179">Test the CDN endpoint</span></span>
<span data-ttu-id="55d0f-180">若發佈狀態為 [已完成]，請開啟瀏覽器視窗並瀏覽至 **http://<cdnName>*.azureedge.net/Content/bootstrap.css**。</span><span class="sxs-lookup"><span data-stu-id="55d0f-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="55d0f-181">在我的設定中，此 URL 為：</span><span class="sxs-lookup"><span data-stu-id="55d0f-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="55d0f-182">對應至 CDN 端點上的下列原始 URL：</span><span class="sxs-lookup"><span data-stu-id="55d0f-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="55d0f-183">瀏覽至 **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css** 時，根據您的瀏覽器而定，系統會提示您下載或開啟來自已發佈 Web 應用程式的 bootstrap.css。</span><span class="sxs-lookup"><span data-stu-id="55d0f-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="55d0f-184">同樣地，您可以從 CDN 端點，以 http://&lt;serviceName>.cloudapp.net/ 存取任何可公開存取的 URL。</span><span class="sxs-lookup"><span data-stu-id="55d0f-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="55d0f-185">例如：</span><span class="sxs-lookup"><span data-stu-id="55d0f-185">For example:</span></span>

* <span data-ttu-id="55d0f-186">/Script 路徑中的 .js 檔案</span><span class="sxs-lookup"><span data-stu-id="55d0f-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="55d0f-187">/Content 路徑中的任何內容檔案</span><span class="sxs-lookup"><span data-stu-id="55d0f-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="55d0f-188">任何控制器/動作</span><span class="sxs-lookup"><span data-stu-id="55d0f-188">Any controller/action</span></span>
* <span data-ttu-id="55d0f-189">任何含有查詢字串的 URL (若 CDN 端點已啟用查詢字串的話)</span><span class="sxs-lookup"><span data-stu-id="55d0f-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="55d0f-190">實際上，以上述設定來說，您可以從 **http://*&lt;cdnName>*.azureedge.net/** 代管整個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="55d0f-191">如果我瀏覽至 **http://camservice.azureedge.net/**，就可以從 Home/Index 取得動作結果。</span><span class="sxs-lookup"><span data-stu-id="55d0f-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="55d0f-192">然而，這不表示透過 Azure CDN 來提供整個雲端服務一定是好辦法。</span><span class="sxs-lookup"><span data-stu-id="55d0f-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="55d0f-193">因為 CDN 必須經常地從原始伺服器提取資產的新版本，所以已將靜態傳遞最佳化的 CDN 不一定能加速傳遞原本就沒有要快取或是會頻繁更新的動態資產。</span><span class="sxs-lookup"><span data-stu-id="55d0f-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="55d0f-194">若情況如此，您可以在 CDN 端點上啟用[動態網站加速](cdn-dynamic-site-acceleration.md)最佳化 (DSA)，以使用各種技術來加速傳遞無法快取的動態資產。</span><span class="sxs-lookup"><span data-stu-id="55d0f-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="55d0f-195">如果您的網站混合使用靜態及動態內容，您可以選擇從具有靜態最佳化類型的 CDN 提供靜態內容 (例如一般 Web 傳遞)，也可以選擇直接從原始伺服器或依個別情況透過已開啟 DSA 最佳化的 CDN 端點來提供動態內容。</span><span class="sxs-lookup"><span data-stu-id="55d0f-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="55d0f-196">總之，您已了解如何從 CDN 端點存取個別的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="55d0f-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="55d0f-197">我將在透過 Azure CDN 從控制器動作提供內容中說明如何透過特定 CDN 端點提供特定的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="55d0f-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="55d0f-198">替代方法是在雲端服務中依個別情況決定從 Azure CDN 提供什麼內容。</span><span class="sxs-lookup"><span data-stu-id="55d0f-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="55d0f-199">總之，您已了解如何從 CDN 端點存取個別的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="55d0f-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="55d0f-200">我將在 [透過 Azure CDN 從控制器動作提供內容](#controller)中說明如何透過 CDN 端點提供特定的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="55d0f-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="55d0f-201">在雲端服務中設定靜態檔案的快取選項</span><span class="sxs-lookup"><span data-stu-id="55d0f-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="55d0f-202">利用雲端服務中的 Azure CDN 整合，您可以指定如何在 CDN 端點中快取靜態內容。</span><span class="sxs-lookup"><span data-stu-id="55d0f-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="55d0f-203">若要執行此動作，從 Web 角色專案 (例如 WebRole1) 開啟 *Web.config*，然後將 `<staticContent>` 元素加入至 `<system.webServer>`。</span><span class="sxs-lookup"><span data-stu-id="55d0f-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="55d0f-204">以下的 XML 將快取設為 3 天過期。</span><span class="sxs-lookup"><span data-stu-id="55d0f-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="55d0f-205">這樣做時，雲端服務中的所有靜態檔案會在您的 CDN 快取中遵守相同規則。</span><span class="sxs-lookup"><span data-stu-id="55d0f-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="55d0f-206">若要更精確控制快取設定，請將 *Web.config* 檔案加入至資料夾，並在檔案中新增您的設定。</span><span class="sxs-lookup"><span data-stu-id="55d0f-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="55d0f-207">例如，將 Web.config 檔案新增至 \Content 資料夾，並將內容改成下列 XML：</span><span class="sxs-lookup"><span data-stu-id="55d0f-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="55d0f-208">此設定會將 \Content 資料夾中的所有靜態檔案快取 15 天。</span><span class="sxs-lookup"><span data-stu-id="55d0f-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="55d0f-209">如需有關如何設定 `<clientCache>` 元素的詳細資訊，請參閱[用戶端快取 &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="55d0f-210">在 [透過 Azure CDN 從控制器動作提供內容](#controller)中，我也會說明如何在 CDN 快取中設定控制器動作結果的快取設定。</span><span class="sxs-lookup"><span data-stu-id="55d0f-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="55d0f-211">透過 Azure CDN 使用控制器動作提供內容</span><span class="sxs-lookup"><span data-stu-id="55d0f-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="55d0f-212">整合雲端服務 Web 角色與 Azure CDN 時，透過 Azure CDN 從控制器動作提供內容就非常簡單。</span><span class="sxs-lookup"><span data-stu-id="55d0f-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="55d0f-213">除了透過 Azure CDN 直接提供雲端服務 (如上面示範) 以外，在[使用 Azure CDN 縮短網路延遲時間](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN) (英文) 中，[Maarten Balliauw](https://twitter.com/maartenballiauw) 示範如何透過有趣的 MemeGenerator 控制器提供雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="55d0f-214">我在這裡簡單地重述一次。</span><span class="sxs-lookup"><span data-stu-id="55d0f-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="55d0f-215">假設您想在雲端服務中利用查克羅禮士年輕時的一張相片 ( [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)拍攝) 來引起網路瘋傳：</span><span class="sxs-lookup"><span data-stu-id="55d0f-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="55d0f-216">您有一個簡單的 `Index` 動作可讓客戶在照片上指定笑梗，再傳給此動作來引起網路瘋傳。</span><span class="sxs-lookup"><span data-stu-id="55d0f-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="55d0f-217">因為是查克羅禮士，您預期此頁面一定會在全球造成一股旋風。</span><span class="sxs-lookup"><span data-stu-id="55d0f-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="55d0f-218">這就是利用 Azure CDN 來提供半動態內容的一個最佳例子。</span><span class="sxs-lookup"><span data-stu-id="55d0f-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="55d0f-219">請依照上述步驟來設定此控制器動作：</span><span class="sxs-lookup"><span data-stu-id="55d0f-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="55d0f-220">在 \Controllers 資料夾中，建立一個新的 .cs 檔案稱為 MemeGeneratorController.cs，並將內容改成下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="55d0f-221">請務必以您的 CDN 名稱取代醒目提示的部分。</span><span class="sxs-lookup"><span data-stu-id="55d0f-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="55d0f-222">以滑鼠右鍵按一下預設的 `Index()` 動作，選取 [ **加入檢視**]。</span><span class="sxs-lookup"><span data-stu-id="55d0f-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="55d0f-223">接受下列設定，按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="55d0f-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="55d0f-224">開啟新的 Views\MemeGenerator\Index.cshtml，將內容改成下列簡單的 HTML 來提交笑梗：</span><span class="sxs-lookup"><span data-stu-id="55d0f-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="55d0f-225">重新發佈雲端服務，然後在瀏覽器中瀏覽至 **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index**。</span><span class="sxs-lookup"><span data-stu-id="55d0f-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="55d0f-226">當您將表單值提交至 `/MemeGenerator/Index` 時，`Index_Post` 動作方法會傳回 `Show` 動作方法的連結及個別的輸入識別碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="55d0f-227">按一下連結會執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="55d0f-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="55d0f-228">如果已附加本機偵錯程式，您將經由本機重新導向而享有一般的偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="55d0f-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="55d0f-229">如果是在雲端服務中執行，則會重新導向至：</span><span class="sxs-lookup"><span data-stu-id="55d0f-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="55d0f-230">對應至 CDN 端點上的下列原始 URL：</span><span class="sxs-lookup"><span data-stu-id="55d0f-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="55d0f-231">然後，您可以在 `Generate` 方法上使用 `OutputCacheAttribute` 屬性，以指定如何快取 Azure CDN 將接受的動作結果。</span><span class="sxs-lookup"><span data-stu-id="55d0f-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="55d0f-232">以下程式碼指定快取到期時間 1 小時 (3,600 秒)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="55d0f-233">同樣地，您可以在雲端服務中透過 Azure CDN，並指定想要的快取選項，從任何控制器動作提供內容。</span><span class="sxs-lookup"><span data-stu-id="55d0f-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="55d0f-234">在下一節，我將說明如何透過 Azure CDN 提供統合和縮製的指令碼與 CSS。</span><span class="sxs-lookup"><span data-stu-id="55d0f-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="55d0f-235">整合 ASP.NET 統合和縮製與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="55d0f-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="55d0f-236">指令碼和 CSS 樣式表不常變更，是 Azure CDN 快取的最佳候選項。</span><span class="sxs-lookup"><span data-stu-id="55d0f-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="55d0f-237">透過 Azure CDN 提供整個 Web 角色是整合統合和縮製與 Azure CDN 最輕鬆的方法。</span><span class="sxs-lookup"><span data-stu-id="55d0f-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="55d0f-238">然而，您可能不想這樣做，我將說明如何這樣做，但同時保留開發人員希望的 ASP.NET 統合和縮製體驗，例如：</span><span class="sxs-lookup"><span data-stu-id="55d0f-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="55d0f-239">絕佳的偵錯模式體驗</span><span class="sxs-lookup"><span data-stu-id="55d0f-239">Great debug mode experience</span></span>
* <span data-ttu-id="55d0f-240">流暢的部署</span><span class="sxs-lookup"><span data-stu-id="55d0f-240">Streamlined deployment</span></span>
* <span data-ttu-id="55d0f-241">隨著指令碼/CSS 版本升級立即更新用戶端</span><span class="sxs-lookup"><span data-stu-id="55d0f-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="55d0f-242">CDN 端點失敗時的後援機制</span><span class="sxs-lookup"><span data-stu-id="55d0f-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="55d0f-243">儘可能不修改程式碼</span><span class="sxs-lookup"><span data-stu-id="55d0f-243">Minimize code modification</span></span>

<span data-ttu-id="55d0f-244">在您於[整合 Azure CDN 端點與 Azure 網站，並從 Azure CDN 提供網頁靜態內容](#deploy)所建立的 **WebRole1** 專案中，開啟 *App_Start\BundleConfig.cs*，然後查看 `bundles.Add()` 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="55d0f-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="55d0f-245">第一個 `bundles.Add()` 陳述式將指令碼套件組合加入至虛擬目錄 `~/bundles/jquery`。</span><span class="sxs-lookup"><span data-stu-id="55d0f-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="55d0f-246">然後，開啟 Views\Shared\_Layout.cshtml，查看指令碼套件組合標籤如何轉譯。</span><span class="sxs-lookup"><span data-stu-id="55d0f-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="55d0f-247">您應該可以找到下列這一行 Razor 程式碼：</span><span class="sxs-lookup"><span data-stu-id="55d0f-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="55d0f-248">當此 Razor 程式碼在 Azure Web 角色中執行時，它會類似如下轉譯指令碼套件組合的 `<script>` 標籤：</span><span class="sxs-lookup"><span data-stu-id="55d0f-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="55d0f-249">不過，當在 Visual Studio 中按 `F5`執行時，則會個別轉譯套件組合中的每一個指令碼檔案 (在上述案例中，套件組合中只有一個指令碼檔案)：</span><span class="sxs-lookup"><span data-stu-id="55d0f-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="55d0f-250">這樣可讓您在開發環境中進行 JavaScript 程式碼偵錯，同時減少並行的用戶端連線 (統合)，在實際執行環境中提升檔案下載效能 (縮製)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="55d0f-251">這是 Azure CDN 整合中保留的絕佳功能。</span><span class="sxs-lookup"><span data-stu-id="55d0f-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="55d0f-252">此外，由於轉譯的套件組合已包含自動產生的版本字串，您可以仿照此功能，每當您透過 NuGet 更新 jQuery 版本時，就會以最快速度更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="55d0f-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="55d0f-253">請遵循下列步驟來整合 ASP.NET 統合和縮製與 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="55d0f-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="55d0f-254">回到 App_Start\BundleConfig.cs，修改 `bundles.Add()` 方法來使用不同的 [Bundle 建構函式](http://msdn.microsoft.com/library/jj646464.aspx) (此函式會指定 CDN 位址)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="55d0f-255">若要這樣做，請將 `RegisterBundles` 方法定義改成下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="55d0f-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="55d0f-256">請記得將 `<yourCDNName>` 取代為您的 Azure CDN 名稱。</span><span class="sxs-lookup"><span data-stu-id="55d0f-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="55d0f-257">簡單地說，您正在設定 `bundles.UseCdn = true` ，且已在每一個套件組合中加入謹慎建構的 CDN URL。</span><span class="sxs-lookup"><span data-stu-id="55d0f-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="55d0f-258">例如，程式碼的第一個建構函式：</span><span class="sxs-lookup"><span data-stu-id="55d0f-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="55d0f-259">就如同：</span><span class="sxs-lookup"><span data-stu-id="55d0f-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="55d0f-260">此建構函式告知 ASP.NET 統合和縮製在本機偵錯時轉譯個別指令碼檔案，但使用指定的 CDN 位址來存取所提及的指令碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="55d0f-261">不過，對於此謹慎建構的 CDN URL，請注意兩項重要特性：</span><span class="sxs-lookup"><span data-stu-id="55d0f-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="55d0f-262">此 CDN URL 的來源是 `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`，事實上就是雲端服務中指令碼套件組合的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="55d0f-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="55d0f-263">由於是使用 CDN 建構函式，套件組合的 CDN 指令碼標籤在轉譯的 URL 中已不再包含自動產生的版本字串。</span><span class="sxs-lookup"><span data-stu-id="55d0f-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="55d0f-264">指令碼套件組合每次修改時，您都必須手動產生唯一的版本字串，以強制在 Azure CDN 上發生快取遺漏。</span><span class="sxs-lookup"><span data-stu-id="55d0f-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="55d0f-265">同時，在部署套件組合之後，此唯一的版本字串在部署的整個存在期間內必須保持不變，讓 Azure CDN 的快取命中率達到最高。</span><span class="sxs-lookup"><span data-stu-id="55d0f-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="55d0f-266">查詢字串 v=<W.X.Y.Z> 會從 Web 角色專案的 Properties\AssemblyInfo.cs 中提取。</span><span class="sxs-lookup"><span data-stu-id="55d0f-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="55d0f-267">您的部署工作流程中可以包含每次發佈至 Azure 時就遞增組件版本。</span><span class="sxs-lookup"><span data-stu-id="55d0f-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="55d0f-268">或者，您可以直接修改專案中的 Properties\AssemblyInfo.cs，使用萬用字元 '*' 表示每次建置時就自動遞增版本字串。</span><span class="sxs-lookup"><span data-stu-id="55d0f-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="55d0f-269">例如：</span><span class="sxs-lookup"><span data-stu-id="55d0f-269">For example:</span></span>
     
        <span data-ttu-id="55d0f-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="55d0f-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="55d0f-271">在此可採取其他任何策略在部署的存在期間內產生唯一字串。</span><span class="sxs-lookup"><span data-stu-id="55d0f-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="55d0f-272">重新發行雲端服務和存取首頁。</span><span class="sxs-lookup"><span data-stu-id="55d0f-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="55d0f-273">檢視頁面的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-273">View the HTML code for the page.</span></span> <span data-ttu-id="55d0f-274">您應該會看到轉譯的 CDN URL，以及每次將變更重新發行至雲端服務時的唯一版本字串。</span><span class="sxs-lookup"><span data-stu-id="55d0f-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="55d0f-275">例如：</span><span class="sxs-lookup"><span data-stu-id="55d0f-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="55d0f-276">在 Visual Studio 中，按下 `F5`在 Visual Studio 中偵錯雲端服務。</span><span class="sxs-lookup"><span data-stu-id="55d0f-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="55d0f-277">檢視頁面的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-277">View the HTML code for the page.</span></span> <span data-ttu-id="55d0f-278">您仍然會看到每一個指令檔以個別方式轉譯，讓您在 Visual Studio 中享有一致的偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="55d0f-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="55d0f-279">CDN URL 的後援機制</span><span class="sxs-lookup"><span data-stu-id="55d0f-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="55d0f-280">當 Azure CDN 端點因故失敗時，您一定希望網頁能夠聰明地存取原始 Web 伺服器，當作後援選項來載入 JavaScript 或 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="55d0f-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="55d0f-281">因 CDN 無法使用而遺失網站的影像就已經夠嚴重，而遺失由指令碼和樣式表所提供的重要頁面功能又更加嚴重。</span><span class="sxs-lookup"><span data-stu-id="55d0f-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="55d0f-282">[Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) 類別包含一個稱為 [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) 的屬性，可讓您設定 CDN 失敗時的後援機制。</span><span class="sxs-lookup"><span data-stu-id="55d0f-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="55d0f-283">若要使用此屬性，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="55d0f-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="55d0f-284">在 Web 角色專案中，開啟 App_Start\BundleConfig.cs (您已在該檔案中，將 CDN URL 加入每個 [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx))，透過下列醒目提示的變更將後援機制加入預設套件組合：</span><span class="sxs-lookup"><span data-stu-id="55d0f-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="55d0f-285">當 `CdnFallbackExpression` 不是 null 時，指令碼會插入 HTML 中來測試是否已成功載入套件組合，如果不是，則直接從原始 Web 伺服器存取套件組合。</span><span class="sxs-lookup"><span data-stu-id="55d0f-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="55d0f-286">此屬性必須設為 JavaScript 運算式來測試個別的 CDN 套件組合是否正確載入。</span><span class="sxs-lookup"><span data-stu-id="55d0f-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="55d0f-287">測試每一個套件組合所需的運算式根據內容而不同。</span><span class="sxs-lookup"><span data-stu-id="55d0f-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="55d0f-288">在以上的預設套件組合中：</span><span class="sxs-lookup"><span data-stu-id="55d0f-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="55d0f-289">`window.jquery` 定義於 jquery-{version}.js 中</span><span class="sxs-lookup"><span data-stu-id="55d0f-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="55d0f-290">`$.validator` 定義於 jquery.validate.js 中</span><span class="sxs-lookup"><span data-stu-id="55d0f-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="55d0f-291">`window.Modernizr` 定義於 modernizer-{version}.js 中</span><span class="sxs-lookup"><span data-stu-id="55d0f-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="55d0f-292">`$.fn.modal` 定義於 bootstrap.js 中</span><span class="sxs-lookup"><span data-stu-id="55d0f-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="55d0f-293">您可能發現到我沒有為 `~/Cointent/css` 套件組合設定 CdnFallbackExpression。</span><span class="sxs-lookup"><span data-stu-id="55d0f-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="55d0f-294">這是因為目前 [System.Web.Optimization 中有錯誤](https://aspnetoptimization.codeplex.com/workitem/104)，導致插入後援 CSS 的 `<script>` 標籤，而非預期的 `<link>` 標籤。</span><span class="sxs-lookup"><span data-stu-id="55d0f-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="55d0f-295">不過，[Ember 顧問團](https://github.com/EmberConsultingGroup) (英文) 提供一套良好的[樣式套件組合後援](https://github.com/EmberConsultingGroup/StyleBundleFallback) (英文)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="55d0f-296">若要使用 CSS 的因應措施，請在 Web 角色專案的 App_Start 資料夾中建立新的 .cs 檔案，命名為 StyleBundleExtensions.cs，並將其內容改成 [GitHub 的程式碼](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="55d0f-297">在 App_Start\StyleFundleExtensions.cs 中，將命名空間重新命名為您的 Web 角色名稱 (例如 **WebRole1**)。</span><span class="sxs-lookup"><span data-stu-id="55d0f-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="55d0f-298">回到 `App_Start\BundleConfig.cs`，將最後一個 `bundles.Add` 陳述式修改為下列醒目提示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="55d0f-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="55d0f-299">這個新的延伸方法採用相同的概念，將指令碼插入 HTML 中來檢查 DOM，尋找 CSS 套件組合中定義的相符類別名稱、規則名稱和規則值，而如果找不到相符項，則退一步存取原始 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="55d0f-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="55d0f-300">重新發行雲端服務和存取首頁。</span><span class="sxs-lookup"><span data-stu-id="55d0f-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="55d0f-301">檢視頁面的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="55d0f-301">View the HTML code for the page.</span></span> <span data-ttu-id="55d0f-302">您應該會發現類似下方的插入指令碼：</span><span class="sxs-lookup"><span data-stu-id="55d0f-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="55d0f-303">請注意，針對 CSS 套件組合插入的指令碼，仍在這一行中包含 `CdnFallbackExpression` 屬性殘留的遊蕩部分：</span><span class="sxs-lookup"><span data-stu-id="55d0f-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="55d0f-304">但因為 || 運算式的開頭部分一定會傳回 true (緊鄰的上一行)，所以 document.write() 函數永遠不會執行。</span><span class="sxs-lookup"><span data-stu-id="55d0f-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="55d0f-305">相關資訊</span><span class="sxs-lookup"><span data-stu-id="55d0f-305">More Information</span></span>
* [<span data-ttu-id="55d0f-306">Azure 內容傳遞網路 (CDN) 概觀</span><span class="sxs-lookup"><span data-stu-id="55d0f-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="55d0f-307">使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="55d0f-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="55d0f-308">ASP.NET 統合和縮製</span><span class="sxs-lookup"><span data-stu-id="55d0f-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
