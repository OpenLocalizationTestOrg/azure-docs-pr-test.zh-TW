---
title: "傳送使用者內容以啟用 Azure Application Insights 中的使用體驗 | Microsoft Docs"
description: "為每個使用者指派 Application Insights 中唯一的持續性識別碼字串之後，追蹤使用者如何透過您的服務移動。"
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 9350029c775643be0dcc679b0f4bb9238b5f8aca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
#  <a name="sending-user-context-to-enable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="71db0-103">傳送使用者內容以啟用 Azure Application Insights 中的使用體驗</span><span class="sxs-lookup"><span data-stu-id="71db0-103">Sending user context to enable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="71db0-104">追蹤使用者</span><span class="sxs-lookup"><span data-stu-id="71db0-104">Tracking users</span></span>

<span data-ttu-id="71db0-105">Application Insights 可讓您透過一組產品使用量工具來監控並追蹤使用者：</span><span class="sxs-lookup"><span data-stu-id="71db0-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="71db0-106">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="71db0-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="71db0-107">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="71db0-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="71db0-108">保留</span><span class="sxs-lookup"><span data-stu-id="71db0-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="71db0-109">同群使用者</span><span class="sxs-lookup"><span data-stu-id="71db0-109">Cohorts</span></span>
* [<span data-ttu-id="71db0-110">活頁簿</span><span class="sxs-lookup"><span data-stu-id="71db0-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="71db0-111">若要追蹤使用者在一段時間內所做的行為，Application Insights 需要每個使用者或工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="71db0-112">包括每個自訂事件或頁面檢視中的識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="71db0-113">使用者、漏斗圖、保留期和同群使用者：包含使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="71db0-114">工作階段：包含工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="71db0-115">如果您的應用程式與 [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page) 整合，則會自動追蹤使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="71db0-116">選擇使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="71db0-116">Choosing user IDs</span></span>

<span data-ttu-id="71db0-117">使用者識別碼應該在使用者工作階段期間持續存在，以追蹤使用者在一段時間內的行為。</span><span class="sxs-lookup"><span data-stu-id="71db0-117">User IDs should persist across user sessions to track how users behave over time.</span></span> <span data-ttu-id="71db0-118">有多種方法可持續使用識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-118">There are various approaches for persisting the ID.</span></span>
- <span data-ttu-id="71db0-119">您的服務中已有使用者定義。</span><span class="sxs-lookup"><span data-stu-id="71db0-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="71db0-120">如果服務可存取瀏覽器，該服務可利用識別碼將 cookie 傳遞給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="71db0-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span></span> <span data-ttu-id="71db0-121">只要 cookie 保留在使用者的瀏覽器中，識別碼就會持續存在。</span><span class="sxs-lookup"><span data-stu-id="71db0-121">The ID will persist for as long as the cookie remains in the user's browser.</span></span>
- <span data-ttu-id="71db0-122">如有必要，您可以每個工作階段都使用新的識別碼，但與使用者相關的結果會受到限制。</span><span class="sxs-lookup"><span data-stu-id="71db0-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span></span> <span data-ttu-id="71db0-123">例如，您將無法看到使用者的行為如何隨著時間而變化。</span><span class="sxs-lookup"><span data-stu-id="71db0-123">For example, you won't be able to see how a user's behavior changes over time.</span></span>

<span data-ttu-id="71db0-124">識別碼應該是 Guid 或足夠複雜的另一個字串，以專門識別每個使用者。</span><span class="sxs-lookup"><span data-stu-id="71db0-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span></span> <span data-ttu-id="71db0-125">例如，它可能是一個長的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="71db0-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="71db0-126">如果識別碼包含使用者的個人識別資訊，則該值不適合傳送至 Application Insights 做為使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span></span> <span data-ttu-id="71db0-127">您可以傳送此類識別碼做為[已驗證的使用者識別碼](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users)，但不符合使用案例的使用者識別碼需求。</span><span class="sxs-lookup"><span data-stu-id="71db0-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="71db0-128">ASP.NET 應用程式：在 ITelemetryInitializer 中設定使用者內容</span><span class="sxs-lookup"><span data-stu-id="71db0-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="71db0-129">建立遙測初始設定式 (依照[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)的詳細說明)，並設定 Context.User.Id 和 Context.Session.Id。</span><span class="sxs-lookup"><span data-stu-id="71db0-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span></span>

<span data-ttu-id="71db0-130">此範例會將使用者識別碼設定為在工作階段之後到期的識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-130">This example sets the user ID to an identifier that expires after the session.</span></span> <span data-ttu-id="71db0-131">如果可能，請使用工作階段期間持續存在的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="71db0-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="71db0-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="71db0-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets the user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on the HttpContext Session.
            // Set the user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set the user id on the Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set the session id on the Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="71db0-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71db0-133">Next steps</span></span>
- <span data-ttu-id="71db0-134">若要啟用使用體驗，請開始傳送「自訂事件」[](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或「頁面檢視」[](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="71db0-134">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="71db0-135">如果您已傳送自訂事件或頁面檢視，請探索「使用量工具」，以了解使用者如何使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="71db0-135">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    * [<span data-ttu-id="71db0-136">使用量概觀</span><span class="sxs-lookup"><span data-stu-id="71db0-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="71db0-137">使用者、工作階段和事件</span><span class="sxs-lookup"><span data-stu-id="71db0-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="71db0-138">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="71db0-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="71db0-139">保留</span><span class="sxs-lookup"><span data-stu-id="71db0-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="71db0-140">活頁簿</span><span class="sxs-lookup"><span data-stu-id="71db0-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
