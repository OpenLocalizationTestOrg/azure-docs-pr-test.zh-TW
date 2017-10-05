---
title: "OMSManagement 解決方案的最佳作法 | Microsoft Docs"
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: b3d07ad3164609a5628c0d9805de55a32870ab94
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a><span data-ttu-id="d3d77-102">在 Operations Management Suite (OMS) 中建立管理解決方案的最佳作法 (預覽)</span><span class="sxs-lookup"><span data-stu-id="d3d77-102">Best practices for creating management solutions in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="d3d77-103">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="d3d77-103">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="d3d77-104">以下所述的任何結構描述可能會有所變更。</span><span class="sxs-lookup"><span data-stu-id="d3d77-104">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="d3d77-105">本文提供在 Operations Management Suite (OMS) 中[建立管理解決方案檔](operations-management-suite-solutions-solution-file.md)的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="d3d77-105">This article provides best practices for [creating a management solution file](operations-management-suite-solutions-solution-file.md) in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="d3d77-106">本資訊會在識別出其他最佳作法時更新。</span><span class="sxs-lookup"><span data-stu-id="d3d77-106">This information will be updated as additional best practices are identified.</span></span>

## <a name="data-sources"></a><span data-ttu-id="d3d77-107">資料來源</span><span class="sxs-lookup"><span data-stu-id="d3d77-107">Data sources</span></span>
- <span data-ttu-id="d3d77-108">資料來源可以[使用 Resource Manager 範本設定](../log-analytics/log-analytics-template-workspace-configuration.md)，但不應該將資源來源包含在解決方案檔中。</span><span class="sxs-lookup"><span data-stu-id="d3d77-108">Data sources can be [configured with a Resource Manager template](../log-analytics/log-analytics-template-workspace-configuration.md), but they should not be included in a solution file.</span></span>  <span data-ttu-id="d3d77-109">原因是設定資料來源目前並非等冪，這表示您的解決方案可能會覆寫使用者工作區中現有的設定。</span><span class="sxs-lookup"><span data-stu-id="d3d77-109">The reason is that configuring data sources is not currently idempotent meaning that your solution could overwrite existing configuration in the user's workspace.</span></span><br><br><span data-ttu-id="d3d77-110">例如，您的解決方案可能需要來自應用程式事件記錄檔的警告和錯誤事件。</span><span class="sxs-lookup"><span data-stu-id="d3d77-110">For example, your solution may require Warning and Error events from the Application event log.</span></span>  <span data-ttu-id="d3d77-111">如果您在解決方案中將此指定為資料來源，在使用者已在其工作區中設定此項的情況下，會有移除資訊事件的風險。</span><span class="sxs-lookup"><span data-stu-id="d3d77-111">If you specify this as a data source in your solution, you risk removing Information events if the user had this configured in their workspace.</span></span>  <span data-ttu-id="d3d77-112">如果您包含所有的事件，則可能會收集使用者工作區中過多的資訊事件。</span><span class="sxs-lookup"><span data-stu-id="d3d77-112">If you included all events, then you may be collecting excessive Information events in the user's workspace.</span></span>

- <span data-ttu-id="d3d77-113">如果您的解決方案需要來自其中一個標準資料來源的資料，則您應該將此定義為必要條件。</span><span class="sxs-lookup"><span data-stu-id="d3d77-113">If your solution requires data from one of the standard data sources, then you should define this as a prerequisite.</span></span>  <span data-ttu-id="d3d77-114">請在文件中表示客戶必須自行設定資料來源。</span><span class="sxs-lookup"><span data-stu-id="d3d77-114">State in documentation that the customer must configure the data source on their own.</span></span>  
- <span data-ttu-id="d3d77-115">將[資料流程驗證](../log-analytics/log-analytics-view-designer-tiles.md)訊息新增至解決方案中的任何檢視，以指示使用者關於需要設定以收集必要資料的資料來源資訊。</span><span class="sxs-lookup"><span data-stu-id="d3d77-115">Add a [Data Flow Verification](../log-analytics/log-analytics-view-designer-tiles.md) message to any views in your solution to instruct the user on data sources that need to be configured for required data to be collected.</span></span>  <span data-ttu-id="d3d77-116">找不到必要資料時，此訊息會顯示在檢視的圖格中。</span><span class="sxs-lookup"><span data-stu-id="d3d77-116">This message is displayed on the tile of the view when required data is not found.</span></span>


