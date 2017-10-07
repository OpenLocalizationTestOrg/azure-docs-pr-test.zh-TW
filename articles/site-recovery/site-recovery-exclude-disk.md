---
title: "使用 Azure Site Recovery 的保護 aaaExclude 磁碟 |Microsoft 文件"
description: "描述原因和方式 tooexclude VM 磁碟從複寫案例的 VMware tooAzure 與 HYPER-V tooAzure。"
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>從複寫排除磁碟
本文說明如何 tooexclude 磁碟從複寫。 這個排除動作可最佳化 hello 耗用複寫頻寬，或最佳化 hello 目標端資源，以便利用這類磁碟。 hello 功能支援的 VMware tooAzure 和 HYPER-V tooAzure 的案例。

## <a name="prerequisites"></a>必要條件

依預設會複寫機器上的所有磁碟。 tooexclude 磁碟從複寫中，您必須手動安裝行動服務的 hello hello 電腦上您啟用複寫，如果您從 VMware tooAzure 複寫之前。


## <a name="why-exclude-disks-from-replication"></a>為什麼要排除磁碟不要複寫？
排除磁碟不要複寫往往是因為︰

- 變換 hello 排除磁碟的 hello 資料並不重要，或不需要 toobe 複寫。

- 您想要 toosave 儲存體和網路資源不在複寫此變換。

## <a name="what-are-hello-typical-scenarios"></a>Hello 典型案例有哪些？
您可以識別資料變換的特定範例，它是排除的絕佳候選項目。 可能的範例包括寫入 tooa 分頁檔 (pagefile.sys)，並將 toohello tempdb 檔案的 Microsoft SQL Server。 根據 hello 工作負載和 hello 儲存子系統，hello 分頁檔可以註冊大量的變換。 不過，從 hello 主要站台 tooAzure 複寫這項資料會需要大量資源。 因此，您可以使用下列步驟 toooptimize 複寫虛擬機器具有 hello 作業系統和 hello 分頁檔的單一虛擬磁碟的 hello:

1. 將 hello 單一虛擬磁碟分割成兩個虛擬磁碟。 一個虛擬磁碟 hello 作業系統，而且其他 hello hello 分頁檔。
2. 從複寫排除 hello 分頁檔案的磁碟。

同樣地，您可以使用下列步驟 toooptimize，有兩個 hello Microsoft SQL Server tempdb fie hello 並 hello 系統資料庫檔案：

1. 兩個不同的磁碟上保留 hello 系統資料庫和 tempdb。
2. 從複寫排除 hello tempdb 磁碟。

## <a name="how-tooexclude-disks-from-replication"></a>如何 tooexclude 磁碟從複寫嗎？

### <a name="vmware-tooazure"></a>VMware tooAzure
請遵循 hello[啟用複寫](site-recovery-vmware-to-azure.md)工作流程 tooprotect hello Azure Site Recovery 入口網站中的虛擬機器。 在 hello hello 工作流程的第四個步驟，使用 hello**磁碟 tooREPLICATE**資料行 tooexclude 磁碟從複寫。 依預設會選取所有磁碟進行複寫。 清除您要從複寫，然後完成 hello 步驟 tooenable 複寫 tooexclude 磁碟 hello 核取方塊。

