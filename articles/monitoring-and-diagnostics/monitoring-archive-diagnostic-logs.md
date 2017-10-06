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
# <a name="archive-azure-diagnostic-logs"></a>封存 Azure 診斷記錄
在本文中，我們示範如何使用 hello Azure 入口網站、 PowerShell Cmdlet，CLI，或 REST API tooarchive 您[Azure 診斷的記錄檔](monitoring-overview-of-diagnostic-logs.md)儲存體帳戶中。 這個選項非常有用，如果您想要的 tooretain 您診斷記錄與稽核、 靜態分析或備份的選擇性的保留原則。 hello 儲存體帳戶中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 資源相同訂用帳戶。

## <a name="prerequisites"></a>必要條件
在開始之前，您需要太[建立儲存體帳戶](../storage/storage-create-storage-account.md)toowhich 可以保存您的診斷記錄檔。 我們強烈建議您務必使用現有的儲存體帳戶具有其他非監視資料，讓您更能夠控制存取 toomonitoring 資料儲存在其中。 不過，如果您的活動記錄檔和診斷度量 tooa 儲存體帳戶時，您也要封存，它會使意義 toouse 該儲存體帳戶您診斷記錄檔以及 tookeep 監視的所有資料在集中位置。 您使用的 hello 儲存體帳戶必須是一般用途儲存體帳戶，而不是 blob 儲存體帳戶。

## <a name="diagnostic-settings"></a>診斷設定
設定您的診斷記錄使用任何下列的 hello 方法 tooarchive，**診斷設定**特定資源。 資源的診斷設定定義 hello 類別的記錄檔和度量資料傳送 tooa 目的地 （儲存體帳戶、 事件中樞命名空間或記錄分析）。 它也會定義事件的每個記錄檔類別目錄和度量資料儲存在儲存體帳戶中的 hello 保留原則 （天 tooretain 數目）。 如果 toozero 設定保留原則，該記錄檔類別目錄的事件會無限期地儲存 （亦即 toosay，不限次數）。 否則，保留原則可以是 1 到 2147483647 之間的任何天數。 [您可以在此深入了解診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。 保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則將會被刪除。 例如，如果您在一天的保留原則，在今天 hello 天 hello 開頭 hello hello 天前昨天的記錄檔，就會刪除

## <a name="archive-diagnostic-logs-using-hello-portal"></a>封存使用 hello 入口網站的診斷記錄檔
1. 在 hello 入口網站中，瀏覽 tooAzure 監視器並按一下**診斷設定**

    ![Azure 監視器的監視區段](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. 選擇性地篩選資源群組或資源類型的 hello 清單，然後按一下 hello 資源，您想要 tooset 診斷設定。

3. 如果您選取的 hello 資源上有沒有設定，您必須提示的 toocreate 設定。 按一下「開啟診斷」。

   ![新增診斷設定 - 無現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   如果 hello 資源上的現有設定，您會看到已設定此資源上設定的清單。 按一下「新增診斷設定」。

   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. 提供設定名稱，並核取方塊 hello**匯出 tooStorage 帳戶**，然後選取 儲存體帳戶。 （選擇性） 設定的天數 tooretain 數，這些記錄檔使用 hello**保留 （天）**滑桿。 保留的天數零會無限期儲存 hello 記錄檔。
   
   ![新增診斷設定 - 現有的設定](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. 按一下 [儲存] 。

在幾分鐘之後, hello 新設定，會出現在此資源，設定的清單，且診斷記錄檔是封存的 toothat 儲存體帳戶只要產生新的事件資料。

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>透過 Azure PowerShell 封存診斷記錄
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| ResourceId |是 |您想要在其上 tooset 診斷設定的 hello 資源的資源識別碼。 |
| StorageAccountId |否 |應該儲存 hello 儲存體帳戶 toowhich 診斷記錄檔的資源識別碼。 |
| 類別 |否 |以逗號分隔的記錄檔分類 tooenable 清單。 |
| 已啟用 |是 |布林值，表示要對資源啟用還是停用診斷。 |
| RetentionEnabled |否 |布林值，表示此資源是否啟用保留原則。 |
| RetentionInDays |否 |事件應保留的天數，1 到 2147483647 之間。 值為 0 會無限期儲存 hello 記錄檔。 |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>封存 hello 跨平台 CLI 透過診斷記錄檔
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| ResourceId |是 |您想要在其上 tooset 診斷設定的 hello 資源的資源識別碼。 |
| storageId |否 |應該儲存 hello 儲存體帳戶 toowhich 診斷記錄檔的資源識別碼。 |
| 類別 |否 |以逗號分隔的記錄檔分類 tooenable 清單。 |
| 已啟用 |是 |布林值，表示要對資源啟用還是停用診斷。 |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>封存透過 hello REST API 的診斷記錄檔
[請參閱本文件](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)有關您可以設定使用 hello Azure 監視 REST API 的診斷設定。

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Hello 儲存體帳戶中的診斷記錄檔的結構描述
在您設定保存，儲存體容器被建立 hello 儲存體帳戶中，只要您已啟用的 hello 記錄類別的其中一個發生的事件。 相同跨診斷記錄檔格式的 hello 與 hello 活動記錄檔，請依照下列 hello hello 容器內的 blob。 這些 blob hello 結構是：

> insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

或者，形式更簡單，

> insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
> 
> 

例如，blob 名稱可能是︰

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

每個 PT1H.json blob 包含 JSON blob hello hello blob URL 中指定的一小時內發生的事件 (例如，h = 12)。 Hello 存在小時，在事件發生時是附加的 toohello PT1H.json 檔案。 hello 分鐘值 (m = 00) 一定是 00，因為診斷記錄檔事件會分為個別每小時的 blob。

在 hello PT1H.json 檔案中，每個事件會儲存在 hello 「 記錄 」 陣列中，遵循此格式：

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

| 元素名稱 | 說明 |
| --- | --- |
| 分析 |Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。 |
| resourceId |資源識別碼 hello 影響資源。 |
| operationName |Hello 作業的名稱。 |
| category |Hello 事件記錄檔類別目錄。 |
| 屬性 |一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。 |

> [!NOTE]
> hello 屬性和這些屬性的使用方式有所不同 hello 資源。
> 
> 

## <a name="next-steps"></a>後續步驟
* [下載 blob 以供分析](../storage/storage-dotnet-how-to-use-blobs.md)
* [資料流診斷記錄 tooan 事件中樞命名空間](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [深入了解診斷記錄](monitoring-overview-of-diagnostic-logs.md)
