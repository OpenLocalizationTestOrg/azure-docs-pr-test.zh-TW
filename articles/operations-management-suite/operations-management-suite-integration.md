---
title: "與 Operations Management Suite (OMS) 進行整合 | Microsoft Docs"
description: "除了使用 OMS 的標準功能，您還可以將它與其他管理應用程式和服務進行整合，以提供混合式管理環境、提供您環境的唯一自訂管理案例，或為您的客戶提供自訂管理體驗。  本文提供與 OMS 進行整合的不同選項及提供詳細技術資訊文章連結的概觀。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 7a24df6f2c3b2c091d1b66b8b9c0a61035ffde11
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a><span data-ttu-id="65b5c-104">與 Operations Management Suite (OMS) 進行整合</span><span class="sxs-lookup"><span data-stu-id="65b5c-104">Integrating with Operations Management Suite (OMS)</span></span>
<span data-ttu-id="65b5c-105">Operations Management Suite 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="65b5c-105">Operations Management Suite is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span>  <span data-ttu-id="65b5c-106">除了使用 OMS 的標準功能，您還可以將它與其他管理應用程式和服務進行整合，以提供混合式管理環境、提供您環境的唯一自訂管理案例，或為您的客戶提供自訂管理體驗。</span><span class="sxs-lookup"><span data-stu-id="65b5c-106">In addition to using the standard features of OMS, you can integrate it with other management applications and services to provide a hybrid management environment, to provide custom management scenarios unique to your environment, or to provide a custom management experience for your customers.</span></span>  <span data-ttu-id="65b5c-107">本文提供與 OMS 服務進行整合的不同選項及提供詳細技術資訊文章連結的概觀。</span><span class="sxs-lookup"><span data-stu-id="65b5c-107">This article provides an overview of your different options for integrating with OMS services and links to articles providing detailed technical information.</span></span> 

## <a name="log-analytics"></a><span data-ttu-id="65b5c-108">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="65b5c-108">Log Analytics</span></span>
<span data-ttu-id="65b5c-109">Log Analytics 收集的管理資料都會儲存到裝載於 Azure 的存放庫中。</span><span class="sxs-lookup"><span data-stu-id="65b5c-109">Management data collected by Log Analytics is stored in a repository which is hosted in Azure.</span></span>  <span data-ttu-id="65b5c-110">記錄檔搜尋中可使用儲存在存放庫中的所有資料，這些記錄檔搜尋會跨極大量的資料提供快速分析。</span><span class="sxs-lookup"><span data-stu-id="65b5c-110">All data stored in the repository is available in log searches which provide quick analysis across extremely large amounts of data.</span></span>  <span data-ttu-id="65b5c-111">整合需求可能會以新的資料填入存放庫，讓它可用於分析，或者是在存放庫中擷取資料，以提供新的視覺效果或與其他管理工具整合。</span><span class="sxs-lookup"><span data-stu-id="65b5c-111">Your integration requirements may be to populate the repository with new data making it available for analysis, or to extract data in the repository to provide a new visualization or to integrate with another management tool.</span></span>

<span data-ttu-id="65b5c-112">存放庫中的每一筆資料會以記錄的形式儲存。</span><span class="sxs-lookup"><span data-stu-id="65b5c-112">Each piece of data in the repository is stored as a record.</span></span>  <span data-ttu-id="65b5c-113">當您填入存放庫時，應該將您的解決方案使用的記錄類型和其屬性的描述提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="65b5c-113">When you populate the repository, you should provide users with the record type that your solution uses and a description of its properties.</span></span>  <span data-ttu-id="65b5c-114">當您擷取資料時，需要您正在使用之資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="65b5c-114">When you retrieve data, you need this information about the data you’re working with.</span></span>

![填入 OMS 存放庫](media/operations-management-suite-integration/repository.png)

### <a name="populate-the-log-analytics-repository"></a><span data-ttu-id="65b5c-116">填入 Log Analytics 存放庫</span><span class="sxs-lookup"><span data-stu-id="65b5c-116">Populate the Log Analytics repository</span></span>
<span data-ttu-id="65b5c-117">有多種方式可填入 OMS 存放庫。</span><span class="sxs-lookup"><span data-stu-id="65b5c-117">There are multiple methods for populating the OMS repository.</span></span>  <span data-ttu-id="65b5c-118">您所使用的方法將取決於各種因素，例如來源資料的所在位置、資料的格式，以及您需要支援的用戶端。</span><span class="sxs-lookup"><span data-stu-id="65b5c-118">The method that you use will depend on factors such as where the source data is located, the format of the data, and which clients you need to support.</span></span>  <span data-ttu-id="65b5c-119">一旦資料儲存在存放庫後，則其收集方式將沒有差異。</span><span class="sxs-lookup"><span data-stu-id="65b5c-119">Once data is stored in the repository, it makes no difference how it was collected.</span></span>

