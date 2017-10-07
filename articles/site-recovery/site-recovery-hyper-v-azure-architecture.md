---
title: "Site Recovery 中的 HYPER-V 複寫 tooAzure 運作 aaaHow？ | Microsoft Docs"
description: "這篇文章提供在 Azure Site Recovery 中 Hyper-V 複寫運作方式的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>HYPER-V 複寫 tooAzure 的運作方式為何？

閱讀此文章 toounderstand hello 架構和工作流程中的 HYPER-V 複寫 tooAzure 使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。

在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

您可以複製下列 tooAzure hello:
- **具有 VMM 的 Hyper-V**：位於內部部署 Hyper-V 主機的 VM 是在 System Center Virtual MAchine Manager (VMM) 雲端進行管理。 主機可以執行任何[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)。 您可以複寫 Hyper-V VM，執行 [Hyper-V 和 Azure 支援](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)的任何客體作業系統。
- **沒有 VMM 的 Hyper-V**：位於 Hyper-V 主機的內部部署 VM，不是在 VMM 雲端進行管理。 主機可以執行任何一個 hello[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)。 您可以複寫 Hyper-V VM，執行 [Hyper-V 和 Azure 支援](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)的任何客體作業系統。


## <a name="architectural-components"></a>架構元件

**領域** | **元件** | **詳細資料**
--- | --- | ---
**Azure** | 在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。 | 儲存體和網路可以是 Resource Manager 型帳戶或傳統帳戶。<br/><br/> 複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。<br/><br/> 在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。
**VMM 伺服器** | 位於 VMM 雲端中的 Hyper-V 主機 | 如果 VMM 雲端中受管理 HYPER-V 主機，您會註冊的 hello 復原服務保存庫中的 hello VMM 伺服器。<br/><br/> Hello VMM 伺服器上您安裝 Azure hello Site Recovery Provider tooorchestrate 複寫。<br/><br/> 您需要邏輯和 VM 網路設定 tooconfigure 網路對應。 VM 網路應連結的 tooa hello 雲端相關聯的邏輯網路。
**Hyper-V 主機** | 可以部署包含或不包含 VMM 伺服器的 Hyper-V 伺服器。 | 如果有任何 VMM 伺服器，hello hello 主機 tooorchestrate 複寫與站台復原已安裝站台復原提供者透過 hello 網際網路。 如果沒有 VMM 伺服器，hello 提供者會安裝它，而不是在 hello 主機。<br/><br/> hello 復原服務代理程式已安裝於 hello 主機 toohandle 資料複寫。<br/><br/> 從提供者 hello 和 hello 代理程式的通訊是安全而且會加密。 Azure 儲存體中的複寫的資料也會加密。
**Hyper-V VM** | 您需要 hello HYPER-V 主機伺服器上的一個或多個 Vm。 | 不需要安裝在 Vm 上的 tooexplicitly

## <a name="deployment-steps"></a>部署步驟