![從複寫排除磁碟，並啟用 VMware tooAzure 容錯回復複寫](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * 您可以排除已擁有 hello 行動服務安裝的磁碟。 您需要 toomanually 安裝 hello 行動服務，因為使用 hello 發送機制啟用複寫後，才會安裝 hello 行動服務。
> * 只有基本磁碟可以從複寫排除。 您無法排除作業系統或動態磁碟。
> * 啟用複寫之後，您無法新增或移除磁碟以進行複寫。 如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello 機器，並再重新啟用。
> * 如果您排除已針對應用程式 toooperate，容錯移轉 tooAzure 之後所需的磁碟必須 toocreate hello 磁碟在 Azure 中以手動方式使 hello 複寫應用程式可執行。 或者，您可以整合 Azure 自動化的復原計劃 toocreate hello 磁碟 hello 機器容錯移轉期間。
> * Windows 虛擬機器：您以手動方式在 Azure 中建立的磁碟將不會容錯回復。 例如，如果您容錯移轉三個磁碟，並直接在 Azure 虛擬機器中建立兩個磁碟，則只有三個已容錯移轉的磁碟會容錯回復。 您不能包含容錯移轉或重新保護從內部部署 tooAzure 中手動建立的磁碟。
> * Linux 虛擬機器：您以手動方式在 Azure 中建立的磁碟將會容錯回復。 例如，如果您容錯移轉三個磁碟，並直接在 Azure 虛擬機器中建立兩個磁碟，則五個磁碟全都將容錯回復。 您無法從容錯回復排除手動建立的磁碟。
>

### <a name="hyper-v-tooazure"></a>HYPER-V tooAzure
請遵循 hello[啟用複寫](site-recovery-hyper-v-site-to-azure.md)工作流程 tooprotect hello Azure Site Recovery 入口網站中的虛擬機器。 在 hello hello 工作流程的第四個步驟，使用 hello**磁碟 tooREPLICATE**資料行 tooexclude 磁碟從複寫。 依預設會選取所有磁碟進行複寫。 清除您要從複寫，然後完成 hello 步驟 tooenable 複寫 tooexclude 磁碟 hello 核取方塊。

![從複寫排除磁碟，並啟用 HYPER-V tooAzure 容錯回復複寫](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * 您只能排除基本磁碟不要複寫。 您無法排除作業系統磁碟。 我們建議您不要排除動態磁碟。 Azure Site Recovery 無法識別哪些虛擬硬碟 (VHD) 是基本或動態 hello 客體虛擬機器中。  如果不排除所有相依的動態磁碟區磁碟，hello 受保護的動態磁碟會容錯移轉虛擬機器上的故障的磁碟，hello 該磁碟上的資料無法存取。
> * 啟用複寫之後，您無法新增或移除磁碟以進行複寫。 如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello 虛擬機器，並再重新啟用。
> * 如果您排除的應用程式 toooperate 所需的磁碟，tooAzure 容錯移轉之後您還需要 toocreate hello 磁碟以手動方式在 Azure 中的以便在執行複寫的 hello 應用程式。 或者，您可以整合 Azure 自動化的復原計劃 toocreate hello 磁碟 hello 機器容錯移轉期間。
> * 您以手動方式在 Azure 中建立的磁碟不會容錯回復。 比方說，如果您無法超過三個磁碟，並直接在 Azure 虛擬機器建立兩個磁碟只有三個磁碟已容錯移轉將無法從 Azure tooHyper-V。 您不能包含在容錯回復或從 HYPER-V tooAzure 反轉複寫中手動建立的磁碟。



## <a name="end-to-end-scenarios-of-exclude-disks"></a>排除磁碟的端對端案例
讓我們考慮兩個案例 toounderstand hello 排除磁碟功能：

- SQL Server tempdb 磁碟
- 分頁檔 (pagefile.sys) 磁碟

### <a name="exclude-hello-sql-server-tempdb-disk"></a>排除 hello SQL Server tempdb 磁碟
我們來看一下有 tempdb 可排除的 SQL Server 虛擬機器。

hello hello 虛擬磁碟名稱是 SalesDB。

如下所示為 hello 來源虛擬機器上的磁碟：


**磁碟名稱** | **客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 作業系統磁碟
DB-Disk1| Disk1 | D:\ | SQL 系統資料庫和使用者資料庫 1
DB Disk2 （排除不予保護的 hello 磁碟） | Disk2 | E:\ | 暫存檔案
DB Disk3 （排除不予保護的 hello 磁碟） | Disk3 | F:\ | SQL tempdb 資料庫 (資料夾路徑 (F:\MSSQL\Data\) </b / >< / b / > 寫下 hello 容錯移轉之前的資料夾路徑。
DB-Disk4 | Disk4 |G:\ |使用者資料庫 2

因為 hello 虛擬機器的兩個磁碟上的資料變換量暫時性的而您也可以保護 hello SalesDB 虛擬機器，請從複寫排除 Disk2 和 Disk3。 Azure Site Recovery 不會複寫這些磁碟。 在容錯移轉時，這些磁碟不會出現在 Azure 上的 hello 容錯移轉虛擬機器上。

如下所示為 hello 容錯移轉後的 Azure 虛擬機器上的磁碟：

**客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | ---
DISK0 | C:\ | 作業系統磁碟
Disk1 | E:\ | 暫存儲存位置 </b / >< / b / > Azure 新增此磁碟，並指派 hello 第一個可用的磁碟機代號。
Disk2 | D:\ | SQL 系統資料庫和使用者資料庫 1
Disk3 | G:\ | 使用者資料庫 2

因為 Disk2 Disk3 已排除 hello SalesDB 虛擬機器，e： 是 hello 第一個磁碟機代號從 hello 可用的清單。 Azure 將指派 e: toohello 暫時存放磁碟區。 所有的複寫 hello 磁碟 hello 磁碟機代號維持 hello 相同。

Disk3，這是 hello SQL tempdb 磁碟 (tempdb 資料夾路徑 F:\MSSQL\Data\)，已從複寫排除。 hello 磁碟不是 hello 容錯移轉虛擬機器上。 如此一來，hello SQL 服務處於停止狀態，而且必須 hello F:\MSSQL\Data 路徑。

有兩種方式 toocreate 這個路徑：

- 新增磁碟和指派 tempdb 資料夾路徑。
- 使用現有的暫存磁碟機為 hello tempdb 資料夾路徑。

#### <a name="add-a-new-disk"></a>新增磁碟：

1. 記下 SQL tempdb.mdf 和容錯移轉之前 tempdb.ldf hello 路徑。
2. Hello Azure 入口網站，加入新磁碟 toohello 容錯移轉的虛擬機器以 hello 相同或更多的大小與 hello 來源 SQL tempdb 磁碟 (Disk3)。
3. 登入 toohello Azure 虛擬機器。 從 hello 磁碟管理 (diskmgmt.msc) 主控台中，初始化和格式 hello 新增磁碟。
4. 相同磁碟機代號 hello SQL tempdb 磁碟 （f:） 所使用的指派 hello。
5. Tempdb 上建立資料夾 hello f： 磁碟區 (F:\MSSQL\Data)。
6. 從 hello 服務主控台中啟動 hello SQL 服務。

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>使用現有的暫存磁碟機為 hello SQL tempdb 資料夾路徑：

1. 開啟命令提示字元。
2. Hello 命令提示字元中，在復原模式下執行 SQL Server。

        Net start MSSQLSERVER /f / T3608

3. 執行下列 sqlcmd toochange hello tempdb toohello 新路徑的 hello。

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. 停止 hello Microsoft SQL Server 服務。

        Net stop MSSQLSERVER
5. 啟動 hello Microsoft SQL Server 服務。

        Net start MSSQLSERVER

請參閱 toohello 遵循的暫存磁碟的 Azure 指導方針：

* [在 Azure Vm toostore SQL Server TempDB 和緩衝集區延伸模組中使用 Ssd](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Azure 虛擬機器中的 SQL Server 效能最佳做法](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>（從 Azure tooan 在內部部署主機） 的容錯回復
現在讓我們了解當您從 Azure tooyour 在內部部署 VMware 或 HYPER-V 主機容錯移轉複寫的 hello 磁碟。 您以手動方式在 Azure 中建立的磁碟不會複寫。 例如，如果您容錯移轉三個磁碟，並直接在 Azure 虛擬機器中建立兩個磁碟，則只有三個已容錯移轉的磁碟會容錯回復。 您不能包含在容錯回復或重新保護從內部部署 tooAzure 中手動建立的磁碟。 它也不會複寫 hello 暫存磁碟 tooon 內部部署主機。

#### <a name="failback-toooriginal-location-recovery"></a>容錯回復 toooriginal 位置復原

Hello 上述範例中，在 hello Azure 虛擬機器是磁碟組態，如下所示：

**客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | ---
DISK0 | C:\ | 作業系統磁碟
Disk1 | E:\ | 暫存儲存位置 </b / >< / b / > Azure 新增此磁碟，並指派 hello 第一個可用的磁碟機代號。
Disk2 | D:\ | SQL 系統資料庫和使用者資料庫 1
Disk3 | G:\ | 使用者資料庫 2


#### <a name="vmware-tooazure"></a>VMware tooAzure
當容錯回復完成 toohello 原始位置時，hello 容錯回復虛擬機器磁碟組態中沒有排除的磁碟。 從 VMware tooAzure 排除的磁碟不會 hello 容錯回復虛擬機器上。

從 Azure tooon 內部部署 VMware 計劃的容錯移轉後, hello VMWare 虛擬機器 （原始位置） 上的磁碟如下：

**客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | ---
DISK0 | C:\ | 作業系統磁碟
Disk1 | D:\ | SQL 系統資料庫和使用者資料庫 1
Disk2 | G:\ | 使用者資料庫 2

#### <a name="hyper-v-tooazure"></a>HYPER-V tooAzure
容錯回復時 toohello 原始位置，hello 容錯回復虛擬機器磁碟組態會維持 hello 相同的 HYPER-V 的原始虛擬機器磁碟組態。 Hello 容錯回復虛擬機器上使用 HYPER-V 站台 tooAzure 已排除的磁碟。

從 Azure tooon 內部部署 HYPER-V 的規劃容錯移轉之後 hello HYPER-V 虛擬機器 （原始位置） 上的磁碟如下：

**磁碟名稱** | **客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | 作業系統磁碟
DB-Disk1 | Disk1 | D:\ | SQL 系統資料庫和使用者資料庫 1
DB-Disk2 (排除的磁碟) | Disk2 | E:\ | 暫存檔案
DB-Disk3 (排除的磁碟) | Disk3 | F:\ | SQL tempdb 資料庫 (資料夾路徑 (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | 使用者資料庫 2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>排除 hello 分頁檔 (pagefile.sys) 磁碟

我們來看一下有分頁檔磁碟可排除的虛擬機器。
有兩種案例。

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>案例 1: hello d： 磁碟機上設定 hello 分頁檔
以下是 hello 磁碟組態：


**磁碟名稱** | **客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 作業系統磁碟
DB Disk1 （排除不予保護 hello hello 磁碟） | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | 使用者資料 1
DB-Disk3 | Disk3 | F:\ | 使用者資料 2

以下是 hello 來源虛擬機器上的 hello 分頁檔案設定：

![來源虛擬機器上的分頁檔設定](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


從 VMware tooAzure 或 HYPER-V tooAzure hello 虛擬機器的容錯移轉之後 hello Azure 虛擬機器上的磁碟如下：

**磁碟名稱** | **客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 作業系統磁碟
DB-Disk1 | Disk1 | D:\ | 暫存儲存體</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | 使用者資料 1
DB-Disk3 | Disk3 | F:\ | 使用者資料 2

已排除 Disk1 （d:），因為 d： 為從 hello 可用清單 hello 第一個磁碟機代號。 Azure 將指派 d toohello 暫時存放磁碟區。 D: hello Azure 虛擬機器功能，因為 hello 分頁檔設定的虛擬機器會維持為 hello hello 相同。

以下是在 hello Azure 虛擬機器上的 hello 分頁檔案設定：

![Azure 虛擬機器上的分頁檔設定](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>案例 2: hello 分頁檔設定 （以外 d： 磁碟機） 的另一個磁碟機上

以下是 hello 來源虛擬機器磁碟組態：

**磁碟名稱** | **客體作業系統磁碟#** | **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 作業系統磁碟
DB Disk1 （排除不予保護的 hello 磁碟） | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | 使用者資料 1
DB-Disk3 | Disk3 | F:\ | 使用者資料 2

以下是 hello 在內部部署虛擬機器上的 hello 分頁檔案設定：

![分頁檔 hello 在內部部署虛擬機器上的設定](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

從 VMware/HYPER-V tooAzure hello 虛擬機器的容錯移轉之後 hello Azure 虛擬機器上的磁碟如下：

**磁碟名稱**| **客體作業系統磁碟#**| **磁碟機代號** | **Hello 磁碟上的資料類型**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |作業系統磁碟
DB-Disk1 | Disk1 | D:\ | 暫存儲存體</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | 使用者資料 1
DB-Disk3 | Disk3 | F:\ | 使用者資料 2

因為 d： 從清單中可用的 hello hello 第一個磁碟機代號，Azure 將指派 d toohello 暫時存放磁碟區。 所有的複寫 hello 磁碟 hello 磁碟機代號維持 hello 相同。 找不到 hello g： 磁碟，因為 hello 系統將會使用分頁檔的 hello hello c： 磁碟機。

以下是在 hello Azure 虛擬機器上的 hello 分頁檔案設定：

![Azure 虛擬機器上的分頁檔設定](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>後續步驟
在您的部署設定完成並開始執行之後，請 [深入了解](site-recovery-failover.md) 不同類型的容錯移轉。
