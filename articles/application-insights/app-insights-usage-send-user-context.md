---
title: "aaaSending 使用者內容 tooenable 使用量體驗 Azure Application Insights |Microsoft 文件"
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
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="ded07-103">傳送的使用者內容 tooenable 使用量體驗 Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="ded07-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="ded07-104">追蹤使用者</span><span class="sxs-lookup"><span data-stu-id="ded07-104">Tracking users</span></span>

<span data-ttu-id="ded07-105">Application Insights 可讓您 toomonitor 並追蹤您透過一組產品使用工具的使用者：</span><span class="sxs-lookup"><span data-stu-id="ded07-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="ded07-106">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="ded07-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="ded07-107">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="ded07-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="ded07-108">保留</span><span class="sxs-lookup"><span data-stu-id="ded07-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="ded07-109">同群使用者</span><span class="sxs-lookup"><span data-stu-id="ded07-109">Cohorts</span></span>
* [<span data-ttu-id="ded07-110">活頁簿</span><span class="sxs-lookup"><span data-stu-id="ded07-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="ded07-111">順序 tootrack 哪些使用者執行一段時間，在 Application Insights 需要每個使用者或工作階段的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="ded07-112">包括每個自訂事件或頁面檢視中的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="ded07-113">使用者、漏斗圖、保留期和同群使用者：包含使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="ded07-114">工作階段：包含工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="ded07-115">如果您的應用程式整合在一起以 hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page)，使用者會自動追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="ded07-116">選擇使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="ded07-116">Choosing user IDs</span></span>

<span data-ttu-id="ded07-117">使用者識別碼應保存跨使用者工作階段 tootrack 使用者一段時間的行為方式。</span><span class="sxs-lookup"><span data-stu-id="ded07-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="ded07-118">有各種方法保存 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="ded07-119">您的服務中已有使用者定義。</span><span class="sxs-lookup"><span data-stu-id="ded07-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="ded07-120">如果 hello 服務存取 tooa 瀏覽器，它可以傳入 hello 瀏覽器的 cookie 識別碼它。</span><span class="sxs-lookup"><span data-stu-id="ded07-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="ded07-121">hello 識別碼將會保存的只要 hello cookie 維持 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ded07-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="ded07-122">如有必要，您可以使用新的識別碼。 每個工作階段，但與使用者相關的 hello 結果會受到限制。</span><span class="sxs-lookup"><span data-stu-id="ded07-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="ded07-123">例如，您必須能夠 toosee 如何隨著時間變更使用者的行為。</span><span class="sxs-lookup"><span data-stu-id="ded07-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="ded07-124">hello 識別碼應為 Guid 或另一個字串不夠複雜而 tooidentify 每位使用者唯一。</span><span class="sxs-lookup"><span data-stu-id="ded07-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="ded07-125">例如，它可能是一個長的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="ded07-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="ded07-126">如果 hello 識別碼包含 hello 使用者的個人識別資訊，它不是適當的值 toosend tooApplication Insights 為使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="ded07-127">您可以傳送這類識別碼，表示為[驗證使用者識別碼](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users)，但不滿足使用案例的 hello 使用者識別碼的需求。</span><span class="sxs-lookup"><span data-stu-id="ded07-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="ded07-128">ASP.NET 應用程式：在 ITelemetryInitializer 中設定使用者內容</span><span class="sxs-lookup"><span data-stu-id="ded07-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="ded07-129">在詳細資料中所述，建立遙測的初始設定式、[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)，和 hello Context.User.Id 和 hello Context.Session.Id 組。</span><span class="sxs-lookup"><span data-stu-id="ded07-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="ded07-130">此範例會設定 hello 使用者識別碼 tooan 識別碼 hello 工作階段之後過期。</span><span class="sxs-lookup"><span data-stu-id="ded07-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="ded07-131">如果可能，請使用工作階段期間持續存在的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="ded07-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="ded07-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="ded07-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="ded07-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ded07-133">Next steps</span></span>
- <span data-ttu-id="ded07-134">tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="ded07-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="ded07-135">如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="ded07-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="ded07-136">使用量概觀</span><span class="sxs-lookup"><span data-stu-id="ded07-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="ded07-137">使用者、工作階段和事件</span><span class="sxs-lookup"><span data-stu-id="ded07-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="ded07-138">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="ded07-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="ded07-139">保留</span><span class="sxs-lookup"><span data-stu-id="ded07-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="ded07-140">活頁簿</span><span class="sxs-lookup"><span data-stu-id="ded07-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
