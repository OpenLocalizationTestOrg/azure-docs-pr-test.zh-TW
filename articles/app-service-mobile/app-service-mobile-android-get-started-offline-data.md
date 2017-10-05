---
title: "啟用 Azure 行動應用程式的離線同步處理 (Android)"
description: "了解如何使用 App Service Mobile Apps 來快取和同步處理離線資料"
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="53d66-103">啟用 Android 行動應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="53d66-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="53d66-104">概觀</span><span class="sxs-lookup"><span data-stu-id="53d66-104">Overview</span></span>
<span data-ttu-id="53d66-105">本教學課程說明 Android 之 Azure Mobile Apps 的離線同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="53d66-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="53d66-106">離線同步處理可讓使用者與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連接進也可行。</span><span class="sxs-lookup"><span data-stu-id="53d66-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="53d66-107">變更會儲存在本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="53d66-107">Changes are stored in a local database.</span></span> <span data-ttu-id="53d66-108">裝置恢復上線後，這些變更就會與遠端後端進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="53d66-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="53d66-109">如果這是您第一次接觸 Azure Mobile Apps，您應先完成 [建立 Android 應用程式]教學課程。</span><span class="sxs-lookup"><span data-stu-id="53d66-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="53d66-110">如果您不要使用下載的快速入門伺服器專案，必須將資料存取擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="53d66-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="53d66-111">如需伺服器擴充套件的詳細資訊，請參閱 [使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="53d66-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="53d66-112">若要深入了解離線同步處理功能，請參閱 [Azure Mobile Apps 中的離線資料同步處理]主題。</span><span class="sxs-lookup"><span data-stu-id="53d66-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="53d66-113">更新應用程式以支援離線同步</span><span class="sxs-lookup"><span data-stu-id="53d66-113">Update the app to support offline sync</span></span>
<span data-ttu-id="53d66-114">利用離線同步讀取和寫入*同步資料表* (使用 *IMobileServiceSyncTable* 介面)，這是您裝置上 **SQLite** 資料庫的一部分。</span><span class="sxs-lookup"><span data-stu-id="53d66-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="53d66-115">若要推送和提取裝置與 Azure 行動服務之間的變更，您可使用*同步處理內容* (*MobileServiceClient.SyncContext*)，這是您用來在本機儲存資料的本機資料庫所初始化。</span><span class="sxs-lookup"><span data-stu-id="53d66-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="53d66-116">在 `TodoActivity.java` 中，將 `mToDoTable` 的現有定義註解化，並取消註解同步資料表版本：</span><span class="sxs-lookup"><span data-stu-id="53d66-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="53d66-117">在 `onCreate` 方法中，將 `mToDoTable` 的現有初始化註解化，並取消註解此定義：</span><span class="sxs-lookup"><span data-stu-id="53d66-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="53d66-118">在 `refreshItemsFromTable` 中，將 `results` 的定義註解化，並取消註解此定義：</span><span class="sxs-lookup"><span data-stu-id="53d66-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="53d66-119">註解化 `refreshItemsFromMobileServiceTable`的定義。</span><span class="sxs-lookup"><span data-stu-id="53d66-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="53d66-120">取消註解 `refreshItemsFromMobileServiceTableSyncTable`的定義：</span><span class="sxs-lookup"><span data-stu-id="53d66-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="53d66-121">取消註解 `sync`的定義：</span><span class="sxs-lookup"><span data-stu-id="53d66-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="53d66-122">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="53d66-122">Test the app</span></span>
<span data-ttu-id="53d66-123">在本節中，您會在開啟 WiFi 的情況下測試行為，然後關閉 WiFi 以建立離線案例。</span><span class="sxs-lookup"><span data-stu-id="53d66-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="53d66-124">當您新增資料項目時，這些項目會存放在本機 SQLite 存放區中，但直到您按 [重新整理]  按鈕時才會同步處理至行動服務。</span><span class="sxs-lookup"><span data-stu-id="53d66-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="53d66-125">對於何時需要同步處理資料，其他應用程式可能會有不同的需求，但是為了示範目的，本教學課程讓使用者明確要求。</span><span class="sxs-lookup"><span data-stu-id="53d66-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="53d66-126">當您按下該按鈕時，新的背景工作會啟動。</span><span class="sxs-lookup"><span data-stu-id="53d66-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="53d66-127">它會使用同步處理內容先推送對本機存放區做的所有變更，然後將所有變更的資料從 Azure 提取至本機資料表。</span><span class="sxs-lookup"><span data-stu-id="53d66-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="53d66-128">離線測試</span><span class="sxs-lookup"><span data-stu-id="53d66-128">Offline testing</span></span>
1. <span data-ttu-id="53d66-129">讓裝置或模擬器處於「飛航模式」 。</span><span class="sxs-lookup"><span data-stu-id="53d66-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="53d66-130">這會建立離線案例。</span><span class="sxs-lookup"><span data-stu-id="53d66-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="53d66-131">新增一些 *ToDo* 項目，或將某些項目標示為完成。</span><span class="sxs-lookup"><span data-stu-id="53d66-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="53d66-132">結束裝置或模擬器 (或強制關閉應用程式)，然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="53d66-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="53d66-133">請確認您的變更已保存在裝置上，因為它們會保留在本機 SQLite 存放區中。</span><span class="sxs-lookup"><span data-stu-id="53d66-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="53d66-134">使用 SQL 工具 (如 *SQL Server Management Studio*) 或 REST 用戶端 (如 *Fiddler* 或 *Postman*) 檢視 Azure *TodoItem* 資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="53d66-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="53d66-135">請確認新項目「尚未」  同步處理到伺服器</span><span class="sxs-lookup"><span data-stu-id="53d66-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="53d66-136">若為 Node.js 後端，請移至 [Azure 入口網站](https://portal.azure.com/)，在您的行動應用程式後端中按一下 [簡單資料表] > [TodoItem]，檢視 `TodoItem` 資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="53d66-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="53d66-137">若為 .NET 後端，請使用 SQL 工具 (例如 *SQL Server Management Studio*) 或 REST 用戶端 (例如 *Fiddler* 或 *Postman*) 檢視資料表內容。</span><span class="sxs-lookup"><span data-stu-id="53d66-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="53d66-138">在裝置或模擬器中開啟 WiFi。</span><span class="sxs-lookup"><span data-stu-id="53d66-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="53d66-139">接著，按 [重新整理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="53d66-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="53d66-140">在 Azure 入口網站中，再次檢視 TodoItem 資料。</span><span class="sxs-lookup"><span data-stu-id="53d66-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="53d66-141">新的和變更的 TodoItems 現在應該會出現。</span><span class="sxs-lookup"><span data-stu-id="53d66-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53d66-142">其他資源</span><span class="sxs-lookup"><span data-stu-id="53d66-142">Additional Resources</span></span>
* <span data-ttu-id="53d66-143">[Azure Mobile Apps 中的離線資料同步處理]</span><span class="sxs-lookup"><span data-stu-id="53d66-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="53d66-144">[雲端報導：Azure Mobile Services 中的離線同步處理] \(注意：影片位於 Mobile Services 上，但離線同步處理的運作方式類似在 Azure Mobile Apps 中的方式\)</span><span class="sxs-lookup"><span data-stu-id="53d66-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="53d66-145">[Azure Mobile Apps 中的離線資料同步處理]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="53d66-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="53d66-146">[建立 Android 應用程式]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="53d66-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="53d66-147">[雲端報導：Azure Mobile Services 中的離線同步處理]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="53d66-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

