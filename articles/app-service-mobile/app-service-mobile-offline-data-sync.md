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
# <a name="offline-data-sync-in-azure-mobile-apps"></a><span data-ttu-id="124da-103">Azure 行動應用程式中的離線資料同步處理</span><span class="sxs-lookup"><span data-stu-id="124da-103">Offline Data Sync in Azure Mobile Apps</span></span>
## <a name="what-is-offline-data-sync"></a><span data-ttu-id="124da-104">什麼是離線資料同步處理？</span><span class="sxs-lookup"><span data-stu-id="124da-104">What is offline data sync?</span></span>
<span data-ttu-id="124da-105">離線資料同步處理是用戶端和伺服器的 Azure 行動應用程式，以簡化開發人員不需要網路連線正常運作的 toocreate 應用程式的 SDK 功能。</span><span class="sxs-lookup"><span data-stu-id="124da-105">Offline data sync is a client and server SDK feature of Azure Mobile Apps that makes it easy for developers toocreate apps that are functional without a network connection.</span></span>

<span data-ttu-id="124da-106">當您的應用程式處於離線模式時，仍可以建立及修改儲存 tooa 本機存放區的資料。</span><span class="sxs-lookup"><span data-stu-id="124da-106">When your app is in offline mode, you can still create and modify data, which are saved tooa local store.</span></span> <span data-ttu-id="124da-107">Hello 應用程式再度上線時，它可以與您的 Azure 行動應用程式後端同步處理本機變更。</span><span class="sxs-lookup"><span data-stu-id="124da-107">When hello app is back online, it can synchronize local changes with your Azure Mobile App backend.</span></span> <span data-ttu-id="124da-108">hello 功能也包含支援同時變更同一筆記錄的 hello hello 用戶端與 hello 後端時，偵測衝突。</span><span class="sxs-lookup"><span data-stu-id="124da-108">hello feature also includes support for detecting conflicts when hello same record is changed on both hello client and hello backend.</span></span> <span data-ttu-id="124da-109">在伺服器 hello 或 hello 用戶端可以處理衝突。</span><span class="sxs-lookup"><span data-stu-id="124da-109">Conflicts can then be handled either on hello server or hello client.</span></span>

<span data-ttu-id="124da-110">離線同步處理有幾項優點：</span><span class="sxs-lookup"><span data-stu-id="124da-110">Offline sync has several benefits:</span></span>

* <span data-ttu-id="124da-111">透過快取伺服器 hello 裝置本機上的資料來改善應用程式的回應</span><span class="sxs-lookup"><span data-stu-id="124da-111">Improve app responsiveness by caching server data locally on hello device</span></span>
* <span data-ttu-id="124da-112">建立當網路有問題時仍可以使用的健全應用程式。</span><span class="sxs-lookup"><span data-stu-id="124da-112">Create robust apps that remain useful when there are network issues</span></span>
* <span data-ttu-id="124da-113">讓終端使用者 toocreate 和修改資料，即使在沒有網路存取權，幾乎沒有任何連線以支援案例</span><span class="sxs-lookup"><span data-stu-id="124da-113">Allow end users toocreate and modify data even when there is no network access, supporting scenarios with little or no connectivity</span></span>
* <span data-ttu-id="124da-114">跨多個裝置同步處理的資料和 hello 相同記錄而修改時兩個裝置偵測衝突</span><span class="sxs-lookup"><span data-stu-id="124da-114">Sync data across multiple devices and detect conflicts when hello same record is modified by two devices</span></span>
* <span data-ttu-id="124da-115">高延遲或計量付費網路的網路使用限制。</span><span class="sxs-lookup"><span data-stu-id="124da-115">Limit network use on high-latency or metered networks</span></span>

<span data-ttu-id="124da-116">hello 遵循教學課程顯示如何離線 tooadd 同步 tooyour 行動用戶端使用 Azure 行動應用程式：</span><span class="sxs-lookup"><span data-stu-id="124da-116">hello following tutorials show how tooadd offline sync tooyour mobile clients using Azure Mobile Apps:</span></span>

