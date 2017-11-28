---
title: "aaaUse 休息 tooback 與還原 App Service 應用程式"
description: "了解如何 toouse RESTful API 呼叫 tooback 和還原 Azure App Service 中的應用程式"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="099a4-103">使用 REST tooback] 和 [還原 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="099a4-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="099a4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="099a4-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="099a4-105">REST API</span><span class="sxs-lookup"><span data-stu-id="099a4-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="099a4-106">[App Service 應用程式](https://azure.microsoft.com/services/app-service/web/) 可以備份成 Azure 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="099a4-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="099a4-107">hello 備份也可以包含 hello 應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="099a4-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="099a4-108">如果曾不小心刪除 hello 應用程式，或 hello 應用程式需求 toobe 還原 tooa 先前的版本，便可以從任何先前的備份還原。</span><span class="sxs-lookup"><span data-stu-id="099a4-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="099a4-109">您可以視需要隨時進行備份，或排定在間隔適當時間後進行備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="099a4-110">本文說明如何 toobackup 和還原應用程式，但 rest 式 API 要求。</span><span class="sxs-lookup"><span data-stu-id="099a4-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="099a4-111">如果您會喜歡 toocreate，且管理應用程式備份，以圖形方式透過 hello Azure 入口網站，請參閱[備份 Azure App Service 中的 web 應用程式](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="099a4-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="099a4-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="099a4-112">Getting Started</span></span>
<span data-ttu-id="099a4-113">toosend REST 要求時，您的應用程式需要 tooknow**名稱**，**資源群組**，和**訂用帳戶 id**。可以找到此資訊，按一下您的應用程式在 hello **App Service**刀鋒視窗中的 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="099a4-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="099a4-114">如需本文章中的 hello 範例，我們要設定 hello 網站**backuprestoreapiexamples.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="099a4-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="099a4-115">它會儲存在 hello Uswest-預設的 Web 資源群組，且正在執行以 hello 識別碼 00001111-2222年-3333-4444-555566667777 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="099a4-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![範例網站資訊][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="099a4-117">備份和還原 REST API</span><span class="sxs-lookup"><span data-stu-id="099a4-117">Backup and restore REST API</span></span>
<span data-ttu-id="099a4-118">現在，我們將討論如何 toouse hello REST API toobackup 和還原應用程式的幾個範例。</span><span class="sxs-lookup"><span data-stu-id="099a4-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="099a4-119">每個範例都包含 URL 和 HTTP 要求本文。</span><span class="sxs-lookup"><span data-stu-id="099a4-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="099a4-120">hello 範例 URL 會包含預留位置包裝在大括號，例如 {訂閱 id}。</span><span class="sxs-lookup"><span data-stu-id="099a4-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="099a4-121">Hello 預留位置取代為 hello 應用程式的對應資訊。</span><span class="sxs-lookup"><span data-stu-id="099a4-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="099a4-122">如需參考，這裡是 hello 範例 Url 中會顯示每個預留位置的說明。</span><span class="sxs-lookup"><span data-stu-id="099a4-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="099a4-123">訂用帳戶 id – hello Azure 訂用帳戶包含 hello 應用程式的識別碼</span><span class="sxs-lookup"><span data-stu-id="099a4-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="099a4-124">資源-群組-名稱 – hello 資源群組包含 hello 應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="099a4-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="099a4-125">名稱 – hello 應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="099a4-125">name – Name of hello app</span></span>
* <span data-ttu-id="099a4-126">備份-識別碼 – 識別碼 hello 應用程式備份</span><span class="sxs-lookup"><span data-stu-id="099a4-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="099a4-127">如 hello hello 應用程式開發介面的完整文件，包括數個選擇性參數可以包含在 hello HTTP 要求中，請參閱 hello [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="099a4-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="099a4-128">視需求備份應用程式</span><span class="sxs-lookup"><span data-stu-id="099a4-128">Backup an app on demand</span></span>
<span data-ttu-id="099a4-129">設定應用程式的 tooback 立即傳送**POST**要求太**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/備份 /**。</span><span class="sxs-lookup"><span data-stu-id="099a4-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="099a4-130">以下是 hello URL 看起來像使用我們的範例網站。</span><span class="sxs-lookup"><span data-stu-id="099a4-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="099a4-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="099a4-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="099a4-132">提供的 JSON 物件的儲存體帳戶 toouse toostore hello 備份您的要求 toospecify hello 主體中。</span><span class="sxs-lookup"><span data-stu-id="099a4-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="099a4-133">hello JSON 物件必須有一個名為屬性**storageAccountUrl**，一個保存[SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md)授與寫入權限 toohello Azure 儲存體容器，其中含有 hello 備份 blob。</span><span class="sxs-lookup"><span data-stu-id="099a4-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="099a4-134">如果您想 tooback 資料庫時，您也必須提供包含 hello 名稱、 類型和備份 hello 資料庫 toobe 的連接字串的清單。</span><span class="sxs-lookup"><span data-stu-id="099a4-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="099a4-135">立即收到 hello 要求時，才會開始 hello 應用程式的備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="099a4-136">hello 備份程序可能需要很長的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="099a4-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="099a4-137">hello HTTP 回應會包含您可以使用在另一個要求 toosee hello hello 備份的狀態識別碼。</span><span class="sxs-lookup"><span data-stu-id="099a4-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="099a4-138">以下是主體的範例的 hello hello HTTP 回應 tooour 備份要求。</span><span class="sxs-lookup"><span data-stu-id="099a4-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="099a4-139">錯誤訊息可以找到 hello HTTP 回應 hello 記錄屬性中。</span><span class="sxs-lookup"><span data-stu-id="099a4-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="099a4-140">排程自動備份</span><span class="sxs-lookup"><span data-stu-id="099a4-140">Schedule automatic backups</span></span>
<span data-ttu-id="099a4-141">在 設定應用程式的隨選加法 toobacking，您也可以自動排程備份 toohappen。</span><span class="sxs-lookup"><span data-stu-id="099a4-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="099a4-142">設定新的自動備份排程</span><span class="sxs-lookup"><span data-stu-id="099a4-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="099a4-143">備份排程，tooset 傳送**放**要求太**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config備份/**。</span><span class="sxs-lookup"><span data-stu-id="099a4-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="099a4-144">以下是 hello URL 我們的範例網站的外觀。</span><span class="sxs-lookup"><span data-stu-id="099a4-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="099a4-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="099a4-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="099a4-146">hello 要求主體必須具有指定 hello 備份設定的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="099a4-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="099a4-147">以下是範例與 hello 所需的所有參數。</span><span class="sxs-lookup"><span data-stu-id="099a4-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="099a4-148">這個範例會設定 hello 應用程式 toobe 耐用性 — 每隔七天。</span><span class="sxs-lookup"><span data-stu-id="099a4-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="099a4-149">hello 參數**frequencyInterval**和**frequencyUnit**同時決定頻率 hello 備份，就可能發生。</span><span class="sxs-lookup"><span data-stu-id="099a4-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="099a4-150">**frequencyUnit** 的有效值為**小時**和**天**。</span><span class="sxs-lookup"><span data-stu-id="099a4-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="099a4-151">例如，設定應用程式的每隔 12 小時，tooback 設定 frequencyInterval too12 和 frequencyUnit toohour。</span><span class="sxs-lookup"><span data-stu-id="099a4-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="099a4-152">從 hello 儲存體帳戶，會自動移除舊的備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="099a4-153">您可以控制備份可以藉由在設定 hello 舊 hello **retentionPeriodInDays**參數。</span><span class="sxs-lookup"><span data-stu-id="099a4-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="099a4-154">如果您想 tooalways 有至少一個儲存，不論它，設定舊的備份**keepAtLeastOneBackup** tootrue。</span><span class="sxs-lookup"><span data-stu-id="099a4-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="099a4-155">取得 hello 自動備份排程</span><span class="sxs-lookup"><span data-stu-id="099a4-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="099a4-156">tooget 應用程式的備份設定，請傳送**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/站台 / {name} / config/備份列出**。</span><span class="sxs-lookup"><span data-stu-id="099a4-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="099a4-157">我們的範例網站 hello url **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**。</span><span class="sxs-lookup"><span data-stu-id="099a4-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="099a4-158">取得備份的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="099a4-158">Get hello status of a backup</span></span>
<span data-ttu-id="099a4-159">根據多大的 hello 應用程式時，備份可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="099a4-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="099a4-160">備份程序也可能失敗、逾時或是部分成功。</span><span class="sxs-lookup"><span data-stu-id="099a4-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="099a4-161">toosee hello 狀態的所有應用程式的備份，傳送給**取得**要求 toohello URL **https://management.azure.com/subscriptions/ {訂閱 id} /resourceGroups/ {資源-群組-名稱} /providers/Microsoft.Web/sites/{name}/backups**。</span><span class="sxs-lookup"><span data-stu-id="099a4-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="099a4-162">toosee hello 狀態的特定備份，傳送 GET 要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ {備份-識別碼}**。</span><span class="sxs-lookup"><span data-stu-id="099a4-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="099a4-163">以下是 hello URL 我們的範例網站的外觀。</span><span class="sxs-lookup"><span data-stu-id="099a4-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="099a4-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="099a4-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="099a4-165">hello 回應主體包含 JSON 物件類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="099a4-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="099a4-166">備份 hello 狀態是列舉型別。</span><span class="sxs-lookup"><span data-stu-id="099a4-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="099a4-167">以下是各個可能的狀態。</span><span class="sxs-lookup"><span data-stu-id="099a4-167">Here is every possible state.</span></span>

* <span data-ttu-id="099a4-168">0 – InProgress: hello 備份已啟動，但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="099a4-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="099a4-169">1 – 失敗： hello 備份未成功。</span><span class="sxs-lookup"><span data-stu-id="099a4-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="099a4-170">2 – 成功： hello 備份順利完成。</span><span class="sxs-lookup"><span data-stu-id="099a4-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="099a4-171">3 – 逾時： hello 備份未完成的時間，而被取消。</span><span class="sxs-lookup"><span data-stu-id="099a4-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="099a4-172">4 – 建立： hello 備份要求排入佇列，但尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="099a4-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="099a4-173">5 – 略過： hello 備份尚未進行 tooa 排程觸發太多備份到期。</span><span class="sxs-lookup"><span data-stu-id="099a4-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="099a4-174">6 – PartiallySucceeded: hello 備份成功，但無法備份部分檔案，因為無法讀取。</span><span class="sxs-lookup"><span data-stu-id="099a4-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="099a4-175">因為已在 hello 檔案上設定的獨佔鎖定，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="099a4-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="099a4-176">7 – DeleteInProgress: hello 備份已經刪除，要求的 toobe，但尚未刪除。</span><span class="sxs-lookup"><span data-stu-id="099a4-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="099a4-177">8 – DeleteFailed： 無法刪除 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="099a4-178">這可能是因為 hello SAS URL 是使用的 toocreate hello 備份已過期。</span><span class="sxs-lookup"><span data-stu-id="099a4-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="099a4-179">9 – 刪除： hello 備份已成功刪除。</span><span class="sxs-lookup"><span data-stu-id="099a4-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="099a4-180">從備份還原應用程式</span><span class="sxs-lookup"><span data-stu-id="099a4-180">Restore an app from a backup</span></span>
<span data-ttu-id="099a4-181">如果您的應用程式已遭刪除，或如果您想 toorevert 應用程式 tooa 舊版本，您可以從備份還原 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="099a4-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="099a4-182">tooinvoke 還原，傳送**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/備份 / {備份-識別碼} / 還原**。</span><span class="sxs-lookup"><span data-stu-id="099a4-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="099a4-183">以下是 hello URL 我們的範例網站的外觀。</span><span class="sxs-lookup"><span data-stu-id="099a4-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="099a4-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="099a4-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="099a4-185">在 hello 要求主體中，傳送包含 hello 還原作業的 hello 屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="099a4-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="099a4-186">以下是包含所有必要屬性的範例：</span><span class="sxs-lookup"><span data-stu-id="099a4-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="099a4-187">還原 tooa 新應用程式</span><span class="sxs-lookup"><span data-stu-id="099a4-187">Restore tooa new app</span></span>
<span data-ttu-id="099a4-188">有時候您可能想 toocreate 新的應用程式，當您還原的備份，而非覆寫現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="099a4-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="099a4-189">toodo，變更 hello 要求 URL toopoint toohello 新應用程式 toocreate，並變更 hello**覆寫**中的屬性太 hello JSON**false**。</span><span class="sxs-lookup"><span data-stu-id="099a4-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="099a4-190">刪除應用程式備份</span><span class="sxs-lookup"><span data-stu-id="099a4-190">Delete an app backup</span></span>
<span data-ttu-id="099a4-191">如果您想要備份 toodelete，傳送**刪除**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/站台 / {name} /backups/ {備份-識別碼}**。</span><span class="sxs-lookup"><span data-stu-id="099a4-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="099a4-192">以下是 hello URL 我們的範例網站的外觀。</span><span class="sxs-lookup"><span data-stu-id="099a4-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="099a4-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="099a4-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="099a4-194">管理備份的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="099a4-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="099a4-195">Azure 應用程式服務將嘗試 toodelete 您從使用 hello 時建立 hello 備份應用程式提供的 SAS URL 的 Azure 儲存體的備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="099a4-196">如果此 SAS URL 已不再有效，無法透過 hello REST API 會刪除 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="099a4-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="099a4-197">不過，您可以更新 SAS URL 與備份相關聯的傳送的嗨**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {訂閱 id} /resourceGroups/ {資源-群組-名稱} /providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**。</span><span class="sxs-lookup"><span data-stu-id="099a4-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="099a4-198">以下是 hello URL 我們的範例網站的外觀。</span><span class="sxs-lookup"><span data-stu-id="099a4-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="099a4-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="099a4-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="099a4-200">在 hello 要求主體中，傳送包含 hello 新 SAS URL 的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="099a4-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="099a4-201">範例如下。</span><span class="sxs-lookup"><span data-stu-id="099a4-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="099a4-202">基於安全性理由，傳送 GET 要求進行特定的備份時，不會傳回的 hello 與備份相關聯的 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="099a4-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="099a4-203">如果您想 tooview hello 與備份相關聯的 SAS URL，傳送 POST 要求 toohello 上述相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="099a4-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="099a4-204">Hello 要求主體中包含空白的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="099a4-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="099a4-205">hello 回應 hello 伺服器包含所有的備份的資訊，包括其 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="099a4-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
