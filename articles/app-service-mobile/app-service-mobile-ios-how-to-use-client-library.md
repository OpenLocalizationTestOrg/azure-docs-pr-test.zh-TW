---
title: "aaaHow tooUse iOS SDK for Azure 行動應用程式"
description: "如何 tooUse iOS SDK for Azure 行動應用程式"
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
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="d78ac-103">如何 tooUse iOS Azure 行動應用程式的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="d78ac-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="d78ac-104">本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式 iOS SDK][1]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="d78ac-105">如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端，建立資料表，並下載預先建立的 iOS Xcode 專案。</span><span class="sxs-lookup"><span data-stu-id="d78ac-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="d78ac-106">在本指南中，我們會著重在 hello 用戶端 iOS SDK。</span><span class="sxs-lookup"><span data-stu-id="d78ac-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="d78ac-107">toolearn 深入了解 hello hello 後端伺服器端 SDK，請參閱 hello 伺服器 SDK 來。</span><span class="sxs-lookup"><span data-stu-id="d78ac-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="d78ac-108">參考文件</span><span class="sxs-lookup"><span data-stu-id="d78ac-108">Reference documentation</span></span>
<span data-ttu-id="d78ac-109">hello hello iOS 用戶端 SDK 的參考文件位於此處： [Azure 行動應用程式 iOS 用戶端參考][2]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d78ac-110">支援的平台</span><span class="sxs-lookup"><span data-stu-id="d78ac-110">Supported Platforms</span></span>
<span data-ttu-id="d78ac-111">hello iOS SDK 支援 iOS 8.0 或更新版本的版本 Objective C 專案、 Swift 2.2 專案和 Swift 2.3 專案。</span><span class="sxs-lookup"><span data-stu-id="d78ac-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="d78ac-112">hello 「 伺服器-流程 」 驗證會使用 WebView hello 呈現 UI。</span><span class="sxs-lookup"><span data-stu-id="d78ac-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="d78ac-113">如果 hello 裝置不能 toopresent WebView UI，則需要其他的驗證方法，則將 hello 範圍外的 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="d78ac-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="d78ac-114">因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。</span><span class="sxs-lookup"><span data-stu-id="d78ac-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="d78ac-115"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="d78ac-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="d78ac-116">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="d78ac-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="d78ac-117">本指南假設 hello 資料表具有在這些教學課程中的 hello 資料表相同的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d78ac-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="d78ac-118">本指南也假設您在程式碼中，參考了 `MicrosoftAzureMobile.framework` 並匯入了 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="d78ac-119"><a name="create-client"></a>作法：建立用戶端</span><span class="sxs-lookup"><span data-stu-id="d78ac-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="d78ac-120">在專案中，Azure 行動應用程式後端 tooaccess 建立`MSClient`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="d78ac-121">取代`AppUrl`hello 應用程式 url。</span><span class="sxs-lookup"><span data-stu-id="d78ac-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="d78ac-122">您可以將 `gatewayURLString` 和 `applicationKey` 留白。</span><span class="sxs-lookup"><span data-stu-id="d78ac-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="d78ac-123">如果您設定閘道，以進行驗證時，擴展`gatewayURLString`與 hello gateway URL。</span><span class="sxs-lookup"><span data-stu-id="d78ac-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="d78ac-124">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="d78ac-125">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="d78ac-126"><a name="table-reference"></a>作法：建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="d78ac-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="d78ac-127">tooaccess 或更新的資料，建立參考 toohello 後端的資料表。</span><span class="sxs-lookup"><span data-stu-id="d78ac-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="d78ac-128">取代`TodoItem`與資料表的名稱，hello</span><span class="sxs-lookup"><span data-stu-id="d78ac-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="d78ac-129">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="d78ac-130">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="d78ac-131"><a name="querying"></a>作法：查詢資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="d78ac-132">toocreate 資料庫查詢，查詢 hello`MSTable`物件。</span><span class="sxs-lookup"><span data-stu-id="d78ac-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="d78ac-133">hello 下列查詢會取得所有 hello 項目`TodoItem`和記錄檔 hello 每個項目的文字。</span><span class="sxs-lookup"><span data-stu-id="d78ac-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="d78ac-134">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-134">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-135">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-135">**Swift**:</span></span>

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

