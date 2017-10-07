---
title: "aaaTroubleshoot 使用 Application Insights 雲端服務 |Microsoft 文件"
description: "了解如何使用 Application Insights tooprocess 資料從 Azure 診斷會發出 tootroubleshoot 雲端服務。"
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a><span data-ttu-id="192bf-103">使用 Application Insights 疑難排解雲端服務</span><span class="sxs-lookup"><span data-stu-id="192bf-103">Troubleshoot Cloud Services using Application Insights</span></span>
<span data-ttu-id="192bf-104">與[Azure SDK 2.8](https://azure.microsoft.com/downloads/)和 Azure 診斷擴充功能 1.5，可以傳送 Azure 診斷資料，針對您的雲端服務直接 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="192bf-104">With [Azure SDK 2.8](https://azure.microsoft.com/downloads/) and Azure diagnostics extension 1.5, you can send Azure Diagnostics data for your Cloud Service directly tooApplication Insights.</span></span> <span data-ttu-id="192bf-105">hello Azure 診斷所收集的記錄檔&mdash;包括應用程式記錄檔、 Windows 事件記錄檔、 ETW 記錄檔，以及效能計數器&mdash;可以傳送 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="192bf-105">hello logs collected by Azure Diagnostics&mdash;including application logs, Windows Event Logs, ETW Logs, and performance counters&mdash;can be sent tooApplication Insights.</span></span> <span data-ttu-id="192bf-106">然後，您可以視覺化 hello Application Insights 入口網站 UI 中的此資訊。</span><span class="sxs-lookup"><span data-stu-id="192bf-106">You can then visualize this information in hello Application Insights portal UI.</span></span> <span data-ttu-id="192bf-107">然後，您可以使用 hello Application Insights SDK tooget 深入了解標準和來自您的應用程式，以及 hello 系統和來自 Azure 診斷基礎結構層級資料的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="192bf-107">You can then use hello Application Insights SDK tooget insights into metrics and logs that come from your application, as well as hello system and infrastructure-level data that comes from Azure Diagnostics.</span></span>

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a><span data-ttu-id="192bf-108">設定 Azure 診斷 toosend 資料 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="192bf-108">Configure Azure Diagnostics toosend data tooApplication Insights</span></span>
<span data-ttu-id="192bf-109">請遵循這些步驟 tooset，設定您雲端服務專案 toosend Azure 診斷資料 tooApplication Insights。</span><span class="sxs-lookup"><span data-stu-id="192bf-109">Follow these steps tooset up your cloud service project toosend Azure Diagnostics data tooApplication Insights.</span></span>

1. <span data-ttu-id="192bf-110">在 Visual Studio 方案總管 中，以滑鼠右鍵按一下角色，然後選取**屬性**tooopen hello 角色設計工具。</span><span class="sxs-lookup"><span data-stu-id="192bf-110">In Visual Studio Solution Explorer, right-click a role and select **Properties** tooopen hello Role designer.</span></span>

    ![方案總管角色屬性][1]

2. <span data-ttu-id="192bf-112">在 hello**診斷**區段 hello 角色設計工具中，選取 hello**傳送診斷資料 tooApplication Insights**選項。</span><span class="sxs-lookup"><span data-stu-id="192bf-112">In hello **Diagnostics** section of hello Role designer, select hello **Send diagnostics data tooApplication Insights** option.</span></span>

    ![角色設計工具將診斷傳送資料 tooapplication insights][2]

3. <span data-ttu-id="192bf-114">在快顯的 hello 對話方塊中，選取您想要 toosend hello Azure 診斷資料的 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="192bf-114">In hello dialog box that pops up, select hello Application Insights resource that you want toosend hello Azure diagnostics data to.</span></span> <span data-ttu-id="192bf-115">hello 對話方塊可讓您從您的訂用帳戶的現有 Application Insights 資源 tooselect 或 toomanually，請指定 Application Insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="192bf-115">hello dialog box allows you tooselect an existing Application Insights resource from your subscription or toomanually specify an instrumentation key for an Application Insights resource.</span></span> <span data-ttu-id="192bf-116">如需建立 Application Insights 資源的詳細資訊，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="192bf-116">For more information on creating an Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

    ![選取 Application Insights 資源][3]

    <span data-ttu-id="192bf-118">一旦您加入 hello Application Insights 資源，該資源的 hello 檢測金鑰會儲存為 hello 名稱的服務組態設定**APPINSIGHTS_INSTRUMENTATIONKEY**。</span><span class="sxs-lookup"><span data-stu-id="192bf-118">Once you have added hello Application Insights resource, hello instrumentation key for that resource is stored as a service configuration setting with hello name **APPINSIGHTS_INSTRUMENTATIONKEY**.</span></span> <span data-ttu-id="192bf-119">您可以針對每個服務設定或環境變更此組態設定。</span><span class="sxs-lookup"><span data-stu-id="192bf-119">You can change this configuration setting for each service configuration or environment.</span></span> <span data-ttu-id="192bf-120">toodo 因此，選取不同的組態從 hello**服務組態**清單，並指定新的檢測金鑰，該設定。</span><span class="sxs-lookup"><span data-stu-id="192bf-120">toodo so, select a different configuration from hello **Service Configuration** list and specify a new instrumentation key for that configuration.</span></span>

    ![選取服務組態][4]

    <span data-ttu-id="192bf-122">hello **APPINSIGHTS_INSTRUMENTATIONKEY**的 Visual Studio tooconfigure hello 診斷延伸模組的 hello 適當 Application Insights 資源資訊發行期間會使用組態設定。</span><span class="sxs-lookup"><span data-stu-id="192bf-122">hello **APPINSIGHTS_INSTRUMENTATIONKEY** configuration setting is used by Visual Studio tooconfigure hello diagnostics extension with hello appropriate Application Insights resource information during publishing.</span></span> <span data-ttu-id="192bf-123">hello 組態設定會定義不同的檢測金鑰不同的服務組態的便利的方式。</span><span class="sxs-lookup"><span data-stu-id="192bf-123">hello configuration setting is a convenient way of defining different instrumentation keys for different service configurations.</span></span> <span data-ttu-id="192bf-124">Visual Studio 會轉譯該設定，並將其插入期間 hello 的 hello 診斷擴充功能公用組態發佈程序。</span><span class="sxs-lookup"><span data-stu-id="192bf-124">Visual Studio will translate that setting and insert it into hello diagnostics extension public configuration during hello publish process.</span></span> <span data-ttu-id="192bf-125">toosimplify hello 程序使用 PowerShell 設定 hello 診斷延伸模組，從 Visual Studio 的 hello 封裝輸出也包含 hello 公用組態 XML hello 適當 Application Insights 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="192bf-125">toosimplify hello process of configuring hello diagnostics extension with PowerShell, hello package output from Visual Studio also contains hello public configuration XML with hello appropriate Application Insights instrumentation key.</span></span> <span data-ttu-id="192bf-126">hello 公用組態檔會在 hello 擴充功能 資料夾中建立，並遵循 hello 模式*Paasdiagnostics.<rolename>.pubconfig.xml。&lt;RoleName&gt;。模式*。</span><span class="sxs-lookup"><span data-stu-id="192bf-126">hello public config files are created in hello Extensions folder and follow hello pattern *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml*.</span></span> <span data-ttu-id="192bf-127">任何 PowerShell 為基礎的部署可以使用此模式 toomap 每個組態 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="192bf-127">Any PowerShell-based deployments can use this pattern toomap each configuration tooa role.</span></span>

4) <span data-ttu-id="192bf-128">tooconfigure Azure 診斷 toosend hello Azure 診斷代理程式 tooApplication 見解，收集所有效能計數器和錯誤層級記錄檔啟用 hello**傳送診斷資料 tooApplication Insights**選項。</span><span class="sxs-lookup"><span data-stu-id="192bf-128">tooconfigure Azure diagnostics toosend all performance counters and error-level logs collected by hello Azure diagnostics agent tooApplication Insights, enable hello **Send diagnostics data tooApplication Insights** option.</span></span> 

    <span data-ttu-id="192bf-129">如果您想 toofurther 設定哪些資料會傳送 tooApplication Insights，您必須手動編輯 hello *diagnostics.wadcfgx*每個角色的檔案。</span><span class="sxs-lookup"><span data-stu-id="192bf-129">If you want toofurther configure what data is sent tooApplication Insights, you must manually edit hello *diagnostics.wadcfgx* file for each role.</span></span> <span data-ttu-id="192bf-130">請參閱[設定 Azure 診斷 toosend 資料 tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn 更多關於手動更新 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="192bf-130">See [Configure Azure Diagnostics toosend data tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn more about manually updating hello configuration.</span></span>

<span data-ttu-id="192bf-131">設定的 toosend Azure 診斷資料 tooapplication insights hello 雲端服務時，您可以部署它 tooAzure 正常，並確定已啟用 hello Azure 診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="192bf-131">When hello cloud service is configured toosend Azure diagnostics data tooapplication insights, you can deploy it tooAzure normally, making sure hello Azure diagnostics extension is enabled.</span></span> <span data-ttu-id="192bf-132">如需詳細資訊，請參閱[使用 Visual Studio 發佈雲端服務](../vs-azure-tools-publishing-a-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="192bf-132">For more information, see  [Publishing a Cloud Service using Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).</span></span>  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a><span data-ttu-id="192bf-133">在 Application Insights 中檢視 Azure 診斷資料</span><span class="sxs-lookup"><span data-stu-id="192bf-133">Viewing Azure diagnostics data in Application Insights</span></span>
<span data-ttu-id="192bf-134">hello Azure 診斷遙測會顯示 hello Application Insights 資源設定為您的雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="192bf-134">hello Azure diagnostic telemetry shows up in hello Application Insights resource configured for your cloud service.</span></span>

<span data-ttu-id="192bf-135">Azure 診斷記錄類型對應 tooApplication Insights 概念，以下列方式：</span><span class="sxs-lookup"><span data-stu-id="192bf-135">Azure diagnostics log types map tooApplication Insights concepts in these ways:</span></span>

* <span data-ttu-id="192bf-136">效能計數器在 Application Insights 中會顯示為自訂計量。</span><span class="sxs-lookup"><span data-stu-id="192bf-136">Performance counters are displayed as Custom Metrics in Application Insights.</span></span>
* <span data-ttu-id="192bf-137">Windows 事件記錄在 Application Insights 中會顯示為追蹤和自訂事件。</span><span class="sxs-lookup"><span data-stu-id="192bf-137">Windows Event Logs are shown as Traces and Custom Events in Application Insights.</span></span>
* <span data-ttu-id="192bf-138">應用程式記錄、ETW 記錄和任何診斷基礎結構記錄在 Application Insights 中會顯示為追蹤。</span><span class="sxs-lookup"><span data-stu-id="192bf-138">Application logs, ETW logs, and any Diagnostics Infrastructure logs are shown as Traces in Application Insights.</span></span>

<span data-ttu-id="192bf-139">tooview Application Insights 中的 Azure 診斷資料執行 hello 下列其中一種動作：</span><span class="sxs-lookup"><span data-stu-id="192bf-139">tooview Azure diagnostics data in Application Insights, do one of hello following:</span></span>

* <span data-ttu-id="192bf-140">使用[計量瀏覽器](../application-insights/app-insights-metrics-explorer.md)toovisualize 任何自訂效能計數器，或不同類型的 Windows 事件記錄檔事件的計數。</span><span class="sxs-lookup"><span data-stu-id="192bf-140">Use [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) toovisualize any custom performance counters or counts of different types of Windows Event Log events.</span></span>

    ![[計量瀏覽器] 中的自訂計量][5]

* <span data-ttu-id="192bf-142">使用[搜尋](../application-insights/app-insights-diagnostic-search.md)toosearch 跨 hello Azure 診斷所傳送的追蹤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="192bf-142">Use [Search](../application-insights/app-insights-diagnostic-search.md) toosearch across hello  trace logs sent by Azure Diagnostics.</span></span> <span data-ttu-id="192bf-143">比方說，如果未處理的例外狀況造成 hello 角色 toocrash 和回收，hello 例外狀況的相關資訊就會出現在 hello*應用程式*通道*Windows 事件記錄檔*。</span><span class="sxs-lookup"><span data-stu-id="192bf-143">For example, if an unhandled exception has caused hello role toocrash and recycle, information about hello exception shows up in hello *Application* channel of *Windows Event Log*.</span></span> <span data-ttu-id="192bf-144">您可以使用搜尋 toolook 在 hello Windows 事件記錄檔錯誤，並取得 hello 例外狀況 toohelp 尋找 hello hello 問題原因的 hello 完整的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="192bf-144">You can use search toolook at hello Windows Event Log error and get hello full stack trace for hello exception toohelp find hello cause of hello issue.</span></span>

    ![搜尋追蹤][6]

## <a name="next-steps"></a><span data-ttu-id="192bf-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="192bf-146">Next Steps</span></span>
* <span data-ttu-id="192bf-147">[新增 hello Application Insights SDK tooyour 雲端服務](../application-insights/app-insights-cloudservices.md)toosend 要求、 例外狀況、 相依性，以及從您的應用程式的任何自訂遙測資料。</span><span class="sxs-lookup"><span data-stu-id="192bf-147">[Add hello Application Insights SDK tooyour cloud service](../application-insights/app-insights-cloudservices.md) toosend data about requests, exceptions, dependencies, and any custom telemetry from your application.</span></span> <span data-ttu-id="192bf-148">當與 hello Azure 診斷資料，您可以取得完整的應用程式和系統中，檢視此資訊結合全都在 hello 相同 Application Insight 資源。</span><span class="sxs-lookup"><span data-stu-id="192bf-148">When combined with hello Azure Diagnostics data, this information you can get a complete view of your application and system, all in hello same Application Insight resource.</span></span>  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
