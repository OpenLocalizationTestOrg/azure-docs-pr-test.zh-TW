---
title: "aaaEnable HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "描述如何針對 HYPER-V Vm 複寫 tooa tooenable 複寫次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>步驟 9： 啟用複寫 tooa 次要站台的 HYPER-V Vm


設定好的複寫原則之後，使用此發行項 tooenable 複寫 tooa 次要 System Center Virtual Machine Manager (VMM) 站台的內部部署 HYPER-V 虛擬機器 (VM)，使用[Azure Site Recovery](site-recovery-overview.md)。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="select-vms-tooreplicate"></a>選取 Vm tooreplicate

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。 

    ![啟用複寫](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. 在**來源**、 選取 hello VMM 伺服器，和 hello 中的 hello 想 tooreplicate 的 HYPER-V 主機位於的雲端。 然後按一下 [確定] 。

    ![啟用複寫](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. 在**目標**，確認 hello 次要 VMM 伺服器和雲端。
4. 在**虛擬機器**，選取您想要從 hello 清單 tooprotect hello Vm。

    ![啟用虛擬機器保護](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

您可以追蹤進度的 hello**啟用保護**中的動作**作業** > **站台復原工作**。 之後 hello**完成保護**作業完成、 hello 初始複寫完成，且 hello 虛擬機器是否已做好容錯移轉。

請注意：

- 您也可以啟用 hello VMM 主控台中的虛擬機器的保護。 按一下**啟用保護**hello 虛擬機器內容中的 hello 工具列上 > **Azure Site Recovery**  索引標籤。
- 啟用複寫之後，您可以檢視內容 hello VM 中**複寫的項目**。 在 hello **Essentials**儀表板，您可以看到 hello hello VM 和其狀態的複寫原則的相關資訊。 如需詳細資訊，請按一下 [屬性]  。

## <a name="onboard-existing-vms"></a>加入現有的 VM

如果 VMM 中目前已經有使用 Hyper-V 複本複寫的虛擬機器，您可以使用下列方式加入它們以提供 Azure Site Recovery 複寫：

1. 請確認裝載現有 VM 的 hello hello HYPER-V 伺服器位於 hello 主要雲端，然後裝載 hello 複本虛擬機器的 hello HYPER-V 伺服器位於 hello 次要雲端。
2. 請確定 hello 主要 VMM 雲端所設定的複寫原則。
3. 啟用 hello 主要虛擬機器的複寫。 Azure Site Recovery 和 VMM 確定 hello 相同的複本主機和虛擬機器偵測到，，和 Azure Site Recovery 會重複使用，並重新建立複寫使用 hello 指定設定。


## <a name="next-steps"></a>後續步驟

跳過[步驟 10： 執行測試容錯移轉](vmm-to-vmm-walkthrough-test-failover.md)。
