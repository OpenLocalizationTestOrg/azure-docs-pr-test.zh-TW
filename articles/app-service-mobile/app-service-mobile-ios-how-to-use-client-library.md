---
title: "如何使用適用於 Azure Mobile Apps 的 iOS SDK"
description: "如何使用適用於 Azure Mobile Apps 的 iOS SDK"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="378c2-103">如何使用適用於 Azure Mobile Apps 的 iOS 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="378c2-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="378c2-104">本指南說明如何使用最新的 [Azure Mobile Apps iOS SDK][1] 執行常見案例。</span><span class="sxs-lookup"><span data-stu-id="378c2-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="378c2-105">如果您是 Azure Mobile Apps 的新手，請先完成 [Azure Mobile Apps 快速入門] 以建立後端、建立資料表及下載預先建置的 iOS Xcode 專案。</span><span class="sxs-lookup"><span data-stu-id="378c2-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="378c2-106">在本指南中，我們會著重於用戶端 iOS SDK。</span><span class="sxs-lookup"><span data-stu-id="378c2-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="378c2-107">若要深入了解後端的伺服器端 SDK，請參閱伺服器 SDK 做法。</span><span class="sxs-lookup"><span data-stu-id="378c2-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="378c2-108">參考文件</span><span class="sxs-lookup"><span data-stu-id="378c2-108">Reference documentation</span></span>
<span data-ttu-id="378c2-109">iOS 用戶端 SDK 的參考文件位於此處：[Azure Mobile Apps iOS 用戶端參考資料][2]。</span><span class="sxs-lookup"><span data-stu-id="378c2-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="378c2-110">支援的平台</span><span class="sxs-lookup"><span data-stu-id="378c2-110">Supported Platforms</span></span>
<span data-ttu-id="378c2-111">iOS SDK 支援 Objective-C 專案、Swift 2.2 專案，以及適用於 iOS 8.0 版或更新版本的 Swift 2.3 專案。</span><span class="sxs-lookup"><span data-stu-id="378c2-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="378c2-112">「伺服器流程」驗證在呈現的 UI 中使用 WebView。</span><span class="sxs-lookup"><span data-stu-id="378c2-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="378c2-113">如果裝置無法呈現 WebView UI，您需要本產品無法提供的其他驗證方法。</span><span class="sxs-lookup"><span data-stu-id="378c2-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="378c2-114">因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。</span><span class="sxs-lookup"><span data-stu-id="378c2-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="378c2-115"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="378c2-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="378c2-116">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="378c2-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="378c2-117">本指南假設資料表的結構描述與這些教學課程中的資料表相同。</span><span class="sxs-lookup"><span data-stu-id="378c2-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="378c2-118">本指南也假設您在程式碼中，參考了 `MicrosoftAzureMobile.framework` 並匯入了 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`。</span><span class="sxs-lookup"><span data-stu-id="378c2-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="378c2-119"><a name="create-client"></a>作法：建立用戶端</span><span class="sxs-lookup"><span data-stu-id="378c2-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="378c2-120">若要在專案中存取 Azure Mobile Apps 後端，請建立 `MSClient`。</span><span class="sxs-lookup"><span data-stu-id="378c2-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="378c2-121">以應用程式 URL 取代 `AppUrl` 。</span><span class="sxs-lookup"><span data-stu-id="378c2-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="378c2-122">您可以將 `gatewayURLString` 和 `applicationKey` 留白。</span><span class="sxs-lookup"><span data-stu-id="378c2-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="378c2-123">如果您設定驗證的閘道器，請將 `gatewayURLString` 填入閘道器 URL。</span><span class="sxs-lookup"><span data-stu-id="378c2-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="378c2-124">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="378c2-125">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="378c2-126"><a name="table-reference"></a>作法：建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="378c2-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="378c2-127">若要存取或更新資料，請建立後端資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="378c2-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="378c2-128">以您的資料表名稱取代 `TodoItem`</span><span class="sxs-lookup"><span data-stu-id="378c2-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="378c2-129">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="378c2-130">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="378c2-131"><a name="querying"></a>作法：查詢資料</span><span class="sxs-lookup"><span data-stu-id="378c2-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="378c2-132">若要建立資料庫查詢，請查詢 `MSTable` 物件。</span><span class="sxs-lookup"><span data-stu-id="378c2-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="378c2-133">下列查詢會取得 `TodoItem` 中的所有項目並記錄每個項目的文字。</span><span class="sxs-lookup"><span data-stu-id="378c2-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="378c2-134">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="378c2-135">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="378c2-136"><a name="filtering"></a>作法：篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="378c2-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="378c2-137">若要篩選結果，有許多可用的選項。</span><span class="sxs-lookup"><span data-stu-id="378c2-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="378c2-138">若要使用述詞篩選，請使用 `NSPredicate` 和 `readWithPredicate`。</span><span class="sxs-lookup"><span data-stu-id="378c2-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="378c2-139">下列篩選器傳回的資料只尋找未完成的待辦事項。</span><span class="sxs-lookup"><span data-stu-id="378c2-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="378c2-140">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="378c2-141">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="378c2-142"><a name="query-object"></a>作法：使用 MSQuery</span><span class="sxs-lookup"><span data-stu-id="378c2-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="378c2-143">若要執行複雜的查詢 (包括排序和分頁)，請使用述詞直接建立 `MSQuery` 物件：</span><span class="sxs-lookup"><span data-stu-id="378c2-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="378c2-144">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="378c2-145">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="378c2-146">`MSQuery` 可讓您控制幾種查詢行為。</span><span class="sxs-lookup"><span data-stu-id="378c2-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="378c2-147">指定結果的順序</span><span class="sxs-lookup"><span data-stu-id="378c2-147">Specify order of results</span></span>
* <span data-ttu-id="378c2-148">限制要傳回的欄位</span><span class="sxs-lookup"><span data-stu-id="378c2-148">Limit which fields to return</span></span>
* <span data-ttu-id="378c2-149">限制要傳回的記錄數</span><span class="sxs-lookup"><span data-stu-id="378c2-149">Limit how many records to return</span></span>
* <span data-ttu-id="378c2-150">指定回應中的總計數</span><span class="sxs-lookup"><span data-stu-id="378c2-150">Specify total count in response</span></span>
* <span data-ttu-id="378c2-151">在要求中指定自訂查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="378c2-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="378c2-152">套用其他函式</span><span class="sxs-lookup"><span data-stu-id="378c2-152">Apply additional functions</span></span>

