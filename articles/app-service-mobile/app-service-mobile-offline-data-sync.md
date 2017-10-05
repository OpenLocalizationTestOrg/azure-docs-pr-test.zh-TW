---
title: "Azure Mobile Apps 中的離線資料同步處理 | Microsoft Docs"
description: "Azure 行動應用程式離線資料同步處理功能的概念參考與概觀"
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
ms.openlocfilehash: 8e2bd755d14319f8c66f7ae7ec64fbd10801b39d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a><span data-ttu-id="657f6-103">Azure 行動應用程式中的離線資料同步處理</span><span class="sxs-lookup"><span data-stu-id="657f6-103">Offline Data Sync in Azure Mobile Apps</span></span>
## <a name="what-is-offline-data-sync"></a><span data-ttu-id="657f6-104">什麼是離線資料同步處理？</span><span class="sxs-lookup"><span data-stu-id="657f6-104">What is offline data sync?</span></span>
<span data-ttu-id="657f6-105">離線資料同步處理是 Azure 行動應用程式的用戶端和伺服器 SDK 功能，可讓開發人員建立不需要網路連線就能運作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="657f6-105">Offline data sync is a client and server SDK feature of Azure Mobile Apps that makes it easy for developers to create apps that are functional without a network connection.</span></span>

<span data-ttu-id="657f6-106">當您的應用程式處於離線模式時，您仍然可以建立和修改資料，所做的變更會儲存至本機存放區。</span><span class="sxs-lookup"><span data-stu-id="657f6-106">When your app is in offline mode, you can still create and modify data, which are saved to a local store.</span></span> <span data-ttu-id="657f6-107">當應用程式回到線上時，即可將本機變更與您的 Azure 行動應用程式後端同步處理。</span><span class="sxs-lookup"><span data-stu-id="657f6-107">When the app is back online, it can synchronize local changes with your Azure Mobile App backend.</span></span> <span data-ttu-id="657f6-108">此功能也包含偵測衝突的支援，即當同一筆記錄在用戶端和後端都發生變更。</span><span class="sxs-lookup"><span data-stu-id="657f6-108">The feature also includes support for detecting conflicts when the same record is changed on both the client and the backend.</span></span> <span data-ttu-id="657f6-109">衝突可以在伺服器或用戶端處理。</span><span class="sxs-lookup"><span data-stu-id="657f6-109">Conflicts can then be handled either on the server or the client.</span></span>

<span data-ttu-id="657f6-110">離線同步處理有幾項優點：</span><span class="sxs-lookup"><span data-stu-id="657f6-110">Offline sync has several benefits:</span></span>

* <span data-ttu-id="657f6-111">在裝置上本機快取伺服器資料，以改善應用程式回應性</span><span class="sxs-lookup"><span data-stu-id="657f6-111">Improve app responsiveness by caching server data locally on the device</span></span>
* <span data-ttu-id="657f6-112">建立當網路有問題時仍可以使用的健全應用程式。</span><span class="sxs-lookup"><span data-stu-id="657f6-112">Create robust apps that remain useful when there are network issues</span></span>
* <span data-ttu-id="657f6-113">即使無法存取網路，使用者也能建立和修改資料，支援連線不佳或無連線的情況</span><span class="sxs-lookup"><span data-stu-id="657f6-113">Allow end users to create and modify data even when there is no network access, supporting scenarios with little or no connectivity</span></span>
* <span data-ttu-id="657f6-114">同步多個裝置之間的資料，並在兩個裝置修改相同的記錄時偵測衝突</span><span class="sxs-lookup"><span data-stu-id="657f6-114">Sync data across multiple devices and detect conflicts when the same record is modified by two devices</span></span>
* <span data-ttu-id="657f6-115">高延遲或計量付費網路的網路使用限制。</span><span class="sxs-lookup"><span data-stu-id="657f6-115">Limit network use on high-latency or metered networks</span></span>

<span data-ttu-id="657f6-116">下列教學課程說明如何使用 Azure 行動應用程式將離線同步處理新增至您的行動用戶端：</span><span class="sxs-lookup"><span data-stu-id="657f6-116">The following tutorials show how to add offline sync to your mobile clients using Azure Mobile Apps:</span></span>

