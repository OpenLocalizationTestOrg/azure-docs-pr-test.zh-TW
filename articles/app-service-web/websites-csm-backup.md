---
title: "使用 REST 來備份及還原 App Service 應用程式"
description: "了解如何使用 RESTful API 呼叫來備份和還原 Azure App Service 中的 Web 應用程式"
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
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="691de-103">使用 REST 來備份及還原 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="691de-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="691de-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="691de-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="691de-105">REST API</span><span class="sxs-lookup"><span data-stu-id="691de-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="691de-106">[App Service 應用程式](https://azure.microsoft.com/services/app-service/web/) 可以備份成 Azure 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="691de-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="691de-107">此備份中也可以包含應用程式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="691de-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="691de-108">如果不小心刪除應用程式，或需要將應用程式還原成先前的版本，則可以從任何先前的備份加以還原。</span><span class="sxs-lookup"><span data-stu-id="691de-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="691de-109">您可以視需要隨時進行備份，或排定在間隔適當時間後進行備份。</span><span class="sxs-lookup"><span data-stu-id="691de-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="691de-110">本文說明如何透過 RESTful API 要求，來備份和還原應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="691de-111">如果您想要透過 Azure 入口網站以圖形方式建立和管理 Web 應用程式的備份，請參閱 [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="691de-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="691de-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="691de-112">Getting Started</span></span>
<span data-ttu-id="691de-113">若要傳送 REST 要求，您必須知道應用程式的**名稱**、**資源群組**和**訂用帳戶識別碼**。如要尋找這些資訊，請在 [Azure 入口網站](https://portal.azure.com)的 [App Service] 刀鋒視窗中按一下您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="691de-114">在本文的範例中，我們會設定 **backuprestoreapiexamples.azurewebsites.net** 網站。</span><span class="sxs-lookup"><span data-stu-id="691de-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="691de-115">它儲存在 Default-Web-WestUS 資源群組中，並在識別碼為 00001111-2222-3333-4444-555566667777 的訂用帳戶上執行。</span><span class="sxs-lookup"><span data-stu-id="691de-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![範例網站資訊][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="691de-117">備份和還原 REST API</span><span class="sxs-lookup"><span data-stu-id="691de-117">Backup and restore REST API</span></span>
<span data-ttu-id="691de-118">現在我們要討論幾個範例，說明如何使用 REST API 來備份和還原應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="691de-119">每個範例都包含 URL 和 HTTP 要求本文。</span><span class="sxs-lookup"><span data-stu-id="691de-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="691de-120">範例 URL 中包含以大括號括住的預留位置，例如 {subscription-id}。</span><span class="sxs-lookup"><span data-stu-id="691de-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="691de-121">請以對應的應用程式資訊來取代預留位置。</span><span class="sxs-lookup"><span data-stu-id="691de-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="691de-122">以下有範例 URL 中會出現之預留位置的說明可供您參考。</span><span class="sxs-lookup"><span data-stu-id="691de-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="691de-123">subscription-id – 包含應用程式的 Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="691de-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="691de-124">resource-group-name – 包含應用程式的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="691de-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="691de-125">name – 應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="691de-125">name – Name of the app</span></span>
* <span data-ttu-id="691de-126">backup-id – 應用程式備份的識別碼</span><span class="sxs-lookup"><span data-stu-id="691de-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="691de-127">如需 API 的完整說明文件，包括可在 HTTP 要求內加入的幾個選用參數，請參閱 [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="691de-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="691de-128">視需求備份應用程式</span><span class="sxs-lookup"><span data-stu-id="691de-128">Backup an app on demand</span></span>
<span data-ttu-id="691de-129">若要立即備份應用程式，請傳送 **POST** 要求至 **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**。</span><span class="sxs-lookup"><span data-stu-id="691de-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="691de-130">使用範例網站後的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="691de-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="691de-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="691de-132">請在要求本文中提供 JSON 物件，以指定要用來儲存備份的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="691de-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="691de-133">JSON 物件必須有名為 **storageAccountUrl**的屬性以保存 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ，此 URL 會授與保有備份 Blob 之 Azure 儲存體容器的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="691de-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="691de-134">如果您想要備份資料庫，則還必須提供包含所要備份之資料庫的名稱、類型和連接字串的清單。</span><span class="sxs-lookup"><span data-stu-id="691de-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

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

<span data-ttu-id="691de-135">當系統收到要求時，就會立刻開始備份應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="691de-136">備份程序可能需要很長的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="691de-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="691de-137">HTTP 回應中會有識別碼可供您用於其他要求以查看備份狀態。</span><span class="sxs-lookup"><span data-stu-id="691de-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="691de-138">以下是備份要求之 HTTP 回應本文的範例。</span><span class="sxs-lookup"><span data-stu-id="691de-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

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
> <span data-ttu-id="691de-139">在 HTTP 回應的記錄檔屬性中可以找到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="691de-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="691de-140">排程自動備份</span><span class="sxs-lookup"><span data-stu-id="691de-140">Schedule automatic backups</span></span>
<span data-ttu-id="691de-141">除了視需要備份應用程式，您也可以建立排程來自動備份。</span><span class="sxs-lookup"><span data-stu-id="691de-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="691de-142">設定新的自動備份排程</span><span class="sxs-lookup"><span data-stu-id="691de-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="691de-143">若要設定備份排程，請傳送 **POST** 要求至 **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**。</span><span class="sxs-lookup"><span data-stu-id="691de-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="691de-144">範例網站的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="691de-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="691de-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="691de-146">要求本文必須有指定備份組態的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="691de-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="691de-147">以下是具有所有必要參數的範例。</span><span class="sxs-lookup"><span data-stu-id="691de-147">Here is an example with all the required parameters.</span></span>

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
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="691de-148">此範例設定應用程式每隔七天自動備份。</span><span class="sxs-lookup"><span data-stu-id="691de-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="691de-149">**frequencyInterval** 和 **frequencyUnit** 參數一起決定備份的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="691de-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="691de-150">**frequencyUnit** 的有效值為**小時**和**天**。</span><span class="sxs-lookup"><span data-stu-id="691de-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="691de-151">例如，若要每 12 小時備份一次應用程式，請將 frequencyInterval 設為 12，並將 frequencyUnit 設為小時。</span><span class="sxs-lookup"><span data-stu-id="691de-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="691de-152">系統會自動移除儲存體帳戶中的舊有備份。</span><span class="sxs-lookup"><span data-stu-id="691de-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="691de-153">您可以藉由設定 **retentionPeriodInDays** 參數來控制舊有備份的保留期。</span><span class="sxs-lookup"><span data-stu-id="691de-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="691de-154">如果您想要永遠儲存至少一個備份，不論它已存在多久，請將 **keepAtLeastOneBackup** 設為 true。</span><span class="sxs-lookup"><span data-stu-id="691de-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="691de-155">取得自動備份排程</span><span class="sxs-lookup"><span data-stu-id="691de-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="691de-156">若要取得應用程式的備份設定，請傳送 **POST** 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**。</span><span class="sxs-lookup"><span data-stu-id="691de-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="691de-157">我們的範例站台 URL 是 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**。</span><span class="sxs-lookup"><span data-stu-id="691de-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="691de-158">取得備份狀態</span><span class="sxs-lookup"><span data-stu-id="691de-158">Get the status of a backup</span></span>
<span data-ttu-id="691de-159">視應用程式的大小而定，備份程序可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="691de-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="691de-160">備份程序也可能失敗、逾時或是部分成功。</span><span class="sxs-lookup"><span data-stu-id="691de-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="691de-161">若要查看所有應用程式的備份狀態，請傳送 **GET** 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**。</span><span class="sxs-lookup"><span data-stu-id="691de-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="691de-162">若要查看特定備份的狀態，請傳送 GET 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**。</span><span class="sxs-lookup"><span data-stu-id="691de-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="691de-163">範例網站的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="691de-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="691de-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="691de-165">回應本文會包含類似此範例的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="691de-165">The response body contains a JSON object similar to this example.</span></span>

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

<span data-ttu-id="691de-166">備份狀態是列舉的類型。</span><span class="sxs-lookup"><span data-stu-id="691de-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="691de-167">以下是各個可能的狀態。</span><span class="sxs-lookup"><span data-stu-id="691de-167">Here is every possible state.</span></span>

* <span data-ttu-id="691de-168">0 – 進行中：備份已啟動但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="691de-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="691de-169">1 – 失敗：備份未能成功。</span><span class="sxs-lookup"><span data-stu-id="691de-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="691de-170">2 – 成功：已成功完成備份。</span><span class="sxs-lookup"><span data-stu-id="691de-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="691de-171">3 – 逾時：備份未能及時完成，因此已取消。</span><span class="sxs-lookup"><span data-stu-id="691de-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="691de-172">4 - 已建立：備份要求已排入佇列，但尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="691de-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="691de-173">5 - 略過：未進行備份，因為排程觸發了太多備份。</span><span class="sxs-lookup"><span data-stu-id="691de-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="691de-174">6 – 部分成功：備份成功，但某些檔案因為無法讀取而未能予以備份。</span><span class="sxs-lookup"><span data-stu-id="691de-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="691de-175">會發生此狀況通常是因為檔案已遭到獨佔鎖定。</span><span class="sxs-lookup"><span data-stu-id="691de-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="691de-176">7 – 正在進行刪除：已要求刪除備份，但系統尚未刪除。</span><span class="sxs-lookup"><span data-stu-id="691de-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="691de-177">8 - 刪除失敗：無法刪除備份。</span><span class="sxs-lookup"><span data-stu-id="691de-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="691de-178">會發生此狀況通常是因為用來建立備份的 SAS URL 已過期。</span><span class="sxs-lookup"><span data-stu-id="691de-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="691de-179">9 - 已刪除：已成功刪除備份。</span><span class="sxs-lookup"><span data-stu-id="691de-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="691de-180">從備份還原應用程式</span><span class="sxs-lookup"><span data-stu-id="691de-180">Restore an app from a backup</span></span>
<span data-ttu-id="691de-181">如果應用程式遭到刪除，或是當您想要把應用程式還原為較舊的版本時，您可以從備份還原應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="691de-182">若要叫用還原，請傳送 **POST** 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**。</span><span class="sxs-lookup"><span data-stu-id="691de-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="691de-183">範例網站的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="691de-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="691de-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="691de-185">在要求本文中，傳送包含還原作業屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="691de-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="691de-186">以下是包含所有必要屬性的範例：</span><span class="sxs-lookup"><span data-stu-id="691de-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="691de-187">還原成新的應用程式</span><span class="sxs-lookup"><span data-stu-id="691de-187">Restore to a new app</span></span>
<span data-ttu-id="691de-188">當您在還原備份時，可能有時您會想要建立新的 Web 應用程式，而非覆寫現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="691de-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="691de-189">方法是變更要求 URL 來指向您要建立的新應用程式，然後把 JSON 中的 **overwrite** 屬性變更為 **false**。</span><span class="sxs-lookup"><span data-stu-id="691de-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="691de-190">刪除應用程式備份</span><span class="sxs-lookup"><span data-stu-id="691de-190">Delete an app backup</span></span>
<span data-ttu-id="691de-191">如果您想要刪除備份，請傳送 **DELETE** 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**。</span><span class="sxs-lookup"><span data-stu-id="691de-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="691de-192">範例網站的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="691de-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="691de-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="691de-194">管理備份的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="691de-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="691de-195">Azure App Service 會嘗試使用備份建立時所提供的 SAS URL，來刪除 Azure 儲存體中的備份。</span><span class="sxs-lookup"><span data-stu-id="691de-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="691de-196">如果此 SAS URL 不再有效，就無法透過 REST API 刪除備份。</span><span class="sxs-lookup"><span data-stu-id="691de-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="691de-197">不過，您可以更新與備份相關聯的 SAS URL，方法為傳送 **POST** 要求至 URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**。</span><span class="sxs-lookup"><span data-stu-id="691de-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="691de-198">範例網站的 URL 看起來就像這樣。</span><span class="sxs-lookup"><span data-stu-id="691de-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="691de-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="691de-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="691de-200">在要求本文中，傳送包含新的 SAS URL 的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="691de-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="691de-201">範例如下。</span><span class="sxs-lookup"><span data-stu-id="691de-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="691de-202">為了確保安全，在傳送特定備份的 GET 要求時，並不會傳回與該備份相關聯的 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="691de-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="691de-203">如果您想要檢視與備份相關聯的 SAS URL，請傳送 POST 要求給上述的同一個 URL。</span><span class="sxs-lookup"><span data-stu-id="691de-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="691de-204">在要求本文中包含空的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="691de-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="691de-205">伺服器所傳回的回應中便會包含該備份的所有資訊，包括其 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="691de-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
