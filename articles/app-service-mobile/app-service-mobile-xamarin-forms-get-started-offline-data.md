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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="48688-103">啟用 Xamarin.Forms 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="48688-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="48688-104">概觀</span><span class="sxs-lookup"><span data-stu-id="48688-104">Overview</span></span>
<span data-ttu-id="48688-105">本教學課程介紹 Xamarin.Forms hello 離線的同步處理功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="48688-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="48688-106">離線同步處理可讓使用者與行動應用程式進行互動--檢視、新增或修改資料--即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="48688-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="48688-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="48688-107">Changes are stored in a local database.</span></span> <span data-ttu-id="48688-108">Hello 裝置已上線，一旦這些變更會與 hello 遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="48688-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="48688-109">本教學課程根據當您完成本教學課程 [建立 Xamarin iOS 應用程式] 時，您建立的行動應用程式 hello Xamarin.Forms 快速入門方案。</span><span class="sxs-lookup"><span data-stu-id="48688-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="48688-110">Xamarin.Forms hello 快速入門解決方案包含 hello 程式碼 toosupport 離線同步處理，這只需要啟用 toobe。</span><span class="sxs-lookup"><span data-stu-id="48688-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="48688-111">在本教學課程中，您可以更新 hello 快速入門方案 tooturn hello 離線功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="48688-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="48688-112">我們也反白 hello 應用程式中的 hello 離線特定程式碼。</span><span class="sxs-lookup"><span data-stu-id="48688-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="48688-113">如果您不使用下載的 hello 快速入門方案，您必須加入 hello 資料存取擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="48688-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="48688-114">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][1]。</span><span class="sxs-lookup"><span data-stu-id="48688-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="48688-115">toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步][2]。</span><span class="sxs-lookup"><span data-stu-id="48688-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="48688-116">啟用 hello 快速入門方案中的離線同步處理功能</span><span class="sxs-lookup"><span data-stu-id="48688-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="48688-117">hello 離線同步程式碼併入 hello 專案中，使用 C# 前置處理器指示詞。</span><span class="sxs-lookup"><span data-stu-id="48688-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="48688-118">當 hello**離線\_同步\_啟用**符號已定義，這些程式碼路徑都會納入 hello 組建。</span><span class="sxs-lookup"><span data-stu-id="48688-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="48688-119">針對 Windows 應用程式，您也必須安裝 hello SQLite 平台。</span><span class="sxs-lookup"><span data-stu-id="48688-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="48688-120">在 Visual Studio 中，以滑鼠右鍵按一下 hello 方案 >**管理方案的 NuGet 套件...**，然後尋找並安裝**Microsoft.Azure.Mobile.Client.SQLiteStore** hello 方案中的所有專案的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="48688-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="48688-121">在 [hello 方案總管] 中，開啟 hello TodoItemManager.cs 檔案來自 hello 專案，**可攜式**在 hello 名稱，亦即可攜式類別庫專案，然後取消註解 hello 前置處理器指示詞後面：</span><span class="sxs-lookup"><span data-stu-id="48688-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="48688-122">（選擇性） toosupport Windows 裝置，安裝其中一個 hello 遵循 SQLite 執行階段封裝：</span><span class="sxs-lookup"><span data-stu-id="48688-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="48688-123">**Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。</span><span class="sxs-lookup"><span data-stu-id="48688-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="48688-124">**Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。</span><span class="sxs-lookup"><span data-stu-id="48688-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="48688-125">**通用 Windows 平台**安裝[SQLite 對通用 Windows 通用 hello][5]。</span><span class="sxs-lookup"><span data-stu-id="48688-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="48688-126">雖然 hello 快速入門未包含通用 Windows 專案，hello 通用 Windows 平台支援使用 Xamarin Forms。</span><span class="sxs-lookup"><span data-stu-id="48688-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="48688-127">（選擇性）在每個 Windows 應用程式專案中，以滑鼠右鍵按一下**參考** > **加入參考...**，依序展開 hello **Windows**資料夾 >**延伸**。</span><span class="sxs-lookup"><span data-stu-id="48688-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="48688-128">啟用適當的 hello **SQLite 適用於 Windows 的**SDK 以及 hello **Visual c + + 2013 Runtime for Windows** SDK。</span><span class="sxs-lookup"><span data-stu-id="48688-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="48688-129">hello SQLite SDK 的名稱會稍微不同的每個 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="48688-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="48688-130">檢閱 hello 用戶端同步程式碼</span><span class="sxs-lookup"><span data-stu-id="48688-130">Review hello client sync code</span></span>
<span data-ttu-id="48688-131">以下是 內部 hello hello 教學課程的程式碼中已包含內容的簡短概觀`#if OFFLINE_SYNC_ENABLED`指示詞。</span><span class="sxs-lookup"><span data-stu-id="48688-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="48688-132">離線同步處理功能是 hello 可攜式類別庫專案中的 hello TodoItemManager.cs 專案檔案中。</span><span class="sxs-lookup"><span data-stu-id="48688-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="48688-133">Hello 功能的概念性概觀，請參閱[離線 Azure 行動應用程式中的資料同步處理][2]。</span><span class="sxs-lookup"><span data-stu-id="48688-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="48688-134">在執行任何資料表的作業之前，必須先初始化 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="48688-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="48688-135">hello 本機存放區資料庫已初始化在 hello **TodoItemManager**類別建構函式使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="48688-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="48688-136">此程式碼會建立新的本機 SQLite 資料庫使用 hello **MobileServiceSQLiteStore**類別。</span><span class="sxs-lookup"><span data-stu-id="48688-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="48688-137">hello **DefineTable**方法符合提供的 hello 類型中的 hello 欄位的 hello 本機存放區中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="48688-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="48688-138">hello 類型沒有 tooinclude hello 遠端資料庫中的所有 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="48688-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="48688-139">很可能 toostore 資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="48688-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="48688-140">hello **todoTable**欄位**TodoItemManager**是**IMobileServiceSyncTable**型別而非**IMobileServiceTable**。</span><span class="sxs-lookup"><span data-stu-id="48688-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="48688-141">此類別會使用 hello 本機資料庫所有建立、 讀取、 更新和刪除 (CRUD) 資料表的作業。</span><span class="sxs-lookup"><span data-stu-id="48688-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="48688-142">您可以決定當這些變更會藉由呼叫推送 toohello 行動裝置應用程式後端**PushAsync**上 hello **IMobileServiceSyncContext**。</span><span class="sxs-lookup"><span data-stu-id="48688-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="48688-143">hello 同步處理內容可以藉由追蹤，並將變更推入用戶端應用程式有修改時的所有資料表中保留資料表關聯性**PushAsync**呼叫。</span><span class="sxs-lookup"><span data-stu-id="48688-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="48688-144">hello 下列**SyncAsync**呼叫 toosync 與 hello 行動裝置應用程式後端的方法：</span><span class="sxs-lookup"><span data-stu-id="48688-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

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

    <span data-ttu-id="48688-145">這個範例會使用簡單的錯誤處理與 hello 預設同步處理常式。</span><span class="sxs-lookup"><span data-stu-id="48688-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="48688-146">實際的應用程式會處理使用自訂衝突的各種錯誤，例如網路狀況和伺服器 hello **IMobileServiceSyncHandler**實作。</span><span class="sxs-lookup"><span data-stu-id="48688-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="48688-147">離線同步處理考量</span><span class="sxs-lookup"><span data-stu-id="48688-147">Offline sync considerations</span></span>
