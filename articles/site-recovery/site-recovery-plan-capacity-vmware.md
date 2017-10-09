---
title: "aaaPlan 容量與縮放比例的 VMware 複寫 tooAzure 與 Azure Site Recovery |Microsoft 文件"
description: "當複寫與 Azure Site Recovery 的 VMware Vm tooAzure 時使用此發行項 tooplan 容量和小數位數"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>使用 Azure Site Recovery 規劃容量並調整 Azure 中的 VMware 複寫

使用容量規劃和調整，當複寫在內部部署 VMware Vm 和實體伺服器 tooAzure 與此發行項 toofigure [Azure Site Recovery](site-recovery-overview.md)。

## <a name="how-do-i-start-capacity-planning"></a>如何開始容量規劃？

複寫環境資訊，請執行蒐集 hello [Azure 站台復原部署規劃](https://aka.ms/asr-deployment-planner-doc)VMware 複寫。 [深入了解](site-recovery-deployment-planner.md) 此工具。 您可收集相容與不相容 VM、每個 VM 的磁碟，以及每個磁碟的資料變換等相關資訊。 網路頻寬需求和 hello 順利進行複寫和測試容錯移轉所需的 Azure 基礎結構，同時也包含 hello 工具。

## <a name="capacity-considerations"></a>容量考量

**元件** | **詳細資料** |
--- | --- | ---
**複寫** | **每日最大的變更率：**受保護的電腦只能使用一個處理序伺服器，而且單一處理序伺服器可以處理每日的變更率向上 too2 TB。 因此 2 TB 為 hello 最大的每日資料變更率支援的受保護的機器。<br/><br/> **最大輸送量：**複寫的機器可以隸屬 tooone 在 Azure 中的儲存體帳戶。 標準儲存體帳戶可以處理最多 20,000 每秒的要求，並建議來源機器 too20 000 維持 hello 輸入/輸出作業每秒 (IOPS) 數目。 例如，如果您有使用 5 磁碟時，來源電腦，而且每個磁碟會產生 hello 來源電腦上的 120 IOPS （8 千個大小），表示它會在每個磁碟的 IOPS 限制為 500 hello Azure 內。 （儲存體帳戶所需的 hello 數目是等於 toohello 總來源機器 IOPS，除以 20000）。
**組態伺服器** | hello 組態伺服器應該可以 toohandle hello 每日變更速率容量跨所有受保護的機器上執行的工作負載而且需要足夠的頻寬 toocontinuously 複寫資料 tooAzure 儲存體。<br/><br/> 最佳做法，找出 hello 組態伺服器 hello 上相同的網路和區域網路區段，做為 hello 想 tooprotect 機器。 它可以位於不同的網路，但您想 tooprotect 應該有層級 3 網路可見性 tooit 機器上。<br/><br/> Hello 組態伺服器的大小建議將摘要列出 hello 之後 > 一節中的 hello 資料表中。
**處理序伺服器** | hello 組態伺服器上預設會安裝第一個處理序伺服器 hello。 您可以部署額外的處理序伺服器 tooscale 您的環境。 <br/><br/> hello 處理序伺服器接收複寫資料從受保護的機器，並最佳化與快取、 壓縮和加密。 然後它會傳送 hello 資料 tooAzure。 hello 處理序伺服器的電腦應該有足夠的資源 tooperform 這些工作。<br/><br/> hello 處理序伺服器會使用以磁碟為基礎的快取。 使用不同的快取磁碟 600 GB 或更多的 toohandle 資料變更，儲存在網路瓶頸後或中斷 hello 事件。

## <a name="size-recommendations-for-hello-configuration-server"></a>Hello 組態伺服器的大小建議

**CPU** | **記憶體** | **快取磁碟大小** | **資料變更率** | **受保護的機器**
--- | --- | --- | --- | ---
8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz) | 16 GB | 300 GB | 500 GB 或更少 | 複寫少於 100 部機器。
12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz) | 18 GB | 600 GB | 500 GB too1 TB | 複寫 100-150 部機器。
16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz) | 32 GB | 1 TB | 1 TB too2 TB | 複寫 150-200 部機器。
部署另一個處理序伺服器 | | | > 2 TB | 如果您要複寫 200 個以上的機器，或如果 hello 每日資料變更速率超過 2TB，請部署額外的處理序伺服器。

其中：

* 每個來源機器已設定各 100 GB 的 3 個磁碟。
* 我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。

## <a name="size-recommendations-for-hello-process-server"></a>大小建議 hello 之處理序伺服器

如果您需要 tooprotect 200 個以上的機器，或每日變更率 hello 大於 2 TB，您可以加入處理序伺服器 toohandle hello 複寫載入。 tooscale 外的，您可以：

* 增加 hello 組態伺服器的數目。 例如，您可以保護 too400 機器組態，兩台伺服器上。
* 新增更多的處理序伺服器，並使用這些 toohandle 流量，而不是 （或其他） hello 組態伺服器。

hello 下表描述的案例：

* 您不打算 toouse hello 組態伺服器的處理序伺服器。
* 您已設定額外的處理序伺服器。
* 您已設定受保護的虛擬機器 toouse hello 額外的處理序伺服器。
* 每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。

**組態伺服器** | **額外處理序伺服器** | **快取磁碟大小** | **資料變更率** | **受保護的機器**
--- | --- | --- | --- | ---
8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體 | 4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體 | 300 GB | 250 GB 或更少 | 複寫 85 部或更少的機器。
8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體 | 8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體 | 600 GB | 250 GB too1 TB | 複寫 85-150 部機器。
12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，18 GB 記憶體 | 12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體 | 1 TB | 1 TB too2 TB | 複寫 150-225 部機器。

