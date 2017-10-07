---
title: "Azure 雲端服務與 Azure CDN aaaIntegrate |Microsoft 文件"
description: "了解如何 toodeploy 雲端服務提供整合的 Azure CDN 端點的內容"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="36f84-103"><a name="intro"></a> 整合雲端服務與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="36f84-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="36f84-104">雲端服務可以整合 Azure cdn，提供任何內容來自 hello 雲端服務的位置。</span><span class="sxs-lookup"><span data-stu-id="36f84-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="36f84-105">這個方法提供下列您 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="36f84-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="36f84-106">輕鬆地在雲端服務的專案目錄中部署和更新影像、指令碼和樣式表</span><span class="sxs-lookup"><span data-stu-id="36f84-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="36f84-107">輕鬆升級您的雲端服務，例如 jQuery 或啟動程序的版本中的 hello NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="36f84-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="36f84-108">管理您的 Web 應用程式和您 CDN 服務內容所有從 hello 相同 Visual Studio 介面</span><span class="sxs-lookup"><span data-stu-id="36f84-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="36f84-109">Web 應用程式和 CDN 提供的內容採用統一的部署工作流程</span><span class="sxs-lookup"><span data-stu-id="36f84-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="36f84-110">整合 ASP.NET 統合和縮製與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="36f84-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36f84-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="36f84-111">What you will learn</span></span>
<span data-ttu-id="36f84-112">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="36f84-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="36f84-113">整合 Azure CDN 端點與雲端服務，並從 Azure CDN 提供網頁的靜態內容</span><span class="sxs-lookup"><span data-stu-id="36f84-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="36f84-114">在雲端服務中為靜態內容設定快取設定</span><span class="sxs-lookup"><span data-stu-id="36f84-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="36f84-115">透過 Azure CDN 使用控制器動作提供內容</span><span class="sxs-lookup"><span data-stu-id="36f84-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="36f84-116">Serve 結合在一起，並縮短透過 Azure CDN 的內容，同時保留 hello 指令碼偵錯 Visual Studio 體驗</span><span class="sxs-lookup"><span data-stu-id="36f84-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="36f84-117">設定 Azure CDN 離線時的後援指令碼和 CSS</span><span class="sxs-lookup"><span data-stu-id="36f84-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="36f84-118">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="36f84-118">What you will build</span></span>
<span data-ttu-id="36f84-119">您將部署雲端服務 Web 角色將 hello 預設的 ASP.NET MVC 範本、 從整合式的 Azure CDN，例如影像、 控制器動作的結果及 hello 預設 JavaScript 和 CSS 檔案，加入程式碼 tooserve 內容和也可以撰寫程式碼 tooconfigure hello組合服務 hello 事件中的 hello CDN 的遞補機制已離線。</span><span class="sxs-lookup"><span data-stu-id="36f84-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="36f84-120">必要元件</span><span class="sxs-lookup"><span data-stu-id="36f84-120">What you will need</span></span>
<span data-ttu-id="36f84-121">本教學課程有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="36f84-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="36f84-122">使用中的 [Microsoft Azure 帳戶](/account/)</span><span class="sxs-lookup"><span data-stu-id="36f84-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="36f84-123">Visual Studio 2015 (含 [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="36f84-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="36f84-124">您需要 Azure 帳戶 toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="36f84-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="36f84-125">您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且即使他們用於之後您可以在最多保留 hello 帳戶，並使用免費的 Azure 服務，例如網站。</span><span class="sxs-lookup"><span data-stu-id="36f84-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="36f84-126">您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - 您的 MSDN 訂閱每月會提供您額度，您可以用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="36f84-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="36f84-127">部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="36f84-127">Deploy a cloud service</span></span>
<span data-ttu-id="36f84-128">在本節中，您會部署 hello 預設 Visual Studio 2015 tooa 雲端服務 Web 角色，在 ASP.NET MVC 應用程式範本，然後將它整合到新的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="36f84-129">請遵循下列的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="36f84-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="36f84-130">在 Visual Studio 2015 中，建立新的 Azure 雲端服務從功能表列中 hello 太移**檔案 > 新增 > 專案 > 雲端 > Azure 雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="36f84-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="36f84-131">命名並按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="36f84-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="36f84-132">選取**ASP.NET Web 角色**按一下 hello  **>**   按鈕。</span><span class="sxs-lookup"><span data-stu-id="36f84-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="36f84-133">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="36f84-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="36f84-134">選取 [MVC]，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="36f84-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="36f84-135">現在，將發佈此 Web 角色 tooan Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="36f84-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="36f84-136">Hello 雲端服務專案上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="36f84-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="36f84-137">如果您不尚未登入 Microsoft Azure，請按一下 hello**新增帳戶...**下拉式清單中，然後按一下 hello**將帳戶加入**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="36f84-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="36f84-138">在 hello 登入頁面中，使用登入 hello tooactivate 您使用您的 Azure 帳戶的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="36f84-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="36f84-139">登入後，按一下 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="36f84-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="36f84-140">如果您未建立雲端服務或儲存體帳戶，Visual Studio 會協助您建立兩者。</span><span class="sxs-lookup"><span data-stu-id="36f84-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="36f84-141">在 hello**建立雲端服務和帳戶**對話方塊、 型別 hello 所需的服務名稱和選取 hello 所需的區域。</span><span class="sxs-lookup"><span data-stu-id="36f84-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="36f84-142">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="36f84-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="36f84-143">在 hello 發佈設定 頁面上，確認 hello 組態，按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="36f84-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="36f84-144">雲端服務的 hello 發行程序需要較長時間。</span><span class="sxs-lookup"><span data-stu-id="36f84-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="36f84-145">hello 啟用 Web Deploy 的所有角色 選項可以進行偵錯雲端服務更快，藉由提供快速 （但暫存） 更新 tooyour Web 角色。</span><span class="sxs-lookup"><span data-stu-id="36f84-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="36f84-146">如需有關這個選項的詳細資訊，請參閱[發行雲端服務使用 hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx)。</span><span class="sxs-lookup"><span data-stu-id="36f84-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="36f84-147">當 hello **Microsoft Azure 活動記錄檔**顯示發行狀態為**已完成**，您將建立 CDN 端點與此雲端服務整合。</span><span class="sxs-lookup"><span data-stu-id="36f84-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="36f84-148">如果之後發佈，部署的 hello 雲端服務會顯示錯誤畫面，它可能是因為您已部署的 hello 雲端服務正在使用[客體 OS 不包含.NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates)。</span><span class="sxs-lookup"><span data-stu-id="36f84-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="36f84-149">您可 [將 .NET 4.5.2 部署為啟動工作](../cloud-services/cloud-services-dotnet-install-dotnet.md)，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="36f84-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="36f84-150">建立新的 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="36f84-150">Create a new CDN profile</span></span>
<span data-ttu-id="36f84-151">CDN 設定檔就是 CDN 端點的集合。</span><span class="sxs-lookup"><span data-stu-id="36f84-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="36f84-152">每個設定檔皆包含一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="36f84-153">您可能希望 toouse 多個設定檔 tooorganize 您的 CDN 端點的網際網路網域、 web 應用程式，或其他一些準則。</span><span class="sxs-lookup"><span data-stu-id="36f84-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="36f84-154">如果您已經有您想 toouse，本教學課程中的 CDN 設定檔時，繼續太[建立新的 CDN 端點](#create-a-new-cdn-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="36f84-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="36f84-155">建立新的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="36f84-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="36f84-156">**toocreate 新儲存體帳戶的 CDN 端點**</span><span class="sxs-lookup"><span data-stu-id="36f84-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="36f84-157">在 hello [Azure 管理入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="36f84-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="36f84-158">您可能已釘選它 toohello 儀表板 hello 上一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="36f84-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="36f84-159">如果您不是，您可以找到它，即可**瀏覽**，然後**CDN 設定檔**，而且 hello 設定檔上按一下您想 tooadd 至您的端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="36f84-160">hello CDN 設定檔 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="36f84-160">hello CDN profile blade appears.</span></span>
   
    ![CDN 設定檔][cdn-profile-settings]
2. <span data-ttu-id="36f84-162">按一下 hello**加入端點** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36f84-162">Click hello **Add Endpoint** button.</span></span>
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    <span data-ttu-id="36f84-164">hello**將端點加入**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="36f84-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. <span data-ttu-id="36f84-166">輸入這個 CDN 端點的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="36f84-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="36f84-167">此名稱將會使用的 tooaccess hello 網域您快取的資源`<EndpointName>.azureedge.net`。</span><span class="sxs-lookup"><span data-stu-id="36f84-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="36f84-168">在 hello**來源類型**下拉式清單中，選取*雲端服務*。</span><span class="sxs-lookup"><span data-stu-id="36f84-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="36f84-169">在 hello**來源主機名稱**下拉式清單中，選取您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="36f84-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="36f84-170">保留 hello 的預設值**原始路徑**，**原始主機標頭**，和**原始通訊協定/連接埠**。</span><span class="sxs-lookup"><span data-stu-id="36f84-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="36f84-171">您至少必須指定一個通訊協定 (HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="36f84-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="36f84-172">按一下 hello**新增**按鈕 toocreate hello 新端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="36f84-173">一旦建立 hello 端點時，它會出現在 hello 設定檔的端點清單。</span><span class="sxs-lookup"><span data-stu-id="36f84-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="36f84-174">hello 清單檢視會顯示 hello URL toouse tooaccess 快取內容，以及 hello 原始網域。</span><span class="sxs-lookup"><span data-stu-id="36f84-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![CDN 端點][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="36f84-176">hello 端點將無法立即可供使用。</span><span class="sxs-lookup"><span data-stu-id="36f84-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="36f84-177">就可以在透過 hello CDN 網路 hello 註冊 toopropagate too90 分鐘。</span><span class="sxs-lookup"><span data-stu-id="36f84-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="36f84-178">可透過 hello CDN hello 內容之前，立即嘗試 toouse hello CDN 網域名稱的使用者可能會收到狀態碼 404。</span><span class="sxs-lookup"><span data-stu-id="36f84-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="36f84-179">測試 hello CDN 端點</span><span class="sxs-lookup"><span data-stu-id="36f84-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="36f84-180">發行狀態的 hello 時**已完成**、 開啟瀏覽器視窗，並瀏覽過**http://<cdnName>*.azureedge.net/Content/bootstrap.css**。</span><span class="sxs-lookup"><span data-stu-id="36f84-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="36f84-181">在我的設定中，此 URL 為：</span><span class="sxs-lookup"><span data-stu-id="36f84-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="36f84-182">對應 toohello 遵循在 hello CDN 端點的原始 URL:</span><span class="sxs-lookup"><span data-stu-id="36f84-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="36f84-183">當您巡覽太**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**，根據您的瀏覽器中，您將會是提示的 toodownload 或開啟 hello bootstrap.css，來自已發行的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36f84-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="36f84-184">同樣地，您可以從 CDN 端點，以 http://&lt;serviceName>.cloudapp.net/ 存取任何可公開存取的 URL。</span><span class="sxs-lookup"><span data-stu-id="36f84-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="36f84-185">例如：</span><span class="sxs-lookup"><span data-stu-id="36f84-185">For example:</span></span>

* <span data-ttu-id="36f84-186">從 hello /Script 路徑.js 檔案</span><span class="sxs-lookup"><span data-stu-id="36f84-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="36f84-187">Hello /Content 從任何內容的檔案路徑</span><span class="sxs-lookup"><span data-stu-id="36f84-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="36f84-188">任何控制器/動作</span><span class="sxs-lookup"><span data-stu-id="36f84-188">Any controller/action</span></span>
* <span data-ttu-id="36f84-189">如果已在您的 CDN 端點，任何 URL 查詢字串以啟用 hello 查詢字串</span><span class="sxs-lookup"><span data-stu-id="36f84-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="36f84-190">事實上，以 hello 上述組態，您可以主控 hello 整個雲端服務從 **http://*&lt;cdnName >*.azureedge.net/**。如果太瀏覽**http://camservice.azureedge.net/ * * 將 hello 動作結果中的 Home/Index。</span><span class="sxs-lookup"><span data-stu-id="36f84-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="36f84-191">不過，這不表示永遠是個不錯的主意 tooserve 透過 Azure CDN 的整個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="36f84-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="36f84-192">CDN 與靜態傳遞最佳化不會不一定被加速並非 toobe 快取，或因為 hello CDN 必須 hello 資產的新版本從提取 hello 原始伺服器通常很頻繁地更新動態資產的傳遞。</span><span class="sxs-lookup"><span data-stu-id="36f84-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="36f84-193">針對此案例中，您可以啟用[動態網站加速](cdn-dynamic-site-acceleration.md)最佳化 (DSA)，您會使用各種技術 toospeed 向上傳遞非快取的動態資產的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="36f84-194">如果您有混合的靜態及動態內容的站台，您可以選擇 tooserve 靜態內容從 CDN 與靜態最佳化型別 （例如一般 web 傳遞） 和 tooserve 動態內容直接從 hello 原始伺服器，或是透過 CDNDSA 最佳化端點開啟個別的情況。</span><span class="sxs-lookup"><span data-stu-id="36f84-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="36f84-195">toothat 結束時，您已經看過如何 tooaccess 個別的內容檔案從 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="36f84-196">我將示範如何 tooserve 特定控制器動作，透過特定的 CDN 端點在服務控制器的動作，透過 Azure CDN 的內容。</span><span class="sxs-lookup"><span data-stu-id="36f84-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="36f84-197">hello 的替代方式是 toodetermine 的雲端服務中的案例為基礎的 tooserve 從 Azure CDN 的內容。</span><span class="sxs-lookup"><span data-stu-id="36f84-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="36f84-198">toothat 結束時，您已經看過如何 tooaccess 個別的內容檔案從 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="36f84-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="36f84-199">我將示範如何 tooserve 特定控制器動作，透過 hello 中的 CDN 端點[提供從控制器動作，透過 Azure CDN 的內容](#controller)。</span><span class="sxs-lookup"><span data-stu-id="36f84-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="36f84-200">在雲端服務中設定靜態檔案的快取選項</span><span class="sxs-lookup"><span data-stu-id="36f84-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="36f84-201">與雲端服務中的 Azure CDN 整合，您可以指定您想在 hello CDN 端點中快取靜態內容 toobe 的方式。</span><span class="sxs-lookup"><span data-stu-id="36f84-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="36f84-202">toodo，開啟*Web.config*從您的 Web 角色專案 (例如 WebRole1)，並加入`<staticContent>`項目太`<system.webServer>`。</span><span class="sxs-lookup"><span data-stu-id="36f84-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="36f84-203">hello 以下的 XML 設定 hello 快取 tooexpire 3 天內。</span><span class="sxs-lookup"><span data-stu-id="36f84-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="36f84-204">一旦您這樣做，您的雲端服務中的所有靜態檔案將會觀察的 hello 相同規則在您的 CDN 快取。</span><span class="sxs-lookup"><span data-stu-id="36f84-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="36f84-205">若要更精確控制快取設定，請將 *Web.config* 檔案加入至資料夾，並在檔案中新增您的設定。</span><span class="sxs-lookup"><span data-stu-id="36f84-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="36f84-206">例如，加入*Web.config*檔案 toohello *\Content*資料夾和取代 hello 內容以下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="36f84-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="36f84-207">這項設定會導致所有靜態檔案從 hello *\Content*資料夾 toobe 快取 15 天。</span><span class="sxs-lookup"><span data-stu-id="36f84-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="36f84-208">如需有關如何 tooconfigure hello`<clientCache>`項目，請參閱[用戶端快取&lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache)。</span><span class="sxs-lookup"><span data-stu-id="36f84-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="36f84-209">在[提供從控制器動作，透過 Azure CDN 的內容](#controller)，我也會顯示您如何設定控制器的動作結果的快取設定，以及在 hello CDN 快取中。</span><span class="sxs-lookup"><span data-stu-id="36f84-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="36f84-210">透過 Azure CDN 使用控制器動作提供內容</span><span class="sxs-lookup"><span data-stu-id="36f84-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="36f84-211">當您使用 Azure CDN 整合的雲端服務 Web 角色時，是相當容易 tooserve 從控制器動作，透過 hello Azure CDN 的內容。</span><span class="sxs-lookup"><span data-stu-id="36f84-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="36f84-212">以外處理您的雲端服務直接透過 Azure CDN （示範上面），[馬頓 Balliauw](https://twitter.com/maartenballiauw)為您示範如何 toodo 它與有趣 MemeGenerator 控制器中的[減少以 hello Azure CDN 的 hello 網站上的延遲時間](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="36f84-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="36f84-213">我在這裡簡單地重述一次。</span><span class="sxs-lookup"><span data-stu-id="36f84-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="36f84-214">假設您想要在您的雲端服務中的年輕 Chuck Norris 映像為基礎的 toogenerate memes (由相片[Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="36f84-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="36f84-215">您有簡單`Index`動作，可 hello 客戶 toospecify hello superlatives hello 影像中，然後產生 hello 卡通人物，一旦他們後 toohello 動作。</span><span class="sxs-lookup"><span data-stu-id="36f84-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="36f84-216">因為這是 Chuck Norris，您希望此頁面 toobecome 末來而多半極受歡迎全域。</span><span class="sxs-lookup"><span data-stu-id="36f84-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="36f84-217">這就是利用 Azure CDN 來提供半動態內容的一個最佳例子。</span><span class="sxs-lookup"><span data-stu-id="36f84-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="36f84-218">請遵循上述 toosetup hello 步驟，此控制器的動作：</span><span class="sxs-lookup"><span data-stu-id="36f84-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="36f84-219">在 hello *\Controllers*資料夾中，建立新的.cs 檔案呼叫*MemeGeneratorController.cs*並取代 hello 內容以 hello 遵循程式碼。</span><span class="sxs-lookup"><span data-stu-id="36f84-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="36f84-220">確定 tooreplace hello 反白顯示的部分是您 CDN 的名稱。</span><span class="sxs-lookup"><span data-stu-id="36f84-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="36f84-221">以滑鼠右鍵按一下 hello 預設`Index()`動作，並選取**加入檢視**。</span><span class="sxs-lookup"><span data-stu-id="36f84-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="36f84-222">接受下列 hello 設定值，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="36f84-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="36f84-223">開啟新的 hello *Views\MemeGenerator\Index.cshtml*和 hello 內容取代為下列簡單的 HTML 送出 hello superlatives hello:</span><span class="sxs-lookup"><span data-stu-id="36f84-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="36f84-224">重新發行 hello 雲端服務，並瀏覽過**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="36f84-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="36f84-225">當您送出 hello 表單值太`/MemeGenerator/Index`，hello`Index_Post`動作方法會傳回連結 toohello`Show`動作方法，以個別的輸入識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="36f84-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="36f84-226">當您按一下 hello 連結時，您會到達 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="36f84-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="36f84-227">如果您的本機偵錯工具已附加，將會取得本機的重新導向的 hello 一般偵錯經驗。</span><span class="sxs-lookup"><span data-stu-id="36f84-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="36f84-228">如果它 hello 雲端服務中執行，它會重新導向至：</span><span class="sxs-lookup"><span data-stu-id="36f84-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="36f84-229">對應 toohello 之後在您的 CDN 端點的原始 URL:</span><span class="sxs-lookup"><span data-stu-id="36f84-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="36f84-230">然後，您可以使用 hello`OutputCacheAttribute`屬性 hello`Generate`方法 toospecify 方式應該快取 hello 動作結果，這將會採用 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="36f84-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="36f84-231">下列程式碼 hello 指定快取的到期日 1 小時 （3600 秒）。</span><span class="sxs-lookup"><span data-stu-id="36f84-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="36f84-232">同樣地，您可從任何控制器動作的內容在您的雲端服務中透過您的 Azure CDN，預期的 hello 快取選項。</span><span class="sxs-lookup"><span data-stu-id="36f84-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="36f84-233">Hello 下一節，我將說明如何配套 tooserve hello，及縮短指令碼並透過 Azure CDN 的 CSS。</span><span class="sxs-lookup"><span data-stu-id="36f84-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="36f84-234">整合 ASP.NET 統合和縮製與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="36f84-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="36f84-235">指令碼和 CSS 樣式表不常變更，而是主要的 hello Azure CDN 快取。</span><span class="sxs-lookup"><span data-stu-id="36f84-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="36f84-236">處理 hello 整個 Web 角色透過 Azure CDN 是最簡單方式 toointegrate hello 統合及縮製的 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="36f84-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="36f84-237">不過，因為您可能不想 toodo 此，我將說明如何 toodo 它同時保留 hello 預期 develper 經驗的 ASP.NET 統合及縮製，例如：</span><span class="sxs-lookup"><span data-stu-id="36f84-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="36f84-238">絕佳的偵錯模式體驗</span><span class="sxs-lookup"><span data-stu-id="36f84-238">Great debug mode experience</span></span>
* <span data-ttu-id="36f84-239">流暢的部署</span><span class="sxs-lookup"><span data-stu-id="36f84-239">Streamlined deployment</span></span>
* <span data-ttu-id="36f84-240">立即更新 tooclients 指令碼/CSS 版本升級</span><span class="sxs-lookup"><span data-stu-id="36f84-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="36f84-241">CDN 端點失敗時的後援機制</span><span class="sxs-lookup"><span data-stu-id="36f84-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="36f84-242">儘可能不修改程式碼</span><span class="sxs-lookup"><span data-stu-id="36f84-242">Minimize code modification</span></span>

<span data-ttu-id="36f84-243">在 hello **WebRole1**您建立專案時[整合您的 Azure 網站的 Azure CDN 端點，並提供靜態內容在網頁中，從 Azure CDN](#deploy)，開啟*App_Start\BundleConfig.cs* ，看看 hello`bundles.Add()`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="36f84-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="36f84-244">第一次 hello`bundles.Add()`陳述式會將指令碼組合在 hello 虛擬目錄`~/bundles/jquery`。</span><span class="sxs-lookup"><span data-stu-id="36f84-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="36f84-245">然後，開啟*_layout.cshtml\_Layout.cshtml* toosee hello 指令碼組合標記的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="36f84-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="36f84-246">您應該能夠 toofind hello 遵循的 Razor 程式碼行：</span><span class="sxs-lookup"><span data-stu-id="36f84-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="36f84-247">Hello Azure Web 角色中執行此 Razor 程式碼時，它會呈現`<script>`標記 hello 指令碼類似 toohello 下列組合：</span><span class="sxs-lookup"><span data-stu-id="36f84-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="36f84-248">不過，當它執行 Visual Studio 中輸入`F5`，它會分別轉譯 hello 配套中的每個指令碼檔案 （在上述的 hello 情況下，只有一個指令碼檔案是 hello 配套中）：</span><span class="sxs-lookup"><span data-stu-id="36f84-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="36f84-249">這可讓您在開發環境中的 toodebug hello JavaScript 程式碼時降低並行的用戶端連線 （結合在一起） 並改進檔案下載效能 （縮小） 在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="36f84-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="36f84-250">Azure CDN 整合功能很不錯 toopreserve 它。</span><span class="sxs-lookup"><span data-stu-id="36f84-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="36f84-251">此外，由於 hello 轉譯組合已經包含自動產生的版本字串，您需要 tooreplicate 的功能，因此 hello 每當您更新您的 jQuery 版本透過 NuGet，它可以在 hello 用戶端更新儘速可能的。</span><span class="sxs-lookup"><span data-stu-id="36f84-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="36f84-252">請遵循以下 toointegration ASP.NET 統合及縮製與您的 CDN 端點的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="36f84-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="36f84-253">回到*App_Start\BundleConfig.cs*，修改 hello`bundles.Add()`方法 toouse 不同[配套建構函式](http://msdn.microsoft.com/library/jj646464.aspx)，其中指定 CDN 位址。</span><span class="sxs-lookup"><span data-stu-id="36f84-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="36f84-254">toodo，取代 hello`RegisterBundles`方法定義，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="36f84-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="36f84-255">要確定 tooreplace `<yourCDNName>` hello 的 Azure CDN 的名稱。</span><span class="sxs-lookup"><span data-stu-id="36f84-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="36f84-256">純文字的方式，在您要設定`bundles.UseCdn = true`並加入精心製作的 CDN URL tooeach 組合。</span><span class="sxs-lookup"><span data-stu-id="36f84-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="36f84-257">例如，hello 第一個建構函式在 hello 程式碼中：</span><span class="sxs-lookup"><span data-stu-id="36f84-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="36f84-258">是 hello 與相同：</span><span class="sxs-lookup"><span data-stu-id="36f84-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="36f84-259">這個建構函式會告知 ASP.NET 統合及縮製 toorender 個別的指令碼檔案偵錯時在本機，但使用 hello 指定有問題的 CDN 位址 tooaccess hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="36f84-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="36f84-260">不過，對於此謹慎建構的 CDN URL，請注意兩項重要特性：</span><span class="sxs-lookup"><span data-stu-id="36f84-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="36f84-261">此 CDN url hello 原點`http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`，這是實際 hello 虛擬目錄的雲端服務中的 hello 指令碼組合。</span><span class="sxs-lookup"><span data-stu-id="36f84-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="36f84-262">因為您使用 CDN 建構函式，hello hello 組合的 CDN 指令碼標記不再包含自動產生的 hello hello 轉譯 URL 中的版本字串。</span><span class="sxs-lookup"><span data-stu-id="36f84-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="36f84-263">每次 hello 指令碼組合會在您的 Azure CDN 的快取遺漏的已修改的 tooforce，您必須以手動方式產生唯一的版本字串。</span><span class="sxs-lookup"><span data-stu-id="36f84-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="36f84-264">在 hello 相同時間，此唯一的版本字串必須保持不變透過 hello 部署 toomaximize 在 Azure CDN 的快取點擊 hello 生命 hello 組合部署之後。</span><span class="sxs-lookup"><span data-stu-id="36f84-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="36f84-265">hello 查詢字串 v = < W.X.Y.Z > 提取從*Properties\AssemblyInfo.cs* Web 角色專案中。</span><span class="sxs-lookup"><span data-stu-id="36f84-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="36f84-266">您可以部署工作流程，其中包含每次發行 tooAzure 遞增 hello 組件版本。</span><span class="sxs-lookup"><span data-stu-id="36f84-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="36f84-267">或者，您可以修改*Properties\AssemblyInfo.cs*專案 tooautomatically 遞增 hello 版本字串中，每次建置時，使用 hello 萬用字元 ' *'。</span><span class="sxs-lookup"><span data-stu-id="36f84-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="36f84-268">例如：</span><span class="sxs-lookup"><span data-stu-id="36f84-268">For example:</span></span>
     
        <span data-ttu-id="36f84-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="36f84-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="36f84-270">產生的唯一字串 hello 存留期間部署的任何其他策略 toostreamline 運作此處所示。</span><span class="sxs-lookup"><span data-stu-id="36f84-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="36f84-271">重新發佈 hello 雲端服務和存取 hello 首頁。</span><span class="sxs-lookup"><span data-stu-id="36f84-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="36f84-272">檢視 hello hello 網頁的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="36f84-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="36f84-273">您應該能夠 toosee hello CDN URL 轉譯，每次您重新發行變更 tooyour 雲端服務是唯一的版本字串。</span><span class="sxs-lookup"><span data-stu-id="36f84-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="36f84-274">例如：</span><span class="sxs-lookup"><span data-stu-id="36f84-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="36f84-275">在 Visual Studio 中偵錯 Visual Studio 中的 hello 雲端服務輸入`F5`。，</span><span class="sxs-lookup"><span data-stu-id="36f84-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="36f84-276">檢視 hello hello 網頁的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="36f84-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="36f84-277">您仍然會看到每一個指令檔以個別方式轉譯，讓您在 Visual Studio 中享有一致的偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="36f84-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="36f84-278">CDN URL 的後援機制</span><span class="sxs-lookup"><span data-stu-id="36f84-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="36f84-279">當您的 Azure CDN 端點因任何原因失敗時，您會想網頁 toobe 智慧足夠 tooaccess 您的原始 Web 伺服器作為 hello 載入 JavaScript 或啟動程序的後援選項。</span><span class="sxs-lookup"><span data-stu-id="36f84-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="36f84-280">它是在您的網站，因為 tooCDN 無法使用，但提供的指令碼和樣式表更嚴重 toolose 重要頁面功能的嚴重 toolose 映像。</span><span class="sxs-lookup"><span data-stu-id="36f84-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="36f84-281">hello[配套](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx)類別包含內容呼叫[CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) ，可讓您的 CDN 失敗 tooconfigure hello 後援機制。</span><span class="sxs-lookup"><span data-stu-id="36f84-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="36f84-282">toouse 這個屬性，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="36f84-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="36f84-283">在 Web 角色專案中，開啟*App_Start\BundleConfig.cs*，其中每個新增 CDN URL[配套建構函式](http://msdn.microsoft.com/library/jj646464.aspx)，並讓 hello 下列反白顯示變更 tooadd 後援機制 toohello預設組合：</span><span class="sxs-lookup"><span data-stu-id="36f84-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="36f84-284">當`CdnFallbackExpression`是不是 null，指令碼會插入 hello HTML tootest 是否 hello 配套已順利載入，否則，請存取 hello 配套直接從 hello 原始 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="36f84-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="36f84-285">這個屬性需要 toobe 集合 tooa JavaScript 運算式會測試是否會正確載入 hello 個別 CDN 組合。</span><span class="sxs-lookup"><span data-stu-id="36f84-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="36f84-286">hello 運算式需要 tootest 每個組合不同相應 toohello 內容。</span><span class="sxs-lookup"><span data-stu-id="36f84-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="36f84-287">如 hello 預設組合上述：</span><span class="sxs-lookup"><span data-stu-id="36f84-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="36f84-288">`window.jquery` 定義於 jquery-{version}.js 中</span><span class="sxs-lookup"><span data-stu-id="36f84-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="36f84-289">`$.validator` 定義於 jquery.validate.js 中</span><span class="sxs-lookup"><span data-stu-id="36f84-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="36f84-290">`window.Modernizr` 定義於 modernizer-{version}.js 中</span><span class="sxs-lookup"><span data-stu-id="36f84-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="36f84-291">`$.fn.modal` 定義於 bootstrap.js 中</span><span class="sxs-lookup"><span data-stu-id="36f84-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="36f84-292">您可能已注意到我未設定 CdnFallbackExpression hello`~/Cointent/css`組合。</span><span class="sxs-lookup"><span data-stu-id="36f84-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="36f84-293">這是因為目前沒有[System.Web.Optimization 中的 bug](https://aspnetoptimization.codeplex.com/workitem/104) ，插入`<script>`標記而不是 hello 後援 CSS 預期的 hello`<link>`標記。</span><span class="sxs-lookup"><span data-stu-id="36f84-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="36f84-294">不過，[Ember 顧問團](https://github.com/EmberConsultingGroup) (英文) 提供一套良好的[樣式套件組合後援](https://github.com/EmberConsultingGroup/StyleBundleFallback) (英文)。</span><span class="sxs-lookup"><span data-stu-id="36f84-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="36f84-295">CSS toouse hello 因應措施建立新的.cs 檔案在您 Web 角色專案*App_Start*資料夾稱為*StyleBundleExtensions.cs*，並將其內容取代 hello[從程式碼GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs)。</span><span class="sxs-lookup"><span data-stu-id="36f84-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="36f84-296">在*App_Start\StyleFundleExtensions.cs*，重新命名 hello 命名空間 tooyour Web 角色的名稱 (例如**WebRole1**)。</span><span class="sxs-lookup"><span data-stu-id="36f84-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="36f84-297">請返回太`App_Start\BundleConfig.cs`和上次修改 hello`bundles.Add`陳述式搭配下列反白顯示的程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="36f84-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="36f84-298">這個新的擴充方法會使用 hello tooinject 編寫指令碼 hello HTML toocheck hello DOM 中，符合類別名稱、 規則名稱和 hello CSS 組合和便在 2008 年後 toohello 原始 Web 伺服器時 toofind hello 相符項目中定義的規則值相同的概念。</span><span class="sxs-lookup"><span data-stu-id="36f84-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="36f84-299">發佈一次 hello 雲端服務和存取 hello 首頁。</span><span class="sxs-lookup"><span data-stu-id="36f84-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="36f84-300">檢視 hello hello 網頁的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="36f84-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="36f84-301">您應該尋找類似 toohello 下列插入指令碼：</span><span class="sxs-lookup"><span data-stu-id="36f84-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="36f84-302">請注意，hello CSS 組合插入指令碼仍會包含從 hello hello 郵政編碼的地方剩餘`CdnFallbackExpression`hello 列中的屬性：</span><span class="sxs-lookup"><span data-stu-id="36f84-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="36f84-303">但由於 hello 第一部分 hello | |運算式一律會傳回 （在正上方的 hello 行），則為 true，hello document.write() 函式永遠不會執行。</span><span class="sxs-lookup"><span data-stu-id="36f84-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="36f84-304">相關資訊</span><span class="sxs-lookup"><span data-stu-id="36f84-304">More Information</span></span>
* [<span data-ttu-id="36f84-305">Hello Azure 內容傳遞網路 (CDN) 的概觀</span><span class="sxs-lookup"><span data-stu-id="36f84-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="36f84-306">使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="36f84-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="36f84-307">ASP.NET 統合和縮製</span><span class="sxs-lookup"><span data-stu-id="36f84-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
