---
title: "從 Azure tooVMware aaaHow toofail |Microsoft 文件"
description: "容錯移轉之後的虛擬機器 tooAzure，您可以起始容錯回復 toobring 虛擬機器回復 tooon 內部。 了解如何 toofail 回 hello 步驟。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>從 Azure tooan 在內部部署站台失敗

本文說明 toofail 從 Azure 虛擬機器 toohello 在內部部署站台所備份的虛擬機器。 遵循本文章 toofail 中的 hello 指示您的 VMware 虛擬機器或實體 Windows/Linux 的伺服器後回它們已經由容錯移轉從 hello 在內部部署站台 tooAzure 使用 hello[複寫 VMware 虛擬機器和實體伺服器與 Azure Site Recovery 的 tooAzure](site-recovery-vmware-to-azure-classic.md)教學課程。

> [!WARNING]
> 如果您有[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)，移動的 hello 的虛擬機器 tooanother 資源群組，或已刪除 hello Azure 虛擬機器，您之後就無法容錯回復。

> [!NOTE]
> 如果您無法透過 VMware 虛擬機器便無法回復 tooa hyper-v 主機。

## <a name="overview-of-failback"></a>容錯回復的概觀
容錯回復的運作方式如下。 您無法透過 tooAzure 之後，您容錯回復 tooyour 在內部部署站台幾個階段中：

1. [重新保護](site-recovery-how-to-reprotect.md)hello Azure 上的虛擬機器，讓他們在內部部署網站中啟動 tooreplicate tooVMware 虛擬機器。 在此程序進行期間，您還需要︰
    1. 設定內部部署主要目標︰Windows 主要目標 (若為 Windows 虛擬機器) 和 [Linux 主要目標](site-recovery-how-to-install-linux-master-target.md) (若為 Linux 虛擬機器)。
    2. 設定[處理序伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)。
    3. 起始[重新保護](site-recovery-how-to-reprotect.md)。 這將會關閉 hello 在內部部署虛擬機器並同步處理 hello Azure 虛擬機器的 hello 與內部資料磁碟。
5. 您在 Azure 上的虛擬機器要複寫 tooyour 在內部部署站台之後，您起始容錯移轉從 Azure toohello 在內部部署站台。

資料回失敗之後，您重新保護 hello 您容錯回復到內部部署虛擬機器，讓他們啟動 tooreplicate tooAzure。

取得快速概觀，觀賞 hello 下列關於如何從 Azure tooan 透過 toofail 內部部署站台的視訊。
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>失敗後 toohello 原始或替代位置

如果您容錯移轉 VMware 虛擬機器，您可以容錯回復 toohello 相同來源內部部署虛擬機器它是否依然存在。 在此案例中，只有 hello 變更會複寫回。 此案例稱為原始位置復原。 如果 hello 在內部部署虛擬機器不存在，hello 案例是替代位置復原。

> [!NOTE]
> 您可以只容錯回復 toohello 原始 vCenter 和組態伺服器。 您無法部署新的組態伺服器和使用它進行容錯回復。 此外，您無法加入新 vCenter toohello 現有的組態伺服器和容錯回復到 hello 新 vCenter。

#### <a name="original-location-recovery"></a>原始位置復原

如果您無法回復 toohello 原始虛擬機器時，下列條件的 hello 是必要的：
* 如果 hello 虛擬機器 vCenter server 所管理，然後 hello 主要目標 ESX 主機應該具有存取 toohello 虛擬機器的資料存放區。
* Hello 虛擬機器位於 ESX 主機，而不是由 vCenter，管理 hello 硬碟 hello 虛擬機器必須在資料存放區，然後該 hello 主要目標主機都可以存取。
* 如果您的虛擬機器位於 ESX 主機，而且不會使用 vCenter，您應該完成 hello ESX 主機的 hello 主要目標的探索之前您重新保護。 如果您要容錯回復實體伺服器，則也適用這一條件。
* 您可以容錯回復 tooa 虛擬存放區域網路 (vSAN) 或根據未經處理的裝置對應 (RDM)，如果 hello 磁碟已存在，且可供連接的 toohello 在內部部署虛擬機器的磁碟。

#### <a name="alternate-location-recovery"></a>替代位置復原
如果 hello 在內部部署虛擬機器不存在之前重新保護 hello 虛擬機器，hello 案例稱為替代位置復原。 hello 重新保護工作流程會再次建立 hello 在內部部署虛擬機器。 這也會導致下載完整資料。

* 當您無法回復 tooan 替代位置時，hello 虛擬機器會復原的 toohello 部署的 hello 主要目標伺服器的相同 ESX 主機。 hello 已使用 toocreate hello 磁碟的資料存放區會 hello 重新保護 hello 虛擬機器時所選取的相同資料存放區。
* 您可以容錯移轉只傳回 tooa 虛擬機器檔案系統 (VMFS) 資料存放區。 若您有 vSAN 或 RDM，重新保護與容錯回復將無法運作。
* 重新保護牽涉到一個大型初始資料傳輸，後面接著 hello 變更。 此程序存在是因為 hello 虛擬機器不存在於內部部署。 hello 完整的資料必須複寫回 toobe。 此重新保護作業也需要比原始位置復原更長的時間。
* 您無法容錯移轉回 toovSAN 或 RDM 為基礎的磁碟。 新的虛擬機器磁碟 (VMDK) 才能建立在 VMFS 資料存放區上。

實體機器，透過 tooAzure，失敗時可以進行容錯移轉回只為 VMware 虛擬機器 (也參考 tooas P2A2V)。 此流程會落在 hello 替代位置復原。

