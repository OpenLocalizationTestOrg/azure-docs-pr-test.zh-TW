---
title: "aaaApplication Azure 雲端服務的深入資訊 |Microsoft 文件"
description: "使用 Application Insights 有效地監視您的 Web 和背景工作角色"
services: application-insights
documentationcenter: 
keywords: "WAD2AI, Azure 診斷"
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Azure 雲端服務的 Application Insights
您可以透過 [Application Insights][start] 來監視 [Microsoft Azure 雲端服務應用程式](https://azure.microsoft.com/services/cloud-services/)，它會結合 Application Insights SDK 的資料與雲端服務的 [Azure 診斷](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics)資料，來讓您了解應用程式的可用性、效能、失敗和使用情形。 Hello 您善加 hello 效能和效率 hello 中的應用程式的相關意見反應，可以讓謹慎的選擇 hello 方向 hello 設計的每個開發週期中。

![範例](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>開始之前
您需要：

* [Microsoft Azure](http://azure.com) 的訂用帳戶。 使用 Microsoft 帳戶登入，可能是針對 Windows、XBox Live 或其他 Microsoft 雲端服務具備的帳戶。 
* Microsoft Azure 工具 2.9 或更新版本
* 開發人員分析工具 7.10 或更新版本

## <a name="quick-start"></a>快速入門
hello 與 Application Insights 雲端服務是當您發行服務 tooAzure 時的 toochoose 最快速且輕鬆的方式 toomonitor。

![範例](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

此選項儀器，您的應用程式在執行階段，讓您所有的 hello 遙測 toomonitor 要求、 例外狀況，以及您的 web 角色，以及效能中的相依性，您需要從背景工作角色的計數器。 任何應用程式所產生的診斷追蹤也會傳送 tooApplication 深入資訊。

如果這就是您所需的一切，您就已大功告成！ 接下來的步驟包括[檢視來自您應用程式的度量](app-insights-metrics-explorer.md)、[利用分析查詢您的資料](app-insights-analytics.md)，還可能包括設定[儀表板](app-insights-dashboards.md)。 您可能會想 tooset[可用性測試](app-insights-monitor-web-app-availability.md)和[加入程式碼 tooyour 網頁](app-insights-javascript.md)toomonitor hello 瀏覽器中的效能。

但是您也可以取得更多選項：

* 從不同元件傳送資料和組建組態 tooseparate 資源。
* 新增來自您應用程式的自訂遙測。

如果這些選項屬於感興趣 tooyou，閱讀。

## <a name="sample-application-instrumented-with-application-insights"></a>使用 Application Insights 檢測的範例應用程式
看看這[範例應用程式](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService)Application Insights 加入時所在 tooa 雲端服務與 Azure 中裝載兩個背景工作角色。 

以下會告訴您如何 tooadapt 雲端服務專案中 hello 相同的方式。

## <a name="plan-resources-and-resource-groups"></a>規劃資源和資源群組
從您的應用程式的 hello 遙測是儲存、 分析並顯示在類型 Application Insights 的 Azure 資源。 

每個資源所屬 tooa 資源群組。 資源群組用來管理成本，授與存取 tooteam 成員和 toodeploy 更新單一協調交易。 例如，您可以[撰寫指令碼 toodeploy](../azure-resource-manager/resource-group-template-deploy.md) Azure 雲端服務和其的 Application Insights 監視在一個作業之內的資源。

### <a name="resources-for-components"></a>元件的資源
hello 建議配置是 toocreate 不同的資源，您的應用程式-也就是每個 web 角色和背景工作角色的每個元件。 您可以分別分析每個元件，但是可以建立[儀表板](app-insights-dashboards.md)，結合 hello 重要圖表來自所有 hello 元件，以便您可以比較，並監視在一起。 

替代的配置會從多個角色 toohello toosend hello 遙測相同的資源，但[加入維度屬性 tooeach 遙測項目](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)識別其來源的角色。 在此配置中，度量的圖表，例如例外狀況通常顯示 hello 中的 hello 計數的彙總不同的角色，但是您可以依 hello 角色識別項時所需分割 hello 圖表。 Hello 也可以篩選搜尋相同的維度。 這個替代方案可便於 tooview 在 hello 相同的時間，但也可能導致 toosome 混淆 hello 角色之間的所有項目。

瀏覽器遙測通常包含在 hello 做為其伺服器端 web 角色有相同的資源。

將 hello 不同元件的 hello Application Insights 資源放在一個資源群組。 這可讓您輕鬆 toomanage 一起。 

### <a name="separating-development-test-and-production"></a>區分開發、測試及生產環境
如果您正在開發的自訂事件您下一步 功能，即時 hello 舊版本時，您會想 toosend hello 開發遙測 tooa 個別 Application Insights 資源。 否則它會需要硬 toofind 您測試的遙測之間所有 hello hello 即時網站的流量。

tooavoid 這種情況下，建立個別針對每個組建組態或 「 戳記 」 （開發、 測試、 生產環境中，...） 的系統資源。 將每個組建組態的 hello 資源放在不同的資源群組。 

toosend hello 遙測 toohello 適當資源，您可以設定 hello Application Insights SDK，讓它挑選不同的檢測金鑰視 hello 組建組態而定。 

## <a name="create-an-application-insights-resource-for-each-role"></a>為每個角色建立 Application Insights 資源
如果您已經決定 toocreate 個別針對每個角色的資源，而且可能是個別設定每個組建組態-則是最簡單的 toocreate hello Application Insights 入口網站中的所有。 (如果您經常建立資源，您可以[hello 程序自動化](app-insights-powershell.md)。

1. 在 hello [Azure 入口網站][portal]，建立新的 Application Insights 資源。 針對應用程式類型，選擇 ASP.NET 應用程式。 

    ![按一下 新增，然後按一下Application Insights](./media/app-insights-cloudservices/01-new.png)
2. 請注意，每個資源都是以「檢測金鑰」作為識別。 您可能需要此稍後如果您想 toomanually 設定或確認 hello SDK hello 組態。

    ![按一下 內容選取 hello 金鑰，請按 ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>設定每個角色的 Azure 診斷
設定此選項 toomonitor 使用 Application Insights 的應用程式。 針對 Web 角色，這除了提供使用情況分析之外，也提供效能監視、警示及診斷。 對於其他角色，您可以搜尋和監視 Azure 診斷，例如重新啟動、 效能計數器，以及呼叫 tooSystem.Diagnostics.Trace。 

1. 在 Visual Studio 方案總管 中，在&lt;YourCloudService&gt;，角色，開啟每個角色的 hello 屬性。
2. 在**組態**，將**傳送診斷資料 tooApplication Insights**和選取 hello 適當您稍早建立的 Application Insights 資源。

如果您已決定 toouse 個別的 Application Insights 資源，每個組建組態，請先選取 hello 組態。

![在 hello 內容的每個 Azure 角色設定 Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

這是插入名為 hello 檔案中的 Application Insights 檢測金鑰的 hello 效果`ServiceConfiguration.*.cscfg`。 ([範例程式碼](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg))。

如果您想傳送的診斷資訊 tooApplication Insights toovary hello 層級，則您可以這樣[藉由編輯 hello`.cscfg`直接檔案](app-insights-azure-diagnostics.md)。

## <a name="sdk"></a>安裝每個專案中的 hello SDK
此選項會增加 hello 能力 tooadd 自訂商務遙測 tooany 角色，您的應用程式如何使用和執行進一步分析。

在 Visual Studio 中，設定每個雲端應用程式專案的 hello Application Insights SDK。

1. **Web 角色**: hello 專案上按一下滑鼠右鍵，然後選擇 **設定 Application Insights**或**新增 > Application Insights 遙測**。

2. **背景工作角色**： 
 * Hello 專案上按一下滑鼠右鍵，然後選取**管理 Nuget 封裝**。
 * 新增[適用於 Windows 伺服器的 Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)。

    ![搜尋「Application Insights」](./media/app-insights-cloudservices/04-ai-nuget.png)

3. 設定 hello SDK toosend 資料 toohello Application Insights 資源。

    在適當的啟動函數中，設定 hello 組態設定從 hello 檢測金鑰 hello.cscfg 檔案中：
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    對於應用程式中的每個角色執行這項操作。 請參閱 hello 範例：
   
   * [Web 角色](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [背景工作角色](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [針對網頁](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. 設定 hello ApplicationInsights.config 檔案 toobe 一律複製 toohello 輸出目錄。 
   
    （在 hello.config 檔案中，您會看到訊息詢問您 tooplace hello 檢測金鑰那里。 不過，為雲端應用程式是較佳的 tooset 從 hello.cscfg 檔案。 這可確保該 hello 角色正確識別 hello 入口網站中。）

#### <a name="run-and-publish-hello-app"></a>執行及發行 hello 應用程式
執行應用程式，並且登入 Azure。 您建立開啟 hello Application Insights 資源，而且您會看到中出現的個別資料點[搜尋](app-insights-diagnostic-search.md)，並彙總中的資料[度量總管](app-insights-metrics-explorer.md)。 

加入多個遙測-請參閱下列的-hello 章節，然後發行您的應用程式 tooget 即時診斷和使用方式的意見反應。 

#### <a name="no-data"></a>沒有資料？
* 開啟 hello[搜尋][ diagnostic]磚，toosee 個別事件。
* 使用 hello 應用程式，使其產生某些遙測開啟不同的頁面。
* 請稍等片刻，然後按一下 [重新整理]。
* 請參閱[疑難排解][qna]。

## <a name="view-azure-diagnostic-events"></a>檢視 Azure 診斷事件
其中 toofind hello [Azure 診斷](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics)Application Insights 中的資訊：

* 效能計數器顯示為自訂度量。 
* Windows 事件記錄檔顯示為追蹤和自訂事件。
* 應用程式記錄檔、ETW 記錄檔和任何診斷基礎結構記錄檔顯示為追蹤。

toosee 效能計數器和事件，計數開啟[計量瀏覽器](app-insights-metrics-explorer.md)並加入新的圖表：

![Azure 診斷資料](./media/app-insights-cloudservices/23-wad.png)

使用[搜尋](app-insights-diagnostic-search.md)或[分析查詢](app-insights-analytics-tour.md)toosearch 跨各種追蹤記錄檔傳送 Azure 診斷的 hello。 例如，假設您有未處理的例外狀況而導致角色 toocrash 和回收。 這項資訊就會出現在 hello 應用程式通道的 Windows 事件記錄檔。 您可以使用搜尋 toolook 在 hello Windows 事件記錄檔錯誤，並取得 hello 例外狀況的 hello 完整的堆疊追蹤。 幫助您找出 hello hello 問題根本原因。

![Azure 診斷搜尋](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>更多遙測
hello 各節顯示如何從您的應用程式的不同層面的 tooget 其他遙測。

## <a name="track-requests-from-worker-roles"></a>從背景工作角色追蹤要求
在 web 角色 hello 要求模組會自動收集有關 HTTP 要求的資料。 請參閱 hello[範例 MVCWebRole](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)如需如何覆寫 hello 預設集合行為的範例。 

您可以擷取呼叫 tooworker 角色 hello 效能追蹤它們在 hello 與 HTTP 要求相同的方式。 在 Application Insights hello 要求遙測類型會測量具名的伺服器端工作可以逾時，並可獨立成功或失敗的單位。 雖然 hello SDK，即可自動擷取 HTTP 要求，您可以插入您自己的程式碼 tootrack 要求 tooworker 角色。

請參閱 hello 兩個範例背景工作角色檢測的 tooreport 要求： [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA)和[WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>例外狀況
如需如何從不同的 Web 應用程式類型收集未處理的例外狀況的資訊，請參閱 [在 Application Insights 中監視例外狀況](app-insights-asp-net-exceptions.md) 。

hello 範例 web 角色有 MVC5 及 Web API 2 控制器。 hello 從 hello 兩個未處理的例外狀況會擷取以 hello 下列處理常式：

* 針對 MVC5 控制器，[這裡](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12)設定的 [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs)
* 針對 Web API 2 控制器，[這裡](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25)設定的 [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs)

背景工作角色有兩種方式 tootrack 例外狀況：

* TrackException(ex)
* 如果您已經加入 hello Application Insights 追蹤接聽程式 NuGet 封裝，您可以使用**System.Diagnostics.Trace** toolog 例外狀況。 [程式碼範例。](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>效能計數器
預設會收集 hello 下列計數器：

    * \Process(??APP_WIN32_PROC??)\%Processor Time
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

若是 Web 角色，也會收集這些計數器︰

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

您可以藉由編輯 ApplicationInsights.config 來指定額外的自訂或其他 Windows 效能計數器，[如此範例所示](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14)。

  ![效能計數器](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>背景工作角色的相互關聯遙測
它時，較豐富的診斷經驗，您可以看到哪些 led 的 tooa 失敗或高度延遲的要求。 Web 角色與 hello SDK 會自動設定之間的相互關聯相關的遙測。 背景工作角色，您可以使用自訂的遙測初始設定式 tooset 常見 Operation.Id 內容屬性的所有 hello 遙測 tooachieve 這。 這可讓您 toosee 是否 hello 延遲/失敗問題所造成到期 tooa 相依性或您的程式碼，看 ！ 

方式如下：

* 設定成 CallContext hello 相互關聯識別碼所示[這裡](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36)。 在此情況下，我們使用 hello 要求識別碼為 hello 相互關聯識別碼
* 加入自訂 TelemetryInitializer 實作，tooset hello Operation.Id toohello correlationId 設為以上。 範例如下：[ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* 新增 hello 自訂遙測初始設定式。 您可以執行在 hello ApplicationInsights.config 檔案中，或在程式碼所示[這裡](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

就這麼簡單！ hello 入口網站體驗是已固定 toohelp 看一眼所有相關聯的遙測：

![相互關聯的遙測](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>用戶端遙測
[新增 hello JavaScript SDK tooyour 網頁][ client]例如頁面檢視計數、 頁面載入時間、 指令碼的例外狀況，以及您頁面指令碼中撰寫自訂遙測 toolet tooget 瀏覽器型遙測。

## <a name="availability-tests"></a>可用性集合
[設定 web 測試][ availability] toomake 即時且回應迅速，保持您的應用程式。

## <a name="display-everything-together"></a>將所有內容一起顯示
tooget 系統的整體概況，您可以整合 hello 金鑰一起監控圖表，其中一個上[儀表板](app-insights-dashboards.md)。 例如，您無法釘選 hello 要求與失敗計數每個角色。 

如果您的系統使用其他 Azure 服務 (例如「串流分析」)，請將它們的監視圖表一併納入。 

如果您有用戶端行動裝置應用程式時，插入一些程式碼 toosend 自訂上的事件索引鍵的使用者作業，並建立[HockeyApp 橋接器](app-insights-hockeyapp-bridge-app.md)。 建立查詢中的[分析](app-insights-analytics.md)toodisplay hello 事件計數，並將其釘選 toohello 儀表板。

## <a name="example"></a>範例
[hello 範例](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService)監視具有 web 角色和兩個背景工作角色的服務。

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>在 Azure 雲端服務中執行時發生的「找不到方法」例外狀況
您是否已針對 .NET 4.6 組建？ Azure 雲端服務角色不自動支援 4.6。 [在每個角色上安裝 4.6](../cloud-services/cloud-services-dotnet-install-dotnet.md) ，再執行您的 App。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟
* [設定傳送 Azure 診斷 tooApplication Insights](app-insights-azure-diagnostics.md)
* [自動建立 Application Insights 資源](app-insights-powershell.md)
* [自動執行 Azure 診斷](app-insights-powershell-azure-diagnostics.md)
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
