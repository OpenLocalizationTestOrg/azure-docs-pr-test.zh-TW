---
title: "aaaEnable 離線同步處理針對通用 Windows 平台 (UWP) 應用程式與行動應用程式 |Microsoft 文件"
description: "深入了解如何 toouse Azure 行動應用程式 toocache 和同步處理離線資料在通用 Windows 平台 (UWP) 應用程式中。"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>啟用 Windows 應用程式離線同步處理
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何離線 tooadd 支援 tooa 通用 Windows 平台 (UWP) 應用程式使用 Azure 行動應用程式後端。 離線同步處理可讓終端使用者 toointeract 與行動裝置應用程式-檢視、 加入或修改資料集，即使在沒有網路連線。 變更會儲存在本機資料庫中。 Hello 裝置已上線，一旦這些變更同步處理與 hello 遠端後端中。

在本教學課程中，您可以更新 hello UWP 應用程式專案，從 hello 教學課程[建立 Windows 應用程式]toosupport hello 離線功能的 Azure 行動應用程式。 如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 資料存取擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。

## <a name="requirements"></a>需求
本教學課程需要 hello 下列先決條件：

* 執行於 Windows 8.1 或更新版本的 Visual Studio 2013。
* 完成 [建立 Windows 應用程式][建立 Windows 應用程式]。
* [Azure 行動服務 SQLite Store][sqlite store nuget]
* [適用於通用 Windows 平台開發的 SQLite](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>更新 hello 用戶端應用程式 toosupport 離線功能
Azure 行動裝置應用程式離線功能可讓您使用本機資料庫 toointeract 當您在離線案例中。 toouse 初始化應用程式中的這些功能， [SyncContext] [ synccontext] tooa 本機存放區。 然後在參考資料表透過 hello [IMobileServiceSyncTable][IMobileServiceSyncTable]介面。 SQLite 做為 hello hello 裝置上的本機存放區。

1. 安裝 hello [hello 通用 Windows 平台的 SQLite 執行階段](http://sqlite.org/2016/sqlite-uwp-3120200.vsix)。
2. 在 Visual Studio 中，開啟您在 hello 完成 hello UWP 應用程式專案 hello NuGet 封裝管理員[建立 Windows 應用程式]教學課程。
    搜尋及安裝 hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 封裝。
3. 在 [方案總管] 中，以滑鼠右鍵按一下 [參考] > [新增參考...]> [通用 Windows] >[擴充功能]，然後啟用 [適用於通用 Windows 平台的 SQLite] 和 [適用於通用 Windows 平台應用程式的 Visual C++ 2015 執行階段]。

    ![新增 SQLite UWP 參考][1]
4. 開啟 hello MainPage.xaml.cs 檔案，並取消註解 hello`#define OFFLINE_SYNC_ENABLED`定義。
5. 在 Visual Studio 中，按 hello **F5**金鑰 toorebuild 以及執行的 hello 用戶端應用程式。 hello 應用程式的運作方式相同，因為它並未啟用離線同步處理之前的 hello。不過，hello 本機資料庫現在填入可用在離線案例中的資料。

## <a name="update-sync"></a>更新 hello 應用程式 toodisconnect hello 後端
本節中，您可以中斷 hello 連接 tooyour 行動裝置應用程式後端 toosimulate 離線的情況。 當您將資料的項目時，您的例外狀況處理常式會告訴您該 hello 應用程式處於離線模式。 處於此狀態，在本機的 hello 中加入新項目儲存和 hello 行動裝置應用程式後端時發送接下來執行處於連線狀態會同步。

1. 編輯 App.xaml.cs hello 共用專案中。 註解的 hello hello 初始化**MobileServiceClient**並加入下列一行，也會使用無效的行動裝置應用程式 URL 的 hello:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    您也可以停用 wifi 和 hello 裝置上的行動電話通訊網路示範離線的行為，或使用飛航模式。
2. 按**F5** toobuild 和執行 hello 應用程式。 請注意當 hello 啟動應用程式無法在重新整理您同步處理。
3. 輸入新項目，並注意每次您按一下 **[儲存]** 時，推送都會失敗並具有 [CancelledByNetworkError] 狀態。 不過，hello todo 項目存在於 hello 本機存放區之前可以被推入 toohello 行動裝置應用程式後端。  在生產環境中應用程式，如果您隱藏 hello 用戶端應用程式的行為就如同它仍然是這些例外狀況會連接 toohello 行動裝置應用程式後端。
4. 關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。
5. (選擇性) 在 Visual Studio 中，開啟 [伺服器總管] 。 瀏覽 tooyour 資料庫**Azure**->**SQL 資料庫**。 在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。 現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。 請確認，hello 後端資料庫中的 hello 資料尚未變更。
6. （選擇性）使用 Fiddler 或郵差 tooquery 等其他工具行動後端，在表單中使用 GET 查詢`https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`。

## <a name="update-online-app"></a>更新您的行動裝置應用程式後端 hello 應用程式 tooreconnect
在本節中，您可以重新連線用 hello 應用程式 toohello 行動裝置應用程式後端。 這些變更模擬的網路重新連接上 hello 應用程式。

當您第一次執行 hello 應用程式時，hello`OnNavigatedTo`事件處理常式呼叫`InitLocalStoreAsync`。 這個方法會呼叫`SyncAsync`toosync hello 後端資料庫的本機存放區。 hello 應用程式會嘗試在啟動 toosync。

1. 開啟 App.xaml.cs hello 共用專案中，並取消註解您先前的初始化`MobileServiceClient`toouse hello 正確 hello 行動裝置應用程式 URL。
2. 按 hello **F5**金鑰 toorebuild 以及執行的 hello 應用程式。 hello 應用程式同步處理您的本機變更與 hello Azure 行動應用程式後端使用推送和提取作業時 hello`OnNavigatedTo`事件處理常式都會執行。
3. （選擇性）檢視 hello 更新的資料使用 SQL Server 物件總管 或 Fiddler 等其他工具。 請注意 hello 資料已同步處理 hello Azure 行動應用程式後端資料庫與 hello 本機存放區。
4. 在 hello 應用程式中，按一下 hello 核取方塊旁幾個項目 toocomplete 它們 hello 本機存放區中。

   `UpdateCheckedTodoItem`呼叫`SyncAsync`toosync 每個已完成與 hello 行動裝置應用程式後端的項目。 `SyncAsync` 會同時呼叫推送與提取。 不過，**每當您執行對資料表提取該 hello 用戶端所做的變更，一律自動執行推入**。 此行為可確保所有的資料表，以及關聯性的 hello 本機存放區中維持一致。 此行為可能會導致非預期的推送。  如需此行為的詳細資訊，請參閱 [Azure 行動應用程式中的離線資料同步]。

## <a name="api-summary"></a>API 摘要
toosupport hello 離線功能的行動服務，我們使用 hello [IMobileServiceSyncTable]介面，並初始化[MobileServiceClient.SyncContext] [ synccontext]與本機 SQLite 資料庫。 當離線，hello 行動應用程式的一般 CRUD 作業工作一樣 hello 作業發生 hello 本機存放區時，仍連線 hello 應用程式。 hello 下列方法是使用的 toosynchronize hello 本機存放區與 hello 伺服器：

* **[PushAsync]** 因為這個方法是隸屬[IMobileServicesSyncContext]，所有資料表的變更會推入 toohello 後端。 只有具有本機變更的記錄會傳送 toohello 伺服器。
* **[PullAsync]** 從 [IMobileServiceSyncTable] 開始提取。 當 hello 資料表中有追蹤的變更時，隱含的推入執行 toomake 確定所有的資料表，以及關聯性的 hello 本機存放區中維持一致。 hello *pushOtherTables*參數會控制是否在其他資料表 hello 內容中隱含的推播推送。 hello*查詢*參數接受[IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery]或 OData 查詢字串 toofilter hello 傳回的資料。 hello *queryId*參數用 toodefine 增量同步處理。如需詳細資訊，請參閱 [Azure Mobile Apps 中的離線資料同步處理](app-service-mobile-offline-data-sync.md#how-sync-works)。
* **[PurgeAsync]** 從 hello 本機存放區中應用程式應該定期呼叫這個方法 toopurge 過時資料。 使用 hello*強制*參數，當您需要 toopurge 尚未同步的任何變更。

如需這些概念的詳細資訊，請參閱 [Azure Mobile Apps 中的離線資料同步處理](app-service-mobile-offline-data-sync.md#how-sync-works)。

## <a name="more-info"></a>其他資訊
hello 下列主題提供的額外背景資訊的行動應用程式的 hello 離線同步處理功能：

* [Azure 行動應用程式中的離線資料同步]
* [Azure Mobile Apps .NET SDK HOWTO][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[Azure 行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md
[建立 Windows 應用程式]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
