---
title: "aaaEnable 離線同步處理您的 Azure 行動應用程式 (Xamarin.Forms) |Microsoft 文件"
description: "深入了解如何 toouse App Service 行動應用程式 toocache 和同步處理離線資料 Xamarin.Forms 應用程式中"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>啟用 Xamarin.Forms 行動應用程式的離線同步處理
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>概觀
本教學課程介紹 Xamarin.Forms hello 離線的同步處理功能的 Azure 行動應用程式。 離線同步處理可讓使用者與行動應用程式進行互動--檢視、新增或修改資料--即使沒有網路連線進也可行。 變更會儲存在本機資料庫中。 Hello 裝置已上線，一旦這些變更會與 hello 遠端服務進行同步處理。

本教學課程根據當您完成本教學課程 [建立 Xamarin iOS 應用程式] 時，您建立的行動應用程式 hello Xamarin.Forms 快速入門方案。 Xamarin.Forms hello 快速入門解決方案包含 hello 程式碼 toosupport 離線同步處理，這只需要啟用 toobe。 在本教學課程中，您可以更新 hello 快速入門方案 tooturn hello 離線功能的 Azure 行動應用程式。 我們也反白 hello 應用程式中的 hello 離線特定程式碼。 如果您不使用下載的 hello 快速入門方案，您必須加入 hello 資料存取擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][1]。

toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步][2]。

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>啟用 hello 快速入門方案中的離線同步處理功能
hello 離線同步程式碼併入 hello 專案中，使用 C# 前置處理器指示詞。 當 hello**離線\_同步\_啟用**符號已定義，這些程式碼路徑都會納入 hello 組建。 針對 Windows 應用程式，您也必須安裝 hello SQLite 平台。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello 方案 >**管理方案的 NuGet 套件...**，然後尋找並安裝**Microsoft.Azure.Mobile.Client.SQLiteStore** hello 方案中的所有專案的 NuGet 封裝。
2. 在 [hello 方案總管] 中，開啟 hello TodoItemManager.cs 檔案來自 hello 專案，**可攜式**在 hello 名稱，亦即可攜式類別庫專案，然後取消註解 hello 前置處理器指示詞後面：

        #define OFFLINE_SYNC_ENABLED
3. （選擇性） toosupport Windows 裝置，安裝其中一個 hello 遵循 SQLite 執行階段封裝：

   * **Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。
   * **Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。
   * **通用 Windows 平台**安裝[SQLite 對通用 Windows 通用 hello][5]。

     雖然 hello 快速入門未包含通用 Windows 專案，hello 通用 Windows 平台支援使用 Xamarin Forms。
4. （選擇性）在每個 Windows 應用程式專案中，以滑鼠右鍵按一下**參考** > **加入參考...**，依序展開 hello **Windows**資料夾 >**延伸**。
    啟用適當的 hello **SQLite 適用於 Windows 的**SDK 以及 hello **Visual c + + 2013 Runtime for Windows** SDK。
    hello SQLite SDK 的名稱會稍微不同的每個 Windows 平台。

## <a name="review-hello-client-sync-code"></a>檢閱 hello 用戶端同步程式碼
以下是 內部 hello hello 教學課程的程式碼中已包含內容的簡短概觀`#if OFFLINE_SYNC_ENABLED`指示詞。 離線同步處理功能是 hello 可攜式類別庫專案中的 hello TodoItemManager.cs 專案檔案中。 Hello 功能的概念性概觀，請參閱[離線 Azure 行動應用程式中的資料同步處理][2]。

* 在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。 hello 本機存放區資料庫已初始化在 hello **TodoItemManager**類別建構函式使用下列程式碼的 hello:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    此程式碼會建立新的本機 SQLite 資料庫使用 hello **MobileServiceSQLiteStore**類別。

    hello **DefineTable**方法符合提供的 hello 類型中的 hello 欄位的 hello 本機存放區中建立資料表。  hello 類型沒有 tooinclude hello 遠端資料庫中的所有 hello 資料行。 很可能 toostore 資料行的子集。
* hello **todoTable**欄位**TodoItemManager**是**IMobileServiceSyncTable**型別而非**IMobileServiceTable**。 此類別會使用 hello 本機資料庫所有建立、 讀取、 更新和刪除 (CRUD) 資料表的作業。 您可以決定當這些變更會藉由呼叫推送 toohello 行動裝置應用程式後端**PushAsync**上 hello **IMobileServiceSyncContext**。 hello 同步處理內容可以藉由追蹤，並將變更推入用戶端應用程式有修改時的所有資料表中保留資料表關聯性**PushAsync**呼叫。

    hello 下列**SyncAsync**呼叫 toosync 與 hello 行動裝置應用程式後端的方法：

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    這個範例會使用簡單的錯誤處理與 hello 預設同步處理常式。 實際的應用程式會處理使用自訂衝突的各種錯誤，例如網路狀況和伺服器 hello **IMobileServiceSyncHandler**實作。

