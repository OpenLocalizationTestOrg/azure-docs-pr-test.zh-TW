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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>傳送的使用者內容 tooenable 使用量體驗 Azure Application Insights

## <a name="tracking-users"></a>追蹤使用者

Application Insights 可讓您 toomonitor 並追蹤您透過一組產品使用工具的使用者： 
* [使用者、工作階段、事件](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [漏斗圖](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [保留](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* 同群使用者
* [活頁簿](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

順序 tootrack 哪些使用者執行一段時間，在 Application Insights 需要每個使用者或工作階段的識別碼。 包括每個自訂事件或頁面檢視中的識別碼。
- 使用者、漏斗圖、保留期和同群使用者：包含使用者識別碼。
- 工作階段：包含工作階段識別碼。

如果您的應用程式整合在一起以 hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page)，使用者會自動追蹤識別碼。

## <a name="choosing-user-ids"></a>選擇使用者識別碼

使用者識別碼應保存跨使用者工作階段 tootrack 使用者一段時間的行為方式。 有各種方法保存 hello 識別碼。
- 您的服務中已有使用者定義。
- 如果 hello 服務存取 tooa 瀏覽器，它可以傳入 hello 瀏覽器的 cookie 識別碼它。 hello 識別碼將會保存的只要 hello cookie 維持 hello 使用者的瀏覽器。
- 如有必要，您可以使用新的識別碼。 每個工作階段，但與使用者相關的 hello 結果會受到限制。 例如，您必須能夠 toosee 如何隨著時間變更使用者的行為。

hello 識別碼應為 Guid 或另一個字串不夠複雜而 tooidentify 每位使用者唯一。 例如，它可能是一個長的隨機數字。

如果 hello 識別碼包含 hello 使用者的個人識別資訊，它不是適當的值 toosend tooApplication Insights 為使用者識別碼。 您可以傳送這類識別碼，表示為[驗證使用者識別碼](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users)，但不滿足使用案例的 hello 使用者識別碼的需求。

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>ASP.NET 應用程式：在 ITelemetryInitializer 中設定使用者內容

在詳細資料中所述，建立遙測的初始設定式、[這裡](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)，和 hello Context.User.Id 和 hello Context.Session.Id 組。

此範例會設定 hello 使用者識別碼 tooan 識別碼 hello 工作階段之後過期。 如果可能，請使用工作階段期間持續存在的使用者識別碼。

*C#*

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

## <a name="next-steps"></a>後續步驟
- tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。
- 如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。
    * [使用量概觀](app-insights-usage-overview.md)
    * [使用者、工作階段和事件](app-insights-usage-segmentation.md)
    * [漏斗圖](usage-funnels.md)
    * [保留](app-insights-usage-retention.md)
    * [活頁簿](app-insights-usage-workbooks.md)
