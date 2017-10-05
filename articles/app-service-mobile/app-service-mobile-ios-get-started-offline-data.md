---
title: "啟用 iOS Mobile Apps 的離線同步處理 | Microsoft Docs"
description: "了解如何使用 Azure App Service Mobile Apps 來快取及同步處理 iOS 應用程式中的離線資料。"
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
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="e5ac1-103">啟用 iOS Mobile Apps 的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="e5ac1-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="e5ac1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e5ac1-104">Overview</span></span>
<span data-ttu-id="e5ac1-105">本教學課程涵蓋適用於 iOS 的 Azure App Service Mobile Apps 功能的離線同步處理說明。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="e5ac1-106">透過離線同步處理，終端使用者即使沒有網路連線，也可以和行動裝置 App 互動以檢視、新增、修改資料。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="e5ac1-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-107">Changes are stored in a local database.</span></span> <span data-ttu-id="e5ac1-108">裝置恢復上線後，這些變更就會與遠端後端進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="e5ac1-109">如果這是您第一次接觸 Mobile Apps，請先完成[建立 iOS 應用程式] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="e5ac1-110">如果您不使用下載的快速入門伺服器專案，則必須將資料存取擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="e5ac1-111">如需伺服器擴充套件的詳細資訊，請參閱 [使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="e5ac1-112">若要深入了解離線同步處理功能，請參閱 [Mobile Apps 中的離線資料同步處理]。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="e5ac1-113"><a name="review-sync"></a>檢閱用戶端同步程式碼</span><span class="sxs-lookup"><span data-stu-id="e5ac1-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="e5ac1-114">您針對[建立 iOS 應用程式]教學課程下載的用戶端專案，已經包含了使用本機核心資料式資料庫支援離線同步處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="e5ac1-115">本節將摘要說明已包含在教學課程程式碼中的內容。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="e5ac1-116">如需此功能的概念性概觀，請參閱 [Mobile Apps 中的離線資料同步處理]。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="e5ac1-117">Mobile Apps 的離線資料同步處理功能可讓終端使用者在無法存取網路時，仍可與本機資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="e5ac1-118">若要在您的應用程式中使用這些功能，您可初始化 `MSClient` 的同步處理內容以及參考本機存放區。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="e5ac1-119">然後透過 **MSSyncTable** 介面參考您的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="e5ac1-120">在 **QSTodoService.m** (Objective-C) 或 **ToDoTableViewController.swift** (Swift) 中，注意到成員 **syncTable** 的類型為 **MSSyncTable**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="e5ac1-121">離線同步處理會使用此同步處理資料表介面，而不是 **MSTable**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="e5ac1-122">使用同步處理資料表時，所有作業都會移至本機存放區，而且只會與具有明確推送和提取作業的遠端後端同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="e5ac1-123">若要取得同步處理資料表的參考，請在 `MSClient` 上使用 **syncTableWithName** 方法。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="e5ac1-124">若要移除離線同步處理功能，請改用 **tableWithName**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="e5ac1-125">必須先初始化本機存放區，才可以執行資料表作業。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="e5ac1-126">以下是相關的程式碼：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-126">Here is the relevant code:</span></span>

* <span data-ttu-id="e5ac1-127">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-127">**Objective-C**.</span></span> <span data-ttu-id="e5ac1-128">在 **QSTodoService.init** 方法中：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="e5ac1-129">**Swift**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-129">**Swift**.</span></span> <span data-ttu-id="e5ac1-130">在 **ToDoTableViewController.viewDidLoad** 方法中︰</span><span class="sxs-lookup"><span data-stu-id="e5ac1-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="e5ac1-131">這方法會以 Mobile Apps SDK 提供的 `MSCoreDataStore` 介面建立一個本機存放區。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="e5ac1-132">或者，您也可以實作 `MSSyncContextDataSource` 通訊協定，改為提供不同的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="e5ac1-133">此外，**MSSyncContext** 的第一個參數是用來指定衝突處理常式。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="e5ac1-134">因為已傳遞 `nil`，所以我們會取得預設衝突處理常式，該處理常式在任何衝突時都會失敗。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="e5ac1-135">現在，讓我們執行實際的同步處理作業，並從遠端後端取得資料：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="e5ac1-136">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-136">**Objective-C**.</span></span> <span data-ttu-id="e5ac1-137">`syncData` 先推送新的變更，然後呼叫 **pullData** 以從遠端後端取得資料。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="e5ac1-138">最後，**pullData** 方法會取得符合查詢的新資料︰</span><span class="sxs-lookup"><span data-stu-id="e5ac1-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="e5ac1-139">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="e5ac1-140">在 Objective-C 版本中，於 `syncData`，我們會先在同步處理內容上呼叫 **pushWithCompletion**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="e5ac1-141">此方法是 `MSSyncContext` 的成員 (而非同步處理資料表本身)，因為它會將變更推送至所有資料表。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="e5ac1-142">只有以某種方式在本機上修改過的記錄 (透過 CUD 作業)，才會傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="e5ac1-143">接著會呼叫 **pullData** 協助程式，該程式會呼叫 **MSSyncTable.pullWithQuery** 來擷取遠端資料並存放在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="e5ac1-144">在 Swift 版本中，因為推送作業不是絕對必要，所以並沒有呼叫 **pushWithCompletion**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="e5ac1-145">如果同步處理內容中正在進行推送作業的資料表有任何變更擱置，則提取一律會先發出推送。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="e5ac1-146">不過，如果您有一個以上的同步處理資料表，最好能明確呼叫推送，以確保所有的相關資料表都能一致。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="e5ac1-147">在 Objective-C 與 Swift 版本中，您可以使用 **pullWithQuery** 方法來指定查詢，以篩選想要擷取的記錄。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="e5ac1-148">在此範例中，查詢會擷取遠端 `TodoItem` 資料表中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="e5ac1-149">**pullWithQuery** 的第二個參數是用於「增量同步處理」的查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="e5ac1-150">增量同步處理會使用記錄的 `UpdatedAt` 時間戳記 (在本機存放區中稱為 `updatedAt`)，僅取出自上次同步處理後修改的記錄。對您應用程式中的每個邏輯查詢而言，查詢識別碼應該是唯一的描述性字串。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="e5ac1-151">若選擇不要增量同步處理，請傳遞 `nil` 做為查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="e5ac1-152">此方法可能效率不佳，因為它會在每次提取作業擷取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="e5ac1-153">當您修改或新增資料、使用者執行重新整理動作及啟動時，Objective-C 應用程式就會同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="e5ac1-154">當使用者執行重新整理動作及啟動時，Swift 應用程式就會同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="e5ac1-155">因為每當資料修改 (Objective-C) 或 App 啟動 (Objective-C 和 Swift) 時，App 就會同步處理，故 App 假設使用者在線上。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="e5ac1-156">在後續章節中，您將會更新 App，讓使用者即使是離線狀態也能進行編輯。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="e5ac1-157"><a name="review-core-data"></a>檢閱核心資料模型</span><span class="sxs-lookup"><span data-stu-id="e5ac1-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="e5ac1-158">在使用「核心資料離線」存放區時，您必須在資料模型中定義特定資料表和欄位。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="e5ac1-159">範例應用程式已經包含具有正確格式的資料模型。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="e5ac1-160">在這一節中，我們會逐步介紹這些資料表並示範其使用方式。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="e5ac1-161">開啟 **QSDataModel.xcdatamodeld**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="e5ac1-162">已定義四個資料表--其中三個由 SDK 使用，而一個是用於 To-do 項目本身：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="e5ac1-163">MS_TableOperations：追蹤需要與伺服器同步的項目。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="e5ac1-164">MS_TableOperationErrors：追蹤在離線同步處理期間發生的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="e5ac1-165">MS_TableConfig：追蹤所有提取作業的最後一次同步處理作業的上次更新時間。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="e5ac1-166">TodoItem：儲存 To-do 項目。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="e5ac1-167">系統資料行 **createdAt**、**updatedAt** 和 **version** 為選擇性系統屬性。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="e5ac1-168">Mobile Apps SDK 會保留以 "**``**" 為開頭的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="e5ac1-169">請不要將此前置詞用於系統資料行以外的項目。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="e5ac1-170">否則，當您使用遠端後端時，系統會修改您的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="e5ac1-171">當您使用離線同步處理功能時，請定義三個系統資料表，以及資料資料表。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="e5ac1-172">系統資料表</span><span class="sxs-lookup"><span data-stu-id="e5ac1-172">System tables</span></span>

<span data-ttu-id="e5ac1-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="e5ac1-173">**MS_TableOperations**</span></span>  

![MS_TableOperations 資料表屬性][defining-core-data-tableoperations-entity]

| <span data-ttu-id="e5ac1-175">屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-175">Attribute</span></span> | <span data-ttu-id="e5ac1-176">類型</span><span class="sxs-lookup"><span data-stu-id="e5ac1-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e5ac1-177">id</span><span class="sxs-lookup"><span data-stu-id="e5ac1-177">id</span></span> | <span data-ttu-id="e5ac1-178">整數 64</span><span class="sxs-lookup"><span data-stu-id="e5ac1-178">Integer 64</span></span> |
| <span data-ttu-id="e5ac1-179">itemId</span><span class="sxs-lookup"><span data-stu-id="e5ac1-179">itemId</span></span> | <span data-ttu-id="e5ac1-180">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-180">String</span></span> |
| <span data-ttu-id="e5ac1-181">properties</span><span class="sxs-lookup"><span data-stu-id="e5ac1-181">properties</span></span> | <span data-ttu-id="e5ac1-182">二進位資料</span><span class="sxs-lookup"><span data-stu-id="e5ac1-182">Binary Data</span></span> |
| <span data-ttu-id="e5ac1-183">資料表</span><span class="sxs-lookup"><span data-stu-id="e5ac1-183">table</span></span> | <span data-ttu-id="e5ac1-184">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-184">String</span></span> |
| <span data-ttu-id="e5ac1-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="e5ac1-185">tableKind</span></span> | <span data-ttu-id="e5ac1-186">整數 16</span><span class="sxs-lookup"><span data-stu-id="e5ac1-186">Integer 16</span></span> |


<span data-ttu-id="e5ac1-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="e5ac1-187">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors 資料表屬性][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="e5ac1-189">屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-189">Attribute</span></span> | <span data-ttu-id="e5ac1-190">類型</span><span class="sxs-lookup"><span data-stu-id="e5ac1-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e5ac1-191">id</span><span class="sxs-lookup"><span data-stu-id="e5ac1-191">id</span></span> |<span data-ttu-id="e5ac1-192">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-192">String</span></span> |
| <span data-ttu-id="e5ac1-193">operationId</span><span class="sxs-lookup"><span data-stu-id="e5ac1-193">operationId</span></span> |<span data-ttu-id="e5ac1-194">整數 64</span><span class="sxs-lookup"><span data-stu-id="e5ac1-194">Integer 64</span></span> |
| <span data-ttu-id="e5ac1-195">properties</span><span class="sxs-lookup"><span data-stu-id="e5ac1-195">properties</span></span> |<span data-ttu-id="e5ac1-196">二進位資料</span><span class="sxs-lookup"><span data-stu-id="e5ac1-196">Binary Data</span></span> |
| <span data-ttu-id="e5ac1-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="e5ac1-197">tableKind</span></span> |<span data-ttu-id="e5ac1-198">整數 16</span><span class="sxs-lookup"><span data-stu-id="e5ac1-198">Integer 16</span></span> |

 <span data-ttu-id="e5ac1-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="e5ac1-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="e5ac1-200">屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-200">Attribute</span></span> | <span data-ttu-id="e5ac1-201">類型</span><span class="sxs-lookup"><span data-stu-id="e5ac1-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e5ac1-202">id</span><span class="sxs-lookup"><span data-stu-id="e5ac1-202">id</span></span> |<span data-ttu-id="e5ac1-203">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-203">String</span></span> |
| <span data-ttu-id="e5ac1-204">索引鍵</span><span class="sxs-lookup"><span data-stu-id="e5ac1-204">key</span></span> |<span data-ttu-id="e5ac1-205">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-205">String</span></span> |
| <span data-ttu-id="e5ac1-206">keyType</span><span class="sxs-lookup"><span data-stu-id="e5ac1-206">keyType</span></span> |<span data-ttu-id="e5ac1-207">整數 64</span><span class="sxs-lookup"><span data-stu-id="e5ac1-207">Integer 64</span></span> |
| <span data-ttu-id="e5ac1-208">資料表</span><span class="sxs-lookup"><span data-stu-id="e5ac1-208">table</span></span> |<span data-ttu-id="e5ac1-209">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-209">String</span></span> |
| <span data-ttu-id="e5ac1-210">value</span><span class="sxs-lookup"><span data-stu-id="e5ac1-210">value</span></span> |<span data-ttu-id="e5ac1-211">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="e5ac1-212">資料表</span><span class="sxs-lookup"><span data-stu-id="e5ac1-212">Data table</span></span>

<span data-ttu-id="e5ac1-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="e5ac1-213">**TodoItem**</span></span>

| <span data-ttu-id="e5ac1-214">屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-214">Attribute</span></span> | <span data-ttu-id="e5ac1-215">類型</span><span class="sxs-lookup"><span data-stu-id="e5ac1-215">Type</span></span> | <span data-ttu-id="e5ac1-216">注意</span><span class="sxs-lookup"><span data-stu-id="e5ac1-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5ac1-217">id</span><span class="sxs-lookup"><span data-stu-id="e5ac1-217">id</span></span> | <span data-ttu-id="e5ac1-218">字串 (標示為必要)</span><span class="sxs-lookup"><span data-stu-id="e5ac1-218">String, marked required</span></span> |<span data-ttu-id="e5ac1-219">遠端存放區中的主索引鍵</span><span class="sxs-lookup"><span data-stu-id="e5ac1-219">Primary key in remote store</span></span> |
| <span data-ttu-id="e5ac1-220">完成</span><span class="sxs-lookup"><span data-stu-id="e5ac1-220">complete</span></span> | <span data-ttu-id="e5ac1-221">Boolean</span><span class="sxs-lookup"><span data-stu-id="e5ac1-221">Boolean</span></span> | <span data-ttu-id="e5ac1-222">To-do 項目欄位</span><span class="sxs-lookup"><span data-stu-id="e5ac1-222">To-do item field</span></span> |
| <span data-ttu-id="e5ac1-223">文字</span><span class="sxs-lookup"><span data-stu-id="e5ac1-223">text</span></span> |<span data-ttu-id="e5ac1-224">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-224">String</span></span> |<span data-ttu-id="e5ac1-225">To-do 項目欄位</span><span class="sxs-lookup"><span data-stu-id="e5ac1-225">To-do item field</span></span> |
| <span data-ttu-id="e5ac1-226">建立時間</span><span class="sxs-lookup"><span data-stu-id="e5ac1-226">createdAt</span></span> | <span data-ttu-id="e5ac1-227">日期</span><span class="sxs-lookup"><span data-stu-id="e5ac1-227">Date</span></span> | <span data-ttu-id="e5ac1-228">(選擇性) 對應至 **createdAt** 系統屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="e5ac1-229">更新時間</span><span class="sxs-lookup"><span data-stu-id="e5ac1-229">updatedAt</span></span> | <span data-ttu-id="e5ac1-230">日期</span><span class="sxs-lookup"><span data-stu-id="e5ac1-230">Date</span></span> | <span data-ttu-id="e5ac1-231">(選擇性) 對應至 **updatedAt** 系統屬性</span><span class="sxs-lookup"><span data-stu-id="e5ac1-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="e5ac1-232">版本</span><span class="sxs-lookup"><span data-stu-id="e5ac1-232">version</span></span> | <span data-ttu-id="e5ac1-233">String</span><span class="sxs-lookup"><span data-stu-id="e5ac1-233">String</span></span> | <span data-ttu-id="e5ac1-234">(選擇性) 用來偵測衝突，對應至版本</span><span class="sxs-lookup"><span data-stu-id="e5ac1-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="e5ac1-235"><a name="setup-sync"></a>變更應用程式的同步處理行為</span><span class="sxs-lookup"><span data-stu-id="e5ac1-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="e5ac1-236">在本節中，您將修改 App，使它在啟動或有使用者插入並更新項目時不會同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="e5ac1-237">只有在執行重新整理動作按鈕時，它才會同步。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="e5ac1-238">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-238">**Objective-C**:</span></span>

1. <span data-ttu-id="e5ac1-239">在 **QSTodoListViewController.m** 中，變更 **viewDidLoad** 方法以移除在方法結尾的 `[self refresh]` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="e5ac1-240">資料現在已經不會在 App 啟動時同步。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="e5ac1-241">反之，它是與本機存放區的內容同步。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="e5ac1-242">在 **QSTodoService.m** 中，修改 `addItem` 的定義，使其不會在插入項目後同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="e5ac1-243">移除 `self syncData` 區塊並以下列項目取代：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="e5ac1-244">如先前所述修改 `completeItem` 的定義。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="e5ac1-245">移除 `self syncData` 的區塊並以下列項目取代：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="e5ac1-246">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-246">**Swift**:</span></span>

<span data-ttu-id="e5ac1-247">在 **ToDoTableViewController.swift** 的 `viewDidLoad` 中，註解化這兩行以停止在 App 啟動時同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="e5ac1-248">在本文撰寫期間，當某人新增或完成項目時，Swift Todo App 不會更新服務。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="e5ac1-249">只有在 App 啟動時它才會更新。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="e5ac1-250"><a name="test-app"></a>測試應用程式</span><span class="sxs-lookup"><span data-stu-id="e5ac1-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="e5ac1-251">在本節中，您將連接至無效的 URL，以模擬離線情況。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="e5ac1-252">當您新增資料項目時，這些項目會存放在本機核心資料存放區，但不會同步到行動裝置 App 後端。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="e5ac1-253">將 **QSTodoService.m** 中的行動裝置 App URL 變更為無效的 URL，然後再次執行該 App：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="e5ac1-254">**Objective-C**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-254">**Objective-C**.</span></span> <span data-ttu-id="e5ac1-255">在 QSTodoService.m 中：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="e5ac1-256">**Swift**。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-256">**Swift**.</span></span> <span data-ttu-id="e5ac1-257">在 ToDoTableViewController.swift 中：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="e5ac1-258">新增一些 To-do 項目。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-258">Add some to-do items.</span></span> <span data-ttu-id="e5ac1-259">結束模擬器 (或強制關閉 App)，然後重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="e5ac1-260">確認已保存您的變更。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="e5ac1-261">檢視遠端 **TodoItem** 資料表的內容：</span><span class="sxs-lookup"><span data-stu-id="e5ac1-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="e5ac1-262">針對 Node.js 後端，請移至 [Azure 入口網站](https://portal.azure.com/)，在您的行動裝置 App 後端中按一下 [簡易表]  >  [TodoItem]。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="e5ac1-263">針對 .NET 後端，請使用 SQL 工具 (例如 SQL Server Management Studio) 或 REST 用戶端 (例如 Fiddler 或 Postman)。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="e5ac1-264">請確認新項目「尚未」同步處理到伺服器。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="e5ac1-265">請將 **QSTodoService.m** 中的 URL 變更回正確的 URL，然後重新執行 App。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="e5ac1-266">將項目清單往下拉，執行重新整理動作。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="e5ac1-267">會出現旋轉進度指示器。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="e5ac1-268">再次檢視 **TodoItem** 資料。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="e5ac1-269">其中會顯示已變更的新 To-do 項目。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="e5ac1-270">摘要</span><span class="sxs-lookup"><span data-stu-id="e5ac1-270">Summary</span></span>
<span data-ttu-id="e5ac1-271">為了支援離線同步處理功能，我們使用了 `MSSyncTable` 介面，並對本機存放區初始化 `MSClient.syncContext`。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="e5ac1-272">在此案例中，本機存放區是以核心資料為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="e5ac1-273">使用核心資料本機存放區時，您必須使用[正確的系統屬性](#review-core-data)定義數個資料表。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="e5ac1-274">針對行動裝置 App 的建立、讀取、更新及刪除 (CRUD) 等一般作業，會以 App 有如處於連線狀態之下執行，但所有的作業都是對本機存放區執行。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="e5ac1-275">我們使用 **MSSyncTable.pullWithQuery** 方法來同步處理本機存放區與伺服器。</span><span class="sxs-lookup"><span data-stu-id="e5ac1-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5ac1-276">其他資源</span><span class="sxs-lookup"><span data-stu-id="e5ac1-276">Additional resources</span></span>
* <span data-ttu-id="e5ac1-277">[Mobile Apps 中的離線資料同步處理]</span><span class="sxs-lookup"><span data-stu-id="e5ac1-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="e5ac1-278">[雲端報導：Azure Mobile Services 中的離線同步處理] \(雖然影片是關於 Mobile Services，但 Mobile Apps 也是以類似的方式進行離線同步處理。\)</span><span class="sxs-lookup"><span data-stu-id="e5ac1-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="e5ac1-279">[建立 iOS 應用程式]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="e5ac1-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="e5ac1-280">[Mobile Apps 中的離線資料同步處理]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="e5ac1-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="e5ac1-281">[雲端報導：Azure Mobile Services 中的離線同步處理]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="e5ac1-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
