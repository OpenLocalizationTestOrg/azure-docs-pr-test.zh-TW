---
title: "SQL Database 災害復原演練 | Microsoft Docs"
description: "了解使用 Azure SQL Database 來執行災害復原演練的指引和最佳作法，以協助確保您的關鍵性商務應用程式在失敗和中斷時可迅速復原。"
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
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="8c8da-103">執行災害復原演練</span><span class="sxs-lookup"><span data-stu-id="8c8da-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="8c8da-104">建議您定期驗證應用程式的復原工作流程整備。</span><span class="sxs-lookup"><span data-stu-id="8c8da-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="8c8da-105">最佳設計作法是，驗證容錯移轉所涉及之資料遺失和 (或) 中斷的應用程式行為和影響。</span><span class="sxs-lookup"><span data-stu-id="8c8da-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="8c8da-106">這也是大多數業界標準在商務持續性認證中的規定。</span><span class="sxs-lookup"><span data-stu-id="8c8da-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="8c8da-107">災害復原演練內容包括：</span><span class="sxs-lookup"><span data-stu-id="8c8da-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="8c8da-108">模擬資料層中斷情況</span><span class="sxs-lookup"><span data-stu-id="8c8da-108">Simulating data tier outage</span></span>
* <span data-ttu-id="8c8da-109">復原</span><span class="sxs-lookup"><span data-stu-id="8c8da-109">Recovering</span></span>
* <span data-ttu-id="8c8da-110">驗證復原後的應用程式完整性</span><span class="sxs-lookup"><span data-stu-id="8c8da-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="8c8da-111">執行演練的工作流程會因您 [設計商務持續性之應用程式](sql-database-business-continuity.md)的方式而異。</span><span class="sxs-lookup"><span data-stu-id="8c8da-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="8c8da-112">以下將說明在 Azure SQL Database 的內容中進行災害復原演練的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="8c8da-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="8c8da-113">異地還原</span><span class="sxs-lookup"><span data-stu-id="8c8da-113">Geo-restore</span></span>
<span data-ttu-id="8c8da-114">為了避免在進行災害復原演練時可能遺失資料，建議您使用測試環境來執行演練，方法是建立生產環境的複本，然後使用這個複本來驗證應用程式的容錯移轉工作流程。</span><span class="sxs-lookup"><span data-stu-id="8c8da-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="8c8da-115">中斷模擬</span><span class="sxs-lookup"><span data-stu-id="8c8da-115">Outage simulation</span></span>
<span data-ttu-id="8c8da-116">若要模擬中斷，您可以刪除或重新命名來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c8da-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="8c8da-117">這會導致應用程式連線失敗。</span><span class="sxs-lookup"><span data-stu-id="8c8da-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="8c8da-118">復原</span><span class="sxs-lookup"><span data-stu-id="8c8da-118">Recovery</span></span>
* <span data-ttu-id="8c8da-119">如[此處](sql-database-disaster-recovery.md)所述，將資料庫異地還原至其他伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c8da-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="8c8da-120">將應用程式組態變更為連接到復原資料庫，並遵循[在復原後設定資料庫](sql-database-disaster-recovery.md)指南以完成復原。</span><span class="sxs-lookup"><span data-stu-id="8c8da-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="8c8da-121">驗證</span><span class="sxs-lookup"><span data-stu-id="8c8da-121">Validation</span></span>
* <span data-ttu-id="8c8da-122">驗證復原後的應用程式完整性 (包括連接字串、登入、基本功能測試或標準應用程式登出程序的其他驗證部分)，完成演練。</span><span class="sxs-lookup"><span data-stu-id="8c8da-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="8c8da-123">異地複寫</span><span class="sxs-lookup"><span data-stu-id="8c8da-123">Geo-replication</span></span>
<span data-ttu-id="8c8da-124">針對使用異地複寫保護的資料庫，本演練內容涵蓋規劃容錯移轉至次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c8da-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="8c8da-125">計劃性容錯移轉可確保在切換角色時，主要與次要資料庫會保持同步。</span><span class="sxs-lookup"><span data-stu-id="8c8da-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="8c8da-126">與未計畫的容錯移轉不同的是，這項作業不會導致資料遺失，所以可以在生產環境中執行這項演練。</span><span class="sxs-lookup"><span data-stu-id="8c8da-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="8c8da-127">中斷模擬</span><span class="sxs-lookup"><span data-stu-id="8c8da-127">Outage simulation</span></span>
<span data-ttu-id="8c8da-128">若要模擬中斷，您可以停用連接到資料庫的 Web 應用程式或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8c8da-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="8c8da-129">這會導致 Web 用戶端的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="8c8da-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="8c8da-130">復原</span><span class="sxs-lookup"><span data-stu-id="8c8da-130">Recovery</span></span>
* <span data-ttu-id="8c8da-131">請確定 DR 區域中的應用程式組態指向先前的次要資料庫，該資料庫會變成可完全存取的新主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c8da-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="8c8da-132">執行 [規劃的容錯移轉](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) 將次要資料庫變成新的主要資料庫</span><span class="sxs-lookup"><span data-stu-id="8c8da-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="8c8da-133">請遵循 [在復原後設定資料庫](sql-database-disaster-recovery.md) 指南以完成復原。</span><span class="sxs-lookup"><span data-stu-id="8c8da-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="8c8da-134">驗證</span><span class="sxs-lookup"><span data-stu-id="8c8da-134">Validation</span></span>
* <span data-ttu-id="8c8da-135">驗證復原後的應用程式完整性 (包括連接字串、登入、基本功能測試或標準應用程式登出程序的其他驗證部分)，完成演練。</span><span class="sxs-lookup"><span data-stu-id="8c8da-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c8da-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c8da-136">Next steps</span></span>
* <span data-ttu-id="8c8da-137">若要了解商務持續性案例，請參閱 [持續性案例](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="8c8da-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="8c8da-138">若要了解 Azure SQL Database 自動備份，請參閱 [SQL Database 自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="8c8da-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="8c8da-139">若要了解如何使用自動備份進行復原，請參閱 [從服務起始的備份還原資料庫](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="8c8da-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="8c8da-140">若要了解更快速的復原選項，請參閱[主動式異地複寫](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8c8da-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
