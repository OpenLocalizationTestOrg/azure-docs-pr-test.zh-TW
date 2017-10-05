---
title: "使用 Application Insights 針對雲端服務進行疑難排解 | Microsoft Docs"
description: "了解如何使用 Application Insights 疑難排解雲端服務問題，以處理 Azure 診斷的資料。"
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
ms.openlocfilehash: 4001ca908ff00b1a40829d687589080e9b07b18a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a><span data-ttu-id="6094a-103">使用 Application Insights 疑難排解雲端服務</span><span class="sxs-lookup"><span data-stu-id="6094a-103">Troubleshoot Cloud Services using Application Insights</span></span>
<span data-ttu-id="6094a-104">使用 [Azure SDK 2.8](https://azure.microsoft.com/downloads/) 和 Azure 診斷延伸模組 1.5，您可以將雲端服務的 Azure 診斷資料直接傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="6094a-104">With [Azure SDK 2.8](https://azure.microsoft.com/downloads/) and Azure diagnostics extension 1.5, you can send Azure Diagnostics data for your Cloud Service directly to Application Insights.</span></span> <span data-ttu-id="6094a-105">Azure 診斷所收集的記錄&mdash;包括應用程式記錄、Windows 事件記錄、ETW 記錄，以及效能計數器&mdash;可以傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="6094a-105">The logs collected by Azure Diagnostics&mdash;including application logs, Windows Event Logs, ETW Logs, and performance counters&mdash;can be sent to Application Insights.</span></span> <span data-ttu-id="6094a-106">然後，您可以在 Application Insights 入口網站 UI 中，將這項資訊視覺化。</span><span class="sxs-lookup"><span data-stu-id="6094a-106">You can then visualize this information in the Application Insights portal UI.</span></span> <span data-ttu-id="6094a-107">接著，您可以使用 Application Insights SDK 深入了解來自您的應用程式和系統的計量和記錄，以及來自 Azure 診斷的基礎結構層級資料。</span><span class="sxs-lookup"><span data-stu-id="6094a-107">You can then use the Application Insights SDK to get insights into metrics and logs that come from your application, as well as the system and infrastructure-level data that comes from Azure Diagnostics.</span></span>

## <a name="configure-azure-diagnostics-to-send-data-to-application-insights"></a><span data-ttu-id="6094a-108">設定 Azure 診斷將資料傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="6094a-108">Configure Azure Diagnostics to send data to Application Insights</span></span>
<span data-ttu-id="6094a-109">請遵循下列步驟來設定雲端服務專案，將 Azure 診斷資料傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="6094a-109">Follow these steps to set up your cloud service project to send Azure Diagnostics data to Application Insights.</span></span>

1. <span data-ttu-id="6094a-110">在 Visual Studio 方案總管中，以滑鼠右鍵按一下角色，然後選取 [屬性] 以開啟角色設計工具。</span><span class="sxs-lookup"><span data-stu-id="6094a-110">In Visual Studio Solution Explorer, right-click a role and select **Properties** to open the Role designer.</span></span>

    ![方案總管角色屬性][1]

2. <span data-ttu-id="6094a-112">在角色設計的 [診斷] 區段中，選取 [將診斷資料傳送至 Application Insights] 選項。</span><span class="sxs-lookup"><span data-stu-id="6094a-112">In the **Diagnostics** section of the Role designer, select the **Send diagnostics data to Application Insights** option.</span></span>

    ![角色設計工具會將診斷資料傳送至 Application Insights][2]

3. <span data-ttu-id="6094a-114">在快顯的對話方塊中，選取您想要傳送 Azure 診斷資料的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="6094a-114">In the dialog box that pops up, select the Application Insights resource that you want to send the Azure diagnostics data to.</span></span> <span data-ttu-id="6094a-115">對話方塊可讓您從訂用帳戶中選取現有的 Application Insights 資源，或是為 Application Insights 資源手動指定檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="6094a-115">The dialog box allows you to select an existing Application Insights resource from your subscription or to manually specify an instrumentation key for an Application Insights resource.</span></span> <span data-ttu-id="6094a-116">如需建立 Application Insights 資源的詳細資訊，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="6094a-116">For more information on creating an Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

    ![選取 Application Insights 資源][3]

    <span data-ttu-id="6094a-118">新曾 Application Insights 資源後，該資源的檢測金鑰會儲存為名稱是 **APPINSIGHTS_INSTRUMENTATIONKEY** 的服務組態設定。</span><span class="sxs-lookup"><span data-stu-id="6094a-118">Once you have added the Application Insights resource, the instrumentation key for that resource is stored as a service configuration setting with the name **APPINSIGHTS_INSTRUMENTATIONKEY**.</span></span> <span data-ttu-id="6094a-119">您可以針對每個服務設定或環境變更此組態設定。</span><span class="sxs-lookup"><span data-stu-id="6094a-119">You can change this configuration setting for each service configuration or environment.</span></span> <span data-ttu-id="6094a-120">若要這樣做，請從 [服務設定] 清單中選取不同的設定，並為該設定指定新的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="6094a-120">To do so, select a different configuration from the **Service Configuration** list and specify a new instrumentation key for that configuration.</span></span>

    ![選取服務組態][4]

    <span data-ttu-id="6094a-122">在發佈期間，Visual studio 使用 **APPINSIGHTS_INSTRUMENTATIONKEY** 組態設定來設定診斷延伸模組的適當 Application Insights 資源資訊。</span><span class="sxs-lookup"><span data-stu-id="6094a-122">The **APPINSIGHTS_INSTRUMENTATIONKEY** configuration setting is used by Visual Studio to configure the diagnostics extension with the appropriate Application Insights resource information during publishing.</span></span> <span data-ttu-id="6094a-123">組態設定是為不同的服務組態定義不同檢測金鑰的便利方式。</span><span class="sxs-lookup"><span data-stu-id="6094a-123">The configuration setting is a convenient way of defining different instrumentation keys for different service configurations.</span></span> <span data-ttu-id="6094a-124">在發佈過程期間，Visual Studio 會轉譯該設定，並將它插入診斷延伸模組公用組態。</span><span class="sxs-lookup"><span data-stu-id="6094a-124">Visual Studio will translate that setting and insert it into the diagnostics extension public configuration during the publish process.</span></span> <span data-ttu-id="6094a-125">為簡化使用 PowerShell 設定診斷延伸模組的程序，Visual Studio 中的套件輸出也包含了公用組態 XML，並且包含適當的 Application Insights 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="6094a-125">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML with the appropriate Application Insights instrumentation key.</span></span> <span data-ttu-id="6094a-126">公用設定檔會在延伸模組資料夾中建立並遵循模式 *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml*。</span><span class="sxs-lookup"><span data-stu-id="6094a-126">The public config files are created in the Extensions folder and follow the pattern *PaaSDiagnostics.&lt;RoleName&gt;.PubConfig.xml*.</span></span> <span data-ttu-id="6094a-127">任何以 PowerShell 為基礎的部署都可以使用此模式，將每個設定對應至角色。</span><span class="sxs-lookup"><span data-stu-id="6094a-127">Any PowerShell-based deployments can use this pattern to map each configuration to a role.</span></span>

4) <span data-ttu-id="6094a-128">若要設定 Azure 診斷將 Azure 診斷代理程式所收集的所有效能計數器和錯誤層級記錄傳送至 Application Insights，請啟用 [將診斷資料傳送至 Application Insights] 選項。</span><span class="sxs-lookup"><span data-stu-id="6094a-128">To configure Azure diagnostics to send all performance counters and error-level logs collected by the Azure diagnostics agent to Application Insights, enable the **Send diagnostics data to Application Insights** option.</span></span> 

    <span data-ttu-id="6094a-129">如果您想進一步設定哪些資料要傳送至 Application Insights，就必須手動編輯每個角色的 *diagnostics.wadcfgx* 檔案。</span><span class="sxs-lookup"><span data-stu-id="6094a-129">If you want to further configure what data is sent to Application Insights, you must manually edit the *diagnostics.wadcfgx* file for each role.</span></span> <span data-ttu-id="6094a-130">若要深入了解手動更新組，請參閱 [設定 Azure 診斷以將資料傳送至 Application Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) 。</span><span class="sxs-lookup"><span data-stu-id="6094a-130">See [Configure Azure Diagnostics to send data to Application Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) to learn more about manually updating the configuration.</span></span>

