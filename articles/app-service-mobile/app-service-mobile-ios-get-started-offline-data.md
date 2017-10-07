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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>啟用 iOS Mobile Apps 的離線同步處理
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>概觀
本教學課程涵蓋與 hello 行動應用程式功能的 Azure App Service 適用於 iOS 的離線同步處理。 使用離線同步處理的使用者可以與行動裝置應用程式 tooview 互動中、 新增或修改資料，即使它們有沒有網路連線。 變更會儲存在本機資料庫中。 Hello 裝置恢復連線後，同步處理 hello 變更 hello 遠端的後端。

如果這是您首次經驗與行動應用程式，您應該先完成 hello 教學課程[建立 iOS 應用程式]。 如果您不使用下載的 hello 伺服器快速入門專案，您必須加入 hello 資料存取擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

toolearn 進一步了解 hello 離線同步處理功能，請參閱[行動應用程式中的離線資料同步]。

## <a name="review-sync"></a>檢閱 hello 用戶端同步程式碼
您下載的 hello hello 用戶端專案[建立 iOS 應用程式]教學課程已包含可支援使用本機的核心資料為基礎資料庫的離線同步處理的程式碼。 本節摘要說明在 hello 教學課程的程式碼中已包含內容。 Hello 功能的概念性概觀，請參閱[行動應用程式中的離線資料同步]。

使用行動應用程式的 hello 離線的資料同步處理功能，使用者可以互動本機資料庫即使 hello 網路是無法存取。 toouse 初始化 hello 同步處理內容的應用程式中的這些功能，`MSClient`和參考本機存放區。 然後參考資料表透過 hello **MSSyncTable**介面。

在**QSTodoService.m** (OBJECTIVE-C) 或**ToDoTableViewController.swift** hello hello 成員型別 (Swift)，請注意**syncTable**是**MSSyncTable**。 離線同步處理會使用此同步處理資料表介面，而不是 **MSTable**。 使用同步處理資料表時，所有作業移 toohello 本機存放區只能與 hello 遠端端與明確的推入進行同步處理和提取作業。

 tooget 參考 tooa 同步處理資料表，使用 hello **syncTableWithName**方法`MSClient`。 tooremove 離線同步處理功能、 使用**tableWithName**改為。

在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。 Hello 相關程式碼如下：

* **Objective-C**。 在 hello **QSTodoService.init**方法：

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**。 在 hello **ToDoTableViewController.viewDidLoad**方法：

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   這個方法會建立本機存放區使用 hello `MSCoreDataStore` hello 行動應用程式 SDK 的介面提供。 或者，您可以提供不同的本機存放區，藉由實作 hello`MSSyncContextDataSource`通訊協定。 此外，hello 的第一個參數**MSSyncContext**是使用的 toospecify 衝突處理常式。 因為我們傳遞`nil`，我們取得 hello 預設衝突處理常式，在任何衝突時失敗。

現在，讓我們執行 hello 實際的同步處理作業，並從 hello 遠端的後端取得資料：

* **Objective-C**。 `syncData`第一次將新的變更推入，然後呼叫**pullData** tooget hello 遠端的後端的資料。 接著，hello **pullData**方法會取得新的資料與查詢相符：

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
* **Swift**：
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

在 hello Objective C 版本中，在`syncData`，我們先呼叫**pushWithCompletion** hello 同步處理內容上。 這個方法是屬於`MSSyncContext`（而不 hello 同步處理資料表本身） 因為跨所有資料表發送變更。 已修改以某種方式在本機 （透過 CUD 作業） 的記錄傳送 toohello 伺服器。 然後 hello helper **pullData**呼叫，而它會呼叫**MSSyncTable.pullWithQuery** tooretrieve 遠端資料並將它儲存在 hello 本機資料庫。

在 hello Swift 版本中，hello 推入作業不是絕對必要，因為沒有呼叫太**pushWithCompletion**。 如果正在進行推入作業的 hello 資料表的 hello 同步內容中沒有任何暫止的變更，提取永遠會發出推入第一次。 不過，如果您有一個以上的同步處理資料表時，它是所有設定都一致跨相關資料表最佳的 tooexplicitly 呼叫發送 tooensure。

