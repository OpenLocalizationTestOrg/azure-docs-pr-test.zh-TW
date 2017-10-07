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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>使用 REST tooback] 和 [還原 App Service 應用程式
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

[App Service 應用程式](https://azure.microsoft.com/services/app-service/web/) 可以備份成 Azure 儲存體中的 blob。 hello 備份也可以包含 hello 應用程式資料庫。 如果曾不小心刪除 hello 應用程式，或 hello 應用程式需求 toobe 還原 tooa 先前的版本，便可以從任何先前的備份還原。 您可以視需要隨時進行備份，或排定在間隔適當時間後進行備份。

本文說明如何 toobackup 和還原應用程式，但 rest 式 API 要求。 如果您會喜歡 toocreate，且管理應用程式備份，以圖形方式透過 hello Azure 入口網站，請參閱[備份 Azure App Service 中的 web 應用程式](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>開始使用
toosend REST 要求時，您的應用程式需要 tooknow**名稱**，**資源群組**，和**訂用帳戶 id**。可以找到此資訊，按一下您的應用程式在 hello **App Service**刀鋒視窗中的 hello [Azure 入口網站](https://portal.azure.com)。 如需本文章中的 hello 範例，我們要設定 hello 網站**backuprestoreapiexamples.azurewebsites.net**。 它會儲存在 hello Uswest-預設的 Web 資源群組，且正在執行以 hello 識別碼 00001111-2222年-3333-4444-555566667777 訂用帳戶。

![範例網站資訊][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>備份和還原 REST API
現在，我們將討論如何 toouse hello REST API toobackup 和還原應用程式的幾個範例。 每個範例都包含 URL 和 HTTP 要求本文。 hello 範例 URL 會包含預留位置包裝在大括號，例如 {訂閱 id}。 Hello 預留位置取代為 hello 應用程式的對應資訊。 如需參考，這裡是 hello 範例 Url 中會顯示每個預留位置的說明。

* 訂用帳戶 id – hello Azure 訂用帳戶包含 hello 應用程式的識別碼
* 資源-群組-名稱 – hello 資源群組包含 hello 應用程式的名稱
* 名稱 – hello 應用程式的名稱
* 備份-識別碼 – 識別碼 hello 應用程式備份

如 hello hello 應用程式開發介面的完整文件，包括數個選擇性參數可以包含在 hello HTTP 要求中，請參閱 hello [Azure 資源總管](https://resources.azure.com/)。

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>視需求備份應用程式
設定應用程式的 tooback 立即傳送**POST**要求太**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/備份 /**。

以下是 hello URL 看起來像使用我們的範例網站。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

提供的 JSON 物件的儲存體帳戶 toouse toostore hello 備份您的要求 toospecify hello 主體中。 hello JSON 物件必須有一個名為屬性**storageAccountUrl**，一個保存[SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md)授與寫入權限 toohello Azure 儲存體容器，其中含有 hello 備份 blob。 如果您想 tooback 資料庫時，您也必須提供包含 hello 名稱、 類型和備份 hello 資料庫 toobe 的連接字串的清單。

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

立即收到 hello 要求時，才會開始 hello 應用程式的備份。 hello 備份程序可能需要很長的時間 toocomplete。 hello HTTP 回應會包含您可以使用在另一個要求 toosee hello hello 備份的狀態識別碼。 以下是主體的範例的 hello hello HTTP 回應 tooour 備份要求。

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
> 錯誤訊息可以找到 hello HTTP 回應 hello 記錄屬性中。
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>排程自動備份
在 設定應用程式的隨選加法 toobacking，您也可以自動排程備份 toohappen。

### <a name="set-up-a-new-automatic-backup-schedule"></a>設定新的自動備份排程
備份排程，tooset 傳送**放**要求太**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config備份/**。

以下是 hello URL 我們的範例網站的外觀。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

hello 要求主體必須具有指定 hello 備份設定的 JSON 物件。 以下是範例與 hello 所需的所有參數。

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

這個範例會設定 hello 應用程式 toobe 耐用性 — 每隔七天。 hello 參數**frequencyInterval**和**frequencyUnit**同時決定頻率 hello 備份，就可能發生。 **frequencyUnit** 的有效值為**小時**和**天**。 例如，設定應用程式的每隔 12 小時，tooback 設定 frequencyInterval too12 和 frequencyUnit toohour。

從 hello 儲存體帳戶，會自動移除舊的備份。 您可以控制備份可以藉由在設定 hello 舊 hello **retentionPeriodInDays**參數。 如果您想 tooalways 有至少一個儲存，不論它，設定舊的備份**keepAtLeastOneBackup** tootrue。

### <a name="get-hello-automatic-backup-schedule"></a>取得 hello 自動備份排程
tooget 應用程式的備份設定，請傳送**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/站台 / {name} / config/備份列出**。

我們的範例網站 hello url **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**。

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>取得備份的 hello 狀態
根據多大的 hello 應用程式時，備份可能需要一些時間 toocomplete。 備份程序也可能失敗、逾時或是部分成功。 toosee hello 狀態的所有應用程式的備份，傳送給**取得**要求 toohello URL **https://management.azure.com/subscriptions/ {訂閱 id} /resourceGroups/ {資源-群組-名稱} /providers/Microsoft.Web/sites/{name}/backups**。

toosee hello 狀態的特定備份，傳送 GET 要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ {備份-識別碼}**。

以下是 hello URL 我們的範例網站的外觀。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

hello 回應主體包含 JSON 物件類似 toothis 範例。

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

備份 hello 狀態是列舉型別。 以下是各個可能的狀態。

* 0 – InProgress: hello 備份已啟動，但尚未完成。
* 1 – 失敗： hello 備份未成功。
* 2 – 成功： hello 備份順利完成。
* 3 – 逾時： hello 備份未完成的時間，而被取消。
* 4 – 建立： hello 備份要求排入佇列，但尚未啟動。
* 5 – 略過： hello 備份尚未進行 tooa 排程觸發太多備份到期。
* 6 – PartiallySucceeded: hello 備份成功，但無法備份部分檔案，因為無法讀取。 因為已在 hello 檔案上設定的獨佔鎖定，就會發生這種情形。
* 7 – DeleteInProgress: hello 備份已經刪除，要求的 toobe，但尚未刪除。
* 8 – DeleteFailed： 無法刪除 hello 備份。 這可能是因為 hello SAS URL 是使用的 toocreate hello 備份已過期。
* 9 – 刪除： hello 備份已成功刪除。

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>從備份還原應用程式
如果您的應用程式已遭刪除，或如果您想 toorevert 應用程式 tooa 舊版本，您可以從備份還原 hello 應用程式。 tooinvoke 還原，傳送**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/備份 / {備份-識別碼} / 還原**。

以下是 hello URL 我們的範例網站的外觀。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

在 hello 要求主體中，傳送包含 hello 還原作業的 hello 屬性的 JSON 物件。 以下是包含所有必要屬性的範例：

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

### <a name="restore-tooa-new-app"></a>還原 tooa 新應用程式
有時候您可能想 toocreate 新的應用程式，當您還原的備份，而非覆寫現有的應用程式。 toodo，變更 hello 要求 URL toopoint toohello 新應用程式 toocreate，並變更 hello**覆寫**中的屬性太 hello JSON**false**。

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>刪除應用程式備份
如果您想要備份 toodelete，傳送**刪除**要求 toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/站台 / {name} /backups/ {備份-識別碼}**。

以下是 hello URL 我們的範例網站的外觀。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>管理備份的 SAS URL
Azure 應用程式服務將嘗試 toodelete 您從使用 hello 時建立 hello 備份應用程式提供的 SAS URL 的 Azure 儲存體的備份。 如果此 SAS URL 已不再有效，無法透過 hello REST API 會刪除 hello 備份。 不過，您可以更新 SAS URL 與備份相關聯的傳送的嗨**POST**要求 toohello URL **https://management.azure.com/subscriptions/ {訂閱 id} /resourceGroups/ {資源-群組-名稱} /providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**。

以下是 hello URL 我們的範例網站的外觀。 **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

在 hello 要求主體中，傳送包含 hello 新 SAS URL 的 JSON 物件。 範例如下。

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> 基於安全性理由，傳送 GET 要求進行特定的備份時，不會傳回的 hello 與備份相關聯的 SAS URL。 如果您想 tooview hello 與備份相關聯的 SAS URL，傳送 POST 要求 toohello 上述相同的 URL。 Hello 要求主體中包含空白的 JSON 物件。 hello 回應 hello 伺服器包含所有的備份的資訊，包括其 SAS URL。
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
