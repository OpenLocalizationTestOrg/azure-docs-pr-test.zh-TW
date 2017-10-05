---
title: "啟用 Azure 行動應用程式的離線同步處理 (Cordova) | Microsoft Docs"
description: "了解如何在 Cordova 應用程式中使用 App Service 行動應用程式快取和同步離線資料"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="389b2-103">啟用 Cordova 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="389b2-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="389b2-104">此教學課程介紹適用於 Cordova 之 Azure 行動應用程式的離線同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="389b2-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="389b2-105">離線同步處理可讓使用者與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連接進也可行。</span><span class="sxs-lookup"><span data-stu-id="389b2-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="389b2-106">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="389b2-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="389b2-107">裝置恢復上線後，這些變更就會與遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="389b2-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="389b2-108">本教學課程是根據您完成教學課程 [Apache Cordova 快速入門]時所建立之 Mobile Apps 的 Cordova 快速入門方案。</span><span class="sxs-lookup"><span data-stu-id="389b2-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="389b2-109">在本教學課程中，您將會更新快速入門方案來新增 Azure Mobile Apps 的離線功能。</span><span class="sxs-lookup"><span data-stu-id="389b2-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="389b2-110">我們也會在應用程式中反白顯示離線特有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="389b2-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="389b2-111">若要深入了解離線同步處理功能，請參閱 [Azure Mobile Apps 中的離線資料同步處理]主題。</span><span class="sxs-lookup"><span data-stu-id="389b2-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="389b2-112">API 使用方式的詳細資訊，請參閱 [API 文件](https://azure.github.io/azure-mobile-apps-js-client)。</span><span class="sxs-lookup"><span data-stu-id="389b2-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="389b2-113">在快速入門方案中新增離線同步處理</span><span class="sxs-lookup"><span data-stu-id="389b2-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="389b2-114">應用程式中必須新增離線同步處理程式碼。</span><span class="sxs-lookup"><span data-stu-id="389b2-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="389b2-115">離線同步處理需要 cordova-sqlite-storage 外掛程式，此外掛程式會在專案中納入 Azure Mobile Apps 外掛程式時自動新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="389b2-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="389b2-116">快速入門專案包含上述兩個外掛程式。</span><span class="sxs-lookup"><span data-stu-id="389b2-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="389b2-117">在 Visual Studio 的 [方案總管] 中開啟 index.js，並將下列程式碼</span><span class="sxs-lookup"><span data-stu-id="389b2-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="389b2-118">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="389b2-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="389b2-119">接下來，將下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="389b2-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="389b2-120">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="389b2-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="389b2-121">前面新增的程式碼會初始化本機存放區，並定義與 Azure 後端所使用的資料行值相符的本機資料表 </span><span class="sxs-lookup"><span data-stu-id="389b2-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="389b2-122">(您不需要在此程式碼中包含所有資料行值)。`version` 欄位由行動後端維護，用於解決衝突。</span><span class="sxs-lookup"><span data-stu-id="389b2-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="389b2-123">您可以藉由呼叫 **getSyncContext**取得同步處理內容的參考。</span><span class="sxs-lookup"><span data-stu-id="389b2-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="389b2-124">當呼叫 `.push()` 時，透過追蹤和推送所有用戶端應用程式修改之資料表中的變更，同步處理內容可協助保存資料表關聯性。</span><span class="sxs-lookup"><span data-stu-id="389b2-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="389b2-125">將應用程式的 URL 更新為行動應用程式的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="389b2-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="389b2-126">接下來，將此程式碼：</span><span class="sxs-lookup"><span data-stu-id="389b2-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="389b2-127">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="389b2-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="389b2-128">上述程式碼會初始化同步處理內容，然後呼叫 getSyncTable (而不是 getTable) 來取得本機資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="389b2-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="389b2-129">此程式碼使用本機資料庫來進行所有建立、讀取、更新和刪除 (CRUD) 資料表作業。</span><span class="sxs-lookup"><span data-stu-id="389b2-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="389b2-130">這個範例會對同步處理衝突執行簡單的錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="389b2-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="389b2-131">實際的應用程式會處理各種錯誤，例如網路狀況、伺服器衝突及其他問題。</span><span class="sxs-lookup"><span data-stu-id="389b2-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="389b2-132">如需程式碼範例，請參閱 [離線同步處理範例]。</span><span class="sxs-lookup"><span data-stu-id="389b2-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="389b2-133">接著，新增此函式以執行實際的同步處理。</span><span class="sxs-lookup"><span data-stu-id="389b2-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="389b2-134">您可以呼叫 **syncContext.push()**，以決定何時將變更推送至行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="389b2-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="389b2-135">例如，您可以在繫結至同步處理按鈕的按鈕事件處理常式中呼叫 **syncBackend**。</span><span class="sxs-lookup"><span data-stu-id="389b2-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="389b2-136">離線同步處理考量</span><span class="sxs-lookup"><span data-stu-id="389b2-136">Offline sync considerations</span></span>

