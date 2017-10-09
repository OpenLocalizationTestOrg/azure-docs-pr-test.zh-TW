---
title: "aaaMigrating tooAzure 使用 「 Azure 站台復原的進階儲存體 |Microsoft 文件"
description: "移轉您現有的虛擬機器 tooAzure 使用站台復原的進階儲存體。 「進階儲存體」可針對在「Azure 虛擬機器」上執行且需要大量 I/O 的工作負載，提供高效能、低延遲的磁碟支援。"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cb71c06e4a1a73d484e226a573d1ade48c87664d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery"></a>移轉 tooPremium 使用 「 Azure 站台復原的儲存體

針對執行時需要大量 I/O 之工作負載的虛擬機器 (VM)，[Azure 進階儲存體](storage-premium-storage.md)可提供高效能、低延遲的磁碟支援。 本指南 hello 用途是 toohelp 使用者可以使用標準儲存體帳戶 tooa 進階儲存體帳戶從移轉的 VM 磁碟[Azure Site Recovery](../site-recovery/site-recovery-overview.md)。

站台復原是一項 Azure 服務可提供 tooyour 業務續航力和災害復原策略可藉由協調 hello 複寫在內部部署實體伺服器和 Vm toohello 雲端 (Azure) 或 tooa 次要資料中心。 當您的主要位置發生中斷時，您容錯移轉 toohello 次要位置 tookeep 應用程式和可用的工作負載。 當它傳回 toonormal 作業，您就會容錯回復 tooyour 主要位置。 站台復原提供測試容錯移轉 toosupport 災害復原演練而不會影響實際執行環境。 在發生未預期的災害時，您可以執行容錯移轉，讓資料損失量降到最低 (取決於複寫頻率)。 Hello 案例中，移轉 tooPremium 儲存體，您可以使用 hello [Site Recovery 中的容錯移轉](../site-recovery/site-recovery-failover.md)Azure Site Recovery toomigrate 目標磁碟 tooa 進階儲存體帳戶中。

我們建議您移轉 tooPremium 儲存體使用站台復原，因為此選項提供最少停機時間，並可避免複製磁碟，並建立新的 Vm hello 手動執行。 在容錯移轉期間，Site Recovery 會有系統地複製您的磁碟並建立新的 VM。 Site Recovery 支援數種類型的容錯移轉，且停機時間最短或甚至不用停機。 tooplan 停機時間並估計資料遺失，請參閱 hello[容錯移轉的類型](../site-recovery/site-recovery-failover.md)Site Recovery 中的資料表。 如果您[準備 tooconnect tooAzure Vm 容錯移轉之後](../site-recovery/site-recovery-vmware-to-azure.md)，您應該能夠 tooconnect toohello Azure VM 容錯移轉之後使用 RDP。

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery 元件

這些是相關 toothis 移轉案例的 hello 站台復原元件。

* **組態伺服器**是協調通訊以及管理資料複寫與復原程序的 Azure VM。 您將此 VM 上執行的單一安裝程式檔案 tooinstall hello 組態伺服器和其他元件，呼叫處理序伺服器，做為複寫閘道。 請參閱[組態伺服器必要條件](../site-recovery/site-recovery-vmware-to-azure.md)。 設定伺服器只需要設定一次 toobe 與可以用於所有移轉 toohello 相同的區域。

* **處理序伺服器**是接收複寫資料從來源 Vm 複寫閘道最佳化 hello 資料快取、 壓縮和加密，並將它傳送 tooa 儲存體帳戶。 也會處理推入安裝的 hello 行動服務 toosource Vm，並執行自動探索的來源 Vm。 hello 組態伺服器上已安裝 hello 預設處理序伺服器。 您可以將其他獨立處理序伺服器 tooscale 部署您的部署。 請參閱[處理序伺服器部署的最佳作法](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/)和[部署額外的處理序伺服器](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers)。 處理序伺服器只需要設定一次 toobe 和可用於所有移轉 toohello 相同的區域。

* **行動服務**是部署的元件要在每個標準 VM tooreplicate。 它會擷取資料寫入在 hello 標準的 VM，並將它們轉送 toohello 處理序伺服器。 請參閱[複寫之機器的必要條件](../site-recovery/site-recovery-vmware-to-azure.md)。

此圖顯示這些元件如何互動。

![][15]

> [!NOTE]
> 站台復原不支援儲存空間磁碟 hello 的移轉。

如需其他案例的其他元件，請參閱太[案例架構](../site-recovery/site-recovery-vmware-to-azure.md)。

## <a name="azure-essentials"></a>Azure 基本元件

