---
title: "aaaEnable 離線同步處理您的 Azure 行動應用程式 (Android)"
description: "深入了解如何 toouse App Service Mobile App toocache 和同步處理離線資料 Android 應用程式中"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="c2be5-103">啟用 Android 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="c2be5-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="c2be5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c2be5-104">Overview</span></span>
<span data-ttu-id="c2be5-105">本教學課程涵蓋 Android 的 Azure 行動應用程式的 hello 離線同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="c2be5-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="c2be5-106">離線同步處理允許與行動裝置應用程式的終端使用者 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="c2be5-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="c2be5-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="c2be5-107">Changes are stored in a local database.</span></span> <span data-ttu-id="c2be5-108">Hello 裝置已上線，一旦這些變更同步處理與 hello 遠端後端中。</span><span class="sxs-lookup"><span data-stu-id="c2be5-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="c2be5-109">如果這是您首次經驗與 Azure 行動應用程式，您應該先完成 hello 教學課程[建立 Android 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c2be5-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="c2be5-110">如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 資料存取擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="c2be5-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="c2be5-111">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="c2be5-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="c2be5-112">toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="c2be5-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="c2be5-113">更新 hello 應用程式 toosupport 離線同步處理</span><span class="sxs-lookup"><span data-stu-id="c2be5-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="c2be5-114">離線同步時，您可以閱讀 tooand 寫入從*同步處理資料表*(使用 hello *IMobileServiceSyncTable*介面)，這是屬於**SQLite**在裝置上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c2be5-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="c2be5-115">hello 裝置與 Azure 行動服務之間 toopush 及提取變更，使用*同步處理內容*(*MobileServiceClient.SyncContext*)，其中您初始化 hello 本機資料庫toostore 資料儲存在本機。</span><span class="sxs-lookup"><span data-stu-id="c2be5-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="c2be5-116">在`TodoActivity.java`，註解的 hello 現有定義`mToDoTable`並取消註解 hello 的同步處理資料表版本：</span><span class="sxs-lookup"><span data-stu-id="c2be5-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="c2be5-117">在 hello`onCreate`方法，註解的 hello 現有初始化`mToDoTable`並取消註解此定義：</span><span class="sxs-lookup"><span data-stu-id="c2be5-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="c2be5-118">在`refreshItemsFromTable`註解的 hello 定義`results`並取消註解此定義：</span><span class="sxs-lookup"><span data-stu-id="c2be5-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="c2be5-119">註解的 hello 定義`refreshItemsFromMobileServiceTable`。</span><span class="sxs-lookup"><span data-stu-id="c2be5-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="c2be5-120">請取消註解的 hello 定義`refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="c2be5-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="c2be5-121">請取消註解的 hello 定義`sync`:</span><span class="sxs-lookup"><span data-stu-id="c2be5-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="c2be5-122">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2be5-122">Test hello app</span></span>
<span data-ttu-id="c2be5-123">在本節中，您會測試 WiFi hello 行為上，，，然後將 WiFi toocreate 關閉離線的案例。</span><span class="sxs-lookup"><span data-stu-id="c2be5-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="c2be5-124">當您將資料的項目時，它們會保留在 hello 本機 SQLite 存放區，但不是同步的 toohello 行動服務直到按 hello**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2be5-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="c2be5-125">其他應用程式可能會有不同的需求，關於資料必須 toobe 同步處理，但基於示範目的本教學課程 hello 使用者明確要求它。</span><span class="sxs-lookup"><span data-stu-id="c2be5-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="c2be5-126">當您按下該按鈕時，新的背景工作會啟動。</span><span class="sxs-lookup"><span data-stu-id="c2be5-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="c2be5-127">第一次將推送所有所做的變更 toohello 本機存放區同步處理內容，則提取所有變更資料從 Azure toohello 本機資料表使用。</span><span class="sxs-lookup"><span data-stu-id="c2be5-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="c2be5-128">離線測試</span><span class="sxs-lookup"><span data-stu-id="c2be5-128">Offline testing</span></span>
1. <span data-ttu-id="c2be5-129">位置 hello 裝置或模擬器中的*飛航模式*。</span><span class="sxs-lookup"><span data-stu-id="c2be5-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="c2be5-130">這會建立離線案例。</span><span class="sxs-lookup"><span data-stu-id="c2be5-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="c2be5-131">新增一些 *ToDo* 項目，或將某些項目標示為完成。</span><span class="sxs-lookup"><span data-stu-id="c2be5-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="c2be5-132">結束 hello 裝置或模擬器 （或強制關閉 hello 應用程式），然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c2be5-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="c2be5-133">確認，您的變更已經保存 hello 裝置上因為它們會保持 hello 本機 SQLite 存放區中。</span><span class="sxs-lookup"><span data-stu-id="c2be5-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="c2be5-134">檢視 hello Azure hello 內容*TodoItem*這類資料表是使用 SQL 工具*SQL Server Management Studio*，或之類的其他用戶端*Fiddler*或*郵差*。</span><span class="sxs-lookup"><span data-stu-id="c2be5-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="c2be5-135">請確認 hello 新項目有*不*已同步處理的 toohello 伺服器</span><span class="sxs-lookup"><span data-stu-id="c2be5-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="c2be5-136">Node.js 後端移 toohello [Azure 入口網站](https://portal.azure.com/)，在您的行動裝置應用程式後端按一下**簡單資料表** > **TodoItem** hello tooviewhello內容`TodoItem`資料表。</span><span class="sxs-lookup"><span data-stu-id="c2be5-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="c2be5-137">.NET 後端中，檢視 hello 資料表的內容是使用 SQL 工具例如*SQL Server Management Studio*，或之類的其他用戶端*Fiddler*或*郵差*。</span><span class="sxs-lookup"><span data-stu-id="c2be5-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="c2be5-138">開啟 WiFi hello 裝置或模擬器中。</span><span class="sxs-lookup"><span data-stu-id="c2be5-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="c2be5-139">接下來，請按 hello**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2be5-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="c2be5-140">再次檢視 hello TodoItem 資料 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c2be5-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="c2be5-141">現在應該會出現新的和變更 TodoItems hello。</span><span class="sxs-lookup"><span data-stu-id="c2be5-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2be5-142">其他資源</span><span class="sxs-lookup"><span data-stu-id="c2be5-142">Additional Resources</span></span>
* <span data-ttu-id="c2be5-143">[Azure 行動應用程式中的離線資料同步]</span><span class="sxs-lookup"><span data-stu-id="c2be5-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="c2be5-144">[雲端涵蓋： Azure Mobile Services 中的離線同步]\(附註： hello 視訊在行動服務中，但離線同步的運作方式類似的方式，在 Azure 行動應用程式\)</span><span class="sxs-lookup"><span data-stu-id="c2be5-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[Azure 行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md

[建立 Android 應用程式]: app-service-mobile-android-get-started.md

[雲端涵蓋： Azure Mobile Services 中的離線同步]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