<span data-ttu-id="6094a-131">當雲端服務設定為將 Azure 診斷資料傳送到 Application Insights 時，您就可以像平常一樣將它部署至 Azure，確定已啟用 Azure 診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6094a-131">When the cloud service is configured to send Azure diagnostics data to application insights, you can deploy it to Azure normally, making sure the Azure diagnostics extension is enabled.</span></span> <span data-ttu-id="6094a-132">如需詳細資訊，請參閱[使用 Visual Studio 發佈雲端服務](../vs-azure-tools-publishing-a-cloud-service.md)。</span><span class="sxs-lookup"><span data-stu-id="6094a-132">For more information, see  [Publishing a Cloud Service using Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).</span></span>  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a><span data-ttu-id="6094a-133">在 Application Insights 中檢視 Azure 診斷資料</span><span class="sxs-lookup"><span data-stu-id="6094a-133">Viewing Azure diagnostics data in Application Insights</span></span>
<span data-ttu-id="6094a-134">Azure 診斷遙測會顯示在為您雲端服務設定的 Application Insights 資源中。</span><span class="sxs-lookup"><span data-stu-id="6094a-134">The Azure diagnostic telemetry shows up in the Application Insights resource configured for your cloud service.</span></span>

<span data-ttu-id="6094a-135">Azure 診斷記錄類型會以下列方式對應至 Application Insights 概念：</span><span class="sxs-lookup"><span data-stu-id="6094a-135">Azure diagnostics log types map to Application Insights concepts in these ways:</span></span>

