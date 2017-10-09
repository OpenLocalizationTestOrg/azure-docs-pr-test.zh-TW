---
title: "從 CSV aaaLoad 資料檔案儲存到 Azure SQL Database (bcp) |Microsoft 文件"
description: "若是較小的資料大小，會使用 bcp tooimport 資料至 Azure SQL Database。"
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="dbec8-103">將資料從 CSV 載入 Azure SQL Database (一般檔案)</span><span class="sxs-lookup"><span data-stu-id="dbec8-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="dbec8-104">您可以使用從 CSV 檔案的 hello bcp 命令列公用程式 tooimport 資料至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="dbec8-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dbec8-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="dbec8-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="dbec8-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="dbec8-106">Prerequisites</span></span>
<span data-ttu-id="dbec8-107">toocomplete hello 步驟在本文中，您需要：</span><span class="sxs-lookup"><span data-stu-id="dbec8-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="dbec8-108">Azure SQL Database 邏輯伺服器和資料庫</span><span class="sxs-lookup"><span data-stu-id="dbec8-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="dbec8-109">hello bcp 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="dbec8-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="dbec8-110">hello sqlcmd 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="dbec8-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="dbec8-111">您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。</span><span class="sxs-lookup"><span data-stu-id="dbec8-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="dbec8-112">ASCII 或 UTF-16 格式的資料</span><span class="sxs-lookup"><span data-stu-id="dbec8-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="dbec8-113">如果您嘗試本教學課程使用您自己的資料，您的資料需要 toouse hello ASCII 或因為 bcp 不支援 utf-8，utf-16 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="dbec8-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="dbec8-114">1.建立目的資料表</span><span class="sxs-lookup"><span data-stu-id="dbec8-114">1. Create a destination table</span></span>
<span data-ttu-id="dbec8-115">SQL Database 中的資料表定義為 hello 目的地資料表中。</span><span class="sxs-lookup"><span data-stu-id="dbec8-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="dbec8-116">hello hello 資料表中的資料行必須對應 toohello 每一個資料列的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="dbec8-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="dbec8-117">toocreate 資料表中，開啟命令提示字元，並使用 sqlcmd.exe toorun hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="dbec8-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="dbec8-118">2.建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="dbec8-118">2. Create a source data file</span></span>
<span data-ttu-id="dbec8-119">開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="dbec8-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="dbec8-120">此資料是 ASCII 格式。</span><span class="sxs-lookup"><span data-stu-id="dbec8-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="dbec8-121">（選擇性） tooexport 您自己的資料從 SQL Server 資料庫，開啟命令提示字元並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="dbec8-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="dbec8-122">使用您自己的資訊取代 TableName、ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="dbec8-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="dbec8-123">3.將資料載入 hello</span><span class="sxs-lookup"><span data-stu-id="dbec8-123">3. Load hello data</span></span>
<span data-ttu-id="dbec8-124">tooload hello 資料，開啟命令提示字元，並執行下列命令，為伺服器名稱、 資料庫名稱、 使用者名稱和密碼的 hello 值取代您自己的資訊 hello。</span><span class="sxs-lookup"><span data-stu-id="dbec8-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="dbec8-125">使用此資料已載入正確的命令 tooverify hello</span><span class="sxs-lookup"><span data-stu-id="dbec8-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="dbec8-126">hello 結果看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="dbec8-126">hello results should look like this:</span></span>

| <span data-ttu-id="dbec8-127">DateId</span><span class="sxs-lookup"><span data-stu-id="dbec8-127">DateId</span></span> | <span data-ttu-id="dbec8-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="dbec8-128">CalendarQuarter</span></span> | <span data-ttu-id="dbec8-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="dbec8-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbec8-130">20150101</span><span class="sxs-lookup"><span data-stu-id="dbec8-130">20150101</span></span> |<span data-ttu-id="dbec8-131">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-131">1</span></span> |<span data-ttu-id="dbec8-132">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-132">3</span></span> |
| <span data-ttu-id="dbec8-133">20150201</span><span class="sxs-lookup"><span data-stu-id="dbec8-133">20150201</span></span> |<span data-ttu-id="dbec8-134">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-134">1</span></span> |<span data-ttu-id="dbec8-135">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-135">3</span></span> |
| <span data-ttu-id="dbec8-136">20150301</span><span class="sxs-lookup"><span data-stu-id="dbec8-136">20150301</span></span> |<span data-ttu-id="dbec8-137">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-137">1</span></span> |<span data-ttu-id="dbec8-138">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-138">3</span></span> |
| <span data-ttu-id="dbec8-139">20150401</span><span class="sxs-lookup"><span data-stu-id="dbec8-139">20150401</span></span> |<span data-ttu-id="dbec8-140">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-140">2</span></span> |<span data-ttu-id="dbec8-141">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-141">4</span></span> |
| <span data-ttu-id="dbec8-142">20150501</span><span class="sxs-lookup"><span data-stu-id="dbec8-142">20150501</span></span> |<span data-ttu-id="dbec8-143">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-143">2</span></span> |<span data-ttu-id="dbec8-144">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-144">4</span></span> |
| <span data-ttu-id="dbec8-145">20150601</span><span class="sxs-lookup"><span data-stu-id="dbec8-145">20150601</span></span> |<span data-ttu-id="dbec8-146">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-146">2</span></span> |<span data-ttu-id="dbec8-147">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-147">4</span></span> |
| <span data-ttu-id="dbec8-148">20150701</span><span class="sxs-lookup"><span data-stu-id="dbec8-148">20150701</span></span> |<span data-ttu-id="dbec8-149">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-149">3</span></span> |<span data-ttu-id="dbec8-150">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-150">1</span></span> |
| <span data-ttu-id="dbec8-151">20150801</span><span class="sxs-lookup"><span data-stu-id="dbec8-151">20150801</span></span> |<span data-ttu-id="dbec8-152">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-152">3</span></span> |<span data-ttu-id="dbec8-153">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-153">1</span></span> |
| <span data-ttu-id="dbec8-154">20150801</span><span class="sxs-lookup"><span data-stu-id="dbec8-154">20150801</span></span> |<span data-ttu-id="dbec8-155">3</span><span class="sxs-lookup"><span data-stu-id="dbec8-155">3</span></span> |<span data-ttu-id="dbec8-156">1</span><span class="sxs-lookup"><span data-stu-id="dbec8-156">1</span></span> |
| <span data-ttu-id="dbec8-157">20151001</span><span class="sxs-lookup"><span data-stu-id="dbec8-157">20151001</span></span> |<span data-ttu-id="dbec8-158">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-158">4</span></span> |<span data-ttu-id="dbec8-159">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-159">2</span></span> |
| <span data-ttu-id="dbec8-160">20151101</span><span class="sxs-lookup"><span data-stu-id="dbec8-160">20151101</span></span> |<span data-ttu-id="dbec8-161">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-161">4</span></span> |<span data-ttu-id="dbec8-162">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-162">2</span></span> |
| <span data-ttu-id="dbec8-163">20151201</span><span class="sxs-lookup"><span data-stu-id="dbec8-163">20151201</span></span> |<span data-ttu-id="dbec8-164">4</span><span class="sxs-lookup"><span data-stu-id="dbec8-164">4</span></span> |<span data-ttu-id="dbec8-165">2</span><span class="sxs-lookup"><span data-stu-id="dbec8-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dbec8-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dbec8-166">Next steps</span></span>
<span data-ttu-id="dbec8-167">toomigrate SQL Server 資料庫，請參閱[SQL Server 資料庫移轉](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="dbec8-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
