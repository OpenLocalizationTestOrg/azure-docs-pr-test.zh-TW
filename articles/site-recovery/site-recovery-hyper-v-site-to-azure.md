---
title: "aaaReplicate HYPER-V Vm tooAzure |Microsoft 文件"
description: "描述如何 tooorchestrate 複寫、 容錯移轉和復原的內部部署 Hyper-v-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure hello Azure 入口網站中使用 Azure Site Recovery

> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-hyper-v-site-to-azure.md)
> * [Azure 傳統型](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - 資源管理員](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

本文說明如何 tooreplicate 內部部署 HYPER-V 虛擬機器 tooAzure，使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。 在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

如果您想 toomigrate 機器 tooAzure （不含錯誤後回復），進一步了解[本文](site-recovery-migrate-to-azure.md)。



## <a name="deployment-steps"></a>部署步驟

請依照下列 hello 文章 toocomplete 部署步驟執行：

1. [進一步了解](site-recovery-components.md#hyper-v-to-azure)有關此部署的 hello 架構。 此外，[深入了解](site-recovery-hyper-v-azure-architecture.md) Site Recovery 中 Hyper-V 複寫的運作方式。
2. 確認必要條件和限制。
3. 設定 Azure 網路和儲存體帳戶。
4. 準備 Hyper-V 主機。
5. 建立復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。
6. 指定來源設定。 建立 HYPER-V 站台包含 hello 與 HYPER-V 主機，並在 hello 保存庫中註冊 hello 站台。 安裝 Azure Site Recovery Provider，hello 和 hello Microsoft 復原服務代理程式，hello HYPER-V 主機上。
7. 設定目標和複寫設定。
8. 啟用複寫 hello Vm。
9. 執行測試容錯移轉 toomake 確定一切如預期般運作。



## <a name="prerequisites"></a>必要條件


**需求** | **詳細資料** |
--- | --- |
**Azure** | 了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。
**內部部署伺服器** | [進一步了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)關於 hello 在內部部署 HYPER-V 主機的需求。
**內部部署 Hyper-V VM** | 您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
**Azure URL** | HYPER-V 主機需要存取 toothese Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。<br/></br> 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。<br/></br> 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。



## <a name="prepare-for-deployment"></a>準備部署

您需要部署 tooprepare:

1. [設定 Azure 網路](#set-up-an-azure-network) ，這是 Azure VM 於容錯移轉後建立時將所在的網路。
2. [設定 Azure 儲存體帳戶](#set-up-an-azure-storage-account) 。
3. [準備 hello HYPER-V 主機](#prepare-the-hyper-v-hosts)tooensure 他們可以存取 hello 所需的 Url。

### <a name="set-up-an-azure-network"></a>設定 Azure 網路

設定 Azure 網路。 您將需要此以便 hello Azure Vm 建立容錯移轉之後連接的 tooa 網路。

* hello 網路應位於 hello hello 與相同的區域復原服務保存庫。
* 根據 hello 資源模型，您會想 toouse 容錯移轉 Azure Vm、 hello Azure 網路中設定[Resource Manager 模式](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)，或[傳統模式](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。
* 建議您在開始之前先設定網路。 如果沒有，您需要 toodo Site Recovery 部署期間它。
- Site Recovery 所使用的儲存體帳戶不能是[移動](../azure-resource-manager/resource-group-move-resources.md)hello 相同，或跨不同，訂用帳戶內。


### <a name="set-up-an-azure-storage-account"></a>設定 Azure 儲存體帳戶

- 您需要標準/優質 toohold 資料複寫 tooAzure 的 Azure 儲存體帳戶。[高階儲存體](../storage/storage-premium-storage.md)通常用於需要一直居高 IO 效能和低度延遲 toohost IO 密集工作負載的虛擬機器。
- 如果您想要 toouse premium 帳戶 toostore 複寫的資料，您也需要標準儲存體帳戶 toostore 複寫記錄檔擷取進行中變更 tooon 內部部署資料。
- Hello 資源模型，根據您想 toouse 容錯移轉 Azure Vm，您在設定帳戶[Resource Manager 模式](../storage/storage-create-storage-account.md)，或[傳統模式](../storage/storage-create-storage-account-classic-portal.md)。
- 建議您在開始之前先設定儲存體帳戶。 如果您需要 toodo Site Recovery 部署期間它。 hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。
- 儲存體帳戶之間所使用的站台復原 hello 內的資源群組相同，則無法移動訂用帳戶，或跨不同的訂用帳戶。


### <a name="prepare-hello-hyper-v-hosts"></a>準備 hello 與 HYPER-V 主機

* 請確定 hello HYPER-V 主機符合 hello[必要條件](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)。
- 請確定 hello 主機可存取所需的 hello Url。


## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [監視 + 管理] > [備份和 Site Recovery (OMS)]。  

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. 在**名稱**，指定易記名稱 tooidentify hello 保存庫。 如果您有多個訂用帳戶，請選取其中一個。

4. [建立新的資源群組](../azure-resource-manager/resource-group-template-deploy-portal.md) 或選取現有的資源群組，並指定 Azure 區域。 機器必須複寫的 toothis 區域。 支援 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。

5. 如果您想從儀表板 hello tooquickly 存取 hello 保存庫，請按一下**Pin toodashboard**，然後按一下**建立**。

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

hello 新的保存庫會出現在 hello**儀表板** > **所有資源**清單，並在 hello 主要**復原服務保存庫**刀鋒視窗。



## <a name="select-hello-protection-goal"></a>選取 hello 保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 在 hello**復原服務保存庫**，選取 hello 保存庫。
2. 在 [快速入門] 中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. 在**保護目標**，選取**tooAzure**，然後選取**是的含 HYPER-V**。 選取**否**tooconfirm 您未使用 VMM。 然後按一下 [確定] 。

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello HYPER-V 站台、 HYPER-V 主機上安裝 Azure Site Recovery Provider hello 和 hello Azure 復原服務代理程式和 hello 保存庫中註冊 hello 站台。

1. 在 [準備基礎結構] 中，按一下 [來源]。 按一下 新的 HYPER-V 站台做為您的 HYPER-V 主機或叢集的容器 tooadd **+ HYPER-V 站台**。

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. 在**建立 HYPER-V 站台**，指定 hello 網站的名稱。 然後按一下 [確定] 。 現在，選取您建立，然後按一下 「 hello 」 站台**+ HYPER-V Server** tooadd 伺服器 toohello 站台。

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. 在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。

    - 請確定您想要 hello tooadd 符合該 hello HYPER-V 伺服器[必要條件](#on-premises-prerequisites)，和是無法 tooaccess hello 指定的 Url。
    - 下載 hello Azure Site Recovery Provider 安裝檔案。 執行此檔案 tooinstall hello 提供者並 hello 每個 HYPER-V 主機上的復原服務代理程式。

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>安裝 hello 提供者和代理程式

1. 您已新增 toohello HYPER-V 站台執行每個主機上的 hello 提供者安裝程式檔案。 如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。 安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。
2. 在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。
3. 在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。
4. 在**保存庫設定**，按一下 **瀏覽**tooselect hello 保存庫金鑰檔下載。 指定 hello Azure Site Recovery 訂用帳戶，hello 保存庫名稱，並所屬 hello HYPER-V 站台 toowhich hello HYPER-V 伺服器。

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. 在**Proxy 設定**，指定 HYPER-V 主機上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路的方式。

    * 如果您想 hello 提供者 tooconnect 直接選取**直接連接不使用 proxy 的站台復原 tooAzure**。
    * 如果您現有的 proxy 需要驗證，或者您想 toouse 自訂 proxy hello 提供者連接，請選取**連線使用 proxy 伺服器的站台復原 tooAzure**。
    * 如果您使用 Proxy：
        - 指定 hello 位址、 連接埠和認證
        - 請確定 hello 中所述的 hello Url[必要條件](#prerequisites)允許透過 hello proxy。

    ![網際網路](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. 安裝完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![安裝位置](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. 註冊完成之後，Azure Site Recovery 中，擷取中繼資料從 hello HYPER-V 伺服器和中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **HYPER-V 主機**。


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

指定 hello Azure 儲存體帳戶來進行複寫，並容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。

1. 按一下 [準備基礎結構] > [目標]。
2. 選取 hello 訂用帳戶與您想 toocreate hello Azure Vm 容錯移轉之後的 hello 資源群組。 選擇 hello 部署模型的 toouse Azure （classic 或資源管理） 中的 hello Vm。

3. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

    - 如果您沒有儲存體帳戶，按一下**+ 儲存體**toocreate 資源管理員帳戶內嵌。 深入了解[儲存體需求](site-recovery-prereq.md#azure-requirements)。
    - 如果您沒有 Azure 網路，按一下**+ 網路**toocreate 資源管理員為基礎的網路內嵌。

    ![儲存體](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>設定複寫設定

1. toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。
3. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。

    > [!NOTE]
    > 複寫 toopremium 存放裝置時，不支援第二個頻率為 30。 hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。 [深入了解](../storage/storage-premium-storage.md#snapshots-and-copy-blob)。

4. 在**復原點保留**，指定以小時多久 hello 保留週期是每個復原點。 Vm 就能復原 tooany 視窗內的點。
5. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。

    - HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。
    - 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。
    - 如果您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。

6. 在**初始複寫開始時間**，指定當 toostart hello 初始複寫。 hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。 然後按一下 [確定] 。

    ![複寫原則](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

當您建立新的原則時，它會自動與相關聯 hello HYPER-V 站台。 您可以將 HYPER-V 站台 （和中的 hello Vm） 中的多個複寫原則與**複寫**> 原則名稱 >**關聯 HYPER-V 站台**。

## <a name="capacity-planning"></a>容量規劃

您現已設定您的基本基礎結構，您可以思考容量規劃並找出您是否需要額外的資源。

站台復原提供容量規劃 toohelp 讓您針對計算、 網路及存放裝置配置 hello 正確的資源。 您可以執行 hello 規劃 detailed 模式或快速模式的 Vm、 磁碟和儲存體的平均數目為基礎的估計中使用自訂的數字在 hello 工作負載層級。 開始之前，您必須︰

* 收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。
* 評估 hello 每日變更 （變換） 速率複寫的資料。 您可以使用 hello [HYPER-V 複本的容量規劃](https://www.microsoft.com/download/details.aspx?id=39057)toohelp 執行這項操作。

1. 按一下**下載**toodownload hello 工具，並加以執行。 [閱讀文章 hello](site-recovery-capacity-planner.md) ，伴隨著 hello 工具。
2. 當您完成時，選取**是**中**已執行 hello 容量規劃**嗎？

   ![容量規劃](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

深入了解[控制網路頻寬](#network-bandwidth-considerations)



## <a name="enable-replication"></a>啟用複寫

在開始之前，請確定您的 Azure 使用者帳戶具有所需的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。

啟用 VM 複寫，如下所示︰          

1. 按一下 [複寫應用程式] > [來源]。 您已設定第一次的 hello 複寫之後，您可以按一下**+ 複寫**tooenable 其他機器複寫。

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. 在**來源**，選取 hello HYPER-V 站台。 然後按一下 [確定] 。
3. 在**目標**選取 hello 保存庫訂用帳戶，hello 想在容錯移轉之後 toouse Azure （classic 或資源管理） 中的容錯移轉模式。
4. 選取您想 toouse hello 儲存體帳戶。 如果您沒有您想要讓 toouse 帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。 然後按一下 [確定] 。
5. 正在建立容錯移轉時，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。

    - 選取 tooapply hello 網路設定 tooall 機器啟用複寫，**現在選取的機器設定**。
    - 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。
    - 如果您沒有您想 toouse 網路，您可以[建立一個](#set-up-an-azure-network)。 選取適用的子網路。 然後按一下 [確定] 。

   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. 在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。
8. 確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
9. 根據預設，所有 hello 磁碟的 hello VM 都選取複寫，但是您可以清除磁碟 tooexclude 它們。
    - 您可能想 tooexclude 磁碟 tooreduce 複寫的頻寬。 例如，您可能不想 tooreplicate 磁碟取代為暫存資料，或重新整理每次在電腦或應用程式的資料會重新啟動 （例如 pagefile.sys 或 Microsoft SQL Server tempdb）。 您可以取消選取 hello 磁碟從複寫排除 hello 磁碟。
    - 只有基本磁碟可以排除。 您無法排除作業系統磁碟。
    - 我們建議不要排除動態磁碟。 Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。 如果所有相依的動態磁碟區磁碟不排除，hello 受保護的動態磁碟會顯示失敗的磁碟時 hello VM 容錯移轉，而且您無法存取該磁碟上的 hello 資料。
        - 啟用複寫後，您無法加入或移除複寫的磁碟。 如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello VM，並重新啟用它。
        - 您以手動方式在 Azure 中建立的磁碟將不會容錯回復。 比方說，如果您無法超過三個磁碟，並建立兩個直接在 Azure VM 中，只有 hello 三個磁碟已容錯移轉將無法從 Azure tooHyper-V。 您不能包含在容錯回復，或從 HYPER-V tooAzure 的反向複寫以手動方式建立的磁碟。
        - 如果您排除的應用程式 toooperate 所需的磁碟，在容錯移轉 tooAzure 之後您需要的 toocreate 它以手動方式在 Azure 中，因此該 hello 複寫應用程式可以執行。 或者，您無法將 Azure 自動化整合至復原計劃，hello 機器容錯移轉期間 toocreate hello 磁碟。

10. 按一下**確定**toosave 變更。 您可以稍後再設定其他屬性。

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. 在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。 然後按一下 [確定] 。 您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。 您套用的變更將用於已在複寫的機器和新的機器。


   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。 之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。

### <a name="view-and-manage-vm-properties"></a>檢視及管理 VM 屬性

我們建議您確認 hello hello 來源機器的屬性。

1. 在**受保護項目**，按一下 **複寫的項目**，並選取 hello 機器。

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. 在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. 在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。 如果您需要，修改 hello 名稱 toocomply Azure 需求。 您也可以檢視和修改 hello 目標網路、 子網路及指派 toohello Azure VM 的 IP 位址資訊。 請注意 hello 下列：

   * 您可以設定 hello 目標 IP 位址。 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。 如果您將無法使用在容錯移轉的位址，hello 容錯移轉將會失敗。 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。
   * hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：

     * 如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
     * 如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
     * 例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。     
     * 如果 hello VM 有多張網路介面卡將所有連線 toohello 相同的網路。
     * 如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。

     ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. 在**磁碟**、 您所見 hello 作業系統和資料磁碟上的 hello 將複寫的 VM。

#### <a name="managed-disks"></a>受控磁碟

在**計算與網路** > **計算屬性**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器，您可以設定 「 使用受管理磁碟 」 設定太"Yes"hello VM。 受管理的磁碟，藉以管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure IaaS Vm 的磁碟管理。 [深入了解受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)。

   - 受管理的磁碟是已建立並附加 toohello 只能在容錯移轉 tooAzure 上的虛擬機器。 啟用保護之後，在內部部署機器的資料會繼續 tooreplicate toostorage 帳戶。
   受管理的磁碟只可以建立使用 hello 資源管理員部署模型部署虛擬機器。

  > [!NOTE]
  > 從 Azure tooon 部署的 HYPER-V 環境中的容錯回復目前不支援受管理的磁碟使用的機器。 「 使用受管理磁碟 」 太"Yes"時才設定此機器 tooAzure 想 toomigrate。

   - 當您設定 「 使用受管理磁碟 」 太"Yes"時，只可用性設定組 hello 資源群組中的使用 「 使用受管理磁碟 」 組太"Yes"時將可讓您選取。 這是因為受管理的磁碟與虛擬機器只能太 「 是 」 是 「 受管理的使用磁碟 」 屬性設定的可用性設定組的一部分。 請確定您使用 「 使用受管理磁碟 」 屬性集，根據您在容錯移轉的受管理的意圖 toouse 磁碟建立可用性設定組。 同樣地，當您設定 「 使用受管理磁碟 」 太"No"時，只有與 「 使用受管理磁碟 」 的屬性設定太"No"hello 資源群組中的可用性設定組將可讓您選取。 [深入了解受控磁碟和可用性設定組](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。

  > [!NOTE]
  > 如果 hello 儲存體帳戶用於複寫加密所使用的儲存體服務加密的任何一點的時間，在容錯移轉期間建立受管理的磁碟將會失敗。 您可以設定 「 使用受管理磁碟 」 太"No"時和重試容錯移轉或停用 hello 虛擬機器的保護和 tooa 儲存體帳戶沒有時間啟用在任何時間點的儲存體服務加密可保護它。
  > [深入了解儲存體服務加密及受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。


## <a name="test-hello-deployment"></a>測試 hello 部署

您可以執行單一的虛擬機器或包含一或多個虛擬機器的復原計劃的測試容錯移轉 tootest hello 部署。

### <a name="before-you-start"></a>開始之前

 - 如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP 深入了解[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。
 - 您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。 [深入了解](site-recovery-active-directory.md#test-failover-considerations)。

### <a name="run-a-test-failover"></a>執行測試容錯移轉

1. 透過單一電腦、 toofail 中**複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。
2. toofail 透過復原計劃，在**復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。
3. 在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。
4. 按一下**確定**toobegin hello 容錯移轉。 您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**作業** > **站台復原工作**。
5. Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。
6. 如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。
7. 一旦您完成時，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。

如需詳細資訊，請閱讀 hello[測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)發行項。



## <a name="monitor-hello-deployment"></a>監視 hello 部署

Hello 組態設定、 狀態和站台復原部署的健全狀況監視：

1. 按一下 hello 保存庫名稱 tooaccess hello **Essentials**儀表板。 在此儀表板中，您可以追蹤 Site Recovery 作業、複寫狀態、復原方案、伺服器健康情況和事件。  

    ![基本資訊](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. 在 hello**健全狀況**磚，您可以監視發生問題，並 hello 引發的事件 Site recovery hello 過去 24 小時內的站台伺服器。 您可以自訂 Essentials tooshow hello 磚和配置的是最有用的 tooyou，包括 hello 狀態的其他站台復原和備份保存庫。
3. 您可以管理和監視複寫的 hello**複寫的項目**，**復原計劃**，和**站台復原作業**磚。 您可以在 [作業]  >  [Site Recovery 作業] 中鑽研作業以了解詳細資訊。

## <a name="command-line-provider-and-agent-installation"></a>命令列 Provider 和代理程式安裝

hello Azure Site Recovery Provider 代理程式也可以被安裝和使用下列命令列的 hello。 這個方法可以是使用的 tooinstall hello 的提供者的 Windows Server 2012 R2 的 Server Core 上。

1. 下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。 例如 C:\ASR。
2. 從提升權限的命令提示字元中執行這些命令 tooextract hello 提供者安裝程式：

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. 執行這個命令 tooinstall hello 元件：

            C:\ASR> setupdr.exe /i
4. 然後伺服器上執行這些命令 tooregister hello hello 保存庫中：

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
其中：

* **/ 認證**： 指定 hello 位置中的 hello 註冊金鑰檔所在的必要參數  
* **/Friendlyname**: hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要參數。
* **/proxyAddress**： 指定 hello hello proxy 伺服器位址的選擇性參數。
* **/proxyport** ： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。
* **/proxyUsername**： 指定 hello Proxy 使用者名稱 （如果 proxy 需要驗證） 的選擇性參數。
* **/proxyPassword**： 指定的選擇性參數 hello 密碼進行驗證的 hello proxy 伺服器 （proxy 需要驗證）。


## <a name="network-bandwidth-considerations"></a>網路頻寬考量
您可以使用 hello [HYPER-V 產能規劃工具](site-recovery-capacity-planner.md)toocalculate hello 頻寬，您需要複寫 （初始複寫，然後差異處）。 toocontrol hello 數量的複寫的頻寬使用量，您有幾個選項：

* **節流的頻寬**: HYPER-V 複寫 tooAzure 流量透過特定的 HYPER-V 主機。 您可以節流處理 hello 主機伺服器上的頻寬。
* **調整頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬。

### <a name="throttle-bandwidth"></a>節流頻寬
1. 開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機伺服器上。 依預設 Microsoft Azure 備份的捷徑。 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin
2. 在 [hello] 嵌入式管理單元中按一下**變更屬性**。
3. 在 hello**節流**索引標籤上選取**啟用網際網路頻寬使用節流設定的備份操作**，並設定工作的 hello 限制和非工作小時。 有效範圍是從每秒 512 Kbps too102 Mbps。

    ![節流頻寬](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。 以下是一個範例：

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 表示不需要節流。

### <a name="influence-network-bandwidth"></a>影響網路頻寬
1. Hello 登錄中瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。
   * tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值 hello **UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。
   * 從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。
2. hello 預設值為 4。 在 「 超量佈建 」 的網路中，應該從 hello 預設值變更這些登錄機碼。 hello 上限為 32。 監視流量 toooptimize hello 值。

## <a name="next-steps"></a>後續步驟

初始複寫完成，並測試過 hello 部署之後，您可以在 hello 需要時叫用容錯移轉。 [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。
