---
title: "VMM 和 HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 的 aaaSet |Microsoft 文件"
description: "描述如何 tooset System Center VMM 伺服器和 HYPER-V 主機複寫 tooa 次要 VMM 站台。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>步驟 4： 設定 VMM 和 HYPER-V 的 HYPER-V 虛擬機器複寫 tooa 次要站台 

您已備妥的網路功能之後，設定 System Center Virtual Machine Manager (VMM) 伺服器和 HYPER-V 主機的 HYPER-V 虛擬機器 (VM) 複寫 tooa 次要站台，使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。 

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="prepare-vmm-servers"></a>準備 VMM 伺服器 

tooprepare 部署：


1. 請確定 VMM 伺服器符合 hello[支援需求](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)，和[部署必要條件](vmm-to-vmm-walkthrough-prerequisites.md)。
2. 請確定 VMM 伺服器可以連線的 toohello 網際網路，而且有存取 toothese Url。
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。
    - 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。
    - 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。
3. 請確定 hello VMM 伺服器[準備網路對應](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>準備 Hyper-V 主機/叢集

1. 請確定 HYPER-V 主機叢集符合 hello[支援需求](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)，和[部署必要條件](vmm-to-vmm-walkthrough-prerequisites.md)。
2. 確認 hello 需求[HYPER-V Vm](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. 驗證[網路](site-recovery-support-matrix-to-sec-site.md#network-configuration)和[儲存體](site-recovery-support-matrix-to-sec-site.md#storage)需求。
4. 請確定在 HYPER-V 主機連線的 toohello 網際網路，而且有存取 toothese Url。
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。
    - 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。
    - 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。

## <a name="prepare-for-single-server-deployment"></a>準備進行單一伺服器部署


如果您只有單一 VMM 伺服器，您可以將複寫 Vm hello VMM 雲端中的 HYPER-V 主機中太[Azure](hyper-v-site-walkthrough-overview.md)或 tooa 次要 VMM 雲端，這份文件中所述。 我們建議 hello 第一個選項，因為雲端之間的複寫不順暢。

如果您想 tooreplicate 雲端之間，您可以使用單一獨立 VMM 伺服器，或複寫延展 Windows 叢集中部署一部 VMM 伺服器

### <a name="replicate-with-a-standalone-vmm-server"></a>以獨立 VMM 伺服器進行複寫

在此案例中，您為虛擬機器在 hello 主要站台部署單一 VMM 伺服器 hello 和複寫 VM tooa 此次要站台使用站台復原 」 和 「 HYPER-V 複本。

1. **在 Hyper-V VM 上設定 VMM**。 我們建議您將共置 hello hello 上使用 VMM 的 SQL Server 執行個體相同的 VM。 這可以節省時間只能有一個 VM 仍為 toobe 建立。 如果您想 toouse 遠端 SQL Server 執行個體發生中斷，您需要 toorecover 該執行個體之前，您可以復原 VMM。
2. **請 hello VMM 伺服器已設定至少兩個雲端**。 一個雲端會包含您想 tooreplicate 和 hello 其他雲端的 Vm 將做為 hello 次要位置的 hello。 hello，其中包含您想要 tooprotect 應遵守的 hello Vm 雲端[必要條件](#prerequisites)。
3. 以本文所述的方式設定 Site Recovery。 建立及註冊保存庫中的 hello VMM 伺服器、 設定的複寫原則，並啟用複寫。 hello 來源與目標 VMM 名稱將 hello 相同。 指定初始複寫會透過 hello 網路進行。
4. 當您設定網路對應會對應 hello hello 主要雲端 toohello hello 次要雲端的 VM 網路的 VM 網路。
5. 在 hello HYPER-V 管理員主控台中，包含 hello VMM VM 的 hello HYPER-V 主機上啟用 HYPER-V 複本和 hello VM 上啟用複寫。 請確定您不要新增 hello VMM 虛擬機器 tooclouds Site recovery，tooensure HYPER-V 複本設定不覆寫 Site recovery 保護。
6. 如果您建立您所使用的容錯移轉的復原計劃 hello 相同的 VMM 伺服器，來源和目標。
7. 在完全中斷運作的情況下，您進行容錯移轉和復原的方式如下︰

   1. Hello hello 次要站台中，toofail hello 主要 VMM VM toohello 次要站台上的 HYPER-V Manager 主控台中，執行未規劃的容錯移轉。
   2. 請確認 VMM VM 已啟動該 hello 並正常執行，並在 hello 保存庫 hello Vm 上執行規劃的容錯移轉 toofail 從主要 toosecondary 雲端。 認可 hello 容錯移轉，並視需要選取替代的復原點。
   3. Hello 規劃的容錯移轉完成之後，所有存取的資源可以從 hello 主要站台一次。
   4. 同樣地，在 hello hello 次要站台中的 HYPER-V Manager 主控台中可用 hello 主要站台時，啟用 hello VMM VM 的反向複寫。 這是從次要 tooprimary 開始 hello VM 的複寫。
   5. Hello hello 次要站台中，toofail hello VMM VM toohello 主要站台上的 HYPER-V Manager 主控台中執行規劃的容錯移轉。 認可 hello 容錯移轉。 再啟用反向複寫，如此 hello VMM VM 會再次從伺服器複寫主要 toosecondary。
   6. 在 hello 復原服務保存庫，讓 hello 工作負載的 Vm，從次要 tooprimary 複寫它們 toostart 的反向複寫。
   7. Hello 復原服務保存庫中，執行規劃的容錯移轉 toofail 後 hello 工作負載 Vm toohello 主要站台。 認可 hello 容錯移轉 toocomplete 它。 然後啟用反向複寫 toostart 複寫 hello 工作負載 Vm 從主要 toosecondary。

### <a name="replicate-with-a-stretched-vmm-cluster"></a>以延伸的 VMM 叢集複寫

而是作為複寫 tooa 次要站台 VM 部署獨立 VMM 伺服器，您可以讓 VMM 高可用性部署為 Windows 容錯移轉叢集中的 VM。 這可以提供工作負載彈性及硬體故障的防護。 在各地不同的站台之間，應該自動縮放叢集中部署 toodeploy 以 Site Recovery hello VMM VM。 toodo 這樣：

1. 在 Windows 容錯移轉叢集中的虛擬機器上安裝 VMM，並在安裝期間選取 hello 選項 toorun hello 伺服器為高可用性。
2. hello SQL Server 執行個體，以供 VMM 應該複寫使用 SQL Server AlwaysOn 可用性群組，使 hello hello 次要站台資料庫複本。
3. 遵循本文章 toocreate 保存庫中的 hello 指示，註冊 hello 伺服器，以及設定保護。 您需要的 tooregister hello 復原服務保存庫中的 hello 中的每部 VMM 伺服器叢集。 toodo，作用中節點上，安裝 hello 提供者，並註冊 hello VMM 伺服器。 然後您可以安裝 hello 提供者的其他節點上。
4. 發生中斷時，會容錯移轉，而且從 hello 次要站台存取 hello VMM 伺服器和其相對應的 SQL Server 資料庫。



## <a name="next-steps"></a>後續步驟

跳過[步驟 5： 設定保存庫](vmm-to-vmm-walkthrough-create-vault.md)。
