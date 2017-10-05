---
title: "Azure Data Factory 中的可重複複製 | Microsoft Docs"
description: "了解如何在即使將複製資料的配量執行多次的情況下，也能避免產生重複的項目。"
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
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="a4e96-103">Azure Data Factory 中的可重複複製</span><span class="sxs-lookup"><span data-stu-id="a4e96-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a4e96-104">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="a4e96-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="a4e96-105">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="a4e96-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a4e96-106">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="a4e96-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a4e96-107">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="a4e96-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a4e96-108">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="a4e96-109">下面的範例是針對 Azure SQL，但也適用於任何支援矩形資料集的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a4e96-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="a4e96-110">您可能必須針對資料存放區調整來源的**類型**和 **query** 屬性 (例如：query 而不是 sqlReaderQuery)。</span><span class="sxs-lookup"><span data-stu-id="a4e96-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="a4e96-111">通常從關聯式存放區進行讀取時，您會希望只讀取與該配量對應的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="a4e96-112">有一個可達到此目的的方法，就是使用 Azure Data Factory 中提供的 WindowStart 和 WindowEnd 系統變數。</span><span class="sxs-lookup"><span data-stu-id="a4e96-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="a4e96-113">若要了解 Azure Data Factory 中的變數與函式，請參閱 [Azure Data Factory - 函式與系統變數](data-factory-functions-variables.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a4e96-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="a4e96-114">範例：</span><span class="sxs-lookup"><span data-stu-id="a4e96-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="a4e96-115">此查詢會從 MyTable 資料表中，讀取配量持續時間範圍內 (WindowStart -> WindowEnd) 的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="a4e96-116">重新執行此配量也會一律確保讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="a4e96-117">在其他情況下，您可能會想要閱讀整份資料表，而可以依下列方式定義 sqlReaderQuery：</span><span class="sxs-lookup"><span data-stu-id="a4e96-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="a4e96-118">對 SqlSink 進行可重複的寫入</span><span class="sxs-lookup"><span data-stu-id="a4e96-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="a4e96-119">將資料從其他資料存放區複製到 **Azure SQL/SQL Server** 時，您需將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="a4e96-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="a4e96-120">將資料複製到「Azure SQL/SQL Server 資料庫」時，複製活動預設會將資料附加至接收資料表。</span><span class="sxs-lookup"><span data-stu-id="a4e96-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="a4e96-121">假設您要將資料從包含兩筆記錄的 CSV (逗點分隔值) 檔案複製到「Azure SQL/SQL Server 資料庫」中的下列資料表。</span><span class="sxs-lookup"><span data-stu-id="a4e96-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="a4e96-122">當配量執行時，會將該兩筆記錄複製到 SQL 資料表中。</span><span class="sxs-lookup"><span data-stu-id="a4e96-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="a4e96-123">假設您在來源檔案中發現錯誤，並將 Down Tube 的數量從 2 更新為 4。</span><span class="sxs-lookup"><span data-stu-id="a4e96-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="a4e96-124">如果您手動重新執行該期間的資料配量，您將會發現有兩筆新記錄附加到「Azure SQL/SQL Server 資料庫」。</span><span class="sxs-lookup"><span data-stu-id="a4e96-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="a4e96-125">此範例是假設資料表中的所有資料行都沒有主索引鍵條件約束。</span><span class="sxs-lookup"><span data-stu-id="a4e96-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="a4e96-126">若要避免此行為，您必須使用以下兩個機制其中之一來指定 UPSERT 語意：</span><span class="sxs-lookup"><span data-stu-id="a4e96-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="a4e96-127">機制 1：使用 sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="a4e96-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="a4e96-128">您可以在執行配量時，先使用 **sqlWriterCleanupScript** 屬性將資料從接收資料表中清除，然後才插入資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="a4e96-129">當配量執行時，會先執行清除指令碼，從 SQL 資料表中刪除與該配量對應的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="a4e96-130">複製活動會接著將資料插入到 SQL 資料表中。</span><span class="sxs-lookup"><span data-stu-id="a4e96-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="a4e96-131">如果重新執行配量，將會視需要更新數量。</span><span class="sxs-lookup"><span data-stu-id="a4e96-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="a4e96-132">假設原始 csv 中的 Flat Washer 記錄被移除。</span><span class="sxs-lookup"><span data-stu-id="a4e96-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="a4e96-133">則重新執行配量會產生以下結果：</span><span class="sxs-lookup"><span data-stu-id="a4e96-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="a4e96-134">複製活動執行清除指令碼來刪除該配量的對應資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="a4e96-135">接著，它會從 csv (只包含一筆記錄) 讀取輸入，並將它插入到資料表中。</span><span class="sxs-lookup"><span data-stu-id="a4e96-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="a4e96-136">機制 2：使用 sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="a4e96-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a4e96-137">目前「Azure SQL 資料倉儲」並不支援 sliceIdentifierColumnName。</span><span class="sxs-lookup"><span data-stu-id="a4e96-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="a4e96-138">達成可重複性的第二個機制是在目標資料表中擁有一個專用的資料行 (sliceIdentifierColumnName)。</span><span class="sxs-lookup"><span data-stu-id="a4e96-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="a4e96-139">Azure Data Factory 會使用這個資料行以確保來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="a4e96-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="a4e96-140">當目的地 SQL 資料表結構描述可彈性變更或定義，就可以使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="a4e96-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="a4e96-141">Azure Data Factory 會基於可重複性目的使用此資料行，且在過程中 Azure Data Factory 不會對資料表進行任何結構描述變更。</span><span class="sxs-lookup"><span data-stu-id="a4e96-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="a4e96-142">如何使用這個方法：</span><span class="sxs-lookup"><span data-stu-id="a4e96-142">Way to use this approach:</span></span>

1. <span data-ttu-id="a4e96-143">在目的地 SQL 資料表中定義一個「二進位 (32)」類型的資料行。</span><span class="sxs-lookup"><span data-stu-id="a4e96-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="a4e96-144">此資料行不應該有任何條件約束。</span><span class="sxs-lookup"><span data-stu-id="a4e96-144">There should be no constraints on this column.</span></span> <span data-ttu-id="a4e96-145">讓我們針對此範例將這個資料行命名為 AdfSliceIdentifier。</span><span class="sxs-lookup"><span data-stu-id="a4e96-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="a4e96-146">來源資料表：</span><span class="sxs-lookup"><span data-stu-id="a4e96-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="a4e96-147">目的地資料表：</span><span class="sxs-lookup"><span data-stu-id="a4e96-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="a4e96-148">在複製活動中使用它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4e96-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="a4e96-149">Azure Data Factory 會根據其需求來填入此資料行，以確保來源和目的地保持同步。</span><span class="sxs-lookup"><span data-stu-id="a4e96-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="a4e96-150">此資料行的值不應用於此內容之外。</span><span class="sxs-lookup"><span data-stu-id="a4e96-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="a4e96-151">與機制 1 類似，「複製活動」也會自動從目的地 SQL 資料表中清除所指定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="a4e96-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="a4e96-152">接著，它會將來自來源的資料插入到目的地資料表中。</span><span class="sxs-lookup"><span data-stu-id="a4e96-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a4e96-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4e96-153">Next steps</span></span>
<span data-ttu-id="a4e96-154">如需完整的 JSON 範例，請檢閱下列連接器文章：</span><span class="sxs-lookup"><span data-stu-id="a4e96-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="a4e96-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4e96-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="a4e96-156">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="a4e96-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="a4e96-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a4e96-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)