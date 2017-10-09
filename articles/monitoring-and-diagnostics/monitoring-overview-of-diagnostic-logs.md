---
title: "Azure 診斷記錄檔的 aaaOverview |Microsoft 文件"
description: "了解 Azure 診斷的記錄檔是什麼，以及您可以如何使用這些 toounderstand 事件內的 Azure 資源發生。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="c3258-103">收集並取用來自 Azure 資源的記錄資料</span><span class="sxs-lookup"><span data-stu-id="c3258-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="c3258-104">什麼是 Azure 資源診斷記錄</span><span class="sxs-lookup"><span data-stu-id="c3258-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="c3258-105">**Azure 資源層級的診斷記錄檔**是由資源發出記錄檔，提供豐富、 且經常 hello 該資源的作業有關的資料。</span><span class="sxs-lookup"><span data-stu-id="c3258-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="c3258-106">這些記錄檔的 hello 內容會因資源類型。</span><span class="sxs-lookup"><span data-stu-id="c3258-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="c3258-107">例如，網路安全性群組規則計數器和 Key Vault 稽核是其中兩種資源記錄類別。</span><span class="sxs-lookup"><span data-stu-id="c3258-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="c3258-108">資源層級的診斷記錄檔不同 hello[活動記錄檔](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="c3258-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="c3258-109">hello 活動記錄檔提供深入了解您訂用帳戶使用資源管理員，例如，建立虛擬機器，或刪除邏輯應用程式中的資源執行的 hello 操作。</span><span class="sxs-lookup"><span data-stu-id="c3258-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="c3258-110">hello 活動記錄檔是訂用帳戶層級記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c3258-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="c3258-111">資源層級診斷記錄可讓您深入探索在該資源本身內所執行的作業，例如從 Key Vault 取得密碼。</span><span class="sxs-lookup"><span data-stu-id="c3258-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="c3258-112">資源層級診斷記錄也與客體 OS 層級診斷記錄不同。</span><span class="sxs-lookup"><span data-stu-id="c3258-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="c3258-113">客體 OS 診斷記錄是由虛擬機器內執行的代理程式或其他支援的資源類型所收集的記錄。</span><span class="sxs-lookup"><span data-stu-id="c3258-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="c3258-114">資源層級的診斷記錄檔需要 hello Azure 平台本身，從任何代理程式並擷取特定資源的資料，而客體作業系統層級的診斷記錄檔擷取 hello 作業系統和虛擬機器上執行的應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="c3258-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="c3258-115">並非所有資源都支援 hello 資源此處所述的診斷記錄檔的新的類型。</span><span class="sxs-lookup"><span data-stu-id="c3258-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="c3258-116">本文章包含哪些資源類型支援 hello 新資源層級診斷記錄檔的區段清單。</span><span class="sxs-lookup"><span data-stu-id="c3258-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="c3258-117">資源診斷記錄與其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="c3258-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="c3258-118">資源層級診斷記錄的用途</span><span class="sxs-lookup"><span data-stu-id="c3258-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="c3258-119">以下是一些您可以執行與資源的診斷記錄檔的 hello 事項：</span><span class="sxs-lookup"><span data-stu-id="c3258-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![資源診斷記錄的邏輯位置](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="c3258-121">將它們儲存 tooa [**儲存體帳戶**](monitoring-archive-diagnostic-logs.md)稽核或手動檢查。</span><span class="sxs-lookup"><span data-stu-id="c3258-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="c3258-122">您可以指定 hello 保留時間 （以天為單位），使用**資源的診斷設定**。</span><span class="sxs-lookup"><span data-stu-id="c3258-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="c3258-123">[它們進行串流處理太**事件中心**](monitoring-stream-diagnostic-logs-to-event-hubs.md)來擷取第三方服務或自訂的分析解決方案，例如 power Bi。</span><span class="sxs-lookup"><span data-stu-id="c3258-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="c3258-124">以 [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md) 分析記錄檔</span><span class="sxs-lookup"><span data-stu-id="c3258-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="c3258-125">您可以使用儲存體帳戶，或不在事件中樞命名空間 hello 相同訂用帳戶，因為 hello 發出記錄檔的其中一個。</span><span class="sxs-lookup"><span data-stu-id="c3258-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="c3258-126">將設定 hello 設定的 hello 使用者必須擁有 hello 適當 RBAC 存取 tooboth 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3258-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="c3258-127">資源診斷設定</span><span class="sxs-lookup"><span data-stu-id="c3258-127">Resource diagnostic settings</span></span>
<span data-ttu-id="c3258-128">非計算資源的資源診斷記錄是使用資源診斷設定來設定的。</span><span class="sxs-lookup"><span data-stu-id="c3258-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="c3258-129">資源的**資源診斷設定**可控制：</span><span class="sxs-lookup"><span data-stu-id="c3258-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="c3258-130">資源診斷記錄和計量傳送至何處 (儲存體帳戶、事件中樞和/或 OMS Log Analytics)。</span><span class="sxs-lookup"><span data-stu-id="c3258-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="c3258-131">傳送何種記錄類別，以及是否也會傳送計量資料。</span><span class="sxs-lookup"><span data-stu-id="c3258-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="c3258-132">每個記錄類別應該在儲存體帳戶中保留多久</span><span class="sxs-lookup"><span data-stu-id="c3258-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="c3258-133">保留期為 0 天表示會永遠保留記錄。</span><span class="sxs-lookup"><span data-stu-id="c3258-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="c3258-134">否則，hello 值可以是任意數目的 1 到 2147483647 之間的天數。</span><span class="sxs-lookup"><span data-stu-id="c3258-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="c3258-135">如果設定保留原則，但記錄檔儲存體帳戶中已停用儲存 （例如，如果只選取事件中心 或 OMS 選項），hello 保留原則會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="c3258-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="c3258-136">保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則會刪除。</span><span class="sxs-lookup"><span data-stu-id="c3258-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="c3258-137">例如，如果您在一天的保留原則，hello 從今天 hello 日開始時 hello hello 天前昨天的記錄檔會刪除。</span><span class="sxs-lookup"><span data-stu-id="c3258-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="c3258-138">透過 hello hello Azure 入口網站中的資源的診斷設定，透過 Azure PowerShell 和 CLI 命令，或透過 hello，輕鬆地設定這些設定[Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c3258-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="c3258-139">診斷記錄檔和度量的 hello 客體 OS 層的計算資源 （例如，Vm 或服務的網狀架構） 使用[設定與選取的輸出的不同機制](../azure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="c3258-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="c3258-140">如何 tooenable 收集資源的診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="c3258-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="c3258-141">啟用資源的診斷記錄檔的集合[一部分 Resource Manager 範本中建立資源](./monitoring-enable-diagnostic-logs-using-template.md)或之後從該資源的 hello 入口網站頁面中建立資源。</span><span class="sxs-lookup"><span data-stu-id="c3258-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="c3258-142">您也可以啟用在任何時間點，使用 Azure PowerShell 或 CLI 命令，或使用 hello Azure 監視 REST API 的集合。</span><span class="sxs-lookup"><span data-stu-id="c3258-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="c3258-143">這些可能不適用直接 tooevery 資源。</span><span class="sxs-lookup"><span data-stu-id="c3258-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="c3258-144">請參閱下方的這個頁面 toounderstand 特殊步驟，可能需支付 toocertain 資源類型 hello hello 結構描述連結。</span><span class="sxs-lookup"><span data-stu-id="c3258-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="c3258-145">啟用收集資源 hello 入口網站中的診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="c3258-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="c3258-146">您可以開始收集資源 hello Azure 中的診斷記錄移 tooa 特定資源或瀏覽 tooAzure 監視器建立資源之後，入口網站。</span><span class="sxs-lookup"><span data-stu-id="c3258-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="c3258-147">tooenable 這透過 Azure 監視：</span><span class="sxs-lookup"><span data-stu-id="c3258-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="c3258-148">在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 tooAzure 監視器，然後按一下 **診斷設定**</span><span class="sxs-lookup"><span data-stu-id="c3258-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure 監視器的監視區段](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="c3258-150">選擇性地篩選資源群組或資源類型的 hello 清單，然後按一下 hello 資源，您想要 tooset 診斷設定。</span><span class="sxs-lookup"><span data-stu-id="c3258-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="c3258-151">如果您選取的 hello 資源上有沒有設定，您必須提示的 toocreate 設定。</span><span class="sxs-lookup"><span data-stu-id="c3258-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="c3258-152">按一下「開啟診斷」。</span><span class="sxs-lookup"><span data-stu-id="c3258-152">Click "Turn on diagnostics."</span></span>

   ![新增診斷設定 - 無現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="c3258-154">如果 hello 資源上的現有設定，您會看到已設定此資源上設定的清單。</span><span class="sxs-lookup"><span data-stu-id="c3258-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="c3258-155">按一下「新增診斷設定」。</span><span class="sxs-lookup"><span data-stu-id="c3258-155">Click "Add diagnostic setting."</span></span>

   ![新增診斷設定 - 現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="c3258-157">提供設定名稱，請檢查 hello 方塊，每個目的地 toowhich，toosend 資料，然後設定哪些資源是用於每個目的地。</span><span class="sxs-lookup"><span data-stu-id="c3258-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="c3258-158">（選擇性） 設定的天數 tooretain 數，這些記錄檔使用 hello**保留 （天）**滑桿 （只適用 toohello 儲存體帳戶目的地）。</span><span class="sxs-lookup"><span data-stu-id="c3258-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="c3258-159">保留的天數零會無限期儲存 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c3258-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![新增診斷設定 - 現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="c3258-161">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c3258-161">Click **Save**.</span></span>

<span data-ttu-id="c3258-162">在幾分鐘之後, hello 新設定會出現在清單中的這個資源，設定診斷記錄檔傳送 toohello 會指定目的地，只要產生新的事件資料。</span><span class="sxs-lookup"><span data-stu-id="c3258-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="c3258-163">透過 PowerShell 啟用資源診斷記錄的收集</span><span class="sxs-lookup"><span data-stu-id="c3258-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="c3258-164">透過 Azure PowerShell，下列命令使用 hello 資源診斷的記錄檔的 tooenable 集合：</span><span class="sxs-lookup"><span data-stu-id="c3258-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="c3258-165">tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="c3258-166">hello 儲存體帳戶識別碼 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c3258-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="c3258-167">tooenable 串流的診斷記錄檔 tooan 事件中樞，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="c3258-168">hello 服務匯流排規則識別碼是這種格式的字串： `{Service Bus resource ID}/authorizationrules/{key name}`。</span><span class="sxs-lookup"><span data-stu-id="c3258-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="c3258-169">tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="c3258-170">您可以取得您記錄分析工作區中使用下列命令的 hello hello 資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="c3258-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="c3258-171">您可以結合這些參數 tooenable 多個輸出選項。</span><span class="sxs-lookup"><span data-stu-id="c3258-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="c3258-172">透過 CLI 啟用資源診斷記錄的收集</span><span class="sxs-lookup"><span data-stu-id="c3258-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="c3258-173">tooenable 集合資源 hello Azure CLI 透過診斷記錄檔的使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="c3258-174">tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="c3258-175">hello 儲存體帳戶識別碼 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c3258-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="c3258-176">tooenable 串流的診斷記錄檔 tooan 事件中樞，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="c3258-177">hello 服務匯流排規則識別碼是這種格式的字串： `{Service Bus resource ID}/authorizationrules/{key name}`。</span><span class="sxs-lookup"><span data-stu-id="c3258-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="c3258-178">tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3258-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="c3258-179">您可以結合這些參數 tooenable 多個輸出選項。</span><span class="sxs-lookup"><span data-stu-id="c3258-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="c3258-180">透過 REST API 啟用資源診斷記錄的收集</span><span class="sxs-lookup"><span data-stu-id="c3258-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="c3258-181">toochange 診斷設定使用 hello Azure 監視 REST API，請參閱[這份文件](https://msdn.microsoft.com/library/azure/dn931931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c3258-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="c3258-182">管理資源 hello 入口網站中的診斷設定</span><span class="sxs-lookup"><span data-stu-id="c3258-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="c3258-183">請確定所有資源皆已設定了診斷設定。</span><span class="sxs-lookup"><span data-stu-id="c3258-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="c3258-184">瀏覽過**監視器**hello 入口網站與開啟中**診斷設定**。</span><span class="sxs-lookup"><span data-stu-id="c3258-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Hello 入口網站中的診斷記錄檔 刀鋒視窗](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="c3258-186">您可能必須 tooclick 「 多個服務 」 toofind hello 監視器 > 一節。</span><span class="sxs-lookup"><span data-stu-id="c3258-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="c3258-187">您可以在此處檢視和篩選診斷啟用後，才支援診斷設定 toosee 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="c3258-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="c3258-188">您也可以 toosee 向下鑽研，如果在資源上設定多個設定，並檢查哪一個儲存體帳戶、 事件中樞命名空間，及/或資料流向的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="c3258-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![入口網站中的診斷記錄結果](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="c3258-190">新增診斷的設定會顯示 hello 診斷設定檢視中，您可以在其中啟用、 停用，或修改您的診斷設定 hello 選取資源。</span><span class="sxs-lookup"><span data-stu-id="c3258-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="c3258-191">資源診斷記錄支援的服務、類別和結構描述</span><span class="sxs-lookup"><span data-stu-id="c3258-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="c3258-192">[請參閱本文章](monitoring-diagnostic-logs-schema.md)如需支援的服務和 hello 記錄檔分類使用這些服務結構描述的完整清單。</span><span class="sxs-lookup"><span data-stu-id="c3258-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3258-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3258-193">Next steps</span></span>

* [<span data-ttu-id="c3258-194">串流處理資源的診斷記錄檔太**事件中心**</span><span class="sxs-lookup"><span data-stu-id="c3258-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="c3258-195">變更資源使用 hello Azure 監視 REST API 的診斷設定</span><span class="sxs-lookup"><span data-stu-id="c3258-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="c3258-196">使用 Log Analytics 分析來自 Azure 儲存體的記錄</span><span class="sxs-lookup"><span data-stu-id="c3258-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
