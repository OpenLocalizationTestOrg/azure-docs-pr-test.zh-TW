---
title: "HYPER-V 與 Azure Site Recovery 的複寫 （搭配 System Center VMM) tooAzure aaaReview hello 架構 |Microsoft 文件"
description: "這篇文章提供元件的概觀，並複寫時使用的架構在內部部署 HYPER-V Vm 的 VMM 雲端 tooAzure hello Azure Site Recovery 服務。"
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
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: ee1f2775b0c929894933b639464176d7a0441519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture"></a>步驟 1： 檢閱 hello 架構


本文說明 hello 元件和複寫在內部使用 hello tooAzure System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器時使用的處理序[Azure Site Recovery](site-recovery-overview.md)服務。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="architectural-components"></a>架構元件

有多個元件在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時。

**元件** | **需求** | **詳細資料**
--- | --- | ---
**Azure** | 在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。 | 複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。<br/><br/> 在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。
**VMM 伺服器** | hello VMM 伺服器包含 HYPER-V 主機的一或多個雲端。 | Hello VMM 伺服器上安裝與 Site Recovery 的 hello Site Recovery Provider tooorchestrate 複寫，並在 hello 復原服務保存庫中註冊 hello 伺服器。
**Hyper-V 主機** | 一或多個由 VMM 管理的 Hyper-V 主機/叢集。 |  您每個主機或叢集成員上安裝 hello 復原服務代理程式。
**Hyper-V VM** | 一或多個在 Hyper-V 主機伺服器上執行的 VM。 | Tooexplicitly Vm 上安裝，不需要。
**網路功能** |邏輯和 VM 網路設定 hello VMM 伺服器上。 VM 網路應連結的 tooa hello 雲端相關聯的邏輯網路。 | VM 網路會對應的 tooAzure 虛擬網路，Azure Vm 位在網路中，當建立容錯移轉之後。

深入了解 hello 部署先決條件和需求的每個元件在 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)。


**圖 1： 在 VMM 雲端 tooAzure 的 HYPER-V 主機上的複寫 Vm**

![元件](./media/vmm-to-azure-walkthrough-architecture/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>複寫程序

**HYPER-V 複寫 tooAzure 如圖 2： 複寫和復原程序**

![工作流程](./media/vmm-to-azure-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>啟用保護。

1. 您針對 HYPER-V 虛擬機器啟用保護之後，在 hello Azure 入口網站或內部部署，hello**啟用保護**啟動。
2. hello 工作會檢查該 hello 機器符合必要條件，再叫用 hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)，tooset hello 設定已設定的複寫設定。
3. hello 工作所叫用 hello 啟動初始複寫[StartReplication](https://msdn.microsoft.com/library/hh850303.aspx)方法、 tooinitialize 完整的 VM 複寫，以及傳送嗨 VM 的虛擬磁碟 tooAzure。
4. 您可以監視 hello 作業在 hello**作業** 索引標籤。    ![作業清單](media/vmm-to-azure-walkthrough-architecture/image1.png) ![啟用保護向下鑽研](media/vmm-to-azure-walkthrough-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Hello 初始資料複寫

1. 系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。
2. 虛擬硬碟才是所有的複製的 tooAzure 複寫的一個。 它可能需要一些時間，視 hello VM 大小和網路頻寬。 toooptimize 網路使用量，請參閱[如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)。
3. 如果磁碟上的變更會發生初始複寫正在進行時，hello HYPER-V 複本複寫追蹤器會追蹤這些變更為 HYPER-V 複寫記錄檔 (.hrl)。 這些檔案位在 hello 與 hello 磁碟相同的資料夾。 每個磁碟具有相關聯的.hrl 檔案傳送 toosecondary 儲存體。
4. 初始複寫正在進行時，hello 快照集和記錄檔會消耗磁碟資源。
5. Hello 初始複寫完成時，會刪除 hello VM 快照集。 Hello 記錄檔中的差異磁碟變更為已同步處理和合併 toohello 父系磁碟。


### <a name="finalize-protection"></a>完成保護

1. Hello 初始複寫完成，hello 之後**完成 hello 虛擬機器上的保護**作業設定網路和其他複寫後續設定，以便 hello 虛擬機器時保護。
    ![完成保護作業](media/vmm-to-azure-walkthrough-architecture/image3.png)
2. 如果您要複寫 tooAzure，您可能需要 tootweak hello 設定 hello 虛擬機器，讓它準備好進行容錯移轉。 此時，您可以執行測試容錯移轉 toocheck 一切如預期般運作。

### <a name="replicate-hello-delta"></a>複寫 hello 差異

1. Hello 初始複寫之後，差異同步處理開始時，根據複寫設定。
2. hello HYPER-V 複本複寫追蹤器會為.hrl 檔案追蹤 hello 變更 tooa 虛擬硬碟。 每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。 此記錄檔會在初始複寫完成之後傳送 toohello 客戶儲存體帳戶。 在另一個記錄檔，在 hello 傳輸 tooAzure 記錄時，會追蹤 hello 變更 hello 主要磁碟相同的目錄。
3. 初始和差異在複寫期間，您可以監視 hello VM 檢視中的 hello VM。 [深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。  

### <a name="synchronize-replication"></a>同步處理複寫

1. 如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。 例如，如果 hello.hrl 檔案到達 hello 磁碟大小的 50%，然後 hello VM 將會標示為重新同步處理。
2.  重新同步處理將 hello 會計算總和檢查碼的 hello 的來源和目標虛擬機器，並傳送 hello 差異資料傳送的資料量降到最低。 重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。 總和檢查碼的每個區塊產生，則會比較，它會封鎖從 hello 來源需要 toobe 套用的 toohello 目標 toodetermine。
3. 重新同步處理完成之後，應會繼續進行正常的差異複寫。 預設重新同步處理排程的 toorun 自動外上班時間時，但是您可以手動重新同步虛擬機器。 例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。 toodo hello 入口網站中的，選取 hello VM >**重新同步處理**。

    ![手動重新同步處理](media/vmm-to-azure-walkthrough-architecture/image4.png)


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

跳過[步驟 2： 檢閱 hello 部署必要條件](vmm-to-azure-walkthrough-prerequisites.md)
