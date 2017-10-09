---
title: "aaaLog 分析記錄搜尋 REST API |Microsoft 文件"
description: "本指南提供基本教學課程，描述如何使用 hello 記錄分析搜尋 REST API 中的 hello Operations Management Suite (OMS)，並提供範例，教您如何 toouse hello 命令。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>Log Analytics 記錄檔搜尋 REST API
本指南提供基本教學課程，包括範例，您可以如何使用 hello 記錄分析搜尋 REST API。 記錄分析是 hello Operations Management Suite (OMS) 的一部分。

> [!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您應該繼續與 hello 記錄搜尋 API toouse hello 舊版的查詢語言，這篇文章中所述。  新的應用程式開發介面就會發行升級後的工作區，並會在該時間更新 hello 文件。 

> [!NOTE]
> 記錄分析前稱為 Operational Insights，這也是為什麼 hello hello 資源提供者中使用的名稱。
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Hello 記錄搜尋 REST API 的概觀
hello 記錄分析搜尋 REST API 是 RESTful，而且可以透過 hello Azure 資源管理員 API 存取。 本文提供的存取透過 hello API 範例[ARMClient](https://github.com/projectkudu/ARMClient)，簡化叫用的開放原始碼命令列工具 hello Azure 資源管理員 API。 使用 ARMClient hello 是許多選項 tooaccess hello 記錄分析搜尋 API 的其中一個。 另一個選項是 OperationalInsights，其中包含用於存取搜尋 cmdlet toouse hello Azure PowerShell 模組。 使用這些工具，您可以利用 hello Azure 資源管理員 API toomake 呼叫 tooOMS 工作區，以及它們在執行搜尋命令。 hello API 輸出搜尋結果以 JSON 格式，可讓您 toouse hello 搜尋結果中許多不同的方式以程式設計的方式。

hello Azure 資源管理員可透過[.NET 程式庫](https://msdn.microsoft.com/library/azure/dn910477.aspx)和 hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx)。 toolearn 詳細資訊，請檢閱 hello 連結 web 網頁。

> [!NOTE]
> 如果您使用的彙總命令，例如`|measure count()`或`distinct`，每個呼叫 toosearch 可以傳回最多 500,000 個記錄。 不含彙總命令的搜尋最多傳回 5,000 筆記錄。
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>基本 Log Analytics 搜尋 REST API 教學課程
### <a name="toouse-armclient"></a>toouse ARMClient
1. 安裝 [Chocolatey](https://chocolatey.org/)，這是適用於 Windows 的開放原始碼封裝管理員。 開啟命令提示字元視窗，以系統管理員身分，並執行下列命令的 hello:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. 執行下列命令的 hello 來安裝 ARMClient:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>使用 ARMClient 搜尋 tooperform
1. 使用您的 Microsoft 帳戶、公司帳戶或學校帳戶登入：

    ```
    armclient login
    ```

    成功的登入會列出指定帳戶的所有繫結訂用 toohello:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. 取得 hello Operations Management Suite 工作區：

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    成功的 Get 呼叫會輸出所有的工作區繫結 toohello 訂用帳戶：

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. 建立您的搜尋變數：

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. 使用新的搜尋變數來搜尋：

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Log Analytics 搜尋 REST API 參考範例
hello 遵循範例會示範如何使用 Search API hello。

### <a name="search---actionread"></a>搜尋 - 動作/讀取
**範例 Url：**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**要求：**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
hello 下表描述可用的 hello 屬性。

| **屬性** | **說明** |
| --- | --- |
| top |hello 結果 tooreturn 的數目上限。 |
| highlight |包含 pre 和 post 參數，通常用於反白顯示比對欄位 |
| pre |Hello 給定字串 tooyour 比對欄位的前置詞。 |
| post |將附加 hello 給定字串 tooyour 比對欄位。 |
| query |使用 toocollect hello 搜尋查詢，並傳回結果。 |
| start |您想要從其中找到結果 toobe hello 時間範圍 hello 開頭。 |
| end |hello 與您想要從其中找到結果 toobe hello 時間視窗結尾。 |

**回應：**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>搜尋/{ID} - 動作/讀取
**要求已儲存搜尋的 hello 的內容：**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> 如果 hello 搜尋會傳回 「 擱置中 」 狀態，然後輪詢更新的 hello 結果可以透過此 API 完成。 6 分鐘後 hello 搜尋結果的 hello 皆會予以捨棄從 hello 快取，並將傳回 HTTP Gone。 如果 hello 初始搜尋要求立即傳回 「 成功 」 狀態，hello 結果不會新增 toohello 快取，使 HTTP Gone 此 API tooreturn，如果查詢。 hello HTTP 200 結果內容位於的 hello 相同格式化為 hello 初始搜尋要求和更新值。
>
>

### <a name="saved-searches"></a>已儲存的搜尋
**已儲存搜尋的要求清單：**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

支援的方法：GET PUT DELETE

支援的收集方法：GET

hello 下表描述可用的 hello 屬性。

| 屬性 | 說明 |
| --- | --- |
| 識別碼 |hello 唯一識別項。 |
| Etag |**修補程式的必要項目**。 每次寫入時由伺服器進行更新。 值必須等於 toohello 目前儲存的值或 ' *' tooupdate。 舊值/無效值時會傳回 409。 |
| properties.query |**必要**。 hello 搜尋查詢。 |
| properties.displayName |**必要**。 hello hello 查詢的使用者定義的顯示名稱。 |
| properties.category |**必要**。 hello 使用者定義的分類 hello 查詢。 |

> [!NOTE]
> hello 記錄分析搜尋 API 目前會傳回使用者建立已儲存的搜尋時工作區中的儲存搜尋的輪詢。 hello 應用程式開發介面不會傳回儲存的搜尋解決方案所提供。
>
>

### <a name="create-saved-searches"></a>建立已儲存的搜尋
**要求：**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> 所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。

### <a name="delete-saved-searches"></a>刪除儲存搜尋
**要求：**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>更新儲存搜尋
 **要求：**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>中繼資料 - 僅限 JSON
以下是 hello 資料收集工作區中的所有記錄檔類型的方式 toosee hello 欄位。 例如，如果您想知道是否 hello 事件類型是否具有名為電腦的欄位，然後此查詢是其中一種方式 toocheck。

**欄位要求：**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**回應：**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

hello 下表描述可用的 hello 屬性。

| **屬性** | **說明** |
| --- | --- |
| 名稱 |欄位名稱。 |
| displayName |hello 顯示 hello 欄位的名稱。 |
| 類型 |hello hello 欄位值的型別。 |
| 可面向化 |目前 ‘indexed’、‘stored ‘和 ‘facet’ 屬性的組合。 |
| 顯示 |目前 ‘display’ 屬性。 如果欄位顯示在搜尋中，則為 True。 |
| ownerType |降低的 tooonly 屬於 tooonboarded IP 型別。 |

## <a name="optional-parameters"></a>選擇性參數
hello 下列資訊描述可用的選擇性參數。

### <a name="highlighting"></a>醒目提示
hello"Highlight"參數是選擇性參數，您可以用 toorequest hello 搜尋子系統在其回應中包含的一組標記。

這些標記表示 hello 開頭與結尾的反白顯示的文字，以符合您的搜尋查詢中所提供的 hello 詞彙。
您可以指定 hello 開始和結束標記所使用的字詞 toowrap hello 反白顯示。

**範例搜尋查詢**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**範例結果：**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

請注意，hello 上述結果包含已做為前置詞及附加詞的錯誤訊息。

## <a name="computer-groups"></a>電腦群組
電腦群組是一種特殊的已儲存搜尋，其會傳回一組電腦。  您可以使用電腦群組中的其他查詢 toolimit hello 結果 toohello 電腦 hello 群組中。  電腦群組會實作為已儲存的搜尋，其含有 Group 標籤與 Computer 值。

以下是電腦群組的回應範例。

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>擷取電腦群組
tooretrieve 電腦群組，請使用 hello Get 方法與 hello 群組識別碼。

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>建立或更新電腦群組
toocreate 電腦群組，並提供唯一的儲存的搜尋的識別碼。 使用 hello Put 方法 如果您使用現有的電腦群組識別碼，則系統會修改它。 當您在 hello 記錄分析入口網站中建立電腦群組時，則會建立 hello 識別碼 hello 群組與名稱。

用於 hello 群組定義的 hello 查詢必須正確地傳回一組 hello 群組 toofunction 的電腦。  建議您結束與查詢`| Distinct Computer`tooensure hello 正確傳回資料。

儲存搜尋的 hello 的 hello 定義必須包含值的電腦是具名群組的 hello 搜尋 toobe 歸類為電腦群組的標記。

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>刪除電腦群組
toodelete 電腦群組，請使用 hello Delete 方法與 hello 群組識別碼。

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢準則中使用自訂欄位。
