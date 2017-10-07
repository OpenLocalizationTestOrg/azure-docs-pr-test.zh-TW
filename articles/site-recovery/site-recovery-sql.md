---
title: "aaaReplicate 應用程式，以 SQL Server 及 Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooreplicate SQL Server 的 SQL Server 災害功能使用 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>使用 SQL Server 災害復原和 Azure Site Recovery 保護 SQL Server

本文說明如何 tooprotect hello SQL Server 備份結尾使用的 SQL Server 業務續航力和災害復原 (BCDR) 技術，組合的應用程式和[Azure Site Recovery](site-recovery-overview.md)。

開始之前，請確定您了解 SQL Server 災害復原功能，包括容錯移轉叢集、Always On 可用性群組、資料庫鏡像和記錄傳送。


## <a name="sql-server-deployments"></a>SQL Server 部署

許多工作負載使用 SQL Server 為基礎，且它可以與應用程式，例如 SharePoint、 Dynamics 和 SAP、 tooimplement 資料服務整合。  有許多方法可以部署 SQL Server：

* **獨立 SQL Server**：SQL Server 和所有資料庫都裝載在單一電腦 (實體或虛擬) 上。 如果是虛擬，則主機叢集用於高可用性。 不實作來賓層級的高可用性。
* **SQL Server 容錯移轉叢集執行個體 (Always ON FCI)**：在「Windows 容錯移轉」叢集中設定 2 個或更多個具有共用磁碟的 SQL Server 執行個體節點。 如果節點已關閉，hello 叢集可以容錯 tooanother 執行個體的 SQL Server。 此安裝程式的主要站台的一般常用的 tooimplement 高可用性。 此部署不防範失敗或中斷 hello 共用的儲存層。 共用磁碟可以使用 iSCSI、光纖通道或共用 vhdx 來實作。
* **SQL Always On 可用性群組**：在不共用任何內容的叢集中設定兩個節點，其中此叢集的 SQL Server 資料庫是設定在具有同步複寫和自動容錯移轉功能的可用性群組中。

 這篇文章會利用下列復原資料庫 tooa 遠端站台的原生 SQL 災害復原技術的 hello:

* SQL Alwayson 可用性群組，tooprovide 嚴重損壞修復的 SQL Server 2012 或 2014 Enterprise edition。
* SQL Server Standard 版本 (任何版本) 或 SQL Server 2008 R2 的高安全性模式「SQL 資料庫鏡像」。

## <a name="site-recovery-support"></a>Site Recovery 支援

### <a name="supported-scenarios"></a>支援的案例
站台復原可以保護 hello 表中摘要說明 SQL Server。

**案例** | **tooa 次要站台** | **tooAzure**
--- | --- | ---
**Hyper-V** | 是 | 是
**VMware** | 是 | 是
**實體伺服器** | 是 | 是

### <a name="supported-sql-server-versions"></a>支援的 SQL Server 版本
這些 SQL Server 支援的版本，支援的 hello 案例：

* SQL Server 2016 Enterprise 和 Standard
* SQL Server 2014 Enterprise 和 Standard
* SQL Server 2012 Enterprise 和 Standard
* SQL Server 2008 R2 Enterprise 和 Standard

### <a name="supported-sql-server-integration"></a>支援的 SQL Server 整合

站台復原可以整合與 hello 表，tooprovide 災害復原方案中摘要說明原生 SQL Server BCDR 技術。

**功能** | **詳細資料** | **SQL Server** |
--- | --- | ---
**Always On 可用性群組** | 多個 SQL Server 獨立執行個體中，每個都在含有多個節點的容錯移轉叢集中執行。<br/><br/>資料庫可以分組到可以在 SQL Server 執行個體上複製 (鏡像) 的容錯移轉群組，因此不需要任何共用儲存體。<br/><br/>在主要站台與一或多個次要站台之間提供災害復原功能。 使用同步複寫與自動容錯移轉在可用性群組中設定 SQL Server 資料庫時，可以在不共用任何內容的叢集中設定兩個節點。 | SQL Server 2014 和 2012 Enterprise 版本
**容錯移轉叢集 (Always On FCI)** | SQL Server 會針對內部部署 SQL Server 工作負載的高可用性，運用 Windows 容錯移轉叢集。<br/><br/>使用共用磁碟執行 SQL Server 執行個體的節點是在容錯移轉叢集中設定。 如果執行個體已關閉 hello 叢集會容錯移轉 toodifferent 其中一個。<br/><br/>hello 叢集不防範失敗或中斷共用存放裝置中。 hello 共用的磁碟可以使用 iSCSI、 光纖通道實作，或共用 Vhdx。 | SQL Server Enterprise Edition<br/><br/>SQL Server Standard edition （有限的 tootwo 節點）
**資料庫鏡像 (高安全性模式)** | 保護單一資料庫 tooa 單一次要複本。 提供高安全性 (同步) 和高效能 (非同步) 複寫模式。 不需要容錯移轉叢集。 | SQL Server 2008 R2<br/><br/>SQL Server Enterprise 所有版本
**獨立式 SQL Server** | hello SQL Server 和資料庫裝載在單一伺服器 （實體或虛擬）。 如果 hello 伺服器為虛擬，主機叢集會使用高可用性。 沒有來賓層級的高可用性。 | Enterprise 或 Standard Edition

