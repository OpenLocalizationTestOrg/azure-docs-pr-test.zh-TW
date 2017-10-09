---
title: "aaaUser 起始 Azure 自動化 Runbook 中的動作記錄分析 |Microsoft 文件"
description: "本文說明如何 toorun 自動化 runbook 的記錄分析搜尋結果視。"
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
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a><span data-ttu-id="9460b-103">從 Log Analytics 記錄搜尋結果利用自動化 Runbook 採取動作</span><span class="sxs-lookup"><span data-stu-id="9460b-103">Take Action with an Automation Runbook from a Log Analytics log search result</span></span>

<span data-ttu-id="9460b-104">從 Azure Log Analytics 中的記錄搜尋結果，您現在可以選取**採取的動作**toorun 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="9460b-104">From a log search result in Azure Log Analytics, you can now select **Take action** toorun an Automation runbook.</span></span>  <span data-ttu-id="9460b-105">hello runbook 可用 tooremediate hello 問題或執行某些其他動作，例如收集疑難排解資訊、 傳送電子郵件，或建立服務要求。</span><span class="sxs-lookup"><span data-stu-id="9460b-105">hello runbook can be used tooremediate hello issue or take some other action such as collect troubleshooting information, send an email, or create a service request.</span></span> 

## <a name="components-and-features-used"></a><span data-ttu-id="9460b-106">使用的元件和功能</span><span class="sxs-lookup"><span data-stu-id="9460b-106">Components and features used</span></span>
* [<span data-ttu-id="9460b-107">Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="9460b-107">Azure Automation account</span></span>](../automation/automation-offering-get-started.md)
* [<span data-ttu-id="9460b-108">Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="9460b-108">Log Analytics workspace</span></span>](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a><span data-ttu-id="9460b-109">從記錄檔搜尋 tooinitiate runbook</span><span class="sxs-lookup"><span data-stu-id="9460b-109">tooinitiate runbook from log search</span></span>

<span data-ttu-id="9460b-110">您開始建立記錄檔搜尋 tootake 事件和啟動 runbook，以從您的記錄搜尋結果的動作，，並從 hello 結果叫用 runbook 隨。</span><span class="sxs-lookup"><span data-stu-id="9460b-110">tootake action on an event and initiate a runbook from your log search results, you start by creating a log search and from hello results you can invoke a runbook on-demand.</span></span>  <span data-ttu-id="9460b-111">這可以從 hello Azure 中的 hello 記錄搜尋功能來達成或[OMS 入口網站](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="9460b-111">This can be achieved from hello log search feature in hello Azure or [OMS portal](../log-analytics/log-analytics-log-searches.md).</span></span>  <span data-ttu-id="9460b-112">在此範例中，我們會從 hello 與基本示範這項功能的 Azure 入口網站執行記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="9460b-112">In this example, we perform a log search from hello Azure portal with a basic demonstration of this feature.</span></span>

1. <span data-ttu-id="9460b-113">在 hello Azure 入口網站，hello 中樞功能表上按一下 **更多服務**選取**記錄分析**。</span><span class="sxs-lookup"><span data-stu-id="9460b-113">In hello Azure portal, on hello Hub menu click **More services** and select **Log Analytics**.</span></span>  
2. <span data-ttu-id="9460b-114">在 hello 記錄分析刀鋒視窗中，選取您的記錄分析工作區，hello 工作區刀鋒視窗上選取**記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="9460b-114">On hello Log Analytics blade, select your Log Analytics workspace and on hello workspace blade select **Log Search**.</span></span>  
3. <span data-ttu-id="9460b-115">Hello 記錄搜尋 刀鋒視窗中，執行記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="9460b-115">On hello Log Search blade, perform a log search.</span></span>  
4. <span data-ttu-id="9460b-116">從 hello 記錄搜尋結果中，按一下 hello 橢圓形 toohello 左邊的 hello 欄位，並從 hello 快顯視窗，選取一個**採取的動作**。</span><span class="sxs-lookup"><span data-stu-id="9460b-116">From hello log search results, click hello ellipse toohello left of one of hello fields and from hello popup, select **Take action on**.</span></span><br><br> <span data-ttu-id="9460b-117">![從搜尋結果中選取採取動作](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span><span class="sxs-lookup"><span data-stu-id="9460b-117">![Select Take Action from search result](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png)</span></span> 
5. <span data-ttu-id="9460b-118">從 hello 採取動作刀鋒視窗中，選取**執行 runbook**，在 hello**執行 runbook**刀鋒視窗，您可以選取 runbook toorun。</span><span class="sxs-lookup"><span data-stu-id="9460b-118">From hello Take action blade, select **Run a runbook**, and on hello **Run a runbook** blade you can select a runbook toorun.</span></span>  <span data-ttu-id="9460b-119">您可以選取任何 runbook 中 hello 是連結的 toohello 記錄分析工作區的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9460b-119">You can select any runbook in hello Automation account that is linked toohello Log Analytics workspace.</span></span>  <span data-ttu-id="9460b-120">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9460b-120">Note hello following:</span></span>

    * <span data-ttu-id="9460b-121">Runbook 是依標籤來組織。</span><span class="sxs-lookup"><span data-stu-id="9460b-121">Runbooks are organized by tags</span></span>
    * <span data-ttu-id="9460b-122">Runbook 輸入的參數值可以直接從 hello 搜尋結果的 hello 欄位中選取。</span><span class="sxs-lookup"><span data-stu-id="9460b-122">Runbook input parameter values can be selected directly from hello fields of hello search result.</span></span>  <span data-ttu-id="9460b-123">顯示所有 hello 可用的欄位從 hello 結果 tooselect 即會出現下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9460b-123">A drop-down list will appear displaying all hello available fields from hello result tooselect from.</span></span>  
    * <span data-ttu-id="9460b-124">您也可以選擇 toorun hello runbook 上[混合式 runbook 背景工作](../automation/automation-hybrid-runbook-worker.md)您已安裝在具有 hello 問題，如果您有對應的混合式 Runbook 背景工作群組只包含該機器為成員的 hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="9460b-124">You can choose toorun hello runbook on a [hybrid runbook worker](../automation/automation-hybrid-runbook-worker.md) that you have installed on hello machine that has hello issue if you have a corresponding Hybrid Runbook Worker group that only contains this machine as a member.</span></span>  <span data-ttu-id="9460b-125">如果 hello hello Hybrid Worker 群組名稱符合 hello hello 記錄搜尋結果中的 hello 電腦名稱，然後會自動選取 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="9460b-125">If hello name of hello Hybrid Worker group matches hello name of hello computer that is in hello log search result, then hello group is selected automatically.</span></span>    

6. <span data-ttu-id="9460b-126">按一下 之後**執行**，hello runbook 作業刀鋒視窗會開啟 tooallow 您 tooreview hello hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="9460b-126">After you click **Run**, hello runbook job blade will open tooallow you tooreview hello status of hello job.</span></span>   

<span data-ttu-id="9460b-127">如果您選取的 runbook 時設定的 toobe[記錄分析警示從呼叫](../automation/automation-invoke-runbook-from-omsla-alert.md)，它有輸入的參數呼叫**WebhookData**也就是**物件**型別。</span><span class="sxs-lookup"><span data-stu-id="9460b-127">If you select a runbook that was configured toobe [called from a Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md), it has an input parameter called **WebhookData** that is **Object** type.</span></span>  <span data-ttu-id="9460b-128">如果 hello 輸入的參數是必要的因此它可以將 hello JSON 格式化字串轉換成物件類型可讓您將 runbook 活動中參照的特定項目上的 toofilter 需要 toopass hello 搜尋結果 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="9460b-128">If hello input parameter is mandatory, you need toopass hello search results toohello runbook so it can convert hello JSON-formatted string into an object type allowing you toofilter on specific items that you will reference in runbook activities.</span></span>  <span data-ttu-id="9460b-129">您可以選取**搜尋結果 （物件）** hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="9460b-129">You do this by selecting **Search result (Object)** from hello drop-down list.</span></span><br><br> <span data-ttu-id="9460b-130">![選取 Webhook 資料物件給 Runbook 參數](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span><span class="sxs-lookup"><span data-stu-id="9460b-130">![Select Webhook data object for runbook parameter](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)</span></span>   
    
## <a name="next-steps"></a><span data-ttu-id="9460b-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9460b-131">Next steps</span></span>

* <span data-ttu-id="9460b-132">檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)tooview hello 的所有搜尋欄位和 facet 用於記錄分析。</span><span class="sxs-lookup"><span data-stu-id="9460b-132">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
* <span data-ttu-id="9460b-133">toolearn tooinvoke 自動化 runbook 自動檢閱[呼叫 Azure 自動化 runbook 從 OMS 記錄分析警示](../automation/automation-invoke-runbook-from-omsla-alert.md)。</span><span class="sxs-lookup"><span data-stu-id="9460b-133">toolearn how tooinvoke an Automation runbook automatically, review [calling an Azure Automation runbook from an OMS Log Analytics alert](../automation/automation-invoke-runbook-from-omsla-alert.md).</span></span>  
