## <a name="repeatability-during-copy"></a><span data-ttu-id="6b8f4-101">在複製期間的重複性</span><span class="sxs-lookup"><span data-stu-id="6b8f4-101">Repeatability during Copy</span></span>
<span data-ttu-id="6b8f4-102">當複製資料 tooAzure SQL/SQL Server 從其他資料存放一個需求 tookeep 重複性注意 tooavoid 非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="6b8f4-103">複製資料 tooAzure SQL/SQL Server 資料庫，複製活動會依預設附加 hello 資料集 toohello 接收資料表預設。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="6b8f4-104">例如，當複製資料，資料來源的 CSV （逗號分隔值） 檔案包含兩個記錄 tooAzure SQL/SQL Server 資料庫，這會是看起來像哪些 hello 資料表：</span><span class="sxs-lookup"><span data-stu-id="6b8f4-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="6b8f4-105">假設您在原始程式檔和更新的 hello 數量的向下 Tube 從 2 too4 找到錯誤 hello 原始程式檔中。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="6b8f4-106">如果您重新執行 hello 資料配量，該期間內，您會看到兩個新的記錄會附加 tooAzure SQL/SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="6b8f4-107">下面的 hello 假設 hello hello 資料表中的資料行都沒有 hello 主索引鍵條件約束。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="6b8f4-108">tooavoid，您必須利用以下 2 的機制，如下所示的 hello toospecify UPSERT 語意。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="6b8f4-109">配量可以重新執行自動 Azure Data Factory 中根據指定的 hello 重試原則。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="6b8f4-110">機制 1</span><span class="sxs-lookup"><span data-stu-id="6b8f4-110">Mechanism 1</span></span>
<span data-ttu-id="6b8f4-111">您可以利用**sqlWriterCleanupScript**屬性 toofirst 執行配量時，請執行清理動作。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="6b8f4-112">hello 清除指令碼就會執行第一個複製指定的配量會刪除 hello SQL 資料表對應 toothat 配量的 hello 資料的期間。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="6b8f4-113">hello 活動接著會插入 hello 資料 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="6b8f4-114">如果 hello 配量是現在重新執行，則您會發現 hello 數量會更新為所需。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="6b8f4-115">假設 hello 一般墊圈記錄被移除了 hello 原始 csv。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="6b8f4-116">然後重新執行 hello 配量會產生下列結果 hello:</span><span class="sxs-lookup"><span data-stu-id="6b8f4-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="6b8f4-117">新的執行任何動作必須 toobe 完成。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-117">Nothing new had toobe done.</span></span> <span data-ttu-id="6b8f4-118">hello 複製活動已執行 hello 清除指令碼 toodelete hello 對應的資料為該扇區。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="6b8f4-119">然後輸入 hello 讀取 hello csv （可再包含只有 1 筆記錄） 並插入 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="6b8f4-120">機制 2</span><span class="sxs-lookup"><span data-stu-id="6b8f4-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6b8f4-121">目前 Azure SQL 資料倉儲不支援 sliceIdentifierColumnName。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="6b8f4-122">另一個機制 tooachieve 重複性，是由專用的資料行 (**sliceIdentifierColumnName**) 在 hello 為目標資料表。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="6b8f4-123">Azure Data Factory tooensure hello 來源和目的地保持同步處理會使用這個資料行。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="6b8f4-124">這個方法的效果時變更，或定義 hello 目的地 SQL 資料表結構描述的彈性。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="6b8f4-125">重複性基於 Azure Data Factory 會使用這個資料行和 hello 程序在 Azure Data Factory 不會進行任何結構描述變更 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="6b8f4-126">方式 toouse 這種方法：</span><span class="sxs-lookup"><span data-stu-id="6b8f4-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="6b8f4-127">Hello 目的地 SQL 資料表中定義類型的二進位 (32) 的資料行。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="6b8f4-128">此資料行不應該有任何條件約束。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-128">There should be no constraints on this column.</span></span> <span data-ttu-id="6b8f4-129">此範例中我們將這個資料行命名為 'ColumnForADFuseOnly'。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="6b8f4-130">使用它 hello 複製活動中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b8f4-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="6b8f4-131">Azure Data Factory 會擴展這個資料行會根據其 tooensure hello 來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="6b8f4-132">hello 這個資料行值不應該使用這個環境之外 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="6b8f4-133">類似 toomechanism 1，複製活動便會自動清除 hello 從 hello 目的地 SQL 資料表配量，然後執行正常 hello 複製活動的 hello 資料第一次從該扇區的來源 toodestination tooinsert hello 資料。</span><span class="sxs-lookup"><span data-stu-id="6b8f4-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