## <span data-ttu-id="d78ac-136"><a name="filtering"></a>作法：篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="d78ac-137">toofilter 結果中，有許多可用的選項。</span><span class="sxs-lookup"><span data-stu-id="d78ac-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="d78ac-138">使用述詞，而使用 toofilter`NSPredicate`和`readWithPredicate`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="d78ac-139">hello 下列篩選傳回的資料 toofind 僅完整 Todo 項目。</span><span class="sxs-lookup"><span data-stu-id="d78ac-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="d78ac-140">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
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

<span data-ttu-id="d78ac-141">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
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

## <span data-ttu-id="d78ac-142"><a name="query-object"></a>作法：使用 MSQuery</span><span class="sxs-lookup"><span data-stu-id="d78ac-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="d78ac-143">建立複雜的查詢 （包括排序和分頁） tooperform`MSQuery`物件直接或使用述詞：</span><span class="sxs-lookup"><span data-stu-id="d78ac-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="d78ac-144">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="d78ac-145">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="d78ac-146">`MSQuery` 可讓您控制幾種查詢行為。</span><span class="sxs-lookup"><span data-stu-id="d78ac-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="d78ac-147">指定結果的順序</span><span class="sxs-lookup"><span data-stu-id="d78ac-147">Specify order of results</span></span>
* <span data-ttu-id="d78ac-148">欄位 tooreturn 的限制</span><span class="sxs-lookup"><span data-stu-id="d78ac-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="d78ac-149">限制的記錄數 tooreturn</span><span class="sxs-lookup"><span data-stu-id="d78ac-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="d78ac-150">指定回應中的總計數</span><span class="sxs-lookup"><span data-stu-id="d78ac-150">Specify total count in response</span></span>
* <span data-ttu-id="d78ac-151">在要求中指定自訂查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="d78ac-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="d78ac-152">套用其他函式</span><span class="sxs-lookup"><span data-stu-id="d78ac-152">Apply additional functions</span></span>

<span data-ttu-id="d78ac-153">執行`MSQuery`查詢藉由呼叫`readWithCompletion`hello 物件上。</span><span class="sxs-lookup"><span data-stu-id="d78ac-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="d78ac-154"><a name="sorting"></a>做法：使用 MSQuery 排序資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="d78ac-155">toosort 結果，讓我們來看一個範例。</span><span class="sxs-lookup"><span data-stu-id="d78ac-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="d78ac-156">以遞增的欄位 'text'，然後依照 「 完成 」 遞減排列，toosort 叫用`MSQuery`就像這樣：</span><span class="sxs-lookup"><span data-stu-id="d78ac-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="d78ac-157">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-157">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-158">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-158">**Swift**:</span></span>

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


