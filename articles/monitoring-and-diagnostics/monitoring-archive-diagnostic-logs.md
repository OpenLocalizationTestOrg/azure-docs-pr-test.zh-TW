---
title: "封存 Azure 診斷記錄 | Microsoft Docs"
description: "了解如何封存 Azure 診斷記錄以在儲存體帳戶中長期保存。"
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
ms.openlocfilehash: dbc5f89001dcb6cd1ab061cb0a9632e4e5d2c1c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="a2911-103">封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="a2911-104">在本文中，我們會示範如何使用 Azure 入口網站、PowerShell Cmdlet、CLI 或 REST API 來封存儲存體帳戶中的 [Azure 診斷記錄](monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="a2911-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="a2911-105">如果您想要使用適用於稽核、靜態分析或備份的選用保留原則來保留診斷記錄，這個選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="a2911-105">This option is useful if you would like to retain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="a2911-106">儲存體帳戶不一定要和資源發出記錄檔屬於相同的訂用帳戶，只要使用者有適當的設定可 RBAC 存取這兩個訂用帳戶即可。</span><span class="sxs-lookup"><span data-stu-id="a2911-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2911-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a2911-107">Prerequisites</span></span>
<span data-ttu-id="a2911-108">在開始之前，您需要[建立儲存體帳戶](../storage/storage-create-storage-account.md)，以便將診斷記錄封存至其中。</span><span class="sxs-lookup"><span data-stu-id="a2911-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md) to which you can archive your diagnostic logs.</span></span> <span data-ttu-id="a2911-109">我們強烈建議您不要使用已儲存了其他非監視資料的現有儲存體帳戶，這樣您對監視資料才能有更好的存取控制。</span><span class="sxs-lookup"><span data-stu-id="a2911-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="a2911-110">不過，如果您也要封存活動記錄和診斷度量至儲存體帳戶，則將同一儲存體帳戶用於診斷記錄合情合理，因為可以將所有監視資料集中在一個位置。</span><span class="sxs-lookup"><span data-stu-id="a2911-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your diagnostic logs as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="a2911-111">您使用的儲存體帳戶必須是一般用途的儲存體帳戶，不可以是 blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2911-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="a2911-112">診斷設定</span><span class="sxs-lookup"><span data-stu-id="a2911-112">Diagnostic settings</span></span>
<span data-ttu-id="a2911-113">若要使用下列任何方法封存診斷記錄，您必須為特定資源設定**診斷設定**。</span><span class="sxs-lookup"><span data-stu-id="a2911-113">To archive your diagnostic logs using any of the methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="a2911-114">資源的診斷設定會定義要傳送至目的地 (儲存體帳戶、事件中樞命名空間或 Log Analytics) 的記錄類別與計量資料。</span><span class="sxs-lookup"><span data-stu-id="a2911-114">A diagnostic setting for a resource defines the categories of logs and metric data sent to a destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="a2911-115">它也會定義儲存在儲存體帳戶中每個記錄類別之事件和計量資料的保留原則 (保留的天數)。</span><span class="sxs-lookup"><span data-stu-id="a2911-115">It also defines the retention policy (number of days to retain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="a2911-116">如果保留原則設定為零，則會無限期地 (亦即永遠) 儲存該記錄類別的事件。</span><span class="sxs-lookup"><span data-stu-id="a2911-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span></span> <span data-ttu-id="a2911-117">否則，保留原則可以是 1 到 2147483647 之間的任何天數。</span><span class="sxs-lookup"><span data-stu-id="a2911-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="a2911-118">[您可以在此深入了解診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。</span><span class="sxs-lookup"><span data-stu-id="a2911-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="a2911-119">保留原則是每天套用，因此在一天結束時 (UTC)，這一天超過保留原則的記錄檔將被刪除。</span><span class="sxs-lookup"><span data-stu-id="a2911-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="a2911-120">例如，如果您的保留原則為一天，在今天一開始，昨天之前的記錄檔會被刪除</span><span class="sxs-lookup"><span data-stu-id="a2911-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-the-portal"></a><span data-ttu-id="a2911-121">使用入口網站封存診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-121">Archive diagnostic logs using the portal</span></span>
1. <span data-ttu-id="a2911-122">在入口網站中，瀏覽至 Azure 監視器，然後按一下 [診斷設定]</span><span class="sxs-lookup"><span data-stu-id="a2911-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure 監視器的監視區段](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="a2911-124">選擇性地依資源群組或資源類型篩選清單，然後按一下您要設定診斷設定的資源。</span><span class="sxs-lookup"><span data-stu-id="a2911-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="a2911-125">如果您選取的資源上沒有任何設定，系統會提示您建立設定。</span><span class="sxs-lookup"><span data-stu-id="a2911-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="a2911-126">按一下「開啟診斷」。</span><span class="sxs-lookup"><span data-stu-id="a2911-126">Click "Turn on diagnostics."</span></span>

   ![新增診斷設定 - 無現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="a2911-128">如果資源上已有設定，您將會看此資源上已設定的設定清單。</span><span class="sxs-lookup"><span data-stu-id="a2911-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="a2911-129">按一下「新增診斷設定」。</span><span class="sxs-lookup"><span data-stu-id="a2911-129">Click "Add diagnostic setting."</span></span>

   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="a2911-131">為您的設定提供名稱，並勾選 [匯出到儲存體帳戶] 核取方塊，然後選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2911-131">Give your setting a name and check the box for **Export to Storage Account**, then select a storage account.</span></span> <span data-ttu-id="a2911-132">使用 [保留 (天)]  滑桿選擇性地設定這些記錄的保留天數。</span><span class="sxs-lookup"><span data-stu-id="a2911-132">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span></span> <span data-ttu-id="a2911-133">保留天數為 0 會無限期地儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="a2911-133">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="a2911-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a2911-135">Click **Save**.</span></span>

<span data-ttu-id="a2911-136">過了幾分鐘之後，新的設定就會出現在此資源的設定清單中，而且每次產生新的事件資料，都會將診斷記錄封存至該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2911-136">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are archived to that storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="a2911-137">透過 Azure PowerShell 封存診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="a2911-138">屬性</span><span class="sxs-lookup"><span data-stu-id="a2911-138">Property</span></span> | <span data-ttu-id="a2911-139">必要</span><span class="sxs-lookup"><span data-stu-id="a2911-139">Required</span></span> | <span data-ttu-id="a2911-140">說明</span><span class="sxs-lookup"><span data-stu-id="a2911-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2911-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a2911-141">ResourceId</span></span> |<span data-ttu-id="a2911-142">是</span><span class="sxs-lookup"><span data-stu-id="a2911-142">Yes</span></span> |<span data-ttu-id="a2911-143">要對其設定診斷設定之資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="a2911-143">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="a2911-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="a2911-144">StorageAccountId</span></span> |<span data-ttu-id="a2911-145">否</span><span class="sxs-lookup"><span data-stu-id="a2911-145">No</span></span> |<span data-ttu-id="a2911-146">資源識別碼，診斷記錄應該要儲存至此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2911-146">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="a2911-147">類別</span><span class="sxs-lookup"><span data-stu-id="a2911-147">Categories</span></span> |<span data-ttu-id="a2911-148">否</span><span class="sxs-lookup"><span data-stu-id="a2911-148">No</span></span> |<span data-ttu-id="a2911-149">要啟用之記錄類別的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="a2911-149">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="a2911-150">已啟用</span><span class="sxs-lookup"><span data-stu-id="a2911-150">Enabled</span></span> |<span data-ttu-id="a2911-151">是</span><span class="sxs-lookup"><span data-stu-id="a2911-151">Yes</span></span> |<span data-ttu-id="a2911-152">布林值，表示要對資源啟用還是停用診斷。</span><span class="sxs-lookup"><span data-stu-id="a2911-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="a2911-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="a2911-153">RetentionEnabled</span></span> |<span data-ttu-id="a2911-154">否</span><span class="sxs-lookup"><span data-stu-id="a2911-154">No</span></span> |<span data-ttu-id="a2911-155">布林值，表示此資源是否啟用保留原則。</span><span class="sxs-lookup"><span data-stu-id="a2911-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="a2911-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="a2911-156">RetentionInDays</span></span> |<span data-ttu-id="a2911-157">否</span><span class="sxs-lookup"><span data-stu-id="a2911-157">No</span></span> |<span data-ttu-id="a2911-158">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="a2911-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="a2911-159">值為 0 會無限期地儲存記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a2911-159">A value of zero stores the logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-the-cross-platform-cli"></a><span data-ttu-id="a2911-160">透過跨平台 CLI 封存診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-160">Archive diagnostic logs via the Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="a2911-161">屬性</span><span class="sxs-lookup"><span data-stu-id="a2911-161">Property</span></span> | <span data-ttu-id="a2911-162">必要</span><span class="sxs-lookup"><span data-stu-id="a2911-162">Required</span></span> | <span data-ttu-id="a2911-163">說明</span><span class="sxs-lookup"><span data-stu-id="a2911-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2911-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a2911-164">resourceId</span></span> |<span data-ttu-id="a2911-165">是</span><span class="sxs-lookup"><span data-stu-id="a2911-165">Yes</span></span> |<span data-ttu-id="a2911-166">要對其設定診斷設定之資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="a2911-166">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="a2911-167">storageId</span><span class="sxs-lookup"><span data-stu-id="a2911-167">storageId</span></span> |<span data-ttu-id="a2911-168">否</span><span class="sxs-lookup"><span data-stu-id="a2911-168">No</span></span> |<span data-ttu-id="a2911-169">資源識別碼，診斷記錄應該要儲存至此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2911-169">Resource ID of the Storage Account to which diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="a2911-170">類別</span><span class="sxs-lookup"><span data-stu-id="a2911-170">categories</span></span> |<span data-ttu-id="a2911-171">否</span><span class="sxs-lookup"><span data-stu-id="a2911-171">No</span></span> |<span data-ttu-id="a2911-172">要啟用之記錄類別的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="a2911-172">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="a2911-173">已啟用</span><span class="sxs-lookup"><span data-stu-id="a2911-173">enabled</span></span> |<span data-ttu-id="a2911-174">是</span><span class="sxs-lookup"><span data-stu-id="a2911-174">Yes</span></span> |<span data-ttu-id="a2911-175">布林值，表示要對資源啟用還是停用診斷。</span><span class="sxs-lookup"><span data-stu-id="a2911-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-the-rest-api"></a><span data-ttu-id="a2911-176">透過 REST API 封存診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-176">Archive diagnostic logs via the REST API</span></span>
<span data-ttu-id="a2911-177">[請參閱本文件](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)，以取得如何使用 Azure 監視器 REST API 設定診斷設定的資訊。</span><span class="sxs-lookup"><span data-stu-id="a2911-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="a2911-178">儲存體帳戶中的診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="a2911-178">Schema of diagnostic logs in the storage account</span></span>
<span data-ttu-id="a2911-179">設定了封存之後，便會在已啟用的其中一個記錄類別發生事件時，立即於儲存體帳戶中建立儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="a2911-179">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span></span> <span data-ttu-id="a2911-180">容器內的 Blob 的診斷記錄和活動記錄會遵循相同的格式。</span><span class="sxs-lookup"><span data-stu-id="a2911-180">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span></span> <span data-ttu-id="a2911-181">這些 blob 的結構為：</span><span class="sxs-lookup"><span data-stu-id="a2911-181">The structure of these blobs is:</span></span>

> <span data-ttu-id="a2911-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="a2911-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="a2911-183">或者，形式更簡單，</span><span class="sxs-lookup"><span data-stu-id="a2911-183">Or, more simply,</span></span>

> <span data-ttu-id="a2911-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="a2911-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="a2911-185">例如，blob 名稱可能是︰</span><span class="sxs-lookup"><span data-stu-id="a2911-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="a2911-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="a2911-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="a2911-187">每個 PT1H.json blob 有一個 JSON blob，包含在 blob URL 指定時數內 (例如 h = 12) 發生的事件。</span><span class="sxs-lookup"><span data-stu-id="a2911-187">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="a2911-188">在目前這一小時，事件一發生就會附加到 PT1H.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2911-188">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="a2911-189">分鐘值 (m = 00) 一定是 00，因為診斷記錄事件是分成每小時的個別 blob。</span><span class="sxs-lookup"><span data-stu-id="a2911-189">The minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="a2911-190">在 PT1H.json 檔案中，每個事件會以下列格式儲存在 “records” 陣列︰</span><span class="sxs-lookup"><span data-stu-id="a2911-190">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

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

| <span data-ttu-id="a2911-191">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a2911-191">Element name</span></span> | <span data-ttu-id="a2911-192">說明</span><span class="sxs-lookup"><span data-stu-id="a2911-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2911-193">分析</span><span class="sxs-lookup"><span data-stu-id="a2911-193">time</span></span> |<span data-ttu-id="a2911-194">處理與事件對應之要求的Azure 服務產生事件時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="a2911-194">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="a2911-195">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a2911-195">resourceId</span></span> |<span data-ttu-id="a2911-196">受影響資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="a2911-196">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="a2911-197">operationName</span><span class="sxs-lookup"><span data-stu-id="a2911-197">operationName</span></span> |<span data-ttu-id="a2911-198">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="a2911-198">Name of the operation.</span></span> |
| <span data-ttu-id="a2911-199">category</span><span class="sxs-lookup"><span data-stu-id="a2911-199">category</span></span> |<span data-ttu-id="a2911-200">事件的記錄類別。</span><span class="sxs-lookup"><span data-stu-id="a2911-200">Log category of the event.</span></span> |
| <span data-ttu-id="a2911-201">properties</span><span class="sxs-lookup"><span data-stu-id="a2911-201">properties</span></span> |<span data-ttu-id="a2911-202">描述事件詳細資料的一組 `<Key, Value>` 配對 (也就是字典)。</span><span class="sxs-lookup"><span data-stu-id="a2911-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="a2911-203">屬性和這些屬性的使用方式，依資源而異。</span><span class="sxs-lookup"><span data-stu-id="a2911-203">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a2911-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2911-204">Next steps</span></span>
* [<span data-ttu-id="a2911-205">下載 blob 以供分析</span><span class="sxs-lookup"><span data-stu-id="a2911-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="a2911-206">將診斷記錄串流至事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="a2911-206">Stream diagnostic logs to an Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="a2911-207">深入了解診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a2911-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
