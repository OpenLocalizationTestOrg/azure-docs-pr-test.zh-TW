---
title: "HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 的 aaaReview hello 架構 |Microsoft 文件"
description: "本文章會提供用來複寫在內部部署 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery hello 架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>步驟 1： 檢閱 HYPER-V 複寫 tooa 次要站台的 hello 架構

本文說明 hello 元件和複寫時所涉及程序內部使用 hello tooa 次要 VMM 站台 System Center Virtual Machine Manager (VMM) 雲端中的 HYPER-V 虛擬機器 (Vm) [Azure Site Recovery](site-recovery-overview.md)hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="architectural-components"></a>架構元件

以下是您需要複寫 HYPER-V Vm tooa 次要 VMM 站台。

**元件** | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | **詳細資料**
--- | --- | ---
**Azure** | Azure 中的訂用帳戶。 | 您在 hello Azure 訂用帳戶，tooorchestrate 中建立的復原服務保存庫和管理 VMM 位置之間的複寫。
**VMM 伺服器** | 您需要 VMM 主要和次要位置。 | 我們建議您在 hello 主要站台 VMM 伺服器，一個在 hello 次要站台 
**Hyper-V 伺服器** |  一或多個 HYPER-V 主機伺服器 hello 主要和次要 VMM 雲端中。 | Hello LAN 或 VPN，使用 Kerberos 或憑證驗證的 hello 主要和次要 HYPER-V 主機伺服器之間複寫資料。  
**Hyper-V VM** | 在 Hyper-V 主機伺服器上。 | hello 來源主機伺服器應該有至少一個 VM 的 tooreplicate。

## <a name="replication-process"></a>複寫程序

1. 您設定 hello Azure 帳戶、 建立復原服務保存庫，並指定您想要 tooreplicate。
2. 您設定 hello 來源和目標複寫設定，包括 hello Azure Site Recovery Provider 安裝 VMM 伺服器和每個 HYPER-V 主機上的 hello Microsoft Azure 復原服務代理程式。
3. 您建立 hello 來源 VMM 雲端的複寫原則。 hello 原則會套用的 tooall 位於 hello 雲端中的主機上的 Vm。
4. 您為每個 VMM 中啟用，並會依據您選擇的 hello 設定的 VM 的初始複寫。
5. 初始複寫之後，就會開始複寫差異變更。 項目的追蹤變更會保存在 .hrl 檔案中。


![在內部部署內部部署 tooon](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

1. 您可以在內部部署網站間執行計劃性或非計劃性的[容錯移轉](site-recovery-failover.md)。 如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。
4. 如果您執行未規劃的容錯移轉 tooa 次要站台之後在 hello 次要位置中的 hello 容錯移轉機器未啟用保護或複寫。 如果您已規劃的容錯移轉，執行 hello 容錯移轉之後，會受到保護 hello 次要位置中的機器。
5. 然後，您會從 hello 複本 VM 認可 hello 容錯移轉 toostart 存取 hello 工作負載。
6. 您的主要站台再次可用時，會起始反向複寫 tooreplicate 從 hello 次要站台 toohello 主要。 反轉複寫方向將 hello 虛擬機器放置到受保護的狀態，但 hello 次要資料中心仍然是 hello 作用中的位置。
7. toomake hello 主要站台到 hello 作用中的位置，您起始規劃的容錯移轉，從次要 tooprimary，後面接著另一個的反向複寫。



## <a name="next-steps"></a>後續步驟

跳過[步驟 2： 檢閱 hello 必要條件和限制](vmm-to-vmm-walkthrough-prerequisites.md)。
