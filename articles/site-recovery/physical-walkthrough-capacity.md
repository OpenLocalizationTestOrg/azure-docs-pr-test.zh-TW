---
title: "aaaPlan 容量與縮放比例為實體伺服器複寫 tooAzure 與 Azure Site Recovery |Microsoft 文件"
description: "複寫 Windows/Linux 實體伺服器 tooAzure 與 Azure Site Recovery 時使用此發行項 tooplan 容量和小數位數"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>步驟 3： 規劃容量和調整實體伺服器 tooAzure 複寫

使用容量出此發行項 toofigure 和縮放功能，當您要複寫在內部部署與 Windows/Linux 實體伺服器 tooAzure [Azure Site Recovery](site-recovery-overview.md)。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="plan-deployment-capacity"></a>規劃部署容量

1. 請閱讀本[文章](site-recovery-plan-capacity-vmware.md)toolearn 有關評估複寫需求和指導方針縮放站台復原元件。
2. 閱讀下方關於調整的伺服器元件，以及控制複寫的機器頻寬 toolearn hello 考量。

## <a name="replication-considerations"></a>複寫考量

使用複寫的伺服器需求出這些考量 toofigure。

**元件** | **詳細資料** 
--- | --- 
**複寫** | **每日最大的變更率：**受保護的電腦只能使用一個處理序伺服器，而且單一處理序伺服器可以處理每日的變更率向上 too2 TB。 因此 2 TB 為 hello 最大的每日資料變更率支援的受保護的機器。<br/><br/> **最大輸送量：**複寫的機器可以隸屬 tooone 在 Azure 中的儲存體帳戶。 標準儲存體帳戶可以處理最多 20,000 每秒的要求，並建議來源機器 too20 000 維持 hello 輸入/輸出作業每秒 (IOPS) 數目。 例如，如果您有使用 5 磁碟時，來源電腦，而且每個磁碟會產生 hello 來源電腦上的 120 IOPS （8 千個大小），表示它會在每個磁碟的 IOPS 限制為 500 hello Azure 內。 （儲存體帳戶所需的 hello 數目是等於 toohello 總來源機器 IOPS，除以 20000）。

## <a name="configuration-server-capacity"></a>組態伺服器容量

hello 組態伺服器應該可以 toohandle hello 每日變更速率容量跨所有受保護的機器上執行的工作負載而且需要足夠的頻寬 toocontinuously 複寫資料 tooAzure 儲存體。

最佳做法，找出 hello 組態伺服器 hello 上相同的網路和區域網路區段，做為 hello 想 tooprotect 機器。 它可以位於不同的網路，但您想 tooprotect 應該有層級 3 網路可見性 tooit 機器上。

## <a name="sizing-recommendations"></a>大小調整建議

hello 表格摘要說明根據 CPU 調整建議。

**CPU** | **記憶體** | **快取磁碟大小** | **資料變更率** | **受保護的機器**
--- | --- | --- | --- | ---
8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz) | 16 GB | 300 GB | 500 GB 或更少 | 複寫少於 100 部機器。
12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz) | 18 GB | 600 GB | 500 GB too1 TB | 複寫 100-150 部機器。
16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz) | 32 GB | 1 TB | 1 TB too2 TB | 複寫 150-200 部機器。
部署另一個處理序伺服器 | | | > 2 TB | 如果您要複寫 200 個以上的機器，或如果 hello 每日資料變更速率超過 2TB，請部署額外的處理序伺服器。

其中：

* 每個來源機器已設定各 100 GB 的 3 個磁碟。
* 我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。

## <a name="process-server-capacity"></a>處理伺服器容量


hello 處理序伺服器接收複寫資料從受保護的機器，並最佳化與快取、 壓縮和加密。 然後它會傳送 hello 資料 tooAzure。

