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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Toouse hello 如何管理 Azure 行動應用程式的用戶端
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>概觀
本指南也說明使用 hello tooperform 常見的案例如何管理用戶端程式庫，針對 Azure 應用程式服務行動裝置應用程式的 Windows 與 Xamarin 應用程式。 如果您是新 tooMobile 應用程式，您應該考慮第一個完成的 hello [Azure 行動應用程式快速入門][ 1]教學課程。 本指南中，我們將重點放在 hello 上用戶端管理 SDK。 toolearn 深入了解 hello 行動應用程式的伺服器端 Sdk，請參閱 hello 文件以 hello [.NET 伺服器 SDK] [ 2]或[Node.js 伺服器 SDK] [ 3].

## <a name="reference-documentation"></a>參考文件
hello hello client SDK 的參考文件位於此處： [Azure 行動應用程式的.NET 用戶端參考][4]。
您也可以找到數個用戶端範例在 hello [Azure 範例 GitHub 儲存機制][5]。

## <a name="supported-platforms"></a>支援的平台
hello.NET 平台支援下列平台的 hello:

* 適用於 API 19 到 24 (KitKat 到 Nougat) 的 Xamarin Android 版本
* 適用於 iOS 8.0 版和更新版本的 Xamarin iOS 版本
* 通用 Windows 平台
* Windows Phone 8.1
* Windows Phone 8.0 (Silverlight 應用程式除外)

hello 「 伺服器-流程 」 驗證會使用 WebView hello 呈現 UI。  如果 hello 裝置不能 toopresent WebView UI，則會需要其他的驗證方法。  因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。

## <a name="setup"></a>設定和必要條件
我們假設您已建立並發佈您的行動應用程式後端專案 (至少包含一個資料表)。  使用本主題中的 hello 程式碼，在名為 hello 資料表`TodoItem`並具有下列資料行的 hello: `Id`， `Text`，和`Complete`。 此資料表是相同的資料表建立，當您完成時的 hello [Azure 行動應用程式快速入門][1]。

hello 對應型別的用戶端的類型在 C# 中為下列類別的 hello:

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

hello [JsonPropertyAttribute] [ 6]為使用的 toodefine hello *PropertyName* hello 用戶端欄位與 hello 資料表欄位之間的對應。

toolearn toocreate 行動應用程式後端中的資料表，請參閱 「 hello [.NET 伺服器 SDK 主題][ 7]或 hello [Node.js 伺服器 SDK 主題][ 8]. 如果您已建立您的行動裝置應用程式後端中 hello Azure 入口網站使用 hello 快速入門中，您也可以使用 hello**簡單資料表**hello 中設定[Azure 入口網站]。

### <a name="how-to-install-hello-managed-client-sdk-package"></a>如何： 安裝 hello 受管理用戶端 SDK 封裝
使用其中一個 hello 遵循方法 tooinstall hello 適用於從行動裝置應用程式管理的用戶端 SDK 套件[NuGet][9]:

* **Visual Studio**以滑鼠右鍵按一下您的專案中，按一下**管理 NuGet 封裝**，搜尋 hello`Microsoft.Azure.Mobile.Client`封裝，然後按一下 **安裝**。
* **Xamarin Studio**以滑鼠右鍵按一下您的專案中，按一下**新增** > **新增 NuGet 套件**，搜尋 hello`Microsoft.Azure.Mobile.Client `封裝，然後按一下**新增封裝**。

在您的主要活動檔案，請記得 tooadd hello 下列**使用**陳述式：

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>做法︰使用 Visual Studio 中的偵錯符號
hello 符號 hello Microsoft.Azure.Mobile 命名空間位於[SymbolSource][10]。  請參閱 toothe [SymbolSource 指示][ 11] toointegrate SymbolSource 與 Visual Studio。

## <a name="create-client"></a>建立 hello 行動應用程式用戶端
hello 下列程式碼會建立 hello [MobileServiceClient] [ 12]亦即使用的 tooaccess 您的行動裝置應用程式後端。

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

在上述程式碼的 hello，取代`MOBILE_APP_URL`hello hello 行動裝置應用程式後端 url，找到在刀鋒視窗中的行動裝置應用程式後端中 hello [Azure 入口網站]。 hello MobileServiceClient 物件應該是單一值。