<span data-ttu-id="48688-148">在 hello 範例 hello **SyncAsync**方法只會在啟動和同步處理要求時呼叫。</span><span class="sxs-lookup"><span data-stu-id="48688-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="48688-149">tooinitiate Android 或 iOS 應用程式中，提取 hello 項目清單; 上的同步處理適用於 Windows、 使用 hello**同步** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="48688-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="48688-150">在真實世界應用程式中，您也可以讓 hello 同步處理觸發程序 hello 網路狀態變更時。</span><span class="sxs-lookup"><span data-stu-id="48688-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="48688-151">提取針對有暫止的資料表執行本機更新追蹤先前的內容推播 hello 內容，提取作業會自動觸發程序。</span><span class="sxs-lookup"><span data-stu-id="48688-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="48688-152">當重新整理、 新增和完成項目在此範例中，您可以省略 hello 明確**PushAsync**呼叫。</span><span class="sxs-lookup"><span data-stu-id="48688-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="48688-153">Hello 提供程式碼中，查詢 hello 遠端 TodoItem 資料表中的所有記錄，但也可能 toofilter 記錄藉由傳遞查詢識別碼和查詢太**PushAsync**。</span><span class="sxs-lookup"><span data-stu-id="48688-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="48688-154">如需詳細資訊，請參閱 hello 節*增量同步處理*中[離線 Azure 行動應用程式中的資料同步處理][2]。</span><span class="sxs-lookup"><span data-stu-id="48688-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="48688-155">執行 hello 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="48688-155">Run hello client app</span></span>
<span data-ttu-id="48688-156">現在已啟用離線同步時，執行 hello 用戶端應用程式每個平台 toopopulate hello 本機存放區資料庫的至少一次。</span><span class="sxs-lookup"><span data-stu-id="48688-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="48688-157">更新版本中，模擬離線案例中，並修改 hello 本機存放區中的 hello 資料 hello 應用程式處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="48688-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="48688-158">更新 hello hello 用戶端應用程式同步處理行為</span><span class="sxs-lookup"><span data-stu-id="48688-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="48688-159">在本節中，修改 hello 用戶端專案 toosimulate 離線案例中為您的後端使用無效的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="48688-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="48688-160">或者，您可以關閉網路連線太移動您的裝置 「 飛航模式 」。</span><span class="sxs-lookup"><span data-stu-id="48688-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="48688-161">當您新增或變更資料的項目時，這些變更會 hello 本機存放區中保留，但未同步處理 toohello 後端資料存放區，直到 hello 連接重新建立。</span><span class="sxs-lookup"><span data-stu-id="48688-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="48688-162">在 [hello 方案總管] 中，開啟 hello Constants.cs 專案檔從 hello**可攜式**專案，並變更 hello 值`ApplicationURL`toopoint tooan URL 無效：</span><span class="sxs-lookup"><span data-stu-id="48688-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="48688-163">開啟 hello TodoItemManager.cs 檔案從 hello**可攜式**專案，然後新增**攔截**hello 基底**例外狀況**類別 toohello **try … catch**中區塊**SyncAsync**。</span><span class="sxs-lookup"><span data-stu-id="48688-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="48688-164">這**攔截**區塊寫入 hello 例外狀況訊息 toohello 主控台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="48688-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="48688-165">建置並執行 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="48688-165">Build and run hello client app.</span></span>  <span data-ttu-id="48688-166">新增一些新項目。</span><span class="sxs-lookup"><span data-stu-id="48688-166">Add some new items.</span></span> <span data-ttu-id="48688-167">請注意例外狀況會記錄在 hello 與 hello 後端的每個嘗試 toosync 主控台。</span><span class="sxs-lookup"><span data-stu-id="48688-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="48688-168">這些新的項目存在於 hello 本機存放區，直到它們可以推送 toohello 行動後端。</span><span class="sxs-lookup"><span data-stu-id="48688-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="48688-169">hello 用戶端應用程式行為就如同它是連接的 toohello 後端、 支援所有建立、 讀取、 更新、 刪除 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="48688-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="48688-170">關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="48688-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="48688-171">（選擇性）使用 Visual Studio tooview hello 後端資料庫中的 hello 資料尚未變更您 Azure SQL Database 資料表 toosee。</span><span class="sxs-lookup"><span data-stu-id="48688-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="48688-172">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="48688-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="48688-173">瀏覽 tooyour 資料庫**Azure**->**SQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="48688-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="48688-174">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="48688-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="48688-175">現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="48688-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="48688-176">更新 hello 用戶端應用程式 tooreconnect 行動後端</span><span class="sxs-lookup"><span data-stu-id="48688-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="48688-177">在本節中，重新連線 hello 應用程式 toohello 行動後端，這將模擬 hello 光顧 tooan 線上狀態的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48688-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="48688-178">當您執行 hello 重新整理鍵筆勢時，資料會是已同步的 tooyour 行動後端。</span><span class="sxs-lookup"><span data-stu-id="48688-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="48688-179">重新開啟 Constants.cs。</span><span class="sxs-lookup"><span data-stu-id="48688-179">Reopen Constants.cs.</span></span> <span data-ttu-id="48688-180">正確的 hello `applicationURL` toopoint toohello 更正 URL。</span><span class="sxs-lookup"><span data-stu-id="48688-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="48688-181">重新建置並執行 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="48688-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="48688-182">hello 與 hello 行動裝置應用程式後端應用程式嘗試 toosync 之後啟動。</span><span class="sxs-lookup"><span data-stu-id="48688-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="48688-183">請確認在 hello 偵錯主控台也會記錄任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="48688-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="48688-184">（選擇性）使用 SQL Server 物件總管 或 Fiddler 等其他工具的資料更新時檢視 hello 或[郵差][6]。</span><span class="sxs-lookup"><span data-stu-id="48688-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="48688-185">請注意 hello 資料已同步處理 hello 後端資料庫與 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="48688-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="48688-186">請注意 hello 資料已同步處理 hello 資料庫與 hello 本機存放區，並包含您加入您的應用程式已中斷連接時的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="48688-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48688-187">其他資源</span><span class="sxs-lookup"><span data-stu-id="48688-187">Additional Resources</span></span>
* <span data-ttu-id="48688-188">[Azure Mobile Apps 中的離線資料同步處理][2]</span><span class="sxs-lookup"><span data-stu-id="48688-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="48688-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="48688-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