1. **Azure**： 您設定 hello Azure 元件。 我們建議您先設定儲存體和網路帳戶，再開始 Site Recovery 部署。
2. **保存庫**︰您建立 Site Recovery 的復原服務保存庫，並設定保存庫設定，包括設定來源和目標設定、設定複寫原則，以及啟用複寫。
3. **來源與目標**：
    - **VMM 雲端中的 HYPER-V 主機**： 指定來源設定的一部分，您上下載並安裝 Azure Site Recovery Provider hello hello VMM 伺服器和每個 HYPER-V 主機上的 hello Azure 復原服務代理程式。 hello 來源將 hello VMM 伺服器。 Azure hello 目標。
    - 無 VMM 的 HYPER-V 主機： 當您指定來源設定時，下載並安裝在每部 HYPER-V 主機上的 hello 提供者和代理程式。 在部署期間您會蒐集到 HYPER-V 站台的 hello 主機，並指定此站台 hello 來源。 Azure hello 目標。

    ![VMM/Hyper-v-V 複寫 tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![HYPER-V 站台複寫 tooAzure](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **複寫原則**： 建立 hello HYPER-V 站台或 VMM 雲端的複寫原則。 hello 原則會套用的 tooall Vm 位於 hello 網站或雲端中的主機。
5. **啟用複寫**：針對 Hyper-V VM 啟用複寫。 根據 hello 複寫原則設定，就會發生初始複寫。 會追蹤資料變更，並複寫差異變更 tooAzure 開始 hello 初始複寫完成之後。 項目的追蹤變更會保存在 .hrl 檔案中。
6. **測試容錯移轉**： 執行測試容錯移轉 toomake 確定一切如預期般運作。

深入了解部署：
- [開始使用 HYPER-V 虛擬機器複寫 tooAzure-與 VMM](site-recovery-vmm-to-azure.md)
- [開始使用 HYPER-V 虛擬機器複寫 tooAzure-無 VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Hyper-V 複寫工作流程

### <a name="enable-protection"></a>啟用保護。

1. 您針對 HYPER-V 虛擬機器啟用保護之後，在 hello Azure 入口網站或內部部署，hello**啟用保護**啟動。
2. hello 工作會檢查該 hello 機器符合必要條件，再叫用 hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)，tooset hello 設定已設定的複寫設定。
3. hello 工作所叫用 hello 啟動初始複寫[StartReplication](https://msdn.microsoft.com/library/hh850303.aspx)方法、 tooinitialize 完整的 VM 複寫，以及傳送嗨 VM 的虛擬磁碟 tooAzure。
4. 您可以監視 hello 作業在 hello**作業** 索引標籤。    ![作業清單](media/site-recovery-hyper-v-azure-architecture/image1.png) ![啟用保護向下鑽研](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>初始複寫

1. 系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。
2. 虛擬硬碟才是所有的複製的 tooAzure 複寫的一個。 它可能需要一些時間，視 hello VM 大小和網路頻寬。 toooptimize 網路使用量，請參閱[如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)。
3. 如果磁碟上的變更會發生初始複寫正在進行時，hello HYPER-V 複本複寫追蹤器會追蹤這些變更為 HYPER-V 複寫記錄檔 (.hrl)。 這些檔案位在 hello 與 hello 磁碟相同的資料夾。 每個磁碟具有相關聯的.hrl 檔案傳送 toosecondary 儲存體。
4. 初始複寫正在進行時，hello 快照集和記錄檔會消耗磁碟資源。
5. Hello 初始複寫完成時，會刪除 hello VM 快照集。 Hello 記錄檔中的差異磁碟變更為已同步處理和合併 toohello 父系磁碟。


### <a name="finalize-protection"></a>完成保護

1. Hello 初始複寫完成，hello 之後**完成 hello 虛擬機器上的保護**作業設定網路和其他複寫後續設定，以便 hello 虛擬機器時保護。
    ![完成保護作業](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. 如果您要複寫 tooAzure，您可能需要 tootweak hello 設定 hello 虛擬機器，讓它準備好進行容錯移轉。 此時，您可以執行測試容錯移轉 toocheck 一切如預期般運作。

### <a name="delta-replication"></a>差異複寫

1. Hello 初始複寫之後，差異同步處理開始時，根據複寫設定。
2. hello HYPER-V 複本複寫追蹤器會為.hrl 檔案追蹤 hello 變更 tooa 虛擬硬碟。 每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。 此記錄檔會在初始複寫完成之後傳送 toohello 客戶儲存體帳戶。 在另一個記錄檔，在 hello 傳輸 tooAzure 記錄時，會追蹤 hello 變更 hello 主要磁碟相同的目錄。
3. 初始和差異在複寫期間，您可以監視 hello VM 檢視中的 hello VM。 [深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。  

### <a name="replication-synchronization"></a>複寫同步處理

1. 如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。 例如，如果 hello.hrl 檔案到達 hello 磁碟大小的 50%，然後 hello VM 將會標示為重新同步處理。
2.  重新同步處理將 hello 會計算總和檢查碼的 hello 的來源和目標虛擬機器，並傳送 hello 差異資料傳送的資料量降到最低。 重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。 總和檢查碼的每個區塊產生，則會比較，它會封鎖從 hello 來源需要 toobe 套用的 toohello 目標 toodetermine。
3. 重新同步處理完成之後，應會繼續進行正常的差異複寫。 預設重新同步處理排程的 toorun 自動外上班時間時，但是您可以手動重新同步虛擬機器。 例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。 toodo hello 入口網站中的，選取 hello VM >**重新同步處理**。

    ![手動重新同步處理](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>重試

如果發生複寫錯誤，會有內建的重試。 此邏輯可分為以下兩種類別：

**類別** | **詳細資料**
--- | ---
**無法復原的錯誤** | 不嘗試重試。 VM 狀態為**重大**，需要管理員介入處理。 這些錯誤的範例包括： 中斷 VHD 鏈結。Hello 複本 VM; 無效的狀態網路驗證錯誤： 授權錯誤。找不到錯誤 （適用於獨立 HYPER-V 伺服器） 的 VM
**可復原的錯誤** | 產生每個複寫間隔，使用指數型撤退，從而 hello 從 hello 開頭的 1、 2、 4、 8、 hello 第一次嘗試的重試間隔和 10 分鐘重試作業。 如果錯誤持續發生，會每隔 30 分鐘重試一次。 範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況 |

## <a name="protection-and-recovery-lifecycle"></a>保護和復原生命週期

![工作流程](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>後續步驟

- [檢查部署必要條件](site-recovery-prereq.md)
- 疑難排解：
    - [針對保護進行監視和疑難排解](site-recovery-monitoring-and-troubleshooting.md)
    - [Microsoft 支援的說明](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [常見錯誤和解決方案](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
