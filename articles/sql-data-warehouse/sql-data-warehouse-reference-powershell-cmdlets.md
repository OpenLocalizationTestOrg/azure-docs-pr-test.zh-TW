---
title: "Azure SQL 資料倉儲的 aaaPowerShell cmdlet"
description: "尋找 Azure SQL 資料倉儲 hello 最上層的 PowerShell 指令程式包括如何 toopause 和繼續資料庫。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="dfcdc-103">適用於 SQL 資料倉儲的 PowerShell Cmdlet 和 REST API</span><span class="sxs-lookup"><span data-stu-id="dfcdc-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="dfcdc-104">您可使用 Azure PowerShell Cmdlet 或 REST API 管理許多 SQL 資料倉儲系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="dfcdc-105">以下是如何 toouse PowerShell 命令 tooautomate 您的 SQL 資料倉儲中的一般工作的一些範例。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="dfcdc-106">某些良好的其他範例，請參閱 hello 文章[管理與其餘的延展性][Manage scalability with REST]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="dfcdc-107">順序 toouse 向 SQL 資料倉儲的 Azure PowerShell，在中，您需要 Azure PowerShell 1.0.3 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="dfcdc-108">您可以執行 **Get-Module -ListAvailable -Name Azure**來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="dfcdc-109">hello 最新版本可以從安裝[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="dfcdc-110">如需有關如何安裝 hello 最新版本的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="dfcdc-111">開始使用 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="dfcdc-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="dfcdc-112">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="dfcdc-113">Hello PowerShell 命令提示字元，執行這些命令 toosign toohello Azure 資源管理員中，選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="dfcdc-114">暫停 SQL 資料倉儲範例</span><span class="sxs-lookup"><span data-stu-id="dfcdc-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="dfcdc-115">暫停 "Server01" 伺服器上託管的 "Database02" 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="dfcdc-116">hello 伺服器是在名為"ResourceGroup1。 「 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="dfcdc-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="dfcdc-117">一種變化中，此範例會使用管線傳送 hello 擷取物件太[暫停 AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="dfcdc-118">如此一來，hello 資料庫已暫停。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-118">As a result, hello database is paused.</span></span> <span data-ttu-id="dfcdc-119">hello 最後一個命令會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="dfcdc-120">啟動 SQL 資料倉儲範例</span><span class="sxs-lookup"><span data-stu-id="dfcdc-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="dfcdc-121">繼續 "Server01" 伺服器上託管之 "Database02" 資料庫的作業。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="dfcdc-122">hello 伺服器包含在資源群組中名為"ResourceGroup1。 」</span><span class="sxs-lookup"><span data-stu-id="dfcdc-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="dfcdc-123">一種變化，此範例會從 "ResourceGroup1" 資源群組包含的 "Server01" 伺服器中，擷取 "Database02" 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="dfcdc-124">它使用管線傳送 hello 擷取物件太[繼續 AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="dfcdc-125">請注意，如果您的伺服器是 foo.database.windows.net，做為"foo"hello-ServerName hello PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="dfcdc-126">其他支援的 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="dfcdc-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="dfcdc-127">這些 PowerShell Cmdlet 皆由 Azure SQL 資料倉儲所支援。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="dfcdc-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="dfcdc-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="dfcdc-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="dfcdc-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="dfcdc-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfcdc-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfcdc-138">Next steps</span></span>
<span data-ttu-id="dfcdc-139">如需更多 PowerShell 範例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dfcdc-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="dfcdc-140">[使用 PowerShell 建立 SQL 資料倉儲][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="dfcdc-141">[資料庫還原][Database restore]</span><span class="sxs-lookup"><span data-stu-id="dfcdc-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="dfcdc-142">如需可以使用 PowerShell 進行自動化的其他工作，請參閱 [Azure SQL Database Cmdlet][Azure SQL Database Cmdlets]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="dfcdc-143">請注意，Azure SQL 資料倉儲並沒有支援所有的 Azure SQL Database Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="dfcdc-144">如需可以使用 REST 來自動化的工作清單，請參閱 [Azure SQL Database 的作業][Operations for Azure SQL Databases]。</span><span class="sxs-lookup"><span data-stu-id="dfcdc-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
