---
title: "aaaArchive hello Azure 活動記錄檔 |Microsoft 文件"
description: "了解如何 tooarchive Azure 活動記錄檔以取得儲存體帳戶中的長期保存。"
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="66922-103">封存 hello Azure 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="66922-104">在本文中，我們示範如何使用 hello Azure 入口網站、 PowerShell 指令程式或跨平台 CLI tooarchive 您[ **Azure 活動記錄檔**](monitoring-overview-activity-logs.md)儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="66922-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="66922-105">這個選項非常有用，如果您想要的 tooretain 您活動記錄中超過 90 天 （具有完整控制權 hello 保留原則的詳細資訊） 的稽核，靜態分析，或備份。</span><span class="sxs-lookup"><span data-stu-id="66922-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="66922-106">如果您只需要 tooretain 事件 90 天或更少，您不需要 tooset 保存 tooa 儲存體帳戶，因為活動記錄檔事件會保留在 hello Azure 平台 90 天內沒有啟用封存。</span><span class="sxs-lookup"><span data-stu-id="66922-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66922-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="66922-107">Prerequisites</span></span>
<span data-ttu-id="66922-108">在開始之前，您需要太[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)toowhich 可以封存活動記錄。</span><span class="sxs-lookup"><span data-stu-id="66922-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="66922-109">我們強烈建議您務必使用現有的儲存體帳戶具有其他非監視資料，讓您更能夠控制存取 toomonitoring 資料儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="66922-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="66922-110">不過，如果您也要封存診斷記錄檔和度量 tooa 儲存體帳戶，它會使意義 toouse 該儲存體帳戶為您的活動記錄檔以及 tookeep 監視的所有資料在集中位置。</span><span class="sxs-lookup"><span data-stu-id="66922-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="66922-111">您使用的 hello 儲存體帳戶必須是一般用途儲存體帳戶，而不是 blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="66922-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="66922-112">hello 儲存體帳戶中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 訂用帳戶相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66922-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="66922-113">記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="66922-113">Log Profile</span></span>
<span data-ttu-id="66922-114">tooarchive hello 使用任何下列的 hello 方法的活動記錄檔，設定 hello**記錄檔的設定檔**訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66922-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="66922-115">hello 記錄檔的設定檔定義 hello 儲存或資料流處理之事件的類型與 hello 輸出-儲存體帳戶及/或事件中樞。</span><span class="sxs-lookup"><span data-stu-id="66922-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="66922-116">它也會定義事件儲存在儲存體帳戶中的 hello 保留原則 （天 tooretain 數目）。</span><span class="sxs-lookup"><span data-stu-id="66922-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="66922-117">如果 hello 保留原則設定 toozero，事件會無限期儲存。</span><span class="sxs-lookup"><span data-stu-id="66922-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="66922-118">否則，這可以設定 tooany 值介於 1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="66922-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="66922-119">保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則將會被刪除。</span><span class="sxs-lookup"><span data-stu-id="66922-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="66922-120">例如，如果您在一天的保留原則，hello 從今天 hello 日開始時 hello hello 天前昨天的記錄檔會刪除。</span><span class="sxs-lookup"><span data-stu-id="66922-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="66922-121">[您可以至此處閱讀記錄檔設定檔的相關資訊](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)。</span><span class="sxs-lookup"><span data-stu-id="66922-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="66922-122">封存 hello 使用 hello 入口網站的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="66922-123">在 hello 入口網站中，按一下 hello**活動記錄檔**hello 左側導覽上的連結。</span><span class="sxs-lookup"><span data-stu-id="66922-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="66922-124">如果您沒有看到 hello 活動記錄檔的連結，按一下 hello**更服務**連結第一次。</span><span class="sxs-lookup"><span data-stu-id="66922-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![瀏覽 tooActivity 記錄刀鋒視窗](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="66922-126">在 hello hello 刀鋒視窗頂端，按一下**匯出**。</span><span class="sxs-lookup"><span data-stu-id="66922-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![按一下 hello 匯出按鈕](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="66922-128">在出現的 hello 刀鋒視窗，勾選 [hello] 方塊**tooa 儲存體帳戶匯出**並選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="66922-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![設定儲存體帳戶](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="66922-130">使用 hello 滑桿或文字方塊中，定義的活動記錄檔事件應該保持儲存體帳戶中的天數。</span><span class="sxs-lookup"><span data-stu-id="66922-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="66922-131">如果您偏好的 toohave 資料無限期地保存 hello 儲存體帳戶中，設定此數字 toozero。</span><span class="sxs-lookup"><span data-stu-id="66922-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="66922-132">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="66922-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="66922-133">封存 hello 透過 PowerShell 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="66922-134">屬性</span><span class="sxs-lookup"><span data-stu-id="66922-134">Property</span></span> | <span data-ttu-id="66922-135">必要</span><span class="sxs-lookup"><span data-stu-id="66922-135">Required</span></span> | <span data-ttu-id="66922-136">說明</span><span class="sxs-lookup"><span data-stu-id="66922-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66922-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="66922-137">StorageAccountId</span></span> |<span data-ttu-id="66922-138">否</span><span class="sxs-lookup"><span data-stu-id="66922-138">No</span></span> |<span data-ttu-id="66922-139">應該儲存 hello 儲存體帳戶 toowhich 活動記錄檔的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="66922-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="66922-140">位置</span><span class="sxs-lookup"><span data-stu-id="66922-140">Locations</span></span> |<span data-ttu-id="66922-141">是</span><span class="sxs-lookup"><span data-stu-id="66922-141">Yes</span></span> |<span data-ttu-id="66922-142">以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="66922-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="66922-143">您可以檢視所有區域的清單[造訪此頁](https://azure.microsoft.com/en-us/regions)或使用[hello Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。</span><span class="sxs-lookup"><span data-stu-id="66922-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="66922-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="66922-144">RetentionInDays</span></span> |<span data-ttu-id="66922-145">是</span><span class="sxs-lookup"><span data-stu-id="66922-145">Yes</span></span> |<span data-ttu-id="66922-146">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="66922-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="66922-147">值為 0 會無限期儲存 hello 記錄檔 （永久）。</span><span class="sxs-lookup"><span data-stu-id="66922-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="66922-148">類別</span><span class="sxs-lookup"><span data-stu-id="66922-148">Categories</span></span> |<span data-ttu-id="66922-149">是</span><span class="sxs-lookup"><span data-stu-id="66922-149">Yes</span></span> |<span data-ttu-id="66922-150">以逗號分隔的類別清單，其中列出應該收集的事件類別。</span><span class="sxs-lookup"><span data-stu-id="66922-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="66922-151">可能的值有 Write、Delete、Action。</span><span class="sxs-lookup"><span data-stu-id="66922-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="66922-152">封存 hello 透過 CLI 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="66922-153">屬性</span><span class="sxs-lookup"><span data-stu-id="66922-153">Property</span></span> | <span data-ttu-id="66922-154">必要</span><span class="sxs-lookup"><span data-stu-id="66922-154">Required</span></span> | <span data-ttu-id="66922-155">說明</span><span class="sxs-lookup"><span data-stu-id="66922-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66922-156">名稱</span><span class="sxs-lookup"><span data-stu-id="66922-156">name</span></span> |<span data-ttu-id="66922-157">是</span><span class="sxs-lookup"><span data-stu-id="66922-157">Yes</span></span> |<span data-ttu-id="66922-158">記錄檔設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="66922-158">Name of your log profile.</span></span> |
| <span data-ttu-id="66922-159">storageId</span><span class="sxs-lookup"><span data-stu-id="66922-159">storageId</span></span> |<span data-ttu-id="66922-160">否</span><span class="sxs-lookup"><span data-stu-id="66922-160">No</span></span> |<span data-ttu-id="66922-161">應該儲存 hello 儲存體帳戶 toowhich 活動記錄檔的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="66922-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="66922-162">位置</span><span class="sxs-lookup"><span data-stu-id="66922-162">locations</span></span> |<span data-ttu-id="66922-163">是</span><span class="sxs-lookup"><span data-stu-id="66922-163">Yes</span></span> |<span data-ttu-id="66922-164">以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="66922-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="66922-165">您可以檢視所有區域的清單[造訪此頁](https://azure.microsoft.com/en-us/regions)或使用[hello Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。</span><span class="sxs-lookup"><span data-stu-id="66922-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="66922-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="66922-166">retentionInDays</span></span> |<span data-ttu-id="66922-167">是</span><span class="sxs-lookup"><span data-stu-id="66922-167">Yes</span></span> |<span data-ttu-id="66922-168">事件應保留的天數，1 到 2147483647 之間。</span><span class="sxs-lookup"><span data-stu-id="66922-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="66922-169">零值將會無限期儲存 hello 記錄檔 （永久）。</span><span class="sxs-lookup"><span data-stu-id="66922-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="66922-170">類別</span><span class="sxs-lookup"><span data-stu-id="66922-170">categories</span></span> |<span data-ttu-id="66922-171">是</span><span class="sxs-lookup"><span data-stu-id="66922-171">Yes</span></span> |<span data-ttu-id="66922-172">以逗號分隔的類別清單，其中列出應該收集的事件類別。</span><span class="sxs-lookup"><span data-stu-id="66922-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="66922-173">可能的值有 Write、Delete、Action。</span><span class="sxs-lookup"><span data-stu-id="66922-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="66922-174">儲存結構描述的 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="66922-175">在您設定保存，儲存體容器將建立 hello 儲存體帳戶中，只要發生活動記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="66922-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="66922-176">hello 容器中的 hello blob 遵循的 hello 相同格式跨 hello 活動記錄檔和診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="66922-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="66922-177">這些 blob hello 結構是：</span><span class="sxs-lookup"><span data-stu-id="66922-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="66922-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="66922-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="66922-179">例如，blob 名稱可能是︰</span><span class="sxs-lookup"><span data-stu-id="66922-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="66922-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="66922-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="66922-181">每個 PT1H.json blob 包含 JSON blob hello hello blob URL 中指定的一小時內發生的事件 (例如 h = 12)。</span><span class="sxs-lookup"><span data-stu-id="66922-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="66922-182">Hello 存在小時，在事件發生時是附加的 toohello PT1H.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="66922-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="66922-183">hello 分鐘值 (m = 00) 一定是 00，因為活動記錄檔事件會分為個別每小時的 blob。</span><span class="sxs-lookup"><span data-stu-id="66922-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="66922-184">在 hello PT1H.json 檔案中，每個事件會儲存在 hello 「 記錄 」 陣列中，遵循此格式：</span><span class="sxs-lookup"><span data-stu-id="66922-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="66922-185">元素名稱</span><span class="sxs-lookup"><span data-stu-id="66922-185">Element name</span></span> | <span data-ttu-id="66922-186">說明</span><span class="sxs-lookup"><span data-stu-id="66922-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66922-187">分析</span><span class="sxs-lookup"><span data-stu-id="66922-187">time</span></span> |<span data-ttu-id="66922-188">Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="66922-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="66922-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="66922-189">resourceId</span></span> |<span data-ttu-id="66922-190">資源識別碼 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="66922-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="66922-191">operationName</span><span class="sxs-lookup"><span data-stu-id="66922-191">operationName</span></span> |<span data-ttu-id="66922-192">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="66922-192">Name of hello operation.</span></span> |
| <span data-ttu-id="66922-193">category</span><span class="sxs-lookup"><span data-stu-id="66922-193">category</span></span> |<span data-ttu-id="66922-194">分類的 hello 動作，例如。</span><span class="sxs-lookup"><span data-stu-id="66922-194">Category of hello action, eg.</span></span> <span data-ttu-id="66922-195">寫入、讀取、動作。</span><span class="sxs-lookup"><span data-stu-id="66922-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="66922-196">resultType</span><span class="sxs-lookup"><span data-stu-id="66922-196">resultType</span></span> |<span data-ttu-id="66922-197">例如 hello hello 結果的型別。</span><span class="sxs-lookup"><span data-stu-id="66922-197">hello type of hello result, eg.</span></span> <span data-ttu-id="66922-198">成功、失敗、開始</span><span class="sxs-lookup"><span data-stu-id="66922-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="66922-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="66922-199">resultSignature</span></span> |<span data-ttu-id="66922-200">Hello 資源類型而定。</span><span class="sxs-lookup"><span data-stu-id="66922-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="66922-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="66922-201">durationMs</span></span> |<span data-ttu-id="66922-202">以毫秒為單位的 hello 作業的持續時間</span><span class="sxs-lookup"><span data-stu-id="66922-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="66922-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="66922-203">callerIpAddress</span></span> |<span data-ttu-id="66922-204">已執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="66922-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="66922-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="66922-205">correlationId</span></span> |<span data-ttu-id="66922-206">通常是 hello 字串格式 GUID。</span><span class="sxs-lookup"><span data-stu-id="66922-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="66922-207">共用的相互關聯識別碼的事件屬於 toohello 相同超級動作。</span><span class="sxs-lookup"><span data-stu-id="66922-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="66922-208">身分識別</span><span class="sxs-lookup"><span data-stu-id="66922-208">identity</span></span> |<span data-ttu-id="66922-209">Hello 授權和宣告描述的 JSON blob。</span><span class="sxs-lookup"><span data-stu-id="66922-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="66922-210">授權</span><span class="sxs-lookup"><span data-stu-id="66922-210">authorization</span></span> |<span data-ttu-id="66922-211">Blob hello 事件的 RBAC 屬性。</span><span class="sxs-lookup"><span data-stu-id="66922-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="66922-212">通常包含 hello 「 動作 」、 「 角色 」 和 「 範圍 」 屬性。</span><span class="sxs-lookup"><span data-stu-id="66922-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="66922-213">層級</span><span class="sxs-lookup"><span data-stu-id="66922-213">level</span></span> |<span data-ttu-id="66922-214">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="66922-214">Level of hello event.</span></span> <span data-ttu-id="66922-215">Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」</span><span class="sxs-lookup"><span data-stu-id="66922-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="66922-216">location</span><span class="sxs-lookup"><span data-stu-id="66922-216">location</span></span> |<span data-ttu-id="66922-217">Hello 位置發生 （或全域） 中的區域。</span><span class="sxs-lookup"><span data-stu-id="66922-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="66922-218">屬性</span><span class="sxs-lookup"><span data-stu-id="66922-218">properties</span></span> |<span data-ttu-id="66922-219">一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="66922-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="66922-220">hello 屬性和這些屬性的使用方式有所不同 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="66922-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="66922-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66922-221">Next steps</span></span>
* [<span data-ttu-id="66922-222">下載 blob 以供分析</span><span class="sxs-lookup"><span data-stu-id="66922-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="66922-223">資料流 hello 活動記錄檔 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="66922-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="66922-224">深入了解 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="66922-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