## <span data-ttu-id="d78ac-159"><a name="selecting"></a><a name="parameters"></a>作法：使用 MSQuery 限制欄位和展開查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="d78ac-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="d78ac-160">在查詢中，傳回 toolimit 欄位 toobe 指定 hello hello 欄位名稱在 hello **selectFields**屬性。</span><span class="sxs-lookup"><span data-stu-id="d78ac-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="d78ac-161">這個範例會傳回只 hello 文字和已完成的欄位：</span><span class="sxs-lookup"><span data-stu-id="d78ac-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="d78ac-162">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="d78ac-163">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="d78ac-164">tooinclude 其他查詢字串參數中 hello 伺服器要求 （例如，因為自訂伺服器端指令碼使用它們），填入`query.parameters`就像這樣：</span><span class="sxs-lookup"><span data-stu-id="d78ac-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="d78ac-165">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="d78ac-166">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="d78ac-167"><a name="paging"></a>如何：設定頁面大小</span><span class="sxs-lookup"><span data-stu-id="d78ac-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="d78ac-168">Azure 行動應用程式，與 hello 頁面大小控制項 hello 會提取從 hello 後端資料表一次的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="d78ac-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="d78ac-169">呼叫太`pull`資料然後會批次處理資料，根據此頁面大小，直到沒有任何多個記錄 toopull 為止。</span><span class="sxs-lookup"><span data-stu-id="d78ac-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="d78ac-170">它會使用頁面大小可能 tooconfigure **MSPullSettings**如下所示。</span><span class="sxs-lookup"><span data-stu-id="d78ac-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="d78ac-171">hello 預設頁面大小為 50，且 hello 下面範例會變更 too3。</span><span class="sxs-lookup"><span data-stu-id="d78ac-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="d78ac-172">您可以基於效能的考量設定不同的頁面大小。</span><span class="sxs-lookup"><span data-stu-id="d78ac-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="d78ac-173">如果您有大量的小型資料記錄，較高的頁面大小會減少往返伺服器的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="d78ac-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="d78ac-174">此設定會控制只 hello 頁面大小 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d78ac-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="d78ac-175">如果 hello 用戶端要求較大的頁面大小高於 hello 行動應用程式後端支援，hello 頁面大小上限為 hello 最大 hello 後端是設定的 toosupport。</span><span class="sxs-lookup"><span data-stu-id="d78ac-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="d78ac-176">這項設定也是 hello*數目*資料記錄不 hello*位元組大小*。</span><span class="sxs-lookup"><span data-stu-id="d78ac-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="d78ac-177">如果您增加 hello 用戶端頁面大小，您也應該增加 hello hello 伺服器上的頁面大小。</span><span class="sxs-lookup"><span data-stu-id="d78ac-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="d78ac-178">請參閱["如何： 調整 hello 表格分頁大小 」](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello 步驟 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="d78ac-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="d78ac-179">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="d78ac-180">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="d78ac-181"><a name="inserting"></a>作法：插入資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="d78ac-182">建立新的資料表資料列，tooinsert`NSDictionary`和叫用`table insert`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="d78ac-183">如果[動態結構描述]已啟用，hello Azure App Service 行動後端會自動產生新資料行是根據 hello `NSDictionary`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="d78ac-184">如果`id`未提供，hello 後端會自動產生新的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="d78ac-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="d78ac-185">提供您自己`id`toouse 傳送電子郵件地址、 使用者名稱或您自己自訂的值為識別碼。</span><span class="sxs-lookup"><span data-stu-id="d78ac-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="d78ac-186">提供您自己的識別碼可以讓聯結和商務導向的資料庫邏輯變得更容易。</span><span class="sxs-lookup"><span data-stu-id="d78ac-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="d78ac-187">hello`result`包含插入的 hello 新項目。</span><span class="sxs-lookup"><span data-stu-id="d78ac-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="d78ac-188">根據您伺服器的邏輯，它可能有其他或已修改的資料比較 toowhat 已傳遞 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d78ac-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="d78ac-189">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-189">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-190">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-190">**Swift**:</span></span>

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

## <span data-ttu-id="d78ac-191"><a name="modifying"></a>作法：修改資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="d78ac-192">tooupdate 現有的資料列，修改項目並呼叫`update`:</span><span class="sxs-lookup"><span data-stu-id="d78ac-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="d78ac-193">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-193">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-194">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-194">**Swift**:</span></span>

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

<span data-ttu-id="d78ac-195">或者，提供 hello 資料列識別碼和更新的 hello 欄位：</span><span class="sxs-lookup"><span data-stu-id="d78ac-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="d78ac-196">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="d78ac-197">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="d78ac-198">最小值，hello`id`進行更新時，必須設定屬性。</span><span class="sxs-lookup"><span data-stu-id="d78ac-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="d78ac-199"><a name="deleting"></a>作法：刪除資料</span><span class="sxs-lookup"><span data-stu-id="d78ac-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="d78ac-200">叫用的項目，toodelete`delete`與 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="d78ac-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="d78ac-201">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="d78ac-202">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="d78ac-203">或者，提供資料列識別碼來進行刪除：</span><span class="sxs-lookup"><span data-stu-id="d78ac-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="d78ac-204">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="d78ac-205">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="d78ac-206">最小值，hello`id`進行刪除時，必須設定屬性。</span><span class="sxs-lookup"><span data-stu-id="d78ac-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="d78ac-207"><a name="customapi"></a>如何：呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="d78ac-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="d78ac-208">使用自訂 API，您可以公開任何後端功能。</span><span class="sxs-lookup"><span data-stu-id="d78ac-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="d78ac-209">它沒有 toomap tooa 資料表作業。</span><span class="sxs-lookup"><span data-stu-id="d78ac-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="d78ac-210">不只取得更多控制訊息，您甚至還可以讀取或設定標頭，並變更 hello 回應內文格式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="d78ac-211">hello 後端，toocreate 自訂 API 的讀取方式 toolearn[自訂 Api](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="d78ac-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="d78ac-212">toocall 自訂 API 中，呼叫`MSClient.invokeAPI`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="d78ac-213">hello 要求和回應內容會被視為 JSON。</span><span class="sxs-lookup"><span data-stu-id="d78ac-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="d78ac-214">toouse 其他類型的媒體，[使用 hello 其他多載`invokeAPI` ] [ 5]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="d78ac-215">toomake`GET`要求而不是`POST`要求，集參數`HTTPMethod`太`"GET"`和參數`body`太`nil`（因為 GET 要求並沒有訊息內文。）如果您的自訂 API 支援其他 HTTP 動詞命令，請適當地變更 `HTTPMethod`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="d78ac-216">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-216">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-217">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-217">**Swift**:</span></span>

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

