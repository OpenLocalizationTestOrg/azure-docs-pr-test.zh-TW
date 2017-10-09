---
title: "aaaReplicate 實體伺服器 tooAzure |Microsoft 文件"
description: "描述如何 toodeploy Azure Site Recovery tooorchestrate 複寫、 容錯移轉和復原的內部部署 Windows/Linux 實體伺服器 tooAzure 使用 hello Azure 入口網站"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>將實體機器 tooAzure 複寫使用站台復原


本文說明如何 tooreplicate 內部部署實體機器 tooAzure hello Azure 入口網站中使用 hello Azure Site Recovery 服務。

如果您想 toomigrate 實體機器 tooAzure （僅限容錯移轉），讀取[移轉與 Site Recovery tooAzure](site-recovery-migrate-to-azure.md) toolearn 更多。

在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="prerequisites"></a>必要條件

**支援需求** | **詳細資料**
--- | ---
**Azure** | 了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。
**內部部署組態伺服器** | 執行 Windows Server 2012 R2 或更新版本的內部部署機器 (實體或 VMware VM)。 在站台復原 」 部署期間設定 hello 組態伺服器。<br/><br/> 根據預設，hello 處理序伺服器與主要目標伺服器也安裝在這部電腦上。 當您向上延展，您可能需要不同的處理序伺服器，並且具有 hello 與 hello 組態伺服器相同的需求。<br/><br/> 深入了解這些元件在[設定 hello 來源環境](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)。
**內部部署 VM** | 您想應該執行 tooreplicate 機器[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)和符合[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
**URL** | hello 組態伺服器需要存取 toothese Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。<br/></br> 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 hello HTTPS (443) 連接埠。<br/></br> 允許的 IP 位址範圍 hello Azure 地區的訂用帳戶和西部 （用於存取控制和身分識別管理）。<br/><br/> 允許 hello MySQL 下載此 URL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi。
**行動服務** | 這項服務安裝在每部電腦上您想 tooreplicate。

## <a name="limitations"></a>限制

**限制** | **詳細資料**
--- | ---
**Azure** | 儲存體和網路的帳戶必須在 hello 與 hello 保存庫相同的區域。<br/><br/> 如果您使用進階儲存體帳戶，您也需要標準儲存帳戶 toostore 複寫記錄檔。<br/><br/> 您無法複寫在中部和印度南部及印度 toopremium 帳戶。
**內部部署組態伺服器** | 如果您在 VMware VM 上安裝 hello 組態伺服器，hello VM 配接器類型應該是 VMXNET3。 如果不是，請[安裝此更新](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)。<br/><br/> 如果您使用 VMware VM，則應該在其上安裝 vSphere PowerCLI 6.0。<br/><br> hello 機器不應該是網域控制站。<br/><br/> hello 電腦應該具有靜態 IP 位址。<br/><br/> hello 主機名稱必須是 15 個字元或更少，而且 hello 作業系統應該是英文。
**複寫的機器** | 確認 [Azure VM 限制](site-recovery-prereq.md#azure-requirements)。<br/><br/> 如果您 tooenable 多重 VM 一致性，可讓執行相同工作負載 toobe 復原的 hello 機器一起 tooa 一致的資料點，請開啟連接埠 20004 hello 機器上。<br/><br/> 支援特定類型的 [Linux 儲存體](site-recovery-support-matrix-to-azure.md#support-for-storage)。
**容錯回復** | 您無法從 Azure tooa 實體機器失敗。 如果您想 toobe 無法 toofail 後 tooon 內部部署容錯移轉之後，您需要的 VMware 環境，讓您可以容錯回復 tooa VMware VM。


## <a name="set-up-azure"></a>設定 Azure

1. [設定 Azure 網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。

      a. 在容錯移轉之後建立的 Azure VM 會置於這個網路。

      b.這是另一個 C# 主控台應用程式。 您可以在 Azure [Resource Manager](../resource-manager-deployment-model.md) 或傳統模式中設定網路。

2. 為複寫的資料設定 [Azure 儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。

    a. hello 帳戶可以是標準或[premium](../storage/storage-premium-storage.md)。

    b. 您可以在 Resource Manager 或傳統模式中設定帳戶。

## <a name="prepare-hello-configuration-server"></a>準備 hello 組態伺服器

1. 在內部部署實體伺服器或 VMware VM 上，安裝 Windows Server 2012 R2 或更新版本。

2. 請確定 hello 電腦具有存取 toohello Url 中所列[必要條件](#prerequisites)。

## <a name="prepare-for-mobility-service-installation"></a>準備行動服務安裝

如果您想 toopush hello 行動服務 tooa 實體機器，您必須可供 hello 處理序伺服器 tooaccess hello 機器帳戶。 hello 帳戶只能用於 hello 推入安裝。 您可以使用網域或本機帳戶：

  - 對於 Windows，如果您不使用網域帳戶，您需要 toodisable hello 本機電腦上的遠端使用者存取控制。 toodo hello 下的登錄中的這**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**，新增 hello DWORD 項目**LocalAccountTokenFilterPolicy**，值為 1。 如果您想用於 Windows 的 tooadd hello 登錄項目從命令列介面上，輸入：

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - 適用於 Linux，hello 帳戶應該是 hello 來源 Linux 伺服器上的根使用者。


## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>選取 hello 保護目標

選取您想要 tooreplicate 和您想要 tooreplicate。

1. 按一下 [復原服務保存庫] > [保存庫]。
2. 在 hello**資源**功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**.

    ![選擇目標](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. 在**保護目標**，選取**tooAzure** > **未虛擬化 / 其他**。


## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello 組態伺服器、 其註冊 hello 保存庫，以及探索 Vm。

1. 按一下 [Site Recovery] > [準備基礎結構] > [來源]。
2. 如果您沒有設定伺服器，請按一下 [+設定伺服器]。

    ![設定來源](./media/site-recovery-vmware-to-azure/set-source1.png)

3. 在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。
4. 下載 hello **Site Recovery 整合安裝程式**安裝檔案。
5. 下載 hello**保存庫註冊金鑰**。 您會在執行統一安裝時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

   ![設定來源](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>執行 Site Recovery 統一安裝

開始之前，請勿 hello 遵循：

- 透過影片快速建立概念。 (hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- 在 hello 組態伺服器的電腦，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。 如果快慢誤差 15 分鐘，安裝就可能會失敗。
- Hello 組態伺服器電腦上，本機系統管理員身分執行安裝程式。
- 請確定 hello 機器上已啟用 TLS 1.0。

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

設定 hello 目標環境之前，請確定您有 toomake [Azure 儲存體帳戶和網路](#set-up-azure)。

1. 按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。
2. 指定目標部署模型為 Resource Manager 還是傳統的。
3. Site Recovery 會檢查 toomake 確定您有一或多個相容的 Azure 儲存體帳戶和網路。

   ![目標](./media/site-recovery-vmware-to-azure/gs-target.png)

4. 如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**toocreate 資源管理員帳戶或網路內嵌。

## <a name="set-up-replication-settings"></a>設定複寫設定

在開始之前，請透過影片快速建立概念。 (hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate 新的複寫原則，請按一下**Site Recovery 基礎結構** > **複寫原則** > **+ 複寫原則**。
2. 在 [建立複寫原則]中，指定原則名稱。
3. 在**RPO 臨界值**，指定 hello RPO 上限。 這個值指定資料復原點的建立頻率。 連續複寫超過此限制時會產生警示。
4. 在**復原點保留**，指定時間長度 （以小時為單位） hello 保留週期是每個復原點。 複寫的 Vm 就能復原 tooany 點視窗中的。 向上 too24 機器複寫的 toopremium 存放裝置支援小時的保留。 向上 too72 機器複寫的 toostandard 存放裝置支援小時的保留。
5. 在 [應用程式一致快照集頻率] 中，指定建立包含應用程式一致快照集之復原點的頻率 (以分鐘為單位)。 按一下**確定**toocreate hello 原則。

    ![複寫原則](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. 當您建立新的原則時，它會自動與相關聯 hello 組態伺服器。 依預設會自動建立容錯回復的比對原則。 例如，如果 hello 複寫原則是**rep 原則**，那麼 hello 容錯回復原則是**容錯原則 rep 回復**。 從 Azure 起始容錯回復時才會使用此原則。  


## <a name="plan-capacity"></a>規劃容量

1. 現在您已設定基本基礎結構，可以思考容量規劃，並找出您是否需要額外的資源。 [深入了解](site-recovery-plan-capacity-vmware.md)。
2. 當您完成容量規劃時，請在 [已完成容量計劃了嗎?] 中選取 [是]。

   ![容量規劃](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>準備 VM 進行複寫

您要讓 tooreplicate 必須已安裝的 hello 行動服務的所有機器。 您可以在數種方式安裝 hello 行動服務：

- 以從 hello 處理序伺服器推入安裝來安裝 hello 服務。 這個方法需要進階 toouse tooprepare 機器。
- 使用 System Center Configuration Manager 或 Azure 自動化 Desired State Configuration 之類的部署工具安裝 hello 服務。
- 手動安裝 hello 服務。

[深入了解](site-recovery-vmware-to-azure-install-mob-svc.md)。


## <a name="enable-replication"></a>啟用複寫

開始之前：

- 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。
- 當您加入或修改 Vm 時，可能需要向上 too15 分鐘或更久變更 tootake 效果，並為其 tooappear hello 入口網站中的。
- 您可以檢查 hello 上次探索的時間中的 Vm**設定伺服器** > **上次連絡時間**。
- 不需等到 hello 已排程的探索，反白顯示 hello 組態伺服器 tooadd Vm （但不要按），然後按一下**重新整理**。
- 如果 VM 備妥推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。
- 透過影片快速建立概念。 (hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>從複寫排除磁碟

依預設會複寫機器上的所有磁碟。 您可以從複寫排除磁碟。 比方說，您可能不想使用暫存資料 tooreplicate 磁碟或資料重新整理每一次電腦或應用程式重新啟動 （例如，pagefile.sys 或 SQL Server tempdb）。

### <a name="replicate-vms"></a>複寫 VM

1. 按一下 [複寫應用程式] > [來源]。
2. 在 [來源] 中，選取 [內部部署]。
3. 在**來源位置**，選取 hello 組態伺服器名稱。
4. 在 [機器類型] 中，選取 [實體機器]。
5. 在**處理序伺服器**，選擇 hello 處理序伺服器。 如果您尚未建立任何額外的處理序伺服器，此伺服器是 hello 組態伺服器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-physical-to-azure/chooseVM.png)

6. 在**目標**，選取 hello**訂用帳戶**和 hello**資源群組**您想 toocreate hello Azure Vm 容錯移轉之後。 選擇 hello 部署模型，您想要在 Azure 中的 toouse (傳統或資源管理員) 的 hello 容錯移轉 Vm。

7. 選取要用於複寫資料 toouse hello Azure 儲存體帳戶。 如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。

8. 選取 hello **Azure 網路**和**子網路**toowhich Azure Vm 容錯移轉之後連接。 選取**現在選取的機器設定**tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。 如果您不想 toouse 現有網路，您可以建立一個。

    ![啟用複寫](./media/site-recovery-physical-to-azure/targetsettings.png)

9. 在**實體機器**，按一下  **+ 實體機器**，然後輸入 hello**名稱**和**IP 位址**。 選擇 hello 作業系統要 tooreplicate 的 hello 機器。 花幾分鐘的時間之前的電腦系統會探索並 hello 清單所示。

    ![啟用複寫](./media/site-recovery-physical-to-azure/machineselect.png)

10. 在**屬性** > **設定屬性**，選取 hello toobe 供 hello 處理序伺服器 tooautomatically hello 機器上安裝 hello 行動服務的帳戶。
11. 依預設會複寫所有磁碟。 按一下**所有磁碟**，並清除您不想 tooreplicate 任何磁碟。 然後按一下 [確定] 。 您可以稍後再設定其他 VM 屬性。

    ![啟用複寫](./media/site-recovery-physical-to-azure/configprop.png)

12. 在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。 如果您修改原則時，變更將會套用的 toohello 機器和 toonew 機器複寫。
13. 啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。 然後按一下 [確定] 。 請注意：

    a. 複寫群組中的電腦會一起複寫，且在容錯移轉時，會有共用的損毀一致和應用程式一致的復原點。

    b.這是另一個 C# 主控台應用程式。 我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。 啟用多 VM 一致性可能會影響工作負載的效能。 如果電腦執行 hello 相同的工作負載，且您需要一致性應該使用它。

    ![啟用複寫](./media/site-recovery-physical-to-azure/policy.png)

14. 按一下 [啟用複寫] 。 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**. 之後 hello**完成保護**作業會執行，hello 機器是否已做好容錯移轉。

啟用複寫後，如果您設定推入安裝安裝 hello 行動服務。 Hello 行動服務推入安裝在電腦上後，保護工作會啟動，並會失敗。 Hello 失敗之後，您需要 toomanually 重新啟動每一部機器。 Hello 保護作業，然後再次，開始，就會發生初始複寫。


### <a name="view-and-manage-azure-vm-properties"></a>檢視及管理 Azure VM 屬性

我們建議您確認 hello VM 屬性，然後進行您需要的任何變更。

1. 按一下**複寫項目**，並選取 hello 機器。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。
2. 在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。
3. 在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。 修改與 hello 名稱 toocomply [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)如果您需要。
4. 修改設定 hello 目標網路、 子網路和 IP 位址指派 toohello Azure VM:

    a. 您可以設定 hello 目標 IP 位址。

    b.  如果您沒有提供的地址，hello 容錯機器會使用 DHCP。

    c. 如果您設定的位址在容錯移轉時無法使用，容錯移轉就無法運作。

    d. 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。

    e. 網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：

     - 如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標有 hello 做 hello 來源的相同數目的介面卡。
     - 如果 hello hello 來源虛擬機器介面卡的數目超過 hello 目標大小，允許 hello 數目，則使用 hello 目標大小最大值。
     - 例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但支援 hello 目標大小僅支援一個，hello 目標電腦有只有一張介面卡。     
   - 如果 hello 虛擬機器有多張網路介面卡，它們全部連接 toohello 相同的網路。
   - 如果 hello 虛擬機器有多張網路介面卡，則 hello hello 清單中所顯示的最早 hello*預設*hello Azure VM 中的網路介面卡。
5. 在**磁碟**，您可以看到 hello VM 作業系統以及 hello 複寫的資料磁碟。

## <a name="run-a-test-failover"></a>執行測試容錯移轉

您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。 開始之前，請觀看影片快速建立概念。

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. 透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 **測試容錯移轉**。

    ![測試容錯移轉](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。  
3. 在**測試容錯移轉**，選取 hello Azure 網路 toowhich Azure Vm 容錯移轉發生後的連線。
4. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，方法是按一下 hello VM tooopen 其屬性，或按一下 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。
5. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。
6. 如果您[做好容錯移轉之後的連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)，您應該能夠 tooconnect toohello Azure VM。
7. 瀏覽完畢之後，請按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 此步驟會刪除 hello 測試容錯移轉期間所建立的虛擬機器。

如需詳細資訊，請參閱 hello[測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)文件。

## <a name="next-steps"></a>後續步驟

之後看到 複寫和執行、 發生中斷時，您容錯移轉 tooAzure，和從 hello 複寫資料建立 Azure Vm。 然後您可以存取工作負載和應用程式在 Azure 中，直到它傳回 toonormal 作業時，無法回復 tooyour 主要位置。

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。
- 如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。
- 當複寫實體機器，您可以只容錯回復 tooa VMware 環境。 [了解容錯回復](site-recovery-failback-azure-to-vmware.md)。

## <a name="third-party-software-notices-and-information"></a>第三方廠商軟體注意事項和資訊
Do Not Translate or Localize

hello 軟體和韌體中執行 hello Microsoft 產品或服務為基礎，或納入 hello 從資料列下方 （以下合稱 「 第三方程式碼 」） 的專案。 Microsoft 不 hello 的 hello 協力廠商程式碼的原始作者。 hello 原始著作權聲明與授權，在其下 Microsoft 接收這類協力廠商程式碼中，會設定制定下方。

區段 A 中的 hello 資訊關於從 hello 專案元件下面所列的第三方程式碼。 Such licenses and information are provided for informational purposes only. 此協力廠商程式碼正在 relicensed 的 tooyou microsoft 在 Microsoft 軟體授權條款的 hello Microsoft 產品或服務。  

節 B 中的 hello 資訊有關第三方廠商程式碼元件所進行可用 tooyou microsoft hello 原始授權條款。

hello 完整的檔案可以位於 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428)。 Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.