## <a name="runbooks"></a><span data-ttu-id="d3d77-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="d3d77-117">Runbooks</span></span>
- <span data-ttu-id="d3d77-118">為您解決方案中每個需要依排程執行的 Runbook 新增[自動化排程](../automation/automation-schedules.md)。</span><span class="sxs-lookup"><span data-stu-id="d3d77-118">Add an [Automation schedule](../automation/automation-schedules.md) for each runbook in your solution that needs to run on a schedule.</span></span>
- <span data-ttu-id="d3d77-119">在您的解決方案中包含 [IngestionAPI 模組 (英文)](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)，以供將資料寫入 Log Analytics 存放庫的 Runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="d3d77-119">Include the [IngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) in your solution to be used by runbooks writing data to the Log Analytics repository.</span></span>  <span data-ttu-id="d3d77-120">將解決方案設定為[參考](operations-management-suite-solutions-solution-file.md#solution-resource)此資源，讓它在移除解決方案後仍能保留。</span><span class="sxs-lookup"><span data-stu-id="d3d77-120">Configure the solution to [reference](operations-management-suite-solutions-solution-file.md#solution-resource) this resource so that it remains if the solution is removed.</span></span>  <span data-ttu-id="d3d77-121">這可讓多個解決方案共用模組。</span><span class="sxs-lookup"><span data-stu-id="d3d77-121">This allows multiple solutions to share the module.</span></span>
- <span data-ttu-id="d3d77-122">使用[自動化變數](../automation/automation-schedules.md)來將值提供給使用者於稍後可能會想要變更的解決方案。</span><span class="sxs-lookup"><span data-stu-id="d3d77-122">Use [Automation variables](../automation/automation-schedules.md) to provide values to the solution that users may want to change later.</span></span>  <span data-ttu-id="d3d77-123">即使解決方案已設定為包含變數，其值仍可以變更。</span><span class="sxs-lookup"><span data-stu-id="d3d77-123">Even if the solution is configured to contain the variable, it's value can still be changed.</span></span>

## <a name="views"></a><span data-ttu-id="d3d77-124">Views</span><span class="sxs-lookup"><span data-stu-id="d3d77-124">Views</span></span>
- <span data-ttu-id="d3d77-125">所有的解決方案都應該包含會在使用者的入口網站中顯示的單一檢視。</span><span class="sxs-lookup"><span data-stu-id="d3d77-125">All solutions should include a single view that is displayed in the user's portal.</span></span>  <span data-ttu-id="d3d77-126">檢視可以包含多個[視覺效果組件](../log-analytics/log-analytics-view-designer-parts.md)，以說明不同的資料集。</span><span class="sxs-lookup"><span data-stu-id="d3d77-126">The view can contain multiple [visualization parts](../log-analytics/log-analytics-view-designer-parts.md) to illustrate different sets of data.</span></span>
- <span data-ttu-id="d3d77-127">將[資料流程驗證](../log-analytics/log-analytics-view-designer-tiles.md)訊息新增至解決方案中的任何檢視，以指示使用者關於需要設定以收集必要資料的資料來源資訊。</span><span class="sxs-lookup"><span data-stu-id="d3d77-127">Add a [Data Flow Verification](../log-analytics/log-analytics-view-designer-tiles.md) message to any views in your solution to instruct the user on data sources that need to be configured for required data to be collected.</span></span>
- <span data-ttu-id="d3d77-128">將解決方案設定為[包含](operations-management-suite-solutions-solution-file.md#solution-resource)該檢視，讓檢視會隨著解決方案一起移除。</span><span class="sxs-lookup"><span data-stu-id="d3d77-128">Configure the solution to [contain](operations-management-suite-solutions-solution-file.md#solution-resource) the view so that it's removed if the solution is removed.</span></span>

## <a name="alerts"></a><span data-ttu-id="d3d77-129">Alerts</span><span class="sxs-lookup"><span data-stu-id="d3d77-129">Alerts</span></span>
- <span data-ttu-id="d3d77-130">將收件者清單定義為解決方案檔中的參數，讓使用者可以在安裝解決方案時定義它們。</span><span class="sxs-lookup"><span data-stu-id="d3d77-130">Define the recipients list as a parameter in the solution file so the user can define them when they install the solution.</span></span>
- <span data-ttu-id="d3d77-131">將解決方案設定為[參考](operations-management-suite-solutions-solution-file.md#solution-resource)警示規則，讓使用者可以變更其設定。</span><span class="sxs-lookup"><span data-stu-id="d3d77-131">Configure the solution to [reference](operations-management-suite-solutions-solution-file.md#solution-resource) alert rules so that user's can change their configuration.</span></span>  <span data-ttu-id="d3d77-132">他們可能會想要做出如修改收件者清單、變更警示閾值，或停用警示規則等變更。</span><span class="sxs-lookup"><span data-stu-id="d3d77-132">They may want to make changes such as modifying the recipient list, changing the threshold of the alert, or disabling the alert rule.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d3d77-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3d77-133">Next steps</span></span>
* <span data-ttu-id="d3d77-134">逐步了解[設計與建置管理解決方案](operations-management-suite-solutions-creating.md)的基本程序。</span><span class="sxs-lookup"><span data-stu-id="d3d77-134">Walk through the basic process of [designing and building a management solution](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="d3d77-135">了解如何[建立解決方案檔](operations-management-suite-solutions-solution-file.md)。</span><span class="sxs-lookup"><span data-stu-id="d3d77-135">Learn how to [create a solution file](operations-management-suite-solutions-solution-file.md).</span></span>
* <span data-ttu-id="d3d77-136">在您的管理解決方案中[新增儲存的搜尋和警示](operations-management-suite-solutions-resources-searches-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="d3d77-136">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="d3d77-137">在您的管理解決方案中[新增檢視](operations-management-suite-solutions-resources-views.md)。</span><span class="sxs-lookup"><span data-stu-id="d3d77-137">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="d3d77-138">在您的管理解決方案中[新增自動化 Runbook 及其他資源](operations-management-suite-solutions-resources-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="d3d77-138">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

