---
title: "aaaEnable 離線同步處理使用 iOS 行動應用程式 |Microsoft 文件"
description: "深入了解如何 toouse Azure App Service 行動應用程式 toocache 和同步處理離線 iOS 應用程式資料。"
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="8f274-103">啟用 iOS Mobile Apps 的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="8f274-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="8f274-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8f274-104">Overview</span></span>
<span data-ttu-id="8f274-105">本教學課程涵蓋與 hello 行動應用程式功能的 Azure App Service 適用於 iOS 的離線同步處理。</span><span class="sxs-lookup"><span data-stu-id="8f274-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="8f274-106">使用離線同步處理的使用者可以與行動裝置應用程式 tooview 互動中、 新增或修改資料，即使它們有沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="8f274-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="8f274-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="8f274-107">Changes are stored in a local database.</span></span> <span data-ttu-id="8f274-108">Hello 裝置恢復連線後，同步處理 hello 變更 hello 遠端的後端。</span><span class="sxs-lookup"><span data-stu-id="8f274-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="8f274-109">如果這是您首次經驗與行動應用程式，您應該先完成 hello 教學課程[建立 iOS 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8f274-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="8f274-110">如果您不使用下載的 hello 伺服器快速入門專案，您必須加入 hello 資料存取擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="8f274-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="8f274-111">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="8f274-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="8f274-112">toolearn 進一步了解 hello 離線同步處理功能，請參閱[行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="8f274-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="8f274-113"><a name="review-sync"></a>檢閱 hello 用戶端同步程式碼</span><span class="sxs-lookup"><span data-stu-id="8f274-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="8f274-114">您下載的 hello hello 用戶端專案[建立 iOS 應用程式]教學課程已包含可支援使用本機的核心資料為基礎資料庫的離線同步處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8f274-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="8f274-115">本節摘要說明在 hello 教學課程的程式碼中已包含內容。</span><span class="sxs-lookup"><span data-stu-id="8f274-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="8f274-116">Hello 功能的概念性概觀，請參閱[行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="8f274-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="8f274-117">使用行動應用程式的 hello 離線的資料同步處理功能，使用者可以互動本機資料庫即使 hello 網路是無法存取。</span><span class="sxs-lookup"><span data-stu-id="8f274-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="8f274-118">toouse 初始化 hello 同步處理內容的應用程式中的這些功能，`MSClient`和參考本機存放區。</span><span class="sxs-lookup"><span data-stu-id="8f274-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="8f274-119">然後參考資料表透過 hello **MSSyncTable**介面。</span><span class="sxs-lookup"><span data-stu-id="8f274-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="8f274-120">在**QSTodoService.m** (OBJECTIVE-C) 或**ToDoTableViewController.swift** hello hello 成員型別 (Swift)，請注意**syncTable**是**MSSyncTable**。</span><span class="sxs-lookup"><span data-stu-id="8f274-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="8f274-121">離線同步處理會使用此同步處理資料表介面，而不是 **MSTable**。</span><span class="sxs-lookup"><span data-stu-id="8f274-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="8f274-122">使用同步處理資料表時，所有作業移 toohello 本機存放區只能與 hello 遠端端與明確的推入進行同步處理和提取作業。</span><span class="sxs-lookup"><span data-stu-id="8f274-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="8f274-123">tooget 參考 tooa 同步處理資料表，使用 hello **syncTableWithName**方法`MSClient`。</span><span class="sxs-lookup"><span data-stu-id="8f274-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="8f274-124">tooremove 離線同步處理功能、 使用**tableWithName**改為。</span><span class="sxs-lookup"><span data-stu-id="8f274-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="8f274-125">在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="8f274-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="8f274-126">Hello 相關程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="8f274-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="8f274-127">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="8f274-127">**Objective-C**.</span></span> <span data-ttu-id="8f274-128">在 hello **QSTodoService.init**方法：</span><span class="sxs-lookup"><span data-stu-id="8f274-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="8f274-129">**Swift**。</span><span class="sxs-lookup"><span data-stu-id="8f274-129">**Swift**.</span></span> <span data-ttu-id="8f274-130">在 hello **ToDoTableViewController.viewDidLoad**方法：</span><span class="sxs-lookup"><span data-stu-id="8f274-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="8f274-131">這個方法會建立本機存放區使用 hello `MSCoreDataStore` hello 行動應用程式 SDK 的介面提供。</span><span class="sxs-lookup"><span data-stu-id="8f274-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="8f274-132">或者，您可以提供不同的本機存放區，藉由實作 hello`MSSyncContextDataSource`通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8f274-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="8f274-133">此外，hello 的第一個參數**MSSyncContext**是使用的 toospecify 衝突處理常式。</span><span class="sxs-lookup"><span data-stu-id="8f274-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="8f274-134">因為我們傳遞`nil`，我們取得 hello 預設衝突處理常式，在任何衝突時失敗。</span><span class="sxs-lookup"><span data-stu-id="8f274-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="8f274-135">現在，讓我們執行 hello 實際的同步處理作業，並從 hello 遠端的後端取得資料：</span><span class="sxs-lookup"><span data-stu-id="8f274-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="8f274-136">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="8f274-136">**Objective-C**.</span></span> <span data-ttu-id="8f274-137">`syncData`第一次將新的變更推入，然後呼叫**pullData** tooget hello 遠端的後端的資料。</span><span class="sxs-lookup"><span data-stu-id="8f274-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="8f274-138">接著，hello **pullData**方法會取得新的資料與查詢相符：</span><span class="sxs-lookup"><span data-stu-id="8f274-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="8f274-139">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="8f274-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="8f274-140">在 hello Objective C 版本中，在`syncData`，我們先呼叫**pushWithCompletion** hello 同步處理內容上。</span><span class="sxs-lookup"><span data-stu-id="8f274-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="8f274-141">這個方法是屬於`MSSyncContext`（而不 hello 同步處理資料表本身） 因為跨所有資料表發送變更。</span><span class="sxs-lookup"><span data-stu-id="8f274-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="8f274-142">已修改以某種方式在本機 （透過 CUD 作業） 的記錄傳送 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f274-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="8f274-143">然後 hello helper **pullData**呼叫，而它會呼叫**MSSyncTable.pullWithQuery** tooretrieve 遠端資料並將它儲存在 hello 本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="8f274-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="8f274-144">在 hello Swift 版本中，hello 推入作業不是絕對必要，因為沒有呼叫太**pushWithCompletion**。</span><span class="sxs-lookup"><span data-stu-id="8f274-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="8f274-145">如果正在進行推入作業的 hello 資料表的 hello 同步內容中沒有任何暫止的變更，提取永遠會發出推入第一次。</span><span class="sxs-lookup"><span data-stu-id="8f274-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="8f274-146">不過，如果您有一個以上的同步處理資料表時，它是所有設定都一致跨相關資料表最佳的 tooexplicitly 呼叫發送 tooensure。</span><span class="sxs-lookup"><span data-stu-id="8f274-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="8f274-147">在 hello Objective C 和 Swift 的版本中，您可以使用 hello **pullWithQuery**方法 toospecify 查詢 toofilter hello 想 tooretrieve 記錄。</span><span class="sxs-lookup"><span data-stu-id="8f274-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="8f274-148">在此範例中，hello 查詢會擷取所有記錄遠端 hello`TodoItem`資料表。</span><span class="sxs-lookup"><span data-stu-id="8f274-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="8f274-149">hello 第二個參數**pullWithQuery**是用於查詢識別碼*增量同步處理*。增量同步處理擷取自 hello 上次同步處理，使用 hello 記錄已修改的記錄`UpdatedAt`時間戳記 (稱為`updatedAt`hello 本機存放區中。) 應該對每個邏輯的查詢中是唯一的描述性字串 hello 查詢識別碼。您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f274-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="8f274-150">tooopt 未增量同步，傳遞`nil`如 hello 的查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f274-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="8f274-151">此方法可能效率不佳，因為它會在每次提取作業擷取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="8f274-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="8f274-152">當您修改或加入的資料，當使用者執行 hello 重新整理鍵筆勢，而且在啟動 hello Objective C 應用程式同步處理。</span><span class="sxs-lookup"><span data-stu-id="8f274-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="8f274-153">hello Swift 應用程式進行同步時 hello 使用者執行 hello 重新整理筆勢和啟動。</span><span class="sxs-lookup"><span data-stu-id="8f274-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="8f274-154">Hello 應用程式同步處理資料時修改 (OBJECTIVE-C)，或是每當 hello 應用程式啟動時 （Objective C 和 Swift），hello 應用程式會假設該 hello 使用者在線上。</span><span class="sxs-lookup"><span data-stu-id="8f274-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="8f274-155">在更新版本的區段中，您將更新 hello 應用程式，讓使用者可以編輯，即使它們是離線。</span><span class="sxs-lookup"><span data-stu-id="8f274-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="8f274-156"><a name="review-core-data"></a>檢閱 hello 核心資料模型</span><span class="sxs-lookup"><span data-stu-id="8f274-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="8f274-157">當您使用 hello 的核心資料離線存放區時，您必須定義資料模型中的特定資料表和欄位。</span><span class="sxs-lookup"><span data-stu-id="8f274-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="8f274-158">hello 範例應用程式已經包含資料模型與 hello 正確的格式。</span><span class="sxs-lookup"><span data-stu-id="8f274-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="8f274-159">在本節中，我們逐步進行這些資料表 tooshow 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="8f274-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="8f274-160">開啟 **QSDataModel.xcdatamodeld**。</span><span class="sxs-lookup"><span data-stu-id="8f274-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="8f274-161">四個資料表所使用的三個定義-hello SDK 和一個用於 hello 待辦項目本身：</span><span class="sxs-lookup"><span data-stu-id="8f274-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="8f274-162">MS_TableOperations： 曲目 hello 需要 toobe 與 hello 伺服器同步處理的項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="8f274-163">MS_TableOperationErrors：追蹤在離線同步處理期間發生的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="8f274-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="8f274-164">MS_TableConfig： 曲目 hello hello 上次同步處理作業的所有提取作業的上次更新時間。</span><span class="sxs-lookup"><span data-stu-id="8f274-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="8f274-165">TodoItem： 儲存 hello 待辦項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="8f274-166">hello 系統資料行**createdAt**， **updatedAt**，和**版本**是選用的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="8f274-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="8f274-167">hello 行動應用程式 SDK 保留開頭的資料行名稱"**``**"。</span><span class="sxs-lookup"><span data-stu-id="8f274-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="8f274-168">請不要將此前置詞用於系統資料行以外的項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="8f274-169">否則，當您使用 hello 遠端的後端時，會修改資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="8f274-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="8f274-170">當您使用 hello 離線同步處理功能時，定義三個系統資料表 hello 和 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="8f274-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="8f274-171">系統資料表</span><span class="sxs-lookup"><span data-stu-id="8f274-171">System tables</span></span>

<span data-ttu-id="8f274-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="8f274-172">**MS_TableOperations**</span></span>  

![MS_TableOperations 資料表屬性][defining-core-data-tableoperations-entity]

| <span data-ttu-id="8f274-174">屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-174">Attribute</span></span> | <span data-ttu-id="8f274-175">類型</span><span class="sxs-lookup"><span data-stu-id="8f274-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="8f274-176">id</span><span class="sxs-lookup"><span data-stu-id="8f274-176">id</span></span> | <span data-ttu-id="8f274-177">整數 64</span><span class="sxs-lookup"><span data-stu-id="8f274-177">Integer 64</span></span> |
| <span data-ttu-id="8f274-178">itemId</span><span class="sxs-lookup"><span data-stu-id="8f274-178">itemId</span></span> | <span data-ttu-id="8f274-179">String</span><span class="sxs-lookup"><span data-stu-id="8f274-179">String</span></span> |
| <span data-ttu-id="8f274-180">properties</span><span class="sxs-lookup"><span data-stu-id="8f274-180">properties</span></span> | <span data-ttu-id="8f274-181">二進位資料</span><span class="sxs-lookup"><span data-stu-id="8f274-181">Binary Data</span></span> |
| <span data-ttu-id="8f274-182">資料表</span><span class="sxs-lookup"><span data-stu-id="8f274-182">table</span></span> | <span data-ttu-id="8f274-183">String</span><span class="sxs-lookup"><span data-stu-id="8f274-183">String</span></span> |
| <span data-ttu-id="8f274-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="8f274-184">tableKind</span></span> | <span data-ttu-id="8f274-185">整數 16</span><span class="sxs-lookup"><span data-stu-id="8f274-185">Integer 16</span></span> |


<span data-ttu-id="8f274-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="8f274-186">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors 資料表屬性][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="8f274-188">屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-188">Attribute</span></span> | <span data-ttu-id="8f274-189">類型</span><span class="sxs-lookup"><span data-stu-id="8f274-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="8f274-190">id</span><span class="sxs-lookup"><span data-stu-id="8f274-190">id</span></span> |<span data-ttu-id="8f274-191">String</span><span class="sxs-lookup"><span data-stu-id="8f274-191">String</span></span> |
| <span data-ttu-id="8f274-192">operationId</span><span class="sxs-lookup"><span data-stu-id="8f274-192">operationId</span></span> |<span data-ttu-id="8f274-193">整數 64</span><span class="sxs-lookup"><span data-stu-id="8f274-193">Integer 64</span></span> |
| <span data-ttu-id="8f274-194">properties</span><span class="sxs-lookup"><span data-stu-id="8f274-194">properties</span></span> |<span data-ttu-id="8f274-195">二進位資料</span><span class="sxs-lookup"><span data-stu-id="8f274-195">Binary Data</span></span> |
| <span data-ttu-id="8f274-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="8f274-196">tableKind</span></span> |<span data-ttu-id="8f274-197">整數 16</span><span class="sxs-lookup"><span data-stu-id="8f274-197">Integer 16</span></span> |

 <span data-ttu-id="8f274-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="8f274-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="8f274-199">屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-199">Attribute</span></span> | <span data-ttu-id="8f274-200">類型</span><span class="sxs-lookup"><span data-stu-id="8f274-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="8f274-201">id</span><span class="sxs-lookup"><span data-stu-id="8f274-201">id</span></span> |<span data-ttu-id="8f274-202">String</span><span class="sxs-lookup"><span data-stu-id="8f274-202">String</span></span> |
| <span data-ttu-id="8f274-203">索引鍵</span><span class="sxs-lookup"><span data-stu-id="8f274-203">key</span></span> |<span data-ttu-id="8f274-204">String</span><span class="sxs-lookup"><span data-stu-id="8f274-204">String</span></span> |
| <span data-ttu-id="8f274-205">keyType</span><span class="sxs-lookup"><span data-stu-id="8f274-205">keyType</span></span> |<span data-ttu-id="8f274-206">整數 64</span><span class="sxs-lookup"><span data-stu-id="8f274-206">Integer 64</span></span> |
| <span data-ttu-id="8f274-207">資料表</span><span class="sxs-lookup"><span data-stu-id="8f274-207">table</span></span> |<span data-ttu-id="8f274-208">String</span><span class="sxs-lookup"><span data-stu-id="8f274-208">String</span></span> |
| <span data-ttu-id="8f274-209">value</span><span class="sxs-lookup"><span data-stu-id="8f274-209">value</span></span> |<span data-ttu-id="8f274-210">String</span><span class="sxs-lookup"><span data-stu-id="8f274-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="8f274-211">資料表</span><span class="sxs-lookup"><span data-stu-id="8f274-211">Data table</span></span>

<span data-ttu-id="8f274-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="8f274-212">**TodoItem**</span></span>

| <span data-ttu-id="8f274-213">屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-213">Attribute</span></span> | <span data-ttu-id="8f274-214">類型</span><span class="sxs-lookup"><span data-stu-id="8f274-214">Type</span></span> | <span data-ttu-id="8f274-215">注意</span><span class="sxs-lookup"><span data-stu-id="8f274-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f274-216">id</span><span class="sxs-lookup"><span data-stu-id="8f274-216">id</span></span> | <span data-ttu-id="8f274-217">字串 (標示為必要)</span><span class="sxs-lookup"><span data-stu-id="8f274-217">String, marked required</span></span> |<span data-ttu-id="8f274-218">遠端存放區中的主索引鍵</span><span class="sxs-lookup"><span data-stu-id="8f274-218">Primary key in remote store</span></span> |
| <span data-ttu-id="8f274-219">完成</span><span class="sxs-lookup"><span data-stu-id="8f274-219">complete</span></span> | <span data-ttu-id="8f274-220">Boolean</span><span class="sxs-lookup"><span data-stu-id="8f274-220">Boolean</span></span> | <span data-ttu-id="8f274-221">To-do 項目欄位</span><span class="sxs-lookup"><span data-stu-id="8f274-221">To-do item field</span></span> |
| <span data-ttu-id="8f274-222">文字</span><span class="sxs-lookup"><span data-stu-id="8f274-222">text</span></span> |<span data-ttu-id="8f274-223">String</span><span class="sxs-lookup"><span data-stu-id="8f274-223">String</span></span> |<span data-ttu-id="8f274-224">To-do 項目欄位</span><span class="sxs-lookup"><span data-stu-id="8f274-224">To-do item field</span></span> |
| <span data-ttu-id="8f274-225">建立時間</span><span class="sxs-lookup"><span data-stu-id="8f274-225">createdAt</span></span> | <span data-ttu-id="8f274-226">Date</span><span class="sxs-lookup"><span data-stu-id="8f274-226">Date</span></span> | <span data-ttu-id="8f274-227">（選擇性）對應太**createdAt**系統屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="8f274-228">更新時間</span><span class="sxs-lookup"><span data-stu-id="8f274-228">updatedAt</span></span> | <span data-ttu-id="8f274-229">Date</span><span class="sxs-lookup"><span data-stu-id="8f274-229">Date</span></span> | <span data-ttu-id="8f274-230">（選擇性）對應太**updatedAt**系統屬性</span><span class="sxs-lookup"><span data-stu-id="8f274-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="8f274-231">版本</span><span class="sxs-lookup"><span data-stu-id="8f274-231">version</span></span> | <span data-ttu-id="8f274-232">String</span><span class="sxs-lookup"><span data-stu-id="8f274-232">String</span></span> | <span data-ttu-id="8f274-233">（選擇性）使用的 toodetect 衝突，對應 tooversion</span><span class="sxs-lookup"><span data-stu-id="8f274-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="8f274-234"><a name="setup-sync"></a>Hello hello 應用程式同步行為變更</span><span class="sxs-lookup"><span data-stu-id="8f274-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="8f274-235">本節中，您會修改 hello 應用程式，使它不會同步啟動應用程式，或當您插入和更新項目上。</span><span class="sxs-lookup"><span data-stu-id="8f274-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="8f274-236">其會同步執行 hello 重新整理手勢按鈕時，才。</span><span class="sxs-lookup"><span data-stu-id="8f274-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="8f274-237">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="8f274-237">**Objective-C**:</span></span>

1. <span data-ttu-id="8f274-238">在**QSTodoListViewController.m**，變更 hello **viewDidLoad**方法 tooremove 太 hello 呼叫`[self refresh]`hello hello 方法結尾。</span><span class="sxs-lookup"><span data-stu-id="8f274-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="8f274-239">現在 hello 資料未與 hello 伺服器上啟動應用程式同步處理。</span><span class="sxs-lookup"><span data-stu-id="8f274-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="8f274-240">相反地，它會與 hello hello 本機存放區內容同步。</span><span class="sxs-lookup"><span data-stu-id="8f274-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="8f274-241">在**QSTodoService.m**，修改 hello 定義`addItem`，讓它在 hello 項目插入後不會同步處理。</span><span class="sxs-lookup"><span data-stu-id="8f274-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="8f274-242">移除 hello`self syncData`封鎖，並取代為下列 hello:</span><span class="sxs-lookup"><span data-stu-id="8f274-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="8f274-243">修改 hello 定義`completeItem`如先前所述。</span><span class="sxs-lookup"><span data-stu-id="8f274-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="8f274-244">移除 hello 區塊`self syncData`並取代為下列 hello:</span><span class="sxs-lookup"><span data-stu-id="8f274-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="8f274-245">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="8f274-245">**Swift**:</span></span>

<span data-ttu-id="8f274-246">在`viewDidLoad`，請在**ToDoTableViewController.swift**，這裡顯示，toostop 上啟動應用程式同步處理 hello 兩行程式碼的註解。</span><span class="sxs-lookup"><span data-stu-id="8f274-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="8f274-247">Hello Swift 待辦事項應用程式在 hello 撰寫本文時，它不會更新 hello 服務新增或完成項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="8f274-248">它會更新 hello 服務只在啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f274-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="8f274-249"><a name="test-app"></a>測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8f274-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="8f274-250">本節中，您可以連接無效 URL toosimulate tooan 離線的案例。</span><span class="sxs-lookup"><span data-stu-id="8f274-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="8f274-251">當您將資料的項目時，它們保留在 hello 本機的核心資料存放區，但它們未同步處理 hello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="8f274-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="8f274-252">變更中的 hello 行動裝置應用程式 URL **QSTodoService.m** tooan 無效的 URL，然後再次執行的 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="8f274-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="8f274-253">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="8f274-253">**Objective-C**.</span></span> <span data-ttu-id="8f274-254">在 QSTodoService.m 中：</span><span class="sxs-lookup"><span data-stu-id="8f274-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="8f274-255">**Swift**。</span><span class="sxs-lookup"><span data-stu-id="8f274-255">**Swift**.</span></span> <span data-ttu-id="8f274-256">在 ToDoTableViewController.swift 中：</span><span class="sxs-lookup"><span data-stu-id="8f274-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="8f274-257">新增一些 To-do 項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-257">Add some to-do items.</span></span> <span data-ttu-id="8f274-258">結束模擬器 hello （或強制關閉 hello 應用程式），然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="8f274-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="8f274-259">確認已保存您的變更。</span><span class="sxs-lookup"><span data-stu-id="8f274-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="8f274-260">檢視遠端 hello hello 內容**TodoItem**資料表：</span><span class="sxs-lookup"><span data-stu-id="8f274-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="8f274-261">Node.js 的後端，請移 toohello [Azure 入口網站](https://portal.azure.com/)，然後在您行動裝置應用程式後端中，按一下**簡單資料表** > **TodoItem**。</span><span class="sxs-lookup"><span data-stu-id="8f274-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="8f274-262">針對 .NET 後端，請使用 SQL 工具 (例如 SQL Server Management Studio) 或 REST 用戶端 (例如 Fiddler 或 Postman)。</span><span class="sxs-lookup"><span data-stu-id="8f274-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="8f274-263">請確認 hello 新項目有*不*已與 hello 伺服器進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="8f274-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="8f274-264">變更 hello URL 後 toohello 更正其中中**QSTodoService.m**，並重新執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f274-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="8f274-265">Hello 清單中的項目，藉以執行 hello 重新整理筆勢。</span><span class="sxs-lookup"><span data-stu-id="8f274-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="8f274-266">會出現旋轉進度指示器。</span><span class="sxs-lookup"><span data-stu-id="8f274-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="8f274-267">檢視 hello **TodoItem**資料一次。</span><span class="sxs-lookup"><span data-stu-id="8f274-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="8f274-268">現在應該顯示 hello 新增和變更待辦項目。</span><span class="sxs-lookup"><span data-stu-id="8f274-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="8f274-269">摘要</span><span class="sxs-lookup"><span data-stu-id="8f274-269">Summary</span></span>
<span data-ttu-id="8f274-270">toosupport hello 離線同步處理功能，我們使用 hello`MSSyncTable`介面，並初始化`MSClient.syncContext`與本機存放區。</span><span class="sxs-lookup"><span data-stu-id="8f274-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="8f274-271">在此情況下，hello 本機存放區當時在核心資料為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8f274-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="8f274-272">當您使用的核心資料本機存放區時，您必須定義數個資料表以 hello[更正系統屬性](#review-core-data)。</span><span class="sxs-lookup"><span data-stu-id="8f274-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="8f274-273">hello 一般建立、 讀取、 更新和刪除 (CRUD) 作業的行動應用程式可視為 hello 應用程式仍然連接，但所有 hello 作業都發生 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="8f274-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="8f274-274">當我們與 hello 伺服器同步 hello 本機存放區時，我們使用 hello **MSSyncTable.pullWithQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="8f274-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f274-275">其他資源</span><span class="sxs-lookup"><span data-stu-id="8f274-275">Additional resources</span></span>
* <span data-ttu-id="8f274-276">[行動應用程式中的離線資料同步]</span><span class="sxs-lookup"><span data-stu-id="8f274-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="8f274-277">[雲端涵蓋： Azure Mobile Services 中的離線同步] \(hello 視訊是關於行動服務，但行動應用程式離線同步運作方式類似。\)</span><span class="sxs-lookup"><span data-stu-id="8f274-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[建立 iOS 應用程式]: app-service-mobile-ios-get-started.md
[行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[雲端涵蓋： Azure Mobile Services 中的離線同步]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
