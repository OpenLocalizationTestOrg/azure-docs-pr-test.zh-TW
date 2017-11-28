---
title: "aaaEnable 離線同步處理您的 Azure 行動應用程式 (Cordova) |Microsoft 文件"
description: "深入了解如何 toouse App Service 行動應用程式 toocache 和同步處理離線資料在您的 Cordova 應用程式"
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
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="f89ff-103">啟用 Cordova 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="f89ff-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="f89ff-104">本教學課程介紹 Cordova hello 離線的同步處理功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="f89ff-105">離線同步處理允許與行動裝置應用程式的終端使用者 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="f89ff-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="f89ff-106">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f89ff-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="f89ff-107">Hello 裝置已上線，一旦這些變更會與 hello 遠端服務進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="f89ff-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="f89ff-108">本教學課程根據 hello Cordova 快速入門解決方案的行動應用程式，當您完成時，您建立 hello 教學課程[Apache Cordova 快速入門]。</span><span class="sxs-lookup"><span data-stu-id="f89ff-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="f89ff-109">在本教學課程中，您可以更新 hello 快速入門方案 tooadd 離線功能的 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="f89ff-110">我們也反白 hello 應用程式中的 hello 離線特定程式碼。</span><span class="sxs-lookup"><span data-stu-id="f89ff-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="f89ff-111">toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="f89ff-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="f89ff-112">如需的應用程式開發介面使用方式的詳細資訊，請參閱 hello [API 文件](https://azure.github.io/azure-mobile-apps-js-client)。</span><span class="sxs-lookup"><span data-stu-id="f89ff-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="f89ff-113">新增離線同步 toohello 快速入門解決方案</span><span class="sxs-lookup"><span data-stu-id="f89ff-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="f89ff-114">toohello 應用程式，必須加入 hello 離線同步處理程式碼。</span><span class="sxs-lookup"><span data-stu-id="f89ff-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="f89ff-115">離線同步處理需要 hello cordova sqlite 儲存體外掛程式會自動取得 tooyour 應用程式新增 hello 專案中包含 hello Azure 行動應用程式的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="f89ff-116">hello 快速入門專案包含兩個這些外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="f89ff-117">在 Visual Studio 方案總管 中，開啟 index.js，並取代下列程式碼的 hello</span><span class="sxs-lookup"><span data-stu-id="f89ff-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="f89ff-118">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="f89ff-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="f89ff-119">接下來，將下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f89ff-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="f89ff-120">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="f89ff-120">with this code:</span></span>

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

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="f89ff-121">hello 上述程式碼加入初始化 hello 本機存放區並將符合 hello 所使用的資料行值的本機資料表定義在您的 Azure 後端。</span><span class="sxs-lookup"><span data-stu-id="f89ff-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="f89ff-122">（您不需要 tooinclude 這個程式碼中的所有資料行值。） hello`version`欄位由 hello 行動後端維護和用來解決衝突。</span><span class="sxs-lookup"><span data-stu-id="f89ff-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="f89ff-123">您藉由呼叫取得參考 toohello 同步處理內容**getSyncContext**。</span><span class="sxs-lookup"><span data-stu-id="f89ff-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="f89ff-124">hello 同步處理內容可以藉由追蹤，並將變更推入用戶端應用程式有修改時的所有資料表中保留資料表關聯性`.push()`呼叫。</span><span class="sxs-lookup"><span data-stu-id="f89ff-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="f89ff-125">更新 hello 應用程式 URL tooyour 行動裝置應用程式的應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f89ff-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="f89ff-126">接下來，將此程式碼：</span><span class="sxs-lookup"><span data-stu-id="f89ff-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="f89ff-127">取代為此程式碼：</span><span class="sxs-lookup"><span data-stu-id="f89ff-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="f89ff-128">hello 上述程式碼初始化 hello 同步處理內容，然後呼叫 （而不是 getTable) getSyncTable tooget 參考 toohello 本機資料表。</span><span class="sxs-lookup"><span data-stu-id="f89ff-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="f89ff-129">此程式碼會使用 hello 本機資料庫所有建立、 讀取、 更新和刪除 (CRUD) 資料表的作業。</span><span class="sxs-lookup"><span data-stu-id="f89ff-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="f89ff-130">這個範例會對同步處理衝突執行簡單的錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="f89ff-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="f89ff-131">實際的應用程式會處理 hello 如網路狀況、 伺服器衝突，以及其他各種錯誤。</span><span class="sxs-lookup"><span data-stu-id="f89ff-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="f89ff-132">如需程式碼範例，請參閱 hello[離線同步處理範例]。</span><span class="sxs-lookup"><span data-stu-id="f89ff-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="f89ff-133">接著，將此函式 tooperform hello 實際同步作業。</span><span class="sxs-lookup"><span data-stu-id="f89ff-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="f89ff-134">您可以決定當 toopush 變更 toohello 行動裝置應用程式後端藉由呼叫**syncContext.push()**。</span><span class="sxs-lookup"><span data-stu-id="f89ff-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="f89ff-135">例如，您可以呼叫**syncBackend**按鈕事件處理常式繫結的 tooa 同步處理按鈕中。</span><span class="sxs-lookup"><span data-stu-id="f89ff-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="f89ff-136">離線同步處理考量</span><span class="sxs-lookup"><span data-stu-id="f89ff-136">Offline sync considerations</span></span>

