---
title: "使用 Azure Site Recovery 的複寫 tooAzure 的 aaaPrerequisites |Microsoft 文件"
description: "深入了解使用 hello Azure Site Recovery 服務複寫 Vm 和實體機器 tooAzure hello 必要條件。"
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>從內部部署 tooAzure 使用站台復原的複寫的必要條件

> [!div class="op_single_selector"]
> * [從 Azure tooAzure 複寫](site-recovery-azure-to-azure-prereq.md)
> * [從內部部署 tooAzure 複寫](site-recovery-prereq.md)

Azure Site Recovery 可協助您支援業務續航力和災害復原 (BCDR) 策略可藉由協調複寫的 Azure 虛擬機器 (VM) tooanother Azure 區域。 在內部部署實體伺服器和 Vm toohello 雲端 (Azure) 或 tooa 次要資料中心，也會複寫站台復原。 如果在主要位置發生中斷，您可以容錯移轉 tooa 次要位置 tookeep 應用程式和可用的工作負載。 Hello 主要位置傳回 toonormal 作業時，您可以容錯回復 tooyour 主要位置。 如需 Site Recovery 的詳細資訊，請參閱[什麼是 Site Recovery？](site-recovery-overview.md)。

在本文中，我們摘要說明從站台復原複寫從內部部署機器 tooAzure hello 必要條件。

您可以張貼在 hello hello 文章底部的任何註解。 您也可以詢問技術問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="azure-requirements"></a>Azure 需求

