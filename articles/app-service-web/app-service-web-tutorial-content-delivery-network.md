---
title: "aaaAdd CDN tooan Azure App Service |Microsoft 文件"
description: "加入內容傳遞網路 (CDN) tooan Azure App Service toocache，並從伺服器關閉 tooyour hello 世界各地的客戶提供靜態檔案。"
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="d2833-103">將內容傳遞網路 (CDN) tooan Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d2833-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="d2833-104">[Azure 內容傳遞網路 (CDN)](../cdn/cdn-overview.md)會在策略性放置的位置傳遞內容 toousers tooprovide 最大輸送量的靜態網頁內容快取。</span><span class="sxs-lookup"><span data-stu-id="d2833-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="d2833-105">hello CDN 也會減少伺服器負載 web 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="d2833-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="d2833-106">本教學課程示範如何 tooadd Azure CDN tooa [Azure App Service 中的 web 應用程式](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="d2833-107">以下是 hello hello 範例靜態 HTML 網站首頁，您將使用：</span><span class="sxs-lookup"><span data-stu-id="d2833-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="d2833-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="d2833-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2833-110">建立 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d2833-111">重新整理快取的資產。</span><span class="sxs-lookup"><span data-stu-id="d2833-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="d2833-112">使用查詢字串快取 toocontrol 版本。</span><span class="sxs-lookup"><span data-stu-id="d2833-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d2833-113">使用自訂網域 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2833-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="d2833-114">Prerequisites</span></span>

<span data-ttu-id="d2833-115">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="d2833-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="d2833-116">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="d2833-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="d2833-117">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2833-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="d2833-118">建立 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d2833-118">Create hello web app</span></span>

<span data-ttu-id="d2833-119">toocreate hello web 應用程式，您會使用後續 hello[靜態 HTML 快速入門](app-service-web-get-started-html.md)透過 hello**瀏覽 toohello 應用程式**步驟。</span><span class="sxs-lookup"><span data-stu-id="d2833-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="d2833-120">備妥自訂網域</span><span class="sxs-lookup"><span data-stu-id="d2833-120">Have a custom domain ready</span></span>

<span data-ttu-id="d2833-121">toocomplete hello 自訂網域步驟本教學課程中，您需要 tooown 自訂網域，並存取 tooyour DNS 登錄的網域提供者 （例如 GoDaddy)。</span><span class="sxs-lookup"><span data-stu-id="d2833-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="d2833-122">例如，tooadd DNS 項目`contoso.com`和`www.contoso.com`，您必須擁有存取 tooconfigure hello 的 DNS 設定 hello`contoso.com`根網域。</span><span class="sxs-lookup"><span data-stu-id="d2833-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="d2833-123">如果您還沒有網域名稱，請考慮下列 hello[應用程式服務網域教學課程](custom-dns-web-site-buydomains-web-app.md)toopurchase 網域使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2833-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="d2833-124">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d2833-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="d2833-125">開啟瀏覽器並瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d2833-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="d2833-126">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="d2833-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="d2833-127">在左瀏覽 hello，選取**應用程式服務**，然後選取 hello 應用程式，您可以在 hello[靜態 HTML 快速入門](app-service-web-get-started-html.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![選取在 hello 入口網站 App Service 應用程式](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="d2833-129">在 hello **App Service**  頁面的 hello**設定**區段中，選取**網路 > 設定您的應用程式的 Azure CDN**。</span><span class="sxs-lookup"><span data-stu-id="d2833-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![選取在 hello 入口網站中的 CDN](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="d2833-131">在 hello **Azure 內容傳遞網路**頁面上，提供 hello**新端點**hello 資料表中所指定的設定。</span><span class="sxs-lookup"><span data-stu-id="d2833-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![在 hello 入口網站中建立設定檔和端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="d2833-133">設定</span><span class="sxs-lookup"><span data-stu-id="d2833-133">Setting</span></span> | <span data-ttu-id="d2833-134">建議的值</span><span class="sxs-lookup"><span data-stu-id="d2833-134">Suggested value</span></span> | <span data-ttu-id="d2833-135">說明</span><span class="sxs-lookup"><span data-stu-id="d2833-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="d2833-136">**CDN 設定檔**</span><span class="sxs-lookup"><span data-stu-id="d2833-136">**CDN profile**</span></span> | <span data-ttu-id="d2833-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="d2833-137">myCDNProfile</span></span> | <span data-ttu-id="d2833-138">選取**建立新**toocreate CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="d2833-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="d2833-139">CDN 設定檔是以 hello 的 CDN 端點的集合，相同的定價層。</span><span class="sxs-lookup"><span data-stu-id="d2833-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="d2833-140">**定價層**</span><span class="sxs-lookup"><span data-stu-id="d2833-140">**Pricing tier**</span></span> | <span data-ttu-id="d2833-141">標準 Akamai</span><span class="sxs-lookup"><span data-stu-id="d2833-141">Standard Akamai</span></span> | <span data-ttu-id="d2833-142">hello[定價層](../cdn/cdn-overview.md#azure-cdn-features)指定 hello 提供者和可用的功能。</span><span class="sxs-lookup"><span data-stu-id="d2833-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="d2833-143">在本教學課程中，我們會使用標準 Akamai。</span><span class="sxs-lookup"><span data-stu-id="d2833-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="d2833-144">**CDN 端點名稱**</span><span class="sxs-lookup"><span data-stu-id="d2833-144">**CDN endpoint name**</span></span> | <span data-ttu-id="d2833-145">任何在 hello azureedge.net 網域中為唯一的名稱</span><span class="sxs-lookup"><span data-stu-id="d2833-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="d2833-146">存取您快取的資源在 hello 網域*\<端點名稱 >。 azureedge.net*。</span><span class="sxs-lookup"><span data-stu-id="d2833-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="d2833-147">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="d2833-147">Select **Create**.</span></span>

<span data-ttu-id="d2833-148">Azure 會建立 hello 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="d2833-149">hello 新端點會出現在 hello**端點**清單 hello 相同頁面上，而且已佈建時 hello 狀態**執行**。</span><span class="sxs-lookup"><span data-stu-id="d2833-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![清單中的新端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="d2833-151">測試 hello CDN 端點</span><span class="sxs-lookup"><span data-stu-id="d2833-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="d2833-152">如果您選取了 Verizon 定價層，通常需要大約 90 分鐘的時間進行端點傳播。</span><span class="sxs-lookup"><span data-stu-id="d2833-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="d2833-153">若為 Akamai，傳播需要幾分鐘的時間</span><span class="sxs-lookup"><span data-stu-id="d2833-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="d2833-154">hello 範例應用程式具有`index.html`檔案和*css*， *img*，和*js*包含其他靜態資產的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d2833-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="d2833-155">內容的所有這些檔案的路徑是 hello hello 相同在 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="d2833-156">例如，這兩個 hello 下列 Url 存取 hello *bootstrap.css*檔案在 hello *css*資料夾：</span><span class="sxs-lookup"><span data-stu-id="d2833-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="d2833-157">瀏覽下列 URL 的瀏覽器 toohello:</span><span class="sxs-lookup"><span data-stu-id="d2833-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 提供的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="d2833-159">您會看到的 hello 相同頁面上您先前在 Azure web 應用程式中執行。</span><span class="sxs-lookup"><span data-stu-id="d2833-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="d2833-160">Azure CDN 已擷取 hello 來源 web 應用程式的資產，並為從 hello CDN 端點服務</span><span class="sxs-lookup"><span data-stu-id="d2833-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="d2833-161">tooensure hello CDN，重新整理 hello 頁面中，此頁面會快取。</span><span class="sxs-lookup"><span data-stu-id="d2833-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="d2833-162">兩個要求的 hello 相同資產有時候是必要的 hello CDN toocache hello 要求的內容。</span><span class="sxs-lookup"><span data-stu-id="d2833-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="d2833-163">如需建立 Azure CDN 設定檔和端點的詳細資訊，請參閱[開始使用 Azure CDN](../cdn/cdn-create-new-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="d2833-164">清除 hello CDN</span><span class="sxs-lookup"><span data-stu-id="d2833-164">Purge hello CDN</span></span>

<span data-ttu-id="d2833-165">hello CDN 會定期重新整理其資源與 hello 來源 web 應用程式根據 hello 存留時間 (TTL) 設定。</span><span class="sxs-lookup"><span data-stu-id="d2833-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="d2833-166">hello 預設 TTL 是七天。</span><span class="sxs-lookup"><span data-stu-id="d2833-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="d2833-167">有時候您可能需要 toorefresh hello CDN 之前 hello TTL 到期-比方說，當您部署更新的內容 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2833-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="d2833-168">tootrigger 重新整理，您可以手動清除 hello CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="d2833-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="d2833-169">在本節中的 hello 教學課程，您可以部署變更 toohello web 應用程式，並清除 hello CDN tootrigger hello CDN toorefresh 其快取。</span><span class="sxs-lookup"><span data-stu-id="d2833-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="d2833-170">部署變更 toohello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d2833-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="d2833-171">開啟 hello`index.html`檔案，然後加入"-V2"toohello H1 標題，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d2833-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="d2833-172">認可您的變更，並將它部署 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2833-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="d2833-173">部署完成後，請瀏覽 toohello web 應用程式 URL，並請參閱變更 hello。</span><span class="sxs-lookup"><span data-stu-id="d2833-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Web 應用程式標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="d2833-175">瀏覽 URL hello 首頁上和您看不到變更，因為 hello hello CDN 中快取的版本尚未到期的 hello toohello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中沒有 V2](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="d2833-177">清除 hello 入口網站中的 hello CDN</span><span class="sxs-lookup"><span data-stu-id="d2833-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="d2833-178">tootrigger hello CDN tooupdate 快取的版本中，清除 hello CDN。</span><span class="sxs-lookup"><span data-stu-id="d2833-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="d2833-179">在 hello 入口網站的左側瀏覽選取**資源群組**，然後選取您為您的 web 應用程式 (myResourceGroup) 建立的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d2833-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![選取資源群組](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="d2833-181">在 [hello] 清單中的資源，選取您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-181">In hello list of resources, select your CDN endpoint.</span></span>

![選取端點](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="d2833-183">頂端的 hello hello**端點**頁面上，按一下**清除**。</span><span class="sxs-lookup"><span data-stu-id="d2833-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![選取清除](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="d2833-185">輸入您想 toopurge hello 內容路徑。</span><span class="sxs-lookup"><span data-stu-id="d2833-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="d2833-186">您可以將個別檔案或路徑區段 toopurge 所傳遞的完整檔案路徑 toopurge，並重新整理資料夾中的所有內容。</span><span class="sxs-lookup"><span data-stu-id="d2833-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="d2833-187">因為您變更`index.html`，確定其中一個 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="d2833-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="d2833-188">在 hello hello 頁面底部，選取**清除**。</span><span class="sxs-lookup"><span data-stu-id="d2833-188">At hello bottom of hello page, select **Purge**.</span></span>

![清除頁面](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="d2833-190">確認 CDN 會更新該 hello</span><span class="sxs-lookup"><span data-stu-id="d2833-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="d2833-191">等候 hello 的清除要求完成處理時，通常需要幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="d2833-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="d2833-192">toosee hello 目前狀態，在 hello hello 頁面最上方的 hello 選取鈴鐺圖示。</span><span class="sxs-lookup"><span data-stu-id="d2833-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![清除通知](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="d2833-194">瀏覽 toohello CDN 端點 URL `index.html`，現在您會看見 hello V2 hello 首頁上，加入 toohello 標題和。</span><span class="sxs-lookup"><span data-stu-id="d2833-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="d2833-195">這會顯示 hello CDN 快取重新整理。</span><span class="sxs-lookup"><span data-stu-id="d2833-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="d2833-197">如需詳細資訊，請參閱[清除 Azure CDN 端點](../cdn/cdn-purge-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="d2833-198">使用查詢字串 tooversion 內容</span><span class="sxs-lookup"><span data-stu-id="d2833-198">Use query strings tooversion content</span></span>

<span data-ttu-id="d2833-199">hello Azure CDN 提供 hello 下列快取行為的選項：</span><span class="sxs-lookup"><span data-stu-id="d2833-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="d2833-200">忽略查詢字串</span><span class="sxs-lookup"><span data-stu-id="d2833-200">Ignore query strings</span></span>
* <span data-ttu-id="d2833-201">略過查詢字串的快取</span><span class="sxs-lookup"><span data-stu-id="d2833-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="d2833-202">快取每個唯一的 URL</span><span class="sxs-lookup"><span data-stu-id="d2833-202">Cache every unique URL</span></span> 

<span data-ttu-id="d2833-203">第一次 hello 這些是 hello 預設，這表示不論 hello 查詢字串 hello URL 中的資產只能有一個快取的版本。</span><span class="sxs-lookup"><span data-stu-id="d2833-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="d2833-204">在本節中的 hello 教學課程，您可以變更 hello 快取行為 toocache 每個唯一的 URL。</span><span class="sxs-lookup"><span data-stu-id="d2833-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="d2833-205">變更 hello 快取行為</span><span class="sxs-lookup"><span data-stu-id="d2833-205">Change hello cache behavior</span></span>

<span data-ttu-id="d2833-206">在 Azure 入口網站 hello **CDN 端點**頁面上，選取**快取**。</span><span class="sxs-lookup"><span data-stu-id="d2833-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="d2833-207">選取**快取每個唯一的 URL**從 hello**查詢字串快取行為**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d2833-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="d2833-208">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d2833-208">Select **Save**.</span></span>

![選取查詢字串快取行為](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="d2833-210">確認唯一的 URL 會分開快取</span><span class="sxs-lookup"><span data-stu-id="d2833-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="d2833-211">在瀏覽器中，瀏覽 toohello 首頁上，在 hello CDN 端點，但包含查詢字串：</span><span class="sxs-lookup"><span data-stu-id="d2833-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="d2833-212">hello CDN 傳回 hello 目前 web 應用程式內容，其中包含 「 V2"hello 標題中。</span><span class="sxs-lookup"><span data-stu-id="d2833-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="d2833-213">tooensure hello CDN，重新整理 hello 頁面中，此頁面會快取。</span><span class="sxs-lookup"><span data-stu-id="d2833-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="d2833-214">開啟`index.html`也變更 「 V2"和"V3"，並將部署的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d2833-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="d2833-215">在瀏覽器，移 toohello CDN 端點 URL 」 包含新的查詢字串例如`q=2`。</span><span class="sxs-lookup"><span data-stu-id="d2833-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="d2833-216">目前的 hello CDN 取得 hello`index.html`檔並且顯示"V3"。</span><span class="sxs-lookup"><span data-stu-id="d2833-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="d2833-217">但是，如果您瀏覽 toohello CDN 端點以 hello`q=1`查詢字串，您會看到 「 V2"。</span><span class="sxs-lookup"><span data-stu-id="d2833-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN 標題中的 V3，查詢字串 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN 標題中的 V2，查詢字串 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="d2833-220">此輸出會顯示每個查詢字串是以不同方式處理：</span><span class="sxs-lookup"><span data-stu-id="d2833-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="d2833-221">以前使用 q=1，因此會傳回快取內容 (V2)。</span><span class="sxs-lookup"><span data-stu-id="d2833-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="d2833-222">q = 2 是新的因此 hello 最新的 web 應用程式內容都會擷取並傳回 (V3)。</span><span class="sxs-lookup"><span data-stu-id="d2833-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="d2833-223">如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../cdn/cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="d2833-224">對應的自訂網域 tooa CDN 端點</span><span class="sxs-lookup"><span data-stu-id="d2833-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="d2833-225">您會藉由建立一筆 CNAME 記錄對應您的自訂網域 tooyour CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="d2833-226">CNAME 記錄是一種 DNS 功能，將來源網域 tooa 目的地定義域對應。</span><span class="sxs-lookup"><span data-stu-id="d2833-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="d2833-227">例如，您可能會將對應`cdn.contoso.com`或`static.contoso.com`太`contoso.azureedge.net`。</span><span class="sxs-lookup"><span data-stu-id="d2833-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="d2833-228">如果您沒有自訂網域，請考慮下列 hello[應用程式服務網域教學課程](custom-dns-web-site-buydomains-web-app.md)toopurchase 網域使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2833-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="d2833-229">尋找 hello hostname toouse 以 hello CNAME</span><span class="sxs-lookup"><span data-stu-id="d2833-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="d2833-230">Hello Azure 入口網站中**端點**頁面上，確定**概觀**已選取左瀏覽，，然後選取 hello hello **+ 自訂網域**hello hello 頁頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2833-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![選取新增自訂網域](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="d2833-232">在 [hello**加入自訂網域**] 頁面上，您會看到 hello 端點主機名稱 toouse 中建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d2833-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="d2833-233">hello 主機名稱衍生自您的 CDN 端點 URL: **&lt;端點名稱 >。 azureedge.net**。</span><span class="sxs-lookup"><span data-stu-id="d2833-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![新增網域頁面](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="d2833-235">設定向網域註冊機構 hello CNAME</span><span class="sxs-lookup"><span data-stu-id="d2833-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="d2833-236">瀏覽 tooyour 網域註冊機構的網站，並找出 hello 區段，用於建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d2833-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="d2833-237">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="d2833-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="d2833-238">用於管理 Cname 尋找 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="d2833-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="d2833-239">您可能會有 toogo tooan 進階的設定 頁面上，並尋找 hello 文字 CNAME、 別名或子網域。</span><span class="sxs-lookup"><span data-stu-id="d2833-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="d2833-240">建立 CNAME 記錄對應您所選擇的子網域 (例如，**靜態**或**cdn**) toohello**端點主機名稱**hello 入口網站中稍早所示。</span><span class="sxs-lookup"><span data-stu-id="d2833-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="d2833-241">輸入在 Azure 中的 hello 自訂網域</span><span class="sxs-lookup"><span data-stu-id="d2833-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="d2833-242">傳回 toohello**加入自訂網域**頁面，然後輸入您的自訂網域，包括 hello 子網域，在 [hello] 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="d2833-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="d2833-243">例如，輸入 `cdn.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="d2833-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="d2833-244">Azure 會確認 hello CNAME 記錄存在您所輸入的 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d2833-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="d2833-245">如果 hello CNAME 正確無誤，則會驗證您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="d2833-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="d2833-246">可能需要 hello CNAME 記錄 toopropagate tooname 伺服器 hello 網際網路上的時間。</span><span class="sxs-lookup"><span data-stu-id="d2833-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="d2833-247">如果您的網域不會立即驗證，請稍候幾分鐘，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="d2833-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="d2833-248">測試 hello 自訂網域</span><span class="sxs-lookup"><span data-stu-id="d2833-248">Test hello custom domain</span></span>

<span data-ttu-id="d2833-249">在瀏覽器中，瀏覽 toohello`index.html`檔案使用自訂網域 (例如， `cdn.contoso.com/index.html`) tooverify hello 結果是相同 hello 做為當您移直接太`<endpointname>azureedge.net/index.html`。</span><span class="sxs-lookup"><span data-stu-id="d2833-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![使用自訂網域 URL 的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="d2833-251">如需詳細資訊，請參閱[對應 Azure CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="d2833-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d2833-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2833-252">Next steps</span></span>

<span data-ttu-id="d2833-253">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="d2833-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2833-254">建立 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d2833-255">重新整理快取的資產。</span><span class="sxs-lookup"><span data-stu-id="d2833-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="d2833-256">使用查詢字串快取 toocontrol 版本。</span><span class="sxs-lookup"><span data-stu-id="d2833-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d2833-257">使用自訂網域 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d2833-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="d2833-258">了解下列 hello toooptimize CDN 效能的文件：</span><span class="sxs-lookup"><span data-stu-id="d2833-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2833-259">在 Azure CDN 中壓縮檔案以改善效能</span><span class="sxs-lookup"><span data-stu-id="d2833-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2833-260">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="d2833-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
