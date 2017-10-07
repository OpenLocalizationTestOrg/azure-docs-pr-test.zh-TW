---
title: "aaaCreate HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 保存庫 |Microsoft 文件"
description: "描述如何 toocreate 保存庫時複寫 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>步驟 5： 建立 HYPER-V 複寫 tooa 次要站台的保存庫

準備內部部署之後[System Center Virtual Machine Manager (VMM) 伺服器和 HYPER-V 主機叢集](vmm-to-vmm-walkthrough-vmm-hyper-v.md)HYPER-V 複寫 tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md)，您可以建立復原服務保存庫，並選取 hello 複寫案例。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>選擇保護目標

選取您想要 tooreplicate 和您想要 tooreplicate。

1. 按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [保護目標]。
2. 選取**toorecovery 網站**，然後選取**是的含 HYPER-V**。
3. 選取**是**tooindicate 您使用 VMM toomanage hello HYPER-V 主機。
4. 如果您有次要 VMM 伺服器，請選取 [是]。 如果您要在單一 VMM 伺服器上的雲端之間部署複寫，請按一下 [否] 。 然後按一下 [確定] 。

    ![選擇目標](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>後續步驟

跳過[步驟 6： 設定 hello 複寫來源和目標](vmm-to-vmm-walkthrough-source-target.md)。
