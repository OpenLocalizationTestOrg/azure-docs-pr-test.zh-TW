---
title: "使用 App Service Mobile Apps 受管理的用戶端程式庫 (Windows | Microsoft Docs"
description: "了解如何搭配 Windows 和 Xamarin 應用程式針對 Azure App Service Mobile Apps 使用 .NET 用戶端。"
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
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="31b3b-103">如何針對 Azure Mobile Apps 使用受管理的用戶端</span><span class="sxs-lookup"><span data-stu-id="31b3b-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="31b3b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="31b3b-104">Overview</span></span>
<span data-ttu-id="31b3b-105">本指南將示範如何在 Windows 和 Xamarin 應用程式中針對 Azure App Service Mobile Apps 使用受管理的用戶端程式庫，來執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="31b3b-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="31b3b-106">如果您不熟悉 Mobile Apps，應該考慮先完成 [Azure Mobile Apps 快速入門][1]教學課程。</span><span class="sxs-lookup"><span data-stu-id="31b3b-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="31b3b-107">在本指南中，我們會著重於用戶端受管理的 SDK。</span><span class="sxs-lookup"><span data-stu-id="31b3b-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="31b3b-108">若要深入了解 Mobile Apps 的伺服器端 SDK，請參閱 [.NET 伺服器 SDK][2] 或 [Node.js 伺服器 SDK][3] 的文件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="31b3b-109">參考文件</span><span class="sxs-lookup"><span data-stu-id="31b3b-109">Reference documentation</span></span>
<span data-ttu-id="31b3b-110">用戶端 SDK 的參考文件位於此處：[Azure Mobile Apps .NET 用戶端參考資料][4]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="31b3b-111">您也可以在 [Azure 範例 GitHub 儲存機制][5]中找到數個用戶端範例。</span><span class="sxs-lookup"><span data-stu-id="31b3b-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="31b3b-112">支援的平台</span><span class="sxs-lookup"><span data-stu-id="31b3b-112">Supported Platforms</span></span>
<span data-ttu-id="31b3b-113">.NET 平台支援下列平台︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="31b3b-114">適用於 API 19 到 24 (KitKat 到 Nougat) 的 Xamarin Android 版本</span><span class="sxs-lookup"><span data-stu-id="31b3b-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="31b3b-115">適用於 iOS 8.0 版和更新版本的 Xamarin iOS 版本</span><span class="sxs-lookup"><span data-stu-id="31b3b-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="31b3b-116">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="31b3b-116">Universal Windows Platform</span></span>
* <span data-ttu-id="31b3b-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="31b3b-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="31b3b-118">Windows Phone 8.0 (Silverlight 應用程式除外)</span><span class="sxs-lookup"><span data-stu-id="31b3b-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="31b3b-119">「伺服器流程」驗證在呈現的 UI 中使用 WebView。</span><span class="sxs-lookup"><span data-stu-id="31b3b-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="31b3b-120">如果裝置無法呈現 WebView UI，您需要其他驗證方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="31b3b-121">因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。</span><span class="sxs-lookup"><span data-stu-id="31b3b-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="31b3b-122"><a name="setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="31b3b-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="31b3b-123">我們假設您已建立並發佈您的行動應用程式後端專案 (至少包含一個資料表)。</span><span class="sxs-lookup"><span data-stu-id="31b3b-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="31b3b-124">在本主題使用的程式碼中，資料表的名稱為 `TodoItem`，且其具有下列資料行：`Id`、`Text` 和 `Complete`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="31b3b-125">此資料表與您完成 [Azure Mobile Apps 快速入門][1]時所建立的資料表相同。</span><span class="sxs-lookup"><span data-stu-id="31b3b-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="31b3b-126">C# 中對應的具類型用戶端類型為下列類別：</span><span class="sxs-lookup"><span data-stu-id="31b3b-126">The corresponding typed client-side type in C# is the following class:</span></span>

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

<span data-ttu-id="31b3b-127">[JsonPropertyAttribute][6] 是用來定義用戶端欄位與資料表欄位之間的 *PropertyName* 對應。</span><span class="sxs-lookup"><span data-stu-id="31b3b-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="31b3b-128">若要了解如何在 Mobile Apps 後端中建立資料表，請參閱 [.NET 伺服器 SDK 主題][7] 或 [Node.js 伺服器 SDK 主題][8]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="31b3b-129">如果您已使用＜快速入門＞在 Azure 入口網站中建立行動應用程式後端，也可以使用 **Azure 入口網站** 中的 [Azure 入口網站]設定。</span><span class="sxs-lookup"><span data-stu-id="31b3b-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="31b3b-130">做法︰安裝受管理的用戶端 SDK 封裝</span><span class="sxs-lookup"><span data-stu-id="31b3b-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="31b3b-131">使用下列其中一種方法，從 [NuGet][9] 安裝適用於 Mobile Apps 的受管理用戶端 SDK 套件：</span><span class="sxs-lookup"><span data-stu-id="31b3b-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="31b3b-132">**Visual Studio** 以滑鼠右鍵按一下您的專案、按一下 [管理 NuGet 套件]，搜尋 `Microsoft.Azure.Mobile.Client` 套件，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="31b3b-133">**Xamarin Studio** 以滑鼠右鍵按一下您的專案、按一下 [新增] > [新增 NuGet 套件]，搜尋 `Microsoft.Azure.Mobile.Client ` 套件，然後按一下 [新增套件]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="31b3b-134">在您的主要活動檔案中，記得加入下列 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="31b3b-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="31b3b-135"><a name="symbolsource"></a>做法︰使用 Visual Studio 中的偵錯符號</span><span class="sxs-lookup"><span data-stu-id="31b3b-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="31b3b-136">您可以從 [SymbolSource][10] 取得適用於 Microsoft.Azure.Mobile 命名空間的符號。</span><span class="sxs-lookup"><span data-stu-id="31b3b-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="31b3b-137">若要將 SymbolSource 與 Visual Studio 整合，請參閱 [SymbolSource 指示][11]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="31b3b-138"><a name="create-client"></a>建立 Mobile Apps 用戶端</span><span class="sxs-lookup"><span data-stu-id="31b3b-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="31b3b-139">下列程式碼會建立用來存取「行動應用程式」後端的 [MobileServiceClient][12] 物件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="31b3b-140">在上述程式碼中，以行動應用程式後端 URL 取代 `MOBILE_APP_URL` ，這位於 [Azure 入口網站]的行動應用程式後端刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="31b3b-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="31b3b-141">MobileServiceClient 物件應該是單一的。</span><span class="sxs-lookup"><span data-stu-id="31b3b-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="31b3b-142">使用資料表</span><span class="sxs-lookup"><span data-stu-id="31b3b-142">Work with Tables</span></span>
<span data-ttu-id="31b3b-143">下一節將詳細說明如何搜尋和擷取記錄，以及修改資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="31b3b-144">本文涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="31b3b-144">The following topics are covered:</span></span>

