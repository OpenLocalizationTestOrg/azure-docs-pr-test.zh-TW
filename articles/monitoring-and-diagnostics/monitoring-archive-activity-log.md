---
title: "封存 Azure 活動記錄檔 | Microsoft Docs"
description: "了解如何封存 Azure 活動記錄檔以在儲存體帳戶中長期保存。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="4e42d-103">封存 Azure 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="4e42d-104">在本文中，我們示範如何使用 Azure 入口網站、PowerShell Cmdlet 或跨平台 CLI 封存儲存體帳戶中的 [**Azure 活動記錄檔**](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="4e42d-105">如果您想要保留活動記錄檔超過 90 天 (而且對保留原則有完全的控制)，以便稽核、靜態分析或備份，這個選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="4e42d-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="4e42d-106">如果您只需要保留事件 90 天或更短，則不需要設定封存至儲存體帳戶，因為在不啟用封存的情況下，活動記錄檔就會在 Azure 平台保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="4e42d-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e42d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4e42d-107">Prerequisites</span></span>
<span data-ttu-id="4e42d-108">在開始之前，您需要 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) ，以便將活動記錄檔封存至此。</span><span class="sxs-lookup"><span data-stu-id="4e42d-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="4e42d-109">我們強烈建議您不要使用已儲存了其他非監視資料的現有儲存體帳戶，這樣您對監視資料才能有更好的存取控制。</span><span class="sxs-lookup"><span data-stu-id="4e42d-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="4e42d-110">不過，如果您也要封存診斷記錄檔和度量至儲存體帳戶，則將同一儲存體帳戶用於活動記錄檔合情合理，因為可以將所有監視資料集中在一個位置。</span><span class="sxs-lookup"><span data-stu-id="4e42d-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="4e42d-111">您使用的儲存體帳戶必須是一般用途的儲存體帳戶，不可以是 blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e42d-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="4e42d-112">儲存體帳戶不一定要和訂用帳戶發出記錄檔屬於相同的訂用帳戶，只要使用者有適當的設定可 RBAC 存取這兩個訂用帳戶即可。</span><span class="sxs-lookup"><span data-stu-id="4e42d-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="4e42d-113">記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-113">Log Profile</span></span>
<span data-ttu-id="4e42d-114">若要使用下列任一方法封存活動記錄檔，請設定訂用帳戶的 **記錄檔設定檔** 。</span><span class="sxs-lookup"><span data-stu-id="4e42d-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="4e42d-115">記錄檔的設定檔定義了要儲存或串流的事件類型以及輸出 — 儲存體帳戶和/或事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4e42d-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="4e42d-116">它也定義事件儲存在儲存體帳戶中的保留原則 (保留的天數)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="4e42d-117">如果保留原則設定為零，則會無限期地儲存事件。</span><span class="sxs-lookup"><span data-stu-id="4e42d-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="4e42d-118">否則，這可以設為介於 1 到 2147483647 之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="4e42d-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="4e42d-119">保留原則是每天套用，因此在一天結束時 (UTC)，這一天超過保留原則的記錄檔將被刪除。</span><span class="sxs-lookup"><span data-stu-id="4e42d-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="4e42d-120">例如，如果您的保留原則為一天，在今天一開始，昨天之前的記錄檔會被刪除。</span><span class="sxs-lookup"><span data-stu-id="4e42d-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="4e42d-121">[您可以至此處閱讀記錄檔設定檔的相關資訊](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="4e42d-122">使用入口網站封存活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="4e42d-123">在入口網站中，按一下左側導覽中的 [活動記錄檔]  連結。</span><span class="sxs-lookup"><span data-stu-id="4e42d-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="4e42d-124">如果您沒有看到活動記錄檔的連結，先按一下 [更多服務]  連結。</span><span class="sxs-lookup"><span data-stu-id="4e42d-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![瀏覽至活動記錄檔刀鋒視窗](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="4e42d-126">在刀鋒視窗頂端，按一下 [匯出] 。</span><span class="sxs-lookup"><span data-stu-id="4e42d-126">At the top of the blade, click **Export**.</span></span>
   
    ![按一下匯出按鈕](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="4e42d-128">在出現的刀鋒視窗中，勾選 [匯出至儲存體帳戶]  方塊，選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e42d-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![設定儲存體帳戶](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="4e42d-130">使用滑桿或文字方塊，定義活動記錄事件應該在儲存體帳戶中保留的天數。</span><span class="sxs-lookup"><span data-stu-id="4e42d-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="4e42d-131">如果您想要讓您的資料無限期保存在儲存體帳戶，將此數目設定為零。</span><span class="sxs-lookup"><span data-stu-id="4e42d-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="4e42d-132">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4e42d-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="4e42d-133">透過 PowerShell 封存活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="4e42d-134">屬性</span><span class="sxs-lookup"><span data-stu-id="4e42d-134">Property</span></span> | <span data-ttu-id="4e42d-135">必要</span><span class="sxs-lookup"><span data-stu-id="4e42d-135">Required</span></span> | <span data-ttu-id="4e42d-136">說明</span><span class="sxs-lookup"><span data-stu-id="4e42d-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e42d-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="4e42d-137">StorageAccountId</span></span> |<span data-ttu-id="4e42d-138">否</span><span class="sxs-lookup"><span data-stu-id="4e42d-138">No</span></span> |<span data-ttu-id="4e42d-139">資源識別碼，活動記錄檔應該要儲存至此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e42d-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="4e42d-140">位置</span><span class="sxs-lookup"><span data-stu-id="4e42d-140">Locations</span></span> |<span data-ttu-id="4e42d-141">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-141">Yes</span></span> |<span data-ttu-id="4e42d-142">以逗號分隔的區域清單，其中列出您要收集的活動記錄檔事件的區域。</span><span class="sxs-lookup"><span data-stu-id="4e42d-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="4e42d-143">您要檢視所有地區的清單，可以[瀏覽此頁面](https://azure.microsoft.com/en-us/regions)或使用 [Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="4e42d-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="4e42d-144">RetentionInDays</span></span> |<span data-ttu-id="4e42d-145">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-145">Yes</span></span> |<span data-ttu-id="4e42d-146">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="4e42d-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="4e42d-147">值為 0 會無限期地 (永遠) 儲存記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e42d-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="4e42d-148">類別</span><span class="sxs-lookup"><span data-stu-id="4e42d-148">Categories</span></span> |<span data-ttu-id="4e42d-149">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-149">Yes</span></span> |<span data-ttu-id="4e42d-150">以逗號分隔的類別清單，其中列出應該收集的事件類別。</span><span class="sxs-lookup"><span data-stu-id="4e42d-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="4e42d-151">可能的值有 Write、Delete、Action。</span><span class="sxs-lookup"><span data-stu-id="4e42d-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="4e42d-152">透過 CLI 封存活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="4e42d-153">屬性</span><span class="sxs-lookup"><span data-stu-id="4e42d-153">Property</span></span> | <span data-ttu-id="4e42d-154">必要</span><span class="sxs-lookup"><span data-stu-id="4e42d-154">Required</span></span> | <span data-ttu-id="4e42d-155">說明</span><span class="sxs-lookup"><span data-stu-id="4e42d-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e42d-156">名稱</span><span class="sxs-lookup"><span data-stu-id="4e42d-156">name</span></span> |<span data-ttu-id="4e42d-157">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-157">Yes</span></span> |<span data-ttu-id="4e42d-158">記錄檔設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e42d-158">Name of your log profile.</span></span> |
| <span data-ttu-id="4e42d-159">storageId</span><span class="sxs-lookup"><span data-stu-id="4e42d-159">storageId</span></span> |<span data-ttu-id="4e42d-160">否</span><span class="sxs-lookup"><span data-stu-id="4e42d-160">No</span></span> |<span data-ttu-id="4e42d-161">資源識別碼，活動記錄檔應該要儲存至此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e42d-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="4e42d-162">位置</span><span class="sxs-lookup"><span data-stu-id="4e42d-162">locations</span></span> |<span data-ttu-id="4e42d-163">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-163">Yes</span></span> |<span data-ttu-id="4e42d-164">以逗號分隔的區域清單，其中列出您要收集的活動記錄檔事件的區域。</span><span class="sxs-lookup"><span data-stu-id="4e42d-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="4e42d-165">您要檢視所有地區的清單，可以[瀏覽此頁面](https://azure.microsoft.com/en-us/regions)或使用 [Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="4e42d-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="4e42d-166">retentionInDays</span></span> |<span data-ttu-id="4e42d-167">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-167">Yes</span></span> |<span data-ttu-id="4e42d-168">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="4e42d-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="4e42d-169">值為 0 會無限期地 (永遠) 儲存記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e42d-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="4e42d-170">類別</span><span class="sxs-lookup"><span data-stu-id="4e42d-170">categories</span></span> |<span data-ttu-id="4e42d-171">是</span><span class="sxs-lookup"><span data-stu-id="4e42d-171">Yes</span></span> |<span data-ttu-id="4e42d-172">以逗號分隔的類別清單，其中列出應該收集的事件類別。</span><span class="sxs-lookup"><span data-stu-id="4e42d-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="4e42d-173">可能的值有 Write、Delete、Action。</span><span class="sxs-lookup"><span data-stu-id="4e42d-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="4e42d-174">活動記錄檔的儲存體結構描述</span><span class="sxs-lookup"><span data-stu-id="4e42d-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="4e42d-175">一旦您已經設定封存，只要一發生活動記錄檔事件，就會在儲存體帳戶中建立儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="4e42d-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="4e42d-176">在容器內的 blob 的活動記錄檔和診斷記錄檔會遵循相同的格式。</span><span class="sxs-lookup"><span data-stu-id="4e42d-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="4e42d-177">這些 blob 的結構為：</span><span class="sxs-lookup"><span data-stu-id="4e42d-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="4e42d-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="4e42d-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="4e42d-179">例如，blob 名稱可能是︰</span><span class="sxs-lookup"><span data-stu-id="4e42d-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="4e42d-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="4e42d-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="4e42d-181">每個 PT1H.json blob 有一個 JSON blob，包含在 blob URL 指定時數內 (例如 h = 12) 發生的事件。</span><span class="sxs-lookup"><span data-stu-id="4e42d-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="4e42d-182">在目前這一小時，事件一發生就會附加到 PT1H.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e42d-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="4e42d-183">分鐘值 (m = 00) 一定是 00，因為活動記錄檔事件是分成每小時的個別 blob。</span><span class="sxs-lookup"><span data-stu-id="4e42d-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="4e42d-184">在 PT1H.json 檔案中，每個事件會以下列格式儲存在 “records” 陣列︰</span><span class="sxs-lookup"><span data-stu-id="4e42d-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="4e42d-185">元素名稱</span><span class="sxs-lookup"><span data-stu-id="4e42d-185">Element name</span></span> | <span data-ttu-id="4e42d-186">說明</span><span class="sxs-lookup"><span data-stu-id="4e42d-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e42d-187">分析</span><span class="sxs-lookup"><span data-stu-id="4e42d-187">time</span></span> |<span data-ttu-id="4e42d-188">處理與事件對應之要求的Azure 服務產生事件時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4e42d-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4e42d-189">ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e42d-189">resourceId</span></span> |<span data-ttu-id="4e42d-190">受影響資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e42d-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="4e42d-191">operationName</span><span class="sxs-lookup"><span data-stu-id="4e42d-191">operationName</span></span> |<span data-ttu-id="4e42d-192">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="4e42d-192">Name of the operation.</span></span> |
| <span data-ttu-id="4e42d-193">category</span><span class="sxs-lookup"><span data-stu-id="4e42d-193">category</span></span> |<span data-ttu-id="4e42d-194">事件的類別，例如</span><span class="sxs-lookup"><span data-stu-id="4e42d-194">Category of the action, eg.</span></span> <span data-ttu-id="4e42d-195">寫入、讀取、動作。</span><span class="sxs-lookup"><span data-stu-id="4e42d-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="4e42d-196">resultType</span><span class="sxs-lookup"><span data-stu-id="4e42d-196">resultType</span></span> |<span data-ttu-id="4e42d-197">結果的類型，例如</span><span class="sxs-lookup"><span data-stu-id="4e42d-197">The type of the result, eg.</span></span> <span data-ttu-id="4e42d-198">成功、失敗、開始</span><span class="sxs-lookup"><span data-stu-id="4e42d-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="4e42d-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="4e42d-199">resultSignature</span></span> |<span data-ttu-id="4e42d-200">取決於資源類型。</span><span class="sxs-lookup"><span data-stu-id="4e42d-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="4e42d-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="4e42d-201">durationMs</span></span> |<span data-ttu-id="4e42d-202">作業的持續時間 (以毫秒為單位)</span><span class="sxs-lookup"><span data-stu-id="4e42d-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="4e42d-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="4e42d-203">callerIpAddress</span></span> |<span data-ttu-id="4e42d-204">已執行作業的使用者的 IP 地址，根據可用性的 UPN 宣告或 SPN 宣告。</span><span class="sxs-lookup"><span data-stu-id="4e42d-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="4e42d-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="4e42d-205">correlationId</span></span> |<span data-ttu-id="4e42d-206">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="4e42d-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="4e42d-207">具有相同 correlationId、屬於同一 uber 動作的事件。</span><span class="sxs-lookup"><span data-stu-id="4e42d-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="4e42d-208">身分識別</span><span class="sxs-lookup"><span data-stu-id="4e42d-208">identity</span></span> |<span data-ttu-id="4e42d-209">描述授權和宣告的 JSON blob。</span><span class="sxs-lookup"><span data-stu-id="4e42d-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="4e42d-210">授權</span><span class="sxs-lookup"><span data-stu-id="4e42d-210">authorization</span></span> |<span data-ttu-id="4e42d-211">事件的 RBAC 屬性的 blob。</span><span class="sxs-lookup"><span data-stu-id="4e42d-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="4e42d-212">通常包括 action、role 和 scope 屬性。</span><span class="sxs-lookup"><span data-stu-id="4e42d-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="4e42d-213">層級</span><span class="sxs-lookup"><span data-stu-id="4e42d-213">level</span></span> |<span data-ttu-id="4e42d-214">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="4e42d-214">Level of the event.</span></span> <span data-ttu-id="4e42d-215">下列其中一個值：重大、錯誤、警告、資訊和詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4e42d-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4e42d-216">location</span><span class="sxs-lookup"><span data-stu-id="4e42d-216">location</span></span> |<span data-ttu-id="4e42d-217">在 location 發生 (或全球) 的區域。</span><span class="sxs-lookup"><span data-stu-id="4e42d-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="4e42d-218">properties</span><span class="sxs-lookup"><span data-stu-id="4e42d-218">properties</span></span> |<span data-ttu-id="4e42d-219">描述事件詳細資料的一組 `<Key, Value>` 配對 (也就是字典)。</span><span class="sxs-lookup"><span data-stu-id="4e42d-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="4e42d-220">屬性和這些屬性的使用方式，依資源而異。</span><span class="sxs-lookup"><span data-stu-id="4e42d-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4e42d-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e42d-221">Next steps</span></span>
* [<span data-ttu-id="4e42d-222">下載 blob 以供分析</span><span class="sxs-lookup"><span data-stu-id="4e42d-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="4e42d-223">將活動記錄檔串流至事件中樞</span><span class="sxs-lookup"><span data-stu-id="4e42d-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="4e42d-224">深入了解活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4e42d-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

