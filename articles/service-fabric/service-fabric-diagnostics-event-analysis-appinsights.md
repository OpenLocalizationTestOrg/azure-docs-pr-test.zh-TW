---
title: "Azure Service Fabric 事件分析與 Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 4085a607b800f4f4f155cdc266bc203b0858fd7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a><span data-ttu-id="ff4de-103">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="ff4de-103">Event analysis and visualization with Application Insights</span></span>

<span data-ttu-id="ff4de-104">Azure Application Insights 是監視和診斷應用程式的擴充式平台。</span><span class="sxs-lookup"><span data-stu-id="ff4de-104">Azure Application Insights is an extensible platform for application monitoring and diagnostics.</span></span> <span data-ttu-id="ff4de-105">它包含強大的分析和查詢工具、可自訂的儀表板和視覺效果，以及包括自動化警示的進一步選項。</span><span class="sxs-lookup"><span data-stu-id="ff4de-105">It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting.</span></span> <span data-ttu-id="ff4de-106">我們建議使用此平台監視和診斷 Service Fabric 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="ff4de-106">It is the recommended platform for monitoring and diagnostics for Service Fabric applications and services.</span></span>

## <a name="setting-up-application-insights"></a><span data-ttu-id="ff4de-107">設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff4de-107">Setting up Application Insights</span></span>

### <a name="creating-an-ai-resource"></a><span data-ttu-id="ff4de-108">建立 AI 資源</span><span class="sxs-lookup"><span data-stu-id="ff4de-108">Creating an AI Resource</span></span>

<span data-ttu-id="ff4de-109">若要建立 AI 資源，請前往 Azure Marketplace 搜尋 "Application Insights"。</span><span class="sxs-lookup"><span data-stu-id="ff4de-109">To create an AI resource, head over to the Azure Marketplace, and search for "Application Insights".</span></span> <span data-ttu-id="ff4de-110">它應該會顯示為第一個解決方案 (在 [Web + 行動] 類別目錄下)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-110">It should show up as the first solution (it is under category "Web + Mobile").</span></span> <span data-ttu-id="ff4de-111">找到正確的資源時，請按一下 [建立] (確認您的路徑與下圖相符)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-111">Click **Create** when you are looking at the right resource (confirm that your path matches the image below).</span></span>