- hello 處理序伺服器的電腦應該有足夠的資源 tooperform 這些工作。
- hello 組態伺服器上預設會安裝第一個處理序伺服器 hello。 您可以部署額外的處理序伺服器 tooscale 您的環境。
- hello 處理序伺服器會使用以磁碟為基礎的快取。 使用不同的快取磁碟 600 GB 或更多的 toohandle 資料變更，儲存在網路瓶頸後或中斷 hello 事件。
- 如果您需要 tooprotect 200 個以上的機器，或每日變更率 hello 大於 2 TB，您可以加入處理序伺服器 toohandle hello 複寫載入。 tooscale 外的，您可以：
    - 增加 hello 組態伺服器的數目。 例如，您可以保護 too400 機器組態，兩台伺服器上。
    - 新增更多的處理序伺服器，並使用這些 toohandle 流量，而不是 （或其他） hello 組態伺服器。


### <a name="example-process-server-scaling"></a>範例處理伺服器調整

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

## <a name="deploy-additional-process-servers"></a>部署額外處理序伺服器

1. 請遵循[這些指示](site-recovery-vmware-setup-azure-ps-resource-manager.md)tooset 額外的處理序伺服器。
2. 如果您沒有 hello 複雜密碼，執行**[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello 組態伺服器 tooget 上它。
3. 設定好 hello 處理序伺服器之後，您將移轉來源機器 toouse 它。

    1. 在**設定** > **站台復原伺服器**，按一下 hello 組態伺服器 >**處理伺服器**。
    2. 目前使用中的，以滑鼠右鍵按一下 hello 處理序伺服器 >**交換器**。
    3. 在**選取目標處理序伺服器**，請選取該 hello 伺服器將處理 toouse，再選取 hello Vm hello 處理序伺服器。
    4. 按一下 hello 資訊圖示。 toohelp 您進行載入決策，hello 平均 tooreplicate 會顯示每個選取的 VM toohello 新處理序伺服器所需的空間。
    5. 按一下 hello 核取記號 toostart 複寫 toohello 新處理序伺服器。

## <a name="control-network-bandwidth"></a>控制網路頻寬

當您執行[hello 部署規劃工具](site-recovery-deployment-planner.md)，您必須複寫 （hello 初始複寫，然後差異） toocalculate hello 頻寬，您可以控制 hello 數量所使用頻寬的複寫使用幾個選項：

* **節流的頻寬**： 複寫 tooAzure VMware 流量通過特定處理序伺服器。 您可以將做為處理序伺服器 hello 機器上的頻寬節流處理。
* **影響頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬：
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM**登錄值會指定 hello 磁碟的資料傳輸 （初始或差異複寫） 所使用的執行緒數目。 較高的值會增加 hello 網路頻寬用於複寫。
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM**指定 hello 容錯回復期間用來傳送資料的執行緒數目。

### <a name="throttle-bandwidth"></a>節流頻寬

1. 開啟 Azure 備份 MMC 嵌入式管理單元在 hello 機器採取行動的 hello hello 處理序伺服器。 根據預設，備份的捷徑可在 hello 桌面上或 hello 下列資料夾中： C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin。
2. 在 hello 嵌入式管理單元，按一下 **變更屬性**。
3. 在 hello**節流**索引標籤上，選取**啟用網際網路頻寬使用節流設定的備份操作**。
4. 設定工作的 hello 限制和非工作小時。 有效範圍是從每秒 512 Kbps too102 Mbps。

    ![節流](./media/physical-walkthrough-capacity/throttle2.png)

您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。 以下是一個範例：

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 表示不需要節流。

### <a name="influence-network-bandwidth-for-a-vm"></a>影響 VM 的網路頻寬

1. 在登錄中的 hello VM，請移過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。
   * tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值**UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。
   * 從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。
2. hello 預設值為 4。 在過度佈建的網路中，應該修改這些登錄機碼。 hello 上限為 32。 監視流量 toooptimize hello 值。




## <a name="next-steps"></a>後續步驟

跳過[步驟 4： 規劃網路](physical-walkthrough-network.md)。
