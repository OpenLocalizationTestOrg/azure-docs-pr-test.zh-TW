---
title: "StorSimple Virtual Array aaaBest 作法 |Microsoft 文件"
description: "說明用於部署與管理 hello StorSimple Virtual Array hello 最佳作法。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>StorSimple Virtual Array 的最佳作法
## <a name="overview"></a>Overview
Microsoft Azure StorSimple Virtual Array 是一個整合式儲存體解決方案，可管理 Hypervisor 中執行之內部部署虛擬裝置與 Microsoft Azure 雲端儲存體之間的儲存體工作。 StorSimple Virtual Array 是有效率且符合成本效益替代 toohello 8000 系列實體陣列。 hello 虛擬陣列可以在現有的 hypervisor 基礎結構上執行，同時支援 hello iSCSI 和 hello SMB 通訊協定，而且非常適用於遠端辦公室/分公司案例。 如需 hello StorSimple 解決方案的詳細資訊，請移至太[Microsoft Azure StorSimple 概觀](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx)。

本文涵蓋 hello hello 初始設定、 部署和管理的 hello StorSimple Virtual Array 期間實作的最佳作法。 這些最佳作法會提供已驗證的指導方針 hello 安裝並管理您的虛擬陣列。 這份文件為目標朝向 hello IT 系統管理員部署和管理 hello 虛擬陣列，其資料中心。

我們建議您定期檢閱最佳作法 toohelp hello 確保您的裝置仍然處於相容性變更時 toohello 安裝或作業流程。 如果您在虛擬陣列上實作這些最佳作法時遇到任何問題，請 [連絡 Microsoft 支援服務](storsimple-virtual-array-log-support-ticket.md) 以取得協助。

## <a name="configuration-best-practices"></a>組態的最佳作法
這些最佳作法會涵蓋，需要在 hello 初始安裝和部署的 hello 虛擬陣列 toobe hello 指導方針。 這些最佳作法 」 包含這些相關的 toohello 佈建的 hello 虛擬機器，群組原則設定，調整大小、 網路功能、 設定儲存體帳戶，以及建立共用設定 hello 和磁碟區的 hello 虛擬陣列。 

### <a name="provisioning"></a>佈建
StorSimple Virtual Array hello hypervisor （HYPER-V 或 VMware） 上佈建虛擬機器 (VM) 是您的主機伺服器。 佈建 hello 虛擬機器，請確認您的主機時，可以 toodedicate 足夠的資源。 如需詳細資訊，請移至太[最少資源需求](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements)tooprovision 陣列。

實作下列最佳作法，佈建 hello 虛擬陣列時的 hello:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **虛擬機器類型** |可與 Windows Server 2012 或更新版本搭配使用的**第 2 代** VM 和「.vhdx」映像。 <br></br> 可與 Windows Server 2008 或更新版本搭配使用的**第 1 代** VM 和「.vhd」映像。 |在使用「.vmdk」  映像時，請使用虛擬機器第 8 版至第 11 版。 |
| **記憶體類型** |設定為 **靜態記憶體**。 <br></br> 請勿使用 hello**動態記憶體**選項。 | |
| **資料磁碟類型** |佈建為**動態擴充**。<br></br> **固定大小**需要很長的時間。 <br></br> 請勿使用 hello**差異**選項。 |使用 hello**精簡佈建**選項。 |
| **資料磁碟修改** |不允許擴充或縮小。 嘗試 toodo 因此導致 hello 裝置上的 hello 本機資料遺失。 |不允許擴充或縮小。 嘗試 toodo 因此導致 hello 裝置上的 hello 本機資料遺失。 |

### <a name="sizing"></a>調整大小
當調整您的 StorSimple Virtual Array，請考慮下列因素的 hello:

* 保留給磁碟區或共用的本機空間。 大約有 12%的 hello 空間都會保留在 hello 本機層之每個已佈建分層磁碟區或共用。 大約 10%的 hello 空間也會保留固定在本機檔案系統磁碟區。
* 快照額外負荷。 大約 15 %hello 本機層上的空間被保留供快照集。
* 還原需求。 如果進行還原為新的作業，調整大小應該考量 hello 還原所需的空間。 還原完成後，tooa 共用或磁碟區的 hello 相同的大小。
* 應配置部分緩衝區來應付非預期的成長。

根據上述因素的 hello，可以透過下列方程式 hello 表示 hello 調整大小需求：

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

hello 下列範例說明如何調整大小的虛擬陣列，根據您的需求。

#### <a name="example-1"></a>範例 1：
在您的虛擬陣列，您想 toobe 能夠

* 佈建 2 TB 的分層式磁碟區或共用。
* 佈建 1 TB 的分層式磁碟區或共用。
* 佈建 300 GB 的固定在本機的磁碟區或共用。

Hello 上述的磁碟區或共用，讓我們計算 hello hello 本機層上的空間需求。

首先，每個階層式磁碟區/共用，本機保留項目將會是等於 too12 %hello 磁碟區/共用大小。 Hello 固定在本機磁碟區/共用，本機保留會是 hello 的 10%本機固定磁碟區/共用 （除了 toohello 佈建大小） 的大小。 在此範例中，您需要

* 240 GB 的本機保留空間 (針對 2 TB 的分層式磁碟區/共用)
* 120 GB 的本機保留空間 (針對 1 TB 的分層式磁碟區/共用)
* 330 GB 本機固定磁碟區或共用 （新增的本機保留 toohello 佈建的 300 GB 大小的 10%）

hello hello 本機層上到目前為止所需的總空間是： 240 GB + 120 GB + 330 GB = 690 GB。

其次，我們必須至少一樣多的空間 hello 本機層上為 hello 最大的單一保留區。 萬一您需要 toorestore 從雲端快照集，則會使用此額外的容量。 在此範例中，hello 最大的本機保留項目會 330 GB （包括檔案系統的保留項目），因此您會加入該 toohello 690 GB: 690 GB + 330 GB = 1020 GB。
如果我們執行後續其他還原時，我們可以永遠釋出 hello 空間 hello 先前的還原作業。

第三步，我們需要 15%的總本機空間為止 toostore 本機快照集，以便只有 85%的可用。 在此範例中，這大約是 1020 GB，而這等於 85% 的已佈建資料磁碟 TB。&ast; 因此，會是 hello 佈建的資料磁碟 (1020年&ast;(1/0.85)) = 1200 GB = 1.20 TB ~ 1.25 TB （四捨五入 toonearest 四分位數）

將非預期的成長和新的還原作業考慮進來後，您應該佈建大約 1.25 - 1.5 TB 的本機磁碟。

> [!NOTE]
> 我們也建議在精簡佈建該 hello 本機磁碟。 這項建議是因為您想要為五天前的 toorestore 資料時才需要 hello 還原空間。 項目層級復原可讓您 hello toorestore 資料過去五天內而不需要 hello 還原額外的空間。


#### <a name="example-2"></a>範例 2：
在您的虛擬陣列，您想 toobe 能夠

* 佈建 2 TB 的分層式磁碟區
* 佈建 300 GB 的固定在本機的磁碟區

根據 12% 的本機空間要保留給分層式磁碟區/共用，10% 要給固定在本機的磁碟區/共用的原則，我們需要

* 240 GB 的本機保留空間 (針對 2 TB 的分層式磁碟區/共用)
* 330 GB 本機固定磁碟區或共用 （新增的本機保留 toohello 佈建的 300 GB 空間的 10%）

Hello 本機層上所需的總空間是： 240 GB + 330 GB = 570 GB

最小 hello 需要還原的本機空間是 330 GB。

15%的總硬碟是使用的 toostore 快照集，以便只有 0.85 提供。 因此，hello 磁碟大小是 (900&ast;(1/0.85)) = 1.06 TB ~ 1.25 TB （四捨五入 toonearest 四分位數）