<span data-ttu-id="f89ff-137">在 hello 範例中，hello**發送**方法**syncContext**只會在應用程式啟動時在 hello 登入的回呼函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="f89ff-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="f89ff-138">在真實世界應用程式中，您也可以將手動觸發此同步處理功能或 hello 網路狀態變更時。</span><span class="sxs-lookup"><span data-stu-id="f89ff-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="f89ff-139">針對具有暫止的資料表執行提取本機更新追蹤推入 hello 內容，提取作業會自動觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f89ff-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="f89ff-140">當重新整理、 新增和完成項目在此範例中，您可以省略 hello 明確**發送**呼叫，因為它可能會重複。</span><span class="sxs-lookup"><span data-stu-id="f89ff-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="f89ff-141">Hello 提供程式碼中，查詢 hello 遠端 todoItem 資料表中的所有記錄，但也可能 toofilter 記錄藉由傳遞查詢識別碼和查詢太**發送**。</span><span class="sxs-lookup"><span data-stu-id="f89ff-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="f89ff-142">如需詳細資訊，請參閱 hello 節*增量同步處理*中[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="f89ff-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="f89ff-143">(選擇性) 停用驗證</span><span class="sxs-lookup"><span data-stu-id="f89ff-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="f89ff-144">如果您不想 tooset 總測試離線同步處理之前驗證、 註解 hello 回呼函式登入，但保留 hello 內的程式碼取消註解 hello 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="f89ff-145">標記為註解 hello 登入行之後, hello 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="f89ff-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="f89ff-146">現在，hello 以 hello Azure 後端，當您執行 hello 應用程式的應用程式同步處理。</span><span class="sxs-lookup"><span data-stu-id="f89ff-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="f89ff-147">執行 hello 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="f89ff-147">Run hello client app</span></span>
<span data-ttu-id="f89ff-148">現在已啟用 離線同步處理的情況下，您可以使用執行 hello 用戶端應用程式至少一次，hello 本機存放區資料庫中填入每個平台上。</span><span class="sxs-lookup"><span data-stu-id="f89ff-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="f89ff-149">更新版本中，模擬離線案例中，並修改 hello 本機存放區中的 hello 資料 hello 應用程式處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="f89ff-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="f89ff-150">（選擇性）測試 hello 同步處理行為</span><span class="sxs-lookup"><span data-stu-id="f89ff-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="f89ff-151">本節中，在中，您可以修改 hello 用戶端專案 toosimulate 離線案例中為您的後端使用無效的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="f89ff-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="f89ff-152">當您新增或變更資料的項目時，這些變更會保留在本機存放區中，但不同步的 toohello 後端資料存放區，直到 hello 連接重新建立。</span><span class="sxs-lookup"><span data-stu-id="f89ff-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="f89ff-153">在 [hello 方案總管] 中，開啟 hello index.js 專案檔並將變更 hello 應用程式 URL toopoint 無效的 URL，如下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f89ff-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="f89ff-154">在 index.html 中，更新 hello CSP`<meta>`元素與 hello 相同的 URL 無效。</span><span class="sxs-lookup"><span data-stu-id="f89ff-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="f89ff-155">建置和執行 hello 用戶端應用程式，請注意 hello 應用程式嘗試登入之後的同步處理與 hello 後端時，會在 hello 主控台記錄例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f89ff-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="f89ff-156">您新增任何新項目存在於 hello 本機存放區，直到它們會推入 toohello 行動後端。</span><span class="sxs-lookup"><span data-stu-id="f89ff-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="f89ff-157">hello 用戶端應用程式行為就如同它是連接的 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="f89ff-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="f89ff-158">關閉 hello 應用程式並重新啟動它 tooverify hello 您所建立的新項目會保存的 toohello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="f89ff-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="f89ff-159">（選擇性）使用 Visual Studio tooview hello 後端資料庫中的 hello 資料尚未變更您 Azure SQL Database 資料表 toosee。</span><span class="sxs-lookup"><span data-stu-id="f89ff-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="f89ff-160">在 Visual Studio 中，開啟 [伺服器總管] 。</span><span class="sxs-lookup"><span data-stu-id="f89ff-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="f89ff-161">瀏覽 tooyour 資料庫**Azure**->**SQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="f89ff-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="f89ff-162">在資料庫上按一下滑鼠右鍵，並選取 [在 SQL Server 物件總管中開啟] 。</span><span class="sxs-lookup"><span data-stu-id="f89ff-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="f89ff-163">現在您可以瀏覽 tooyour SQL 資料庫資料表和其內容。</span><span class="sxs-lookup"><span data-stu-id="f89ff-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="f89ff-164">（選擇性）測試 hello 重新連線 tooyour 行動後端</span><span class="sxs-lookup"><span data-stu-id="f89ff-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="f89ff-165">本節中，在您重新連線 hello 應用程式 toohello 行動後端，這將模擬 hello 應用程式回到線上狀態。</span><span class="sxs-lookup"><span data-stu-id="f89ff-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="f89ff-166">當您登入時，資料將會同步處理的 tooyour 行動後端。</span><span class="sxs-lookup"><span data-stu-id="f89ff-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="f89ff-167">重新開啟 index.js，並還原 hello 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="f89ff-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="f89ff-168">重新開啟 index.html，並更正 hello 應用程式 URL 在 hello CSP`<meta>`項目。</span><span class="sxs-lookup"><span data-stu-id="f89ff-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="f89ff-169">重新建置並執行 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f89ff-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="f89ff-170">與 hello 登入之後的行動裝置應用程式後端應用程式嘗試 toosync hello。</span><span class="sxs-lookup"><span data-stu-id="f89ff-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="f89ff-171">請確認在 hello 偵錯主控台也會記錄任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f89ff-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="f89ff-172">（選擇性）檢視 hello 更新的資料使用 SQL Server 物件總管 或 Fiddler 等其他工具。</span><span class="sxs-lookup"><span data-stu-id="f89ff-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="f89ff-173">請注意 hello 資料已同步處理 hello 後端資料庫與 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="f89ff-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="f89ff-174">請注意 hello 資料已同步處理 hello 資料庫與 hello 本機存放區，並包含您加入您的應用程式已中斷連接時的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="f89ff-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f89ff-175">其他資源</span><span class="sxs-lookup"><span data-stu-id="f89ff-175">Additional resources</span></span>
* <span data-ttu-id="f89ff-176">[Azure 行動應用程式中的離線資料同步]</span><span class="sxs-lookup"><span data-stu-id="f89ff-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="f89ff-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="f89ff-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="f89ff-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f89ff-178">Next steps</span></span>
* <span data-ttu-id="f89ff-179">檢閱更進階的離線同步處理功能，例如衝突解決中 hello[離線同步處理範例]</span><span class="sxs-lookup"><span data-stu-id="f89ff-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="f89ff-180">檢閱 hello 離線同步處理應用程式開發介面參考在 hello [API 文件](https://azure.github.io/azure-mobile-apps-js-client)。</span><span class="sxs-lookup"><span data-stu-id="f89ff-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[Apache Cordova 快速入門]: app-service-mobile-cordova-get-started.md
[離線同步處理範例]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Azure 行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
