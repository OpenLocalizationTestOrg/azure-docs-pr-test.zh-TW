---
title: "aaaArchive Azure 診斷記錄檔 |Microsoft 文件"
description: "了解如何 tooarchive 您 Azure 診斷記錄供長期保存在儲存體帳戶。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="aa030-103">封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="aa030-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="aa030-104">在本文中，我們示範如何使用 hello Azure 入口網站、 PowerShell Cmdlet，CLI，或 REST API tooarchive 您[Azure 診斷的記錄檔](monitoring-overview-of-diagnostic-logs.md)儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="aa030-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, CLI, or REST API tooarchive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="aa030-105">這個選項非常有用，如果您想要的 tooretain 您診斷記錄與稽核、 靜態分析或備份的選擇性的保留原則。</span><span class="sxs-lookup"><span data-stu-id="aa030-105">This option is useful if you would like tooretain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="aa030-106">hello 儲存體帳戶中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 資源相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa030-106">hello storage account does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa030-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="aa030-107">Prerequisites</span></span>
<span data-ttu-id="aa030-108">在開始之前，您需要太[建立儲存體帳戶](../storage/storage-create-storage-account.md)toowhich 可以保存您的診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa030-108">Before you begin, you need too[create a storage account](../storage/storage-create-storage-account.md) toowhich you can archive your diagnostic logs.</span></span> <span data-ttu-id="aa030-109">我們強烈建議您務必使用現有的儲存體帳戶具有其他非監視資料，讓您更能夠控制存取 toomonitoring 資料儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="aa030-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="aa030-110">不過，如果您的活動記錄檔和診斷度量 tooa 儲存體帳戶時，您也要封存，它會使意義 toouse 該儲存體帳戶您診斷記錄檔以及 tookeep 監視的所有資料在集中位置。</span><span class="sxs-lookup"><span data-stu-id="aa030-110">However, if you are also archiving your Activity Log and diagnostic metrics tooa storage account, it may make sense toouse that storage account for your diagnostic logs as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="aa030-111">您使用的 hello 儲存體帳戶必須是一般用途儲存體帳戶，而不是 blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa030-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="aa030-112">診斷設定</span><span class="sxs-lookup"><span data-stu-id="aa030-112">Diagnostic settings</span></span>
<span data-ttu-id="aa030-113">設定您的診斷記錄使用任何下列的 hello 方法 tooarchive，**診斷設定**特定資源。</span><span class="sxs-lookup"><span data-stu-id="aa030-113">tooarchive your diagnostic logs using any of hello methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="aa030-114">資源的診斷設定定義 hello 類別的記錄檔和度量資料傳送 tooa 目的地 （儲存體帳戶、 事件中樞命名空間或記錄分析）。</span><span class="sxs-lookup"><span data-stu-id="aa030-114">A diagnostic setting for a resource defines hello categories of logs and metric data sent tooa destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="aa030-115">它也會定義事件的每個記錄檔類別目錄和度量資料儲存在儲存體帳戶中的 hello 保留原則 （天 tooretain 數目）。</span><span class="sxs-lookup"><span data-stu-id="aa030-115">It also defines hello retention policy (number of days tooretain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="aa030-116">如果 toozero 設定保留原則，該記錄檔類別目錄的事件會無限期地儲存 （亦即 toosay，不限次數）。</span><span class="sxs-lookup"><span data-stu-id="aa030-116">If a retention policy is set toozero, events for that log category are stored indefinitely (that is toosay, forever).</span></span> <span data-ttu-id="aa030-117">否則，保留原則可以是 1 到 2147483647 之間的任何天數。</span><span class="sxs-lookup"><span data-stu-id="aa030-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="aa030-118">[您可以在此深入了解診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。</span><span class="sxs-lookup"><span data-stu-id="aa030-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="aa030-119">保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則將會被刪除。</span><span class="sxs-lookup"><span data-stu-id="aa030-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="aa030-120">例如，如果您在一天的保留原則，在今天 hello 天 hello 開頭 hello hello 天前昨天的記錄檔，就會刪除</span><span class="sxs-lookup"><span data-stu-id="aa030-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="aa030-121">封存使用 hello 入口網站的診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="aa030-121">Archive diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="aa030-122">在 hello 入口網站中，瀏覽 tooAzure 監視器並按一下**診斷設定**</span><span class="sxs-lookup"><span data-stu-id="aa030-122">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure 監視器的監視區段](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="aa030-124">選擇性地篩選資源群組或資源類型的 hello 清單，然後按一下 hello 資源，您想要 tooset 診斷設定。</span><span class="sxs-lookup"><span data-stu-id="aa030-124">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="aa030-125">如果您選取的 hello 資源上有沒有設定，您必須提示的 toocreate 設定。</span><span class="sxs-lookup"><span data-stu-id="aa030-125">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="aa030-126">按一下「開啟診斷」。</span><span class="sxs-lookup"><span data-stu-id="aa030-126">Click "Turn on diagnostics."</span></span>

   ![新增診斷設定 - 無現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="aa030-128">如果 hello 資源上的現有設定，您會看到已設定此資源上設定的清單。</span><span class="sxs-lookup"><span data-stu-id="aa030-128">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="aa030-129">按一下「新增診斷設定」。</span><span class="sxs-lookup"><span data-stu-id="aa030-129">Click "Add diagnostic setting."</span></span>

   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="aa030-131">提供設定名稱，並核取方塊 hello**匯出 tooStorage 帳戶**，然後選取 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa030-131">Give your setting a name and check hello box for **Export tooStorage Account**, then select a storage account.</span></span> <span data-ttu-id="aa030-132">（選擇性） 設定的天數 tooretain 數，這些記錄檔使用 hello**保留 （天）**滑桿。</span><span class="sxs-lookup"><span data-stu-id="aa030-132">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders.</span></span> <span data-ttu-id="aa030-133">保留的天數零會無限期儲存 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa030-133">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="aa030-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="aa030-135">Click **Save**.</span></span>

<span data-ttu-id="aa030-136">在幾分鐘之後, hello 新設定，會出現在此資源，設定的清單，且診斷記錄檔是封存的 toothat 儲存體帳戶只要產生新的事件資料。</span><span class="sxs-lookup"><span data-stu-id="aa030-136">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are archived toothat storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="aa030-137">透過 Azure PowerShell 封存診斷記錄</span><span class="sxs-lookup"><span data-stu-id="aa030-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="aa030-138">屬性</span><span class="sxs-lookup"><span data-stu-id="aa030-138">Property</span></span> | <span data-ttu-id="aa030-139">必要</span><span class="sxs-lookup"><span data-stu-id="aa030-139">Required</span></span> | <span data-ttu-id="aa030-140">說明</span><span class="sxs-lookup"><span data-stu-id="aa030-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aa030-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="aa030-141">ResourceId</span></span> |<span data-ttu-id="aa030-142">是</span><span class="sxs-lookup"><span data-stu-id="aa030-142">Yes</span></span> |<span data-ttu-id="aa030-143">您想要在其上 tooset 診斷設定的 hello 資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa030-143">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="aa030-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="aa030-144">StorageAccountId</span></span> |<span data-ttu-id="aa030-145">否</span><span class="sxs-lookup"><span data-stu-id="aa030-145">No</span></span> |<span data-ttu-id="aa030-146">應該儲存 hello 儲存體帳戶 toowhich 診斷記錄檔的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa030-146">Resource ID of hello Storage Account toowhich Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="aa030-147">類別</span><span class="sxs-lookup"><span data-stu-id="aa030-147">Categories</span></span> |<span data-ttu-id="aa030-148">否</span><span class="sxs-lookup"><span data-stu-id="aa030-148">No</span></span> |<span data-ttu-id="aa030-149">以逗號分隔的記錄檔分類 tooenable 清單。</span><span class="sxs-lookup"><span data-stu-id="aa030-149">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="aa030-150">已啟用</span><span class="sxs-lookup"><span data-stu-id="aa030-150">Enabled</span></span> |<span data-ttu-id="aa030-151">是</span><span class="sxs-lookup"><span data-stu-id="aa030-151">Yes</span></span> |<span data-ttu-id="aa030-152">布林值，表示要對資源啟用還是停用診斷。</span><span class="sxs-lookup"><span data-stu-id="aa030-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="aa030-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="aa030-153">RetentionEnabled</span></span> |<span data-ttu-id="aa030-154">否</span><span class="sxs-lookup"><span data-stu-id="aa030-154">No</span></span> |<span data-ttu-id="aa030-155">布林值，表示此資源是否啟用保留原則。</span><span class="sxs-lookup"><span data-stu-id="aa030-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="aa030-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="aa030-156">RetentionInDays</span></span> |<span data-ttu-id="aa030-157">否</span><span class="sxs-lookup"><span data-stu-id="aa030-157">No</span></span> |<span data-ttu-id="aa030-158">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="aa030-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="aa030-159">值為 0 會無限期儲存 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa030-159">A value of zero stores hello logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a><span data-ttu-id="aa030-160">封存 hello 跨平台 CLI 透過診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="aa030-160">Archive diagnostic logs via hello Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="aa030-161">屬性</span><span class="sxs-lookup"><span data-stu-id="aa030-161">Property</span></span> | <span data-ttu-id="aa030-162">必要</span><span class="sxs-lookup"><span data-stu-id="aa030-162">Required</span></span> | <span data-ttu-id="aa030-163">說明</span><span class="sxs-lookup"><span data-stu-id="aa030-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aa030-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="aa030-164">resourceId</span></span> |<span data-ttu-id="aa030-165">是</span><span class="sxs-lookup"><span data-stu-id="aa030-165">Yes</span></span> |<span data-ttu-id="aa030-166">您想要在其上 tooset 診斷設定的 hello 資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa030-166">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="aa030-167">storageId</span><span class="sxs-lookup"><span data-stu-id="aa030-167">storageId</span></span> |<span data-ttu-id="aa030-168">否</span><span class="sxs-lookup"><span data-stu-id="aa030-168">No</span></span> |<span data-ttu-id="aa030-169">應該儲存 hello 儲存體帳戶 toowhich 診斷記錄檔的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa030-169">Resource ID of hello Storage Account toowhich diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="aa030-170">類別</span><span class="sxs-lookup"><span data-stu-id="aa030-170">categories</span></span> |<span data-ttu-id="aa030-171">否</span><span class="sxs-lookup"><span data-stu-id="aa030-171">No</span></span> |<span data-ttu-id="aa030-172">以逗號分隔的記錄檔分類 tooenable 清單。</span><span class="sxs-lookup"><span data-stu-id="aa030-172">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="aa030-173">已啟用</span><span class="sxs-lookup"><span data-stu-id="aa030-173">enabled</span></span> |<span data-ttu-id="aa030-174">是</span><span class="sxs-lookup"><span data-stu-id="aa030-174">Yes</span></span> |<span data-ttu-id="aa030-175">布林值，表示要對資源啟用還是停用診斷。</span><span class="sxs-lookup"><span data-stu-id="aa030-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a><span data-ttu-id="aa030-176">封存透過 hello REST API 的診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="aa030-176">Archive diagnostic logs via hello REST API</span></span>
<span data-ttu-id="aa030-177">[請參閱本文件](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)有關您可以設定使用 hello Azure 監視 REST API 的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="aa030-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using hello Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="aa030-178">Hello 儲存體帳戶中的診斷記錄檔的結構描述</span><span class="sxs-lookup"><span data-stu-id="aa030-178">Schema of diagnostic logs in hello storage account</span></span>
<span data-ttu-id="aa030-179">在您設定保存，儲存體容器被建立 hello 儲存體帳戶中，只要您已啟用的 hello 記錄類別的其中一個發生的事件。</span><span class="sxs-lookup"><span data-stu-id="aa030-179">Once you have set up archival, a storage container is created in hello storage account as soon as an event occurs in one of hello log categories you have enabled.</span></span> <span data-ttu-id="aa030-180">相同跨診斷記錄檔格式的 hello 與 hello 活動記錄檔，請依照下列 hello hello 容器內的 blob。</span><span class="sxs-lookup"><span data-stu-id="aa030-180">hello blobs within hello container follow hello same format across Diagnostic Logs and hello Activity Log.</span></span> <span data-ttu-id="aa030-181">這些 blob hello 結構是：</span><span class="sxs-lookup"><span data-stu-id="aa030-181">hello structure of these blobs is:</span></span>

> <span data-ttu-id="aa030-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="aa030-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="aa030-183">或者，形式更簡單，</span><span class="sxs-lookup"><span data-stu-id="aa030-183">Or, more simply,</span></span>

> <span data-ttu-id="aa030-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="aa030-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="aa030-185">例如，blob 名稱可能是︰</span><span class="sxs-lookup"><span data-stu-id="aa030-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="aa030-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="aa030-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="aa030-187">每個 PT1H.json blob 包含 JSON blob hello hello blob URL 中指定的一小時內發生的事件 (例如，h = 12)。</span><span class="sxs-lookup"><span data-stu-id="aa030-187">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (for example, h=12).</span></span> <span data-ttu-id="aa030-188">Hello 存在小時，在事件發生時是附加的 toohello PT1H.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa030-188">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="aa030-189">hello 分鐘值 (m = 00) 一定是 00，因為診斷記錄檔事件會分為個別每小時的 blob。</span><span class="sxs-lookup"><span data-stu-id="aa030-189">hello minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="aa030-190">在 hello PT1H.json 檔案中，每個事件會儲存在 hello 「 記錄 」 陣列中，遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="aa030-190">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="aa030-191">元素名稱</span><span class="sxs-lookup"><span data-stu-id="aa030-191">Element name</span></span> | <span data-ttu-id="aa030-192">說明</span><span class="sxs-lookup"><span data-stu-id="aa030-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa030-193">分析</span><span class="sxs-lookup"><span data-stu-id="aa030-193">time</span></span> |<span data-ttu-id="aa030-194">Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="aa030-194">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="aa030-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="aa030-195">resourceId</span></span> |<span data-ttu-id="aa030-196">資源識別碼 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="aa030-196">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="aa030-197">operationName</span><span class="sxs-lookup"><span data-stu-id="aa030-197">operationName</span></span> |<span data-ttu-id="aa030-198">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa030-198">Name of hello operation.</span></span> |
| <span data-ttu-id="aa030-199">category</span><span class="sxs-lookup"><span data-stu-id="aa030-199">category</span></span> |<span data-ttu-id="aa030-200">Hello 事件記錄檔類別目錄。</span><span class="sxs-lookup"><span data-stu-id="aa030-200">Log category of hello event.</span></span> |
| <span data-ttu-id="aa030-201">屬性</span><span class="sxs-lookup"><span data-stu-id="aa030-201">properties</span></span> |<span data-ttu-id="aa030-202">一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aa030-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="aa030-203">hello 屬性和這些屬性的使用方式有所不同 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="aa030-203">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="aa030-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa030-204">Next steps</span></span>
* [<span data-ttu-id="aa030-205">下載 blob 以供分析</span><span class="sxs-lookup"><span data-stu-id="aa030-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="aa030-206">資料流診斷記錄 tooan 事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="aa030-206">Stream diagnostic logs tooan Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="aa030-207">深入了解診斷記錄</span><span class="sxs-lookup"><span data-stu-id="aa030-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
