---
title: "測試容錯移轉的 VMware 複寫 tooAzure aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉，複寫使用 hello Azure Site Recovery 服務 tooAzure VMware vm 的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>步驟 12： 執行測試容錯移轉 tooAzure VMware vm

本文說明如何 toorun 測試容錯移轉從內部部署 VMware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

執行測試容錯移轉，我們建議您確認 hello VM 屬性，並進行任何變更之前，您需要。 您可以存取在 hello VM 屬性**複寫項目**。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。

## <a name="managed-disk-considerations"></a>受控磁碟的考量

[管理磁碟](../virtual-machines/windows/managed-disks-overview.md)管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure Vm 的磁碟管理。 

- 當您啟用 vm 保護時，VM 資料會複寫 tooa 儲存體帳戶。 受管理的磁碟建立並附加 toohello VM，只會容錯移轉發生時。
- 只部署的 Vm 使用 hello 資源管理員的模型，可以建立受管理的磁碟。  
- 啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。 受管理的磁碟的 Vm 必須在可用性設定組與**使用受管理磁碟**設定得**是**。 如果 Vm 未啟用 hello 設定，則可以選取只可用性集資源群組中而不會啟用受管理的磁碟。
- [深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)受控磁碟和可用性設定組。
- 如果 hello 複寫所使用的儲存體帳戶與儲存體服務加密已加密，不能在容錯移轉期間建立受管理的磁碟。 在此情況下可能是不允許使用受管理的磁碟，或停用保護 hello VM，然後將它重新啟用 toouse 沒有加密已啟用儲存體帳戶。 [深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。


## <a name="network-considerations"></a>網路考量事項

您可以建立容錯移轉後的 Azure vm 中設定 hello 目標 IP 位址。

- 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。
- 如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。
- 相同的目標 IP 位址可用於測試容錯移轉，若 hello 位址 hello 測試容錯移轉網路中的 hello。
- 網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：

     - 如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標必須 hello 做 hello 來源的相同數目的介面卡。
     - 如果 hello hello 來源虛擬機器介面卡的數目超過允許 hello 目標大小，hello 數目 hello 目標大小最大值則會使用。
     - 例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。     
   - 如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。
   - 如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。
 - [深入了解](vmware-walkthrough-network.md) IP 位址指定。



## <a name="view-and-modify-vm-settings"></a>檢視及修改 VM 設定

我們建議您執行容錯移轉之前，確認 hello hello 來源機器的屬性。

1. 在**受保護項目**，按一下**複寫的項目**，然後按一下 hello VM。
2. 在 [hello**複寫項目**] 窗格中，您可以看到 VM 資訊、 健全狀況狀態，以及最新可用的復原點 hello 的摘要。 按一下**屬性**tooview 更多詳細資訊。
3. 在 [計算與網路] 中，您可以：
    - 修改 hello Azure VM 的名稱。 hello 名稱必須符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
    - 指定容錯移轉後的 [資源群組]。
    - 指定 hello Azure VM 的目標大小
    - 選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。
    - 指定是否 toouse[管理磁碟](#managed-disk-considerations)。 選取**是**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器。
    - 檢視或修改網路設定，包括 hello 網路/子網路中的 hello Azure VM 將會位於容錯移轉之後，以及要指派 tooit hello IP 位址。
4. 在**磁碟**、 您可以看到 hello 作業系統的相關資訊和資料磁碟上的 hello VM。

## <a name="run-a-test-failover"></a>執行測試容錯移轉

您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。

- 如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。
 - 您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。 [深入了解](site-recovery-active-directory.md#test-failover-considerations)。
 - 如需有關測試容錯移轉的完整資訊，請參閱[這篇文章](site-recovery-test-failover-to-azure.md)。
- 在開始之前，請透過影片快速建立概念︰


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


現在，請執行容錯移轉：

1. 透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。

    ![測試容錯移轉](./media/vmware-walkthrough-test-failover/test-failover.png)

2. toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。  

3. 在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。

4. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。

5. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。

6. 如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。

7. 完成後，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這將刪除測試容錯移轉期間所建立的 hello Vm。



## <a name="next-steps"></a>後續步驟

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。
- 如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。
- [閱讀 容錯回復](site-recovery-failback-azure-to-vmware.md)，toofail 回和複寫的 Azure Vm 回 toohello 內部主要站台。
