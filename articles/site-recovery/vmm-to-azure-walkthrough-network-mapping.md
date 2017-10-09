---
title: "aaaConfigure 網路對應，複寫在 VMM 中的 HYPER-V Vm 雲端與 Azure Site Recovery tooAzure |Microsoft 文件"
description: "描述如何在 VMM 中的 HYPER-V Vm 進行複寫時，tooconfigure 網路對應雲端 tooAzure 與 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>步驟 9： 設定 HYPER-V 複寫 （VMM) tooAzure 網路對應

設定 hello 之後[來源和目標的複寫設定](vmm-to-azure-walkthrough-source-target.md)，使用此發行項 tooconfigure 網路對應 toomap 在內部部署 VMM VM 網路與 Azure 網路之間。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="before-you-start"></a>開始之前

- 深入了解[網路對應](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)。
- [準備 VMM 以進行網路對應](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping)。 
- 請確認 hello VMM 伺服器上的虛擬機器連線的 tooa VM 網路，而且您已建立至少一個 Azure 虛擬網路。 多個 VM 網路可以是對應的 tooa 單一 Azure 網路。

## <a name="configure-mapping"></a>設定對應

設定對應，如下所示︰

1. 在**Site Recovery 基礎結構** > **網路對應** > **網路對應**，按一下 hello **+ 的網路對應**圖示。

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. 在**加入網路對應**，選取 hello 來源 VMM 伺服器，和**Azure**為 hello 目標。
3. 在容錯移轉之後，請確認 hello 訂用帳戶和 hello 部署模型。
4. 在**來源網路**，選取您想要從 hello VMM 伺服器相關聯的 hello 清單 toomap hello 來源內部部署 VM 網路。
5. 在**目標網路**，選取 hello 複本 Azure 的 Vm 會位於位置在建立時即 Azure 網路。 然後按一下 [確定] 。

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

以下是網路對應開始時發生的事情︰

* Hello 來源 VM 網路上的現有 Vm 時開始對應連接的 toohello 目標網路。 新的 Vm 連接的 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。
* 如果您修改現有的網路對應，複本虛擬機器會連接使用 hello 新設定。
* 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。
* 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。



## <a name="next-steps"></a>後續步驟

跳過[步驟 10： 建立複寫原則](vmm-to-azure-walkthrough-replication.md)
