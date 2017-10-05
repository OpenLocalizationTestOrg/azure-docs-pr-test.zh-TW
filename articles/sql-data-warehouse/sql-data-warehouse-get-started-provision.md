---
title: "在 Azure 入口網站中建立 SQL 資料倉儲 | Microsoft Docs"
description: "了解如何在 Azure 入口網站中建立 Azure SQL 資料倉儲"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="a64c7-103">建立 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="a64c7-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a64c7-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a64c7-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="a64c7-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="a64c7-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="a64c7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a64c7-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="a64c7-107">本教學課程使用 Azure 入口網站來建立包含 AdventureWorksDW 範例資料庫的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="a64c7-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a64c7-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a64c7-108">Prerequisites</span></span>
<span data-ttu-id="a64c7-109">若要開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="a64c7-109">To get started, you need:</span></span>

* <span data-ttu-id="a64c7-110">**Azure 帳戶**︰請瀏覽 [Azure 免費試用][Azure Free Trial]或 [MSDN Azure 點數][MSDN Azure Credits]以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="a64c7-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="a64c7-111">**Azure SQL Server**︰如需詳細資訊，請參閱[使用 Azure 入口網站建立 Azure SQL Database][Create an Azure SQL database in the Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="a64c7-112">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="a64c7-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="a64c7-113">如需詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="a64c7-114">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="a64c7-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="a64c7-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a64c7-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a64c7-116">按一下 [+ 新增] > [資料庫] > [SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![建立](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="a64c7-118">在 [SQL 資料倉儲]  刀鋒視窗中，填入所需的資訊，然後按 [建立] 來建立。</span><span class="sxs-lookup"><span data-stu-id="a64c7-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![建立資料庫](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="a64c7-120">**伺服器**︰我們建議您先選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a64c7-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="a64c7-121">**資料庫名稱**︰用來參考 SQL 資料倉儲的名稱。</span><span class="sxs-lookup"><span data-stu-id="a64c7-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="a64c7-122">對伺服器而言，它必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a64c7-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="a64c7-123">**效能**：我們建議從 400 [DWU][DWU] 開始。</span><span class="sxs-lookup"><span data-stu-id="a64c7-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="a64c7-124">您可以將滑桿向左邊或向右移動，以調整資料倉儲的效能，在建立之後相應增加或相應減少。</span><span class="sxs-lookup"><span data-stu-id="a64c7-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="a64c7-125">若要深入了解 DWU，請參閱[調整](sql-data-warehouse-manage-compute-overview.md)相關文件或我們的[價格頁面][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="a64c7-126">**訂用帳戶**：選取此 SQL 資料倉儲將會計費的 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="a64c7-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="a64c7-127">**資源群組**：[資源群組][Resource group]是為了協助您管理 Azure 資源集合而設計的容器。</span><span class="sxs-lookup"><span data-stu-id="a64c7-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="a64c7-128">深入了解[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a64c7-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="a64c7-129">**選取來源**：按一下 [選取來源] > [範例]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="a64c7-130">Azure 會自動將 AdventureWorksDW 填入 [選取範例]  選項。</span><span class="sxs-lookup"><span data-stu-id="a64c7-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a64c7-131">SQL 資料倉儲的預設定序為 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="a64c7-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="a64c7-132">如果需要不同的定序，可以使用 [T-SQL][T-SQL] 來建立具有不同定序的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a64c7-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="a64c7-133">按一下 [建立]  來建立您的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="a64c7-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="a64c7-134">等候幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a64c7-134">Wait for a few minutes.</span></span> <span data-ttu-id="a64c7-135">當您的資料倉儲準備就緒時，您應該會返回 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a64c7-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a64c7-136">您可以在儀表板上尋找您的 SQL 資料倉儲，其列在您的 SQL 資料庫之下，或在您用來建立它的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="a64c7-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![入口網站檢視](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="a64c7-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a64c7-138">Next steps</span></span>
<span data-ttu-id="a64c7-139">既然您已建立 SQL 資料倉儲，您已準備好 [連接](sql-data-warehouse-connect-overview.md) 和開始查詢。</span><span class="sxs-lookup"><span data-stu-id="a64c7-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="a64c7-140">若要將資料載入 SQL 資料倉儲，請參閱 [載入概觀](sql-data-warehouse-overview-load.md)。</span><span class="sxs-lookup"><span data-stu-id="a64c7-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="a64c7-141">如果您嘗試將現有的資料庫移轉至 SQL 資料倉儲，請參閱[移轉概觀](sql-data-warehouse-overview-migrate.md)或使用[移轉公用程式](sql-data-warehouse-migrate-migration-utility.md)。</span><span class="sxs-lookup"><span data-stu-id="a64c7-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="a64c7-142">也可以使用 Transact-SQL 來設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a64c7-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="a64c7-143">如需詳細資訊，請參閱 [sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。</span><span class="sxs-lookup"><span data-stu-id="a64c7-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="a64c7-144">查看我們的[最佳作法][Best practices]也是不錯的辦法。</span><span class="sxs-lookup"><span data-stu-id="a64c7-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="a64c7-145">[訂用帳戶]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="a64c7-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
