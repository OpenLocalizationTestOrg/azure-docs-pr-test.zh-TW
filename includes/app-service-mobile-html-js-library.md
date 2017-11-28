## <span data-ttu-id="3532c-101"><a name="create-client"></a>建立用戶端連接</span><span class="sxs-lookup"><span data-stu-id="3532c-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="3532c-102">建立 `WindowsAzure.MobileServiceClient` 物件來建立用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="3532c-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="3532c-103">以您行動應用程式的 URL 取代 `appUrl` 。</span><span class="sxs-lookup"><span data-stu-id="3532c-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="3532c-104"><a name="table-reference"></a>使用資料表</span><span class="sxs-lookup"><span data-stu-id="3532c-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="3532c-105">若要存取或更新資料，請建立後端資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="3532c-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="3532c-106">以您的資料表名稱取代 `tableName`</span><span class="sxs-lookup"><span data-stu-id="3532c-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="3532c-107">只要有資料表參考，就進一步使用資料表進行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="3532c-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="3532c-108">查詢資料表</span><span class="sxs-lookup"><span data-stu-id="3532c-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="3532c-109">篩選資料</span><span class="sxs-lookup"><span data-stu-id="3532c-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="3532c-110">逐頁查看資料</span><span class="sxs-lookup"><span data-stu-id="3532c-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="3532c-111">排序資料</span><span class="sxs-lookup"><span data-stu-id="3532c-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="3532c-112">插入資料</span><span class="sxs-lookup"><span data-stu-id="3532c-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="3532c-113">修改資料</span><span class="sxs-lookup"><span data-stu-id="3532c-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="3532c-114">刪除資料</span><span class="sxs-lookup"><span data-stu-id="3532c-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="3532c-115"><a name="querying"></a>操作說明 ：查詢資料表參考</span><span class="sxs-lookup"><span data-stu-id="3532c-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="3532c-116">取得資料表參考之後，您可以使用它來查詢伺服器上的資料。</span><span class="sxs-lookup"><span data-stu-id="3532c-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="3532c-117">您可以使用「類似 LINQ」的語言來撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="3532c-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="3532c-118">若要從資料表傳回所有資料，使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="3532c-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="3532c-119">搭配 results 呼叫 success 函式。</span><span class="sxs-lookup"><span data-stu-id="3532c-119">The success function is called with the results.</span></span>  <span data-ttu-id="3532c-120">請勿在 success 函式中使用 `for (var i in results)`，因為當使用其他查詢函式時 (例如 `.includeTotalCount()`)，這樣會反覆檢查結果中包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="3532c-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="3532c-121">如需 Query 語法的詳細資訊，請參閱 [Query 物件文件]。</span><span class="sxs-lookup"><span data-stu-id="3532c-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="3532c-122"><a name="table-filter"></a>篩選伺服器的資料</span><span class="sxs-lookup"><span data-stu-id="3532c-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="3532c-123">您可以在資料表參考上使用 `where` 子句：</span><span class="sxs-lookup"><span data-stu-id="3532c-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="3532c-124">您也可以使用函式來篩選物件。</span><span class="sxs-lookup"><span data-stu-id="3532c-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="3532c-125">在此案例中， `this` 變數會指派給目前篩選的物件。</span><span class="sxs-lookup"><span data-stu-id="3532c-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="3532c-126">以下程式碼在功能上等同於先前的範例：</span><span class="sxs-lookup"><span data-stu-id="3532c-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="3532c-127"><a name="table-paging"></a>逐頁查看資料</span><span class="sxs-lookup"><span data-stu-id="3532c-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="3532c-128">利用 `take()` 和 `skip()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3532c-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="3532c-129">例如，如果您想要將資料表分割成 100 列的記錄：</span><span class="sxs-lookup"><span data-stu-id="3532c-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
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

<span data-ttu-id="3532c-130">`.includeTotalCount()` 方法是用來將 totalCount 欄位加入至 results 物件。</span><span class="sxs-lookup"><span data-stu-id="3532c-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="3532c-131">totalCount 欄位中填入未使用分頁時會傳回的記錄總數。</span><span class="sxs-lookup"><span data-stu-id="3532c-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="3532c-132">接著，您可以使用 pages 變數和一些 UI 按鈕來提供頁面清單。您可以使用 `loadPage()` 載入每個頁面的新記錄。</span><span class="sxs-lookup"><span data-stu-id="3532c-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="3532c-133">實作快取來加速存取已經載入的記錄。</span><span class="sxs-lookup"><span data-stu-id="3532c-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="3532c-134"><a name="sorting-data"></a>操作說明：傳回已排序的資料</span><span class="sxs-lookup"><span data-stu-id="3532c-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="3532c-135">使用 `.orderBy()` 或 `.orderByDescending()` 查詢方法︰</span><span class="sxs-lookup"><span data-stu-id="3532c-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="3532c-136">如需 Query 物件的詳細資訊，請參閱 [Query 物件文件]。</span><span class="sxs-lookup"><span data-stu-id="3532c-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="3532c-137"><a name="inserting"></a>操作說明：插入資料</span><span class="sxs-lookup"><span data-stu-id="3532c-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="3532c-138">以適當的日期建立 JavaScript 物件，並以非同步方式呼叫 `table.insert()`：</span><span class="sxs-lookup"><span data-stu-id="3532c-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="3532c-139">在成功插入時，插入的項目及同步處理作業所需的其他欄位會一起傳回。</span><span class="sxs-lookup"><span data-stu-id="3532c-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="3532c-140">以這項資訊更新您自己的快取，後續更新時才會正確。</span><span class="sxs-lookup"><span data-stu-id="3532c-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="3532c-141">Azure Mobile Apps Node.js Server SDK 支援的動態結構描述適用於開發用途。</span><span class="sxs-lookup"><span data-stu-id="3532c-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="3532c-142">動態結構描述可讓您在插入或更新作業中指定資料行，以將資料行新增至資料表。</span><span class="sxs-lookup"><span data-stu-id="3532c-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="3532c-143">在將應用程式移至生產環境之前，我們建議您關閉動態結構描述。</span><span class="sxs-lookup"><span data-stu-id="3532c-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="3532c-144"><a name="modifying"></a>操作說明：修改資料</span><span class="sxs-lookup"><span data-stu-id="3532c-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="3532c-145">類似於 `.insert()` 方法，您應該建立 Update 物件，然後呼叫 `.update()`。</span><span class="sxs-lookup"><span data-stu-id="3532c-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="3532c-146">Update 物件必須包含要更新的記錄的識別碼 - 在讀取記錄或呼叫 `.insert()` 時會取得此識別碼。</span><span class="sxs-lookup"><span data-stu-id="3532c-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="3532c-147"><a name="deleting"></a>操作說明：刪除資料</span><span class="sxs-lookup"><span data-stu-id="3532c-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="3532c-148">若要刪除記錄時，請呼叫 `.del()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3532c-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="3532c-149">將識別碼傳入物件參考中：</span><span class="sxs-lookup"><span data-stu-id="3532c-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
