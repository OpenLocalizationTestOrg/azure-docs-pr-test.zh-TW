---
title: "aaaCreate SQL 資料倉儲與 TSQL |Microsoft 文件"
description: "了解如何 toocreate Azure SQL 資料倉儲與 TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="8e46d-103">使用 Transact-SQL (TSQL) 建立 SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="8e46d-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e46d-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8e46d-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="8e46d-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="8e46d-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="8e46d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e46d-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="8e46d-107">本文章將示範如何 toocreate SQL 資料倉儲使用 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="8e46d-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e46d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="8e46d-108">Prerequisites</span></span>
<span data-ttu-id="8e46d-109">tooget 開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="8e46d-109">tooget started, you need:</span></span>

* <span data-ttu-id="8e46d-110">**Azure 帳戶**： 瀏覽[Azure 免費試用][ Azure Free Trial]或[MSDN Azure 信用額度][ MSDN Azure Credits] toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e46d-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="8e46d-111">**Azure SQL server**： 請參閱 [建立 hello Azure 入口網站的 Azure SQL Database 邏輯伺服器] [以 hello Azure 入口網站建立 Azure SQL Database 邏輯伺服器] 或 [使用 PowerShell 建立 Azure SQL Database 邏輯伺服器] [建立 Azure SQL使用 PowerShell 邏輯伺服器的資料庫] 如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8e46d-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="8e46d-112">**資源群組**： 請使用相同的資源與您的 Azure SQL server 群組，或參閱的 hello[如何 toocreate 資源群組][how toocreate a resource group]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="8e46d-113">**環境 tooexecute T-SQL**： 您可以使用[Visual Studio][Installing Visual Studio and SSDT]， [sqlcmd][sqlcmd]，或[SSMS][ SSMS] tooexecute T-SQL。</span><span class="sxs-lookup"><span data-stu-id="8e46d-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="8e46d-114">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="8e46d-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="8e46d-115">如需價格的詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="8e46d-116">使用 Visual Studio 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="8e46d-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="8e46d-117">如果您是新 tooVisual Studio，請參閱 hello 文章[查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="8e46d-118">toostart，Visual Studio 中開啟 SQL Server 物件總管，並將裝載 SQL 資料倉儲資料庫 toohello 伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="8e46d-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="8e46d-119">一旦連接之後，您可以建立 SQL 資料倉儲由執行下列 SQL 命令，針對 hello hello**主要**資料庫。</span><span class="sxs-lookup"><span data-stu-id="8e46d-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="8e46d-120">此命令會建立 hello 資料庫 MySqlDwDb DW400 服務目標，並允許 hello 資料庫 toogrow tooa 最大大小的 10 TB。</span><span class="sxs-lookup"><span data-stu-id="8e46d-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="8e46d-121">使用 sqlcmd 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="8e46d-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="8e46d-122">或者，您可以執行下列的命令提示字元的同一個命令使用 sqlcmd 執行 hello 的 hello。</span><span class="sxs-lookup"><span data-stu-id="8e46d-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="8e46d-123">hello 預設定序時未指定為定序 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="8e46d-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="8e46d-124">hello`MAXSIZE`可以是 250 GB 到 240 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="8e46d-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="8e46d-125">hello`SERVICE_OBJECTIVE`可介於 DW100 到 DW2000 [DWU][DWU]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="8e46d-126">如需所有有效的值的清單，請參閱 hello MSDN 文件[CREATE DATABASE][CREATE DATABASE]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="8e46d-127">Hello MAXSIZE 和 SERVICE_OBJECTIVE 來將其變更與[ALTER DATABASE] [ ALTER DATABASE] T-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="8e46d-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="8e46d-128">建立之後就無法變更資料庫定序 hello。</span><span class="sxs-lookup"><span data-stu-id="8e46d-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="8e46d-129">變更為變更 DWU hello service_objective，將會導致重新啟動服務，這樣會取消航班中的所有查詢時，應注意。</span><span class="sxs-lookup"><span data-stu-id="8e46d-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="8e46d-130">變更 MAXSIZE 並不會重新啟動服務，因為這只是簡單的中繼資料作業。</span><span class="sxs-lookup"><span data-stu-id="8e46d-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e46d-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e46d-131">Next steps</span></span>
<span data-ttu-id="8e46d-132">您可以佈建完成您的 SQL 資料倉儲後[範例資料載入][ load sample data]或太簽出如何[開發][develop]， [載入][load]，或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="8e46d-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
