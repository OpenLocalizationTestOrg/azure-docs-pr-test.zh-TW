---
title: "SQL database aaaAzure PowerShell 指令碼範例 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 toohelp 您建立和管理 Azure SQL Database 伺服器、 彈性集區、 資料庫和防火牆。"
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
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Azure SQL Database 的 Azure PowerShell 範例

hello 下表包含連結 toosample Azure PowerShell 指令碼的 Azure SQL Database。

| |  |
|---|---|
|**建立單一資料庫和彈性集區**||
| [建立單一資料庫並設定防火牆規則](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 此 PowerShell 指令碼會建立單一 Azure SQL Database，並設定伺服器層級防火牆規則。 |
| [建立彈性集區並移動集區資料庫](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 此 PowerShell 指令碼會建立 Azure SQL Database 彈性集區、移動集區資料庫，並變更效能層級。|
|**設定異地複寫和容錯移轉**||
| [使用作用中異地複寫設定單一資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 這個 PowerShell 指令碼會設定為單一的 Azure SQL database 的作用中地理複寫，並容錯 toohello 次要複本。 |
| [使用作用中異地複寫設定集區資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 這個 PowerShell 指令碼位於 SQL 彈性集區中設定的 Azure SQL database 的作用中地理複寫和容錯 toohello 次要複本。 |
| [設定單一資料庫的容錯移轉群組並進行容錯移轉 (預覽)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 這個 PowerShell 指令碼會設定 Azure SQL Database 伺服器執行個體的容錯移轉群組加入資料庫 toohello 容錯移轉群組，並容錯 toohello 次要伺服器 |
|**調整單一資料庫和彈性集區**||
| [調整單一資料庫](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 這個 PowerShell 指令碼監視 hello 的 Azure SQL database 的效能標準、 縮放，使其 tooa 較高的效能層級和 hello 效能度量的其中一個上建立警示規則。 |
| [調整彈性集區](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 這個 PowerShell 指令碼監視 Azure SQL Database 彈性集區的 hello 效能標準、 縮放，使其 tooa 較高的效能層級和 hello 效能度量的其中一個上建立警示規則。  |
| **稽核與威脅偵測** |
| [設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 此 PowerShell 指令碼會設定 Azure SQL Database 的稽核與威脅偵測原則。 |
| **還原、複製和匯入資料庫**||
| [還原資料庫](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 這個 PowerShell 指令碼從異地備援備份還原 Azure SQL database，並還原已刪除的 Azure SQL database toohello 最新備份。 |
| [複製資料庫 toonew 伺服器](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 此 PowerShell 指令碼會在新的 Azure SQL Server 中建立現有 Azure SQL Database 的複本。 |
| [從 bacpac 檔案匯入資料庫](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 這個 PowerShell 指令碼會從 bacpac 檔案匯入 tooan Azure SQL server 的資料庫。 |
| **同步處理資料庫之間的資料**||
| [同步處理 SQL Database 之間的資料](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 這個 PowerShell 指令碼會設定多個 Azure SQL database 之間的資料同步 toosync。 |
| [內部部署 SQL Database 與 SQL Server 之間的同步資料](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 這個 PowerShell 指令碼會設定 Azure SQL database 和 SQL Server 在內部部署資料庫之間的資料同步 toosync。 |
|||
|||
