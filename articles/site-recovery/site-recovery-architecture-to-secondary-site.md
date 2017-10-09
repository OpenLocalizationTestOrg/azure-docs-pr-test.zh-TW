---
title: "aaaHow 運作在內部部署機器複寫 tooa 次要內部部署網站在 Azure Site Recovery？ | Microsoft Docs"
description: "本文提供元件和複寫在內部部署 Vm 和實體伺服器 tooa 次要站台以 hello Azure Site Recovery 服務時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>如何在內部部署機器在站台復原的複寫 tooa 次要站台工作？

這篇文章描述 hello 元件和處理程序涉及複寫時在內部部署虛擬機器和實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。

您可以複製下列 tooa 次要內部部署站台的 hello:
- Hyper-V 叢集和獨立主機上在 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V VM。
- 內部部署 VMware VM 和 Windows/Linux 實體伺服器。 在此案例中，複寫是由 Scout 管理。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>複寫 HYPER-V Vm tooa 內部次要站台


### <a name="architectural-components"></a>架構元件

以下是您需要複寫 HYPER-V Vm tooa 次要站台。

**元件** | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | **詳細資料**
--- | --- | ---
**Azure** | 您需要 Microsoft 帳戶。 |
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

**圖 1: VMM tooVMM 複寫**

![在內部部署內部部署 tooon](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

1. 您可以在內部部署網站間執行計劃性或非計劃性的[容錯移轉](site-recovery-failover.md)。 如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。
4. 如果您執行未規劃的容錯移轉 tooa 次要站台之後在 hello 次要位置中的 hello 容錯移轉機器未啟用保護或複寫。 如果您已規劃的容錯移轉，執行 hello 容錯移轉之後，會受到保護 hello 次要位置中的機器。
5. 然後，您會從 hello 複本 VM 認可 hello 容錯移轉 toostart 存取 hello 工作負載。
6. 您的主要站台再次可用時，會起始反向複寫 tooreplicate 從 hello 次要站台 toohello 主要。 反轉複寫方向將 hello 虛擬機器放置到受保護的狀態，但 hello 次要資料中心仍然是 hello 作用中的位置。
7. toomake hello 主要站台到 hello 作用中的位置，您起始規劃的容錯移轉，從次要 tooprimary，後面接著另一個的反向複寫。




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>複製 VMware Vm/實體伺服器 tooa 次要站台

您複寫 VMware Vm 或實體伺服器 tooa 次要站台使用 InMage Scout，使用這些架構的元件：


### <a name="architectural-components"></a>架構元件

**元件** | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | **詳細資料**
--- | --- | ---
**Azure** | InMage Scout。 | tooobtain InMage Scout，您需要 Azure 訂用帳戶。<br/><br/> 建立復原服務保存庫之後，您會下載 InMage Scout，並安裝 hello 最新的更新 tooset hello 部署。
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

**圖 2: VMware tooVMware 複寫**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>後續步驟

檢閱 hello[支援矩陣](site-recovery-support-matrix-to-sec-site.md)