在 hello Objective C 和 Swift 的版本中，您可以使用 hello **pullWithQuery**方法 toospecify 查詢 toofilter hello 想 tooretrieve 記錄。 在此範例中，hello 查詢會擷取所有記錄遠端 hello`TodoItem`資料表。

hello 第二個參數**pullWithQuery**是用於查詢識別碼*增量同步處理*。增量同步處理擷取自 hello 上次同步處理，使用 hello 記錄已修改的記錄`UpdatedAt`時間戳記 (稱為`updatedAt`hello 本機存放區中。) 應該對每個邏輯的查詢中是唯一的描述性字串 hello 查詢識別碼。您的應用程式。 tooopt 未增量同步，傳遞`nil`如 hello 的查詢識別碼。 此方法可能效率不佳，因為它會在每次提取作業擷取所有記錄。

當您修改或加入的資料，當使用者執行 hello 重新整理鍵筆勢，而且在啟動 hello Objective C 應用程式同步處理。

hello Swift 應用程式進行同步時 hello 使用者執行 hello 重新整理筆勢和啟動。

Hello 應用程式同步處理資料時修改 (OBJECTIVE-C)，或是每當 hello 應用程式啟動時 （Objective C 和 Swift），hello 應用程式會假設該 hello 使用者在線上。 在更新版本的區段中，您將更新 hello 應用程式，讓使用者可以編輯，即使它們是離線。

## <a name="review-core-data"></a>檢閱 hello 核心資料模型
當您使用 hello 的核心資料離線存放區時，您必須定義資料模型中的特定資料表和欄位。 hello 範例應用程式已經包含資料模型與 hello 正確的格式。 在本節中，我們逐步進行這些資料表 tooshow 的使用方式。

開啟 **QSDataModel.xcdatamodeld**。 四個資料表所使用的三個定義-hello SDK 和一個用於 hello 待辦項目本身：
  * MS_TableOperations： 曲目 hello 需要 toobe 與 hello 伺服器同步處理的項目。
  * MS_TableOperationErrors：追蹤在離線同步處理期間發生的任何錯誤。
  * MS_TableConfig： 曲目 hello hello 上次同步處理作業的所有提取作業的上次更新時間。
  * TodoItem： 儲存 hello 待辦項目。 hello 系統資料行**createdAt**， **updatedAt**，和**版本**是選用的系統屬性。

> [!NOTE]
> hello 行動應用程式 SDK 保留開頭的資料行名稱"**``**"。 請不要將此前置詞用於系統資料行以外的項目。 否則，當您使用 hello 遠端的後端時，會修改資料行名稱。
>
>

當您使用 hello 離線同步處理功能時，定義三個系統資料表 hello 和 hello 資料表。

### <a name="system-tables"></a>系統資料表

**MS_TableOperations**  

![MS_TableOperations 資料表屬性][defining-core-data-tableoperations-entity]

| 屬性 | 類型 |
| --- | --- |
| id | 整數 64 |
| itemId | String |
| properties | 二進位資料 |
| 資料表 | String |
| tableKind | 整數 16 |


**MS_TableOperationErrors**

 ![MS_TableOperationErrors 資料表屬性][defining-core-data-tableoperationerrors-entity]

| 屬性 | 類型 |
| --- | --- |
| id |String |
| operationId |整數 64 |
| properties |二進位資料 |
| tableKind |整數 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| 屬性 | 類型 |
| --- | --- |
| id |String |
| 索引鍵 |String |
| keyType |整數 64 |
| 資料表 |String |
| value |String |

### <a name="data-table"></a>資料表

**TodoItem**

| 屬性 | 類型 | 注意 |
| --- | --- | --- |
| id | 字串 (標示為必要) |遠端存放區中的主索引鍵 |
| 完成 | Boolean | To-do 項目欄位 |
| 文字 |String |To-do 項目欄位 |
| 建立時間 | Date | （選擇性）對應太**createdAt**系統屬性 |
| 更新時間 | Date | （選擇性）對應太**updatedAt**系統屬性 |
| 版本 | String | （選擇性）使用的 toodetect 衝突，對應 tooversion |

