---
title: "使用 Azure Site Recovery 移轉到 Azure 進階儲存體 (非受控磁碟) | Microsoft Docs"
description: "使用 Site Recovery (非受控磁碟) 將您現有的虛擬機器移轉到 Azure 進階儲存體。"
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: fe9b5014d01e404919b53b8dc4812f357b1ca435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-premium-storage-using-azure-site-recovery-unmanaged-disks"></a>使用 Azure Site Recovery (非受控磁碟) 移轉到進階儲存體

針對執行時需要大量 I/O 之工作負載的虛擬機器 (VM)，[Azure 進階儲存體](storage-premium-storage.md)可提供高效能、低延遲的磁碟支援。 本指南的目的，是要協助使用者使用 [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) 將其 VM 磁碟從標準儲存體帳戶移轉到進階儲存體帳戶。

Site Recovery 是一項 Azure 服務，可藉由將內部部署實體伺服器和 VM 的複寫協調至雲端 (Azure) 或次要資料中心，協助您建立商務持續性和災害復原策略。 當您的主要位置發生故障時，您容錯移轉至次要位置，讓應用程式和工作負載保持可用。 當它恢復正常作業時，容錯回復至您的主要位置。 Site Recovery 可提供測試用容錯移轉，既能支援災害復原演練，又不會影響生產環境。 在發生未預期的災害時，您可以執行容錯移轉，讓資料損失量降到最低 (取決於複寫頻率)。 在移轉到進階儲存體的案例中，您可以使用 Azure Site Recovery 中的 [Site Recovery 中的容錯移轉](../../site-recovery/site-recovery-failover.md)，將目標磁碟移轉到進階儲存體帳戶。

我們的建議是使用 Site Recovery 來移轉到進階儲存體，因為此選項的停機時間最短，並且不用手動執行複製磁碟和建立新 VM 的作業。 在容錯移轉期間，Site Recovery 會有系統地複製您的磁碟並建立新的 VM。 Site Recovery 支援數種類型的容錯移轉，且停機時間最短或甚至不用停機。 若要規劃停機時間並預估資料損失情形，請參閱 Site Recovery 中的[容錯移轉的類型](../../site-recovery/site-recovery-failover.md)資料表。 如果您[準備在容錯移轉後連接到 Azure VM](../../site-recovery/vmware-walkthrough-overview.md)，您應該可以在容錯移轉後使用 RDP 連接到 Azure VM。

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery 元件

以下是與此移轉案例相關的 Site Recovery 元件。

* **組態伺服器**是協調通訊以及管理資料複寫與復原程序的 Azure VM。 在此 VM 上，您將執行單一安裝程式檔案，以安裝組態伺服器和其他元件 (稱為處理序伺服器) 來做為複寫閘道。 請參閱[組態伺服器必要條件](../../site-recovery/vmware-walkthrough-overview.md)。 組態伺服器只需設定一次，即可用於所有移轉到相同區域的作業。

* **處理序伺服器**是一個複寫閘道，其會從來源 VM 接收複寫資料，運用快取、壓縮和加密將此資料最佳化，然後傳送至儲存體帳戶。 它還會處理對來源 VM 進行的行動服務推送安裝作業，並執行來源 VM 的自動探索。 組態伺服器上會安裝預設的處理序伺服器。 您可以部署額外的獨立處理序伺服器來調整您的部署。 請參閱[處理序伺服器部署的最佳作法](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/)和[部署額外的處理序伺服器](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers)。 處理序伺服器只需設定一次，即可用於所有移轉到相同區域的作業。

* **行動服務**是部署在每個您想要複寫之標準 VM 上的元件。 它會擷取在標準 VM 上寫入的資料，並將它們轉送到處理序伺服器。 請參閱[複寫之機器的必要條件](../../site-recovery/vmware-walkthrough-overview.md)。

此圖顯示這些元件如何互動。

![][15]

> [!NOTE]
> Site Recovery 不支援儲存空間磁碟的移轉。

如需適用於其他案例的其他元件，請參閱[案例架構](../../site-recovery/vmware-walkthrough-overview.md)。

## <a name="azure-essentials"></a>Azure 基本元件