將非預期的成長考慮進來後，您可以佈建 1.25 - 1.5 TB 的本機磁碟。

### <a name="group-policy"></a>群組原則
群組原則是一種基礎結構，可讓您 tooimplement 特定組態的使用者和電腦。 群組原則設定會包含在群組原則物件 (Gpo)，也就是連結的 toohello 下列 Active Directory 網域服務 (AD DS) 容器： 站台、 網域或組織單位 (Ou)。 

如果您的虛擬陣列，已加入網域的 Gpo 可以套用的 tooit。 這些 Gpo 可以安裝應用程式，例如防毒軟體可能造成負面影響的 hello StorSimple Virtual Array hello 作業。

因此，我們建議您︰

* 確定虛擬陣列位於它自己的 Active Directory 組織單位 (OU) 中。
* 請確定群組原則物件 (Gpo) 的套用的 tooyour 虛擬陣列。 您可以禁止繼承 tooensure hello 虛擬陣列 （子節點），不會自動繼承任何現有的 Gpo 從 hello 父代。 如需詳細資訊，請移至太[禁止繼承](https://technet.microsoft.com/library/cc731076.aspx)。

### <a name="networking"></a>網路
您的虛擬陣列的 hello 網路組態是透過 hello 本機 web UI。 在虛擬網路介面已啟用透過 hello hypervisor hello 虛擬陣列已佈建。 使用 hello[網路設定](storsimple-virtual-array-deploy3-fs-setup.md)頁面 tooconfigure hello 虛擬網路介面 IP 位址、 子網路和閘道。  您也可以設定為您的裝置 hello 主要和次要 DNS 伺服器、 時間設定，以及選擇性的 proxy 設定。 大部分的 hello 網路組態是一次設定。 檢閱 hello[網路需求的 StorSimple](storsimple-ova-system-requirements.md#networking-requirements)先前 toodeploying hello 虛擬陣列。

在部署虛擬陣列時，建議您遵循下列最佳作法︰

* 請確定在哪一個 hello 虛擬陣列一律會部署該 hello 網路有 hello 容量 toodedicate 5 Mbps 網際網路頻寬 （或以上）。
  
  * 網際網路頻寬需求會根據您的工作負載特性和 hello 資料變更率而有所不同。
  * hello 可以處理的資料變更是與呈現直接正比 tooyour 網際網路頻寬。 舉例來說，在進行備份時，5 Mbps 的頻寬可以在 8 小時內應付大約 18 GB 的資料變更。 頻寬大 4 倍時 (20 Mbps)，則可以處理大 4 倍的資料變更 (72 GB)。
* 確認連線 toohello 網際網路永遠存在。 斷斷續續或不可靠網際網路連線 toohello 裝置可能會導致不支援的組態，並可能依法 hello 雲端中存取 toodata 遺失。
* 如果您計劃 toodeploy iSCSI 伺服器為您的裝置：
  
  * 我們建議您停用 hello**自動取得 IP 位址**選項 (DHCP)。
  * 設定靜態 IP 位址。 您必須設定主要和次要 DNS 伺服器。
  * 如果您的虛擬陣列上定義多個網路介面，僅 hello 第一個網路介面 (根據預設，這個介面是**乙太網路**) 可達到 hello 雲端。 toocontrol hello 類型的流量，您可以在您的虛擬陣列 （設定為 iSCSI 伺服器） 上建立多個虛擬網路介面，並連接這些介面 toodifferent 子網路。
* toothrottle hello 雲端頻寬只 （hello 虛擬陣列所使用），設定節流設定 hello 路由器或 hello 防火牆上。 如果您定義您的 hypervisor 中節流，它將會節流所有 hello 通訊協定包括 iSCSI 和 SMB，而不只 hello 雲端頻寬。
* 確定 Hypervisor 的時間同步處理會啟用。 如果使用 HYPER-V，hello HYPER-V 管理員中選取您的虛擬陣列，請移至太**設定&gt;Integration Services**，並確定該 hello**時間同步化**已核取。

### <a name="storage-accounts"></a>儲存體帳戶
StorSimple Virtual Array 可與單一儲存體帳戶相關聯。 這個儲存體帳戶可能是自動產生的儲存體帳戶，帳戶在 hello 與 hello 服務或儲存體帳戶相同的訂閱相關 tooanother 訂用帳戶。 如需詳細資訊，請參閱如何太[管理儲存體帳戶的虛擬陣列](storsimple-virtual-array-manage-storage-accounts.md)。

使用 hello 遵循您的虛擬陣列與相關聯的儲存體帳戶的建議。

* 連結時使用單一儲存體帳戶的多個虛擬陣列，納入 hello 的最大容量 (64 TB) 的虛擬陣列和 hello 的大小上限 500 TB 的儲存體帳戶。 這會限制 hello 數目的完整大小的虛擬陣列，可以使用該儲存體帳戶 tooabout 7 相關聯。
* 建立新的儲存體帳戶時
  
  * 我們建議您建立它 hello 區域最接近 toohello 遠端總公司/分公司辦公室您 StorSimple Virtual Array 其中是已部署的 toominimize 延遲。
  * 請記住，您無法跨不同區域移動儲存體帳戶。 同時，您無法跨訂用帳戶移動服務。
  * 使用實作 hello 資料中心之間的備援儲存體帳戶。 異地備援儲存體 (GRS)、區域備援儲存體 (ZRS) 和本地備援儲存體 (LRS) 皆支援與虛擬陣列搭配使用。 如需 hello 不同類型的儲存體帳戶的詳細資訊，請移至太[Azure 儲存體複寫](../storage/common/storage-redundancy.md)。

### <a name="shares-and-volumes"></a>共用和磁碟區
若 StorSimple Virtual Array 設定為檔案伺服器，您可以佈建共用，若設定為 iSCSI 伺服器，則可以佈建磁碟區。 hello 建立共用與磁碟區的最佳作法被相關 toohello 大小和 hello 類型設定。

#### <a name="volumeshare-size"></a>磁碟區/共用大小
若虛擬陣列設定為檔案伺服器，您可以在上面佈建共用，若設定為 iSCSI 伺服器，則可以在上面佈建磁碟區。 hello 建立共用與磁碟區的最佳作法和方面 toohello 大小 hello 設定類型。 

請注意 hello 佈建共用或虛擬裝置上的磁碟區時，下列最佳作法。

* hello 檔案大小的階層式共用的相對 toohello 佈建大小會影響 hello 階層處理效能。 使用大型檔案可能會導致緩慢分層輸出。當使用大型檔案，我們建議您該 hello 最大檔案為小於 3 hello 共用大小的百分比。
* 16 的磁碟區/共用最多可以建立 hello 虛擬陣列上。 Hello 大小限制的 hello 本機釘選與分層磁碟區/共用，會參考 toohello [StorSimple Virtual Array 限制](storsimple-ova-limits.md)。
* 建立磁碟區時，在 hello 預期資料耗用量，以及未來的成長因數。 無法將稍後擴充 hello 磁碟區。
* 一旦建立 hello 磁碟區之後，就無法縮小 hello 的 hello StorSimple 磁碟區的大小。
* Hello 磁碟區的資料達到特定的臨界值 （相對 toohello 本機保留的空間 hello 磁碟區） 時，寫入 tooa 分層磁碟區上 StorSimple、，時發生 hello IO 已節流。 繼續 toowrite toothis 磁碟區會減慢 hello IO 明顯。 雖然您可以撰寫 tooa 分層磁碟區超過其佈建的容量 （我們不要主動停止寫入 hello 佈建的容量超出 hello 使用者），您會看到有超額警示通知 toohello 效果。 一旦您看到 hello 警示，請務必您採取補救措施，例如刪除 hello 大量資料 （磁碟區目前不支援展開）。
* 災害復原使用案例中，可允許的共用/磁碟區的 hello 數目是 16，最大的 hello 共用/磁碟區數目可平行處理也是 16，hello 共用/磁碟區的數目並沒有關係到您的 RPO 和 Rto。

#### <a name="volumeshare-type"></a>磁碟區/共用類型
StorSimple 支援 hello 使用量為基礎的兩個磁碟區/共用類型： 在本機固定和階層。 本機固定磁碟區/共用以佈建而 hello 分層磁碟區/共用精簡佈建。 您無法將本機固定磁碟區/共用 tootiered 轉換或*反之亦然*一次建立。

我們建議您實作下列最佳作法設定 StorSimple 磁碟區/共用時的 hello:

* 識別您在建立磁碟區之前想 toodeploy hello 工作負載為基礎的 hello 磁碟區類型。 對於需要確保資料位於本機 (即使在雲端中斷的期間) 以及需要低雲端延遲的工作負載，請使用固定在本機的磁碟區。 一旦您的虛擬陣列上建立磁碟區，就無法變更 hello 磁碟區類型從本機固定 tootiered 或*反之亦然*。 例如，在部署 SQL 工作負載或裝載虛擬機器 (VM) 的工作負載時，請建立固定在本機的磁碟區；若為檔案共用工作負載，則使用分層式磁碟區。
* 在處理大型檔案的大小，請檢查 hello 較不常用的封存資料的選項。 啟用此選項時，使用較大的重複資料刪除區塊大小為 512 K tooexpedite hello 資料傳輸 toohello 雲端。

#### <a name="volume-format"></a>磁碟區格式
ISCSI 伺服器上建立 StorSimple 磁碟區之後，您需要 tooinitialize、 掛接和格式 hello 磁碟區。 Hello 連接主機 tooyour StorSimple 裝置上執行此作業。 當裝載及格式化 hello StorSimple 主機上的磁碟區時，建議您使用下列最佳作法。

* 對所有 StorSimple 磁碟區執行快速格式化。
* 在格式化 StorSimple 磁碟區時，使用 64 KB 的配置單位大小 (AUS) (預設值為 4 KB)。 hello 64 KB AUS 根據內部進行一般 StorSimple 工作負載和其他工作負載的測試。
* 當使用 hello StorSimple Virtual Array 設定為 iSCSI 伺服器，請勿使用跨距磁碟區或動態磁碟做為這些磁碟區或磁碟不支援 StorSimple。

#### <a name="share-access"></a>共用的存取
在虛擬陣列檔案伺服器上建立共用時，請遵循下列指導方針︰

* 在建立共用時，請指派使用者群組 (而非單一使用者) 來做為共用系統管理員。
* 藉由編輯 hello 共用，透過 Windows 檔案總管建立 hello 共用之後，您可以管理 hello NTFS 權限。

#### <a name="volume-access"></a>磁碟區的存取
設定您的 StorSimple Virtual Array hello iSCSI 磁碟區，時，重要 toocontrol 存取必要的地方。 toodetermine 主控伺服器可以存取磁碟區、 建立及存取控制記錄 (Acr) 關聯的 StorSimple 磁碟區。

使用下列最佳作法，當設定為 StorSimple 磁碟區的 Acr hello:

* 一律至少將一個 ACR 關聯至磁碟區。

* 指派多個 ACR tooa 磁碟區時，請確定 hello 磁碟區不一定要公開的方式，它可以由多個非叢集主機進行並行存取。 如果您已指派多個 Acr tooa 磁碟區，警告訊息快顯您 tooreview 為您的設定。

### <a name="data-security-and-encryption"></a>資料安全性與加密
您的 StorSimple Virtual Array 有資料安全性和加密功能，確保 hello 機密性和資料的完整性。 在使用這些功能時，建議您遵循下列最佳作法︰ 

* 從您的虛擬陣列 toohello 雲端傳送嗨資料之前，請定義雲端儲存體加密金鑰 toogenerate aes-256 加密。 如果您的資料是以加密的 toobegin，則不需要此金鑰。 hello 金鑰可以產生並保持在安全使用的金鑰管理系統，例如[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。
* 當設定 hello 儲存體帳戶，透過 hello StorSimple Manager 服務，請確定您啟用 hello SSL 模式 toocreate 定域機組 StorSimple 裝置與 hello 之間的網路通訊的安全通道。
* 重新產生 hello （藉由存取 hello Azure 儲存體服務） 的儲存體帳戶金鑰任何 tooaccount 定期變更 tooaccess hello 變更清單的系統管理員為基礎。
* 您的虛擬陣列上的資料壓縮，然後傳送 tooAzure 之前進行重複資料刪除。 我們不建議使用 Windows Server 主機上的 hello 重複資料刪除 」 角色服務。

## <a name="operational-best-practices"></a>作業的最佳作法
hello 操作的最佳作法是在 hello 日常管理或 hello 虛擬陣列的作業期間，應遵循的指導方針。 這些做法涵蓋的特定管理工作，例如進行備份，還原從備份組、 執行容錯移轉，請停用及刪除 hello 陣列，監視系統使用量和健全狀況，並對您的虛擬陣列執行病毒掃描。

### <a name="backups"></a>備份
有兩種 toohello 雲端備份您的虛擬陣列上 hello 資料，預設值自動 hello 整個裝置啟動 22:30，或透過手動指定備份的每日備份。 根據預設，hello 裝置會自動建立所有 hello 資料位於其上的每日雲端快照的集。 如需詳細資訊，請移至太[備份您的 StorSimple Virtual Array](storsimple-virtual-array-backup.md)。

hello 頻率和保留 hello 預設備份相關聯無法變更，但您可以設定每日備份會在哪一個 hello 起始每天 hello 時間。 當設定 hello hello 的開始時間自動備份時，我們建議：

* 將備份排程在離峰時間。 備份開始時間不應該與大量主機 IO 一致。
* 起始手動視備份計劃 tooperform 裝置容錯移轉或先前 toohello 維護視窗中，您的虛擬陣列上 tooprotect hello 資料。

### <a name="restore"></a>還原
您可以還原的備份組有兩種： 還原 tooanother 磁碟區或共用，或執行項目層級復原 （只適用於設定為檔案伺服器的虛擬陣列）。 項目層級復原可讓您從雲端備份所有 hello 共用的檔案和資料夾的精細復原 toodo hello StorSimple 裝置上。 如需詳細資訊，請移至太[從備份還原](storsimple-virtual-array-clone.md)。

在執行還原時，請記住的指導方針的 hello:

* StorSimple Virtual Array 不支援就地還原。 不過可能隨時可以達成兩步驟程序： hello 虛擬上的空間陣列，然後再還原 tooanother 磁碟區/共用。
* 從本機磁碟區還原時，請記得 hello 還原將會是長時間執行的作業。 雖然 hello 磁碟區可能會快速上線，請繼續 toobe hydrated hello 背景 hello 資料。
* 會維持為磁碟區類型 hello hello 相同 hello 還原程序。 還原為分層磁碟區 tooanother 分層磁碟區和本機固定磁碟區 tooanother 固定在本機磁碟區。
* 當嘗試 toorestore，磁碟區或備份組，從共用 hello 還原作業失敗時，目標磁碟區或共用仍可能在 hello 入口網站中建立。 請務必您刪除這個未使用的目標磁碟區或共用的 hello 入口 toominimize 從這個項目造成任何未來問題。

### <a name="failover-and-disaster-recovery"></a>容錯移轉和災害復原
裝置容錯移轉可讓您 toomigrate 資料由*來源*裝置 hello datacenter tooanother*目標*裝置位於 hello 相同或不同的地理位置。 hello 裝置容錯移轉是 hello 整個裝置。 容錯移轉期間，hello hello 來源裝置的雲端資料會變更擁有權 toothat 的 hello 目標裝置。

為 StorSimple 虛擬陣列，您只能容錯移轉 tooanother 虛擬陣列受 hello 相同 StorSimple Manager 服務。 不允許容錯移轉 tooan 8000 系列裝置或不同的 StorSimple Manager 服務 （比 hello 一個 hello 來源裝置) 所管理的陣列。 進一步了解 hello 容錯移轉的考量，toolearn 移過[hello 裝置容錯移轉的必要條件](storsimple-virtual-array-failover-dr.md)。

當您的虛擬陣列，透過執行失敗，請記住 hello 下列：

* 規劃的容錯移轉，就是建議的最佳作法 tootake 所有 hello 磁碟區/共用離線先前 tooinitiating hello 容錯移轉。 請遵循 hello 作業系統特定指示 tootake hello 磁碟區/共用離線 hello 上裝載第一次，然後採取那些離線虛擬裝置上。
* 檔案伺服器嚴重損壞修復 (DR)，我們建議您加入 hello 目標裝置 toohello hello 來源的 hello 共用權限，以便與相同的網域會自動解決。 只有 hello 的 hello 這個版本支援相同的網域中的容錯移轉 tooa 目標裝置。
* Hello DR 成功完成後，會自動刪除 hello 來源裝置。 Hello 裝置已無法再使用，雖然 hello 您 hello 主機系統佈建的虛擬機器仍然會消耗資源。 我們建議您刪除此虛擬機器從您的主機系統 tooprevent 從持任何費用。
* 請注意，即使 hello 容錯移轉不成功， **hello 資料永遠處於安全 hello 雲端**。 請考慮下列三個案例中的 hello 容錯移轉未順利完成的 hello:
  
  * Hello 的 hello 容錯移轉，例如當 hello DR 預先檢查正在執行的初始階段中發生失敗。 在此情況下，目標裝置仍可使用。 您可以重試 hello hello 容錯移轉相同的目標裝置。
  * 在 hello 實際容錯移轉程序期間發生失敗。 在此情況下，hello 目標裝置是標示為無法使用。 您必須佈建並設定另一個目標虛擬陣列，以用於容錯移轉。
  * hello 的容錯移轉已完成之後已刪除的 hello 來源裝置但 hello 目標裝置有問題，您無法存取任何資料。 hello 仍然安全 hello 雲端中及資料可以輕鬆地擷取建立另一個虛擬的陣列，然後用它來作為 hello DR 的目標裝置。

### <a name="deactivate"></a>停用
當您停用 StorSimple Virtual Array 時，但您伺服器 hello hello 裝置與之間連線 hello 相對應的 StorSimple Manager 服務。 停用是 **永久性** 作業，而且無法復原。 已停用的裝置無法向 StorSimple Manager 服務的 hello 一次。 如需詳細資訊，請移至太[停用及刪除您的 StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md)。

請注意下列最佳作法，請注意，停用您的虛擬陣列時的 hello:

* 取得所有 hello 資料先前 toodeactivating 虛擬裝置的雲端快照。 當您停用虛擬陣列時，所有的 hello 本機裝置資料將會遺失。 建立雲端快照可讓您 toorecover 資料在後續階段。
* 您停用 StorSimple Virtual Array 之前，請確定 toostop 或刪除用戶端和相依於該裝置的主機。
* 刪除不再使用的已停用裝置，以免它產生費用。

### <a name="monitoring"></a>監視
tooensure StorSimple 虛擬陣列處於連續的狀況良好狀態，您需要 toomonitor hello 陣列，並確定您從包括警示的 hello 系統接收資訊。 toomonitor hello hello 虛擬陣列，實作下列最佳作法的 hello 的整體健全狀況：

* 設定您的虛擬陣列資料磁碟以及 hello OS 磁碟監視 tootrack hello 磁碟使用量。 如果執行 HYPER-V，您可以使用 System Center Virtual Machine Manager (SCVMM) 和 System Center Operations Manager (SCOM) toomonitor 多種虛擬化主機。
* 您的虛擬陣列 toosend 警示具備特定的使用量層級上設定電子郵件通知。                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>索引搜尋和病毒掃描應用程式
StorSimple Virtual Array 可以自動層 hello 本機層 toohello Microsoft Azure 雲端的資料。 使用的 tooscan hello 資料儲存在 StorSimple 上的應用程式，例如索引搜尋或病毒掃描時，您會需要 tootake 照顧，hello 雲端資料不會取得存取和提取回 toohello 本機層。

我們建議您實作下列最佳作法，在您的虛擬陣列上設定 hello 索引搜尋或病毒掃描時 hello:

* 停用任何自動設定的完整掃描作業。
* 對於分層磁碟區，設定 hello 索引搜尋或病毒掃描應用程式 tooperform 累加的掃描。 這會掃描只 hello 新資料可能位於 hello 本機層上。 階層式的 toohello 雲端的 hello 資料才能累加作業期間存取。
* 請確定 hello 正確的搜尋篩選和設定，以便取得掃描只有 hello 預期類型的檔案。 例如，影像檔 （JPEG、 GIF 和 TIFF） 和工程繪圖應該不會掃描在 hello 累加或完整索引重建期間。

如果使用 Windows 索引程序，請遵循下列指導方針︰

* 請勿使用 hello Windows 索引子階層式磁碟區，因為它需要經常重建 toobe hello 索引回收大量的資料 (TBs) 從 hello 雲端。 重建 hello 索引會擷取所有的檔案類型 tooindex 其內容。
* 使用 hello Windows 索引本機固定磁碟區的程序，因為這只會存取 hello 本機層 toobuild hello 索引 （hello 雲端將無法存取資料） 上的資料。

### <a name="byte-range-locking"></a>位元組範圍鎖定
應用程式可以將指定的位元組範圍鎖定 hello 檔案中。 如果要撰寫 tooyour StorSimple hello 應用程式上啟用位元組範圍鎖定，然後分層不適用於您的虛擬陣列。 Hello 分層 toowork，所有區域的存取 hello 檔案都應該解除鎖定。 虛擬陣列上的分層式磁碟區不支援位元組範圍鎖定。

建議使用 tooalleviate 位元組範圍鎖定包括量值：

* 關閉應用程式邏輯中的位元組範圍鎖定。
* 使用本機固定磁碟區 （而不是階層） hello 與此應用程式相關聯的資料。 本機固定磁碟區無法到 hello 雲端層。
* 當使用本機固定磁碟區的位元組範圍鎖定已啟用時，hello 磁碟區可以上線之前 hello 還原已完成。 在這些情況下，您必須等候 hello 還原 toobe 完成。

## <a name="multiple-arrays"></a>多個陣列
多個虛擬陣列可能需要部署 toobe tooaccount 持續成長的工作集無法溢出到 hello 雲端，因此會影響 hello 裝置 hello 效能上的資料。 在這些情況下，它會是最佳 tooscale 裝置隨著 hello 工作集。 這需要在 hello 在內部部署資料中心新增一或多個裝置 toobe。 加入時 hello 裝置，您可以：

* 分割 hello 目前設定的資料。
* 部署新的工作負載 toonew 裝置。
* 如果部署多個虛擬陣列，我們建議最好讓從負載平衡的觀點而言，分配不同 hypervisor 主機中的 hello 陣列。
* 分散式檔案系統命名空間中可以部署多個虛擬陣列 (設定為檔案伺服器或 iSCSI 伺服器時)。 如需詳細步驟，請移太[混合式雲端儲存體部署指南與分散式檔案系統命名空間方案](https://www.microsoft.com/download/details.aspx?id=45507)。 分散式的檔案系統複寫目前不建議用於 hello 虛擬陣列。 

## <a name="see-also"></a>另請參閱
了解如何太[管理您的 StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md)透過 hello StorSimple Manager 服務。