<span data-ttu-id="378c2-153">在物件上呼叫 `readWithCompletion` 以執行 `MSQuery` 查詢。</span><span class="sxs-lookup"><span data-stu-id="378c2-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="378c2-154"><a name="sorting"></a>做法：使用 MSQuery 排序資料</span><span class="sxs-lookup"><span data-stu-id="378c2-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="378c2-155">我們來看一下範例如何排序結果。</span><span class="sxs-lookup"><span data-stu-id="378c2-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="378c2-156">若要根據 'text' 欄位依照遞增順序排序，然後再根據 'complete' 欄位依照遞減順序排序，請叫用 `MSQuery` ，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="378c2-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="378c2-157">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="378c2-158">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="378c2-159"><a name="selecting"></a><a name="parameters"></a>作法：使用 MSQuery 限制欄位和展開查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="378c2-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="378c2-160">若要限制在查詢中傳回的欄位，請在 **selectFields** 屬性中指定欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="378c2-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="378c2-161">本範例僅會傳回文字和已完成欄位：</span><span class="sxs-lookup"><span data-stu-id="378c2-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="378c2-162">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="378c2-163">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="378c2-164">若要在伺服器要求中包含額外的查詢字串參數 (例如有某個自訂的伺服器端指令碼使用這些參數)，請如下填入 `query.parameters` ：</span><span class="sxs-lookup"><span data-stu-id="378c2-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="378c2-165">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="378c2-166">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="378c2-167"><a name="paging"></a>如何：設定頁面大小</span><span class="sxs-lookup"><span data-stu-id="378c2-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="378c2-168">使用 Azure Mobile Apps，頁面大小會控制從後端資料表一次提取的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="378c2-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="378c2-169">然後對 `pull`資料的呼叫會根據此頁面大小將資料分批，直到沒有更多要提取的記錄為止。</span><span class="sxs-lookup"><span data-stu-id="378c2-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="378c2-170">您可以使用 **MSPullSettings** 設定頁面大小，如下所示。</span><span class="sxs-lookup"><span data-stu-id="378c2-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="378c2-171">預設頁面大小為 50，而下列範例將它變更為 3。</span><span class="sxs-lookup"><span data-stu-id="378c2-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="378c2-172">您可以基於效能的考量設定不同的頁面大小。</span><span class="sxs-lookup"><span data-stu-id="378c2-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="378c2-173">如果您有大量的小型資料記錄時，較高的分頁大小可減少伺服器的來回行程。</span><span class="sxs-lookup"><span data-stu-id="378c2-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="378c2-174">此設定只能控制用戶端上的頁面大小。</span><span class="sxs-lookup"><span data-stu-id="378c2-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="378c2-175">如果用戶端要求較 Mobile Apps 所支援更大的頁面大小，頁面大小會設為後端設定可支援的最大值。</span><span class="sxs-lookup"><span data-stu-id="378c2-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="378c2-176">此設定也是資料記錄的*數目*，而不是*位元組大小*。</span><span class="sxs-lookup"><span data-stu-id="378c2-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="378c2-177">如果您增加用戶端頁面大小，也應該增加伺服器上的頁面大小。</span><span class="sxs-lookup"><span data-stu-id="378c2-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="378c2-178">相關步驟請參閱[作法︰調整資料表分頁大小」](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="378c2-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="378c2-179">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="378c2-180">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="378c2-181"><a name="inserting"></a>作法：插入資料</span><span class="sxs-lookup"><span data-stu-id="378c2-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="378c2-182">若要插入新的資料表資料列，請建立 `NSDictionary` 並叫用 `table insert`。</span><span class="sxs-lookup"><span data-stu-id="378c2-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="378c2-183">如果[動態結構描述]已啟用，Azure App Service 行動後端會根據 `NSDictionary` 自動產生新的資料欄。</span><span class="sxs-lookup"><span data-stu-id="378c2-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="378c2-184">如果未提供 `id` ，則後端會自動產生新的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="378c2-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="378c2-185">提供您自己的 `id` ，以使用電子郵件地址、使用者名稱或您自己自訂的值作為識別碼。</span><span class="sxs-lookup"><span data-stu-id="378c2-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="378c2-186">提供您自己的識別碼可以讓聯結和商務導向的資料庫邏輯變得更容易。</span><span class="sxs-lookup"><span data-stu-id="378c2-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="378c2-187">`result` 含有先前插入的新項目。</span><span class="sxs-lookup"><span data-stu-id="378c2-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="378c2-188">視您的伺服器邏輯而定，相較於傳遞給伺服器的項目，它可能會含有其他或已修改的資料。</span><span class="sxs-lookup"><span data-stu-id="378c2-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="378c2-189">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="378c2-190">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="378c2-191"><a name="modifying"></a>作法：修改資料</span><span class="sxs-lookup"><span data-stu-id="378c2-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="378c2-192">若要更新現有的資料列，請修改項目並呼叫 `update`：</span><span class="sxs-lookup"><span data-stu-id="378c2-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="378c2-193">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="378c2-194">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="378c2-195">或者，提供資料列識別碼和更新的欄位：</span><span class="sxs-lookup"><span data-stu-id="378c2-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="378c2-196">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="378c2-197">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="378c2-198">進行更新時，至少必須設定 `id` 屬性。</span><span class="sxs-lookup"><span data-stu-id="378c2-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="378c2-199"><a name="deleting"></a>作法：刪除資料</span><span class="sxs-lookup"><span data-stu-id="378c2-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="378c2-200">若要刪除項目，請叫用 `delete` 搭配項目：</span><span class="sxs-lookup"><span data-stu-id="378c2-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="378c2-201">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="378c2-202">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="378c2-203">或者，提供資料列識別碼來進行刪除：</span><span class="sxs-lookup"><span data-stu-id="378c2-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="378c2-204">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="378c2-205">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="378c2-206">進行刪除時，至少必須設定 `id` 屬性。</span><span class="sxs-lookup"><span data-stu-id="378c2-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="378c2-207"><a name="customapi"></a>如何：呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="378c2-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="378c2-208">使用自訂 API，您可以公開任何後端功能。</span><span class="sxs-lookup"><span data-stu-id="378c2-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="378c2-209">它不必對應至資料表作業。</span><span class="sxs-lookup"><span data-stu-id="378c2-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="378c2-210">您不僅能進一步控制訊息，甚至還可以讀取或設定標頭，並變更回應內文格式。</span><span class="sxs-lookup"><span data-stu-id="378c2-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="378c2-211">若要了解如何在後端上建立自訂 API，請閱讀 [自訂 API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="378c2-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="378c2-212">若要呼叫自訂 API，請呼叫 `MSClient.invokeAPI`。</span><span class="sxs-lookup"><span data-stu-id="378c2-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="378c2-213">要求和回應內容會被視為 JSON。</span><span class="sxs-lookup"><span data-stu-id="378c2-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="378c2-214">若要使用其他媒體類型，[請使用 `invokeAPI`] 的其他多載[5]。</span><span class="sxs-lookup"><span data-stu-id="378c2-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="378c2-215">若要進行 `GET` 要求而不是 `POST` 要求，請將參數 `HTTPMethod` 設為 `"GET"`，以及將參數 `body` 設為 `nil` (因為 GET 要求沒有訊息內文)。如果您的自訂 API 支援其他 HTTP 動詞命令，請適當地變更 `HTTPMethod`。</span><span class="sxs-lookup"><span data-stu-id="378c2-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="378c2-216">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="378c2-217">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="378c2-218"><a name="templates"></a>作法：註冊推送範本以傳送跨平台通知</span><span class="sxs-lookup"><span data-stu-id="378c2-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="378c2-219">若要註冊範本，請在用戶端應用程式中利用 **client.push registerDeviceToken** 方法傳遞範本。</span><span class="sxs-lookup"><span data-stu-id="378c2-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="378c2-220">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="378c2-221">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="378c2-222">您的範本類型為 NSDictionary，並且可能包含多個下列格式的範本：</span><span class="sxs-lookup"><span data-stu-id="378c2-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="378c2-223">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="378c2-224">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="378c2-225">所有標記都將因安全性而移除。</span><span class="sxs-lookup"><span data-stu-id="378c2-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="378c2-226">若要將標籤新增至安裝中或安裝內的範本，請參閱[使用適用於 Azure Mobile Apps 的 .NET 後端伺服器 SDK][4]。</span><span class="sxs-lookup"><span data-stu-id="378c2-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="378c2-227">若要使用這些已註冊的範本來傳送通知，請使用[通知中樞 API][3]。</span><span class="sxs-lookup"><span data-stu-id="378c2-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="378c2-228"><a name="errors"></a>作法：處理錯誤</span><span class="sxs-lookup"><span data-stu-id="378c2-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="378c2-229">呼叫 Azure App Service行動後端時，completion 區塊會包含 `NSError` 參數。</span><span class="sxs-lookup"><span data-stu-id="378c2-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="378c2-230">發生錯誤時，此參數便會傳回非 Nil。</span><span class="sxs-lookup"><span data-stu-id="378c2-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="378c2-231">您應檢查程式碼中的此參數，並視需要處理錯誤，如上述的程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="378c2-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="378c2-232">檔案 [`<WindowsAzureMobileServices/MSError.h>`][6] 定義常數 `MSErrorResponseKey`、`MSErrorRequestKey` 和 `MSErrorServerItemKey`。</span><span class="sxs-lookup"><span data-stu-id="378c2-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="378c2-233">若要取得與錯誤相關的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="378c2-233">To get more data related to the error:</span></span>

<span data-ttu-id="378c2-234">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="378c2-235">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="378c2-236">此外，檔案也定義每個錯誤代碼的常數：</span><span class="sxs-lookup"><span data-stu-id="378c2-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="378c2-237">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="378c2-238">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="378c2-239"><a name="adal"></a>如何：使用 Active Directory Authentication Library 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="378c2-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="378c2-240">您可以使用 Active Directory Authentication Library (ADAL)，利用 Azure Active Directory 將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="378c2-241">相較於使用 `loginWithProvider:completion:` 方法，較建議使用身分識別提供者 SDK 的用戶端流程驗證。</span><span class="sxs-lookup"><span data-stu-id="378c2-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="378c2-242">用戶端流程驗證能提供較原生的 UX 風格，並允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="378c2-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="378c2-243">依照[如何設定 App Service 來進行 Active Directory 登入][7]教學課程的說明，設定您的行動應用程式後端來進行 AAD 登入。</span><span class="sxs-lookup"><span data-stu-id="378c2-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="378c2-244">請務必完成註冊原生用戶端應用程式的選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="378c2-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="378c2-245">若是 iOS，我們建議採用 `<app-scheme>://<bundle-id>` 形式的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="378c2-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="378c2-246">如需詳細資訊，請參閱 [ADAL iOS 快速入門][8]。</span><span class="sxs-lookup"><span data-stu-id="378c2-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="378c2-247">使用 Cocoapods 安裝 ADAL。</span><span class="sxs-lookup"><span data-stu-id="378c2-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="378c2-248">編輯您的 Podfile 以納入下列定義，並以您的 Xcode 專案名稱取代 **YOUR-PROJECT** ：</span><span class="sxs-lookup"><span data-stu-id="378c2-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="378c2-249">以及 Pod：</span><span class="sxs-lookup"><span data-stu-id="378c2-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="378c2-250">使用終端機，從包含您專案的目錄執行 `pod install`，然後開啟產生的 Xcode 工作區 (而不是專案)。</span><span class="sxs-lookup"><span data-stu-id="378c2-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="378c2-251">根據您使用的語言，將下列程式碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="378c2-252">取代每個程式碼的以下項目：</span><span class="sxs-lookup"><span data-stu-id="378c2-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="378c2-253">以您佈建應用程式的租用戶名稱取代 **INSERT-AUTHORITY-HERE** 。</span><span class="sxs-lookup"><span data-stu-id="378c2-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="378c2-254">格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="378c2-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="378c2-255">此值可從 [Azure 傳統入口網站] 複製到 Azure Active Directory 的 [網域] 索引標籤以外。</span><span class="sxs-lookup"><span data-stu-id="378c2-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="378c2-256">以您行動應用程式後端的用戶端識別碼取代 INSERT-RESOURCE-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="378c2-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="378c2-257">您可以從入口網站 [Azure Active Directory 設定] 底下的 [進階] 索引標籤取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="378c2-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="378c2-258">以您從原生用戶端應用程式中複製的用戶端識別碼取代 INSERT-CLIENT-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="378c2-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="378c2-259">使用 HTTPS 配置，以您網站的 **/.auth/login/done** 端點取代 *INSERT-REDIRECT-URI-HERE* 。</span><span class="sxs-lookup"><span data-stu-id="378c2-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="378c2-260">此值應與 *https://contoso.azurewebsites.net/.auth/login/done* 類似。</span><span class="sxs-lookup"><span data-stu-id="378c2-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="378c2-261">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-261">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="378c2-262">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="378c2-263"><a name="facebook-sdk"></a>作法：使用 Facebook SDK for iOS 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="378c2-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="378c2-264">您可以使用 Facebook SDK for iOS，利用 Facebook 將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="378c2-265">相較於使用 `loginWithProvider:completion:` 方法，較建議使用用戶端流程驗證。</span><span class="sxs-lookup"><span data-stu-id="378c2-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="378c2-266">用戶端流程驗證能提供較原生的 UX 風格，並允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="378c2-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="378c2-267">依照[如何設定 App Service 來進行 Facebook 登入][9]教學課程的說明，設定您的行動應用程式後端來進行 Facebook 登入。</span><span class="sxs-lookup"><span data-stu-id="378c2-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="378c2-268">依照 [Facebook SDK for iOS - 開始使用][10]文件來安裝 Facebook SDK for iOS。</span><span class="sxs-lookup"><span data-stu-id="378c2-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="378c2-269">您可以在現有註冊中新增 iOS 平台，而不必建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="378c2-270">Facebook 的文件包含應用程式委派中的某些 Objective-C 程式碼。</span><span class="sxs-lookup"><span data-stu-id="378c2-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="378c2-271">如果您要使用 **Swift**，您可以使用 AppDelegate.swift 的下列轉譯：</span><span class="sxs-lookup"><span data-stu-id="378c2-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="378c2-272">除了在專案中新增 `FBSDKCoreKit.framework`，也請以相同方式新增 `FBSDKLoginKit.framework` 的參考。</span><span class="sxs-lookup"><span data-stu-id="378c2-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="378c2-273">根據您使用的語言，將下列程式碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="378c2-274">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-274">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="378c2-275">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="378c2-276"><a name="twitter-fabric"></a>作法：使用 Twitter Fabric for iOS 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="378c2-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="378c2-277">您可以使用 Fabric for iOS，利用 Twitter 將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="378c2-278">與使用 `loginWithProvider:completion:` 方法相比，較建議使用用戶端流程驗證，因為它提供更原生的 UX 風格，並可允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="378c2-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="378c2-279">依照 [如何設定 App Service 來進行 Twitter 登入](app-service-mobile-how-to-configure-twitter-authentication.md) 教學課程的說明，設定您的行動應用程式後端來進行 Twitter 登入。</span><span class="sxs-lookup"><span data-stu-id="378c2-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="378c2-280">依照 [Fabric for iOS - 開始使用]文件並設定 TwitterKit，在專案中新增網狀架構。</span><span class="sxs-lookup"><span data-stu-id="378c2-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="378c2-281">根據預設，網狀架構會為您建立 Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="378c2-282">您可以使用下列程式碼片段，註冊您稍早所建立的取用者金鑰和取用者密碼，以避免建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="378c2-283">或者，您可以使用您在 [網狀架構儀表板]中看到的值，取代您提供給 App Service 的取用者金鑰和取用者密碼值。</span><span class="sxs-lookup"><span data-stu-id="378c2-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="378c2-284">如果您選擇此選項，請務必將回呼 URL 設定為預留位置值，例如 `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`。</span><span class="sxs-lookup"><span data-stu-id="378c2-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="378c2-285">如果您選擇使用稍早所建立的密碼，請在應用程式委派中新增下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="378c2-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="378c2-286">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-286">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="378c2-287">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="378c2-288">根據您使用的語言，將下列程式碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="378c2-289">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-289">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="378c2-290">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-290">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="378c2-291"><a name="google-sdk"></a>作法：使用 Google Sign-In SDK for iOS 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="378c2-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="378c2-292">您可以使用 Google Sign-In SDK for iOS，利用 Google 帳戶將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="378c2-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="378c2-293">近期內，Google 宣布他們的 OAuth 安全性原則變更。</span><span class="sxs-lookup"><span data-stu-id="378c2-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="378c2-294">這些原則變更要求您未來必須使用 Google SDK。</span><span class="sxs-lookup"><span data-stu-id="378c2-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="378c2-295">依照 [如何設定 App Service 來進行 Google 登入](app-service-mobile-how-to-configure-google-authentication.md) 教學課程的說明，設定您的行動應用程式後端來進行 Google 登入。</span><span class="sxs-lookup"><span data-stu-id="378c2-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="378c2-296">請依照 [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) 文件安裝 Google SDK for iOS。</span><span class="sxs-lookup"><span data-stu-id="378c2-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="378c2-297">您可以略過＜使用後端伺服器進行驗證＞一節。</span><span class="sxs-lookup"><span data-stu-id="378c2-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="378c2-298">請根據您使用的語言，將下列內容新增到委派的 `signIn:didSignInForUser:withError:` 方法。</span><span class="sxs-lookup"><span data-stu-id="378c2-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="378c2-299">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="378c2-300">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="378c2-301">務必也將下列內容新增到應用程式委派中的 `application:didFinishLaunchingWithOptions:`，將 "SERVER_CLIENT_ID" 取代為您用來在步驟 1 中設定 App Service 的相同識別碼。</span><span class="sxs-lookup"><span data-stu-id="378c2-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="378c2-302">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="378c2-303">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="378c2-304">根據您所使用的語言，將下列程式碼新增到應用程式的 UIViewController 中以實作 `GIDSignInUIDelegate` 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="378c2-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="378c2-305">系統會先將您登出，然後再將您登入；雖然不需要再次輸入認證，不過您會看到同意對話方塊。</span><span class="sxs-lookup"><span data-stu-id="378c2-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="378c2-306">請只在工作階段權杖過期時才呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="378c2-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="378c2-307">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="378c2-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="378c2-308">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="378c2-308">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="378c2-309">[Azure Mobile Apps 快速入門]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="378c2-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="378c2-310">[動態結構描述]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="378c2-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="378c2-311">[網狀架構儀表板]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="378c2-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="378c2-312">[Fabric for iOS - 開始使用]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="378c2-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
