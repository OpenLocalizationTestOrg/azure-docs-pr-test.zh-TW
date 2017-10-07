---
title: "aaaReplicate VMware Vm 和實體伺服器 tooAzure （傳統舊版） |Microsoft 文件"
description: "描述如何 tooreplicate 內部部署 Vm 和 Windows/Linux 實體伺服器 tooAzure hello 傳統入口網站中的舊版部署中使用 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>將 VMware 虛擬機器和實體伺服器 tooAzure 複寫與 Azure Site Recovery 使用 hello 傳統入口網站 （舊版）
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmware-to-azure.md)
> * [傳統入口網站](site-recovery-vmware-to-azure-classic.md)
> * [傳統入口網站 (舊版)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

歡迎使用 tooAzure Site Recovery ！ 本文說明複寫在內部部署 VMware 虛擬機器或 Windows/Linux 實體伺服器 tooAzure hello 傳統入口網站中使用 Azure Site Recovery 的舊版部署。

## <a name="overview"></a>概觀
組織需要 BCDR 策略，以決定如何應用程式、 工作負載和資料維持執行且可用在計劃性與非計劃性停機時間，並且儘速復原 toonormal 工作條件。 BCDR 策略應保護商務資料安全且可復原，並確保發生災害時工作負載仍持續可用。

站台復原是一項 Azure 服務可由協調複寫在內部部署實體伺服器和虛擬機器 toohello 雲端 (Azure) 或 tooa 次要資料中心提供 tooyour BCDR 策略。 當您的主要位置發生中斷時，您容錯移轉 toohello 次要位置 tookeep 應用程式和可用的工作負載。 當它傳回 toonormal 作業，您就會容錯回復 tooyour 主要位置。 如需深入了解，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)

> [!WARNING]
> 本文包含 **舊版指示**。 請勿用於新的部署。 相反地，[遵循這些指示](site-recovery-vmware-to-azure.md)hello Azure 入口網站中的站台復原 toodeploy 或[使用這些指示](site-recovery-vmware-to-azure-classic.md)tooconfigure hello 增強 hello 傳統入口網站中的部署。 如果您已部署了使用這份文件中所述的 hello 方法，我們建議您移轉 toohello 增強 hello 傳統入口網站中的部署。
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>增強的 toohello 部署移轉
本節僅與相關，如果您已部署了使用本文章中的 hello 指示的站台復原。

toomigrate 您現有的部署，您將需要：

1. 在內部部署網站部署新的 Site Recovery 元件。
2. Hello 新的組態伺服器上設定的 VMware Vm 的自動探索的認證。
3. 探索新組態伺服器 hello hello VMware server。
4. 建立新的保護群組使用新組態伺服器 hello。

開始之前：

* 建議您設計維護時段進行移轉。
* hello**移轉機器**選項才會提供您有舊版部署期間所建立的現有保護群組。
* Hello 移轉步驟完成之後可能需要 15 分鐘或更長 toorefresh hello 認證和 toodiscover 和重新整理虛擬機器，以便新增 tooa 保護群組。 您可以手動重新整理而不用等待。

移轉如下所示：

