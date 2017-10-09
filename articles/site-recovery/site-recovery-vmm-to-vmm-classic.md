---
title: "在 VMM tooa 次要站台 （Azure 傳統） 的 HYPER-V Vm aaaReplicate |Microsoft 文件"
description: "本文說明如何在 VMM 中的 HYPER-V Vm tooreplicate 雲端 tooa 次要 VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>將 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台複寫
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-vmm.md)
> * [傳統入口網站](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

tooyour 業務續航力和災害復原 (BCDR) 策略來協調複寫、 容錯移轉和復原的虛擬機器和實體伺服器都是計算 hello Azure Site Recovery 服務。 電腦可以是複寫的 tooAzure 或 tooa 次要內部部署資料中心。 如需快速概觀，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)

## <a name="overview"></a>概觀
本文說明如何 tooreplicate HYPER-V 虛擬機器上 HYPER-V 主機在 VMM 雲端 toosecondary VMM 站台使用 Azure Site Recovery 管理的伺服器。

hello 發行項包含必要條件，會顯示您如何註冊 Site Recovery 保存庫 tooset 安裝 hello 來源上的 Azure Site Recovery Provider 與目標 VMM 伺服器、 hello 保存庫中註冊伺服器 hello、 設定 VMM 雲端的保護設定，然後啟用HYPER-V Vm 的保護。 完成的測試 hello 容錯移轉 toomake 確定一切如預期般運作。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="architecture"></a>架構
hello 圖會顯示 hello 不同的通訊通道與連接埠的協調流程 」 和 「 複寫使用 Azure Site recovery