* <span data-ttu-id="6094a-136">效能計數器在 Application Insights 中會顯示為自訂計量。</span><span class="sxs-lookup"><span data-stu-id="6094a-136">Performance counters are displayed as Custom Metrics in Application Insights.</span></span>
* <span data-ttu-id="6094a-137">Windows 事件記錄在 Application Insights 中會顯示為追蹤和自訂事件。</span><span class="sxs-lookup"><span data-stu-id="6094a-137">Windows Event Logs are shown as Traces and Custom Events in Application Insights.</span></span>
* <span data-ttu-id="6094a-138">應用程式記錄、ETW 記錄和任何診斷基礎結構記錄在 Application Insights 中會顯示為追蹤。</span><span class="sxs-lookup"><span data-stu-id="6094a-138">Application logs, ETW logs, and any Diagnostics Infrastructure logs are shown as Traces in Application Insights.</span></span>

<span data-ttu-id="6094a-139">若要在 Application Insights 中檢視 Azure 診斷資料，請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="6094a-139">To view Azure diagnostics data in Application Insights, do one of the following:</span></span>

* <span data-ttu-id="6094a-140">使用[計量瀏覽器](../application-insights/app-insights-metrics-explorer.md)，以視覺化方式檢視任何自訂的效能計數器，或是不同類型的 Windows 事件記錄事件的計數。</span><span class="sxs-lookup"><span data-stu-id="6094a-140">Use [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) to visualize any custom performance counters or counts of different types of Windows Event Log events.</span></span>

    ![[計量瀏覽器] 中的自訂計量][5]

* <span data-ttu-id="6094a-142">使用 [搜尋](../application-insights/app-insights-diagnostic-search.md)，在 Azure 診斷傳送的追蹤記錄中進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="6094a-142">Use [Search](../application-insights/app-insights-diagnostic-search.md) to search across the  trace logs sent by Azure Diagnostics.</span></span> <span data-ttu-id="6094a-143">例如，如果未處理的例外狀況造成角色當機和回收，例外狀況的相關資訊就會顯示在 [Windows 事件記錄] 的 [應用程式] 通道中。</span><span class="sxs-lookup"><span data-stu-id="6094a-143">For example, if an unhandled exception has caused the role to crash and recycle, information about the exception shows up in the *Application* channel of *Windows Event Log*.</span></span> <span data-ttu-id="6094a-144">您可以使用搜尋來查看 Windows 事件記錄錯誤，並取得例外狀況的完整堆疊追蹤，可協助找出問題的原因。</span><span class="sxs-lookup"><span data-stu-id="6094a-144">You can use search to look at the Windows Event Log error and get the full stack trace for the exception to help find the cause of the issue.</span></span>

    ![搜尋追蹤][6]

## <a name="next-steps"></a><span data-ttu-id="6094a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6094a-146">Next Steps</span></span>
* <span data-ttu-id="6094a-147">[將 Application Insights SDK 加入您的雲端服務](../application-insights/app-insights-cloudservices.md) ，從您的應用程式傳送有關要求、例外狀況、相依性及任何自訂遙測的資料。</span><span class="sxs-lookup"><span data-stu-id="6094a-147">[Add the Application Insights SDK to your cloud service](../application-insights/app-insights-cloudservices.md) to send data about requests, exceptions, dependencies, and any custom telemetry from your application.</span></span> <span data-ttu-id="6094a-148">與 Azure 診斷資料結合時，您可以在此資訊相同的 Application Insight 資源中取得應用程式和系統的完整檢視。</span><span class="sxs-lookup"><span data-stu-id="6094a-148">When combined with the Azure Diagnostics data, this information you can get a complete view of your application and system, all in the same Application Insight resource.</span></span>  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
