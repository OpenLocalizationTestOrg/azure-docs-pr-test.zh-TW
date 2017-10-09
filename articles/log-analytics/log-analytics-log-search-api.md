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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="f8631-103">Log Analytics 記錄檔搜尋 REST API</span><span class="sxs-lookup"><span data-stu-id="f8631-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="f8631-104">本指南提供基本教學課程，包括範例，您可以如何使用 hello 記錄分析搜尋 REST API。</span><span class="sxs-lookup"><span data-stu-id="f8631-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="f8631-105">記錄分析是 hello Operations Management Suite (OMS) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f8631-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="f8631-106">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您應該繼續與 hello 記錄搜尋 API toouse hello 舊版的查詢語言，這篇文章中所述。</span><span class="sxs-lookup"><span data-stu-id="f8631-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="f8631-107">新的應用程式開發介面就會發行升級後的工作區，並會在該時間更新 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="f8631-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="f8631-108">記錄分析前稱為 Operational Insights，這也是為什麼 hello hello 資源提供者中使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8631-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="f8631-109">Hello 記錄搜尋 REST API 的概觀</span><span class="sxs-lookup"><span data-stu-id="f8631-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="f8631-110">hello 記錄分析搜尋 REST API 是 RESTful，而且可以透過 hello Azure 資源管理員 API 存取。</span><span class="sxs-lookup"><span data-stu-id="f8631-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="f8631-111">本文提供的存取透過 hello API 範例[ARMClient](https://github.com/projectkudu/ARMClient)，簡化叫用的開放原始碼命令列工具 hello Azure 資源管理員 API。</span><span class="sxs-lookup"><span data-stu-id="f8631-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="f8631-112">使用 ARMClient hello 是許多選項 tooaccess hello 記錄分析搜尋 API 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="f8631-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="f8631-113">另一個選項是 OperationalInsights，其中包含用於存取搜尋 cmdlet toouse hello Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="f8631-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="f8631-114">使用這些工具，您可以利用 hello Azure 資源管理員 API toomake 呼叫 tooOMS 工作區，以及它們在執行搜尋命令。</span><span class="sxs-lookup"><span data-stu-id="f8631-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="f8631-115">hello API 輸出搜尋結果以 JSON 格式，可讓您 toouse hello 搜尋結果中許多不同的方式以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="f8631-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="f8631-116">hello Azure 資源管理員可透過[.NET 程式庫](https://msdn.microsoft.com/library/azure/dn910477.aspx)和 hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8631-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="f8631-117">toolearn 詳細資訊，請檢閱 hello 連結 web 網頁。</span><span class="sxs-lookup"><span data-stu-id="f8631-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="f8631-118">如果您使用的彙總命令，例如`|measure count()`或`distinct`，每個呼叫 toosearch 可以傳回最多 500,000 個記錄。</span><span class="sxs-lookup"><span data-stu-id="f8631-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="f8631-119">不含彙總命令的搜尋最多傳回 5,000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="f8631-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="f8631-120">基本 Log Analytics 搜尋 REST API 教學課程</span><span class="sxs-lookup"><span data-stu-id="f8631-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="f8631-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="f8631-121">toouse ARMClient</span></span>
1. <span data-ttu-id="f8631-122">安裝 [Chocolatey](https://chocolatey.org/)，這是適用於 Windows 的開放原始碼封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="f8631-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="f8631-123">開啟命令提示字元視窗，以系統管理員身分，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8631-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="f8631-124">執行下列命令的 hello 來安裝 ARMClient:</span><span class="sxs-lookup"><span data-stu-id="f8631-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="f8631-125">使用 ARMClient 搜尋 tooperform</span><span class="sxs-lookup"><span data-stu-id="f8631-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="f8631-126">使用您的 Microsoft 帳戶、公司帳戶或學校帳戶登入：</span><span class="sxs-lookup"><span data-stu-id="f8631-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="f8631-127">成功的登入會列出指定帳戶的所有繫結訂用 toohello:</span><span class="sxs-lookup"><span data-stu-id="f8631-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="f8631-128">取得 hello Operations Management Suite 工作區：</span><span class="sxs-lookup"><span data-stu-id="f8631-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="f8631-129">成功的 Get 呼叫會輸出所有的工作區繫結 toohello 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="f8631-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="f8631-130">建立您的搜尋變數：</span><span class="sxs-lookup"><span data-stu-id="f8631-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="f8631-131">使用新的搜尋變數來搜尋：</span><span class="sxs-lookup"><span data-stu-id="f8631-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="f8631-132">Log Analytics 搜尋 REST API 參考範例</span><span class="sxs-lookup"><span data-stu-id="f8631-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="f8631-133">hello 遵循範例會示範如何使用 Search API hello。</span><span class="sxs-lookup"><span data-stu-id="f8631-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="f8631-134">搜尋 - 動作/讀取</span><span class="sxs-lookup"><span data-stu-id="f8631-134">Search - Action/Read</span></span>
<span data-ttu-id="f8631-135">**範例 Url：**</span><span class="sxs-lookup"><span data-stu-id="f8631-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="f8631-136">**要求：**</span><span class="sxs-lookup"><span data-stu-id="f8631-136">**Request:**</span></span>

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
<span data-ttu-id="f8631-137">hello 下表描述可用的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f8631-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="f8631-138">**屬性**</span><span class="sxs-lookup"><span data-stu-id="f8631-138">**Property**</span></span> | <span data-ttu-id="f8631-139">**說明**</span><span class="sxs-lookup"><span data-stu-id="f8631-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f8631-140">top</span><span class="sxs-lookup"><span data-stu-id="f8631-140">top</span></span> |<span data-ttu-id="f8631-141">hello 結果 tooreturn 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="f8631-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="f8631-142">highlight</span><span class="sxs-lookup"><span data-stu-id="f8631-142">highlight</span></span> |<span data-ttu-id="f8631-143">包含 pre 和 post 參數，通常用於反白顯示比對欄位</span><span class="sxs-lookup"><span data-stu-id="f8631-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="f8631-144">pre</span><span class="sxs-lookup"><span data-stu-id="f8631-144">pre</span></span> |<span data-ttu-id="f8631-145">Hello 給定字串 tooyour 比對欄位的前置詞。</span><span class="sxs-lookup"><span data-stu-id="f8631-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="f8631-146">post</span><span class="sxs-lookup"><span data-stu-id="f8631-146">post</span></span> |<span data-ttu-id="f8631-147">將附加 hello 給定字串 tooyour 比對欄位。</span><span class="sxs-lookup"><span data-stu-id="f8631-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="f8631-148">query</span><span class="sxs-lookup"><span data-stu-id="f8631-148">query</span></span> |<span data-ttu-id="f8631-149">使用 toocollect hello 搜尋查詢，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="f8631-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="f8631-150">start</span><span class="sxs-lookup"><span data-stu-id="f8631-150">start</span></span> |<span data-ttu-id="f8631-151">您想要從其中找到結果 toobe hello 時間範圍 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="f8631-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="f8631-152">end</span><span class="sxs-lookup"><span data-stu-id="f8631-152">end</span></span> |<span data-ttu-id="f8631-153">hello 與您想要從其中找到結果 toobe hello 時間視窗結尾。</span><span class="sxs-lookup"><span data-stu-id="f8631-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="f8631-154">**回應：**</span><span class="sxs-lookup"><span data-stu-id="f8631-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="f8631-155">搜尋/{ID} - 動作/讀取</span><span class="sxs-lookup"><span data-stu-id="f8631-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="f8631-156">**要求已儲存搜尋的 hello 的內容：**</span><span class="sxs-lookup"><span data-stu-id="f8631-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="f8631-157">如果 hello 搜尋會傳回 「 擱置中 」 狀態，然後輪詢更新的 hello 結果可以透過此 API 完成。</span><span class="sxs-lookup"><span data-stu-id="f8631-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="f8631-158">6 分鐘後 hello 搜尋結果的 hello 皆會予以捨棄從 hello 快取，並將傳回 HTTP Gone。</span><span class="sxs-lookup"><span data-stu-id="f8631-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="f8631-159">如果 hello 初始搜尋要求立即傳回 「 成功 」 狀態，hello 結果不會新增 toohello 快取，使 HTTP Gone 此 API tooreturn，如果查詢。</span><span class="sxs-lookup"><span data-stu-id="f8631-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="f8631-160">hello HTTP 200 結果內容位於的 hello 相同格式化為 hello 初始搜尋要求和更新值。</span><span class="sxs-lookup"><span data-stu-id="f8631-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="f8631-161">已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="f8631-161">Saved searches</span></span>
<span data-ttu-id="f8631-162">**已儲存搜尋的要求清單：**</span><span class="sxs-lookup"><span data-stu-id="f8631-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="f8631-163">支援的方法：GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="f8631-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="f8631-164">支援的收集方法：GET</span><span class="sxs-lookup"><span data-stu-id="f8631-164">Supported collection methods: GET</span></span>

<span data-ttu-id="f8631-165">hello 下表描述可用的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f8631-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="f8631-166">屬性</span><span class="sxs-lookup"><span data-stu-id="f8631-166">Property</span></span> | <span data-ttu-id="f8631-167">說明</span><span class="sxs-lookup"><span data-stu-id="f8631-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8631-168">識別碼</span><span class="sxs-lookup"><span data-stu-id="f8631-168">Id</span></span> |<span data-ttu-id="f8631-169">hello 唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="f8631-169">hello unique identifier.</span></span> |
| <span data-ttu-id="f8631-170">Etag</span><span class="sxs-lookup"><span data-stu-id="f8631-170">Etag</span></span> |<span data-ttu-id="f8631-171">**修補程式的必要項目**。</span><span class="sxs-lookup"><span data-stu-id="f8631-171">**Required for Patch**.</span></span> <span data-ttu-id="f8631-172">每次寫入時由伺服器進行更新。</span><span class="sxs-lookup"><span data-stu-id="f8631-172">Updated by server on each write.</span></span> <span data-ttu-id="f8631-173">值必須等於 toohello 目前儲存的值或 ' *' tooupdate。</span><span class="sxs-lookup"><span data-stu-id="f8631-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="f8631-174">舊值/無效值時會傳回 409。</span><span class="sxs-lookup"><span data-stu-id="f8631-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="f8631-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="f8631-175">properties.query</span></span> |<span data-ttu-id="f8631-176">**必要**。</span><span class="sxs-lookup"><span data-stu-id="f8631-176">**Required**.</span></span> <span data-ttu-id="f8631-177">hello 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="f8631-177">hello search query.</span></span> |
| <span data-ttu-id="f8631-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="f8631-178">properties.displayName</span></span> |<span data-ttu-id="f8631-179">**必要**。</span><span class="sxs-lookup"><span data-stu-id="f8631-179">**Required**.</span></span> <span data-ttu-id="f8631-180">hello hello 查詢的使用者定義的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="f8631-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="f8631-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="f8631-181">properties.category</span></span> |<span data-ttu-id="f8631-182">**必要**。</span><span class="sxs-lookup"><span data-stu-id="f8631-182">**Required**.</span></span> <span data-ttu-id="f8631-183">hello 使用者定義的分類 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="f8631-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="f8631-184">hello 記錄分析搜尋 API 目前會傳回使用者建立已儲存的搜尋時工作區中的儲存搜尋的輪詢。</span><span class="sxs-lookup"><span data-stu-id="f8631-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="f8631-185">hello 應用程式開發介面不會傳回儲存的搜尋解決方案所提供。</span><span class="sxs-lookup"><span data-stu-id="f8631-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="f8631-186">建立已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="f8631-186">Create saved searches</span></span>
<span data-ttu-id="f8631-187">**要求：**</span><span class="sxs-lookup"><span data-stu-id="f8631-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="f8631-188">所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="f8631-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="f8631-189">刪除儲存搜尋</span><span class="sxs-lookup"><span data-stu-id="f8631-189">Delete saved searches</span></span>
<span data-ttu-id="f8631-190">**要求：**</span><span class="sxs-lookup"><span data-stu-id="f8631-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="f8631-191">更新儲存搜尋</span><span class="sxs-lookup"><span data-stu-id="f8631-191">Update saved searches</span></span>
 <span data-ttu-id="f8631-192">**要求：**</span><span class="sxs-lookup"><span data-stu-id="f8631-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="f8631-193">中繼資料 - 僅限 JSON</span><span class="sxs-lookup"><span data-stu-id="f8631-193">Metadata - JSON only</span></span>
<span data-ttu-id="f8631-194">以下是 hello 資料收集工作區中的所有記錄檔類型的方式 toosee hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="f8631-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="f8631-195">例如，如果您想知道是否 hello 事件類型是否具有名為電腦的欄位，然後此查詢是其中一種方式 toocheck。</span><span class="sxs-lookup"><span data-stu-id="f8631-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="f8631-196">**欄位要求：**</span><span class="sxs-lookup"><span data-stu-id="f8631-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="f8631-197">**回應：**</span><span class="sxs-lookup"><span data-stu-id="f8631-197">**Response:**</span></span>

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

<span data-ttu-id="f8631-198">hello 下表描述可用的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f8631-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="f8631-199">**屬性**</span><span class="sxs-lookup"><span data-stu-id="f8631-199">**Property**</span></span> | <span data-ttu-id="f8631-200">**說明**</span><span class="sxs-lookup"><span data-stu-id="f8631-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f8631-201">名稱</span><span class="sxs-lookup"><span data-stu-id="f8631-201">name</span></span> |<span data-ttu-id="f8631-202">欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="f8631-202">Field name.</span></span> |
| <span data-ttu-id="f8631-203">displayName</span><span class="sxs-lookup"><span data-stu-id="f8631-203">displayName</span></span> |<span data-ttu-id="f8631-204">hello 顯示 hello 欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8631-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="f8631-205">類型</span><span class="sxs-lookup"><span data-stu-id="f8631-205">type</span></span> |<span data-ttu-id="f8631-206">hello hello 欄位值的型別。</span><span class="sxs-lookup"><span data-stu-id="f8631-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="f8631-207">可面向化</span><span class="sxs-lookup"><span data-stu-id="f8631-207">facetable</span></span> |<span data-ttu-id="f8631-208">目前 ‘indexed’、‘stored ‘和 ‘facet’ 屬性的組合。</span><span class="sxs-lookup"><span data-stu-id="f8631-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="f8631-209">顯示</span><span class="sxs-lookup"><span data-stu-id="f8631-209">display</span></span> |<span data-ttu-id="f8631-210">目前 ‘display’ 屬性。</span><span class="sxs-lookup"><span data-stu-id="f8631-210">Current ‘display’ property.</span></span> <span data-ttu-id="f8631-211">如果欄位顯示在搜尋中，則為 True。</span><span class="sxs-lookup"><span data-stu-id="f8631-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="f8631-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="f8631-212">ownerType</span></span> |<span data-ttu-id="f8631-213">降低的 tooonly 屬於 tooonboarded IP 型別。</span><span class="sxs-lookup"><span data-stu-id="f8631-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="f8631-214">選擇性參數</span><span class="sxs-lookup"><span data-stu-id="f8631-214">Optional parameters</span></span>
<span data-ttu-id="f8631-215">hello 下列資訊描述可用的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="f8631-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="f8631-216">醒目提示</span><span class="sxs-lookup"><span data-stu-id="f8631-216">Highlighting</span></span>
<span data-ttu-id="f8631-217">hello"Highlight"參數是選擇性參數，您可以用 toorequest hello 搜尋子系統在其回應中包含的一組標記。</span><span class="sxs-lookup"><span data-stu-id="f8631-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="f8631-218">這些標記表示 hello 開頭與結尾的反白顯示的文字，以符合您的搜尋查詢中所提供的 hello 詞彙。</span><span class="sxs-lookup"><span data-stu-id="f8631-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="f8631-219">您可以指定 hello 開始和結束標記所使用的字詞 toowrap hello 反白顯示。</span><span class="sxs-lookup"><span data-stu-id="f8631-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="f8631-220">**範例搜尋查詢**</span><span class="sxs-lookup"><span data-stu-id="f8631-220">**Example search query**</span></span>

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

<span data-ttu-id="f8631-221">**範例結果：**</span><span class="sxs-lookup"><span data-stu-id="f8631-221">**Sample result:**</span></span>

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

<span data-ttu-id="f8631-222">請注意，hello 上述結果包含已做為前置詞及附加詞的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="f8631-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="f8631-223">電腦群組</span><span class="sxs-lookup"><span data-stu-id="f8631-223">Computer groups</span></span>
<span data-ttu-id="f8631-224">電腦群組是一種特殊的已儲存搜尋，其會傳回一組電腦。</span><span class="sxs-lookup"><span data-stu-id="f8631-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="f8631-225">您可以使用電腦群組中的其他查詢 toolimit hello 結果 toohello 電腦 hello 群組中。</span><span class="sxs-lookup"><span data-stu-id="f8631-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="f8631-226">電腦群組會實作為已儲存的搜尋，其含有 Group 標籤與 Computer 值。</span><span class="sxs-lookup"><span data-stu-id="f8631-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="f8631-227">以下是電腦群組的回應範例。</span><span class="sxs-lookup"><span data-stu-id="f8631-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="f8631-228">擷取電腦群組</span><span class="sxs-lookup"><span data-stu-id="f8631-228">Retrieving computer groups</span></span>
<span data-ttu-id="f8631-229">tooretrieve 電腦群組，請使用 hello Get 方法與 hello 群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8631-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="f8631-230">建立或更新電腦群組</span><span class="sxs-lookup"><span data-stu-id="f8631-230">Creating or updating a computer group</span></span>
<span data-ttu-id="f8631-231">toocreate 電腦群組，並提供唯一的儲存的搜尋的識別碼。 使用 hello Put 方法</span><span class="sxs-lookup"><span data-stu-id="f8631-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="f8631-232">如果您使用現有的電腦群組識別碼，則系統會修改它。</span><span class="sxs-lookup"><span data-stu-id="f8631-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="f8631-233">當您在 hello 記錄分析入口網站中建立電腦群組時，則會建立 hello 識別碼 hello 群組與名稱。</span><span class="sxs-lookup"><span data-stu-id="f8631-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="f8631-234">用於 hello 群組定義的 hello 查詢必須正確地傳回一組 hello 群組 toofunction 的電腦。</span><span class="sxs-lookup"><span data-stu-id="f8631-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="f8631-235">建議您結束與查詢`| Distinct Computer`tooensure hello 正確傳回資料。</span><span class="sxs-lookup"><span data-stu-id="f8631-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="f8631-236">儲存搜尋的 hello 的 hello 定義必須包含值的電腦是具名群組的 hello 搜尋 toobe 歸類為電腦群組的標記。</span><span class="sxs-lookup"><span data-stu-id="f8631-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="f8631-237">刪除電腦群組</span><span class="sxs-lookup"><span data-stu-id="f8631-237">Deleting computer groups</span></span>
<span data-ttu-id="f8631-238">toodelete 電腦群組，請使用 hello Delete 方法與 hello 群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8631-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="f8631-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8631-239">Next steps</span></span>
* <span data-ttu-id="f8631-240">深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢準則中使用自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="f8631-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