![E2E 拓樸](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>開始之前
確認您已備妥這些必要條件：

| **必要條件** | **詳細資料** |
| --- | --- |
| **Azure** |您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 定價。 |
| **VMM** |您至少需要一個 VMM 伺服器。<br/><br/>hello VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新累計更新。<br/><br/>如果您想 tooset 與單一 VMM 伺服器的保護，您需要至少兩個 hello 伺服器上設定的雲端。<br/><br/>如果您想 toodeploy 保護兩部 VMM 伺服器時，每一部伺服器必須設定至少一個雲端 hello 想 tooprotect 的 hello 次要 VMM 伺服器上設定一個雲端，而且主要 VMM 伺服器上您要保護和復原 toouse<br/><br/>所有 VMM 雲端都必須 hello HYPER-V 功能設定檔集合。<br/><br/>您想 tooprotect hello 來源雲端必須包含一個或多個 VMM 主機群組。 |
| **Hyper-V** |您需要 hello 主要和次要 VMM 主機群組中的一個或多個 HYPER-V 主機伺服器與每部 HYPER-V 主機伺服器上的一個或多個虛擬機器。<br/><br/>hello 主機與目標 HYPER-V 伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。<br/><br/>您所要的任何包含 Vm 的 HYPER-V 伺服器 tooprotect 必須位於 VMM 雲端。<br/><br/>如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。 必須以手動方式 tooconfigure hello 叢集代理人。 在 Aidan Finn 的部落格項目中[深入了解](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters)。 |
| **網路對應** |您可以設定網路對應 toomake 確定容錯移轉之後，以最佳方式次要 HYPER-V 主機伺服器上置於複寫的虛擬機器，而且它們可以連接 tooappropriate VM 網路。 如果您未設定網路對應，複本 Vm 將容錯移轉之後無法連接的 tooany 網路。<br/><br/>tooset 網路對應，在部署期間，請確定 hello hello 來源 HYPER-V 主機伺服器上的虛擬機器的連線的 tooa VMM VM 網路。 該網路應連結的 tooa 與 hello 雲端相關聯的邏輯網路 < b /<br/>hello hello 次要 VMM 伺服器上您用於復原的目標雲端應該有對應的 VM 網路設定，並接著應該連結的 tooa 對應與 hello 目標雲端相關聯的邏輯網路。 |
| **儲存體對應** |根據預設複寫來源 HYPER-V 主機伺服器 tooa 目標 HYPER-V 主機伺服器上的虛擬機器時複寫的資料儲存在 hello hello 目標 HYPER-V 主機在 HYPER-V 管理員中指定的預設位置。 如果要進一步控制複寫資料的儲存位置，您可以設定儲存體對應<br/><br/> tooconfigure 儲存體對應，您需要 tooset 向上 hello 來源上的存放裝置分類和目標 VMM 伺服器在開始部署之前。 |

## <a name="step-1-create-a-site-recovery-vault"></a>步驟 1：建立 Site Recovery 保存庫
1. 登入 toohello[管理入口網站](https://portal.azure.com)想 tooregister 從 hello VMM 伺服器。
2. 展開 [資料服務]  >  [復原服務]，然後按一下 [Site Recovery 保存庫]。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](http://go.microsoft.com/fwlink/?LinkId=389880)。
6. 按一下 [建立保存庫] 。

    ![建立保存庫](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

已建立該 hello 保存庫的 hello 狀態列中的核取。 hello 保存庫會列為**Active** hello 主要復原服務頁面上。

## <a name="step-2-generate-a-vault-registration-key"></a>步驟 2：產生保存庫註冊金鑰
Hello 保存庫中產生註冊金鑰。 您下載 hello Azure Site Recovery Provider，並將它安裝在 hello VMM 伺服器之後，您將使用此索引鍵 tooregister hello VMM 伺服器 hello 保存庫中。

1. 在 [hello**復原服務**頁面上，按一下 hello 保存庫 tooopen hello 快速入門] 頁面。 也可以使用 [hello] 圖示，隨時開啟快速入門。

    ![快速啟動圖示](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. 在 hello 下拉式清單中，選取 **兩個內部部署 VMM 站台之間**。
3. 在 [準備 VMM 伺服器] 中，按一下 [產生註冊金鑰檔案]。 hello 金鑰檔案會自動產生並有效產生後 5 天。 如果您不從 hello VMM 伺服器存取 hello Azure 入口網站您需要 toocopy toohello 中此檔案伺服器。

    ![註冊金鑰](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>步驟 3： 安裝 hello Azure Site Recovery Provider
1. 在 hello**快速入門**頁面上，於**準備 VMM 伺服器**，按一下**下載 Microsoft Azure Site Recovery Provider 安裝於 VMM 伺服器上**tooobtain hello 最新版本hello 提供者安裝檔案的版本。
2. 執行這個 hello 來源 VMM 伺服器上的檔案。

   > [!NOTE]
   > 如果 VMM 部署在叢集中，且您要安裝的 hello hello 提供者在第一次將它安裝在作用中的節點，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。 然後 hello 提供者上安裝 hello 其他節點。 請注意，如果您要升級提供者，您需要的所有節點上 tooupgrade，因為它們應該全部是的 hello 執行 hello 相同的提供者版本。
   >
   >
3. hello 安裝程式沒有一些**先決條件檢查**和權限 toostop hello VMM 服務 toobegin Provider 安裝程式的要求。 hello VMM 服務將會自動重新啟動安裝程式完成時。 如果您要安裝上 VMM 叢集，您應該會提示您 toostop hello 叢集角色。
4. 在 [Microsoft Update]  中，您可以選擇加入以取得更新。 這項設定將根據 tooyour Microsoft Update 原則會安裝已啟用的提供者更新。

    ![Microsoft Update](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. hello 安裝位置設定得**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**。 按一下 hello 安裝按鈕 toostart 安裝 hello 提供者。

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. 在已安裝提供者的 hello 之後按**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. 在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。 按一下 [下一步] 。

    ![伺服器註冊](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. 在**網際網路連線**指定如何 hello hello VMM 上執行提供者伺服器連接 toohello 網際網路。 選取**利用現有的 proxy 設定連線**toouse hello 預設網際網路連線設定 hello 伺服器上設定。

    ![網際網路設定](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * 如果您想 toouse 自訂 proxy，您應該設定它，然後安裝 hello 提供者。 當您設定自訂 proxy 設定 toocheck hello proxy 連線將會執行測試。
   * 如果您使用自訂 proxy，或您的預設 proxy 需要驗證您需要 tooenter hello proxy 詳細資料，包括 hello proxy 位址和連接埠。
   * 下列 url 必須能夠存取 hello VMM 伺服器與 hello 與 hyper-v 主機
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * 允許 hello 中所述的 IP 位址[Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 通訊協定。 您必須 toowhite 清單 IP 範圍的 hello 您規劃 toouse 與美國西部的 Azure 區域。
   * 如果您使用自訂 proxy 將使用指定的 hello 自動建立 VMM RunAs 帳戶 (DRAProxyAccount) proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。 hello VMM 主控台中，可以修改 hello VMM RunAs 帳戶的設定。 toodo，開啟 hello**設定**工作區中，展開 **安全性**，按一下 **執行身分帳戶**，然後修改 draproxyaccount 的 hello 密碼。 您將需要 toorestart hello VMM 服務，讓這項設定會生效。
9. 在**登錄機碼**，選取您從 Azure Site Recovery 下載並複製 toohello VMM 伺服器的 hello 索引鍵。
10. 只有在您要在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時，才會使用 hello 加密設定。 如果您要複寫 tooa 次要站台不使用它。
11. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中指定 hello VMM 叢集角色名稱。
12. 在**同步處理雲端中繼資料**選取是否要在 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端的 toosynchronize 中繼資料。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。
13. 按一下**下一步**toocomplete hello 程序。 註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 在中，會顯示 hello 伺服器**VMM 伺服器** > **伺服器**hello 保存庫中。

    ![伺服器](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>命令列安裝
hello Azure Site Recovery 提供者也可以從 hello 命令列安裝。 這個方法可以是使用的 tooinstall hello 的提供者的 Windows Server 2012 R2 的 Server CORE 上。

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如 C:\ASR。
2. 停止 hello System Center Virtual Machine Manager 服務
3. 從命令提示字元執行這些命令擷取 hello 提供者安裝程式**管理員**權限：

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. 執行安裝 hello 提供者：

        C:\ASR> setupdr.exe /i
5. 執行註冊 hello 提供者：

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

其中 hello 參數如下：

* **/ 認證**： 指定 hello 位置中的 hello 註冊金鑰檔所在的必要參數  
* **/Friendlyname**: hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要參數。
* **/ EncryptionEnabled**： 您需要 toouse 只能在 hello VMM tooAzure 案例中的，如果您需要您的虛擬機器，在 Azure 中的靜止的加密的選擇性參數。 請確定該 hello 檔案的名稱 hello 您提供具有**.pfx**延伸模組。
* **/proxyAddress**： 指定 hello hello proxy 伺服器位址的選擇性參數。
* **/proxyport**： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。
* **/proxyUsername**： 指定 hello Proxy 使用者名稱 （如果 proxy 需要驗證） 的選擇性參數。
* **/proxyPassword**： 指定的選擇性參數 hello 密碼進行驗證的 hello proxy 伺服器 （proxy 需要驗證）。  

## <a name="step-4-configure-cloud-protection-settings"></a>步驟 4：設定雲端保護設定
註冊 VMM 伺服器之後，您就可以設定雲端保護設定。 如果您啟用 hello 選項**hello 保存庫同步處理雲端資料**當您安裝提供者 hello hello VMM 伺服器上的所有雲端就會出現在 hello**受保護項目**hello 保存庫中的索引標籤。 如果未指定您可以同步處理特定雲端與 Azure Site Recovery 中 hello**一般**hello VMM 主控台中的 hello 雲端屬性頁面 索引標籤。

![發佈的雲端](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. 在 hello 快速入門 頁面上，按一下 **設定 VMM 雲端的保護**。
2. 在 [hello **VMM 雲端**索引標籤上，選取您想 tooconfigure，並移 toohello hello 雲端**組態**] 索引標籤。
3. 在 [目標] 中，選取 [VMM]。
4. 在**目標位置**，選取 hello 站上管理您想要復原 toouse hello 雲端的 VMM 伺服器。
5. 在**目標雲端**，選取您想 toouse hello 來源雲端中的虛擬機器進行容錯移轉的 hello 目標雲端。 請注意：

   * 我們建議您選取符合復原需求的 hello 將保護的虛擬機器的目標雲端。
   * 雲端可以只隸屬 tooa 單一雲端配對-做為主要或目標雲端。
6. 在 [複製頻率] 中，指定資料應該在來源與目標位置之間同步處理的頻率。 請注意，這項設定時才相關 hello HYPER-V 主機正在執行 Windows Server 2012 R2。 對於其他伺服器，使用預設設定的 5 分鐘即可。
7. 在**其他復原點**，指定是否要讓 toocreate 其他點。 hello 預設零值表示只 hello 最近復原點的主要虛擬機器會儲存在複本主機伺服器上。 請注意，啟用多個復原點需要額外的存放裝置 hello 快照集儲存在每個復原點。 根據預設，每個小時都會建立復原點，所以每個復原點都包含一小時有價值的資料。 hello hello VMM 主控台中的虛擬機器指派的 hello 復原點值不應該小於您在 hello Azure Site Recovery 主控台中指派的 hello 值。
8. 在**應用程式一致快照的頻率**，指定頻率 toocreate 應用程式一致快照集。 HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 請注意，是否您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。

    ![進行保護設定](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. 在 [資料傳輸壓縮] 中，指定是否應該將傳輸的已複寫資料壓縮。
10. 在**驗證**，指定如何驗證主要 hello 和復原 HYPER-V 主機伺服器之間的流量。 除非您已設定可用的 Kerberos 環境，否則請選取 HTTPS。 Azure Site Recovery 會自動設定用於 HTTPS 驗證的憑證。 不需要進行任何手動設定。 如果您選取 Kerberos，Kerberos 票證會用於相互驗證的 hello 主機伺服器。 根據預設，將 hello HYPER-V 主機伺服器上的 hello Windows 防火牆中開啟連接埠 8083 和 8084 （用於憑證）。 請注意，這項設定只有在 Hyper-V 主機伺服器是執行於 Windows Server 2012 R2 時才有重要性。
11. 在**連接埠**、 修改 hello 通訊埠編號上的 hello 來源和目標主機電腦接聽複寫流量。 例如，您可能會修改 hello 設定，如果您想 tooapply 服務品質 (QoS) 網路頻寬節流處理複寫流量。 請檢查 hello 連接埠不使用任何其他應用程式，而且它是在 hello 防火牆設定中開啟。
12. 在**複寫方法**，指定 hello 初始複寫的資料從來源 tootarget 位置將，如何處理一般複寫開始之前：

    * **透過網路**— hello 網路上進行複製的資料可能既費時又需要大量資源。 我們建議您如果 hello 雲端包含虛擬機器具有相對較小虛擬硬碟，而且 hello 主要站台是透過具有大量頻寬連線連接的 toohello 次要站台時，才使用此選項。 您可以指定 hello 複製應立即啟動，或選取的時間。 如果您使用網路複寫，建議您排在離峰時段進行。
    * **離線**— 此方法可讓您指定要執行 hello 初始複寫使用外部媒體。 如果您想要 tooavoid 網路效能降低，或是針對遠端地理位置，就會很有用。 toouse 這個 hello 來源雲端與 hello 匯入位置 hello 目標雲端上的指定 hello 匯出位置的方法。 當您啟用虛擬機器的保護時，虛擬硬碟 hello 是複製的 toohello 指定匯出位置。 您將它送出 toohello 目標網站，並將它複製 toohello 匯入位置。 hello 系統複製 hello 匯入資訊 toohello 複本虛擬機器。
13. 選取**刪除複本虛擬機器**hello 複本虛擬機器的 toospecify 應該刪除，如果您停止保護 hello 虛擬機器選取 hello**刪除 hello 虛擬機器的保護** hello 虛擬機器 索引標籤上的 hello 雲端屬性的選項。 啟用此設定，當您停用會從 Azure Site Recovery 移除保護 hello 虛擬機器、 在 hello VMM 主控台中，移除 hello hello 虛擬機器的 Site Recovery 設定與 hello 複本被刪除。

    ![進行保護設定](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

儲存 hello 設定之後作業將會建立，您可以在 hello 監視**作業** 索引標籤。Hello VMM 來源雲端中的所有 HYPER-V 主機伺服器將會都設定為複寫。 可以在 hello 上修改雲端設定**設定** 索引標籤。如果您想 toomodify hello 目標位置或目標雲端必須移除 hello 雲端組態，然後再重新設定 hello 雲端。

### <a name="prepare-for-offline-initial-replication"></a>準備進行離線初始複寫
您必須遵循離線初始複寫的動作 tooprepare toodo hello:

* Hello 來源伺服器上，您會指定從哪個 hello 資料匯出，就會進行的路徑位置。 指派 「 完整控制 NTFS 和共用權限 toohello hello 匯出路徑上的 VMM 服務。 在 hello 目標伺服器上，您會指定要從中 hello 資料匯入的路徑位置就會發生。 指派 hello 這個匯入路徑上的相同權限。
* 如果 hello 匯入或匯出路徑共用，指派 hello 遠端電腦上的 hello VMM 服務帳戶的系統管理員、 Power User、 列印操作員或伺服器操作員群組成員資格位於上共用的 hello。
* 如果您使用的任何執行身分帳戶 tooadd 主機，hello 上匯入和匯出路徑、 指派讀取和寫入權限 toohello 執行身分帳戶在 VMM 中。
* hello 匯入和匯出共用應該位於任何做為 HYPER-V 主機伺服器的電腦因為 HYPER-V 不支援回送設定。
* 在每個包含您想 tooprotect，虛擬機器的 HYPER-V 主機伺服器上的 Active Directory 中啟用及設定限制的委派 tootrust hello 遠端電腦上的 hello 匯入和匯出路徑，如下：
  1. 在 hello 網域控制站上開啟**Active Directory 使用者和電腦**。
  2. 在 hello 主控台樹狀目錄中按一下**DomainName** > **電腦**。
  3. 以滑鼠右鍵按一下 hello HYPER-V 主機伺服器名稱 >**屬性**。
  4. 在 hello**委派**索引標籤上按一下 T**rust 這台電腦所委派 toospecified 服務只**。
  5. 按一下 [使用任何驗證通訊協定] 。
  6. 按一下 [新增]  > 提出技術問題。
  7. 型別 hello 裝載 hello 匯出路徑的 hello 電腦名稱 >**確定**。從 hello 的可用服務清單，請在按住 hello CTRL 鍵，然後按一下  **cifs** > **確定**。 Hello 電腦名稱的 hello 重複該主機 hello 匯入路徑。 視需要為其他 Hyper-V 主機伺服器重複動作。

## <a name="step-5-configure-network-mapping"></a>步驟 5：設定網路對應
1. 在 hello 快速入門 頁面上，按一下 **對應網路**。
2. 選取您想 toomap 網路與然後 hello 要對應網路的目標 VMM 伺服器 toowhich hello hello 來源 VMM 伺服器。 會顯示來源網路及其相關聯的目標網路的 hello 清單。 目前尚未對應的網路會顯示空白值。
3. 在 [來源上的網路]  >  [對應] 中選取網路。 hello 服務會偵測 hello hello 目標伺服器上的 VM 網路，並加以顯示。 按一下 hello 資訊圖示下一步 toohello 來源和目標網路名稱 tooview hello 子網路的每個網路。

    ![設定網路對應](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Hello 對話方塊中選取其中一個 hello VM 網路從 hello 目標 VMM 伺服器。

    ![選取目標網路](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. 當您選取的目標網路時，hello 使用 hello 來源網路的受保護的雲端會顯示。 也會顯示與用於保護的 hello 雲端相關聯的可用目標網路。 我們建議您選取可用的 tooall hello 雲端都可以使用保護的目標網路。 或者，您也可以移 toohello VMM 伺服器，然後修改 hello 雲端屬性 tooadd hello 邏輯網路對應的 toochoose toohello vm 網路。
6. 按一下 hello 核取記號 toocomplete hello 對應處理序。 作業會啟動 tootrack hello 對應進度。 您可以檢視其 hello**作業** 索引標籤。

## <a name="step-6-configure-storage-mapping"></a>步驟 6：設定儲存體對應
根據預設複寫來源 HYPER-V 主機伺服器 tooa 目標 HYPER-V 主機伺服器上的虛擬機器時複寫的資料儲存在 hello hello 目標 HYPER-V 主機在 HYPER-V 管理員中指定的預設位置。 如果要進一步控制複寫資料的儲存位置，您可以用以下方式設定儲存體對應：

1. 在這兩個 hello 來源上定義的儲存體分類和目標 VMM 伺服器。 [深入了解](https://technet.microsoft.com/library/gg610685.aspx)。 分類必須是來源和目標雲端中的可用 toohello HYPER-V 主機伺服器。 分類不需 toohave hello 相同類型的儲存體。 例如，您可以對應來源分類，其中包含 SMB 共用 tooa 目標分類包含 Csv。
2. 設定分類之後，您就可以建立對應。 toodo 這在 hello**快速入門**頁面 >**對應儲存**。
3. 按一下 hello**儲存體** 索引標籤 >**對應儲存體分類**。
4. 在 hello**對應儲存體分類**索引標籤上，選取分類 hello 來源與目標 VMM 伺服器。 儲存您的設定。

    ![選取目標網路](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>步驟 7：啟用虛擬機器保護
伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。

1. 在 hello**虛擬機器**索引標籤中的 hello 虛擬機器所在的 hello 雲端中，按一下**啟用保護** > **新增虛擬機器**。
2. 從 hello hello 雲端中虛擬機器清單，選取 hello 其中一個要 tooprotect。

    ![啟用虛擬機器保護](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. 追蹤進度 hello 啟用保護 」 動作 hello**作業**索引標籤上，包括 hello 初始複寫。 Hello 完成保護 」 工作後執行 hello 虛擬機器已做好容錯移轉。 啟用保護，並複寫虛擬機器之後，您會無法 tooview 他們在 Azure 中。

    ![虛擬機器保護工作](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> 您也可以啟用 hello VMM 主控台中的虛擬機器的保護。 按一下**啟用保護**hello hello 工具列上**Azure Site Recovery** hello 虛擬機器內容 索引標籤。
>
>

### <a name="on-board-existing-virtual-machines"></a>加入現有的虛擬機器
如果您有現有的虛擬機器在 VMM 中要與 HYPER-V 複本複寫，您將需要 tooonboard 以供 Azure Site Recovery 保護，如下所示：

1. 請確認您有主要和次要雲端。 請確認裝載現有虛擬機器 hello hello HYPER-V 伺服器位於 hello 主要雲端，然後裝載 hello 複本虛擬機器的 hello HYPER-V 伺服器位於 hello 次要雲端。 請確定您已設定 hello 雲端的保護設定。 hello 設定應符合目前為 HYPER-V 複本設定。 否則虛擬機器複寫可能無法如預期般運作。
2. 然後啟用 hello 主要虛擬機器的保護。 Azure Site Recovery 和 VMM 可確保 hello 相同的複本主機和虛擬機器偵測到，而且 Azure Site Recovery 會重複使用及重新建立複寫使用雲端組態設定期間的 hello 設定。

## <a name="test-your-deployment"></a>測試您的部署
tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器並執行測試容錯移轉的 hello。  測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。

### <a name="create-a-recovery-plan"></a>建立復原計畫
1. 在 hello**復原計劃**索引標籤上，按一下 **建立復原計劃**。
2. 指定 hello 復原計劃，以及來源和目標 VMM 伺服器的名稱。 hello 來源伺服器必須具有啟用容錯移轉和復原的虛擬機器。 選取**HYPER-V** tooview 僅雲端設定的 HYPER-V 複寫。

    ![建立復原計畫](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. 在 [選取虛擬機器] 中，選取複寫群組。 Hello 複寫群組相關聯的所有虛擬機器將會選取並加入 toohello 復原計劃。 這些虛擬機器會新增 toohello 復原計劃預設群組-群組 1。 您可以視需要新增更多群組。 請注意，當複寫虛擬機器，將會啟動根據 hello hello 復原計畫群組順序。

    ![新增虛擬機器](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

在建立復原方案之後，它會顯示 hello hello 清單中**復原計劃** 索引標籤。

### <a name="run-a-test-failover"></a>執行測試容錯移轉
1. 在 hello**復原計劃**索引標籤上，選取 hello 計劃，並按一下**測試容錯移轉**。
2. 在 hello**確認測試容錯移轉**頁面上，選取**無**。 請注意，使用此選項時啟用的 hello 容錯移轉複本虛擬機器將不會連接的 tooany 網路。 這將會測試，如預期般超過 hello 虛擬機器失敗，但不會測試您的複寫網路環境。 看看過[執行測試容錯移轉](site-recovery-failover.md)如需有關如何 toouse 不同的網路功能選項。
3. hello 測試虛擬機器將建立的 hello 相同裝載為複本虛擬機器有哪些 hello hello 主機上。 它會加入 toohello 相同的 hello 中複本虛擬機器所在的雲端。

### <a name="run-a-recovery-plan"></a>執行復原計畫
複寫 hello 複本虛擬機器可能沒有為 hello 的 IP 位址之後 hello IP 位址的相同 hello 主要虛擬機器。 虛擬機器將會更新他們使用的 hello DNS 伺服器啟動之後。 您也可以加入指令碼 tooupdate hello DNS 伺服器 tooensure 即時更新。

#### <a name="script-tooretrieve-hello-ip-address"></a>指令碼 tooretrieve hello IP 位址
執行這個範例指令碼 tooretrieve hello IP 位址。

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>指令碼 tooupdate DNS
執行這個範例指令碼 tooupdate DNS，指定 hello 的 IP 位址擷取使用 hello 先前的範例指令碼。

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Site Recovery 的隱私權資訊
本節中的 hello Microsoft Azure Site Recovery 服務 （「 服務 」） 的其他隱私權資訊。 tooview hello 隱私權聲明，Microsoft Azure 服務，請參閱[Microsoft Azure 隱私權聲明](http://go.microsoft.com/fwlink/?LinkId=324899)

**功能：註冊**

* **作用**：向服務註冊伺服器，如此可以保護虛擬機器
* **收集資訊**： 之後註冊的 hello 服務會收集、 處理及傳輸從 hello tooprovide 災害復原使用 hello hello VMM 伺服器，服務名稱指定的 VMM 伺服器的管理憑證資訊與 VMM 伺服器上的虛擬機器雲端 hello 名稱。
* **資訊的用途**：

  * 管理憑證，這用 toohelp 識別及驗證存取 toohello 服務的 hello 註冊 VMM 伺服器。 hello 服務會使用 hello 公開金鑰部分 hello 憑證 toosecure 只 hello 的語彙基元註冊 VMM 伺服器可以存取。 hello 伺服器需要 toouse 這個語彙基元 toogain 存取 toohello 服務功能。
  * Hello VMM 伺服器的名稱 — hello VMM 伺服器名稱是必要的 tooidentify 和與 hello 哪些 hello 雲端位於適當 VMM 伺服器通訊。
  * Hello VMM 伺服器中的雲端名稱： hello 雲端名稱時，需要使用 hello 服務雲端配對/取消配對功能如下所述。 當您決定 toopair 主要資料中心的雲端，與 hello 復原資料中心中的另一個雲端時，則會顯示 hello hello 復原資料中心的所有 hello 雲端名稱。
* **選擇**： 這項資訊是 hello 服務註冊程序中不可或缺的一部分，因為它可協助您和 hello 服務 tooidentify hello VMM 伺服器，您想 tooprovide Azure Site Recovery 保護，因為 tooidentify hello正確註冊的 VMM 伺服器。 如果您不想 toosend 此資訊 toohello 服務，不會使用此服務。 如果您註冊您的伺服器，並稍後想 toounregister，您可以從 hello 服務入口網站 （也就是 hello Azure 入口網站) 刪除 hello VMM 伺服器資訊。

**功能：啟用 Azure Site Recovery 保護**

* **其用途**: hello hello VMM 伺服器上安裝 Azure Site Recovery Provider 是 hello 管道來與 hello 服務進行通訊。 hello 提供者是在 hello VMM 程序中裝載的動態連結程式庫 (DLL)。 安裝提供者的 hello 之後, 取得 hello VMM 系統管理員主控台中啟用 hello 「 資料中心復原 」 功能。 在雲端中任何新的或現有虛擬機器可啟用名為 「 資料中心復原 」 的屬性 toohelp 保護 hello 虛擬機器。 這個屬性設定之後，hello 提供者會傳送 hello 名稱和識別碼 hello 虛擬機器 toohello 服務。 hello 虛擬保護是由 Windows Server 2012 或 Windows Server 2012 R2 HYPER-V 複寫技術所啟用的。 從一個 HYPER-V 主機 tooanother （通常位於不同的 「 復原 」 資料中心），取得複寫 hello 虛擬機器資料。
* **收集資訊**: hello 服務會收集、 處理序，並將傳送 hello 虛擬機器，其中包含 hello 名稱、 識別碼、 虛擬網路，以及 hello hello 雲端名稱的中繼資料它所屬。
* **資訊的用途**: hello 服務服務 」 入口網站上使用 hello 上述資訊 toopopulate hello 虛擬機器資訊。
* **選擇**： 這是 hello 服務不可或缺的一部分，而且無法關閉。 如果您不想傳送 toohello 服務這項資訊，請勿啟用任何虛擬機器的 Azure Site Recovery 保護。 請注意，透過 HTTPS 傳送 hello 提供者 toohello 服務所傳送的所有資料。

**功能：復原計畫**

* **其用途**： 這項功能可協助您 toobuild hello 「 復原 」 資料中心協調流程方案。 您可以定義 hello 順序中的 hello 虛擬機器或虛擬機器群組應該啟動在 hello 復原站台。 您也可以指定執行時，任何自動化的指令碼 toobe 或復原每個虛擬機器 hello 時採取的任何手動動作 toobe。 容錯移轉 （涵蓋在 hello 下一節） 通常是在 hello 復原計劃協調的復原層級觸發。
* **收集資訊**: hello 服務會收集、 處理序，並將傳送 hello 復原計劃，包括虛擬機器中繼資料和中繼資料的任何自動化指令碼和手動動作備註的中繼資料。
* **資訊的用途**: hello 上面所述的中繼資料是使用的 toobuild hello 復原計劃服務 」 入口網站中。
* **選擇**： 這是 hello 服務不可或缺的一部分，而且無法關閉。 如果您不想傳送 toohello 服務這項資訊，不建立復原方案中這項服務。

**功能：網路對應**

* **其用途**： 這項功能可讓您從 hello 主要資料中心 toohello 復原資料中心 toomap 網路資訊。 Hello 虛擬機器會復原 hello 復原站台上，這項對應有助於為其建立的網路連線。
* **收集資訊**: hello 網路對應功能的一部分，hello 服務會收集、 處理或傳輸 hello hello 邏輯網路，每個站台 （主要和 datacenter） 的中繼資料。
* **資訊的用途**: hello 服務會使用 hello 中繼資料 toopopulate 服務 」 入口網站，您可以將對應 hello 網路資訊。
* **選擇**： 這是 hello 服務不可或缺的一部分，而且無法關閉。 如果您不想傳送 toohello 服務這項資訊，請勿使用 hello 網路對應功能。

**功能：容錯移轉 - 已規畫、未規劃、測試**

* **其用途**： 這項功能有助於從一個 VMM 管理的資料中心 tooanother VMM 受管理的資料中心的虛擬機器容錯移轉。 hello 容錯移轉動作會觸發 hello 使用者在其服務入口網站上。 在容錯移轉的可能原因包括未計劃的事件 (例如在 hello 大小寫的自然的 disaster0; 計劃的事件 （例如資料中心負載平衡），則測試容錯移轉 （例如復原方案演習）。

hello VMM 伺服器上的 hello 提供者取得的 hello hello 服務，事件通知，並且 hello HYPER-V 主機上透過 VMM 介面執行容錯移轉動作。 Hello 從一個 HYPER-V 主機 tooanother （通常在不同 「 復原 」 資料中心執行） 的虛擬機器實際容錯移轉是由 hello Windows Server 2012 或 Windows Server 2012 R2 HYPER-V 複寫技術所處理。 Hello 容錯移轉已完成之後，hello hello hello 「 復原 」 資料中心的 VMM 伺服器上安裝的提供者會傳送 hello 成功資訊 toohello 服務。

* **收集資訊**: hello 服務服務 」 入口網站上使用 hello hello 容錯移轉動作資訊的資訊 toopopulate hello 狀態上方。
* **資訊的用途**: hello 服務會使用上述資訊 hello，如下所示：

  * 管理憑證，這用 toohelp 識別及驗證存取 toohello 服務的 hello 註冊 VMM 伺服器。 hello 服務會使用 hello 公開金鑰部分 hello 憑證 toosecure 只 hello 的語彙基元註冊 VMM 伺服器可以存取。 hello 伺服器需要 toouse 這個語彙基元 toogain 存取 toohello 服務功能。
  * Hello VMM 伺服器的名稱 — hello VMM 伺服器名稱是必要的 tooidentify 和與 hello 哪些 hello 雲端位於適當 VMM 伺服器通訊。
  * Hello VMM 伺服器中的雲端名稱： hello 雲端名稱時，需要使用 hello 服務雲端配對/取消配對功能如下所述。 當您決定 toopair 主要資料中心的雲端，與 hello 復原資料中心中的另一個雲端時，則會顯示 hello hello 復原資料中心的所有 hello 雲端名稱。
* **選擇**： 這是 hello 服務不可或缺的一部分，而且無法關閉。 如果您不想傳送 toohello 服務這項資訊，請勿使用此服務。

## <a name="next-steps"></a>後續步驟
您已經執行您的環境是否正常運作，測試容錯移轉 toocheck 之後[深入了解](site-recovery-failover.md)不同類型的容錯移轉。
