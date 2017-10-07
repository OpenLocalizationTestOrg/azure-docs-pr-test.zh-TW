---
title: "aaaConnect tooAzure SQL 資料倉儲 sqlcmd |Microsoft 文件"
description: "使用 [sqlcmd] [sqlcmd] 命令列公用程式 tooconnect tooand 查詢 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="4da29-103">使用 sqlcmd 連接 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="4da29-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4da29-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="4da29-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="4da29-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4da29-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="4da29-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4da29-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="4da29-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="4da29-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="4da29-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="4da29-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="4da29-109">使用[sqlcmd] [ sqlcmd]命令列公用程式 tooconnect tooand 查詢 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="4da29-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="4da29-110">1.連線</span><span class="sxs-lookup"><span data-stu-id="4da29-110">1. Connect</span></span>
<span data-ttu-id="4da29-111">tooget 入門[sqlcmd][sqlcmd]，開啟 hello 命令提示字元並輸入**sqlcmd**後面接著 hello SQL 資料倉儲資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4da29-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="4da29-112">hello 連接字串需要下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="4da29-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="4da29-113">**伺服器 (-S):**伺服器 hello 形式`<`伺服器名稱`>`。.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="4da29-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="4da29-114">**資料庫 (-d)：** 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="4da29-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="4da29-115">**啟用引號識別碼 (-I):**引號識別項必須是啟用的 tooconnect tooa SQL 資料倉儲執行個體。</span><span class="sxs-lookup"><span data-stu-id="4da29-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="4da29-116">toouse SQL Server 驗證，您需要 tooadd hello 使用者名稱/密碼參數：</span><span class="sxs-lookup"><span data-stu-id="4da29-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="4da29-117">**使用者 (-U):** hello 表單中的伺服器使用者`<`使用者`>`</span><span class="sxs-lookup"><span data-stu-id="4da29-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="4da29-118">**密碼 (-P):** hello 使用者相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="4da29-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="4da29-119">例如，您的連接字串可能會看起來像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4da29-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="4da29-120">toouse Azure Active Directory 整合式驗證，您需要 tooadd hello Azure Active Directory 參數：</span><span class="sxs-lookup"><span data-stu-id="4da29-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="4da29-121">**Azure Active Directory 驗證 (-G)：** 使用 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="4da29-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="4da29-122">例如，您的連接字串可能會看起來像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4da29-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="4da29-123">您需要[啟用 Azure Active Directory 驗證](sql-data-warehouse-authentication.md)tooauthenticate 使用 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="4da29-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="4da29-124">2.查詢</span><span class="sxs-lookup"><span data-stu-id="4da29-124">2. Query</span></span>
<span data-ttu-id="4da29-125">連線之後，您可以發出任何支援的 TRANSACT-SQL 陳述式，針對 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4da29-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="4da29-126">此範例會在互動模式中提交查詢。</span><span class="sxs-lookup"><span data-stu-id="4da29-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="4da29-127">這些下面的範例會示範如何使用 hello-Q 選項或以管線傳送 SQL toosqlcmd 批次模式來執行您的查詢。</span><span class="sxs-lookup"><span data-stu-id="4da29-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="4da29-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4da29-128">Next steps</span></span>
<span data-ttu-id="4da29-129">請參閱[sqlcmd 文件][ sqlcmd]如需詳細資訊在 sqlcmd 中可用的 hello 選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4da29-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
