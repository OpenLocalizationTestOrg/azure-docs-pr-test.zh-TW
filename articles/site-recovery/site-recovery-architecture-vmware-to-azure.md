---
title: "Azure Site Recovery 中的 VMware 複寫 tooAzure 運作 aaaHow？ | Microsoft Docs"
description: "本文提供元件和複寫在內部部署 VMware Vm 和實體伺服器 tooAzure 以 hello Azure Site Recovery 服務時使用的架構的概觀"
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
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: f0fb834f8b251640f97e4d0163b2b9e54de691e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-vmware-replication-tooazure-work-in-site-recovery"></a>VMware 複寫 tooAzure 的運作方式在站台復原中？

本文說明 hello 元件和複寫時所涉及程序內部使用 hello VMware 虛擬機器和實體 Windows/Linux 的伺服器，tooAzure [Azure Site Recovery](site-recovery-overview.md)服務。

當您複製實體在內部部署伺服器 tooAzure 時，複寫會使用也 hello 相同元件和處理程序作為 VMware VM 複寫，但這些差異：

- 您可以使用實體伺服器 hello 組態伺服器，而不是 VMware VM。
- 您需要內部部署的 VMware 基礎結構以供進行容錯回復。 您不能容錯回復 tooa 實體機器。

張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="architectural-components"></a>架構元件

有多個元件所涉及複寫 VMware Vm 和實體伺服器 tooAzure 時。

**元件** | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | **詳細資料**
--- | --- | ---
**Azure** | 在 Azure 中，您需要 Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。 | 複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。 在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。
**組態伺服器** | 單一內部部署 (VMWare VM) 執行的管理伺服器所需的 hello 部署，包括 hello 組態伺服器、 處理序伺服器、 主要目標伺服器的所有 hello 在內部部署元件 | hello 組態伺服器元件會協調在內部部署與 Azure 之間的通訊並管理資料複寫。
 **處理序伺服器**：  | Hello 組態伺服器上的預設安裝。 | 會做為複寫閘道器。 接收複寫資料、 最佳化與快取、 壓縮和加密，並將它傳送 tooAzure 儲存體。<br/><br/> hello 處理序伺服器也會處理推入安裝的 hello 行動服務 tooprotected 機器，並執行的 VMware Vm 的自動探索。<br/><br/> 隨著您的部署，您可以加入其他個別的專用處理序伺服器 toohandle 增加磁碟區的複寫流量。
 **主要目標伺服器** | Hello 在內部部署組態伺服器上的預設安裝。 | 在從 Azure 容錯回復期間，處理複寫資料。<br/><br/> 如果容錯回復的流量很高，您可以部署個別的主要目標伺服器來供容錯回復使用。
**VMware 伺服器** | VMware Vm 上 vSphere ESXi 伺服器，以及建議的 vCenter server toomanage hello 主機。 | 您新增 VMware 伺服器 tooyour 復原服務保存庫。
**複寫的機器** | hello 行動服務將會安裝在每個 VMware 想 tooreplicate VM 上。 它可以手動安裝在每部電腦上，或從 hello 處理序伺服器推入安裝。

深入了解 hello 部署先決條件和需求的每個元件在 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)。

**圖 1: VMware tooAzure 元件**

![元件](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>複寫程序

1. 您設定 hello 部署，包含 Azure 的元件，與復原服務保存庫。 Hello 保存庫中指定 hello 複寫來源和目標，設定 hello 組態伺服器，新增 VMware 伺服器、 建立複寫原則，部署 hello 行動服務、 啟用複寫，以及執行測試容錯移轉。
2.  機器會開始複寫 hello 複寫原則，根據與 hello 資料的初始複本會複寫的 tooAzure 儲存體。
4. 在 hello 初始複寫完成後，就會開始複寫差異變更 tooAzure。 機器的追蹤變更會保存在 .hrl 檔案中。
    - 複寫機器 hello 組態與伺服器通訊連接埠 HTTPS 443 輸入複寫管理的。
    - 複寫機器複寫資料 toohello 處理序伺服器連接埠上傳送 HTTPS 9443 輸入 （可以在設定）。
    - hello 組態伺服器協調使用 Azure 的複寫管理透過 HTTPS 443 輸出連接埠。
    - hello 處理序伺服器接收資料從來源機器、 最佳化及加密，並將它 tooAzure 儲存體傳送連接埠 443 輸出。
    - 如果您啟用多重 VM 一致性，然後 hello 複寫群組中的電腦與對方進行通訊透過連接埠 20004。 如果您將多部機器群組為幾個共用當機時保持一致復原點和應用程式一致復原點的複寫群組，當這些群組在進行容錯移轉時，便會使用多部 VM。 這非常有用，如果電腦執行 hello 相同的工作負載，而且需要 toobe 一致。
5. 流量會複寫的 tooAzure 儲存體公用端點，超過 hello 網際網路。 或者，您可以使用 Azure ExpressRoute [公用對等](../expressroute/expressroute-circuit-peerings.md#public-peering)。 不支援透過站對站 VPN 從內部部署站台 tooAzure 複寫流量。

**圖 2: VMware tooAzure 複寫**

![增強](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

1. 在您確認測試容錯移轉正常運作之後，您可以視需要執行未規劃的容錯移轉 tooAzure。 不支援有計劃的容錯移轉。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)，toofail 於多個 Vm。
3. 當您執行容錯移轉時，會在 Azure 中建立複本 VM。 您從 Azure VM 的 hello 複本認可容錯移轉 toostart 存取 hello 工作負載。
4. 當主要的內部部署網站恢復可用狀態時，您就可以容錯回復。 您設定容錯回復基礎結構，開始從主要的 hello 次要站台 toohello 複寫 hello 機器，並從 hello 次要站台執行未規劃的容錯移轉。 確認此容錯移轉之後，資料將會回復在內部，並再次需要 tooenable 複寫 tooAzure。 [深入了解](site-recovery-failback-azure-to-vmware.md)

容錯回復有以下幾項需求︰


- **在 Azure 中的暫存處理序伺服器**： 如果您想 toofail 從 Azure 容錯移轉之後您將需要 tooset 設定處理序伺服器，從 Azure toohandle 複寫為 Azure vm。 容錯回復完成後，您可以刪除此 VM。
- **VPN 連線**： 您必須容錯回復的 VPN 連線 （或 Azure ExpressRoute） 設定從 hello Azure 網路 toohello 在內部部署站台。
- **另一個在內部部署主要目標伺服器**: hello 在內部部署主要目標伺服器可處理容錯回復。 hello 管理伺服器上，預設會安裝 hello 主要目標伺服器，但如果您在容錯回較大量的流量您應該設定不同內部部署主要目標伺服器針對此目的。
- **容錯回復原則**: tooreplicate 後 tooyour 內部網站，您需要容錯回復原則。 此原則會在您建立複寫原則時自動建立。
- **VMware 基礎結構**： 您必須容錯回復 tooan 內部部署 VMware VM。 這表示您需要在內部部署 VMware 基礎結構中，即使您要複寫在內部部署實體伺服器 tooAzure。

**圖 3：VMware/實體容錯回復**

![容錯回復](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>後續步驟

檢閱 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)
