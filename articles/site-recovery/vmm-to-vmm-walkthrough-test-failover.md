---
title: "aaaRun 測試容錯移轉的 HYPER-V 虛擬機器複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "說明如何測試容錯移轉的 HYPER-V 虛擬機器複寫 tooa toorun 次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>步驟 10： 執行測試容錯移轉的 HYPER-V 複寫 tooa 次要站台


使用啟用為 HYPER-V 虛擬機器 (Vm) 的複寫之後[Azure Site Recovery](site-recovery-overview.md)，使用此發行項 toorun 測試容錯移轉。 測試容錯移轉會驗證該複寫是否正常運作，且不會影響您的生產環境。 


閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

- 當您正在觸發測試容錯移轉時，您可以指定 hello 網路 toowhich hello 測試複本 Vm 會連線。 [進一步了解](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery)需 hello 網路選項。
- 我們建議您不要選擇您在網路對應期間選取的網路。
- 本文章中的 hello 指示說明如何容錯移轉的單一 VM toofail。 閱讀有關[建立復原計劃](site-recovery-create-recovery-plans.md)如果您想 toofail 透過多個 Vm 在一起。
- 閱讀＜[測試容錯移轉的限制](site-recovery-test-failover-vmm-to-vmm.md#things-to-note)＞。
- hello tooa VM 指定測試容錯移轉期間的 IP 位址為 hello 規劃或未規劃的容錯移轉 （假設 hello IP 位址可供 hello 測試容錯移轉網路中） 將會收到 hello VM 的同一個 IP 位址。 如果 hello IP 位址不可用在 hello 測試容錯移轉網路，hello VM 將會收到另一個用於 hello 測試容錯移轉網路的 IP 位址。
- 如果您想 toodo 測試容錯移轉您的生產網路中的端對端網路連線電腦的完整驗證，請注意:
    - hello 主要 VM 關機時您所做 hello 測試容錯移轉。 否則，兩個 Vm hello hello 將會執行相同的身分識別與相同網路 hello 在相同的時間。 
    - 如果您進行變更 tootest Vm 時，會失去這些變更清除 hello 測試容錯移轉時。 這些變更不會複寫後 toohello 主要 VM。
    - 測試生產網路會導致 toodowntime 生產工作負載。 要求使用者不 toouse hello 應用程式時 hello 災害復原訓練正在進行中。  


## <a name="run-a-test-failover-for-a-vm"></a>執行 VM 的測試容錯移轉

1. 容錯移轉的單一 VM，toofail 中**複寫的項目**，按一下 hello VM >**測試容錯移轉**。
2. 在**測試容錯移轉**，指定如何測試 Vm 後，即可連接的 toonetworks hello 測試容錯移轉。 
3. 按一下**確定**toobegin hello 容錯移轉。 追蹤進度 hello**作業** 索引標籤。
5. 容錯移轉已完成之後，請確認該 hello 測試 Vm 啟動成功。
6. 當您完成時，按一下**清除測試容錯移轉**hello 復原計劃。
7. 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 此步驟會刪除 hello 虛擬機器和測試容錯移轉期間所建立的網路。


## <a name="next-steps"></a>後續步驟

測試過 hello 部署之後，深入了解其他類型的[容錯移轉](site-recovery-failover.md)。
