---
title: "aaaEnable 離線同步處理您的 Azure 行動應用程式 (Xamarin iOS)"
description: "深入了解如何 toouse App Service 行動應用程式 toocache 和同步處理離線資料 Xamarin iOS 應用程式中"
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>啟用 Xamarin iOS 行動應用程式的離線同步處理
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>概觀
本教學課程介紹 Xamarin.iOS hello 離線的同步處理功能的 Azure 行動應用程式。 離線同步處理可讓終端使用者 toointeract 與行動裝置應用程式-檢視、 加入或修改資料--，即使在沒有網路連線。 變更會儲存在本機資料庫中。 Hello 裝置已上線，一旦這些變更會與 hello 遠端服務進行同步處理。

在本教學課程中，更新 hello Xamarin.iOS 應用程式專案，從[建立 Xamarin iOS 應用程式]toosupport hello 離線功能的 Azure 行動應用程式。 如果您不要使用 hello 下載快速入門的伺服器專案，您必須加入您的專案中的 hello 資料存取擴充功能封裝。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。

## <a name="update-hello-client-app-toosupport-offline-features"></a>更新 hello 用戶端應用程式 toosupport 離線功能
Azure 行動裝置應用程式離線功能可讓您使用本機資料庫 toointeract 當您在離線案例中。 toouse 這些功能的應用程式初始化[SyncContext] tooa 本機存放區。 參考資料表透過 hello [IMobileServiceSyncTable] 介面。 SQLite 做為 hello hello 裝置上的本機存放區。

1. 在您完成在 hello 的 hello 專案中開啟 hello NuGet 套件管理員[建立 Xamarin iOS 應用程式]教學課程中，然後再搜尋及安裝 hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet封裝。
2. 開啟 hello QSTodoService.cs 檔案，並取消註解 hello`#define OFFLINE_SYNC_ENABLED`定義。
3. 重新建置並執行 hello 用戶端應用程式。 hello 應用程式的運作方式相同，因為它並未啟用離線同步處理之前的 hello。不過，hello 本機資料庫現在填入可用在離線案例中的資料。

## <a name="update-sync"></a>更新 hello 應用程式 toodisconnect hello 後端
本節中，您可以中斷 hello 連接 tooyour 行動裝置應用程式後端 toosimulate 離線的情況。 當您將資料的項目時，您的例外狀況處理常式會告訴您該 hello 應用程式處於離線模式。 處於此狀態，在本機的 hello 中加入新項目儲存和 hello 行動裝置應用程式後端時發送接下來執行處於連線狀態會同步。

1. 編輯 QSToDoService.cs hello 共用專案中。 變更 hello **applicationURL** toopoint tooan URL 無效：

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    您也可以藉由停用 wifi 和 hello 裝置上的行動電話通訊網路，或使用飛航模式示範離線的行為。
2. 建置並執行 hello 應用程式。 請注意當 hello 啟動應用程式無法在重新整理您同步處理。
3. 輸入新項目，並注意每次您按一下 [儲存]  時，推送都會失敗並具有 [CancelledByNetworkError] 狀態。 不過，hello todo 項目存在於 hello 本機存放區之前可以被推入 toohello 行動裝置應用程式後端。  在生產環境中應用程式，如果您隱藏 hello 用戶端應用程式的行為就如同它仍然是這些例外狀況會連接 toohello 行動裝置應用程式後端。
4. 關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。
5. (選擇性) 如果您已在電腦上安裝 Visual Studio，請開啟 [伺服器總管]。 瀏覽 tooyour 資料庫**Azure**-> **SQL 資料庫**。 在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。 現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。 請確認，hello 後端資料庫中的 hello 資料尚未變更。
6. （選擇性）使用 Fiddler 或郵差 tooquery 等其他工具行動後端，在表單中使用 GET 查詢`https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`。

## <a name="update-online-app"></a>更新您的行動裝置應用程式後端 hello 應用程式 tooreconnect
在本節中，重新連線 hello 應用程式 toohello 行動裝置應用程式後端。 這會模擬 hello 移動從離線狀態 tooan 線上狀態與 hello 行動裝置應用程式後端的應用程式。   如果您關閉 網路連線來模擬 hello 網路遭破壞，則不需要變更任何程式碼。
Hello 網路再次開啟。  當您第一次執行 hello 應用程式時，hello`RefreshDataAsync`方法呼叫。 這會依次呼叫`SyncAsync`toosync hello 後端資料庫的本機存放區。

