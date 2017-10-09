---
title: "使用 Azure Site Recovery 的 VMM 與 SAN 中的 HYPER-V Vm aaaReplicate |Microsoft 文件"
description: "本文說明如何與使用 SAN 複寫的 Azure Site Recovery 的兩個網站間的 tooreplicate HYPER-V 虛擬機器。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>使用 SAN 來複寫 VMM 雲端 tooa 次要站台與 Azure Site Recovery 中的 HYPER-V Vm


使用這份文件，如果您想 toodeploy [Azure Site Recovery](site-recovery-overview.md) toomanage 複寫 （在 System Center Virtual Machine Manager 雲端中管理） 的 HYPER-V Vm tooa 次要 VMM 站台，使用 Azure Site Recovery hello 傳統入口網站中。 此案例中不提供 hello 新版 Azure 入口網站。



張貼在 hello 本文結尾的任何註解。 取得解答 tootechnical 問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="why-replicate-with-san-and-site-recovery"></a>為什麼使用 SAN 搭配 Site Recovery 進行複寫？

* SAN 提供企業層級、 可擴充的複寫解決方案，讓主要站台包含 HYPER-V 與 SAN 可以複寫的 Lun tooa 次要站台與 SAN。 儲存體由 VMM 管理，複寫及容錯移轉使用 Site Recovery 進行協調。
* 站台復原，曾有數個[SAN 儲存體夥伴](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx)tooprovide 複寫透過光纖通道及 iSCSI 存放裝置。  
* 使用現有 SAN 基礎結構 tooprotect 關鍵任務應用程式部署在 HYPER-V 叢集。 VM 可以整組複寫，使多層式架構應用程式可以一致地容錯移轉。
* SAN 複寫藉由低 RTO 與 RPO 的同步複寫，以及高彈性的非同步複寫 (視存放裝置陣列功能而定) 確保不同層應用程式的複寫一致性。  
* 您可以管理在 hello VMM 網狀架構中的 SAN 存放裝置，並使用 SMI-S VMM toodiscover 現有儲存體中。  

請注意：
- 使用 SAN 的站台對站台複寫無法使用 hello Azure 入口網站。 您僅供以 hello 傳統入口網站。 無法建立新的保存庫 hello 傳統入口網站中。 可以保留現有的保存庫。
- 不支援從 SAN tooAzure 複寫。
- 您無法將共用的 Vhdx，複寫或邏輯單元 (Lun) 直接連接 tooVMs 透過 iSCSI 或光纖通道。 可以複寫客體叢集。


## <a name="architecture"></a>架構

