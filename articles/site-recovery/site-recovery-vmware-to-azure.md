---
title: "aaaReplicate VMware Vm tooAzure |Microsoft 文件"
description: "摘要說明 hello 複寫 VMware Vm tooAzure 存放裝置上執行的工作負載所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>複寫與站台復原的 VMware 虛擬機器 tooAzure

> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmware-to-azure.md)
> * [Azure 傳統型](site-recovery-vmware-to-azure-classic.md)


本文說明如何 tooreplicate 內部部署 VMware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

如果您想 toomigrate VMware Vm tooAzure （僅限容錯移轉），讀取[本文](site-recovery-migrate-to-azure.md)toolearn 更多。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="deployment-steps"></a>部署步驟

以下是您的需要 toodo:

1. 確認必要條件和限制。
2. 設定 Azure 網路和儲存體帳戶。
3. 準備 hello 在內部部署機器想 toodeploy 為 hello 組態伺服器。
4. 準備 VMware toobe 用於自動探索的 Vm，以及選擇性的 hello 行動服務推入安裝的帳戶。
4. 建立復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。
5. 指定來源、目標和複寫設定。
6. 部署 hello 行動服務想 tooreplicate 在 Vm 上。
7. 啟用複寫 hello Vm。
7. 執行測試容錯移轉 toomake 確定一切如預期般運作。

## <a name="prerequisites"></a>必要條件

**支援需求** | **詳細資料**
--- | ---
**Azure** | 了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)
**內部部署組態伺服器** | 您需要有執行 Windows Server 2012 R2 或更新版本的 VMware VM。 您在 Site Recovery 部署期間設定此伺服器。<br/><br/> 預設 hello 處理序伺服器與主要目標伺服器也會安裝此 VM 上。 當您向上延展，您可能需要不同的處理序伺服器，並且具有 hello 與 hello 組態伺服器相同的需求。<br/><br/> 在[這裡](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)深入了解這些元件
**內部部署 VMware 伺服器** | 一個或多個 VMware vSphere 伺服器 (執行具有最新更新的 6.0、5.5 或 5.1)。 伺服器應該位於相同網路 hello 組態伺服器 （或不同的處理序伺服器） 的 hello。<br/><br/> 我們建議 vCenter server toomanage 主機，執行 6.0 或 5.5 hello 最新的更新。 當您部署 6.0 版時，僅支援 5.5 中可用的功能。
**內部部署 VM** | 您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。 VM 應該執行 VMware 工具。
**URL** | hello 組態伺服器需要存取 toothese Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。<br/></br> 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。<br/></br> 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。<br/><br/> 允許 hello MySQL 下載此 URL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi。
**行動服務** | 安裝在每個複寫的 VM 上。




## <a name="limitations"></a>限制