## <a name="deployment-recommendations"></a>部署建議

下表摘要說明我們將 SQL Server BCDR 技術與 Site Recovery 整合的建議。

| **版本** | **版本** | **部署** | **內部 tooon 內部** | **內部 tooAzure** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 或 2012 |Enterprise |容錯移轉叢集執行個體 |Always On 可用性群組 |Always On 可用性群組 |
|| Enterprise |高可用性的 Always On 可用性群組 |Always On 可用性群組 |Always On 可用性群組 | |
|| 標準 |容錯移轉叢集執行個體 (FCI) |包含本機鏡像的 Site Recovery 複寫 |包含本機鏡像的 Site Recovery 複寫 | |
|| Enterprise 或 Standard |獨立 |Site Recovery 複寫 |Site Recovery 複寫 | |
| SQL Server 2008 R2 或 2008 |Enterprise 或 Standard |容錯移轉叢集執行個體 (FCI) |包含本機鏡像的 Site Recovery 複寫 |包含本機鏡像的 Site Recovery 複寫 |
|| Enterprise 或 Standard |獨立 |Site Recovery 複寫 |Site Recovery 複寫 | |
| SQL Server (任何版本) |Enterprise 或 Standard |容錯移轉叢集執行個體 - DTC 應用程式 |Site Recovery 複寫 |不支援 |

## <a name="deployment-prerequisites"></a>部署必要條件

