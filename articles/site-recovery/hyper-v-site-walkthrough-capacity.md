---
title: "aaaPlan 容量與縮放比例為 HYPER-V 虛擬機器與 Azure Site Recovery 的複寫 （無 VMM) tooAzure |Microsoft 文件"
description: "當複寫與 Azure Site Recovery 的 HYPER-V Vm tooAzure 時使用此發行項 tooplan 容量和小數位數"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a>步驟 3： 規劃容量和調整 HYPER-V tooAzure 複寫

使用容量規劃和調整，當複寫與在內部部署 HYPER-V Vm （不含 System Center VMM) tooAzure 出此發行項 toofigure [Azure Site Recovery](site-recovery-overview.md)。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="how-do-i-start-capacity-planning"></a>如何開始容量規劃？


您收集資訊的複寫環境，並規劃容量使用這項資訊，以及在本文中反白顯示 hello 考量。


## <a name="gather-information"></a>收集資訊

1. 收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。
2. 識別複寫資料的每日變更 (流失) 率。 下載 hello [HYPER-V 容量規劃工具](https://www.microsoft.com/download/details.aspx?id=39057)tooget hello 變更率。 我們建議您執行此工具透過週 toocapture 平均值。
 

## <a name="figure-out-capacity"></a>找出產能

根據已收集的 hello 資訊，您執行 hello[站台復原產能規劃工具](http://aka.ms/asr-capacity-planner-excel)tooanalyze 您的來源環境和工作負載，估計頻寬需求和伺服器 hello 來源位置，資源和 hello資源 （虛擬機器和存放裝置等等），您需要在 hello 目標位置。 您可以透過幾種模式來執行 hello 工具：

- 快速的計劃： hello 工具以此模式執行的 tooget 網路和伺服器投影根據 Vm、 磁碟、 存放裝置和變更速率平均數目。
- 詳細的規劃： 在此模式中，執行 hello 工具，並提供每個工作負載在 VM 層級的詳細資料。 分析 VM 相容性，並取得網路和伺服器預測。

現在執行 hello 工具：

1. 下載 hello[工具](http://aka.ms/asr-capacity-planner-excel)
2. toorun hello 快速規劃中，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-quick-planner)，並選取 hello 案例**HYPER-V tooAzure**。
3. toorun hello 詳細的規劃，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-detailed-planner)，並選取 hello 案例**HYPER-V tooAzure**。

## <a name="control-network-bandwidth"></a>控制網路頻寬

您需要的導出的 hello 頻寬之後，您會有幾個選項用於複寫的頻寬控制 hello 量：

* **節流的頻寬**: HYPER-V 複寫 tooAzure 流量透過特定的 HYPER-V 主機。 您可以節流處理 hello 主機伺服器上的頻寬。
* **影響頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬。

### <a name="throttle-bandwidth"></a>節流頻寬
1. 開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機伺服器上。 依預設 Microsoft Azure 備份的捷徑。 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin
2. 在 [hello] 嵌入式管理單元中按一下**變更屬性**。
3. 在 hello**節流**索引標籤上選取**啟用網際網路頻寬使用節流設定的備份操作**，並設定工作的 hello 限制和非工作小時。 有效範圍是從每秒 512 Kbps too102 Mbps。

    ![節流頻寬](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

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

跳過[步驟 4： 規劃網路](hyper-v-site-walkthrough-network.md)。
