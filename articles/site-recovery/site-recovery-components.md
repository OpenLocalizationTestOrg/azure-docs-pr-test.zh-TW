---
title: "aaaHow Site Recovery 運作？ | Microsoft Docs"
description: "本文提供 Site Recovery 架構的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Azure Site Recovery 如何在內部部署基礎結構中運作？

> [!div class="op_single_selector"]
> * [複寫 Azure 虛擬機器](site-recovery-azure-to-azure-architecture.md)
> * [複寫內部部署機器](site-recovery-components.md)

這篇文章描述基礎架構 hello [Azure Site Recovery](site-recovery-overview.md)服務與支援 hello 元件，可將它用於從內部部署 tooAzure 複寫工作負載。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="replicate-tooazure"></a>複寫 tooAzure

您可以將複寫和保護內部部署基礎結構 tooAzure hello 下列：

- **VMware**︰[支援主機](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)上執行的內部部署 VMware VM。 您可以複寫執行[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)的 VMware VM
- **Hyper-V**︰[支援主機](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)上執行的內部部署 Hyper-V VM。
- **實體機器**︰[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)上執行 Windows 或 Linux 的內部部署實體伺服器。 您可以複寫 Hyper-V VM，執行 [Hyper-V 和 Azure 支援](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)的任何客體作業系統。

## <a name="vmware-tooazure"></a>VMware tooAzure

以下是您需要複寫 VMware Vm tooAzure。

領域 | 元件 | 詳細資料
--- | --- | ---
**組態伺服器** | 單一管理伺服器 (VMWare VM) 執行所有內部部署元件 - 組態伺服器、處理序伺服器、主要目標伺服器 | hello 組態伺服器協調在內部部署與 Azure 之間的通訊，並管理資料複寫。
 **處理序伺服器**：  | Hello 組態伺服器上的預設安裝。 | 會做為複寫閘道器。 接收複寫資料、 最佳化與快取、 壓縮和加密，並將它傳送 tooAzure 儲存體。<br/><br/> hello 處理序伺服器也會處理推入安裝的 hello 行動服務 tooprotected 機器，並執行的 VMware Vm 的自動探索。<br/><br/> 隨著您的部署，您可以加入其他個別的專用處理序伺服器 toohandle 增加磁碟區的複寫流量。
 **主要目標伺服器** | Hello 在內部部署組態伺服器上的預設安裝。 | 在從 Azure 容錯回復期間，處理複寫資料。<br/><br/> 如果容錯回復的流量很高，您可以部署個別的主要目標伺服器來供容錯回復使用。
**VMware 伺服器** | VMware Vm 上 vSphere ESXi 伺服器，以及建議的 vCenter server toomanage hello 主機。 | 您新增 VMware 伺服器 tooyour 復原服務保存庫。<br/><br/>
**複寫的機器** | hello 行動服務將會安裝在每個 VMware 想 tooreplicate VM 上。 它可以手動安裝在每部電腦上，或從 hello 處理序伺服器推入安裝。| -

**圖 1: VMware tooAzure 元件**

