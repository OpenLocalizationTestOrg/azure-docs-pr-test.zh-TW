---
title: "使用 Application Insights 服務網狀架構事件分析 aaaAzure |Microsoft 文件"
description: "了解如何使用 Application Insights 視覺化及分析事件，來監視和診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a><span data-ttu-id="58bf4-103">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="58bf4-103">Event analysis and visualization with Application Insights</span></span>

<span data-ttu-id="58bf4-104">Azure Application Insights 是監視和診斷應用程式的擴充式平台。</span><span class="sxs-lookup"><span data-stu-id="58bf4-104">Azure Application Insights is an extensible platform for application monitoring and diagnostics.</span></span> <span data-ttu-id="58bf4-105">它包含強大的分析和查詢工具、可自訂的儀表板和視覺效果，以及包括自動化警示的進一步選項。</span><span class="sxs-lookup"><span data-stu-id="58bf4-105">It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting.</span></span> <span data-ttu-id="58bf4-106">它是建議的平台監視和診斷 Service Fabric 應用程式和服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="58bf4-106">It is hello recommended platform for monitoring and diagnostics for Service Fabric applications and services.</span></span>

## <a name="setting-up-application-insights"></a><span data-ttu-id="58bf4-107">設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="58bf4-107">Setting up Application Insights</span></span>

### <a name="creating-an-ai-resource"></a><span data-ttu-id="58bf4-108">建立 AI 資源</span><span class="sxs-lookup"><span data-stu-id="58bf4-108">Creating an AI Resource</span></span>

<span data-ttu-id="58bf4-109">toocreate AI 資源，透過 Azure Marketplace toohello 並搜尋"Application Insights"標頭。</span><span class="sxs-lookup"><span data-stu-id="58bf4-109">toocreate an AI resource, head over toohello Azure Marketplace, and search for "Application Insights".</span></span> <span data-ttu-id="58bf4-110">它應顯示為 hello （它是在類別目錄 」 Web + 行動裝置版 」） 的第一個方案。</span><span class="sxs-lookup"><span data-stu-id="58bf4-110">It should show up as hello first solution (it is under category "Web + Mobile").</span></span> <span data-ttu-id="58bf4-111">按一下**建立**您要尋找在 hello 適當的資源 （確認您的路徑符合 hello 圖）。</span><span class="sxs-lookup"><span data-stu-id="58bf4-111">Click **Create** when you are looking at hello right resource (confirm that your path matches hello image below).</span></span>