* <span data-ttu-id="124da-117">[Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-117">[Android: Enable offline sync]</span></span>
* [<span data-ttu-id="124da-118">Apache Cordova︰啟用離線同步處理</span><span class="sxs-lookup"><span data-stu-id="124da-118">Apache Cordova: Enable offline sync</span></span>](app-service-mobile-cordova-get-started-offline-data.md)
* <span data-ttu-id="124da-119">[iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-119">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="124da-120">[Xamarin iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-120">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="124da-121">[Xamarin Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-121">[Xamarin Android: Enable offline sync]</span></span>
* [<span data-ttu-id="124da-122">Xamarin.Forms：啟用離線同步處理</span><span class="sxs-lookup"><span data-stu-id="124da-122">Xamarin.Forms: Enable offline sync</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* <span data-ttu-id="124da-123">[通用 Windows 平台︰啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-123">[Universal Windows Platform: Enable offline sync]</span></span>

## <a name="what-is-a-sync-table"></a><span data-ttu-id="124da-124">什麼是同步處理資料表？</span><span class="sxs-lookup"><span data-stu-id="124da-124">What is a sync table?</span></span>
<span data-ttu-id="124da-125">tooaccess hello"/ 資料表 」 的端點，hello Azure 行動用戶端 Sdk 提供介面，例如`IMobileServiceTable`（.NET 用戶端 SDK） 或`MSTable`（iOS 用戶端）。</span><span class="sxs-lookup"><span data-stu-id="124da-125">tooaccess hello "/tables" endpoint, hello Azure Mobile client SDKs provide interfaces such as `IMobileServiceTable` (.NET client SDK) or `MSTable` (iOS client).</span></span> <span data-ttu-id="124da-126">這些應用程式開發介面直接連接 toohello Azure 行動應用程式後端，而且如果 hello 用戶端裝置沒有網路連線失敗。</span><span class="sxs-lookup"><span data-stu-id="124da-126">These APIs connect directly toohello Azure Mobile App backend and fail if hello client device does not have a network connection.</span></span>

<span data-ttu-id="124da-127">toosupport 離線使用，您的應用程式應該改用 hello*同步處理資料表*應用程式開發介面，例如`IMobileServiceSyncTable`（.NET 用戶端 SDK） 或`MSSyncTable`（iOS 用戶端）。</span><span class="sxs-lookup"><span data-stu-id="124da-127">toosupport offline use, your app should instead use hello *sync table* APIs, such as `IMobileServiceSyncTable` (.NET client SDK) or `MSSyncTable` (iOS client).</span></span> <span data-ttu-id="124da-128">針對同步處理相同 CRUD 作業 （建立、 讀取、 更新、 刪除） 的所有 hello 資料表應用程式開發介面，除了現在它們讀取或寫入 tooa*本機存放區*。</span><span class="sxs-lookup"><span data-stu-id="124da-128">All hello same CRUD operations (Create, Read, Update, Delete) work against sync table APIs, except now they read from or write tooa *local store*.</span></span> <span data-ttu-id="124da-129">在執行任何同步處理的資料表作業之前，必須先初始化 hello 本機存放區。</span><span class="sxs-lookup"><span data-stu-id="124da-129">Before any sync table operations can be performed, hello local store must be initialized.</span></span>

## <a name="what-is-a-local-store"></a><span data-ttu-id="124da-130">什麼是本機存放區？</span><span class="sxs-lookup"><span data-stu-id="124da-130">What is a local store?</span></span>
<span data-ttu-id="124da-131">本機存放區是 hello 的資料持久層 hello 用戶端裝置上。</span><span class="sxs-lookup"><span data-stu-id="124da-131">A local store is hello data persistence layer on hello client device.</span></span> <span data-ttu-id="124da-132">hello Azure 行動應用程式用戶端 Sdk 提供的預設本機存放區實作。</span><span class="sxs-lookup"><span data-stu-id="124da-132">hello Azure Mobile Apps client SDKs provide a default local store implementation.</span></span> <span data-ttu-id="124da-133">在 Windows、Xamarin 和 Android 上，它是以 SQLite 為基礎。</span><span class="sxs-lookup"><span data-stu-id="124da-133">On Windows, Xamarin and Android, it is based on SQLite.</span></span> <span data-ttu-id="124da-134">在 iOS 上，它是以 Core Data 為基礎。</span><span class="sxs-lookup"><span data-stu-id="124da-134">On iOS, it is based on Core Data.</span></span>

<span data-ttu-id="124da-135">toouse hello SQLite 型實作 Windows Phone 或 Windows 市集 8.1，您需要 tooinstall SQLite 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="124da-135">toouse hello SQLite-based implementation on Windows Phone or Windows Store 8.1, you need tooinstall a SQLite extension.</span></span> <span data-ttu-id="124da-136">如需詳細資訊，請參閱[通用 Windows 平台︰啟用離線同步處理]。Android 和 iOS 隨附的 SQLite 中 hello 裝置作業系統本身，所以不需要 tooreference SQLite 自己版本的版本。</span><span class="sxs-lookup"><span data-stu-id="124da-136">For more information, see [Universal Windows Platform: Enable offline sync]. Android and iOS ship with a version of SQLite in hello device operating system itself, so it is not necessary tooreference your own version of SQLite.</span></span>

<span data-ttu-id="124da-137">開發人員也可以實作自己的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="124da-137">Developers can also implement their own local store.</span></span> <span data-ttu-id="124da-138">比方說，如果您想 toostore 資料以加密格式 hello 行動用戶端上，您可以定義使用 SQLCipher 進行加密的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="124da-138">For instance, if you wish toostore data in an encrypted format on hello mobile client, you can define a local store that uses SQLCipher for encryption.</span></span>

## <a name="what-is-a-sync-context"></a><span data-ttu-id="124da-139">什麼是同步處理內容？</span><span class="sxs-lookup"><span data-stu-id="124da-139">What is a sync context?</span></span>
<span data-ttu-id="124da-140">「同步處理內容」會與行動用戶端物件相關聯 (例如 `IMobileServiceClient` 或 `MSClient`)，並且追蹤對同步處理資料表所做的變更。</span><span class="sxs-lookup"><span data-stu-id="124da-140">A *sync context* is associated with a mobile client object (such as `IMobileServiceClient` or `MSClient`) and tracks changes that are made with sync tables.</span></span> <span data-ttu-id="124da-141">hello 同步處理內容會維持*作業佇列*，該物件保存 CUD 作業 (Create、 Update、 Delete) 的已排序的清單稍後傳送 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="124da-141">hello sync context maintains an *operation queue*, which keeps an ordered list of CUD operations (Create, Update, Delete) that is later be sent toohello server.</span></span>

<span data-ttu-id="124da-142">本機存放區都與 hello 同步處理內容，例如使用 initialize 方法`IMobileServicesSyncContext.InitializeAsync(localstore)`在 hello [.NET 用戶端 SDK]。</span><span class="sxs-lookup"><span data-stu-id="124da-142">A local store is associated with hello sync context using an initialize method such as `IMobileServicesSyncContext.InitializeAsync(localstore)` in hello [.NET client SDK].</span></span>

## <span data-ttu-id="124da-143"><a name="how-sync-works"></a>離線同步處理如何運作</span><span class="sxs-lookup"><span data-stu-id="124da-143"><a name="how-sync-works"></a>How offline synchronization works</span></span>
<span data-ttu-id="124da-144">使用同步處理資料表時，您的用戶端程式碼需要控制本機變更與 Azure 行動應用程式後端同步處理的時機。</span><span class="sxs-lookup"><span data-stu-id="124da-144">When using sync tables, your client code controls when local changes are synchronized with an Azure Mobile App backend.</span></span> <span data-ttu-id="124da-145">不會傳送 toohello 後端，直到有太呼叫*發送*本機變更。</span><span class="sxs-lookup"><span data-stu-id="124da-145">Nothing is sent toohello backend until there is a call too*push* local changes.</span></span> <span data-ttu-id="124da-146">同樣地，hello 本機存放區會填入新的資料時，才呼叫太*提取*資料。</span><span class="sxs-lookup"><span data-stu-id="124da-146">Similarly, hello local store is populated with new data only when there is a call too*pull* data.</span></span>

* <span data-ttu-id="124da-147">**推入**： 推播是 hello 同步處理內容上的操作，因為 hello 最後一個推播傳送所有 CUD 變更。</span><span class="sxs-lookup"><span data-stu-id="124da-147">**Push**: Push is an operation on hello sync context and sends all CUD changes since hello last push.</span></span> <span data-ttu-id="124da-148">請注意它，所以不可能 toosend 只有個別資料表的變更，否則作業可能會傳送順序。</span><span class="sxs-lookup"><span data-stu-id="124da-148">Note that it is not possible toosend only an individual table's changes, because otherwise operations could be sent out of order.</span></span> <span data-ttu-id="124da-149">推入執行一系列的 REST 呼叫 tooyour Azure 行動應用程式後端，進而又修改伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="124da-149">Push executes a series of REST calls tooyour Azure Mobile App backend, which in turn modifies your server database.</span></span>
* <span data-ttu-id="124da-150">**提取**： 提取執行每個資料表為基礎，而且可以是自訂查詢 tooretrieve hello 伺服器資料的子集。</span><span class="sxs-lookup"><span data-stu-id="124da-150">**Pull**: Pull is performed on a per-table basis and can be customized with a query tooretrieve only a subset of hello server data.</span></span> <span data-ttu-id="124da-151">hello Azure 行動用戶端 Sdk，然後插入 hello 本機存放區中的 hello 產生的資料。</span><span class="sxs-lookup"><span data-stu-id="124da-151">hello Azure Mobile client SDKs then insert hello resulting data into hello local store.</span></span>
* <span data-ttu-id="124da-152">**隱含的推播通知**: hello 提取針對具有暫止的本機更新的資料表執行提取時，如果第一次執行`push()`hello 同步處理內容上。</span><span class="sxs-lookup"><span data-stu-id="124da-152">**Implicit Pushes**: If a pull is executed against a table that has pending local updates, hello pull first executes a `push()` on hello sync context.</span></span> <span data-ttu-id="124da-153">此 push 有助於減少已排入佇列的變更和新的資料，從 hello 伺服器之間的衝突。</span><span class="sxs-lookup"><span data-stu-id="124da-153">This push helps minimize conflicts between changes that are already queued and new data from hello server.</span></span>
* <span data-ttu-id="124da-154">**增量同步處理**: hello 第一個參數 toohello 提取作業*查詢名稱*，只適用於 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="124da-154">**Incremental Sync**: hello first parameter toohello pull operation is a *query name* that is used only on hello client.</span></span> <span data-ttu-id="124da-155">如果您使用非 null 的查詢名稱，就會執行 hello Azure Mobile SDK*增量同步處理*。每次提取作業會傳回一組結果，最新 hello `updatedAt` hello SDK 本機系統資料表中儲存該結果集內的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="124da-155">If you use a non-null query name, hello Azure Mobile SDK performs an *incremental sync*. Each time a pull operation returns a set of results, hello latest `updatedAt` timestamp from that result set is stored in hello SDK local system tables.</span></span> <span data-ttu-id="124da-156">後續的提取作業只會擷取該時間戳記之後的記錄。</span><span class="sxs-lookup"><span data-stu-id="124da-156">Subsequent pull operations retrieve only records after that timestamp.</span></span>

  <span data-ttu-id="124da-157">toouse 增量同步處理您的伺服器必須傳回有意義`updatedAt`值，並且也必須支援依此欄位排序。</span><span class="sxs-lookup"><span data-stu-id="124da-157">toouse incremental sync, your server must return meaningful `updatedAt` values and must also support sorting by this field.</span></span> <span data-ttu-id="124da-158">不過，由於 hello SDK hello updatedAt 欄位加入自己的排序，您無法使用有它自己的提取查詢`orderBy`子句。</span><span class="sxs-lookup"><span data-stu-id="124da-158">However, since hello SDK adds its own sort on hello updatedAt field, you cannot use a pull query that has its own `orderBy` clause.</span></span>

  <span data-ttu-id="124da-159">hello 查詢名稱可以是任何字串您選擇，但必須是唯一的應用程式中的每個邏輯查詢。</span><span class="sxs-lookup"><span data-stu-id="124da-159">hello query name can be any string you choose, but it must be unique for each logical query in your app.</span></span>
  <span data-ttu-id="124da-160">否則，不同的提取作業可能會覆寫 hello 相同的增量同步處理時間戳記和您的查詢可以傳回不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="124da-160">Otherwise, different pull operations could overwrite hello same incremental sync timestamp and your queries can return incorrect results.</span></span>

  <span data-ttu-id="124da-161">如果 hello 查詢的參數，其中一種方式 toocreate 是唯一的查詢名稱 tooincorporate hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="124da-161">If hello query has a parameter, one way toocreate a unique query name is tooincorporate hello parameter value.</span></span>
  <span data-ttu-id="124da-162">例如，如果您要篩選 userid，您的查詢名稱可能如下 (在 C# 中)：</span><span class="sxs-lookup"><span data-stu-id="124da-162">For instance, if you are filtering on userid, your query name could be as follows (in C#):</span></span>

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  <span data-ttu-id="124da-163">如果您想要 tooopt 超出增量同步處理時，傳遞`null`如 hello 的查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="124da-163">If you want tooopt out of incremental sync, pass `null` as hello query ID.</span></span> <span data-ttu-id="124da-164">在此情況下，會擷取所有記錄在每次呼叫太`PullAsync`，這是可能會沒有效率。</span><span class="sxs-lookup"><span data-stu-id="124da-164">In this case, all records are retrieved on every call too`PullAsync`, which is potentially inefficient.</span></span>
* <span data-ttu-id="124da-165">**清除**： 您可以清除 hello 本機存放區使用的 hello 內容`IMobileServiceSyncTable.PurgeAsync`。</span><span class="sxs-lookup"><span data-stu-id="124da-165">**Purging**: You can clear hello contents of hello local store using `IMobileServiceSyncTable.PurgeAsync`.</span></span>
  <span data-ttu-id="124da-166">清除可能需要有過時的資料在 hello 用戶端資料庫中，或如果您想 toodiscard 所有暫止的變更。</span><span class="sxs-lookup"><span data-stu-id="124da-166">Purging may be necessary if you have stale data in hello client database, or if you wish toodiscard all pending changes.</span></span>

  <span data-ttu-id="124da-167">清除清除 hello 本機存放區中的資料表。</span><span class="sxs-lookup"><span data-stu-id="124da-167">A purge clears a table from hello local store.</span></span> <span data-ttu-id="124da-168">如果有作業正在等待同步處理與 hello server 資料庫，hello 清除擲回例外狀況，除非 hello*強制清除*參數設定。</span><span class="sxs-lookup"><span data-stu-id="124da-168">If there are operations awaiting synchronization with hello server database, hello purge throws an exception unless hello *force purge* parameter is set.</span></span>

  <span data-ttu-id="124da-169">例如 hello 用戶端上的過時資料中，假設在 hello 「 todo 清單 」 範例中，Device1 只會提取未完成的項目。</span><span class="sxs-lookup"><span data-stu-id="124da-169">As an example of stale data on hello client, suppose in hello "todo list" example, Device1 only pulls items that are not completed.</span></span> <span data-ttu-id="124da-170">Todoitem"買牛奶"標示為另一個裝置 hello 伺服器上完成。</span><span class="sxs-lookup"><span data-stu-id="124da-170">A todoitem "Buy milk" is marked completed on hello server by another device.</span></span> <span data-ttu-id="124da-171">不過，Device1 仍有的 hello 本機存放區中的 「 購買牛奶 」 todoitem 因為它只會提取項目，則不標示為完成。</span><span class="sxs-lookup"><span data-stu-id="124da-171">However, Device1 still has hello "Buy milk" todoitem in local store because it is only pulling items that are not marked complete.</span></span> <span data-ttu-id="124da-172">清除作業會清除這個過時項目。</span><span class="sxs-lookup"><span data-stu-id="124da-172">A purge clears this stale item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="124da-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="124da-173">Next steps</span></span>
* <span data-ttu-id="124da-174">[iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-174">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="124da-175">[Xamarin iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-175">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="124da-176">[Xamarin Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-176">[Xamarin Android: Enable offline sync]</span></span>
* <span data-ttu-id="124da-177">[通用 Windows 平台︰啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="124da-177">[Universal Windows Platform: Enable offline sync]</span></span>

<!-- Links -->
[.NET 用戶端 SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android：啟用離線同步處理]: app-service-mobile-android-get-started-offline-data.md
[iOS：啟用離線同步處理]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS：啟用離線同步處理]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android：啟用離線同步處理]: app-service-mobile-xamarin-android-get-started-offline-data.md
[通用 Windows 平台︰啟用離線同步處理]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
