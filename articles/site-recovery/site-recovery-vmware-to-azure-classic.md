---
title: "aaaReplicate VMware Vm 和中的實體伺服器 tooAzure hello 傳統入口網站 |Microsoft 文件"
description: "本文說明如何 toodeploy Azure Site Recovery tooorchestrate 複寫、 容錯移轉和復原的內部部署 VMware 虛擬機器和 Windows/Linux 實體伺服器 tooAzure。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure 複寫
> [!div class="op_single_selector"]
> * [hello Azure 入口網站](site-recovery-vmware-to-azure.md)
> * [hello 傳統入口網站](site-recovery-vmware-to-azure-classic.md)
> * [hello 傳統入口網站 （舊版）](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

hello Azure Site Recovery 服務是由協調複寫、 容錯移轉和復原的虛擬機器和實體伺服器提供 tooyour 業務續航力和災害復原 (BCDR) 策略。 電腦可以是複寫的 tooAzure 或 tooa 次要內部部署資料中心。 如需快速概觀，請參閱[什麼是 Azure Site Recovery？](site-recovery-overview.md)。

## <a name="overview"></a>概觀
這篇文章說明如何：

* **複製 VMware 虛擬機器 tooAzure**： 部署站台復原 toocoordinate 複寫、 容錯移轉和復原的內部部署 VMware 虛擬機器 tooAzure 存放裝置。
* **複寫實體伺服器 tooAzure**： 部署 Azure Site Recovery toocoordinate 複寫、 容錯移轉和復原的內部部署實體 Windows 和 Linux 伺服器 tooAzure。

> [!NOTE]
> 本文說明如何 tooreplicate tooAzure。 如果您想 tooreplicate VMware Vm 或 Windows/Linux 實體伺服器 tooa 次要資料中心，請參閱[站台復原 VMware tooVMware](site-recovery-vmware-to-vmware.md)。
>
>

將任何註解或問題張貼底部 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="enhanced-deployment"></a>增強部署
本文會包含增強的部署指示 hello Azure 傳統入口網站中。 建議您對所有新的部署使用這個版本。 如果您已部署所使用 hello 舊版舊版，我們建議您將移轉 toohello 新版本。 如需有關移轉的詳細資訊，請參閱[舊版的站台復原 VMware tooAzure 傳統](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment)。

增強的 hello 部署是一項重大更新。 以下是我們所做的 hello 加強功能摘要：

* **在 Azure 中的 Vm 沒有基礎結構**： 資料會直接複寫 tooan Azure 儲存體帳戶。 此外，沒有任何基礎結構的 Vm （例如設定伺服器或主要目標伺服器） 需要 tooset 適用於複寫和容錯移轉已 hello 舊版部署中需要。  
* **整合安裝**：單一安裝可提供內部部署元件的簡單設定及延展性。
* **安全部署**：所有流量都會加密，且複寫管理通訊會透過 HTTPS 443 傳送。
* **復原點**：支援 Windows 和 Linux 環境中的當機和應用程式一致復原點，並同時支援單一 VM 和多個 VM 一致組態。
* **測試容錯移轉**： 支援非干擾性測試容錯移轉 tooAzure，而不會影響生產環境或暫停複寫。
* **未規劃的容錯移轉**： 支援未規劃的容錯移轉 tooAzure 增強的選項 tooautomatically 與容錯移轉之前，關閉 Vm。
* **容錯回復**： 整合式容錯回復複寫差異變更回 toohello 僅內部部署站台。
* **vSphere 6.0**：有限制支援 VMware vSphere 6.0 部署。

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Site Recovery 如何協助保護虛擬機器與實體伺服器？
* VMware 系統管理員可以設定異地保護措施 tooprotect Azure 從商業工作負載和 VMware 虛擬機器上執行的應用程式。 伺服器管理員可以將內部實體 Windows 和 Linux 伺服器 tooAzure 複寫。
* hello Azure Site Recovery 主控台提供簡易的安裝和管理複寫、 容錯移轉和復原程序的單一位置。
* 如果複寫由 vCenter 伺服器管理的 VMware 虛擬機器，Site Recovery 就可以自動探索這些 VM。 如果機器 ESXi 主機上，站台復原會探索 hello 主機上的 Vm。
* 如果您是從您的內部部署基礎結構 tooAzure 執行簡單的容錯移轉，您無法從 Azure tooVMware VM hello 在內部部署站台伺服器備份 （還原）。
* 您可以設定復原方案，將分散於多部機器上的應用程式工作負載聚集起來。 如果您容錯移轉的方案時，站台復原，讓執行可以是相同的工作負載的 hello 機器一起復原 tooa 一致的資料點，就會提供多重 VM 一致性。

## <a name="supported-operating-systems"></a>受支援的作業系統
### <a name="windows-64-bit-only"></a>Windows (僅 64 位元)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (僅 64 位元)
* Red Hat Enterprise Linux 6.7、7.1 和 7.2
* CentOS 6.5、6.6、6.7、7.0、7.1 和 7.2
* Oracle 6.4 和 6.5 執行任一 hello Red Hat Enterprise Linux 相容核心或以企業核心的第 3 版 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>案例架構
案例元件：

* **在內部部署管理伺服器**: hello 管理伺服器執行復原站台元件：
  * **組態伺服器**：協調通訊和管理資料複寫與復原程序。
  * **處理序伺服器**：作為複寫閘道器。 從受保護的來源機器; 接收資料最佳化與快取、 壓縮和加密;和傳送複寫資料 tooAzure 存放區。 也會處理推入安裝的行動服務 tooprotected 機器，並執行的 VMware Vm 的自動探索。
  * **主要目標伺服器**：在從 Azure 容錯回復期間，處理複寫資料。
    您也可以部署僅作為處理序伺服器 tooscale 部署管理伺服器。
* **hello 行動服務**： 此元件部署在您想 tooreplicate tooAzure 每部電腦 （VMware VM 或實體伺服器） 上。 它會擷取 hello 機器上的資料寫入，並將它們轉送 toohello 處理序伺服器。
* **Azure**： 您不需要 toocreate，任何 Azure Vm toohandle 複寫和容錯移轉。 hello Site Recovery 服務處理資料管理，而資料會直接複寫 tooAzure 儲存體。 複寫的 Azure Vm 會調整大小會自動只 tooAzure 容錯移轉發生時。 不過，如果您想 toofail 從 Azure toohello 在內部部署站台，您必須設定 Azure VM tooact tooset 的處理序伺服器。

hello 遵循 （Henry Robalino 所建立） 的圖形會顯示這些元件之間的互動：

![元件架構](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>容量規劃
在您規劃容量時，以下是您需要 toothink 有關：

* **hello 來源環境**： 容量規劃或 hello VMware 基礎結構和來源電腦的要求。
* **hello 管理伺服器**： 規劃 hello 內部部署站台復原 」 元件執行的管理伺服器。
* **從來源 tootarget 的網路頻寬**： 規劃的 hello 來源與 Azure 之間的複寫所需的網路頻寬。

### <a name="source-environment-considerations"></a>來源環境考量
* **每日變更率上限**︰受保護的機器只能使用一個處理序伺服器。 單一處理序伺服器可以處理的 too2 TB 的資料變更每日總。 因此，2 TB 為 hello 最大的每日資料變更率支援的受保護的機器。
* **最大輸送量**： 複寫的機器可以隸屬 tooone 在 Azure 中的儲存體帳戶。 標準儲存體帳戶可以處理最多 20,000 每秒的要求，並建議您保留 hello IOPS 數目在來源機器 too20 000。 例如，如果您有 5 磁碟的來源電腦，而且每個磁碟會產生 hello 來源上的 120 IOPS （8 KB 的大小），它會在每個磁碟的 IOPS 限制為 500 hello Azure 內。 hello 所需的儲存體帳戶數目 = 總來源 IOPs/20，000。

### <a name="management-server-considerations"></a>管理伺服器考量
hello 管理伺服器會執行處理資料最佳化、 複寫和管理的站台復原元件。 它應該跨所有受保護的機器上執行的工作負載無法 toohandle hello 每日變更速率容量，而且它有足夠的頻寬 toocontinuously 備援儲存體，tooAzure 資料。 具體而言：

* hello 處理序伺服器接收複寫資料從受保護的機器，並將它與快取、 壓縮和加密，再將它傳送 tooAzure 中調整。 hello 管理伺服器應該有足夠的資源 tooperform 這些工作。
* hello 處理序伺服器會使用以磁碟為基礎的快取。 我們建議 600 GB 或更多的 toohandle 資料變更，儲存在網路瓶頸後或中斷 hello 事件不同的快取的磁碟。 在部署期間，您可以設定 hello 快取有至少 5 GB 的可用儲存空間，任何磁碟機上，而 600 GB hello 最小的建議。
* 最佳做法，我們建議該 hello 管理伺服器位於 hello 相同網路和區域網路區段，做為 hello 想 tooprotect 機器。 它可以位於不同的網路，但您想 tooprotect 應有 L3 網路可見性 tooit 機器上。

下表中的 hello 摘要 hello 管理伺服器的大小建議：

| **管理伺服器 CPU** | **記憶體** | **快取磁碟大小** | **資料變更率** | **受保護的機器** |
| --- | --- | --- | --- | --- |
| 8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz) |16 GB |300 GB |500 GB 或更少 |將管理伺服器使用這些設定 tooreplicate 少於 100 個機器的部署。 |
| 12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz) |18 GB |600 GB |500 GB too1 TB |使用這些設定 tooreplicate 100-150 機器中部署管理伺服器。 |
| 16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz) |32 GB |1 TB |1 TB too2 TB |使用這些設定 tooreplicate 150-200 機器中部署管理伺服器。 |
| 部署另一個處理序伺服器 | | |> 2 TB |如果您要複寫 200 個以上的機器，或如果 hello 每日資料變更速率超過 2TB，請部署額外的處理序伺服器。 |