## <a name="work-with-tables"></a>使用資料表
hello 遵循本節詳述如何 toosearch 和擷取記錄，以及修改 hello 資料表中的 hello 資料。  涵蓋下列主題中的 hello:

* [建立資料表參考](#instantiating)
* [查詢資料](#querying)
* [篩選傳回的資料](#filtering)
* [排序傳回的資料](#sorting)
* [以分頁方式傳回資料](#paging)
* [選取特定資料欄](#selecting)
* [依據識別碼查詢記錄](#lookingup)
* [處理不具類型的查詢](#untypedqueries)
* [插入資料](#inserting)
* [更新資料](#updating)
* [刪除資料](#deleting)
* [衝突解決和開放式並行存取](#optimisticconcurrency)
* [繫結 tooa Windows 使用者介面](#binding)
* [變更頁面大小 hello](#pagesize)

### <a name="instantiating"></a>作法：建立資料表參考
所有的 「 hello 」 程式碼，可以存取或修改後端資料表中的資料呼叫函式上 hello`MobileServiceTable`物件。 取得參考 toohello 資料表呼叫 hello [GetTable]方法，如下所示：

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

hello 傳回物件使用 hello 具類型的序列化模式。 也支援不具類型的序列化模型。 下列範例[建立參考 tooan 不具型別的資料表]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

在不具類型的查詢中，您必須指定 hello 基礎 OData 查詢字串。

### <a name="querying"></a>如何：查詢行動應用程式中的資料
本章節描述如何 tooissue 查詢 toohello 行動裝置應用程式後端，其中包括下列功能的 hello:

* [篩選傳回的資料](#filtering)
* [排序傳回的資料](#sorting)
* [以分頁方式傳回資料](#paging)
* [選取特定資料欄](#selecting)
* [按識別碼查詢資料](#lookingup)

> [!NOTE]
> 伺服器導向的頁面大小是強制的 tooprevent 傳回所有資料列。  分頁可避免針對大型資料集的預設要求對於 hello 服務造成負面影響。  tooreturn 多超過 50 個資料列，使用 hello`Skip`和`Take`方法中所述[頁面中傳回資料](#paging)。

### <a name="filtering"></a>作法：篩選傳回的資料
hello 下列程式碼說明如何藉由 toofilter 資料`Where`在查詢中的子句。 它會傳回所有項目從`todoTable`其`Complete`屬性等於太`false`。 hello[其中]函式適用於將資料列篩選述詞，以針對 hello 資料表 hello 查詢。

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

您可以使用訊息檢查軟體，例如瀏覽器開發人員工具來檢視 hello hello 傳送要求 toohello 後端的 URI 或[Fiddler]。 如果您看一下 hello 要求 URI，請注意會修改 hello 查詢字串：

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

此 OData 要求會轉譯成 SQL 查詢，由伺服器 SDK hello:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

hello 函式傳遞 toohello`Where`方法可以有任意數目的條件。

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

這個範例會轉譯成 SQL 查詢，由伺服器 SDK hello:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

此查詢也可以分割成多個子句︰

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

hello 兩種方法是相等的可能會交換使用。  hello 先前選項&mdash;串連多個述詞在單一查詢中的&mdash;更簡潔且建議。

hello`Where`子句支援的作業會轉譯成 hello OData 子集。 這些作業包括︰

* 關係運算子 (==、!=、<、<=、>、>=)、
* 算術運算子 (+、-、/、*、%)、
* 精確度位數 (Math.Floor、Math.Ceiling)、
* 字串函數 (Length、Substring、Replace、IndexOf、StartsWith、EndsWith)、
* 日期屬性 (Year、Month、Day、Hour、Minute、Second)、
* 物件的存取屬性，及
* 結合上述任何運算的運算式。

請考慮什麼 hello 伺服器 SDK 當支援時，您可以考慮 hello [OData v3 文件]。

### <a name="sorting"></a>作法：排序傳回的資料
hello 下列程式碼說明如何藉由 toosort 資料[OrderBy]或[OrderByDescending] hello 查詢中的函式。 它會傳回項目從`todoTable`排序按遞增 hello`Text`欄位。

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

### <a name="paging"></a>作法：以分頁方式傳回資料
根據預設，hello 後端會傳回只 hello 前 50 個資料列。 您可以透過呼叫 hello 增加 hello 傳回的資料列數目[採取]方法。 使用`Take`以及 hello[略過]方法 toorequest 特定"page"hello 總計的資料集的 hello 查詢所傳回。 hello 執行時，下列查詢傳回 hello 前三個項目 hello 資料表中。

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

hello 下列修訂過的查詢會略過 hello 前三個結果，並傳回 hello 接下來三個結果。 此查詢會產生 hello 第二個 「 頁 」 資料，其中 hello 頁面大小是三個項目。

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

hello [IncludeTotalCount]方法會要求 hello 總計數*所有*hello 會傳回，忽略任何 paging/limit 子句，指定的記錄：

```
query = query.IncludeTotalCount();
```

在真實世界應用程式中，您可以使用查詢類似 toohello 前面範例和頁面巡覽區控制項或類似的 UI 頁面之間巡覽。

> [!NOTE]
> 在行動裝置應用程式後端 toooverride hello 50 同資料列限制，您必須套用 hello [EnableQueryAttribute] toohello 公用 GET 方法，並指定 hello 分頁行為。 當套用的 toohello 方法，下列的 hello 設定傳回的最大資料列 too1000:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>作法：選取特定資料欄
您可以指定哪屬性 tooinclude hello 中一組結果加[選取]子句 tooyour 查詢。 例如，hello 下列程式碼會示範如何 tooselect 只有一個欄位和也方式 tooselect 並格式化多個欄位：

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

所有 hello 到目前為止所述的函式會加總，因此我們可以保留鏈結它們。 鏈結的每個呼叫會影響多個 hello 查詢。 再提供一個範例：

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>作法：按識別碼查詢資料
hello [LookupAsync]函式可以是使用的 toolook 已從 hello 與特定識別碼的資料庫物件

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>如何：執行不具類型的查詢
執行時使用的資料表不具型別的的物件查詢，您必須明確地指定 hello OData 查詢字串呼叫[ReadAsync]，如下列範例中的 hello:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

您將收到可用作屬性包的 JSON 值。 如需 JToken 和 Newtonsoft Json.NET 的詳細資訊，請參閱 hello [Json.NET]站台。

### <a name="inserting"></a>如何：將資料插入行動應用程式後端
所有用戶端類型都必須包含名為 **Id**的成員，其預設為字串。 這**識別碼**才能執行 CRUD 作業，且針對 hello 離線同步處理。 下列程式碼說明如何 toouse hello [InsertAsync]方法 tooinsert 新的資料列插入資料表。 hello 參數包含 hello 資料 toobe 插入為.NET 物件。

```
await todoTable.InsertAsync(todoItem);
```

如果自訂的唯一識別碼值不會包含在 hello `todoItem` hello 伺服器時，插入，產生的 GUID。
您可以擷取 hello hello 呼叫傳回後，檢查 hello 物件產生識別碼。

tooinsert 不具類型的資料，您可能會利用 Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

以下是使用電子郵件地址作為唯一字串 id 的範例：

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>使用識別碼值
行動應用程式支援自訂的唯一字串值 hello 資料表**識別碼**資料行。 字串值，可讓應用程式 toouse 自訂值，例如電子郵件地址或 hello 識別碼的使用者名稱  字串 Id 為您提供下列優點 hello:

* 不會進行往返 toohello 資料庫產生的識別碼。
* 更容易 toomerge 來自不同資料表或資料庫的記錄。
* 識別碼值與應用程式邏輯的整合更理想。

插入的記錄上未設定字串 ID 值，當 hello 行動裝置應用程式後端產生唯一值的識別碼。 您可以使用 hello [Guid.NewGuid]方法 toogenerate 您自己的識別碼值 hello 用戶端上或在 hello 後端中。

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>如何：修改行動應用程式後端中的資料
hello 下列程式碼說明如何 toouse hello [UpdateAsync]方法 tooupdate hello 與現有的記錄相同的識別碼以新資訊。 hello 參數包含 hello 資料 toobe 更新為.NET 物件。

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate 不具類型的資料，您可能會利用[Json.NET] ，如下所示：

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

更新時，您必須指定 `id` 欄位。 hello 後端使用 hello`id`欄位 tooidentify 的資料列 tooupdate。 hello`id`欄位可以取自 hello hello 結果`InsertAsync`呼叫。 `ArgumentException`如果您嘗試使用沒有提供 hello tooupdate 項目就會引發`id`值。

### <a name="deleting"></a>如何：刪除行動應用程式後端中的資料
hello 下列程式碼說明如何 toouse hello [DeleteAsync]方法 toodelete 現有執行個體。 hello 執行個體由 hello`id`欄位上 hello `todoItem`。

```
await todoTable.DeleteAsync(todoItem);
```

toodelete 不具類型的資料，您可能會利用 Json.NET，如下所示：

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

提出刪除要求時，必須指定 ID。 其他屬性不會傳遞 toohello 服務，或在 hello 服務會被忽略。 hello 結果`DeleteAsync`呼叫通常是`null`。 中的 hello 識別碼 toopass 可以取自 hello hello 結果`InsertAsync`呼叫。 A`MobileServiceInvalidOperationException`您嘗試使用沒有指定 hello toodelete 項目時，會擲回`id`欄位。

### <a name="optimisticconcurrency"></a>做法：使用開放式並行存取來解決衝突
兩個或多個用戶端可能會寫入變更 toohello 相同項目在 hello 相同的時間。 沒有衝突偵測、 hello 最後一次寫入會覆寫任何先前的更新。  會假設每筆交易都可以認可，因此不會使用任何資源鎖定。  認可交易之前, 開放式並行存取控制會確認沒有其他交易已修改 hello 資料。 如果已修改 hello 資料，會回復 hello 認可交易。

行動應用程式透過追蹤使用 hello 變更 tooeach 項目，支援開放式並行存取控制`version`定義您的行動裝置應用程式後端中每個資料表的系統屬性資料行。 每次更新一筆記錄時，行動應用程式設定 hello`version`屬性，該記錄 tooa 新值。 每個更新要求期間 hello `version` hello 記錄 hello 要求所包含的屬性是比較的 toohello hello hello 伺服器上的記錄相同的屬性。 如果版本傳遞與 hello 要求不符合 hello 後端，則 hello 用戶端程式庫引發`MobileServicePreconditionFailedException<T>`例外狀況。 hello hello 例外狀況所包含的型別是 hello hello 後端包含 hello 伺服器 hello 記錄版本記錄。 hello 應用程式可以接著使用此資訊 toodecide 是否 tooexecute hello 更新要求，再次以正確的 hello `version` hello 的後端 toocommit 變更的值。

Hello 的 hello 資料表類別上定義的資料行`version`系統屬性 tooenable 開放式並行存取。 例如：

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

使用不具類型的資料表的應用程式會啟用開放式並行存取所設定的 hello`Version`加上旗標上`SystemProperties`hello 的資料表，如下所示。

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

在加法 tooenabling 開放式並行存取，您也必須攔截 hello`MobileServicePreconditionFailedException<T>`時呼叫程式碼中的例外狀況[UpdateAsync]。  藉由套用正確的 hello 解決 hello 衝突`version`toothe 更新記錄，以及呼叫[UpdateAsync]以 hello 已解決的記錄。 hello，下列程式碼顯示如何 tooresolve 寫入一次偵測到衝突：

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

如需詳細資訊，請參閱 hello[離線 Azure 行動應用程式中的資料同步處理]主題。

### <a name="binding"></a>如何： 繫結行動應用程式資料 tooa Windows 使用者介面
本節說明如何 toodisplay 傳回資料物件在 Windows 應用程式中使用 UI 項目。  下列範例程式碼會繫結 hello 清單不完整的項目查詢與 toohello 來源。 [MobileServiceCollection] 會建立 Mobile Apps 感知的繫結集合。

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

有些控制項在 hello managed 介面呼叫的執行階段支援[ISupportIncrementalLoading]。 這個介面可讓控制項 toorequest hello 使用者捲動時的額外資料。 沒有內建支援的通用 Windows 應用程式，透過此介面[MobileServiceIncrementalLoadingCollection]，這會自動處理從 hello 控制項呼叫。 在 Windows 應用程式中使用 `MobileServiceIncrementalLoadingCollection` ，如下所示︰

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello 新的集合，在 Windows Phone 8 和"Silverlight 」 應用程式，使用 hello`ToCollection`的擴充方法`IMobileServiceTableQuery<T>`和`IMobileServiceTable<T>`。 tooload 資料呼叫`LoadMoreItemsAsync()`。

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

當您使用藉由呼叫建立 hello 集合`ToCollectionAsync`或`ToCollection`，取得可以繫結的 tooUI 控制項的集合。  此集合有分頁感知功能。  Hello 集合從網路載入資料，因為載入有時會失敗。 toohandle 這類失敗，覆寫 hello`OnException`方法`MobileServiceIncrementalLoadingCollection`太造成呼叫 toohandle 例外狀況`LoadMoreItemsAsync`。

請考慮您的資料表有許多欄位，但您只想 toodisplay 其中一個，在您的控制項。 您可能使用 hello 指引 hello 前面一節中 「[選取特定資料行](#selecting)"tooselect 特定資料行 toodisplay hello UI 中的。

### <a name="pagesize"></a>變更 hello 頁面大小
Azure Mobile Apps 預設針對每個要求最多會傳回 50 個項目。  您可以藉由增加 hello hello 用戶端和伺服器上的最大頁面大小變更 hello 分頁大小。  tooincrease hello 要求的頁面大小，指定`PullOptions`時使用`PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

假設您已經 hello`PageSize`等於 tooor 大於 100 hello 伺服器中，要求會傳回最多 100 個項目。

## <a name="#offlinesync"></a>使用離線資料表
離線的資料表會使用本機的 SQLite 儲存 toostore 資料離線時使用。  作業會針對 hello 完成的所有資料表 SQLite 本機都儲存而非 hello 遠端伺服器存放都區。  toocreate 離線的資料表中，先準備您的專案：

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello 方案 >**管理方案的 NuGet 套件...**，然後尋找並安裝**Microsoft.Azure.Mobile.Client.SQLiteStore** hello 方案中的所有專案的 NuGet 封裝。
2. （選擇性） toosupport Windows 裝置，安裝其中一個 hello 遵循 SQLite 執行階段封裝：

   * **Windows 8.1 執行階段：**安裝[適用於 Windows 8.1 的 SQLite][3]。
   * **Windows Phone 8.1：**安裝[適用於 Windows Phone 8.1 的 SQLite][4]。
   * **通用 Windows 平台**安裝[SQLite 對通用 Windows hello][5]。
3. (選擇性)。 針對 Windows 裝置，請按一下**參考** > **加入參考...**，展開 hello **Windows**資料夾 >**延伸**，然後啟用適當的 hello **SQLite 適用於 Windows 的**hello以及SDK**適用於 Windows 的 visual c + + 2013 Runtime** SDK。
    hello SQLite SDK 的名稱會稍微不同的每個 Windows 平台。

在建立資料表參考之前，必須先備妥 hello 本機存放區：

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

存放區初始化動作通常是在建立 hello 用戶端之後。  hello **OfflineDbPath**應該是適用於所有支援的平台上的檔案名稱。  如果 hello 路徑是完整的路徑 （也就是它的開頭斜線），則會使用該路徑。  如果 hello 路徑的格式不完整，hello 檔案被放在特定平台的位置。

* 針對 iOS 和 Android 裝置，hello 預設路徑會是 hello"個人 Files"資料夾。
* 適用於 Windows 裝置 hello 預設路徑會是 hello 特定應用程式"AppData"資料夾。

可取得資料表參考使用 hello`GetSyncTable<>`方法：

```
var table = client.GetSyncTable<TodoItem>();
```

您不需要 tooauthenticate toouse 離線的資料表。  您會與 hello 後端服務進行通訊時，只需要 tooauthenticate。

### <a name="syncoffline"></a>同步處理離線資料表
根據預設離線資料表未同步處理與 hello 後端。  同步處理會分割成兩個部分。  您可以透過下載新的項目，個別推送變更。  以下是典型的同步處理方法：

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

如果 hello 第一個引數太`PullAsync`為 null，則不會使用增量同步處理。  每個同步處理作業會擷取所有記錄。

hello SDK 執行隱含`PushAsync()`提取記錄前。

衝突處理會發生在 `PullAsync()` 方法。  您可以處理相同衝突 hello 線上資料表的方式。  hello 衝突產生時`PullAsync()`hello insert、 update 或 delete 期間會呼叫而不是。 如果發生多個衝突，則會將它們會搭配至單一 MobileServicePushFailedException。  個別處理每一個失敗。

## <a name="#customapi"></a>使用自訂 API
自訂 API 可讓您 toodefine 自訂端點來公開伺服器功能並不對應 tooan 插入、 更新、 刪除或讀取作業。 透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。

您可以呼叫自訂 API 透過呼叫其中一個 hello [InvokeApiAsync] hello 用戶端上的方法。 例如，下列程式碼行 hello 會傳送 POST 要求 toohello **completeAll** hello 後端 API:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

這種形式是具類型的方法呼叫，而且需要該 hello **MarkAllResult**傳回型別定義。 具類型的和不具類型的方法皆受支援。

hello InvokeApiAsync() 方法前面加上 ' / api /' toohello API 您想 toocall，除非應用程式開發介面 hello 開頭 '/'。
例如：

* `InvokeApiAsync("completeAll",...)`呼叫 /api/completeAll hello 後端
* `InvokeApiAsync("/.auth/me",...)`呼叫 /.auth/me hello 後端

您可以使用任何 WebAPI，包括與 Azure 行動應用程式未定義這些 WebAPIs InvokeApiAsync toocall。  當您使用 InvokeApiAsync() 時，與 hello 要求傳送 hello 適當標頭，包括驗證標頭。

## <a name="authentication"></a>驗證使用者
Mobile Apps 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory)，來驗證與授權應用程式使用者。 您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。 您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。 如需詳細資訊，請參閱 hello 教學課程[新增 authentication tooyour 應用程式]。

支援兩種驗證流程：*用戶端管理*和*伺服器管理*流程。 hello 管理伺服器的流量提供 hello 最簡單的驗證體驗，它會仰賴 hello 提供者 web 驗證介面。 因為它是倚賴特定提供者裝置特有的 Sdk 與裝置特定功能的更深入整合能 hello 管理用戶端流量。

> [!NOTE]
> 我們建議在生產應用程式中使用用戶端管理的流程。

tooset 驗證設定，您必須具有一個或多個身分識別提供者註冊您的應用程式。  hello 身分識別提供者會產生用戶端識別碼和您的應用程式的用戶端密碼。  這些值接著會在您的後端 tooenable Azure 應用程式服務驗證/授權設定。  如需詳細資訊，請遵循 hello 詳細教學課程中的指示[新增 authentication tooyour 應用程式]。

此章節將討論下列主題中的 hello:

* [用戶端管理的驗證](#clientflow)
* [伺服器管理的驗證](#serverflow)
* [快取的 hello 驗證權杖](#caching)

### <a name="clientflow"></a>用戶端管理的驗證
您的應用程式可以獨立連絡 hello 身分識別提供者，然後在與您的後端的登入期間提供 hello 傳回的權杖。 此用戶端流程可讓您 tooprovide 單一登入體驗的使用者或 tooretrieve hello 身分識別提供者的其他使用者資料。 用戶端流量驗證為慣用的 toousing 伺服器流程 hello 身分識別提供者 SDK 提供較原始的 UX 操作，並允許其他自訂。

範例可供下列用戶端流程驗證模式的 hello:

* [Active Directory Authentication Library](#adal)
* [Facebook 或 Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>驗證使用者以 hello Active Directory Authentication Library
您可以使用 hello Active Directory 驗證程式庫 (ADAL) tooinitiate 從 hello 用戶端使用 Azure Active Directory 驗證的使用者驗證。

1. 設定您的行動裝置應用程式後端的 AAD 登入下列 hello [tooconfigure Active Directory 登入服務的應用程式如何]教學課程。 請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。
2. 在 Visual Studio 或 Xamarin Studio，開啟您的專案並加入參考 toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 封裝。 搜尋時，包含發行前版本。
3. 新增下列程式碼 tooyour 應用程式，根據您使用 toohello 平台的 hello。 在每個，請遵循取代 hello:

   * 取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。 格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。這個值可以複製 hello 網域 索引標籤中 Azure Active Directory 中 hello [Azure 傳統入口網站]。
   * 取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。 您可以從 hello 取得 hello 用戶端識別碼**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。
   * 取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。
   * 取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。 此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。

     每個平台所需的 hello 程式碼如下：

     **Windows：**

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

     **Xamarin.iOS**

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

     **Xamarin.Android**

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

#### <a name="client-facebook"></a>使用來自 Facebook 或 Google 的權杖單一登入
您可以使用 hello 用戶端流量，如 Facebook 或 Google 中此程式碼片段所示。

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

#### <a name="client-livesdk"></a>單一登入使用 Microsoft 帳戶與 hello Live SDK
tooauthenticate 使用者，您必須註冊在 hello 開發人員中心的 Microsoft 帳戶應用程式。 請在行動應用程式後端設定註冊詳細資料。 toocreate Microsoft 帳戶註冊，並將它連接 tooyour 行動裝置應用程式後端中的步驟完成 hello[註冊您的 Microsoft 帳戶登入的應用程式 toouse]。 如果您有應用程式的 Windows 市集和 Windows Phone 8/Silverlight 版本，請先註冊 hello Windows 市集版本。

hello 下列程式碼會使用 Live SDK 進行驗證並使用傳回語彙基元 toosign tooyour 行動裝置應用程式後端中的 hello。

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

如需詳細資訊，請參閱 hello [Windows Live SDK]文件。

### <a name="serverflow"></a>伺服器管理的驗證
當您註冊您的身分識別提供者之後時，呼叫 hello [LoginAsync] hello 與 hello [d] 上的方法[MobileServiceAuthenticationProvider]您的提供者的值。 比方說，hello 下列程式碼起始的伺服器流程登入使用 Facebook。

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

如果您使用 Facebook 以外的身分識別提供者，變更 hello 值[MobileServiceAuthenticationProvider] toohello 值提供者。

資料流程中的伺服器，Azure 應用程式服務會管理 hello OAuth 驗證流程，藉由顯示 hello 登入頁面的 hello 選的提供者。  一次 hello 身分識別提供者傳回時，Azure 應用程式服務會產生應用程式服務驗證權杖。 hello [LoginAsync]方法會傳回[MobileServiceUser]，這樣會提供這兩個 hello [UserId] hello 的驗證之使用者與 hello [MobileServiceAuthenticationToken]，做為 JSON web 權杖 (JWT)。 您可以快取並重複使用此權杖，直到它到期為止。 如需詳細資訊，請參閱[Caching hello 驗證語彙基元](#caching)。

### <a name="caching"></a>快取的 hello 驗證權杖
在某些情況下，hello 呼叫 toohello 登入方法可避免在 hello 第一次成功驗證之後儲存 hello 驗證 token 來自 hello 提供者。  Windows 市集和 UWP 應用程式可以使用[PasswordVault] toocache 目前驗證語彙基元成功登入之後，，如下所示：

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

hello 使用者識別碼值會儲存為 hello hello 認證的使用者名稱和 hello 語彙基元為 hello 儲存為 hello 密碼。 您可以在後續的創檢查 hello **PasswordVault**快取的認證。 hello 下列範例會使用快取的認證時找不到，，否則為嘗試一次與 hello 後端 tooauthenticate:

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

當您登出使用者時，您也必須移除 hello 預存認證，如下所示：

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Xamarin 應用程式使用 hello [Xamarin.Auth]中的應用程式開發介面 toosecurely 存放區認證**帳戶**物件。 如需使用這些 Api 的範例，請參閱 hello [AuthStore.cs]程式碼檔案中 hello [ContosoMoments 相片分享範例](https://github.com/azure-appservice-samples/ContosoMoments)。

當您使用管理用戶端驗證時，您也可以快取從您的提供者，例如 Facebook 或 Twitter 取得的 hello 存取權杖。 這個語彙基元可以提供的 toorequest hello 後端中，從新的驗證權杖，如下所示：

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>推播通知
下列主題涵蓋了推播通知的 hello:

* [註冊推播通知](#register-for-push)
* [取得 Windows 市集封裝 SID](#package-sid)
* [利用跨平台範本進行註冊](#register-xplat)

### <a name="register-for-push"></a>做法：註冊推播通知
hello 行動應用程式用戶端可讓您與 Azure 通知中心的推播通知的 tooregister。 您註冊時，取得的控制代碼，您取得從 hello 平台專屬推播通知服務 (PNS)。 當您建立 hello 註冊，然後提供此值以及任何標記。 hello 下列程式碼會註冊您的 Windows 應用程式的推播通知以 hello Windows 通知服務 (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

如果您要推入 tooWNS，則您必須[取得 Windows 市集封裝 SID](#package-sid)。  如需有關 Windows 應用程式，包括如何 tooregister 的範本註冊，請參閱[新增推播通知 tooyour 應用程式]。

不支援從 hello 用戶端要求標記。  註冊時會自動捨棄標記要求。
如果您想 tooregister 標記與您的裝置，建立您的身分使用 hello 通知中樞 API tooperform hello 註冊自訂 API。  [呼叫自訂 API hello](#customapi)而不是 hello`RegisterNativeAsync()`方法。

### <a name="package-sid"></a>如何：取得 Windows 市集封裝 SID
在 Windows 市集應用程式中啟用推播通知需有封裝 SID。  tooreceive 封裝 SID，以 hello Windows 市集註冊您的應用程式。

tooobtain 此值：

1. 在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello Windows 市集應用程式專案中，按一下**存放區** > **將應用程式建立關聯以 hello 存放區...**.
2. 在 hello 精靈中，按一下 **下一步**，使用您的 Microsoft 帳戶登入，輸入您的應用程式中的名稱**新的應用程式名稱保留**，然後按一下 **保留**。
3. Hello 應用程式註冊已成功建立，請選取 hello 應用程式名稱後，請按一下**下一步**，然後按一下**關聯**。
4. 登入 toohello [Windows 開發人員中心]使用您的 Microsoft 帳戶。 在下**我的應用程式**，按一下您建立 hello 應用程式註冊。
5. 按一下**應用程式管理** > **應用程式識別**，然後向下 toofind 捲動您**封裝 SID**。

許多用途的 hello 封裝 SID 將其視為一個 URI，在此情況下您需要 toouse *ms 應用程式: / /*為 hello 配置。 記下您的封裝 SID 做為前置詞，這個值串連起來所構成的 hello 版本。

Xamarin 應用程式需要一些額外的程式碼 toobe 無法 tooregister hello iOS 或 Android 平台上執行的應用程式。 如需詳細資訊，請參閱您的平台的 hello 主題：

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>如何： 註冊推播範本 toosend 跨平台通知
tooregister 範本使用 hello `RegisterAsync()` hello 範本，如下所示的方法：

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

您的範本應該`JObject`類型，而且可以包含多個範本中下列 JSON 格式的 hello:

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

hello 方法**RegisterAsync()**也接受次要磚：

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

為確保安全，註冊期間會移除所有標籤。 tooadd 標記 tooinstallations 或內安裝的範本，查看 [Azure 行動應用程式的工作與 hello.NET 後端伺服器 SDK]。

toosend 通知使用這些已註冊的範本，請參閱 toohello[通知中樞 Api]。

## <a name="misc"></a>其他主題
### <a name="errors"></a>作法：處理錯誤
Hello 後端中發生錯誤時，hello 用戶端 SDK 引發`MobileServiceInvalidOperationException`。  下列範例會示範如何 toohandle hello 後端所傳回的例外狀況：

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

處理錯誤狀況的其他範例，請參閱在 hello[行動應用程式檔案範例]。 [LoggingHandler]範例提供記錄委派處理常式 toolog hello 提出的要求，toohello 後端。

### <a name="headers"></a>作法：自訂要求標頭
toosupport 特定的應用程式案例中，您可能需要與 hello 行動裝置應用程式後端 toocustomize 通訊。 比方說，您可能想 tooadd 自訂標頭 tooevery 外送要求，或甚至變更回應狀態碼。 您可以使用自訂[DelegatingHandler]，如下列範例中的 hello:

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