1. 在 hello 共用專案中，開啟 QSToDoService.cs 並還原您的變更 hello **applicationURL**屬性。
2. 重新建置並執行 hello 應用程式。 hello 應用程式同步處理您的本機變更與 hello Azure 行動應用程式後端使用推送和提取作業時 hello`OnRefreshItemsSelected`方法執行。
3. （選擇性）檢視 hello 更新的資料使用 SQL Server 物件總管 或 Fiddler 等其他工具。 請注意 hello 資料已同步處理 hello Azure 行動應用程式後端資料庫與 hello 本機存放區。
4. 在 hello 應用程式中，按一下 hello 核取方塊旁幾個項目 toocomplete 它們 hello 本機存放區中。

   `CompleteItemAsync`呼叫`SyncAsync`toosync 每個已完成與 hello 行動裝置應用程式後端的項目。 `SyncAsync` 會同時呼叫推送與提取。
   **每當您執行對資料表提取該 hello 用戶端所做的變更，hello 用戶端同步處理內容上的推入會永遠執行第一次自動**。 hello 隱含發送可確保所有的資料表，以及關聯性的 hello 本機存放區中維持一致。 如需此行為的詳細資訊，請參閱 [Azure 行動應用程式中的離線資料同步]。

## <a name="review-hello-client-sync-code"></a>檢閱 hello 用戶端同步程式碼
當您完成 hello 教學課程，您下載的 hello Xamarin 用戶端專案[建立 Xamarin iOS 應用程式]已經包含支援使用本機 SQLite 資料庫離線同步處理的程式碼。 以下是在 hello 教學課程的程式碼中已包含內容的簡短概觀。 Hello 功能的概念性概觀，請參閱[Azure 行動應用程式中的離線資料同步]。

* 在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。 hello 本機存放區資料庫已初始化時`QSTodoListViewController.ViewDidLoad()`執行`QSTodoService.InitializeStoreAsync()`。 這個方法會建立新的本機 SQLite 資料庫使用 hello `MobileServiceSQLiteStore` hello Azure 行動應用程式用戶端 SDK 所提供的類別。

    hello`DefineTable`方法符合提供的 hello 類型中的 hello 欄位的 hello 本機存放區中建立資料表`ToDoItem`在此情況下。 hello 類型沒有 tooinclude hello 遠端資料庫中的所有 hello 資料行。 很可能 toostore 只要資料行的子集。

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* hello`todoTable`隸屬`QSTodoService`的 hello`IMobileServiceSyncTable`型別而非`IMobileServiceTable`。 hello IMobileServiceSyncTable 指示所有建立、 讀取、 更新和刪除 (CRUD) 資料表作業 toohello 本機存放區資料庫。

    您可以決定當這些變更會藉由呼叫推送 toohello Azure 行動應用程式後端`IMobileServiceSyncContext.PushAsync()`。 hello 同步處理內容可以藉由追蹤，並將變更推入用戶端應用程式有修改時的所有資料表中保留資料表關聯性`PushAsync`呼叫。

    hello 提供程式碼會呼叫`QSTodoService.SyncAsync()`toosync 每當 hello todoitem 清單重新整理或加入或已完成的 todoitem。 每次本機變更之後，應用程式會同步處理。 如果提取 hello 內容的執行對已暫止的本機更新追蹤的資料表，該提取作業自動將會先觸發內容推入。

    Hello 提供程式碼中，所有的記錄中遠端 hello`TodoItem`查詢資料表，但也可能 toofilter 記錄藉由傳遞查詢識別碼和查詢太`PushAsync`。 如需詳細資訊，請參閱 hello 節*增量同步處理*中[Azure 行動應用程式中的離線資料同步]。

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>其他資源
* [Azure 行動應用程式中的離線資料同步]
* [Azure Mobile Apps .NET SDK HOWTO][8]

<!-- Images -->

<!-- URLs. -->
[建立 Xamarin iOS 應用程式]: app-service-mobile-xamarin-ios-get-started.md
[Azure 行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
