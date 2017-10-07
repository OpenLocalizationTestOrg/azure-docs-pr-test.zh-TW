---
title: "hello 來源和目標 （使用 System Center VMM) 」 與 Azure Site Recovery 中的 HYPER-V 複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset 與 Azure Site Recovery 的 VMM 雲端 tooAzure 儲存體中的 HYPER-V Vm 複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>步驟 8: Hello 來源和目標 （使用 VMM) 的 HYPER-V 複寫 tooAzure 設定

之後[建立保存庫](vmm-to-azure-walkthrough-create-vault.md)並指定您想 tooreplicate、 使用此發行項 tooconfigure 來源和目標設定，當複寫在內部部署 HYPER-V 虛擬機器在 System Center Virtual Machine Manager (VMM)雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

S1. 按一下 [準備基礎結構]  >  [來源]。

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. 在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. 在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件和 URL需求](#prerequisites)。
4. 下載 hello Azure Site Recovery Provider 安裝檔案。
5. 下載 hello 登錄機碼。 您會在執行安裝程式時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Hello VMM 伺服器上安裝提供者 hello

1. 執行 hello VMM 伺服器上的 hello 提供者設定檔。
2. 在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。
3. 在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。

    ![安裝位置](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. 安裝完成後，按一下**註冊**tooregister hello VMM 伺服器 hello 保存庫中的。
5. 在 hello**保存庫設定**頁面上，按一下**瀏覽**tooselect hello 保存庫金鑰檔。 指定 hello Azure Site Recovery 訂用帳戶和 hello 保存庫名稱。

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. 在**網際網路連線**，指定如何 hello hello VMM 伺服器上執行的提供者會透過連線 tooSite 復原 hello 網際網路。

   * 若要直接 hello 提供者 tooconnect，選取**直接連接不使用 proxy 的站台復原 tooAzure**。
   * 如果您現有的 proxy 需要驗證，或您想要 toouse 自訂 proxy，選取**連線使用 proxy 伺服器的站台復原 tooAzure**。
   * 如果您使用自訂 proxy，請指定 hello 位址、 連接埠，以及認證。
   * 如果您使用 proxy，您應該已經允許 hello Url 中所述[必要條件](#on-premises-prerequisites)。
   * 如果您使用自訂 proxy，將會使用指定的 hello，自動建立 VMM RunAs 帳戶 (DRAProxyAccount) proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。 hello VMM 主控台中，可以修改 hello VMM RunAs 帳戶的設定。 在**設定**，依序展開**安全性** > **執行身分帳戶**，然後修改 draproxyaccount 的 hello 密碼。 您將需要 toorestart hello VMM 服務，讓這項設定會生效。

     ![網際網路](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. 接受或修改 hello 位置之資料加密時，會自動產生 SSL 憑證。 如果您啟用資料加密受 Azure 保護的 hello Azure Site Recovery 入口網站雲端，則會使用此憑證。 請保護此憑證的安全。 當您執行容錯移轉 tooAzure 您將需要它 toodecrypt，如果已啟用資料加密。
8. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中，指定 hello VMM 叢集角色名稱。
9. 啟用**同步處理雲端中繼資料**，如果您想 toosynchronize 中繼資料的 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。 按一下**註冊**toocomplete hello 程序。

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. 註冊作業隨即開始。 註冊完成之後，在中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **VMM 伺服器**。


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>HYPER-V 主機上安裝 hello Azure 復原服務代理程式

1. 當您設定 hello 提供者之後，您需要 toodownload hello 安裝檔案 hello Azure 復原服務代理程式。 Hello VMM 雲端中的每個 HYPER-V 伺服器上執行安裝程式。

    ![Hyper-V 網站](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. 在 [檢查先決條件] 中，按 [下一步]。 將自動安裝任何缺少的必要元件。

    ![Prerequisites Recovery Services Agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. 在**安裝設定**，接受或修改 hello 安裝位置，與 hello 快取位置。 您可以設定 hello 快取有至少 5 GB 的可用儲存體的磁碟機上，但我們建議 600 GB 或更多的可用空間的快取磁碟機。 然後按一下 [安裝] 。
4. 安裝已完成之後，請按一下**關閉**toofinish。

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>命令列安裝
您可以從命令列使用下列命令的 hello 安裝 Microsoft Azure Recovery Services Agent hello:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>設定網際網路的 proxy 存取 tooSite 復原，從 HYPER-V 主機

HYPER-V 主機上執行的 hello 復原服務代理程式需要網際網路存取 tooAzure VM 複寫。 如果您正在存取 hello 網際網路透過 proxy、 設定它，如下所示：

1. 開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機上。 根據預設，Microsoft Azure 備份的捷徑使用。 在 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。
3. 在 hello **Proxy 組態**索引標籤上，指定 proxy 伺服器資訊。

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. 檢查該 hello 代理程式是否可送達 hello 中所述的 hello Url[必要條件](#on-premises-prerequisites)。

## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定
指定用於複寫，hello Azure 儲存體帳戶 toobe 和容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。

1. 按一下**準備基礎結構** > **目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉虛擬機器的資源群組。 選擇要容錯移轉虛擬機器的 hello toouse Azure （classic 或資源管理） 中的 hello 部署模型。

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. 如果您尚未建立儲存體帳戶，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 儲存體帳戶**toodo 該內嵌。  在 hello**建立儲存體帳戶**刀鋒視窗中指定帳戶名稱、 類型、 訂閱與位置。 hello 帳戶應該位於 hello hello 與相同的位置復原服務保存庫。

   ![儲存體](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * 如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，請在 hello Azure 入口網站中。 [深入了解](../storage/common/storage-create-storage-account.md)
   * 如果您使用進階儲存體帳戶複寫資料，設定額外標準儲存體帳戶，擷取進行中的變更 tooon 內部部署資料的 toostore 複寫記錄檔。
5. 如果您尚未建立 Azure 網路，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 網路**toodo 該內嵌。 在 hello**建立虛擬網路**刀鋒視窗中指定的網路名稱、 位址範圍、 子網路詳細資料、 訂閱與位置。 hello 網路應位於 hello hello 與相同的位置復原服務保存庫。

   ![網路](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   如果您想 toocreate 網路使用 hello 傳統模式，請 hello Azure 入口網站中。 [深入了解](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。





## <a name="next-steps"></a>後續步驟

跳過[步驟 9： 設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)