* <span data-ttu-id="657f6-117">[Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-117">[Android: Enable offline sync]</span></span>
* [<span data-ttu-id="657f6-118">Apache Cordova︰啟用離線同步處理</span><span class="sxs-lookup"><span data-stu-id="657f6-118">Apache Cordova: Enable offline sync</span></span>](app-service-mobile-cordova-get-started-offline-data.md)
* <span data-ttu-id="657f6-119">[iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-119">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="657f6-120">[Xamarin iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-120">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="657f6-121">[Xamarin Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-121">[Xamarin Android: Enable offline sync]</span></span>
* [<span data-ttu-id="657f6-122">Xamarin.Forms：啟用離線同步處理</span><span class="sxs-lookup"><span data-stu-id="657f6-122">Xamarin.Forms: Enable offline sync</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* <span data-ttu-id="657f6-123">[通用 Windows 平台︰啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-123">[Universal Windows Platform: Enable offline sync]</span></span>

## <a name="what-is-a-sync-table"></a><span data-ttu-id="657f6-124">什麼是同步處理資料表？</span><span class="sxs-lookup"><span data-stu-id="657f6-124">What is a sync table?</span></span>
<span data-ttu-id="657f6-125">若要存取 "/tables" 端點，Azure 行動用戶端 SDK 提供 `IMobileServiceTable` (.NET 用戶端 SDK) 或 `MSTable` (iOS 用戶端) 等介面。</span><span class="sxs-lookup"><span data-stu-id="657f6-125">To access the "/tables" endpoint, the Azure Mobile client SDKs provide interfaces such as `IMobileServiceTable` (.NET client SDK) or `MSTable` (iOS client).</span></span> <span data-ttu-id="657f6-126">這些 API 直接連接至 Azure 行動應用程式後端，如果用戶端裝置沒有網路連接，則會失敗。</span><span class="sxs-lookup"><span data-stu-id="657f6-126">These APIs connect directly to the Azure Mobile App backend and fail if the client device does not have a network connection.</span></span>

<span data-ttu-id="657f6-127">若要支援離線使用，您的應用程式應改為使用「同步處理資料表」API，例如 `IMobileServiceSyncTable` (.NET 用戶端 SDK) 或 `MSSyncTable` (iOS 用戶端)。</span><span class="sxs-lookup"><span data-stu-id="657f6-127">To support offline use, your app should instead use the *sync table* APIs, such as `IMobileServiceSyncTable` (.NET client SDK) or `MSSyncTable` (iOS client).</span></span> <span data-ttu-id="657f6-128">所有相同的 CRUD 作業 (Create、Read、Update、Delete) 適用於同步資料表 API，但現在會讀取或寫入「本機存放區」。</span><span class="sxs-lookup"><span data-stu-id="657f6-128">All the same CRUD operations (Create, Read, Update, Delete) work against sync table APIs, except now they read from or write to a *local store*.</span></span> <span data-ttu-id="657f6-129">必須先初始化本機存放區，才能執行任何同步處理資料表作業。</span><span class="sxs-lookup"><span data-stu-id="657f6-129">Before any sync table operations can be performed, the local store must be initialized.</span></span>

## <a name="what-is-a-local-store"></a><span data-ttu-id="657f6-130">什麼是本機存放區？</span><span class="sxs-lookup"><span data-stu-id="657f6-130">What is a local store?</span></span>
<span data-ttu-id="657f6-131">本機存放區是用戶端裝置上的資料持續層。</span><span class="sxs-lookup"><span data-stu-id="657f6-131">A local store is the data persistence layer on the client device.</span></span> <span data-ttu-id="657f6-132">Azure 行動應用程式用戶端 SDK 提供預設的本機存放區實作。</span><span class="sxs-lookup"><span data-stu-id="657f6-132">The Azure Mobile Apps client SDKs provide a default local store implementation.</span></span> <span data-ttu-id="657f6-133">在 Windows、Xamarin 和 Android 上，它是以 SQLite 為基礎。</span><span class="sxs-lookup"><span data-stu-id="657f6-133">On Windows, Xamarin and Android, it is based on SQLite.</span></span> <span data-ttu-id="657f6-134">在 iOS 上，它是以 Core Data 為基礎。</span><span class="sxs-lookup"><span data-stu-id="657f6-134">On iOS, it is based on Core Data.</span></span>

<span data-ttu-id="657f6-135">若要在 Windows Phone 或 Windows 市集 8.1 上使用 SQLite 為基礎的實作，您需要安裝 SQLite 擴充。</span><span class="sxs-lookup"><span data-stu-id="657f6-135">To use the SQLite-based implementation on Windows Phone or Windows Store 8.1, you need to install a SQLite extension.</span></span> <span data-ttu-id="657f6-136">如需詳細資訊，請參閱[通用 Windows 平台︰啟用離線同步處理]。Android 與 iOS 裝置的作業系統本身即包含 SQLite 版本，因此您不需要再參考自己的 SQLite 版本。</span><span class="sxs-lookup"><span data-stu-id="657f6-136">For more information, see [Universal Windows Platform: Enable offline sync]. Android and iOS ship with a version of SQLite in the device operating system itself, so it is not necessary to reference your own version of SQLite.</span></span>

<span data-ttu-id="657f6-137">開發人員也可以實作自己的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="657f6-137">Developers can also implement their own local store.</span></span> <span data-ttu-id="657f6-138">例如，如果您希望將資料以加密格式儲存在行動用戶端上，則您可以定義使用 SQLCipher 進行加密的本機存放區。</span><span class="sxs-lookup"><span data-stu-id="657f6-138">For instance, if you wish to store data in an encrypted format on the mobile client, you can define a local store that uses SQLCipher for encryption.</span></span>

## <a name="what-is-a-sync-context"></a><span data-ttu-id="657f6-139">什麼是同步處理內容？</span><span class="sxs-lookup"><span data-stu-id="657f6-139">What is a sync context?</span></span>
<span data-ttu-id="657f6-140">「同步處理內容」會與行動用戶端物件相關聯 (例如 `IMobileServiceClient` 或 `MSClient`)，並且追蹤對同步處理資料表所做的變更。</span><span class="sxs-lookup"><span data-stu-id="657f6-140">A *sync context* is associated with a mobile client object (such as `IMobileServiceClient` or `MSClient`) and tracks changes that are made with sync tables.</span></span> <span data-ttu-id="657f6-141">同步處理內容會維護「作業佇列」，其中會保留 CUD 作業 (Create、Update、Delete) 的排序清單，這些作業稍後會傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="657f6-141">The sync context maintains an *operation queue*, which keeps an ordered list of CUD operations (Create, Update, Delete) that is later be sent to the server.</span></span>

<span data-ttu-id="657f6-142">本機存放區會使用初始化方法 (例如 [.NET 用戶端 SDK] 中的 `IMobileServicesSyncContext.InitializeAsync(localstore)`)，來與同步處理內容相關聯。</span><span class="sxs-lookup"><span data-stu-id="657f6-142">A local store is associated with the sync context using an initialize method such as `IMobileServicesSyncContext.InitializeAsync(localstore)` in the [.NET client SDK].</span></span>

## <span data-ttu-id="657f6-143"><a name="how-sync-works"></a>離線同步處理如何運作</span><span class="sxs-lookup"><span data-stu-id="657f6-143"><a name="how-sync-works"></a>How offline synchronization works</span></span>
<span data-ttu-id="657f6-144">使用同步處理資料表時，您的用戶端程式碼需要控制本機變更與 Azure 行動應用程式後端同步處理的時機。</span><span class="sxs-lookup"><span data-stu-id="657f6-144">When using sync tables, your client code controls when local changes are synchronized with an Azure Mobile App backend.</span></span> <span data-ttu-id="657f6-145">在有呼叫要「推送」( *push* ) 變更之前不會傳送任何項目到後端。</span><span class="sxs-lookup"><span data-stu-id="657f6-145">Nothing is sent to the backend until there is a call to *push* local changes.</span></span> <span data-ttu-id="657f6-146">同樣地，只當有呼叫要「提取」( *pull* ) 時才會將新資料填入本機存放區。</span><span class="sxs-lookup"><span data-stu-id="657f6-146">Similarly, the local store is populated with new data only when there is a call to *pull* data.</span></span>

* <span data-ttu-id="657f6-147">**推送**：推送是同步處理內容的作業，會傳送自上一次推送之後的所有 CUD 變更。</span><span class="sxs-lookup"><span data-stu-id="657f6-147">**Push**: Push is an operation on the sync context and sends all CUD changes since the last push.</span></span> <span data-ttu-id="657f6-148">請注意，您無法只傳送個別資料表的變更，因為這樣作業傳送順序可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="657f6-148">Note that it is not possible to send only an individual table's changes, because otherwise operations could be sent out of order.</span></span> <span data-ttu-id="657f6-149">推送會對 Azure 行動應用程式後端執行一系列的 REST 呼叫，再由後端修改伺服器資料庫。</span><span class="sxs-lookup"><span data-stu-id="657f6-149">Push executes a series of REST calls to your Azure Mobile App backend, which in turn modifies your server database.</span></span>
* <span data-ttu-id="657f6-150">**提取**：提取會以各資料表為基礎執行，並且可以使用佇列來自訂，以抓取伺服器資料的特定子集。</span><span class="sxs-lookup"><span data-stu-id="657f6-150">**Pull**: Pull is performed on a per-table basis and can be customized with a query to retrieve only a subset of the server data.</span></span> <span data-ttu-id="657f6-151">然後 Azure 行動用戶端 SDK 會將該結果資料插入本機存放區。</span><span class="sxs-lookup"><span data-stu-id="657f6-151">The Azure Mobile client SDKs then insert the resulting data into the local store.</span></span>
* <span data-ttu-id="657f6-152">**隱含推送**：如果對有擱置中本機更新的資料表執行提取，則提取會先在同步處理內容上執行 `push()`。</span><span class="sxs-lookup"><span data-stu-id="657f6-152">**Implicit Pushes**: If a pull is executed against a table that has pending local updates, the pull first executes a `push()` on the sync context.</span></span> <span data-ttu-id="657f6-153">此推送有助於將已排入佇列的變更與來自伺服器的新資料之間的衝突降到最低。</span><span class="sxs-lookup"><span data-stu-id="657f6-153">This push helps minimize conflicts between changes that are already queued and new data from the server.</span></span>
* <span data-ttu-id="657f6-154">**增量同步處理**：提取作業的第一個參數是「查詢名稱」，此參數只在用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="657f6-154">**Incremental Sync**: the first parameter to the pull operation is a *query name* that is used only on the client.</span></span> <span data-ttu-id="657f6-155">如果您使用非 null 的查詢名稱，Azure 行動 SDK 會執行「增量同步處理」 。每當提取作業傳回結果集，該結果集中最新的 `updatedAt` 時間戳記就會儲存在 SDK 本機系統資料表。</span><span class="sxs-lookup"><span data-stu-id="657f6-155">If you use a non-null query name, the Azure Mobile SDK performs an *incremental sync*. Each time a pull operation returns a set of results, the latest `updatedAt` timestamp from that result set is stored in the SDK local system tables.</span></span> <span data-ttu-id="657f6-156">後續的提取作業只會擷取該時間戳記之後的記錄。</span><span class="sxs-lookup"><span data-stu-id="657f6-156">Subsequent pull operations retrieve only records after that timestamp.</span></span>

  <span data-ttu-id="657f6-157">若要使用增量同步處理，您的伺服器必須傳回有意義的 `updatedAt` 值，也必須支援依據此欄位排序。</span><span class="sxs-lookup"><span data-stu-id="657f6-157">To use incremental sync, your server must return meaningful `updatedAt` values and must also support sorting by this field.</span></span> <span data-ttu-id="657f6-158">不過，由於 SDK 會在 updatedAt 欄位上加入自己的排序，所以您不能使用本身具備 `orderBy` 子句的提取查詢。</span><span class="sxs-lookup"><span data-stu-id="657f6-158">However, since the SDK adds its own sort on the updatedAt field, you cannot use a pull query that has its own `orderBy` clause.</span></span>

  <span data-ttu-id="657f6-159">查詢名稱可以是您選擇的任何字串，但它在應用程式中的每個邏輯查詢都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="657f6-159">The query name can be any string you choose, but it must be unique for each logical query in your app.</span></span>
  <span data-ttu-id="657f6-160">否則，不同的提取作業可能會覆寫相同的增量同步處理時間戳記，您的查詢可能因此傳回不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="657f6-160">Otherwise, different pull operations could overwrite the same incremental sync timestamp and your queries can return incorrect results.</span></span>

  <span data-ttu-id="657f6-161">如果查詢具有參數，一個建立唯一查詢名稱的方法是納入該參數值。</span><span class="sxs-lookup"><span data-stu-id="657f6-161">If the query has a parameter, one way to create a unique query name is to incorporate the parameter value.</span></span>
  <span data-ttu-id="657f6-162">例如，如果您要篩選 userid，您的查詢名稱可能如下 (在 C# 中)：</span><span class="sxs-lookup"><span data-stu-id="657f6-162">For instance, if you are filtering on userid, your query name could be as follows (in C#):</span></span>

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  <span data-ttu-id="657f6-163">如果您想選擇不要增量同步處理，則傳遞 `null` 做為查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="657f6-163">If you want to opt out of incremental sync, pass `null` as the query ID.</span></span> <span data-ttu-id="657f6-164">在此情況下，每次呼叫 `PullAsync` 時都會擷取所有的記錄，這樣可能沒有效率。</span><span class="sxs-lookup"><span data-stu-id="657f6-164">In this case, all records are retrieved on every call to `PullAsync`, which is potentially inefficient.</span></span>
* <span data-ttu-id="657f6-165">**清除**：您可以使用 `IMobileServiceSyncTable.PurgeAsync` 來清除本機存放區的內容。</span><span class="sxs-lookup"><span data-stu-id="657f6-165">**Purging**: You can clear the contents of the local store using `IMobileServiceSyncTable.PurgeAsync`.</span></span>
  <span data-ttu-id="657f6-166">如果用戶端資料庫中有過時資料，或者您想要捨棄所有擱置的變更，可能就需要清除。</span><span class="sxs-lookup"><span data-stu-id="657f6-166">Purging may be necessary if you have stale data in the client database, or if you wish to discard all pending changes.</span></span>

  <span data-ttu-id="657f6-167">清除作業會從本機存放區清除資料表。</span><span class="sxs-lookup"><span data-stu-id="657f6-167">A purge clears a table from the local store.</span></span> <span data-ttu-id="657f6-168">如果有正在等待與伺服器資料庫同步處理的作業，則清除會擲回例外狀況，除非設定 *force purge* 參數。</span><span class="sxs-lookup"><span data-stu-id="657f6-168">If there are operations awaiting synchronization with the server database, the purge throws an exception unless the *force purge* parameter is set.</span></span>

  <span data-ttu-id="657f6-169">舉例說明用戶端上過時資料，假設在 "todo list" 範例中，Device1 只會提取未完成的項目。</span><span class="sxs-lookup"><span data-stu-id="657f6-169">As an example of stale data on the client, suppose in the "todo list" example, Device1 only pulls items that are not completed.</span></span> <span data-ttu-id="657f6-170">有其他裝置在伺服器上將 "Buy milk" todoitem 標記為已完成。</span><span class="sxs-lookup"><span data-stu-id="657f6-170">A todoitem "Buy milk" is marked completed on the server by another device.</span></span> <span data-ttu-id="657f6-171">不過，Device1 在本機存放區仍有 "Buy milk" todoitem，因為它只提取未標記為已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="657f6-171">However, Device1 still has the "Buy milk" todoitem in local store because it is only pulling items that are not marked complete.</span></span> <span data-ttu-id="657f6-172">清除作業會清除這個過時項目。</span><span class="sxs-lookup"><span data-stu-id="657f6-172">A purge clears this stale item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="657f6-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="657f6-173">Next steps</span></span>
* <span data-ttu-id="657f6-174">[iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-174">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="657f6-175">[Xamarin iOS：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-175">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="657f6-176">[Xamarin Android：啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-176">[Xamarin Android: Enable offline sync]</span></span>
* <span data-ttu-id="657f6-177">[通用 Windows 平台︰啟用離線同步處理]</span><span class="sxs-lookup"><span data-stu-id="657f6-177">[Universal Windows Platform: Enable offline sync]</span></span>

<!-- Links -->
[.NET 用戶端 SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android：啟用離線同步處理]: app-service-mobile-android-get-started-offline-data.md
[iOS：啟用離線同步處理]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS：啟用離線同步處理]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android：啟用離線同步處理]: app-service-mobile-xamarin-android-get-started-offline-data.md
[通用 Windows 平台︰啟用離線同步處理]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
