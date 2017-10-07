---
title: "HYPER-V 與 Azure Site Recovery 的複寫 （而不使用 System Center VMM) tooAzure aaaReview hello 架構 |Microsoft 文件"
description: "本文提供元件和複寫在內部部署 （無 VMM) 的 HYPER-V Vm tooAzure hello Azure Site Recovery 服務時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ec148e87ab2fa17485001ee447ad9f9bf795840e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooazure"></a>步驟 1： 檢閱 HYPER-V 複寫 tooAzure hello 架構


這篇文章描述 hello 元件和處理程序涉及複寫時在內部部署 HYPER-V 虛擬機器 （不由 System Center VMM 管理），使用 hello tooAzure [Azure Site Recovery](site-recovery-overview.md)服務。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="architectural-components"></a>架構元件

有多個元件所涉及複寫無 VMM 的 HYPER-V Vm tooAzure 時。

**元件** | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | **詳細資料**
--- | --- | ---
**Azure** | 在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。 | 複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。<br/><br/> 在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。
**Hyper-V** | Hyper-V 主機和叢集會蒐集到 Hyper-V 網站中。 hello Azure Site Recovery Provider 和復原服務代理程式安裝在每個 HYPER-V 主機上。 | hello 提供者會協調複寫與站台復原 hello 透過網際網路。 hello 復原服務代理程式處理資料的複寫。<br/><br/> 從提供者 hello 和 hello 代理程式的通訊是安全而且會加密。 Azure 儲存體中的複寫的資料也會加密。
**Hyper-V VM** | 您必須有一或多部在 Hyper-V 主機伺服器上執行的 VM。 | Tooexplicitly Vm 上安裝，不需要。

深入了解 hello 部署先決條件和需求的每個元件在 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)。

**圖 1： 使用 HYPER-V 站台 tooAzure 複寫**

![元件](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a>複寫程序

**HYPER-V 複寫 tooAzure 如圖 2： 複寫和復原程序**

![工作流程](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>啟用保護。

1. 您針對 HYPER-V 虛擬機器啟用保護之後，在 hello Azure 入口網站或內部部署，hello**啟用保護**啟動。
2. hello 工作會檢查該 hello 機器符合必要條件，再叫用 hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)，tooset hello 設定已設定的複寫設定。
3. hello 工作所叫用 hello 啟動初始複寫[StartReplication](https://msdn.microsoft.com/library/hh850303.aspx)方法、 tooinitialize 完整的 VM 複寫，以及傳送嗨 VM 的虛擬磁碟 tooAzure。
4. 您可以監視 hello 作業在 hello**作業** 索引標籤。
 
### <a name="replicate-hello-initial-data"></a>Hello 初始資料複寫

1. 系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。
2. 虛擬硬碟才是所有的複製的 tooAzure 複寫的一個。 它可能需要一些時間，視 hello VM 大小和網路頻寬。 toooptimize 網路使用量，請參閱[如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)。
3. 如果磁碟上的變更會發生初始複寫正在進行時，hello HYPER-V 複本複寫追蹤器會追蹤這些變更為 HYPER-V 複寫記錄檔 (.hrl)。 這些檔案位在 hello 與 hello 磁碟相同的資料夾。 每個磁碟具有相關聯的.hrl 檔案傳送 toosecondary 儲存體。
4. 初始複寫正在進行時，hello 快照集和記錄檔會消耗磁碟資源。
5. Hello 初始複寫完成時，會刪除 hello VM 快照集。 Hello 記錄檔中的差異磁碟變更為已同步處理和合併 toohello 父系磁碟。


### <a name="finalize-protection"></a>完成保護

1. Hello 初始複寫完成，hello 之後**完成 hello 虛擬機器上的保護**作業設定網路和其他複寫後續設定，以便 hello 虛擬機器時保護。
2. 如果您要複寫 tooAzure，您可能需要 tootweak hello 設定 hello 虛擬機器，讓它準備好進行容錯移轉。 此時，您可以執行測試容錯移轉 toocheck 一切如預期般運作。

### <a name="replicate-hello-delta"></a>複寫 hello 差異

1. Hello 初始複寫之後，差異同步處理開始時，根據複寫設定。
2. hello HYPER-V 複本複寫追蹤器會為.hrl 檔案追蹤 hello 變更 tooa 虛擬硬碟。 每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。 此記錄檔會在初始複寫完成之後傳送 toohello 客戶儲存體帳戶。 在另一個記錄檔，在 hello 傳輸 tooAzure 記錄時，會追蹤 hello 變更 hello 主要磁碟相同的目錄。
3. 初始和差異在複寫期間，您可以監視 hello VM 檢視中的 hello VM。 [深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。  

### <a name="synchronize-replication"></a>同步處理複寫

1. 如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。 例如，如果 hello.hrl 檔案到達 hello 磁碟大小的 50%，然後 hello VM 將會標示為重新同步處理。
2.  重新同步處理將 hello 會計算總和檢查碼的 hello 的來源和目標虛擬機器，並傳送 hello 差異資料傳送的資料量降到最低。 重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。 總和檢查碼的每個區塊產生，則會比較，它會封鎖從 hello 來源需要 toobe 套用的 toohello 目標 toodetermine。
3. 重新同步處理完成之後，應會繼續進行正常的差異複寫。 預設重新同步處理排程的 toorun 自動外上班時間時，但是您可以手動重新同步虛擬機器。 例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。 toodo hello 入口網站中的，選取 hello VM >**重新同步處理**。

    ![手動重新同步處理](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a>重試邏輯

如果發生複寫錯誤，會有內建的重試。 此邏輯可分為以下兩種類別：

**類別** | **詳細資料**
--- | ---
**無法復原的錯誤** | 不嘗試重試。 VM 狀態為**重大**，需要管理員介入處理。 這些錯誤的範例包括： 中斷 VHD 鏈結。Hello 複本 VM; 無效的狀態網路驗證錯誤： 授權錯誤。找不到錯誤 （適用於獨立 HYPER-V 伺服器） 的 VM
**可復原的錯誤** | 產生每個複寫間隔，使用指數型撤退，從而 hello 從 hello 開頭的 1、 2、 4、 8、 hello 第一次嘗試的重試間隔和 10 分鐘重試作業。 如果錯誤持續發生，會每隔 30 分鐘重試一次。 範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況 |



## <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

1. 您可以執行的已規劃或未規劃[容錯移轉](site-recovery-failover.md)從內部部署 HYPER-V Vm tooAzure。 如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。
2. 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。
4. 執行 hello 容錯移轉之後，您應該在 Azure 中建立複本 Vm 可以 toosee hello。 如果需要，您可以指定公用 IP 位址 toohello VM。
5. 然後，您就會認可 hello 容錯移轉 toostart 從 hello 複本 Azure VM 存取 hello 工作負載。
6. 當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。 您開始進行規劃的容錯移轉，從 Azure toohello 主要站台。 規劃的容錯移轉，您可以選取 toofailback toohello 相同 VM 或 tooan 替代位置，並同步處理變更 Azure 和內部部署、 tooensure 之間不會遺失資料。 Vm 建立時在內部部署，您就會認可 hello 容錯移轉。




## <a name="next-steps"></a>後續步驟

跳過[步驟 2： 檢閱 hello 部署必要條件](hyper-v-site-walkthrough-prerequisites.md)