<span data-ttu-id="389b2-137">在範例中，只有在應用程式啟動時，才會於登入的回呼函式中呼叫 **syncContext** 的 **push** 方法。</span><span class="sxs-lookup"><span data-stu-id="389b2-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="389b2-138">在實際的應用程式中，您也可以透過手動方式或在網路狀態變更時觸發此同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="389b2-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="389b2-139">對資料表執行提取時，如果該資料表有內容所追蹤的擱置中本機更新，則提取作業會自動觸發推送。</span><span class="sxs-lookup"><span data-stu-id="389b2-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="389b2-140">在此範例中重新整理、新增和完成項目時，您可以省略明確的 **push** 呼叫，因為它可能是多餘的。</span><span class="sxs-lookup"><span data-stu-id="389b2-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="389b2-141">在提供的程式碼中，遠端 todoItem 資料表中的所有記錄都會進行查詢，但是也可能透過將查詢識別碼與查詢傳遞至 **push**來篩選記錄。</span><span class="sxs-lookup"><span data-stu-id="389b2-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="389b2-142">如需詳細資訊，請參閱 [Azure Mobile Apps 中的離線資料同步處理]中的*增量同步處理*一節。</span><span class="sxs-lookup"><span data-stu-id="389b2-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="389b2-143">(選擇性) 停用驗證</span><span class="sxs-lookup"><span data-stu-id="389b2-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="389b2-144">如果您不想在測試離線同步處理之前設定驗證，請將登入的回呼函式註解化，但讓回呼函式內部的程式碼保持取消註解狀態。</span><span class="sxs-lookup"><span data-stu-id="389b2-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="389b2-145">將登入那幾行註解化之後，程式碼如下︰</span><span class="sxs-lookup"><span data-stu-id="389b2-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="389b2-146">現在，當您執行應用程式，應用程式會與 Azure 後端同步處理。</span><span class="sxs-lookup"><span data-stu-id="389b2-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="389b2-147">執行用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="389b2-147">Run the client app</span></span>
<span data-ttu-id="389b2-148">離線同步現在已啟用，您可以在每個平台執行用戶端應用程式至少一次，以填入本機存放區資料庫。</span><span class="sxs-lookup"><span data-stu-id="389b2-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="389b2-149">稍後，模擬一個離線案例，並在應用程式離線時修改本機存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="389b2-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="389b2-150">(選擇性) 測試同步處理行為</span><span class="sxs-lookup"><span data-stu-id="389b2-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="389b2-151">在本節中，您將修改用戶端專案，使用對後端而言無效的應用程式 URL，以模擬離線案例。</span><span class="sxs-lookup"><span data-stu-id="389b2-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="389b2-152">當您新增或變更資料項目時，這些變更會保留在本機存放區，直到重新建立連接時，才會同步處理至後端資料存放區。</span><span class="sxs-lookup"><span data-stu-id="389b2-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="389b2-153">在 [方案總管] 中開啟 index.js 專案檔案，然後將應用程式 URL 變更為指向無效的 URL，如下列程式碼所示︰</span><span class="sxs-lookup"><span data-stu-id="389b2-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="389b2-154">在 index.html 中，以相同的無效 URL 更新 CSP `<meta>` 元素。</span><span class="sxs-lookup"><span data-stu-id="389b2-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="389b2-155">建置並執行用戶端應用程式，並請注意，當應用程式嘗試在登入之後與後端進行同步處理時，主控台會記錄例外狀況。</span><span class="sxs-lookup"><span data-stu-id="389b2-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="389b2-156">您新增的任何項目在推送至行動後端之前，只存在於本機存放區。</span><span class="sxs-lookup"><span data-stu-id="389b2-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="389b2-157">用戶端應用程式運作時就如同已連接至後端一樣。</span><span class="sxs-lookup"><span data-stu-id="389b2-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="389b2-158">關閉應用程式並重新加以開啟，以驗證您所建立的新項目持續存留於本機存放區中。</span><span class="sxs-lookup"><span data-stu-id="389b2-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="389b2-159">(選擇性) 使用 Visual Studio 檢視您的 Azure SQL Database 資料表，以查看後端資料庫中的資料並無變更。</span><span class="sxs-lookup"><span data-stu-id="389b2-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="389b2-160">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="389b2-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="389b2-161">瀏覽至 [Azure]->[SQL Database 中您的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="389b2-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="389b2-162">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="389b2-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="389b2-163">現在您可以瀏覽至您的 SQL Database 資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="389b2-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="389b2-164">(選擇性) 測試與行動後端的重新連線</span><span class="sxs-lookup"><span data-stu-id="389b2-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="389b2-165">在本節中，您會將應用程式重新連接至行動後端，以模擬應用程式回到線上狀態。</span><span class="sxs-lookup"><span data-stu-id="389b2-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="389b2-166">當您登入時，資料會同步處理至行動後端。</span><span class="sxs-lookup"><span data-stu-id="389b2-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="389b2-167">重新開啟 index.js，並還原應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="389b2-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="389b2-168">重新開啟 index.html，並修正 CSP `<meta>` 元素中的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="389b2-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="389b2-169">重建並執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="389b2-169">Rebuild and run the client app.</span></span> <span data-ttu-id="389b2-170">應用程式在登入後會嘗試與行動應用程式後端同步處理。</span><span class="sxs-lookup"><span data-stu-id="389b2-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="389b2-171">請確認偵錯主控台沒有記錄任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="389b2-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="389b2-172">(選擇性) 使用 SQL Server 物件總管或 REST 工具 (例如 Fiddler) 檢視已更新的資料。</span><span class="sxs-lookup"><span data-stu-id="389b2-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="389b2-173">請注意，後端資料庫與本機存放區之間尚未同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="389b2-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="389b2-174">請注意，資料庫與本機存放區之間的資料已同步處理，並包含應用程式中斷連接時您所新增的項目。</span><span class="sxs-lookup"><span data-stu-id="389b2-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="389b2-175">其他資源</span><span class="sxs-lookup"><span data-stu-id="389b2-175">Additional resources</span></span>
* <span data-ttu-id="389b2-176">[Azure Mobile Apps 中的離線資料同步處理]</span><span class="sxs-lookup"><span data-stu-id="389b2-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="389b2-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="389b2-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="389b2-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="389b2-178">Next steps</span></span>
* <span data-ttu-id="389b2-179">在[離線同步處理範例]中，檢閱更進階的離線同步處理功能，例如衝突解決</span><span class="sxs-lookup"><span data-stu-id="389b2-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="389b2-180">在 [API 文件](https://azure.github.io/azure-mobile-apps-js-client)中，檢閱離線同步處理 API 參考</span><span class="sxs-lookup"><span data-stu-id="389b2-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="389b2-181">[Apache Cordova 快速入門]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="389b2-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="389b2-182">[離線同步處理範例]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="389b2-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="389b2-183">[Azure Mobile Apps 中的離線資料同步處理]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="389b2-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="389b2-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="389b2-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
