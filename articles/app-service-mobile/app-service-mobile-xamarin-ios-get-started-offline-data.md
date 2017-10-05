---
title: "啟用 Azure 行動應用程式 (Xamarin iOS) 的離線同步處理"
description: "了解如何在 Xamarin iOS 應用程式中使用應用程式服務行動應用程式快取和同步離線資料"
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
ms.openlocfilehash: b5878d8a2e18cf08b6e9074ecf40cd732624f0c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a><span data-ttu-id="18fa5-103">啟用 Xamarin iOS 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="18fa5-103">Enable offline sync for your Xamarin.iOS mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="18fa5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="18fa5-104">Overview</span></span>
<span data-ttu-id="18fa5-105">此教學課程介紹適用於 Xamarin.iOS 之 Azure 行動應用程式的離線同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="18fa5-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.iOS.</span></span> <span data-ttu-id="18fa5-106">離線同步處理可讓使用者與行動應用程式進行互動--檢視、新增或修改資料--即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="18fa5-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="18fa5-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="18fa5-107">Changes are stored in a local database.</span></span> <span data-ttu-id="18fa5-108">裝置恢復上線後，這些變更就會與遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="18fa5-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="18fa5-109">在本教學課程中，更新[建立 Xamarin iOS 應用程式]中的 Xamarin.iOS 應用程式專案，來支援 Azure Mobile Apps 的離線功能。</span><span class="sxs-lookup"><span data-stu-id="18fa5-109">In this tutorial, update the Xamarin.iOS app project from [Create a Xamarin iOS app] to support the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="18fa5-110">如果您不要使用下載的快速入門伺服器專案，必須將資料存取擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="18fa5-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="18fa5-111">如需伺服器擴充套件的詳細資訊，請參閱 [使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="18fa5-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="18fa5-112">若要深入了解離線同步處理功能，請參閱 [Azure 行動應用程式中的離線資料同步處理]主題。</span><span class="sxs-lookup"><span data-stu-id="18fa5-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-client-app-to-support-offline-features"></a><span data-ttu-id="18fa5-113">更新用戶端應用程式以支援離線功能</span><span class="sxs-lookup"><span data-stu-id="18fa5-113">Update the client app to support offline features</span></span>
<span data-ttu-id="18fa5-114">Azure 行動應用程式的離線功能可讓您在離線狀態時，仍可與本機資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="18fa5-114">Azure Mobile App offline features allow you to interact with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="18fa5-115">若要在您的應用程式中使用這些功能，您必須將 [SyncContext] 初始化至本機存放區。</span><span class="sxs-lookup"><span data-stu-id="18fa5-115">To use these features in your app, initialize a [SyncContext] to a local store.</span></span> <span data-ttu-id="18fa5-116">透過 [IMobileServiceSyncTable] 介面參考您的資料表。</span><span class="sxs-lookup"><span data-stu-id="18fa5-116">Reference your table through the [IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="18fa5-117">SQLite 可做為裝置上的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="18fa5-117">SQLite is used as the local store on the device.</span></span>

1. <span data-ttu-id="18fa5-118">在您於[建立 Xamarin iOS 應用程式]教學課程所完成的專案中，開啟 NuGet 封裝管理員，然後搜尋並安裝 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="18fa5-118">Open the NuGet package manager in the project that you completed in the [Create a Xamarin iOS app] tutorial,  then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="18fa5-119">開啟 QSTodoService.cs 檔案，並取消註解 `#define OFFLINE_SYNC_ENABLED` 定義。</span><span class="sxs-lookup"><span data-stu-id="18fa5-119">Open the QSTodoService.cs file and uncomment the `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="18fa5-120">重建並執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="18fa5-120">Rebuild and run the client app.</span></span> <span data-ttu-id="18fa5-121">應用程式的運作方式和啟用離線同步處理之前的方式相同。</span><span class="sxs-lookup"><span data-stu-id="18fa5-121">The app works the same as it did before you enabled offline sync.</span></span> <span data-ttu-id="18fa5-122">不過，本機資料庫現在會填入可在離線案例下使用的資料。</span><span class="sxs-lookup"><span data-stu-id="18fa5-122">However, the local database is now populated with data that can be used in an offline scenario.</span></span>

## <span data-ttu-id="18fa5-123"><a name="update-sync"></a>更新應用程式以使其與後端中斷連線</span><span class="sxs-lookup"><span data-stu-id="18fa5-123"><a name="update-sync"></a>Update the app to disconnect from the backend</span></span>
<span data-ttu-id="18fa5-124">在本節中，您將中斷與行動應用程式後端的連線，以模擬離線狀態。</span><span class="sxs-lookup"><span data-stu-id="18fa5-124">In this section, you break the connection to your Mobile App backend to simulate an offline situation.</span></span> <span data-ttu-id="18fa5-125">當您新增資料項目時，您的例外狀況處理常式會指出應用程式處於離線模式。</span><span class="sxs-lookup"><span data-stu-id="18fa5-125">When you add data items, your exception handler tells you that the app is in offline mode.</span></span> <span data-ttu-id="18fa5-126">處於此狀態時，新項目會新增到本機存放區，並且會在推送接下來於連線狀態執行時，同步處理至行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="18fa5-126">In this state, new items added in the local store and will be synced to the mobile app backend when push is next run in a connected state.</span></span>

1. <span data-ttu-id="18fa5-127">編輯共用專案中的 QSToDoService.cs。</span><span class="sxs-lookup"><span data-stu-id="18fa5-127">Edit QSToDoService.cs in the shared project.</span></span> <span data-ttu-id="18fa5-128">變更 **applicationURL** 以指向無效的 URL：</span><span class="sxs-lookup"><span data-stu-id="18fa5-128">Change the **applicationURL** to point to an invalid URL:</span></span>

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    <span data-ttu-id="18fa5-129">您也可以透過停用裝置的 WiFi 和行動電話通訊網路，或使用飛航模式來示範離線行為。</span><span class="sxs-lookup"><span data-stu-id="18fa5-129">You can also demonstrate offline behavior by disabling wifi and cellular networks on the device or using airplane mode.</span></span>
2. <span data-ttu-id="18fa5-130">建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="18fa5-130">Build and run the app.</span></span> <span data-ttu-id="18fa5-131">請注意，應用程式啟動後同步處理無法重新整理。</span><span class="sxs-lookup"><span data-stu-id="18fa5-131">Notice your sync failed on refresh when the app launched.</span></span>
3. <span data-ttu-id="18fa5-132">輸入新項目，並注意每次您按一下 [儲存]  時，推送都會失敗並具有 [CancelledByNetworkError] 狀態。</span><span class="sxs-lookup"><span data-stu-id="18fa5-132">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="18fa5-133">不過，新的 todo 項目在可推送至行動應用程式後端之前，都會存留在本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="18fa5-133">However, the new todo items exist in the local store until they can be pushed to the mobile app backend.</span></span>  <span data-ttu-id="18fa5-134">在生產應用程式中，如果您隱藏這些例外狀況，用戶端應用程式的行為會如同它仍連線到行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="18fa5-134">In a production app, if you suppress these exceptions the client app behaves as if it's still connected to the mobile app backend.</span></span>
4. <span data-ttu-id="18fa5-135">關閉應用程式並重新加以開啟，以驗證您所建立的新項目持續存留於本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="18fa5-135">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="18fa5-136">(選擇性) 如果您已在電腦上安裝 Visual Studio，請開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="18fa5-136">(Optional) If you have Visual Studio installed on a PC, open **Server Explorer**.</span></span> <span data-ttu-id="18fa5-137">瀏覽至 [Azure]-> [SQL Database 中您的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="18fa5-137">Navigate to your database in **Azure**-> **SQL Databases**.</span></span> <span data-ttu-id="18fa5-138">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="18fa5-138">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="18fa5-139">現在您可以瀏覽至您的 SQL Database 資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="18fa5-139">Now you can browse to your SQL database table and its contents.</span></span> <span data-ttu-id="18fa5-140">確認後端資料庫中的資料沒有變更。</span><span class="sxs-lookup"><span data-stu-id="18fa5-140">Verify that the data in the backend database has not changed.</span></span>
6. <span data-ttu-id="18fa5-141">(選擇性) 使用 REST 工具 (例如 Fiddler 或 Postman) 來查詢您的行動後端 (使用表單 `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`中的 GET 查詢)。</span><span class="sxs-lookup"><span data-stu-id="18fa5-141">(Optional) Use a REST tool such as Fiddler or Postman to query your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <span data-ttu-id="18fa5-142"><a name="update-online-app"></a>更新應用程式以重新連線您的行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="18fa5-142"><a name="update-online-app"></a>Update the app to reconnect your Mobile App backend</span></span>
<span data-ttu-id="18fa5-143">在本節中，您會將應用程式重新連接至行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="18fa5-143">In this section, reconnect the app to the mobile app backend.</span></span> <span data-ttu-id="18fa5-144">您將藉此模擬應用程式在行動應用程式後端中，從離線狀態恢復為線上狀態的情境。</span><span class="sxs-lookup"><span data-stu-id="18fa5-144">This simulates the app moving from an offline state to an online state with the mobile app backend.</span></span>   <span data-ttu-id="18fa5-145">如果您關閉網路連線來模擬網路中斷情況，則不需要變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="18fa5-145">If you simulated the network breakage by turning off network connectivity, no code changes are needed.</span></span>
<span data-ttu-id="18fa5-146">重新開啟網路。</span><span class="sxs-lookup"><span data-stu-id="18fa5-146">Turn the network on again.</span></span>  <span data-ttu-id="18fa5-147">第一次執行應用程式時會呼叫 `RefreshDataAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="18fa5-147">When you first run the application, the `RefreshDataAsync` method is called.</span></span> <span data-ttu-id="18fa5-148">這會進而呼叫 `SyncAsync` 來同步處理您的本機存放區與後端資料庫。</span><span class="sxs-lookup"><span data-stu-id="18fa5-148">This in turn calls `SyncAsync` to sync your local store with the backend database.</span></span>

1. <span data-ttu-id="18fa5-149">在共用專案中，開啟 QSToDoService.cs，並還原您對 **applicationURL** 屬性所做的變更。</span><span class="sxs-lookup"><span data-stu-id="18fa5-149">Open QSToDoService.cs in the shared project, and revert your change of the **applicationURL** property.</span></span>
2. <span data-ttu-id="18fa5-150">重新建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="18fa5-150">Rebuild and run the app.</span></span> <span data-ttu-id="18fa5-151">該應用程式會在 `OnRefreshItemsSelected` 方法執行時使用推送與提取作業，同步處理您的本機變更與 Azure 行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="18fa5-151">The app syncs your local changes with the Azure Mobile App backend using push and pull operations when the `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="18fa5-152">(選擇性) 使用 SQL Server 物件總管或 REST 工具 (例如 Fiddler) 檢視已更新的資料。</span><span class="sxs-lookup"><span data-stu-id="18fa5-152">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="18fa5-153">請注意，Azure 行動應用程式後端資料庫與本機存放區之間的資料已同步處理。</span><span class="sxs-lookup"><span data-stu-id="18fa5-153">Notice the data has been synchronized between the Azure Mobile App backend database and the local store.</span></span>
4. <span data-ttu-id="18fa5-154">在應用程式中，按一下幾個項目旁邊的核取方塊，以在本機存放區中完成它們。</span><span class="sxs-lookup"><span data-stu-id="18fa5-154">In the app, click the check box beside a few items to complete them in the local store.</span></span>

   <span data-ttu-id="18fa5-155">`CompleteItemAsync` 會呼叫 `SyncAsync`，以便與行動應用程式後端同步處理每個已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="18fa5-155">`CompleteItemAsync` calls `SyncAsync` to sync each completed item with the Mobile App backend.</span></span> <span data-ttu-id="18fa5-156">`SyncAsync` 會同時呼叫推送與提取。</span><span class="sxs-lookup"><span data-stu-id="18fa5-156">`SyncAsync` calls both push and pull.</span></span>
   <span data-ttu-id="18fa5-157">**每當您針對用戶端進行變更的資料表執行提取時，用戶端同步處理內容上的推送一律會先自動執行**。</span><span class="sxs-lookup"><span data-stu-id="18fa5-157">**Whenever you execute a pull against a table that the client has made changes to, a push on the client sync context is always executed first automatically**.</span></span> <span data-ttu-id="18fa5-158">隱含推送可確保本機存放區中的所有資料表和關聯性都保持一致。</span><span class="sxs-lookup"><span data-stu-id="18fa5-158">The implicit push ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="18fa5-159">如需此行為的詳細資訊，請參閱 [Azure 行動應用程式中的離線資料同步處理]。</span><span class="sxs-lookup"><span data-stu-id="18fa5-159">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="18fa5-160">檢閱用戶端同步處理程式碼</span><span class="sxs-lookup"><span data-stu-id="18fa5-160">Review the client sync code</span></span>
<span data-ttu-id="18fa5-161">您完成 [建立 Xamarin iOS 應用程式] 教學課程時所下載的 Xamarin 用戶端專案，已經包含了使用本機 SQLite 資料庫支援離線同步處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="18fa5-161">The Xamarin client project that you downloaded when you completed the tutorial [Create a Xamarin iOS app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="18fa5-162">以下是已經包含在教學課程程式碼中之內容的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="18fa5-162">Here is a brief overview of what is already included in the tutorial code.</span></span> <span data-ttu-id="18fa5-163">如需此功能的概念性概觀，請參閱 [Azure 行動應用程式中的離線資料同步處理]。</span><span class="sxs-lookup"><span data-stu-id="18fa5-163">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="18fa5-164">必須先初始化本機存放區，才可以執行資料表作業。</span><span class="sxs-lookup"><span data-stu-id="18fa5-164">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="18fa5-165">當 `QSTodoListViewController.ViewDidLoad()` 執行 `QSTodoService.InitializeStoreAsync()` 時會初始化本機存放區資料庫。</span><span class="sxs-lookup"><span data-stu-id="18fa5-165">The local store database is initialized when `QSTodoListViewController.ViewDidLoad()` executes `QSTodoService.InitializeStoreAsync()`.</span></span> <span data-ttu-id="18fa5-166">這個方法會使用 Azure 行動應用程式用戶端 SDK 所提供的 `MobileServiceSQLiteStore` 類別，建立新的本機 SQLite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="18fa5-166">This method creates a new local SQLite database using the `MobileServiceSQLiteStore` class provided by the Azure Mobile App client SDK.</span></span>

    <span data-ttu-id="18fa5-167">`DefineTable` 方法會在本機存放區中建立與給定類型中的欄位相符的資料表，在此案例中為 `ToDoItem`。</span><span class="sxs-lookup"><span data-stu-id="18fa5-167">The `DefineTable` method creates a table in the local store that matches the fields in the provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="18fa5-168">該類型不必包含遠端資料庫中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="18fa5-168">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="18fa5-169">可以只儲存資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="18fa5-169">It is possible to store just a subset of columns.</span></span>

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses the default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="18fa5-170">`QSTodoService` 的 `todoTable` 成員屬於 `IMobileServiceSyncTable` 類型而非 `IMobileServiceTable`。</span><span class="sxs-lookup"><span data-stu-id="18fa5-170">The `todoTable` member of `QSTodoService` is of the `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="18fa5-171">IMobileServiceSyncTable 會將所有建立、讀取、更新和刪除 (CRUD) 資料表作業導向至本機存放區資料庫。</span><span class="sxs-lookup"><span data-stu-id="18fa5-171">The IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations to the local store database.</span></span>

    <span data-ttu-id="18fa5-172">您可以呼叫 `IMobileServiceSyncContext.PushAsync()`，以決定何時將那些變更推送至 Azure 行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="18fa5-172">You decide when those changes are pushed to the Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="18fa5-173">當呼叫 `PushAsync` 時，透過追蹤和推送所有用戶端應用程式修改之資料表中的變更，同步處理內容可協助保存資料表關聯性。</span><span class="sxs-lookup"><span data-stu-id="18fa5-173">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>

    <span data-ttu-id="18fa5-174">每當重新整理 todoitem 清單或是已新增或完成 todoitem 時，提供的程式碼會呼叫 `QSTodoService.SyncAsync()` 來進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="18fa5-174">The provided code calls `QSTodoService.SyncAsync()` to sync whenever the todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="18fa5-175">每次本機變更之後，應用程式會同步處理。</span><span class="sxs-lookup"><span data-stu-id="18fa5-175">The app syncs after every local change.</span></span> <span data-ttu-id="18fa5-176">如果針對具有內容追蹤之擱置中本機更新的資料表執行提取，該提取作業會先自動觸發內容推送。</span><span class="sxs-lookup"><span data-stu-id="18fa5-176">If a pull is executed against a table that has pending local updates tracked by the context, that pull operation will automatically trigger a context push first.</span></span>

    <span data-ttu-id="18fa5-177">在提供的程式碼中，遠端 `TodoItem` 資料表中的所有記錄都會進行查詢，但是也可能透過將查詢識別碼與查詢傳遞至 `PushAsync` 來篩選記錄。</span><span class="sxs-lookup"><span data-stu-id="18fa5-177">In the provided code, all records in the remote `TodoItem` table are queried, but it is also possible to filter records by passing a query id and query to `PushAsync`.</span></span> <span data-ttu-id="18fa5-178">如需詳細資訊，請參閱 [Azure 行動應用程式中的離線資料同步處理]中的*增量同步處理*一節。</span><span class="sxs-lookup"><span data-stu-id="18fa5-178">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="18fa5-179">其他資源</span><span class="sxs-lookup"><span data-stu-id="18fa5-179">Additional Resources</span></span>
* <span data-ttu-id="18fa5-180">[Azure 行動應用程式中的離線資料同步處理]</span><span class="sxs-lookup"><span data-stu-id="18fa5-180">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="18fa5-181">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="18fa5-181">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="18fa5-182">[建立 Xamarin iOS 應用程式]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="18fa5-182">[Create a Xamarin iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="18fa5-183">[Azure 行動應用程式中的離線資料同步處理]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="18fa5-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="18fa5-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="18fa5-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span></span>
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