**限制** | **詳細資料**
--- | ---
**Azure** | 儲存體和網路的帳戶必須在 hello 與 hello 保存庫相同的區域<br/><br/> 如果您使用進階儲存體帳戶，您也需要標準儲存帳戶 toostore 複寫記錄檔<br/><br/> 您無法複寫在中部和印度南部及印度 toopremium 帳戶。
**內部部署組態伺服器** | VMware VM 配接器類型應該是 VMXNET3。 如果不是，請[安裝此更新](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> 應該安裝 vSphere PowerCLI 6.0。<br/><br> hello 機器不應該是網域控制站。 hello 電腦應該具有靜態 IP 位址。<br/><br/> hello 主機名稱必須是 15 個字元或更少，而且作業系統應該是英文。
**VMware** | vCenter 6.0 僅支援 5.5 功能。 Site Recovery 不支援新的 vCenter 和 vSphere 6.0 功能，例如跨 vCenter vMotion、虛擬磁碟區和儲存體 DRS。
**VM** | 確認 [Azure VM 限制](site-recovery-prereq.md#azure-requirements)<br/><br/> 您無法複寫具有加密磁碟的 VM 或具有 UEFI/EFI 開機的 VM。<br/><br> 不支援共用磁碟叢集。 如果 NIC 小組 hello 來源 VM，則會轉換 tooa 容錯移轉之後的單一 NIC。<br/><br/> 如果 Vm 有 iSCSI 磁碟時，站台復原將它轉換 tooa VHD 檔案在容錯移轉之後。 如果 hello iSCSI 目標可到達的 hello Azure VM，將它連接 tooit，並會查看它並 hello VHD。 如果發生這種情況，先中斷 hello iSCSI 目標。<br/><br/> 如果您 tooenable 多重 VM 一致性，可讓 Vm 執行相同工作負載 toobe 復原的 hello 一起 tooa 一致的資料點，請開啟連接埠 20004 hello VM 上。<br/><br/> 必須安裝 Windows hello C 磁碟機上。 hello OS 磁碟應該是基本功能，而非動態。 hello 資料磁碟可以是動態的。<br/><br/> Linux Vm 上的 /etc/hosts 檔案應該包含所有網路介面卡相關都聯的 hello 本機主機名稱 tooIP 位址對應的項目。 hello 主機名稱、 掛接點、 裝置名稱、 系統路徑和檔案名稱 (/ 等等; libodbc) 只應該是英文。<br/><br/> 支援特定類型的 [Linux 儲存體](site-recovery-support-matrix-to-azure.md#support-for-storage)。<br/><br/>建立或設定**disk.enableUUID=true** hello VM 設定中。 這提供一致的 UUID toohello VMDK，，讓它正確掛載，並確保容錯回復，但沒有完整的複寫期間所傳送後 tooon 單位唯一的差異變更。

## <a name="set-up-azure"></a>設定 Azure

1. [設定 Azure 網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。
    - 在容錯移轉之後建立的 Azure VM 會置於這個網路。
    - 您可以在 [Resource Manager](../resource-manager-deployment-model.md) 或傳統模式中設定網路。

2. 為複寫的資料設定 [Azure 儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。
    - hello 帳戶可以是標準或[premium](../storage/storage-premium-storage.md)。
    - 您可以在 Resource Manager 或傳統模式中設定帳戶。

3. [準備帳戶](#prepare-for-automatic-discovery-and-push-installation)hello vCenter server 或 vSphere 主機，所以此站台復原可以自動偵測 VMware Vm。

## <a name="prepare-hello-configuration-server"></a>準備 hello 組態伺服器

1. 在 VMware VM 上安裝 Windows Server 2012 R2 或更新版本。
2. 請確定 hello VM 具有存取 toohello Url 中所列[必要條件](#prerequisites)。
3. 安裝 [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1)。


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>為自動探索和推入安裝做準備

- **準備進行自動探索的帳戶**: hello 站台復原處理序伺服器會自動探索的 Vm。 toodo vCenter server 和 vSphere ESXi 主機可以存取這個，Site Recovery 需要認證。

    1. toouse 專用的帳戶，建立角色 (在 hello vCenter 的層級，使用這類[權限](#vmware-account-permissions)。 指定名稱，例如 **Azure_Site_Recovery**。
    2. 然後，在 hello vSphere 主機/vCenter 伺服器上，建立使用者並指派 hello 角色 toohello 使用者。 您在 Site Recovery 部署期間指定此使用者帳戶。

- **準備行動服務的帳戶 toopush hello**： 如果您想 toopush hello 行動服務 tooVMs，您必須可供 hello 處理序伺服器 tooaccess hello VM 的帳戶。 hello 帳戶僅用於 hello 推入安裝。 您可以使用網域或本機帳戶：

    - 對於 Windows，如果您不使用網域帳戶，您需要 toodisable hello 本機電腦上的遠端使用者存取控制。 這樣一來，在 hello 註冊下 toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**，新增 hello DWORD 項目**LocalAccountTokenFilterPolicy**，值為 1。
    - 如果您想要從 CLI Windows tooadd hello 登錄項目，輸入：``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - 適用於 Linux，hello 帳戶應為 hello 來源 Linux 伺服器上的根。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>選取 hello 保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 按一下 [復原服務保存庫] > 保存庫。
2. 在 hello 資源功能表上，按一下  **Site Recovery** > **步驟 1： 準備基礎結構** > **保護目標**。

    ![選擇目標](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. 在**保護目標**，選取**tooAzure** > **是的與 VMware vSphere Hypervisor**。

    ![選擇目標](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello 組態伺服器、 其註冊 hello 保存庫，以及探索 Vm。

1. 按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。
2. 如果您沒有設定伺服器，請按一下 [+設定伺服器]。

    ![設定來源](./media/site-recovery-vmware-to-azure/set-source1.png)
3. 在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。
4. 下載 hello Site Recovery 整合安裝程式安裝檔案。
5. 下載 hello 保存庫註冊金鑰。 您會在執行統一安裝時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

   ![設定來源](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>執行 Site Recovery 統一安裝

請勿 hello 下列之前啟動，然後執行整合安裝 tooinstall hello 組態伺服器、 hello 處理序伺服器，以及 hello 主要目標伺服器。
    - 透過影片快速建立概念

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - 在 hello 組態伺服器 VM，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。 應該相符。 如果快慢誤差 15 分鐘，安裝可能會失敗。
    - 以本機系統管理員身分 hello 組態伺服器 VM 上執行安裝程式。
    - 請確定 hello VM 上啟用 TLS 1.0。


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。



### <a name="add-hello-account-for-automatic-discovery"></a>新增自動探索的 hello 帳戶

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>TooVMware 伺服器連線

ToovSphere ESXi 主機或 vCenter server，toodiscover VMware Vm 連接。

- 如果您加入 hello vCenter server 或不具有系統管理員權限的帳戶的 vSphere 主機 hello 伺服器上，hello 帳戶必須啟用這些權限：
    - 資料中心、資料存放區、資料夾、主機、網路、資源、虛擬機器、vSphere 分散式交換器。
    - hello vCenter server 必須儲存檢視的權限。
- 當您新增 VMware 伺服器時，可能需要 15 分鐘或更長，tooappear hello 入口網站中的。
在內部部署環境中執行 tooallow Azure Site Recovery toodiscover 虛擬機器，您需要 tooconnect，您的 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery。

選取**+ vCenter** toostart VMware vCenter server 或 VMware vSphere ESXi 主機連接。

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

站台復原連接 tooVMware 伺服器使用 hello 指定設定，並探索 Vm。

## <a name="set-up-hello-target"></a>設定 hello 目標

Hello 目標環境設定之前，請檢查您是否具有[Azure 儲存體帳戶和網路](#set-up-azure)

1. 按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。
2. 指定目標部署模型是以 Resource Manager 為基礎或傳統。
3. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

   ![目標](./media/site-recovery-vmware-to-azure/gs-target.png)
4. 如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**，toocreate 資源管理員帳戶或網路內嵌。

## <a name="set-up-replication-settings"></a>設定複寫設定

在開始之前，請透過影片快速建立概念︰
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate 新的複寫原則，請按一下**Site Recovery 基礎結構** > **複寫原則** > **+ 複寫原則**。
2. 在 [建立複寫原則]中，指定原則名稱。
3. 在**RPO 臨界值**，指定 hello RPO 上限。 這個值指定資料復原點的建立頻率。 連續複寫超過此限制時會產生警示。
4. 在**復原點保留**，指定時間長度 （以小時為單位） hello 保留週期是每個復原點。 複寫的 Vm 就能復原 tooany 點視窗中的。 向上 too24 小時保留支援機器複寫 toopremium 儲存體和標準儲存體 72 小時的時間。
5. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。 按一下**確定**toocreate hello 原則。

    ![複寫原則](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. 當您建立新的原則會自動對 hello 組態伺服器與其相關。 依預設會自動建立容錯回復的比對原則。 例如，如果 hello 複寫原則是**rep 原則**hello 容錯回復原則將會**容錯原則 rep 回復**。 從 Azure 起始容錯回復時才會使用此原則。  



## <a name="plan-capacity"></a>規劃容量

1. 您現已設定您的基本基礎結構，您可以思考容量規劃並找出您是否需要額外的資源。 [深入了解](site-recovery-plan-capacity-vmware.md)。
2. 當您完成容量規劃時，請在 [已完成容量計劃了嗎?] 中選取 [是]。

   ![容量規劃](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>準備 VM 進行複寫

hello 行動服務上必須安裝所有的 VMware Vm 的 tooreplicate。 您可以在數種方式安裝 hello 行動服務：

1. 使用從 hello 處理序伺服器推入安裝來安裝。 這個方法需要 tooprepare Vm toouse。
2. 使用 System Center Configuration Manager 或 Azure 自動化 DSC 之類的部署工具來安裝。
3.  手動安裝。

[深入了解](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>啟用複寫

開始之前：

- 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。
- 當您加入或修改 Vm 時，可能需要向上 too15 分鐘或更久變更 tootake 效果，以及它們 tooappear hello 入口網站中的。
- 您可以檢查 hello 上次探索的時間中的 Vm**設定伺服器** > **上次連絡時間**。
- 不需等到 hello 已排程的探索，反白顯示 hello 組態伺服器 tooadd Vm （但不要按），然後按一下**重新整理**。
- 如果 VM 備妥推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。


### <a name="exclude-disks-from-replication"></a>從複寫排除磁碟

依預設會複寫電腦上的所有磁碟。 您可以從複寫排除磁碟。 例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。

### <a name="replicate-vms"></a>複寫 VM

在開始之前，請觀看快速的影片概觀

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。
2. 在**來源**，選取 hello 組態伺服器。
3. 在 [機器類型] 中，選取 [虛擬機器]
4. 在**vCenter vSphere Hypervisor**、 選取 hello vCenter 伺服器負責管理 hello vSphere 主機，或選取 hello 的主機。
5. 選取 hello 處理序伺服器。 如果您尚未建立任何額外的處理序伺服器，這會是 hello 組態伺服器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. 在**目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉 Vm 的資源群組。 選擇要容錯移轉 Vm hello toouse （classic 或資源管理），Azure 中的 hello 部署模型。


7. 選取要用於複寫資料 toouse hello Azure 儲存體帳戶。 如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。

8. 在建立時即容錯移轉之後，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。 選取**現在選取的機器設定**，tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。 如果您不想 toouse 現有網路，您可以建立一個。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. 在**屬性** > **設定屬性**，選取將由 hello 處理序伺服器 tooautomatically 的 hello 帳戶 hello 機器上安裝 hello 行動服務。
11. 依預設會複寫所有磁碟。 按一下**所有磁碟**並清除您不想 tooreplicate 任何磁碟。 然後按一下 [確定] 。 您可以稍後再設定其他 VM 屬性。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. 在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。 如果您修改原則時，將變更套用的 tooreplicating 機器和 toonew 機器。
12. 啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。 然後按一下 [確定] 。 請注意：

    * 複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。
    * 我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。 啟用多重 VM 一致性可能會影響工作負載的效能，應該只用於如果機器 hello 執行相同的工作負載，且需要一致性。

    ![啟用複寫](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. 按一下 [啟用複寫] 。 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**. 之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。

### <a name="view-and-manage-vm-properties"></a>檢視及管理 VM 屬性

我們建議您確認 hello VM 內容，然後進行您需要的任何變更。

1. 按一下**複寫項目**>，並選取 hello 機器。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。
2. 在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。
3. 在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。 修改與 hello 名稱 toocomply [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)如果您需要。
4. 修改 hello 目標網路、 子網路和 IP 位址指派 toohello Azure VM 的設定：

   - 您可以設定 hello 目標 IP 位址。

    - 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。
    - 如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。
    - 相同的目標 IP 位址可用於測試容錯移轉，若 hello 位址 hello 測試容錯移轉網路中的 hello。

   - 網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：

     - 如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標必須 hello 做 hello 來源的相同數目的介面卡。
     - 如果 hello hello 來源虛擬機器介面卡的數目超過允許 hello 目標大小，hello 數目 hello 目標大小最大值則會使用。
     - 例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。     
   - 如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。
   - 如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。
4. 在**磁碟**、 hello VM 的作業系統，請參閱 < 和 hello 資料磁碟，將會複寫。

#### <a name="managed-disks"></a>受控磁碟

在**計算與網路** > **計算屬性**，如果您想要在容錯移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器，您可以設定 「 使用受管理磁碟 」 設定太"Yes"hello VM。 受管理的磁碟，藉以管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure IaaS Vm 的磁碟管理。 深入了解[受控磁碟。](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - 受管理的磁碟是已建立並附加 toohello 只能在容錯移轉 tooAzure 上的虛擬機器。 啟用保護之後，在內部部署機器的資料會繼續 tooreplicate toostorage 帳戶。  受管理的磁碟只可以建立使用 hello 資源管理員部署模型部署虛擬機器。  

   - 當您設定 「 使用受管理磁碟 」 太"Yes"時，只可用性設定組 hello 資源群組中的使用 「 使用受管理磁碟 」 組太"Yes"時將可讓您選取。 這是因為受管理的磁碟與虛擬機器只能太 「 是 」 是 「 受管理的使用磁碟 」 屬性設定的可用性設定組的一部分。 請確定您使用 「 使用受管理磁碟 」 屬性集，根據您在容錯移轉的受管理的意圖 toouse 磁碟建立可用性設定組。  同樣地，當您設定 「 使用受管理磁碟 」 太"No"時，只有與 「 使用受管理磁碟 」 的屬性設定太"No"hello 資源群組中的可用性設定組將可讓您選取。 [深入了解受控磁碟和可用性設定組](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。

  > [!NOTE]
  > 如果 hello 儲存體帳戶用於複寫加密所使用的儲存體服務加密的任何一點的時間，在容錯移轉期間建立受管理的磁碟將會失敗。 您可以設定 「 使用受管理磁碟 」 太"No"時和重試容錯移轉或停用 hello 虛擬機器的保護和 tooa 儲存體帳戶沒有時間啟用在任何時間點的儲存體服務加密可保護它。
  > [深入了解儲存體服務加密及受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。


## <a name="run-a-test-failover"></a>執行測試容錯移轉


您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。 在開始之前，請透過影片快速建立概念
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. 透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。

    ![測試容錯移轉](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。  

1. 在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。

1. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。

1. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。

1. 如果您[做好容錯移轉之後的連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)，您應該能夠 tooconnect toohello Azure VM。

1. 一旦您完成時，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這將刪除測試容錯移轉期間所建立的 hello Vm。

[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。


## <a name="vmware-account-permissions"></a>VMware 帳戶權限

Site Recovery 需要存取 tooVMware hello 處理序伺服器 tooautomatically 探索的 Vm，以及容錯移轉和容錯回復的 Vm。

- **移轉**： 如果您只想 toomigrate VMware Vm tooAzure，而未曾經回失敗，您可以使用具有唯讀角色 VMware 帳戶。 這種角色可以執行容錯移轉，但不能關閉受保護的來源電腦。 移轉時不需要這樣。
- **Replicate/復原**： 如果您想 toodeploy 完整的複寫，複寫、 容錯移轉 （回復） hello 帳戶必須是能夠 toorun 作業，例如建立和移除磁碟，Vm 等上的電源。
- **自動探索**︰需要至少一個唯讀帳戶。


**Task** | **必要的帳戶/角色** | **權限** | **詳細資料**
--- | --- | --- | ---
**處理序伺服器自動探索 VMware VM** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild**物件、 toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路）。
**容錯移轉** | 您需要至少一個唯讀使用者 | 資料中心物件 –> 傳播 tooChild 物件，角色 = 唯讀 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild** toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路） 的物件。<br/><br/> 適用於移轉用途，而不是完整複寫、容錯移轉、容錯回復。
**容錯移轉和容錯回復** | 我們建議您建立含有 hello 所需的權限的角色 (Azure_Site_Recovery)，然後 hello 角色 tooa VMware 使用者或群組指派 | 資料中心物件 –> 傳播 tooChild 物件，角色 = Azure_Site_Recovery<br/><br/> 資料存放區 -> 配置空間、瀏覽資料存放區、底層檔案作業、移除檔案、更新虛擬機器檔案<br/><br/> 網路 -> 網路指派<br/><br/> 資源]-> [指派的 VM tooresource 集區、 移轉電源關閉的 VM、 移轉已開機的 VM<br/><br/> 工作 -> 建立工作、更新工作<br/><br/> 虛擬機器 -> 組態<br/><br/> 虛擬機器 -> 互動 -> 回答問題、裝置連線、設定 CD 媒體、設定磁碟片媒體、電源關閉、電源開啟、VMware 工具安裝<br/><br/> 虛擬機器 -> 清查 -> 建立、註冊、取消註冊<br/><br/> 虛擬機器 -> 佈建 -> 允許虛擬機器下載、允許虛擬機器檔案上傳<br/><br/> 虛擬機器 -> 快照 -> 移除快照 | 使用者指定在資料中心層級，而存取 tooall hello 物件 hello 資料中心。<br/><br/> toorestrict 存取權，指派 hello**沒有存取**角色以 hello**傳播 toochild**物件、 toohello 子物件 （vSphere 主機、 datastores、 Vm 及網路）。


## <a name="next-steps"></a>後續步驟

之後看到 複寫和執行、 發生中斷時，您容錯移轉 tooAzure，和從 hello 複寫資料建立 Azure Vm。 然後您可以存取工作負載和應用程式在 Azure 中，直到它傳回 toonormal 作業時，無法回復 tooyour 主要位置。

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。
- 如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。
- [閱讀 容錯回復](site-recovery-failback-azure-to-vmware.md)，toofail 回和複寫的 Azure Vm 回 toohello 內部主要站台。

## <a name="third-party-software-notices-and-information"></a>第三方廠商軟體注意事項和資訊
Do Not Translate or Localize

hello 軟體和韌體中執行 hello Microsoft 產品或服務為基礎，或納入 hello 從資料列下方 （以下合稱 「 第三方程式碼 」） 的專案。  Microsoft 為 hello 不原始作者的 hello 協力廠商程式碼。  hello 原始著作權聲明與授權，在其下 Microsoft 接收這類協力廠商程式碼，會設定制定下方。

區段 A 中的 hello 資訊關於元件 hello 專案從下面所列的第三方廠商程式碼。 Such licenses and information are provided for informational purposes only.  此第三方廠商程式碼正在 relicensed 的 tooyou microsoft 在 Microsoft 軟體授權條款的 hello Microsoft 產品或服務。  

節 B 中的 hello 資訊有關第三方廠商程式碼元件所進行可用 tooyou microsoft hello 原始授權條款。

hello 完整的檔案可能位於 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428)。 Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