1. 閱讀有關[增強 hello 傳統入口網站中的部署](site-recovery-vmware-to-azure-classic.md)。 檢閱 hello 增強[架構](site-recovery-vmware-to-azure-classic.md)，和[必要條件](site-recovery-vmware-to-azure-classic.md)。
2. 解除安裝您要複寫的機器 hello 行動服務。 加入 toohello 新的保護群組時，將 hello 機器上安裝新版 hello 服務。
3. 下載[保存庫註冊金鑰](site-recovery-vmware-to-azure-classic.md)和[執行 hello 統一的安裝精靈](site-recovery-vmware-to-azure-classic.md)tooinstall hello 組態伺服器、 處理序伺服器和主要目標伺服器元件。 深入了解 [容量規劃](site-recovery-vmware-to-azure-classic.md)。
4. [設定認證](site-recovery-vmware-to-azure-classic.md)此站台復原可以使用 tooaccess VMware server tooautomatically 探索 VMware Vm。 閱讀 [需要的權限](site-recovery-vmware-to-azure-classic.md)的相關資訊。
5. 加入 [vCenter 伺服器或 vSphere 主機](site-recovery-vmware-to-azure-classic.md)。 可能需要 15 分鐘，多個伺服器 tooappear hello Site Recovery 入口網站。
6. 建立 [新的保護群組](site-recovery-vmware-to-azure-classic.md)。 就可以在 hello 入口 toorefresh too15 分鐘 hello 虛擬機器探索到，而顯示。 如果您不想 toowait 您可以反白顯示 hello 管理伺服器名稱 （但不要按） >**重新整理**。
7. Hello 新的保護群組下的 **移轉機器**。

    ![新增帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. 在**選取機器**toomigrate，並將這些 hello 想 toomigrate 機器選取 hello 保護群組。

    ![新增帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. 在**設定目標設定**指定是否要讓 toouse hello 相同設定的所有機器，選取 hello 處理序伺服器和 Azure 儲存體帳戶。 如果您沒有個別處理序伺服器，這會是 hello hello hello 設定伺服器的伺服器的 IP 位址。

    ![新增帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [移轉儲存體帳戶](../resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶，或跨訂用帳戶不支援用來部署站台復原的儲存體帳戶。

1. 在**指定帳戶**，選取您建立的 hello 處理序伺服器 tooaccess hello 機器 toopush hello 新版 hello 行動服務的 hello 帳戶。

   ![新增帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. 站台復原將會移轉您提供您的複寫的資料 toohello Azure 儲存體帳戶。 （選擇性） 您可以重複使用您用於 hello 舊版部署的 hello 儲存體帳戶。
3. Hello 工作之後完成虛擬機器將會自動同步處理。 同步處理完成之後，您可以從 hello 舊版保護群組刪除 hello 虛擬機器。
4. 所有機器都移轉之後，您可以刪除 hello 舊版保護群組。
5. 記住 toospecify hello 容錯移轉內容的機器，並同步處理完成後 hello Azure 網路設定。
6. 如果您有現有的復原計劃，您可以移轉這些 toohello 增強部署以 hello**移轉復原計劃**選項。 您應該只在已經移轉所有受保護的機器之後執行這項操作。

   ![新增帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> 完成移轉之後繼續 hello[增強的文章](site-recovery-vmware-to-azure-classic.md)。 hello 本文其餘部分舊版將不再相關，而且您無須 toofollow 任何多個 hello it * * 中所述的步驟。
>
>

## <a name="what-do-i-need"></a>我需要什麼？
這個圖表可顯示 hello 部署元件。

![新增保存庫](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

以下是您需要的內容：

| **元件** | **部署** | **詳細資料** |
| --- | --- | --- |
| **組態伺服器** |在 hello Azure 標準 A3 虛擬機器相同站台復原訂用帳戶。 |hello 組態伺服器協調受保護的機器，hello 處理序伺服器，與 Azure 中的主要目標伺服器之間的通訊。 它會在容錯移轉發生時在 Azure 中設定複寫並協調復原。 |
| **主要目標伺服器** |Azure 虛擬機器 — 根據 Windows Server 2012 R2 資源庫映像 （tooprotect Windows 電腦） 或做為 Linux 伺服器的其中一個 Windows server 基礎 OpenLogic CentOS 6.6 資源庫映像 （tooprotect Linux 機器）。<br/><br/> 有三種大小選項可供使用 - 標準 A4、標準 D14 和標準 DS4。<br/><br/> hello 伺服器是連線的 toohello hello 組態伺服器相同的 Azure 網路。<br/><br/> 在 hello Site Recovery 入口網站中設定 |它會使用在您 Azure 儲存體帳戶中 Blob 儲存體上建立之連結的 VHD，從您的受保護機器接收和保留複寫的資料。<br/><br/> 特別針對設定工作負載的保護選取標準 DS4，該工作負載需要使用進階儲存體帳戶的一致高效能和低延遲。 |
| **處理序伺服器** |執行 Windows Server 2012 R2 的內部部署虛擬或實體伺服器<br/><br/> 建議將它放在 hello 相同網路和區域網路區段，做為 hello 機器，您想要 tooprotect，但它可以在不同的網路上執行，只要受保護的機器 L3 網路 tooit 可見性。<br/><br/> 您將進行設定，並在 hello Site Recovery 入口網站 toohello 組態伺服器註冊它。 |受保護的機器傳送複寫資料 toohello 內部處理序伺服器。 它已收到以磁碟為基礎的快取 toocache 複寫資料。 它會對該資料執行一些動作。<br/><br/> 最佳化和快取、 壓縮、 加密，再將它傳送 toohello 主要目標伺服器上的資料。<br/><br/> 它會處理 hello 行動服務推入安裝。<br/><br/> 它會執行 VMware 虛擬機器的自動探索。 |
| **內部部署機器** |內部部署 VMware 虛擬機器，或執行 Windows 或 Linux 的實體伺服器。 |您設定要套用至一或多部機器的複寫設定。 您可以將容錯移轉個別機器，或者，更常見的是您聚集到復原方案的多部機器。 |
| **行動服務** |每個虛擬機器或實體伺服器上安裝您想 tooprotect<br/><br/> 可以手動安裝或推送和 hello 處理序伺服器的自動安裝，當您啟用機器的複寫。 |hello 行動服務 （重新同步處理） 的初始複寫期間，將傳送資料 toohello 處理序伺服器。 （重新同步處理完成時） 後，受保護的狀態處於 hello 機器之後 hello 行動服務會擷取寫入 toodisk 記憶體中，並將它們傳送 toohello 處理序伺服器。 Windows 伺服器的應用程式一致性是利用 VSS 來達成。 |
| **Azure Site Recovery 保存庫** |您 Azure 訂用帳戶中建立站台復原保存庫，和 hello 保存庫中註冊伺服器。 |hello 保存庫會協調並協調資料複寫、 容錯移轉，以及您在內部部署站台與 Azure 之間的復原。 |
| **複寫機制** |**透過網際網路 hello**— 從受保護的內部部署伺服器 tooAzure 透過使用 SSL/TLS 的安全通道的通訊和複寫資料 hello 網際網路。 這是 hello 預設選項。<br/><br/> **VPN/ExpressRoute** - 透過 VPN 連線，在內部部署伺服器與 Azure 之間進行通訊和資料複寫。 您將需要 tooset 站對站 VPN 或 ExpressRoute 連線在內部部署站台與 Azure 網路之間。<br/><br/> 您可以選取要如何 tooreplicate Site Recovery 部署期間。 設定而不會影響現有的機器的複寫功能之後，您無法變更 hello 機制。 |這兩個選項需要您 tooopen 受保護的電腦上任何傳入的網路連接埠。 從 hello 在內部部署站台起始的所有網路通訊。 |

## <a name="capacity-planning"></a>容量規劃
您將需要 tooconsider hello 的主要區域：

* **來源環境**— hello VMware 基礎結構、 來源機器的設定和需求。
* **元件伺服器**— hello 處理序伺服器、 設定伺服器和主要目標伺服器

### <a name="considerations-for-hello-source-environment"></a>Hello 來源環境的考量
* **最大磁碟大小**— hello 目前的大小上限可以附加的 tooa 虛擬機器的 hello 磁碟是 1 TB。 因此 hello 可複寫的來源磁碟的大小上限也是有限的 too1 TB。
* **每個來源的最大大小**— hello 單一來源機器的大小上限是 31 TB （含 31 磁碟） 和佈建的 hello 主要目標伺服器 D14 執行個體。
* **每一主要目標伺服器的來源數目**—可以使用單一主要目標伺服器保護的多個來源機器。 不過，單一來源機器無法受到保護跨多個主要目標伺服器，因為當磁碟複寫，在 Azure blob 儲存體上建立，附加與資料磁碟 toohello 主要目標伺服器鏡射 hello hello 磁碟大小的 VHD。  
* **每個來源的最大每日變更率**— 有三個因素需要 toobe 視為時考慮 hello 建議變更每個來源的速率。 Hello 目標基礎考量 hello hello 來源上的每項作業的目標磁碟需要兩個 IOPS。 這是因為舊資料的讀取和寫入的 hello 新資料將會發生在 hello 目標磁碟。
  * **每日變更率 hello 處理序伺服器支援**— 在來源機器不能跨越多個處理序伺服器。 單一處理序伺服器可以支援註冊的每日變更率 too1 TB。 因此 1 TB，是 hello 最大的每日資料變更率來源機器的支援。
  * **Hello 目標磁碟所支援的最大輸送量**— 每個來源磁碟的最大值變換不能超過 144 GB/天 （含 8 千個寫入大小）。 請參閱 hello hello 輸送量和 IOPs 的各種寫入大小的 hello 目標的主要目標區段中的 hello 表格。 必須由兩個分割這個數字，因為每個來源 IOP 產生 2 的 hello 目標磁碟機的 IOPS。 閱讀有關[Azure 延展性和效能目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)設定進階儲存體帳戶的 hello 目標時。
  * **Hello 儲存體帳戶所支援的最大輸送量**— 來源不能跨越多個儲存體帳戶。 指定儲存體帳戶所花費的最多 20,000 每秒的要求和 IOP 每一個來源會產生 2 IOPS hello 主要目標伺服器上的，建議您保留 hello IOPS 數目跨 hello 來源 too10 000。 閱讀有關[Azure 延展性和效能目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)設定進階儲存體帳戶的 hello 來源時。

### <a name="considerations-for-component-servers"></a>元件伺服器的考量
表 1 摘要 hello hello 組態和主要目標伺服器的虛擬機器大小。

| **元件** | **部署的 Azure 執行個體** | **核心** | **記憶體** | **最大磁碟** | **磁碟大小** |
| --- | --- | --- | --- | --- | --- |
| 組態伺服器 |標準 A3 |4 |7 GB |8 |1023 GB |
| 主要目標伺服器 |標準 A4 |8 |14 GB |16 |1023 GB |
| 標準 D14 |16 |112 GB |32 |1023 GB | |
| 標準 DS4 |8 |28 GB |16 |1023 GB | |

**表 1**

#### <a name="process-server-considerations"></a>處理序伺服器考量
通常處理序伺服器的大小取決於每日變更率 hello 跨所有受保護的工作負載。

* 您需要足夠的計算 tooperform 工作，例如內嵌壓縮及加密。
* hello 處理序伺服器會使用磁碟型快取。 請確定 hello 建議快取空間，且磁碟輸送量可用 toofacilitate hello 資料變更儲存在網路瓶頸後或中斷 hello 事件。
* 確保足夠的頻寬，方便的 hello 處理序伺服器可以上傳 hello 資料 toohello 主要目標伺服器 tooprovide 連續資料保護。

表 2 提供摘要的 hello 處理序伺服器的指導方針。

| **資料變更率** | **CPU** | **記憶體** | **快取磁碟大小** | **快取磁碟輸送量** | **輸入/輸出頻寬** |
| --- | --- | --- | --- | --- | --- |
| < 300 GB |4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5GHz) |4 GB |600 GB |每秒的 7 too10 MB |30 Mbps/21 Mbps |
| 300 too600 GB |8 個 vCPU (2 個通訊端 * 四核心 @ 2.5GHz) |6 GB |600 GB |每秒 11 too15 MB |60 Mbps/42 Mbps |
| 600 GB too1 TB |12 個 vCPU (2 個通訊端 * 六核心 @ 2.5GHz) |8 GB |600 GB |每秒 16 too20 MB |100 Mbps/70 Mbps |
| > 1 TB |部署另一個處理序伺服器 | | | | |

**資料表 2**

其中：

* 輸入是下載頻寬 （hello 來源和處理序伺服器之間的內部網路）。
* 輸出是上傳的頻寬 （hello 處理序伺服器與主要目標伺服器之間的網際網路）。 輸出數目假設平均 30% 的處理序伺服器壓縮。
* 針對快取磁碟，建議所有的處理序伺服器的個別作業系統磁碟最少有 128 GB。
* 快取磁碟輸送量 hello 下列儲存體用於效能評定： 8 的 SAS 磁碟機的 10 K RPM 使用 RAID 10 設定。

#### <a name="configuration-server-considerations"></a>設定伺服器考量
3-4 磁碟區，每個組態伺服器可以支援註冊 too100 來源機器。 如果部署較大，建議您部署另一個組態伺服器。 Hello 組態伺服器 hello 預設虛擬機器的內容，請參閱 表 1。

#### <a name="master-target-server-and-storage-account-considerations"></a>主要目標伺服器與儲存體帳戶的考量
hello 儲存體的每個主要目標伺服器包含作業系統磁碟、 保留磁碟區和資料磁碟。 hello 保留磁碟機 hello hello hello Site Recovery 入口網站中定義的保留週期期間維護 hello 日誌的磁碟上的變更。  Hello 的 hello 主要目標伺服器的虛擬機器內容，請參閱 tooTable 1。 表 3 顯示 hello A4 磁碟的使用方式。

| **執行個體** | **作業系統磁碟** | **保留** | **資料磁碟** |
| --- | --- | --- | --- |
| **保留** |**資料磁碟** | | |
| 標準 A4 |1 個磁碟 (1 * 1023 GB) |1 個磁碟 (1 * 1023 GB) |15 個磁碟 (15 * 1023 GB) |
| 標準 D14 |1 個磁碟 (1 * 1023 GB) |1 個磁碟 (1 * 1023 GB) |31 個磁碟 (15 * 1023 GB) |
| 標準 DS4 |1 個磁碟 (1 * 1023 GB) |1 個磁碟 (1 * 1023 GB) |15 個磁碟 (15 * 1023 GB) |

**資料表 3**

容量規劃 hello 主要目標伺服器而定：

* Azure 儲存體效能和限制
  * hello 最大數目高過高標準層 vm 的磁碟，約 40 (每個磁碟 20000/500 IOPS) 的單一儲存體帳戶中。 請參閱[標準儲存體帳戶的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)和[進階儲存體帳戶的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)。
* 每日變更率
* 保留磁碟區儲存體。

請注意：

* 一個來源不能跨越多個儲存體帳戶。 這適用於 toohello 移 toohello 儲存體帳戶設定保護時，選取的資料磁碟。 hello OS 和 hello 保留磁碟通常會送 toohello 自動部署的儲存體帳戶。
* hello 保留存放磁碟區所需取決於每日變更率 hello 與 hello 的保留天數。 hello 保留每個主要目標伺服器所需的儲存體 = 每天來源變換總計 * 數字的保留天數。
* 每個主要目標伺服器只有一個保留磁碟區。 hello 保留磁碟區是跨 hello 磁碟附加的 toohello 主要目標伺服器共用。 例如：
  * 如果有 5 磁碟的來源機器，且每個磁碟會產生 hello 來源上的 120 IOPS （8 千個大小），這會轉譯每個磁碟 （2 作業的每個來源 IO hello 目標磁碟機） too240 IOPS。 240 IOPS 的 hello Azure 每個磁碟的 IOPS 限制為 500。
  * 在 hello 保留磁碟區，這會變成 120 * 5 = 600 IOPS，而這可能會變得常會形成瓶頸。 在此案例中，是不錯的策略會 tooadd 更多磁碟 toohello 保留磁碟區，跨越時，為 RAID 等量磁碟區設定。 這可以改善效能，因為 hello IOPS 分散於多個磁碟機。 所加入的磁碟機 toobe hello 許多 toohello 保留磁碟區會顯示如下：
    * 來自來源環境的 IOP 總計 / 500
    * 每日來自來源環境的變換總計 (未壓縮) / 287 GB。 287 GB 是 hello 目標磁碟每日所支援的最大輸送量。 此標準會隨著 hello 寫入大小以 8 K 的因數，所以在此情況下 8k 假設寫入大小的三個。 例如，如果 hello 寫入大小是 4k 輸送量將會是 287/2。 而且如果 hello 寫入大小為 16k 然後輸送量 287 * 2。
* hello 所需的儲存體帳戶數目 = 總來源 IOPs/10000。

## <a name="before-you-start"></a>開始之前
| **元件** | **需求** | **詳細資料** |
| --- | --- | --- |
| **Azure 帳戶** |您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 | |
| **Azure 儲存體** |您將需要 Azure 儲存體帳戶 toostore 複寫資料<br/><br/> 任一個 hello 帳戶應該是[標準異地備援儲存體帳戶](../storage/common/storage-redundancy.md#geo-redundant-storage)或[進階儲存體帳戶](../storage/common/storage-premium-storage.md)。<br/><br/> 它必須在 hello 與 hello Azure Site Recovery 服務相同的區域並與相關聯 hello 相同訂用帳戶。 我們不支援的儲存體帳戶使用 hello 建立 hello 移動[新版 Azure 入口網站](../storage/common/storage-create-storage-account.md)跨越資源群組。<br/><br/> 讀取 toolearn[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md) | |
| **Azure 虛擬網路** |您將需要哪些 hello 設定伺服器與主要目標伺服器將會部署在 Azure 虛擬網路。 Hello 中應該有相同的訂用帳戶和區域，所以 hello Azure Site Recovery 保存庫。 如果您想 tooreplicate 資料透過 ExpressRoute 或 VPN 連線 hello Azure 虛擬網路必須連接的 tooyour 在內部部署網路透過 ExpressRoute 連線或站對站 VPN。 | |
| **Azure 資源** |請確定您有足夠的 Azure 資源 toodeploy 所有元件。 如需深入了解，請參閱 [Azure 訂用帳戶限制](../azure-subscription-service-limits.md)。 | |
| **Azure 虛擬機器** |您想 tooprotect 虛擬機器都應該符合[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。<br/><br/> **磁碟計數**—一個受保護的伺服器最多可支援 31 個磁碟<br/><br/> **磁碟大小**—個別磁碟容量不可超過 1023 GB<br/><br/> **叢集**—不支援叢集伺服器<br/><br/> **開機**—不支援整合可延伸韌體介面 (UEFI)/可延伸韌體介面 (EFI) 開機<br/><br/> **磁碟區**—不支援 Bitlocker 加密的磁碟區<br/><br/> **伺服器名稱**—名稱應包含介於 1 到 63 個字元 (字母、數字和連字號)。 hello 名稱必須以字母或數字開頭，並以字母或數字結尾。 受保護電腦之後，您可以修改 hello Azure 的名稱。 | |
| **組態伺服器** |Azure 站台復原 Windows Server 2012 R2 資源庫映像為基礎的標準 A3 虛擬機器將建立在 hello 組態伺服器的訂用帳戶中。 它會建立為 hello 新的雲端服務中的第一個執行個體。 如果您選取公用網際網路，作為 hello hello 設定伺服器 hello 雲端服務的連線類型會建立使用保留公用 IP 位址。<br/><br/> hello 安裝路徑應該僅限英文字元。 | |
| **主要目標伺服器** |Azure 虛擬機器，標準 A4、D14 或 DS4。<br/><br/> hello 安裝路徑應該僅限英文字元。 例如 hello 路徑應該**/usr/local/ASR**執行 Linux 主要目標伺服器。 | |
| **處理序伺服器** |您可以部署 hello 實體或虛擬機器與 hello 最新的更新執行 Windows Server 2012 R2 上的處理序伺服器。 在 C:/ 上安裝。<br/><br/> 我們建議您將 hello 伺服器放在 hello 相同的網路和子網路為 hello 想 tooprotect 機器。<br/><br/> Hello 處理序伺服器上安裝 VMware vSphere CLI 5.5.0。 hello VMware vSphere CLI 元件被必要 hello 順序 toodiscover 虛擬機器管理的 vCenter server 或 ESXi 主機上執行的虛擬機器中的處理序伺服器上。<br/><br/> hello 安裝路徑應該僅限英文字元。<br/><br/> 不支援 ReFS 檔案系統。 | |
| **VMware** |VMware vCenter 伺服器，管理您的 VMware vSphere Hypervisor。 它應執行 5.1 或 5.5 vCenter 版本與 hello 最新的更新。<br/><br/> 包含 VMware 虛擬機器的一或多個 vSphere hypervisor tooprotect 您。 hello hypervisor 應執行 ESX/ESXi 5.1 或 5.5 版的 hello 最新的更新。<br/><br/> VMware 虛擬機器應該安裝 VMware 工具且在執行中。 | |
| **Windows 機器** |執行 Windows 的受保護實體伺服器或 VMware 虛擬機器有一些需求。<br/><br/> 支援的 64 位元作業系統：**Windows Server 2012 R2**、**Windows Server 2012** 或 **Windows Server 2008 R2 (至少為 SP1)**。<br/><br/> hello 主機名稱、 掛接點、 裝置名稱、 Windows 系統路徑 (例如： C:\Windows) 只應該是英文。<br/><br/> hello 作業系統應該安裝在 C:\ 磁碟機上。<br/><br/> 僅支援基本磁碟。 不支援動態磁碟。<br/><br/> 受保護的機器上的防火牆規則應該允許它們 tooreach hello 組態和主要目標伺服器中 Azure.p ><p>您將需要 tooprovide 系統管理員帳戶 （必須是 hello Windows 電腦上的本機系統管理員） toopush Windows 伺服器上安裝行動服務的 hello。 如果提供的 hello 帳戶是在非網域帳戶，您將需要 toodisable hello 本機電腦上的遠端使用者存取控制。 toodo 此新增 hello LocalAccountTokenFilterPolicy DWORD 登錄項目底下 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System 1 的值。 從 CLI tooadd hello 登錄項目開啟 cmd 或 powershell，並輸入 **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 。 [深入了解](https://msdn.microsoft.com/library/aa826699.aspx)存取控制。<br/><br/> 容錯移轉之後，如果您想要使用遠端桌面連線 tooWindows Azure 虛擬機器中確定 hello 在內部部署機器已啟用遠端桌面。 如果您不透過 VPN 連接，防火牆規則應該允許 hello 透過遠端桌面連線網際網路。 | |
| **Linux 機器** |支援 64 位元作業系統： **Centos 6.4，6.5、 6.6**;**Oracle Enterprise Linux 6.4，執行 hello Red Hat 相容核心或以企業核心的第 3 版 (UEK3) 6.5**， **SUSE Linux Enterprise Server 11 SP3**。<br/><br/> 受保護的機器上的防火牆規則應該允許它們 tooreach hello 組態和主要目標伺服器在 Azure 中。<br/><br/> 受保護的機器上的 /etc/hosts 檔案應包含所有 Nic 相關都聯的 hello 本機主機名稱 tooIP 位址對應的項目 <br/><br/> 如果您想 tooconnect tooan Azure 虛擬機器的 Linux 執行容錯移轉使用安全殼層用戶端 (ssh)，確保該 hello Secure Shell 服務上受保護的 hello 之後 toostart 在系統開機時自動設定機器，防火牆規則允許 ssh連接 tooit。<br/><br/> hello 主機名稱、 掛接點、 裝置名稱，以及 Linux 系統路徑和檔案名稱 （例如 /etc/hosts; libodbc） 應該是以英文只。<br/><br/> 可以在內部部署機器啟用保護，以下列儲存體的 hello:-<br>檔案系統：EXT3、ETX4、ReiserFS、XFS<br>多重路徑軟體裝置對應程式 (多重路徑)<br>磁碟區管理員：LVM2<br>不支援使用 HP CCISS 控制站儲存體的實體伺服器。 | |
| **第三方** |在此案例中的某些部署元件取決於協力廠商軟體 toofunction 正確。 如需完整清單，請參閱 [第三方廠商軟體注意事項和資訊](#third-party) | |

### <a name="network-connectivity"></a>網路連線
您有兩個選項，設定您的內部部署站台之間的網路連線時，hello Azure 基礎結構元件 （組態伺服器、 主要目標伺服器） 部署的 hello 的虛擬網路。 您將需要的 toodecide 之前您的網路連線選項 toouse 可以部署組態伺服器。 您將需要 toochoose 部署的 hello 次此設定。 稍後無法變更。

**網際網路：**通訊和複寫 hello 在內部部署伺服器 （處理序伺服器、 受保護的機器） 與 hello Azure 基礎結構元件伺服器 （伺服器組態，主要目標伺服器） 之間的資料會透過安全的 SSL /從內部部署 toohello 公用端點 hello 組態和主要目標伺服器上的 TLS 連線。 （hello 唯一的例外狀況是 hello hello 處理序伺服器與 hello TCP 連接埠 9080 此未加密的主要目標伺服器之間的連線。 只有控制資訊相關的此連接上交換 toohello 複寫通訊協定的複寫設定。）

![部署圖表網際網路](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**： 通訊和複寫 hello 在內部部署伺服器 （處理序伺服器、 受保護的機器） 與 hello Azure 基礎結構元件伺服器 （伺服器組態，主要目標伺服器） 之間的資料會透過 VPN 連線在內部部署網路之間 hello Azure 虛擬網路的 hello 組態伺服器和主要目標伺服器部署。 請確定您在內部部署網路連線的 toohello ExpressRoute 連線，或站對站 VPN 連線的 Azure 虛擬網路。

![部署圖表 VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>步驟 1：建立保存庫
1. 登入 toohello[管理入口網站](https://portal.azure.com)。
2. 展開 [資料服務]  >  [復原服務]，然後按一下 [Site Recovery 保存庫]。
3. 按一下 [新建]  >  [快速建立]。
4. 在**名稱**，輸入好記名稱 tooidentify hello 保存庫。
5. 在**區域**，選取 hello hello 保存庫的地理區域。 支援的 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)
6. 按一下 [建立保存庫] 。

    ![新增保存庫](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

請檢查已成功建立 hello 保存庫的 hello 狀態列 tooconfirm。 hello 保存庫會列為**Active**上主要的 hello**復原服務**頁面。

## <a name="step-2-deploy-a-configuration-server"></a>步驟 2：部署設定伺服器
### <a name="configure-server-settings"></a>設定伺服器設定
1. 在 [hello**復原服務**頁面上，按一下 hello 保存庫 tooopen hello 快速入門] 頁面。 也可以使用 [hello] 圖示，隨時開啟快速入門。

    ![快速啟動圖示](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. 在 hello 下拉式清單中，選取 **具有 VMware/實體伺服器和 Azure 部署在內部部署網站之間**。
3. 在 [準備目標 (Azure) 資源] 按一下 [部署組態伺服器]。

    ![部署設定伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. 在 [新的組態伺服器詳細資料]  中指定：

   * Hello 組態伺服器和認證 tooconnect tooit 名稱。
   * 在 hello 網路連線類型中，下拉式清單選取**公用網際網路**或**VPN**。 請注意，套用此設定後，就無法修改此設定。
   * 選取 hello Azure 網路的 hello 伺服器應該位於。 如果您使用 VPN，請確定 hello Azure 網路是連線的 tooyour 在內部部署網路如預期般。
   * 指定 hello 內部 IP 位址和子網路指派 toohello 伺服器。 請注意，hello 任何子網路中的前四個 IP 位址已保留給內部 Azure 的使用量。 使用任何其他可用的 IP 位址。

     ![部署設定伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. 當您按一下**確定**hello 組態伺服器的訂用帳戶中建立 Azure 站台復原 Windows Server 2012 R2 資源庫映像為基礎的標準 A3 虛擬機器。 它會建立為 hello 新的雲端服務中的第一個執行個體。 如果您選取 tooconnect 透過 hello 網際網路 hello 雲端服務會建立使用保留公用 IP 位址。 您可以監視正在 hello**作業** 索引標籤。

    ![監視進度](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. 如果您要連線透過 hello 網際網路，hello 組態伺服器之後已部署的附註 hello 公用 IP 位址指派 tooit 上 hello**虛擬機器**hello Azure 入口網站中的頁面。 然後在 [hello**端點**] 索引標籤注意 hello 公用 HTTPS 連接埠對應 tooprivate 連接埠 443。 您將需要這項資訊稍後您 hello 主要目標及處理伺服器 hello 組態伺服器註冊。 hello 組態伺服器部署使用這些端點：

   * HTTPS： 公用連接埠是使用的 toocoordinate 元件伺服器之間的通訊，並透過 Azure hello 網際網路。 私用連接埠 443 是使用的 toocoordinate 元件伺服器與 Azure 之間的通訊透過 VPN。
   * Custom： 公用連接埠來進行容錯回復工具通訊 hello 透過網際網路。 私人連接埠 9443 是用於透過 VPN 的容錯回復工具通訊。
   * PowerShell：私人連接埠 5986
   * 遠端桌面：私人連接埠 3389

   ![VM 端點](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > 不要刪除或變更任何組態伺服器部署期間建立的端點 hello 公用或私用連接埠號碼。
   >
   >

使用保留的 IP 位址自動建立的 Azure 雲端服務部署所在 hello 組態伺服器。 hello 保留的位址是 hello 組態伺服器雲端服務 IP 位址的所需的 tooensure 維持相同 hello 整個 hello 上的虛擬機器 （包括 hello 組態伺服器） hello 雲端服務的重新啟動。 hello 保留公用 IP 位址必須 toobe 手動未保留當 hello 組態伺服器已解除任務，或將會維持保留。 每一訂用帳戶預設的保留公用 IP 位址數目限制為 20 個。 [深入了解](../virtual-network/virtual-networks-reserved-private-ip.md) 保留的 IP 位址。

### <a name="register-hello-configuration-server-in-hello-vault"></a>Hello 保存庫中註冊伺服器 hello 組態
1. 在 hello**快速入門**頁面上，按一下**準備目標資源** > **下載註冊金鑰**。 會自動產生 hello 金鑰檔。 該金鑰在產生後會維持 5 天有效。 將它複製 toohello 組態伺服器。
2. 在**虛擬機器**hello 虛擬機器清單中的選取 hello 組態伺服器。 開啟 hello**儀表板**索引標籤上，按一下 **連接**。 **開啟**hello 下載 RDP 檔案 toolog 到 hello 設定伺服器使用遠端桌面。 如果您使用 VPN，用於從 hello 在內部部署站台的遠端桌面連線 hello 內部 IP 位址 （hello 位址部署 hello 組態伺服器時所指定）。 當您登入 hello 第一次 hello Azure Site Recovery 組態伺服器安裝精靈會自動執行。

    ![註冊](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. 在**協力廠商軟體安裝**按一下**我接受**toodownload 並安裝 MySQL。

    ![MySQL 安裝](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. 在**MySQL 伺服器的詳細資料**建立認證 toolog 至 hello MySQL 伺服器執行個體。

    ![MySQL 認證](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. 在**網際網路設定**指定 hello 設定伺服器如何連接 toohello 網際網路。 請注意：

   * 如果您想 toouse 自訂 proxy，您應該設定它，然後安裝 hello 提供者。
   * 當您按一下**下一步**toocheck hello proxy 連線將會執行測試。
   * 如果您使用自訂 proxy，或您的預設 proxy 需要驗證，您將需要 tooenter hello proxy 詳細資料，包括 hello 位址、 連接埠，以及認證。
   * 下列 Url 的 hello 必須能夠存取透過 hello proxy:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * 如果您有 IP 位址為基礎的防火牆規則確定 hello 規則設定 tooallow 從 hello 組態伺服器 toohello IP 位址中所述的通訊[Azure Datacenter IP 範圍](https://msdn.microsoft.com/library/azure/dn175718.aspx)和 HTTPS (443) 通訊協定。 您必須 toowhite 清單 IP 範圍的 hello 您規劃 toouse，與美國西部的 Azure 區域。

     ![Proxy 註冊](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. 在**提供者錯誤訊息的當地語系化設定**指定要在哪一個語言中錯誤訊息 tooappear。

    ![錯誤訊息註冊](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. 在**Azure 站台復原登錄**瀏覽和選取 hello 金鑰檔複製 toohello 伺服器。

    ![金鑰檔註冊](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Hello hello 精靈完成頁面上選取下列選項：

   * 選取**啟動帳戶管理對話方塊**hello 管理帳戶 對話方塊的 toospecify 應該開啟當您完成 hello 精靈。
   * 選取**Cspsconfigtool 為建立桌面圖示**tooadd hello 組態伺服器上的桌面捷徑，讓您可以開啟 hello**管理帳戶**在任何時間，而不需要 toorerun hello 對話方塊精靈。

     ![完成註冊](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. 按一下**完成**toocomplete hello 精靈。 隨即產生複雜密碼。 將它複製 tooa 安全的位置。 您將需要 tooauthenticate 並 hello 程序和主要目標伺服器 hello 組態伺服器註冊。 它也有組態伺服器的通訊使用 tooensure 通道完整性。 您可以重新產生 hello 複雜密碼，但就需要 toore 暫存器 hello 主要目標處理序使用和伺服器 hello 新的複雜密碼。

    ![複雜密碼](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

註冊後 hello 組態伺服器就會列在 hello**設定伺服器**hello 保存庫中的頁面。

### <a name="set-up-and-manage-accounts"></a>設定和管理帳戶
在部署期間 Site Recovery 會要求認證 hello 下列動作：

* VMware 帳戶，讓 Site Recovery 可自動探索 vCenter 伺服器或 vSphere 主機上的 VM。
* 當您加入機器進行保護，如此站台復原才能在其上安裝 hello 行動服務。

在您已註冊 hello 組態伺服器之後，您就可以開啟 hello**管理帳戶**對話方塊 tooadd 及管理帳戶用於這些動作。 有幾個方式 toodo 這樣：

* 開啟您選擇 toocreated hello 對話方塊 hello 的 hello 組態伺服器 (cspsconfigtool) 安裝程式的最後一頁上的 hello 捷徑。
* 開啟 hello 對話方塊上的完成的組態伺服器安裝程式。

1. 在 [選取機器]  click 。 您也可以修改並刪除現有的帳戶。

    ![管理帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. 在**帳戶詳細資料**指定帳戶名稱 toouse Azure 與認證 （網域/使用者名稱）。

    ![管理帳戶](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Toohello 設定伺服器連接
有兩種方式 tooconnect toohello 組態伺服器：

* 透過 VPN 站對站或 ExpressRoute 連線
* 透過 hello 網際網路

請注意：

* 網際網路連線會使用搭配 hello 公用虛擬 IP 位址的 hello 伺服器 hello hello 虛擬機器的端點。
* VPN 連線使用 hello 伺服器 hello 內部 IP 的位址與 hello 端點私用通訊埠。
* 它是一次性的決策 toodecide 是否從您的內部部署伺服器 toohello tooconnect （控制項和複寫的資料） （主要目標伺服器中的 設定伺服器） 的各種元件伺服器在 Azure 中執行，透過 VPN 連線，或 hello 網際網路。 您之後無法變更此設定。 如果您這樣做您將需要 tooredeploy hello 案例，並重新保護您的電腦。  

## <a name="step-3-deploy-hello-master-target-server"></a>步驟 3： 部署的 hello 主要目標伺服器
1. 按一下 [準備目標 (Azure) 資源]  >  [部署主要目標伺服器]。
2. 指定 hello 主要目標伺服器詳細資料和認證。 hello 伺服器部署在 hello 與 hello 組態伺服器相同的 Azure 網路。 當您按一下 toocomplete Azure 虛擬機器將會建立 Windows 或 Linux 的資源庫映像。

    ![目標伺服器設定](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

請注意，hello 任何子網路中的前四個 IP 位址已保留給內部 Azure 的使用量。 指定任何其他可用的 IP 位址。

> [!NOTE]
> 設定保護的工作負載需要一致的高 I/O 效能和低度延遲順序 toohost I/O 密集型工作負載使用中的時，選取標準 DS4[進階儲存體帳戶](../storage/common/storage-premium-storage.md)。
>
>

1. 利用這些端點建立 Windows 主要目標伺服器 VM。 請注意，只有當您透過連線 hello 網際網路，會建立公用端點。

   * Custom： 公用連接埠供 hello 處理序伺服器 toosend 複寫資料透過 hello 網際網路。 私用連接埠 9443 供 hello 處理序伺服器 toosend 複寫資料 toohello 主要目標伺服器，透過 VPN。
   * Custom1： 透過 hello hello 處理序伺服器 toosend 中繼資料所使用的公用連接埠網際網路。 Hello 處理序伺服器 toosend 中繼資料 toohello 主要目標伺服器會使用私用連接埠 9080 透過 VPN。
   * PowerShell：私人連接埠 5986
   * 遠端桌面：私人連接埠 3389
2. 利用這些端點建立 Linux 主要目標伺服器 VM。 請注意，將公用端點，建立只有當您透過 hello 正在連線網際網路。

   * Custom： 公用連接埠資料所使用的處理序伺服器 toosend 複寫 hello 透過網際網路。 私用連接埠 9443 供 hello 處理序伺服器 toosend 複寫資料 toohello 主要目標伺服器，透過 VPN。
   * Custom1： 公用連接埠正由 hello 處理序伺服器 toosend 中繼資料透過 hello 網際網路。 Hello 處理序伺服器 toosend 中繼資料 toohello 主要目標伺服器會使用私用連接埠 9080 透過 VPN
   * SSH：私人連接埠 22

     > [!WARNING]
     > 不會刪除，或變更任何 hello hello 主要目標伺服器部署期間建立的端點的 hello 公用或私用連接埠號碼。
     >
     >
3. 在**虛擬機器**等候 hello 虛擬機器 toostart。

   * 如果是 Windows 伺服器記下 hello 遠端桌面的詳細資料。
   * 如果它是在 Linux 伺服器，而且您要透過 VPN 注意 hello 內部 IP 位址 hello 虛擬機器的連線。 如果您要連線透過 hello 網際網路注意 hello 公用 IP 位址。
4. 登入 hello toocomplete 安裝伺服器並向 hello 組態伺服器。
5. 如果您在執行 Windows：

   1. 起始遠端桌面連線 toohello 虛擬機器。 hello 第一次登入指令碼會在執行的 PowerShell 視窗。 不要關閉它。 完成時 hello 主機 Agent 組態工具會自動開啟 tooregister hello 伺服器。
   2. 在**主機代理程式設定**指定 hello 組態伺服器和連接埠 443 的 hello 內部 IP 位址。 您可以使用 hello 內部位址和私用連接埠 443 即使因為附加的 toohello hello 虛擬機器時，您要不在透過 VPN 連線與 hello 組態伺服器相同的 Azure 網路。 讓 [使用 HTTPS]  保持啟用狀態。 輸入您先前記下的 hello 組態伺服器 hello 複雜密碼。 按一下**確定**tooregister hello 伺服器。 您可以忽略 hello NAT 選項。 它們不會被使用。
   3. 如果您估計的保留磁碟機的需求超過 1 TB，您就可以設定 hello 保留磁碟區 (R) 使用的虛擬磁碟和[儲存空間](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Windows 主要目標伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. 如果您在執行 Linux：

   1. 請確定您已安裝最新的 Linux Integration Services (LIS) 安裝之前安裝 hello 主要目標伺服器 hello。 您可以找到 hello 最新版本的 LIS 以及指示如何 tooinstall[這裡](https://www.microsoft.com/download/details.aspx?id=46842)。 Hello LIS 安裝之後，請重新啟動 hello 機器。
   2. 在 [準備目標 (Azure) 資源] 中，按一下 [下載及安裝其他軟體 (僅適用於 Linux 主要目標伺服器)]。 複製 hello 下載 tar 檔案解壓縮檔案 toohello 虛擬機器使用 sftp 用戶端。 或者，您便可以登入 toohello 已部署的 linux 主要目標伺服器上，並使用*wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* toodownload hello hello 檔案。
   3. 使用安全殼層用戶端的 toohello 伺服器上的記錄。 如果您已經連接 toohello 透過 VPN 的 Azure 網路使用 hello 內部 IP 位址。 否則使用 hello 外部 IP 位址與 hello SSH 公用端點。
   4. 執行從 hello gzipped installer 擷取 hello 檔案： **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![Linux 主要目標伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. 請確定您在 hello 目錄 toowhich 擷取 hello hello tar 檔案解壓縮檔案內容。
   6. 複製 hello 組態伺服器的複雜密碼 tooa 本機檔案使用 hello 命令**echo  *`<passphrase>`*  > passphrase.txt**
   7. 執行 hello 命令"**sudo。 / 安裝-t 這兩個-裝載-R MasterTarget-d /usr/local/ASR-i  *`<Configuration server internal IP address>`*  -p 443-s y-c https-P passphrase.txt**"。

      ![註冊目標伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. 等候幾分鐘的時間 (10-15)，且上 hello 頁面檢查該 hello 主要目標伺服器會列在中註冊**伺服器** > **設定伺服器****伺服器詳細資料**  索引標籤。如果您要執行 Linux，且它並未登錄 hello 主機組態工具一次從執行 /usr/local/ASR/Vx/bin/hostconfigcli。 您必須以 root 身分執行 chmod tooset 存取權限。

    ![確認目標伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> 它最多可能需要 too15 hello hello 入口網站中所列的主要目標伺服器 toobe 完成註冊之後的分鐘。 立即按一下 tooupdate**重新整理**上 hello**設定伺服器**頁面。
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>步驟 4： 部署的 hello 內部處理序伺服器
在開始之前，建議您 hello 處理序伺服器上設定靜態 IP 位址，以便保證 toobe 永續性透過重新開機。

1. 按一下 快速入門 >**安裝處理序伺服器在內部** > **下載並安裝 hello 處理序伺服器**。

    ![安裝處理序伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. 複製 hello 下載 zip 檔案 toohello 伺服器您將 tooinstall hello 處理序伺服器。 hello zip 檔案包含兩個安裝檔案：

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. 將解壓縮 hello 封存及複製 hello 檔案 tooa 伺服器上的安裝位置 hello。
4. 執行 hello **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** 安裝檔案，然後遵循 hello 指示。 這會安裝所需的 hello 部署的協力廠商元件。
5. 然後執行 **Microsoft-ASR_CX_8.4.0.0_Windows***。
6. 在 hello**伺服器模式**頁面上，選取**處理序伺服器**。
7. 在 hello**環境詳細資料**頁面執行下列 hello:

    - 如果您想 tooprotect VMware 虛擬機器按一下**[是]**
    - 如果您只想 tooprotect 實體伺服器，因此不需要安裝在 hello 處理序伺服器上的 VMware vCLI。 按一下 [否]  並繼續。

1. 安裝 VMware vCLI 時，請注意下列 hello:

   * **僅支援 VMware vSphere CLI 5.5.0**。 hello 處理序伺服器無法與其他版本或更新的 vSphere CLI 運作。
   * 從 [這裡](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * 如果您之前在您開始安裝 hello 處理序伺服器，並安裝程式不會偵測到已安裝 vSphere CLI，，等候 toofive 分鐘的時間才能在再次嘗試安裝程式。 這可確保，所有的 hello 環境變數所需 vSphere CLI 偵測有已正確初始化。
2. 在**NIC 選取項目之處理序伺服器**選取 hello 網路介面卡應該使用該 hello 處理序伺服器。

   ![選取配接器](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. 在 [組態伺服器詳細資料] 中：

   * Hello ip 位址和連接埠，如果您要透過 VPN 連線，可指定 hello 組態伺服器 hello 內部 IP 位址和 hello 連接埠為 443。 否則指定 hello 公用虛擬 IP 位址和對應的公用 HTTP 端點。
   * 輸入 hello hello 組態伺服器的複雜密碼。
   * 清除**確認行動服務軟體簽章**如果當您使用自動推送 tooinstall hello 服務時，您會想 toodisable 驗證。 簽章驗證必須從 hello 處理序伺服器的網際網路連線。
   * 按一下 [下一步] 。

   ![註冊設定伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. 在 [選取安裝磁碟機]  中，選取快取磁碟機。 hello 處理序伺服器必須至少 600 GB 的可用空間的快取磁碟機。 然後按一下 [安裝] 。

   ![註冊設定伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. 請注意，您可能需要 toorestart hello toocomplete hello 安裝伺服器。 在**組態伺服器** > **伺服器詳細資料**檢查該 hello 處理序伺服器隨即出現，並在 hello 保存庫中註冊成功。

> [!NOTE]
> 它可能會佔用 too15 分鐘之後註冊已完成 hello 的處理序伺服器 tooappear hello 組態伺服器底下所列。 tooupdate 立即重新整理 hello 組態伺服器上 hello 重新整理 按鈕在 hello hello 組態伺服器 頁面底部的 
>
>

![驗證處理序伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

如果您註冊 hello 處理序伺服器時，您未停用 hello 行動服務的簽章驗證您稍後可以執行它，如下所示：

1. 登入系統管理員身分的 hello 處理序伺服器，然後開啟 hello 檔案 C:\pushinstallsvc\pushinstaller.conf 進行編輯。 在 [hello] 區段下**[PushInstaller.transport]**新增這行： **SignatureVerificationChecks ="0"**。 儲存並關閉 hello 檔案。
2. 重新啟動 hello InMage PushInstall 服務。

## <a name="step-5-update-site-recovery-components"></a>步驟 5：更新 Site Recovery 元件
站台復原元件會從時間 tootime 更新。 新的更新可用時您應該安裝在 hello 順序：

1. 組態伺服器
2. 處理序伺服器
3. 主要目標伺服器
4. 容錯回復工具 (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>取得並安裝 hello 更新
1. 您可以從站台復原 hello 取得 hello 組態、 程序和主要目標伺服器更新**儀表板**。 Linux 的安裝，請從 hello gzipped 安裝程式解壓縮 hello 檔案，並執行 hello 命令"sudo。 / 安裝 「 tooinstall hello 更新。
2. [下載](http://go.microsoft.com/fwlink/?LinkID=533813)hello hello 容錯回復 tool(vContinuum) 最新的更新。
3. 如果您正在執行的虛擬機器或實體已經有安裝 hello 行動服務的伺服器，您可以取得更新 hello 服務，如下所示：

   * **選項 1**：下載更新：
     * [Windows Server (僅限 64 位元)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4、6.5、6.6 (僅限 64 位元)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (僅限 64 位元)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Hello 處理序伺服器 hello 在更新之後，更新的版的 hello 行動服務會使用在 hello C:\pushinstallsvc\repository 資料夾 hello 處理序伺服器上。
   * **選項 2**： 如果您有較舊版本的 hello 安裝行動服務的電腦，您可以從 hello 管理入口網站，自動升級 hello 電腦上的 hello 行動服務。

     1. 確定更新該 hello 處理序伺服器。
     2. 請確定該 hello 受保護的電腦符合 < 以 hello[必要條件](#install-the-mobility-service-automatically)自動將發送 hello 行動服務，以便 hello 更新可以正常運作。
     3. 選取 hello 保護群組時，反白顯示 hello 受保護的電腦和按一下**更新行動服務**。 這個按鈕才可以使用較新版本的 hello 行動服務。

         ![選取 vCenter 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

在選取的帳戶指定 hello 系統管理員帳戶使用 toobe tooupdate hello 行動服務 hello 受保護伺服器上。 按一下 [確定]，並等候觸發 hello 作業 toocomplete。

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>步驟 6：新增 vCenter 伺服器或 vSphere 主機
1. 按一下**伺服器** > **設定伺服器**> 組態伺服器 >**新增 vCenter Server** tooadd vCenter server 或 vSphere 主機。

    ![選取 vCenter 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. 指定伺服器 hello 或主應用程式與伺服器詳細資料選取 hello 程序將會使用的 toodiscover 它。

   * 如果 hello vCenter server 未 hello 預設連接埠 443 上執行指定的 hello vCenter server 正在執行的 hello 連接埠號碼。
   * hello 處理序伺服器必須位於相同的 hello vCenter 伺服器 /vsphere 主機為網路和應有 VMware vSphere CLI 5.5.0 安裝的 hello。

     ![vCenter 伺服器設定](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. 探索完成後 hello vCenter 伺服器將列在 hello 組態伺服器詳細資料。

    ![vCenter 伺服器設定](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. 如果您使用非系統管理員帳戶 tooadd hello 伺服器或主機，請確定 hello 帳戶具有下列權限的 hello:

   * vCenter 帳戶應該已啟用資料中心、資料存放區、資料夾、主機、網路、資源、儲存體檢視、虛擬機器和 vSphere 分散式切換權限。
   * vSphere 主機帳戶應該擁有 hello 資料中心，資料存放區、 資料夾、 主機、 網路、 資源、 虛擬機器和啟用的 vSphere 分散式交換器權限

## <a name="step-7-create-a-protection-group"></a>步驟 7：建立保護群組
1. 開啟 [受保護的項目]  >  [保護群組]  >  [建立保護群組]。

    ![建立保護群組](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. 在 hello**指定保護群組設定**頁面上指定 hello 群組和選取 hello 組態伺服器，您會想 toocreate hello 群組的名稱。

    ![保護群組設定](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. 在 hello**指定複寫設定**頁面設定將用於所有 hello 機器 hello 群組中的 hello 複寫設定。

    ![保護群組複寫](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. 設定：

   * **多重 VM 一致性**： 如果您開啟此選項，它會 hello 保護群組中的 hello 電腦上建立共用的應用程式一致復原點。 當所有 hello 保護群組中的 hello 機器執行這項設定就非常重要 hello 相同的工作負載。 所有機器將都會復原的 toohello 相同的資料點。 僅適用於 Windows 伺服器。
   * **RPO 臨界值**: hello 持續資料保護複寫 RPO 超過 hello 設定 RPO 臨界值時，將會產生警示。
   * **復原點保留**： 指定 hello 保留視窗。 受保護的電腦可以是復原 tooany 這個視窗內的點。
   * **應用程式一致的快照頻率**：指定建立包含應用程式一致快照的復原點的頻率。

您可以監視 hello 保護群組建立在 hello**受保護項目**頁面。

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>您想 tooprotect 步驟 8： 設定好電腦
您將需要 tooinstall hello 上虛擬機器和實體伺服器，您想要 tooprotect 行動服務。 您可以使用兩種方式執行此動作：

* 自動推入，並從 hello 處理序伺服器的每部機器上安裝 hello 服務。
* 手動安裝 hello 服務。

### <a name="install-hello-mobility-service-automatically"></a>自動安裝 hello 行動服務
當您將加入機器 tooa 保護群組 hello 行動服務會自動推入，並且 hello 處理序伺服器安裝在每部電腦。

**自動推入的 Windows 伺服器上安裝 hello 行動服務：**

1. 中所述安裝最新更新 hello 處理序伺服器 hello[步驟 5： 安裝最新的更新](#step-5-install-latest-updates)，並確定該 hello 處理序伺服器可供使用。
2. 確認 hello 來源電腦之間沒有網路連線且 hello 處理序伺服器和該 hello 來源電腦可以存取從 hello 處理序伺服器。  
3. 設定 hello Windows 防火牆 tooallow**檔案及印表機共用**和**Windows Management Instrumentation**。 在 Windows 防火牆設定 下選取 hello 選項 「 允許應用程式或功能通過防火牆 」，選取 hello 應用程式中 hello 圖所示。 針對屬於 tooa 網域，您可以使用 GPO 來設定 hello 防火牆原則的電腦。

    ![防火牆設定](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. hello 使用帳戶 tooperform hello 推入安裝必須是您想要 tooprotect hello hello 機器上的 Administrators 群組中。 這些認證只用於 hello 行動服務推入安裝，您會提供當您新增電腦 tooa 保護群組。
5. 如果帳戶不是網域帳戶的 hello 提供您將需要 toodisable hello 本機電腦上的遠端使用者存取控制。 toodo 此新增 hello LocalAccountTokenFilterPolicy DWORD 登錄項目底下 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System 1 的值。 從 CLI tooadd hello 登錄項目開啟 cmd 或 powershell，並輸入 **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 。

**自動推入安裝 hello 行動服務在 Linux 伺服器上：**

1. 中所述安裝最新更新 hello 處理序伺服器 hello[步驟 5： 安裝最新的更新](#step-5-install-latest-updates)，並確定該 hello 處理序伺服器可供使用。
2. 確認 hello 來源電腦之間沒有網路連線且 hello 處理序伺服器和該 hello 來源電腦可以存取從 hello 處理序伺服器。  
3. 請確定 hello 帳戶 hello 來源 Linux 伺服器上的根使用者。
4. 請確定該 hello 來源 Linux 伺服器包含所有 Nic 相關都聯的 hello 本機主機名稱 tooIP 位址對應的項目上的 hello /etc/hosts 檔案。
5. 安裝最新 openssh 的 hello、 openssh 伺服器、 openssl 封裝要 tooprotect hello 機器上。
6. 請確定 SSH 已啟用且正在連接埠 22 上執行。
7. 啟用 hello sshd_config 檔案中的 SFTP 子系統和密碼驗證，如下所示：

   * a) 以 root 的身分登入。
   * b） 在 hello 檔案等/ssh/sshd_config 檔，尋找 hello 線開頭**PasswordAuthentication**。
   * c） hello 行取消註解再變更 hello 值從 「 否 」 太"yes"。

       ![Linux 行動性](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d） 尋找 hello 第一行皆為開頭子系統 hello 行取消註解。

       ![Linux 推播行動性](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. 請確認支援 hello 來源電腦 Linux variant。

### <a name="install-hello-mobility-service-manually"></a>手動安裝 hello 行動服務
tooinstall hello 行動服務會在 C:\pushinstallsvc\repository hello 處理序伺服器使用 hello 軟體封裝。 登入 hello 處理序伺服器與複本 hello 適當的安裝封裝 toohello 來源機器 hello 表為基礎:-

| 來源作業系統 | 處理序伺服器上的行動服務封裝 |
| --- | --- |
| Windows Server (僅限 64 位元) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4、6.5、6.6 (僅限 64 位元) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**tooinstall hello 行動服務在 Windows server 上手動**，請勿遵循 hello:

1. 複製 hello **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** toohello 來源電腦上的 hello 表中列出的 hello 處理序伺服器的目錄路徑的包裝。
2. 執行可執行檔的 hello hello 來源電腦上，以安裝 hello 行動服務。
3. 請遵循 hello 安裝指示。
4. 選取**行動服務**為 hello 角色，然後按一下**下一步**。

    ![安裝行動服務](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. 保留 hello 安裝目錄為 hello 預設安裝路徑，再按**安裝**。
6. 在**主機代理程式設定**指定 hello IP 位址和 HTTPS 連接埠 hello 組態伺服器。

   * 如果您要連線透過網際網路指定的 hello hello 與 hello 的通訊埠公用虛擬 IP 位址和公用的 HTTPS 端點。
   * 如果您要透過 VPN 連線指定 hello 內部 IP 位址和 hello 連接埠為 443。 讓 [使用 HTTPS]  保持勾選狀態。

     ![安裝行動服務](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. 指定 hello 組態伺服器的複雜密碼，然後按一下**確定**tooregister hello 與 hello 組態伺服器的行動服務。

**toorun 從 hello 命令列：**

1. Hello 複雜密碼複製 hello CX toohello"C:\connection.passphrase"hello 伺服器檔案，然後執行這個命令。 在我們的範例 CX i 104.40.75.37 和 hello HTTPS 連接埠是 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**在 Linux 伺服器上手動安裝 hello 行動服務**:

1. 將複製 hello 適當 tar 檔案解壓縮的封存 hello 處理序伺服器 toohello 來源電腦，上面的 hello 資料表為基礎。
2. 開啟殼層程式並執行，以擷取 hello 壓縮的 tar 封存 tooa 本機路徑`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. 建立 passphrase.txt 檔案您可以在 hello 本機目錄 toowhich 解壓縮 hello hello tar 檔案解壓縮的封存內容來輸入 *`echo <passphrase> >passphrase.txt`* 從殼層。
4. 輸入安裝 hello 行動服務 *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* 。
5. 指定 hello IP 位址和連接埠：

   * 如果您要透過網際網路指定 hello 組態伺服器的虛擬公用 IP 位址和公用的 HTTPS 端點中的 hello 連線 toohello 組態伺服器`<IP address>`和`<port>`。
   * 如果您要透過 VPN 連線來連接指定 hello 內部 IP 位址和 443。

**從 hello 命令列 toorun**:

1. 複製 hello CX toohello"passphrase.txt"hello 伺服器檔案中的 hello 複雜密碼，以及執行此命令。 在我們的範例 CX i 104.40.75.37 和 hello HTTPS 連接埠是 62519:

tooinstall 實際執行伺服器上：

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall hello 目標伺服器上：

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> 當您新增已經在執行適當版本的 hello 行動服務則會略過 hello 推入安裝的機器 tooa 保護群組。
>
>

## <a name="step-9-enable-protection"></a>步驟 9：啟用保護
您新增虛擬機器和實體伺服器 tooa 保護群組的 tooenable 保護。 開始之前，請注意：

* 虛擬機器會探索每隔 15 分鐘，且它可能會佔用 too15 分鐘，讓它們在探索後的在 Azure Site Recovery tooappear。
* Hello （例如 VMware 工具安裝） 的虛擬機器上的環境變更也可能佔用 too15 分鐘 toobe 更新 Site Recovery 中。
* 您可以檢查 hello 上次探索的時間，以 hello**上次連絡時間**欄位 hello vCenter server/ESXi 主機上 hello**設定伺服器**頁面。
* 如果您已經建立保護群組並新增 vCenter Server 或 ESXi 主機之後，會在 15 分鐘 hello Azure Site Recovery 入口網站 toorefresh 和 hello 中所列的虛擬機器 toobe**加入機器 tooa 保護群組**對話方塊。
* 如果您想要立即以加入機器 tooprotection 群組而不需等待 hello 已排程的探索 tooproceed，反白顯示 hello 組態伺服器 （但不要按），按一下 [hello**重新整理**] 按鈕。
* 當您新增虛擬機器或實體機器 tooa 保護群組時，hello 處理序伺服器自動推播通知，並 hello 來源伺服器上安裝 hello 行動服務，如果 hello 尚未安裝。
* Hello 自動推入機制 toowork 請確定您已設定受保護的機器 hello 上一個步驟中所述。

如下所示加入機器：

1. 按一下 [受保護的項目]  >  [保護群組]  >  [機器]  >  [新增機器]。 我們建議最佳作法是保護群組應該反映您的工作負載，讓您新增執行特定應用程式 toohello 機器相同的群組。
2. 在**選取虛擬機器**如果您要保護實體伺服器、 hello**加入實體機器**精靈提供 hello IP 位址和易記名稱。 然後，選取 hello 作業系統系列。

    ![加入 V-Center 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. 在**選取虛擬機器**如果您要保護 VMware 虛擬機器，選取您的虛擬機器 （或 hello EXSi 主機正在執行），來管理的 vCenter 伺服器，然後選取 hello 機器。

    ![加入 V-Center 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. 在**指定目標資源**選取 hello 主要目標伺服器和儲存體 toouse 複寫，然後選取是否 hello 設定適用於所有工作負載。 選取[進階儲存體帳戶](../storage/common/storage-premium-storage.md)設定需要一致的高 IO 效能和順序 toohost IO 密集工作負載中的低延遲工作負載的保護時。 如果您想要工作負載磁碟 toouse 高階儲存體帳戶，您會需要 toouse hello DS 系列的主要目標。 您無法搭配使用進階儲存體磁碟與非 DS 系列的主要目標。

   > [!NOTE]
   > 我們不支援的儲存體帳戶使用 hello 建立 hello 移動[新版 Azure 入口網站](../storage/common/storage-create-storage-account.md)跨越資源群組。
   >
   >

    ![vCenter 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. 在**指定帳戶**選取您想 toouse 受保護的機器上安裝 hello 行動服務的 hello 帳戶。 hello 帳戶認證，才能自動安裝 hello 行動服務。 如果您無法選取帳戶，請確定您如步驟 2 中所述設定一個。 請注意，Azure 無法存取此帳戶。 Windows server hello 帳戶應擁有 hello 來源伺服器上的系統管理員權限。 適用於 Linux hello 帳戶必須是根目錄。

    ![Linux 認證](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. 按一下 hello 核取記號 toofinish 加入機器 toohello 保護群組和 toostart 初始複寫的每一部機器。 您可以監視狀態 hello**作業**頁面。

    ![加入 V-Center 伺服器](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. 此外，您可以監視保護狀態，方法是按一下 [受保護的項目] > 保護群組名稱 > [虛擬機器]。 初始複寫完成，且 hello 機器進行同步處理資料之後會顯示**保護**狀態。

    ![虛擬機器作業](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>設定受保護機器屬性
1. 在機器具有 **受保護** 狀態之後，您可以設定其容錯移轉屬性。 Hello 保護群組的詳細資料中選取 hello 電腦及開啟 hello**設定** 索引標籤。
2. 您可以修改將 toohello 機器在 Azure 中之後指定容錯移轉和 hello Azure 虛擬機器大小的 hello 名稱。 您也可以選取會在容錯移轉之後連接 hello Azure 網路 toowhich hello 機器。

   > [!NOTE]
   > [移轉網路](../resource-group-move-resources.md)跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間不支援的網路用來部署站台復原。
   >
   >

    ![設定虛擬機器屬性](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

請注意：

* hello hello Azure 機器名稱必須符合 Azure 需求。
* 依預設在 Azure 中複寫的虛擬機器未連接的 tooan Azure 網路。 如果您想要複寫的虛擬機器 toocommunicate 確定 tooset hello 相同的 Azure 網路它們。
* 如果您調整 VMware 虛擬機器或實體伺服器上磁碟區的大小，它會進入嚴重狀態。 如果您需要 toomodify hello 大小，請勿 hello 遵循：

  * a） 變更 hello 大小設定。
  * b） 在 hello**虛擬機器**索引標籤，選取 hello 虛擬機器，然後按一下 **移除**。
  * c） 在**移除虛擬機器**選取 hello 選項**停用保護 （用於復原切入及調整磁碟區）**。 此選項會停用保護，但會保留在 Azure 中的 hello 復原點。

      ![設定虛擬機器屬性](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d） 重新啟用 hello 虛擬機器的保護。 當您重新啟用保護 hello 資料 hello 調整磁碟區將會傳送的 tooAzure。

## <a name="step-10-run-a-failover"></a>步驟 10：執行容錯移轉
目前您只能為受保護的 VMware 虛擬機器和實體伺服器執行非計劃的容錯移轉。 請注意 hello 下列：

* 起始容錯移轉之前，請確定執行且狀況良好的 hello 組態和主要目標伺服器。 否則容錯移轉將會失敗。
* 來源機器未隨著非計劃的容錯移轉關閉。 執行未規劃的容錯移轉，就會停止 hello 受保護伺服器的資料複寫。 您將需要 toodelete hello 電腦從 hello 保護群組，並且將它們加入再次順序 toostart hello 規劃的容錯移轉完成之後，再次保護機器。
* 如果您想透過 toofail 而不會遺失任何資料，請確定 hello 主要站台虛擬機器均已關閉，才能起始 hello 容錯移轉。

1. 在 hello**復原計劃**頁面上，並加入復原方案。 指定 hello 計劃的詳細資料，然後選取**Azure**為 hello 目標。

    ![設定復原計畫](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. 在**選取虛擬機器**選取保護群組，然後選取 hello 群組 tooadd toohello 復原計劃中的 機器。 [閱讀更多](site-recovery-create-recovery-plans.md) 復原方案的相關資訊。

    ![新增虛擬機器](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. 如果需要您可以自訂 hello 計畫 toocreate 群組和順序 hello 順序機器 hello 復原計劃已容錯移轉。 您也可以加入進行手動動作和指令碼的提示。 hello 指令碼時復原 tooAzure 可以使用 新增[Azure 自動化 Runbook](site-recovery-runbook-automation.md)。
4. 在 hello**復原計劃**頁面上選取 hello 計劃，然後按一下**規劃的容錯移轉**。
5. 在**確認容錯移轉**確認 hello 容錯移轉方向 (tooAzure)，並選取 hello 復原點 toofail 透過。
6. 等候 hello 容錯移轉作業 toocomplete，然後確認 hello 容錯移轉依照預期方式運作，而且該 hello 複寫已成功在 Azure 中的虛擬機器開始。

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>步驟 11：來自 Azure 機器的容錯移轉失敗
[進一步了解](site-recovery-failback-azure-to-vmware-classic-legacy.md)有關 toobring 失敗您在 Azure 中執行回 tooyour 在內部部署環境的機器上。

## <a name="manage-your-process-servers"></a>管理您的處理序伺服器
hello 處理序伺服器在 Azure 中，會傳送複寫資料 toohello 主要目標伺服器，並探索新的 VMware 虛擬機器加入的 tooa vCenter server。 在下列情況下的 hello 中，您可能想 toochange hello 處理序伺服器部署中：

* 如果目前處理序伺服器 hello 關閉
* 如果您的復原點目標 (RPO) 就會上升 tooan 為您的組織無法接受的程度。

必要時您可以移動 hello 複寫的部分或所有您在內部部署 VMware 虛擬機器和實體伺服器 tooa 不同處理伺服器。 例如：

* **失敗**— 如果處理序伺服器失敗或無法使用，您就可以移動受保護的機器複寫 tooanother 處理序伺服器。 Hello 來源機器和複本機器的中繼資料也會移動的 toohello 新處理序伺服器，並重新同步處理資料。 hello 新處理序伺服器會自動連線 toohello vCenter server tooperform 自動探索。 您可以監視 hello hello 站台復原儀表板上的處理序伺服器的狀態。
* **負載平衡 tooadjust RPO**，改善的負載平衡，您可以選取不同的處理序伺服器 hello Site Recovery 入口網站，並將一或多個機器 tooit 手動載入平衡的複寫移動。 在此情況下的 hello 選的來源與複本機器的中繼資料是新處理序伺服器已移動的 toohello。 hello 原始的處理序伺服器維持連接的 toohello vCenter 伺服器。

### <a name="monitor-hello-process-server"></a>監視 hello 處理序伺服器
如果處理序伺服器處於重大狀態，狀態將會顯示警告 hello 站台復原儀表板。 您可以按一下 hello 狀態 tooopen hello 事件索引標籤上，，然後向下切入 toospecific hello 工作 索引標籤上的作業。

### <a name="modify-hello-process-server-used-for-replication"></a>修改用來進行複寫的 hello 處理序伺服器
1. 開啟 [伺服器]  >  [組態伺服器] > 選取組態伺服器 > [伺服器詳細資料]。
2. 按一下**處理序伺服器** > **變更處理序伺服器**想 toomodify 的下一個 toohello 伺服器。

    ![變更處理序伺服器 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. 在**變更處理序伺服器** > **目標處理序伺服器**選取 hello 新的伺服器，您想 toouse，，然後選取您想 tooreplicate toohello 新伺服器的 hello 虛擬機器。 按一下 hello 資訊圖示下一步 toohello 伺服器名稱，可用空間，已用的記憶體的詳細資料。 hello 平均空間將會需要的 tooreplicate 每個選取的虛擬機器 toohello 新處理序伺服器已顯示的 toohelp 要載入的決策。

    ![變更處理序伺服器 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. 按一下 hello 核取記號 toobegin 複寫 toohello 新處理序伺服器。 請注意，是否是重要的處理序伺服器中移除所有虛擬機器它應該不會再顯示嚴重警告 hello 儀表板中。

## <a name="third-party-software-notices-and-information"></a>第三方廠商軟體注意事項和資訊
Do Not Translate or Localize

hello 軟體和韌體中執行 hello Microsoft 產品或服務為基礎，或納入 hello 從資料列下方 （以下合稱 「 第三方程式碼 」） 的專案。  Microsoft 為 hello 不原始作者的 hello 協力廠商程式碼。  hello 原始著作權聲明與授權，在其下 Microsoft 接收這類協力廠商程式碼，會設定制定下方。

區段 A 中的 hello 資訊關於元件 hello 專案從下面所列的第三方廠商程式碼。 Such licenses and information are provided for informational purposes only.  此第三方廠商程式碼正在 relicensed 的 tooyou microsoft 在 Microsoft 軟體授權條款的 hello Microsoft 產品或服務。  

節 B 中的 hello 資訊有關第三方廠商程式碼元件所進行可用 tooyou microsoft hello 原始授權條款。

hello 完整的檔案可能位於 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428)。 Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
