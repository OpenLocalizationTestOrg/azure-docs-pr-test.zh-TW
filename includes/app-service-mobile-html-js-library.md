## <a name="create-client"></a>建立用戶端連接
建立 `WindowsAzure.MobileServiceClient` 物件來建立用戶端連接。  取代`appUrl`與 URL tooyour 行動裝置應用程式。

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>使用資料表
tooaccess 或更新的資料，建立參考 toohello 後端的資料表。 取代`tableName`與資料表的名稱，hello

```
var table = client.getTable(tableName);
```

只要有資料表參考，就進一步使用資料表進行下列作業︰

* [查詢資料表](#querying)
  * [篩選資料](#table-filter)
  * [逐頁查看資料](#table-paging)
  * [排序資料](#sorting-data)
* [插入資料](#inserting)
* [修改資料](#modifying)
* [刪除資料](#deleting)

### <a name="querying"></a>操作說明 ：查詢資料表參考
一旦您擁有的資料表參考時，您可以使用它 tooquery hello 伺服器上的資料。  您可以使用「類似 LINQ」的語言來撰寫查詢。
tooreturn 所有資料從 hello 資料表中，使用 hello 下列程式都碼：

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

hello 成功函式會呼叫 hello 結果。  請勿使用`for (var i in results)`hello 成功函式，會逐一查看包含在 hello 結果的資訊，當其他查詢函式 (例如`.includeTotalCount()`) 所使用。

如需有關 hello 查詢語法的詳細資訊，請參閱 hello 查詢物件文件]。

#### <a name="table-filter"></a>Hello 伺服器上的篩選資料
您可以使用`where`hello 資料表參考上的子句：

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

您也可以使用篩選 hello 物件的函式。  在此情況下，hello `this` toothe 目前正進行篩選的物件指派給變數。  下列程式碼的 hello 是功能上相當 toohello 先前的範例：

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>逐頁查看資料
利用 hello`take()`和`skip()`方法。  例如，如果您想 toosplit hello 資料表為資料列 100 筆記錄：

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

hello`.includeTotalCount()`方法是使用的 tooadd totalCount 欄位 toohello 結果物件。  TotalCount 欄位填滿 hello 的總記錄數，如果使用不使用分頁，則會傳回。

您可以接著使用 hello 頁面變數，以及一些 UI 按鈕 tooprovide 頁面清單。使用`loadPage()`載入每個頁面的 hello 新記錄。  實作快取 toospeed 存取 toorecords 已載入。

#### <a name="sorting-data"></a>操作說明：傳回已排序的資料
使用 hello`.orderBy()`或`.orderByDescending()`查詢方法：

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

如需有關 hello 查詢物件的詳細資訊，請參閱 hello 查詢物件文件]。

### <a name="inserting"></a>操作說明：插入資料
建立具有 hello 適當的日期和呼叫 JavaScript 物件`table.insert()`以非同步的方式：

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

在成功插入，hello 插入項目會傳回與 hello 所需的同步處理作業的其他欄位。  以這項資訊更新您自己的快取，後續更新時才會正確。

hello Azure 行動應用程式 Node.js 伺服器 SDK 支援動態結構描述為開發用途。  動態結構描述可讓您 toohello tooadd 資料行 資料表的 insert 或 update 作業中指定它們。  我們建議您在移動應用程式 tooproduction 之前關閉動態結構描述。

### <a name="modifying"></a>操作說明：修改資料
類似 toohello`.insert()`方法，您應該建立更新物件，然後呼叫`.update()`。  hello 更新物件必須包含 hello hello 記錄 toobe 更新識別碼-讀取 hello 記錄時，或呼叫時，取得 hello 識別碼`.insert()`。

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

### <a name="deleting"></a>操作說明：刪除資料
toodelete 記錄，呼叫 hello`.del()`方法。  物件參考中傳遞識別碼 hello:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
