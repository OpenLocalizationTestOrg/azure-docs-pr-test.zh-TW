---
title: "測試容錯移轉的 HYPER-V 複寫 （而不使用 System Center VMM) tooAzure aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉的 HYPER-V Vm 複寫 tooAzure 使用 hello Azure Site Recovery 服務的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>步驟 11： 執行測試容錯移轉的 HYPER-V 複寫 tooAzure

本文說明如何 toorun 測試容錯移轉從內部部署 HYPER-V 虛擬機器 （不受 System Center VMM） tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="before-you-start"></a>開始之前

執行測試容錯移轉，我們建議您確認 hello VM 屬性，並進行任何變更之前，您需要。 您可以存取在 hello VM 屬性**複寫項目**。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。

## <a name="managed-disk-considerations"></a>受控磁碟的考量

[管理磁碟](../virtual-machines/windows/managed-disks-overview.md)管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure Vm 的磁碟管理。 

- 受管理的磁碟建立並附加 toohello VM，只會發生容錯移轉 tooAzure 時。 當您啟用保護時，在內部部署的 Vm 所傳來的資料會複寫 toostorage 帳戶。
- 受管理的磁碟只可以建立使用 hello 資源管理員部署模型所部署的 Vm。
- 從 Azure tooan 容錯回復內部部署 HYPER-V 環境目前不支援受管理的磁碟使用的機器。 您應該只設定**使用受管理磁碟**太**是**若您正在進行移轉唯一 (容錯移轉 tooAzure 容錯回復不)
- 啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。 受管理的磁碟的 Vm 必須在可用性設定組與**使用受管理磁碟**設定得**是**。 如果 Vm 未啟用 hello 設定，則可以選取只可用性集資源群組中而不會啟用受管理的磁碟。 [深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。
- - 如果 hello 複寫所使用的儲存體帳戶與儲存體服務加密已加密，不能在容錯移轉期間建立受管理的磁碟。 在此情況下可能是不允許使用受管理的磁碟，或停用保護 hello VM，然後將它重新啟用 toouse 沒有加密已啟用儲存體帳戶。 [深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。

 
## <a name="network-considerations"></a>網路考量事項
    
- 您可以設定用於容錯移轉之後的 hello Azure VM 的 hello 目標 IP 位址 toobe。 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。 如果您將無法使用在容錯移轉的位址，hello 容錯移轉將會失敗。 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。
- hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：
    - 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
    - 如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
    - 例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。     
- 如果 hello VM 有多張網路介面卡將所有連線 toohello 相同的網路。
- 如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。


## <a name="view-and-manage-vm-settings"></a>檢視及管理 VM 設定

我們建議您執行容錯移轉之前，確認 hello hello 來源機器的屬性。

1. 在**受保護項目**，按一下**複寫的項目**，然後按一下 hello VM。

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. 在 [hello**複寫項目**] 窗格中，您可以看到 VM 資訊、 健全狀況狀態，以及最新可用的復原點 hello 的摘要。 按一下**屬性**tooview 更多詳細資訊。

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. 在 [計算與網路] 中，您可以：
    - 修改 hello Azure VM 的名稱。 hello 名稱必須符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
    - 指定容錯移轉後的 [資源群組]。
    - 指定 hello Azure VM 的目標大小
    - 選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。
    - 指定是否 toouse[管理磁碟](#managed-disk-considerations)。 選取**是**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器。
    - 檢視或修改網路設定，包括 hello 網路/子網路中的 hello Azure VM 將會位於容錯移轉之後，以及要指派 tooit hello IP 位址。

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. 在**磁碟**、 您可以看到 hello 作業系統的相關資訊和資料磁碟上的 hello VM。


## <a name="run-a-test-failover"></a>執行測試容錯移轉

現在，執行測試容錯移轉 toomake 確定一切如預期般運作。

- 如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。
 - 您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。 [深入了解](site-recovery-active-directory.md#test-failover-considerations)。
 - 如需關於測試容錯移轉的完整資訊，請參閱[本文](site-recovery-test-failover-to-azure.md)。
 
 立即執行容錯移轉：

1. 透過單一電腦、 toofail 中**複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。
2. toofail 透過復原計劃，在**復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。
3. 在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。
4. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**作業** > **站台復原工作**。
5. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。
6. 如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。
7. 完成後，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。



## <a name="next-steps"></a>後續步驟

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。
- [閱讀 容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)，toofail 回和複寫的 Azure Vm 回 toohello 主要內部部署 HYPER-V 站台。