## <span data-ttu-id="d78ac-218"><a name="templates"></a>如何： 註冊推播範本 toosend 跨平台通知</span><span class="sxs-lookup"><span data-stu-id="d78ac-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="d78ac-219">tooregister 範本，將範本與您**client.push registerDeviceToken**用戶端應用程式中的方法。</span><span class="sxs-lookup"><span data-stu-id="d78ac-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="d78ac-220">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="d78ac-221">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="d78ac-222">您的範本，屬於類型 NSDictionary，且可以包含多個範本中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="d78ac-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="d78ac-223">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="d78ac-224">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="d78ac-225">所有標籤都都會從 hello 安全性要求。</span><span class="sxs-lookup"><span data-stu-id="d78ac-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="d78ac-226">tooadd 標記 tooinstallations 或內安裝的範本，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][4]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="d78ac-227">使用這些已註冊的範本，toosend 通知使用[通知中樞 Api][3]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="d78ac-228"><a name="errors"></a>作法：處理錯誤</span><span class="sxs-lookup"><span data-stu-id="d78ac-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="d78ac-229">當您呼叫 Azure App Service 行動後端時，hello 完成區塊包含`NSError`參數。</span><span class="sxs-lookup"><span data-stu-id="d78ac-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="d78ac-230">發生錯誤時，此參數便會傳回非 Nil。</span><span class="sxs-lookup"><span data-stu-id="d78ac-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="d78ac-231">在您的程式碼中，您應該檢查此參數，並處理 hello 錯誤，可以視 hello 前面程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="d78ac-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="d78ac-232">hello 檔案[ `<WindowsAzureMobileServices/MSError.h>` ] [ 6]定義 hello 常數`MSErrorResponseKey`， `MSErrorRequestKey`，和`MSErrorServerItemKey`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="d78ac-233">tooget 相關 toohello 錯誤的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d78ac-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="d78ac-234">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="d78ac-235">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="d78ac-236">此外，hello 檔案會定義每個錯誤碼的常數：</span><span class="sxs-lookup"><span data-stu-id="d78ac-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="d78ac-237">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="d78ac-238">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="d78ac-239"><a name="adal"></a>如何： 驗證使用者以 hello Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="d78ac-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="d78ac-240">您可以使用 hello Active Directory 驗證程式庫 (ADAL) toosign 使用者將使用 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="d78ac-241">使用身分識別提供者 SDK 用戶端流量驗證會偏好 toousing hello`loginWithProvider:completion:`方法。</span><span class="sxs-lookup"><span data-stu-id="d78ac-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="d78ac-242">用戶端流程驗證能提供較原生的 UX 風格，並允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="d78ac-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d78ac-243">設定下列 hello AAD 登入您的行動裝置應用程式後端[tooconfigure Active Directory 登入服務的應用程式如何][ 7]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d78ac-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="d78ac-244">請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="d78ac-245">對於 iOS，我們建議您該 hello 重新導向 URI 是 hello 表單的`<app-scheme>://<bundle-id>`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="d78ac-246">如需詳細資訊，請參閱 hello [ADAL iOS 快速入門][8]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="d78ac-247">使用 Cocoapods 安裝 ADAL。</span><span class="sxs-lookup"><span data-stu-id="d78ac-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="d78ac-248">編輯下列定義，取代您 Podfile tooinclude hello**您專案**hello 名稱，為您的 Xcode 專案：</span><span class="sxs-lookup"><span data-stu-id="d78ac-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="d78ac-249">和 hello Pod:</span><span class="sxs-lookup"><span data-stu-id="d78ac-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="d78ac-250">使用執行 hello 終端機`pod install`hello 目錄從包含您的專案，然後再開啟 產生 hello Xcode 工作區 （非 hello 專案）。</span><span class="sxs-lookup"><span data-stu-id="d78ac-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="d78ac-251">新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。</span><span class="sxs-lookup"><span data-stu-id="d78ac-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="d78ac-252">取代每個程式碼的以下項目：</span><span class="sxs-lookup"><span data-stu-id="d78ac-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="d78ac-253">取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d78ac-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="d78ac-254">格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。從 Azure Active Directory hello [Azure 傳統入口網站] 中的 hello 網域] 索引標籤，可以複製此值。</span><span class="sxs-lookup"><span data-stu-id="d78ac-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="d78ac-255">取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="d78ac-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="d78ac-256">您可以取得用戶端識別碼，從 hello**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d78ac-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="d78ac-257">取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="d78ac-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="d78ac-258">取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。</span><span class="sxs-lookup"><span data-stu-id="d78ac-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="d78ac-259">此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。</span><span class="sxs-lookup"><span data-stu-id="d78ac-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="d78ac-260">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-260">**Objective-C**:</span></span>

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


