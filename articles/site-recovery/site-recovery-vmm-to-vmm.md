---
title: "aaaReplicate HYPER-V Vm tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "描述如何在 VMM 雲端 tooa 次要 VMM 站台使用的 HYPER-V Vm tooreplicate hello Azure 入口網站。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>複寫 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-vmm.md)
> * [傳統入口網站](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

本文說明如何 tooreplicate 內部部署 System Center Virtual Machine Manager (VMM) 雲端中受管理的 HYPER-V 虛擬機器 tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。 深入了解此[案例架構](site-recovery-components.md)。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="prerequisites"></a>必要條件

**必要條件** | **詳細資料**
--- | ---
**Azure** | 您需要 [Microsoft Azure](http://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。
**內部部署 VMM** | 我們建議您有兩部 VMM 伺服器在 hello 主要站台，一個次要的 hello 中。<br/><br/> 您可以在單一 VMM 伺服器上的雲端之間進行複寫。<br/><br/> VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新的更新。<br/><br/> VMM 伺服器需要網際網路存取。
**VMM 雲端** | 每一部 VMM 伺服器必須在一個或多個雲端，而所有雲端必須都具有 hello HYPER-V 容量設定檔集合。 <br/><br/>雲端必須包含一或多個 VMM 主機群組。<br/><br/> 如果您只有一部 VMM 伺服器，它需要至少兩個雲端、 tooact 為主要和次要資料庫。
**Hyper-V** | HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。<br/><br/> Hyper-V 伺服器應該包含一或多部 VM。<br/><br/>  HYPER-V 主機伺服器應該位於 hello 主要和次要 VMM 雲端中的主機群組。<br/><br/> 如果您在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，請安裝[更新 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> 如果您在 Windows Server 2012 上的叢集中執行 Hyper-V，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集訊息代理程式。 手動設定 hello 叢集代理人。 [閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。<br/><br/> Hyper-V 伺服器需要網際網路存取。
**URL** | VMM 伺服器和 HYPER-V 主機應能 tooreach 這些 Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>部署步驟

以下是您要執行的動作：

1. 驗證必要條件。
2. 準備 hello VMM 伺服器和 HYPER-V 主機。
3. 建立復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。
4. 指定來源、目標和複寫設定。
5. 您想 tooreplicate 部署 Vm 上的 hello 行動服務。
6. 準備進行複寫，並啟用 Hyper-V VM 的複寫。
7. 執行測試容錯移轉 toomake 確定一切如預期般運作。

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>準備 VMM 伺服器和 Hyper-V 主機

tooprepare 部署：

1. 請確定 hello VMM 伺服器和 HYPER-V 主機符合上面所述的 hello 必要條件，而且可以到達所需的 hello Url。
2. 設定 VMM 網路，以便設定[網路對應](#network-mapping-overview)。

    - 請確定 hello 來源 HYPER-V 主機伺服器上的 Vm 的連線的 tooa VMM VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
    確認您用於復原的 hello 次要雲端已設定的對應 VM 網路。 該 VM 網路應連結的 tooa hello 次要雲端相關聯的邏輯網路。

3. 準備[單一伺服器部署](#single-vmm-server-deployment)，如果您想在 hello 雲端之間 tooreplicate Vm 相同的 VMM 伺服器。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [管理] > [復原服務]。
3. 在**名稱**，指定易記名稱 tooidentify hello 保存庫。 如果您有多個訂用帳戶，請選取其中一個。
4. [建立資源群組](../azure-resource-manager/resource-group-template-deploy-portal.md)，或選取現有的資源群組。 指定 Azure 區域。 機器會複寫的 toothis 區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)
5. 如果您想從儀表板 hello tooquickly 存取 hello 保存庫，請按一下**Pin toodashboard** > **建立保存庫**。

    ![新增保存庫](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

hello 新的保存庫會出現在 hello**儀表板**，請在**所有資源**，在主要 hello**復原服務保存庫**刀鋒視窗。


## <a name="choose-a-protection-goal"></a>選擇保護目標

選取您想要 tooreplicate 和您想要 tooreplicate。

2. 按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [保護目標]。
3. 選取**toorecovery 網站**，然後選取**是的含 HYPER-V**。
4. 選取**是**tooindicate 您使用 VMM toomanage hello HYPER-V 主機。
5. 如果您有次要 VMM 伺服器，請選取 [是]。 如果您要在單一 VMM 伺服器上的雲端之間部署複寫，請按一下 [否] 。 然後按一下 [確定] 。

    ![選擇目標](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

Hello Azure Site Recovery Provider 安裝 VMM 伺服器上探索和 hello 保存庫中註冊伺服器。

1. 按一下 [步驟 1：準備基礎結構]  >  [來源]。

    ![設定來源](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. 在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。

    ![設定來源](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. 在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件](#prerequisites).
4. 下載 hello Azure Site Recovery Provider 安裝檔案。
5. 下載 hello 登錄機碼。 您會在執行安裝程式時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Hello VMM 伺服器上安裝 hello Azure Site Recovery Provider。 您不需要 tooexplicitly 則會在 HYPER-V 主機伺服器上安裝任何項目。


### <a name="install-hello-azure-site-recovery-provider"></a>安裝 Azure Site Recovery Provider hello

1. 執行每一部 VMM 伺服器上的 hello 提供者安裝程式檔案。 如果 VMM 部署在叢集中，請勿遵循您所安裝的第一次 hello hello:
    -  Hello 提供者上安裝的作用中的節點，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。
    - 然後，hello 提供者上安裝 hello 其他節點。 叢集節點應該執行所有 hello 相同版本的 hello 提供者。
2. 安裝程式會執行幾個必要條件檢查，並要求權限 toostop hello VMM 服務。 hello VMM 服務將會自動重新啟動安裝程式完成時。 如果您安裝在 VMM 叢集上，您提示的 toostop hello 叢集角色。
3. 在**Microsoft Update**，您也可以選擇 toospecify，根據 Microsoft Update 原則安裝 provider 更新。
4. 在**安裝**接受或修改 hello 預設安裝位置，然後按**安裝**。

    ![安裝位置](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. 安裝已完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![安裝位置](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. 在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。 按一下 [下一步] 。

    ![伺服器註冊](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. 在**網際網路連線**，指定 hello hello VMM 伺服器上執行的提供者如何連接 tooAzure。

    ![網際網路設定](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - 您可以指定該 hello 提供者應該連接直接 toohello 網際網路，或透過 proxy。
   - 指定 proxy 設定 (如有需要)。
   - VMM RunAs 帳戶 (DRAProxyAccount) 如果您使用 proxy，使用指定的 hello 自動會建立 proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。 hello RunAs 帳戶的設定可以修改 hello VMM 主控台中 >**設定** > **安全性** > **執行身分帳戶**。 重新啟動 hello VMM 服務 tooupdate 變更。
8. 在**登錄機碼**，選取您從 Azure Site Recovery 下載並複製 toohello VMM 伺服器的 hello 索引鍵。
9. 只有在您要在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時，才會使用 hello 加密設定。 如果您要複寫 tooa 次要站台不使用它。
10. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中指定 hello VMM 叢集角色名稱。
11. 在**同步處理雲端中繼資料**，選取是否要在 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端的 toosynchronize 中繼資料。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選，此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。
12. 按一下**下一步**toocomplete hello 程序。 註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 hello 伺服器顯示在 [hello **VMM 伺服器**] 索引標籤上 hello**伺服器**hello 保存庫中的頁面。

    ![伺服器](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Hello 伺服器可以使用在 hello 站台復原主控台中之後, 在**來源** > **準備來源**hello VMM 伺服器，並選取 hello 雲端中的 hello HYPER-V 主機所在的選取。 然後按一下 [確定] 。

您也可以從 hello 命令列安裝 hello 提供者：

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

選取 hello 目標 VMM 伺服器和雲端。

1. 按一下**準備基礎結構** > **目標**，和您想要 toouse hello 選取目標 VMM 伺服器。
2. 將會顯示 hello 伺服器上會同步處理與 Site Recovery 的雲端。 選取 hello 目標雲端。

   ![目標](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>設定複寫設定

- 當您建立的複寫原則時，使用 hello 原則的所有主機必須有都 hello 相同的作業系統。 hello VMM 雲端可以包含執行不同版本的 Windows Server HYPER-V 主機，但在此情況下，您需要多個複寫原則。
- 您可以執行 hello 的離線初始複寫。 [深入了解](#prepare-for-initial-offline-replication)

1. 按一下 新的複寫原則 toocreate**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。 hello 來源和目標型別應該是**HYPER-V**。
3. 在**HYPER-V 主機版本**，選取 hello 主機上執行的作業系統。
4. 在**驗證類型**和**驗證連接埠**，指定如何驗證主要 hello 和復原 HYPER-V 主機伺服器之間的流量。 除非您有有效的 Kerberos 環境，否則請選取 [憑證]。 Azure Site Recovery 會自動設定用於 HTTPS 驗證的憑證。 您不需要 toodo 任何項目以手動方式。 根據預設，將 hello HYPER-V 主機伺服器上的 hello Windows 防火牆中開啟連接埠 8083 和 8084 （用於憑證）。 如果您選取**Kerberos**，將會進行相互驗證的 hello 主機伺服器使用 Kerberos 票證。 請注意，這項設定只有在 Hyper-V 主機伺服器是執行於 Windows Server 2012 R2 時才有重要性。
5. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。
6. 在**復原點保留**，以小時為單位指定多久 hello 保留時間將會針對每個復原點。 受保護的電腦可以是復原 tooany 視窗內的點。
7. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。 HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 如果您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。
8. 在 [資料傳輸壓縮] 中，指定是否應該將傳輸的已複寫資料壓縮。
9. 選取**刪除複本 VM**，應該刪除 hello 複本虛擬機器的 toospecify，如果您停用 hello 來源 VM 的保護。 如果您啟用此設定，當您停用保護 hello 來源會從 hello Site Recovery 主控台中移除的 VM，hello VMM 站台復原設定移除了 hello VMM 主控台中，並刪除 hello 複本。
10. 在**初始複寫方法**，如果您要複寫 hello 網路上指定是否 toostart hello 初始複寫，或者排程它。 toosave 網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。 然後按一下 [確定] 。

     ![複寫原則](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. 當您建立新的原則會自動對 hello VMM 雲端與其相關。 在 [複寫原則] 中，按一下 [確定]。 您可以將其他 VMM 雲端 （和它們的 hello Vm），與在此複寫原則**複寫**> 原則名稱 >**關聯 VMM 雲端**。

     ![複寫原則](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>設定網路對應

- 開始之前，深入了解[網路對應](#prepare-for-network-mapping)。
- 請確認 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。


1. 在 [Site Recovery 基礎結構] > [網路對應] > [網路對應]，按一下 [+網路對應]。

    ![網路對應](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. 在**加入網路對應**索引標籤上，選取 hello 來源與目標 VMM 伺服器。 擷取 hello 與 hello VMM 伺服器相關聯的 VM 網路。
3. 在**來源網路**，選取您想 toouse hello 清單中的 hello 主要 VMM 伺服器相關聯的 VM 網路的 hello 網路。
4. 在**目標網路**，選取您想 toouse hello 次要 VMM 伺服器上的 hello 網路。 然後按一下 [確定] 。

    ![網路對應](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

以下是網路對應開始時發生的事情︰

* 對應 toohello 來源 VM 網路的任何現有複本虛擬機器會連接的 toohello 目標 VM 網路。
* 新的虛擬機器所連接的 toohello 來源 VM 網路在複寫之後會連接的 toohello 目標對應的網路。
* 如果您修改現有的對應與新的網路，複本虛擬機器將使用 hello 新設定連接。
* 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。

### <a name="configure-storage-mapping"></a>設定儲存體對應。

[儲存體對應](#prepare-for-storage-mapping)hello 新版 Azure 入口網站中，不支援。 不過，可以使用 Powershell 來啟用這項功能。 [深入了解](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping)。

## <a name="step-5-capacity-planning"></a>步驟 5︰容量規劃

您現已設定您的基本基礎結構，請思考容量規劃並找出您是否需要額外的資源。

- 下載並執行 hello [Azure 站台復原容量規劃](site-recovery-capacity-planner.md)，每個 VM 和每個磁碟的儲存體磁碟 toogather 複寫環境，包括 Vm 的相關資訊。
- 已收集到的即時複寫資訊之後，您可以修改 hello NetQos 原則 toocontrol 複寫頻寬的 Vm。 請至 Thomas Maurer 部落格深入了解[節流處理 Hyper-V 複本流量](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/)。 取得詳細資訊 hello [New-netqospolicy cmdlet](https://technet.microsoft.com/library/hh967468.aspx.)。

## <a name="enable-replication"></a>啟用複寫

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。 您已啟用複寫 hello 第一次後，按一下  **+ 複寫**中的其他機器 hello 保存庫 tooenable 複寫。

    ![啟用複寫](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. 在**來源**、 選取 hello VMM 伺服器，和 hello 中的 hello 想 tooreplicate 的 HYPER-V 主機位於的雲端。 然後按一下 [確定] 。

    ![啟用複寫](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. 在**目標**，確認 hello 次要 VMM 伺服器和雲端。
4. 在**虛擬機器**，選取您想要從 hello 清單 tooprotect hello Vm。

    ![啟用虛擬機器保護](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

您可以追蹤進度的 hello**啟用保護**中的動作**作業** > **站台復原工作**。 之後 hello**完成保護**作業完成、 hello 虛擬機器是否已做好容錯移轉。

請注意：

- 您也可以啟用 hello VMM 主控台中的虛擬機器的保護。 按一下**啟用保護**hello 虛擬機器內容中的 hello 工具列上 > **Azure Site Recovery**  索引標籤。
- 啟用複寫之後，您可以檢視內容 hello VM 中**複寫的項目**。 在 hello **Essentials**儀表板，您可以看到 hello hello VM 和其狀態的複寫原則的相關資訊。 如需詳細資訊，請按一下 [屬性]  。

### <a name="onboard-existing-virtual-machines"></a>建立現有的虛擬機器
如果 VMM 中目前已經有使用 Hyper-V 複本複寫的虛擬機器，您可以使用下列方式加入它們以提供 Azure Site Recovery 複寫：

1. 請確認裝載現有 VM 的 hello hello HYPER-V 伺服器位於 hello 主要雲端，然後裝載 hello 複本虛擬機器的 hello HYPER-V 伺服器位於 hello 次要雲端。
2. 請確定 hello 主要 VMM 雲端所設定的複寫原則。
3. 啟用 hello 主要虛擬機器的複寫。 Azure Site Recovery 和 VMM 確定 hello 相同的複本主機和虛擬機器偵測到，，和 Azure Site Recovery 會重複使用，並重新建立複寫使用 hello 指定設定。

## <a name="test-your-deployment"></a>測試您的部署

tootest 您的部署，您可以執行[測試容錯移轉](site-recovery-test-failover-vmm-to-vmm.md)單一的虛擬機器，或[建立復原計劃](site-recovery-create-recovery-plans.md)，其中包含一或多個虛擬機器。



## <a name="prepare-for-offline-initial-replication"></a>準備進行離線初始複寫

您可以進行離線複寫 hello 初始資料複本。 您可以如下所示方式進行準備︰

* Hello 來源伺服器上，您可以指定從哪個 hello 資料匯出，就會進行的路徑位置。 指派 「 完整控制 NTFS 和共用權限 toohello hello 匯出路徑上的 VMM 服務。 在 hello 目標伺服器上，指定從中 hello 資料匯入的路徑位置就會發生。 指派 hello 這個匯入路徑上的相同權限。
* 如果 hello 匯入或匯出路徑共用，指派 hello 遠端電腦上的 hello VMM 服務帳戶的系統管理員、 Power User、 列印操作員或伺服器操作員群組成員資格位於上共用的 hello。
* 如果您使用的任何執行身分帳戶 tooadd 主機，hello 上匯入和匯出路徑、 指派讀取和寫入權限 toohello 執行身分帳戶在 VMM 中。
* hello 匯入和匯出共用應該位於任何做為 HYPER-V 主機伺服器的電腦因為 HYPER-V 不支援回送設定。
* 在每個包含您想 tooprotect，虛擬機器的 HYPER-V 主機伺服器上的 Active Directory 中啟用及設定限制的委派 tootrust hello 遠端電腦上的 hello 匯入和匯出路徑，如下：
  1. 在 hello 網域控制站上開啟**Active Directory 使用者和電腦**。
  2. 在 hello 主控台樹狀目錄中，按一下  **DomainName** > **電腦**。
  3. 以滑鼠右鍵按一下 hello HYPER-V 主機伺服器名稱 >**屬性**。
  4. 在 hello**委派**索引標籤上，按一下 **信任這台電腦所委派 toospecified 服務只**。
  5. 按一下 [使用任何驗證通訊協定] 。
  6. 按一下 [新增]  > 提出技術問題。
  7. 型別 hello 裝載 hello 匯出路徑的 hello 電腦名稱 >**確定**。 從 hello 的可用服務清單，請在按住 hello CTRL 鍵，然後按一下  **cifs** > **確定**。 Hello 電腦名稱的 hello 重複該主機 hello 匯入路徑。 視需要為其他 Hyper-V 主機伺服器重複動作。



## <a name="prepare-for-network-mapping"></a>準備網路對應
Hello 主要和次要 VMM 伺服器上的 VMM VM 網路之間的網路對應會：

* 容錯移轉之後，選擇性地在次要 Hyper-V 主機上放置複本 VM。
* 容錯移轉之後連接複本 Vm tooappropriate VM 網路。

請注意：
- 網路對應可以設定兩部 VMM 伺服器上的 VM 網路之間或單一 VMM 伺服器上如果兩個站台由管理 hello 相同伺服器。
- 當正確設定對應和已啟用複寫，hello 主要位置的 VM 將會連接的 tooa 網路而它在 hello 目標位置的複本將會連接 tooits 對應網路。
- 如果網路有已正確設定在 VMM 中，當您在網路對應期間選取目標 VM 網路時，使用 hello 來源 VM 網路的 hello VMM 來源雲端將會顯示，以及用於 hello 目標雲端上的 hello 可用目標 VM 網路保護。
- 如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。


以下是範例 tooillustrate 這項機制。 讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。

| **位置** | **VMM 伺服器** | **VM 網路** | **對應至** |
| --- | --- | --- | --- |
| 紐約 |VMM-NewYork |VMNetwork1-NewYork |對應的 tooVMNetwork1 芝加哥 |
| VMNetwork2-NewYork |未對應 | | |
| 芝加哥 |VMM-Chicago |VMNetwork1-Chicago |對應的 tooVMNetwork1 紐約 |
| VMNetwork2-Chicago |未對應 | | |

在此範例中：

* 針對已連線的 tooVMNetwork1 紐約任何虛擬機器建立複本虛擬機器時，就會連接的 tooVMNetwork1 芝加哥。
* VMNetwork2 紐約或 VMNetwork2 芝加哥建立複本虛擬機器時，它將無法連接的 tooany 網路。

以下是如何在我們的範例組織中，與 hello 與 hello 雲端相關聯的邏輯網路中設定 VMM 雲端。

### <a name="cloud-protection-settings"></a>雲端保護設定
| **受保護的雲端** | **保護雲端** | **邏輯網路 (紐約)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>NA</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |
| SilverCloud2 |<p>NA</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>邏輯和 VM 網路設定
| **位置** | **邏輯網路** | **相關聯的 VM 網路** |
| --- | --- | --- |
| 紐約 |LogicalNetwork1-NewYork |VMNetwork1-NewYork |
| 芝加哥 |LogicalNetwork1-Chicago |VMNetwork1-Chicago |
| LogicalNetwork2Chicago |VMNetwork2-Chicago | |

### <a name="target-networks"></a>目標網路
根據這些設定，當您選取 hello 目標 VM 網路，hello 下表顯示的 hello 選項可供使用。

| **選取** | **受保護的雲端** | **保護雲端** | **可用的目標網路** |
| --- | --- | --- | --- |
| VMNetwork1-Chicago |SilverCloud1 |SilverCloud2 |可用 |
| GoldCloud1 |GoldCloud2 |可用 | |
| VMNetwork2-Chicago |SilverCloud1 |SilverCloud2 |尚未提供 |
| GoldCloud1 |GoldCloud2 |可用 | |


### <a name="failback"></a>容錯回復
toosee 怎樣 hello 案例容錯回復 （反向複寫），讓我們假設 VMNetwork1 紐約對應的 tooVMNetwork1-芝加哥，以下列設定的 hello。

| **虛擬機器** | **連接的 tooVM 網路** |
| --- | --- |
| VM1 |VMNetwork1-Network |
| VM2 (VM1 的複本) |VMNetwork1-Chicago |

讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。

| **案例** | **結果** |
| --- | --- |
| Vm-2 的容錯移轉之後的 hello 網路屬性沒有變更。 |Vm-1 依然連接的 toohello 來源網路。 |
| 在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。 |VM-1 已中斷連線。 |
| Vm-2 的網路屬性會變更容錯移轉之後，並且已連線的 tooVMNetwork2 芝加哥。 |如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。 |
| VMNetwork1-Chicago 的網路對應已變更。 |Vm-1 將會連接的 toohello 現在對應的網路 tooVMNetwork1 芝加哥。 |


## <a name="prepare-for-single-server-deployment"></a>準備進行單一伺服器部署


如果您只有單一 VMM 伺服器，您可以將複寫 Vm hello VMM 雲端中的 HYPER-V 主機中太[Azure](site-recovery-vmm-to-azure.md)或 tooa 次要 VMM 雲端。 我們建議 hello 第一個選項，因為雲端之間的複寫不順暢。 如果您想 tooreplicate 雲端之間，您可以使用單一獨立 VMM 伺服器，或複寫延展 Windows 叢集中部署一部 VMM 伺服器

### <a name="standalone-vmm-server"></a>獨立 VMM 伺服器

在此案例中，您為虛擬機器在 hello 主要站台部署單一 VMM 伺服器 hello 和複寫 VM tooa 此次要站台使用站台復原 」 和 「 HYPER-V 複本。

1. **在 Hyper-V VM 上設定 VMM**。 我們建議您將共置 hello hello 上使用 VMM 的 SQL Server 執行個體相同的 VM。 這可以節省時間只能有一個 VM 仍為 toobe 建立。 如果您想 toouse 遠端 SQL Server 執行個體發生中斷，您需要 toorecover 該執行個體之前，您可以復原 VMM。
2. **請 hello VMM 伺服器已設定至少兩個雲端**。 一個雲端會包含您想 tooreplicate 和 hello 其他雲端的 Vm 將做為 hello 次要位置的 hello。 hello，其中包含您想要 tooprotect 應遵守的 hello Vm 雲端[必要條件](#prerequisites)。
3. 以本文所述的方式設定 Site Recovery。 建立及註冊保存庫中的 hello VMM 伺服器、 設定的複寫原則，並啟用複寫。 hello 來源與目標 VMM 名稱將 hello 相同。 指定初始複寫會透過 hello 網路進行。
4. 當您設定網路對應會對應 hello hello 主要雲端 toohello hello 次要雲端的 VM 網路的 VM 網路。
5. 在 hello HYPER-V 管理員主控台中，包含 hello VMM VM 的 hello HYPER-V 主機上啟用 HYPER-V 複本和 hello VM 上啟用複寫。 請確定您不要新增 hello VMM 虛擬機器 tooclouds Site recovery，tooensure HYPER-V 複本設定不覆寫 Site recovery 保護。
6. 如果您建立您所使用的容錯移轉的復原計劃 hello 相同的 VMM 伺服器，來源和目標。
7. 在完全中斷運作的情況下，您進行容錯移轉和復原的方式如下︰

   1. Hello hello 次要站台中，toofail hello 主要 VMM VM toohello 次要站台上的 HYPER-V Manager 主控台中，執行未規劃的容錯移轉。
   2. 請確認 VMM VM 已啟動該 hello 並正常執行，並在 hello 保存庫 hello Vm 上執行規劃的容錯移轉 toofail 從主要 toosecondary 雲端。 認可 hello 容錯移轉，並視需要選取替代的復原點。
   3. Hello 規劃的容錯移轉完成之後，所有存取的資源可以從 hello 主要站台一次。
   4. 同樣地，在 hello hello 次要站台中的 HYPER-V Manager 主控台中可用 hello 主要站台時，啟用 hello VMM VM 的反向複寫。 這是從次要 tooprimary 開始 hello VM 的複寫。
   5. Hello hello 次要站台中，toofail hello VMM VM toohello 主要站台上的 HYPER-V Manager 主控台中執行規劃的容錯移轉。 認可 hello 容錯移轉。 再啟用反向複寫，如此 hello VMM VM 會再次從伺服器複寫主要 toosecondary。
   6. 在 hello 復原服務保存庫，讓 hello 工作負載的 Vm，從次要 tooprimary 複寫它們 toostart 的反向複寫。
   7. Hello 復原服務保存庫中，執行規劃的容錯移轉 toofail 後 hello 工作負載 Vm toohello 主要站台。 認可 hello 容錯移轉 toocomplete 它。 然後啟用反向複寫 toostart 複寫 hello 工作負載 Vm 從主要 toosecondary。

### <a name="stretched-vmm-cluster"></a>延伸的 VMM 叢集

而是作為複寫 tooa 次要站台 VM 部署獨立 VMM 伺服器，您可以讓 VMM 高可用性部署為 Windows 容錯移轉叢集中的 VM。 這可以提供工作負載彈性及硬體故障的防護。 在各地不同的站台之間，應該自動縮放叢集中部署 toodeploy 以 Site Recovery hello VMM VM。 toodo 這樣：

1. 在 Windows 容錯移轉叢集中的虛擬機器上安裝 VMM，並在安裝期間選取 hello 選項 toorun hello 伺服器為高可用性。
2. hello SQL Server 執行個體，以供 VMM 應該複寫使用 SQL Server AlwaysOn 可用性群組，使 hello hello 次要站台資料庫複本。
3. 遵循本文章 toocreate 保存庫中的 hello 指示，註冊 hello 伺服器，以及設定保護。 您需要的 tooregister hello 復原服務保存庫中的 hello 中的每部 VMM 伺服器叢集。 toodo，作用中節點上，安裝 hello 提供者，並註冊 hello VMM 伺服器。 然後您可以安裝 hello 提供者的其他節點上。
4. 發生中斷時，會容錯移轉，而且從 hello 次要站台存取 hello VMM 伺服器和其相對應的 SQL Server 資料庫。



## <a name="prepare-for-storage-mapping"></a>準備儲存體對應


您可以設定儲存體對應所對應的儲存體分類在來源及目標 VMM 伺服器 toodo hello 下列：

  * **識別複本虛擬機器的目標儲存體**— 來源 VM 硬碟會將複寫您指定的 toohello 儲存體 （SMB 共用或叢集共用磁碟區 (Csv)） 在 hello 目標位置。
  * **複本虛擬機器放置**— 儲存對應是在 HYPER-V 主機伺服器上使用的 toooptimally 放置複本虛擬機器。 複本虛擬機器會置於可以存取對應的 hello 存放裝置分類的主機。
  * **沒有儲存體對應**— 如果您未設定儲存對應，虛擬機器必須複寫的 toohello hello 複本虛擬機器相關聯的 hello HYPER-V 主機伺服器上所指定的預設儲存位置。

請注意：
- 您可以在單一伺服器上設定兩個 VMM 雲端之間的對應。
- 儲存分類必須可使用 toohello 位於來源與目標雲端的主機群組。
- 分類不需 toohave hello 相同類型的儲存體。 例如，您可以對應來源分類，其中包含 SMB 共用 tooa 目標分類包含 Csv。

### <a name="example"></a>範例
如果在 VMM 中，當您選取 hello 來源和目標 VMM 伺服器期間儲存對應分類均正確無誤，將會顯示 hello 來源與目標分類。 以下是儲存體檔案共用和分類的範例，以供擁有兩個位置 (紐約和芝加哥) 的組織使用。

| **位置** | **VMM 伺服器** | **檔案共用 (來源)** | **分類 (來源)** | **對應至** | **檔案共用 (目標)** |
| --- | --- | --- | --- | --- | --- |
| 紐約 |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| 芝加哥 |VMM_Target | |GOLD_TARGET |未對應 | |
|  |SILVER_TARGET |未對應 | | | |
|  |BRONZE_TARGET |未對應 | | | |

在此範例中：

* 金級存放裝置 (SourceShare1) 上的任何虛擬機器建立複本虛擬機器時，就會複寫的 tooa GOLD_TARGET 儲存體 (TargetShare1)。
* 銀級存放裝置 (SourceShare2) 上的任何虛擬機器建立複本虛擬機器時，它會複寫的 tooa SILVER_TARGET (TargetShare2) 儲存體，以此類推。

### <a name="multiple-storage-locations"></a>多個儲存體位置
如果 hello 目標分類指派 toomultiple SMB 共用或 Csv，hello 最佳的儲存體位置將會自動選取受保護 hello 虛擬機器時。 如果沒有適合的目標儲存體是適用於 hello 指定分類，hello 預設 hello HYPER-V 主機上指定的儲存位置是使用的 tooplace hello 複本虛擬硬碟。

下表中的 hello 顯示存放裝置分類和叢集共用磁碟區設定的方式在我們的範例。

| **位置** | **分類** | **相關聯的儲存體** |
| --- | --- | --- |
| 紐約 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| 芝加哥 |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

當您啟用在此範例的環境中的虛擬機器 (VM1-VM5) 的保護時，此表格概述 hello 行為。

| **虛擬機器** | **來源儲存體** | **來源分類** | **對應的目標儲存體** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>兩個 GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>兩個 GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>兩個 SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N/A |沒有對應，因此會使用 hello 預設儲存位置的 hello HYPER-V 主機 |



### <a name="data-privacy-overview"></a>資料隱私權概觀

下表摘要說明此案例中儲存資料的方式︰

- - -
| 動作 | **詳細資料** | **收集的資料** | **使用** | **必要** |
| --- | --- | --- | --- | --- |
| **註冊** | 您在復原服務保存庫中註冊 VMM 伺服器。 如果您稍後想 toounregister 伺服器，您可以從 hello Azure 入口網站刪除 hello 伺服器資訊。 | 在註冊 VMM 伺服器之後 Site Recovery 會收集處理程序，以及傳輸 hello VMM 伺服器和 hello 名稱 hello 偵測到 Site recovery 的 VMM 雲端的相關中繼資料。 | hello 資料是使用的 tooidentify 及與 hello 適當 VMM 伺服器通訊，並設定適當的 VMM 雲端的設定。 | 此為必要功能。 如果您不想 toosend 此資訊 tooSite 復原您不應該使用 hello Site Recovery 服務。 |
| **啟用複寫** | hello Azure Site Recovery Provider 安裝 hello VMM 伺服器上並 hello 管道與 hello Site Recovery 服務進行通訊。 hello 提供者是在 hello VMM 程序中裝載的動態連結程式庫 (DLL)。 安裝提供者的 hello 之後, 取得 hello VMM 系統管理員主控台中啟用 hello 「 資料中心復原 」 功能。 新的和現有的 Vm 可以啟用此功能 tooenable 保護 vm。 |設定這個屬性 hello 提供者會傳送 hello 名稱和識別碼 hello VM tooSite 復原。  複寫是透過 Windows Server 2012 或 Windows Server 2012 R2 Hyper-V 複本來啟用。 從一個 HYPER-V 主機 tooanother （通常位於不同的 「 復原 」 資料中心），取得複寫 hello 虛擬機器資料。 |站台復原使用 hello Azure 入口網站中的 hello 中繼資料 toopopulate hello VM 資訊。 | 此功能是 hello 服務不可或缺的一部分，且無法關閉。 如果您不想 toosend 這項資訊，請勿啟用之 Vm 的 Site Recovery 保護。 請注意，透過 HTTPS 傳送 hello 提供者 tooSite 復原所傳送的所有資料。 |
| **復原計畫** | 復原計劃可協助您建置 hello 復原資料中心協調流程方案。 您可以定義應該在 hello 復原站台啟動 Vm 或一群虛擬機器的 hello 順序。 您也可以指定執行時，任何自動化的指令碼 toobe 或復原每個 VM hello 時採取的任何手動動作 toobe。 容錯移轉通常是在 hello 協調的復原的復原計劃層級觸發。 | Site Recovery 會收集、 處理或傳輸 hello 復原計劃，包括虛擬機器中繼資料和中繼資料的任何自動化指令碼和手動動作備註的中繼資料。 |hello 中繼資料是使用的 toobuild hello 復原計劃 hello Azure 入口網站中。 |此功能是 hello 服務不可或缺的一部分，且無法關閉。 如果您不想 toosend 此資訊 tooSite 復原，不會建立復原方案。 |
| **網路對應** | 對應網路 hello 主要資料中心 toohello 復原資料中心的資訊。 當 Vm 復原 hello 復原站台上時，網路對應會有助於中建立的網路連線。 |Site Recovery 會收集、 處理或傳輸 hello hello 邏輯網路，每個站台 （主要和 datacenter） 的中繼資料。 |hello 中繼資料是使用的 toopopulate 網路設定，因此您可以將對應 hello 網路資訊。 | 此功能是 hello 服務不可或缺的一部分，且無法關閉。 如果您不想 toosend 此資訊 tooSite 復原，請勿使用網路對應。 |
| **容錯移轉 (計劃性/非計劃性/測試)** | 容錯移轉從容錯移轉 Vm 一個 VMM 管理的資料中心 tooanother。 hello Azure 入口網站中手動觸發 hello 容錯移轉動作。 |hello VMM 伺服器上的 hello 提供者會 hello 容錯移轉事件通知，Site recovery，並透過 VMM 介面執行 hello HYPER-V 主機上的容錯移轉動作。 實際的容錯移轉虛擬機器從一個 HYPER-V 主機 tooanother 並由 Windows Server 2012 或 Windows Server 2012 R2 HYPER-V 複本。 後 Site Recovery 會使用傳送 hello 容錯移轉動作資訊 toopopulate hello 狀態 hello Azure 入口網站中的 hello 資訊。 | 此功能是 hello 服務不可或缺的一部分，且無法關閉。 如果您不想 toosend 此資訊 tooSite 復原，不要使用容錯移轉。 |

## <a name="next-steps"></a>後續步驟

測試過 hello 部署之後，深入了解其他類型的[容錯移轉](site-recovery-failover.md)