* 執行支援的 SQL Server 版本的內部部署 SQL Server 部署。 通常，您的 SQL Server 也需要 Active Directory。
* hello 需求 hello 想 toodeploy 案例。 深入了解支援需求[複寫 tooAzure](site-recovery-support-matrix-to-azure.md)和[內部](site-recovery-support-matrix.md)，和[部署必要條件](site-recovery-prereq.md)。
* 在 Azure 中，執行 hello 復原 tooset [Azure 虛擬機器整備評估](http://www.microsoft.com/download/details.aspx?id=40898)toomake 確定它們相容與 Azure Site Recovery 的工具 SQL Server 虛擬機器上。

## <a name="set-up-active-directory"></a>設定 Active Directory

適當地設定 hello 復原次要站台，而 SQL Server toorun 中 Active Directory。

* **小型企業**— 少量應用程式和 hello 在內部部署站台的單一網域控制站，如果您想 toofail 透過 hello 整個站台，我們建議您使用站台復原複寫 tooreplicate hello 網域控制站toohello 次要資料中心或 tooAzure。
* **中度 toolarge 企業**— 如果您有大量的應用程式，Active Directory 樹系，而且您想 toofail 依應用程式或工作負載，我們建議您設定在 hello 次要資料中心或其他網域控制站Azure。 如果您使用 Alwayson 可用性群組 toorecover tooa 遠端站台，建議您設定另一個的額外網域控制站 hello 次要站台上或在 Azure 中，toouse hello 復原 SQL Server 執行個體。

這篇文章中的 hello 指示會假設為 hello 次要位置中的網域控制站為可用。 [閱讀更多](site-recovery-active-directory.md) 有關使用 Site Recovery 保護 Active Directory。


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>針對複寫 tooAzure 整合與 SQL Server Alwayson

以下是您的需要 toodo:

1. 將指令碼匯入您的 Azure 自動化帳戶。 這包含 hello 指令碼 toofailover SQL 可用性群組中[資源管理員虛擬機器](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1)和[傳統虛擬機器](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1)。

    [![部署 tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. 新增 ASR-SQL-FailoverAG 以 hello hello 復原方案的第一個群組前動作。

1. 請遵循 hello hello 可用性群組的可用 hello 指令碼 toocreate 自動化變數 tooprovide hello 名稱中的指示。

### <a name="steps-toodo-a-test-failover"></a>步驟 toodo 測試容錯移轉

SQL Always On 原本就不支援測試容錯移轉。 因此，我們建議下列 hello:

1. 設定[Azure Backup](../backup/backup-azure-vms.md) hello 裝載在 Azure 中的 hello 可用性群組複本的虛擬機器上。

1. 觸發 hello 復原計劃的測試容錯移轉之前, 復原 hello 備份是取自 hello 上一個步驟中的 hello 虛擬機器。

    ![從 Azure 備份還原 ](./media/site-recovery-sql/restore-from-backup.png)

1. [強制仲裁](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure)hello 從備份還原的虛擬機器中。

1. 更新 hello 接聽程式 tooan IP hello 測試容錯移轉網路中可用的 IP。

    ![更新接聽程式 IP](./media/site-recovery-sql/update-listener-ip.png)

1. 使接聽程式上線。

    ![使接聽程式上線](./media/site-recovery-sql/bring-listener-online.png)

1. 前端 IP 集區對應 tooeach 可用性群組接聽程式底下建立一個 IP 與 hello SQL 虛擬機器加入 hello 後端集區中建立負載平衡器。

     ![建立負載平衡器 - 前端 IP 集區 ](./media/site-recovery-sql/create-load-balancer1.png)

    ![建立負載平衡器 - 後端集區 ](./media/site-recovery-sql/create-load-balancer2.png)

1. 請勿 hello 復原計劃的測試容錯移轉。

### <a name="steps-toodo-a-failover"></a>步驟 toodo 容錯移轉

一旦您加入 hello 指令碼 hello 復原計劃和已驗證的 hello 復原方案中執行測試容錯移轉，您可以 hello 復原計劃的容錯移轉。


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>整合複寫 tooa 次要內部部署站台的 SQL Server Alwayson

如果 hello SQL Server 會使用高可用性 （或 FCI） 的可用性群組，建議使用 hello 復原網站上的可用性群組。 請注意這適用於不使用分散式的交易的 tooapps。

1. [設定資料庫](https://msdn.microsoft.com/library/hh213078.aspx) 。
1. Hello 次要站台上建立虛擬網路。
1. 設定站對站 VPN 連線之間 hello 虛擬網路和 hello 主要站台。
1. 虛擬機器上建立 hello 復原站台，並在其上安裝 SQL Server。
1. 擴充 hello 現有 Alwayson 可用性群組 toohello 新的 SQL Server VM。 將此 SQL Server 執行個體設定為非同步複本。
1. 建立可用性群組接聽程式，或更新 hello 現有接聽程式 tooinclude hello 非同步複本虛擬機器。
1. 請確定該 hello 應用程式伺服器陣列已設定使用 hello 接聽程式。 如果它是安裝程式使用 hello 資料庫伺服器名稱，來更新它 toouse hello 接聽程式，因此您不需要 tooreconfigure hello 容錯移轉之後。

對於使用分散式交易的應用程式，建議您使用 [VMware/實體伺服器站對站複寫](site-recovery-vmware-to-vmware.md)來部署 Site Recovery。

### <a name="recovery-plan-considerations"></a>復原計畫考量
1. 將這個範例指令碼 toohello VMM 程式庫，hello 主要和次要站台上。

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. 當您建立 hello 應用程式的復原計劃時，新增一個前置動作 tooGroup 1 已編寫指令碼的步驟，移轉可用性群組叫用 hello 指令碼 toofail。

## <a name="protect-a-standalone-sql-server"></a>保護獨立式 SQL Server

在此案例中，我們建議您使用站台復原複寫 tooprotect hello SQL Server 電腦。 hello 確切步驟取決於 SQL Server 是否 VM 或實體伺服器上，以及是否要 tooreplicate tooAzure 或次要內部部署站台。 了解 [Site Recovery 案例](site-recovery-overview.md)。

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>保護 SQL Server 叢集 (標準版/Windows Server 2008 R2)

執行 SQL Server Standard edition 或 SQL Server 2008 R2 的叢集，我們建議您針對使用站台復原複寫 tooprotect SQL Server。

### <a name="on-premises-tooon-premises"></a>在內部部署內部部署 tooon

* 如果 hello 應用程式使用分散式的交易我們建議您部署[使用 SAN 複寫的站台復原](site-recovery-vmm-san.md)HYPER-V 環境中，或[VMware/實體伺服器 tooVMware](site-recovery-vmware-to-vmware.md)的 VMware 環境。
* 非 DTC 應用程式，使用上述方法 toorecover hello 叢集 hello 做為獨立伺服器，利用本機的高安全性資料庫鏡像。

### <a name="on-premises-tooazure"></a>在內部部署 tooAzure

Site Recovery 並不提供客體叢集支援複寫 tooAzure 時。 SQL Server 也不會為 Standard Edition 提供低成本的災害復原解決方案。 在此案例中，我們建議您保護 hello 在內部部署 SQL Server 叢集 tooa 獨立 SQL Server，然後在 Azure 中進行復原。

1. Hello 在內部部署站台上設定其他的獨立 SQL Server 執行個體。
1. Hello 資料庫您，做為鏡像設定 hello 執行個體 tooserve 想 tooprotect。 在高安全性模式下設定鏡像。
1. 設定的 hello 在內部部署站台，站台復原 ([HYPER-V](site-recovery-hyper-v-site-to-azure.md)或[VMware Vm/實體伺服器)](site-recovery-vmware-to-azure-classic.md)。
1. 使用站台復原複寫 tooreplicate hello 新 SQL Server 執行個體 tooAzure。 因為這是高安全性的鏡像副本，將與 hello 主要叢集中，同步處理，但實際上會使用站台復原複寫的複寫的 tooAzure。


![標準叢集](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>容錯回復考量

SQL Server Standard 的叢集，發生未規劃的容錯移轉後容錯回復需要 SQL server 備份及還原中，從 hello 鏡像執行個體 toohello 原始叢集 reestablishment hello 鏡像的一部分。

## <a name="next-steps"></a>後續步驟
[深入了解](site-recovery-components.md) Site Recovery 架構。
