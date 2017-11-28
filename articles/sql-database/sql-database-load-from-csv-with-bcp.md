---
title: "將資料從 CSV 檔案載入 Azure SQL Database (bcp) | Microsoft Docs"
description: "對於較小的資料大小，請使用 bcp 將資料匯入 Azure SQL Database。"
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="d0306-103">將資料從 CSV 載入 Azure SQL Database (一般檔案)</span><span class="sxs-lookup"><span data-stu-id="d0306-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="d0306-104">您可以使用 bcp 命令列公用程式，將資料從 CSV 檔案匯入 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d0306-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d0306-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="d0306-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d0306-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="d0306-106">Prerequisites</span></span>
<span data-ttu-id="d0306-107">若要完成本文中的步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="d0306-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="d0306-108">Azure SQL Database 邏輯伺服器和資料庫</span><span class="sxs-lookup"><span data-stu-id="d0306-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="d0306-109">已安裝的 bcp 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="d0306-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="d0306-110">已安裝的 sqlcmd 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="d0306-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="d0306-111">您可以從 [Microsoft 下載中心][Microsoft Download Center]下載 bcp 和 sqlcmd 公用程式。</span><span class="sxs-lookup"><span data-stu-id="d0306-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="d0306-112">ASCII 或 UTF-16 格式的資料</span><span class="sxs-lookup"><span data-stu-id="d0306-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="d0306-113">如果您使用您自己的資料嘗試本教學課程，您的資料必須使用 ASCII 或 UTF-16 編碼，因為 bcp 不支援 UFT-8。</span><span class="sxs-lookup"><span data-stu-id="d0306-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="d0306-114">1.建立目的資料表</span><span class="sxs-lookup"><span data-stu-id="d0306-114">1. Create a destination table</span></span>
<span data-ttu-id="d0306-115">在 SQL Database 中定義做為目的地資料表的資料表。</span><span class="sxs-lookup"><span data-stu-id="d0306-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="d0306-116">資料表中的資料行必須對應到資料檔的每一個資料列中的資料。</span><span class="sxs-lookup"><span data-stu-id="d0306-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="d0306-117">若要建立資料表，請開啟命令提示字元並使用 sqlcmd.exe 執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d0306-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="d0306-118">2.建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="d0306-118">2. Create a source data file</span></span>
<span data-ttu-id="d0306-119">開啟 [記事本]，將下列幾行資料複製到新的文字檔，然後將此檔案儲存到本機暫存目錄 C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="d0306-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="d0306-120">此資料是 ASCII 格式。</span><span class="sxs-lookup"><span data-stu-id="d0306-120">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="d0306-121">(選擇性) 若要從 SQL Server 資料庫匯出您自己的資料，請開啟命令提示字元並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d0306-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="d0306-122">使用您自己的資訊取代 TableName、ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="d0306-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="d0306-123">3.載入資料</span><span class="sxs-lookup"><span data-stu-id="d0306-123">3. Load the data</span></span>
<span data-ttu-id="d0306-124">若要載入資料，請開啟命令提示字元並執行下列命令，使用您自己的資訊取代 ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="d0306-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="d0306-125">使用此命令來確認已正確載入資料</span><span class="sxs-lookup"><span data-stu-id="d0306-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="d0306-126">結果應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="d0306-126">The results should look like this:</span></span>