<span data-ttu-id="d78ac-261">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
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

## <span data-ttu-id="d78ac-262"><a name="facebook-sdk"></a>如何： 驗證使用者以 hello Facebook SDK for iOS</span><span class="sxs-lookup"><span data-stu-id="d78ac-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="d78ac-263">您可以使用 iOS toosign 使用者的 hello Facebook SDK 至使用 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="d78ac-264">使用用戶端流程驗證是比 toousing hello`loginWithProvider:completion:`方法。</span><span class="sxs-lookup"><span data-stu-id="d78ac-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="d78ac-265">hello 用戶端流程驗證，提供較原始的 UX 操作，並允許其他自訂。</span><span class="sxs-lookup"><span data-stu-id="d78ac-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d78ac-266">依照下列設定 Facebook 登入您的行動裝置應用程式後端[tooconfigure Facebook 登入服務應用程式如何][ 9]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d78ac-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="d78ac-267">安裝 hello Facebook SDK for iOS 的下列 hello [Facebook SDK iOS-快速入門][ 10]文件。</span><span class="sxs-lookup"><span data-stu-id="d78ac-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="d78ac-268">如果不建立應用程式，您可以加入 hello iOS 平台 tooyour 現有註冊。</span><span class="sxs-lookup"><span data-stu-id="d78ac-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="d78ac-269">Facebook 的文件包含一些 Objective C 程式碼中 hello 應用程式委派。</span><span class="sxs-lookup"><span data-stu-id="d78ac-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="d78ac-270">如果您使用**Swift**，您可以使用下列的 AppDelegate.swift 翻譯的 hello:</span><span class="sxs-lookup"><span data-stu-id="d78ac-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
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
4. <span data-ttu-id="d78ac-271">在加法 tooadding `FBSDKCoreKit.framework` tooyour 專案，也將參考加入太`FBSDKLoginKit.framework`hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="d78ac-272">新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。</span><span class="sxs-lookup"><span data-stu-id="d78ac-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="d78ac-273">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-273">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-274">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
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

