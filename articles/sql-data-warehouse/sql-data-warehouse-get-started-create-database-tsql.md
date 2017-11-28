---
title: "使用 TSQL 建立 SQL 資料倉儲 | Microsoft Docs"
description: "了解如何使用 TSQL 建立 Azure SQL 資料倉儲"
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
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="27fc5-103">使用 Transact-SQL (TSQL) 建立 SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="27fc5-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27fc5-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="27fc5-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="27fc5-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="27fc5-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="27fc5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27fc5-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="27fc5-107">本文說明如何使用 T-SQL 建立 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="27fc5-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27fc5-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="27fc5-108">Prerequisites</span></span>
<span data-ttu-id="27fc5-109">若要開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="27fc5-109">To get started, you need:</span></span>

* <span data-ttu-id="27fc5-110">**Azure 帳戶**︰請瀏覽 [Azure 免費試用][Azure Free Trial]或 [MSDN Azure 點數][MSDN Azure Credits]以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="27fc5-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="27fc5-111">**Azure SQL server**： 請參閱 [透過 Azure 入口網站建立 Azure SQL Database 邏輯伺服器] [透過 Azure 入口網站建立 Azure SQL Database 邏輯伺服器] 或 [使用 PowerShell 建立 Azure SQL Database 邏輯伺服器] [建立 Azure SQL使用 PowerShell 邏輯伺服器的資料庫] 如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="27fc5-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="27fc5-112">**資源群組**︰使用與 Azure SQL Server 相同的資源群組，或參閱[如何建立資源群組][how to create a resource group]。</span><span class="sxs-lookup"><span data-stu-id="27fc5-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="27fc5-113">**執行 T-SQL 的環境**︰您可以使用 [Visual Studio][Installing Visual Studio and SSDT]、[sqlcmd][sqlcmd] 或 [SSMS][SSMS] 執行 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="27fc5-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="27fc5-114">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="27fc5-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="27fc5-115">如需價格的詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="27fc5-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="27fc5-116">使用 Visual Studio 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="27fc5-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="27fc5-117">如果您不熟悉 Visual Studio，請參閱[查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)] 一文。</span><span class="sxs-lookup"><span data-stu-id="27fc5-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="27fc5-118">若要開始，請在 Visual Studio 中開啟 SQL Server 物件總管，並連接到將要裝載 SQL 資料倉儲資料庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="27fc5-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="27fc5-119">連接後，您即可對 **master** 資料庫執行下列 SQL 命令來建立 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="27fc5-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="27fc5-120">此命令會建立服務目標為 DW400 的資料庫 MySqlDwDb，並允許此資料庫成長至大小上限 10 TB。</span><span class="sxs-lookup"><span data-stu-id="27fc5-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="27fc5-121">使用 sqlcmd 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="27fc5-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="27fc5-122">或者，您可以在命令提示字元執行下列命令，以使用 sqlcmd 執行相同的命令。</span><span class="sxs-lookup"><span data-stu-id="27fc5-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="27fc5-123">未指定定序時的預設值為 COLLATE SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="27fc5-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="27fc5-124">`MAXSIZE` 可以介於 250 GB 與 240 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="27fc5-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="27fc5-125">`SERVICE_OBJECTIVE` 可以介於 DW100 與 DW2000 [DWU][DWU] 之間。</span><span class="sxs-lookup"><span data-stu-id="27fc5-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="27fc5-126">如需所有有效值的清單，請參閱 MSDN 文件中的 [CREATE DATABASE][CREATE DATABASE]。</span><span class="sxs-lookup"><span data-stu-id="27fc5-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="27fc5-127">使用 [ALTER DATABASE][ALTER DATABASE] T-SQL 命令可以變更 MAXSIZE 和 SERVICE_OBJECTIVE。</span><span class="sxs-lookup"><span data-stu-id="27fc5-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="27fc5-128">建立資料庫定序之後，就無法進行變更。</span><span class="sxs-lookup"><span data-stu-id="27fc5-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="27fc5-129">變更 SERVICE_OBJECTIVE 時應格外小心，因為變更 DWU 會導致服務重新啟動，而取消所有進行中的查詢。</span><span class="sxs-lookup"><span data-stu-id="27fc5-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="27fc5-130">變更 MAXSIZE 並不會重新啟動服務，因為這只是簡單的中繼資料作業。</span><span class="sxs-lookup"><span data-stu-id="27fc5-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27fc5-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27fc5-131">Next steps</span></span>
<span data-ttu-id="27fc5-132">您的 SQL 資料倉儲完成佈建之後，您可以[載入範例資料][load sample data]或查看如何[開發][develop]、[載入][load]，或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="27fc5-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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