其中：

* 每個來源機器已設定各 100 GB 的 3 個磁碟。
* 我們使用具有 RAID 10 的 8 個 10,000 RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。

### <a name="network-bandwidth-from-source-tootarget"></a>從來源 tootarget 的網路頻寬
請確定您計算 hello 頻寬是必要的初始複寫和差異複寫使用 hello[產能規劃工具](site-recovery-capacity-planner.md)。

#### <a name="throttling-bandwidth-used-for-replication"></a>用於複寫的節流頻寬
VMware 複寫流量 tooAzure 會經過特定處理序伺服器。 您可以節流處理 hello 頻寬可供該伺服器上的站台復原複寫，如下所示：

1. 開啟 Microsoft Azure 備份 MMC 嵌入式管理單元的 hello hello 主要管理伺服器上，或管理伺服器上執行其他佈建程序伺服器。 根據預設，hello 桌面上建立捷徑的 Microsoft Azure 備份。 您也可以在 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin 中找到它。
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。

    ![節流頻寬變更屬性](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. 在 hello**節流**索引標籤上，指定可用於站台復原的複寫和 hello 適用排程的 hello 頻寬。

    ![節流頻寬複寫](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

您也可以使用 PowerShell 設定節流。 以下是範例：

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>最大化頻寬使用量
Azure Site Recovery 所使用的複寫 tooincrease hello 頻寬，您需要 toochange 登錄機碼。

hello 下列索引鍵的控制項 hello 每個磁碟的複寫，複寫時所使用的執行緒數目：

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 在超量佈建的網路中，此登錄機碼必須 toobe 從其預設值變更。 我們支援最多 32 個。  

如需容量規劃的詳細資訊，請參閱 [Site Recovery Capacity Planner](site-recovery-capacity-planner.md)。

### <a name="additional-process-servers"></a>額外處理序伺服器
如果您需要 tooprotect 200 個以上的電腦或每日的變更率大於 2 TB，您可以新增其他伺服器 toohandle hello 負載。 tooscale 外的，您可以：

* 增加 hello 管理伺服器的數目。 例如，您可以保護 too400 兩部管理伺服器的電腦。
* 新增額外的處理序伺服器，然後使用這些 toohandle 流量，而不是 （或其他） hello 的管理伺服器。

下表描述案例，其中：

* 您為設定伺服器設定 hello 原始的管理伺服器 toouse。
* 您設定額外的處理序伺服器。
* 設定受保護的虛擬機器 toouse hello 額外的處理序伺服器。
* 每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。

| **原始管理伺服器**<br/><br/>(組態伺服器) | **額外處理序伺服器** | **快取磁碟大小** | **資料變更率** | **受保護的機器** |
| --- | --- | --- | --- | --- |
| 8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)，16 GB RAM |4 個 vCPU (2 個插槽 * 2 核心 @ 2.5GHz)，8 GB RAM |300 GB |250 GB 或更少 |您可以複寫 85 部或更少的機器。 |
| 8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)，16 GB RAM |8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)，12 GB RAM |600 GB |250 GB too1 TB |您可以複寫 85-150 部機器。 |
| 12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)，18 GB RAM |12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)，24 GB RAM |1 TB |1 TB too2 TB |您可以複寫 150-225 部機器。 |

如何調整伺服器取決於相應增加或相應放大模型的喜好設定。 您部署幾個高階管理和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。 例如： 如果您需要 tooprotect 220 機器，您可以執行 hello 下列其中一項：

* Hello 原始的管理伺服器設定與 12 Vcpu 18 GB 的 RAM。 設定具有 12 個 vCPU 和 24 GB RAM 的額外處理序伺服器。 設定受保護的機器 toouse 唯一 hello 額外的處理序伺服器。
* 設定兩部管理伺服器 （2 x 8 Vcpu、 16 GB 的 RAM） 和兩個額外的處理序伺服器 （1 x 8 Vcpu、 4vCPUs x 1 toohandle 135 + 85 (220) 機器）。 設定受保護的機器 toouse 只有 hello 額外的處理序伺服器。

