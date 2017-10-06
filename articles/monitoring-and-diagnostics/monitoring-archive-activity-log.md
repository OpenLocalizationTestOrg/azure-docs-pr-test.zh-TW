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
# <a name="archive-hello-azure-activity-log"></a>封存 hello Azure 活動記錄檔
在本文中，我們示範如何使用 hello Azure 入口網站、 PowerShell 指令程式或跨平台 CLI tooarchive 您[ **Azure 活動記錄檔**](monitoring-overview-activity-logs.md)儲存體帳戶中。 這個選項非常有用，如果您想要的 tooretain 您活動記錄中超過 90 天 （具有完整控制權 hello 保留原則的詳細資訊） 的稽核，靜態分析，或備份。 如果您只需要 tooretain 事件 90 天或更少，您不需要 tooset 保存 tooa 儲存體帳戶，因為活動記錄檔事件會保留在 hello Azure 平台 90 天內沒有啟用封存。

## <a name="prerequisites"></a>必要條件
在開始之前，您需要太[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)toowhich 可以封存活動記錄。 我們強烈建議您務必使用現有的儲存體帳戶具有其他非監視資料，讓您更能夠控制存取 toomonitoring 資料儲存在其中。 不過，如果您也要封存診斷記錄檔和度量 tooa 儲存體帳戶，它會使意義 toouse 該儲存體帳戶為您的活動記錄檔以及 tookeep 監視的所有資料在集中位置。 您使用的 hello 儲存體帳戶必須是一般用途儲存體帳戶，而不是 blob 儲存體帳戶。 hello 儲存體帳戶中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 訂用帳戶相同訂用帳戶。

## <a name="log-profile"></a>記錄檔設定檔
tooarchive hello 使用任何下列的 hello 方法的活動記錄檔，設定 hello**記錄檔的設定檔**訂用帳戶。 hello 記錄檔的設定檔定義 hello 儲存或資料流處理之事件的類型與 hello 輸出-儲存體帳戶及/或事件中樞。 它也會定義事件儲存在儲存體帳戶中的 hello 保留原則 （天 tooretain 數目）。 如果 hello 保留原則設定 toozero，事件會無限期儲存。 否則，這可以設定 tooany 值介於 1 到 2147483647 之間。 保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則將會被刪除。 例如，如果您在一天的保留原則，hello 從今天 hello 日開始時 hello hello 天前昨天的記錄檔會刪除。 [您可以至此處閱讀記錄檔設定檔的相關資訊](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)。 

## <a name="archive-hello-activity-log-using-hello-portal"></a>封存 hello 使用 hello 入口網站的活動記錄檔
1. 在 hello 入口網站中，按一下 hello**活動記錄檔**hello 左側導覽上的連結。 如果您沒有看到 hello 活動記錄檔的連結，按一下 hello**更服務**連結第一次。
   
    ![瀏覽 tooActivity 記錄刀鋒視窗](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. 在 hello hello 刀鋒視窗頂端，按一下**匯出**。
   
    ![按一下 hello 匯出按鈕](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. 在出現的 hello 刀鋒視窗，勾選 [hello] 方塊**tooa 儲存體帳戶匯出**並選取儲存體帳戶。
   
    ![設定儲存體帳戶](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. 使用 hello 滑桿或文字方塊中，定義的活動記錄檔事件應該保持儲存體帳戶中的天數。 如果您偏好的 toohave 資料無限期地保存 hello 儲存體帳戶中，設定此數字 toozero。
5. 按一下 [儲存] 。

## <a name="archive-hello-activity-log-via-powershell"></a>封存 hello 透過 PowerShell 活動記錄檔
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| StorageAccountId |否 |應該儲存 hello 儲存體帳戶 toowhich 活動記錄檔的資源識別碼。 |
| 位置 |是 |以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。 您可以檢視所有區域的清單[造訪此頁](https://azure.microsoft.com/en-us/regions)或使用[hello Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。 |
| RetentionInDays |是 |事件應保留的天數，1 到 2147483647 之間。 值為 0 會無限期儲存 hello 記錄檔 （永久）。 |
| 類別 |是 |以逗號分隔的類別清單，其中列出應該收集的事件類別。 可能的值有 Write、Delete、Action。 |

## <a name="archive-hello-activity-log-via-cli"></a>封存 hello 透過 CLI 活動記錄檔
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| 名稱 |是 |記錄檔設定檔的名稱。 |
| storageId |否 |應該儲存 hello 儲存體帳戶 toowhich 活動記錄檔的資源識別碼。 |
| 位置 |是 |以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。 您可以檢視所有區域的清單[造訪此頁](https://azure.microsoft.com/en-us/regions)或使用[hello Azure 管理 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)。 |
| RetentionInDays |是 |事件應保留的天數，1 到 2147483647 之間。 零值將會無限期儲存 hello 記錄檔 （永久）。 |
| 類別 |是 |以逗號分隔的類別清單，其中列出應該收集的事件類別。 可能的值有 Write、Delete、Action。 |

## <a name="storage-schema-of-hello-activity-log"></a>儲存結構描述的 hello 活動記錄檔
在您設定保存，儲存體容器將建立 hello 儲存體帳戶中，只要發生活動記錄檔事件。 hello 容器中的 hello blob 遵循的 hello 相同格式跨 hello 活動記錄檔和診斷記錄檔。 這些 blob hello 結構是：

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

例如，blob 名稱可能是︰

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

每個 PT1H.json blob 包含 JSON blob hello hello blob URL 中指定的一小時內發生的事件 (例如 h = 12)。 Hello 存在小時，在事件發生時是附加的 toohello PT1H.json 檔案。 hello 分鐘值 (m = 00) 一定是 00，因為活動記錄檔事件會分為個別每小時的 blob。

在 hello PT1H.json 檔案中，每個事件會儲存在 hello 「 記錄 」 陣列中，遵循此格式：

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


| 元素名稱 | 說明 |
| --- | --- |
| 分析 |Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。 |
| resourceId |資源識別碼 hello 影響資源。 |
| operationName |Hello 作業的名稱。 |
| category |分類的 hello 動作，例如。 寫入、讀取、動作。 |
| resultType |例如 hello hello 結果的型別。 成功、失敗、開始 |
| resultSignature |Hello 資源類型而定。 |
| durationMs |以毫秒為單位的 hello 作業的持續時間 |
| callerIpAddress |已執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的 IP 位址。 |
| correlationId |通常是 hello 字串格式 GUID。 共用的相互關聯識別碼的事件屬於 toohello 相同超級動作。 |
| 身分識別 |Hello 授權和宣告描述的 JSON blob。 |
| 授權 |Blob hello 事件的 RBAC 屬性。 通常包含 hello 「 動作 」、 「 角色 」 和 「 範圍 」 屬性。 |
| 層級 |Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」 |
| location |Hello 位置發生 （或全域） 中的區域。 |
| 屬性 |一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。 |

> [!NOTE]
> hello 屬性和這些屬性的使用方式有所不同 hello 資源。
> 
> 

## <a name="next-steps"></a>後續步驟
* [下載 blob 以供分析](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [資料流 hello 活動記錄檔 tooEvent 集線器](monitoring-stream-activity-logs-event-hubs.md)
* [深入了解 hello 活動記錄檔](monitoring-overview-activity-logs.md)

