---
title: "適用於 SQL Database 的 Azure PowerShell 指令碼範例 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例可協助您建立和管理 Azure SQL Database 伺服器、彈性集區、資料庫和防火牆。"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 5a5f77b9adafe32e8559d0b3396febca4b191de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a><span data-ttu-id="81494-103">Azure SQL Database 的 Azure PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="81494-103">Azure PowerShell samples for Azure SQL Database</span></span>

<span data-ttu-id="81494-104">下表包含適用於 Azure SQL Database 之範例 Azure PowerShell 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="81494-104">The following table includes links to sample Azure PowerShell scripts for Azure SQL Database.</span></span>

| |  |
|---|---|
|<span data-ttu-id="81494-105">**建立單一資料庫和彈性集區**</span><span class="sxs-lookup"><span data-stu-id="81494-105">**Create a single database and an elastic pool**</span></span>||
| [<span data-ttu-id="81494-106">建立單一資料庫並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="81494-106">Create a single database and configure a firewall rule</span></span>](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-107">此 PowerShell 指令碼會建立單一 Azure SQL Database，並設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="81494-107">This PowerShell script creates a single Azure SQL database and configures a server-level firewall rule.</span></span> |
| [<span data-ttu-id="81494-108">建立彈性集區並移動集區資料庫</span><span class="sxs-lookup"><span data-stu-id="81494-108">Create elastic pools and move pooled databases</span></span>](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-109">此 PowerShell 指令碼會建立 Azure SQL Database 彈性集區、移動集區資料庫，並變更效能層級。</span><span class="sxs-lookup"><span data-stu-id="81494-109">This PowerShell script creates Azure SQL Database elastic pools, and moves pooled databases, and changes performance levels.</span></span>|
|<span data-ttu-id="81494-110">**設定異地複寫和容錯移轉**</span><span class="sxs-lookup"><span data-stu-id="81494-110">**Configure geo-replication and failover**</span></span>||
| [<span data-ttu-id="81494-111">使用作用中異地複寫設定單一資料庫並進行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="81494-111">Configure and failover a single database using active geo-replication</span></span>](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-112">此 PowerShell 指令碼會為單一 Azure SQL Database 設定作用中異地複寫，並將其容錯移轉到次要複本。</span><span class="sxs-lookup"><span data-stu-id="81494-112">This PowerShell script configures active geo-replication for a single Azure SQL database and fails it over to the secondary replica.</span></span> |
| [<span data-ttu-id="81494-113">使用作用中異地複寫設定集區資料庫並進行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="81494-113">Configure and failover a pooled database using active geo-replication</span></span>](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-114">此 PowerShell 指令碼會為 SQL 彈性集區中的 Azure SQL Database 設定作用中異地複寫，並將其容錯移轉到次要複本。</span><span class="sxs-lookup"><span data-stu-id="81494-114">This PowerShell script configures active geo-replication for an Azure SQL database in a SQL elastic pool, and fails it over to the secondary replica.</span></span> |
| [<span data-ttu-id="81494-115">設定單一資料庫的容錯移轉群組並進行容錯移轉 (預覽)</span><span class="sxs-lookup"><span data-stu-id="81494-115">Configure and failover a failover group for a single database (preview)</span></span>](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-116">此 PowerShell 指令碼會為 Azure SQL Database 伺服器執行個體設定容錯移轉群組，並將資料庫新增到容錯移轉群組，然後將其容錯移轉到次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="81494-116">This PowerShell script configures a failover group for an Azure SQL Database server instance, adds a database to the failover group, and fails it over to the secondary server</span></span> |
|<span data-ttu-id="81494-117">**調整單一資料庫和彈性集區**</span><span class="sxs-lookup"><span data-stu-id="81494-117">**Scale a single databases and an elastic pool**</span></span>||
| [<span data-ttu-id="81494-118">調整單一資料庫</span><span class="sxs-lookup"><span data-stu-id="81494-118">Scale a single database</span></span>](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-119">此 PowerShell 指令碼會監視 Azure SQL Database 的效能計量，並將其調整為較高的效能層級，然後對其中一個效能計量建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="81494-119">This PowerShell script monitors the performance metrics of an Azure SQL database, scales it to a higher performance level and creates an alert rule on one of the performance metrics.</span></span> |
| [<span data-ttu-id="81494-120">調整彈性集區</span><span class="sxs-lookup"><span data-stu-id="81494-120">Scale an elastic pool</span></span>](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-121">此 PowerShell 指令碼會監視 Azure SQL Database 彈性集區的效能計量，並將其調整為較高的效能層級，然後對其中一個效能計量建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="81494-121">This PowerShell script monitors the performance metrics of an Azure SQL Database elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span>  |
| <span data-ttu-id="81494-122">**稽核與威脅偵測**</span><span class="sxs-lookup"><span data-stu-id="81494-122">**Auditing and threat detection**</span></span> |
| [<span data-ttu-id="81494-123">設定稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="81494-123">Configure auditing and threat-detection</span></span>](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-124">此 PowerShell 指令碼會設定 Azure SQL Database 的稽核與威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="81494-124">This PowerShell script configures auditing and threat detection policies for an Azure SQL database.</span></span> |
| <span data-ttu-id="81494-125">**還原、複製和匯入資料庫**</span><span class="sxs-lookup"><span data-stu-id="81494-125">**Restore, copy, and import a database**</span></span>||
| [<span data-ttu-id="81494-126">還原資料庫</span><span class="sxs-lookup"><span data-stu-id="81494-126">Restore a database</span></span>](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-127">此 PowerShell 指令碼會從異地備援備份還原 Azure SQL Database，並將已刪除的 Azure SQL Database 還原為最新的備份。</span><span class="sxs-lookup"><span data-stu-id="81494-127">This PowerShell script restores an Azure SQL database from a geo-redundant backup and restores a deleted Azure SQL database to the latest backup.</span></span> |
| [<span data-ttu-id="81494-128">將資料庫複製到新伺服器</span><span class="sxs-lookup"><span data-stu-id="81494-128">Copy a database to new server</span></span>](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-129">此 PowerShell 指令碼會在新的 Azure SQL Server 中建立現有 Azure SQL Database 的複本。</span><span class="sxs-lookup"><span data-stu-id="81494-129">This PowerShell script creates a copy of an existing Azure SQL database in a new Azure SQL server.</span></span> |
| [<span data-ttu-id="81494-130">從 bacpac 檔案匯入資料庫</span><span class="sxs-lookup"><span data-stu-id="81494-130">Import a database from a bacpac file</span></span>](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="81494-131">此 PowerShell 指令碼會從 bacpac 檔案將資料庫匯入 Azure SQL Server。</span><span class="sxs-lookup"><span data-stu-id="81494-131">This PowerShell script imports a database to an Azure SQL server from a bacpac file.</span></span> |
| <span data-ttu-id="81494-132">**同步處理資料庫之間的資料**</span><span class="sxs-lookup"><span data-stu-id="81494-132">**Sync data between databases**</span></span>||
| [<span data-ttu-id="81494-133">同步處理 SQL Database 之間的資料</span><span class="sxs-lookup"><span data-stu-id="81494-133">Sync data between SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-134">此 PowerShell 指令碼會設定「資料同步」在多個 Azure SQL Database 之間進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="81494-134">This PowerShell script configures Data Sync to sync between multiple Azure SQL databases.</span></span> |
| [<span data-ttu-id="81494-135">內部部署 SQL Database 與 SQL Server 之間的同步資料</span><span class="sxs-lookup"><span data-stu-id="81494-135">Sync data between SQL Database and SQL Server on-premises</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="81494-136">此 PowerShell 指令碼會設定「資料同步」在內部部署的 Azure SQL Database 和 SQL Server 之間進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="81494-136">This PowerShell script configures Data Sync to sync between an Azure SQL database and a SQL Server on-premises database.</span></span> |
|||
|||
