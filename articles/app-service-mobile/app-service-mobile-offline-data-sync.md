---
title: "aaaOffline Azure 行動應用程式中的資料同步 |Microsoft 文件"
description: "概念式的參考和 Azure 行動應用程式的 hello 離線資料同步處理功能的概觀"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Azure 行動應用程式中的離線資料同步處理
## <a name="what-is-offline-data-sync"></a>什麼是離線資料同步處理？
離線資料同步處理是用戶端和伺服器的 Azure 行動應用程式，以簡化開發人員不需要網路連線正常運作的 toocreate 應用程式的 SDK 功能。

當您的應用程式處於離線模式時，仍可以建立及修改儲存 tooa 本機存放區的資料。 Hello 應用程式再度上線時，它可以與您的 Azure 行動應用程式後端同步處理本機變更。 hello 功能也包含支援同時變更同一筆記錄的 hello hello 用戶端與 hello 後端時，偵測衝突。 在伺服器 hello 或 hello 用戶端可以處理衝突。

離線同步處理有幾項優點：

* 透過快取伺服器 hello 裝置本機上的資料來改善應用程式的回應
* 建立當網路有問題時仍可以使用的健全應用程式。
* 讓終端使用者 toocreate 和修改資料，即使在沒有網路存取權，幾乎沒有任何連線以支援案例
* 跨多個裝置同步處理的資料和 hello 相同記錄而修改時兩個裝置偵測衝突
* 高延遲或計量付費網路的網路使用限制。

hello 遵循教學課程顯示如何離線 tooadd 同步 tooyour 行動用戶端使用 Azure 行動應用程式：

