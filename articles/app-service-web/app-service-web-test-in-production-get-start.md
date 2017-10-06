---
title: "開始使用 Web 應用程式的生產環境中測試 aaaGet"
description: "深入了解 Azure App Service Web 應用程式中的實際執行環境 (TiP) 功能中的 hello 測試。"
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
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="07815-103">開始使用 Web Apps 的生產測試</span><span class="sxs-lookup"><span data-stu-id="07815-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="07815-104">在生產環境中測試，或使用實際的客戶流量實測您的 Web 應用程式，是應用程式開發人員逐漸整合至其[靈活式開發](https://en.wikipedia.org/wiki/Agile_software_development)方法的測試策略。</span><span class="sxs-lookup"><span data-stu-id="07815-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="07815-105">它可讓您 tootest hello 品質的應用程式與即時的使用者流量在實際執行環境中，做為相對於的 toosynthesized 在測試環境中的資料。</span><span class="sxs-lookup"><span data-stu-id="07815-105">It enables you tootest hello quality of your apps with live user traffic in your production environment, as opposed toosynthesized data in a test environment.</span></span> <span data-ttu-id="07815-106">藉由公開您新的應用程式 tooreal 使用者，您可以通知 hello 真正的問題，一旦部署之後，您的應用程式可能會面臨上。</span><span class="sxs-lookup"><span data-stu-id="07815-106">By exposing your new app tooreal users, you can be informed on hello real problems your app may face once it is deployed.</span></span> <span data-ttu-id="07815-107">您可以確認 hello 功能、 效能及針對 hello 磁碟區、 速度，以及各種不同的真正的使用者流量，您可以在測試環境中永遠不會近似您應用程式更新的值。</span><span class="sxs-lookup"><span data-stu-id="07815-107">You can verify hello functionality, performance, and value of your app updates against hello volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="07815-108">App Service Web Apps 中的流量路由</span><span class="sxs-lookup"><span data-stu-id="07815-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="07815-109">以 hello 流量路由功能[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，您可以直接使用即時的使用者流量 tooone 或多個部分[部署位置](web-sites-staged-publishing.md)，然後分析應用程式與[Azure 應用程式Insights](/services/application-insights/)或[Azure HDInsight](/services/hdinsight/)，或是協力廠商工具，像是[New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate 您的變更。</span><span class="sxs-lookup"><span data-stu-id="07815-109">With hello Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic tooone or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate your change.</span></span> <span data-ttu-id="07815-110">例如，您可以實作下列案例與應用程式服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="07815-110">For example, you can implement hello following scenarios with App Service:</span></span>

