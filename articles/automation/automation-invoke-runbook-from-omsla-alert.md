---
title: "Azure 自動化 Runbook 的記錄分析警示 aaaCalling |Microsoft 文件"
description: "本文提供的概觀 tooinvoke 自動化 runbook 從 Microsoft OMS 記錄分析警示。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a><span data-ttu-id="56f3d-103">從 OMS Log Analytics Alert 呼叫 Azure 自動化 Runbook | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="56f3d-103">Calling an Azure Automation runbook from an OMS Log Analytics alert</span></span>

<span data-ttu-id="56f3d-104">如果結果符合特定準則，例如長時間的突然增加處理器使用率 」 或 「 企業營運應用程式的特定應用程式處理序重大 toohello 功能中的警示記錄中記錄分析 toocreate 設定警示時失敗該警示可以自動執行自動化 runbook 在嘗試 tooauto hello Windows 事件記錄檔中寫入對應的事件和-補救 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="56f3d-104">When an alert is configured in Log Analytics toocreate an alert record if results match a particular criteria, such as a prolonged spike in processor utilization or a particular application process critical toohello functionality of a business application fails and writes a corresponding event in hello Windows event log, that alert can automatically run an Automation runbook in an attempt tooauto-remediate hello issue.</span></span>  

<span data-ttu-id="56f3d-105">有兩個選項 toocall runbook 設定 hello 警示時。</span><span class="sxs-lookup"><span data-stu-id="56f3d-105">There are two options toocall a runbook when configuring hello alert.</span></span>  <span data-ttu-id="56f3d-106">具體而言，</span><span class="sxs-lookup"><span data-stu-id="56f3d-106">Specifically,</span></span>

1. <span data-ttu-id="56f3d-107">使用 Webhook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-107">Using a Webhook.</span></span>
   * <span data-ttu-id="56f3d-108">如果您的 OMS 工作區不是連結的 tooan 自動化帳戶，這是 hello 唯一可用的選項。</span><span class="sxs-lookup"><span data-stu-id="56f3d-108">This is hello only option available if your OMS workspace is not linked tooan Automation account.</span></span>
   * <span data-ttu-id="56f3d-109">如果您沒有自動化帳戶連結 tooan OMS 工作區，此選項，還是可以。</span><span class="sxs-lookup"><span data-stu-id="56f3d-109">If you already have an Automation account linked tooan OMS workspace, this option is still available.</span></span>  

2. <span data-ttu-id="56f3d-110">直接選取 Runbook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-110">Select a runbook directly.</span></span>
   * <span data-ttu-id="56f3d-111">Hello OMS 工作區是連結的 tooan 自動化帳戶時，才使用此選項。</span><span class="sxs-lookup"><span data-stu-id="56f3d-111">This option is available only when hello OMS workspace is linked tooan Automation account.</span></span>  

## <a name="calling-a-runbook-using-a-webhook"></a><span data-ttu-id="56f3d-112">使用 Webhook 來呼叫 Runbook</span><span class="sxs-lookup"><span data-stu-id="56f3d-112">Calling a runbook using a webhook</span></span>

