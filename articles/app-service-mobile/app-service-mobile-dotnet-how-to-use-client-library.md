---
title: "以 hello 的 App Service Mobile App aaaWorking managed 用戶端程式庫 (Windows |Microsoft 文件"
description: "深入了解如何 toouse Azure App Service 行動應用程式與 Windows 和 Xamarin 應用程式的.NET 用戶端。"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="bfc31-103">Toouse hello 如何管理 Azure 行動應用程式的用戶端</span><span class="sxs-lookup"><span data-stu-id="bfc31-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="bfc31-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bfc31-104">Overview</span></span>
<span data-ttu-id="bfc31-105">本指南也說明使用 hello tooperform 常見的案例如何管理用戶端程式庫，針對 Azure 應用程式服務行動裝置應用程式的 Windows 與 Xamarin 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="bfc31-106">如果您是新 tooMobile 應用程式，您應該考慮第一個完成的 hello [Azure 行動應用程式快速入門][ 1]教學課程。</span><span class="sxs-lookup"><span data-stu-id="bfc31-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="bfc31-107">本指南中，我們將重點放在 hello 上用戶端管理 SDK。</span><span class="sxs-lookup"><span data-stu-id="bfc31-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="bfc31-108">toolearn 深入了解 hello 行動應用程式的伺服器端 Sdk，請參閱 hello 文件以 hello [.NET 伺服器 SDK] [ 2]或[Node.js 伺服器 SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="bfc31-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="bfc31-109">參考文件</span><span class="sxs-lookup"><span data-stu-id="bfc31-109">Reference documentation</span></span>
<span data-ttu-id="bfc31-110">hello hello client SDK 的參考文件位於此處： [Azure 行動應用程式的.NET 用戶端參考][4]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="bfc31-111">您也可以找到數個用戶端範例在 hello [Azure 範例 GitHub 儲存機制][5]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="bfc31-112">支援的平台</span><span class="sxs-lookup"><span data-stu-id="bfc31-112">Supported Platforms</span></span>
<span data-ttu-id="bfc31-113">hello.NET 平台支援下列平台的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="bfc31-114">適用於 API 19 到 24 (KitKat 到 Nougat) 的 Xamarin Android 版本</span><span class="sxs-lookup"><span data-stu-id="bfc31-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="bfc31-115">適用於 iOS 8.0 版和更新版本的 Xamarin iOS 版本</span><span class="sxs-lookup"><span data-stu-id="bfc31-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="bfc31-116">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="bfc31-116">Universal Windows Platform</span></span>
* <span data-ttu-id="bfc31-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="bfc31-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="bfc31-118">Windows Phone 8.0 (Silverlight 應用程式除外)</span><span class="sxs-lookup"><span data-stu-id="bfc31-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="bfc31-119">hello 「 伺服器-流程 」 驗證會使用 WebView hello 呈現 UI。</span><span class="sxs-lookup"><span data-stu-id="bfc31-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="bfc31-120">如果 hello 裝置不能 toopresent WebView UI，則會需要其他的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="bfc31-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="bfc31-121">因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。</span><span class="sxs-lookup"><span data-stu-id="bfc31-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="bfc31-122"><a name="setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="bfc31-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="bfc31-123">我們假設您已建立並發佈您的行動應用程式後端專案 (至少包含一個資料表)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="bfc31-124">使用本主題中的 hello 程式碼，在名為 hello 資料表`TodoItem`並具有下列資料行的 hello: `Id`， `Text`，和`Complete`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="bfc31-125">此資料表是相同的資料表建立，當您完成時的 hello [Azure 行動應用程式快速入門][1]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="bfc31-126">hello 對應型別的用戶端的類型在 C# 中為下列類別的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="bfc31-127">hello [JsonPropertyAttribute] [ 6]為使用的 toodefine hello *PropertyName* hello 用戶端欄位與 hello 資料表欄位之間的對應。</span><span class="sxs-lookup"><span data-stu-id="bfc31-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="bfc31-128">toolearn toocreate 行動應用程式後端中的資料表，請參閱 「 hello [.NET 伺服器 SDK 主題][ 7]或 hello [Node.js 伺服器 SDK 主題][ 8].</span><span class="sxs-lookup"><span data-stu-id="bfc31-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="bfc31-129">如果您已建立您的行動裝置應用程式後端中 hello Azure 入口網站使用 hello 快速入門中，您也可以使用 hello**簡單資料表**hello 中設定[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="bfc31-130">如何： 安裝 hello 受管理用戶端 SDK 封裝</span><span class="sxs-lookup"><span data-stu-id="bfc31-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="bfc31-131">使用其中一個 hello 遵循方法 tooinstall hello 適用於從行動裝置應用程式管理的用戶端 SDK 套件[NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="bfc31-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="bfc31-132">**Visual Studio**以滑鼠右鍵按一下您的專案中，按一下**管理 NuGet 封裝**，搜尋 hello`Microsoft.Azure.Mobile.Client`封裝，然後按一下 **安裝**。</span><span class="sxs-lookup"><span data-stu-id="bfc31-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="bfc31-133">**Xamarin Studio**以滑鼠右鍵按一下您的專案中，按一下**新增** > **新增 NuGet 套件**，搜尋 hello`Microsoft.Azure.Mobile.Client `封裝，然後按一下**新增封裝**。</span><span class="sxs-lookup"><span data-stu-id="bfc31-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="bfc31-134">在您的主要活動檔案，請記得 tooadd hello 下列**使用**陳述式：</span><span class="sxs-lookup"><span data-stu-id="bfc31-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="bfc31-135"><a name="symbolsource"></a>做法︰使用 Visual Studio 中的偵錯符號</span><span class="sxs-lookup"><span data-stu-id="bfc31-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="bfc31-136">hello 符號 hello Microsoft.Azure.Mobile 命名空間位於[SymbolSource][10]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="bfc31-137">請參閱 toothe [SymbolSource 指示][ 11] toointegrate SymbolSource 與 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bfc31-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="bfc31-138"><a name="create-client"></a>建立 hello 行動應用程式用戶端</span><span class="sxs-lookup"><span data-stu-id="bfc31-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="bfc31-139">hello 下列程式碼會建立 hello [MobileServiceClient] [ 12]亦即使用的 tooaccess 您的行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="bfc31-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="bfc31-140">在上述程式碼的 hello，取代`MOBILE_APP_URL`hello hello 行動裝置應用程式後端 url，找到在刀鋒視窗中的行動裝置應用程式後端中 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="bfc31-141">hello MobileServiceClient 物件應該是單一值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="bfc31-142">使用資料表</span><span class="sxs-lookup"><span data-stu-id="bfc31-142">Work with Tables</span></span>
<span data-ttu-id="bfc31-143">hello 遵循本節詳述如何 toosearch 和擷取記錄，以及修改 hello 資料表中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="bfc31-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="bfc31-144">涵蓋下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="bfc31-145">建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="bfc31-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="bfc31-146">查詢資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-146">Query data</span></span>](#querying)
* [<span data-ttu-id="bfc31-147">篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="bfc31-148">排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="bfc31-149">以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="bfc31-150">選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="bfc31-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="bfc31-151">依據識別碼查詢記錄</span><span class="sxs-lookup"><span data-stu-id="bfc31-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="bfc31-152">處理不具類型的查詢</span><span class="sxs-lookup"><span data-stu-id="bfc31-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="bfc31-153">插入資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="bfc31-154">更新資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="bfc31-155">刪除資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="bfc31-156">衝突解決和開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="bfc31-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="bfc31-157">繫結 tooa Windows 使用者介面</span><span class="sxs-lookup"><span data-stu-id="bfc31-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="bfc31-158">變更頁面大小 hello</span><span class="sxs-lookup"><span data-stu-id="bfc31-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="bfc31-159"><a name="instantiating"></a>作法：建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="bfc31-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="bfc31-160">所有的 「 hello 」 程式碼，可以存取或修改後端資料表中的資料呼叫函式上 hello`MobileServiceTable`物件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="bfc31-161">取得參考 toohello 資料表呼叫 hello [GetTable]方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="bfc31-162">hello 傳回物件使用 hello 具類型的序列化模式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="bfc31-163">也支援不具類型的序列化模型。</span><span class="sxs-lookup"><span data-stu-id="bfc31-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="bfc31-164">下列範例[建立參考 tooan 不具型別的資料表]:</span><span class="sxs-lookup"><span data-stu-id="bfc31-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="bfc31-165">在不具類型的查詢中，您必須指定 hello 基礎 OData 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="bfc31-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="bfc31-166"><a name="querying"></a>如何：查詢行動應用程式中的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="bfc31-167">本章節描述如何 tooissue 查詢 toohello 行動裝置應用程式後端，其中包括下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="bfc31-168">篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="bfc31-169">排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="bfc31-170">以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="bfc31-171">選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="bfc31-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="bfc31-172">按識別碼查詢資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="bfc31-173">伺服器導向的頁面大小是強制的 tooprevent 傳回所有資料列。</span><span class="sxs-lookup"><span data-stu-id="bfc31-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="bfc31-174">分頁可避免針對大型資料集的預設要求對於 hello 服務造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="bfc31-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="bfc31-175">tooreturn 多超過 50 個資料列，使用 hello`Skip`和`Take`方法中所述[頁面中傳回資料](#paging)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="bfc31-176"><a name="filtering"></a>作法：篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="bfc31-177">hello 下列程式碼說明如何藉由 toofilter 資料`Where`在查詢中的子句。</span><span class="sxs-lookup"><span data-stu-id="bfc31-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="bfc31-178">它會傳回所有項目從`todoTable`其`Complete`屬性等於太`false`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="bfc31-179">hello[其中]函式適用於將資料列篩選述詞，以針對 hello 資料表 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="bfc31-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="bfc31-180">您可以使用訊息檢查軟體，例如瀏覽器開發人員工具來檢視 hello hello 傳送要求 toohello 後端的 URI 或[Fiddler]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="bfc31-181">如果您看一下 hello 要求 URI，請注意會修改 hello 查詢字串：</span><span class="sxs-lookup"><span data-stu-id="bfc31-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="bfc31-182">此 OData 要求會轉譯成 SQL 查詢，由伺服器 SDK hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="bfc31-183">hello 函式傳遞 toohello`Where`方法可以有任意數目的條件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="bfc31-184">這個範例會轉譯成 SQL 查詢，由伺服器 SDK hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="bfc31-185">此查詢也可以分割成多個子句︰</span><span class="sxs-lookup"><span data-stu-id="bfc31-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="bfc31-186">hello 兩種方法是相等的可能會交換使用。</span><span class="sxs-lookup"><span data-stu-id="bfc31-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="bfc31-187">hello 先前選項&mdash;串連多個述詞在單一查詢中的&mdash;更簡潔且建議。</span><span class="sxs-lookup"><span data-stu-id="bfc31-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="bfc31-188">hello`Where`子句支援的作業會轉譯成 hello OData 子集。</span><span class="sxs-lookup"><span data-stu-id="bfc31-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="bfc31-189">這些作業包括︰</span><span class="sxs-lookup"><span data-stu-id="bfc31-189">Operations include:</span></span>

* <span data-ttu-id="bfc31-190">關係運算子 (==、!=、<、<=、>、>=)、</span><span class="sxs-lookup"><span data-stu-id="bfc31-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="bfc31-191">算術運算子 (+、-、/、*、%)、</span><span class="sxs-lookup"><span data-stu-id="bfc31-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="bfc31-192">精確度位數 (Math.Floor、Math.Ceiling)、</span><span class="sxs-lookup"><span data-stu-id="bfc31-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="bfc31-193">字串函數 (Length、Substring、Replace、IndexOf、StartsWith、EndsWith)、</span><span class="sxs-lookup"><span data-stu-id="bfc31-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="bfc31-194">日期屬性 (Year、Month、Day、Hour、Minute、Second)、</span><span class="sxs-lookup"><span data-stu-id="bfc31-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="bfc31-195">物件的存取屬性，及</span><span class="sxs-lookup"><span data-stu-id="bfc31-195">Access properties of an object, and</span></span>
* <span data-ttu-id="bfc31-196">結合上述任何運算的運算式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="bfc31-197">請考慮什麼 hello 伺服器 SDK 當支援時，您可以考慮 hello [OData v3 文件]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="bfc31-198"><a name="sorting"></a>作法：排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="bfc31-199">hello 下列程式碼說明如何藉由 toosort 資料[OrderBy]或[OrderByDescending] hello 查詢中的函式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="bfc31-200">它會傳回項目從`todoTable`排序按遞增 hello`Text`欄位。</span><span class="sxs-lookup"><span data-stu-id="bfc31-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="bfc31-201"><a name="paging"></a>作法：以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="bfc31-202">根據預設，hello 後端會傳回只 hello 前 50 個資料列。</span><span class="sxs-lookup"><span data-stu-id="bfc31-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="bfc31-203">您可以透過呼叫 hello 增加 hello 傳回的資料列數目[採取]方法。</span><span class="sxs-lookup"><span data-stu-id="bfc31-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="bfc31-204">使用`Take`以及 hello[略過]方法 toorequest 特定"page"hello 總計的資料集的 hello 查詢所傳回。</span><span class="sxs-lookup"><span data-stu-id="bfc31-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="bfc31-205">hello 執行時，下列查詢傳回 hello 前三個項目 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="bfc31-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="bfc31-206">hello 下列修訂過的查詢會略過 hello 前三個結果，並傳回 hello 接下來三個結果。</span><span class="sxs-lookup"><span data-stu-id="bfc31-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="bfc31-207">此查詢會產生 hello 第二個 「 頁 」 資料，其中 hello 頁面大小是三個項目。</span><span class="sxs-lookup"><span data-stu-id="bfc31-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="bfc31-208">hello [IncludeTotalCount]方法會要求 hello 總計數*所有*hello 會傳回，忽略任何 paging/limit 子句，指定的記錄：</span><span class="sxs-lookup"><span data-stu-id="bfc31-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="bfc31-209">在真實世界應用程式中，您可以使用查詢類似 toohello 前面範例和頁面巡覽區控制項或類似的 UI 頁面之間巡覽。</span><span class="sxs-lookup"><span data-stu-id="bfc31-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="bfc31-210">在行動裝置應用程式後端 toooverride hello 50 同資料列限制，您必須套用 hello [EnableQueryAttribute] toohello 公用 GET 方法，並指定 hello 分頁行為。</span><span class="sxs-lookup"><span data-stu-id="bfc31-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="bfc31-211">當套用的 toohello 方法，下列的 hello 設定傳回的最大資料列 too1000:</span><span class="sxs-lookup"><span data-stu-id="bfc31-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="bfc31-212"><a name="selecting"></a>作法：選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="bfc31-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="bfc31-213">您可以指定哪屬性 tooinclude hello 中一組結果加[選取]子句 tooyour 查詢。</span><span class="sxs-lookup"><span data-stu-id="bfc31-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="bfc31-214">例如，hello 下列程式碼會示範如何 tooselect 只有一個欄位和也方式 tooselect 並格式化多個欄位：</span><span class="sxs-lookup"><span data-stu-id="bfc31-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="bfc31-215">所有 hello 到目前為止所述的函式會加總，因此我們可以保留鏈結它們。</span><span class="sxs-lookup"><span data-stu-id="bfc31-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="bfc31-216">鏈結的每個呼叫會影響多個 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="bfc31-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="bfc31-217">再提供一個範例：</span><span class="sxs-lookup"><span data-stu-id="bfc31-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="bfc31-218"><a name="lookingup"></a>作法：按識別碼查詢資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="bfc31-219">hello [LookupAsync]函式可以是使用的 toolook 已從 hello 與特定識別碼的資料庫物件</span><span class="sxs-lookup"><span data-stu-id="bfc31-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="bfc31-220"><a name="untypedqueries"></a>如何：執行不具類型的查詢</span><span class="sxs-lookup"><span data-stu-id="bfc31-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="bfc31-221">執行時使用的資料表不具型別的的物件查詢，您必須明確地指定 hello OData 查詢字串呼叫[ReadAsync]，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="bfc31-222">您將收到可用作屬性包的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="bfc31-223">如需 JToken 和 Newtonsoft Json.NET 的詳細資訊，請參閱 hello [Json.NET]站台。</span><span class="sxs-lookup"><span data-stu-id="bfc31-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="bfc31-224"><a name="inserting"></a>如何：將資料插入行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="bfc31-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="bfc31-225">所有用戶端類型都必須包含名為 **Id**的成員，其預設為字串。</span><span class="sxs-lookup"><span data-stu-id="bfc31-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="bfc31-226">這**識別碼**才能執行 CRUD 作業，且針對 hello 離線同步處理。 下列程式碼說明如何 toouse hello [InsertAsync]方法 tooinsert 新的資料列插入資料表。</span><span class="sxs-lookup"><span data-stu-id="bfc31-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="bfc31-227">hello 參數包含 hello 資料 toobe 插入為.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="bfc31-228">如果自訂的唯一識別碼值不會包含在 hello `todoItem` hello 伺服器時，插入，產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="bfc31-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="bfc31-229">您可以擷取 hello hello 呼叫傳回後，檢查 hello 物件產生識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="bfc31-230">tooinsert 不具類型的資料，您可能會利用 Json.NET:</span><span class="sxs-lookup"><span data-stu-id="bfc31-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="bfc31-231">以下是使用電子郵件地址作為唯一字串 id 的範例：</span><span class="sxs-lookup"><span data-stu-id="bfc31-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="bfc31-232">使用識別碼值</span><span class="sxs-lookup"><span data-stu-id="bfc31-232">Working with ID values</span></span>
<span data-ttu-id="bfc31-233">行動應用程式支援自訂的唯一字串值 hello 資料表**識別碼**資料行。</span><span class="sxs-lookup"><span data-stu-id="bfc31-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="bfc31-234">字串值，可讓應用程式 toouse 自訂值，例如電子郵件地址或 hello 識別碼的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="bfc31-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="bfc31-235">字串 Id 為您提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="bfc31-236">不會進行往返 toohello 資料庫產生的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="bfc31-237">更容易 toomerge 來自不同資料表或資料庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="bfc31-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="bfc31-238">識別碼值與應用程式邏輯的整合更理想。</span><span class="sxs-lookup"><span data-stu-id="bfc31-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="bfc31-239">插入的記錄上未設定字串 ID 值，當 hello 行動裝置應用程式後端產生唯一值的識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="bfc31-240">您可以使用 hello [Guid.NewGuid]方法 toogenerate 您自己的識別碼值 hello 用戶端上或在 hello 後端中。</span><span class="sxs-lookup"><span data-stu-id="bfc31-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="bfc31-241"><a name="modifying"></a>如何：修改行動應用程式後端中的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="bfc31-242">hello 下列程式碼說明如何 toouse hello [UpdateAsync]方法 tooupdate hello 與現有的記錄相同的識別碼以新資訊。</span><span class="sxs-lookup"><span data-stu-id="bfc31-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="bfc31-243">hello 參數包含 hello 資料 toobe 更新為.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="bfc31-244">tooupdate 不具類型的資料，您可能會利用[Json.NET] ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="bfc31-245">更新時，您必須指定 `id` 欄位。</span><span class="sxs-lookup"><span data-stu-id="bfc31-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="bfc31-246">hello 後端使用 hello`id`欄位 tooidentify 的資料列 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="bfc31-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="bfc31-247">hello`id`欄位可以取自 hello hello 結果`InsertAsync`呼叫。</span><span class="sxs-lookup"><span data-stu-id="bfc31-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="bfc31-248">`ArgumentException`如果您嘗試使用沒有提供 hello tooupdate 項目就會引發`id`值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="bfc31-249"><a name="deleting"></a>如何：刪除行動應用程式後端中的資料</span><span class="sxs-lookup"><span data-stu-id="bfc31-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="bfc31-250">hello 下列程式碼說明如何 toouse hello [DeleteAsync]方法 toodelete 現有執行個體。</span><span class="sxs-lookup"><span data-stu-id="bfc31-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="bfc31-251">hello 執行個體由 hello`id`欄位上 hello `todoItem`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="bfc31-252">toodelete 不具類型的資料，您可能會利用 Json.NET，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="bfc31-253">提出刪除要求時，必須指定 ID。</span><span class="sxs-lookup"><span data-stu-id="bfc31-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="bfc31-254">其他屬性不會傳遞 toohello 服務，或在 hello 服務會被忽略。</span><span class="sxs-lookup"><span data-stu-id="bfc31-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="bfc31-255">hello 結果`DeleteAsync`呼叫通常是`null`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="bfc31-256">中的 hello 識別碼 toopass 可以取自 hello hello 結果`InsertAsync`呼叫。</span><span class="sxs-lookup"><span data-stu-id="bfc31-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="bfc31-257">A`MobileServiceInvalidOperationException`您嘗試使用沒有指定 hello toodelete 項目時，會擲回`id`欄位。</span><span class="sxs-lookup"><span data-stu-id="bfc31-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="bfc31-258"><a name="optimisticconcurrency"></a>做法：使用開放式並行存取來解決衝突</span><span class="sxs-lookup"><span data-stu-id="bfc31-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="bfc31-259">兩個或多個用戶端可能會寫入變更 toohello 相同項目在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="bfc31-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="bfc31-260">沒有衝突偵測、 hello 最後一次寫入會覆寫任何先前的更新。</span><span class="sxs-lookup"><span data-stu-id="bfc31-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="bfc31-261"> 會假設每筆交易都可以認可，因此不會使用任何資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="bfc31-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="bfc31-262">認可交易之前, 開放式並行存取控制會確認沒有其他交易已修改 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="bfc31-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="bfc31-263">如果已修改 hello 資料，會回復 hello 認可交易。</span><span class="sxs-lookup"><span data-stu-id="bfc31-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="bfc31-264">行動應用程式透過追蹤使用 hello 變更 tooeach 項目，支援開放式並行存取控制`version`定義您的行動裝置應用程式後端中每個資料表的系統屬性資料行。</span><span class="sxs-lookup"><span data-stu-id="bfc31-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="bfc31-265">每次更新一筆記錄時，行動應用程式設定 hello`version`屬性，該記錄 tooa 新值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="bfc31-266">每個更新要求期間 hello `version` hello 記錄 hello 要求所包含的屬性是比較的 toohello hello hello 伺服器上的記錄相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="bfc31-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="bfc31-267">如果版本傳遞與 hello 要求不符合 hello 後端，則 hello 用戶端程式庫引發`MobileServicePreconditionFailedException<T>`例外狀況。</span><span class="sxs-lookup"><span data-stu-id="bfc31-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="bfc31-268">hello hello 例外狀況所包含的型別是 hello hello 後端包含 hello 伺服器 hello 記錄版本記錄。</span><span class="sxs-lookup"><span data-stu-id="bfc31-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="bfc31-269">hello 應用程式可以接著使用此資訊 toodecide 是否 tooexecute hello 更新要求，再次以正確的 hello `version` hello 的後端 toocommit 變更的值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="bfc31-270">Hello 的 hello 資料表類別上定義的資料行`version`系統屬性 tooenable 開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="bfc31-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="bfc31-271">例如：</span><span class="sxs-lookup"><span data-stu-id="bfc31-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="bfc31-272">使用不具類型的資料表的應用程式會啟用開放式並行存取所設定的 hello`Version`加上旗標上`SystemProperties`hello 的資料表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bfc31-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="bfc31-273">在加法 tooenabling 開放式並行存取，您也必須攔截 hello`MobileServicePreconditionFailedException<T>`時呼叫程式碼中的例外狀況[UpdateAsync]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="bfc31-274">藉由套用正確的 hello 解決 hello 衝突`version`toothe 更新記錄，以及呼叫[UpdateAsync]以 hello 已解決的記錄。</span><span class="sxs-lookup"><span data-stu-id="bfc31-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="bfc31-275">hello，下列程式碼顯示如何 tooresolve 寫入一次偵測到衝突：</span><span class="sxs-lookup"><span data-stu-id="bfc31-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="bfc31-276">如需詳細資訊，請參閱 hello[離線 Azure 行動應用程式中的資料同步處理]主題。</span><span class="sxs-lookup"><span data-stu-id="bfc31-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="bfc31-277"><a name="binding"></a>如何： 繫結行動應用程式資料 tooa Windows 使用者介面</span><span class="sxs-lookup"><span data-stu-id="bfc31-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="bfc31-278">本節說明如何 toodisplay 傳回資料物件在 Windows 應用程式中使用 UI 項目。</span><span class="sxs-lookup"><span data-stu-id="bfc31-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="bfc31-279">下列範例程式碼會繫結 hello 清單不完整的項目查詢與 toohello 來源。</span><span class="sxs-lookup"><span data-stu-id="bfc31-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="bfc31-280">[MobileServiceCollection] 會建立 Mobile Apps 感知的繫結集合。</span><span class="sxs-lookup"><span data-stu-id="bfc31-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="bfc31-281">有些控制項在 hello managed 介面呼叫的執行階段支援[ISupportIncrementalLoading]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="bfc31-282">這個介面可讓控制項 toorequest hello 使用者捲動時的額外資料。</span><span class="sxs-lookup"><span data-stu-id="bfc31-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="bfc31-283">沒有內建支援的通用 Windows 應用程式，透過此介面[MobileServiceIncrementalLoadingCollection]，這會自動處理從 hello 控制項呼叫。</span><span class="sxs-lookup"><span data-stu-id="bfc31-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="bfc31-284">在 Windows 應用程式中使用 `MobileServiceIncrementalLoadingCollection` ，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="bfc31-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="bfc31-285">toouse hello 新的集合，在 Windows Phone 8 和"Silverlight 」 應用程式，使用 hello`ToCollection`的擴充方法`IMobileServiceTableQuery<T>`和`IMobileServiceTable<T>`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="bfc31-286">tooload 資料呼叫`LoadMoreItemsAsync()`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="bfc31-287">當您使用藉由呼叫建立 hello 集合`ToCollectionAsync`或`ToCollection`，取得可以繫結的 tooUI 控制項的集合。</span><span class="sxs-lookup"><span data-stu-id="bfc31-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="bfc31-288">此集合有分頁感知功能。</span><span class="sxs-lookup"><span data-stu-id="bfc31-288">This collection is paging-aware.</span></span>  <span data-ttu-id="bfc31-289">Hello 集合從網路載入資料，因為載入有時會失敗。</span><span class="sxs-lookup"><span data-stu-id="bfc31-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="bfc31-290">toohandle 這類失敗，覆寫 hello`OnException`方法`MobileServiceIncrementalLoadingCollection`太造成呼叫 toohandle 例外狀況`LoadMoreItemsAsync`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="bfc31-291">請考慮您的資料表有許多欄位，但您只想 toodisplay 其中一個，在您的控制項。</span><span class="sxs-lookup"><span data-stu-id="bfc31-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="bfc31-292">您可能使用 hello 指引 hello 前面一節中 「[選取特定資料行](#selecting)"tooselect 特定資料行 toodisplay hello UI 中的。</span><span class="sxs-lookup"><span data-stu-id="bfc31-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="bfc31-293"><a name="pagesize"></a>變更 hello 頁面大小</span><span class="sxs-lookup"><span data-stu-id="bfc31-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="bfc31-294">Azure Mobile Apps 預設針對每個要求最多會傳回 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="bfc31-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="bfc31-295">您可以藉由增加 hello hello 用戶端和伺服器上的最大頁面大小變更 hello 分頁大小。</span><span class="sxs-lookup"><span data-stu-id="bfc31-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="bfc31-296">tooincrease hello 要求的頁面大小，指定`PullOptions`時使用`PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="bfc31-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="bfc31-297">假設您已經 hello`PageSize`等於 tooor 大於 100 hello 伺服器中，要求會傳回最多 100 個項目。</span><span class="sxs-lookup"><span data-stu-id="bfc31-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="bfc31-298"><a name="#offlinesync"></a>使用離線資料表</span><span class="sxs-lookup"><span data-stu-id="bfc31-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="bfc31-299">離線的資料表會使用本機的 SQLite 儲存 toostore 資料離線時使用。</span><span class="sxs-lookup"><span data-stu-id="bfc31-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="bfc31-300">作業會針對 hello 完成的所有資料表 SQLite 本機都儲存而非 hello 遠端伺服器存放都區。</span><span class="sxs-lookup"><span data-stu-id="bfc31-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="bfc31-301">toocreate 離線的資料表中，先準備您的專案：</span><span class="sxs-lookup"><span data-stu-id="bfc31-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="bfc31-302">在 Visual Studio 中，以滑鼠右鍵按一下 hello 方案 >**管理方案的 NuGet 套件...**，然後尋找並安裝**Microsoft.Azure.Mobile.Client.SQLiteStore** hello 方案中的所有專案的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="bfc31-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="bfc31-303">（選擇性） toosupport Windows 裝置，安裝其中一個 hello 遵循 SQLite 執行階段封裝：</span><span class="sxs-lookup"><span data-stu-id="bfc31-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="bfc31-304">**Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="bfc31-305">**Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="bfc31-306">**通用 Windows 平台**安裝[SQLite 對通用 Windows hello][5]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="bfc31-307">(選擇性)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-307">(Optional).</span></span> <span data-ttu-id="bfc31-308">針對 Windows 裝置，請按一下**參考** > **加入參考...**，展開 hello **Windows**資料夾 >**延伸**，然後啟用適當的 hello **SQLite 適用於 Windows 的**hello以及SDK**適用於 Windows 的 visual c + + 2013 Runtime** SDK。</span><span class="sxs-lookup"><span data-stu-id="bfc31-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="bfc31-309">hello SQLite SDK 的名稱會稍微不同的每個 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="bfc31-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="bfc31-310">在建立資料表參考之前，必須先備妥 hello 本機存放區：</span><span class="sxs-lookup"><span data-stu-id="bfc31-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="bfc31-311">存放區初始化動作通常是在建立 hello 用戶端之後。</span><span class="sxs-lookup"><span data-stu-id="bfc31-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="bfc31-312">hello **OfflineDbPath**應該是適用於所有支援的平台上的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc31-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="bfc31-313">如果 hello 路徑是完整的路徑 （也就是它的開頭斜線），則會使用該路徑。</span><span class="sxs-lookup"><span data-stu-id="bfc31-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="bfc31-314">如果 hello 路徑的格式不完整，hello 檔案被放在特定平台的位置。</span><span class="sxs-lookup"><span data-stu-id="bfc31-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="bfc31-315">針對 iOS 和 Android 裝置，hello 預設路徑會是 hello"個人 Files"資料夾。</span><span class="sxs-lookup"><span data-stu-id="bfc31-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="bfc31-316">適用於 Windows 裝置 hello 預設路徑會是 hello 特定應用程式"AppData"資料夾。</span><span class="sxs-lookup"><span data-stu-id="bfc31-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="bfc31-317">可取得資料表參考使用 hello`GetSyncTable<>`方法：</span><span class="sxs-lookup"><span data-stu-id="bfc31-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="bfc31-318">您不需要 tooauthenticate toouse 離線的資料表。</span><span class="sxs-lookup"><span data-stu-id="bfc31-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="bfc31-319">您會與 hello 後端服務進行通訊時，只需要 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="bfc31-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="bfc31-320"><a name="syncoffline"></a>同步處理離線資料表</span><span class="sxs-lookup"><span data-stu-id="bfc31-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="bfc31-321">根據預設離線資料表未同步處理與 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="bfc31-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="bfc31-322">同步處理會分割成兩個部分。</span><span class="sxs-lookup"><span data-stu-id="bfc31-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="bfc31-323">您可以透過下載新的項目，個別推送變更。</span><span class="sxs-lookup"><span data-stu-id="bfc31-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="bfc31-324">以下是典型的同步處理方法：</span><span class="sxs-lookup"><span data-stu-id="bfc31-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="bfc31-325">如果 hello 第一個引數太`PullAsync`為 null，則不會使用增量同步處理。</span><span class="sxs-lookup"><span data-stu-id="bfc31-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="bfc31-326">每個同步處理作業會擷取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="bfc31-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="bfc31-327">hello SDK 執行隱含`PushAsync()`提取記錄前。</span><span class="sxs-lookup"><span data-stu-id="bfc31-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="bfc31-328">衝突處理會發生在 `PullAsync()` 方法。</span><span class="sxs-lookup"><span data-stu-id="bfc31-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="bfc31-329">您可以處理相同衝突 hello 線上資料表的方式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="bfc31-330">hello 衝突產生時`PullAsync()`hello insert、 update 或 delete 期間會呼叫而不是。</span><span class="sxs-lookup"><span data-stu-id="bfc31-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="bfc31-331">如果發生多個衝突，則會將它們會搭配至單一 MobileServicePushFailedException。</span><span class="sxs-lookup"><span data-stu-id="bfc31-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="bfc31-332">個別處理每一個失敗。</span><span class="sxs-lookup"><span data-stu-id="bfc31-332">Handle each failure separately.</span></span>

## <span data-ttu-id="bfc31-333"><a name="#customapi"></a>使用自訂 API</span><span class="sxs-lookup"><span data-stu-id="bfc31-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="bfc31-334">自訂 API 可讓您 toodefine 自訂端點來公開伺服器功能並不對應 tooan 插入、 更新、 刪除或讀取作業。</span><span class="sxs-lookup"><span data-stu-id="bfc31-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="bfc31-335">透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="bfc31-336">您可以呼叫自訂 API 透過呼叫其中一個 hello [InvokeApiAsync] hello 用戶端上的方法。</span><span class="sxs-lookup"><span data-stu-id="bfc31-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="bfc31-337">例如，下列程式碼行 hello 會傳送 POST 要求 toohello **completeAll** hello 後端 API:</span><span class="sxs-lookup"><span data-stu-id="bfc31-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="bfc31-338">這種形式是具類型的方法呼叫，而且需要該 hello **MarkAllResult**傳回型別定義。</span><span class="sxs-lookup"><span data-stu-id="bfc31-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="bfc31-339">具類型的和不具類型的方法皆受支援。</span><span class="sxs-lookup"><span data-stu-id="bfc31-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="bfc31-340">hello InvokeApiAsync() 方法前面加上 ' / api /' toohello API 您想 toocall，除非應用程式開發介面 hello 開頭 '/'。</span><span class="sxs-lookup"><span data-stu-id="bfc31-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="bfc31-341">例如：</span><span class="sxs-lookup"><span data-stu-id="bfc31-341">For example:</span></span>

* <span data-ttu-id="bfc31-342">`InvokeApiAsync("completeAll",...)`呼叫 /api/completeAll hello 後端</span><span class="sxs-lookup"><span data-stu-id="bfc31-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="bfc31-343">`InvokeApiAsync("/.auth/me",...)`呼叫 /.auth/me hello 後端</span><span class="sxs-lookup"><span data-stu-id="bfc31-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="bfc31-344">您可以使用任何 WebAPI，包括與 Azure 行動應用程式未定義這些 WebAPIs InvokeApiAsync toocall。</span><span class="sxs-lookup"><span data-stu-id="bfc31-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="bfc31-345">當您使用 InvokeApiAsync() 時，與 hello 要求傳送 hello 適當標頭，包括驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="bfc31-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="bfc31-346"><a name="authentication"></a>驗證使用者</span><span class="sxs-lookup"><span data-stu-id="bfc31-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="bfc31-347">Mobile Apps 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory)，來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc31-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="bfc31-348">您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="bfc31-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="bfc31-349">您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。</span><span class="sxs-lookup"><span data-stu-id="bfc31-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="bfc31-350">如需詳細資訊，請參閱 hello 教學課程[新增 authentication tooyour 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="bfc31-351">支援兩種驗證流程：*用戶端管理*和*伺服器管理*流程。</span><span class="sxs-lookup"><span data-stu-id="bfc31-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="bfc31-352">hello 管理伺服器的流量提供 hello 最簡單的驗證體驗，它會仰賴 hello 提供者 web 驗證介面。</span><span class="sxs-lookup"><span data-stu-id="bfc31-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="bfc31-353">因為它是倚賴特定提供者裝置特有的 Sdk 與裝置特定功能的更深入整合能 hello 管理用戶端流量。</span><span class="sxs-lookup"><span data-stu-id="bfc31-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="bfc31-354">我們建議在生產應用程式中使用用戶端管理的流程。</span><span class="sxs-lookup"><span data-stu-id="bfc31-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="bfc31-355">tooset 驗證設定，您必須具有一個或多個身分識別提供者註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="bfc31-356">hello 身分識別提供者會產生用戶端識別碼和您的應用程式的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="bfc31-357">這些值接著會在您的後端 tooenable Azure 應用程式服務驗證/授權設定。</span><span class="sxs-lookup"><span data-stu-id="bfc31-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="bfc31-358">如需詳細資訊，請遵循 hello 詳細教學課程中的指示[新增 authentication tooyour 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="bfc31-359">此章節將討論下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="bfc31-360">用戶端管理的驗證</span><span class="sxs-lookup"><span data-stu-id="bfc31-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="bfc31-361">伺服器管理的驗證</span><span class="sxs-lookup"><span data-stu-id="bfc31-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="bfc31-362">快取的 hello 驗證權杖</span><span class="sxs-lookup"><span data-stu-id="bfc31-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="bfc31-363"><a name="clientflow"></a>用戶端管理的驗證</span><span class="sxs-lookup"><span data-stu-id="bfc31-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="bfc31-364">您的應用程式可以獨立連絡 hello 身分識別提供者，然後在與您的後端的登入期間提供 hello 傳回的權杖。</span><span class="sxs-lookup"><span data-stu-id="bfc31-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="bfc31-365">此用戶端流程可讓您 tooprovide 單一登入體驗的使用者或 tooretrieve hello 身分識別提供者的其他使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bfc31-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="bfc31-366">用戶端流量驗證為慣用的 toousing 伺服器流程 hello 身分識別提供者 SDK 提供較原始的 UX 操作，並允許其他自訂。</span><span class="sxs-lookup"><span data-stu-id="bfc31-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="bfc31-367">範例可供下列用戶端流程驗證模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="bfc31-368">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="bfc31-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="bfc31-369">Facebook 或 Google</span><span class="sxs-lookup"><span data-stu-id="bfc31-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="bfc31-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="bfc31-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="bfc31-371"><a name="adal"></a>驗證使用者以 hello Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="bfc31-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="bfc31-372">您可以使用 hello Active Directory 驗證程式庫 (ADAL) tooinitiate 從 hello 用戶端使用 Azure Active Directory 驗證的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="bfc31-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="bfc31-373">設定您的行動裝置應用程式後端的 AAD 登入下列 hello [tooconfigure Active Directory 登入服務的應用程式如何]教學課程。</span><span class="sxs-lookup"><span data-stu-id="bfc31-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="bfc31-374">請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="bfc31-375">在 Visual Studio 或 Xamarin Studio，開啟您的專案並加入參考 toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="bfc31-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="bfc31-376">搜尋時，包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="bfc31-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="bfc31-377">新增下列程式碼 tooyour 應用程式，根據您使用 toohello 平台的 hello。</span><span class="sxs-lookup"><span data-stu-id="bfc31-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="bfc31-378">在每個，請遵循取代 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="bfc31-379">取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc31-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="bfc31-380">格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。這個值可以複製 hello 網域 索引標籤中 Azure Active Directory 中 hello [Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="bfc31-381">取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="bfc31-382">您可以從 hello 取得 hello 用戶端識別碼**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="bfc31-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="bfc31-383">取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="bfc31-384">取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。</span><span class="sxs-lookup"><span data-stu-id="bfc31-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="bfc31-385">此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。</span><span class="sxs-lookup"><span data-stu-id="bfc31-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="bfc31-386">每個平台所需的 hello 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="bfc31-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="bfc31-387">**Windows：**</span><span class="sxs-lookup"><span data-stu-id="bfc31-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="bfc31-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="bfc31-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="bfc31-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="bfc31-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="bfc31-390"><a name="client-facebook"></a>使用來自 Facebook 或 Google 的權杖單一登入</span><span class="sxs-lookup"><span data-stu-id="bfc31-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="bfc31-391">您可以使用 hello 用戶端流量，如 Facebook 或 Google 中此程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="bfc31-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="bfc31-392"><a name="client-livesdk"></a>單一登入使用 Microsoft 帳戶與 hello Live SDK</span><span class="sxs-lookup"><span data-stu-id="bfc31-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="bfc31-393">tooauthenticate 使用者，您必須註冊在 hello 開發人員中心的 Microsoft 帳戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="bfc31-394">請在行動應用程式後端設定註冊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bfc31-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="bfc31-395">toocreate Microsoft 帳戶註冊，並將它連接 tooyour 行動裝置應用程式後端中的步驟完成 hello[註冊您的 Microsoft 帳戶登入的應用程式 toouse]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="bfc31-396">如果您有應用程式的 Windows 市集和 Windows Phone 8/Silverlight 版本，請先註冊 hello Windows 市集版本。</span><span class="sxs-lookup"><span data-stu-id="bfc31-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="bfc31-397">hello 下列程式碼會使用 Live SDK 進行驗證並使用傳回語彙基元 toosign tooyour 行動裝置應用程式後端中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bfc31-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="bfc31-398">如需詳細資訊，請參閱 hello [Windows Live SDK]文件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="bfc31-399"><a name="serverflow"></a>伺服器管理的驗證</span><span class="sxs-lookup"><span data-stu-id="bfc31-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="bfc31-400">當您註冊您的身分識別提供者之後時，呼叫 hello [LoginAsync] hello 與 hello [d] 上的方法[MobileServiceAuthenticationProvider]您的提供者的值。</span><span class="sxs-lookup"><span data-stu-id="bfc31-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="bfc31-401">比方說，hello 下列程式碼起始的伺服器流程登入使用 Facebook。</span><span class="sxs-lookup"><span data-stu-id="bfc31-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="bfc31-402">如果您使用 Facebook 以外的身分識別提供者，變更 hello 值[MobileServiceAuthenticationProvider] toohello 值提供者。</span><span class="sxs-lookup"><span data-stu-id="bfc31-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="bfc31-403">資料流程中的伺服器，Azure 應用程式服務會管理 hello OAuth 驗證流程，藉由顯示 hello 登入頁面的 hello 選的提供者。</span><span class="sxs-lookup"><span data-stu-id="bfc31-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="bfc31-404">一次 hello 身分識別提供者傳回時，Azure 應用程式服務會產生應用程式服務驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="bfc31-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="bfc31-405">hello [LoginAsync]方法會傳回[MobileServiceUser]，這樣會提供這兩個 hello [UserId] hello 的驗證之使用者與 hello [MobileServiceAuthenticationToken]，做為 JSON web 權杖 (JWT)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="bfc31-406">您可以快取並重複使用此權杖，直到它到期為止。</span><span class="sxs-lookup"><span data-stu-id="bfc31-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="bfc31-407">如需詳細資訊，請參閱[Caching hello 驗證語彙基元](#caching)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="bfc31-408"><a name="caching"></a>快取的 hello 驗證權杖</span><span class="sxs-lookup"><span data-stu-id="bfc31-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="bfc31-409">在某些情況下，hello 呼叫 toohello 登入方法可避免在 hello 第一次成功驗證之後儲存 hello 驗證 token 來自 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="bfc31-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="bfc31-410">Windows 市集和 UWP 應用程式可以使用[PasswordVault] toocache 目前驗證語彙基元成功登入之後，，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="bfc31-411">hello 使用者識別碼值會儲存為 hello hello 認證的使用者名稱和 hello 語彙基元為 hello 儲存為 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="bfc31-412">您可以在後續的創檢查 hello **PasswordVault**快取的認證。</span><span class="sxs-lookup"><span data-stu-id="bfc31-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="bfc31-413">hello 下列範例會使用快取的認證時找不到，，否則為嘗試一次與 hello 後端 tooauthenticate:</span><span class="sxs-lookup"><span data-stu-id="bfc31-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="bfc31-414">當您登出使用者時，您也必須移除 hello 預存認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="bfc31-415">Xamarin 應用程式使用 hello [Xamarin.Auth]中的應用程式開發介面 toosecurely 存放區認證**帳戶**物件。</span><span class="sxs-lookup"><span data-stu-id="bfc31-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="bfc31-416">如需使用這些 Api 的範例，請參閱 hello [AuthStore.cs]程式碼檔案中 hello [ContosoMoments 相片分享範例](https://github.com/azure-appservice-samples/ContosoMoments)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="bfc31-417">當您使用管理用戶端驗證時，您也可以快取從您的提供者，例如 Facebook 或 Twitter 取得的 hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bfc31-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="bfc31-418">這個語彙基元可以提供的 toorequest hello 後端中，從新的驗證權杖，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bfc31-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="bfc31-419"><a name="pushnotifications"></a>推播通知</span><span class="sxs-lookup"><span data-stu-id="bfc31-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="bfc31-420">下列主題涵蓋了推播通知的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="bfc31-421">註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="bfc31-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="bfc31-422">取得 Windows 市集封裝 SID</span><span class="sxs-lookup"><span data-stu-id="bfc31-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="bfc31-423">利用跨平台範本進行註冊</span><span class="sxs-lookup"><span data-stu-id="bfc31-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="bfc31-424"><a name="register-for-push"></a>做法：註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="bfc31-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="bfc31-425">hello 行動應用程式用戶端可讓您與 Azure 通知中心的推播通知的 tooregister。</span><span class="sxs-lookup"><span data-stu-id="bfc31-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="bfc31-426">您註冊時，取得的控制代碼，您取得從 hello 平台專屬推播通知服務 (PNS)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="bfc31-427">當您建立 hello 註冊，然後提供此值以及任何標記。</span><span class="sxs-lookup"><span data-stu-id="bfc31-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="bfc31-428">hello 下列程式碼會註冊您的 Windows 應用程式的推播通知以 hello Windows 通知服務 (WNS):</span><span class="sxs-lookup"><span data-stu-id="bfc31-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="bfc31-429">如果您要推入 tooWNS，則您必須[取得 Windows 市集封裝 SID](#package-sid)。</span><span class="sxs-lookup"><span data-stu-id="bfc31-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="bfc31-430">如需有關 Windows 應用程式，包括如何 tooregister 的範本註冊，請參閱[新增推播通知 tooyour 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="bfc31-431">不支援從 hello 用戶端要求標記。</span><span class="sxs-lookup"><span data-stu-id="bfc31-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="bfc31-432">註冊時會自動捨棄標記要求。</span><span class="sxs-lookup"><span data-stu-id="bfc31-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="bfc31-433">如果您想 tooregister 標記與您的裝置，建立您的身分使用 hello 通知中樞 API tooperform hello 註冊自訂 API。</span><span class="sxs-lookup"><span data-stu-id="bfc31-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="bfc31-434">[呼叫自訂 API hello](#customapi)而不是 hello`RegisterNativeAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="bfc31-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="bfc31-435"><a name="package-sid"></a>如何：取得 Windows 市集封裝 SID</span><span class="sxs-lookup"><span data-stu-id="bfc31-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="bfc31-436">在 Windows 市集應用程式中啟用推播通知需有封裝 SID。</span><span class="sxs-lookup"><span data-stu-id="bfc31-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="bfc31-437">tooreceive 封裝 SID，以 hello Windows 市集註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="bfc31-438">tooobtain 此值：</span><span class="sxs-lookup"><span data-stu-id="bfc31-438">tooobtain this value:</span></span>

1. <span data-ttu-id="bfc31-439">在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello Windows 市集應用程式專案中，按一下**存放區** > **將應用程式建立關聯以 hello 存放區...**.</span><span class="sxs-lookup"><span data-stu-id="bfc31-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="bfc31-440">在 hello 精靈中，按一下 **下一步**，使用您的 Microsoft 帳戶登入，輸入您的應用程式中的名稱**新的應用程式名稱保留**，然後按一下 **保留**。</span><span class="sxs-lookup"><span data-stu-id="bfc31-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="bfc31-441">Hello 應用程式註冊已成功建立，請選取 hello 應用程式名稱後，請按一下**下一步**，然後按一下**關聯**。</span><span class="sxs-lookup"><span data-stu-id="bfc31-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="bfc31-442">登入 toohello [Windows 開發人員中心]使用您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfc31-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="bfc31-443">在下**我的應用程式**，按一下您建立 hello 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="bfc31-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="bfc31-444">按一下**應用程式管理** > **應用程式識別**，然後向下 toofind 捲動您**封裝 SID**。</span><span class="sxs-lookup"><span data-stu-id="bfc31-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="bfc31-445">許多用途的 hello 封裝 SID 將其視為一個 URI，在此情況下您需要 toouse *ms 應用程式: / /*為 hello 配置。</span><span class="sxs-lookup"><span data-stu-id="bfc31-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="bfc31-446">記下您的封裝 SID 做為前置詞，這個值串連起來所構成的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="bfc31-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="bfc31-447">Xamarin 應用程式需要一些額外的程式碼 toobe 無法 tooregister hello iOS 或 Android 平台上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bfc31-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="bfc31-448">如需詳細資訊，請參閱您的平台的 hello 主題：</span><span class="sxs-lookup"><span data-stu-id="bfc31-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="bfc31-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="bfc31-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="bfc31-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="bfc31-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="bfc31-451"><a name="register-xplat"></a>如何： 註冊推播範本 toosend 跨平台通知</span><span class="sxs-lookup"><span data-stu-id="bfc31-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="bfc31-452">tooregister 範本使用 hello `RegisterAsync()` hello 範本，如下所示的方法：</span><span class="sxs-lookup"><span data-stu-id="bfc31-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="bfc31-453">您的範本應該`JObject`類型，而且可以包含多個範本中下列 JSON 格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="bfc31-454">hello 方法**RegisterAsync()**也接受次要磚：</span><span class="sxs-lookup"><span data-stu-id="bfc31-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="bfc31-455">為確保安全，註冊期間會移除所有標籤。</span><span class="sxs-lookup"><span data-stu-id="bfc31-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="bfc31-456">tooadd 標記 tooinstallations 或內安裝的範本，查看 [Azure 行動應用程式的工作與 hello.NET 後端伺服器 SDK]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="bfc31-457">toosend 通知使用這些已註冊的範本，請參閱 toohello[通知中樞 Api]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="bfc31-458"><a name="misc"></a>其他主題</span><span class="sxs-lookup"><span data-stu-id="bfc31-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="bfc31-459"><a name="errors"></a>作法：處理錯誤</span><span class="sxs-lookup"><span data-stu-id="bfc31-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="bfc31-460">Hello 後端中發生錯誤時，hello 用戶端 SDK 引發`MobileServiceInvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="bfc31-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="bfc31-461">下列範例會示範如何 toohandle hello 後端所傳回的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="bfc31-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="bfc31-462">處理錯誤狀況的其他範例，請參閱在 hello[行動應用程式檔案範例]。</span><span class="sxs-lookup"><span data-stu-id="bfc31-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="bfc31-463">[LoggingHandler]範例提供記錄委派處理常式 toolog hello 提出的要求，toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="bfc31-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="bfc31-464"><a name="headers"></a>作法：自訂要求標頭</span><span class="sxs-lookup"><span data-stu-id="bfc31-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="bfc31-465">toosupport 特定的應用程式案例中，您可能需要與 hello 行動裝置應用程式後端 toocustomize 通訊。</span><span class="sxs-lookup"><span data-stu-id="bfc31-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="bfc31-466">比方說，您可能想 tooadd 自訂標頭 tooevery 外送要求，或甚至變更回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="bfc31-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="bfc31-467">您可以使用自訂[DelegatingHandler]，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bfc31-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[新增 authentication tooyour 應用程式]: app-service-mobile-windows-store-dotnet-get-started-users.md
[離線 Azure 行動應用程式中的資料同步處理]: app-service-mobile-offline-data-sync.md
[新增推播通知 tooyour 應用程式]: app-service-mobile-windows-store-dotnet-get-started-push.md
[註冊您的 Microsoft 帳戶登入的應用程式 toouse]: app-service-mobile-how-to-configure-microsoft-authentication.md
[tooconfigure Active Directory 登入服務的應用程式如何]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[建立參考 tooan 不具型別的資料表]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[採取]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[選取]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[略過]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[其中]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure 入口網站]: https://portal.azure.com/
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows 開發人員中心]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[通知中樞 Api]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[行動應用程式檔案範例]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 文件]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
