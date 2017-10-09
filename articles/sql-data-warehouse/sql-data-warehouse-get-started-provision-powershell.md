---
title: "使用 PowerShell aaaCreate SQL 資料倉儲 |Microsoft 文件"
description: "使用 PowerShell 建立 SQL 資料倉儲"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="3a084-103">使用 PowerShell 建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3a084-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a084-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3a084-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="3a084-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="3a084-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="3a084-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a084-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="3a084-107">本文章將示範如何 toocreate SQL 資料倉儲使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3a084-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a084-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="3a084-108">Prerequisites</span></span>
<span data-ttu-id="3a084-109">tooget 開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="3a084-109">tooget started, you need:</span></span>

* <span data-ttu-id="3a084-110">**Azure 帳戶**： 瀏覽[Azure 免費試用][ Azure Free Trial]或[MSDN Azure 信用額度][ MSDN Azure Credits] toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a084-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="3a084-111">**Azure SQL server**： 請參閱[hello Azure 入口網站中建立 Azure SQL database] [ Create an Azure SQL database in hello Azure Portal]或[使用 PowerShell 建立 Azure SQL database] [Create an Azure SQL database with PowerShell]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3a084-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="3a084-112">**資源群組**： 請使用相同的資源與您的 Azure SQL server 群組，或參閱的 hello[如何 toocreate 資源群組](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3a084-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="3a084-113">**PowerShell 1.0.3 版或更新版本**：您可以執行 **Get-Module -ListAvailable -Name Azure** 來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="3a084-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="3a084-114">hello 最新版本可以從安裝[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。</span><span class="sxs-lookup"><span data-stu-id="3a084-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="3a084-115">如需有關如何安裝 hello 最新版本的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="3a084-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="3a084-116">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="3a084-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="3a084-117">如需價格的詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="3a084-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="3a084-118">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3a084-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="3a084-119">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3a084-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="3a084-120">執行這個指令程式 toologin tooAzure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="3a084-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="3a084-121">選取您想 toouse 目前工作階段的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a084-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="3a084-122">建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="3a084-122">Create database.</span></span> <span data-ttu-id="3a084-123">這個範例會建立名為"mynewsqldw"，服務目標等級 」 DW400"，toohello 伺服器名為"sqldwserver1"，這是在名為"mywesteuroperesgp1"hello 資源群組中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3a084-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="3a084-124">必要參數如下：</span><span class="sxs-lookup"><span data-stu-id="3a084-124">Required Parameters are:</span></span>

* <span data-ttu-id="3a084-125">**RequestedServiceObjectiveName**: hello 數量[DWU] [ DWU]您要求。</span><span class="sxs-lookup"><span data-stu-id="3a084-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="3a084-126">支援的值為︰DW100、DW200、DW300、DW400、DW500、DW600、DW1000、DW1200、DW1500、DW2000、DW3000 和 DW6000。</span><span class="sxs-lookup"><span data-stu-id="3a084-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="3a084-127">**DatabaseName**: hello 的 hello 您所建立的 SQL 資料倉儲的名稱。</span><span class="sxs-lookup"><span data-stu-id="3a084-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="3a084-128">**ServerName**: hello 伺服器用來建立 hello 名稱 （必須是 V12）。</span><span class="sxs-lookup"><span data-stu-id="3a084-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="3a084-129">**ResourceGroupName**：您使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a084-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="3a084-130">toofind 可用的資源群組，您的訂用帳戶中使用 Get AzureResource。</span><span class="sxs-lookup"><span data-stu-id="3a084-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="3a084-131">**Edition**： 必須是 「 資料倉儲"toocreate SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3a084-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="3a084-132">選擇性參數如下：</span><span class="sxs-lookup"><span data-stu-id="3a084-132">Optional Parameters are:</span></span>

* <span data-ttu-id="3a084-133">**CollationName**： 如果未指定的 hello 預設定序為 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="3a084-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="3a084-134">無法變更資料庫的定序。</span><span class="sxs-lookup"><span data-stu-id="3a084-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="3a084-135">**MaxSizeBytes**: hello 資料庫的預設最大大小為 10 GB。</span><span class="sxs-lookup"><span data-stu-id="3a084-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="3a084-136">如需有關 hello 參數選項的詳細資訊，請參閱[新增 AzureRmSqlDatabase] [ New-AzureRmSqlDatabase]和[Create Database （Azure SQL 資料倉儲）][Create Database (Azure SQL Data Warehouse)]。</span><span class="sxs-lookup"><span data-stu-id="3a084-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a084-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a084-137">Next steps</span></span>
<span data-ttu-id="3a084-138">完成您的 SQL 資料倉儲之後佈建您可能會想 tootry[範例資料載入][ loading sample data]或太簽出如何[開發][ develop][載入][load]，或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="3a084-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="3a084-139">如果您想要更多有關 toomanage SQL 資料倉儲以程式設計的方式，查看我們的文件如何 toouse [PowerShell cmdlet 和 REST Api][PowerShell cmdlets and REST APIs]。</span><span class="sxs-lookup"><span data-stu-id="3a084-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
