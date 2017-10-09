---
title: "aaaCreate hello Azure 入口網站中的 SQL 資料倉儲 |Microsoft 文件"
description: "了解如何 toocreate Azure SQL 資料倉儲中的 hello Azure 入口網站"
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
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="82fa7-103">建立 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="82fa7-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82fa7-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="82fa7-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="82fa7-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="82fa7-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="82fa7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82fa7-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="82fa7-107">本教學課程使用 hello Azure 入口網站 toocreate 包含 AdventureWorksDW 範例資料庫的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="82fa7-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82fa7-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="82fa7-108">Prerequisites</span></span>
<span data-ttu-id="82fa7-109">tooget 開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="82fa7-109">tooget started, you need:</span></span>

* <span data-ttu-id="82fa7-110">**Azure 帳戶**： 瀏覽[Azure 免費試用][ Azure Free Trial]或[MSDN Azure 信用額度][ MSDN Azure Credits] toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="82fa7-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="82fa7-111">**Azure SQL server**： 請參閱[以 hello Azure 入口網站建立 Azure SQL database] [ Create an Azure SQL database in hello Azure portal]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="82fa7-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="82fa7-112">建立 SQL 資料倉儲可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="82fa7-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="82fa7-113">如需詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="82fa7-114">建立 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="82fa7-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="82fa7-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="82fa7-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="82fa7-116">按一下 [+ 新增] > [資料庫] > [SQL 資料倉儲]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![建立](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="82fa7-118">在 hello **SQL 資料倉儲**刀鋒視窗中，填入 hello 所需資訊，然後按 建立 5d toocreate。</span><span class="sxs-lookup"><span data-stu-id="82fa7-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![建立資料庫](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="82fa7-120">**伺服器**︰我們建議您先選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="82fa7-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="82fa7-121">**資料庫名稱**: hello 為使用的 tooreference hello SQL 資料倉儲的名稱。</span><span class="sxs-lookup"><span data-stu-id="82fa7-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="82fa7-122">它必須是唯一的 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="82fa7-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="82fa7-123">**效能**：我們建議從 400 [DWU][DWU] 開始。</span><span class="sxs-lookup"><span data-stu-id="82fa7-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="82fa7-124">您可以移動保留的 hello 滑桿 toohello，或以滑鼠右鍵 tooadjust hello 效能資料倉儲或小數位數的向上或向下建立之後。</span><span class="sxs-lookup"><span data-stu-id="82fa7-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="82fa7-125">toolearn 深入了解 dwu 調整，請參閱我們的文件上[調整](sql-data-warehouse-manage-compute-overview.md)或我們[定價頁面][SQL Data Warehouse pricing]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="82fa7-126">**訂用帳戶**： 選取 hello[訂用帳戶]，將付款人此 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="82fa7-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="82fa7-127">**資源群組**:[資源群組][ Resource group]所設計的容器 toohelp 管理 Azure 資源的集合。</span><span class="sxs-lookup"><span data-stu-id="82fa7-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="82fa7-128">深入了解[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82fa7-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="82fa7-129">**選取來源**：按一下 [選取來源] > [範例]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="82fa7-130">Azure 會自動填入 hello**選取範例**AdventureWorksDW 的選項。</span><span class="sxs-lookup"><span data-stu-id="82fa7-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82fa7-131">hello SQL 資料倉儲的預設定序為 SQL_Latin1_General_CP1_CI_AS。</span><span class="sxs-lookup"><span data-stu-id="82fa7-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="82fa7-132">如果需要不同的定序， [T-SQL] [ T-SQL]可以是使用的 toocreate hello 資料庫具有不同的定序。</span><span class="sxs-lookup"><span data-stu-id="82fa7-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="82fa7-133">按一下**建立**toocreate SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="82fa7-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="82fa7-134">等候幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="82fa7-134">Wait for a few minutes.</span></span> <span data-ttu-id="82fa7-135">準備您的資料倉儲時，您應該傳回 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="82fa7-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="82fa7-136">您可以尋找您的 SQL 資料倉儲儀表板上，列在您的 SQL 資料庫，或在 hello 資源群組，您使用 toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="82fa7-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![入口網站檢視](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="82fa7-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82fa7-138">Next steps</span></span>
<span data-ttu-id="82fa7-139">現在您已經建立 SQL 資料倉儲，您就可以準備太[連接](sql-data-warehouse-connect-overview.md)並開始查詢。</span><span class="sxs-lookup"><span data-stu-id="82fa7-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="82fa7-140">tooload 資料到 SQL 資料倉儲，請參閱 hello[載入概觀](sql-data-warehouse-overview-load.md)。</span><span class="sxs-lookup"><span data-stu-id="82fa7-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="82fa7-141">如果您嘗試 toomigrate 現有的資料庫 tooSQL 資料倉儲時，請參閱 hello[移轉概觀](sql-data-warehouse-overview-migrate.md)或使用[移轉公用程式](sql-data-warehouse-migrate-migration-utility.md)。</span><span class="sxs-lookup"><span data-stu-id="82fa7-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="82fa7-142">也可以使用 Transact-SQL 來設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="82fa7-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="82fa7-143">如需詳細資訊，請參閱 [sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="82fa7-144">它也是很好的想法 toolook 在 hello[最佳做法][Best practices]。</span><span class="sxs-lookup"><span data-stu-id="82fa7-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[訂用帳戶]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
