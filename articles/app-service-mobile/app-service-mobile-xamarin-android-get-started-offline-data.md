---
title: "aaaEnable 離線同步處理您的 Azure 行動應用程式 (Xamarin Android)"
description: "深入了解如何 toouse App Service 行動應用程式 toocache 和同步處理離線資料 Xamarin Android 應用程式中"
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a><span data-ttu-id="1d54c-103">啟用您 Xamarin.Android 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="1d54c-103">Enable offline sync for your Xamarin.Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="1d54c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1d54c-104">Overview</span></span>
<span data-ttu-id="1d54c-105">本教學課程介紹 Xamarin.Android hello 離線的同步處理功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Android.</span></span> <span data-ttu-id="1d54c-106">離線同步處理可讓終端使用者 toointeract 與行動裝置應用程式-檢視、 加入或修改資料--，即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="1d54c-106">Offline sync allows end users toointeract with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="1d54c-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="1d54c-107">Changes are stored in a local database.</span></span>
<span data-ttu-id="1d54c-108">Hello 裝置已上線，一旦這些變更會與 hello 遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d54c-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="1d54c-109">在本教學課程中，您可以更新 hello 用戶端 hello 教學課程專案[建立 Xamarin Android 應用程式]toosupport hello 離線功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-109">In this tutorial, you update hello client project from hello tutorial [Create a Xamarin Android app] toosupport hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="1d54c-110">如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 資料存取擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="1d54c-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="1d54c-111">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="1d54c-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="1d54c-112">toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="1d54c-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-client-app-toosupport-offline-features"></a><span data-ttu-id="1d54c-113">更新 hello 用戶端應用程式 toosupport 離線功能</span><span class="sxs-lookup"><span data-stu-id="1d54c-113">Update hello client app toosupport offline features</span></span>
<span data-ttu-id="1d54c-114">Azure 行動裝置應用程式離線功能可讓您使用本機資料庫 toointeract 當您在離線案例中。</span><span class="sxs-lookup"><span data-stu-id="1d54c-114">Azure Mobile App offline features allow you toointeract with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="1d54c-115">toouse 初始化應用程式中的這些功能， [SyncContext] tooa 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-115">toouse these features in your app, you initialize a [SyncContext] tooa local store.</span></span> <span data-ttu-id="1d54c-116">然後在參考資料表透過 hello [IMobileServiceSyncTable] [IMobileServiceSyncTable] 介面。</span><span class="sxs-lookup"><span data-stu-id="1d54c-116">Then reference your table through hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="1d54c-117">SQLite 做為 hello hello 裝置上的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-117">SQLite is used as hello local store on hello device.</span></span>

1. <span data-ttu-id="1d54c-118">在 Visual Studio 中，開啟您在 hello 完成 hello 專案中的 hello NuGet 套件管理員[建立 Xamarin Android 應用程式]教學課程。</span><span class="sxs-lookup"><span data-stu-id="1d54c-118">In Visual Studio, open hello NuGet package manager in hello project that you completed in hello [Create a Xamarin Android app] tutorial.</span></span>  <span data-ttu-id="1d54c-119">搜尋及安裝 hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1d54c-119">Search for and install hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="1d54c-120">開啟 hello ToDoActivity.cs 檔案，並取消註解 hello`#define OFFLINE_SYNC_ENABLED`定義。</span><span class="sxs-lookup"><span data-stu-id="1d54c-120">Open hello ToDoActivity.cs file and uncomment hello `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="1d54c-121">在 Visual Studio 中，按 hello **F5**金鑰 toorebuild 以及執行的 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-121">In Visual Studio, press hello **F5** key toorebuild and run hello client app.</span></span> <span data-ttu-id="1d54c-122">hello 應用程式的運作方式相同，因為它並未啟用離線同步處理之前的 hello。不過，hello 本機資料庫現在填入可用在離線案例中的資料。</span><span class="sxs-lookup"><span data-stu-id="1d54c-122">hello app works hello same as it did before you enabled offline sync. However, hello local database is now populated with data that can be used in an offline scenario.</span></span>

