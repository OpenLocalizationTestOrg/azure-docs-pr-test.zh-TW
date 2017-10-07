---
title: "aaaBackup 和還原 SQL server |Microsoft 文件"
description: "描述 Azure 虛擬機器上執行的 SQL Server 資料庫之備份和還原考量。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server 備份和還原
## <a name="overview"></a>概觀
Azure 儲存體維護 3 份每個 Azure VM 磁碟 tooguarantee 防止資料遺失或實體資料損毀。 因此，不同於內部部署，您不需要有關這些 tooworry。 不過，您仍應該備份您對應用程式或使用者錯誤 （例如將錯誤資料插入或刪除資料表） 的 SQL Server 資料庫 tooprotect 而且正在無法 toorestore 時間 tooa 點。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

針對 Azure Vm 中執行的 SQL Server，您可以使用原生備份和還原 hello 目的地 hello 備份檔案的使用已連接的磁碟的技術。 不過，沒有您可以附加根據 hello tooan Azure 的虛擬機器的磁碟數量限制 toohello [hello 虛擬機器的大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 也沒有磁碟管理 tooconsider hello 負擔。

從 SQL Server 2014 開始，您可以備份和還原 tooMicrosoft Azure Blob 儲存體。 SQL Server 2016 也提供這個選項的增強功能。 此外，針對儲存在 Microsoft Azure Blob 儲存體的資料庫檔案，SQL Server 2016 提供的選項，可使用 Azure 的快照集，用於幾乎即時的備份和快速的還原作業。 本文章提供這些選項的概觀，而您可以在 [SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148.aspx)中找到其他資訊。

> [!NOTE]
> Hello 非常龐大的資料庫備份選項的討論，請參閱[多 Tb SQL Server 資料庫備份策略適用於 Azure 虛擬機器](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx)。
> 
> 

hello 的以下各節包含 Azure 的虛擬機器中支援的 SQL Server 資訊特定 toohello 不同版本。

## <a name="sql-server-virtual-machines"></a>SQL Server 虛擬機器
當您的 SQL Server 執行個體在 Azure 虛擬機器上執行時，您的資料庫檔案已經位於 Azure 中的資料磁碟。 這些磁碟存在於 Azure Blob 儲存體中。 因此 hello 的原因備份您的資料庫和 hello 方法您採取稍微變更。 請考慮下列 hello。 

* 您不再需要 tooperform 資料庫備份 tooprovide 防止硬體故障或媒體失敗，因為 Microsoft Azure 提供這項保護 hello Microsoft Azure 服務的一部分。
* 您仍然需要 tooperform 資料庫備份 tooprovide 保護對使用者錯誤或封存之用、 規範的原因，或達成管理目的。
* 您可以直接在 Azure 中儲存 hello 備份檔案。 如需詳細資訊，請參閱下列各節會提供指引 hello 不同版本的 SQL Server 的 hello。

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 支援在 SQL Server 2014 中也能找到的 [使用 Azure Blob 進行備份及還原](https://msdn.microsoft.com/library/jj919148.aspx) 功能。 不過，它也包含下列增強功能的 hello:

| 2016 增強功能 | 詳細資料 |
| --- | --- |
| **串接** |備份時 tooMicrosoft Azure blob 儲存體，SQL Server 2016 支援備份 toomultiple blob tooenable 向上 tooa 上限為 12.8 TB 的大型資料庫備份。 |
| **快照集備份** |藉由 hello 使用 Azure 快照集，SQL Server 檔案快照集備份會提供幾乎即時的備份和快速使用 hello Azure Blob 儲存體服務儲存的資料庫檔案還原。 這項功能可讓您 toosimplify 您備份和還原原則。 檔案快照集備份也支援還原時間點。 如需詳細資訊，請參閱 [適用於在 Azure 中的資料庫檔案的快照集備份](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx)。 |
| **管理備份排程** |SQL Server Managed Backup tooAzure 現在支援自訂排程。 如需詳細資訊，請參閱[SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)。 |

教學課程中的 hello 功能的 SQL Server 2016 使用 Azure Blob 儲存體時，請參閱[教學課程： 搭配使用 hello Microsoft Azure Blob 儲存體服務和 SQL Server 2016 資料庫](https://msdn.microsoft.com/library/dn466438.aspx)。

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 包含下列增強功能的 hello:

1. **備份和還原 tooAzure**:
   
   * *SQL Server 備份 tooURL*現可支援在 SQL Server Management Studio。 使用 SQL Server Management Studio 中的備份或還原工作或維護計畫精靈時，現在可使用 hello 選項 tooback tooAzure 組成。 如需詳細資訊，請參閱[SQL Server 備份 tooURL](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx)。
   * *SQL Server Managed Backup tooAzure*具有讓備份管理自動化的新功能。 這特別適用於在 Azure 機器上執行的 SQL Server 2014 執行個體之自動化備份管理。 如需詳細資訊，請參閱[SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx)。
   * *自動備份*提供額外的自動化 tooautomatically 啟用*SQL Server Managed Backup tooAzure* Azure 中的 SQL Server VM 的所有現有和新資料庫上。 如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的自動化備份](virtual-machines-windows-sql-automated-backup.md)。
   * 如需所有 SQL Server 2014 備份 tooAzure hello 選項的概觀，請參閱[SQL Server 備份及還原與 Microsoft Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx)。
2. **加密**：SQL Server 2014 支援在建立備份時加密資料。 它支援數種加密演算法，並用 hello osf 憑證或非對稱金鑰。 如需詳細資訊，請參閱 [備份加密](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx)。

## <a name="sql-server-2012"></a>SQL Server 2012
如需 SQL Server 2012 中 SQL Server 備份及還原的詳細資訊，請參閱 [SQL Server 資料庫備份及還原 (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx)。

從 SQL Server 2012 SP1 累計更新 2 開始，您可以備份 tooand 還原從 hello Azure Blob 儲存體服務。 這項增強功能可使用的 tooback Azure 虛擬機器或在內部部署執行個體上執行的 SQL Server 上的 SQL Server 資料庫。 如需詳細資訊，請參閱 [SQL Server 備份及還原與 Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx)。

使用 hello Azure Blob 儲存體服務的 hello 優點包括 hello 能力 toobypass hello 16 磁碟限制連接的磁碟，方便管理，在 Azure 上執行的 SQL Server 執行個體的 hello 備份檔案 tooanother 執行個體的 hello 直接可用性虛擬機器或在內部部署執行個體進行移轉或災害復原。 優點 toousing 是 SQL Server 備份的 Azure blob 儲存體服務的完整清單，請參閱 hello*優點*一節中[SQL Server 備份及還原與 Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx)。

如需最佳做法建議和疑難排解資訊，請參閱 [備份與還原最佳做法 (Azure Blob 儲存體服務)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx)。

## <a name="sql-server-2008"></a>SQL Server 2008
如需在 SQL Server 2008 R2 中進行 SQL Server 備份及還原，請參閱 [在 SQL Server 中備份和還原資料庫 (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx)。

如需在 SQL Server 2008 中進行 SQL Server 備份及還原，請參閱 [在 SQL Server 中備份和還原資料庫 (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx)。

## <a name="next-steps"></a>後續步驟
如果您的 Azure VM 中的 SQL Server 的部署計劃，您可以在教學課程的 hello 找到佈建的指引：[佈建 Azure 與 Azure 資源管理員上的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

雖然備份和還原資料時可以是使用的 toomigrate，有可能更容易資料移轉路徑 tooSQL Azure VM 上的伺服器。 移轉選項和建議的完整討論，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](virtual-machines-windows-migrate-sql.md)。

請檢閱其他 [在 Azure 虛擬機器中執行 SQL Server 的資源](virtual-machines-windows-sql-server-iaas-overview.md)。