| <span data-ttu-id="d0306-127">DateId</span><span class="sxs-lookup"><span data-stu-id="d0306-127">DateId</span></span> | <span data-ttu-id="d0306-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="d0306-128">CalendarQuarter</span></span> | <span data-ttu-id="d0306-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="d0306-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d0306-130">20150101</span><span class="sxs-lookup"><span data-stu-id="d0306-130">20150101</span></span> |<span data-ttu-id="d0306-131">1</span><span class="sxs-lookup"><span data-stu-id="d0306-131">1</span></span> |<span data-ttu-id="d0306-132">3</span><span class="sxs-lookup"><span data-stu-id="d0306-132">3</span></span> |
| <span data-ttu-id="d0306-133">20150201</span><span class="sxs-lookup"><span data-stu-id="d0306-133">20150201</span></span> |<span data-ttu-id="d0306-134">1</span><span class="sxs-lookup"><span data-stu-id="d0306-134">1</span></span> |<span data-ttu-id="d0306-135">3</span><span class="sxs-lookup"><span data-stu-id="d0306-135">3</span></span> |
| <span data-ttu-id="d0306-136">20150301</span><span class="sxs-lookup"><span data-stu-id="d0306-136">20150301</span></span> |<span data-ttu-id="d0306-137">1</span><span class="sxs-lookup"><span data-stu-id="d0306-137">1</span></span> |<span data-ttu-id="d0306-138">3</span><span class="sxs-lookup"><span data-stu-id="d0306-138">3</span></span> |
| <span data-ttu-id="d0306-139">20150401</span><span class="sxs-lookup"><span data-stu-id="d0306-139">20150401</span></span> |<span data-ttu-id="d0306-140">2</span><span class="sxs-lookup"><span data-stu-id="d0306-140">2</span></span> |<span data-ttu-id="d0306-141">4</span><span class="sxs-lookup"><span data-stu-id="d0306-141">4</span></span> |
| <span data-ttu-id="d0306-142">20150501</span><span class="sxs-lookup"><span data-stu-id="d0306-142">20150501</span></span> |<span data-ttu-id="d0306-143">2</span><span class="sxs-lookup"><span data-stu-id="d0306-143">2</span></span> |<span data-ttu-id="d0306-144">4</span><span class="sxs-lookup"><span data-stu-id="d0306-144">4</span></span> |
| <span data-ttu-id="d0306-145">20150601</span><span class="sxs-lookup"><span data-stu-id="d0306-145">20150601</span></span> |<span data-ttu-id="d0306-146">2</span><span class="sxs-lookup"><span data-stu-id="d0306-146">2</span></span> |<span data-ttu-id="d0306-147">4</span><span class="sxs-lookup"><span data-stu-id="d0306-147">4</span></span> |
| <span data-ttu-id="d0306-148">20150701</span><span class="sxs-lookup"><span data-stu-id="d0306-148">20150701</span></span> |<span data-ttu-id="d0306-149">3</span><span class="sxs-lookup"><span data-stu-id="d0306-149">3</span></span> |<span data-ttu-id="d0306-150">1</span><span class="sxs-lookup"><span data-stu-id="d0306-150">1</span></span> |
| <span data-ttu-id="d0306-151">20150801</span><span class="sxs-lookup"><span data-stu-id="d0306-151">20150801</span></span> |<span data-ttu-id="d0306-152">3</span><span class="sxs-lookup"><span data-stu-id="d0306-152">3</span></span> |<span data-ttu-id="d0306-153">1</span><span class="sxs-lookup"><span data-stu-id="d0306-153">1</span></span> |
| <span data-ttu-id="d0306-154">20150801</span><span class="sxs-lookup"><span data-stu-id="d0306-154">20150801</span></span> |<span data-ttu-id="d0306-155">3</span><span class="sxs-lookup"><span data-stu-id="d0306-155">3</span></span> |<span data-ttu-id="d0306-156">1</span><span class="sxs-lookup"><span data-stu-id="d0306-156">1</span></span> |
| <span data-ttu-id="d0306-157">20151001</span><span class="sxs-lookup"><span data-stu-id="d0306-157">20151001</span></span> |<span data-ttu-id="d0306-158">4</span><span class="sxs-lookup"><span data-stu-id="d0306-158">4</span></span> |<span data-ttu-id="d0306-159">2</span><span class="sxs-lookup"><span data-stu-id="d0306-159">2</span></span> |
| <span data-ttu-id="d0306-160">20151101</span><span class="sxs-lookup"><span data-stu-id="d0306-160">20151101</span></span> |<span data-ttu-id="d0306-161">4</span><span class="sxs-lookup"><span data-stu-id="d0306-161">4</span></span> |<span data-ttu-id="d0306-162">2</span><span class="sxs-lookup"><span data-stu-id="d0306-162">2</span></span> |
| <span data-ttu-id="d0306-163">20151201</span><span class="sxs-lookup"><span data-stu-id="d0306-163">20151201</span></span> |<span data-ttu-id="d0306-164">4</span><span class="sxs-lookup"><span data-stu-id="d0306-164">4</span></span> |<span data-ttu-id="d0306-165">2</span><span class="sxs-lookup"><span data-stu-id="d0306-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d0306-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0306-166">Next steps</span></span>
<span data-ttu-id="d0306-167">若要移轉 SQL Server 資料庫，請參閱 [SQL Server 資料庫移轉](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="d0306-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
