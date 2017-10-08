---
title: "在 VMM 中的 HYPER-V Vm aaaReplicate 雲端 tooAzure |Microsoft 文件"
description: "協調複寫、 容錯移轉和復原的 System Center VMM 雲端 tooAzure 中受管理的 HYPER-V Vm"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>複寫 HYPER-V 虛擬機器在 VMM 雲端 tooAzure hello Azure 入口網站中使用站台復原中
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-azure.md)
> * [Azure 傳統型](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell 傳統](site-recovery-deploy-with-powershell.md)


本文說明如何 tooreplicate 內部部署 HYPER-V 虛擬機器管理 System Center VMM 雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

如果您想 toomigrate 機器 tooAzure （不含錯誤後回復），進一步了解[本文](site-recovery-migrate-to-azure.md)。


## <a name="deployment-steps"></a>部署步驟

請依照下列 hello 文章 toocomplete 部署步驟執行：


1. [進一步了解](site-recovery-components.md)有關此部署的 hello 架構。 此外，[深入了解](site-recovery-hyper-v-azure-architecture.md) Site Recovery 中 Hyper-V 複寫的運作方式。
2. 確認必要條件和限制。
3. 設定 Azure 網路和儲存體帳戶。
4. 準備 hello 在內部部署 VMM 伺服器和 HYPER-V 主機。
5. 建立復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。
6. 指定來源設定。 Hello 保存庫中註冊 hello VMM 伺服器。 安裝 Azure Site Recovery Provider hello hello VMM 伺服器安裝 hello Microsoft 復原服務代理程式上 HYPER-V 主機。
7. 設定目標和複寫設定。
8. 啟用複寫 hello Vm。
9. 執行測試容錯移轉 toomake 確定一切如預期般運作。



## <a name="prerequisites"></a>必要條件


**支援需求** | **詳細資料**
--- | ---
**Azure** | 了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。
**內部部署伺服器** | [進一步了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure)需 hello 在內部部署 VMM 伺服器和 HYPER-V 主機。
**內部部署 Hyper-V VM** | 您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
**Azure URL** | hello VMM 伺服器需要存取 toothese Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。<br/></br> 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。<br/></br> 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。


## <a name="prepare-for-deployment"></a>準備部署
您必須部署 tooprepare:

1. [設定 Azure 網路](#set-up-an-azure-network) ，這是 Azure VM 於容錯移轉後所在的網路。
2. [設定 Azure 儲存體帳戶](#set-up-an-azure-storage-account) 。
3. [準備 hello VMM 伺服器](#prepare-the-vmm-server)的站台復原 」 部署。
4. 準備網路對應。 設定網路，以便在 Site Recovery 部署期間設定網路對應。

### <a name="set-up-an-azure-network"></a>設定 Azure 網路
您需要 Azure 網路 toowhich 之後會連接容錯移轉建立 Azure Vm。

* hello 網路應位於 hello hello 與相同的區域復原服務保存庫。
* 根據 hello 資源模型，您會想 toouse 容錯移轉 Azure Vm、 hello Azure 網路中設定[Resource Manager 模式](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)或[傳統模式](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。
* 建議您在開始之前先設定網路。 如果沒有，您需要 toodo Site Recovery 部署期間它。
Azure Site Recovery 所使用的網路不能[移動](../azure-resource-manager/resource-group-move-resources.md)hello 相同，或跨不同，訂用帳戶內。

### <a name="set-up-an-azure-storage-account"></a>設定 Azure 儲存體帳戶
* 您需要標準/優質 toohold 資料複寫 tooAzure 的 Azure 儲存體帳戶。[高階儲存體](../storage/common/storage-premium-storage.md)用於需要一直居高 IO 效能和低度延遲 toohost IO 密集工作負載的虛擬機器。 如果您想要 toouse premium 帳戶 toostore 複寫的資料，您也需要標準儲存體帳戶 toostore 複寫記錄檔擷取進行中變更 tooon 內部部署資料。 hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。
* Hello 資源模型，根據您想 toouse 容錯移轉 Azure Vm，您在設定帳戶[Resource Manager 模式](../storage/common/storage-create-storage-account.md)或[傳統模式](../storage/common/storage-create-storage-account.md)。
* 建議您在開始之前先設定帳戶。 如果沒有，您需要 toodo Site Recovery 部署期間它。
- 請注意，Site Recovery 所使用的儲存體帳戶不可[移動](../azure-resource-manager/resource-group-move-resources.md)hello 相同，或跨不同，訂用帳戶內。

### <a name="prepare-hello-vmm-server"></a>準備 hello VMM 伺服器
* 請確定該 hello VMM 伺服器符合 hello[必要條件](#prerequisites)。
* Site Recovery 部署期間，您可以指定的 VMM 伺服器上所有雲端都都可在 hello Azure 入口網站中。 如果您只想特定雲端 tooappear hello 入口網站中的，您可以啟用該 hello VMM 系統管理員主控台中的 hello 雲端上的設定。

### <a name="prepare-for-network-mapping"></a>準備網路對應
您必須在 Site Recovery 部署期間設定網路對應。 網路對應會之間 VMM VM 網路的來源和目標 Azure 網路，遵循 tooenable hello:

* 容錯移轉 hello 相同的電腦網路可以連接其他 tooeach，即使它們未容錯移轉中在方法或 hello hello 相同相同復原計劃。
* 如果網路閘道設定 hello 目標 Azure 網路上，Azure 虛擬機器可以連接 tooon 內部部署虛擬機器。
* tooset 網路對應，以下是您的需要：

  * 請確定 hello 來源 HYPER-V 主機伺服器上的 Vm 的連線的 tooa VMM VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
  * [如上](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [監視 + 管理] > [備份和 Site Recovery (OMS)]。

    ![新增保存庫](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. 在**名稱**，指定易記名稱 tooidentify hello 保存庫。 如果您有多個訂用帳戶，請選取其中一個。
4. [建立資源群組](../azure-resource-manager/resource-group-template-deploy-portal.md)，或選取現有的資源群組。 指定 Azure 區域。 機器必須複寫的 toothis 區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)
5. 如果您想從儀表板 hello tooquickly 存取 hello 保存庫，請按一下**Pin toodashboard** > **建立保存庫**。

    ![新增保存庫](./media/site-recovery-vmm-to-azure/new-vault.png)

hello 新的保存庫會出現在 hello**儀表板** > **所有資源**，在主要 hello**復原服務保存庫**刀鋒視窗。


## <a name="select-hello-protection-goal"></a>選取 hello 保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 在**復原服務保存庫**，選取 hello 保存庫。
2. 在 [快速入門] 中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。

    ![選擇目標](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. 在**保護目標**選取**tooAzure**，然後選取**是的含 HYPER-V**。 選取**是**tooconfirm 您使用 VMM toomanage HYPER-V 主機和 hello 復原站台。 然後按一下 [確定] 。

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

Hello VMM 伺服器上，安裝 hello Azure Site Recovery Provider 並註冊 hello 伺服器 hello 保存庫中。 在 HYPER-V 主機上安裝 hello Azure 復原服務代理程式。

1. 按一下 [準備基礎結構]  >  [來源]。

    ![設定來源](./media/site-recovery-vmm-to-azure/set-source1.png)

2. 在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。

    ![設定來源](./media/site-recovery-vmm-to-azure/set-source2.png)

3. 在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件和 URL需求](#prerequisites)。
4. 下載 hello Azure Site Recovery Provider 安裝檔案。
5. 下載 hello 登錄機碼。 您會在執行安裝程式時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Hello VMM 伺服器上安裝提供者 hello

1. 執行 hello VMM 伺服器上的 hello 提供者設定檔。
2. 在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。
3. 在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。

    ![安裝位置](./media/site-recovery-vmm-to-azure/provider2.png)
4. 安裝完成後，按一下**註冊**tooregister hello VMM 伺服器 hello 保存庫中的。
5. 在 hello**保存庫設定**頁面上，按一下**瀏覽**tooselect hello 保存庫金鑰檔。 指定 hello Azure Site Recovery 訂用帳戶和 hello 保存庫名稱。

    ![伺服器註冊](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. 在**網際網路連線**，指定如何 hello hello VMM 伺服器上執行的提供者會透過連線 tooSite 復原 hello 網際網路。

   * 若要直接 hello 提供者 tooconnect，選取**直接連接不使用 proxy 的站台復原 tooAzure**。
   * 如果您現有的 proxy 需要驗證，或您想要 toouse 自訂 proxy，選取**連線使用 proxy 伺服器的站台復原 tooAzure**。
   * 如果您使用自訂 proxy，請指定 hello 位址、 連接埠，以及認證。
   * 如果您使用 proxy，您應該已經允許 hello Url 中所述[必要條件](#on-premises-prerequisites)。
   * 如果您使用自訂 proxy，將會使用指定的 hello，自動建立 VMM RunAs 帳戶 (DRAProxyAccount) proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。 hello VMM 主控台中，可以修改 hello VMM RunAs 帳戶的設定。 在**設定**，依序展開**安全性** > **執行身分帳戶**，然後修改 draproxyaccount 的 hello 密碼。 您將需要 toorestart hello VMM 服務，讓這項設定會生效。

     ![網際網路](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. 接受或修改 hello 位置之資料加密時，會自動產生 SSL 憑證。 如果您啟用資料加密受 Azure 保護的 hello Azure Site Recovery 入口網站雲端，則會使用此憑證。 請保護此憑證的安全。 當您執行容錯移轉 tooAzure 您將需要它 toodecrypt，如果已啟用資料加密。

    > [!NOTE]
    > 建議您使用 Azure 所提供用於加密的待用資料，而不是使用 hello 資料加密 選項提供的 Azure Site Recovery toouse hello 加密功能。 hello Azure 所提供的加密功能可以開啟儲存體 > 帳戶，並可協助您達到更佳的效能，因為 hello 加密/解密由 Azure 儲存體。
    > [深入了解 Azure 中的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)。
    
8. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中，指定 hello VMM 叢集角色名稱。
9. 啟用**同步處理雲端中繼資料**，如果您想 toosynchronize 中繼資料的 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。 按一下**註冊**toocomplete hello 程序。

    ![伺服器註冊](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. 註冊作業隨即開始。 註冊完成之後，在中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **VMM 伺服器**。


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>HYPER-V 主機上安裝 hello Azure 復原服務代理程式

1. 當您設定 hello 提供者之後，您需要 toodownload hello 安裝檔案 hello Azure 復原服務代理程式。 Hello VMM 雲端中的每個 HYPER-V 伺服器上執行安裝程式。

    ![Hyper-V 網站](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. 在 [檢查先決條件] 中，按 [下一步]。 將自動安裝任何缺少的必要元件。

    ![Prerequisites Recovery Services Agent](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. 在**安裝設定**，接受或修改 hello 安裝位置，與 hello 快取位置。 您可以設定 hello 快取有至少 5 GB 的可用儲存體的磁碟機上，但我們建議 600 GB 或更多的可用空間的快取磁碟機。 然後按一下 [安裝] 。
4. 安裝已完成之後，請按一下**關閉**toofinish。

    ![註冊 MARS 代理程式](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>命令列安裝
您可以從命令列使用下列命令的 hello 安裝 Microsoft Azure Recovery Services Agent hello:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>設定網際網路的 proxy 存取 tooSite 復原，從 HYPER-V 主機

HYPER-V 主機上執行的 hello 復原服務代理程式需要網際網路存取 tooAzure VM 複寫。 如果您正在存取 hello 網際網路透過 proxy、 設定它，如下所示：

1. 開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機上。 根據預設，Microsoft Azure 備份的捷徑使用。 在 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。
3. 在 hello **Proxy 組態**索引標籤上，指定 proxy 伺服器資訊。

    ![註冊 MARS 代理程式](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. 檢查該 hello 代理程式是否可送達 hello 中所述的 hello Url[必要條件](#on-premises-prerequisites)。

## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定
指定用於複寫，hello Azure 儲存體帳戶 toobe 和容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。

1. 按一下**準備基礎結構** > **目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉虛擬機器的資源群組。 選擇要容錯移轉虛擬機器的 hello toouse Azure （classic 或資源管理） 中的 hello 部署模型。

    ![儲存體](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

    ![儲存體](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. 如果您尚未建立儲存體帳戶，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 儲存體帳戶**toodo 該內嵌。  在 hello**建立儲存體帳戶**刀鋒視窗中指定帳戶名稱、 類型、 訂閱與位置。 hello 帳戶應該位於 hello hello 與相同的位置復原服務保存庫。

   ![儲存體](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * 如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，請在 hello Azure 入口網站中。 [深入了解](../storage/common/storage-create-storage-account.md)
   * 如果您使用進階儲存體帳戶複寫資料，設定額外標準儲存體帳戶，擷取進行中的變更 tooon 內部部署資料的 toostore 複寫記錄檔。
5. 如果您尚未建立 Azure 網路，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 網路**toodo 該內嵌。 在 hello**建立虛擬網路**刀鋒視窗中指定的網路名稱、 位址範圍、 子網路詳細資料、 訂閱與位置。 hello 網路應位於 hello hello 與相同的位置復原服務保存庫。

   ![網路](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   如果您想 toocreate 網路使用 hello 傳統模式，請 hello Azure 入口網站中。 [深入了解](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。

### <a name="configure-network-mapping"></a>設定網路對應

* [閱讀](#prepare-for-network-mapping) 網路對應的快速概觀。
* 請確認 hello VMM 伺服器上的虛擬機器連線的 tooa VM 網路，而且您已建立至少一個 Azure 虛擬網路。 多個 VM 網路可以是對應的 tooa 單一 Azure 網路。

設定對應，如下所示︰

1. 在**Site Recovery 基礎結構** > **網路對應** > **網路對應**，按一下 hello **+ 的網路對應**圖示。

    ![網路對應](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. 在**加入網路對應**，選取 hello 來源 VMM 伺服器，和**Azure**為 hello 目標。
3. 在容錯移轉之後，請確認 hello 訂用帳戶和 hello 部署模型。
4. 在**來源網路**，選取您想要從 hello VMM 伺服器相關聯的 hello 清單 toomap hello 來源內部部署 VM 網路。
5. 在**目標網路**，選取 hello 複本 Azure 的 Vm 會位於位置在建立時即 Azure 網路。 然後按一下 [確定] 。

    ![網路對應](./media/site-recovery-vmm-to-azure/network-mapping2.png)

以下是網路對應開始時發生的事情︰

* Hello 來源 VM 網路上的現有 Vm 時開始對應連接的 toohello 目標網路。 新的 Vm 連接的 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。
* 如果您修改現有的網路對應，複本虛擬機器會連接使用 hello 新設定。
* 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。
* 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。

## <a name="configure-replication-settings"></a>設定複寫設定
1. toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。
3. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。

    > [!NOTE]
    >  複寫 toopremium 存放裝置時，不支援第二個頻率為 30。 hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。 [深入了解](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. 在**復原點保留**，以小時為單位指定多久 hello 保留時間將會針對每個復原點。 受保護的電腦可以是復原 tooany 視窗內的點。
5. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。 HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 請注意，是否您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。
6. 在**初始複寫開始時間**，指出當 toostart hello 初始複寫。 hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。
7. 在**加密資料儲存在 Azure 上**，指定是否在 Azure 儲存體中的其餘資料 tooencrypt。 然後按一下 [確定] 。

    ![複寫原則](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. 當您建立新的原則會自動對 hello VMM 雲端與其相關。 按一下 [確定] 。 您可以將其他 VMM 雲端 （和它們的 hello Vm），與在此複寫原則**複寫**> 原則名稱 >**關聯 VMM 雲端**。

    ![複寫原則](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>容量規劃

您現已設定您的基本基礎結構，請思考容量規劃並找出您是否需要額外的資源。

站台復原提供容量規劃 toohelp 您為來源環境、 站台復原元件、 網路及存放裝置配置 hello 正確的資源。 快速模式的 Vm、 磁碟和儲存體的平均數目為基礎的估計或在其中輸入數字在 hello 負載層級的詳細模式，您可以執行 hello 規劃。 開始之前：

* 收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。
* 評估 hello 複寫的資料可能會採用每日變更 （變換） 速率。 您可以使用 hello [HYPER-V 複本的容量規劃](https://www.microsoft.com/download/details.aspx?id=39057)toohelp 執行這項操作。

1. 按一下**下載**，toodownload hello 工具，然後加以執行。 [閱讀文章 hello](site-recovery-capacity-planner.md) ，伴隨著 hello 工具。
2. 當您完成時，選取**是**中**已執行 hello 容量規劃**嗎？

   ![容量規劃](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   深入了解[控制網路頻寬](#network-bandwidth-considerations)




## <a name="enable-replication"></a>啟用複寫

在開始之前，請確定您的 Azure 使用者帳戶具有所需的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。

立即啟用複寫，如下所示︰

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。 您已啟用複寫 hello 第一次之後，請按一下**+ 複寫**中的其他機器 hello 保存庫 tooenable 複寫。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. 在 hello**來源**刀鋒視窗中，選取 hello VMM 伺服器和 hello 雲端中的 hello HYPER-V 主機位於。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. 在**目標**、 選取 hello 訂用帳戶，容錯移轉後的部署模型，以及 hello 您所使用的複寫資料的儲存體帳戶。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. 選取您想 toouse hello 儲存體帳戶。 如果您想 toouse 您有不同的儲存體帳戶以外，您可以[建立一個](#set-up-an-azure-storage-account)。 如果您使用進階儲存體帳戶複寫資料，您需要 tooselect 額外標準儲存體帳戶 toostore 複寫記錄檔擷取進行中的變更 tooon 內部 data.toocreate 使用 hello 資源管理員模型的儲存體帳戶按一下**建立新**。 如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，這樣做， [hello Azure 入口網站中](../storage/common/storage-create-storage-account.md)。 然後按一下 [確定] 。
5. 在建立時即容錯移轉之後，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。 選取**現在選取的機器設定**，tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**，tooselect hello 每部機器的 Azure 網路。 如果您想 toouse 與您有不同的網路，您可以[建立一個](#set-up-an-azure-network)。 網路使用 toocreate hello 資源管理員模型中，按一下**建立新**。 如果您想 toocreate 網路使用 hello 傳統模式，這樣做， [hello Azure 入口網站中](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 選取適用的子網路。 然後按一下 [確定] 。
6. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. 在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。

    - 確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。   
    - 根據預設，所有 hello 磁碟的 hello VM 都選取複寫，但是您可以清除磁碟 tooexclude 它們。

        - 您可能想 tooexclude 磁碟 tooreduce 複寫的頻寬。 例如，您可能不想 tooreplicate 磁碟取代為暫存資料，或重新整理每次在電腦或應用程式的資料會重新啟動 （例如 pagefile.sys 或 Microsoft SQL Server tempdb）。 您可以取消選取 hello 磁碟從複寫排除 hello 磁碟。
        - 只有基本磁碟可以排除。 您無法排除作業系統磁碟。
        - 我們建議不要排除動態磁碟。 Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。 如果所有相依的動態磁碟區磁碟不排除，hello 受保護的動態磁碟會顯示失敗的磁碟時 hello VM 容錯移轉，而且您無法存取該磁碟上的 hello 資料。
        - 啟用複寫後，您無法加入或移除複寫的磁碟。 如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello VM，並重新啟用它。
        - 您以手動方式在 Azure 中建立的磁碟將不會容錯回復。 比方說，如果您無法超過三個磁碟，並建立兩個直接在 Azure VM 中，只有 hello 三個磁碟已容錯移轉將無法從 Azure tooHyper-V。 您不能包含在容錯回復，或從 HYPER-V tooAzure 的反向複寫以手動方式建立的磁碟。
        - 如果您排除的應用程式 toooperate 所需的磁碟，在容錯移轉 tooAzure 之後您需要的 toocreate 它以手動方式在 Azure 中，因此該 hello 複寫應用程式可以執行。 或者，您無法將 Azure 自動化整合至復原計劃，hello 機器容錯移轉期間 toocreate hello 磁碟。

    按一下**確定**toosave 變更。 您可以稍後再設定其他屬性。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. 在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。 然後按一下 [確定] 。 您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。 您套用的變更用於已在複寫的機器和新的機器。

   ![啟用複寫](./media/site-recovery-vmm-to-azure/enable-replication7.png)

您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。 之後 hello**完成保護**作業會執行，hello 機器是否已做好容錯移轉。

### <a name="view-and-manage-vm-properties"></a>檢視及管理 VM 屬性

我們建議您確認 hello hello 來源機器的屬性。 請記住該 hello Azure VM 名稱應該符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

1. 在**受保護項目**，按一下 **複寫的項目**，並選取 hello 機器 toosee 其詳細資料。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. 在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。

    ![啟用複寫](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. 在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。 修改與 hello 名稱 toocomply [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)如果您需要。 您也可以檢視和修改 hello 目標網路、 子網路及 hello 指派的 IP 位址資訊 toohello Azure VM。
請注意：

   * 您可以設定 hello 目標 IP 位址。 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。 如果您將無法使用在容錯移轉的位址，hello 容錯移轉將會失敗。 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。
   * hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：

     * 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
     * 如果 hello hello 來源虛擬機器介面卡的數目超過 hello 目標大小，允許 hello 數目，則使用 hello 目標大小最大值。
     * 例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個，然後 hello 目標電腦必須只有一個介面卡。     
     * 如果 hello VM 有多張網路介面卡，將所有連線 toohello 相同的網路。

     ![啟用複寫](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. 在**磁碟**您可以在 hello 將複寫的 VM 上看到 hello 作業系統和資料磁碟。

#### <a name="managed-disks"></a>受控磁碟

在**計算與網路** > **計算屬性**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器，您可以設定 「 使用受管理磁碟 」 設定太"Yes"hello VM。 受管理的磁碟，藉以管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure IaaS Vm 的磁碟管理。 [深入了解受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)。

   - 受管理的磁碟是已建立並附加 toohello 只能在容錯移轉 tooAzure 上的虛擬機器。 啟用保護之後，在內部部署機器的資料會繼續 tooreplicate toostorage 帳戶。
   受管理的磁碟只可以建立使用 hello 資源管理員部署模型部署虛擬機器。  

  > [!NOTE]
  > 從 Azure tooon 部署的 HYPER-V 環境中的容錯回復目前不支援受管理的磁碟使用的機器。 設定 「 使用受管理磁碟 」 太"Yes"唯有當您想 toomigrate 這部電腦到 Azure。

   - 當您設定 「 使用受管理磁碟 」 太"Yes"時，只可用性設定組 hello 資源群組中的使用 「 使用受管理磁碟 」 組太"Yes"時將可讓您選取。 這是因為受管理的磁碟與虛擬機器只能太 「 是 」 是 「 受管理的使用磁碟 」 屬性設定的可用性設定組的一部分。 請確定您使用 「 使用受管理磁碟 」 屬性集，根據您在容錯移轉的受管理的意圖 toouse 磁碟建立可用性設定組。  同樣地，當您設定 「 使用受管理磁碟 」 太"No"時，只有與 「 使用受管理磁碟 」 的屬性設定太"No"hello 資源群組中的可用性設定組將可讓您選取。 [深入了解受控磁碟和可用性設定組](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。

  > [!NOTE]
  > 如果 hello 儲存體帳戶用於複寫加密所使用的儲存體服務加密的任何一點的時間，在容錯移轉期間建立受管理的磁碟將會失敗。 您可以設定 「 使用受管理磁碟 」 太"No"時和重試容錯移轉或停用 hello 虛擬機器的保護和 tooa 儲存體帳戶沒有時間啟用在任何時間點的儲存體服務加密可保護它。
  > [深入了解儲存體服務加密及受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。


## <a name="test-hello-deployment"></a>測試 hello 部署

您可以執行單一的虛擬機器或包含一或多個虛擬機器的復原計劃的測試容錯移轉 tootest hello 部署。

### <a name="before-you-start"></a>開始之前

 - 如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP 深入了解[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。
 - 您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。 [深入了解](site-recovery-active-directory.md#test-failover-considerations)。

### <a name="run-a-test-failover"></a>執行測試容錯移轉

1. 容錯移轉的單一 VM，toofail 中**複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**。
2. toofail 透過復原計劃，在**復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。
3. 在**測試容錯移轉**，選取 hello Azure 網路 toowhich Azure Vm 連接之後發生容錯移轉。
4. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業中**站台復原工作**。
5. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，並正在執行。
6. 如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。
7. 一旦您完成時，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。

如需詳細資訊，請閱讀 hello[測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)發行項。

## <a name="monitor-hello-deployment"></a>監視 hello 部署

以下是如何監視組態設定、 狀態和健全狀況 hello 部署站台復原：

1. 按一下 hello 保存庫名稱 tooaccess hello **Essentials**儀表板。 在此儀表板中，您可以看見 Site Recovery 作業、複寫狀態、復原方案、伺服器健康狀態和事件。  您可以自訂**Essentials** tooshow hello 磚和配置的是最有用的 tooyou，包括 hello 狀態的其他站台復原和備份保存庫。

    ![基本資訊](./media/site-recovery-vmm-to-azure/essentials.png)
2. 在**健全狀況**，您可以監視內部部署伺服器 （VMM 或組態伺服器） 上的問題和 hello Site recovery 中 hello 過去 24 小時的引發的事件。
3. 在 hello**複寫的項目**，**復原計劃**，和**站台復原作業**磚，您可以管理和監視複寫。 您可以在 [作業]  > [Site Recovery 作業] 中鑽研作業。

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery 提供者的命令列安裝

可以從命令列 hello 安裝 hello Azure Site Recovery Provider。 此方法就會使用的 tooinstall hello 的 Windows Server 2012 R2 的 Server Core 上的提供者。

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如，C:\ASR。
2. 從提升權限的命令提示字元中執行這些命令 tooextract hello 提供者安裝程式：

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. 執行這個命令 tooinstall hello 元件：

            C:\ASR> setupdr.exe /i
4. 然後在 hello 保存庫中執行這些命令及 tooregister hello 伺服器：

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

其中：

* **/ 認證**： 指定 hello 註冊金鑰檔所在位置的必要參數。  
* **/Friendlyname**: hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要參數。
* * **/ EncryptionEnabled**： 選擇性參數，當您要複寫在 VMM 中的 HYPER-V Vm 雲端 tooAzure。 指定是否要讓 tooencrypt Azure 虛擬機器中 （在 rest 加密）。 請確定該 hello hello 檔案名稱具有**.pfx**延伸模組。 預設會關閉加密。

    > [!NOTE]
    > 建議您使用 Azure 所提供用於加密的待用資料，而不是使用 hello 加密選項 （EncryptionEnabled 選項） 提供的 Azure Site Recovery toouse hello 加密功能。 hello Azure 所提供的加密功能可以開啟儲存體帳戶，且可協助達到更佳的效能 hello 加密/解密是由 Azure  
    > 。
    > [深入了解 Azure 中的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)。
    
* **/proxyAddress**： 指定 hello hello proxy 伺服器位址的選擇性參數。
* **/proxyport**： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。
* **/proxyUsername**： 指定 hello proxy 使用者名稱 （如果 proxy 需要驗證） 的選擇性參數。
* **/proxyPassword**： 指定 proxy 伺服器 hello 密碼 tooauthenticate （如果 hello proxy 需要驗證） 的選擇性參數。


### <a name="network-bandwidth-considerations"></a>網路頻寬考量
您可以使用 hello 容量規劃工具 toocalculate hello 頻寬您需要複寫 （初始複寫，然後差異處）。 toocontrol hello 數量進行複寫的頻寬用量，您有幾個選項：

* **節流的頻寬**: HYPER-V tooa 次要站台進行複寫流量透過特定的 HYPER-V 主機。 您可以節流處理 hello 主機伺服器上的頻寬。
* **調整頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬。

#### <a name="throttle-bandwidth"></a>節流頻寬
1. 開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機伺服器上。 根據預設，Microsoft Azure 備份的捷徑使用。 在 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。
3. 在 hello**節流**索引標籤上，選取**啟用網際網路頻寬使用節流設定的備份操作**，並設定工作的 hello 限制和非工作小時。 有效範圍是從每秒 512 Kbps too102 Mbps。

    ![節流頻寬](./media/site-recovery-vmm-to-azure/throttle2.png)

您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。 以下是一個範例：

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 表示不需要節流。

#### <a name="influence-network-bandwidth"></a>影響網路頻寬
hello **UploadThreadsPerVM**登錄值會控制 hello 磁碟的資料傳輸 （初始或差異複寫） 所使用的執行緒數目。 較高的值會增加 hello 網路頻寬用於複寫。 hello **DownloadThreadsPerVM**登錄值會指定 hello 容錯回復期間用來傳送資料的執行緒數目。

1. 在 hello 登錄中，瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。

   * 修改 hello 值**UploadThreadsPerVM** （或建立 hello 索引鍵，如果不存在） toocontrol 執行緒用於磁碟複寫。
   * 修改 hello 值**DownloadThreadsPerVM** （或建立 hello 索引鍵，如果不存在） 用於從 Azure 容錯回復流量 toocontrol 執行緒。
2. hello 預設值為 4。 在 「 超量佈建 」 的網路中，應該從 hello 預設值變更這些登錄機碼。 hello 上限為 32。 監視流量 toooptimize hello 值。

## <a name="next-steps"></a>後續步驟

初始複寫完成，並測試過 hello 部署之後，您可以在 hello 需要時叫用容錯移轉。 [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。
