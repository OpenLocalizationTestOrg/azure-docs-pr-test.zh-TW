---
title: "使用 PowerShell 建立 SQL 資料倉儲 | Microsoft Docs"
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
ms.openlocfilehash: a763f1c600c1a3f37cb565a8eb7db3c3f27dcf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="2b30b-103">使用 PowerShell 建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="2b30b-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b30b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2b30b-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="2b30b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="2b30b-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="2b30b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b30b-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="2b30b-107">本文說明如何使用 PowerShell 建立 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2b30b-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b30b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b30b-108">Prerequisites</span></span>
<span data-ttu-id="2b30b-109">若要開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="2b30b-109">To get started, you need:</span></span>

* <span data-ttu-id="2b30b-110">**Azure 帳戶**︰請瀏覽 [Azure 免費試用][Azure Free Trial]或 [MSDN Azure 點數][MSDN Azure Credits]以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b30b-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="2b30b-111">**Azure SQL Server**︰如需詳細資訊，請參閱[在 Azure 入口網站中建立 Azure SQL Database][Create an Azure SQL database in the Azure Portal] 或[使用 PowerShell 建立 Azure SQL Database][Create an Azure SQL database with PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="2b30b-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="2b30b-112">**資源群組**︰使用與 Azure SQL Server 相同的資源群組，或參閱 [如何建立資源群組](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2b30b-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="2b30b-113">**PowerShell 1.0.3 版或更新版本**：您可以執行 **Get-Module -ListAvailable -Name Azure** 來檢查您的版本。</span><span class="sxs-lookup"><span data-stu-id="2b30b-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="2b30b-114">可透過 [Microsoft Web Platform Installer][Microsoft Web Platform Installer]安裝最新的版本。</span><span class="sxs-lookup"><span data-stu-id="2b30b-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="2b30b-115">如需安裝最新版本的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell][How to install and configure Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="2b30b-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="2b30b-116">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="2b30b-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="2b30b-117">如需價格的詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="2b30b-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="2b30b-118">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="2b30b-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="2b30b-119">開啟 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2b30b-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="2b30b-120">執行此 Cmdlet 來登入 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="2b30b-120">Run this cmdlet to login to Azure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="2b30b-121">選取目前的工作階段要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b30b-121">Select the subscription you want to use for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="2b30b-122">建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="2b30b-122">Create database.</span></span> <span data-ttu-id="2b30b-123">這個範例會使用服務目標等級 "DW400" 建立名為 "mynewsqldw" 的資料庫，以部署到 "mywesteuroperesgp1" 資源群組中名為 "sqldwserver1" 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2b30b-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="2b30b-124">必要參數如下：</span><span class="sxs-lookup"><span data-stu-id="2b30b-124">Required Parameters are:</span></span>

* <span data-ttu-id="2b30b-125">**RequestedServiceObjectiveName**：您要求的 [DWU][DWU] 數量。</span><span class="sxs-lookup"><span data-stu-id="2b30b-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="2b30b-126">支援的值為︰DW100、DW200、DW300、DW400、DW500、DW600、DW1000、DW1200、DW1500、DW2000、DW3000 和 DW6000。</span><span class="sxs-lookup"><span data-stu-id="2b30b-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="2b30b-127">**DatabaseName**：您要建立的 SQL 資料倉儲的名稱。</span><span class="sxs-lookup"><span data-stu-id="2b30b-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="2b30b-128">**ServerName**：您用來建立的伺服器名稱 (必須是 V12)。</span><span class="sxs-lookup"><span data-stu-id="2b30b-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="2b30b-129">**ResourceGroupName**：您使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2b30b-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="2b30b-130">若要尋找訂用帳戶中可用的資源，請使用 Get-AzureResource。</span><span class="sxs-lookup"><span data-stu-id="2b30b-130">To find available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="2b30b-131">**版本**：必須是 "DataWarehouse"，才能建立 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2b30b-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span></span>

<span data-ttu-id="2b30b-132">選擇性參數如下：</span><span class="sxs-lookup"><span data-stu-id="2b30b-132">Optional Parameters are:</span></span>

* <span data-ttu-id="2b30b-133">**CollationName**：未指定定序時的預設值為 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="2b30b-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="2b30b-134">無法變更資料庫的定序。</span><span class="sxs-lookup"><span data-stu-id="2b30b-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="2b30b-135">**MaxSizeBytes**︰資料庫的預設大小上限為 10 GB。</span><span class="sxs-lookup"><span data-stu-id="2b30b-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span></span>

<span data-ttu-id="2b30b-136">如需參數選項的詳細資訊，請參閱 [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] 和[建立資料庫 (Azure SQL 資料倉儲)][Create Database (Azure SQL Data Warehouse)]。</span><span class="sxs-lookup"><span data-stu-id="2b30b-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b30b-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b30b-137">Next steps</span></span>
<span data-ttu-id="2b30b-138">SQL 資料倉儲完成佈建之後，建議您試著[載入範例資料][loading sample data]，或查看如何[開發][develop]、[載入][load]或[移轉][migrate]。</span><span class="sxs-lookup"><span data-stu-id="2b30b-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="2b30b-139">如果您有興趣進一步了解如何以程式設計方式管理 SQL 資料倉儲，請查看我們的文章中有關 [PowerShell Cmdlet 和 REST API][PowerShell cmdlets and REST APIs] 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="2b30b-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how to create a SQL Data Warehouse from the Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
