---
title: "Azure Application Insights 支援多個元件、微服務和容器 | Microsoft Docs"
description: "監視由多個元件或角色組成之應用程式的效能和使用方式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="1c078-103">使用 Application Insights (預覽) 監視多元件應用程式</span><span class="sxs-lookup"><span data-stu-id="1c078-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="1c078-104">您可以使用 [Azure Application Insights](app-insights-overview.md)，監視由多個伺服器元件、角色或服務所組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c078-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1c078-105">元件的健康情況和其間的關聯性會顯示在單一應用程式對應上。</span><span class="sxs-lookup"><span data-stu-id="1c078-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="1c078-106">您可以使用自動 HTTP 相互關聯，透過多個元件追蹤個別作業。</span><span class="sxs-lookup"><span data-stu-id="1c078-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="1c078-107">容器診斷可以與應用程式遙測整合並相互關聯。</span><span class="sxs-lookup"><span data-stu-id="1c078-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="1c078-108">將單一 Application Insights 資源用於您應用程式的所有元件。</span><span class="sxs-lookup"><span data-stu-id="1c078-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![多元件應用程式對應](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="1c078-110">我們在此使用「元件」來表示大型應用程式之任何運作中的組件。</span><span class="sxs-lookup"><span data-stu-id="1c078-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="1c078-111">例如，一般商務應用程式可能是由用戶端程式碼所組成，這些程式碼會在網頁瀏覽器中執行、與一或多個 Web 應用程式服務通訊，進而使用後端服務。</span><span class="sxs-lookup"><span data-stu-id="1c078-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="1c078-112">伺服器元件可能裝載於內部部署或雲端中，可能是 Azure 的 Web 和背景工作角色，也可能在 Docker 或 Service Fabric 等容器中執行。</span><span class="sxs-lookup"><span data-stu-id="1c078-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="1c078-113">共用單一 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="1c078-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="1c078-114">此處的重要技術是將您應用程式中每個元件的遙測傳送至相同的 Application Insights 資源，但必要時會使用 `cloud_RoleName` 屬性來區別元件。</span><span class="sxs-lookup"><span data-stu-id="1c078-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="1c078-115">Application Insights SDK 將 `cloud_RoleName` 屬性新增至遙測元件發出。</span><span class="sxs-lookup"><span data-stu-id="1c078-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="1c078-116">例如，SDK 會將網站名稱或服務角色名稱新增至 `cloud_RoleName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1c078-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="1c078-117">您可以使用 telemetryinitializer 覆寫這個值。</span><span class="sxs-lookup"><span data-stu-id="1c078-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="1c078-118">應用程式對應會使用 `cloud_RoleName` 屬性以識別地圖上的元件。</span><span class="sxs-lookup"><span data-stu-id="1c078-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="1c078-119">如需有關如何覆寫 `cloud_RoleName` 屬性的詳細資訊，請參閱[新增屬性：ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)。</span><span class="sxs-lookup"><span data-stu-id="1c078-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="1c078-120">在某些情況下，這可能不適當，而且您可能寧願將不同的資源用於不同的元件群組。</span><span class="sxs-lookup"><span data-stu-id="1c078-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="1c078-121">例如，您可能需要將不同的資源用於管理或計費目的。</span><span class="sxs-lookup"><span data-stu-id="1c078-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="1c078-122">使用不同的資源表示您未看到單一應用程式對應上顯示的所有元件；而且您無法在[分析](app-insights-analytics.md)中跨元件進行查詢。</span><span class="sxs-lookup"><span data-stu-id="1c078-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="1c078-123">您也必須設定不同的資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="1c078-124">請特別注意，我們假設在本文件的其餘部分，您想要將資料從多個元件傳送至一個 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="1c078-125">設定多元件應用程式</span><span class="sxs-lookup"><span data-stu-id="1c078-125">Configure multi-component applications</span></span>