## <span data-ttu-id="1d54c-123"><a name="update-sync"></a>更新 hello 應用程式 toodisconnect hello 後端</span><span class="sxs-lookup"><span data-stu-id="1d54c-123"><a name="update-sync"></a>Update hello app toodisconnect from hello backend</span></span>
<span data-ttu-id="1d54c-124">本節中，您可以中斷 hello 連接 tooyour 行動裝置應用程式後端 toosimulate 離線的情況。</span><span class="sxs-lookup"><span data-stu-id="1d54c-124">In this section, you break hello connection tooyour Mobile App backend toosimulate an offline situation.</span></span> <span data-ttu-id="1d54c-125">當您將資料的項目時，您的例外狀況處理常式會告訴您該 hello 應用程式處於離線模式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-125">When you add data items, your exception handler tells you that hello app is in offline mode.</span></span> <span data-ttu-id="1d54c-126">處於此狀態，在本機的 hello 中加入新項目儲存和推入執行處於連線狀態時同步處理至 hello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1d54c-126">In this state, new items added in hello local store and are synced to hello mobile app backend when a push is executed in a connected state.</span></span>

1. <span data-ttu-id="1d54c-127">編輯 ToDoActivity.cs hello 共用專案中。</span><span class="sxs-lookup"><span data-stu-id="1d54c-127">Edit ToDoActivity.cs in hello shared project.</span></span> <span data-ttu-id="1d54c-128">變更 hello **applicationURL** toopoint tooan URL 無效：</span><span class="sxs-lookup"><span data-stu-id="1d54c-128">Change hello **applicationURL** toopoint tooan invalid URL:</span></span>

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    <span data-ttu-id="1d54c-129">您也可以藉由停用 wifi 和 hello 裝置上的行動電話通訊網路，或使用飛航模式示範離線的行為。</span><span class="sxs-lookup"><span data-stu-id="1d54c-129">You can also demonstrate offline behavior by disabling wifi and cellular networks on hello device or using airplane mode.</span></span>
2. <span data-ttu-id="1d54c-130">按**F5** toobuild 和執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-130">Press **F5** toobuild and run hello app.</span></span> <span data-ttu-id="1d54c-131">請注意當 hello 啟動應用程式無法在重新整理您同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d54c-131">Notice your sync failed on refresh when hello app launched.</span></span>
3. <span data-ttu-id="1d54c-132">輸入新項目，並注意每次您按一下 [儲存]  時，推送都會失敗並具有 [CancelledByNetworkError] 狀態。</span><span class="sxs-lookup"><span data-stu-id="1d54c-132">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="1d54c-133">不過，hello todo 項目存在於 hello 本機存放區之前可以被推入 toohello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1d54c-133">However, hello new todo items exist in hello local store until they can be pushed toohello mobile app backend.</span></span>  <span data-ttu-id="1d54c-134">在生產環境中應用程式，如果您隱藏 hello 用戶端應用程式的行為就如同它仍然是這些例外狀況會連接 toohello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1d54c-134">In a production app, if you suppress these exceptions hello client app behaves as if it's still connected toohello mobile app backend.</span></span>
4. <span data-ttu-id="1d54c-135">關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-135">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="1d54c-136">(選擇性) 在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="1d54c-136">(Optional) In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="1d54c-137">瀏覽 tooyour 資料庫**Azure**->**SQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="1d54c-137">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="1d54c-138">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="1d54c-138">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="1d54c-139">現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="1d54c-139">Now you can browse tooyour SQL database table and its contents.</span></span> <span data-ttu-id="1d54c-140">請確認，hello 後端資料庫中的 hello 資料尚未變更。</span><span class="sxs-lookup"><span data-stu-id="1d54c-140">Verify that hello data in hello backend database has not changed.</span></span>
6. <span data-ttu-id="1d54c-141">（選擇性）使用 Fiddler 或郵差 tooquery 等其他工具行動後端，在表單中使用 GET 查詢`https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-141">(Optional) Use a REST tool such as Fiddler or Postman tooquery your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <span data-ttu-id="1d54c-142"><a name="update-online-app"></a>更新您的行動裝置應用程式後端 hello 應用程式 tooreconnect</span><span class="sxs-lookup"><span data-stu-id="1d54c-142"><a name="update-online-app"></a>Update hello app tooreconnect your Mobile App backend</span></span>
<span data-ttu-id="1d54c-143">在本節中，重新連線 hello 應用程式 toohello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1d54c-143">In this section, reconnect hello app toohello mobile app backend.</span></span> <span data-ttu-id="1d54c-144">當您第一次執行 hello 應用程式時，hello`OnCreate`事件處理常式呼叫`OnRefreshItemsSelected`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-144">When you first run hello application, hello `OnCreate` event handler calls `OnRefreshItemsSelected`.</span></span> <span data-ttu-id="1d54c-145">這個方法會呼叫`SyncAsync`toosync hello 後端資料庫的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-145">This method calls `SyncAsync` toosync your local store with hello backend database.</span></span>

1. <span data-ttu-id="1d54c-146">在 hello 共用專案中，開啟 ToDoActivity.cs 並還原您的變更 hello **applicationURL**屬性。</span><span class="sxs-lookup"><span data-stu-id="1d54c-146">Open ToDoActivity.cs in hello shared project, and revert your change of hello **applicationURL** property.</span></span>
2. <span data-ttu-id="1d54c-147">按 hello **F5**金鑰 toorebuild 以及執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d54c-147">Press hello **F5** key toorebuild and run hello app.</span></span> <span data-ttu-id="1d54c-148">hello 應用程式同步處理您的本機變更與 hello Azure 行動應用程式後端使用推送和提取作業時 hello`OnRefreshItemsSelected`方法執行。</span><span class="sxs-lookup"><span data-stu-id="1d54c-148">hello app syncs your local changes with hello Azure Mobile App backend using push and pull operations when hello `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="1d54c-149">（選擇性）檢視 hello 更新的資料使用 SQL Server 物件總管 或 Fiddler 等其他工具。</span><span class="sxs-lookup"><span data-stu-id="1d54c-149">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="1d54c-150">請注意 hello 資料已同步處理 hello Azure 行動應用程式後端資料庫與 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-150">Notice hello data has been synchronized between hello Azure Mobile App backend database and hello local store.</span></span>
4. <span data-ttu-id="1d54c-151">在 hello 應用程式中，按一下 hello 核取方塊旁幾個項目 toocomplete 它們 hello 本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="1d54c-151">In hello app, click hello check box beside a few items toocomplete them in hello local store.</span></span>

   <span data-ttu-id="1d54c-152">`CheckItem`呼叫`SyncAsync`toosync 每個已完成與 hello 行動裝置應用程式後端的項目。</span><span class="sxs-lookup"><span data-stu-id="1d54c-152">`CheckItem` calls `SyncAsync` toosync each completed item with hello Mobile App backend.</span></span> <span data-ttu-id="1d54c-153">`SyncAsync` 會同時呼叫推送與提取。</span><span class="sxs-lookup"><span data-stu-id="1d54c-153">`SyncAsync` calls both push and pull.</span></span> <span data-ttu-id="1d54c-154">**每當您執行對資料表提取該 hello 用戶端所做的變更，一律自動執行推入**。</span><span class="sxs-lookup"><span data-stu-id="1d54c-154">**Whenever you execute a pull against a table that hello client has made changes to, a push is always executed automatically**.</span></span> <span data-ttu-id="1d54c-155">這可確保本機存放區中的所有資料表和關聯性都保持一致。</span><span class="sxs-lookup"><span data-stu-id="1d54c-155">This ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="1d54c-156">此行為可能會導致非預期的推送。</span><span class="sxs-lookup"><span data-stu-id="1d54c-156">This behavior may result in an unexpected push.</span></span> <span data-ttu-id="1d54c-157">如需此行為的詳細資訊，請參閱 [Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="1d54c-157">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="1d54c-158">檢閱 hello 用戶端同步程式碼</span><span class="sxs-lookup"><span data-stu-id="1d54c-158">Review hello client sync code</span></span>
<span data-ttu-id="1d54c-159">當您完成 hello 教學課程，您下載的 hello Xamarin 用戶端專案[建立 Xamarin Android 應用程式]已經包含支援使用本機 SQLite 資料庫離線同步處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d54c-159">hello Xamarin client project that you downloaded when you completed hello tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="1d54c-160">以下是在 hello 教學課程的程式碼中已包含內容的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="1d54c-160">Here is a brief overview of what is already included in hello tutorial code.</span></span> <span data-ttu-id="1d54c-161">Hello 功能的概念性概觀，請參閱[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="1d54c-161">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="1d54c-162">在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="1d54c-162">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="1d54c-163">hello 本機存放區資料庫已初始化時`ToDoActivity.OnCreate()`執行`ToDoActivity.InitLocalStoreAsync()`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-163">hello local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span></span> <span data-ttu-id="1d54c-164">這個方法會建立本機 SQLite 資料庫使用 hello `MobileServiceSQLiteStore` hello Azure 行動應用程式用戶端 SDK 所提供的類別。</span><span class="sxs-lookup"><span data-stu-id="1d54c-164">This method creates a local SQLite database using hello `MobileServiceSQLiteStore` class provided by hello Azure Mobile Apps client SDK.</span></span>

    <span data-ttu-id="1d54c-165">hello`DefineTable`方法符合提供的 hello 類型中的 hello 欄位的 hello 本機存放區中建立資料表`ToDoItem`在此情況下。</span><span class="sxs-lookup"><span data-stu-id="1d54c-165">hello `DefineTable` method creates a table in hello local store that matches hello fields in hello provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="1d54c-166">hello 類型沒有 tooinclude hello 遠端資料庫中的所有 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="1d54c-166">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="1d54c-167">很可能 toostore 只要資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="1d54c-167">It is possible toostore just a subset of columns.</span></span>

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="1d54c-168">hello`toDoTable`隸屬`ToDoActivity`的 hello`IMobileServiceSyncTable`型別而非`IMobileServiceTable`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-168">hello `toDoTable` member of `ToDoActivity` is of hello `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="1d54c-169">hello IMobileServiceSyncTable 指示所有建立、 讀取、 更新和刪除 (CRUD) 資料表作業 toohello 本機存放區資料庫。</span><span class="sxs-lookup"><span data-stu-id="1d54c-169">hello IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations toohello local store database.</span></span>

    <span data-ttu-id="1d54c-170">您可以決定當變更時，會藉由呼叫推送 toohello Azure 行動應用程式後端`IMobileServiceSyncContext.PushAsync()`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-170">You decide when changes are pushed toohello Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="1d54c-171">hello 同步處理內容可以藉由追蹤，並將變更推入用戶端應用程式有修改時的所有資料表中保留資料表關聯性`PushAsync`呼叫。</span><span class="sxs-lookup"><span data-stu-id="1d54c-171">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>

    <span data-ttu-id="1d54c-172">hello 提供程式碼會呼叫`ToDoActivity.SyncAsync()`toosync 每當 hello todoitem 清單重新整理或加入或已完成的 todoitem。</span><span class="sxs-lookup"><span data-stu-id="1d54c-172">hello provided code calls `ToDoActivity.SyncAsync()` toosync whenever hello todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="1d54c-173">hello 每次本機變更後的程式碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d54c-173">hello code syncs after every local change.</span></span>

    <span data-ttu-id="1d54c-174">Hello 提供程式碼中，所有的記錄中遠端 hello`TodoItem`查詢資料表，但也可能 toofilter 記錄藉由傳遞查詢識別碼和查詢太`PushAsync`。</span><span class="sxs-lookup"><span data-stu-id="1d54c-174">In hello provided code, all records in hello remote `TodoItem` table are queried, but it is also possible toofilter records by passing a query id and query too`PushAsync`.</span></span> <span data-ttu-id="1d54c-175">如需詳細資訊，請參閱 hello 節*增量同步處理*中[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="1d54c-175">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a><span data-ttu-id="1d54c-176">其他資源</span><span class="sxs-lookup"><span data-stu-id="1d54c-176">Additional Resources</span></span>
* <span data-ttu-id="1d54c-177">[Azure 行動應用程式中的離線資料同步]</span><span class="sxs-lookup"><span data-stu-id="1d54c-177">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="1d54c-178">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="1d54c-178">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[建立 Xamarin Android 應用程式]: ../app-service-mobile-xamarin-android-get-started.md
[Azure 行動應用程式中的離線資料同步]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[建立 Xamarin Android 應用程式]: app-service-mobile-xamarin-android-get-started.md
[Azure Mobile Apps 中的離線資料同步處理]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
