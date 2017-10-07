---
title: "複寫應用程式 (VMware tooAzure) |Microsoft 文件"
description: "本文說明如何 tooset 複寫的虛擬機器正在執行 VMware 到 Azure 上。"
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
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>複寫 tooAzure VMware Vm 上執行應用程式



本文說明如何 tooset 複寫的虛擬機器正在執行 VMware 到 Azure 上。
## <a name="prerequisites"></a>必要條件

hello 文章假設您已經有

1.  [設定內部部署來源環境](site-recovery-set-up-vmware-to-azure.md)
2.  [在 Azure 中設定目標環境](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>啟用複寫
#### <a name="before-you-start"></a>開始之前
當您要複寫 VMware 虛擬機器時，請注意下列事項︰

* 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。
* 系統會每隔 15 分鐘探索 VMware VM 一次。 可能需要 15 分鐘或更長，tooappear 探索之後 hello 入口網站中的。 同樣地，當您加入新的 vCenter 伺服器或 vSphere 主機時，探索可能需要 15 分鐘以上。
* Hello （例如 VMware 工具安裝） 的虛擬機器上的環境變更可能需要 15 分鐘或更多 toobe hello 入口網站中更新。
* 您可以檢查 hello 上次探索時間 VMware vm 在 hello**上次連絡時間**欄位 hello vCenter 伺服器 /vsphere 主機，在 hello**設定伺服器**刀鋒視窗。
* tooadd 機器的複寫不會等候 hello 已排程的探索，反白顯示 hello 組態伺服器 （但不要按），然後按一下 hello**重新整理** 按鈕。
* 當您啟用複寫，如果 hello 機器已備妥時，hello 處理序伺服器自動安裝 hello 行動服務在其上。


**立即啟用複寫，如下所示**︰

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。 您已啟用複寫 hello 第一次之後，請按一下**+ 複寫**中的其他機器 hello 保存庫 tooenable 複寫。
2. 在 hello**來源**刀鋒視窗 >**來源**，選取 hello 組態伺服器。
3. 在 [機器類型] 中，選取 [虛擬機器] 或 [實體機器]。
4. 在**vCenter vSphere Hypervisor**、 選取 hello vCenter 伺服器負責管理 hello vSphere 主機，或選取 hello 的主機。 如果您是複寫實體機器，則這個設定不相關。
5. 選取 hello 處理序伺服器。 如果您尚未建立任何額外的處理序伺服器會 hello hello 組態伺服器的名稱。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. 在**目標**選取 hello 訂用帳戶和您想要容錯移轉虛擬機器的 toocreate hello hello 資源群組。 選擇要容錯移轉虛擬機器的 hello toouse Azure （classic 或資源管理） 中的 hello 部署模型。
7. 選取要用於複寫資料 toouse hello Azure 儲存體帳戶。 請注意：

   * 您可以選取進階或標準儲存體帳戶。 如果您選取進階帳戶時，您必須 toospecify 額外標準儲存體帳戶進行中的複寫記錄檔。 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。
   * 如果您想 toouse 您有不同的儲存體帳戶以外，您可以建立一個*預留位置連結，開始建立使用資源的儲存體帳戶管理員將涵蓋這*。 按一下 儲存體帳戶使用資源管理員 toocreate**建立新**。 如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，您執行[hello Azure 入口網站中](../storage/common/storage-create-storage-account.md)。

8. 選取 hello Azure 網路和子網路 toowhich Azure Vm 將會連接，當它們容錯移轉後正在開始。 hello 網路必須位於 hello hello 與相同的區域復原服務保存庫。 選取**現在選取的機器設定**，tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。 如果您沒有網路，您需要太[建立一個](#set-up-an-azure-network)。 toocreate 網路使用資源管理員 中，按一下**建立新**。 如果您想 toocreate 網路使用 hello 傳統模式，這樣做， [hello Azure 入口網站中](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 選取適用的子網路。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. 在**屬性** > **設定屬性**，選取將由 hello 處理序伺服器 tooautomatically 的 hello 帳戶 hello 機器上安裝 hello 行動服務。  
11. 依預設會複寫所有磁碟。 tooexclude 磁碟從複寫中，按一下**所有磁碟**並清除您不想 tooreplicate 任何磁碟。  然後按一下 [確定] 。 您可以稍後再設定其他屬性。 [深入了解](site-recovery-exclude-disk.md)排除磁碟。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. 在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。 您可以在 [設定]  >  [複寫原則] > 原則名稱 > [編輯設定] 中修改複寫原則設定。 套用的 tooreplicating 和新的機器，將會套用 tooa 原則的變更。
13. 啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。 然後按一下 [確定] 。 請注意：

    * 複寫群組中的機器會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。
    * 我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。 啟用多重 VM 一致性可能會影響工作負載效能，應該只用於如果機器 hello 執行相同的工作負載，且需要一致性。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. 按一下 [啟用複寫] 。 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**. 之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。

> [!NOTE]
> 如果 hello 機器做好推入安裝 hello 行動服務元件將安裝時已啟用保護。 Hello 元件安裝後 hello 機器保護工作可啟動與失敗。 Hello 失敗後，您需要 toomanually 重新啟動每一部機器。 Hello 重新啟動 hello 保護之後作業會重新開始計算，就會發生初始複寫。
>
>

## <a name="view-and-manage-vm-properties"></a>檢視及管理 VM 屬性

我們建議您確認 hello hello 來源機器的屬性。 請記住該 hello Azure VM 名稱應該符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

1. 按一下**設定** > **複寫項目**>，並選取 hello 機器。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。
2. 在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。
3. 在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。 如果您需要，修改 hello 名稱 toocomply Azure 需求。
    ![啟用複寫](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  您可以選取電腦將成為其後置容錯移轉一部分的[資源群組](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines)。 您可以在容錯移轉之前隨時變更這項設定。 Post 容錯移轉，如果您移轉 hello 機器 tooa 不同資源群組，則會中斷機器的保護設定。
5. 您可以選取[可用性設定組](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)如果您的電腦所需 toobe 變成一篇文章的一部分，容錯移轉。 當選取可用性設定組時，請記住︰

    * 可用性設定組隸屬 toohello 指定只會列出資源群組  
    * 虛擬網路不同的電腦不可在相同的可用性設定組中
    * 只有相同大小的虛擬機器可在相同的可用性設定組中
5. 您也可以檢視和新增 hello 目標網路、 子網路及指派 toohello Azure VM 的 IP 位址資訊。
6. 在**磁碟**、 您所見 hello 作業系統和資料磁碟上的 hello 將複寫的 VM。

### <a name="network-adapters-and-ip-addressing"></a>網路介面卡和 IP 位址 

- 您可以設定 hello 目標 IP 位址。 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。 如果您將無法使用在容錯移轉的位址，將無法運作 hello 容錯移轉。 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。
- hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：
    - 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
    - 如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
    - 例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。
    - 如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。
    - 如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。
   



## <a name="common-issues"></a>常見問題

* 各磁碟大小必須都小於 1 TB。
* hello OS 磁碟應該是基本磁碟和非動態磁碟
* 層代 2/UEFI 啟用虛擬機器，hello 作業系統系列應該是 Windows，而且應小於 300 GB 開機磁碟。

## <a name="next-steps"></a>後續步驟

完成 hello 保護之後，您可以嘗試[容錯移轉](site-recovery-failover.md)toocheck 是否應用程式出現在 Azure 中或不。

如果您想 toodisable 保護，請檢查如何太[清除登錄和保護設定](site-recovery-manage-registration-and-protection.md)