<span data-ttu-id="65b5c-120">下列章節說明用來填入 OMS 存放庫的不同選項。</span><span class="sxs-lookup"><span data-stu-id="65b5c-120">The following sections describe the different options for populating the OMS repository.</span></span>

#### <a name="connected-sources-and-data-sources"></a><span data-ttu-id="65b5c-121">連接的來源和資料來源</span><span class="sxs-lookup"><span data-stu-id="65b5c-121">Connected Sources and Data sources</span></span>
<span data-ttu-id="65b5c-122">連接的來源是可以擷取 OMS 存放庫資料的位置。</span><span class="sxs-lookup"><span data-stu-id="65b5c-122">Connected sources are the locations where data can be retrieved for the OMS repository.</span></span>  <span data-ttu-id="65b5c-123">資料來源和解決方案會在連接來源上執行，並定義所收集的特定資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-123">Data Sources and Solutions run on Connected Sources and define the specific data that’s collected.</span></span>  <span data-ttu-id="65b5c-124">如果您的應用程式將資料寫入這些資料來源其中之一，則您可以藉由設定資料來源收集它。</span><span class="sxs-lookup"><span data-stu-id="65b5c-124">If your application writes data to one of these data sources, then you can collect it by configuring the data source.</span></span>  <span data-ttu-id="65b5c-125">例如，如果您的應用程式建立 Syslog 事件，則可以藉由 Linux 代理程式上的 Syslog 資料來源收集它們。</span><span class="sxs-lookup"><span data-stu-id="65b5c-125">For example, if your application creates Syslog events, then they can be collected by the Syslog data source on a Linux agent.</span></span>

