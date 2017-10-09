---
title: "資料庫的災害復原演練 aaaSQL |Microsoft 文件"
description: "您的任務關鍵性商務應用程式彈性 toofailures 和中斷，了解指引和使用 Azure SQL Database tooperform 災害復原切入 toohelp 保留的最佳作法。"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="0933e-103">執行災害復原演練</span><span class="sxs-lookup"><span data-stu-id="0933e-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="0933e-104">建議您定期驗證應用程式的復原工作流程整備。</span><span class="sxs-lookup"><span data-stu-id="0933e-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="0933e-105">正在驗證 hello 應用程式行為和資料遺失及/或 hello 中斷的影響該容錯移轉牽涉到是好的工程作法。</span><span class="sxs-lookup"><span data-stu-id="0933e-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="0933e-106">這也是大多數業界標準在商務持續性認證中的規定。</span><span class="sxs-lookup"><span data-stu-id="0933e-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="0933e-107">災害復原演練內容包括：</span><span class="sxs-lookup"><span data-stu-id="0933e-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="0933e-108">模擬資料層中斷情況</span><span class="sxs-lookup"><span data-stu-id="0933e-108">Simulating data tier outage</span></span>
* <span data-ttu-id="0933e-109">復原</span><span class="sxs-lookup"><span data-stu-id="0933e-109">Recovering</span></span>
* <span data-ttu-id="0933e-110">驗證復原後的應用程式完整性</span><span class="sxs-lookup"><span data-stu-id="0933e-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="0933e-111">如何根據您[設計您的應用程式的業務續航力](sql-database-business-continuity.md)，hello 工作流程 tooexecute hello 切入而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0933e-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="0933e-112">下面我們將描述 hello 進行災害復原訓練，Azure SQL Database 的 hello 內容中的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0933e-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="0933e-113">異地還原</span><span class="sxs-lookup"><span data-stu-id="0933e-113">Geo-restore</span></span>
<span data-ttu-id="0933e-114">tooprevent hello 潛在資料遺失進行災害復原訓練時，建議您執行建立 hello 實際執行環境的複本並使用它所使用的測試環境的 hello 切入 tooverify hello 應用程式的容錯移轉工作流程。</span><span class="sxs-lookup"><span data-stu-id="0933e-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="0933e-115">中斷模擬</span><span class="sxs-lookup"><span data-stu-id="0933e-115">Outage simulation</span></span>
<span data-ttu-id="0933e-116">toosimulate hello 中斷，您可以刪除或重新命名 hello 來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="0933e-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="0933e-117">這會導致應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="0933e-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="0933e-118">復原</span><span class="sxs-lookup"><span data-stu-id="0933e-118">Recovery</span></span>
* <span data-ttu-id="0933e-119">至不同的伺服器執行 hello 異地還原的 hello 資料庫，如所述[這裡](sql-database-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="0933e-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="0933e-120">變更 hello 應用程式組態 tooconnect toohello 復原的資料庫，然後遵循 hello[設定資料庫復原後](sql-database-disaster-recovery.md)引導 toocomplete hello 復原。</span><span class="sxs-lookup"><span data-stu-id="0933e-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="0933e-121">驗證</span><span class="sxs-lookup"><span data-stu-id="0933e-121">Validation</span></span>
* <span data-ttu-id="0933e-122">完整的 hello 鑽研藉由驗證 hello 應用程式完整性 post 復原 （包括連接字串、 登入、 基本功能測試或驗證的其他部分標準應用程式 signoffs 程序）。</span><span class="sxs-lookup"><span data-stu-id="0933e-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="0933e-123">異地複寫</span><span class="sxs-lookup"><span data-stu-id="0933e-123">Geo-replication</span></span>
<span data-ttu-id="0933e-124">使用地理複寫 hello 向下切入保護資料庫練習會涉及已規劃的容錯移轉 toohello 次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="0933e-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="0933e-125">hello 規劃的容錯移轉可確保，主要的 hello 與 hello 次要資料庫保持同步 hello 角色切換時。</span><span class="sxs-lookup"><span data-stu-id="0933e-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="0933e-126">不同於 hello 規劃的容錯移轉，這項作業不會導致資料遺失，所以無法執行 hello 切入 hello 實際執行環境中。</span><span class="sxs-lookup"><span data-stu-id="0933e-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="0933e-127">中斷模擬</span><span class="sxs-lookup"><span data-stu-id="0933e-127">Outage simulation</span></span>
<span data-ttu-id="0933e-128">toosimulate hello 中斷，您可以停用 hello web 應用程式或連接的虛擬機器 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0933e-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="0933e-129">這會導致 hello 連線失敗之 hello web 用戶端。</span><span class="sxs-lookup"><span data-stu-id="0933e-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="0933e-130">復原</span><span class="sxs-lookup"><span data-stu-id="0933e-130">Recovery</span></span>
* <span data-ttu-id="0933e-131">請確定 hello 應用程式組態中 hello DR 區域點 toohello 前者次要變成 hello 完全可存取的新主要複本。</span><span class="sxs-lookup"><span data-stu-id="0933e-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="0933e-132">執行[規劃的容錯移轉](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)toomake hello 次要資料庫的新主要複本</span><span class="sxs-lookup"><span data-stu-id="0933e-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="0933e-133">請遵循 hello[設定資料庫復原後](sql-database-disaster-recovery.md)引導 toocomplete hello 復原。</span><span class="sxs-lookup"><span data-stu-id="0933e-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="0933e-134">驗證</span><span class="sxs-lookup"><span data-stu-id="0933e-134">Validation</span></span>
* <span data-ttu-id="0933e-135">完整的 hello 鑽研藉由驗證 hello 應用程式完整性 post 復原 （包括連接字串、 登入、 基本功能測試或驗證的其他部分標準應用程式 signoffs 程序）。</span><span class="sxs-lookup"><span data-stu-id="0933e-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0933e-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0933e-136">Next steps</span></span>
* <span data-ttu-id="0933e-137">toolearn 有關業務續航力情況，請參閱[持續性案例](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="0933e-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="0933e-138">toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="0933e-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="0933e-139">toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="0933e-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="0933e-140">toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0933e-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
