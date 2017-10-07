---
title: "在 VMM 雲端 tooAzure aaaReplicate HYPER-V 虛擬機器 |Microsoft 文件"
description: "本文說明如何為 HYPER-V 主機上的 tooreplicate HYPER-V 虛擬機器位於 System Center VMM 雲端 tooAzure。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>在 VMM 雲端 tooAzure 複寫 HYPER-V 虛擬機器
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-azure.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [傳統入口網站](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - 傳統](site-recovery-deploy-with-powershell.md)
>
>

tooyour 業務續航力和災害復原 (BCDR) 策略來協調複寫、 容錯移轉和復原的虛擬機器和實體伺服器都是計算 hello Azure Site Recovery 服務。 電腦可以是複寫的 tooAzure 或 tooa 次要內部部署資料中心。 如需快速概觀，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)

## <a name="overview"></a>概觀
本文說明 toodeploy Site Recovery tooreplicate HYPER-V 虛擬機器上 HYPER-V 主機伺服器位於 VMM 私人雲端 tooAzure 的方式。

hello 發行項包含 hello 案例的先決條件，並示範您如何註冊 Site Recovery 保存庫 tooset 取得 hello hello 來源 VMM 伺服器上，安裝 Azure Site Recovery Provider hello 保存庫中註冊伺服器 hello、 新增 Azure 儲存體帳戶、 安裝 helloAzure 復原服務代理程式在 HYPER-V 主機伺服器，設定將套用的 tooall 受保護的虛擬機器，並再啟用保護這些虛擬機器的 VMM 雲端的保護設定。 完成的測試 hello 容錯移轉 toomake 確定一切如預期般運作。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="architecture"></a>架構
![架構](./media/site-recovery-vmm-to-azure-classic/topology.png)

* hello Azure Site Recovery Provider hello VMM 上安裝站台復原 」 部署期間，hello Site Recovery 保存庫中登錄 hello VMM 伺服器。 hello 提供者會與站台復原 toohandle 複寫協調流程通訊。
* 在站台復原 」 部署期間 hello Azure 復原服務代理程式安裝在 HYPER-V 主機伺服器上。 它會處理資料複寫 tooAzure 的儲存體。

## <a name="azure-prerequisites"></a>Azure 必要條件
以下是您在 Azure 中需要的內容。

