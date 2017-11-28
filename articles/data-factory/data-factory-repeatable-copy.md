---
title: "Azure Data Factory 中的 aaaRepeatable 複製 |Microsoft 文件"
description: "了解 tooavoid 重複即使複製資料配量執行一次以上的資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="9bd0b-103">Azure Data Factory 中的可重複複製</span><span class="sxs-lookup"><span data-stu-id="9bd0b-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="9bd0b-104">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="9bd0b-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="9bd0b-105">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="9bd0b-106">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9bd0b-107">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9bd0b-108">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="9bd0b-109">hello 下列範例是適用於 Azure SQL 但支援矩形的資料集的適用 tooany 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="9bd0b-110">您可能必須 tooadjust hello**類型**的來源和 hello**查詢**屬性 (例如： 查詢，而不是 sqlReaderQuery) hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="9bd0b-111">通常，當從關聯式存放區讀取，您會想 tooread 對應 toothat 配量只 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="9bd0b-112">因此方式 toodo 會是使用 Azure Data Factory 中的 hello WindowStart 和 WindowEnd 系統變數可用。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="9bd0b-113">閱讀有關 hello 變數和 Azure Data Factory 中的函式，在 hello [Azure Data Factory-函式和系統變數](data-factory-functions-variables.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="9bd0b-114">範例：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="9bd0b-115">此查詢會讀取從 hello 資料表 MyTable 落在 hello 配量持續時間範圍 (WindowStart-> WindowEnd) 中的資料。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="9bd0b-116">重新執行此配量一定會確保相同資料讀取該 hello。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="9bd0b-117">在其他情況下，您可能希望 tooread hello 整份資料表，並可能定義 hello sqlReaderQuery，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="9bd0b-118">可重複寫入 tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="9bd0b-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="9bd0b-119">太複製資料時**Azure SQL/SQL Server**從其他資料存放區中，您必須注意 tooavoid tookeep 直至非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="9bd0b-120">當複製資料 tooAzure SQL/SQL Server 資料庫，hello 複製活動將預設附加 toohello 接收資料表。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="9bd0b-121">例如，您會將資料複製包含兩筆記錄 toohello 下表中的 Azure SQL/SQL Server 資料庫 CSV （逗點分隔值） 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="9bd0b-122">配量執行時，hello 兩筆記錄會複製的 toohello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="9bd0b-123">假設您在原始程式檔中發現錯誤，並更新 hello 2 too4 的向下 Tube 最低數量。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="9bd0b-124">如果您重新執行 hello 資料配量的這段時間內以手動方式，您會看到兩個新的記錄會附加 tooAzure SQL/SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="9bd0b-125">這個範例假設所有的 hello hello 資料表中的資料行都沒有 hello 主索引鍵條件約束。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="9bd0b-126">tooavoid 這種行為，您需要 toospecify UPSERT 語意使用其中一種 hello 下列兩種機制：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="9bd0b-127">機制 1：使用 sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="9bd0b-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="9bd0b-128">您可以使用 hello **sqlWriterCleanupScript**屬性 tooclean hello 之前插入 hello 資料配量執行時，接收資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="9bd0b-129">對應來源 hello SQL 資料表 toohello 配量的第一個 toodelete 資料配量執行時，執行 hello 清除指令碼。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="9bd0b-130">然後 hello 複製活動會將資料插入 hello SQL 資料表中。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="9bd0b-131">如果重新執行 hello 配量時，更新 hello 數量視。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="9bd0b-132">假設 hello 一般墊圈記錄被移除了 hello 原始 csv。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="9bd0b-133">然後重新執行 hello 配量會產生下列結果 hello:</span><span class="sxs-lookup"><span data-stu-id="9bd0b-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="9bd0b-134">hello 複製活動已執行 hello 清除指令碼 toodelete hello 對應的資料為該扇區。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="9bd0b-135">然後輸入 hello 讀取 hello csv （可再包含只有一筆記錄） 並插入 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="9bd0b-136">機制 2：使用 sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="9bd0b-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9bd0b-137">目前「Azure SQL 資料倉儲」並不支援 sliceIdentifierColumnName。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="9bd0b-138">第二個機制 tooachieve 重複性 hello 是專用的資料行 (使用 sliceIdentifierColumnName) 擁有 hello 目標資料表中。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="9bd0b-139">Azure Data Factory tooensure hello 來源和目的地保持同步處理會使用這個資料行。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="9bd0b-140">這個方法的效果時變更，或定義 hello 目的地 SQL 資料表結構描述的彈性。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="9bd0b-141">此資料行用於 Azure Data factory 重複性和 hello 程序中，Azure Data Factory 不會進行任何結構描述變更 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="9bd0b-142">方式 toouse 這種方法：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="9bd0b-143">定義類型的資料行**二進位檔 (32)** hello 目的地 SQL 資料表中。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="9bd0b-144">此資料行不應該有任何條件約束。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-144">There should be no constraints on this column.</span></span> <span data-ttu-id="9bd0b-145">讓我們針對此範例將這個資料行命名為 AdfSliceIdentifier。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="9bd0b-146">來源資料表：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="9bd0b-147">目的地資料表：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="9bd0b-148">使用它 hello 複製活動中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="9bd0b-149">Azure Data Factory 會填入此資料行，其需要根據 tooensure hello 來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="9bd0b-150">hello 這個資料行值不應該使用這個環境之外。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="9bd0b-151">類似 toomechanism 1，複製活動會自動清除 hello hello 從 hello 目的地 SQL 資料表指定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="9bd0b-152">然後將資料插入從 toohello 目的地資料表中的來源。</span><span class="sxs-lookup"><span data-stu-id="9bd0b-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9bd0b-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bd0b-153">Next steps</span></span>
<span data-ttu-id="9bd0b-154">檢閱下列連接器的 hello 文件，如需完整的 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="9bd0b-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="9bd0b-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9bd0b-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="9bd0b-156">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9bd0b-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="9bd0b-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9bd0b-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)