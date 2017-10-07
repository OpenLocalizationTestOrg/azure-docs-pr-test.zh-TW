---
title: "HYPER-V 虛擬機器複寫與站台復原的 aaaPlan 網路對應 |Microsoft 文件"
description: "設定 HYPER-V 虛擬機器的複寫從內部部署資料中心 tooAzure 或 tooa 次要站台的網路對應。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>使用 Site Recovery 規劃 Hyper-V VM 複寫的網路對應



這篇文章可協助您 toounderstand 和規劃的網路對應的 HYPER-V Vm tooAzure 或 tooa 次要站台的複寫期間，使用 hello [Azure Site Recovery 服務](site-recovery-overview.md)。

在讀取後這份文件張貼在 hello 下方的本文中，任何註解或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="network-mapping-for-replication-tooazure"></a>複寫 tooAzure 網路對應

當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooAzure 時，會使用網路對應。 網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 Azure 網路。 對應未 hello 遵循：

- **網路連線**— 可確保複寫的 Azure Vm 連接的 toohello 對應的網路。 容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，即使它們在不同的復原計劃中容錯移轉。
- **網路閘道**-Vm 網路閘道已設定 hello 目標 Azure 網路上，如果可以連線 tooother 在內部部署虛擬機器。

請注意：

- 您將對應的來源 VMM VM 網路 tooan Azure 虛擬網路。
- 在容錯移轉 Azure Vm 中 hello 之後來源網路就會連接的 toohello 對應的目標虛擬網路。
- 新的 Vm 加入 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。
- 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。
- 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>複寫 tooa 次要資料中心的網路對應

當複寫 (managed 在 System Center Virtual Machine Manager (VMM)) 的 HYPER-V Vm tooa 次要資料中心時，會使用網路對應。 網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 VMM 伺服器上的 VM 網路。 對應未 hello 遵循：

- **網路連線**— 容錯移轉之後連接 Vm tooappropriate 網路。 hello 複本 VM 將會是對應的 toohello 來源網路的連線的 toohello 目標網路。
- **最佳的放置**— 數位 hello HYPER-V 主機伺服器上的複本 Vm 的最佳方式。 複本 Vm 會放置在主機上，可以存取 hello 對應 VM 網路。
- **任何網路對應**— 如果您未設定網路對應，複本 Vm 容錯移轉之後將無法連接的 tooany VM 網路。

請注意：

- 網路對應可以設定兩部 VMM 伺服器上的 VM 網路之間或單一 VMM 伺服器上如果兩個站台由管理 hello 相同伺服器。
- 當正確設定對應和已啟用複寫，hello 主要位置的 VM 將會連接的 tooa 網路而它在 hello 目標位置的複本將會連接 tooits 對應網路。
-
- 如果網路有已正確設定在 VMM 中，當您在網路對應期間選取目標 VM 網路時，使用 hello 來源 VM 網路的 hello VMM 來源雲端將會顯示，以及用於 hello 目標雲端上的 hello 可用目標 VM 網路保護。
- 如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。



### <a name="example"></a>範例

以下是範例 tooillustrate 這項機制。 讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。

**位置** | **VMM 伺服器** | **VM 網路** | **對應至**
---|---|---|---
紐約 | VMM-NewYork| VMNetwork1-NewYork | 對應的 tooVMNetwork1 芝加哥
 |  | VMNetwork2-NewYork | 未對應
芝加哥 | VMM-Chicago| VMNetwork1-Chicago | 對應的 tooVMNetwork1 紐約
 | | VMNetwork1-Chicago | 未對應

在此範例中：

- 針對已連線的 tooVMNetwork1 紐約任何虛擬機器建立複本虛擬機器時，就會連接的 tooVMNetwork1 芝加哥。
- VMNetwork2 紐約或 VMNetwork2 芝加哥建立複本虛擬機器時，它將無法連接的 tooany 網路。

以下是如何在我們的範例組織中，與 hello 與 hello 雲端相關聯的邏輯網路中設定 VMM 雲端。

#### <a name="cloud-protection-settings"></a>雲端保護設定

**受保護的雲端** | **保護雲端** | **邏輯網路 (紐約)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>邏輯和 VM 網路設定

**位置** | **邏輯網路** | **相關聯的 VM 網路**
---|---|---
紐約 | LogicalNetwork1-NewYork | VMNetwork1-NewYork
芝加哥 | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>目標網路設定

根據這些設定，當您選取 hello 目標 VM 網路，hello 下表顯示的 hello 選項可供使用。

**選取** | **受保護的雲端** | **保護雲端** | **可用的目標網路**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | 可用
 | GoldCloud1 | GoldCloud2 | 可用
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | 尚未提供
 | GoldCloud1 | GoldCloud2 | 可用


如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。


#### <a name="failback-behavior"></a>容錯回復行為

toosee 怎樣 hello 案例容錯回復 （反向複寫），讓我們假設 VMNetwork1 紐約對應的 tooVMNetwork1-芝加哥，以下列設定的 hello。


**虛擬機器** | **連接的 tooVM 網路**
---|---
VM1 | VMNetwork1-Network
VM2 (VM1 的複本) | VMNetwork1-Chicago

讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。

**案例** | **結果**
---|---
Vm-2 的容錯移轉之後的 hello 網路屬性沒有變更。 | Vm-1 依然連接的 toohello 來源網路。
在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。 | VM-1 已中斷連線。
Vm-2 的網路屬性會變更容錯移轉之後，並且已連線的 tooVMNetwork2 芝加哥。 | 如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。
VMNetwork1-Chicago 的網路對應已變更。 | Vm-1 將會連接的 toohello 現在對應的網路 tooVMNetwork1 芝加哥。



## <a name="next-steps"></a>後續步驟

深入了解[規劃 hello 網路基礎結構](site-recovery-network-design.md)。
