---
title: "Log Analytics 中由使用者初始化的 Azure 自動化 Runbook 動作 | Microsoft Docs"
description: "本文說明如何視需要從 Log Analytics 搜尋結果執行自動化 Runbook。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: ff938697add98f3d21b4971175432335ee2e39ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a><span data-ttu-id="8f82e-103">從 Log Analytics 記錄搜尋結果利用自動化 Runbook 採取動作</span><span class="sxs-lookup"><span data-stu-id="8f82e-103">Take Action with an Automation Runbook from a Log Analytics log search result</span></span>

<span data-ttu-id="8f82e-104">從 Azure Log Analytics 中的記錄搜尋結果，您現在可以選取 [採取動作] 執行自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="8f82e-104">From a log search result in Azure Log Analytics, you can now select **Take action** to run an Automation runbook.</span></span>  <span data-ttu-id="8f82e-105">Runbook 可用來修復問題或採取其他動作，例如收集疑難排解資訊、傳送電子郵件，或建立服務要求。</span><span class="sxs-lookup"><span data-stu-id="8f82e-105">The runbook can be used to remediate the issue or take some other action such as collect troubleshooting information, send an email, or create a service request.</span></span> 

## <a name="components-and-features-used"></a><span data-ttu-id="8f82e-106">使用的元件和功能</span><span class="sxs-lookup"><span data-stu-id="8f82e-106">Components and features used</span></span>
* [<span data-ttu-id="8f82e-107">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="8f82e-107">Azure Automation account</span></span>](../automation/automation-offering-get-started.md)
* [<span data-ttu-id="8f82e-108">Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="8f82e-108">Log Analytics workspace</span></span>](../log-analytics/log-analytics-overview.md)

## <a name="to-initiate-runbook-from-log-search"></a><span data-ttu-id="8f82e-109">從記錄搜尋初始化 Runbook</span><span class="sxs-lookup"><span data-stu-id="8f82e-109">To initiate runbook from log search</span></span>

<span data-ttu-id="8f82e-110">若要對事件採取動作，並從記錄搜尋結果初始化 Runbook，首先請建立記錄搜尋，然後就可以從結果中視需要叫用 Runbook。</span><span class="sxs-lookup"><span data-stu-id="8f82e-110">To take action on an event and initiate a runbook from your log search results, you start by creating a log search and from the results you can invoke a runbook on-demand.</span></span>  <span data-ttu-id="8f82e-111">您可以利用 Azure 或 [OMS 入口網站](../log-analytics/log-analytics-log-searches.md)中的記錄搜尋功能達到此目的。</span><span class="sxs-lookup"><span data-stu-id="8f82e-111">This can be achieved from the log search feature in the Azure or [OMS portal](../log-analytics/log-analytics-log-searches.md).</span></span>  <span data-ttu-id="8f82e-112">在此範例中，我們會透過這項功能的基本示範，從 Azure 入口網站執行記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="8f82e-112">In this example, we perform a log search from the Azure portal with a basic demonstration of this feature.</span></span>