* <span data-ttu-id="07815-111">探索功能的 bug，或找出效能瓶頸的更新先前 toosite 全部署</span><span class="sxs-lookup"><span data-stu-id="07815-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior toosite-wide deployment</span></span>
* <span data-ttu-id="07815-112">藉由測量可用性度量 hello beta 應用程式上的執行"受到控制的測試班機 」 您的變更</span><span class="sxs-lookup"><span data-stu-id="07815-112">Perform "controlled test flights" of your changes by measuring usability metrics on hello beta app</span></span>
* <span data-ttu-id="07815-113">逐漸增加 tooa 新的更新，並依正常程序向 toohello 目前版本，如果發生錯誤</span><span class="sxs-lookup"><span data-stu-id="07815-113">Gradually ramp up tooa new update, and gracefully back down toohello current version if an error occurs</span></span> 
* <span data-ttu-id="07815-114">在多個部署位置中執行 [A/B 測試](https://en.wikipedia.org/wiki/A/B_testing)或[多變量測試](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing)，以最佳化應用程式的商務成果</span><span class="sxs-lookup"><span data-stu-id="07815-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="07815-115">在 Web Apps 中使用流量路由的需求</span><span class="sxs-lookup"><span data-stu-id="07815-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="07815-116">您的 Web 應用程式必須在**標準**或**進階**層執行，因為多個部署位置有此需求。</span><span class="sxs-lookup"><span data-stu-id="07815-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="07815-117">在訂單 toowork 流量路由需要正常運作，cookie toobe hello 使用者的瀏覽器中啟用。</span><span class="sxs-lookup"><span data-stu-id="07815-117">In order toowork properly, Traffic Routing requires cookies toobe enabled in hello users' browser.</span></span> <span data-ttu-id="07815-118">流量路由會使用 hello 生命 hello 用戶端工作階段 cookie toopin 用戶端瀏覽器 tooa 部署位置。</span><span class="sxs-lookup"><span data-stu-id="07815-118">Traffic Routing uses cookies toopin a client browser tooa deployment slot for hello life hello client session.</span></span>
* <span data-ttu-id="07815-119">流量路由可透過 Azure PowerShell Cmdlet 支援進階的TiP 案例。</span><span class="sxs-lookup"><span data-stu-id="07815-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-tooa-deployment-slot"></a><span data-ttu-id="07815-120">路由流量區段 tooa 部署位置</span><span class="sxs-lookup"><span data-stu-id="07815-120">Route traffic segment tooa deployment slot</span></span>
<span data-ttu-id="07815-121">在 hello 基本層級中每個提示的情況，您要路由即時流量 tooa 非生產環境部署您的位置預先定義的百分比的表示。</span><span class="sxs-lookup"><span data-stu-id="07815-121">At hello basic level in every TiP scenario, you route a predefined percentage of your live traffic tooa non-production deployment slot.</span></span> <span data-ttu-id="07815-122">toodo，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="07815-122">toodo this, follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="07815-123">hello 以下步驟假設您已經具備[非生產環境部署位置](web-sites-staged-publishing.md)和該 hello 所需的 web 應用程式內容已經是[部署](web-sites-deploy.md)tooit。</span><span class="sxs-lookup"><span data-stu-id="07815-123">hello steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that hello desired web app content is already [deployed](web-sites-deploy.md) tooit.</span></span>
> 
> 

1. <span data-ttu-id="07815-124">登入 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="07815-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="07815-125">在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [流量路由]。</span><span class="sxs-lookup"><span data-stu-id="07815-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="07815-126">您想 tooroute 流量 tooand hello 百分比 hello 總流量您想要然後按一下 選取 hello 插槽**儲存**。</span><span class="sxs-lookup"><span data-stu-id="07815-126">Select hello slot that you want tooroute traffic tooand hello percentage of hello total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="07815-127">移 toohello 部署位置的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07815-127">Go toohello deployment slot's blade.</span></span> <span data-ttu-id="07815-128">您現在應該會看到被路由的 tooit 的即時流量。</span><span class="sxs-lookup"><span data-stu-id="07815-128">You should now see live traffic being routed tooit.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="07815-129">流量路由設定之後，hello 指定百分比的用戶端會隨機路由的 tooyour 非生產環境位置。</span><span class="sxs-lookup"><span data-stu-id="07815-129">Once Traffic Routing is configured, hello specified percentage of clients will be randomly routed tooyour non-production slot.</span></span> <span data-ttu-id="07815-130">不過，它是重要 toonote 一旦用戶端會自動路由的 tooa 特定位置，它會是 「 固定 」 toothat hello 該用戶端工作階段的存留期間的位置。</span><span class="sxs-lookup"><span data-stu-id="07815-130">However, it is important toonote that once a client is automatically routed tooa specific slot, it will be "pinned" toothat slot for hello life of that client session.</span></span> <span data-ttu-id="07815-131">完成上述使用 cookie toopin hello 使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="07815-131">This done using a cookie toopin hello user session.</span></span> <span data-ttu-id="07815-132">如果您檢查 hello HTTP 要求時，您會發現`TipMix`中每個後續要求的 cookie。</span><span class="sxs-lookup"><span data-stu-id="07815-132">If you inspect hello HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a><span data-ttu-id="07815-133">強制用戶端要求 tooa 特定位置</span><span class="sxs-lookup"><span data-stu-id="07815-133">Force client requests tooa specific slot</span></span>
<span data-ttu-id="07815-134">加法 tooautomatic 流量路由傳送中，應用程式服務會是能 tooroute 要求 tooa 特定位置。</span><span class="sxs-lookup"><span data-stu-id="07815-134">In addition tooautomatic traffic routing, App Service is able tooroute requests tooa specific slot.</span></span> <span data-ttu-id="07815-135">當您想您使用者 toobe 無法 tooopt 時這非常有用-成或退出集 beta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07815-135">This is useful when you want your users toobe able tooopt-into or opt-out of your beta app.</span></span> <span data-ttu-id="07815-136">toodo，使用 hello`x-ms-routing-name`查詢參數。</span><span class="sxs-lookup"><span data-stu-id="07815-136">toodo this, you use hello `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="07815-137">tooreroute 使用者 tooa 特定位置使用`x-ms-routing-name`，您必須確定該 hello 位置已新增 toohello 流量路由清單。</span><span class="sxs-lookup"><span data-stu-id="07815-137">tooreroute users tooa specific slot using `x-ms-routing-name`, you must make sure that hello slot is already added toohello Traffic Routing list.</span></span> <span data-ttu-id="07815-138">因為要明確 tooroute tooa 位置，並不重要 hello 實際路由您設定的百分比。</span><span class="sxs-lookup"><span data-stu-id="07815-138">Since you want tooroute tooa slot explicitly, hello actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="07815-139">如果您想，您就可以建立 「 beta 連結 」 的使用者可以按一下 tooaccess hello beta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07815-139">If you want, you can craft a "beta link" that users can click tooaccess hello beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="07815-140">讓使用者選擇退出 beta 應用程式</span><span class="sxs-lookup"><span data-stu-id="07815-140">Opt users out of beta app</span></span>
<span data-ttu-id="07815-141">toolet 使用者退出 beta 應用程式，例如，您可以將此連結放在網頁中：</span><span class="sxs-lookup"><span data-stu-id="07815-141">toolet users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

<span data-ttu-id="07815-142">hello 字串`x-ms-routing-name=self`指定 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="07815-142">hello string `x-ms-routing-name=self` specifies hello production slot.</span></span> <span data-ttu-id="07815-143">一旦 hello 用戶端瀏覽器存取 hello 連結不只是它重新導向 toohello 生產位置，但每個後續的要求將會包含 hello`x-ms-routing-name=self`釘選 hello 工作階段 toohello 生產位置的 cookie。</span><span class="sxs-lookup"><span data-stu-id="07815-143">Once hello client browser access hello link, not only is it redirected toohello production slot, but every subsequent request will contain hello `x-ms-routing-name=self` cookie that pins hello session toohello production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a><span data-ttu-id="07815-144">選擇 toobeta 應用程式中的使用者</span><span class="sxs-lookup"><span data-stu-id="07815-144">Opt users in toobeta app</span></span>
<span data-ttu-id="07815-145">toolet 使用者參加 tooyour beta 應用程式、 設定 hello 相同查詢參數 toohello 名稱 hello 非生產位置，例如：</span><span class="sxs-lookup"><span data-stu-id="07815-145">toolet users opt in tooyour beta app, set hello same query parameter toohello name of hello non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="07815-146">其他資源</span><span class="sxs-lookup"><span data-stu-id="07815-146">More resources</span></span>
* [<span data-ttu-id="07815-147">針對 Azure App Service 中的 Web 應用程式設定預備環境</span><span class="sxs-lookup"><span data-stu-id="07815-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="07815-148">透過可預測方式在 Azure 中部署複雜應用程式</span><span class="sxs-lookup"><span data-stu-id="07815-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="07815-149">敏捷式軟體開發 (Agile Software Development) 與 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="07815-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="07815-150">為 Web 應用程式有效地使用 DevOps 環境</span><span class="sxs-lookup"><span data-stu-id="07815-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

