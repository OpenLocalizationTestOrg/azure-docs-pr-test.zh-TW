---
title: "Log Analytics 記錄檔搜尋 REST API | Microsoft Docs"
description: "本指南提供基本教學課程，說明如何使用 Operations Management Suite (OMS) 中的 Log Analytics 搜尋 REST API，並提供使用命令的範例。"
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
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="07b1b-103">Log Analytics 記錄檔搜尋 REST API</span><span class="sxs-lookup"><span data-stu-id="07b1b-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="07b1b-104">本指南提供基本教學課程 (包括範例)，說明如何使用 Log Analytics 搜尋 REST API。</span><span class="sxs-lookup"><span data-stu-id="07b1b-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="07b1b-105">Log Analytics 是 Operations Management Suite (OMS) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="07b1b-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="07b1b-106">如果您的工作區已升級至[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則您應該如本文所述，繼續搭配使用舊版查詢語言與記錄搜尋 API。</span><span class="sxs-lookup"><span data-stu-id="07b1b-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="07b1b-107">之後將會為更新的工作區發行新的 API，屆時會更新說明文件。</span><span class="sxs-lookup"><span data-stu-id="07b1b-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="07b1b-108">Log Analytics 在以前稱為 Operational Insights，這也是資源提供者中使用此名稱的原因。</span><span class="sxs-lookup"><span data-stu-id="07b1b-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="07b1b-109">記錄檔搜尋 REST API 概觀</span><span class="sxs-lookup"><span data-stu-id="07b1b-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="07b1b-110">Log Analytics 搜尋 API 是 RESTful，可透過 Azure Resource Manager API 來存取。</span><span class="sxs-lookup"><span data-stu-id="07b1b-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="07b1b-111">本文件提供透過 [ARMClient](https://github.com/projectkudu/ARMClient) 存取 API 的範例，這是可簡化叫用 Azure Resource Manager API 的開放原始碼命令列工具。</span><span class="sxs-lookup"><span data-stu-id="07b1b-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="07b1b-112">使用 ARMClient 是存取 Log Analytics 搜尋 API 的許多選項之一。</span><span class="sxs-lookup"><span data-stu-id="07b1b-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="07b1b-113">另一個選項是使用 OperationalInsights 的 Azure PowerShell 模組，其中包含可存取搜尋的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="07b1b-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="07b1b-114">這些工具可讓您利用 Azure Resource Manager API 呼叫 OMS 工作區，並在其中執行搜尋命令。</span><span class="sxs-lookup"><span data-stu-id="07b1b-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="07b1b-115">API 會以 JSON 格式來輸出搜尋結果，可讓您以程式設計方式將搜尋結果用在許多不同用途上。</span><span class="sxs-lookup"><span data-stu-id="07b1b-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="07b1b-116">您可以透過 [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) 和 [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx) 來使用 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="07b1b-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="07b1b-117">若要深入了解，請檢閱連結的網頁。</span><span class="sxs-lookup"><span data-stu-id="07b1b-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="07b1b-118">如果您使用彙總命令，例如 `|measure count()` 或 `distinct`，則每次呼叫搜尋最多可傳回 500,000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="07b1b-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="07b1b-119">不含彙總命令的搜尋最多傳回 5,000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="07b1b-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="07b1b-120">基本 Log Analytics 搜尋 REST API 教學課程</span><span class="sxs-lookup"><span data-stu-id="07b1b-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="07b1b-121">使用 ARMClient</span><span class="sxs-lookup"><span data-stu-id="07b1b-121">To use ARMClient</span></span>
1. <span data-ttu-id="07b1b-122">安裝 [Chocolatey](https://chocolatey.org/)，這是適用於 Windows 的開放原始碼封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="07b1b-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="07b1b-123">以系統管理員身分開啟命令提示字元視窗，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="07b1b-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="07b1b-124">執行下列命令來安裝 ARMClient：</span><span class="sxs-lookup"><span data-stu-id="07b1b-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="07b1b-125">使用 ARMClient 執行搜尋</span><span class="sxs-lookup"><span data-stu-id="07b1b-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="07b1b-126">使用您的 Microsoft 帳戶、公司帳戶或學校帳戶登入：</span><span class="sxs-lookup"><span data-stu-id="07b1b-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="07b1b-127">成功登入會列出繫結至指定帳戶的所有訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="07b1b-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="07b1b-128">取得 Operations Management Suite 工作區：</span><span class="sxs-lookup"><span data-stu-id="07b1b-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="07b1b-129">成功的 Get 呼叫會輸出繫結至訂用帳戶的所有工作區：</span><span class="sxs-lookup"><span data-stu-id="07b1b-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

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
3. <span data-ttu-id="07b1b-130">建立您的搜尋變數：</span><span class="sxs-lookup"><span data-stu-id="07b1b-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="07b1b-131">使用新的搜尋變數來搜尋：</span><span class="sxs-lookup"><span data-stu-id="07b1b-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="07b1b-132">Log Analytics 搜尋 REST API 參考範例</span><span class="sxs-lookup"><span data-stu-id="07b1b-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="07b1b-133">下列範例顯示如何使用 Search API。</span><span class="sxs-lookup"><span data-stu-id="07b1b-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="07b1b-134">搜尋 - 動作/讀取</span><span class="sxs-lookup"><span data-stu-id="07b1b-134">Search - Action/Read</span></span>
<span data-ttu-id="07b1b-135">**範例 Url：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="07b1b-136">**要求：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-136">**Request:**</span></span>

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
<span data-ttu-id="07b1b-137">下表描述可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="07b1b-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="07b1b-138">**屬性**</span><span class="sxs-lookup"><span data-stu-id="07b1b-138">**Property**</span></span> | <span data-ttu-id="07b1b-139">**說明**</span><span class="sxs-lookup"><span data-stu-id="07b1b-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="07b1b-140">top</span><span class="sxs-lookup"><span data-stu-id="07b1b-140">top</span></span> |<span data-ttu-id="07b1b-141">要傳回的結果數目上限。</span><span class="sxs-lookup"><span data-stu-id="07b1b-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="07b1b-142">highlight</span><span class="sxs-lookup"><span data-stu-id="07b1b-142">highlight</span></span> |<span data-ttu-id="07b1b-143">包含 pre 和 post 參數，通常用於反白顯示比對欄位</span><span class="sxs-lookup"><span data-stu-id="07b1b-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="07b1b-144">pre</span><span class="sxs-lookup"><span data-stu-id="07b1b-144">pre</span></span> |<span data-ttu-id="07b1b-145">以指定字串做為比對欄位的前置詞。</span><span class="sxs-lookup"><span data-stu-id="07b1b-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="07b1b-146">post</span><span class="sxs-lookup"><span data-stu-id="07b1b-146">post</span></span> |<span data-ttu-id="07b1b-147">以指定字串附加至比對欄位之後。</span><span class="sxs-lookup"><span data-stu-id="07b1b-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="07b1b-148">query</span><span class="sxs-lookup"><span data-stu-id="07b1b-148">query</span></span> |<span data-ttu-id="07b1b-149">用來收集並傳回結果的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="07b1b-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="07b1b-150">start</span><span class="sxs-lookup"><span data-stu-id="07b1b-150">start</span></span> |<span data-ttu-id="07b1b-151">您想要從其中找到結果的時間範圍開頭。</span><span class="sxs-lookup"><span data-stu-id="07b1b-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="07b1b-152">end</span><span class="sxs-lookup"><span data-stu-id="07b1b-152">end</span></span> |<span data-ttu-id="07b1b-153">您想要從其中找到結果的時間範圍結尾。</span><span class="sxs-lookup"><span data-stu-id="07b1b-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="07b1b-154">**回應：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="07b1b-155">搜尋/{ID} - 動作/讀取</span><span class="sxs-lookup"><span data-stu-id="07b1b-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="07b1b-156">**要求已儲存搜尋的內容：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="07b1b-157">如果搜尋會傳回「擱置中」狀態，則輪詢更新的結果可以透過此 API 完成。</span><span class="sxs-lookup"><span data-stu-id="07b1b-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="07b1b-158">6 分鐘後，搜尋的結果將會從快取卸除，並將傳回 HTTP Gone。</span><span class="sxs-lookup"><span data-stu-id="07b1b-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="07b1b-159">如果初始搜尋要求立即傳回「成功」狀態，則結果不會新增至快取，導致在查詢此 API 時會傳回 HTTP Gone。</span><span class="sxs-lookup"><span data-stu-id="07b1b-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="07b1b-160">HTTP 200 結果內容的格式與初始搜尋要求相同，只是會有更新的值。</span><span class="sxs-lookup"><span data-stu-id="07b1b-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="07b1b-161">已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="07b1b-161">Saved searches</span></span>
<span data-ttu-id="07b1b-162">**已儲存搜尋的要求清單：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="07b1b-163">支援的方法：GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="07b1b-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="07b1b-164">支援的收集方法：GET</span><span class="sxs-lookup"><span data-stu-id="07b1b-164">Supported collection methods: GET</span></span>

<span data-ttu-id="07b1b-165">下表描述可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="07b1b-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="07b1b-166">屬性</span><span class="sxs-lookup"><span data-stu-id="07b1b-166">Property</span></span> | <span data-ttu-id="07b1b-167">說明</span><span class="sxs-lookup"><span data-stu-id="07b1b-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07b1b-168">識別碼</span><span class="sxs-lookup"><span data-stu-id="07b1b-168">Id</span></span> |<span data-ttu-id="07b1b-169">唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-169">The unique identifier.</span></span> |
| <span data-ttu-id="07b1b-170">Etag</span><span class="sxs-lookup"><span data-stu-id="07b1b-170">Etag</span></span> |<span data-ttu-id="07b1b-171">**修補程式的必要項目**。</span><span class="sxs-lookup"><span data-stu-id="07b1b-171">**Required for Patch**.</span></span> <span data-ttu-id="07b1b-172">每次寫入時由伺服器進行更新。</span><span class="sxs-lookup"><span data-stu-id="07b1b-172">Updated by server on each write.</span></span> <span data-ttu-id="07b1b-173">值必須等於目前儲存的值或 ‘*’ 才能進行更新。</span><span class="sxs-lookup"><span data-stu-id="07b1b-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="07b1b-174">舊值/無效值時會傳回 409。</span><span class="sxs-lookup"><span data-stu-id="07b1b-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="07b1b-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="07b1b-175">properties.query</span></span> |<span data-ttu-id="07b1b-176">**必要**。</span><span class="sxs-lookup"><span data-stu-id="07b1b-176">**Required**.</span></span> <span data-ttu-id="07b1b-177">搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="07b1b-177">The search query.</span></span> |
| <span data-ttu-id="07b1b-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="07b1b-178">properties.displayName</span></span> |<span data-ttu-id="07b1b-179">**必要**。</span><span class="sxs-lookup"><span data-stu-id="07b1b-179">**Required**.</span></span> <span data-ttu-id="07b1b-180">使用者定義的查詢顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="07b1b-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="07b1b-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="07b1b-181">properties.category</span></span> |<span data-ttu-id="07b1b-182">**必要**。</span><span class="sxs-lookup"><span data-stu-id="07b1b-182">**Required**.</span></span> <span data-ttu-id="07b1b-183">使用者定義的查詢類別。</span><span class="sxs-lookup"><span data-stu-id="07b1b-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="07b1b-184">目前，當 Log Analytics 搜尋 API 輪詢工作區的儲存搜尋時，其會傳回使用者建立的儲存搜尋。</span><span class="sxs-lookup"><span data-stu-id="07b1b-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="07b1b-185">此 API 不會傳回解決方案所提供之已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="07b1b-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="07b1b-186">建立已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="07b1b-186">Create saved searches</span></span>
<span data-ttu-id="07b1b-187">**要求：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="07b1b-188">Log Analytics API 所建立並儲存的所有搜尋、排程和動作，都必須使用小寫名稱。</span><span class="sxs-lookup"><span data-stu-id="07b1b-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="07b1b-189">刪除儲存搜尋</span><span class="sxs-lookup"><span data-stu-id="07b1b-189">Delete saved searches</span></span>
<span data-ttu-id="07b1b-190">**要求：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="07b1b-191">更新儲存搜尋</span><span class="sxs-lookup"><span data-stu-id="07b1b-191">Update saved searches</span></span>
 <span data-ttu-id="07b1b-192">**要求：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="07b1b-193">中繼資料 - 僅限 JSON</span><span class="sxs-lookup"><span data-stu-id="07b1b-193">Metadata - JSON only</span></span>
<span data-ttu-id="07b1b-194">以下的方法可讓您看到工作區中所收集資料的所有記錄類型欄位。</span><span class="sxs-lookup"><span data-stu-id="07b1b-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="07b1b-195">比方說，如果您想知道事件類型是否具有名為 Computer 的欄位，此查詢可作為一種檢查方法。</span><span class="sxs-lookup"><span data-stu-id="07b1b-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="07b1b-196">**欄位要求：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="07b1b-197">**回應：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-197">**Response:**</span></span>

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

<span data-ttu-id="07b1b-198">下表描述可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="07b1b-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="07b1b-199">**屬性**</span><span class="sxs-lookup"><span data-stu-id="07b1b-199">**Property**</span></span> | <span data-ttu-id="07b1b-200">**說明**</span><span class="sxs-lookup"><span data-stu-id="07b1b-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="07b1b-201">名稱</span><span class="sxs-lookup"><span data-stu-id="07b1b-201">name</span></span> |<span data-ttu-id="07b1b-202">欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="07b1b-202">Field name.</span></span> |
| <span data-ttu-id="07b1b-203">displayName</span><span class="sxs-lookup"><span data-stu-id="07b1b-203">displayName</span></span> |<span data-ttu-id="07b1b-204">欄位的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="07b1b-204">The display name of the field.</span></span> |
| <span data-ttu-id="07b1b-205">類型</span><span class="sxs-lookup"><span data-stu-id="07b1b-205">type</span></span> |<span data-ttu-id="07b1b-206">欄位值的類型。</span><span class="sxs-lookup"><span data-stu-id="07b1b-206">The Type of the field value.</span></span> |
| <span data-ttu-id="07b1b-207">可面向化</span><span class="sxs-lookup"><span data-stu-id="07b1b-207">facetable</span></span> |<span data-ttu-id="07b1b-208">目前 ‘indexed’、‘stored ‘和 ‘facet’ 屬性的組合。</span><span class="sxs-lookup"><span data-stu-id="07b1b-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="07b1b-209">顯示</span><span class="sxs-lookup"><span data-stu-id="07b1b-209">display</span></span> |<span data-ttu-id="07b1b-210">目前 ‘display’ 屬性。</span><span class="sxs-lookup"><span data-stu-id="07b1b-210">Current ‘display’ property.</span></span> <span data-ttu-id="07b1b-211">如果欄位顯示在搜尋中，則為 True。</span><span class="sxs-lookup"><span data-stu-id="07b1b-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="07b1b-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="07b1b-212">ownerType</span></span> |<span data-ttu-id="07b1b-213">減少至僅屬於 onboarded IP 的類型。</span><span class="sxs-lookup"><span data-stu-id="07b1b-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="07b1b-214">選擇性參數</span><span class="sxs-lookup"><span data-stu-id="07b1b-214">Optional parameters</span></span>
<span data-ttu-id="07b1b-215">下列資訊描述可用的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="07b1b-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="07b1b-216">醒目提示</span><span class="sxs-lookup"><span data-stu-id="07b1b-216">Highlighting</span></span>
<span data-ttu-id="07b1b-217">“Highlight” 參數是一種選擇性參數，您可以用來要求搜尋子系統，包含其回應中的一組標記。</span><span class="sxs-lookup"><span data-stu-id="07b1b-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="07b1b-218">這些標記表示開頭與結尾的醒目提示文字，以符合您在搜尋查詢中所提供的詞彙。</span><span class="sxs-lookup"><span data-stu-id="07b1b-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="07b1b-219">您可以指定開頭與結尾的標記，讓搜尋用來包裝醒目提示的詞彙。</span><span class="sxs-lookup"><span data-stu-id="07b1b-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="07b1b-220">**範例搜尋查詢**</span><span class="sxs-lookup"><span data-stu-id="07b1b-220">**Example search query**</span></span>

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

<span data-ttu-id="07b1b-221">**範例結果：**</span><span class="sxs-lookup"><span data-stu-id="07b1b-221">**Sample result:**</span></span>

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

<span data-ttu-id="07b1b-222">請注意，上述結果包含已加上前置詞和附加詞的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="07b1b-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="07b1b-223">電腦群組</span><span class="sxs-lookup"><span data-stu-id="07b1b-223">Computer groups</span></span>
<span data-ttu-id="07b1b-224">電腦群組是一種特殊的已儲存搜尋，其會傳回一組電腦。</span><span class="sxs-lookup"><span data-stu-id="07b1b-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="07b1b-225">您可以在其他查詢中使用電腦群組，以將結果限制為該群組中的電腦。</span><span class="sxs-lookup"><span data-stu-id="07b1b-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="07b1b-226">電腦群組會實作為已儲存的搜尋，其含有 Group 標籤與 Computer 值。</span><span class="sxs-lookup"><span data-stu-id="07b1b-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="07b1b-227">以下是電腦群組的回應範例。</span><span class="sxs-lookup"><span data-stu-id="07b1b-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="07b1b-228">擷取電腦群組</span><span class="sxs-lookup"><span data-stu-id="07b1b-228">Retrieving computer groups</span></span>
<span data-ttu-id="07b1b-229">若要擷取電腦群組，請使用 Get 方法搭配群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="07b1b-230">建立或更新電腦群組</span><span class="sxs-lookup"><span data-stu-id="07b1b-230">Creating or updating a computer group</span></span>
<span data-ttu-id="07b1b-231">若要建立電腦群組，請使用 Put 方法搭配已儲存的唯一搜尋識別碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="07b1b-232">如果您使用現有的電腦群組識別碼，則系統會修改它。</span><span class="sxs-lookup"><span data-stu-id="07b1b-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="07b1b-233">當您在 Log Analytics 入口網站中建立電腦群組時，將會依據群組和名稱來建立識別碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="07b1b-234">用於群組定義的查詢必須傳回一組電腦，群組才能正確運作。</span><span class="sxs-lookup"><span data-stu-id="07b1b-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="07b1b-235">建議您在查詢的結尾加上 `| Distinct Computer`，以確保傳回正確的資料。</span><span class="sxs-lookup"><span data-stu-id="07b1b-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="07b1b-236">已儲存搜尋的定義必須包含 Group 標籤與 Computer 值，才能將搜尋分類為電腦群組。</span><span class="sxs-lookup"><span data-stu-id="07b1b-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="07b1b-237">刪除電腦群組</span><span class="sxs-lookup"><span data-stu-id="07b1b-237">Deleting computer groups</span></span>
<span data-ttu-id="07b1b-238">若要刪除電腦群組，請使用 Delete 方法搭配群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="07b1b-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="07b1b-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07b1b-239">Next steps</span></span>
* <span data-ttu-id="07b1b-240">了解 [記錄搜尋](log-analytics-log-searches.md) ，以使用自訂欄位作為準則來建立查詢。</span><span class="sxs-lookup"><span data-stu-id="07b1b-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
