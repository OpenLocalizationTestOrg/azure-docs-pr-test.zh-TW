---
title: "aaaReplicate 應用程式 (Azure tooAzure) |Microsoft 文件"
description: "本文說明如何 tooset 複寫的虛擬機器執行在一個 Azure 區域中太另一個在 Azure 中的區域。"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>將 Azure 虛擬機器 tooanother Azure 地區複寫



>[!NOTE]
>
> Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。

本文說明如何 tooset 複寫的虛擬機器正在執行一個 Azure 區域 tooanother Azure 區域中。

## <a name="prerequisites"></a>必要條件

* hello 文章假設您已經知道有關站台復原和復原服務保存庫。 您需要 toohave '復原服務保存庫' 預先建立。

    >[!NOTE]
    >
    > 建議您建立 hello 「 復原服務保存庫 」 中您想要 Vm tooreplicate hello 位置。 例如，如果您的目標位置是「美國中部」，請在「美國中部」建立保存庫。

* 如果您正在 hello Azure Vm 上使用網路安全性群組群組 (NSG) 規則或防火牆 proxy toocontrol 存取 toooutbound 網際網路連線，請確定該您白名單 hello 所需的 Url 或 Ip。 請參閱太[網路功能指南 」 文件](./site-recovery-azure-to-azure-networking-guidance.md)如需詳細資訊。

* 如果您有 ExpressRoute 或 VPN 連線在內部部署與 hello 之間來源在 Azure 中的位置，請遵循[站台復原考量 Azure tooon 內部 expressroute / VPN 組態](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration)文件。

* 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。

* 您的 Azure 訂用帳戶應啟用的 toocreate Vm hello 目標位置中您想 toouse 為 DR 區域。 您可以連絡支援 tooenable hello 必要的配額。

## <a name="enable-replication-from-azure-site-recovery-vault"></a>啟用從 Azure Site Recovery 保存庫進行複寫
此圖中，我們將會複寫在 hello '東亞' Azure 位置 toohello '東南亞' 位置中執行的 Vm。 hello 步驟如下所示：

 按一下**+ 複寫**hello hello 虛擬機器的保存庫 tooenable 複寫中。

1. **來源：**它所參考的 hello 機器，即在此情況下的原始 toohello 起點**Azure**。

2. **來源位置：**是 hello 您想 tooprotect 虛擬機器的 Azure 區域。 此圖中，對於 hello 來源位置將會是 ' 東亞 '

3. **部署模型：**它所參考的 hello 來源機器 toohello Azure 部署模型。 您可以選取其中一個傳統或資源管理員和機器屬於 toohello 特定模型會列在 hello 下一個步驟中的保護。

      >[!NOTE]
      >
      > 您只能複寫傳統的虛擬機器，並將它復原為傳統的虛擬機器。 您無法將它復原為資源管理員虛擬機器。

4. **資源群組：**它的來源虛擬機器隸屬的 hello 資源群組 toowhich。 Hello 選取的資源群組下的所有 hello Vm 將會都列出在 hello 下一個步驟中的保護。

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

在**虛擬機器 > 選取的虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定]。
    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


在 [設定] 區段下，您可以設定目標網站內容

1. **目標位置：**就 hello 位置，才能複寫虛擬機器資料來源。 視您選取的機器的位置，站台復原會提供 hello 的適當目標區域清單。

    > [!TIP]
    > 建議 tookeep 目標位置相同為準，您的復原服務保存庫。

2. **目標資源群組：**是 hello 您複寫的虛擬機器所屬的資源群組 toowhich。根據預設 ASR 會 hello 目標地區建立新的資源群組名稱有"asr"後置詞使用。 如果已經 ASR 所建立的資源群組存在，就會重複使用。您也可以選擇 toocustomize hello 一節所示。    
3. **目標虛擬網路：**根據預設，ASR 將會建立新的虛擬網路中 hello 目標區域名稱具有"asr"後置詞。 這會對應的 tooyour 來源網路，並將用於所有未來的保護。

    > [!NOTE]
    > [檢查網路的詳細資料](site-recovery-network-mapping-azure-to-azure.md)tooknow 深入了解網路對應。

4. **目標儲存體帳戶：** ASR 將會根據預設，建立 hello 新目標儲存體帳戶模擬來源 VM 存放裝置設定。 如果 ASR 建立的儲存體帳戶已經存在，就會重複使用。

5. **快取儲存體帳戶：** ASR 需要額外的儲存體帳戶稱為 hello 來源範圍中的快取儲存體。 所有 hello 智慧 hello 來源 Vm，會追蹤並傳送 toocache 儲存體帳戶之前複寫這些 toohello 目標位置的變更。

6. **可用性設定組：** ASR 會根據預設，建立新的可用性設定組 hello 目標區域中，具有"asr"後置字元的名稱。 如果 ASR 建立的可用性設定組已經存在，就會重複使用。

7.  **複寫原則：**它會定義復原點保留歷程記錄和應用程式一致快照頻率的 hello 設定。 根據預設，ASR 將對於復原點保留使用「24 小時」預設設定建立新的複寫原則，並對於應用程式一致快照集頻率使用「60 分鐘」。

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>自訂目標資源

如果您想使用 ASR toochange hello 預設值，您可以變更您的需求為基礎的 hello 設定。

1. **自訂：**按一下 toochange hello ASR 所使用的預設值。

2. **目標資源群組：**您可以從現有的 hello hello 訂用帳戶內的目標位置中的所有 hello 資源群組的 hello 清單中選取 hello 資源群組。

3. **目標虛擬網路：**您可以在 hello 目標位置找到的所有 hello 虛擬網路的 hello 清單。

4. **可用性設定組：**您只能新增可用性集合設定 toohello 虛擬機器屬於來源範圍中的可用性。

5. **目標儲存體帳戶：**

![啟用複寫](./media/site-recovery-replicate-azure-to-azure/customize.PNG)按一下**建立目標資源**及 [啟用複寫]


虛擬機器受到保護之後，您就可以檢查 hello Vm 底下的健全狀況狀態**複寫項目**

>[!NOTE]
>Hello 期間發生初始複寫的時間無法可能狀態會時間 toorefresh，和您沒有看到段時間的進度。 您可以按一下 hello 重新整理 按鈕上 hello 頂端 hello 刀鋒視窗 tooget hello 最新狀態。
>

![啟用複寫](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>後續步驟
- [深入了解](site-recovery-test-failover-to-azure.md)執行測試容錯移轉。
- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。
- 深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)tooreduce RTO。
- 深入了解容錯移轉之後[重新保護 Azure VM](site-recovery-how-to-reprotect.md)。
