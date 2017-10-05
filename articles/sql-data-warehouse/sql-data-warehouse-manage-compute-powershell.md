---
title: "管理 Azure SQL 資料倉儲中的計算能力 (PowerShell) | Microsoft Docs"
description: "管理計算能力的 PowerShell 工作。 透過調整 DWU 以調整計算資源。 或者，暫停和繼續計算資源以節省成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="46221-105">管理 Azure SQL 資料倉儲中的計算能力 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="46221-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46221-106">概觀</span><span class="sxs-lookup"><span data-stu-id="46221-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="46221-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="46221-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="46221-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46221-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="46221-109">REST</span><span class="sxs-lookup"><span data-stu-id="46221-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="46221-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="46221-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="46221-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="46221-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="46221-112">安裝最新版的 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46221-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="46221-113">若要搭配使用 Azure Powershell 與 SQL 資料倉儲，需要有 Azure PowerShell 1.0.3 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="46221-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="46221-114">若要確認目前的版本，請執行命令 **Get-Module -ListAvailable -Name Azure**。</span><span class="sxs-lookup"><span data-stu-id="46221-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="46221-115">您可以從 [Microsoft Web Platform Installer][Microsoft Web Platform Installer] 安裝最新的版本。</span><span class="sxs-lookup"><span data-stu-id="46221-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="46221-116">如需詳細資訊，請參閱[如何安裝和設定 Azure PowerShell][How to install and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="46221-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="46221-117">開始使用 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="46221-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="46221-118">開始進行之前：</span><span class="sxs-lookup"><span data-stu-id="46221-118">To get started:</span></span>

1. <span data-ttu-id="46221-119">開啟 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="46221-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="46221-120">在 PowerShell 提示中，執行下列命令來登入 Azure Resource Manager，並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="46221-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="46221-121">調整計算能力</span><span class="sxs-lookup"><span data-stu-id="46221-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="46221-122">若要變更 DWU，請使用 [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="46221-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="46221-123">下例會將裝載在 MyServer 伺服器上的資料庫 MySQLDW 的服務等級目標設定為 DW1000。</span><span class="sxs-lookup"><span data-stu-id="46221-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="46221-124">暫停計算</span><span class="sxs-lookup"><span data-stu-id="46221-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="46221-125">若要暫停資料庫，請使用 [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="46221-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="46221-126">下例會暫停裝載在 Server01 伺服器上的 Database02 資料庫。</span><span class="sxs-lookup"><span data-stu-id="46221-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="46221-127">此伺服器位於 ResourceGroup1 這個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="46221-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="46221-128">請注意，如果您的伺服器是 foo.database.windows.net，請使用 "foo" 作為 PowerShell Cmdlet 中的 -ServerName。</span><span class="sxs-lookup"><span data-stu-id="46221-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="46221-129">一種變異，這個範例會將資料庫擷取至 $database 物件。</span><span class="sxs-lookup"><span data-stu-id="46221-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="46221-130">然後將物件輸送到 [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]。</span><span class="sxs-lookup"><span data-stu-id="46221-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="46221-131">結果會儲存在物件 resultDatabase 中。</span><span class="sxs-lookup"><span data-stu-id="46221-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="46221-132">最終的命令會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="46221-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="46221-133">繼續計算</span><span class="sxs-lookup"><span data-stu-id="46221-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="46221-134">若要啟動資料庫，請使用 [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="46221-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="46221-135">下例會啟動裝載在 Server01 伺服器上的 Database02 資料庫。</span><span class="sxs-lookup"><span data-stu-id="46221-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="46221-136">此伺服器位於 ResourceGroup1 這個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="46221-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="46221-137">一種變異，這個範例會將資料庫擷取至 $database 物件。</span><span class="sxs-lookup"><span data-stu-id="46221-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="46221-138">接著將物件輸送到 [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]，並將結果儲存在 $resultDatabase 中。</span><span class="sxs-lookup"><span data-stu-id="46221-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="46221-139">最終的命令會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="46221-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="46221-140">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="46221-140">Check database state</span></span>

<span data-ttu-id="46221-141">如上述範例所示，您可以使用 [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] Cmdlet 來取得資料庫的相關資訊，藉此檢查狀態，但也可以用來作為引數。</span><span class="sxs-lookup"><span data-stu-id="46221-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="46221-142">這會導致如以下的結果</span><span class="sxs-lookup"><span data-stu-id="46221-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="46221-143">其中您可以接著查看資料庫的「狀態」。</span><span class="sxs-lookup"><span data-stu-id="46221-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="46221-144">在此情況下，您會看到此資料庫已上線。</span><span class="sxs-lookup"><span data-stu-id="46221-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="46221-145">當您執行此命令時，應該會收到下列其中一個 Status (狀態) 值：Online (上線)、Pausing (暫停中)、Resuming (正在恢復)、Scaling (正在調整) 及 Paused (已暫停)。</span><span class="sxs-lookup"><span data-stu-id="46221-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="46221-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46221-146">Next steps</span></span>
<span data-ttu-id="46221-147">如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="46221-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
