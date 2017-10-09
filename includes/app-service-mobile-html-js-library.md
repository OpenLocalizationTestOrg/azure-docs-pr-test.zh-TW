## <span data-ttu-id="54018-101"><a name="create-client"></a>建立用戶端連接</span><span class="sxs-lookup"><span data-stu-id="54018-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="54018-102">建立 `WindowsAzure.MobileServiceClient` 物件來建立用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="54018-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="54018-103">取代`appUrl`與 URL tooyour 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="54018-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="54018-104"><a name="table-reference"></a>使用資料表</span><span class="sxs-lookup"><span data-stu-id="54018-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="54018-105">tooaccess 或更新的資料，建立參考 toohello 後端的資料表。</span><span class="sxs-lookup"><span data-stu-id="54018-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="54018-106">取代`tableName`與資料表的名稱，hello</span><span class="sxs-lookup"><span data-stu-id="54018-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="54018-107">只要有資料表參考，就進一步使用資料表進行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="54018-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="54018-108">查詢資料表</span><span class="sxs-lookup"><span data-stu-id="54018-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="54018-109">篩選資料</span><span class="sxs-lookup"><span data-stu-id="54018-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="54018-110">逐頁查看資料</span><span class="sxs-lookup"><span data-stu-id="54018-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="54018-111">排序資料</span><span class="sxs-lookup"><span data-stu-id="54018-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="54018-112">插入資料</span><span class="sxs-lookup"><span data-stu-id="54018-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="54018-113">修改資料</span><span class="sxs-lookup"><span data-stu-id="54018-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="54018-114">刪除資料</span><span class="sxs-lookup"><span data-stu-id="54018-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="54018-115"><a name="querying"></a>操作說明 ：查詢資料表參考</span><span class="sxs-lookup"><span data-stu-id="54018-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="54018-116">一旦您擁有的資料表參考時，您可以使用它 tooquery hello 伺服器上的資料。</span><span class="sxs-lookup"><span data-stu-id="54018-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="54018-117">您可以使用「類似 LINQ」的語言來撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="54018-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="54018-118">tooreturn 所有資料從 hello 資料表中，使用 hello 下列程式都碼：</span><span class="sxs-lookup"><span data-stu-id="54018-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="54018-119">hello 成功函式會呼叫 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="54018-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="54018-120">請勿使用`for (var i in results)`hello 成功函式，會逐一查看包含在 hello 結果的資訊，當其他查詢函式 (例如`.includeTotalCount()`) 所使用。</span><span class="sxs-lookup"><span data-stu-id="54018-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="54018-121">如需有關 hello 查詢語法的詳細資訊，請參閱 hello 查詢物件文件]。</span><span class="sxs-lookup"><span data-stu-id="54018-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="54018-122"><a name="table-filter"></a>Hello 伺服器上的篩選資料</span><span class="sxs-lookup"><span data-stu-id="54018-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="54018-123">您可以使用`where`hello 資料表參考上的子句：</span><span class="sxs-lookup"><span data-stu-id="54018-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="54018-124">您也可以使用篩選 hello 物件的函式。</span><span class="sxs-lookup"><span data-stu-id="54018-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="54018-125">在此情況下，hello `this` toothe 目前正進行篩選的物件指派給變數。</span><span class="sxs-lookup"><span data-stu-id="54018-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="54018-126">下列程式碼的 hello 是功能上相當 toohello 先前的範例：</span><span class="sxs-lookup"><span data-stu-id="54018-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="54018-127"><a name="table-paging"></a>逐頁查看資料</span><span class="sxs-lookup"><span data-stu-id="54018-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="54018-128">利用 hello`take()`和`skip()`方法。</span><span class="sxs-lookup"><span data-stu-id="54018-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="54018-129">例如，如果您想 toosplit hello 資料表為資料列 100 筆記錄：</span><span class="sxs-lookup"><span data-stu-id="54018-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="54018-130">hello`.includeTotalCount()`方法是使用的 tooadd totalCount 欄位 toohello 結果物件。</span><span class="sxs-lookup"><span data-stu-id="54018-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="54018-131">TotalCount 欄位填滿 hello 的總記錄數，如果使用不使用分頁，則會傳回。</span><span class="sxs-lookup"><span data-stu-id="54018-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="54018-132">您可以接著使用 hello 頁面變數，以及一些 UI 按鈕 tooprovide 頁面清單。使用`loadPage()`載入每個頁面的 hello 新記錄。</span><span class="sxs-lookup"><span data-stu-id="54018-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="54018-133">實作快取 toospeed 存取 toorecords 已載入。</span><span class="sxs-lookup"><span data-stu-id="54018-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="54018-134"><a name="sorting-data"></a>操作說明：傳回已排序的資料</span><span class="sxs-lookup"><span data-stu-id="54018-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="54018-135">使用 hello`.orderBy()`或`.orderByDescending()`查詢方法：</span><span class="sxs-lookup"><span data-stu-id="54018-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="54018-136">如需有關 hello 查詢物件的詳細資訊，請參閱 hello 查詢物件文件]。</span><span class="sxs-lookup"><span data-stu-id="54018-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="54018-137"><a name="inserting"></a>操作說明：插入資料</span><span class="sxs-lookup"><span data-stu-id="54018-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="54018-138">建立具有 hello 適當的日期和呼叫 JavaScript 物件`table.insert()`以非同步的方式：</span><span class="sxs-lookup"><span data-stu-id="54018-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="54018-139">在成功插入，hello 插入項目會傳回與 hello 所需的同步處理作業的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="54018-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="54018-140">以這項資訊更新您自己的快取，後續更新時才會正確。</span><span class="sxs-lookup"><span data-stu-id="54018-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="54018-141">hello Azure 行動應用程式 Node.js 伺服器 SDK 支援動態結構描述為開發用途。</span><span class="sxs-lookup"><span data-stu-id="54018-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="54018-142">動態結構描述可讓您 toohello tooadd 資料行 資料表的 insert 或 update 作業中指定它們。</span><span class="sxs-lookup"><span data-stu-id="54018-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="54018-143">我們建議您在移動應用程式 tooproduction 之前關閉動態結構描述。</span><span class="sxs-lookup"><span data-stu-id="54018-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="54018-144"><a name="modifying"></a>操作說明：修改資料</span><span class="sxs-lookup"><span data-stu-id="54018-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="54018-145">類似 toohello`.insert()`方法，您應該建立更新物件，然後呼叫`.update()`。</span><span class="sxs-lookup"><span data-stu-id="54018-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="54018-146">hello 更新物件必須包含 hello hello 記錄 toobe 更新識別碼-讀取 hello 記錄時，或呼叫時，取得 hello 識別碼`.insert()`。</span><span class="sxs-lookup"><span data-stu-id="54018-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="54018-147"><a name="deleting"></a>操作說明：刪除資料</span><span class="sxs-lookup"><span data-stu-id="54018-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="54018-148">toodelete 記錄，呼叫 hello`.del()`方法。</span><span class="sxs-lookup"><span data-stu-id="54018-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="54018-149">物件參考中傳遞識別碼 hello:</span><span class="sxs-lookup"><span data-stu-id="54018-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