請依照下列中的 hello 指示[部署額外的處理序伺服器](#deploy-additional-process-servers)tooset 額外的處理序伺服器。

## <a name="before-you-start-deployment"></a>開始部署之前
hello 表摘要說明在 hello 部署這個案例的必要條件。

### <a name="azure-prerequisites"></a>Azure 必要條件
| **必要條件** | **詳細資料** |
| --- | --- |
| **Azure 帳戶** |您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 如需 Site Recovery 價格的詳細資訊，請參閱 [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)。 |
| **Azure 儲存體** |您需要 Azure 儲存體帳戶 toostore 複寫資料。 複寫的資料會儲存在 Azure 儲存體，容錯移轉時會啟動 Azure VM。 <br/><br/>您需要一個[標準異地備援儲存體帳戶](../storage/storage-redundancy.md#geo-redundant-storage)。 hello 與 hello Site Recovery 服務相同的區域並 hello 與相關聯 hello 帳戶必須屬於相同訂用帳戶。 複寫 toopremium 儲存體帳戶目前不支援和不應使用。<br/><br/>我們不支援移動使用 hello 所建立的儲存體帳戶[Azure 入口網站](../storage/storage-create-storage-account.md)跨越資源群組。 如需詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/storage-introduction.md)。<br/><br/> |
| **Azure 網路** |您需要將連接 Azure Vm 的 Azure 虛擬網路 toowhen 容錯移轉，就會發生。 hello Azure 虛擬網路必須在 hello 與 hello Site Recovery 保存庫相同的區域。<br/><br/>toofail tooAzure 容錯移轉之後，您需要 VPN 連線 （或 Azure ExpressRoute） 設定從 hello Azure 網路 toohello 在內部部署站台。 |

### <a name="on-premises-prerequisites"></a>內部部署必要條件
| **必要條件** | **詳細資料** |
| --- | --- |
| **管理伺服器** |您需要在虛擬機器或實體伺服器上執行的內部部署 Windows 2012 R2 伺服器。 所有 hello 在內部部署站台復原元件會安裝此管理伺服器上。<br/><br/> 我們建議您部署高可用性的 VMware VM 的 hello 伺服器。 從 Azure 容錯回復 toohello 在內部部署站台一律是不論是否容錯 Vm 或實體伺服器 tooVMware Vm。 如果您未設定 hello 管理伺服器作為 VMware VM，您需要有個別的主要目標伺服器 tooset 作為 VMware VM tooreceive 容錯回復流量。<br/><br/>hello 伺服器不能在網域控制站。<br/><br/>hello 伺服器應該具有靜態 IP 位址。<br/><br/>hello hello 伺服器主機名稱應該是 15 個字元或更少。<br/><br/>應該只有英文 hello 作業系統地區設定。<br/><br/>hello 管理伺服器需要網際網路存取。<br/><br/>您需要從 hello 伺服器對外存取，如下所示： hello Site Recovery 元件 (toodownload MySQL); 在安裝期間在 HTTP 80 上的暫時存取權持續對外存取 HTTPS 443 上進行複寫管理;持續對外存取 HTTPS 9443 上 （可以修改此連接埠） 的複寫流量。<br/><br/> 請確定這些 Url 已從 hello 管理伺服器存取： <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>如果您有 hello 伺服器上的 IP 位址為基礎的防火牆規則，請檢查 hello 規則允許通訊 tooAzure。 您需要 tooallow hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)和 hello HTTPS (443) 連接埠。 您也需要 toowhitelist IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部。 hello URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")是下載 MySQL。 |
| **VMware vCenter/ESXi 主機** |您需要一或多個 VMware vSphere ESX/ESXi hypervisor 管理 VMware 虛擬機器執行 ESX/ESXi 6.0、 5.5、 或 5.1 版與 hello 最新的更新。<br/><br/> 我們建議您部署 VMware vCenter server toomanage ESXi 主機。 它應執行 vCenter 版本 6.0 或 5.5 與 hello 最新的更新。<br/><br/>請注意，Site Recovery 不支援新的 vCenter 和 vSphere 6.0 功能，例如跨 vCenter vMotion、虛擬磁碟區和儲存體 DRS。 也是 5.5 版中可用的有限的 toofeatures 站台復原支援。 |
| **受保護的機器** |**Azure**<br/><br/>您要讓 tooprotect 都應該符合機器[Azure 的必要條件](site-recovery-prereq.md)建立 Azure Vm。<br><br/>如果您想 tooconnect toohello Azure Vm 容錯移轉之後，您會需要 tooenable hello 本機防火牆上的遠端桌面連線。<br/><br/>受保護機器上的個別磁碟容量不可超過 1023 GB。 VM 可以有向上 too64 磁碟 （因此向上 too64 TB)。 如果您有容量大於 1 TB 的磁碟，請考慮使用資料庫複寫，例如 SQL Server Always On 或 Oracle Data Guard。<br/><br/>Hello 元件安裝的安裝磁碟機上的可用空間的最少 2 GB。<br/><br/>不支援共用磁碟客體叢集。 如果您有叢集部署，請考慮使用資料庫複寫，例如 SQL Server Always On 或 Oracle Data Guard。<br/><br/>不支援整合可延伸韌體介面 (UEFI)/可延伸韌體介面 (EFI) 開機。<br/><br/>機器名稱應包含介於 1 到 63 個字元 (字母、數字和連字號)。 hello 名稱必須以字母或數字開頭，並以字母或數字結尾。 受保護電腦之後，您可以修改 hello Azure 的名稱。<br/><br/>**VMware VM**<br/><br>您需要 tooinstall VMware vSphere PowerCLI 6.0。 hello 管理伺服器 （組態伺服器）。<br/><br/>VMware Vm 想 tooprotect 應該已安裝並執行的 VMware 工具。<br/><br/>如果 NIC 小組 hello 來源 VM，則會轉換 tooa tooAzure 容錯移轉之後的單一 NIC。<br/><br/>如果受保護的 Vm 有 iSCSI 磁碟時，站台復原轉換 hello 受保護 VM 的 iSCSI 磁碟到 VHD 檔案 hello VM 容錯移轉 tooAzure 時。 如果 iSCSI 目標可到達的 hello Azure VM，它將連接 tooiSCSI 目標和基本上查看兩個磁碟： hello hello Azure VM，hello 來源 iSCSI 磁碟上的 VHD 磁碟。 在此情況下，您需要 toodisconnect hello iSCSI 目標出現在 hello 上容錯移轉 Azure VM。<br/><br/>如需有關 hello VMware 使用者權限的站台復原需要請參閱[VMware vCenter 的存取權限](#vmware-permissions-for-vcenter-access)。<br/><br/> **Windows Server 機器 (位於 VMware VM 或實體伺服器上)**<br/><br/>hello 伺服器應執行支援的 64 位元作業系統： Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 在最低 SP1。<br/><br/>hello 作業系統應該安裝在 C 磁碟機，和 hello OS 磁碟應該是 Windows 基本磁碟。 （hello OS 不應該安裝在 Windows 動態磁碟上）。<br/><br/>針對 Windows Server 2008 R2 機器，您需要 toohave.NET Framework 3.5.1 安裝。<br/><br/>您需要 tooprovide 系統管理員帳戶 （必須是 hello Windows 電腦上的本機系統管理員） hello 推入安裝 hello 行動服務在 Windows 伺服器上。 如果 hello 提供帳戶是在非網域帳戶，您會需要 toodisable hello 本機電腦上的遠端使用者存取控制。 如需詳細資訊，請參閱[安裝 hello 行動服務推入安裝](#install-the-mobility-service-with-push-installation)。<br/><br/>Site Recovery 支援具有 RDM 磁碟的 VM。 在容錯回復，Site Recovery 會重複使用 hello RDM 磁碟，如果原始來源 VM hello 和 RDM 磁碟可供使用。 如果它們都無法使用，在容錯回復期間，Site Recovery 會為每個磁碟建立新的 VMDK 檔案。<br/><br/>**Linux 機器**<br/><br/>您需要支援的 64 位元作業系統： Red Hat Enterprise Linux 6.7;Centos 6.5、 6.6 或 6.7;6.4 或 6.5 hello Red Hat 相容核心或以企業核心的第 3 版 (UEK3); 執行 oracle Enterprise LinuxSUSE Linux Enterprise Server 11 SP3。<br/><br/>受保護的機器上的 /etc/hosts 檔案應該包含所有網路介面卡相關都聯的 hello 本機主機名稱 tooIP 位址對應的項目。 <br/><br/>如果您想 tooconnect tooan Azure 虛擬機器執行 Linux 使用安全殼層用戶端 (ssh)，容錯移轉之後請 hello 受保護的電腦上的 hello Secure Shell 服務設定在系統開機時自動 toostart 和防火牆規則允許 ssh連接 tooit。<br/><br/>可以只啟用保護 Linux 機器 hello 下列儲存體： 檔案系統 （EXT3、 ETX4、 ReiserFS、 XFS）;多重路徑軟體裝置對應程式 （多重路徑）。大量管理員 (LVM2)。 不支援使用 HP CCISS 控制站儲存體的實體伺服器。 只有在 SUSE Linux Enterprise Server 11 SP3 上支援 hello ReiserFS 檔案系統。<br/><br/>Site Recovery 支援具有 RDM 磁碟的 VM。 適用於 Linux 的容錯回復，在站台復原不會重複使用 hello RDM 磁碟。 而是會針對每個對應的 RDM 磁碟建立新的 VMDK 檔案。 |

僅適用於 Linux VM： 確定您已設定 hello disk.enableUUID=true 設定在 hello hello VMware 中的 VM 組態參數。 如果此列不存在，請新增它。 這是必要的 tooprovide 一致的 UUID toohello VMDK，讓它正確掛載。 如果沒有此設定，即使 hello VM 內部容錯回復時，會導致完整下載。 新增此設定會確保只有差異變更才會在容錯回復期間傳送回來。

## <a name="step-1-create-a-vault"></a>步驟 1：建立保存庫
1. 登入 toohello [Azure 入口網站](https://manage.windowsazure.com/)。
2. 展開 [資料服務]  >  [復原服務]，然後按一下 [Site Recovery 保存庫]。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
6. 按一下 [建立保存庫] 。
    ![建立保存庫](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

請檢查已成功建立 hello 保存庫的 hello 狀態列 tooconfirm。 hello 保存庫會列為**Active**上主要的 hello**復原服務**頁面。

## <a name="step-2-set-up-an-azure-network"></a>步驟 2：設定 Azure 網路
設定 Azure 網路，讓 Azure Vm 將會連接的 tooa 網路容錯移轉之後，並使錯誤後回復 toohello 內部部署站台可以如預期般運作。

1. 在 hello Azure 入口網站，選取 **建立虛擬網路**並指定 hello 網路名稱、 IP 位址範圍，以及子網路名稱。
2. 如果您需要 toodo 容錯回復，新增 VPN/ExpressRoute toohello 網路。 VPN/ExpressRoute 可以加入容錯移轉之後，即使 toohello 網路。

如需 Azure 網路的詳細資訊，請參閱[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。

> [!NOTE]
> [移轉網路](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間不支援的網路用來部署站台復原。
>
>

## <a name="step-3-install-hello-vmware-components"></a>步驟 3： 安裝 hello VMware 元件
如果您想 tooreplicate VMware 虛擬機器，請遵循下列步驟 hello 管理伺服器上：

1. [下載](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) 並安裝 VMware vSphere PowerCLI 6.0。
2. 重新啟動伺服器 hello。

## <a name="step-4-download-a-vault-registration-key"></a>步驟 4：下載保存庫註冊金鑰
1. 從 hello 管理伺服器上，開啟 hello Site Recovery 主控台在 Azure 中。 在 hello**復原服務**頁面上，按一下 hello 保存庫 tooopen hello**快速入門**頁面。 您也可以開啟 hello**快速入門**hello 圖示，即可隨時頁面。

    ![快速啟動圖示](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. 在 hello**快速入門**頁面上，按一下**準備目標資源** > **下載註冊金鑰**。 hello 註冊檔會自動產生。 該金鑰在產生後會維持五天有效。

## <a name="step-5-install-hello-management-server"></a>步驟 5： 安裝 hello 管理伺服器
> [!TIP]
> 請確定這些 Url 已從 hello 管理伺服器存取：
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. 在 hello**快速入門**頁面上，下載 hello 一致的安裝檔案 toohello 伺服器。
2. 執行 hello 安裝檔案 toostart 安裝程式在 hello **Site Recovery 整合安裝程式**精靈。
3. 在**開始之前**，選取**hello 組態伺服器與處理序伺服器安裝**。

   ![開始之前](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. 在**第三方軟體授權**，按一下 **我接受**toodownload 並安裝 MySQL。

    ![協力廠商軟體](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. 在**註冊**，瀏覽並選取您下載 hello 保存庫中的 hello 註冊金鑰。

    ![註冊](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. 在**網際網路設定**，指定如何 hello hello 組態伺服器上執行的提供者會連線透過網際網路 hello tooAzure 站台復原。

   * 如果您想 tooconnect 要與目前在 hello 機器設定的 hello proxy 時，選取**利用現有的 proxy 設定連線**。
   * 若要直接 hello 提供者 tooconnect，選取**不使用 proxy 直接連線**。
   * 如果 hello 現有 proxy 需要驗證，或是您想要 hello 提供者連接 toouse 自訂 proxy，請選取**使用自訂 proxy 設定連線**。
     * 如果您使用自訂 proxy，您必須 toospecify hello 位址、 連接埠，以及認證。
     * 如果您使用 proxy，您應該已經允許下列 Url 的 hello:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![防火牆](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. 在**必要條件檢查**，安裝程式會執行檢查 toomake 確定 hello 安裝可以執行。

    ![必要條件](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     如果出現有關 hello 警告**通用時間同步處理檢查**，驗證 hello 系統時鐘的 hello 時間 (**日期和時間**設定) hello 相同與 hello 時區。

     ![時間同步問題](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. 在**MySQL 組態**，建立認證登入 toohello MySQL 伺服器執行個體將會安裝。

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. 在**環境詳細資料**，選取是否要 tooreplicate VMware Vm。 如果是的話，安裝程式會檢查是否已安裝 PowerCLI 6.0。

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. 在**安裝位置**，選取您想 tooinstall hello 二進位檔和 hello 快取儲存。 您可以選取至少有 5 GB 可用磁碟空間的磁碟機，但我們建議快取磁碟機至少有 600 GB 的可用空間。

   ![安裝位置](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. 在**網路選取項目**，指定 hello 接聽程式 （網路介面卡和 SSL 連接埠） 的 hello 組態伺服器可以傳送和接收複寫資料。 您可以修改 hello 預設連接埠 (9443)。 在加法 toothis 連接埠，會由協調複寫作業的網頁伺服器使用連接埠 443。 請勿使用 443 來接收複寫流量。

    ![網路選擇](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. 在**摘要**，檢閱 hello 資訊，然後按一下**安裝**。 安裝完成時，會產生複雜密碼。 在您啟用複寫時會需要它，所以請將它複製並保存在安全的位置。

   ![摘要](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> 必須設定 hello Microsoft Azure 復原服務代理程式 proxy。
> Hello 安裝完成之後，請從 hello Windows [開始] 功能表中啟動 hello Microsoft Azure 復原服務介面。 在 hello 命令視窗中開啟，執行下列命令 tooset hello 的 proxy 伺服器設定組的 hello。
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>從 hello 命令列執行安裝程式
您也可以執行 hello 統一的精靈從 hello 命令列，如下所示：

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

其中：

* / ServerMode：必要。 指定 hello 安裝是否應該安裝 hello 組態和處理序伺服器或 hello 程序僅限伺服器 （使用的 tooinstall 額外的處理序伺服器）。 輸入值：CS、PS
* InstallDrive：必要。 指定要安裝 hello 元件 hello 資料夾。
* /MySQLCredFilePath。 必要。 指定 hello 路徑 tooa 檔案 hello MySQL 伺服器認證的儲存位置。 收到 hello 範本 toocreate hello 檔案。
* /VaultCredFilePath。 必要。 Hello 保存庫認證檔案的位置。
* /EnvType。 必要。 安裝類型。 值：VMware、NonVMware。
* /PSIP 和 /CSIP。 必要。 Hello 處理序伺服器和組態伺服器 IP 位址。
* /PassphraseFilePath。 必要。 Hello 複雜密碼檔案的位置。
* /ByPassProxy。 選用。 指定連接不使用 proxy tooAzure hello 管理伺服器。
* /ProxySettingsFilePath。 選用。 指定自訂的 proxy (預設 proxy 需要驗證，hello 伺服器上) 或是自訂 proxy 設定。

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>步驟 6： 設定 hello vCenter 伺服器的認證
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

hello 處理序伺服器可以自動探索 vCenter server 所管理的 VMware Vm。 自動探索，站台復原需求的帳戶和認證可存取 hello vCenter 伺服器。 如果您只是複寫實體伺服器，則這無關緊要。

tooset hello 帳戶和認證：

1. 在 hello vCenter 伺服器上，建立角色 (**Azure_Site_Recovery**) 層級 hello vCenter 以 hello[必要的權限](#vmware-permissions-for-vcenter-access)。
2. 指派 hello **Azure_Site_Recovery**角色 tooa vCenter 使用者。

   > [!NOTE]
   > VCenter 使用者帳戶具有 hello 唯讀角色可以執行容錯移轉，而不會關閉受保護的來源機器。 如果您想 tooshut 關閉這些機器，您將需要 hello Azure_Site_Recovery 角色。 如果您只從 VMware tooAzure 移轉 Vm，不需要回 toofail hello 唯讀角色便已足夠。
   >
   >
3. tooadd hello 帳戶，開啟**cspsconfigtool**。 它會充當 hello 桌面上的捷徑，位在 hello [安裝位置] \home\svsystems\bin 資料夾時。
4. 在 hello**管理帳戶**索引標籤上，按一下 **新增帳戶**。

    ![新增帳戶](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. 在**帳戶詳細資料**，新增認證可以使用的 tooaccess hello vCenter 伺服器。 可能需要超過 15 分鐘的 hello 帳戶名稱 tooappear hello 入口網站中。 立即按一下 tooupdate**重新整理**上 hello**設定伺服器** 索引標籤。

    ![詳細資料](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>步驟 7：新增 vCenter 伺服器和 ESXi 主機
如果您要複寫 VMware Vm，您需要 tooadd vCenter 伺服器 （或 ESXi 主機）。

1. 在 hello**伺服器** > **設定伺服器**索引標籤上，選取**新增 vCenter server**。

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. 加入 hello vCenter server 或 ESXi 主機詳細資料，您指定 tooaccess hello vCenter 伺服器在 hello 先前步驟中，並將使用的 toodiscover hello vCenter server 所管理的 VMware Vm 的 hello 處理序伺服器 hello 帳戶 hello 名稱。 hello vCenter server 或 ESXi 主機應位於相同網路與 hello 伺服器處理序伺服器已安裝在哪些 hello hello。

   > [!NOTE]
   > 如果您要加入 hello vCenter server 或帳戶 hello vCenter 或主機伺服器上沒有系統管理員權限的 ESXi 主機，請確定 hello vCenter 或 ESXi 帳戶已啟用這些權限： 資料中心、 資料存放區、 資料夾、 Jost，網路資源、 虛擬機器，以及 vSphere 分散式交換器。 hello vCenter server 必須啟用權限的 hello 儲存檢視表。
   >
   >

    ![新增 vCenter 伺服器](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. 完成探索之後，hello vCenter 伺服器就會列在 hello**設定伺服器** 索引標籤。

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>步驟 8：建立保護群組
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

保護群組的虛擬機器邏輯群組或實體伺服器，您想要 tooprotect hello 相同保護設定。 套用保護設定 tooa 保護群組中，而這些設定套用的 tooall 機器 （虛擬或實體） 您新增 toohello 群組。

1. 跳過**受保護項目** > **保護群組**按一下 hello 圖示 tooadd 保護群組。

    ![建立保護群組](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. 在 hello**指定保護群組設定**頁面上，指定 hello 群組的名稱。 在 hello**從**下拉式清單中，選取 hello 想 toocreate hello 群組的組態伺服器。 [目標] 是 Microsoft Azure。

    ![保護群組設定](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. 在 hello**指定複寫設定**頁面上，設定將用於所有 hello 機器 hello 群組中的 hello 複寫設定。

    ![保護群組複寫](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **多重 VM 一致性**： 如果您開啟此選項，它會 hello 保護群組中的 hello 電腦上建立共用的應用程式一致復原點。 當 hello 保護群組中的所有電腦都在都執行這項設定就非常重要 hello 相同的工作負載。 所有機器將都會復原的 toohello 相同的資料點。 無論您是複寫 VMware VM 或實體伺服器 (Windows/Linux)，這都可以使用。
   * **RPO 臨界值**： 集 hello RPO。 Hello 持續資料保護複寫超過 hello 設定 RPO 臨界值時，會產生警示。
   * **復原點保留**： 指定 hello 保留視窗。 受保護的電腦可以是復原 tooany 這個視窗內的點。
   * **應用程式一致的快照頻率**：指定每隔多久建立包含應用程式一致快照集的復原點。

當您選取 hello 核取記號時，您指定的 hello 名稱建立保護群組。 此外，第二個保護群組建立 hello 名稱*保護群組名稱*-容錯回復。 如果您無法回復 toohello 在內部部署站台容錯移轉 tooAzure 之後，會使用此保護群組。 您可以監視 hello 保護群組建立在 hello**受保護項目**頁面。

## <a name="step-9-install-hello-mobility-service"></a>步驟 9： 安裝 hello 行動服務
hello 中啟用保護的虛擬機器和實體伺服器的第一個步驟是 tooinstall hello 行動服務。 您可以使用兩種方式執行此動作：

* 自動推入，並從 hello 處理序伺服器的每部機器上安裝 hello 服務。 當您新增機器 tooa 保護群組，且它們已在執行適當版本的 hello 行動服務時，將不會發生推入安裝。 您可以使用您的企業發送方法，例如 WSUS 或 System Center Configuration Manager，也會自動安裝 hello 服務。 請確定您已設定 hello 管理伺服器之前執行這項操作。
* 您想 tooprotect 每部機器上手動安裝 hello 服務。 請確定您已設定 hello 管理伺服器之前執行這項操作。

### <a name="install-hello-mobility-service-with-push-installation"></a>安裝 hello 行動服務推入安裝
當您新增機器 tooa 保護群組時，hello 行動服務會自動推入，並且由 hello 處理序伺服器安裝在每部電腦上。

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>準備在 Windows 機器上自動推入
hello 處理序伺服器可以自動安裝 tooprepare Windows 電腦，因此，hello 行動服務：

1. 建立該 hello 處理序伺服器可以使用 tooaccess hello 機器帳戶。 hello 帳戶應擁有系統管理員權限 （本機或網域）。 這些認證只用於 hello 行動服務推入安裝。

   > [!NOTE]
   > 如果您不使用網域帳戶，您必須 toodisable hello 本機電腦上的遠端使用者存取控制。 toodo，hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System，底下的登錄中新增 hello DWORD 項目 LocalAccountTokenFilterPolicy 的值是 1 下。 開啟命令 tooadd hello 登錄項目從 CLI，或使用 PowerShell，輸入 **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 。
   >
   >
2. 您想 tooprotect hello 機器上的 Windows 防火牆，請選取**允許的應用程式或功能通過防火牆**，並啟用**檔案及印表機共用**和**Windows 管理檢測**。 針對屬於 tooa 網域的機器，您可以設定 hello 防火牆原則的 GPO。

   ![防火牆設定](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. 加入您所建立的 hello 帳戶：

   * 開啟 **cspsconfigtool**。 它會充當 hello 桌面上的捷徑，位在 hello [安裝位置] \home\svsystems\bin 資料夾時。
   * 在 hello**管理帳戶**索引標籤上，按一下 **新增帳戶**。
   * 新增您所建立的 hello 帳戶。 您將加入 hello 帳戶之後，您將需要 tooprovide hello 認證新增機器 tooa 保護群組。

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>準備在 Linux 伺服器上自動推入
1. 請確定您想要支援 tooprotect 中所述的 hello Linux 機器[在內部部署必要條件](#on-premises-prerequisites)。 請確認有網路連線之間 hello 機器想 tooprotect 和 hello 執行 hello 處理序伺服器的管理伺服器。
2. 建立該 hello 處理序伺服器可以使用 tooaccess hello 機器帳戶。 hello 帳戶應為 hello 來源 Linux 伺服器上的根使用者。 這些認證只用於 hello 行動服務推入安裝。

   * 開啟 **cspsconfigtool**。 它會充當 hello 桌面上的捷徑，位在 hello [安裝位置] \home\svsystems\bin 資料夾時。
   * 在 hello**管理帳戶**索引標籤上，按一下 **新增帳戶**。
   * 新增您所建立的 hello 帳戶。 您將加入 hello 帳戶之後，您將需要 tooprovide hello 認證新增機器 tooa 保護群組。
3. 請檢查該 hello /etc/hosts 檔案 hello 來源 Linux 伺服器包含 hello 與所有網路介面卡相關聯的本機主機名稱 tooIP 位址對應的項目上。
4. 您想 tooprotect hello 機器上安裝 hello 最新的 openssh、 openssh 伺服器和 openssl 封裝。
5. 請確定 SSH 已啟用且正在連接埠 22 上執行。
6. 啟用 hello sshd_config 檔案中的 SFTP 子系統和密碼驗證，如下所示：

   * 以 root 的身分登入。
   * 在 hello /etc/ssh/sshd_config 檔案中，尋找開頭為 PasswordAuthentication hello 列。
   * Hello 行取消註解，並將變更從 hello 值**沒有**太**是**。
   * 尋找 hello 行開頭為**子系統**和 hello 行取消註解。

     ![沒有子系統的 Linux 覆寫預設值](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>手動安裝 hello 行動服務
C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository hello 安裝程式可用。

| 來源作業系統 | 行動服務安裝檔案 |
| --- | --- |
| Windows Server (僅限 64 位元) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4、6.5、6.6 (僅限 64 位元) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Windows server 上手動安裝 hello 行動服務
1. 下載並執行 hello 相關的安裝程式。
2. 在 [開始之前] 中，選取 [行動服務]。

    ![行動服務安裝](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. 在**組態伺服器詳細資料**、 指定 hello hello 管理伺服器的 IP 位址和 hello 安裝 hello 管理伺服器元件時所產生的複雜密碼。 您可以藉由執行擷取 hello 複雜密碼 **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello 管理伺服器上。

    ![行動服務](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. 在**安裝位置**、 保留 hello 預設位置，然後按一下 **下一步**toobegin 安裝。
5. 在**安裝進度**，請檢查安裝並重新啟動 hello 機器，如果出現提示。

您也可以輸入下列文字 hello 命令列的 hello 安裝：

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

在上述命令 hello:

* /Role：必要。 指定是否要安裝 hello 行動服務。
* /InstallLocation：必要。 指定 tooinstall hello 服務的位置。
* /PassphraseFilePath：必要。 指定 hello 組態伺服器的複雜密碼。
* /LogFilePath：必要。 指定 hello 記錄檔安裝程式檔案位置。

#### <a name="uninstall-hello-mobility-service-manually"></a>手動解除安裝 hello 行動服務
您可以使用解除安裝 hello 行動服務**解除安裝或變更程式**在控制台中，或使用 hello 命令列。

hello 命令 toouninstall 行動服務使用 hello 命令列是：

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>變更 hello hello 管理伺服器的 IP 位址
執行 hello 精靈之後，您可以變更 hello hello 管理伺服器的 IP 位址，如下所示：

1. 開啟 hello 檔案 hostconfig.exe （位於 hello 桌面）。
2. 在 hello **Global**索引標籤上，變更 hello hello 管理伺服器的 IP 位址。

   > [!NOTE]
   > 只有 hello IP 位址變更 hello 管理伺服器。 管理伺服器通訊的 hello 連接埠號碼必須是 443，及**使用 HTTPS**必須左啟用。 請勿變更 hello 複雜密碼。
   >
   >

    ![管理伺服器 IP 位址](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>在 Linux 伺服器上手動安裝 hello 行動服務
1. 複製 hello 適當 tar 檔案解壓縮封存 toohello Linux 機器，您會想 tooprotect。 請參閱底下的 hello 表格[手動安裝 hello 行動服務](#install-the-mobility-service-manually)toodetermine 哪些 tar 檔案解壓縮封存您應該使用。
2. 開啟殼層程式，並執行擷取 hello 壓縮的 tar 封存 tooa 本機路徑：`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. 建立名為 passphrase.txt hello 本機目錄 toowhich 解壓縮 hello hello tar 檔案解壓縮的封存內容。 toodo，複製 hello 複雜密碼 C:\ProgramData\Microsoft Azure 站台 Recovery\private\connection.passphrase hello 管理伺服器上，並將它儲存在 passphrase.txt 執行 *`echo <passphrase> >passphrase.txt`*  hello shell 中。
4. 輸入下列命令的 hello 安裝 hello 行動服務：*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. 指定 hello 內部 IP 位址的 hello 管理伺服器，並確定已選取連接埠 443。

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>從 hello 命令列安裝 hello 行動服務

Hello 複雜密碼複製 hello 管理伺服器上的 C:\Program Files (x86) \InMage Systems\private\connection 並將它儲存為"passphrase.txt"hello 管理伺服器上。 然後，執行下列命令的 hello。 在本例中，hello 管理伺服器的 IP 位址為 104.40.75.37 且 hello HTTPS 連接埠為 443:

tooinstall 實際執行伺服器上：

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall hello 主要目標伺服器上：

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>步驟 10：對機器啟用保護
tooenable 保護，將虛擬機器和實體伺服器 tooa 保護群組。 開始之前，請注意 hello 下列，如果您要保護 VMware 虛擬機器：

* VMware Vm 會探索每隔 15 分鐘，而且可能需要超過 15 分鐘，tooappear hello Site Recovery 入口網站中探索之後。
* Hello （例如 VMware 工具安裝） 的虛擬機器上的環境變更也可能需要超過 15 分鐘 toobe 更新 Site Recovery 中。
* 您可以檢查 hello 上次探索時間 VMware vm 在 hello**上次連絡時間**欄位 hello vCenter server/ESXi 主機上 hello**設定伺服器** 索引標籤。
* 如果您加入 vCenter Server 或 ESXi 主機在建立保護群組之後，可能需要超過 15 分鐘 hello Azure Site Recovery 入口網站 toorefresh 和 hello 中所列的虛擬機器 toobe**加入機器 tooa 保護群組** 對話方塊。
* 如果您想要立即 tooproceed 並加入機器 tooa 保護群組，而不需等待 hello 已排程的探索，反白顯示 hello 組態伺服器 （但不要按），按一下 **重新整理**。

此外：

* 建議您架構保護群組，使其反映您的工作負載。 例如，加入執行特定應用程式 toohello 機器相同的群組。
* 當您新增機器 tooa 保護群組時，hello 處理序伺服器會自動將推入，並安裝 hello 行動服務，如果尚未安裝。 您必須備妥 hello 上一個步驟中所述的 toohave hello 推入機制。

### <a name="add-machines-tooa-protection-group"></a>新增機器 tooa 保護群組

1. 跳過**受保護項目** > **保護群組** > **機器** > **加入機器**.
2. 如果您要保護 VMware 虛擬機器中**選取虛擬機器**，選取您的虛擬機器 （或 hello EXSi 主機正在執行），來管理的 vCenter 伺服器，然後選取 hello 機器。

    ![對虛擬機器啟用保護](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. 如果您要保護實體伺服器，在**選取虛擬機器**，開啟 hello**加入實體機器**精靈並提供 hello IP 位址及易記的名稱。 然後，選取 hello 作業系統系列。

   ![啟用保護實體伺服器](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. 在**指定目標資源**，選取您所使用的複寫的 hello 儲存體帳戶，然後選取是否 hello 設定適用於所有工作負載。 目前不支援進階儲存體帳戶。

   > [!NOTE]
   > 我們不支援移動使用 hello 所建立的儲存體帳戶[Azure 入口網站](../storage/storage-create-storage-account.md)跨越資源群組。                           
   > [移轉儲存體帳戶](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶，或跨訂用帳戶不支援用來部署站台復原的儲存體帳戶。
   >
   >

    ![進行目標設定](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. 在**指定帳戶**，選取 hello 帳戶[設定](#install-the-mobility-service-with-push-installation)toouse hello 行動服務的自動安裝。

    ![指定帳戶](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. 按一下 hello 核取記號 toofinish 加入機器 toohello 保護群組和 toostart 初始複寫的每一部機器。

   > [!NOTE]
   > 如果已備妥推入安裝，hello 行動服務會自動安裝不需要它時它們加入 toohello 保護群組的電腦上。 Hello 服務安裝後，保護工作會啟動，而且會失敗。 Hello 失敗之後，您將需要 toomanually 何時在每一部機器 hello 安裝行動服務的重新啟動。 Hello 重新啟動之後，hello 保護工作會重新開始計算，以及發生初始複寫。
   >
   >

您可以監視狀態 hello**作業**頁面。

![在 [hello 作業] 頁面上的監視狀態](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

您也可以在 [受保護的項目] > 「保護群組名稱」 > [虛擬機器] 中監視保護狀態。 初始複寫完成，而且資料已同步處理之後，電腦狀態變更太**保護**。

![在 [受保護的項目] 中監視狀態](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>步驟 11：設定受保護機器屬性
1. 在機器進入 [受保護] 狀態之後，您可以設定其容錯移轉屬性。 Hello 保護群組詳細資料中，選取 hello 電腦及開啟 hello**設定** 索引標籤。
2. Site Recovery 會自動建議 hello Azure VM 的屬性，並偵測到 hello 內部網路設定。

    ![設定虛擬機器屬性](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. 您可以變更這些設定：

   * **Azure VM 名稱**： 這是會獲得 toohello 機器在 Azure 中容錯移轉之後的 hello 名稱。 hello 名稱必須符合 Azure 需求。
   * **Azure VM 大小**: hello 網路介面卡的數目取決於 hello 大小由您指定的 hello 目標虛擬機器。 如需有關大小和配接器的詳細資訊，請參閱 hello[大小資料表](../virtual-machines/linux/sizes.md)。 請注意：

     * 當開啟 hello，當您修改 hello 大小的虛擬機器，並儲存 hello 設定時，將會變更 hello 網路介面卡數目**設定** 索引標籤 hello 下一次。 hello 的目標虛擬機器上的網路介面卡的最小數目為等於 toohello 的來源虛擬機器上的網路介面卡的最小數目。 hello 的網路介面卡數目上限取決於 hello hello 虛擬機器大小。
       * Hello 來源電腦上的網路介面卡的 hello 數目是否小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
       * 如果 hello hello 來源虛擬機器介面卡的數目超過 hello hello 目標大小所允許的數目，將會使用 hello 目標大小最大值。
        例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但支援 hello 目標大小僅支援一個，hello 目標機器必須只有一個介面卡。
     * 如果 hello 虛擬機器有多張網路介面卡，為所有配接器應該連接的 toohello 相同的 Azure 網路。
   * **Azure 網路**： 您必須指定 Azure Vm 將會連接的 tooafter 容錯移轉的 Azure 網路。 如果您未指定其中一個，hello Azure Vm 不是連接的 tooany 網路。 此外，如果您想要從 Azure toohello 在內部部署站台 toofailback 需要 toospecify Azure 網路。 容錯回復需要 Azure 網路與內部部署網路之間的 VPN 連線。
   * **Azure IP 位址/子網路**： 每個網路介面卡，選取 hello 子網路 toowhich hello Azure VM 應該連接。 請注意，是否 hello hello 來源機器的網路介面卡設定的 toouse 靜態 IP 位址，您可以指定 hello Azure VM 的靜態 IP 位址。 如果您未指定靜態 IP 位址，則會配置任何可用的 IP 位址。 如果指定 hello 目標 IP 位址，但它已在使用 Azure 中的其他 vm，容錯移轉將會失敗。 如果已設定的 toouse DHCP hello hello 來源機器的網路介面卡，您必須 DHCP 做為 Azure 的 hello 設定。      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>步驟 12：建立復原計畫並執行容錯移轉
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

您可以執行單一電腦的容錯移轉，或者您可以容錯移轉執行相同工作或執行 hello hello 的多部虛擬機器相同的工作負載。 透過多個 toofail 機器 hello 在相同時間，將其加入 tooa 復原計劃。

toocreate 復原計劃：

1. 在 hello**復原計劃**頁面上，按一下**加入復原方案**並加入復原方案。 指定 hello 計劃的詳細資料，然後選取**Azure**為 hello 目標。

 ![設定復原計畫](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. 在**選取虛擬機器**，選取保護群組，然後選取 hello 群組 tooadd toohello 復原計劃中的 機器。

 ![新增虛擬機器](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

您可以自訂 hello 計劃 toocreate 群組與機器 hello 復原計劃中的容錯移轉順序 hello 順序。 您也可以加入進行手動動作的指令碼和提示。 您可以手動建立指令碼，或使用 [Azure 自動化 Runbook](site-recovery-runbook-automation.md) 來建立指令碼。 如需有關自訂復原方案的詳細資訊，請參閱[建立復原方案](site-recovery-create-recovery-plans.md)。

## <a name="run-a-failover"></a>執行容錯移轉
在執行容錯移轉之前：

* 請確定該 hello 管理伺服器正在執行，而且可用。 否則容錯移轉會失敗。
* 如果執行非計劃性容錯移轉：

  * 如果可能的話，您應該在執行非計劃性容錯移轉之前關閉主要機器。 這可確保您不需要在 hello 執行這兩個 hello 來源與複本機器相同的時間。 如果您要複寫 VMware Vm，當您執行非計劃性容錯移轉時，您可以指定站台復原應該嘗試 tooshut hello 來源機器關閉。 根據 hello hello 主要站台狀態，這可能會或可能無法運作。 如果您是複寫實體伺服器，則 Site Recovery 不提供此選項。
  * 非計劃性容錯移轉會停止從主要機器的資料複寫，讓任何資料差異不會在開始非計劃性容錯移轉之後傳送。
  * 如果您想在 Azure 中 tooconnect toohello 複本虛擬機器在容錯移轉之後，啟用遠端桌面連線 hello 來源電腦上執行 hello 容錯移轉之前。 然後允許通過防火牆 hello 的 RDP 連線。 您還需要在容錯移轉之後 tooallow RDP hello 公用端點的 hello Azure 虛擬機器上。 請遵循[最佳做法](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)RDP 的運作方式在容錯移轉之後的 tooensure。

> [!NOTE]
> tooget hello 達到最佳效能時執行的容錯移轉 tooAzure，請確定您已在 hello 受保護的電腦上安裝 hello Azure 代理程式。 這有助於更快的 hello 電腦開機，以及可協助診斷問題。 hello Azure 代理程式是供[Linux](https://github.com/Azure/WALinuxAgent)和[Windows](http://go.microsoft.com/fwlink/?LinkID=394789)。
>
>

### <a name="run-a-test-failover"></a>執行測試容錯移轉
執行測試容錯移轉 toosimulate 您容錯移轉和復原處理程序在隔離網路，並不會影響您的生產環境，並可讓一般複寫中繼續正常。 測試容錯移轉是 initiatd hello 來源上的，您可以透過幾種方式中執行它：

* **未指定 Azure 網路**： 虛擬機器啟動，並正確地顯示在 Azure 中，如果您執行測試容錯移轉不使用網路時，會檢查 hello 測試。 虛擬機器無法容錯移轉之後連接的 tooan Azure 網路。
* **指定 Azure 網路**: hello 整體複寫環境如預期般出現，以及 Azure 虛擬機器會連接的 toohello 指定網路，這種類型的容錯移轉會檢查。

toorun 測試容錯移轉：

1. 在 hello**復原計劃**頁面上，選取 hello 計劃，並按一下**測試容錯移轉**。

 ![選取 hello 計劃](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. 在**確認測試容錯移轉**，選取**無**tooindicate hello 測試容錯移轉，不要 toouse Azure 網路，或選取 hello 網路 toowhich hello 測試 Vm 將會容錯移轉之後連接。 按一下 hello 核取記號 toostart hello 容錯移轉。

 ![選取](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. 監視 hello 容錯移轉進度**作業** 索引標籤。

 ![監視進度](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在**虛擬機器**hello Azure 入口網站中。 如果您想 tooinitiate RDP 連線 toohello Azure VM，您將需要 tooopen 連接埠 3389 hello VM 端點上。
5. 之後完成之後，當容錯移轉到達 hello**完成**測試階段中，按一下**完成測試**toofinish。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。
6. 按一下**hello 測試容錯移轉已完成**tooautomatically 清理 hello 測試環境。 這個動作完成之後，將會顯示 hello 測試容錯移轉**完成**狀態。 會刪除任何項目或 hello 測試容錯移轉期間自動建立的 Vm。 如果測試容錯移轉的持續時間超過兩週，它會被強制 toofinish。

### <a name="run-an-unplanned-failover"></a>執行非計劃性容錯移轉
未規劃的容錯移轉從 Azure 起始，並可以執行，即使 hello 主要站台無法使用。

1. 在 hello**復原計劃**頁面上，選取 hello 計劃，並按一下**容錯移轉** > **規劃的容錯移轉**。

 ![選取 hello 計劃](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. 如果您要複寫的 VMware 虛擬機器，您可以嘗試 tooshut 向內部部署 Vm。 這是最佳的動作，並容錯移轉可讓您繼續 hello 工作成功與否。 如果不成功，錯誤詳細資料會出現在 hello**作業**索引標籤底下**未規劃的容錯移轉工作**。

 ![內部部署 VM 的關閉選項](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > 如果您是複寫實體伺服器，則這個選項無法使用。 您將需要 tootry tooshut 的向下手動的話。
 >
 >

3. 在**確認容錯移轉**，確認 hello 容錯移轉方向 (tooAzure)，然後選取您想 toouse hello 容錯移轉的 hello 復原點。 如果您在設定複寫屬性時，您可以啟用多部 VM，您可以復原 toohello 最新應用程式或損毀一致的復原點。 您也可以選取**自訂復原點**toorecover tooan 稍早的時間點。 按一下 hello 核取記號 toostart hello 容錯移轉。

 ![確認容錯移轉方向](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. 等候 hello 規劃的容錯移轉作業 toofinish。 您可以監視 hello 容錯移轉進度**作業** 索引標籤。即使未規劃的容錯移轉期間發生錯誤，hello 復原方案執行，直到完成為止。 您也應該可以 toosee hello 複本 Azure 的機器會出現在**虛擬機器**hello Azure 入口網站中。

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>連接 tooreplicated Azure 虛擬機器在容錯移轉之後
tooconnect tooreplicated 在 Azure 虛擬機器在容錯移轉之後，您需要：

- Hello 主要電腦上啟用遠端桌面連線。
- Hello 主要機器上的 Windows 防火牆設定 tooallow RDP。
- RDP 加入 toohello hello Azure 虛擬機器的公用端點。

如需此設定的相關資訊，請參閱[使用 ASR 容錯移轉之後針對遠端桌面連線進行疑難排解](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)。

## <a name="deploy-additional-process-servers"></a>部署額外處理序伺服器
如果您必須部署向外延展您超過 200 的來源機器，或總每日的變換率超過 2 TB，您將需要額外的處理序伺服器 toohandle hello 流量磁碟區。 安裝額外的處理序伺服器中的核取 hello 需求 tooset[額外的處理序伺服器](#additional-process-servers)，並根據 toohello hello 處理序伺服器然後設定遵循指示進行。 您設定好 hello 伺服器之後，您可以設定來源機器 toouse 它。

### <a name="set-up-an-additional-process-server"></a>設定額外處理序伺服器
設定額外處理序伺服器，如下所示：

* 處理序伺服器只能執行 hello 整合精靈 tooconfigure 管理伺服器。
* 如果您想要 toomanage 資料複寫只 hello 新處理序伺服器，您需要 toomigrate 受保護的機器。

### <a name="install-hello-process-server"></a>安裝 hello 處理序伺服器
1. 在 hello**快速入門**頁面上，下載 hello Site Recovery 之元件安裝的 hello 一致的安裝檔案。 執行安裝程式。
2. 在**開始之前**，選取**新增額外的處理序伺服器 tooscale 出部署**。

 ![新增處理序伺服器](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. 完成 hello 精靈，您可以如同時您[設定](#step-5-install-the-management-server)hello 第一部管理伺服器。
4. 在**組態伺服器詳細資料**輸入 hello hello 安裝 hello 組態伺服器上原始管理伺服器的 IP 位址，然後輸入 hello 複雜密碼。 如果您沒有 hello 複雜密碼，執行 **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello 原始的管理伺服器 tooretrieve 上它。

 ![組態伺服器詳細資料](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>移轉機器 toouse hello 新處理序伺服器
1. 開啟**設定伺服器** > **伺服器** > *hello 原始的管理伺服器的名稱* >  **伺服器的詳細資料**。

 ![伺服器詳細資料](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. 在 hello**處理序伺服器**清單中，選取**變更處理序伺服器**想 toochange 的下一個 toohello 伺服器。

 ![更新 hello 處理序伺服器](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. 選取**變更處理序伺服器**，選取**目標處理序伺服器**，，然後選取 hello 新的管理伺服器。 然後就會處理選取的 hello hello 新處理序伺服器的虛擬機器。 按一下 hello 資訊圖示 tooget hello 伺服器資訊。 hello 平均每個選取的虛擬機器 toohello 新處理序伺服器是您進行載入決策顯示的 toohelp tooreplicate 所需的空間。 按一下 hello 核取記號 toostart 複寫 toohello 新處理序伺服器。

 ![變更 hello 處理序伺服器](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>vCenter 存取的 VMware 權限
hello 處理序伺服器可以自動探索 Vm vCenter server 上。 tooperform 自動探索，您會需要 toodefine 角色 (Azure_Site_Recovery) 在 hello vCenter 層級 tooallow Site Recovery tooaccess hello vCenter 伺服器。 如果您只需要 toomigrate VMware 機器 tooAzure，而且不需要從 Azure toofailback，您可以定義唯讀的角色具有足夠。 中所述設定 hello 權限[步驟 6： 設定 hello vCenter 伺服器的認證](#step-6-set-up-credentials-for-the-vcenter-server)。 下表中的 hello 摘要 hello 角色權限：

| **角色** | **詳細資料** | **權限** |
| --- | --- | --- |
| Azure_Site_Recovery 角色 |VMware VM 探索 |指派 hello v Center 伺服器的這些權限：<br/><br/>資料存放區：配置空間、瀏覽資料存放區、低階檔案作業、移除檔案、更新虛擬機器檔案<br/><br/>網路：網路指派<br/><br/>資源： 指派虛擬機器 tooresource 集區、 移轉電源已關閉虛擬機器、 移轉開機的虛擬機器<br/><br/>工作：建立工作、更新工作<br/><br/>虛擬機器  > 組態<br/><br/>虛擬機器 > 互動 > 回答問題、裝置連接、設定 CD 媒體、設定磁碟片媒體、關閉電源、開啟電源、VMware 工具安裝<br/><br/>虛擬機器 > 清查 > 建立、註冊、取消註冊<br/><br/>虛擬機器 > 佈建 > 允許虛擬機器下載、允許虛擬機器檔案上傳<br/><br/>虛擬機器 > 快照集 > 移除快照集 |
| vCenter 使用者角色 |VMware VM 探索/容錯移轉而不關閉來源 VM |指派 hello v Center 伺服器的這些權限：<br/><br/>資料中心物件 > 傳播 tooChild 物件，角色 = 唯讀 <br/><br/>hello 使用者指派 hello 資料中心層級，因此具有存取 tooall hello 物件中的 hello 資料中心。 如果您想要 toorestrict hello 存取時，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （ESX 主機、 datastores、 Vm 及網路） 的物件。 |
| vCenter 使用者角色 |容錯移轉和容錯回復 |指派 hello v Center 伺服器的這些權限：<br/><br/>資料中心物件-傳播 toochild 物件，角色 = Azure_Site_Recovery<br/><br/>hello 使用者會在資料中心層級指派，因此具有存取 tooall hello 物件中的 hello 資料中心。  如果您想要 toorestrict hello 存取時，指派 hello * * 不允許存取 * * 角色以 hello**傳播 toochild 物件**toohello 子物件 （ESX 主機、 datastores、 Vm 及網路）。 |

## <a name="third-party-software-notices-and-information"></a>第三方廠商軟體注意事項和資訊
<!--Do Not Translate or Localize-->

hello 軟體和韌體中執行 hello Microsoft 產品或服務為基礎，或納入 hello 從資料列下方 （以下合稱 「 第三方程式碼 」） 的專案。  Microsoft 為 hello 不原始作者的 hello 協力廠商程式碼。  hello 原始著作權聲明與授權，在其下 Microsoft 接收這類協力廠商程式碼，會設定制定下方。

區段 A 中的 hello 資訊關於元件 hello 專案從下面所列的第三方廠商程式碼。 Such licenses and information are provided for informational purposes only.  此第三方廠商程式碼正在 relicensed 的 tooyou microsoft 在 Microsoft 軟體授權條款的 hello Microsoft 產品或服務。  

節 B 中的 hello 資訊有關第三方廠商程式碼元件所進行可用 tooyou microsoft hello 原始授權條款。

hello 完整的檔案可能位於 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428)。 Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>後續步驟
[深入了解錯誤後回復](site-recovery-failback-azure-to-vmware-classic.md)toobring 您在 Azure 中執行的容錯移轉機器回 tooyour 在內部部署環境。
