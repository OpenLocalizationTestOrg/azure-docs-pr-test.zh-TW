---
title: "將 CDN 新增至 Azure App Service | Microsoft Docs"
description: "將內容傳遞網路 (CDN) 新增至 Azure App Service，以從您在世界各地的客戶附近的伺服器快取和傳遞靜態檔案。"
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="ed75e-103">將內容傳遞網路 (CDN) 新增至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ed75e-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="ed75e-104">[Azure 內容傳遞網路 (CDN)](../cdn/cdn-overview.md) 會在策略性放置的位置上快取靜態 Web 內容，以提供最大輸送量來將內容傳遞給使用者。</span><span class="sxs-lookup"><span data-stu-id="ed75e-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="ed75e-105">CDN 也可降低您的 Web 應用程式的伺服器負載。</span><span class="sxs-lookup"><span data-stu-id="ed75e-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="ed75e-106">本教學課程說明如何將 Azure CDN 新增至 [Azure App Service 中的 Web 應用程式](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="ed75e-107">以下是您將使用的範例靜態 HTML 網站首頁︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="ed75e-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="ed75e-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed75e-110">建立 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="ed75e-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ed75e-111">重新整理快取的資產。</span><span class="sxs-lookup"><span data-stu-id="ed75e-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="ed75e-112">使用查詢字串來控制快取的版本。</span><span class="sxs-lookup"><span data-stu-id="ed75e-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="ed75e-113">使用 CDN 端點的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="ed75e-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed75e-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed75e-114">Prerequisites</span></span>

<span data-ttu-id="ed75e-115">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="ed75e-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="ed75e-116">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="ed75e-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="ed75e-117">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ed75e-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="ed75e-118">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ed75e-118">Create the web app</span></span>

<span data-ttu-id="ed75e-119">若要建立您將使用的 Web 應用程式，請遵循[靜態 HTML 快速入門](app-service-web-get-started-html.md)的**瀏覽至應用程式**步驟。</span><span class="sxs-lookup"><span data-stu-id="ed75e-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="ed75e-120">備妥自訂網域</span><span class="sxs-lookup"><span data-stu-id="ed75e-120">Have a custom domain ready</span></span>

<span data-ttu-id="ed75e-121">若要完成本教學課程的自訂網域步驟，您需要擁有自訂網域並且具有網域提供者 (例如 GoDaddy) 的 DNS 登錄存取權。</span><span class="sxs-lookup"><span data-stu-id="ed75e-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="ed75e-122">例如，若要為 `contoso.com` 和 `www.contoso.com` 新增 DNS 項目，您必須有權設定 `contoso.com` 根網域的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="ed75e-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="ed75e-123">如果您還沒有網域名稱，請考慮遵循 [App Service 網域教學課程](custom-dns-web-site-buydomains-web-app.md)的作法，使用 Azure 入口網站來購買網域。</span><span class="sxs-lookup"><span data-stu-id="ed75e-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="ed75e-124">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ed75e-124">Log in to the Azure portal</span></span>

<span data-ttu-id="ed75e-125">開啟瀏覽器並瀏覽至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="ed75e-126">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="ed75e-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="ed75e-127">在左側導覽中，選取 [應用程式服務]，然後選取您在[靜態 HTML 快速入門](app-service-web-get-started-html.md)中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed75e-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![在入口網站中選取 App Service 應用程式](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="ed75e-129">在 [App Service] 頁面的 [設定] 區段中，選取 [網路] > [設定您應用程式的 Azure CDN]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![在入口網站中選取 CDN](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="ed75e-131">在 [Azure 內容傳遞網路] 頁面中，提供表格中所指定的 [新端點] 設定。</span><span class="sxs-lookup"><span data-stu-id="ed75e-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![在入口網站中建立設定檔和端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="ed75e-133">設定</span><span class="sxs-lookup"><span data-stu-id="ed75e-133">Setting</span></span> | <span data-ttu-id="ed75e-134">建議的值</span><span class="sxs-lookup"><span data-stu-id="ed75e-134">Suggested value</span></span> | <span data-ttu-id="ed75e-135">說明</span><span class="sxs-lookup"><span data-stu-id="ed75e-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="ed75e-136">**CDN 設定檔**</span><span class="sxs-lookup"><span data-stu-id="ed75e-136">**CDN profile**</span></span> | <span data-ttu-id="ed75e-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="ed75e-137">myCDNProfile</span></span> | <span data-ttu-id="ed75e-138">選取 [新建] 以建立 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ed75e-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="ed75e-139">CDN 設定檔是定價層相同的 CDN 端點集合。</span><span class="sxs-lookup"><span data-stu-id="ed75e-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="ed75e-140">**定價層**</span><span class="sxs-lookup"><span data-stu-id="ed75e-140">**Pricing tier**</span></span> | <span data-ttu-id="ed75e-141">標準 Akamai</span><span class="sxs-lookup"><span data-stu-id="ed75e-141">Standard Akamai</span></span> | <span data-ttu-id="ed75e-142">[定價層](../cdn/cdn-overview.md#azure-cdn-features)指定提供者和可用的功能。</span><span class="sxs-lookup"><span data-stu-id="ed75e-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="ed75e-143">在本教學課程中，我們會使用標準 Akamai。</span><span class="sxs-lookup"><span data-stu-id="ed75e-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="ed75e-144">**CDN 端點名稱**</span><span class="sxs-lookup"><span data-stu-id="ed75e-144">**CDN endpoint name**</span></span> | <span data-ttu-id="ed75e-145">azureedge.net 網域中任何唯一的名稱</span><span class="sxs-lookup"><span data-stu-id="ed75e-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="ed75e-146">您可在網域 *\<endpointname>.azureedge.net* 存取快取的資源。</span><span class="sxs-lookup"><span data-stu-id="ed75e-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="ed75e-147">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-147">Select **Create**.</span></span>

<span data-ttu-id="ed75e-148">Azure 會建立設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="ed75e-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="ed75e-149">新端點會出現在相同頁面上的 [端點] 清單中，而且其佈建後的狀態為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![清單中的新端點](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="ed75e-151">測試 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="ed75e-151">Test the CDN endpoint</span></span>

<span data-ttu-id="ed75e-152">如果您選取了 Verizon 定價層，通常需要大約 90 分鐘的時間進行端點傳播。</span><span class="sxs-lookup"><span data-stu-id="ed75e-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="ed75e-153">若為 Akamai，傳播需要幾分鐘的時間</span><span class="sxs-lookup"><span data-stu-id="ed75e-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="ed75e-154">範例應用程式有 `index.html` 檔案以及包含其他靜態資產的 css、img 和 js 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed75e-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="ed75e-155">在 CDN 端點上，上述所有檔案的內容路徑都相同。</span><span class="sxs-lookup"><span data-stu-id="ed75e-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="ed75e-156">例如，下列 URL 可存取 css 資料夾中的 bootstrap.css 檔案︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="ed75e-157">在瀏覽器中瀏覽至下列 URL：</span><span class="sxs-lookup"><span data-stu-id="ed75e-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 提供的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="ed75e-159">您會看到與您稍早在 Azure Web 應用程式中執行的相同分頁。</span><span class="sxs-lookup"><span data-stu-id="ed75e-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="ed75e-160">Azure CDN 已擷取原始 Web 應用程式的資產，並從 CDN 端點提供這些資產</span><span class="sxs-lookup"><span data-stu-id="ed75e-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="ed75e-161">若要確保此頁面已在 CDN 中快取，請重新整理此頁面。</span><span class="sxs-lookup"><span data-stu-id="ed75e-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="ed75e-162">CDN 有時需要相同資產的兩個要求，才能快取所要求的內容。</span><span class="sxs-lookup"><span data-stu-id="ed75e-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="ed75e-163">如需建立 Azure CDN 設定檔和端點的詳細資訊，請參閱[開始使用 Azure CDN](../cdn/cdn-create-new-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="ed75e-164">清除 CDN</span><span class="sxs-lookup"><span data-stu-id="ed75e-164">Purge the CDN</span></span>

<span data-ttu-id="ed75e-165">CDN 會根據存留時間 (TTL) 組態，從原始 web 應用程式定期重新整理其資源。</span><span class="sxs-lookup"><span data-stu-id="ed75e-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="ed75e-166">預設 TTL 為 7 天。</span><span class="sxs-lookup"><span data-stu-id="ed75e-166">The default TTL is seven days.</span></span>

<span data-ttu-id="ed75e-167">有時候，您可能需要在 TTL 到期日之前重新整理CDN 更新的內容部署至 web 應用程式時，-例如，。</span><span class="sxs-lookup"><span data-stu-id="ed75e-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="ed75e-168">若要觸發重新整理，您可以手動清除 CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="ed75e-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="ed75e-169">在本節的教學課程中，您會將變更部署到 Web 應用程式並清除 CDN，進而觸發 CDN 重新整理其快取。</span><span class="sxs-lookup"><span data-stu-id="ed75e-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="ed75e-170">將變更部署到 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ed75e-170">Deploy a change to the web app</span></span>

<span data-ttu-id="ed75e-171">開啟 `index.html` 檔案並將 "- V2" 新增至 H1 標題，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="ed75e-172">認可您的變更並將它部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed75e-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="ed75e-173">完成部署後，瀏覽至 Web 應用程式 URL，您會看到變更。</span><span class="sxs-lookup"><span data-stu-id="ed75e-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Web 應用程式標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="ed75e-175">瀏覽至首頁的 CDN 端點 URL，因為 CDN 中快取的版本尚未到期，所以您不會看到變更。</span><span class="sxs-lookup"><span data-stu-id="ed75e-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中沒有 V2](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="ed75e-177">在入口網站中清除 CDN</span><span class="sxs-lookup"><span data-stu-id="ed75e-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="ed75e-178">若要觸發 CDN 更新其快取的版本，請清除 CDN。</span><span class="sxs-lookup"><span data-stu-id="ed75e-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="ed75e-179">在入口網站的左側導覽中，選取 [資源群組]，然後選取您為 Web 應用程式 (myResourceGroup) 建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ed75e-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![選取資源群組](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="ed75e-181">在資源清單中，選取您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="ed75e-181">In the list of resources, select your CDN endpoint.</span></span>

![選取端點](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="ed75e-183">在 [端點] 頁面的頂端，按一下 [清除]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![選取清除](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="ed75e-185">輸入您想要清除的內容路徑。</span><span class="sxs-lookup"><span data-stu-id="ed75e-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="ed75e-186">您可以傳遞完整檔案路徑來清除個別檔案，也可以傳遞路徑區段來清除並重新整理資料夾中的所有內容。</span><span class="sxs-lookup"><span data-stu-id="ed75e-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="ed75e-187">因為您變更了 `index.html`，請確定這是其中一個路徑。</span><span class="sxs-lookup"><span data-stu-id="ed75e-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="ed75e-188">選取頁面底部的 [清除]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-188">At the bottom of the page, select **Purge**.</span></span>

![清除頁面](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="ed75e-190">確認 CDN 已更新</span><span class="sxs-lookup"><span data-stu-id="ed75e-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="ed75e-191">等到清除要求完成處理，通常需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ed75e-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="ed75e-192">若要查看目前的狀態，請選取頁面頂端的鈴鐺圖示。</span><span class="sxs-lookup"><span data-stu-id="ed75e-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![清除通知](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="ed75e-194">瀏覽至 `index.html` 的 CDN 端點 URL，您現在會看到已新增至首頁標題的 V2。</span><span class="sxs-lookup"><span data-stu-id="ed75e-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="ed75e-195">這會顯示已重新整理的 CDN 快取。</span><span class="sxs-lookup"><span data-stu-id="ed75e-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN 標題中的 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="ed75e-197">如需詳細資訊，請參閱[清除 Azure CDN 端點](../cdn/cdn-purge-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="ed75e-198">使用查詢字串來控制內容版本</span><span class="sxs-lookup"><span data-stu-id="ed75e-198">Use query strings to version content</span></span>

<span data-ttu-id="ed75e-199">Azure CDN 提供下列快取行為選項︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="ed75e-200">忽略查詢字串</span><span class="sxs-lookup"><span data-stu-id="ed75e-200">Ignore query strings</span></span>
* <span data-ttu-id="ed75e-201">略過查詢字串的快取</span><span class="sxs-lookup"><span data-stu-id="ed75e-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="ed75e-202">快取每個唯一的 URL</span><span class="sxs-lookup"><span data-stu-id="ed75e-202">Cache every unique URL</span></span> 

<span data-ttu-id="ed75e-203">上述第一個選項是預設值，這表示不管 URL 中的查詢字串為何，資產都只有一個快取的版本。</span><span class="sxs-lookup"><span data-stu-id="ed75e-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="ed75e-204">在本節的教學課程中，您可將快取行為變更為快取每個唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="ed75e-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="ed75e-205">變更快取行為</span><span class="sxs-lookup"><span data-stu-id="ed75e-205">Change the cache behavior</span></span>

<span data-ttu-id="ed75e-206">在 Azure 入口網站的 [CDN 端點] 頁面中，選取 [快取]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="ed75e-207">從 [查詢字串快取行為] 下拉式清單中，選取 [快取每個唯一 URL]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="ed75e-208">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-208">Select **Save**.</span></span>

![選取查詢字串快取行為](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="ed75e-210">確認唯一的 URL 會分開快取</span><span class="sxs-lookup"><span data-stu-id="ed75e-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="ed75e-211">在瀏覽器中，瀏覽至 CDN 端點首頁，但包含查詢字串︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="ed75e-212">CDN 會傳回目前的 Web 應用程式內容，其標題中包含 "V2"。</span><span class="sxs-lookup"><span data-stu-id="ed75e-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="ed75e-213">若要確保此頁面已在 CDN 中快取，請重新整理此頁面。</span><span class="sxs-lookup"><span data-stu-id="ed75e-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="ed75e-214">開啟 `index.html` 並將 "V2" 變更為 "V3"，然後部署變更。</span><span class="sxs-lookup"><span data-stu-id="ed75e-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="ed75e-215">在瀏覽器中，移至含有新查詢字串 (例如`q=2`) 的 CDN 端點 URL。</span><span class="sxs-lookup"><span data-stu-id="ed75e-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="ed75e-216">CDN 會取得目前的 `index.html` 檔案並顯示 "V3"。</span><span class="sxs-lookup"><span data-stu-id="ed75e-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="ed75e-217">但是，如果您瀏覽至含有 `q=1` 查詢字串的 CDN 端點，您會看到 "V2"。</span><span class="sxs-lookup"><span data-stu-id="ed75e-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN 標題中的 V3，查詢字串 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN 標題中的 V2，查詢字串 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="ed75e-220">此輸出會顯示每個查詢字串是以不同方式處理：</span><span class="sxs-lookup"><span data-stu-id="ed75e-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="ed75e-221">以前使用 q=1，因此會傳回快取內容 (V2)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="ed75e-222">q=2 是新的，因此會擷取及傳回最新的 Web 應用程式內容 (V3)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="ed75e-223">如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../cdn/cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="ed75e-224">將自訂網域對應至 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="ed75e-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="ed75e-225">您會建立 CNAME 記錄，以將自訂網域對應至 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="ed75e-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="ed75e-226">CNAME 記錄是將來源網域對應至目的地網域的 DNS 功能。</span><span class="sxs-lookup"><span data-stu-id="ed75e-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="ed75e-227">例如，您可能會將 `cdn.contoso.com` 或 `static.contoso.com` 對應到 `contoso.azureedge.net`。</span><span class="sxs-lookup"><span data-stu-id="ed75e-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="ed75e-228">如果您沒有自訂網域，請考慮遵循 [App Service 網域教學課程](custom-dns-web-site-buydomains-web-app.md)的作法，使用 Azure 入口網站來購買網域。</span><span class="sxs-lookup"><span data-stu-id="ed75e-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="ed75e-229">尋找要搭配 CNAME 使用的主機名稱</span><span class="sxs-lookup"><span data-stu-id="ed75e-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="ed75e-230">在 Azure 入口網站的 [端點] 頁面中，確定已選取左側導覽中的 [概觀]，然後選取頁面頂端的 [+ 自訂網域] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed75e-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![選取新增自訂網域](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="ed75e-232">在 [新增自訂網域] 頁面中，您會看到要用於建立 CNAME 記錄的端點主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ed75e-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="ed75e-233">主機名稱衍生自 CDN 端點 URL：**&lt;EndpointName>.azureedge.net**。</span><span class="sxs-lookup"><span data-stu-id="ed75e-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![新增網域頁面](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="ed75e-235">透過您的網域註冊機構設定 CNAME</span><span class="sxs-lookup"><span data-stu-id="ed75e-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="ed75e-236">瀏覽至您網域註冊機構的網站，並找出用於建立 DNS 記錄的區段。</span><span class="sxs-lookup"><span data-stu-id="ed75e-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="ed75e-237">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="ed75e-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="ed75e-238">尋找管理 CNAME 的區段。</span><span class="sxs-lookup"><span data-stu-id="ed75e-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="ed75e-239">您可能需要移至進階設定頁面，並尋找 CNAME、Alias 或 Subdomains 單字。</span><span class="sxs-lookup"><span data-stu-id="ed75e-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="ed75e-240">建立 CNAME 記錄，將您選擇的子網域 (例如 **static** 或 **cdn**) 對應到入口網站中稍早顯示的 [端點主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="ed75e-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="ed75e-241">在 Azure 中輸入自訂網域</span><span class="sxs-lookup"><span data-stu-id="ed75e-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="ed75e-242">返回 [新增自訂網域]  頁面，在對話方塊中輸入您的自訂網域 (包括子網域)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="ed75e-243">例如，輸入 `cdn.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="ed75e-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="ed75e-244">Azure 會確認您所輸入的網域名稱存在 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ed75e-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="ed75e-245">如果 CNAME 正確，您的自訂網域就會驗證。</span><span class="sxs-lookup"><span data-stu-id="ed75e-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="ed75e-246">可能需要時間讓 CNAME 記錄傳播到網際網路上的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="ed75e-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="ed75e-247">如果您的網域不會立即驗證，請稍候幾分鐘，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="ed75e-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="ed75e-248">測試自訂網域</span><span class="sxs-lookup"><span data-stu-id="ed75e-248">Test the custom domain</span></span>

<span data-ttu-id="ed75e-249">在瀏覽器中，使用自訂網域 (例如 `cdn.contoso.com/index.html`) 瀏覽至 `index.html` 檔案，確認結果與您直接移至 `<endpointname>azureedge.net/index.html` 時相同。</span><span class="sxs-lookup"><span data-stu-id="ed75e-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![使用自訂網域 URL 的範例應用程式首頁](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="ed75e-251">如需詳細資訊，請參閱[將 Azure CDN 內容對應至自訂網域](../cdn/cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="ed75e-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ed75e-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed75e-252">Next steps</span></span>

<span data-ttu-id="ed75e-253">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="ed75e-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed75e-254">建立 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="ed75e-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ed75e-255">重新整理快取的資產。</span><span class="sxs-lookup"><span data-stu-id="ed75e-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="ed75e-256">使用查詢字串來控制快取的版本。</span><span class="sxs-lookup"><span data-stu-id="ed75e-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="ed75e-257">使用 CDN 端點的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="ed75e-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="ed75e-258">在下列文章中了解如何將 CDN 效能最佳化：</span><span class="sxs-lookup"><span data-stu-id="ed75e-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed75e-259">在 Azure CDN 中壓縮檔案以改善效能</span><span class="sxs-lookup"><span data-stu-id="ed75e-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed75e-260">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="ed75e-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
