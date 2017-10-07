---
title: "aaaDiagnose 失敗和例外狀況中的 web 應用程式與 Azure Application Insights |Microsoft 文件"
description: "擷取從 ASP.NET 應用程式與所要求遙測的例外狀況。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>使用 Application Insights 在 Web 應用程式中診斷例外狀況
[Application Insights](app-insights-overview.md) 會回報您即時 Web 應用程式中的例外狀況。 您可以與交互關聯失敗的要求例外狀況和其他事件在 hello 用戶端和伺服器，如此您就可以快速地診斷出 hello 原因。

## <a name="set-up-exception-reporting"></a>設定例外狀況報告
* 從您的伺服器應用程式報告 toohave 例外狀況：
  * 在應用程式程式碼中安裝 [Application Insights SDK](app-insights-asp-net.md)，或
  * IIS Web 伺服器：執行 [Application Insights 代理程式](app-insights-monitor-performance-live-website-now.md)；或
  * Azure web 應用程式： 新增 hello [Application Insights 擴充功能](app-insights-azure-web-apps.md)
  * Java web 應用程式： 安裝 hello [Java 代理程式](app-insights-java-agent.md)
* 安裝 hello [JavaScript 程式碼片段](app-insights-javascript.md)網頁 toocatch 瀏覽器例外狀況。
* 在某些應用程式架構，或使用某些設定，您需要 tootake 某些額外的步驟 toocatch 詳細例外狀況：
  * [Web Form](#web-forms)
  * [MVC](#mvc)
  * [Web API 1.*](#web-api-1)
  * [Web API 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>使用 Visual Studio 診斷例外狀況
在 Visual Studio 偵錯的 toohelp 開啟 hello 應用程式方案。

執行 hello 應用程式，您的伺服器上或使用 F5 在開發電腦上。

在 Visual Studio 中，開啟 hello Application Insights 搜尋視窗，並將它從您的應用程式設定 toodisplay 事件。 您正在偵錯時，您可以只要按一下 hello Application Insights 按鈕。

![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 開啟。](./media/app-insights-asp-net-exceptions/34.png)

請注意，您可以篩選 hello 報表 tooshow 只是例外狀況。

*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*

按一下 [例外狀況報告 tooshow] 其堆疊追蹤。
按一下 hello 堆疊追蹤，tooopen hello 相關的程式碼檔案中的行參考。  

在 hello 程式碼，請注意，CodeLens 會顯示 hello 例外狀況的相關資料：

![CodeLens 的例外狀況通知。](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>使用 hello Azure 入口網站的診斷失敗
從您的應用程式的 hello Application Insights 概觀，hello 失敗磚會顯示例外狀況和失敗的 HTTP 要求的圖表以及 hello 的清單要求會導致 hello 最常失敗的 Url。

![選取 [設定]、[失敗]](./media/app-insights-asp-net-exceptions/012-start.png)

按一下透過其中一個 hello 失敗 hello 清單 tooget tooindividual 相符項目中的 hello 例外狀況，您可以在此查看 hello 詳細資料，堆疊追蹤的例外狀況類型：

![選取的執行個體失敗的要求，並在 例外狀況詳細資料，取得 tooinstances hello 例外狀況。](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**或者，**您可以開始從要求的 hello 清單，然後找出例外狀況相關的 tooit。

*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*


## <a name="custom-tracing-and-log-data"></a>自訂追蹤和記錄資料
tooget 診斷資料特定 tooyour 應用程式中，您可以插入程式碼 toosend 遙測資料。 這顯示在診斷搜尋、 hello 要求、 頁面檢視，以及其他自動收集資料。

您有幾種選項：

* [Trackevent （)](app-insights-api-custom-events-metrics.md#trackevent)通常用來監視使用狀況模式，但它也會傳送的資料出現在自訂事件診斷搜尋 hello。 事件具有名稱，並且可以包含字串屬性和數值度量，您可以對其[篩選診斷搜尋](app-insights-diagnostic-search.md)。
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 可讓您傳送較長的資料，例如 POST 資訊。
* [TrackException()](#exceptions) 會傳送堆疊追蹤。 [深入了解例外狀況](#exceptions)。
* 如果您已經使用 Log4Net 或 NLog 等記錄架構，您可以[擷取這些記錄](app-insights-asp-net-trace-logs.md)，然後在診斷搜尋中將它們連同要求和例外狀況資料一起檢視。

這些事件中，開啟 toosee[搜尋](app-insights-diagnostic-search.md)、 開啟篩選器，，，然後選擇 自訂事件、 追蹤或例外狀況。

![鑽研](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> 如果您的應用程式會產生大量的遙測，hello 調整取樣模組將會自動減少 hello 磁碟區所傳送的 toohello 入口網站傳送代表性數部分的事件。 屬於的 hello 相同的作業將會被選取或取消選取此選項為群組，如此您可以瀏覽之間相關事件的事件。 [了解取樣。](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Toosee 要求張貼資料的方式
要求詳細資料不包含 hello 資料傳送 POST 呼叫 tooyour 應用程式。 toohave 回報這項資料：

* [安裝 hello SDK](app-insights-asp-net.md)應用程式專案中。
* 將程式碼插入您的應用程式 toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace)。 傳送 hello 訊息參數中的 hello 張貼資料。 沒有允許 toohello 大小限制，因此您應該嘗試 toosend 只 hello 重要資料。
* 當您調查失敗的要求時，以尋找相關聯的 hello 追蹤。  

![鑽研](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> 擷取例外狀況和相關的診斷資料
首先，您將不會 hello 入口網站中看到您的應用程式會造成失敗的所有 hello 例外狀況。 您會看到瀏覽器中的任何例外狀況 (如果您使用 hello [JavaScript SDK](app-insights-javascript.md) web 網頁中)。 但大部分的伺服器例外狀況所捕捉 IIS，您有 toowrite 的位元的程式碼 toosee 它們。

您可以：

* **明確地記錄例外狀況**插入程式碼中的例外狀況處理常式 tooreport hello 例外狀況。
* **自動擷取例外狀況** ，方法是設定您的 ASP.NET 架構。 hello 必要新增項目都會有不同不同類型的架構。

## <a name="reporting-exceptions-explicitly"></a>明確報告例外狀況
hello 最簡單的方式是在例外狀況處理常式中呼叫 tooTrackException() tooinsert。

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

hello 屬性和量值的參數是選擇性的但可用於[篩選和加入](app-insights-diagnostic-search.md)額外的資訊。 比方說，如果您有可以執行數個遊戲的應用程式，您無法找到所有 hello 例外狀況報告相關的 tooa 特定遊戲。 您可以像 tooeach 字典，做為您加入數目的項目。

## <a name="browser-exceptions"></a>瀏覽器例外狀況
大部分的瀏覽器例外狀況都會報告。

如果您的網頁包含指令碼檔案的內容傳遞網路或其他網域，請確定指令碼標記具有 hello 屬性```crossorigin="anonymous"```，並將該 hello 伺服器傳送[CORS 標頭](http://enable-cors.org/)。 這可讓您 tooget 堆疊追蹤和從這些資源的未處理 JavaScript 例外狀況的詳細資料。

## <a name="web-forms"></a>Web Form
Web form 設有 CustomErrors 沒有重新導向時 hello HTTP 模組時，將會無法 toocollect hello 例外狀況。

但是如果您有使用中的重新導向，加入下列行 toohello Application_Error 函式中 Global.asax.cs hello。 (如果您還沒有檔案，請加入 Global.asax 檔案。)

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
如果 hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx)設定`Off`，則例外狀況將可供 hello [HTTP 模組](https://msdn.microsoft.com/library/ms178468.aspx)toocollect。 不過，如果它是`RemoteOnly`（預設值） 或`On`，然後將清除 hello 例外狀況並不適用於 Application Insights tooautomatically 收集。 您可以藉由覆寫 hello 修正[System.Web.Mvc.HandleErrorAttribute 類別](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)，並套用覆寫的 hello 類別，如所示為 hello 不同 MVC 以下的版本 ([github 來源](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Hello HandleError 屬性取代為您新的屬性，在您的控制站。

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[範例](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
註冊 `AiHandleErrorAttribute` 做為 Global.asax.cs 中的全域篩選器：

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[範例](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4、MVC5
註冊 AiHandleErrorAttribute 做為 FilterConfig.cs 中的全域篩選器：

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[範例](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
覆寫 System.Web.Http.Filters.ExceptionFilterAttribute：

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

您無法加入此覆寫的屬性 toospecific 控制站，或將它 toohello 全域篩選器設定 hello 到 WebApiConfig 類別中：

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[範例](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

有無法處理 hello 例外狀況篩選條件的案例數目。 例如：

* 從控制器建構函式擲回的例外狀況。
* 從訊息處理常式擲回的例外狀況。
* 在路由期間擲回的例外狀況。
* 在回應內容序列化期間擲回的例外狀況。

## <a name="web-api-2x"></a>Web API 2.x
新增 IExceptionLogger 的實作：

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

視情況中新增此 toohello 服務：

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[範例](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

做為替代方案，您可以：

1. 取代 hello 只 ExceptionHandler 利用 IExceptionHandler 的自訂實作。 這只稱為 hello 架構時仍能 toochoose 的回應訊息 toosend （不是在 hello 連接已中止執行個體）
2. 例外狀況篩選條件 （如中所述在上述的 Web API 1.x 控制站上的 hello > 一節）-不會在所有情況下呼叫。

## <a name="wcf"></a>WCF
新增類別，該類別會擴充屬性和實作 IErrorHandler 和 IServiceBehavior。

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

加入 hello 屬性 toohello 服務實作：

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[範例](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>例外狀況效能計數器
如果您有[安裝 Application Insights 的代理程式 hello](app-insights-monitor-performance-live-website-now.md)您在伺服器上，您可以取得 hello 例外狀況率，.NET 所測量的圖表。 這包括已處理和未處理的 .NET 例外狀況。

開啟 [計量瀏覽器] 刀鋒視窗、加入新圖表，然後選取 [效能計數器] 下方所列的 [例外狀況比率] 。

hello.NET framework 來計算 hello 速率的間隔中計算的例外狀況的 hello 數，然後除以 hello hello 間隔長度。

請注意，它將會不同於 hello '例外狀況' hello Application Insights 入口網站的計算方式是計算 TrackException 報告的計數。 hello 取樣間隔不同，而且 hello SDK 不會將傳送 TrackException 報告所有處理和未處理的例外狀況。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>後續步驟
* [監視 REST、 SQL 及其他呼叫 toodependencies](app-insights-asp-net-dependencies.md)
* [監視頁面載入時間、瀏覽器例外狀況及 AJAX 呼叫](app-insights-javascript.md)
* [監視效能計數器](app-insights-performance-counters.md)