## <a name="offline-sync-considerations"></a>離線同步處理考量
在 hello 範例 hello **SyncAsync**方法只會在啟動和同步處理要求時呼叫。  tooinitiate Android 或 iOS 應用程式中，提取 hello 項目清單; 上的同步處理適用於 Windows、 使用 hello**同步** 按鈕。 在真實世界應用程式中，您也可以讓 hello 同步處理觸發程序 hello 網路狀態變更時。

提取針對有暫止的資料表執行本機更新追蹤先前的內容推播 hello 內容，提取作業會自動觸發程序。 當重新整理、 新增和完成項目在此範例中，您可以省略 hello 明確**PushAsync**呼叫。

Hello 提供程式碼中，查詢 hello 遠端 TodoItem 資料表中的所有記錄，但也可能 toofilter 記錄藉由傳遞查詢識別碼和查詢太**PushAsync**。 如需詳細資訊，請參閱 hello 節*增量同步處理*中[離線 Azure 行動應用程式中的資料同步處理][2]。

## <a name="run-hello-client-app"></a>執行 hello 用戶端應用程式
現在已啟用離線同步時，執行 hello 用戶端應用程式每個平台 toopopulate hello 本機存放區資料庫的至少一次。 更新版本中，模擬離線案例中，並修改 hello 本機存放區中的 hello 資料 hello 應用程式處於離線狀態。

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>更新 hello hello 用戶端應用程式同步處理行為
在本節中，修改 hello 用戶端專案 toosimulate 離線案例中為您的後端使用無效的應用程式 URL。 或者，您可以關閉網路連線太移動您的裝置 「 飛航模式 」。  當您新增或變更資料的項目時，這些變更會 hello 本機存放區中保留，但未同步處理 toohello 後端資料存放區，直到 hello 連接重新建立。

1. 在 [hello 方案總管] 中，開啟 hello Constants.cs 專案檔從 hello**可攜式**專案，並變更 hello 值`ApplicationURL`toopoint tooan URL 無效：

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. 開啟 hello TodoItemManager.cs 檔案從 hello**可攜式**專案，然後新增**攔截**hello 基底**例外狀況**類別 toohello **try … catch**中區塊**SyncAsync**。 這**攔截**區塊寫入 hello 例外狀況訊息 toohello 主控台，如下所示：

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. 建置並執行 hello 用戶端應用程式。  新增一些新項目。 請注意例外狀況會記錄在 hello 與 hello 後端的每個嘗試 toosync 主控台。 這些新的項目存在於 hello 本機存放區，直到它們可以推送 toohello 行動後端。 hello 用戶端應用程式行為就如同它是連接的 toohello 後端、 支援所有建立、 讀取、 更新、 刪除 (CRUD) 作業。
4. 關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。
5. （選擇性）使用 Visual Studio tooview hello 後端資料庫中的 hello 資料尚未變更您 Azure SQL Database 資料表 toosee。

    在 Visual Studio 中，開啟 [伺服器總管] 。 瀏覽 tooyour 資料庫**Azure**->**SQL 資料庫**。 在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。 現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>更新 hello 用戶端應用程式 tooreconnect 行動後端
在本節中，重新連線 hello 應用程式 toohello 行動後端，這將模擬 hello 光顧 tooan 線上狀態的應用程式。 當您執行 hello 重新整理鍵筆勢時，資料會是已同步的 tooyour 行動後端。

1. 重新開啟 Constants.cs。 正確的 hello `applicationURL` toopoint toohello 更正 URL。
2. 重新建置並執行 hello 用戶端應用程式。 hello 與 hello 行動裝置應用程式後端應用程式嘗試 toosync 之後啟動。 請確認在 hello 偵錯主控台也會記錄任何例外狀況。
3. （選擇性）使用 SQL Server 物件總管 或 Fiddler 等其他工具的資料更新時檢視 hello 或[郵差][6]。 請注意 hello 資料已同步處理 hello 後端資料庫與 hello 本機存放區。

    請注意 hello 資料已同步處理 hello 資料庫與 hello 本機存放區，並包含您加入您的應用程式已中斷連接時的 hello 項目。

## <a name="additional-resources"></a>其他資源
* [Azure Mobile Apps 中的離線資料同步處理][2]
* [Azure Mobile Apps .NET SDK HOWTO][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
