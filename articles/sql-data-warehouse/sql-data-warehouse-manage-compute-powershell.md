---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 (PowerShell) |Microsoft 文件"
description: "PowerShell 工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。"
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
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="93be4-105">管理 Azure SQL 資料倉儲中的計算能力 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="93be4-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93be4-106">概觀</span><span class="sxs-lookup"><span data-stu-id="93be4-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="93be4-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="93be4-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="93be4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93be4-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="93be4-109">REST</span><span class="sxs-lookup"><span data-stu-id="93be4-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="93be4-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="93be4-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="93be4-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="93be4-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="93be4-112">安裝 Azure PowerShell hello 最新版本</span><span class="sxs-lookup"><span data-stu-id="93be4-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="93be4-113">toouse 向 SQL 資料倉儲的 Azure PowerShell，您需要 Azure PowerShell 1.0.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="93be4-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="93be4-114">tooverify 您目前的版本執行 hello 命令**Get-module-ListAvailable-Name Azure**。</span><span class="sxs-lookup"><span data-stu-id="93be4-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="93be4-115">您可以安裝來自 hello 最新版本[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。</span><span class="sxs-lookup"><span data-stu-id="93be4-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="93be4-116">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="93be4-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="93be4-117">開始使用 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="93be4-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="93be4-118">tooget 啟動：</span><span class="sxs-lookup"><span data-stu-id="93be4-118">tooget started:</span></span>

1. <span data-ttu-id="93be4-119">開啟 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="93be4-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="93be4-120">Hello PowerShell 命令提示字元，執行這些命令 toosign toohello Azure 資源管理員中，選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="93be4-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="93be4-121">調整計算能力</span><span class="sxs-lookup"><span data-stu-id="93be4-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="93be4-122">toochange hello Dwu，使用 hello[組 AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="93be4-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="93be4-123">hello 下列範例會設定 hello 服務等級目標 tooDW1000 hello 資料庫裝載 MySQLDW MyServer 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="93be4-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="93be4-124">暫停計算</span><span class="sxs-lookup"><span data-stu-id="93be4-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="93be4-125">toopause 資料庫中，使用 hello[暫停 AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet。</span><span class="sxs-lookup"><span data-stu-id="93be4-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="93be4-126">hello 下列範例會暫停名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="93be4-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="93be4-127">hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。</span><span class="sxs-lookup"><span data-stu-id="93be4-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="93be4-128">請注意，如果您的伺服器是 foo.database.windows.net，做為"foo"hello-ServerName hello PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="93be4-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="93be4-129">一種變化中下, 一個範例會將擷取 hello 資料庫到 hello $database 物件。</span><span class="sxs-lookup"><span data-stu-id="93be4-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="93be4-130">它接著會使用管線傳送 hello 物件太[暫停 AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]。</span><span class="sxs-lookup"><span data-stu-id="93be4-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="93be4-131">hello 結果會儲存在 hello 物件 resultDatabase。</span><span class="sxs-lookup"><span data-stu-id="93be4-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="93be4-132">hello 最後一個命令會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="93be4-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="93be4-133">繼續計算</span><span class="sxs-lookup"><span data-stu-id="93be4-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="93be4-134">toostart 資料庫中，使用 hello[繼續 AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet。</span><span class="sxs-lookup"><span data-stu-id="93be4-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="93be4-135">hello 下列範例會啟動名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="93be4-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="93be4-136">hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。</span><span class="sxs-lookup"><span data-stu-id="93be4-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="93be4-137">一種變化中下, 一個範例會將擷取 hello 資料庫到 hello $database 物件。</span><span class="sxs-lookup"><span data-stu-id="93be4-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="93be4-138">它接著會使用管線傳送 hello 物件太[繼續 AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase]並儲存在 $resultDatabase hello 結果。</span><span class="sxs-lookup"><span data-stu-id="93be4-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="93be4-139">hello 最後一個命令會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="93be4-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="93be4-140">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="93be4-140">Check database state</span></span>

<span data-ttu-id="93be4-141">Hello，上述範例所示，您可以使用[Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget 資訊在資料庫上，藉此檢查 hello 狀態，但也 toouse 做為引數。</span><span class="sxs-lookup"><span data-stu-id="93be4-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="93be4-142">這會導致如以下的結果</span><span class="sxs-lookup"><span data-stu-id="93be4-142">Which will result in something like</span></span> 

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

<span data-ttu-id="93be4-143">可以再檢查 toosee hello*狀態*的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="93be4-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="93be4-144">在此情況下，您會看到此資料庫已上線。</span><span class="sxs-lookup"><span data-stu-id="93be4-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="93be4-145">當您執行此命令時，應該會收到下列其中一個 Status (狀態) 值：Online (上線)、Pausing (暫停中)、Resuming (正在恢復)、Scaling (正在調整) 及 Paused (已暫停)。</span><span class="sxs-lookup"><span data-stu-id="93be4-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="93be4-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93be4-146">Next steps</span></span>
<span data-ttu-id="93be4-147">如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="93be4-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