<span data-ttu-id="1c078-126">若要取得多元件應用程式對應，您必須達成下列目標：</span><span class="sxs-lookup"><span data-stu-id="1c078-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="1c078-127">在應用程式的每個元件中**安裝最新的發行前版本** Application Insights 套件。</span><span class="sxs-lookup"><span data-stu-id="1c078-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="1c078-128">對您應用程式的所有元件**共用單一 Application Insights 資源**。</span><span class="sxs-lookup"><span data-stu-id="1c078-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="1c078-129">在 [預覽] 刀鋒視窗中**啟用多角色應用程式對應**。</span><span class="sxs-lookup"><span data-stu-id="1c078-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="1c078-130">使用適合其類型的方法，設定您應用程式的每個元件</span><span class="sxs-lookup"><span data-stu-id="1c078-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="1c078-131">([ASP.NET](app-insights-asp-net.md)、[Java](app-insights-java-get-started.md)、[Node.js](app-insights-nodejs.md)、[JavaScript](app-insights-javascript.md))。</span><span class="sxs-lookup"><span data-stu-id="1c078-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="1c078-132">1.安裝最新的發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="1c078-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="1c078-133">在每個伺服器元件的專案中更新或安裝 Appication Insights 套件。</span><span class="sxs-lookup"><span data-stu-id="1c078-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="1c078-134">如果您使用 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="1c078-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="1c078-135">以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="1c078-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="1c078-136">選取 [包括發行前版本]。</span><span class="sxs-lookup"><span data-stu-id="1c078-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="1c078-137">如果 Application Insights 套件顯示在 [更新] 中，請加以選取。</span><span class="sxs-lookup"><span data-stu-id="1c078-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="1c078-138">否則，請瀏覽並安裝適當的套件：</span><span class="sxs-lookup"><span data-stu-id="1c078-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="1c078-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1c078-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="1c078-140">Microsoft.ApplicationInsights.ServiceFabric - 適用於當做客體可執行檔執行的元件和在 Service Fabric 應用程式中執行的 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="1c078-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="1c078-141">Microsoft.ApplicationInsights.ServiceFabric.Native - 適用於 ServiceFabric 應用程式中的 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1c078-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="1c078-142">Microsoft.ApplicationInsights.Kubernetes - 適用於在 Kubernetes 上的 Docker 中執行的元件</span><span class="sxs-lookup"><span data-stu-id="1c078-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="1c078-143">2.共用單一 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="1c078-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="1c078-144">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [Application Insights] > [設定]。</span><span class="sxs-lookup"><span data-stu-id="1c078-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="1c078-145">對於第一個專案，使用精靈來建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="1c078-146">對於後續專案，選取相同的資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="1c078-147">如果沒有 Application Insights 功能表上，請手動進行設定︰</span><span class="sxs-lookup"><span data-stu-id="1c078-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="1c078-148">在 [Azure 入口網站](https://portal,azure.com)中，開啟您已經為另一個元件建立的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="1c078-149">在 [概觀] 刀鋒視窗中，開啟 [基本資訊] 下拉式索引標籤，然後複製 [檢測金鑰]。</span><span class="sxs-lookup"><span data-stu-id="1c078-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="1c078-150">在您的專案中，開啟 ApplicationInsights.config 並插入︰`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="1c078-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![將檢測金鑰複製到 .config 檔案](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="1c078-152">3.啟動多角色應用程式對應</span><span class="sxs-lookup"><span data-stu-id="1c078-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="1c078-153">在 Azure 入口網站中，開啟您應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="1c078-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="1c078-154">在 [預覽] 刀鋒視窗中，啟用「多角色應用程式對應」。</span><span class="sxs-lookup"><span data-stu-id="1c078-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="1c078-155">4.啟用 Docker 計量 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="1c078-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="1c078-156">如果元件在 Azure Windows VM 上裝載的 Docker 中執行，您可以從容器收集其他計量。</span><span class="sxs-lookup"><span data-stu-id="1c078-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="1c078-157">在您的 [Azure 診斷](../monitoring-and-diagnostics/azure-diagnostics.md)組態檔中插入此程式碼︰</span><span class="sxs-lookup"><span data-stu-id="1c078-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="1c078-158">使用 cloud_RoleName 來區分元件</span><span class="sxs-lookup"><span data-stu-id="1c078-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="1c078-159">`cloud_RoleName` 屬性會附加至所有遙測。</span><span class="sxs-lookup"><span data-stu-id="1c078-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="1c078-160">它會識別源自遙測的元件 (角色或服務)。</span><span class="sxs-lookup"><span data-stu-id="1c078-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="1c078-161">(這與 cloud_RoleInstance 不同，分隔在多個伺服器處理序或電腦上平行執行的相同角色)。</span><span class="sxs-lookup"><span data-stu-id="1c078-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="1c078-162">在入口網站中，您可以使用此屬性來篩選或區隔您的遙測。</span><span class="sxs-lookup"><span data-stu-id="1c078-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="1c078-163">在此範例中，[失敗] 刀鋒視窗會經過篩選，只顯示來自前端 Web 服務的資訊，並篩選出來自 CRM API 後端的失敗︰</span><span class="sxs-lookup"><span data-stu-id="1c078-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![依雲端角色名稱區隔的計量圖表](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="1c078-165">追蹤元件之間的作業</span><span class="sxs-lookup"><span data-stu-id="1c078-165">Trace operations between components</span></span>

<span data-ttu-id="1c078-166">您可以追蹤在處理個別作業時元件之間的呼叫。</span><span class="sxs-lookup"><span data-stu-id="1c078-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![顯示作業的遙測](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="1c078-168">跨前端 Web 伺服器和後端 API，逐一點選此作業的相互關聯遙測清單︰</span><span class="sxs-lookup"><span data-stu-id="1c078-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![跨元件搜尋](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="1c078-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c078-170">Next steps</span></span>

* [<span data-ttu-id="1c078-171">區分開發、測試及生產環境的遙測</span><span class="sxs-lookup"><span data-stu-id="1c078-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