* [<span data-ttu-id="31b3b-145">建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="31b3b-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="31b3b-146">查詢資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-146">Query data</span></span>](#querying)
* [<span data-ttu-id="31b3b-147">篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="31b3b-148">排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="31b3b-149">以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="31b3b-150">選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="31b3b-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="31b3b-151">依據識別碼查詢記錄</span><span class="sxs-lookup"><span data-stu-id="31b3b-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="31b3b-152">處理不具類型的查詢</span><span class="sxs-lookup"><span data-stu-id="31b3b-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="31b3b-153">插入資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="31b3b-154">更新資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="31b3b-155">刪除資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="31b3b-156">衝突解決和開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="31b3b-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="31b3b-157">繫結至 Windows 使用者介面</span><span class="sxs-lookup"><span data-stu-id="31b3b-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="31b3b-158">變更頁面大小</span><span class="sxs-lookup"><span data-stu-id="31b3b-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="31b3b-159"><a name="instantiating"></a>作法：建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="31b3b-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="31b3b-160">存取或修改後端資料表中資料的所有程式碼，都會在 `MobileServiceTable` 物件上呼叫函數。</span><span class="sxs-lookup"><span data-stu-id="31b3b-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="31b3b-161">透過呼叫 [GetTable] 方法來取得資料表的參考，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="31b3b-162">傳回的物件會使用具類型的序列化模型。</span><span class="sxs-lookup"><span data-stu-id="31b3b-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="31b3b-163">也支援不具類型的序列化模型。</span><span class="sxs-lookup"><span data-stu-id="31b3b-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="31b3b-164">下列範例會[建立不具類型的資料表參考]：</span><span class="sxs-lookup"><span data-stu-id="31b3b-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="31b3b-165">在不具類型的查詢中，您必須指定基礎 OData 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="31b3b-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="31b3b-166"><a name="querying"></a>如何：查詢行動應用程式中的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="31b3b-167">本節將說明如何對行動應用程式後端發出查詢，包括下列功能：</span><span class="sxs-lookup"><span data-stu-id="31b3b-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="31b3b-168">篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="31b3b-169">排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="31b3b-170">以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="31b3b-171">選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="31b3b-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="31b3b-172">按識別碼查詢資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="31b3b-173">系統會強制使用伺服器控制的頁面大小，以防止傳回所有資料列。</span><span class="sxs-lookup"><span data-stu-id="31b3b-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="31b3b-174">分頁可避免大型資料集的預設要求對服務造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="31b3b-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="31b3b-175">若要傳回超過 50 個資料列，請依照[以分頁方式傳回資料](#paging)所述，使用 `Skip` 和 `Take` 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="31b3b-176"><a name="filtering"></a>作法：篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="31b3b-177">下列程式碼說明如何在查詢中包含 `Where` 子句，以篩選資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="31b3b-178">它會從 `todoTable` 傳回其 `Complete` 屬性等於 `false` 的所有項目。</span><span class="sxs-lookup"><span data-stu-id="31b3b-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="31b3b-179">[Where] 函數會套用資料列篩選述語來查詢資料表。</span><span class="sxs-lookup"><span data-stu-id="31b3b-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="31b3b-180">您可以使用訊息檢查軟體 (例如瀏覽器開發人員工具或 [Fiddler]) 來檢視傳送至後端的要求 URI。</span><span class="sxs-lookup"><span data-stu-id="31b3b-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="31b3b-181">如果您查看要求 URI，會發現查詢字串已經過修改：</span><span class="sxs-lookup"><span data-stu-id="31b3b-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="31b3b-182">伺服器 SDK 會將此 OData 要求轉譯成 SQL 查詢︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="31b3b-183">傳遞至 `Where` 方法的函式可以有任意數目的條件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="31b3b-184">伺服器 SDK 會將此範例轉譯成 SQL 查詢︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="31b3b-185">此查詢也可以分割成多個子句︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="31b3b-186">這兩種方法是相同的，而且可以交換使用。</span><span class="sxs-lookup"><span data-stu-id="31b3b-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="31b3b-187">舊有的選項&mdash;在一個查詢中串連多個述詞&mdash;較為精簡，也是建議的選項。</span><span class="sxs-lookup"><span data-stu-id="31b3b-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="31b3b-188">`Where` 子句可支援被轉譯成 OData 子集的作業。</span><span class="sxs-lookup"><span data-stu-id="31b3b-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="31b3b-189">這些作業包括︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-189">Operations include:</span></span>

* <span data-ttu-id="31b3b-190">關係運算子 (==、!=、<、<=、>、>=)、</span><span class="sxs-lookup"><span data-stu-id="31b3b-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="31b3b-191">算術運算子 (+、-、/、*、%)、</span><span class="sxs-lookup"><span data-stu-id="31b3b-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="31b3b-192">精確度位數 (Math.Floor、Math.Ceiling)、</span><span class="sxs-lookup"><span data-stu-id="31b3b-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="31b3b-193">字串函數 (Length、Substring、Replace、IndexOf、StartsWith、EndsWith)、</span><span class="sxs-lookup"><span data-stu-id="31b3b-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="31b3b-194">日期屬性 (Year、Month、Day、Hour、Minute、Second)、</span><span class="sxs-lookup"><span data-stu-id="31b3b-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="31b3b-195">物件的存取屬性，及</span><span class="sxs-lookup"><span data-stu-id="31b3b-195">Access properties of an object, and</span></span>
* <span data-ttu-id="31b3b-196">結合上述任何運算的運算式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="31b3b-197">在考慮伺服器 SDK 支援的作業時，您可以考慮 [OData v3 文件]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="31b3b-198"><a name="sorting"></a>作法：排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="31b3b-199">下列程式碼將說明如何透過在查詢中加上 [OrderBy] 或 [OrderByDescending] 函式來排序資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="31b3b-200">它會從 `todoTable` 傳回項目，並依據 `Text` 欄位以遞增順序排列。</span><span class="sxs-lookup"><span data-stu-id="31b3b-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

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

### <span data-ttu-id="31b3b-201"><a name="paging"></a>作法：以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="31b3b-202">依預設，後端僅會傳回前 50 筆資料列。</span><span class="sxs-lookup"><span data-stu-id="31b3b-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="31b3b-203">您可以提高傳回的資料列數，方法是呼叫 [Take] 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="31b3b-204">使用 `Take` 搭配 [Skip] 方法來要求查詢傳回之總資料集的特定「頁面」。</span><span class="sxs-lookup"><span data-stu-id="31b3b-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="31b3b-205">執行下列查詢時，會傳回資料表中的前三個項目。</span><span class="sxs-lookup"><span data-stu-id="31b3b-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="31b3b-206">下列已修訂查詢會略過前三個結果，並傳回接下來的三個結果。</span><span class="sxs-lookup"><span data-stu-id="31b3b-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="31b3b-207">此查詢會產生第二「頁」資料，頁面大小為三個項目。</span><span class="sxs-lookup"><span data-stu-id="31b3b-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="31b3b-208">[IncludeTotalCount] 方法會要求已傳回之 *all* 記錄的總數，忽略指定的任何分頁/限制子句：</span><span class="sxs-lookup"><span data-stu-id="31b3b-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="31b3b-209">在實際的應用程式中，您可以搭配頁面巡覽區控制項或類似的 UI 來使用類似上述範例的查詢，以導覽各個頁面。</span><span class="sxs-lookup"><span data-stu-id="31b3b-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="31b3b-210">若要覆寫行動應用程式後端中的 50 個資料列限制，您也必須將 [EnableQueryAttribute] 套用到公用的 GET 方法並指定分頁行為。</span><span class="sxs-lookup"><span data-stu-id="31b3b-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="31b3b-211">套用到方法時，下列設定最多傳回 1000 個資料列：</span><span class="sxs-lookup"><span data-stu-id="31b3b-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="31b3b-212"><a name="selecting"></a>作法：選取特定資料欄</span><span class="sxs-lookup"><span data-stu-id="31b3b-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="31b3b-213">您可以指定結果中要包含的屬性集，方法是在查詢中加上 [Select] 子句。</span><span class="sxs-lookup"><span data-stu-id="31b3b-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="31b3b-214">例如，下列程式碼將示範如何只選取一個欄位以及如何選取及格式化多個欄位：</span><span class="sxs-lookup"><span data-stu-id="31b3b-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
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

<span data-ttu-id="31b3b-215">目前為止說明的所有函式只是不斷添加，因此只要一直鏈結即可。</span><span class="sxs-lookup"><span data-stu-id="31b3b-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="31b3b-216">每一個鏈結的呼叫都會更加影響查詢。</span><span class="sxs-lookup"><span data-stu-id="31b3b-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="31b3b-217">再提供一個範例：</span><span class="sxs-lookup"><span data-stu-id="31b3b-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="31b3b-218"><a name="lookingup"></a>作法：按識別碼查詢資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="31b3b-219">[LookupAsync] 函數可用來查詢具有特定 ID 的資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="31b3b-220"><a name="untypedqueries"></a>如何：執行不具類型的查詢</span><span class="sxs-lookup"><span data-stu-id="31b3b-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="31b3b-221">使用不具類型的資料表物件執行查詢時，您必須藉由呼叫 [ReadAsync]來明確指定 OData 查詢字串，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="31b3b-222">您將收到可用作屬性包的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="31b3b-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="31b3b-223">如需有關 JToken 和 Newtonsoft Json.NET 的詳細資訊，請參閱 [Json.NET] 網站。</span><span class="sxs-lookup"><span data-stu-id="31b3b-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="31b3b-224"><a name="inserting"></a>如何：將資料插入行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="31b3b-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="31b3b-225">所有用戶端類型都必須包含名為 **Id**的成員，其預設為字串。</span><span class="sxs-lookup"><span data-stu-id="31b3b-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="31b3b-226">需要有此 **Id** 才能執行 CRUD 作業和離線同步處理。</span><span class="sxs-lookup"><span data-stu-id="31b3b-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="31b3b-227">下列程式碼將說明如何使用 [InsertAsync] 方法，將新的資料列插入資料表。</span><span class="sxs-lookup"><span data-stu-id="31b3b-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="31b3b-228">參數包含要作為 .NET 物件插入的資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="31b3b-229">如果插入期間沒有在 `todoItem` 包含唯一的自訂識別碼值，則會由伺服器產生 GUID。</span><span class="sxs-lookup"><span data-stu-id="31b3b-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="31b3b-230">在呼叫傳回之後，您可以藉由檢查物件來擷取產生的識別碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="31b3b-231">若要插入不具類型的資料，您可以充份利用 Json.NET：</span><span class="sxs-lookup"><span data-stu-id="31b3b-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="31b3b-232">以下是使用電子郵件地址作為唯一字串 id 的範例：</span><span class="sxs-lookup"><span data-stu-id="31b3b-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="31b3b-233">使用識別碼值</span><span class="sxs-lookup"><span data-stu-id="31b3b-233">Working with ID values</span></span>
<span data-ttu-id="31b3b-234">Mobile Apps 支援資料表的 **id** 資料行使用唯一自訂字串值。</span><span class="sxs-lookup"><span data-stu-id="31b3b-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="31b3b-235">字串值可讓應用程式使用自訂的值，例如電子郵件地址或使用者名稱作為識別碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="31b3b-236">字串識別碼為您提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="31b3b-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="31b3b-237">不需要往返存取資料庫就能產生識別碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="31b3b-238">輕鬆合併不同資料表或資料庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="31b3b-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="31b3b-239">識別碼值與應用程式邏輯的整合更理想。</span><span class="sxs-lookup"><span data-stu-id="31b3b-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="31b3b-240">當插入的記錄上未設定字串識別碼值時，行動應用程式後端會產生唯一值做為識別碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="31b3b-241">您可以使用 [Guid.NewGuid] 方法，在用戶端上或在後端中產生您自己的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="31b3b-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="31b3b-242"><a name="modifying"></a>如何：修改行動應用程式後端中的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="31b3b-243">下列程式碼將說明如何使用 [UpdateAsync] 方法，利用新資訊來更新具相同識別碼的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="31b3b-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="31b3b-244">參數包含要作為 .NET 物件更新的資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="31b3b-245">若要更新不具類型的資料，您可以充份利用 [Json.NET] ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="31b3b-246">更新時，您必須指定 `id` 欄位。</span><span class="sxs-lookup"><span data-stu-id="31b3b-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="31b3b-247">後端會使用 `id` 欄位來識別要更新哪一個資料列。</span><span class="sxs-lookup"><span data-stu-id="31b3b-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="31b3b-248">您可以從 `InsertAsync` 呼叫的結果取得 `id` 欄位。</span><span class="sxs-lookup"><span data-stu-id="31b3b-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="31b3b-249">當您嘗試更新項目但未提供 `id` 值時，就會引發 `ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="31b3b-250"><a name="deleting"></a>如何：刪除行動應用程式後端中的資料</span><span class="sxs-lookup"><span data-stu-id="31b3b-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="31b3b-251">下列程式碼將說明如何使用 [DeleteAsync] 方法，刪除現有的執行個體。</span><span class="sxs-lookup"><span data-stu-id="31b3b-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="31b3b-252">您可以透過 `todoItem` 上設定的 `id` 欄位來識別執行個體。</span><span class="sxs-lookup"><span data-stu-id="31b3b-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="31b3b-253">若要刪除不具類型的資料，您可以充份利用 Json.NET，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="31b3b-254">提出刪除要求時，必須指定 ID。</span><span class="sxs-lookup"><span data-stu-id="31b3b-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="31b3b-255">其他屬性不會傳遞至服務，或者服務會將它們忽略。</span><span class="sxs-lookup"><span data-stu-id="31b3b-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="31b3b-256">`DeleteAsync` 呼叫的結果通常會是 `null`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="31b3b-257">您可以從 `InsertAsync` 呼叫的結果取得所要傳入的 ID。</span><span class="sxs-lookup"><span data-stu-id="31b3b-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="31b3b-258">當您嘗試刪除項目但未指定 `id` 欄位時，會擲回 `MobileServiceInvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="31b3b-259"><a name="optimisticconcurrency"></a>做法：使用開放式並行存取來解決衝突</span><span class="sxs-lookup"><span data-stu-id="31b3b-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="31b3b-260">兩個或多個用戶端可能會同時對相同項目寫入變更。</span><span class="sxs-lookup"><span data-stu-id="31b3b-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="31b3b-261">在沒有偵測到衝突的情況下，最後寫入將覆寫任何先前的更新。</span><span class="sxs-lookup"><span data-stu-id="31b3b-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="31b3b-262"> 會假設每筆交易都可以認可，因此不會使用任何資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="31b3b-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="31b3b-263">在認可交易之前，開放式並行存取控制項會驗證沒有其他交易已修改此資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="31b3b-264">如果資料已修改，則會復原認可的交易。</span><span class="sxs-lookup"><span data-stu-id="31b3b-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="31b3b-265">Mobile Apps 支援開放式並行存取控制項，方法是使用 `version` 系統屬性資料行來追蹤對每個項目的變更，該資料行是針對行動應用程式後端中的每個資料表所定義的。</span><span class="sxs-lookup"><span data-stu-id="31b3b-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="31b3b-266">每當更新記錄時，Mobile Apps 會將該筆記錄的 `version` 屬性設定為新值。</span><span class="sxs-lookup"><span data-stu-id="31b3b-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="31b3b-267">在每次更新要求期間，要求所提供的該筆記錄 `version` 屬性會與伺服器上該筆記錄的相同屬性進行比對。</span><span class="sxs-lookup"><span data-stu-id="31b3b-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="31b3b-268">如果隨著要求傳遞的版本與後端不符，則用戶端程式庫會引發 `MobileServicePreconditionFailedException<T>` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="31b3b-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="31b3b-269">例外狀況所提供的類型是來自包含該記錄之伺服器版本的後端記錄。</span><span class="sxs-lookup"><span data-stu-id="31b3b-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="31b3b-270">接著應用程式可以使用這項資訊，來決定是否要針對後端的正確 `version` 值來執行更新要求以認可變更。</span><span class="sxs-lookup"><span data-stu-id="31b3b-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="31b3b-271">在 `version` 系統屬性的資料表類別上定義資料行，以啟用開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="31b3b-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="31b3b-272">例如：</span><span class="sxs-lookup"><span data-stu-id="31b3b-272">For example:</span></span>

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

<span data-ttu-id="31b3b-273">使用不具類型之資料表的應用程式會在資料表的 `SystemProperties` 上設定 `Version` 旗標，以啟用開放式並行存取，如下所示。</span><span class="sxs-lookup"><span data-stu-id="31b3b-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="31b3b-274">除了啟用開放式並行存取之外，您還必須在呼叫 [UpdateAsync] 時攔截程式碼中的 `MobileServicePreconditionFailedException<T>` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="31b3b-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="31b3b-275">將正確的 `version` 套用到更新的記錄，並利用解決的記錄呼叫 [UpdateAsync] ，藉此解決衝突。</span><span class="sxs-lookup"><span data-stu-id="31b3b-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="31b3b-276">下列程式碼將示範如何在偵測到寫入衝突之後立即解決：</span><span class="sxs-lookup"><span data-stu-id="31b3b-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
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
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="31b3b-277">如需詳細資訊，請參閱 [Azure Mobile Apps 中的離線資料同步處理] 主題。</span><span class="sxs-lookup"><span data-stu-id="31b3b-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="31b3b-278"><a name="binding"></a>如何：將 Mobile Apps 資料繫結至 Windows 使用者介面</span><span class="sxs-lookup"><span data-stu-id="31b3b-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="31b3b-279">本節說明如何在 Windows app 中使用 UI 元素來顯示傳回的資料物件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="31b3b-280">下列範例程式碼繫結至具有未完成項目之查詢的清單來源。</span><span class="sxs-lookup"><span data-stu-id="31b3b-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="31b3b-281">[MobileServiceCollection] 會建立 Mobile Apps 感知的繫結集合。</span><span class="sxs-lookup"><span data-stu-id="31b3b-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="31b3b-282">受管理執行階段中的部分控制項支援名為 [ISupportIncrementalLoading]的介面。</span><span class="sxs-lookup"><span data-stu-id="31b3b-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="31b3b-283">此介面允許控制項在使用者捲動時要求額外資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="31b3b-284">通用 Windows 應用程式可透過會自動處理控制項呼叫的 [MobileServiceIncrementalLoadingCollection]，內建支援此介面。</span><span class="sxs-lookup"><span data-stu-id="31b3b-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="31b3b-285">在 Windows 應用程式中使用 `MobileServiceIncrementalLoadingCollection` ，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="31b3b-286">若要在 Windows Phone 8 和 「Silverlight」應用程式上使用新的集合，請在 `IMobileServiceTableQuery<T>` 與 `IMobileServiceTable<T>` 上使用 `ToCollection` 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="31b3b-287">若要載入資料，請呼叫 `LoadMoreItemsAsync()`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="31b3b-288">當您使用藉由呼叫 `ToCollectionAsync` 或 `ToCollection` 來建立的集合時，您會取得可繫結至 UI 控制項的集合。</span><span class="sxs-lookup"><span data-stu-id="31b3b-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="31b3b-289">此集合有分頁感知功能。</span><span class="sxs-lookup"><span data-stu-id="31b3b-289">This collection is paging-aware.</span></span>  <span data-ttu-id="31b3b-290">因為集合會從網路中載入資料，因此載入有時會失敗。</span><span class="sxs-lookup"><span data-stu-id="31b3b-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="31b3b-291">若要處理這類失敗，請覆寫 `MobileServiceIncrementalLoadingCollection` 上的 `OnException` 方法，以處理呼叫 `LoadMoreItemsAsync` 時所造成的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="31b3b-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="31b3b-292">請思考一下如果您的資料表有許多欄位，但您只想要在控制項中顯示其中部分欄位。</span><span class="sxs-lookup"><span data-stu-id="31b3b-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="31b3b-293">您可以使用上述[選取特定資料欄](#selecting)一節中的指引，以選取要在 UI 中顯示的特定資料欄。</span><span class="sxs-lookup"><span data-stu-id="31b3b-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="31b3b-294"><a name="pagesize"></a>變更頁面大小</span><span class="sxs-lookup"><span data-stu-id="31b3b-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="31b3b-295">Azure Mobile Apps 預設針對每個要求最多會傳回 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="31b3b-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="31b3b-296">您可以增加用戶端和伺服器上的頁面大小上限，以變更分頁大小。</span><span class="sxs-lookup"><span data-stu-id="31b3b-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="31b3b-297">若要增加要求的頁面大小，請在使用 `PullAsync()`時指定 `PullOptions`：</span><span class="sxs-lookup"><span data-stu-id="31b3b-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="31b3b-298">假設您已經在伺服器中讓 `PageSize` 等於或大於 100，要求最多會傳回 100 個項目。</span><span class="sxs-lookup"><span data-stu-id="31b3b-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="31b3b-299"><a name="#offlinesync"></a>使用離線資料表</span><span class="sxs-lookup"><span data-stu-id="31b3b-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="31b3b-300">離線資料表會使用本機 SQLite 存放區來儲存資料供離線時使用。</span><span class="sxs-lookup"><span data-stu-id="31b3b-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="31b3b-301">所有資料表作業都是針對本機 SQLite 存放區而非遠端伺服器存放區完成。</span><span class="sxs-lookup"><span data-stu-id="31b3b-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="31b3b-302">若要建立離線資料表，先準備您的專案：</span><span class="sxs-lookup"><span data-stu-id="31b3b-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="31b3b-303">在 Visual Studio 中，以滑鼠右鍵按一下方案 > [管理方案的 NuGet 套件...]，然後為方案中的所有專案，尋找並安裝 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="31b3b-304">(選擇性) 若要支援 Windows 裝置，請安裝下列其中一個 SQLite 執行階段封裝︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="31b3b-305">**Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="31b3b-306">**Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="31b3b-307">**通用 Windows 平台：** 安裝[適用於通用 Windows 平台的 SQLite][5]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="31b3b-308">(選擇性)。</span><span class="sxs-lookup"><span data-stu-id="31b3b-308">(Optional).</span></span> <span data-ttu-id="31b3b-309">若為 Windows 裝置，請按一下 [參考]  >  [新增參考...]，展開 **Windows** 資料夾 > [擴充功能]，然後啟用適當的 **SQLite for Windows** SDK 及 **Visual C++ 2013 Runtime for Windows** SDK。</span><span class="sxs-lookup"><span data-stu-id="31b3b-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="31b3b-310">每個 Windows 平台的 SQLite SDK 名稱稍有差異。</span><span class="sxs-lookup"><span data-stu-id="31b3b-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="31b3b-311">建立資料表參考之前，必須準備本機存放區：</span><span class="sxs-lookup"><span data-stu-id="31b3b-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="31b3b-312">存放區初始化通常是在建立用戶端之後隨即完成。</span><span class="sxs-lookup"><span data-stu-id="31b3b-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="31b3b-313">**OfflineDbPath** 應該是適合在您支援的所有平台上使用的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="31b3b-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="31b3b-314">如果路徑是完整路徑 (也就是開頭為斜線)，則會使用該路徑。</span><span class="sxs-lookup"><span data-stu-id="31b3b-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="31b3b-315">如果路徑不是完整路徑，則檔案會放在平台特定的位置。</span><span class="sxs-lookup"><span data-stu-id="31b3b-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="31b3b-316">針對 iOS 和 Android 裝置，預設路徑是「個人檔案」資料夾。</span><span class="sxs-lookup"><span data-stu-id="31b3b-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="31b3b-317">針對 Windows 裝置，預設路徑是應用程式特定的 "AppData" 資料夾。</span><span class="sxs-lookup"><span data-stu-id="31b3b-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="31b3b-318">您可以使用 `GetSyncTable<>` 方法來取得資料表參考：</span><span class="sxs-lookup"><span data-stu-id="31b3b-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="31b3b-319">使用離線資料表不需要取得驗證。</span><span class="sxs-lookup"><span data-stu-id="31b3b-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="31b3b-320">只需要在與後端服務通訊時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="31b3b-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="31b3b-321"><a name="syncoffline"></a>同步處理離線資料表</span><span class="sxs-lookup"><span data-stu-id="31b3b-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="31b3b-322">預設情況下，不會對後端同步處理離線資料表。</span><span class="sxs-lookup"><span data-stu-id="31b3b-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="31b3b-323">同步處理會分割成兩個部分。</span><span class="sxs-lookup"><span data-stu-id="31b3b-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="31b3b-324">您可以透過下載新的項目，個別推送變更。</span><span class="sxs-lookup"><span data-stu-id="31b3b-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="31b3b-325">以下是典型的同步處理方法：</span><span class="sxs-lookup"><span data-stu-id="31b3b-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="31b3b-326">如果 `PullAsync` 的第一個引數為 null，則不會使用增量同步處理。</span><span class="sxs-lookup"><span data-stu-id="31b3b-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="31b3b-327">每個同步處理作業會擷取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="31b3b-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="31b3b-328">SDK 會在提取記錄之前執行隱含 `PushAsync()`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="31b3b-329">衝突處理會發生在 `PullAsync()` 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="31b3b-330">您可以使用與線上資料表相同的方式處理衝突。</span><span class="sxs-lookup"><span data-stu-id="31b3b-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="31b3b-331">衝突是在呼叫 `PullAsync()` 時而不是在插入、更新或刪除期間產生。</span><span class="sxs-lookup"><span data-stu-id="31b3b-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="31b3b-332">如果發生多個衝突，則會將它們會搭配至單一 MobileServicePushFailedException。</span><span class="sxs-lookup"><span data-stu-id="31b3b-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="31b3b-333">個別處理每一個失敗。</span><span class="sxs-lookup"><span data-stu-id="31b3b-333">Handle each failure separately.</span></span>

## <span data-ttu-id="31b3b-334"><a name="#customapi"></a>使用自訂 API</span><span class="sxs-lookup"><span data-stu-id="31b3b-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="31b3b-335">自訂 API 可讓您定義自訂端點，並用來公開無法對應插入、更新、刪除或讀取等操作的伺服器功能。</span><span class="sxs-lookup"><span data-stu-id="31b3b-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="31b3b-336">透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="31b3b-337">若要呼叫自訂 API，您可以呼叫用戶端上的其中一個 [InvokeApiAsync] 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="31b3b-338">例如，下列程式碼行會將 POST 要求傳送至後端的 **completeAll** API：</span><span class="sxs-lookup"><span data-stu-id="31b3b-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="31b3b-339">此形式是具類型的方法呼叫，並且會要求定義 **MarkAllResult** 傳回類型。</span><span class="sxs-lookup"><span data-stu-id="31b3b-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="31b3b-340">具類型的和不具類型的方法皆受支援。</span><span class="sxs-lookup"><span data-stu-id="31b3b-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="31b3b-341">InvokeApiAsync() 方法會在您想要呼叫的 API 前面加上 '/api/'，除非該 API 開頭是 '/'。</span><span class="sxs-lookup"><span data-stu-id="31b3b-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="31b3b-342">例如：</span><span class="sxs-lookup"><span data-stu-id="31b3b-342">For example:</span></span>

* <span data-ttu-id="31b3b-343">`InvokeApiAsync("completeAll",...)` 會呼叫後端上的 /api/completeAll</span><span class="sxs-lookup"><span data-stu-id="31b3b-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="31b3b-344">`InvokeApiAsync("/.auth/me",...)` 會呼叫後端上的 /.auth/me</span><span class="sxs-lookup"><span data-stu-id="31b3b-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="31b3b-345">您可以使用 InvokeApiAsync 來呼叫任何 WebAPI，包括未隨著 Azure Mobile Apps 一起定義的 WebAPI。</span><span class="sxs-lookup"><span data-stu-id="31b3b-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="31b3b-346">當您使用 InvokeApiAsync() 時，會隨著要求一起傳送適當的標頭，包括驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="31b3b-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="31b3b-347"><a name="authentication"></a>驗證使用者</span><span class="sxs-lookup"><span data-stu-id="31b3b-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="31b3b-348">Mobile Apps 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory)，來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="31b3b-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="31b3b-349">您可以在資料表上設定權限，以限制僅有通過驗證使用者可以存取特定操作。</span><span class="sxs-lookup"><span data-stu-id="31b3b-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="31b3b-350">您也可以使用通過驗證使用者的身分識別來實作伺服器指令碼中的授權規則。</span><span class="sxs-lookup"><span data-stu-id="31b3b-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="31b3b-351">如需詳細資訊，請參閱 [將驗證新增至您的應用程式]教學課程。</span><span class="sxs-lookup"><span data-stu-id="31b3b-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="31b3b-352">支援兩種驗證流程：*用戶端管理*和*伺服器管理*流程。</span><span class="sxs-lookup"><span data-stu-id="31b3b-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="31b3b-353">由於伺服器管理流程採用提供者的 Web 驗證介面，因此所提供的驗證體驗也最為簡單。</span><span class="sxs-lookup"><span data-stu-id="31b3b-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="31b3b-354">因為用戶端管理流程採用提供者特定的裝置特定 SDK，因此可允許與裝置特定功能的深入整合。</span><span class="sxs-lookup"><span data-stu-id="31b3b-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="31b3b-355">我們建議在生產應用程式中使用用戶端管理的流程。</span><span class="sxs-lookup"><span data-stu-id="31b3b-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="31b3b-356">若要設定驗證，您必須向一或多個識別提供者註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="31b3b-357">識別提供者會產生應用程式的用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="31b3b-358">這些值接著會設定於後端中以啟用 Azure App Service 驗證/授權。</span><span class="sxs-lookup"><span data-stu-id="31b3b-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="31b3b-359">如需詳細資訊，請依照教學課程 [將驗證新增至您的應用程式]中的詳細指示操作。</span><span class="sxs-lookup"><span data-stu-id="31b3b-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="31b3b-360">這一節涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="31b3b-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="31b3b-361">用戶端管理的驗證</span><span class="sxs-lookup"><span data-stu-id="31b3b-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="31b3b-362">伺服器管理的驗證</span><span class="sxs-lookup"><span data-stu-id="31b3b-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="31b3b-363">快取驗證權杖</span><span class="sxs-lookup"><span data-stu-id="31b3b-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="31b3b-364"><a name="clientflow"></a>用戶端管理的驗證</span><span class="sxs-lookup"><span data-stu-id="31b3b-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="31b3b-365">您的應用程式可以個別連絡識別提供者，然後在用您的後端登入期間提供傳回的權杖。</span><span class="sxs-lookup"><span data-stu-id="31b3b-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="31b3b-366">此用戶端流程可讓您為使用者提供單一登入體驗，或從識別提供者擷取其他使用者資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="31b3b-367">用戶端流程驗證比較適合使用伺服器流程，因為識別提供者 SDK 提供更原生的 UX 風格，並可允許進行其他自訂。</span><span class="sxs-lookup"><span data-stu-id="31b3b-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="31b3b-368">已提供下列用戶端流程驗證模式的範例︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="31b3b-369">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="31b3b-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="31b3b-370">Facebook 或 Google</span><span class="sxs-lookup"><span data-stu-id="31b3b-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="31b3b-371">Live SDK</span><span class="sxs-lookup"><span data-stu-id="31b3b-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="31b3b-372"><a name="adal"></a>使用 Active Directory Authentication Library 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="31b3b-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="31b3b-373">您可以使用 Active Directory Authentication Library (ADAL)，從使用 Azure Active Directory 驗證的用戶端起始使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="31b3b-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="31b3b-374">依照[如何設定 App Service 來進行 Active Directory 登入]教學課程的說明，設定您的行動應用程式後端來進行 AAD 登入。</span><span class="sxs-lookup"><span data-stu-id="31b3b-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="31b3b-375">請務必完成註冊原生用戶端應用程式的選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="31b3b-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="31b3b-376">在 Visual Studio 或 Xamarin Studio 中，開啟您的專案，然後新增對 `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 封裝的參考。</span><span class="sxs-lookup"><span data-stu-id="31b3b-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="31b3b-377">搜尋時，包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="31b3b-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="31b3b-378">根據您使用的平台，將下列程式碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="31b3b-379">在每個程式碼中，進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="31b3b-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="31b3b-380">以您佈建應用程式的租用戶名稱取代 **INSERT-AUTHORITY-HERE** 。</span><span class="sxs-lookup"><span data-stu-id="31b3b-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="31b3b-381">格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="31b3b-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="31b3b-382">此值可從 [Azure 傳統入口網站]複製到 Azure Active Directory 的 [網域] 索引標籤以外。</span><span class="sxs-lookup"><span data-stu-id="31b3b-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="31b3b-383">以您行動應用程式後端的用戶端識別碼取代 INSERT-RESOURCE-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="31b3b-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="31b3b-384">您可以從入口網站 [Azure Active Directory 設定] 底下的 [進階] 索引標籤取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="31b3b-385">以您從原生用戶端應用程式中複製的用戶端識別碼取代 INSERT-CLIENT-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="31b3b-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="31b3b-386">使用 HTTPS 配置，以您網站的 **/.auth/login/done** 端點取代 *INSERT-REDIRECT-URI-HERE* 。</span><span class="sxs-lookup"><span data-stu-id="31b3b-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="31b3b-387">此值應與 *https://contoso.azurewebsites.net/.auth/login/done* 類似。</span><span class="sxs-lookup"><span data-stu-id="31b3b-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="31b3b-388">每個平台所需的程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="31b3b-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="31b3b-389">**Windows：**</span><span class="sxs-lookup"><span data-stu-id="31b3b-389">**Windows:**</span></span>

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

     <span data-ttu-id="31b3b-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="31b3b-390">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="31b3b-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="31b3b-391">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="31b3b-392"><a name="client-facebook"></a>使用來自 Facebook 或 Google 的權杖單一登入</span><span class="sxs-lookup"><span data-stu-id="31b3b-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="31b3b-393">您可以使用用戶端流程，如以下 Facebook 或 Google 的程式碼片段中所示。</span><span class="sxs-lookup"><span data-stu-id="31b3b-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
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
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="31b3b-394"><a name="client-livesdk"></a>使用 Microsoft 帳戶搭配 Live SDK 進行單一登入</span><span class="sxs-lookup"><span data-stu-id="31b3b-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="31b3b-395">若要驗證使用者，您必須在 Microsoft 帳戶開發人員中心註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="31b3b-396">請在行動應用程式後端設定註冊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="31b3b-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="31b3b-397">若要建立 Microsoft 帳戶註冊，並將其連接到您的行動應用程式後端，請完成 [註冊您的應用程式以使用 Microsoft 帳戶登入]中的步驟。</span><span class="sxs-lookup"><span data-stu-id="31b3b-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="31b3b-398">如果您的 app 同時有 Windows 市集與 Windows Phone 8/Silverlight 版本，請先註冊 Windows 市集版本。</span><span class="sxs-lookup"><span data-stu-id="31b3b-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="31b3b-399">以下程式碼會使用 Live SDK 進行驗證，並使用傳回的權杖來登入您的「行動應用程式」後端。</span><span class="sxs-lookup"><span data-stu-id="31b3b-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
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

<span data-ttu-id="31b3b-400">如需詳細資訊，請參閱 [Windows Live SDK] 文件。</span><span class="sxs-lookup"><span data-stu-id="31b3b-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="31b3b-401"><a name="serverflow"></a>伺服器管理的驗證</span><span class="sxs-lookup"><span data-stu-id="31b3b-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="31b3b-402">註冊識別提供者之後，使用提供者的 [MobileServiceAuthenticationProvider] 值，在 [MobileServiceClient] 上呼叫 [LoginAsync] 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="31b3b-403">例如，下列程式碼將透過使用 Facebook 來初始化伺服器流程登入。</span><span class="sxs-lookup"><span data-stu-id="31b3b-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="31b3b-404">如果您打算使用除了 Facebook 以外的識別提供者，請將上方的 [MobileServiceAuthenticationProvider] 值變更成您提供者。</span><span class="sxs-lookup"><span data-stu-id="31b3b-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="31b3b-405">在伺服器流程中，Azure App Service 透過顯示所選提供者的登入頁面，來管理 OAuth 驗證流程。</span><span class="sxs-lookup"><span data-stu-id="31b3b-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="31b3b-406">在識別提供者傳回後，Azure App Service 會產生 App Service 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="31b3b-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="31b3b-407">[LoginAsync] 方法 會傳回 [MobileServiceUser]，並提供通過驗證使用者的 [UserId] 和 [MobileServiceAuthenticationToken]，以作為 JSON Web 權杖 (JWT)。</span><span class="sxs-lookup"><span data-stu-id="31b3b-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="31b3b-408">您可以快取並重複使用此權杖，直到它到期為止。</span><span class="sxs-lookup"><span data-stu-id="31b3b-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="31b3b-409">如需詳細資訊，請參閱 [快取驗證權杖](#caching)。</span><span class="sxs-lookup"><span data-stu-id="31b3b-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="31b3b-410"><a name="caching"></a>快取驗證權杖</span><span class="sxs-lookup"><span data-stu-id="31b3b-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="31b3b-411">在某些情況下，儲存來自提供者的驗證權杖即可避免在第一次成功驗證後呼叫登入方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="31b3b-412">Windows 市集和 UWP 應用程式可以使用 [PasswordVault] ，在成功登入後快取目前的驗證權杖，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="31b3b-413">UserId 值會儲存為認證的 UserName，而權杖會儲存為 Password。</span><span class="sxs-lookup"><span data-stu-id="31b3b-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="31b3b-414">在後續的啟動時，您可以檢查 **PasswordVault** 中的快取認證。</span><span class="sxs-lookup"><span data-stu-id="31b3b-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="31b3b-415">下列範例會使用找到的快取認證，否則會嘗試再次向後端進行驗證︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="31b3b-416">當您登出使用者時，您也必須移除預存的認證，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="31b3b-417">Xamarin 應用程式會使用 [Xamarin.Auth] API，將憑證安全地儲存在 [帳戶] 物件中。</span><span class="sxs-lookup"><span data-stu-id="31b3b-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="31b3b-418">如需使用這些 API 的範例，請參閱 [ContosoMoments 照片分享範例](https://github.com/azure-appservice-samples/ContosoMoments)中的 [AuthStore.cs] 程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="31b3b-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="31b3b-419">當您使用用戶端管理的驗證時，您也可以快取向您的提供者 (例如 Facebook 或 Twitter) 取得的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="31b3b-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="31b3b-420">您可以提供此權杖，以向後端要求新的驗證權杖，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="31b3b-421"><a name="pushnotifications"></a>推播通知</span><span class="sxs-lookup"><span data-stu-id="31b3b-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="31b3b-422">下列主題涵蓋推播通知︰</span><span class="sxs-lookup"><span data-stu-id="31b3b-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="31b3b-423">註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="31b3b-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="31b3b-424">取得 Windows 市集封裝 SID</span><span class="sxs-lookup"><span data-stu-id="31b3b-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="31b3b-425">利用跨平台範本進行註冊</span><span class="sxs-lookup"><span data-stu-id="31b3b-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="31b3b-426"><a name="register-for-push"></a>做法：註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="31b3b-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="31b3b-427">Mobile Apps 用戶端可讓您向 Azure 通知中樞註冊推播通知。</span><span class="sxs-lookup"><span data-stu-id="31b3b-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="31b3b-428">註冊時，您會取得從特定平台「推送通知服務 (PNS)」取得的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="31b3b-429">然後您就可以在建立註冊時提供此值以及任何標記。</span><span class="sxs-lookup"><span data-stu-id="31b3b-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="31b3b-430">下列程式碼會為您的 Windows 應用程式向 Windows 通知服務 (WNS) 註冊推播通知：</span><span class="sxs-lookup"><span data-stu-id="31b3b-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="31b3b-431">如果您要推送到 WNS，必須[取得 Windows 市集套件 SID](#package-sid) (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="31b3b-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="31b3b-432">如需 Windows 應用程式的詳細資訊，包括如何註冊範本，請參閱 [將推播通知新增至您的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="31b3b-433">不支援從用戶端要求標記。</span><span class="sxs-lookup"><span data-stu-id="31b3b-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="31b3b-434">註冊時會自動捨棄標記要求。</span><span class="sxs-lookup"><span data-stu-id="31b3b-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="31b3b-435">如果您想要利用標記註冊裝置，請建立自訂 API，以使用通知中樞 API 代替您執行註冊。</span><span class="sxs-lookup"><span data-stu-id="31b3b-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="31b3b-436">[呼叫自訂 API](#customapi) 而不是 `RegisterNativeAsync()` 方法。</span><span class="sxs-lookup"><span data-stu-id="31b3b-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="31b3b-437"><a name="package-sid"></a>如何：取得 Windows 市集封裝 SID</span><span class="sxs-lookup"><span data-stu-id="31b3b-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="31b3b-438">在 Windows 市集應用程式中啟用推播通知需有封裝 SID。</span><span class="sxs-lookup"><span data-stu-id="31b3b-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="31b3b-439">若要收到套件 SID，請向 Windows 市集註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="31b3b-440">若要取得這個值：</span><span class="sxs-lookup"><span data-stu-id="31b3b-440">To obtain this value:</span></span>

1. <span data-ttu-id="31b3b-441">在 Visual Studio 方案總管中，以滑鼠右鍵按一下 Windows 市集應用程式專案，然後按一下 [市集]  >  [將應用程式與市集建立關聯...]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="31b3b-442">在精靈中按 [下一步]，使用 Microsoft 帳戶登入，在 [保留新的應用程式名稱] 中輸入您應用程式的名稱，然後按一下 [保留]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="31b3b-443">成功建立應用程式註冊之後，選取應用程式名稱，按 [下一步]，然後按一下 [關聯]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="31b3b-444">使用您的 Microsoft 帳戶登入 [Windows 開發人員中心] 。</span><span class="sxs-lookup"><span data-stu-id="31b3b-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="31b3b-445">在 [我的應用程式] 底下，按一下您建立的應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="31b3b-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="31b3b-446">按一下 [應用程式管理]  >  [應用程式身分識別]，然後向下捲動找到您的 [套件 SID]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="31b3b-447">許多使用套件 SID 的情況會將其視為 URI，在這種情況下，您必須使用 *ms-app://* 作為配置。</span><span class="sxs-lookup"><span data-stu-id="31b3b-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="31b3b-448">記下您封裝 SID 的版本，封裝 SID 是由串連這個值作為首碼所形成。</span><span class="sxs-lookup"><span data-stu-id="31b3b-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="31b3b-449">Xamarin 應用程式需要一些額外的程式碼，才能註冊執行於 iOS 或 Android 平台的應用程式。</span><span class="sxs-lookup"><span data-stu-id="31b3b-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="31b3b-450">如需詳細資訊，請參閱平台適用的主題：</span><span class="sxs-lookup"><span data-stu-id="31b3b-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="31b3b-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="31b3b-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="31b3b-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="31b3b-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="31b3b-453"><a name="register-xplat"></a>作法：註冊推送範本以傳送跨平台通知</span><span class="sxs-lookup"><span data-stu-id="31b3b-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="31b3b-454">若要註冊範本，請使用 `RegisterAsync()` 方法搭配範本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="31b3b-455">您的範本應該是 `JObject` 類型，並且可能包含下列 JSON 格式的多個範本：</span><span class="sxs-lookup"><span data-stu-id="31b3b-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

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

<span data-ttu-id="31b3b-456">方法 **RegisterAsync()** 也接受次要磚：</span><span class="sxs-lookup"><span data-stu-id="31b3b-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="31b3b-457">為確保安全，註冊期間會移除所有標籤。</span><span class="sxs-lookup"><span data-stu-id="31b3b-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="31b3b-458">若要在安裝中將標籤新增至安裝或範本，請參閱 [使用適用於 Azure Mobile Apps 的 .NET 後端伺服器 SDK]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="31b3b-459">若要利用這些已註冊的範本傳送通知，請參閱 [通知中樞 API]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="31b3b-460"><a name="misc"></a>其他主題</span><span class="sxs-lookup"><span data-stu-id="31b3b-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="31b3b-461"><a name="errors"></a>作法：處理錯誤</span><span class="sxs-lookup"><span data-stu-id="31b3b-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="31b3b-462">當後端發生錯誤時，用戶端 SDK 會引發 `MobileServiceInvalidOperationException`。</span><span class="sxs-lookup"><span data-stu-id="31b3b-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="31b3b-463">下列範例示範如何處理後端所傳回的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="31b3b-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
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

<span data-ttu-id="31b3b-464">如需另一個處理錯誤狀況的範例，請造訪 [Mobile Apps 檔案範例]。</span><span class="sxs-lookup"><span data-stu-id="31b3b-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="31b3b-465">[LoggingHandler] 範例會提供記錄委派處理常式，以記錄向後端提出的要求。</span><span class="sxs-lookup"><span data-stu-id="31b3b-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="31b3b-466"><a name="headers"></a>作法：自訂要求標頭</span><span class="sxs-lookup"><span data-stu-id="31b3b-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="31b3b-467">若要支援您的特定應用程式案例，您可能需要自訂與行動應用程式後端的通訊。</span><span class="sxs-lookup"><span data-stu-id="31b3b-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="31b3b-468">例如，您可能會想要在每封連出要求上新增自訂標頭，或甚至變更回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="31b3b-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="31b3b-469">您可以使用自訂的 [DelegatingHandler]，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="31b3b-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

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
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
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

<span data-ttu-id="31b3b-470">[將驗證新增至您的應用程式]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="31b3b-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="31b3b-471">[Azure Mobile Apps 中的離線資料同步處理]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="31b3b-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="31b3b-472">[將推播通知新增至您的應用程式]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="31b3b-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="31b3b-473">[註冊您的應用程式以使用 Microsoft 帳戶登入]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="31b3b-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="31b3b-474">[如何設定 App Service 來進行 Active Directory 登入]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="31b3b-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="31b3b-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-481">[建立不具類型的資料表參考]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="31b3b-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="31b3b-497">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="31b3b-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="31b3b-498">[Azure 傳統入口網站]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="31b3b-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="31b3b-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="31b3b-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="31b3b-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="31b3b-502">[Windows 開發人員中心]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="31b3b-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="31b3b-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="31b3b-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="31b3b-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="31b3b-506">[通知中樞 API]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="31b3b-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="31b3b-507">[Mobile Apps 檔案範例]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="31b3b-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="31b3b-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="31b3b-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="31b3b-509">[OData v3 文件]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="31b3b-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="31b3b-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="31b3b-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="31b3b-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="31b3b-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="31b3b-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="31b3b-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="31b3b-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="31b3b-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