![新增 Application Insights 資源](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

<span data-ttu-id="58bf4-113">您將需要某些資訊 tooprovision hello 資源出 toofill 正確。</span><span class="sxs-lookup"><span data-stu-id="58bf4-113">You will need toofill out some information tooprovision hello resource correctly.</span></span> <span data-ttu-id="58bf4-114">在 [hello*應用程式類型*欄位中，使用 「 ASP.NET web 應用程式] 如果您將會使用任何 Service Fabric 的程式設計模型或發行的.NET 應用程式 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="58bf4-114">In hello *Application Type* field, use "ASP.NET web application" if you will be using any of Service Fabric's programming models or publishing a .NET application toohello cluster.</span></span> <span data-ttu-id="58bf4-115">如果您要部署來賓可執行檔和容器，請使用 [一般]。</span><span class="sxs-lookup"><span data-stu-id="58bf4-115">Use "General" if you will be deploying guest executables and containers.</span></span> <span data-ttu-id="58bf4-116">一般情況下，預設 toousing 「 ASP.NET web 應用程式 」 tookeep 選項在中開啟 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="58bf4-116">In general, default toousing "ASP.NET web application" tookeep your options open in hello future.</span></span> <span data-ttu-id="58bf4-117">hello 名稱已啟動 tooyour 喜好設定，且 hello 資源群組和訂用帳戶都可以變更部署後的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="58bf4-117">hello name is up tooyour preference, and both hello resource group and subscription are changeable post-deployment of hello resource.</span></span> <span data-ttu-id="58bf4-118">我們建議您 AI 資源是否處於 hello 與您的叢集相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="58bf4-118">We recommend that your AI resource is in hello same resource group as your cluster.</span></span> <span data-ttu-id="58bf4-119">如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="58bf4-119">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md)</span></span>

<span data-ttu-id="58bf4-120">您需要 hello AI 檢測金鑰 tooconfigure AI 與事件彙總工具。</span><span class="sxs-lookup"><span data-stu-id="58bf4-120">You need hello AI Instrumentation Key tooconfigure AI with your event aggregation tool.</span></span> <span data-ttu-id="58bf4-121">一旦設定 AI 資源之後 （採用 hello 部署會在驗證之後的幾分鐘），瀏覽 tooit，並尋找 hello**屬性**hello 左側的導覽列上一節。</span><span class="sxs-lookup"><span data-stu-id="58bf4-121">Once your AI resource is set up (takes a few minutes after hello deployment is validated), navigate tooit and find hello **Properties** section on hello left navigation bar.</span></span> <span data-ttu-id="58bf4-122">顯示「檢測金鑰」的新刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="58bf4-122">A new blade will open up that shows an *INSTRUMENTATION KEY*.</span></span> <span data-ttu-id="58bf4-123">如果您需要 toochange hello 訂用帳戶或資源群組的 hello 資源時，它可以在這裡進行以及。</span><span class="sxs-lookup"><span data-stu-id="58bf4-123">If you need toochange hello subscription or resource group of hello resource, it can be done here as well.</span></span>

### <a name="configuring-ai-with-wad"></a><span data-ttu-id="58bf4-124">設定具備 WAD 的 AI</span><span class="sxs-lookup"><span data-stu-id="58bf4-124">Configuring AI with WAD</span></span>

<span data-ttu-id="58bf4-125">有兩種主要的方式從 WAD tooAzure AI，toosend 資料中所述新增需 AI 接收 toohello WAD 組態，達成的[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。</span><span class="sxs-lookup"><span data-stu-id="58bf4-125">There are two primary ways toosend data from WAD tooAzure AI, which is achieved by adding an AI sink toohello WAD configuration, as detailed in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a><span data-ttu-id="58bf4-126">在 Azure 入口網站中建立叢集時新增 AI 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="58bf4-126">Add an AI Instrumentation Key when creating a cluster in Azure portal</span></span>

![新增 AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

<span data-ttu-id="58bf4-128">在建立叢集，如果診斷已 「 開啟 」 時，選擇性欄位 tooenter 應用程式 Insights 檢測金鑰即會顯示。</span><span class="sxs-lookup"><span data-stu-id="58bf4-128">When creating a cluster, if Diagnostics is turned "On", an optional field tooenter an Application Insights Instrumentation key will show.</span></span> <span data-ttu-id="58bf4-129">如果您貼上您的 AI IKey，hello AI 接收將會自動為您所使用的 toodeploy hello Resource Manager 範本在您的叢集的設定。</span><span class="sxs-lookup"><span data-stu-id="58bf4-129">If you paste your AI IKey here, hello AI sink will be automatically configured for you in hello Resource Manager template that is used toodeploy your cluster.</span></span>

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a><span data-ttu-id="58bf4-130">新增 hello AI 接收 toohello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="58bf4-130">Add hello AI Sink toohello Resource Manager template</span></span>

<span data-ttu-id="58bf4-131">在 hello"WadCfg 」 的 hello Resource Manager 範本，加入 「 接收 」 包含下列兩項變更的 hello:</span><span class="sxs-lookup"><span data-stu-id="58bf4-131">In hello "WadCfg" of hello Resource Manager template, add a "Sink" by including hello following two changes:</span></span>

1. <span data-ttu-id="58bf4-132">新增 hello 接收設定：</span><span class="sxs-lookup"><span data-stu-id="58bf4-132">Add hello sink configuration:</span></span>

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. <span data-ttu-id="58bf4-133">包含在 hello DiagnosticMonitorConfiguration hello 接收器加入 hello"WadCfg"hello"DiagnosticMonitorConfiguration 」 中的行下：</span><span class="sxs-lookup"><span data-stu-id="58bf4-133">Include hello Sink in hello DiagnosticMonitorConfiguration by adding hello following line in "DiagnosticMonitorConfiguration" of hello "WadCfg":</span></span>

    ```json
    "sinks": "applicationInsights"
    ```

<span data-ttu-id="58bf4-134">這兩個以上 hello 的 hello 程式碼片段名稱"applicationInsights"是使用的 toodescribe hello 接收。</span><span class="sxs-lookup"><span data-stu-id="58bf4-134">In both hello code snippets above, hello name "applicationInsights" was used toodescribe hello sink.</span></span> <span data-ttu-id="58bf4-135">這就不需要，只要 hello 名稱 hello 接收器會包含 「 接收 」 中，您可以設定 hello 名稱 tooany 字串。</span><span class="sxs-lookup"><span data-stu-id="58bf4-135">This is not a requirement and as long as hello name of hello sink is included in "sinks", you can set hello name tooany string.</span></span>

<span data-ttu-id="58bf4-136">目前，從 hello 叢集記錄檔會顯示為 AI 的記錄檔檢視器中的追蹤。</span><span class="sxs-lookup"><span data-stu-id="58bf4-136">Currently, logs from hello cluster will show up as traces in AI's log viewer.</span></span> <span data-ttu-id="58bf4-137">由於大部分的 hello 追蹤來自 hello 平台的 「 資訊 」 層級，您也可以考慮變更 hello 接收組態 tooonly 傳送記錄檔的"Critical"或"Error"的類型。</span><span class="sxs-lookup"><span data-stu-id="58bf4-137">Since most of hello traces coming from hello platform are of level "Informational", you can also consider changing hello sink configuration tooonly send logs of type "Critical" or "Error".</span></span> <span data-ttu-id="58bf4-138">作法是藉由新增 「 通道 」 tooyour 接收，如下所示[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。</span><span class="sxs-lookup"><span data-stu-id="58bf4-138">This can be done by adding "Channels" tooyour sink, as demonstrated in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

>[!NOTE]
><span data-ttu-id="58bf4-139">如果您使用不正確的 AI IKey 入口網站中或資源管理員範本中，您必須 toomanually 變更 hello 金鑰並更新 hello 叢集 / 重新部署它。</span><span class="sxs-lookup"><span data-stu-id="58bf4-139">If you use an incorrect AI IKey either in portal or in your Resource Manager template, you will have toomanually change hello key and update hello cluster / redeploy it.</span></span> 

### <a name="configuring-ai-with-eventflow"></a><span data-ttu-id="58bf4-140">設定具備 EventFlow 的 AI</span><span class="sxs-lookup"><span data-stu-id="58bf4-140">Configuring AI with EventFlow</span></span>

<span data-ttu-id="58bf4-141">如果您使用 EventFlow tooaggregate 事件，請確定 tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="58bf4-141">If you are using EventFlow tooaggregate events, make sure tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet package.</span></span> <span data-ttu-id="58bf4-142">hello 下列已包含在 hello toobe*輸出*區段 hello *eventFlowConfig.json*:</span><span class="sxs-lookup"><span data-stu-id="58bf4-142">hello following has toobe included in hello *outputs* section of hello *eventFlowConfig.json*:</span></span>

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

<span data-ttu-id="58bf4-143">在您的篩選條件，請確定 toomake hello 所需的變更，以及包含任何其他輸入 （以及其個別的 NuGet 封裝）。</span><span class="sxs-lookup"><span data-stu-id="58bf4-143">Make sure toomake hello required changes in your filters, as well as include any other inputs (along with their respective NuGet packages).</span></span>

## <a name="aisdk"></a><span data-ttu-id="58bf4-144">AI.SDK</span><span class="sxs-lookup"><span data-stu-id="58bf4-144">AI.SDK</span></span>

<span data-ttu-id="58bf4-145">一般會建議 toouse EventFlow 和 WAD 為彙總的解決方案，因為它們允許更模組化的方法 toodiagnostics，也就監視，如果您想 toochange EventFlow 您輸出，需要實際沒有變更 tooyour檢測，只要簡單的修改 tooyour 組態檔。</span><span class="sxs-lookup"><span data-stu-id="58bf4-145">It is generally recommended toouse EventFlow and WAD as aggregation solutions, because they allow for a more modular approach toodiagnostics and monitoring, i.e. if you want toochange your outputs from EventFlow, it requires no change tooyour actual instrumentation, just a simple modification tooyour config file.</span></span> <span data-ttu-id="58bf4-146">如果，不過，您決定使用 Application Insights tooinvest，而且不可能 toochange tooa 不同平台，您應該尋找使用的彙總事件，然後將它們傳送 tooAI AI 的新 SDK。</span><span class="sxs-lookup"><span data-stu-id="58bf4-146">If, however, you decide tooinvest in using Application Insights and are not likely toochange tooa different platform, you should look into using AI's new SDK for aggregating events and sending them tooAI.</span></span> <span data-ttu-id="58bf4-147">這表示您將不再有 tooconfigure EventFlow toosend 您資料 tooAI，但改為將安裝 hello ApplicationInsight 服務網狀架構 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="58bf4-147">This means that you will no longer have tooconfigure EventFlow toosend your data tooAI, but instead will install hello ApplicationInsight's Service Fabric NuGet package.</span></span> <span data-ttu-id="58bf4-148">Hello 封裝的詳細資訊可以找到[這裡](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="58bf4-148">Details on hello package can be found [here](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).</span></span>

<span data-ttu-id="58bf4-149">[Application Insights 支援 Microservices 和容器](https://azure.microsoft.com/app-insights-microservices/)顯示部分的 hello 新功能，正在 （目前仍處於 beta 版），可讓您 toohave 更豐富的全新的監視選項與 AI。</span><span class="sxs-lookup"><span data-stu-id="58bf4-149">[Application Insights support for Microservices and Containers](https://azure.microsoft.com/app-insights-microservices/) shows you some of hello new features that are being worked on (currently still in beta), which allow you toohave richer out-of-the-box monitoring options with AI.</span></span> <span data-ttu-id="58bf4-150">其中包括相依性追蹤 （用於建置的所有服務和應用程式在它們之間的叢集與 hello 通訊 AppMap），以及更佳的相互關聯的追蹤來自您的服務 （將有助於更好的查明 hello 的問題工作流程的應用程式或服務）。</span><span class="sxs-lookup"><span data-stu-id="58bf4-150">These include dependency tracking (used in building an AppMap of all your services and applications in a cluster and hello communication between them), and better correlation of traces coming from your services (helps in better pinpointing an issue in hello workflow of an app or service).</span></span>

<span data-ttu-id="58bf4-151">如果您正在開發.NET 中，而且可能會使用 Service Fabric 的程式設計模型的一部分，也會為您的平台，以便於檢視和分析事件和記錄資料，則我們建議，您會移透過 hello 做為您的監視 AI SDK 路由願意 toouse AI 和診斷工作流程。</span><span class="sxs-lookup"><span data-stu-id="58bf4-151">If you are developing in .NET and will likely be using some of Service Fabric's programming models, and are willing toouse AI as your platform for visualizing and analyzing event and log data, then we recommend that you go via hello AI SDK route as your monitoring and diagnostics workflow.</span></span> <span data-ttu-id="58bf4-152">讀取[這](../application-insights/app-insights-asp-net-more.md)和[這](../application-insights/app-insights-asp-net-trace-logs.md)tooget 開始使用 AI toocollect 並顯示您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="58bf4-152">Read [this](../application-insights/app-insights-asp-net-more.md) and [this](../application-insights/app-insights-asp-net-trace-logs.md) tooget started with using AI toocollect and display your logs.</span></span>

## <a name="navigating-hello-ai-resource-in-azure-portal"></a><span data-ttu-id="58bf4-153">瀏覽 Azure 入口網站中的 hello AI 資源</span><span class="sxs-lookup"><span data-stu-id="58bf4-153">Navigating hello AI resource in Azure portal</span></span>

<span data-ttu-id="58bf4-154">一旦您設定了 AI 為輸出，您的事件和記錄檔的資訊應該啟動 tooshow AI 資源中在幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="58bf4-154">Once you have configured AI as an output for your events and logs, information should start tooshow up in your AI resource in a few minutes.</span></span> <span data-ttu-id="58bf4-155">瀏覽 toohello AI 資源，而將採取您 toohello AI 資源儀表板。</span><span class="sxs-lookup"><span data-stu-id="58bf4-155">Navigate toohello AI resource, which will take you toohello AI resource dashboard.</span></span> <span data-ttu-id="58bf4-156">按一下**搜尋**hello AI 工作列 toosee hello 最新的追蹤已經接收和 toobe 無法 toofilter 逐一中。</span><span class="sxs-lookup"><span data-stu-id="58bf4-156">Click **Search** in hello AI taskbar toosee hello latest traces that it has received, and toobe able toofilter through them.</span></span>

<span data-ttu-id="58bf4-157">*計量瀏覽器*是很有用的工具，它可根據應用程式、服務和叢集可能報告的計量，建立自訂的儀表板。</span><span class="sxs-lookup"><span data-stu-id="58bf4-157">*Metrics Explorer* is a useful tool for creating custom dashboards based on metrics that your applications, services, and cluster may be reporting.</span></span> <span data-ttu-id="58bf4-158">請參閱[Application Insights 中的 瀏覽計量](../application-insights/app-insights-metrics-explorer.md)tooset 註冊自己的幾個圖表會根據 hello 您收集的資料。</span><span class="sxs-lookup"><span data-stu-id="58bf4-158">See [Exploring Metrics in Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset up a few charts for yourself based on hello data you are collecting.</span></span>

<span data-ttu-id="58bf4-159">按一下**分析**forma，obtendrá toohello 應用程式 Insights Analytics 入口網站，您可以在其中查詢事件和追蹤具有更大範圍和選用性。</span><span class="sxs-lookup"><span data-stu-id="58bf4-159">Clicking **Analytics** will take you toohello Application Insights Analytics portal, where you can query events and traces with greater scope and optionality.</span></span> <span data-ttu-id="58bf4-160">在 [Application Insights 的 Analytics](../application-insights/app-insights-analytics.md) 中了解更多。</span><span class="sxs-lookup"><span data-stu-id="58bf4-160">Read more about this at [Analytics in Application Insights](../application-insights/app-insights-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58bf4-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58bf4-161">Next steps</span></span>

* <span data-ttu-id="58bf4-162">[設定警示中 AI](../application-insights/app-insights-alerts.md) toobe 有關效能或使用方式中變更的通知</span><span class="sxs-lookup"><span data-stu-id="58bf4-162">[Set up Alerts in AI](../application-insights/app-insights-alerts.md) toobe notified about changes in performance or usage</span></span>
* <span data-ttu-id="58bf4-163">[智慧型 Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md)執行 hello 遙測傳送 tooAI toowarn 主動式分析您的潛在效能問題</span><span class="sxs-lookup"><span data-stu-id="58bf4-163">[Smart Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md) performs a proactive analysis of hello telemetry being sent tooAI toowarn you of potential performance problems</span></span>