**需求** | **詳細資料**
--- | ---
**Azure 帳戶** | [Microsoft Azure 帳戶](http://azure.microsoft.com/)。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
**Site Recovery 服務** | 如需定價的 hello Azure Site Recovery 服務的詳細資訊，請參閱[站台復原定價](https://azure.microsoft.com/pricing/details/site-recovery/)。 |
**Azure 儲存體** | 您需要 Azure 儲存體帳戶 toostore 複寫資料。 hello 儲存體帳戶必須在 hello 與 hello 相同區域 Azure 復原服務保存庫。 發生容錯移轉時，會建立 Azure VM。<br/><br/> 根據 hello 資源模型想 toouse Azure VM 才能容錯移轉，您可以設定帳戶使用 hello [Azure Resource Manager 部署模型](../storage/common/storage-create-storage-account.md)或 hello[傳統部署模型](../storage/common/storage-create-storage-account.md)。<br/><br/>您可以使用[異地備援儲存體](../storage/common/storage-redundancy.md#geo-redundant-storage)或本地備援儲存體。 建議使用異地備援儲存體。 使用地理備援儲存體，地區的中斷發生時，如果或 hello 主要區域無法復原，就復原資料。<br/><br/> 您可以使用標準的 Azure 儲存體帳戶，或使用 Azure 進階儲存體。 [進階儲存體](https://docs.microsoft.com/azure/storage/storage-premium-storage)通常用於需要持續有高 I/O 效能和低延遲的虛擬機器。 使用進階儲存體，虛擬機器即可裝載大量 I/O 的工作負載。 如果您使用進階儲存體來存放複寫的資料，您也需要標準儲存體帳戶。 標準儲存體帳戶會儲存擷取進行中的變更 tooon 內部部署資料的複寫記錄檔。<br/><br/>
**儲存體限制** | 您無法移動您使用站台復原 tooa 不同的資源群組中的儲存體帳戶，或移動 tooor 搭配另一個訂用帳戶。<br/><br/> 目前，複寫 toopremium 印度中部和印度南部及印度中的儲存體帳戶無法使用。
**Azure 網路** | 您需要 Azure 網路，容錯移轉之後連接 toowhich Azure Vm。 hello Azure 網路必須位於 hello hello 與相同的區域復原服務保存庫。<br/><br/> 在 hello Azure 入口網站，您可以建立 Azure 網路使用 hello [Resource Manager 部署模型](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)或 hello[傳統部署模型](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。<br/><br/> 如果您從 System Center Virtual Machine Manager (VMM) tooAzure 複寫時，您必須設定 VMM VM 網路與 Azure 網路之間的網路對應。 這可確保 Azure Vm 容錯移轉之後連接 tooappropriate 網路。
**網路限制** | 您無法移動您在站台復原 tooa 不同的資源群組中，使用的網路帳戶，或移動 tooor 搭配另一個訂用帳戶。
**網路對應** | 如果您要複寫 VMM 雲端中的 Microsoft Hyper-V VM，必須設定網路對應。 這可確保在建立時即容錯移轉之後，Azure Vm 的連線 tooappropriate 網路。

> [!NOTE]
> hello 下列章節說明各種元件的 hello 客戶環境的 hello 的必要條件。 如需支援的特定設定的詳細資訊，請參閱 hello[支援矩陣](site-recovery-support-matrix.md)。
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>VMware Vm 或實體的 Windows 或 Linux 伺服器 tooAzure 的災害復原
hello 下列元件所需的 VMware Vm 或實體的 Windows 或 Linux 伺服器的災害復原。 此外，這些是 1 中所述的 toohello [Azure 需求](#azure-requirements)。


### <a name="configuration-server-or-additional-process-server"></a>組態伺服器或其他處理伺服器

設定為 hello 組態伺服器 tooorchestrate 通訊 hello 在內部部署站台與 Azure 之間的內部部署機器。 hello 在內部部署機器也會管理資料複寫。 <br/></br>

*   **VMware vCenter 或 vSphere 主機必要條件**

    | **元件** | **需求** |
    | --- | --- |
    | **vSphere** | 您必須有一個或多個 VMware vSphere Hypervisor。<br/><br/>Hypervisor 必須執行 vSphere 版本 6.0、 5.5、 或 5.1，hello 與最新的更新。<br/><br/>我們建議，vSphere 主機和 vCenter 伺服器在 hello 中都是相同網路 hello 處理序伺服器。 除非您已設定專用處理序伺服器，這是 hello 網路 hello 組態伺服器所在的位置。 |
    | **vCenter** | 我們建議您部署 VMware vCenter server toomanage vSphere 主機。 它必須執行 vCenter 版本 6.0 或 5.5、 hello 最新的更新。<br/><br/>**限制**：Site Recovery 不支援 vCenter vMotion 執行個體之間的複寫。 在重新保護作業之後，主要目標虛擬機器亦不支援儲存體 DRS 和 Storage vMotion。||

* **複寫之機器的必要條件**

    | **元件** | **需求** |
    | --- | --- |
    | **內部部署機器** (VMware VM) | 複寫的虛擬機器必須安裝並執行 VMware 工具。<br/><br/> 虛擬機器必須符合[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)用於建立 Azure VM。<br/><br/>每部受保護的電腦上的磁碟容量不可超過 1,023 GB。 <br/><br/>Hello 安裝磁碟機上的可用空間的最少 2 GB，才能安裝元件。<br/><br/>如果您想 tooenable 多重 VM 一致性，必須開啟連接埠 20004 hello VM 本機防火牆上。<br/><br/>機器名稱的長度必須介於 1 到 63 個字元 (可使用字母、數字和連字號)。 hello 名稱必須以字母或數字開頭，並且以字母或數字結尾。 <br/><br/>啟用機器的複寫之後，您可以修改 hello Azure 的名稱。<br/><br/> |
    | **Windows 機器** (實體或 VMware) | hello 機器必須執行支援的 hello 下列其中一種 64 位元作業系統： <br/>- Windows Server 2012 R2<br/>- Windows Server 2012<br/>- Windows Server 2008 R2 SP1 或更新版本<br/><br/> hello 作業系統必須是安裝在 c 磁碟機 hello OS 磁碟必須是 Windows 基本磁碟，而非動態。 hello 資料磁碟可以是動態的。<br/><br/>|
    | **Linux 機器** (實體或 VMware) | hello 機器必須執行支援的 hello 下列其中一種 64 位元作業系統： <br/>- Red Hat Enterprise Linux 7.2、7.1、6.8 或 6.7<br/>- Centos 7.2、7.1、7.0、6.8、6.7、6.6 或 6.5<br/>- Ubuntu 14.04 LTS 伺服器 (如需支援的 Ubuntu 核心版本清單，請參閱[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>Oracle Enterprise Linux 6.5 或 6.4，執行任一 hello Red Hat 相容核心或以企業核心的第 3 版 (UEK3)<br/>- SUSE Linux Enterprise Server 11 SP4 或 SUSE Linux Enterprise Server 11 SP3<br/><br/>受保護的機器上的 /etc/hosts 檔案必須具有與所有網路介面卡相關聯的 hello 本機主機名稱 tooIP 位址對應的項目。<br/><br/>容錯移轉之後，如果您想 tooconnect tooan 使用安全殼層 (SSH) 用戶端執行 Linux 的 Azure VM，請確定 hello hello 受保護的電腦上的 SSH 服務設定 toostart 自動在系統啟動。 請確定防火牆規則允許的 SSH 連線 toohello 受保護機器。<br/><br/>hello 主機名稱、 掛接點、 裝置名稱，以及 Linux 系統路徑和檔案名稱 （例如，/etc/ 和 libodbc） 必須以英文只。<br/><br/>hello 下列目錄 (如果設定為不同的磁碟分割或檔案系統) 都必須在 hello hello 來源伺服器上的同一個磁碟 （hello OS 磁碟）：<br/>- / (根)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>目前，XFS v5 功能 (例如，中繼資料總和檢查碼) 不支援 XFS 檔案系統的 Site Recovery。 請確定 XFS 檔案系統未使用任何 v5 功能。 您可以使用 hello xfs_info 公用程式 toocheck hello XFS superblock hello 磁碟分割。 如果**ftype**設定得**1**，XFS v5 功能的使用。<br/><br/>Red Hat Enterprise Linux 7 和 CentOS 7 伺服器 hello lsof 及公用程式必須安裝並可使用。<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>HYPER-V Vm tooAzure (無 VMM) 的災害復原

hello 下列元件所需的 VMM 雲端中的 HYPER-V Vm 的災害復原。 此外，這些是 1 中所述的 toohello [Azure 需求](#azure-requirements)。

| **必要條件** | **詳細資料** |
| --- | --- |
| **Hyper-V 主機** |一或多個內部部署伺服器必須執行 Windows Server 2012 R2 與 hello 最新更新和 hello HYPER-V 角色已啟用或 Microsoft HYPER-V Server 2012 R2。<br/><br/>Hyper-V 伺服器必須有一部或多部虛擬機器。<br/><br/>HYPER-V 伺服器必須連接的 toohello 網際網路，直接或透過 proxy。<br/><br/>HYPER-V 伺服器必須擁有 hello 知識庫文章所述的 hello 修正[2961977](https://support.microsoft.com/kb/2961977)安裝。
|**Provider 和代理程式**| 在站台復原 」 部署，您可以安裝 hello Azure Site Recovery provider。 hello 安裝 「 提供者也會安裝 hello Azure 復原服務代理程式正在執行的 Vm，每部 HYPER-V 伺服器上您想 tooprotect。 <br/><br/>站台復原保存庫必須在所有 HYPER-V 伺服器都 hello 相同版的都 hello 提供者和都 hello 代理程式。<br/><br/>hello 提供者需要透過網際網路 hello tooconnect tooSite 復原。 可以直接或透過 Proxy 傳送流量。 不支援 HTTPS 型 Proxy。 hello proxy 伺服器必須允許存取 toohello 下列 Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>如果您有 hello 伺服器上的 IP 位址為基礎的防火牆規則，請確定 hello 規則允許通訊 tooAzure。<br/><br/> 允許 hello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 HTTPS （連接埠 443）。<br/><br/> 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及 hello 美國西部 （用於存取控制和身分識別管理）。


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>在 VMM 中的 HYPER-V Vm 的災害復原雲端 tooAzure

hello 下列元件所需的 VMM 雲端中的 HYPER-V Vm 的災害復原。 此外，這些是 1 中所述的 toohello [Azure 需求](#azure-requirements)。

| **必要條件** | **詳細資料** |
| --- | --- |
| **Virtual Machine Manager** |在 System Center 2012 R2 或更高版本上必須有一部或多部 VMM 伺服器正在執行。 每部 VMM 伺服器必須有一個或多個雲端。 <br/><br/>雲端必須有：<br/>- 一或多個 VMM 主機群組。<br/>- 每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。<br/><br/>如需設定 VMM 雲端的詳細資訊，請參閱[如何 toocreate Virtual Machine Manager 2012 中的雲端](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx)。 |
| **Hyper-V** |HYPER-V 主機伺服器必須至少執行 Windows Server 2012 R2 HYPER-V hello 啟用角色或 Microsoft HYPER-V Server 2012 R2。 必須安裝 hello 最新的更新。<br/><br/> Hyper-V 伺服器必須有一部或多部虛擬機器。<br/><br/> HYPER-V 主機伺服器或叢集，其中包含您想 tooreplicate Vm 必須在 VMM 雲端中管理。<br/><br/>HYPER-V 伺服器必須連接的 toohello 網際網路，直接或透過 proxy。<br/><br/>HYPER-V 伺服器必須擁有 hello 知識庫文章所述的 hello 修正[2961977](https://support.microsoft.com/kb/2961977)安裝。<br/><br/>HYPER-V 主機伺服器的資料複寫 tooAzure 需要網際網路存取。 |
| **Provider 和代理程式** |在 Azure Site Recovery 部署期間請 hello VMM 伺服器上安裝 Azure Site Recovery Provider。 在 Hyper-V 主機上安裝 Recovery Services 代理程式。 hello provider 和 agent 需要 tooconnect tooAzure hello 網際網路直接或透過 proxy。 不支援 HTTPS 型 Proxy。 hello hello VMM 伺服器和 HYPER-V 主機上的 proxy 伺服器必須允許存取： <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>如果您擁有 hello VMM 伺服器上的 IP 位址為基礎的防火牆規則，請確定 hello 規則允許通訊 tooAzure。<br/><br/> 允許 hello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS （連接埠 443）。<br/><br/>允許 hello Azure 區域，您的訂用帳戶，以及 hello 美國西部 （用於存取控制和身分識別管理） 的 IP 位址範圍。<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>複寫之機器的必要條件

| **元件** | **詳細資料** |
| --- | --- |
| **受保護的 VM** | Site Recovery 支援 [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx) 支援的所有作業系統。<br/><br/>Vm 必須符合 hello [Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)用於建立 Azure VM。 機器名稱的長度必須介於 1 到 63 個字元 (可使用字母、數字和連字號)。 hello 名稱必須以字母或數字開頭，並且以字母或數字結尾。 <br/><br/>在您啟用的 hello VM 複寫之後，您可以修改 hello VM 名稱。 <br/><br/> 每部受保護的電腦上的磁碟容量不可超過 1,023 GB。 VM 可以有向上 too16 磁碟 （向上 too16 TB)。<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>在 VMM 雲端 tooa 客戶擁有站台的 HYPER-V Vm 的災害復原

下列元件的 hello 不需要在 VMM 雲端 tooa 客戶擁有站台的 HYPER-V Vm 的災害復原。 此外，這些是 1 中所述的 toohello [Azure 需求](#azure-requirements)。

| **元件** | **詳細資料** |
| --- | --- |
| **Virtual Machine Manager** |  我們建議您部署的 hello 主要站台和 hello 次要站台上的 VMM 伺服器。<br/><br/> 您可以[在單一 VMM 伺服器上的雲端之間進行複寫](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)。 單一 VMM 伺服器上的雲端之間 tooreplicate，您需要至少兩個 hello VMM 伺服器上設定的雲端。<br/><br/> VMM 伺服器必須至少執行 System Center 2012 SP1，含 hello 最新的更新。<br/><br/> 每個 VMM 伺服器必須有一個或多個雲端。 所有雲端必須都具有 HYPER-V 容量設定檔集合的 hello。 <br/><br/>雲端必須有一個或多個 VMM 主機群組。 如需設定 VMM 雲端的詳細資訊，請參閱 [Azure Site Recovery 部署的準備](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)。 |
| **Hyper-V** | HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色啟用，而且有 hello 安裝最新的更新。<br/><br/> Hyper-V 伺服器必須有一部或多部虛擬機器。<br/><br/>  HYPER-V 主機伺服器必須位於 hello 主要和次要 VMM 雲端中的主機群組。<br/><br/> 如果您在 Windows Server 2012 R2 上，在叢集中執行 HYPER-V，我們建議您安裝知識庫文件中所述的 hello 更新[2961977](https://support.microsoft.com/kb/2961977)。<br/><br/> 如果您是在 Windows Server 2012 上的叢集中執行 Hyper-V，且您的叢集是靜態 IP 位址型叢集，則不會自動建立叢集訊息代理程式。 您必須手動設定 hello 叢集代理人。 如需 hello 叢集代理人的詳細資訊，請參閱[設定 hello 複本代理人角色叢集至叢集複寫](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。 |
| **提供者** | Site Recovery 部署期間，請在 VMM 伺服器上安裝 hello Azure Site Recovery provider。 透過 HTTPS （連接埠 443） tooorchestrate 複寫，hello 提供者進行通訊與站台復原。 Hello 主要和次要 HYPER-V 伺服器 hello LAN 上或透過 VPN 連線之間，進行資料複寫。<br/><br/> hello hello VMM 伺服器執行的提供者需要存取 toohello 下列 Url:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>hello 站台復原提供者必須允許從 hello VMM 伺服器 toohello 防火牆通訊[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，並允許 hello HTTPS （連接埠 443） 通訊協定。 |


## <a name="url-access"></a>URL 存取
這些 URL 必須可透過 VMware、VMM 和 Hyper-V 主機伺服器提供：

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **HYPER-V tooAzure** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | 允許 | 允許 | 允許 | 允許 |
|``*.backup.windowsazure.com`` | 不需要 | 允許 | 允許 | 允許 |
|``*.hypervrecoverymanager.windowsazure.com`` | 允許 | 允許 | 允許 | 允許 |
|``*.store.core.windows.net`` | 允許 | 允許 | 允許 | 允許 |
|``*.blob.core.windows.net`` | 不需要 | 允許 | 允許 | 允許 |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | 不需要 | 不需要 | 不需要 | 允許 SQL 下載 |
|``time.windows.com`` | 允許 | 允許 | 允許 | 允許|
|``time.nist.gov`` | 允許 | 允許 | 允許 | 允許 |