![元件](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>複寫程序

1. 您設定 hello 部署，包含 Azure 的元件，與復原服務保存庫。 Hello 保存庫中指定 hello 複寫來源和目標，設定 hello 組態伺服器，新增 VMware 伺服器、 建立複寫原則，部署 hello 行動服務、 啟用複寫，以及執行測試容錯移轉。
2.  機器會開始複寫 hello 複寫原則，根據與 hello 資料的初始複本會複寫的 tooAzure 儲存體。
4. 在 hello 初始複寫完成後，就會開始複寫差異變更 tooAzure。 機器的追蹤變更會保存在 .hrl 檔案中。
    - 複寫機器 hello 組態與伺服器通訊連接埠 HTTPS 443 輸入複寫管理的。
    - 複寫機器複寫資料 toohello 處理序伺服器連接埠上傳送 HTTPS 9443 輸入 （可以在設定）。
    - hello 組態伺服器協調使用 Azure 的複寫管理透過 HTTPS 443 輸出連接埠。
    - hello 處理序伺服器接收資料從來源機器、 最佳化及加密，並將它 tooAzure 儲存體傳送連接埠 443 輸出。
    - 如果您啟用多重 VM 一致性，然後 hello 複寫群組中的電腦與對方進行通訊透過連接埠 20004。 如果您將多部機器群組為幾個共用當機時保持一致復原點和應用程式一致復原點的複寫群組，當這些群組在進行容錯移轉時，便會使用多部 VM。 這非常有用，如果電腦執行 hello 相同的工作負載，而且需要 toobe 一致。
5. 流量會複寫的 tooAzure 儲存體公用端點，超過 hello 網際網路。 或者，您可以使用 Azure ExpressRoute [公用對等](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering)。 不支援透過站對站 VPN 從內部部署站台 tooAzure 複寫流量。

**圖 2: VMware tooAzure 複寫**

![增強](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>容錯移轉和容錯回復

1. 在您確認測試容錯移轉正常運作之後，您可以視需要執行未規劃的容錯移轉 tooAzure。 不支援有計劃的容錯移轉。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)，toofail 於多個 Vm。
3. 當您執行容錯移轉時，會在 Azure 中建立複本 VM。 您從 Azure VM 的 hello 複本認可容錯移轉 toostart 存取 hello 工作負載。
4. 當主要的內部部署網站恢復可用狀態時，您就可以容錯回復。 您設定容錯回復基礎結構，開始從主要的 hello 次要站台 toohello 複寫 hello 機器，並從 hello 次要站台執行未規劃的容錯移轉。 確認此容錯移轉之後，資料將會回復在內部，並再次需要 tooenable 複寫 tooAzure。 [深入了解](site-recovery-failback-azure-to-vmware.md)

**圖 3：VMware/實體容錯回復**

![容錯回復](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>實體 tooAzure

相同的元件和程序做為當您複製實體在內部部署伺服器 tooAzure 時，複寫會使用也 hello [VMware tooAzure](#vmware-replication-to-azure)，但請注意這些差異：

- 您可以使用實體伺服器 hello 組態伺服器，而不是 VMware VM
- 您需要內部部署的 VMware 基礎結構以供進行容錯回復。 您不能容錯回復 tooa 實體機器。

## <a name="hyper-v-tooazure"></a>HYPER-V tooAzure

### <a name="replication-process"></a>複寫程序

1. 您設定 hello Azure 元件。 我們建議您先設定儲存體和網路帳戶，再開始 Site Recovery 部署。
2. 您要建立用於 Site Recovery 的複寫服務保存庫，並設定保存庫設定，包括︰
    - 來源與目標設定。 如果您未管理的 VMM 雲端中的 HYPER-V 主機，hello 目標為您建立 HYPER-V 站台容器，並新增 HYPER-V 主機 tooit。 若在 VMM 中管理 HYPER-V 主機，hello 來源是 hello VMM 雲端。 Azure hello 目標。
    - 安裝 Azure Site Recovery Provider hello 和 hello Microsoft Azure 復原服務代理程式。 如果您有 VMM hello 會在其上安裝提供者，然後 hello 每個 HYPER-V 主機上的代理程式。 如果您不需要 VMM，hello 提供者和代理程式會安裝在每部主機上。
    - 您建立 hello HYPER-V 站台或 VMM 雲端的複寫原則。 hello 原則會套用的 tooall Vm 位於 hello 網站或雲端中的主機。
    - 您要啟用 Hyper-V VM 的複寫。 根據 hello 複寫原則設定，就會發生初始複寫。
4. 會追蹤資料變更，並複寫差異變更 tooAzure 開始 hello 初始複寫完成之後。 項目的追蹤變更會保存在 .hrl 檔案中。
5. 在您執行測試容錯移轉 toomake 確定一切運作。

### <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

1. 您可以執行的已規劃或未規劃[容錯移轉](site-recovery-failover.md)從內部部署 HYPER-V Vm tooAzure。 如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。
4. 執行 hello 容錯移轉之後，您應該在 Azure 中建立複本 Vm 可以 toosee hello。 如果需要，您可以指定公用 IP 位址 toohello VM。
5. 然後，您就會認可 hello 容錯移轉 toostart 從 hello 複本 Azure VM 存取 hello 工作負載。
6. 當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。 您開始進行規劃的容錯移轉，從 Azure toohello 主要站台。 規劃的容錯移轉，您可以選取 toofailback toohello 相同 VM 或 tooan 替代位置，並同步處理變更 Azure 和內部部署、 tooensure 之間不會遺失資料。 Vm 建立時在內部部署，您就會認可 hello 容錯移轉。

**圖 4： 使用 HYPER-V 站台 tooAzure 複寫**

![元件](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**圖 5: HYPER-V 在 VMM 中雲端 tooAzure 複寫**

![元件](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>複寫 tooa 次要站台

您可以複製下列 tooyour 次要站台的 hello:

- **VMware**︰[支援主機](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)上執行的內部部署 VMware VM。 您可以複寫執行[支援的作業系統](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)的 VMware VM
- **實體機器**︰[支援的作業系統](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)上執行 Windows 或 Linux 的內部部署實體伺服器。
- **Hyper-V**：在 VMM 雲端中進行管理之[支援 Hyper-V 主機](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)上執行的內部部署 Hyper-V VM。 [支援的主機](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). 您可以複寫 Hyper-V VM，執行 [Hyper-V 和 Azure 支援](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)的任何客體作業系統。


## <a name="vmwarephysical-tooa-secondary-site"></a>VMware/實體 tooa 次要站台

VMware Vm 或實體伺服器 tooa 次要站台使用 InMage Scout 您複寫。

### <a name="components"></a>元件

**領域** | **元件** | **詳細資料**
--- | --- | ---
**處理序伺服器** | 位於主要網站 | 您部署 hello 處理序伺服器 toohandle 快取、 壓縮和資料最佳化。<br/><br/> 它也會處理 hello 整合代理程式 toomachines 想 tooprotect 推入安裝。
**組態伺服器** | 位於次要網站 | hello 組態伺服器管理、 設定和監視您的部署，請使用 hello 管理入口網站或 hello vContinuum 主控台。
**vContinuum 伺服器** | 選用。 相同安裝在 hello 與 hello 組態伺服器的位置。 | 它會提供主控台來管理及監視您的受保護的環境。
**主要目標伺服器** | 位於 hello 次要站台 | hello 主要目標伺服器保留複寫的資料。 收到 hello 處理序伺服器的資料、 建立複本機器 hello 次要站台中，以及保存點 hello 資料保留。<br/><br/> 您需要的主要目標伺服器的 hello 數目取決於您要保護的機器的 hello 數目。<br/><br/> 如果您想 toofail 後 toohello 主要站台時，會太需要的主要目標伺服器。 hello 整合安裝代理程式在此伺服器上。
**VMware ESX/ESXi 和 vCenter 伺服器** |  VM 裝載於 ESX/ESXi 主機。 主機是使用 vCenter 伺服器進行管理 | 您需要 VMware 基礎結構 tooreplicate VMware Vm。
**VM/實體伺服器** |  整合 VMware Vm 和您想要 tooreplicate 的實體伺服器上安裝代理程式。 | hello 代理程式做為所有 hello 元件之間的通訊提供者。


### <a name="replication-process"></a>複寫程序

1. 您設定 （設定、 程序、 主要目標），每個站台的 hello 元件伺服器，而且您想 tooreplicate 機器上安裝 hello 整合代理程式。
2. 初始複寫之後，在每部電腦上的 hello 代理程式會傳送差異複寫變更 toohello 處理序伺服器。
3. hello 處理序伺服器最佳化 hello 資料，並將其 hello 次要站台上傳輸 toohello 主要目標伺服器。 hello 組態伺服器管理 hello 複寫程序。

**圖 6: VMware tooVMware 複寫**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>HYPER-V tooa 次要站台

以下是您需要複寫 HYPER-V Vm tooa 次要站台。


**領域** | **元件** | **詳細資料**
--- | --- | ---
**VMM 伺服器** | 我們建議您在 hello 主要站台 VMM 伺服器，一個在 hello 次要站台 | 每一部 VMM 伺服器應 toohello 連接的網際網路。<br/><br/> 每一部伺服器應該有至少一個 VMM 私人雲端中的，與 hello HYPER-V 功能設定檔集合。<br/><br/> Hello VMM 伺服器上安裝 hello Azure Site Recovery Provider。 hello 提供者會協調並透過 hello 協調複寫 hello 站台復原服務與網際網路。 Hello 提供者與 Azure 之間的通訊是安全而且會加密。
**Hyper-V 伺服器** |  一或多個 HYPER-V 主機伺服器 hello 主要和次要 VMM 雲端中。<br/><br/> 伺服器應 toohello 連接的網際網路。<br/><br/> Hello LAN 或 VPN，使用 Kerberos 或憑證驗證的 hello 主要和次要 HYPER-V 主機伺服器之間複寫資料。  
**Hyper-V VM** | 位於 hello 來源 HYPER-V 主機伺服器上。 | hello 來源主機伺服器應該有至少一個 VM 的 tooreplicate。

### <a name="replication-process"></a>複寫程序

1. 您設定 hello Azure 帳戶。
2. 您要建立用於 Site Recovery 的複寫服務保存庫，並設定保存庫設定，包括︰

    - hello 複寫來源和目標 （主要和次要站台）。
    - 安裝 Azure Site Recovery Provider hello 和 hello Microsoft Azure 復原服務代理程式。 hello 提供者安裝在 VMM 伺服器和每個 HYPER-V 主機上的 hello 代理程式。
    - 您要建立來源 VMM 雲端的複寫原則。 hello 原則會套用的 tooall 位於 hello 雲端中的主機上的 Vm。
    - 您要啟用 Hyper-V VM 的複寫。 根據 hello 複寫原則設定，就會發生初始複寫。
4. 會追蹤資料變更，並複寫差異變更 toobegins hello 初始複寫完成之後。 項目的追蹤變更會保存在 .hrl 檔案中。
5. 在您執行測試容錯移轉 toomake 確定一切運作。

**圖 7: VMM tooVMM 複寫**

![在內部部署內部部署 tooon](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>容錯移轉和容錯回復

1. 您可以在內部部署網站間執行計劃性或非計劃性的[容錯移轉](site-recovery-failover.md)。 如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。
4. 如果您執行未規劃的容錯移轉 tooa 次要站台之後在 hello 次要位置中的 hello 容錯移轉機器未啟用保護或複寫。 如果您已規劃的容錯移轉，執行 hello 容錯移轉之後，會受到保護 hello 次要位置中的機器。
5. 然後，您會從 hello 複本 VM 認可 hello 容錯移轉 toostart 存取 hello 工作負載。
6. 您的主要站台再次可用時，會起始反向複寫 tooreplicate 從 hello 次要站台 toohello 主要。 反轉複寫方向將 hello 虛擬機器放置到受保護的狀態，但 hello 次要資料中心仍然是 hello 作用中的位置。
7. toomake hello 主要站台到 hello 作用中的位置，您起始規劃的容錯移轉，從次要 tooprimary，後面接著另一個的反向複寫。


## <a name="next-steps"></a>後續步驟

- [進一步了解](site-recovery-hyper-v-azure-architecture.md)有關 hello HYPER-V 複寫工作流程。
- [檢查必要條件](site-recovery-prereq.md)