![新增 Application Insights 資源](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

<span data-ttu-id="ff4de-113">您需要填寫一些資訊以正確佈建資源。</span><span class="sxs-lookup"><span data-stu-id="ff4de-113">You will need to fill out some information to provision the resource correctly.</span></span> <span data-ttu-id="ff4de-114">如果您要使用任何 Service Fabric 的程式設計模型或將 .NET 應用程式發佈至叢集，[應用程式類型] 欄位請使用 [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff4de-114">In the *Application Type* field, use "ASP.NET web application" if you will be using any of Service Fabric's programming models or publishing a .NET application to the cluster.</span></span> <span data-ttu-id="ff4de-115">如果您要部署來賓可執行檔和容器，請使用 [一般]。</span><span class="sxs-lookup"><span data-stu-id="ff4de-115">Use "General" if you will be deploying guest executables and containers.</span></span> <span data-ttu-id="ff4de-116">一般情況下預設使用 [ASP.NET Web 應用程式] 以在日後保持開放選項。</span><span class="sxs-lookup"><span data-stu-id="ff4de-116">In general, default to using "ASP.NET web application" to keep your options open in the future.</span></span> <span data-ttu-id="ff4de-117">名稱隨您的喜好設定，資源群組和訂用帳戶都可以在資源部署後變更。</span><span class="sxs-lookup"><span data-stu-id="ff4de-117">The name is up to your preference, and both the resource group and subscription are changeable post-deployment of the resource.</span></span> <span data-ttu-id="ff4de-118">我們建議 AI 資源與您的叢集位於相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ff4de-118">We recommend that your AI resource is in the same resource group as your cluster.</span></span> <span data-ttu-id="ff4de-119">如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-119">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md)</span></span>

<span data-ttu-id="ff4de-120">您需要使用 AI 檢測金鑰設定 AI 搭配事件彙總工具。</span><span class="sxs-lookup"><span data-stu-id="ff4de-120">You need the AI Instrumentation Key to configure AI with your event aggregation tool.</span></span> <span data-ttu-id="ff4de-121">完成 AI 資源設定後 (佈署後花幾分鐘驗證)，請在左側的導覽列上瀏覽並尋找 [屬性] 區段。</span><span class="sxs-lookup"><span data-stu-id="ff4de-121">Once your AI resource is set up (takes a few minutes after the deployment is validated), navigate to it and find the **Properties** section on the left navigation bar.</span></span> <span data-ttu-id="ff4de-122">顯示「檢測金鑰」的新刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ff4de-122">A new blade will open up that shows an *INSTRUMENTATION KEY*.</span></span> <span data-ttu-id="ff4de-123">如果您需要變更訂用帳戶或資源的資源群組，也可以在這裡完成。</span><span class="sxs-lookup"><span data-stu-id="ff4de-123">If you need to change the subscription or resource group of the resource, it can be done here as well.</span></span>

### <a name="configuring-ai-with-wad"></a><span data-ttu-id="ff4de-124">設定具備 WAD 的 AI</span><span class="sxs-lookup"><span data-stu-id="ff4de-124">Configuring AI with WAD</span></span>

<span data-ttu-id="ff4de-125">有兩種主要方式可將資料從 WAD 的傳送至 Azure AI，只要將 AI 接收新增到 WAD 設定中即可，詳細資訊請參閱[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-125">There are two primary ways to send data from WAD to Azure AI, which is achieved by adding an AI sink to the WAD configuration, as detailed in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a><span data-ttu-id="ff4de-126">在 Azure 入口網站中建立叢集時新增 AI 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="ff4de-126">Add an AI Instrumentation Key when creating a cluster in Azure portal</span></span>

![新增 AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

<span data-ttu-id="ff4de-128">建立叢集時，如果診斷已 [開啟]，即會顯示輸入 Application Insights 檢測金鑰的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="ff4de-128">When creating a cluster, if Diagnostics is turned "On", an optional field to enter an Application Insights Instrumentation key will show.</span></span> <span data-ttu-id="ff4de-129">如果在此貼上您的 AI IKey，用來部署叢集的 Resource Manager 範本就會自動為您設定 AI 接收。</span><span class="sxs-lookup"><span data-stu-id="ff4de-129">If you paste your AI IKey here, the AI sink will be automatically configured for you in the Resource Manager template that is used to deploy your cluster.</span></span>

#### <a name="add-the-ai-sink-to-the-resource-manager-template"></a><span data-ttu-id="ff4de-130">將 AI 接收新增至 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ff4de-130">Add the AI Sink to the Resource Manager template</span></span>

<span data-ttu-id="ff4de-131">在 Resource Manager 範本的 "WadCfg" 中，納入下列兩項變更以新增「接收」：</span><span class="sxs-lookup"><span data-stu-id="ff4de-131">In the "WadCfg" of the Resource Manager template, add a "Sink" by including the following two changes:</span></span>

1. <span data-ttu-id="ff4de-132">新增接收設定：</span><span class="sxs-lookup"><span data-stu-id="ff4de-132">Add the sink configuration:</span></span>

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

2. <span data-ttu-id="ff4de-133">在 "WadCfg" 的 "DiagnosticMonitorConfiguration" 新增下行程式碼，可在 DiagnosticMonitorConfiguration 中包含接收：</span><span class="sxs-lookup"><span data-stu-id="ff4de-133">Include the Sink in the DiagnosticMonitorConfiguration by adding the following line in "DiagnosticMonitorConfiguration" of the "WadCfg":</span></span>

    ```json
    "sinks": "applicationInsights"
    ```

<span data-ttu-id="ff4de-134">上面這兩個程式碼片段都使用 "applicationInsights" 名稱來描述接收。</span><span class="sxs-lookup"><span data-stu-id="ff4de-134">In both the code snippets above, the name "applicationInsights" was used to describe the sink.</span></span> <span data-ttu-id="ff4de-135">這不是需求，而是只要在「接收」中包含接收的名稱，就可以在任何字串設定該名稱。</span><span class="sxs-lookup"><span data-stu-id="ff4de-135">This is not a requirement and as long as the name of the sink is included in "sinks", you can set the name to any string.</span></span>

<span data-ttu-id="ff4de-136">目前，叢集中的記錄檔會顯示為 AI 記錄檔檢視器中的追蹤。</span><span class="sxs-lookup"><span data-stu-id="ff4de-136">Currently, logs from the cluster will show up as traces in AI's log viewer.</span></span> <span data-ttu-id="ff4de-137">由於大部分來自平台的追蹤層級都是「資訊」，您也可以考慮將接收設定變更為僅傳送「重大」或「錯誤」類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="ff4de-137">Since most of the traces coming from the platform are of level "Informational", you can also consider changing the sink configuration to only send logs of type "Critical" or "Error".</span></span> <span data-ttu-id="ff4de-138">只要將「通道」新增至接收器即可，如[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)所示。</span><span class="sxs-lookup"><span data-stu-id="ff4de-138">This can be done by adding "Channels" to your sink, as demonstrated in [this article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).</span></span>

>[!NOTE]
><span data-ttu-id="ff4de-139">如果您在入口網站或 Resource Manager 範本中使用不正確的 AI IKey，您就必須手動變更金鑰，並更新/重新部署叢集。</span><span class="sxs-lookup"><span data-stu-id="ff4de-139">If you use an incorrect AI IKey either in portal or in your Resource Manager template, you will have to manually change the key and update the cluster / redeploy it.</span></span> 

### <a name="configuring-ai-with-eventflow"></a><span data-ttu-id="ff4de-140">設定具備 EventFlow 的 AI</span><span class="sxs-lookup"><span data-stu-id="ff4de-140">Configuring AI with EventFlow</span></span>

<span data-ttu-id="ff4de-141">如要使用 EventFlow 來彙總事件，請務必匯入 `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ff4de-141">If you are using EventFlow to aggregate events, make sure to import the `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet package.</span></span> <span data-ttu-id="ff4de-142">*eventFlowConfig.json* 的 [輸出] 區段必須包含以下內容：</span><span class="sxs-lookup"><span data-stu-id="ff4de-142">The following has to be included in the *outputs* section of the *eventFlowConfig.json*:</span></span>

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace the following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

<span data-ttu-id="ff4de-143">請務必在您的篩選中進行必要的變更，以及包含任何其他輸入 (以及其個別的 NuGet 套件)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-143">Make sure to make the required changes in your filters, as well as include any other inputs (along with their respective NuGet packages).</span></span>

## <a name="aisdk"></a><span data-ttu-id="ff4de-144">AI.SDK</span><span class="sxs-lookup"><span data-stu-id="ff4de-144">AI.SDK</span></span>

<span data-ttu-id="ff4de-145">通常建議使用 EventFlow 和 WAD 做為彙總解決方案，因為它們允許以更接近模組化的方法來診斷和監視，亦即，如果您想要變更來自 EventFlow 的輸出，不必變更實際的檢測，只要簡單修改組態檔即可。</span><span class="sxs-lookup"><span data-stu-id="ff4de-145">It is generally recommended to use EventFlow and WAD as aggregation solutions, because they allow for a more modular approach to diagnostics and monitoring, i.e. if you want to change your outputs from EventFlow, it requires no change to your actual instrumentation, just a simple modification to your config file.</span></span> <span data-ttu-id="ff4de-146">但如果決定投資使用 Application Insights，而且不太可能變更到不同的平台，您應該考慮使用 AI 的新 SDK 來彙總事件，並將它們傳送到 AI。</span><span class="sxs-lookup"><span data-stu-id="ff4de-146">If, however, you decide to invest in using Application Insights and are not likely to change to a different platform, you should look into using AI's new SDK for aggregating events and sending them to AI.</span></span> <span data-ttu-id="ff4de-147">這表示您不必再設定 EventFlow 將資料傳送至 AI，而是改為安裝 ApplicationInsight 的 Service Fabric NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ff4de-147">This means that you will no longer have to configure EventFlow to send your data to AI, but instead will install the ApplicationInsight's Service Fabric NuGet package.</span></span> <span data-ttu-id="ff4de-148">套件的詳細資訊位於[這裡](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-148">Details on the package can be found [here](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).</span></span>

<span data-ttu-id="ff4de-149">[微服務與容器的 Application Insights 支援](https://azure.microsoft.com/app-insights-microservices/)會顯示一些開發中的新功能 (目前仍為 beta 版)，讓您有更多的 AI 立即可用監視選項。</span><span class="sxs-lookup"><span data-stu-id="ff4de-149">[Application Insights support for Microservices and Containers](https://azure.microsoft.com/app-insights-microservices/) shows you some of the new features that are being worked on (currently still in beta), which allow you to have richer out-of-the-box monitoring options with AI.</span></span> <span data-ttu-id="ff4de-150">包括相依性追蹤 (用於建置叢集中所有服務和應用程式的 AppMap 及它們之間的通訊)，以及來自服務的追蹤有更好的相互關聯 (更有助於查明應用程式或服務工作流程中的問題)。</span><span class="sxs-lookup"><span data-stu-id="ff4de-150">These include dependency tracking (used in building an AppMap of all your services and applications in a cluster and the communication between them), and better correlation of traces coming from your services (helps in better pinpointing an issue in the workflow of an app or service).</span></span>

<span data-ttu-id="ff4de-151">如果您是在 .NET 中進行開發，可能會使用一些 Service Fabric 的程式設計模型，而且是願意使用 AI 做視覺化和分析事件和記錄檔資料的平台，我們建議您在監視和診斷工作流程時透過 AI SDK 路由。</span><span class="sxs-lookup"><span data-stu-id="ff4de-151">If you are developing in .NET and will likely be using some of Service Fabric's programming models, and are willing to use AI as your platform for visualizing and analyzing event and log data, then we recommend that you go via the AI SDK route as your monitoring and diagnostics workflow.</span></span> <span data-ttu-id="ff4de-152">閱讀[本文](../application-insights/app-insights-asp-net-more.md)和[本文](../application-insights/app-insights-asp-net-trace-logs.md)開始使用 AI 來收集和顯示您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ff4de-152">Read [this](../application-insights/app-insights-asp-net-more.md) and [this](../application-insights/app-insights-asp-net-trace-logs.md) to get started with using AI to collect and display your logs.</span></span>

## <a name="navigating-the-ai-resource-in-azure-portal"></a><span data-ttu-id="ff4de-153">在 Azure 入口網站中瀏覽 AI 資源</span><span class="sxs-lookup"><span data-stu-id="ff4de-153">Navigating the AI resource in Azure portal</span></span>

<span data-ttu-id="ff4de-154">一旦將 AI 設定為事件和記錄檔的輸出，資訊就會在幾分鐘內開始出現在 AI 資源中。</span><span class="sxs-lookup"><span data-stu-id="ff4de-154">Once you have configured AI as an output for your events and logs, information should start to show up in your AI resource in a few minutes.</span></span> <span data-ttu-id="ff4de-155">瀏覽至 AI 資源，它會帶您到 AI 資源儀表板。</span><span class="sxs-lookup"><span data-stu-id="ff4de-155">Navigate to the AI resource, which will take you to the AI resource dashboard.</span></span> <span data-ttu-id="ff4de-156">按一下 AI 工作列的 [搜尋]，可查看它接收到的最新追蹤，並可從中進行篩選。</span><span class="sxs-lookup"><span data-stu-id="ff4de-156">Click **Search** in the AI taskbar to see the latest traces that it has received, and to be able to filter through them.</span></span>

<span data-ttu-id="ff4de-157">*計量瀏覽器*是很有用的工具，它可根據應用程式、服務和叢集可能報告的計量，建立自訂的儀表板。</span><span class="sxs-lookup"><span data-stu-id="ff4de-157">*Metrics Explorer* is a useful tool for creating custom dashboards based on metrics that your applications, services, and cluster may be reporting.</span></span> <span data-ttu-id="ff4de-158">請參閱[在 Application Insights 中探索計量](../application-insights/app-insights-metrics-explorer.md)，根據您所收集的資料自行設定幾個圖表。</span><span class="sxs-lookup"><span data-stu-id="ff4de-158">See [Exploring Metrics in Application Insights](../application-insights/app-insights-metrics-explorer.md) to set up a few charts for yourself based on the data you are collecting.</span></span>

<span data-ttu-id="ff4de-159">按一下 [分析] 會帶您到 Application Insights 的 Analytics 入口網站中，您可以在這裡查詢更大範圍和選擇性的事件和追蹤。</span><span class="sxs-lookup"><span data-stu-id="ff4de-159">Clicking **Analytics** will take you to the Application Insights Analytics portal, where you can query events and traces with greater scope and optionality.</span></span> <span data-ttu-id="ff4de-160">在 [Application Insights 的 Analytics](../application-insights/app-insights-analytics.md) 中了解更多。</span><span class="sxs-lookup"><span data-stu-id="ff4de-160">Read more about this at [Analytics in Application Insights](../application-insights/app-insights-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff4de-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff4de-161">Next steps</span></span>

* <span data-ttu-id="ff4de-162">[在 AI 中設定警示](../application-insights/app-insights-alerts.md)以收到效能或使用方式的變更通知</span><span class="sxs-lookup"><span data-stu-id="ff4de-162">[Set up Alerts in AI](../application-insights/app-insights-alerts.md) to be notified about changes in performance or usage</span></span>
* <span data-ttu-id="ff4de-163">[Application Insights 的智慧偵測](../application-insights/app-insights-proactive-diagnostics.md)會對傳送至 AI 的遙測資料執行主動式分析，對可能的效能問題提出警告。</span><span class="sxs-lookup"><span data-stu-id="ff4de-163">[Smart Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md) performs a proactive analysis of the telemetry being sent to AI to warn you of potential performance problems</span></span>