以下是適用於此移轉案例的 Azure 需求。

* Azure 訂用帳戶
* 用來儲存所複寫資料的 Azure 進階儲存體帳戶
* 在容錯移轉時建立 VM 時，VM 將連接的 Azure 虛擬網路 (VNet)。 Azure VNet 必須位於與 Site Recovery 執行所在相同的區域中
* 用來儲存複寫記錄的 Azure 標準儲存體帳戶。 這可以是和所要移轉之 VM 磁碟相同的儲存體帳戶

## <a name="prerequisites"></a>必要條件

* 了解上一節的相關移轉案例元件
* 了解 [Site Recovery 中的容錯移轉](../../site-recovery/site-recovery-failover.md)中的容錯移轉，以規劃停機時間

## <a name="setup-and-migration-steps"></a>設定和移轉步驟

您可以使用 Site Recovery 在區域間或相同區域內移轉 Azure IaaS VM。 下列指示專用於[將 VMware VM 或實體伺服器複寫至 Azure](../../site-recovery/vmware-walkthrough-overview.md) 一文中的移轉案例。 除了這篇文章中的指示外，請遵循連結以取得詳細步驟。

1. **建立復原服務保存庫**。 透過 [Azure 入口網站](https://portal.azure.com)建立及管理 Site Recovery 保存庫。 按一下 [新增] > [管理] > [備份] 和 [Site Recovery (OMS)]。 或者，您也可以按一下 [瀏覽]  >  [復原服務保存庫]  >  [加入]。 VM 將會複寫至您在此步驟中指定的區域。 若要在相同區域中移轉，請選取來源 VM 和來源儲存體帳戶所在的區域。 

2. 下列步驟可協助您**選擇您的保護目標**。

    2a. 在您要安裝組態伺服器的 VM 上，開啟 [Azure 入口網站](https://portal.azure.com)。 移至 [復原服務保存庫] > [設定]。 在 [設定] 下，選取 [Site Recovery]。 在 [Site Recovery] 下，選取 [步驟 1︰準備基礎結構]。 在 [準備基礎結構] 下，選取 [保護目標]。

    ![][2]

    2b. 在 [保護目標] 底下的第一個下拉式清單中，選取 [至 Azure]。 在第二個下拉式清單中，選取 [未虛擬化/其他]，然後按一下 [確定]。

    ![][3]

3. 下列步驟可協助您**設定來源環境 (組態伺服器)**。

    3a. 下載 **Azure Site Recovery 整合安裝**和**保存庫註冊金鑰**，方法是前往 [準備基礎結構] > [準備來源] > [新增伺服器] 刀鋒視窗。 必須有保存庫註冊金鑰才能執行整合安裝。 該金鑰在產生後會維持 5 天有效。

    ![][4]

    3b. 在 [新增伺服器] 刀鋒視窗中新增組態伺服器。

    ![][5]

    3c. 在您用來作為組態伺服器的 VM 上，執行統一安裝以安裝組態伺服器和處理序伺服器。 您可以按照[這裡](../../site-recovery/vmware-walkthrough-overview.md)的螢幕擷取畫面逐步進行，以完成安裝。 您可以參考下列螢幕擷取畫面，來了解此移轉案例的指定步驟。

    在 [開始之前] 選取 [安裝組態伺服器和處理序伺服器]。

    ![][6]

    3d. 在 [註冊] 中，瀏覽並選取您從保存庫下載的註冊金鑰。

    ![][7]

    3e. 在 [環境詳細資料] 中，選取您是否要複寫 VMware VM。 針對這個移轉案例，請選擇 [否]。

    ![][8]

    3f. 安裝完成後，您會看到 [Microsoft Azure Site Recovery 組態伺服器] 視窗。 使用 [管理帳戶] 索引標籤來建立可供 Site Recovery 用於自動探索的帳戶  (在有關保護實體機器的案例中，設定帳戶並非我們的討論範圍，但您至少需要一個帳戶才能啟用下列其中一個步驟。 在此案例中，您可以任意命名帳戶和密碼)。使用 [保存庫註冊] 索引標籤上傳保存庫認證檔。

    ![][9]

4. **設定目標環境**。 按一下 [準備基礎結構] > [目標]，然後指定您要在容錯移轉後用於 VM 的部署模型。 視您的案例而定，您可以選擇 [傳統] 或 [Resource Manager]。

    ![][10]

    Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。 請注意，如果您使用進階儲存體帳戶來存放複寫的資料，則必須設定其他標準儲存體帳戶來儲存複寫記錄。

5. **設定複寫設定**。 請遵循[設定複寫設定](../../site-recovery/vmware-walkthrough-overview.md)，確認組態伺服器已順利與您所建立的複寫原則相關聯。

6. **容量規劃**。 使用 [Capacity Planner](../../site-recovery/site-recovery-capacity-planner.md) 準確地估計網路頻寬、儲存體和其他需求，以符合複寫的需求。 當您完成時，在 [是否已完成容量規劃?] 中選取 [是]。

    ![][11]

7. 下列步驟可協助您**安裝行動服務並啟用複寫**。

    7a. 您可以選擇[推送安裝](../../site-recovery/vmware-walkthrough-overview.md)到來源 VM，或在來源 VM 上[手動安裝行動服務](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md)。 您可以在提供的連結中找到推送安裝的需求和手動安裝程式的路徑。 如果您要手動安裝，您可能需要使用內部 IP 位址來找到組態伺服器。

    ![][12]

    容錯移轉的 VM 會有兩個暫存磁碟︰一個來自主要 VM，另一個則是在 VM 於復原區域中佈建期間所建立。 若要在複寫前排除暫存磁碟，請先安裝行動服務再啟用複寫。 若要深入了解如何排除暫存磁碟，請參閱[從複寫排除磁碟](../../site-recovery/vmware-walkthrough-overview.md)。

    7b. 立即啟用複寫，如下所示︰
      * 按一下 [複寫應用程式] > [來源]。 第一次啟用複寫之後，請按一下保存庫中的 [+複寫]，以對其他機器啟用複寫。
      * 在步驟 1 中，設定來源做為您的處理序伺服器。
      * 在步驟 2 中，指定容錯移轉後部署模型、要移轉到的進階儲存體帳戶、要用來儲存記錄的標準儲存體帳戶，以及要容錯移轉到的虛擬網路。
      * 在步驟 3 中，依 IP 位址新增受保護的 VM (您可能需要內部 IP 位址才能找到這些 VM)。
      * 在步驟 4 中，選取您先前在處理序伺服器上設定的帳戶來設定屬性。
      * 在步驟 5 中，選擇您先前建立的複寫原則來設定複寫設定。
      按一下 [確定] 並啟用複寫。

    > [!NOTE]
    > Azure VM 在取消配置後再重新啟動時，不一定會取得相同的 IP 位址。 如果組態伺服器/處理序伺服器或受保護 Azure VM 的 IP 位址變更，此案例中的複寫作業可能不會正確運作。

    ![][13]

    在設計 Azure 儲存體環境時，建議您為可用性設定組中的每個 VM 使用不同的儲存體帳戶。 我們建議您遵循儲存體層中的最佳做法，[針對每個可用性設定組使用多個儲存體帳戶](../../virtual-machines/windows/manage-availability.md)。 將 VM 磁碟分散到多個儲存體帳戶有助於增進儲存體可用性，並將 I/O 分散到整 Azure 儲存體基礎結構。 如果您的 VM 位於可用性設定組，而非將所有 VM 的磁碟複寫到單一儲存體帳戶，強烈建議您將多個 VM 分數次移轉，讓相同可用性設定組中的 VM 不至於共用單一儲存體帳戶。 使用 [啟用複寫] 刀鋒視窗，來設定每個 VM 的目的地儲存體帳戶，一次一個。 您可以根據需求來選擇容錯移轉後部署模型。 如果您選擇 Resource Manager (RM) 做為容錯移轉後部署模型，您可以將 RM VM 容錯移轉到 RM VM，或者將傳統 VM 容錯移轉到 RM VM。

8. **執行測試容錯移轉**。 若要檢查複寫是否已完成，請按一下 [Site Recovery]，然後按一下 [設定] > [複寫的項目]。 您將會看到複寫程序的狀態和百分比。 在初始複寫完成之後，請執行測試容錯移轉來驗證複寫策略。 如需測試容錯移轉的詳細步驟，請參閱[在 Site Recovery 中執行測試容錯移轉](../../site-recovery/vmware-walkthrough-overview.md)。 您可以在 [設定] > [作業] > [YOUR_FAILOVER_PLAN_NAME] 中看到測試容錯移轉的狀態。 在刀鋒視窗上，您會看到分解步驟和成功/失敗的結果。 如果測試容錯移轉在任一步驟失敗，請按一下該步驟來檢查錯誤訊息。 請確定 VM 和複寫策略符合需求後再執行容錯移轉。 如需測試容錯移轉的詳細資訊和指示，請參閱[在 Site Recovery 中測試容錯移轉到 Azure](../../site-recovery/site-recovery-test-failover-to-azure.md)。

9. **執行容錯移轉**。 在測試容錯移轉完成之後，請執行容錯移轉，將磁碟移轉到進階儲存體，並複寫 VM 執行個體。 請依照[執行容錯移轉](../../site-recovery/site-recovery-failover.md#run-a-failover)中的詳細步驟來執行。 請務必選取 [關閉 VM 並同步處理最新資料]，來指定 Site Recovery 應嘗試關閉受保護的 VM 並同步處理資料，以便為最新的資料版本進行容錯移轉。 如果您未選取此選項或嘗試失敗，容錯移轉將會來自 VM 的最新可用復原點。 Site Recovery 會建立類型與可支援進階儲存體之 VM 相同或類似的 VM 執行個體。 您可以前往 [Windows 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)或 [Linux 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)來查看各種 VM 執行個體的效能和價格。

## <a name="post-migration-steps"></a>移轉後步驟

1. **在情況允許時將複寫的 VM 設定至可用性設定組**。 Site Recovery 不支援移轉 VM 以及可用性設定組。 根據複寫 VM 的部署，執行下列其中一項︰
  * 使用傳統部署模型所建立的 VM︰在 Azure 入口網站中將 VM 新增至可用性設定組。 如需詳細步驟，請移至[將現有虛擬機器加入至可用性設定組](../../virtual-machines/windows/classic/configure-availability.md#addmachine)。
  * Resource Manager 部署模型︰儲存 VM 的組態，然後在可用性設定組中刪除再重新建立 VM。 若要這樣做，請使用[設定 Azure Resource Manager VM 可用性設定組](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4)中的指令碼。 在執行這個指令碼之前，請先查看指令碼的限制並規劃停機時間。

2. **刪除舊 VM 和磁碟**。 在刪除這些項目之前，請確定進階磁碟與來源磁碟一致，而且新的 VM 執行的是與來源 VM 相同的函式。 在 Resource Manager (RM) 部署模型中，於 Azure 入口網站中從來源儲存體帳戶刪除 VM 和磁碟。 在傳統部署模型中，您可以於傳統入口網站或 Azure 入口網站中刪除 VM 和磁碟。 如果有即使已刪除 VM，其中的磁碟卻未刪除的問題，請參閱[針對刪除 VHD 時的錯誤進行疑難排解](storage-resource-manager-cannot-delete-storage-account-container-vhd.md)。

3. **清除 Azure Site Recovery 基礎結構**。 如果不再需要 Site Recovery，您可以藉由刪除複寫的項目、組態伺服器、復原原則和 Azure Site Recovery 保存庫來清理其基礎結構。

## <a name="troubleshooting"></a>疑難排解

* [監視和疑難排解虛擬機器與實體伺服器的保護](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>後續步驟

如需移轉虛擬機器的特定案例，請參閱下列資源：

* [在儲存體帳戶之間移轉 Azure 虛擬機器](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [建立並上傳 Windows Server VHD 到 Azure。](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [建立及上傳包含 Linux 作業系統的虛擬硬碟](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [將虛擬機器從 Amazon AWS 移轉至 Microsoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

若要深入了解 Azure 儲存體和 Azure 虛擬機器，也請參閱下列資源：

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