* [<span data-ttu-id="65b5c-126">Log Analytics 中的資料來源</span><span class="sxs-lookup"><span data-stu-id="65b5c-126">Data sources in Log Analytics</span></span>](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a><span data-ttu-id="65b5c-127">解決方案</span><span class="sxs-lookup"><span data-stu-id="65b5c-127">Solutions</span></span>
<span data-ttu-id="65b5c-128">解決方案會擴充 OMS 的功能。</span><span class="sxs-lookup"><span data-stu-id="65b5c-128">Solutions extend the capabilities of OMS.</span></span>  <span data-ttu-id="65b5c-129">解決方案會從連線來源收集資料，或是它可能會執行存放庫中已收集記錄的分析。</span><span class="sxs-lookup"><span data-stu-id="65b5c-129">A solution may collect data from the connected source or it may perform analysis on records already collected in the repository.</span></span>  <span data-ttu-id="65b5c-130">Microsoft 所提供的每個解決方案都有個別文章，提供它所收集資料的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-130">Each solution provided by Microsoft has an individual article that provides the details on the data that it collects.</span></span>

* [<span data-ttu-id="65b5c-131">Log Analytics 中的解決方案</span><span class="sxs-lookup"><span data-stu-id="65b5c-131">Solutions in Log Analytics</span></span>](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a><span data-ttu-id="65b5c-132">HTTP 資料收集器 API</span><span class="sxs-lookup"><span data-stu-id="65b5c-132">HTTP Data Collector API</span></span>
<span data-ttu-id="65b5c-133">Log Analytics HTTP 資料收集器 API 是 REST API，可讓您將 JSON 資料新增至 Log Analytics 存放庫。</span><span class="sxs-lookup"><span data-stu-id="65b5c-133">The Log Analytics HTTP Data Collector API is a REST API that allows you to add JSON data to the Log Analytics repository.</span></span>  <span data-ttu-id="65b5c-134">當您的應用程式未透過其他資料來源或解決方案其中之一提供資料時，您可以利用這個 API。</span><span class="sxs-lookup"><span data-stu-id="65b5c-134">You can leverage this API when you have an application that doesn’t provide data through one of the other data sources or solutions.</span></span>  <span data-ttu-id="65b5c-135">它可以用來從任何用戶端填入存放庫，這些用戶端可呼叫 API 且不會依賴任何資料來源或方案的集合排程。</span><span class="sxs-lookup"><span data-stu-id="65b5c-135">It can be used to populate the repository from any client that can call the API and does not rely on the collection schedule of any data source or solution.</span></span>

* [<span data-ttu-id="65b5c-136">Log Analytics HTTP 資料收集器 API</span><span class="sxs-lookup"><span data-stu-id="65b5c-136">Log Analytics HTTP Data Collector API</span></span>](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-the-log-analytics-repository"></a><span data-ttu-id="65b5c-137">從 Log Analytics 存放庫擷取資料</span><span class="sxs-lookup"><span data-stu-id="65b5c-137">Retrieve data from the Log Analytics repository</span></span>
<span data-ttu-id="65b5c-138">有多種方式可從 OMS 存放庫擷取資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-138">There are multiple methods for retrieving data from the OMS repository.</span></span>  <span data-ttu-id="65b5c-139">您可能想要讓使用者使用 OMS 主控台擷取資料，並為他們提供各種不同的視覺效果和分析。</span><span class="sxs-lookup"><span data-stu-id="65b5c-139">You may want users to retrieve data using the OMS console and provide them with different kinds of visualizations and analysis.</span></span>  <span data-ttu-id="65b5c-140">您也可以從其他管理解決方案等外部處理序中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-140">You can also retrieve the data from an external process such as another management solution.</span></span>

#### <a name="log-searches"></a><span data-ttu-id="65b5c-141">記錄檔搜尋</span><span class="sxs-lookup"><span data-stu-id="65b5c-141">Log searches</span></span>
<span data-ttu-id="65b5c-142">儲存在 OMS 存放庫中的所有資料都可透過記錄搜尋提供使用。</span><span class="sxs-lookup"><span data-stu-id="65b5c-142">All data stored in the OMS repository is available through log searches.</span></span>  <span data-ttu-id="65b5c-143">使用者可在 OMS 主控台執行他們自己的臨機操作分析，或針對特定記錄檔搜尋建立具有視覺效果的儀表板。</span><span class="sxs-lookup"><span data-stu-id="65b5c-143">Users may perform their own ad hoc analysis in the OMS console or create a dashboard with a visualization for a particular log search.</span></span>  <span data-ttu-id="65b5c-144">解決方案可以根據預先定義的搜尋包含具有視覺效果的自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="65b5c-144">Solutions can contain custom views with visualizations based on predefined searches.</span></span>  <span data-ttu-id="65b5c-145">您可以使用 Log Search API，從外部應用程式或管理工具存取 OMS 存放庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-145">You can use the Log Search API to access data in the OMS repository from an external application or management tool.</span></span>  

* [<span data-ttu-id="65b5c-146">Log Analytics 中的記錄檔搜尋</span><span class="sxs-lookup"><span data-stu-id="65b5c-146">Log searches in Log Analytics</span></span>](../log-analytics/log-analytics-log-searches.md)
* [<span data-ttu-id="65b5c-147">Log Analytics 記錄檔搜尋 REST API</span><span class="sxs-lookup"><span data-stu-id="65b5c-147">Log Analytics log search REST API</span></span>](../log-analytics/log-analytics-log-search-api.md)
* [<span data-ttu-id="65b5c-148">Log Analytics Cmdlet</span><span class="sxs-lookup"><span data-stu-id="65b5c-148">Log Analytics cmdlets</span></span>](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a><span data-ttu-id="65b5c-149">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="65b5c-149">Custom views</span></span>
<span data-ttu-id="65b5c-150">檢視設計工具可讓您在 OMS 主控台建立自訂檢視，為使用者提供解決方案中的資料視覺效果與分析。</span><span class="sxs-lookup"><span data-stu-id="65b5c-150">The View Designer allows you to create custom views in the OMS console that provide users with visualization and analysis of the data in your solution.</span></span>  <span data-ttu-id="65b5c-151">每個檢視都包含主控台主頁面上所顯示的圖格，和根據您所定義之記錄搜尋的任意數目視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="65b5c-151">Each view includes a tile that’s displayed on the main page of the console and any number of visualization parts that are based on log searches that you define.</span></span>

* [<span data-ttu-id="65b5c-152">Log Analytics 檢視設計工具</span><span class="sxs-lookup"><span data-stu-id="65b5c-152">Log Analytics View Designer</span></span>](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a><span data-ttu-id="65b5c-153">Power BI</span><span class="sxs-lookup"><span data-stu-id="65b5c-153">Power BI</span></span>
<span data-ttu-id="65b5c-154">Log Analytics 可以自動將資料從 OMS 儲存機制匯出到 Power BI，讓您可以利用其視覺效果和分析工具。</span><span class="sxs-lookup"><span data-stu-id="65b5c-154">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>  <span data-ttu-id="65b5c-155">它會在排程上執行這個匯出，讓資料處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="65b5c-155">It performs this export on a schedule so the data is kept up to date.</span></span> 

* [<span data-ttu-id="65b5c-156">將 Log Analytics 資料匯出至 Power BI</span><span class="sxs-lookup"><span data-stu-id="65b5c-156">Export Log Analytics data to Power BI</span></span>](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a><span data-ttu-id="65b5c-157">自動化</span><span class="sxs-lookup"><span data-stu-id="65b5c-157">Automation</span></span>
<span data-ttu-id="65b5c-158">OMS 可以自動化程序來回應收集到的資料，或執行其他管理功能。</span><span class="sxs-lookup"><span data-stu-id="65b5c-158">OMS can automate processes to react to collected data or to perform other management functions.</span></span>  <span data-ttu-id="65b5c-159">它可從您的應用程式收集資料，並將它插入 OMS 存放庫，或者您可自動化校正存放庫中已知的問題，以回應存放庫中找到的資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-159">It may collect data from your application and insert it into the OMS repository, or you may automate the correction of a known issue in response to data found in the repository.</span></span> 

![自動化](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a><span data-ttu-id="65b5c-161">Runbook</span><span class="sxs-lookup"><span data-stu-id="65b5c-161">Runbooks</span></span>
<span data-ttu-id="65b5c-162">Azure 自動化中的 Runbook 會在 Azure 雲端中執行 PowerShell 指令碼和工作流程。</span><span class="sxs-lookup"><span data-stu-id="65b5c-162">Runbooks in Azure Automation run PowerShell scripts and workflows in the Azure cloud.</span></span>  <span data-ttu-id="65b5c-163">您可以使用它們來管理 Azure 中的資源，或可從雲端存取的任何其他資源。</span><span class="sxs-lookup"><span data-stu-id="65b5c-163">You can use them to manage resources in Azure or any other resources that can be accessed from the cloud.</span></span>  <span data-ttu-id="65b5c-164">也可以使用混合式 Runbook 背景工作角色在本機資料中心執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="65b5c-164">Runbooks can also be run in a local datacenter using Hybrid Runbook Worker.</span></span>  <span data-ttu-id="65b5c-165">您可以使用多種方法，例如 PowerShell 或自動化 API，從 Azure 入口網站或從外部處理程序啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="65b5c-165">You can start a runbook from the Azure portal or from external processes using a number of methods such as PowerShell or the Automation API.</span></span>

* [<span data-ttu-id="65b5c-166">在 Azure 自動化中啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="65b5c-166">Starting a runbook in Azure Automation</span></span>](../automation/automation-starting-a-runbook.md)
* [<span data-ttu-id="65b5c-167">Azure 自動化 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="65b5c-167">Azure Automation cmdlets</span></span>](https://msdn.microsoft.com/library/dn690262.aspx)
* [<span data-ttu-id="65b5c-168">自動化 REST API</span><span class="sxs-lookup"><span data-stu-id="65b5c-168">Automation REST API</span></span>](https://msdn.microsoft.com/library/mt662285.aspx)
* [<span data-ttu-id="65b5c-169">自動化 .NET</span><span class="sxs-lookup"><span data-stu-id="65b5c-169">Automation .NET</span></span>](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a><span data-ttu-id="65b5c-170">Alerts</span><span class="sxs-lookup"><span data-stu-id="65b5c-170">Alerts</span></span>
<span data-ttu-id="65b5c-171">警示規則會根據排程自動執行記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="65b5c-171">Alert rules automatically run log searches according to a schedule.</span></span>  <span data-ttu-id="65b5c-172">如果結果符合特定準則，產生的警示可以在 Azure 自動化中啟動 Runbook，或呼叫可以啟動外部處理序的 webhook。</span><span class="sxs-lookup"><span data-stu-id="65b5c-172">If the results match particular criteria the resulting alert can start a runbook in Azure Automation or call a webhook which can start an external process.</span></span>  <span data-ttu-id="65b5c-173">這兩個回應都可包括警示的詳細資料，包含記錄搜尋中傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="65b5c-173">Both of these responses can include details of the alert including the data returned in the log search.</span></span>

* [<span data-ttu-id="65b5c-174">Log Analytics 中的警示</span><span class="sxs-lookup"><span data-stu-id="65b5c-174">Alerts in Log Analytics</span></span>](../log-analytics/log-analytics-alerts.md)
* [<span data-ttu-id="65b5c-175">Log Analytics 警示 API</span><span class="sxs-lookup"><span data-stu-id="65b5c-175">Log Analytics Alert API</span></span>](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a><span data-ttu-id="65b5c-176">備份與站台復原</span><span class="sxs-lookup"><span data-stu-id="65b5c-176">Backup and Site Recovery</span></span>
<span data-ttu-id="65b5c-177">Azure 備份與 Site Recovery 提供保護您企業資料，並確認伺服器和應用程式可用性的服務。</span><span class="sxs-lookup"><span data-stu-id="65b5c-177">Azure Backup and Site Recovery provide services for protecting your enterprise data and ensuring the availability of servers and applications.</span></span>  <span data-ttu-id="65b5c-178">您可以利用這些服務來執行諸如為應用程式提供備份服務，或啟動虛擬機器的容錯移轉等案例。</span><span class="sxs-lookup"><span data-stu-id="65b5c-178">You can leverage these services to perform such scenarios as providing backup services for your application or initiating a failover of a virtual machine.</span></span>

* [<span data-ttu-id="65b5c-179">Azure 備份 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="65b5c-179">Azure Backup cmdlets</span></span>](https://msdn.microsoft.com/library/mt619253.aspx)
* [<span data-ttu-id="65b5c-180">Azure Site Recovery REST API</span><span class="sxs-lookup"><span data-stu-id="65b5c-180">Azure Site Recovery REST API</span></span>](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [<span data-ttu-id="65b5c-181">Azure Site Recovery Cmdlet</span><span class="sxs-lookup"><span data-stu-id="65b5c-181">Azure Site Recovery Cmdlets</span></span>](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a><span data-ttu-id="65b5c-182">自訂解決方案</span><span class="sxs-lookup"><span data-stu-id="65b5c-182">Custom solutions</span></span>
<span data-ttu-id="65b5c-183">您可以將整合邏輯封裝至在您的工作區或客戶的工作區中執行的自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="65b5c-183">You can encapsulate integration logic into a custom solution to run in your workspace or in a customer's workspace.</span></span>  <span data-ttu-id="65b5c-184">除了其他可提供完整管理案例的資源之外，您的方案可以包含本文中任何的整合方法。</span><span class="sxs-lookup"><span data-stu-id="65b5c-184">Your solution can include any of the integration methods in this article in addition to other resources to provide a complete management scenario.</span></span>  <span data-ttu-id="65b5c-185">當移除解決方案時解決方案中的資源會予以封裝，它所建立的所有資源會從 OMS 工作區和 Azure 訂用帳戶中移除。</span><span class="sxs-lookup"><span data-stu-id="65b5c-185">The resources in the solution are packaged such that when the solution is removed, all of the resources that it created are removed from the OMS workspace and Azure subscription.</span></span>

<span data-ttu-id="65b5c-186">例如，您的解決方案可包含要收集並處理資料的自動化 Runbook，然後使用 HTTP 資料收集器 API 填入 Log Analytics 存放庫。</span><span class="sxs-lookup"><span data-stu-id="65b5c-186">For example, your solution could include an Automation runbook to gather and process data and then populate the Log Analytics repository using the HTTP Data Collector API.</span></span>  <span data-ttu-id="65b5c-187">您也可以包含會顯示及分析所收集資料的自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="65b5c-187">You could also include a custom view that presents and analyzes the collected data.</span></span>  

* <span data-ttu-id="65b5c-188">建立自訂解決方案 (即將推出)</span><span class="sxs-lookup"><span data-stu-id="65b5c-188">Creating custom solutions (Coming soon)</span></span>    

## <a name="next-steps"></a><span data-ttu-id="65b5c-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65b5c-189">Next steps</span></span>
* <span data-ttu-id="65b5c-190">參考 [OMS SDK](operations-management-suite-sdk.md) 以取得關於自動化 OMS 服務的技術資訊。</span><span class="sxs-lookup"><span data-stu-id="65b5c-190">Reference the [OMS SDK](operations-management-suite-sdk.md) for technical information on automating OMS services.</span></span>  