## <a name="setup-sync"></a>Hello hello 應用程式同步行為變更
本節中，您會修改 hello 應用程式，使它不會同步啟動應用程式，或當您插入和更新項目上。 其會同步執行 hello 重新整理手勢按鈕時，才。

**Objective-C**：

1. 在**QSTodoListViewController.m**，變更 hello **viewDidLoad**方法 tooremove 太 hello 呼叫`[self refresh]`hello hello 方法結尾。 現在 hello 資料未與 hello 伺服器上啟動應用程式同步處理。 相反地，它會與 hello hello 本機存放區內容同步。
2. 在**QSTodoService.m**，修改 hello 定義`addItem`，讓它在 hello 項目插入後不會同步處理。 移除 hello`self syncData`封鎖，並取代為下列 hello:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. 修改 hello 定義`completeItem`如先前所述。 移除 hello 區塊`self syncData`並取代為下列 hello:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**：

在`viewDidLoad`，請在**ToDoTableViewController.swift**，這裡顯示，toostop 上啟動應用程式同步處理 hello 兩行程式碼的註解。 Hello Swift 待辦事項應用程式在 hello 撰寫本文時，它不會更新 hello 服務新增或完成項目。 它會更新 hello 服務只在啟動應用程式。

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>測試 hello 應用程式
本節中，您可以連接無效 URL toosimulate tooan 離線的案例。 當您將資料的項目時，它們保留在 hello 本機的核心資料存放區，但它們未同步處理 hello 行動裝置應用程式後端。

1. 變更中的 hello 行動裝置應用程式 URL **QSTodoService.m** tooan 無效的 URL，然後再次執行的 hello 應用程式：

   **Objective-C**。 在 QSTodoService.m 中：
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**。 在 ToDoTableViewController.swift 中：
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. 新增一些 To-do 項目。 結束模擬器 hello （或強制關閉 hello 應用程式），然後重新啟動。 確認已保存您的變更。

3. 檢視遠端 hello hello 內容**TodoItem**資料表：
   * Node.js 的後端，請移 toohello [Azure 入口網站](https://portal.azure.com/)，然後在您行動裝置應用程式後端中，按一下**簡單資料表** > **TodoItem**。  
   * 針對 .NET 後端，請使用 SQL 工具 (例如 SQL Server Management Studio) 或 REST 用戶端 (例如 Fiddler 或 Postman)。  

4. 請確認 hello 新項目有*不*已與 hello 伺服器進行同步處理。

5. 變更 hello URL 後 toohello 更正其中中**QSTodoService.m**，並重新執行的 hello 應用程式。

6. Hello 清單中的項目，藉以執行 hello 重新整理筆勢。  
會出現旋轉進度指示器。

7. 檢視 hello **TodoItem**資料一次。 現在應該顯示 hello 新增和變更待辦項目。

## <a name="summary"></a>摘要
toosupport hello 離線同步處理功能，我們使用 hello`MSSyncTable`介面，並初始化`MSClient.syncContext`與本機存放區。 在此情況下，hello 本機存放區當時在核心資料為基礎的資料庫。

當您使用的核心資料本機存放區時，您必須定義數個資料表以 hello[更正系統屬性](#review-core-data)。

hello 一般建立、 讀取、 更新和刪除 (CRUD) 作業的行動應用程式可視為 hello 應用程式仍然連接，但所有 hello 作業都發生 hello 本機存放區。

當我們與 hello 伺服器同步 hello 本機存放區時，我們使用 hello **MSSyncTable.pullWithQuery**方法。

## <a name="additional-resources"></a>其他資源
* [行動應用程式中的離線資料同步]
* [雲端涵蓋： Azure Mobile Services 中的離線同步] \(hello 視訊是關於行動服務，但行動應用程式離線同步運作方式類似。\)

<!-- URLs. -->


[建立 iOS 應用程式]: app-service-mobile-ios-get-started.md
[行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[雲端涵蓋： Azure Mobile Services 中的離線同步]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