![SAN 架構](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: hello Azure 入口網站中的站台復原保存庫所設定。
- **SAN 存放裝置**: hello VMM 網狀架構管理的 SAN 存放裝置。 您新增 hello 存放裝置提供者、 建立儲存體分類及設定儲存集區。
- **VMM 與 Hyper-V**：我們建議一個網站一部 VMM 伺服器。 設定 VMM 私人雲端，並將 Hyper-V 叢集放在這些雲端中。 在部署期間，hello Azure Site Recovery Provider 安裝每個 VMM 伺服器上，而 hello 伺服器會註冊在 hello 保存庫中。 hello 提供者會與 hello Site Recovery 服務 toomanage 複寫、 容錯移轉和容錯回復通訊。
- **複寫**: hello 主要和次要 SAN 儲存體之間設定 VMM 中的儲存體後，當您在站台復原中設定複寫時，會發生複寫。 任何複寫資料會不傳送 tooSite 復原。
- **容錯移轉**： 啟用 hello Site Recovery 入口網站中的容錯移轉。 由於複寫是同步作業，容錯移轉期間不會遺失任何資料。
- **容錯回復**: toofail 後，啟用從 hello 次要站台 toohello 主要站台的反轉複寫方向 tootransfer 差異變更。 反轉複寫完成之後，您會從次要 tooprimary 執行規劃的容錯移轉。 此計劃的容錯移轉 hello 次要站台上停止 hello 複本 Vm，並啟動 hello 主要站台上。


## <a name="before-you-start"></a>開始之前


**必要條件** | **詳細資料**
--- | ---
**Azure** |您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。 建立 Azure Site Recovery 保存庫 tooconfigure 和管理複寫和容錯移轉。
**VMM** | 您可以使用單一 VMM 伺服器，以及不同的雲端之間進行複寫，但我們建議在 hello 主要站台的一個 VMM 與 hello 次要站台中的其中一個。 VMM 可部署為實體或虛擬獨立伺服器，或是一個叢集。 <br/><br/>hello VMM 伺服器應執行 System Center 2012 R2 或更新版本以及 hello 最新累計更新。<br/><br/> 您必須設定至少一個雲端 hello 想 tooprotect 的 hello 次要 VMM 伺服器上設定一個雲端，而且主要 VMM 伺服器上要 toouse 容錯移轉。<br/><br/> hello 來源雲端必須包含一個或多個 VMM 主機群組。<br/><br/> 所有 VMM 雲端都必須 hello HYPER-V 容量設定檔集合。<br/><br/> 如需設定 VMM 雲端的相關資訊，請參閱[部署私人 VM 雲端](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview)。
**Hyper-V** | 在主要和次要 VMM 雲端中，您需要一或多個 Hyper-V 叢集。<br/><br/> hello 來源 HYPER-V 叢集必須包含一個或多個 Vm。<br/><br/> hello 主要和次要網站中的 hello VMM 主機群組必須包含至少其中一個 hello HYPER-V 叢集。<br/><br/>hello 主機與目標 HYPER-V 伺服器必須執行 Windows Server 2012 或更新版本以及 hello HYPER-V 角色和 hello 最新的更新安裝。<br/><br/> 如果您在叢集中執行 Hyper-V，且您具有靜態 IP 位址叢集，則不會自動建立叢集訊息代理程式。 您必須手動進行設定。 如需詳細資訊，請參閱[準備 Hyper-V 複本的主機叢集](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters)。
**SAN 儲存體** | 您可以藉由 iSCSI 或光纖通道存放裝置，或藉由使用共用虛擬硬碟 (vhdx)，複寫客體叢集化虛擬機器。<br/><br/> 您需要兩個 SAN 陣列： 一個在 hello 主要站台，一個在 hello 次要站台。<br/><br/> Hello 陣列之間應該被設定網路基礎結構。 應該設定對等互連和複寫。 複寫授權應該根據 hello 存放裝置陣列需求設定。<br/><br/>設定網路 hello HYPER-V 主機伺服器與 hello 存放裝置陣列之間，讓主機可以使用存放裝置 Lun 來使用 iSCSI 或光纖通道通訊。<br/><br/> 請參閱[支援的儲存體陣列](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx)。<br/><br/> 應該安裝 SMI-S 提供者的存放裝置陣列製造商，並 hello SAN 陣列應該受 hello 提供者。 設定 hello 提供者相應 toomanufacturer 指示。<br/><br/>請確定該 hello 陣列的 SMI-S 提供者是在伺服器上該 hello VMM 伺服器可以存取透過 hello 網路和 IP 位址或 FQDN。<br/><br/> 每個 SAN 陣列都應該要有一或多個可用的存放集區。<br/><br/> hello 主要 VMM 伺服器管理主要陣列 hello，和 hello 次要 VMM 伺服器管理 hello 次要陣列。
**網路對應** | 設定網路對應，以便複寫的虛擬機器以最佳方式次要 HYPER-V 主機伺服器上放置容錯移轉之後，並使它們更連接的 tooappropriate VM 網路。 如果您未設定網路對應，複本 Vm 將容錯移轉之後無法連接的 tooany 網路。<br/><br/> 請確定 VMM 網路設定正確，才能在 Site Recovery 部署期間設定網路對應。 在 VMM 中，hello Vm hello 來源 HYPER-V 主機上的應該連接的 tooa VMM VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。<br/><br/> hello 目標雲端應該有對應的 VM 網路，並接著應該連結的 tooa 對應的邏輯網路與 hello 目標雲端相關聯。<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>步驟 1： 準備 hello VMM 基礎結構
tooprepare VMM 基礎結構，您需要：

1. 確認 VMM 雲端。
2. 將 VMM 中的 SAN 存放裝置整合並分類。
3. 建立 LUN 並配置存放裝置。
4. 建立複寫群組。
5. 設定 VM 網路。

### <a name="verify-vmm-clouds"></a>確認 VMM 雲端

開始 Site Recovery 部署之前，請確定您的 VMM 雲端已妥善設定。

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>整合及分類 SAN 存放裝置中 hello VMM 網狀架構

1. 在 hello VMM 主控台中，移過**網狀架構** > **儲存體** > **新增資源** > **的存放裝置**.
2. 在 hello**新增存放裝置**精靈中，選取**選取儲存體提供者類型**並選取**SAN 和 NAS 裝置探索到及管理由 SMI-S 提供者**。

    ![提供者類型](./media/site-recovery-vmm-san/provider-type.png)

3. 在 hello**指定的通訊協定與位址的 hello 儲存體 SMI-S 提供者**頁面上，選取**SMI-S CIMXML**並指定連接 toohello 提供者的 hello 設定。
4. 在**提供者 IP 位址或 FQDN**和**TCP/IP 通訊埠**，指定連接 toohello 提供者的 hello 設定。 您只能針對 SMI-S CIMXML 使用 SSL 連線。

    ![提供者連接](./media/site-recovery-vmm-san/connect-settings.png)
5. 在**執行身分帳戶**，指定 VMM 執行身分帳戶可以存取 hello 提供者，或建立帳戶。
6. 在 hello**收集資訊**頁面上，VMM 會自動嘗試 toodiscover 和匯入 hello 存放裝置資訊。 tooretry 探索按一下**掃描提供者**。 如果 hello 探索程序成功，hello 探索存放裝置陣列、 存放集區、 製造商、 型號及容量會列在 [hello] 頁面。

    ![探索儲存體](./media/site-recovery-vmm-san/discover.png)
7. 在**選取受管理的存放集區 tooplace 並指派分類**，選取 hello 存放集區會管理 VMM，並將其指派的分類。 從 hello 存放集區匯入 LUN 資訊。 建立 Lun 基礎 hello 應用程式所需 tooprotect、 其容量需求，以及您的需求必須的項目 tooreplicate 在一起。

    ![分類儲存體](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>建立 LUN 並配置存放裝置

建立 Lun 基礎 hello 應用程式所需 tooprotect、 容量需求，以及您的需求必須的項目 tooreplicate 在一起。

1. Hello 存放裝置會出現在 hello VMM 網狀架構之後，您可以[佈建的 Lun](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm)。

     > [!NOTE]
     > 不要將 Vhd 新增 hello 可供複寫 tooLUNs 的 VM。 如果這些 LUN 不在 Site Recovery 複寫群組中，Site Recovery 不會偵測到它們。
     >

2. 配置儲存體容量 toohello HYPER-V 主機叢集，讓 VMM 可以部署虛擬機器資料 toohello 佈建存放裝置：

   * 然後再配置儲存體 toohello 叢集，您需要 tooallocate 它 toohello 哪些 hello 叢集所在的 VMM 主機群組。 如需詳細資訊，請參閱[tooallocate 存放裝置邏輯單元 tooa 如何主機在 VMM 中的群組](https://technet.microsoft.com/library/gg610686.aspx)和[如何 tooallocate 存放集區 tooa 在 VMM 中的主機群組](https://technet.microsoft.com/library/gg610635.aspx)。
   * 中所述，配置儲存體容量 toohello 叢集[tooconfigure 存放裝置上的 HYPER-V 主機在 VMM 中的叢集化](https://technet.microsoft.com/library/gg610692.aspx)。

    ![提供者類型](./media/site-recovery-vmm-san/provider-type.png)
3. 在**指定的通訊協定與位址的儲存體 SMI-S 提供者 hello**，選取**SMI-S CIMXML**。 指定 hello 設定用來連接 toohello 提供者。 您只能針對 SMI-S CIMXML 使用 SSL 連線。

    ![提供者連接](./media/site-recovery-vmm-san/connect-settings.png)
4. 在**執行身分帳戶**，指定 VMM 執行身分帳戶可以存取 hello 提供者，或建立帳戶。
5. 在**收集資訊**，VMM 會自動嘗試 toodiscover 和匯入 hello 存放裝置資訊。 如果您需要 tooretry，按一下**掃描提供者**。 Hello 探索程序成功時，hello 存放裝置陣列、 存放集區、 製造商、 型號及容量會列在 [hello] 頁面中。

    ![探索儲存體](./media/site-recovery-vmm-san/discover.png)
7. 在**選取受管理的存放集區 tooplace 並指派分類**，選取 hello 存放集區，VMM 會管理，並將它們指派分類。 從 hello 存放集區匯入 LUN 資訊。

    ![分類儲存體](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>建立複寫群組

建立複寫群組包含所有需要 tooreplicate 在一起的 hello Lun。

1. 在 hello VMM 主控台中，開啟 hello**複寫群組**hello 存放裝置陣列屬性，然後再按一下索引標籤**新增**。
2. 建立 hello 複寫群組。

    ![SAN 複寫群組](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>設定網路

如果您想 tooconfigure 網路對應時，請勿 hello 遵循：

1. 請參閱 Site Recovery 網路對應。
2. 在 VMM 中準備 VM 網路：

   * [設定邏輯網路](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks)。
   * [設定 VM 網路](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks)。


## <a name="step-2-create-a-vault"></a>步驟 2：建立保存庫

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello VMM 伺服器從您想 tooregister hello 保存庫中的。
2. 展開 資料服務 > 復原服務，然後按一下Site Recovery 保存庫。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
6. 按一下 [建立保存庫] 。

    ![新增保存庫](./media/site-recovery-vmm-san/create-vault.png)

請檢查已成功建立 hello 保存庫的 hello 狀態列 tooconfirm。 hello 保存庫會列為**Active**上主要的 hello**復原服務**頁面。

### <a name="register-hello-vmm-servers"></a>註冊 hello VMM 伺服器

1. 開啟 hello**快速入門**頁面從 hello**復原服務**頁面。 快速入門也可以隨時選擇 hello 圖示開啟。

    ![快速啟動圖示](./media/site-recovery-vmm-san/quick-start-icon.png)
2. 在 hello 下拉式清單方塊中，選取 **之間 HYPER-V 內部部署站台使用陣列複寫**。

    ![註冊金鑰](./media/site-recovery-vmm-san/select-san.png)
3. 在**準備 VMM 伺服器**，下載 hello hello Azure Site Recovery Provider 安裝檔案的最新版本。
4. 執行這個 hello 來源 VMM 伺服器上的檔案。 如果 VMM 部署在叢集中，您要安裝的 hello hello 提供者在第一次的作用中節點上安裝 hello 提供者，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。 然後 hello 提供者上安裝 hello 其他節點。 如果您要升級 hello 提供者，您會需要 tooupgrade 所有節點上的，讓它們擁有 hello 相同的提供者版本。
5. hello 安裝會檢查需求和要求權限 toostop hello VMM service toobegin Provider 安裝程式。 hello 服務將會自動重新啟動安裝程式完成時。 在 VMM 叢集上，您將會提示的 toostop hello 叢集角色。
6. 在**Microsoft Update**，您可以選擇進行更新，並將根據 tooyour Microsoft Update 原則安裝 Provider 更新。

    ![Microsoft Update](./media/site-recovery-vmm-san/ms-update.png)

7. 根據預設，hello hello 提供者的安裝位置是<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin。 按一下**安裝**toobegin。

    ![安裝位置](./media/site-recovery-vmm-san/install-location.png)

8. Hello 提供者安裝之後，按一下**註冊**tooregister hello VMM 伺服器 hello 保存庫中的。

    ![安裝完成](./media/site-recovery-vmm-san/install-complete.png)

9. 在**網際網路連線**，指定 hello 提供者如何連接 toohello 網際網路。 選取**使用預設系統 proxy 設定**如果您想 toouse hello 預設網際網路連線設定 hello 伺服器上的。

    ![網際網路設定](./media/site-recovery-vmm-san/proxy-details.png)

   * 如果您想 toouse 自訂 proxy，設定它，然後安裝 hello 提供者。 當您設定自訂 proxy 設定時，測試就會執行 toocheck hello proxy 連線。
   * 如果您使用自訂 proxy，或您的預設 proxy 需要驗證，您應該輸入 hello proxy 詳細資料，包括 hello 位址和連接埠。
   * hello 所需的 Url 必須能夠存取 hello VMM 伺服器。
   * 如果您使用自訂 proxy，使用指定的 hello 自動建立 VMM 執行身分帳戶 (DRAProxyAccount) proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可驗證。 您可以修改帳戶設定執行身分 hello hello VMM 主控台中的 (**設定** > **安全性** > **執行身分帳戶** > **DRAProxyAccount**)。 您必須重新啟動 hello 變更 tootake 效果的 hello VMM 服務。
10. 在**登錄機碼**，選取您下載自 hello 入口網站與複製 toohello VMM 伺服器的 hello 索引鍵。
11. 在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。

    ![伺服器註冊](./media/site-recovery-vmm-san/vault-creds.png)
12. hello 加密設定僅用於 VMM tooAzure 複寫。 您可以忽略它。

    ![伺服器註冊](./media/site-recovery-vmm-san/encrypt.png)
13. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中，指定 hello VMM 叢集角色名稱。
14. 在**初始雲端中繼資料同步**，選取是否要 hello VMM 伺服器上的所有雲端 toosynchronize 中繼資料。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。

    ![伺服器註冊](./media/site-recovery-vmm-san/friendly-name.png)

15. 按一下**下一步**toocomplete hello 程序。 註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 在中，會顯示 hello 伺服器**伺服器** > **VMM 伺服器**hello 保存庫中。

### <a name="command-line-installation"></a>命令列安裝

也可以使用下列命令列的 hello 安裝 hello Azure Site Recovery Provider。 這個方法可以是使用的 tooinstall hello 的提供者的 Windows Server 2012 R2 的 Server Core 上。

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如，C:\ASR。
2. 停止 hello VMM 服務。
3. 擷取 hello 提供者安裝程式。 以系統管理員身分執行這些命令︰

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. 安裝提供者 hello:

        C:\ASR> setupdr.exe /i
5. 登錄提供者 hello:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

參數：

* **/ 認證**: hello 位置中的 hello 註冊金鑰檔所在的必要的參數。  
* **/Friendlyname**: hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要的參數。
* **/ EncryptionEnabled**： 從 VMM tooAzure 複寫時，才使用的選擇性參數。
* **/proxyAddress**： 指定 hello hello proxy 伺服器位址的選擇性參數。
* **/proxyport**： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。
* **/proxyUsername**： 指定 hello proxy 使用者名稱 （如果 hello proxy 需要驗證） 的選擇性參數。
* **/proxyPassword**： 指定 hello 密碼進行驗證的 hello proxy 伺服器 （hello proxy 需要驗證） 的選擇性參數。

## <a name="step-3-map-storage-arrays-and-pools"></a>步驟 3：對應存放裝置陣列和集區

對應主要和次要陣列 toospecify 哪一個次要儲存體集區接收複寫資料從 hello 主要集區。 對應儲存體之前設定複寫，因為當您啟用複寫群組的保護時，會使用 hello 對應資訊。

開始之前，請檢查 VMM 雲端會出現在 hello 保存庫中。 當您同步處理所有雲端提供者安裝期間或 hello VMM 主控台中的特定雲端同步都處理時，會偵測到雲端。

1. 按一下 [資源]  >  [伺服器存放裝置]  >  [對應來源和目標陣列]。
    ![伺服器註冊](./media/site-recovery-vmm-san/storage-map.png)

2. 選取 hello hello 主要站台上的存放裝置陣列，並將它們對應 toostorage hello 次要站台上的陣列。 在**存放集區**、 選取來源和目標存放集區 toomap。

    ![伺服器註冊](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>步驟 4︰設定複寫設定

註冊 VMM 伺服器之後，設定雲端保護設定。

1. 在 hello**快速入門**頁面上，按一下**設定 VMM 雲端的保護**。
2. 在 hello**受保護項目**索引標籤上，選取 hello 雲端**組態**。
3. 在 [目標] 中，選取 [VMM]。
4. 在**目標位置**，請選取管理您想要復原 toouse hello 雲端的 hello VMM 伺服器。
5. 在**目標雲端**，選取您想 toouse VM 才能容錯移轉的 hello 目標雲端。
   * 我們建議您選取符合復原需求，針對您所保護的 hello 虛擬機器的目標雲端。
   * 雲端可以只隸屬 tooa 單一雲端組--做為主要或目標雲端。
6. Site Recovery 會驗證雲端可存取 tooSAN 存放裝置，以及該 hello 儲存體陣列對應。
7. 如果驗證成功，請在 [複寫類型] 中，選取 [SAN]。

儲存 hello 設定之後，會建立一個作業，可監視上 hello**作業** 索引標籤。設定可以修改在 hello**設定** 索引標籤。如果您想 toomodify hello 目標位置或目標雲端，您必須移除 hello 雲端組態，然後再重新 hello 雲端。

## <a name="step-5-enable-network-mapping"></a>步驟 5：啟用網路對應

1. 在 hello**快速入門**頁面上，按一下**對應網路**。
2. 選取 hello 來源 VMM 伺服器，然後選取 hello 目標 VMM 伺服器 toowhich hello 要對應網路。 會顯示來源網路及其相關聯的目標網路的 hello 清單。 對於未對應的網路，將顯示空白值。 按一下 hello 資訊圖示下一步 toohello 來源和目標網路名稱 tooview hello 子網路的每個網路。
3. 在 來源上的網路 中選取網路，然後按一下對應。 hello 服務會偵測 hello hello 目標伺服器上的 VM 網路，並加以顯示。

    ![SAN 架構](./media/site-recovery-vmm-san/network-map1.png)
4. 您可以選取其中一個 hello VM 網路從 hello 目標 VMM 伺服器。

    ![SAN 架構](./media/site-recovery-vmm-san/network-map2.png)

5. 當您選取的目標網路時，hello 使用 hello 來源網路的受保護的雲端會顯示。 也會顯示可用的目標網路。 我們建議您選取的目標網路，您所使用的複寫提供 tooall hello 雲端。
6. 按一下 hello 核取記號 toocomplete hello 對應處理序。 此時會啟動一個作業來追蹤進度。 您可以檢視其 hello**作業** 索引標籤。

## <a name="step-6-enable-replication-for-replication-groups"></a>步驟 6：為複寫群組啟用複寫

您可以啟用虛擬機器的保護之前，您需要 tooenable 複寫儲存體複寫群組。

1. 在 hello**屬性**hello 主要雲端 hello Site Recovery 入口網站，開啟 hello 頁面**虛擬機器**索引標籤上，按一下 **加入複寫群組**。
2. 選取一或多個 VMM 複寫群組與 hello 雲端相關聯的確認 hello 來源和目標陣列，並指定 hello 複寫頻率。

站台復原、 VMM 和 hello SMI-S 提供者佈建 hello 目標網站存放裝置 Lun，並啟用儲存體複寫。 如果已複寫 hello 複寫群組，Site Recovery 會重複使用 hello 現有複寫關聯性，並更新 hello 資訊。

## <a name="step-7-enable-protection-for-virtual-machines"></a>步驟 7：對虛擬機器啟用保護


儲存群組複寫時，啟用 hello VMM 主控台中之 Vm 的保護 hello 下列方法之一：

* **新的虛擬機器**： 當您建立 VM 時，您已啟用複寫，並將 hello VM 與 hello 複寫群組建立關聯。
  使用此選項時，VMM 會使用智慧型放置 toooptimally 位置 hello VM 存放裝置 hello hello 複寫群組的 Lun 上。 Site Recovery 會協調 hello 建立陰影 hello 次要站台上的 VM，配置容量，以便可以在容錯移轉之後啟動複本 Vm。
* **現有的虛擬機器**： 如果已在 VMM 中部署虛擬機器，則您可以啟用複寫，以及執行存放裝置移轉 tooa 複寫群組。 完成時，VMM 及 Site Recovery 偵測之後 hello 新的 VM，並開始管理 Site Recovery 中。 陰影 hello 次要站台上建立 VM，以便在容錯移轉之後啟動該 hello 複本 VM 配置容量。

![啟用保護。](./media/site-recovery-vmm-san/enable-protect.png)

Vm 已啟用複寫之後，它們會出現在 hello Site Recovery 主控台中。 您可以檢視 VM 內容、追蹤狀態，以及追蹤包含多個 VM 的容錯移轉複寫群組。 在 SAN 複寫中，與複寫群組關聯的所有 VM 必須都一起進行容錯移轉。 這是因為容錯移轉，就會發生 hello 儲存層第一次。 它是重要 toogroup 複寫正確分組，並將相關聯的 Vm 放在一起。

> [!NOTE]
> 啟用適用於 VM 複寫之後，不將其 Vhd tooLUNs，除非它們位於站台復原的複寫群組。 Site Recovery 只能偵測位於 Site Recovery 複寫群組中的 VHD。
>
>

您可以追蹤進度，包括 hello 初始複寫，請在 hello**作業** 索引標籤。Hello 完成保護作業執行後，hello 虛擬機器已做好容錯移轉。

![虛擬機器保護工作](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>步驟 8： 測試 hello 部署

測試您的部署 toomake 確定 Vm 的容錯移轉如預期般。 toodo 這個建立復原計劃及執行測試容錯移轉。

1. 在 hello**復原計劃**索引標籤上，按一下 **建立復原計劃**。
2. 指定的名稱對於 hello 復原計劃，並選取來源和目標 VMM 伺服器。 hello 來源伺服器必須具有啟用容錯移轉和復原的 Vm。 選取**SAN** tooview 僅雲端設定 SAN 複寫。

    ![建立復原計畫](./media/site-recovery-vmm-san/r-plan.png)

3. 在 [選取虛擬機器] 中，選取複寫群組。 Hello 群組相關聯的所有 Vm 會都加入 toohello 復原計劃。 這些 Vm 會加入 toohello 復原計劃預設群組 (群組 1)。 您可以視需要新增更多群組。 複寫之後，Vm 根據 hello 復原計畫群組 toohello 順序編號。

    ![選取虛擬機器](./media/site-recovery-vmm-san/r-plan-vm.png)
4. 建立 hello 復原方案之後，它會出現在 hello 清單上 hello**復原計劃**] 索引標籤。選取 hello 方案，然後選擇 [**測試容錯移轉**。
5. 在 hello**確認測試容錯移轉**頁面上，選取**無**。 啟用此選項，hello 容錯移轉複本 Vm，將無法連接的 tooany 網路。 這會測試該 hello 如預期般，Vm 容錯移轉，但是它不會測試 hello 網路環境。 如需其他網路功能選項的相關資訊，請參閱 [Site Recovery 容錯移轉](site-recovery-failover.md)。

    ![選取測試網路](./media/site-recovery-vmm-san/test-fail1.png)

6. hello 相同裝載為 hello 的 hello 複本存在 VM 的主機上建立 hello 測試 VM。 它不會加入 toohello 雲端中的 hello 複本 VM 所在。
2. 複寫之後，hello 複本 VM 將會有不同的 IP 位址，比 hello 主要虛擬機器。 如果您是從 DHCP 發出位址，則會自動更新位址。 如果您不使用 DHCP，而且您想 hello 相同位址，您需要 toorun 幾個指令碼。
3. 執行這個指令碼 tooretrieve hello IP 位址：

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. 執行這個範例指令碼 tooupdate DNS。 指定您所擷取的 hello IP 位址。

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>後續步驟

您已如預期般執行測試容錯移轉 toocheck 正在您的環境之後，請參閱[Site Recovery 的容錯移轉](site-recovery-failover.md)toolearn 有關不同類型的容錯移轉。
