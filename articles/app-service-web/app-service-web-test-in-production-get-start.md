---
title: "開始使用 Web Apps 的生產測試"
description: "了解 Azure App Service Web Apps 中的生產測試 (TiP) 功能。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="7a175-103">開始使用 Web Apps 的生產測試</span><span class="sxs-lookup"><span data-stu-id="7a175-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="7a175-104">在生產環境中測試，或使用實際的客戶流量實測您的 Web 應用程式，是應用程式開發人員逐漸整合至其[靈活式開發](https://en.wikipedia.org/wiki/Agile_software_development)方法的測試策略。</span><span class="sxs-lookup"><span data-stu-id="7a175-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="7a175-105">它可讓您在生產環境中使用實際使用者流量測試應用程式的品質，而不是在測試環境中以綜合資料進行測試。</span><span class="sxs-lookup"><span data-stu-id="7a175-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span></span> <span data-ttu-id="7a175-106">藉由將新的應用程式公開給實際的使用者，您得以獲知應用程式在部署之後可能發生的實際問題。</span><span class="sxs-lookup"><span data-stu-id="7a175-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span></span> <span data-ttu-id="7a175-107">您可以根據實際使用者流量的數量、速度和變化來確認應用程式更新的功能、效能和價值，這些都是您在測試環境中無法測得的。</span><span class="sxs-lookup"><span data-stu-id="7a175-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="7a175-108">App Service Web Apps 中的流量路由</span><span class="sxs-lookup"><span data-stu-id="7a175-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="7a175-109">透過 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 的流量路由功能，您可以將部分的實際使用者流量導向至一或多個[部署位置](web-sites-staged-publishing.md)，然後使用 [Azure Application Insights](/services/application-insights/) 或 [Azure HDInsight](/services/hdinsight/) 來分析您的應用程式，或使用協力廠商工具 (例如 [New Relic](/marketplace/partners/newrelic/newrelic/)) 來驗證變更。</span><span class="sxs-lookup"><span data-stu-id="7a175-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span></span> <span data-ttu-id="7a175-110">例如，您可以使用 App Service 實作下列案例：</span><span class="sxs-lookup"><span data-stu-id="7a175-110">For example, you can implement the following scenarios with App Service:</span></span>

* <span data-ttu-id="7a175-111">在部署至整個網站之前找出更新中的功能錯誤或效能瓶頸</span><span class="sxs-lookup"><span data-stu-id="7a175-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span></span>
* <span data-ttu-id="7a175-112">對 beta 應用程式測量可用性計量，以執行變更的「受控試驗」</span><span class="sxs-lookup"><span data-stu-id="7a175-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span></span>
* <span data-ttu-id="7a175-113">逐漸建構出新的更新，並在錯誤發生時依正常程序回復為目前的版本</span><span class="sxs-lookup"><span data-stu-id="7a175-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span></span> 
* <span data-ttu-id="7a175-114">在多個部署位置中執行 [A/B 測試](https://en.wikipedia.org/wiki/A/B_testing)或[多變量測試](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing)，以最佳化應用程式的商務成果</span><span class="sxs-lookup"><span data-stu-id="7a175-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="7a175-115">在 Web Apps 中使用流量路由的需求</span><span class="sxs-lookup"><span data-stu-id="7a175-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="7a175-116">您的 Web 應用程式必須在**標準**或**進階**層執行，因為多個部署位置有此需求。</span><span class="sxs-lookup"><span data-stu-id="7a175-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="7a175-117">若要正常運作流量路由，必須在使用者的瀏覽器中啟用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="7a175-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span></span> <span data-ttu-id="7a175-118">流量路由會使用 Cookie 將用戶端瀏覽器固定到用戶端工作階段存留期間的部署位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span></span>
* <span data-ttu-id="7a175-119">流量路由可透過 Azure PowerShell Cmdlet 支援進階的TiP 案例。</span><span class="sxs-lookup"><span data-stu-id="7a175-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-to-a-deployment-slot"></a><span data-ttu-id="7a175-120">將流量區段路由傳送至部署位置</span><span class="sxs-lookup"><span data-stu-id="7a175-120">Route traffic segment to a deployment slot</span></span>
<span data-ttu-id="7a175-121">在每個 TiP 案例的基本層級中，您會將預先定義百分比的實際流量路由傳送至非生產部署位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span></span> <span data-ttu-id="7a175-122">若要這樣做，請遵循下面的步驟：</span><span class="sxs-lookup"><span data-stu-id="7a175-122">To do this, follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="7a175-123">此處的步驟假設您已有[非生產部署位置](web-sites-staged-publishing.md)，而且所需的 Web 應用程式內容[已部署](web-sites-deploy.md)給它。</span><span class="sxs-lookup"><span data-stu-id="7a175-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span></span>
> 
> 

1. <span data-ttu-id="7a175-124">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7a175-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7a175-125">在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [流量路由]。</span><span class="sxs-lookup"><span data-stu-id="7a175-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="7a175-126">選取您要將流量路由傳送到的位置，以及您所需的總流量百分比，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7a175-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="7a175-127">移至部署位置的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7a175-127">Go to the deployment slot's blade.</span></span> <span data-ttu-id="7a175-128">現在您應該會看見路由傳送至該處的實際流量。</span><span class="sxs-lookup"><span data-stu-id="7a175-128">You should now see live traffic being routed to it.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="7a175-129">設定流量路由之後，會有指定百分比的用戶端隨機路由傳送至您的非生產位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span></span> <span data-ttu-id="7a175-130">不過，要特別注意的是，一旦用戶端自動路由傳送至特定位置，它在用戶端工作階段存留期間都會「固定」到該位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span></span> <span data-ttu-id="7a175-131">這會藉由使用 Cookie 固定使用者工作階段來完成。</span><span class="sxs-lookup"><span data-stu-id="7a175-131">This done using a cookie to pin the user session.</span></span> <span data-ttu-id="7a175-132">如果您檢視 HTTP 要求，您會發現每個後續要求中都有一個 `TipMix` Cookie。</span><span class="sxs-lookup"><span data-stu-id="7a175-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a><span data-ttu-id="7a175-133">強制將用戶端要求送至特定位置</span><span class="sxs-lookup"><span data-stu-id="7a175-133">Force client requests to a specific slot</span></span>
<span data-ttu-id="7a175-134">除了自動流量路由以外，App Service 也可以將要求路由傳送至特定位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span></span> <span data-ttu-id="7a175-135">如果您想要讓使用者能夠選擇加入或退出您的 beta 應用程式，這就非常有用。</span><span class="sxs-lookup"><span data-stu-id="7a175-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span></span> <span data-ttu-id="7a175-136">若要這樣做，必須使用 `x-ms-routing-name` 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="7a175-136">To do this, you use the `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="7a175-137">若要使用 `x-ms-routing-name` 將使用者重新路由傳送至特定位置，您必須確定該位置已新增至流量路由清單。</span><span class="sxs-lookup"><span data-stu-id="7a175-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span></span> <span data-ttu-id="7a175-138">由於您想要明確地路由傳送至某個位置，因此您所設定的實際路由百分比並不重要。</span><span class="sxs-lookup"><span data-stu-id="7a175-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="7a175-139">如果您想，您可以建立經使用者點按即可存取 beta 應用程式的「beta 連結」。</span><span class="sxs-lookup"><span data-stu-id="7a175-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="7a175-140">讓使用者選擇退出 beta 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a175-140">Opt users out of beta app</span></span>
<span data-ttu-id="7a175-141">舉例而言，若要讓使用者選擇退出您的 beta 應用程式，您可以在網頁中放入下列連結：</span><span class="sxs-lookup"><span data-stu-id="7a175-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

<span data-ttu-id="7a175-142">字串 `x-ms-routing-name=self` 會指定生產位置。</span><span class="sxs-lookup"><span data-stu-id="7a175-142">The string `x-ms-routing-name=self` specifies the production slot.</span></span> <span data-ttu-id="7a175-143">一旦用戶端瀏覽器存取此連結，不僅瀏覽器會重新導向至生產位置，後續的每個要求也會包含將工作階段固定到生產位置的 `x-ms-routing-name=self` Cookie。</span><span class="sxs-lookup"><span data-stu-id="7a175-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a><span data-ttu-id="7a175-144">讓使用者選擇加入 beta 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a175-144">Opt users in to beta app</span></span>
<span data-ttu-id="7a175-145">若要讓使用者選擇加入您的 beta 應用程式，請將相同的查詢參數設為非生產位置的名稱，例如：</span><span class="sxs-lookup"><span data-stu-id="7a175-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="7a175-146">其他資源</span><span class="sxs-lookup"><span data-stu-id="7a175-146">More resources</span></span>
* [<span data-ttu-id="7a175-147">針對 Azure App Service 中的 Web 應用程式設定預備環境</span><span class="sxs-lookup"><span data-stu-id="7a175-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="7a175-148">透過可預測方式在 Azure 中部署複雜應用程式</span><span class="sxs-lookup"><span data-stu-id="7a175-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="7a175-149">敏捷式軟體開發 (Agile Software Development) 與 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7a175-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="7a175-150">為 Web 應用程式有效地使用 DevOps 環境</span><span class="sxs-lookup"><span data-stu-id="7a175-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

