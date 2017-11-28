## <a name="repeatability-during-copy"></a><span data-ttu-id="52595-101">在複製期間的重複性</span><span class="sxs-lookup"><span data-stu-id="52595-101">Repeatability during Copy</span></span>
<span data-ttu-id="52595-102">從其他資料存放區複製資料到 Azure SQL/SQL Server 時，需要記住重複性以避免非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="52595-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="52595-103">將資料複製到 Azure SQL/SQL Server Database 時，複製活動預設會將資料集附加至 sink 資料表的尾端。</span><span class="sxs-lookup"><span data-stu-id="52595-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="52595-104">例如，從包含兩筆記錄的 CSV (逗點分隔值) 檔案來源複製資料到 Azure SQL/SQL Server 資料庫時，資料表看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="52595-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="52595-105">假設您在來源檔案中找到錯誤，並將來源檔案中 Down Tube 的數量 (Quantity) 從 2 更新為 4。</span><span class="sxs-lookup"><span data-stu-id="52595-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="52595-106">如果您重新執行該期間的資料配量，會發現有兩筆新記錄附加到 Azure SQL/SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="52595-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="52595-107">以下假設資料表中的資料行都沒有主索引鍵條件約束。</span><span class="sxs-lookup"><span data-stu-id="52595-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="52595-108">若要避免這個問題，您必須利用下述 2 個機制之一來指定 UPSERT 語意。</span><span class="sxs-lookup"><span data-stu-id="52595-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="52595-109">可以根據指定的重試原則在 Azure Data Factory 中自動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="52595-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="52595-110">機制 1</span><span class="sxs-lookup"><span data-stu-id="52595-110">Mechanism 1</span></span>
<span data-ttu-id="52595-111">您可以利用 **sqlWriterCleanupScript** 屬性在執行配量時先進行清理動作。</span><span class="sxs-lookup"><span data-stu-id="52595-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="52595-112">在複製指定的配量時會先執行清除指令碼，這會刪除 SQL 資料表中對應至該配量的資料。</span><span class="sxs-lookup"><span data-stu-id="52595-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="52595-113">活動接著會將資料插入 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="52595-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="52595-114">如果在此時重新執行配量，則會發現數量已如您所需更新了。</span><span class="sxs-lookup"><span data-stu-id="52595-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="52595-115">假設原始 csv 中的 Flat Washer 記錄被移除。</span><span class="sxs-lookup"><span data-stu-id="52595-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="52595-116">則重新執行配量會產生以下結果：</span><span class="sxs-lookup"><span data-stu-id="52595-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="52595-117">不需要再做什麼別的動作。</span><span class="sxs-lookup"><span data-stu-id="52595-117">Nothing new had to be done.</span></span> <span data-ttu-id="52595-118">複製活動執行清除指令碼來刪除該配量的對應資料。</span><span class="sxs-lookup"><span data-stu-id="52595-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="52595-119">然後它會從 csv (只包含 1 筆記錄) 讀取輸入，並將其插入資料表。</span><span class="sxs-lookup"><span data-stu-id="52595-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="52595-120">機制 2</span><span class="sxs-lookup"><span data-stu-id="52595-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52595-121">目前 Azure SQL 資料倉儲不支援 sliceIdentifierColumnName。</span><span class="sxs-lookup"><span data-stu-id="52595-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="52595-122">達成重複性的另一個機制是在目標資料表中使用專用資料行 (**sliceIdentifierColumnName**)。</span><span class="sxs-lookup"><span data-stu-id="52595-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="52595-123">Azure Data Factory 會使用這個資料行以確保來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="52595-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="52595-124">當目的地 SQL 資料表結構描述可彈性變更或定義，就可以使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="52595-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="52595-125">基於重複性的目的，Azure Data Factory 會使用此資料行，且在程序中 Azure Data Factory 將不會對資料表進行任何結構描述變更。</span><span class="sxs-lookup"><span data-stu-id="52595-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="52595-126">如何使用這個方法：</span><span class="sxs-lookup"><span data-stu-id="52595-126">Way to use this approach:</span></span>

1. <span data-ttu-id="52595-127">在目的地 SQL 資料表中定義二進位 (32) 類型的資料行。</span><span class="sxs-lookup"><span data-stu-id="52595-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="52595-128">此資料行不應該有任何條件約束。</span><span class="sxs-lookup"><span data-stu-id="52595-128">There should be no constraints on this column.</span></span> <span data-ttu-id="52595-129">此範例中我們將這個資料行命名為 'ColumnForADFuseOnly'。</span><span class="sxs-lookup"><span data-stu-id="52595-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="52595-130">在複製活動中使用它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="52595-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="52595-131">Azure Data Factory 會根據此資料行的需求填入資料，以確保來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="52595-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="52595-132">使用者不應在此內容之外使用此資料行的值。</span><span class="sxs-lookup"><span data-stu-id="52595-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="52595-133">和機制 1 類似，複製活動會自動先從目的地 SQL 資料表中清除指定配量的資料，然後正常執行複製活動將資料從來源插入至該配量的目的地。</span><span class="sxs-lookup"><span data-stu-id="52595-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

