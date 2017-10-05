---
title: "啟用 Azure 行動應用程式的離線同步處理 (Xamarin.Forms) | Microsoft Docs"
description: "了解如何在 Xamarin.Forms 應用程式中使用 App Service 行動應用程式快取和同步離線資料"
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
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="1d890-103">啟用 Xamarin.Forms 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="1d890-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="1d890-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1d890-104">Overview</span></span>
<span data-ttu-id="1d890-105">此教學課程介紹適用於 Xamarin.Forms 之 Azure 行Mobile Apps 的離線同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="1d890-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="1d890-106">離線同步處理可讓使用者與行動應用程式進行互動--檢視、新增或修改資料--即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="1d890-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="1d890-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="1d890-107">Changes are stored in a local database.</span></span> <span data-ttu-id="1d890-108">裝置恢復上線後，這些變更就會與遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d890-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="1d890-109">本教學課程是根據您完成教學課程 [建立 Xamarin iOS 應用程式] 時所建立之 Mobile Apps 的 Xamarin.Forms 快速入門方案。</span><span class="sxs-lookup"><span data-stu-id="1d890-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="1d890-110">Xamarin.Forms 的快速入門方案包含程式碼來支援離線同步處理，只需要啟用即可。</span><span class="sxs-lookup"><span data-stu-id="1d890-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="1d890-111">在本教學課程中，您將會更新快速入門方案來開啟 Azure Mobile Apps 的離線功能。</span><span class="sxs-lookup"><span data-stu-id="1d890-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="1d890-112">我們也會在應用程式中反白顯示離線特有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d890-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="1d890-113">如果您不要使用下載的快速入門方案，則必須將資料存取擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="1d890-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="1d890-114">如需伺服器擴充套件的詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK][1]。</span><span class="sxs-lookup"><span data-stu-id="1d890-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="1d890-115">若要深入了解離線同步處理功能，請參閱 [Azure Mobile Apps 中的離線資料同步處理][2]主題。</span><span class="sxs-lookup"><span data-stu-id="1d890-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="1d890-116">啟用快速入門方案中的離線同步處理功能</span><span class="sxs-lookup"><span data-stu-id="1d890-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="1d890-117">專案中使用 C# 前置處理器指示詞來包含離線同步處理程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d890-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="1d890-118">定義 **OFFLINE\_SYNC\_ENABLED** 符號後，組建中會包含這些程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="1d890-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="1d890-119">針對 Windows 應用程式，您也必須安裝 SQLite 平台。</span><span class="sxs-lookup"><span data-stu-id="1d890-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="1d890-120">在 Visual Studio 中，以滑鼠右鍵按一下方案 > [管理方案的 NuGet 套件...]，然後為方案中的所有專案，尋找並安裝 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="1d890-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="1d890-121">在 [方案總管] 中，從名稱中有 **Portable** 的專案中開啟 TodoItemManager.cs 檔案，也就是可攜式類別庫專案，然後取消註解下列前置處理器指示詞︰</span><span class="sxs-lookup"><span data-stu-id="1d890-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="1d890-122">(選擇性) 若要支援 Windows 裝置，請安裝下列其中一個 SQLite 執行階段封裝︰</span><span class="sxs-lookup"><span data-stu-id="1d890-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="1d890-123">**Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。</span><span class="sxs-lookup"><span data-stu-id="1d890-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="1d890-124">**Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。</span><span class="sxs-lookup"><span data-stu-id="1d890-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="1d890-125">**通用 Windows 平台：**安裝 [適用於通用 Windows 平台的 SQLite][5]。</span><span class="sxs-lookup"><span data-stu-id="1d890-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="1d890-126">雖然快速入門中未包含通用 Windows 專案，使用 Xamarin Forms 可支援通用 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="1d890-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="1d890-127">(選擇性) 在每個 Windows 應用程式專案中，以滑鼠右鍵按一下 [參考] >  [新增參考...]，展開 [Windows] 資料夾 > [擴充]。</span><span class="sxs-lookup"><span data-stu-id="1d890-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="1d890-128">啟用適當的 **SQLite for Windows** SDK 及 **Visual C++ 2013 Runtime for Windows** SDK。</span><span class="sxs-lookup"><span data-stu-id="1d890-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="1d890-129">每個 Windows 平台的 SQLite SDK 名稱稍有差異。</span><span class="sxs-lookup"><span data-stu-id="1d890-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="1d890-130">檢閱用戶端同步處理程式碼</span><span class="sxs-lookup"><span data-stu-id="1d890-130">Review the client sync code</span></span>
<span data-ttu-id="1d890-131">以下是教學課程程式碼的 `#if OFFLINE_SYNC_ENABLED` 指示詞內已包含之程式碼的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="1d890-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="1d890-132">離線同步處理功能位於可攜式類別庫專案的 TodoItemManager.cs 專案檔中。</span><span class="sxs-lookup"><span data-stu-id="1d890-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="1d890-133">如需此功能的概念性概觀，請參閱 [Azure Mobile Apps 中的離線資料同步處理][2]。</span><span class="sxs-lookup"><span data-stu-id="1d890-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="1d890-134">必須先初始化本機存放區，才可以執行資料表作業。</span><span class="sxs-lookup"><span data-stu-id="1d890-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="1d890-135">**TodoItemManager** 類別建構函式中使用下列程式碼來初始化本機存放區資料庫︰</span><span class="sxs-lookup"><span data-stu-id="1d890-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="1d890-136">此代碼會使用 **MobileServiceSQLiteStore** 類別建立新的本機 SQLite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1d890-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="1d890-137">**DefineTable** 方法會在本機存放區中建立一個與所提供之類型的欄位相符的資料表。</span><span class="sxs-lookup"><span data-stu-id="1d890-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="1d890-138">該類型不必包含遠端資料庫中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="1d890-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="1d890-139">可以儲存資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="1d890-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="1d890-140">**TodoItemManager** 中的 **todoTable** 欄位是 **IMobileServiceSyncTable** 類型，而非 **IMobileServiceTable**。</span><span class="sxs-lookup"><span data-stu-id="1d890-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="1d890-141">此類別使用本機資料庫來進行所有建立、讀取、更新和刪除 (CRUD) 資料表作業。</span><span class="sxs-lookup"><span data-stu-id="1d890-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="1d890-142">您可以在 **IMobileServiceSyncContext** 上呼叫 **PushAsync**，以決定何時將這些變更推送到行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1d890-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="1d890-143">當呼叫 **PushAsync** 時，透過追蹤和推送所有用戶端應用程式修改之資料表中的變更，同步處理內容可協助保存資料表關聯性。</span><span class="sxs-lookup"><span data-stu-id="1d890-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="1d890-144">呼叫下列 **SyncAsync** 方法可以與行動應用程式後端同步處理︰</span><span class="sxs-lookup"><span data-stu-id="1d890-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

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
                        //Update failed, reverting to server's copy.
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

    <span data-ttu-id="1d890-145">這個範例使用簡單的錯誤處理及預設同步處理常式。</span><span class="sxs-lookup"><span data-stu-id="1d890-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="1d890-146">實際的應用程式會使用自訂 **IMobileServiceSyncHandler** 實作來處理各種錯誤，例如網路狀況和伺服器衝突。</span><span class="sxs-lookup"><span data-stu-id="1d890-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="1d890-147">離線同步處理考量</span><span class="sxs-lookup"><span data-stu-id="1d890-147">Offline sync considerations</span></span>