* Windows Server 2008 R2 SP1 的實體伺服器，不能是回失敗時保護和容錯移轉 tooAzure。
* 請確定您會發現至少一個主要目標伺服器與 hello 必要 ESX/ESXi 主機 toowhich 需要 toofail 回。

## <a name="have-you-completed-reprotection"></a>您已完成重新保護嗎？
在繼續之前，完成 hello 重新保護的步驟，以便 hello 虛擬機器都處於複寫狀態，而且您可以起始容錯移轉後 tooan 在內部部署站台。 如需詳細資訊，請參閱[如何從 Azure tooon 內部 tooreprotect](site-recovery-how-to-reprotect.md)。

## <a name="prerequisites"></a>必要條件

* 執行容錯回復時，組態伺服器必須為內部部署。 在容錯回復，hello 虛擬機器必須存在於 hello 組態伺服器資料庫，或容錯回復不成功。 因此，請確定您有排定來定期備份伺服器。 如果發生嚴重損壞，您必須以 hello toorestore hello 伺服器的容錯回復 toowork 相同的 IP 位址。
* hello 主要目標伺服器不應該有任何快照集之前觸發容錯回復。

## <a name="steps-toofail-back"></a>步驟 toofail 回

> [!IMPORTANT]
> 起始容錯回復之前，請確定您已完成的 hello 虛擬機器的保護。 hello 虛擬機器應該在受保護的狀態，而且它們的健康情況應該**確定**。 tooreprotect hello 虛擬機器，讀取[如何 tooreprotect](site-recovery-how-to-reprotect.md)。

1. 在 hello 複寫的項目頁面，選取 hello 虛擬機器，然後以滑鼠右鍵按一下它 tooselect**規劃的容錯移轉**。
2. 在**確認容錯移轉**，確認 hello 容錯移轉方向 （從 Azure)，然後選取 hello 復原點 （最新或 hello 最新應用程式一致），您想要 toouse hello 容錯移轉。 hello 應用程式一致點 hello 最新的點後面的時間，會導致部分資料遺失。
3. 容錯移轉期間，站台復原會關閉 hello Azure 上的虛擬機器。 您檢查如預期般完成容錯回復後，您可以檢查的 hello Azure 上的虛擬機器已關閉。

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>toowhat 復原點可能會失敗後的 hello 虛擬機器嗎？

容錯回復，在您有兩個選項 toofail 後 hello 虛擬機器/復原計劃。

如果您選取最新處理 hello 的時間點，所有虛擬機器將會都容錯移轉 tootheir 最新可用的點的時間。 萬一有 hello 復原計劃內的複寫群組，然後 hello 複寫群組的每個虛擬機器將容錯移轉 tooits 獨立最新的點的時間。

虛擬機器擁有至少一個復原點之後，才能予以容錯回復。 復原方案的所有虛擬機器至少要有一個復原點，您才能容錯回復此復原方案。

> [!NOTE]
> 最新復原點是損毀一致復原點。

如果您選取 hello 應用程式一致復原點時，單一虛擬機器容錯回復會復原 tooits 最新可用的應用程式一致復原點。 在複寫群組的復原計劃的 hello 情況下，每個複寫群組將會復原 tooits 一般可用的復原點。
請注意，應用程式一致復原點的時間會落後，可能會遺失資料。

### <a name="what-happens-toovmware-tools-post-failback"></a>發生什麼事 tooVMware 工具張貼錯誤後回復？

在容錯移轉 tooAzure hello VMware 工具無法在 hello Azure 虛擬機器上執行。 Windows 虛擬機器時，發生 ASR 容錯移轉期間停用 hello VMware 工具。 Linux 虛擬機器，如果 ASR 解除容錯移轉期間，安裝 hello VMware 工具。

Hello Windows 虛擬機器的容錯回復期間也會重新啟用時容錯回復 hello VMware 工具。 同樣地，linux 虛擬機器，hello VMware 工具會重新安裝 hello 機器上的容錯回復期間。

## <a name="next-steps"></a>後續步驟

容錯回復完成之後，您需要 toocommit hello 復原在 Azure 虛擬機器的虛擬機器 tooensure 會被刪除。

### <a name="commit"></a>認可
Commit 就是必要的 tooremove hello 容錯移轉從 Azure 虛擬機器。
Hello 受保護的項目，以滑鼠右鍵按一下，然後按一下**認可**。 作業會移除容錯移轉虛擬機器，在 Azure 中的 hello。

### <a name="reprotect-from-on-premises-tooazure"></a>從內部部署 tooAzure 重新保護

認可完成之後，您的虛擬機器回在 hello 在內部部署站台，但不會受到保護。 toostart tooreplicate tooAzure 同樣地，請勿 hello 遵循：

1. 在**保存庫** > **設定** > **複寫項目**，選取 hello 失敗上一步，然後按一下虛擬機器**重新保護**。
2. 指定需要使用 toobe toosend 資料回復 tooAzure hello 處理序伺服器的 hello 值。
3. 按一下**確定**toobegin hello 重新保護工作。

> [!NOTE]
> 在內部部署虛擬機器開機之後，花一些時間 hello 代理程式 tooregister 後 toohello 設定伺服器 （向上 too15 分鐘為單位）。 在此期間，重新保護便會失敗並傳回錯誤訊息，說明該 hello 代理程式未安裝。 請等候幾分鐘，然後再次嘗試重新保護。

Hello 重新保護後作業完成、 hello 虛擬機器正在複寫後 tooAzure，和您可以在容錯移轉。

## <a name="common-issues"></a>常見問題
請確定該 hello vCenter 是處於連線狀態，然後再進行容錯回復。 否則，請中斷連接磁碟，並將它們附加後 toohello 虛擬機器將會失敗。