| **必要條件** | **詳細資料** |
| --- | --- |
| **Azure 帳戶** |您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。 |
| **Azure 儲存體** |您將需要 Azure 儲存體帳戶 toostore 複寫資料。 複寫的資料會儲存在 Azure 儲存體，容錯移轉時會啟動 Azure VM。 <br/><br/>您需要一個[標準異地備援儲存體帳戶](../storage/common/storage-redundancy.md#geo-redundant-storage)。 hello 帳戶必須是在 hello 與 hello Site Recovery 服務相同的區域和與其相關聯 hello 相同訂用帳戶。 請注意，目前不支援複寫 toopremium 儲存體帳戶，而且不應使用。<br/><br/>[深入了解](../storage/common/storage-introduction.md) Azure 儲存體。 |
| **Azure 網路** |您必須將連接 Azure Vm 的 Azure 虛擬網路 toowhen 容錯移轉，就會發生。 hello Azure 虛擬網路必須在 hello 與 hello Site Recovery 保存庫相同的區域。 |

## <a name="on-premises-prerequisites"></a>內部部署必要條件
以下是您在內部部署中需要的內容。

| **必要條件** | **詳細資料** |
| --- | --- |
| **VMM** |您需要至少一部部署為實體或虛擬獨立伺服器，或是部署為虛擬叢集的 VMM 伺服器。 <br/><br/>hello VMM 伺服器應執行 System Center 2012 R2 hello 最新累計更新。<br/><br/>您必須至少一個 hello VMM 伺服器上設定的雲端。<br/><br/>您想 tooprotect hello 來源雲端必須包含一個或多個 VMM 主機群組。<br/><br/>若要深入了解如何設定 VMM 雲端，請參閱 Keith Mayer 部落格上的[逐步解說：使用 System Center 2012 SP1 VMM 建立私人雲端](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)。 |
| **Hyper-V** |您將需要一個或多個 HYPER-V 主機伺服器 hello VMM 雲端中的叢集。 hello 主機伺服器應該要有一個或多個 vm。 <br/><br/>hello HYPER-V 伺服器必須執行至少**Windows Server 2012 R2**與 hello HYPER-V 角色或**Microsoft HYPER-V Server 2012 R2**和擁有 hello 安裝最新的更新。<br/><br/>您所要的任何包含 Vm 的 HYPER-V 伺服器 tooprotect 必須位於 VMM 雲端。<br/><br/>如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。 您以手動方式將需要 tooconfigure hello 叢集代理人。 在 Aidan Finn 的部落格項目中[深入了解](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters)。 |
| **受保護的機器** | 您想要 tooprotect 應遵守的 Vm [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。 |

## <a name="network-mapping-prerequisites"></a>網路對應的必要條件
當您保護 Azure 網路對應中的虛擬機器 hello 來源 VMM 伺服器上的 VM 網路和目標 Azure 網路 tooenable hello 下列之間進行對應：

* 所有容錯移轉 hello 相同的電腦網路可以連接 tooeach 其他，無論它們是在復原計劃。
* 如果網路閘道設定 hello 目標 Azure 網路上，虛擬機器可以連接 tooother 在內部部署虛擬機器。
* 如果您未設定網路對應，只有容錯移轉 hello 中相同的虛擬機器容錯移轉 tooAzure 後，即可能 tooconnect tooeach 其他復原方案。

如果您想 toodeploy 網路對應，您將需要下列 hello:

* hello 想 tooprotect hello 來源 VMM 伺服器上的虛擬機器應連接的 tooa VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
* Azure 網路 toowhich 複寫虛擬機器可以容錯移轉之後連接。 在 hello 容錯移轉期間，會選取此網路。 hello 網路應位於 hello 與 Azure Site Recovery 訂用帳戶相同的區域。


在 VMM 中準備網路：

   * [設定邏輯網路](https://technet.microsoft.com/library/jj721568.aspx)。
   * [設定 VM 網路](https://technet.microsoft.com/library/jj721575.aspx)。


## <a name="step-1-create-a-site-recovery-vault"></a>步驟 1：建立 Site Recovery 保存庫
1. 登入 toohello[管理入口網站](https://portal.azure.com)想 tooregister 從 hello VMM 伺服器。
2. 按一下 [資料服務] > [復原服務] > [Site Recovery 保存庫]。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
6. 按一下 [建立保存庫] 。

    ![新增保存庫](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

請檢查已成功建立 hello 保存庫的 hello 狀態列 tooconfirm。 hello 保存庫會列為**Active** hello 主要復原服務頁面上。

## <a name="step-2-generate-a-vault-registration-key"></a>步驟 2：產生保存庫註冊金鑰
Hello 保存庫中產生註冊金鑰。 您下載 hello Azure Site Recovery Provider，並將它安裝在 hello VMM 伺服器之後，您將使用此索引鍵 tooregister hello VMM 伺服器 hello 保存庫中。

1. 在 [hello**復原服務**頁面上，按一下 hello 保存庫 tooopen hello 快速入門] 頁面。 也可以使用 [hello] 圖示，隨時開啟快速入門。

    ![快速啟動圖示](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. 在 hello 下拉式清單中，選取 **在內部部署 VMM 站台與 Microsoft Azure 之間**。
3. 在 [準備 VMM 伺服器] 中，按一下 [產生註冊金鑰檔案]。 hello 金鑰檔案會自動產生並有效產生後 5 天。 如果您不從 hello VMM 伺服器存取 hello Azure 入口網站必須 toocopy toohello 中此檔案伺服器。

    ![註冊金鑰](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>步驟 3： 安裝 hello Azure Site Recovery Provider
1. 在**快速入門** > **準備 VMM 伺服器**，按一下 **下載 Microsoft Azure Site Recovery Provider 安裝於 VMM 伺服器上**tooobtain hellohello 提供者安裝檔案的最新版本。
2. 執行這個 hello 來源 VMM 伺服器上的檔案。

   > [!NOTE]
   > 如果 VMM 部署在叢集中，且您要安裝的 hello hello 提供者在第一次將它安裝在作用中的節點，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。 然後 hello 提供者上安裝 hello 其他節點。 請注意，如果您要升級提供者，您將需要 tooupgrade 所有節點上的，因為它們應該全部是的 hello 執行 hello 相同的提供者版本。
   >
   >
3. hello 安裝程式先決條件檢查，並要求權限 toostop hello VMM service toobegin Provider 安裝程式。 hello VMM 服務將會自動重新啟動安裝程式完成時。 如果您要安裝上 VMM 叢集，您應該會提示您 toostop hello 叢集角色。
4. 在 [Microsoft Update]  中，您可以選擇加入以取得更新。 這項設定將根據 tooyour Microsoft Update 原則會安裝已啟用的提供者更新。

    ![Microsoft Update](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. hello 的 hello 太設定提供者的安裝位置**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**。 按一下 [Install] 。

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. 在已安裝提供者的 hello 之後按**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. 在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。 按一下 [下一步] 。

    ![伺服器註冊](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. 在**網際網路連線**指定如何 hello hello VMM 上執行提供者伺服器連接 toohello 網際網路。 選取**利用現有的 proxy 設定連線**toouse hello 預設網際網路連線設定 hello 伺服器上設定。

    ![網際網路設定](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * 如果您想 toouse 自訂 proxy，您應該設定它，然後安裝 hello 提供者。 當您設定自訂 proxy 設定 toocheck hello proxy 連線將會執行測試。
   * 如果您使用自訂 proxy，或您的預設 proxy 需要驗證，您將需要 tooenter hello proxy 詳細資料，包括 hello proxy 位址和連接埠。
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
13. 按一下**下一步**toocomplete hello 程序。 註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 hello 伺服器顯示在 [hello **VMM 伺服器**] 索引標籤上 hello**伺服器**hello 保存庫中的頁面。

    ![最後一頁](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 hello 伺服器顯示在 hello **VMM 伺服器**索引標籤上 hello**伺服器**hello 保存庫中的頁面。

### <a name="command-line-installation"></a>命令列安裝
hello Azure Site Recovery 提供者也可以使用下列命令列的 hello 來安裝。 這個方法可以是使用的 tooinstall hello 的提供者的 Windows Server 2012 R2 的 Server Core 上。

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如：C:\ASR。
2. 停止 hello System Center Virtual Machine Manager 服務
3. 從提升權限的命令提示字元中，以擷取 hello 與這些命令的提供者安裝程式：

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. 安裝 hello 提供者，如下所示：

        C:\ASR> setupdr.exe /i
5. 註冊 hello 提供者，如下所示：

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

參數如下所示：

* **/ 認證**： 指定 hello 位置中的 hello 註冊金鑰檔所在的必要參數  
* **/Friendlyname** : hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要參數。
* **/ EncryptionEnabled** ： 如果您想 tooencryption 您在 Azure 虛擬機器 （在 rest 加密） 的選擇性參數 toospecify。 hello 檔案名稱必須包含**.pfx**延伸模組。
* **/proxyAddress** ： 指定 hello hello proxy 伺服器位址的選擇性參數。
* **/proxyport** ： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。
* **/proxyUsername** ： 指定 hello proxy 使用者名稱的選擇性參數。
* **/proxyPassword** ： 指定 hello proxy 密碼的選擇性參數。  

## <a name="step-4-create-an-azure-storage-account"></a>步驟 4：建立 Azure 儲存體帳戶
1. 如果您沒有 Azure 儲存體帳戶，按一下 **新增 Azure 儲存體帳戶**toocreate 帳戶。
2. 建立帳戶並啟用異地複寫。 它必須在 hello 與 hello Azure Site Recovery 服務相同的區域並與相關聯 hello 相同訂用帳戶。

    ![儲存體帳戶](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [移轉儲存體帳戶](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶，或跨訂用帳戶不支援用來部署站台復原的儲存體帳戶。
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>步驟 5： 安裝 Azure Recovery Services Agent hello
Hello VMM 雲端中每部 HYPER-V 主機伺服器上安裝 hello Azure 復原服務代理程式。

1. 按一下**快速入門** > **下載 Azure Site Recovery 服務代理程式並安裝於主機上的**tooobtain hello 最新版本的 hello 代理程式安裝檔案。

    ![Install Recovery Services Agent](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. 執行每個 HYPER-V 主機伺服器上的 hello 安裝檔案。
3. 在 hello**必要條件檢查**頁面上，按一下**下一步**。 將自動安裝任何缺少的必要元件。

    ![Prerequisites Recovery Services Agent](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. 在 hello**安裝設定**頁面上，指定您想 tooinstall hello 代理程式和備份中繼資料會安裝在其中選取 hello 快取位置。 然後按一下 [安裝] 。
5. 安裝完成，按一下後**關閉**toocomplete hello 精靈。

    ![註冊 MARS 代理程式](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>命令列安裝
您也可以使用此命令的 hello 命令列安裝 hello Microsoft Azure 復原服務代理程式：

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>步驟 6：設定雲端保護設定
註冊 hello VMM 伺服器之後，您可以設定雲端保護設定。 您已啟用 hello 選項**hello 保存庫同步處理雲端資料**當您安裝提供者 hello hello VMM 伺服器上的所有雲端就會出現在 hello<b>受保護項目</b>hello 保存庫中的索引標籤。

![發佈的雲端](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. 在 hello 快速入門 頁面上，按一下 **設定 VMM 雲端的保護**。
2. 在 hello**受保護項目**索引標籤上，按一下 [hello 雲端上您想 tooconfigure 並移 toohello**組態**] 索引標籤。
3. 在   select 。
4. 在**儲存體帳戶**選取 hello 複寫所使用的 Azure 儲存體帳戶。
5. 設定**加密已儲存的資料**太**關閉**。 此設定指定的資料應該在 hello 在內部部署站台與 Azure 之間的複寫期間加密。
6. 在**複製頻率**保留 hello 預設設定。 這個值指定應在來源與目標位置之間同步處理資料的頻率。
7. 在**保存復原點**，保留 hello 預設設定。 預設值是零，只 hello 最近復原點的主要虛擬機器儲存在複本主機伺服器上。
8. 在**應用程式一致快照的頻率**，保留 hello 預設設定。 這個值會指定頻率 toocreate 快照集。 快照集會使用磁碟區陰影複製服務 (VSS) tooensure 應用程式處於一致的狀態時 hello 快照。  如果您要設定值，請確定它是小於 hello 您設定其他復原點數目。
9. 在**複寫開始時間**，指定資料 tooAzure 的初始複寫應該開始的時間。 將使用 hello hello HYPER-V 主機伺服器上的時區。 我們建議您排程在離峰時間的 hello 初始複寫。

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

儲存 hello 設定之後作業將會建立，您可以在 hello 監視**作業** 索引標籤。Hello VMM 來源雲端中的所有 HYPER-V 主機伺服器將會都設定為複寫。

儲存之後，可以修改雲端設定上 hello**設定** 索引標籤 toomodify hello 目標位置或目標儲存體帳戶您將需要 tooremove hello 雲端組態，然後再重新設定 hello 雲端。 請注意，如果您變更 hello 儲存體帳戶 hello 變更僅會套用之虛擬機器的已啟用保護之後已修改 hello 儲存體帳戶。 現有的虛擬機器不會移轉 toohello 新儲存體帳戶。

## <a name="step-7-configure-network-mapping"></a>步驟 7：設定網路對應
開始之前請確認網路對應 hello 來源 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。 此外，請建立一或多個 Azure 虛擬網路。 請注意，多個 VM 網路可以是對應的 tooa 單一 Azure 網路。

1. 在 hello 快速入門 頁面上，按一下 **對應網路**。
2. 在 hello**網路**索引標籤的**來源位置**，選取 hello 來源 VMM 伺服器。 在 [目標位置]  中選取 [Azure]。
3. 在**來源**網路 hello VMM 伺服器相關聯的 VM 網路的清單會顯示。 在**目標**網路 hello Azure hello 訂用帳戶相關聯的網路會顯示。
4. 選取 hello 來源 VM 網路，然後按一下**對應**。
5. 在 hello**選取目標網路**頁面上，選取 hello 目標 Azure 網路，您想要 toouse。
6. 按一下 hello 核取記號 toocomplete hello 對應處理序。

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

儲存 hello 設定之後會啟動一個工作 tootrack hello 對應進度，它可以監視 hello 工作 索引標籤。對應 toohello 來源 VM 網路的任何現有複本虛擬機器將會連接的 toohello 目標 Azure 網路。 新的虛擬機器所連接的 toohello 來源 VM 網路在複寫之後會連接的 toohello 對應的 Azure 網路。 如果您修改現有的對應與新的網路，複本虛擬機器將使用 hello 新設定連接。

附註是否 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 是相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。

> [!NOTE]
> [移轉網路](../azure-resource-manager/resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間不支援的網路用來部署站台復原。
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>步驟 8：對虛擬機器啟用保護
伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。 請注意 hello 下列：

* 虛擬機器必須符合 [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
* tooenable 保護 hello 作業系統和作業系統磁碟屬性必須設定為 hello 虛擬機器。 當您在 VMM 使用虛擬機器範本中建立虛擬機器時，您可以設定 hello 屬性。 您也可以設定這些屬性的現有虛擬機器上 hello**一般**和**硬體組態**hello 虛擬機器內容 索引標籤。 如果您不需要在 VMM 中設定這些屬性，您將必須能夠 tooconfigure hello Azure Site Recovery 入口網站中。

    ![Create virtual machine](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modify virtual machine properties](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. tooenable 保護 hello**虛擬機器**索引標籤中的 hello 虛擬機器所在的 hello 雲端中，按一下**啟用保護** > **新增虛擬機器**.
2. 從 hello hello 雲端中虛擬機器清單，選取 hello 其中一個要 tooprotect。

    ![啟用虛擬機器保護](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    追蹤進度 hello**啟用保護**動作在 hello**作業**索引標籤上，包括 hello 初始複寫。 之後 hello**完成保護**作業執行 hello 虛擬機器是否已做好容錯移轉。 啟用保護，並複寫虛擬機器之後，您會無法 tooview 他們在 Azure 中。

    ![虛擬機器保護工作](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. 請確認 hello 虛擬機器內容，然後視需要進行修改。

    ![Verify virtual machines](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. 在 [hello**設定**可以修改下列網路內容的 hello 虛擬機器內容] 索引標籤。

* **Hello 目標虛擬機器上的網路介面卡數目**-hello 網路介面卡的數目取決於您指定 hello 目標虛擬機器的 hello 大小。 請檢查[虛擬機器大小規格](../virtual-machines/linux/sizes.md)hello hello 虛擬機器大小所支援的介面卡數目。 網路介面卡數目 hello 修改虛擬機器的 hello 大小儲存 hello 設定時，會變更 hello 下次開啟 hello**設定**頁面。 目標虛擬機器的網路介面卡的 hello 數目是 hello 來源虛擬機器和 hello 最大數目，如下所示選擇 hello 虛擬機器的 hello 大小所支援的網路介面卡上的網路介面卡數目下限：

  * 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
  * 如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
  * 例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。     
* **Hello 目標虛擬機器網路**-hello 網路 toowhich hello 虛擬機器所連接 toois 取決於來源虛擬機器的 hello 網路的網路對應。 如果 hello 來源虛擬機器有多個網路介面卡與來源網路的對應的 toodifferent 網路上的目標，則您必須 toochoose 其中一種 hello 目標網路。
* **每個網路介面卡的子網路**-針對每個網路介面卡，您可以選取 hello 子網路 toowhich hello 容錯移轉虛擬機器會連接到。
* **目標 IP 位址**-如果 hello 的來源虛擬機器的網路介面卡是設定的 toouse 的靜態 IP 位址，然後您可以提供 hello 目標虛擬機器中的 hello IP 位址。 使用這項功能在容錯移轉之後保留 hello 的來源虛擬機器的 IP 位址。 如果不提供的任何 IP 位址任何可用的 IP 位址會在容錯移轉的 hello 階段賦予 toohello 網路介面卡。 如果已指定 hello 目標 IP 位址，但已由另一個在 Azure 中執行的虛擬機器容錯移轉將會失敗。  

    ![修改網路屬性](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> 不支援具有靜態 IP 位址的 Linux 虛擬機器。
>
>

## <a name="test-hello-deployment"></a>測試 hello 部署
tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器，並執行測試容錯移轉的 hello。  

測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。 請注意：

* 如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。
* 容錯移轉之後，您可以使用公用 IP 位址 tooconnect toohello 使用遠端桌面的 Azure VM。 如果您希望 toodo 如此，請確定您沒有任何網域原則，讓您無法使用的公用位址的連接 tooa 虛擬機器。

> [!NOTE]
> tooget hello 達到最佳效能時，您容錯移轉 tooAzure，請確定您已安裝 hello Azure hello VM 上的代理程式。 這會提供更快速的開機，並協助進行疑難排解。 下載 hello [Linux 代理程式](https://github.com/Azure/WALinuxAgent)，或使用 hello [Windows 代理程式](http://go.microsoft.com/fwlink/?LinkID=394789)。
>
>

### <a name="create-a-recovery-plan"></a>建立復原計畫
1. 在 hello**復原計劃**索引標籤上，加入新的計畫。 指定的名稱， **VMM**中**來源類型**，與 hello 來源 VMM 伺服器中的**來源**。 hello 目標為 Azure。

    ![建立復原計畫](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. 在 hello**選取虛擬機器**頁面上，選取虛擬機器 tooadd toohello 復原計劃。 這些虛擬機器會新增 toohello 復原計劃預設群組-群組 1。 最多 100 部虛擬機器已在單一復原計畫中經過測試。

* 如果您想 tooverify hello 虛擬機器內容新增 toohello 計劃之前，請按一下 hello hello hello 雲端屬性頁面上的虛擬機器所在。 您也可以設定 hello VMM 主控台中的 hello 虛擬機器內容。
* 所有顯示的 hello 虛擬機器啟用保護。 hello 清單包含兩個虛擬機器啟用保護與初始複寫完成，而且那些啟用保護而且初始複寫擱置中。 只有已完成初始複寫的虛擬機器可做為復原計畫的一部分進行容錯移轉。

    ![建立復原計畫](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

復原計劃建立它之後會出現在 hello**復原計劃** 索引標籤。您也可以加入[Azure 自動化 runbook](site-recovery-runbook-automation.md) toohello 復原計劃在容錯移轉期間的 tooautomate 動作。

### <a name="run-a-test-failover"></a>執行測試容錯移轉
有兩種方式 toorun 測試容錯移轉 tooAzure。

* **測試容錯移轉，不使用 Azure 網路**— 這種類型的測試容錯移轉會檢查該 hello 虛擬機器確實啟動 Azure 中。 hello 虛擬機器無法容錯移轉之後連接的 tooany Azure 網路。
* **測試容錯移轉與 Azure 網路**— 這種類型的容錯移轉檢查整體複寫環境的 hello 會如預期啟動移，而容錯移轉 hello 虛擬機器將會連接的 toohello 指定的目標 Azure 網路。 子網路處理的測試容錯移轉 hello hello 測試虛擬機器的子網路將會知道 hello 複本虛擬機器的 hello 子網路為基礎。 Hello 子網路，複本虛擬機器的基礎 hello hello 來源虛擬機器的子網路時，這是不同 tooregular 複寫。

如果您想要虛擬機器，而不指定 Azure 目標網路啟用保護 tooAzure toorun 測試容錯移轉，您無須 tooprepare 任何項目。 toorun 目標 Azure 網路，您必須從您的 Azure 生產網路 （預設行為時在 Azure 中建立新的網路） toocreate 新的 Azure 網路有隔離的測試容錯移轉。 看看過[執行測試容錯移轉](site-recovery-failover.md)如需詳細資訊。

您也需要 tooset hello 基礎結構的 hello 複寫虛擬機器 toowork 如預期般。 例如，與網域控制站和 DNS 虛擬機器可以使用 Azure Site Recovery 的複寫的 tooAzure，可以建立在 hello 測試網路中使用測試容錯移轉。 如需詳細資訊，請參閱 [Active Directory 測試容錯移轉考量](site-recovery-active-directory.md#test-failover-considerations) 一節。

toorun 測試容錯移轉，請勿 hello 遵循：

1. 在 hello**復原計劃**索引標籤上，選取 hello 計劃，並按一下**測試容錯移轉**。
2. 在 hello**確認測試容錯移轉**頁面上，選取**無**或特定的 Azure 網路。  請注意，是否您選取 無 hello 測試容錯移轉將 hello 虛擬機器的核取 tooAzure 正確地複寫，但並不會檢查您的複寫網路組態。

    ![沒有網路](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. 如果已啟用資料加密 hello 雲端中**加密金鑰**選取 hello 已發行憑證，hello 提供者在 hello VMM 伺服器上，安裝期間開啟 hello 選項 tooenable 雲端的資料加密.
4. 在 [hello**作業**] 索引標籤，您可以追蹤容錯移轉的進度。 您也應該要能夠 toosee hello 虛擬機器測試複本 hello Azure 入口網站中。 如果您設定好 tooaccess 虛擬機器從內部部署網路，您可以起始遠端桌面連線 toohello 虛擬機器。
5. 當 hello 容錯移轉到達 hello**完成測試**階段時，按一下 **完成測試**toofinish 它。 您可以切入 toohello**作業**索引標籤上 tootrack 容錯移轉的進度和狀態，以及 tooperform 所需的任何動作。
6. 容錯移轉之後，您可以看到 hello Azure 入口網站中的 hello 虛擬機器測試複本。 如果您設定好 tooaccess 虛擬機器從內部部署網路，您可以起始遠端桌面連線 toohello 虛擬機器。 請勿 hello 遵循：

   1. 請確認 hello 虛擬機器成功啟動。
   2. 如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。 您也需要 tooadd hello 虛擬機器上的 RDP 端點。 您可以利用[Azure 自動化 Runbook](site-recovery-runbook-automation.md) toodo 的。
   3. 容錯移轉之後，如果您使用遠端桌面在 Azure 中使用公用 IP 位址 tooconnect toohello 虛擬機器，請確定您沒有任何網域原則，防止您連接 tooa 虛擬機器使用的公用位址。
7. Hello 測試完成之後執行 hello 下列動作：

   * 按一下**hello 測試容錯移轉已完成**。 Hello 清理測試環境 tooautomatically 電源關閉和刪除 hello 測試虛擬機器。
   * 按一下**備忘稿**toorecord 及儲存與 hello 測試容錯移轉相關聯的任何觀察。


## <a name="next-steps"></a>後續步驟
深入了解[設定復原方案](site-recovery-create-recovery-plans.md)和[容錯移轉](site-recovery-failover.md)。