這些是 hello Azure 針對這個移轉案例的需求。

* Azure 訂用帳戶
* Azure 高階儲存體帳戶 toostore 複寫的資料
* 在建立時即在容錯移轉，將會連接 Azure 虛擬網路 (VNet) toowhich Vm。 hello Azure VNet 必須在 hello 相同的區域，因為其中一個站台復原執行中的 hello hello
* 哪些 toostore 複寫記錄檔中標準 Azure 儲存體帳戶。 這可能是因為 hello VM 磁碟移轉 hello 相同儲存體帳戶

## <a name="prerequisites"></a>必要條件

* 了解 hello 前面一節中的 hello 相關的移轉案例元件
* 學習，以將停機時間規劃有關 hello [Site Recovery 中的容錯移轉](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>設定和移轉步驟

區域之間，或在相同地區內，您可以使用站台復原 toomigrate Azure IaaS Vm。 hello 下列指示有已為量身訂做這個 hello 文章中的移轉案例[複寫 VMware Vm 或實體伺服器 tooAzure](../site-recovery/site-recovery-vmware-to-azure.md)。 請遵循下列文章中的其他 toohello 指示的詳細步驟的 hello 連結。

1. **建立復原服務保存庫**。 建立及管理透過 hello hello Site Recovery 保存庫[Azure 入口網站](https://portal.azure.com)。 按一下 [新增] > [管理] > [備份] 和 [Site Recovery (OMS)]。 或者，您也可以按一下 [瀏覽]  >  [復原服務保存庫]  >  [加入]。 Vm 將會是您在此步驟中指定的複寫的 toohello 區域。 Hello 中移轉的 hello 目的相同區域中，選取 hello 地區來源 Vm 和來源儲存體帳戶。 請注意，移轉 tooPremium 儲存體帳戶只支援在 hello [Azure 入口網站](https://portal.azure.com)，不 hello[傳統入口網站](https://manage.windowsazure.com)。

2. hello 下列步驟幫助您**選擇您的保護目標**。

    2a. 開啟 hello 想 tooinstall hello 組態伺服器的 VM，hello [Azure 入口網站](https://portal.azure.com)。 跳過**復原服務保存庫** > **設定**。 在 [設定] 下，選取 [Site Recovery]。 在 [Site Recovery] 下，選取 [步驟 1︰準備基礎結構]。 在 [準備基礎結構] 下，選取 [保護目標]。

    ![][2]

    2b. 在下**保護目標**，在 hello 第一個下拉式清單中選取**tooAzure**。 Hello 第二個下拉式清單中，選取**未虛擬化 / 其他**，然後按一下**確定**。

    ![][3]

3. hello 下列步驟幫助您**設定 hello 來源環境 （組態伺服器）**。

    3a. 下載 hello **Azure Site Recovery 整合安裝**和 hello**保存庫註冊金鑰**所移 toohello**準備基礎結構** >  **準備來源** > **新增伺服器**刀鋒視窗。 您將需要 hello 保存庫註冊金鑰 toorun hello 整合設定。 hello 金鑰有效期為 5 天之後產生它。

    ![][4]

    3b. 加入組態伺服器中 hello**新增伺服器**刀鋒視窗。

    ![][5]

    3c. Hello 您當成 hello 設定伺服器使用的 VM，在執行整合安裝 tooinstall hello 組態伺服器和 hello 處理序伺服器。 您可以逐步完成 hello 螢幕擷取畫面[這裡](../site-recovery/site-recovery-vmware-to-azure.md)toocomplete hello 安裝。 您可以參考 toohello 下列螢幕擷取畫面如指定此移轉案例的步驟。

    在**開始之前**，選取**hello 組態伺服器與處理序伺服器安裝**。

    ![][6]

    3d. 在**註冊**，瀏覽並選取您下載 hello 保存庫中的 hello 註冊金鑰。

    ![][7]

    3e. 在**環境詳細資料**，選取是否要 tooreplicate VMware Vm。 針對這個移轉案例，請選擇 [否]。

    ![][8]

    3f. Hello 安裝已完成之後，您會看到 hello **Microsoft Azure 站台復原設定伺服器**視窗。 使用 hello**管理帳戶**toocreate hello 帳戶，可以使用自動探索的站台復原 索引標籤。 （在保護實體機器的相關 hello 案例中，設定 hello 帳戶無關，但是您必須至少一個帳戶 tooenable 其中一個步驟的 hello。 在此情況下，您可以命名 hello 帳戶和密碼做為任何。）使用 hello**保存庫註冊** 索引標籤 tooupload hello 保存庫認證檔案。

    ![][9]

4. **設定 hello 目標環境**。 按一下**準備基礎結構** > **目標**，並指定您想要 toouse Vm 容錯移轉之後的 hello 部署模型。 視您的案例而定，您可以選擇 [傳統] 或 [Resource Manager]。

    ![][10]

    Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。 請注意，如果您使用進階儲存體帳戶複寫資料，您需要 tooset 額外標準儲存體帳戶 toostore 複寫記錄檔。

5. **設定複寫設定**。 請遵循[設定複寫設定](../site-recovery/site-recovery-vmware-to-azure.md)組態伺服器已成功地與您所建立的 hello 複寫原則相關聯的 tooverify。

6. **容量規劃**。 使用 hello[容量規劃](../site-recovery/site-recovery-capacity-planner.md)tooaccurately 估計網路頻寬、 儲存和其他需求 toomeet 您複寫需求。 當您完成時，在 [是否已完成容量規劃?] 中選取 [是]。

    ![][11]

7. hello 下列步驟幫助您**安裝行動服務和啟用複寫**。

    7a. 您可以選擇在太[推入安裝](../site-recovery/site-recovery-vmware-to-azure.md)tooyour 來源 Vm 或太[手動安裝行動服務](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md)您來源 Vm 上。 您可以提供 hello 連結中找到的推送安裝的 hello 需求和 hello hello 手動安裝程式路徑。 如果您要手動安裝，您可能需要 toouse 內部 IP 位址 toofind hello 組態伺服器。

    ![][12]

    hello 容錯 VM 都有兩個暫存磁碟： 來自 hello 主要 VM 和 hello 其他的 VM hello 復原區域中的 hello 佈建期間建立。 tooexclude hello 暫存磁碟複寫，才能安裝 hello 行動服務，才能啟用複寫。 toolearn 深入了解如何 tooexclude hello 暫存磁碟，請參閱太[從複寫排除磁碟](../site-recovery/site-recovery-vmware-to-azure.md)。

    7b. 立即啟用複寫，如下所示︰
      * 按一下 [複寫應用程式] > [來源]。 啟用複寫 hello 第一次之後，按一下 + 中的其他機器 hello 保存庫 tooenable 複寫，複寫。
      * 在步驟 1 中，設定來源做為您的處理序伺服器。
      * 在步驟 2 中，指定 hello 容錯移轉後的部署模型、 以高階儲存體帳戶 toomigrate、 標準儲存體帳戶 toosave 記錄檔和虛擬網路 toofail 至。
      * 在步驟 3 中，新增受保護的 Vm 的 IP 位址 (您可能需要內部的 IP 位址 toofind 它們)。
      * 在步驟 4 中，選取您先前在 hello 處理序伺服器設定的 hello 帳戶設定 hello 屬性。
      * 在步驟 5 中，選擇您先前建立的 hello 複寫原則設定的複寫設定。
      按一下 [確定] 並啟用複寫。

    > [!NOTE]
    > 當 Azure VM 已解除配置，並重新啟動時，則它會取得無法確保 hello 相同的 IP 位址。 如果受保護的 Azure Vm 變更 hello 組態伺服器/處理序伺服器或 hello hello IP 位址，在此案例中的 hello 複寫可能會無法正常運作。

    ![][13]

    在設計 Azure 儲存體環境時，建議您為可用性設定組中的每個 VM 使用不同的儲存體帳戶。 我們建議您遵循 hello hello 儲存層中的最佳做法太[用於每個可用性設定組中的多個儲存體帳戶](../virtual-machines/windows/manage-availability.md)。 分配給 VM 磁碟 toomultiple 儲存體帳戶可協助 tooimprove 存放裝置可用性和 hello I/O 分散 hello Azure 儲存體基礎結構。 如果您的 Vm 會置於可用性集合，而不是所有的 Vm 磁碟複寫到一個儲存體帳戶，我們強烈建議移轉多個 Vm 多次，以便在 hello Vm hello 相同可用性設定組不會共用單一儲存體帳戶。 使用 hello**啟用複寫**刀鋒視窗 tooset 向上一次一個，每個 VM 的目的地儲存體帳戶。 您可以選擇根據 tooyour 需要容錯移轉後的部署模型。 如果您選擇資源管理員 (RM) 做為容錯移轉後的部署模型時，您可以容錯移轉 RM VM tooan RM VM，或您可以容錯移轉傳統 VM tooan RM VM。

8. **執行測試容錯移轉**。 toocheck 是否複寫已完成，按一下您的站台復原，然後按一下**設定** > **複寫的項目**。 您會看到 hello 狀態和複寫程序的百分比。 初始複寫之後是完成、 執行測試容錯移轉 toovalidate 複寫的策略。 如需詳細的測試容錯移轉的詳細步驟，請參閱太[Site Recovery 中執行測試容錯移轉](../site-recovery/site-recovery-vmware-to-azure.md)。 您可以查看測試容錯移轉中的 hello 狀態**設定** > **作業** > **YOUR_FAILOVER_PLAN_NAME**。 在 hello 刀鋒視窗中，您會看到 hello 步驟成功/失敗結果的細分。 如果 hello 測試容錯移轉失敗的任何步驟，請按一下 hello 步驟 toocheck hello 錯誤訊息。 請確定您的 Vm 和複寫策略符合 hello 需求，才能執行容錯移轉。 讀取[Site Recovery 中的測試容錯移轉 tooAzure](../site-recovery/site-recovery-test-failover-to-azure.md)如需詳細資訊和指示的測試容錯移轉。

9. **執行容錯移轉**。 Hello 測試容錯移轉完成之後，執行容錯移轉 toomigrate 您磁碟 tooPremium 儲存體，並複寫 hello VM 執行個體。 請遵循詳細步驟中的 hello[執行容錯移轉](../site-recovery/site-recovery-failover.md#run-a-failover)。 請確定您選取**關閉 Vm 並同步處理 hello 最新的資料**toospecify 站台復原應該嘗試關閉受保護的 hello Vm tooshut 和同步處理 hello 資料，以便 hello hello 資料的最新版的容錯移轉。 如果您沒有選取此選項，或 hello 嘗試不成功 hello 容錯移轉將會從 hello hello VM 的最新可用復原點。 Site Recovery 將建立的 VM 執行個體，其類型為 hello 與相同或類似 tooa Premium 儲存體具功能的 VM。 您可以檢查 hello 效能和價格的各種不同的 VM 執行個體太移[Windows 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)或[Linux 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)。

## <a name="post-migration-steps"></a>移轉後步驟

1. **設定複寫的 Vm toohello 可用性設定組，如果適用**。 站台復原不支援移轉的 Vm，以及 hello 可用性設定組。 根據您的複寫 VM hello 部署，執行 hello 下列其中一種動作：
  * 使用 hello 傳統部署模型所建立的 vm： 新增 hello VM toohello 可用性設定組 hello Azure 入口網站中。 如需詳細步驟，請移太[加入現有的虛擬機器 tooan 可用性集](../virtual-machines/windows/classic/configure-availability.md#addmachine)。
  * Hello 資源管理員部署模型： 儲存您的 hello VM 的設定，然後刪除並重新建立 hello 可用性設定組中的 hello Vm。 因此，使用 toodo 的 hello 指令碼，在[設定 Azure 資源管理員虛擬機器可用性集](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4)。 請檢查此指令碼的 hello 限制，並規劃停機時間，才能執行 hello 指令碼。

2. **刪除舊 VM 和磁碟**。 然後再刪除這些問題，請確定 hello 高階磁碟是與來源磁碟和新的 Vm 執行相同做 hello 來源 Vm hello hello 一致。 在 hello 資源管理員 (RM) 部署模型中，刪除 hello VM 以及刪除 hello 磁碟從來源儲存體帳戶中 hello Azure 入口網站。 您可以在 hello 傳統部署模型中，刪除 hello VM 和 hello 傳統入口網站或 Azure 入口網站中的磁碟。 如果沒有在哪一個 hello 磁碟不會刪除即使刪除 hello VM 的問題，請參閱[疑難排解錯誤，當您刪除 Vhd](storage-resource-manager-cannot-delete-storage-account-container-vhd.md)。

3. **全新的 hello Azure Site Recovery 基礎結構**。 如果不再需要網站復原，您可以刪除複寫的項目、 hello 組態伺服器上與 hello 修復原則，並將刪除 hello Azure Site Recovery 保存庫在清除它的基礎結構。

## <a name="troubleshooting"></a>疑難排解

* [監視和疑難排解虛擬機器與實體伺服器的保護](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>後續步驟

請參閱下列資源來移轉虛擬機器的特定案例的 hello:

* [在儲存體帳戶之間移轉 Azure 虛擬機器](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [建立並上傳 Windows Server VHD tooAzure。](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [建立和上傳的虛擬硬碟包含 hello Linux 作業系統](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [從 Amazon AWS tooMicrosoft Azure 移轉的虛擬機器](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

另請參閱下列資源 toolearn 深入了解 Azure 儲存體和 Azure 虛擬機器的 hello:

* [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
