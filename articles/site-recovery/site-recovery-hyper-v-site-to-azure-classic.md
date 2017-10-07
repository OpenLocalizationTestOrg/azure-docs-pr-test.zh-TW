---
title: "aaaReplicate hello 傳統入口網站中的 HYPER-V Vm tooAzure |Microsoft 文件"
description: "本文說明如何 tooreplicate HYPER-V 虛擬機器 tooAzure 當機器不 VMM 雲端中管理。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>使用 Azure Site Recovery 在內部部署 Hyper-V 虛擬機器與 Azure (沒有 VMM) 之間複寫
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - 資源管理員](site-recovery-deploy-with-powershell-resource-manager.md)
> * [傳統入口網站](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

本文說明如何 tooreplicate 內部部署 HYPER-V 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務 hello Azure 入口網站中。 在此案例中，不是在 VMM 雲端中管理 Hyper-V 伺服器。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="site-recovery-in-hello-azure-portal"></a>在 hello Azure 入口網站中的站台復原

Azure 用來建立和處理資源的[部署模型](../resource-manager-deployment-model.md)有二種 - Azure Resource Manager 和傳統。 Azure 也有兩個入口網站 – hello Azure 傳統入口網站和 hello Azure 入口網站。

本文說明如何 toodeploy hello 傳統入口網站中的。 hello 傳統入口網站可以使用的 toomaintain 現有保存庫。 您無法建立新的保存庫使用 hello 傳統入口網站。

## <a name="site-recovery-in-your-business"></a>您企業中的 Site Recovery

組織需要 BCDR 策略，以決定如何應用程式和資料維持執行且可用在計劃性與非計劃性停機時間，並且儘速復原 toonormal 工作條件。 以下是 Site Recovery 可以提供的協助︰

* 在 Hyper-V VM 上執行之企業應用程式的異地保護。
* 單一位置 tooset、 管理及監視複寫、 容錯移轉和復原。
* 簡單的容錯移轉 tooAzure 並從內部部署網站中的 Azure 的 tooHyper HYPER-V 主機伺服器的容錯回復 （還原）。
* 包含多部 VM 的復原方案，以便階層式應用程式工作負載一起容錯移轉。

## <a name="azure-prerequisites"></a>Azure 必要條件
* 您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
* 您需要 Azure 儲存體帳戶 toostore 複寫資料。 hello 帳戶必須啟用異地複寫。 它應該會在 hello 與 hello Azure Site Recovery 保存庫相同的區域，並且與相關聯 hello 相同訂用帳戶。 [深入了解 Azure 儲存體](../storage/common/storage-introduction.md)。 請注意，我們不支援移動的儲存體帳戶建立使用 hello[新版 Azure 入口網站](../storage/common/storage-create-storage-account.md)跨越資源群組。
* 您必須在 Azure 虛擬網路，因此 Azure 虛擬機器會連接的 tooa 網路，當您從您的主要站台容錯移轉。

## <a name="hyper-v-prerequisites"></a>Hyper-V 的必要條件
* 在 hello 來源內部部署網站中，您將需要一個或多部執行**Windows Server 2012 R2** hello HYPER-V 已安裝的角色或**Microsoft HYPER-V Server 2012 R2**。 此伺服器應該：
* 包含一或多部虛擬機器。
* 直接或透過 proxy，則是連線的 toohello 網際網路。
* 要執行 hello 修正說明請見 KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977")。

## <a name="virtual-machine-prerequisites"></a>虛擬機器先決條件
您想 tooprotect 虛擬機器都應該符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

## <a name="provider-and-agent-prerequisites"></a>提供者和代理程式的必要條件
Azure Site Recovery 部署的一部分，將安裝 hello Azure Site Recovery Provider 和 hello Azure 復原服務代理程式的每部 HYPER-V 伺服器上。 請注意：

* 我們建議您永遠執行 hello 最新版 hello 提供者和代理程式。 這些是在 hello Site Recovery 入口網站。
* 保存庫中的所有 HYPER-V 伺服器應該有都 hello，相同的都 hello 提供者版本和代理程式。
* hello hello 伺服器上執行的提供者連接 tooSite 復原 hello 透過網際網路。 您可以不使用 proxy、 hello hello HYPER-V 伺服器上目前設定的 proxy 設定或提供者安裝期間設定的自訂 proxy 設定。 您必須確定您想要 toouse hello proxy 伺服器可存取這些 hello 來連接 Url tooAzure toomake:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* 除了允許 hello 中所述的 IP 位址[Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)和 HTTPS (443) 通訊協定。 您有 tooallow hello IP 範圍的 hello 您規劃 toouse 與美國西部的 Azure 區域。

下圖顯示 hello 不同的通訊通道與連接埠的協調流程 」 和 「 複寫使用 Site recovery

![B2A 拓樸](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>步驟 1：建立保存庫
1. 登入 toohello[管理入口網站](https://portal.azure.com)。
2. 展開 [資料服務]  >  [復原服務]，然後按一下 [Site Recovery 保存庫]。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
6. 按一下 [建立保存庫] 。

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

請檢查已成功建立 hello 保存庫的 hello 狀態列 tooconfirm。 hello 保存庫會列為**Active** hello 主要復原服務頁面上。

## <a name="step-2-create-a-hyper-v-site"></a>步驟 2：建立 Hyper-V 站台
1. 在 [hello 復原服務] 頁面上，按一下 [hello 保存庫 tooopen hello 快速入門] 頁面。 也可以使用 [hello] 圖示，隨時開啟快速入門。

    ![快速啟動](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. 在 hello 下拉式清單中，選取 **在內部部署 HYPER-V 站台與 Azure 之間**。

    ![Hyper-V 站台案例](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. 在 [建立 Hyper-V 站台] 中，按一下 [建立 Hyper-V 站台]。 指定站台名稱並儲存。

    ![Hyper-V 站台](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>步驟 3： 安裝 hello 提供者和代理程式
具有您想要 tooprotect Vm 的每部 HYPER-V 伺服器上安裝 hello 提供者和代理程式。

如果您要安裝在 HYPER-V 叢集上，執行步驟 5-11 hello 容錯移轉叢集中的每個節點上。 已註冊的所有節點，並已啟用保護之後，即使它們 hello 叢集中的節點間移轉可保護虛擬機器。

1. 在 [準備 Hyper-V 伺服器] 中，按一下 [下載註冊金鑰] 檔案。
2. 在 hello**下載註冊金鑰**頁面上，按一下**下載**下一步 toohello 站台。 下載 hello 金鑰 tooa 安全的位置，可以輕鬆地存取 hello HYPER-V 伺服器。 hello 金鑰無效，在產生後 5 天。

    ![註冊金鑰](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. 按一下**下載 hello 提供者**tooobtain hello 最新版本。
4. 執行您想要每個 HYPER-V 伺服器上的 hello 檔案 tooregister hello 保存庫中。 hello 檔案會安裝兩個元件：
   * **Azure Site Recovery Provider**— 處理通訊和協調流程之間 hello HYPER-V 伺服器和 hello Azure Site Recovery 入口網站。
   * **Azure Recovery Services Agent**— 處理 hello 來源 HYPER-V 伺服器和 Azure 儲存體上執行的虛擬機器之間的資料傳輸。
5. 在 [Microsoft Update]  中，您可以選擇加入以取得更新。 啟用此設定，將根據 tooyour Microsoft Update 原則會安裝 Provider 和 Agent 更新。

    ![Microsoft Update](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. 在**安裝**指定您想 tooinstall hello 提供者，且代理程式上的 hello HYPER-V 伺服器。

    ![安裝位置](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. 安裝完成之後繼續安裝程式 tooregister hello 伺服器 hello 保存庫中。
8. 在 hello**保存庫設定**頁面上，按一下**瀏覽**tooselect hello 金鑰檔。 指定 hello Azure Site Recovery 訂用帳戶，hello 保存庫名稱，並所屬 hello HYPER-V 站台 toowhich hello HYPER-V 伺服器。

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. 在 hello**網際網路連線**頁面上，指定 hello 提供者如何連接 tooAzure 站台復原。 選取**使用預設系統 proxy 設定**toouse hello 預設網際網路連線設定 hello 伺服器上設定。 如果您未指定值 hello 的預設值，將使用的設定。

   ![網際網路設定](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. 註冊啟動 tooregister hello 伺服器 hello 保存庫中。

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. 註冊完成中繼資料之後 hello HYPER-V 伺服器擷取 Azure Site recovery hello 伺服器上也會顯示 hello **HYPER-V 站台** 索引標籤上 hello**伺服器**hello 保存庫中的頁面。

### <a name="install-hello-provider-from-hello-command-line"></a>從 hello 命令列安裝 hello 提供者
或者您可以從 hello 命令列安裝 hello Azure Site Recovery Provider。 如果您想要執行 Windows 2012 R2 的 Server Core 的電腦上的 tooinstall hello 提供者，您應該使用這個方法。 Hello 命令列執行，如下所示：

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如 C:\ASR。
2. 以系統管理員身分開啟 [命令提示字元] 並輸入：

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. 然後執行安裝 hello 提供者：

        C:\ASR> setupdr.exe /i
4. 執行下列 toocomplete 註冊 hello:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

參數包括：

* **/ 認證**： 指定 hello hello 註冊金鑰下載位置。
* **/Friendlyname**： 指定名稱 tooidentify hello HYPER-V 主機伺服器。 這個名稱會出現在 hello 入口網站
* **/EncryptionEnabled**：選擇性。 指定是否要讓 tooencrypt 複本在 Azure 虛擬機器 （在 rest 加密）。
* **/proxyAddress**；**/proxyport**；**/proxyUsername**；**/proxyPassword**：選擇性。 如果您想 toouse 自訂 proxy，或您現有的 proxy 需要驗證，請指定 proxy 參數。

## <a name="step-4-create-an-azure-storage-account"></a>步驟 4：建立 Azure 儲存體帳戶
* 在**準備資源**選取**建立儲存體帳戶**toocreate 如果您還沒有 Azure 儲存體帳戶。 hello 帳戶應擁有啟用地理複寫。 它應該會在 hello 與 hello Azure Site Recovery 保存庫中，相同的區域，並且與相關聯 hello 相同訂用帳戶。

    ![建立儲存體帳戶](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. 我們不支援的儲存體帳戶使用 hello 建立 hello 移動[新版 Azure 入口網站](../storage/common/storage-create-storage-account.md)跨越資源群組。
> 2. [移轉儲存體帳戶](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶，或跨訂用帳戶不支援用來部署站台復原的儲存體帳戶。
>

## <a name="step-5-create-and-configure-protection-groups"></a>步驟 5：建立和設定保護群組
保護群組是邏輯群組的虛擬機器，您想要使用 tooprotect hello 相同保護設定。 套用保護設定 tooa 保護群組中，而這些設定套用的 tooall 虛擬機器將加入 toohello 群組。

1. 在 [建立和設定保護群組] 中，按一下 [建立保護群組]。 如果有任何必要條件不符，系統就會發出訊息，您可以按一下 [檢視詳細資料]  來取得詳細資訊。
2. 在 hello**保護群組**索引標籤上，新增保護群組。 指定名稱、 hello 來源 HYPER-V 站台、 hello 目標**Azure**、 您 Azure Site Recovery 訂用帳戶名稱和 hello Azure 儲存體帳戶。

    ![保護群組](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. 在**複寫設定**組 hello**複製頻率**toospecify 頻率應 hello 來源和目標之間同步處理 hello 資料差異。 您可以設定 too30 秒、 5 分鐘或 15 分鐘。
4. 在 [保留復原點]  中，指定復原歷程記錄應該儲存多少個小時。
5. 在**應用程式一致快照的頻率**您可以指定是否 tootake 快照集，使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 預設不會建立這些快照。 請確定此值設定 tooless 比 hello 您設定其他復原點數目。 如果 hello 虛擬機器正在執行 Windows 作業系統才支援此功能。
6. 在**初始複寫開始時間**指定何時 hello 保護群組中的虛擬機器的初始複寫應該會傳送 tooAzure。

    ![保護群組](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>步驟 6：啟用虛擬機器保護
新增虛擬機器 tooa 保護群組 tooenable 保護它們。

> [!NOTE]
> 不支援保護使用靜態 IP 位址執行 Linux 的 VM。
>
>

1. 在 hello**機器**hello 保護群組，按一下 * * 新增虛擬機器 tooprotection 索引標籤群組 tooenable 保護 * *。
2. 在 hello**啟用虛擬機器保護**頁面上您想 tooprotect 選取 hello 虛擬機器。

    ![啟用虛擬機器保護](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    hello 啟用保護工作開始。 您可以在 hello 上追蹤進度**作業** 索引標籤。Hello 完成保護 」 工作後執行 hello 虛擬機器已做好容錯移轉。
3. 設定保護之後，您可以：

   * 檢視中的虛擬機器**受保護項目** > **保護群組** > *protectiongroup_name*  >  **虛擬機器**您可以在 hello toomachine 詳細資料向下鑽研**屬性** 索引標籤...
   * 設定中的虛擬機器的 hello 容錯移轉屬性**受保護項目** > **保護群組** > *protectiongroup_name* > **虛擬機器** *virtual_machine_name* > **設定**。 您可以設定：

     * **名稱**: hello hello Azure 中的虛擬機器名稱。
     * **大小**: hello hello 虛擬機器的容錯移轉的目標大小。

       ![設定虛擬機器屬性](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * 在 [受保護的項目]* > [保護群組] > *protectiongroup_name* > [虛擬機器] *virtual_machine_name* > [設定] 中，設定其他虛擬機器設定，包括：

     * **網路介面卡**: hello 網路介面卡的數目取決於您指定 hello 目標虛擬機器的 hello 大小。 請檢查[虛擬機器大小規格](../virtual-machines/linux/sizes.md)hello hello 虛擬機器大小所支援的 nic 數目。

       當您開啟時，當您修改 hello 大小的虛擬機器，並儲存 hello 設定時，會變更 hello 網路介面卡數目**設定**頁面 hello 下一次。 來源虛擬機器上的網路介面卡的 hello 數目以及 hello 選擇的 hello 虛擬機器大小所支援的網路介面卡的最大數目的最小值的目標虛擬機器網路介面卡的 hello 號碼。 其說明如下：

       * 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
       * 如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
       * 例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。

     * **Azure 網路**： 指定 hello 網路 toowhich hello 虛擬機器應該容錯移轉。 如果 hello 虛擬機器具有多張網路介面卡的所有介面卡應該連接的 toohello 相同的 Azure 網路。
     * **子網路**應該 hello 虛擬機器上每個網路介面卡，容錯移轉之後連接選取 hello hello Azure 網路 toowhich hello 機器中的子網路。
     * **目標 IP 位址**: hello 的來源虛擬機器的網路介面卡是否已設定的 toouse 靜態 IP 位址則 hello 機器 hello 目標虛擬機器 tooensure 有 hello，您可以指定 hello IP 位址相同的 IP 位址，在容錯移轉之後.  如果您未指定 IP 位址將會容錯移轉的 hello 次指派任何可用的位址。 如果您指定了使用中的位址，則容錯移轉將會失敗。

     > [!NOTE]
     > [移轉網路](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間不支援的網路用來部署站台復原。
     >

     ![設定虛擬機器屬性](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>步驟 7：建立復原計畫
順序 tootest hello 部署中，您可以執行單一的虛擬機器或包含一或多個虛擬機器的復原計劃的測試容錯移轉。 [深入了解](site-recovery-create-recovery-plans.md) 如何建立復原計劃。

## <a name="step-8-test-hello-deployment"></a>步驟 8： 測試 hello 部署
有兩種方式 toorun 測試容錯移轉 tooAzure。

* **測試容錯移轉，不使用 Azure 網路**— 這種類型的測試容錯移轉會檢查該 hello 虛擬機器確實啟動 Azure 中。 hello 虛擬機器無法容錯移轉之後連接的 tooany Azure 網路。
* **測試容錯移轉與 Azure 網路**— 如預期般最多出現這種類型的 hello 整體複寫環境的容錯移轉檢查以及容錯移轉 hello 虛擬機器連線 toohello 指定的目標 Azure 網路。 請注意，測試容錯移轉的 hello hello 測試虛擬機器的子網路將會說，找出 hello 複本虛擬機器的 hello 子網路為基礎。 Hello 子網路，複本虛擬機器的基礎 hello hello 來源虛擬機器的子網路時，這是不同 tooregular 複寫。

如果您想 toorun 測試容錯移轉但不指定 Azure 網路您無須 tooprepare 任何項目。

toorun 目標 Azure 網路，您必須從您的 Azure 生產網路 （預設行為時在 Azure 中建立新的網路） toocreate 新的 Azure 網路有隔離的測試容錯移轉。 如需詳細資訊，請參閱 [執行測試容錯移轉](site-recovery-failover.md) 。

toofully 測試您將需要 tooset hello 基礎結構，因此該 hello 會如預期般複寫虛擬機器 toowork 複寫和網路部署。 一種具有 DNS 的網域控制站執行此 tootooset 的虛擬機器，並將它複製 tooAzure 使用 Site Recovery toocreate hello 測試在執行測試容錯移轉網路。  [深入了解](site-recovery-active-directory.md#test-failover-considerations) Active Directory 的測試容錯移轉考量。

執行 hello 測試容錯移轉，如下所示：

> [!NOTE]
> tooget hello 達到最佳效能時執行的容錯移轉 tooAzure，請確定您已受保護的 hello 機器中安裝 hello Azure 代理程式。 這有助於更快速開機，也有助於診斷發生的問題。 您可以在[這裡](https://github.com/Azure/WALinuxAgent)找到 Linux 代理程式，而 Windows 代理程式則可在[這裡](http://go.microsoft.com/fwlink/?LinkID=394789)找到
>
>

1. 在 hello**復原計劃**索引標籤上，選取 hello 計劃，並按一下**測試容錯移轉**。
2. 在 hello**確認測試容錯移轉**頁面上，選取**無**或特定的 Azure 網路。  請注意，如果您選取**無**hello 測試容錯移轉會檢查該 hello 虛擬機器正確複寫 tooAzure，但並不會檢查您的複寫網路組態。

    ![測試容錯移轉](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. 在 [hello**作業**] 索引標籤，您可以追蹤容錯移轉的進度。 您也應該要能夠 toosee hello 虛擬機器測試複本 hello Azure 入口網站中。 如果您設定好 tooaccess 虛擬機器從內部部署網路，您可以起始遠端桌面連線 toohello 虛擬機器。
4. 當 hello 容錯移轉到達 hello**完成測試**階段時，按一下 **完成測試**toofinish hello 測試容錯移轉。 您可以切入 toohello**作業**索引標籤上 tootrack 容錯移轉的進度和狀態，以及 tooperform 所需的任何動作。
5. 在容錯移轉之後，您會在 hello Azure 入口網站無法 toosee hello 虛擬機器測試複本。 如果您設定好 tooaccess 虛擬機器從內部部署網路，您可以起始遠端桌面連線 toohello 虛擬機器。

   1. 請確認 hello 虛擬機器成功啟動。
   2. 如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。 您也需要 tooadd hello 虛擬機器上的 RDP 端點。 您可以利用[Azure 自動化 runbook](site-recovery-runbook-automation.md) toodo 的。
   3. 容錯移轉，如果您使用公用 IP 位址 tooconnect toohello 虛擬機器使用遠端桌面，在 Azure 中確認之後，您不需要的任何網域原則，防止您連接 tooa 虛擬機器使用的公用位址。
6. Hello 測試完成之後執行 hello 下列動作：

   * 按一下**hello 測試容錯移轉已完成**。 Hello 清理測試環境 tooautomatically 電源關閉和刪除 hello 測試虛擬機器。
   * 按一下**備忘稿**toorecord 及儲存與 hello 測試容錯移轉相關聯的任何觀察。
7. 當 hello 容錯移轉到達 hello**完成測試**階段完成 hello 的驗證，如下所示：
   1. 在 hello Azure 入口網站中檢視 hello 複本虛擬機器。 請確認該 hello 虛擬機器成功啟動。
   2. 如果您設定好 tooaccess 虛擬機器從內部部署網路，您可以起始遠端桌面連線 toohello 虛擬機器。
   3. 按一下**完成 hello 測試**toofinish 它。
   4. 按一下**備忘稿**toorecord 及儲存與 hello 測試容錯移轉相關聯的任何觀察。
   5. 按一下**hello 測試容錯移轉已完成**。 Hello 清理測試環境 tooautomatically 電源關閉和刪除 hello 測試虛擬機器。

## <a name="next-steps"></a>後續步驟
在您的部署設定完成並開始執行之後， [深入了解](site-recovery-failover.md) 容錯移轉。