## <span data-ttu-id="d78ac-275"><a name="twitter-fabric"></a>作法：使用 Twitter Fabric for iOS 來驗證使用者</span><span class="sxs-lookup"><span data-stu-id="d78ac-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="d78ac-276">您可以用於網狀架構 iOS toosign 使用者使用 Twitter 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="d78ac-277">用戶端流程驗證是比 toousing hello`loginWithProvider:completion:`方法，因為它提供更原生的 UX 操作，並允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="d78ac-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d78ac-278">Twitter 登入您的行動裝置應用程式後端設定下列 hello [tooconfigure Twitter 登入服務的應用程式如何](app-service-mobile-how-to-configure-twitter-authentication.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="d78ac-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="d78ac-279">加入下列 hello 網狀架構 tooyour 專案[iOS-快速入門的網狀架構]文件和設定 TwitterKit。</span><span class="sxs-lookup"><span data-stu-id="d78ac-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d78ac-280">根據預設，網狀架構會為您建立 Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d78ac-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="d78ac-281">您可以避免建立應用程式註冊 hello 取用者索引鍵與您先前使用下列程式碼片段的 hello 建立取用者密碼。</span><span class="sxs-lookup"><span data-stu-id="d78ac-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="d78ac-282">或者，您可以取代 hello 取用者索引鍵和取用者密碼值，提供以 hello tooApp 服務值請參閱在 hello[光纖儀表板]。</span><span class="sxs-lookup"><span data-stu-id="d78ac-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="d78ac-283">如果您選擇此選項，是確定 tooset hello 回呼 URL tooa 預留位置值，例如`https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`。</span><span class="sxs-lookup"><span data-stu-id="d78ac-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="d78ac-284">如果您選擇 toouse 您稍早建立的 hello 機密資料，加入下列程式碼 tooyour 應用程式委派 hello:</span><span class="sxs-lookup"><span data-stu-id="d78ac-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="d78ac-285">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-285">**Objective-C**:</span></span>

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

    <span data-ttu-id="d78ac-286">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="d78ac-287">新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。</span><span class="sxs-lookup"><span data-stu-id="d78ac-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="d78ac-288">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-288">**Objective-C**:</span></span>

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

<span data-ttu-id="d78ac-289">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-289">**Swift**:</span></span>

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

## <span data-ttu-id="d78ac-290"><a name="google-sdk"></a>如何： 驗證使用者以 hello Google 登入 SDK 適用於 iOS</span><span class="sxs-lookup"><span data-stu-id="d78ac-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="d78ac-291">您可以使用 iOS toosign 使用者的 hello Google 登入 SDK 到應用程式使用 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d78ac-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="d78ac-292">Google 最近宣布變更 tootheir OAuth 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="d78ac-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="d78ac-293">這些原則的變更將需要在未來的 hello Google SDK hello 使用。</span><span class="sxs-lookup"><span data-stu-id="d78ac-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="d78ac-294">設定下列 hello Google 登入您的行動裝置應用程式後端[tooconfigure Google 登入服務應用程式如何](app-service-mobile-how-to-configure-google-authentication.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="d78ac-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="d78ac-295">安裝 hello Google SDK 適用於 iOS 的下列 hello [Google 登入的 iOS-啟動整合](https://developers.google.com/identity/sign-in/ios/start-integrating)文件。</span><span class="sxs-lookup"><span data-stu-id="d78ac-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="d78ac-296">您可以略過 hello < 驗證與後端伺服器 > 一節。</span><span class="sxs-lookup"><span data-stu-id="d78ac-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="d78ac-297">新增下列 tooyour 委派 hello`signIn:didSignInForUser:withError:`方法，根據您所使用的 toohello 語言。</span><span class="sxs-lookup"><span data-stu-id="d78ac-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="d78ac-298">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="d78ac-299">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="d78ac-300">請確定您也可以加入 hello 太遵循`application:didFinishLaunchingWithOptions:`應用程式中委派、"SERVER_CLIENT_ID"取代成 hello 相同識別碼使用您在步驟 1 中的 tooconfigure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="d78ac-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="d78ac-301">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="d78ac-302">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="d78ac-303">新增下列程式碼 tooyour 應用程式中實作 hello UIViewController hello`GIDSignInUIDelegate`通訊協定，根據您所使用的 toohello 語言。</span><span class="sxs-lookup"><span data-stu-id="d78ac-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="d78ac-304">同樣地，登入之前已登出，雖然您不需要 tooenter 認證一次，但您會看到同意對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d78ac-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="d78ac-305">Hello 工作階段權杖已過期時，才可以呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="d78ac-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="d78ac-306">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="d78ac-307">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="d78ac-307">**Swift**:</span></span>

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
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure 行動應用程式快速入門]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[動態結構描述]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[光纖儀表板]: https://www.fabric.io/home
[iOS-快速入門的網狀架構]: https://docs.fabric.io/ios/fabric/getting-started.html
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