您可以在其中調整您的伺服器 hello 方式取決於您的喜好設定的向上延展或向外延展模型。  您部署幾個高階組態和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。 比方說，如果您需要 tooprotect 220 機器，您可以執行 hello 下列其中一項：

* 設定 hello 12 vCPU、 18 GB 的記憶體，與 12 vCPU、 24 GB 的記憶體的額外的處理序伺服器的組態伺服器。 設定受保護的機器 toouse hello 只用於其他處理序伺服器。
* 設定兩個組態伺服器 （2 x 8 vCPU、 16 GB 的 RAM） 和兩個額外的處理序伺服器 （1 x 8 vCPU 和 4 vCPU x 1 toohandle 135 + 85 [220] 機器）。 設定受保護的機器 toouse hello 只用於其他處理序伺服器。


## <a name="control-network-bandwidth"></a>控制網路頻寬

您已使用 hello 之後[hello 部署規劃工具](site-recovery-deployment-planner.md)，您必須複寫 （hello 初始複寫，然後差異） toocalculate hello 頻寬，您可以控制 hello 用於使用兩個複寫的頻寬量選項：

* **節流的頻寬**： 複寫 tooAzure VMware 流量通過特定處理序伺服器。 您可以將做為處理序伺服器 hello 機器上的頻寬節流處理。
* **影響頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬：
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM**登錄值會指定 hello 磁碟的資料傳輸 （初始或差異複寫） 所使用的執行緒數目。 較高的值會增加 hello 網路頻寬用於複寫。
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM**指定 hello 容錯回復期間用來傳送資料的執行緒數目。

### <a name="throttle-bandwidth"></a>節流頻寬

1. 開啟 Azure 備份 MMC 嵌入式管理單元在 hello 機器採取行動的 hello hello 處理序伺服器。 根據預設，備份的捷徑可在 hello 桌面上或 hello 下列資料夾中： C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin。
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。

    ![Azure 備份 MMC 螢幕擷取畫面嵌入式管理單元選項 toochange 屬性](./media/site-recovery-vmware-to-azure/throttle1.png)
3. 在 hello**節流**索引標籤上，選取**啟用網際網路頻寬使用節流設定的備份操作**。 設定工作的 hello 限制和非工作小時。 有效範圍是從每秒 512 Kbps too102 Mbps。

    ![[Azure 備份屬性] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/throttle2.png)

您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。 以下是一個範例：

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 表示不需要節流。

### <a name="influence-network-bandwidth-for-a-vm"></a>影響 VM 的網路頻寬

1. 在 hello VM 的登錄中，瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。
   * tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值**UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。
   * 從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。
2. hello 預設值為 4。 在 「 超量佈建 」 的網路中，應該從 hello 預設值變更這些登錄機碼。 hello 上限為 32。 監視流量 toooptimize hello 值。


## <a name="deploy-additional-process-servers"></a>部署額外處理序伺服器

如果您有 tooscale 出您的部署超過 200 的來源機器，或您有每日變換率超過 2 TB，您會需要額外的處理序伺服器 toohandle hello 流量磁碟區。 請遵循這些指示 tooset，hello 的處理序伺服器。 設定好 hello 伺服器之後，您將移轉來源機器 toouse 它。

1. 在**站台復原伺服器**，按一下 hello 組態伺服器，然後按一下**處理序伺服器**。

    ![螢幕擷取畫面的站台復原的伺服器選項 tooadd 處理序伺服器](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. 在 [伺服器類型] 中，按一下 [處理伺服器 (內部部署)]。

    ![[處理序伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. 下載 hello Site Recovery 整合安裝程式檔案，並執行 tooinstall hello 處理序伺服器。 這也會註冊它 hello 保存庫中。
4. 在**開始之前**，選取**新增額外的處理序伺服器 tooscale 出部署**。
5. 完整的 hello 精靈在 hello 相同方式時您[設定](#step-2-set-up-the-source-environment)hello 組態伺服器。

    ![Azure Site Recovery 統一安裝精靈的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. 在**組態伺服器詳細資料**、 指定 hello 的 hello 組態伺服器上的 IP 位址和 hello 複雜密碼。 tooobtain hello 複雜密碼，執行**[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello 組態伺服器上。

    ![[組態伺服器詳細資料] 頁面的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>移轉機器 toouse hello 新處理序伺服器
1. 在**設定** > **站台復原伺服器**，按一下 hello 組態伺服器上，然後展開**處理伺服器**。

    ![[處理序伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. 目前使用中的 hello 處理序伺服器上按一下滑鼠右鍵，然後按一下**交換器**。

    ![[組態伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. 在**選取目標處理序伺服器**，請選取該 hello 伺服器將處理 hello 新處理序伺服器，toouse，然後再選取 hello 虛擬機器。 按一下 hello 資訊圖示 tooget hello 伺服器資訊。 toohelp 您進行載入決策，hello 平均 tooreplicate 會顯示每個選取的虛擬機器 toohello 新處理序伺服器所需的空間。 按一下 hello 核取記號 toostart 複寫 toohello 新處理序伺服器。


## <a name="next-steps"></a>後續步驟

下載並執行 hello [Azure 站台復原部署規劃](https://aka.ms/asr-deployment-planner)