1. <span data-ttu-id="8f82e-113">在 Azure 入口網站的 [中樞] 功能表上按一下 [更多服務]，然後選取 [Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="8f82e-113">In the Azure portal, on the Hub menu click **More services** and select **Log Analytics**.</span></span>  
2. <span data-ttu-id="8f82e-114">在 [Log Analytics] 記錄搜尋上，選取您的 Log Analytics 工作區，然後在工作區刀鋒視窗上選取 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="8f82e-114">On the Log Analytics blade, select your Log Analytics workspace and on the workspace blade select **Log Search**.</span></span>  
3. <span data-ttu-id="8f82e-115">在 [記錄搜尋] 刀鋒視窗中，執行記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="8f82e-115">On the Log Search blade, perform a log search.</span></span>  
4. <span data-ttu-id="8f82e-116">從記錄搜尋結果中，按一下其中一個欄位左邊的省略符號，然後從快顯視窗中，選取 [對...採取動作]。</span><span class="sxs-lookup"><span data-stu-id="8f82e-116">From the log search results, click the ellipse to the left of one of the fields and from the popup, select **Take action on**.</span></span><br><br> <span data-ttu-id="8f82e-117">![從搜尋結果中選取採取動作](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span><span class="sxs-lookup"><span data-stu-id="8f82e-117">![Select Take Action from search result](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span></span> 
5. <span data-ttu-id="8f82e-118">從 [採取動作] 刀鋒視窗中，選取 [執行 Runbook]，然後在 [執行 Runbook] 刀鋒視窗中，您可以選取要執行的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="8f82e-118">From the Take action blade, select **Run a runbook**, and on the **Run a runbook** blade you can select a runbook to run.</span></span>  <span data-ttu-id="8f82e-119">您可以在連結至記錄 Log Analytics 工作區的自動化帳戶中選取任何 Runbook。</span><span class="sxs-lookup"><span data-stu-id="8f82e-119">You can select any runbook in the Automation account that is linked to the Log Analytics workspace.</span></span>  <span data-ttu-id="8f82e-120">請注意：</span><span class="sxs-lookup"><span data-stu-id="8f82e-120">Note the following:</span></span>

    * <span data-ttu-id="8f82e-121">Runbook 是依標籤來組織。</span><span class="sxs-lookup"><span data-stu-id="8f82e-121">Runbooks are organized by tags</span></span>
    * <span data-ttu-id="8f82e-122">從搜尋結果的欄位中，可直接選取 Runbook 輸入參數值。</span><span class="sxs-lookup"><span data-stu-id="8f82e-122">Runbook input parameter values can be selected directly from the fields of the search result.</span></span>  <span data-ttu-id="8f82e-123">出現的下拉式清單會顯示結果中所有可供選取的欄位。</span><span class="sxs-lookup"><span data-stu-id="8f82e-123">A drop-down list will appear displaying all the available fields from the result to select from.</span></span>  
    * <span data-ttu-id="8f82e-124">您選擇執行 Runbook 的地方，可以是您在有問題的電腦上已安裝的[混合式 Runbook 背景工作角色](../automation/automation-hybrid-runbook-worker.md)，前提是您有對應的混合式 Runbook 背景工作群組，而且這台電腦是唯一成員。</span><span class="sxs-lookup"><span data-stu-id="8f82e-124">You can choose to run the runbook on a [hybrid runbook worker](../automation/automation-hybrid-runbook-worker.md) that you have installed on the machine that has the issue if you have a corresponding Hybrid Runbook Worker group that only contains this machine as a member.</span></span>  <span data-ttu-id="8f82e-125">如果混合式背景工作群組的名稱符合記錄搜尋結果中的電腦名稱，則會自動選取該群組。</span><span class="sxs-lookup"><span data-stu-id="8f82e-125">If the name of the Hybrid Worker group matches the name of the computer that is in the log search result, then the group is selected automatically.</span></span>    

6. <span data-ttu-id="8f82e-126">按一下 [執行] 之後，Runbook 作業刀鋒視窗會開啟，讓您檢閱作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="8f82e-126">After you click **Run**, the runbook job blade will open to allow you to review the status of the job.</span></span>   

<span data-ttu-id="8f82e-127">如果您選取的 Runbook 已設定為[從 Log Analytics 警示呼叫](../automation/automation-invoke-runbook-from-omsla-alert.md)，它會有一個 **Object** 類型的輸入參數，稱為 **WebhookData**。</span><span class="sxs-lookup"><span data-stu-id="8f82e-127">If you select a runbook that was configured to be [called from a Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md), it has an input parameter called **WebhookData** that is **Object** type.</span></span>  <span data-ttu-id="8f82e-128">如果是必要的輸入參數，您需要將搜尋結果傳遞給 Runbook，它才能將 JSON 格式的字串轉換成物件類型，讓您篩選要在 Runbook 活動中參考的特定項目。</span><span class="sxs-lookup"><span data-stu-id="8f82e-128">If the input parameter is mandatory, you need to pass the search results to the runbook so it can convert the JSON-formatted string into an object type allowing you to filter on specific items that you will reference in runbook activities.</span></span>  <span data-ttu-id="8f82e-129">作法是從下拉式清單中選取 [搜尋結果 (Object)]。</span><span class="sxs-lookup"><span data-stu-id="8f82e-129">You do this by selecting **Search result (Object)** from the drop-down list.</span></span><br><br> <span data-ttu-id="8f82e-130">![選取 Webhook 資料物件給 Runbook 參數](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span><span class="sxs-lookup"><span data-stu-id="8f82e-130">![Select Webhook data object for runbook parameter](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span></span>   
    
## <a name="next-steps"></a><span data-ttu-id="8f82e-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f82e-131">Next steps</span></span>

* <span data-ttu-id="8f82e-132">檢閱 [Log Analytics 記錄檔搜尋參考資料](log-analytics-search-reference.md) ，以檢視 Log Analytics 中提供的所有搜尋欄位和 Facet。</span><span class="sxs-lookup"><span data-stu-id="8f82e-132">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
* <span data-ttu-id="8f82e-133">若要了解如何自動叫用自動化 Runbook，請檢閱[從 OMS Log Analytics 警示呼叫 Azure 自動化 Runbook](../automation/automation-invoke-runbook-from-omsla-alert.md)。</span><span class="sxs-lookup"><span data-stu-id="8f82e-133">To learn how to invoke an Automation runbook automatically, review [calling an Azure Automation runbook from an OMS Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md).</span></span>  