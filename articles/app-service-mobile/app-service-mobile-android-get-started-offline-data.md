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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>啟用 Android 行動應用程式的離線同步處理
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>概觀
本教學課程涵蓋 Android 的 Azure 行動應用程式的 hello 離線同步處理功能。 離線同步處理允許與行動裝置應用程式的終端使用者 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。 變更會儲存在本機資料庫中。 Hello 裝置已上線，一旦這些變更同步處理與 hello 遠端後端中。

如果這是您首次經驗與 Azure 行動應用程式，您應該先完成 hello 教學課程[建立 Android 應用程式]。 如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 資料存取擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

toolearn 進一步了解 hello 離線同步處理功能，請參閱 hello 主題[Azure 行動應用程式中的離線資料同步]。

## <a name="update-hello-app-toosupport-offline-sync"></a>更新 hello 應用程式 toosupport 離線同步處理
離線同步時，您可以閱讀 tooand 寫入從*同步處理資料表*(使用 hello *IMobileServiceSyncTable*介面)，這是屬於**SQLite**在裝置上的資料庫。

hello 裝置與 Azure 行動服務之間 toopush 及提取變更，使用*同步處理內容*(*MobileServiceClient.SyncContext*)，其中您初始化 hello 本機資料庫toostore 資料儲存在本機。

1. 在`TodoActivity.java`，註解的 hello 現有定義`mToDoTable`並取消註解 hello 的同步處理資料表版本：
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. 在 hello`onCreate`方法，註解的 hello 現有初始化`mToDoTable`並取消註解此定義：
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. 在`refreshItemsFromTable`註解的 hello 定義`results`並取消註解此定義：
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. 註解的 hello 定義`refreshItemsFromMobileServiceTable`。
5. 請取消註解的 hello 定義`refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. 請取消註解的 hello 定義`sync`:
   
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

## <a name="test-hello-app"></a>測試 hello 應用程式
在本節中，您會測試 WiFi hello 行為上，，，然後將 WiFi toocreate 關閉離線的案例。

當您將資料的項目時，它們會保留在 hello 本機 SQLite 存放區，但不是同步的 toohello 行動服務直到按 hello**重新整理** 按鈕。 其他應用程式可能會有不同的需求，關於資料必須 toobe 同步處理，但基於示範目的本教學課程 hello 使用者明確要求它。

當您按下該按鈕時，新的背景工作會啟動。 第一次將推送所有所做的變更 toohello 本機存放區同步處理內容，則提取所有變更資料從 Azure toohello 本機資料表使用。

### <a name="offline-testing"></a>離線測試
1. 位置 hello 裝置或模擬器中的*飛航模式*。 這會建立離線案例。
2. 新增一些 *ToDo* 項目，或將某些項目標示為完成。 結束 hello 裝置或模擬器 （或強制關閉 hello 應用程式），然後重新啟動。 確認，您的變更已經保存 hello 裝置上因為它們會保持 hello 本機 SQLite 存放區中。
3. 檢視 hello Azure hello 內容*TodoItem*這類資料表是使用 SQL 工具*SQL Server Management Studio*，或之類的其他用戶端*Fiddler*或*郵差*。 請確認 hello 新項目有*不*已同步處理的 toohello 伺服器
   
       + Node.js 後端移 toohello [Azure 入口網站](https://portal.azure.com/)，在您的行動裝置應用程式後端按一下**簡單資料表** > **TodoItem** hello tooviewhello內容`TodoItem`資料表。
       + .NET 後端中，檢視 hello 資料表的內容是使用 SQL 工具例如*SQL Server Management Studio*，或之類的其他用戶端*Fiddler*或*郵差*。
4. 開啟 WiFi hello 裝置或模擬器中。 接下來，請按 hello**重新整理** 按鈕。
5. 再次檢視 hello TodoItem 資料 hello Azure 入口網站中。 現在應該會出現新的和變更 TodoItems hello。

## <a name="additional-resources"></a>其他資源
* [Azure 行動應用程式中的離線資料同步]
* [雲端涵蓋： Azure Mobile Services 中的離線同步]\(附註： hello 視訊在行動服務中，但離線同步的運作方式類似的方式，在 Azure 行動應用程式\)

<!-- URLs. -->

[Azure 行動應用程式中的離線資料同步]: app-service-mobile-offline-data-sync.md

[建立 Android 應用程式]: app-service-mobile-android-get-started.md

[雲端涵蓋： Azure Mobile Services 中的離線同步]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