* [Android：啟用離線同步處理]
* [Apache Cordova︰啟用離線同步處理](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS：啟用離線同步處理]
* [Xamarin iOS：啟用離線同步處理]
* [Xamarin Android：啟用離線同步處理]
* [Xamarin.Forms：啟用離線同步處理](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [通用 Windows 平台︰啟用離線同步處理]

## <a name="what-is-a-sync-table"></a>什麼是同步處理資料表？
tooaccess hello"/ 資料表 」 的端點，hello Azure 行動用戶端 Sdk 提供介面，例如`IMobileServiceTable`（.NET 用戶端 SDK） 或`MSTable`（iOS 用戶端）。 這些應用程式開發介面直接連接 toohello Azure 行動應用程式後端，而且如果 hello 用戶端裝置沒有網路連線失敗。

toosupport 離線使用，您的應用程式應該改用 hello*同步處理資料表*應用程式開發介面，例如`IMobileServiceSyncTable`（.NET 用戶端 SDK） 或`MSSyncTable`（iOS 用戶端）。 針對同步處理相同 CRUD 作業 （建立、 讀取、 更新、 刪除） 的所有 hello 資料表應用程式開發介面，除了現在它們讀取或寫入 tooa*本機存放區*。 在執行任何同步處理的資料表作業之前，必須先初始化 hello 本機存放區。

## <a name="what-is-a-local-store"></a>什麼是本機存放區？
本機存放區是 hello 的資料持久層 hello 用戶端裝置上。 hello Azure 行動應用程式用戶端 Sdk 提供的預設本機存放區實作。 在 Windows、Xamarin 和 Android 上，它是以 SQLite 為基礎。 在 iOS 上，它是以 Core Data 為基礎。

toouse hello SQLite 型實作 Windows Phone 或 Windows 市集 8.1，您需要 tooinstall SQLite 延伸模組。 如需詳細資訊，請參閱[通用 Windows 平台︰啟用離線同步處理]。Android 和 iOS 隨附的 SQLite 中 hello 裝置作業系統本身，所以不需要 tooreference SQLite 自己版本的版本。

開發人員也可以實作自己的本機存放區。 比方說，如果您想 toostore 資料以加密格式 hello 行動用戶端上，您可以定義使用 SQLCipher 進行加密的本機存放區。

## <a name="what-is-a-sync-context"></a>什麼是同步處理內容？
「同步處理內容」會與行動用戶端物件相關聯 (例如 `IMobileServiceClient` 或 `MSClient`)，並且追蹤對同步處理資料表所做的變更。 hello 同步處理內容會維持*作業佇列*，該物件保存 CUD 作業 (Create、 Update、 Delete) 的已排序的清單稍後傳送 toohello 伺服器。

本機存放區都與 hello 同步處理內容，例如使用 initialize 方法`IMobileServicesSyncContext.InitializeAsync(localstore)`在 hello [.NET 用戶端 SDK]。

## <a name="how-sync-works"></a>離線同步處理如何運作
使用同步處理資料表時，您的用戶端程式碼需要控制本機變更與 Azure 行動應用程式後端同步處理的時機。 不會傳送 toohello 後端，直到有太呼叫*發送*本機變更。 同樣地，hello 本機存放區會填入新的資料時，才呼叫太*提取*資料。

* **推入**： 推播是 hello 同步處理內容上的操作，因為 hello 最後一個推播傳送所有 CUD 變更。 請注意它，所以不可能 toosend 只有個別資料表的變更，否則作業可能會傳送順序。 推入執行一系列的 REST 呼叫 tooyour Azure 行動應用程式後端，進而又修改伺服器資料庫。
* **提取**： 提取執行每個資料表為基礎，而且可以是自訂查詢 tooretrieve hello 伺服器資料的子集。 hello Azure 行動用戶端 Sdk，然後插入 hello 本機存放區中的 hello 產生的資料。
* **隱含的推播通知**: hello 提取針對具有暫止的本機更新的資料表執行提取時，如果第一次執行`push()`hello 同步處理內容上。 此 push 有助於減少已排入佇列的變更和新的資料，從 hello 伺服器之間的衝突。
* **增量同步處理**: hello 第一個參數 toohello 提取作業*查詢名稱*，只適用於 hello 用戶端。 如果您使用非 null 的查詢名稱，就會執行 hello Azure Mobile SDK*增量同步處理*。每次提取作業會傳回一組結果，最新 hello `updatedAt` hello SDK 本機系統資料表中儲存該結果集內的時間戳記。 後續的提取作業只會擷取該時間戳記之後的記錄。

  toouse 增量同步處理您的伺服器必須傳回有意義`updatedAt`值，並且也必須支援依此欄位排序。 不過，由於 hello SDK hello updatedAt 欄位加入自己的排序，您無法使用有它自己的提取查詢`orderBy`子句。

  hello 查詢名稱可以是任何字串您選擇，但必須是唯一的應用程式中的每個邏輯查詢。
  否則，不同的提取作業可能會覆寫 hello 相同的增量同步處理時間戳記和您的查詢可以傳回不正確的結果。

  如果 hello 查詢的參數，其中一種方式 toocreate 是唯一的查詢名稱 tooincorporate hello 參數值。
  例如，如果您要篩選 userid，您的查詢名稱可能如下 (在 C# 中)：

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  如果您想要 tooopt 超出增量同步處理時，傳遞`null`如 hello 的查詢識別碼。 在此情況下，會擷取所有記錄在每次呼叫太`PullAsync`，這是可能會沒有效率。
* **清除**： 您可以清除 hello 本機存放區使用的 hello 內容`IMobileServiceSyncTable.PurgeAsync`。
  清除可能需要有過時的資料在 hello 用戶端資料庫中，或如果您想 toodiscard 所有暫止的變更。

  清除清除 hello 本機存放區中的資料表。 如果有作業正在等待同步處理與 hello server 資料庫，hello 清除擲回例外狀況，除非 hello*強制清除*參數設定。

  例如 hello 用戶端上的過時資料中，假設在 hello 「 todo 清單 」 範例中，Device1 只會提取未完成的項目。 Todoitem"買牛奶"標示為另一個裝置 hello 伺服器上完成。 不過，Device1 仍有的 hello 本機存放區中的 「 購買牛奶 」 todoitem 因為它只會提取項目，則不標示為完成。 清除作業會清除這個過時項目。

## <a name="next-steps"></a>後續步驟
* [iOS：啟用離線同步處理]
* [Xamarin iOS：啟用離線同步處理]
* [Xamarin Android：啟用離線同步處理]
* [通用 Windows 平台︰啟用離線同步處理]

<!-- Links -->
[.NET 用戶端 SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android：啟用離線同步處理]: app-service-mobile-android-get-started-offline-data.md
[iOS：啟用離線同步處理]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS：啟用離線同步處理]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android：啟用離線同步處理]: app-service-mobile-xamarin-android-get-started-offline-data.md
[通用 Windows 平台︰啟用離線同步處理]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
