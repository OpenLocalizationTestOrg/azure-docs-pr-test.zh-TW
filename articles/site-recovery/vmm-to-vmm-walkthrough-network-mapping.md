---
title: "HYPER-V 虛擬機器複寫 tooa 次要站台與 Azure Site Recovery 的 aaaMap 網路 |Microsoft 文件"
description: "描述如何 toomap 網路複寫 HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery 時。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>步驟 7： 對應網路的 HYPER-V 虛擬機器複寫 tooa 次要站台


設定好後[來源和目標設定](vmm-to-vmm-walkthrough-source-target.md)複寫 HYPER-V 虛擬機器 (Vm) tooa 次要 System Center Virtual Machine Manager (VMM) 站台，使用 HYPER-V 虛擬此發行項 tooconfigure 網路對應機器 (VM) 複寫 tooa 次要站台，使用[Azure Site Recovery](site-recovery-overview.md)。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

- 開始之前，深入了解[網路對應](vmm-to-vmm-walkthrough-network.md#network-mapping-overview)。
- 請確認 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。

## <a name="configure-network-mapping"></a>設定網路對應

1. 在 [網路對應] > [網路對應]，按一下 [+網路對應]。
2. 在**加入網路對應**索引標籤上，選取 hello 來源與目標 VMM 伺服器。 擷取 hello 與 hello VMM 伺服器相關聯的 VM 網路。
3. 在**來源網路**，選取您想 toouse hello 清單中的 hello 主要 VMM 伺服器相關聯的 VM 網路的 hello 網路。
4. 在**目標網路**，選取您想 toouse hello 次要 VMM 伺服器上的 hello 網路。 然後按一下 [確定] 。

    ![網路對應](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

以下是網路對應開始時發生的事情︰

* 對應 toohello 來源 VM 網路的任何現有複本虛擬機器會連接的 toohello 目標 VM 網路。
* 新的虛擬機器所連接的 toohello 來源 VM 網路在複寫之後會連接的 toohello 目標對應的網路。
* 如果您修改現有的對應與新的網路，複本虛擬機器將使用 hello 新設定連接。
* 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。



## <a name="next-steps"></a>後續步驟

跳過[步驟 8： 設定複寫原則](vmm-to-vmm-walkthrough-replication.md)。