<span data-ttu-id="1d890-148">在範例中，只會在開始時和特別要求同步處理時呼叫 **SyncAsync** 方法。</span><span class="sxs-lookup"><span data-stu-id="1d890-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="1d890-149">若要在 Android 或 iOS 應用程式中起始同步處理，請在項目清單上向下拉。若是 Windows，請使用 [同步] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d890-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="1d890-150">在實際的應用程式中，您也可以在網路狀態變更時觸發此同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d890-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="1d890-151">針對具有內容追蹤之擱置中本機更新的資料表執行提取，該提取作業將自動觸發先前的內容推送。</span><span class="sxs-lookup"><span data-stu-id="1d890-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="1d890-152">在此範例中重新整理、新增和完成項目時，您可以省略明確的 **PushAsync** 呼叫。</span><span class="sxs-lookup"><span data-stu-id="1d890-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="1d890-153">在提供的程式碼中，遠端 TodoItem 資料表中的所有記錄都會進行查詢，但是也可能透過將查詢識別碼與查詢傳遞至 **PushAsync**來篩選記錄。</span><span class="sxs-lookup"><span data-stu-id="1d890-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="1d890-154">如需詳細資訊，請參閱 [Azure Mobile Apps 中的離線資料同步處理][2]中的「增量同步處理」一節。</span><span class="sxs-lookup"><span data-stu-id="1d890-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="1d890-155">執行用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="1d890-155">Run the client app</span></span>
<span data-ttu-id="1d890-156">離線同步現在已啟用，請在每個平台執行用戶端應用程式至少一次，以填入本機存放區資料庫。</span><span class="sxs-lookup"><span data-stu-id="1d890-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="1d890-157">稍後，模擬一個離線案例，並在應用程式離線時修改本機存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="1d890-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="1d890-158">更新用戶端應用程式的同步處理行為</span><span class="sxs-lookup"><span data-stu-id="1d890-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="1d890-159">在本節中，您將透過使用無效的後端應用程式 URL，修改用戶端專案來模擬離線案例。</span><span class="sxs-lookup"><span data-stu-id="1d890-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="1d890-160">或者，您可以將裝置切換至「飛航模式」來關閉網路連線。</span><span class="sxs-lookup"><span data-stu-id="1d890-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="1d890-161">當您新增或變更資料項目時，這些變更會存放在本機存放區，但不會同步處理到後端資料存放區，直到重新建立連線為止。</span><span class="sxs-lookup"><span data-stu-id="1d890-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="1d890-162">在 [方案總管] 中，從 **Portable** 專案開啟 Constants.cs 專案檔案，然後變更 `ApplicationURL` 的值以指向無效的 URL：</span><span class="sxs-lookup"><span data-stu-id="1d890-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="1d890-163">從 **Portable** 專案開啟 TodoItemManager.cs 檔案，然後將基底 **Exception** 類別的 **catch** 新增至 **SyncAsync** 中的 **try…catch** 區塊。</span><span class="sxs-lookup"><span data-stu-id="1d890-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="1d890-164">這個 **catch** 區塊會將例外狀況訊息寫入主控台，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1d890-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="1d890-165">建置並執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d890-165">Build and run the client app.</span></span>  <span data-ttu-id="1d890-166">新增一些新項目。</span><span class="sxs-lookup"><span data-stu-id="1d890-166">Add some new items.</span></span> <span data-ttu-id="1d890-167">請注意，每次嘗試與後端同步時，主控台都會記錄例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1d890-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="1d890-168">這些新的項目在可推送至行動後端之前，都只會存留在本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="1d890-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="1d890-169">用戶端應用程式的行為，會如同它已連接到支援所有建立、讀取、更新、刪除 (CRUD) 作業的後端。</span><span class="sxs-lookup"><span data-stu-id="1d890-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="1d890-170">關閉應用程式並重新加以開啟，以驗證您所建立的新項目持續存留於本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="1d890-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="1d890-171">(選擇性) 使用 Visual Studio 檢視您的 Azure SQL Database 資料表，以查看後端資料庫中的資料並無變更。</span><span class="sxs-lookup"><span data-stu-id="1d890-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="1d890-172">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="1d890-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="1d890-173">瀏覽至 [Azure]->[SQL Database 中您的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="1d890-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="1d890-174">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="1d890-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="1d890-175">現在您可以瀏覽至您的 SQL Database 資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="1d890-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="1d890-176">更新用戶端應用程式，重新連接您的行動後端</span><span class="sxs-lookup"><span data-stu-id="1d890-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="1d890-177">在本節中，會將應用程式重新連接到行動後端，而模擬回到線上狀態的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d890-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="1d890-178">當您執行重新整理動作時，資料會同步處理至您的行動後端中。</span><span class="sxs-lookup"><span data-stu-id="1d890-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="1d890-179">重新開啟 Constants.cs。</span><span class="sxs-lookup"><span data-stu-id="1d890-179">Reopen Constants.cs.</span></span> <span data-ttu-id="1d890-180">更正 `applicationURL` 以指向正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="1d890-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="1d890-181">重建並執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d890-181">Rebuild and run the client app.</span></span> <span data-ttu-id="1d890-182">應用程式在啟動後會嘗試與行動應用程式後端同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d890-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="1d890-183">請確認偵錯主控台沒有記錄任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1d890-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="1d890-184">(選擇性) 使用 SQL Server 物件總管或 REST 工具 (例如 Fiddler 或 [Postman][6]) 檢視已更新的資料。</span><span class="sxs-lookup"><span data-stu-id="1d890-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="1d890-185">請注意，後端資料庫與本機存放區之間尚未同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="1d890-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="1d890-186">請注意，資料庫與本機存放區之間的資料已同步處理，並包含應用程式中斷連接時您所新增的項目。</span><span class="sxs-lookup"><span data-stu-id="1d890-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d890-187">其他資源</span><span class="sxs-lookup"><span data-stu-id="1d890-187">Additional Resources</span></span>
* <span data-ttu-id="1d890-188">[Azure Mobile Apps 中的離線資料同步處理][2]</span><span class="sxs-lookup"><span data-stu-id="1d890-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="1d890-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="1d890-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
