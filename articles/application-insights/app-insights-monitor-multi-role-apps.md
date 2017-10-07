---
title: "aaaAzure Application Insights 支援多個元件、 microservices，以及容器 |Microsoft 文件"
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
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="1c362-103">使用 Application Insights (預覽) 監視多元件應用程式</span><span class="sxs-lookup"><span data-stu-id="1c362-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="1c362-104">您可以使用 [Azure Application Insights](app-insights-overview.md)，監視由多個伺服器元件、角色或服務所組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c362-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1c362-105">hello 元件健全狀況 hello 和 hello 兩者間的關聯性會顯示在單一的應用程式對應。</span><span class="sxs-lookup"><span data-stu-id="1c362-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="1c362-106">您可以使用自動 HTTP 相互關聯，透過多個元件追蹤個別作業。</span><span class="sxs-lookup"><span data-stu-id="1c362-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="1c362-107">容器診斷可以與應用程式遙測整合並相互關聯。</span><span class="sxs-lookup"><span data-stu-id="1c362-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="1c362-108">使用單一的 Application Insights 資源的應用程式的所有 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="1c362-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![多元件應用程式對應](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="1c362-110">我們會使用 '元件' 這裡 toomean 的大型應用程式的任何正常運作的一部分。</span><span class="sxs-lookup"><span data-stu-id="1c362-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="1c362-111">例如，一般商務應用程式可能包含在 web 瀏覽器中，指 tooone 中執行的用戶端程式碼或更多的 web 應用程式服務，接著使用 上一步結束服務。</span><span class="sxs-lookup"><span data-stu-id="1c362-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="1c362-112">伺服器元件可能裝載在內部部署上 hello 雲端，或可能是 Azure web 和背景工作角色，或容器，例如 Docker 或 Service Fabric 執行。</span><span class="sxs-lookup"><span data-stu-id="1c362-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="1c362-113">共用單一 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="1c362-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="1c362-114">hello 索引鍵的技術是從每個元件的應用程式 toohello toosend 遙測相同的 Application Insights 資源，但使用 hello`cloud_RoleName`屬性 toodistinguish 元件在必要時。</span><span class="sxs-lookup"><span data-stu-id="1c362-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="1c362-115">hello Application Insights SDK 加入 hello`cloud_RoleName`屬性 toohello 遙測元件發出。</span><span class="sxs-lookup"><span data-stu-id="1c362-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="1c362-116">比方說，hello SDK 會將網站名稱或服務的角色名稱 toohello`cloud_RoleName`屬性。</span><span class="sxs-lookup"><span data-stu-id="1c362-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="1c362-117">您可以使用 telemetryinitializer 覆寫這個值。</span><span class="sxs-lookup"><span data-stu-id="1c362-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="1c362-118">hello 應用程式對應使用 hello `cloud_RoleName` hello 地圖上的屬性 tooidentify hello 元件。</span><span class="sxs-lookup"><span data-stu-id="1c362-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="1c362-119">如需有關如何覆寫 hello`cloud_RoleName`屬性，請參閱[將屬性加入： ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)。</span><span class="sxs-lookup"><span data-stu-id="1c362-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="1c362-120">在某些情況下，這不是適當，，您可能會想 toouse 不同元件的不同群組的資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="1c362-121">例如，您可能需要 toouse 不同的資源管理或計費。</span><span class="sxs-lookup"><span data-stu-id="1c362-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="1c362-122">使用不同的資源表示您沒有看到所有顯示在單一的應用程式對應; 上的 hello 元件而且您不能跨元件中查詢[分析](app-insights-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="1c362-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="1c362-123">您也可以 tooset hello 個別資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="1c362-124">與該警告，我們假設在 hello 這份文件其餘部分的 toosend 資料從多個元件 tooone Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="1c362-125">設定多元件應用程式</span><span class="sxs-lookup"><span data-stu-id="1c362-125">Configure multi-component applications</span></span>

<span data-ttu-id="1c362-126">tooget 多元件的應用程式對應，您需要 tooachieve 這些目標：</span><span class="sxs-lookup"><span data-stu-id="1c362-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="1c362-127">**安裝 hello 最新發行前版本**hello 應用程式的每個元件中的 Application Insights 套件。</span><span class="sxs-lookup"><span data-stu-id="1c362-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="1c362-128">**共用單一的 Application Insights 資源**針對所有 hello 應用程式的元件。</span><span class="sxs-lookup"><span data-stu-id="1c362-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="1c362-129">**啟用多角色應用程式對應**hello 預覽刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="1c362-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="1c362-130">設定使用 hello 適當的方法，其類型的應用程式的每個元件。</span><span class="sxs-lookup"><span data-stu-id="1c362-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="1c362-131">([ASP.NET](app-insights-asp-net.md)、[Java](app-insights-java-get-started.md)、[Node.js](app-insights-nodejs.md)、[JavaScript](app-insights-javascript.md))。</span><span class="sxs-lookup"><span data-stu-id="1c362-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="1c362-132">1.安裝最新發行前套件 hello</span><span class="sxs-lookup"><span data-stu-id="1c362-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="1c362-133">更新或安裝 hello 正 Insights 套件 hello 專案中為每一個伺服器元件。</span><span class="sxs-lookup"><span data-stu-id="1c362-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="1c362-134">如果您使用 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="1c362-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="1c362-135">以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="1c362-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="1c362-136">選取 [包括發行前版本]。</span><span class="sxs-lookup"><span data-stu-id="1c362-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="1c362-137">如果 Application Insights 套件顯示在 [更新] 中，請加以選取。</span><span class="sxs-lookup"><span data-stu-id="1c362-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="1c362-138">否則，請瀏覽及安裝 hello 適當套件：</span><span class="sxs-lookup"><span data-stu-id="1c362-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="1c362-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1c362-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="1c362-140">Microsoft.ApplicationInsights.ServiceFabric - 適用於當做客體可執行檔執行的元件和在 Service Fabric 應用程式中執行的 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="1c362-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="1c362-141">Microsoft.ApplicationInsights.ServiceFabric.Native - 適用於 ServiceFabric 應用程式中的 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1c362-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="1c362-142">Microsoft.ApplicationInsights.Kubernetes - 適用於在 Kubernetes 上的 Docker 中執行的元件</span><span class="sxs-lookup"><span data-stu-id="1c362-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="1c362-143">2.共用單一 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="1c362-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="1c362-144">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [Application Insights] > [設定]。</span><span class="sxs-lookup"><span data-stu-id="1c362-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="1c362-145">Hello 第一個專案中，使用 hello 精靈 toocreate Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="1c362-146">後續專案中，選取 hello 相同的資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="1c362-147">如果沒有 Application Insights 功能表上，請手動進行設定︰</span><span class="sxs-lookup"><span data-stu-id="1c362-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="1c362-148">在[Azure 入口網站](https://portal,azure.com)，開啟您已為另一個元件所建立的 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="1c362-149">在 hello 概觀刀鋒視窗，開啟 hello Essentials 下拉式索引標籤上，複製 hello**檢測金鑰。**</span><span class="sxs-lookup"><span data-stu-id="1c362-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="1c362-150">在您的專案中，開啟 ApplicationInsights.config 並插入︰`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="1c362-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![複製 hello 檢測金鑰 toohello.config 檔案](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="1c362-152">3.啟動多角色應用程式對應</span><span class="sxs-lookup"><span data-stu-id="1c362-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="1c362-153">在 hello Azure 入口網站，開啟您的應用程式的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="1c362-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="1c362-154">在 hello 預覽刀鋒視窗中，啟用*多角色應用程式對應*。</span><span class="sxs-lookup"><span data-stu-id="1c362-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="1c362-155">4.啟用 Docker 計量 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="1c362-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="1c362-156">如果在裝載 Windows Azure VM 上的 Docker 執行元件，您可以從 hello 容器收集其他度量。</span><span class="sxs-lookup"><span data-stu-id="1c362-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="1c362-157">在您的 [Azure 診斷](../monitoring-and-diagnostics/azure-diagnostics.md)組態檔中插入此程式碼︰</span><span class="sxs-lookup"><span data-stu-id="1c362-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="1c362-158">使用 cloud_RoleName tooseparate 元件</span><span class="sxs-lookup"><span data-stu-id="1c362-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="1c362-159">hello`cloud_RoleName`屬性是附加的 tooall 遙測。</span><span class="sxs-lookup"><span data-stu-id="1c362-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="1c362-160">它會識別 hello 元件-hello 角色或服務-源自 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="1c362-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="1c362-161">（它是不相同 hello 為 cloud_RoleInstance，會以平行方式執行多個伺服器處理序或電腦的相同角色分隔）。</span><span class="sxs-lookup"><span data-stu-id="1c362-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="1c362-162">在 hello 入口網站中，您可以篩選或區段您使用這個屬性的遙測。</span><span class="sxs-lookup"><span data-stu-id="1c362-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="1c362-163">在此範例中，hello 失敗刀鋒視窗就是篩選的 tooshow 只 hello 前端的 web 服務，篩選出 hello CRM API 後端的失敗資訊：</span><span class="sxs-lookup"><span data-stu-id="1c362-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![依雲端角色名稱區隔的計量圖表](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="1c362-165">追蹤元件之間的作業</span><span class="sxs-lookup"><span data-stu-id="1c362-165">Trace operations between components</span></span>

<span data-ttu-id="1c362-166">您可以從一個元件 tooanother，hello 呼叫處理個別的作業時進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="1c362-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![顯示作業的遙測](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="1c362-168">透過這項作業的遙測 tooa 相互關聯清單按一下跨 hello 前端網頁伺服器與 hello 後端應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="1c362-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![跨元件搜尋](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="1c362-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c362-170">Next steps</span></span>

* [<span data-ttu-id="1c362-171">區分開發、測試及生產環境的遙測</span><span class="sxs-lookup"><span data-stu-id="1c362-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