<span data-ttu-id="56f3d-113">Webhook 可讓您 toostart 特定 runbook 在 Azure 自動化中透過單一 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="56f3d-113">A webhook allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span>  <span data-ttu-id="56f3d-114">然後再設定 hello[記錄分析警示](../log-analytics/log-analytics-alerts.md#alert-rules)toocall hello runbook 使用 webhook 為警示的動作，您將需要 toofirst 建立 webhook hello runbook 將會使用這個方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="56f3d-114">Before configuring hello [Log Analytics alert](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook using a webhook as an alert action, you will need toofirst create a webhook for hello runbook that will be called using this method.</span></span>  <span data-ttu-id="56f3d-115">檢閱並遵循 hello 中的 hello 步驟[建立 webhook](automation-webhooks.md#creating-a-webhook)發行項，並記得 toorecord hello webhook URL，這樣您就可以設定 hello 警示規則時參考它。</span><span class="sxs-lookup"><span data-stu-id="56f3d-115">Review and follow hello steps in hello [create a webhook](automation-webhooks.md#creating-a-webhook) article and remember toorecord hello webhook URL so that you can reference it while configuring hello alert rule.</span></span>   

## <a name="calling-a-runbook-directly"></a><span data-ttu-id="56f3d-116">直接呼叫 Runbook</span><span class="sxs-lookup"><span data-stu-id="56f3d-116">Calling a runbook directly</span></span>

<span data-ttu-id="56f3d-117">如果您擁有 hello 自動化及控制供應項目中安裝並設定您的 OMS 工作區，設定 hello hello 警示的 Runbook 動作選項時，您可以檢視所有 runbook 從 hello**選取 runbook**下拉式清單然後選取您想 toorun 回應 toohello 警示中的 hello 特定 runbook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-117">If you have hello Automation & Control offering installed and configured in your OMS workspace, when configuring hello Runbook actions option for hello alert, you can view all runbooks from hello **Select a runbook** dropdown list and select hello specific runbook you want toorun in response toohello alert.</span></span>  <span data-ttu-id="56f3d-118">選取的 hello runbook 可以在 hello Azure 雲端或混合式 runbook 背景工作的工作區中執行。</span><span class="sxs-lookup"><span data-stu-id="56f3d-118">hello selected runbook can run in a workspace in hello Azure cloud or on a hybrid runbook worker.</span></span>  <span data-ttu-id="56f3d-119">使用 hello runbook 選項建立 hello 警示時，會建立 webhook hello runbook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-119">When hello alert is created using hello runbook option, a webhook will be created for hello runbook.</span></span>  <span data-ttu-id="56f3d-120">如果您移 toohello 自動化帳戶，並瀏覽 toohello webhook 刀鋒視窗中的 hello 選取 runbook，您可以看到 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-120">You can see hello webhook if you go toohello Automation account and navigate toohello webhook blade of hello selected runbook.</span></span>  <span data-ttu-id="56f3d-121">如果您刪除 hello 警示時，不刪除 hello webhook，但 hello 使用者可以手動刪除 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-121">If you delete hello alert, hello webhook is not deleted, but hello user can delete hello webhook manually.</span></span>  <span data-ttu-id="56f3d-122">它並不是問題，如果沒有刪除 hello webhook，它是只被遺棄項目，最後需要 toobe 刪除順序 toomaintain 組織的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="56f3d-122">It is not a problem if hello webhook is not deleted, it is just an orphaned item that will eventually need toobe deleted in order toomaintain an organized Automation account.</span></span>  

## <a name="characteristics-of-a-runbook-for-both-options"></a><span data-ttu-id="56f3d-123">Runbook 的特性 (適用於兩個選項)</span><span class="sxs-lookup"><span data-stu-id="56f3d-123">Characteristics of a runbook (for both options)</span></span>

<span data-ttu-id="56f3d-124">這兩種方法來呼叫 hello runbook 從 hello 記錄分析警示有不同的行為特性，需要 toobe 瞭解之後再設定您的警示規則。</span><span class="sxs-lookup"><span data-stu-id="56f3d-124">Both methods for calling hello runbook from hello Log Analytics alert have different behavior characteristics that need toobe understood before you configure your alert rules.</span></span>  

* <span data-ttu-id="56f3d-125">您必須擁有名為 **WebhookData** (也就是**物件**類型) 的 Runbook 輸入參數。</span><span class="sxs-lookup"><span data-stu-id="56f3d-125">You must have a runbook input parameter called **WebhookData** that is **Object** type.</span></span>  <span data-ttu-id="56f3d-126">它可以是強制性或選擇性。</span><span class="sxs-lookup"><span data-stu-id="56f3d-126">It can be mandatory or optional.</span></span>  <span data-ttu-id="56f3d-127">hello 警示傳遞 hello 搜尋結果 toohello runbook 使用此輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="56f3d-127">hello alert passes hello search results toohello runbook using this input parameter.</span></span>

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  <span data-ttu-id="56f3d-128">您必須擁有程式碼 tooconvert hello WebhookData tooa PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="56f3d-128">You must have code tooconvert hello WebhookData tooa PowerShell object.</span></span>

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    <span data-ttu-id="56f3d-129">*$SearchResults*將物件的陣列，每個物件都包含一個搜尋結果中的值的 hello 欄位</span><span class="sxs-lookup"><span data-stu-id="56f3d-129">*$SearchResults* will be an array of objects; each object contains hello fields with values from one search result</span></span>

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a><span data-ttu-id="56f3d-130">WebhookData hello webhook 選項 runbook 選項之間的不一致</span><span class="sxs-lookup"><span data-stu-id="56f3d-130">WebhookData inconsistencies between hello webhook option and runbook option</span></span>

* <span data-ttu-id="56f3d-131">設定警示的 toocall Webhook 時, 輸入 webhook URL，您建立 runbook，然後按一下 hello**測試 Webhook**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="56f3d-131">When configuring an alert toocall a Webhook, enter a webhook URL you created for a runbook, and click hello **Test Webhook** button.</span></span>  <span data-ttu-id="56f3d-132">hello 產生 WebhookData 傳送 toohello runbook 未包含*。SearchResult*或*。SearchResults*。</span><span class="sxs-lookup"><span data-stu-id="56f3d-132">hello resulting WebhookData sent toohello runbook does not contain either *.SearchResult* or *.SearchResults*.</span></span>

*  <span data-ttu-id="56f3d-133">如果您將儲存該警示，當 hello 警示觸發程序，並呼叫 hello webhook，hello WebhookData 傳送 toohello runbook 包含*。SearchResult*。</span><span class="sxs-lookup"><span data-stu-id="56f3d-133">If you save that alert, when hello alert triggers and calls hello webhook, hello WebhookData sent toohello runbook contains *.SearchResult*.</span></span>
* <span data-ttu-id="56f3d-134">如果您建立警示，並將它設定 toocall runbook （這也會建立 webhook），當 hello 警示傳送 WebhookData toohello runbook 所含的觸發程序*。SearchResults*。</span><span class="sxs-lookup"><span data-stu-id="56f3d-134">If you create an alert, and configure it toocall a runbook (which also creates a webhook), when hello alert triggers it sends WebhookData toohello runbook that contains *.SearchResults*.</span></span>

<span data-ttu-id="56f3d-135">因此在 hello 上述程式碼範例，您將需要 tooget *。SearchResult*如果 hello 警示呼叫 webhook，並將需要 tooget *。SearchResults*如果 hello 警示直接呼叫 runbook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-135">Thus in hello code example above, you will need tooget *.SearchResult* if hello alert calls a webhook, and will need tooget *.SearchResults* if hello alert calls a runbook directly.</span></span>

## <a name="example-walkthrough"></a><span data-ttu-id="56f3d-136">範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="56f3d-136">Example walkthrough</span></span>

<span data-ttu-id="56f3d-137">我們將示範如何將使用下列範例圖形化 runbook，以便啟動 Windows 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="56f3d-137">We will demonstrate how this works by using hello following example graphical runbook, which starts a Windows service.</span></span><br><br> ![啟動 Windows 服務圖形化 Runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

<span data-ttu-id="56f3d-139">hello runbook 都有一個輸入的參數型別的**物件**，而呼叫**WebhookData**並包含從 hello 警示包含傳入的 hello webhook 資料*。SearchResults*。</span><span class="sxs-lookup"><span data-stu-id="56f3d-139">hello runbook has one input parameter of type **Object** that is called **WebhookData** and includes hello webhook data passed from hello alert containing *.SearchResults*.</span></span><br><br> <span data-ttu-id="56f3d-140">![Runbook 輸入參數](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)</span><span class="sxs-lookup"><span data-stu-id="56f3d-140">![Runbook input parameters](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)</span></span><br>

<span data-ttu-id="56f3d-141">例如，在記錄分析，我們建立兩個自訂欄位， *SvcDisplayName_CF*和*SvcState_CF*，tooextract hello 服務顯示名稱和 hello hello 服務狀態 （也就是執行中或已停止）從 hello 事件寫入 toohello 系統事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="56f3d-141">For this example, in Log Analytics we created two custom fields, *SvcDisplayName_CF* and *SvcState_CF*, tooextract hello service display name and hello state of hello service (i.e. running or stopped) from hello event written toohello System event log.</span></span>  <span data-ttu-id="56f3d-142">我們以 hello 下列搜尋查詢再建立警示規則： `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` ，以便我們可以偵測 hello 列印多工緩衝處理器服務停止 hello Windows 系統上。</span><span class="sxs-lookup"><span data-stu-id="56f3d-142">We then create an alert rule with hello following search query: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` so that we can detect when hello Print Spooler service is stopped on hello Windows system.</span></span>  <span data-ttu-id="56f3d-143">它可以是任何感興趣服務的但此範例中我們會參考 hello 既存的服務 hello Windows 作業系統隨附的其中一個。</span><span class="sxs-lookup"><span data-stu-id="56f3d-143">It can be any service of interest, but for this example we are referencing one of hello pre-existing services that are included with hello Windows OS.</span></span>  <span data-ttu-id="56f3d-144">hello 警示動作是設定的 tooexecute 我們在此範例中所用的 runbook，並執行位於 hello Hybrid Runbook Worker，hello 目標系統上已啟用哪。</span><span class="sxs-lookup"><span data-stu-id="56f3d-144">hello alert action is configured tooexecute our runbook used in this example and run on hello Hybrid Runbook Worker, which are enabled on hello target systems.</span></span>   

<span data-ttu-id="56f3d-145">hello runbook 的程式碼活動**取得服務名稱從 LA**會將 hello JSON 格式化字串轉換成的物件類型和 hello 項目上的篩選器*SvcDisplayName_CF* hello tooextract hello 顯示名稱Windows 服務，並將此變數傳遞到 hello 下一個活動的 hello 服務已停止然後再嘗試 toorestart 會確認它。</span><span class="sxs-lookup"><span data-stu-id="56f3d-145">hello runbook code activity **Get Service Name from LA** will convert hello JSON-formatted string into an object type and filter on hello item *SvcDisplayName_CF* tooextract hello display name of hello Windows service and pass this onto hello next activity which will verify hello service is stopped before attempting toorestart it.</span></span>  <span data-ttu-id="56f3d-146">*SvcDisplayName_CF*是[自訂欄位](../log-analytics/log-analytics-custom-fields.md)記錄分析 toodemonstrate 中建立此範例。</span><span class="sxs-lookup"><span data-stu-id="56f3d-146">*SvcDisplayName_CF* is a [custom field](../log-analytics/log-analytics-custom-fields.md) created in Log Analytics toodemonstrate this example.</span></span>

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

<span data-ttu-id="56f3d-147">當 hello 服務停止時，記錄分析中的 hello 警示規則會偵測到相符項目觸發 hello runbook 和傳送嗨警示內容 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="56f3d-147">When hello service stops, hello alert rule in Log Analytics will detect a match and trigger hello runbook and send hello alert context toohello runbook.</span></span> <span data-ttu-id="56f3d-148">hello runbook 將會採取的動作 tooverify hello 服務已停止，和如果因此嘗試 toorestart hello 服務，並確認已正確地啟動，並輸出 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="56f3d-148">hello runbook will take action tooverify hello service is stopped, and if so attempt toorestart hello service and verify it started correctly and output hello results.</span></span>     

<span data-ttu-id="56f3d-149">或者如果您沒有自動化帳戶連結 tooyour OMS 工作區，您會設定 hello 警示規則 webhook 動作 tootrigger hello runbook 並設定 hello runbook tooconvert hello JSON 格式的字串和篩選*.SearchResult*遵循先前所述的 hello 指引。</span><span class="sxs-lookup"><span data-stu-id="56f3d-149">Alternatively if you don't have your Automation account linked tooyour OMS workspace, you would configure hello alert rule with a webhook action tootrigger hello runbook and configure hello runbook tooconvert hello JSON-formatted string and filter on *.SearchResult* following hello guidance mentioned earlier.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="56f3d-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56f3d-150">Next steps</span></span>

* <span data-ttu-id="56f3d-151">toolearn 深入了解記錄分析中的警示和如何 toocreate 其中一個，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="56f3d-151">toolearn more about alerts in Log Analytics and how toocreate one, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md).</span></span>

* <span data-ttu-id="56f3d-152">如何 tootrigger runbook 使用 webhook，請參閱的 toounderstand [Azure 自動化 webhook](automation-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="56f3d-152">toounderstand how tootrigger runbooks using a webhook, see [Azure Automation webhooks](automation-webhooks.md).</span></span>
