---
title: "使用 Azure Site Recovery 進行站台間 Hyper-V 複寫的測試結果 | Microsoft Docs"
description: "本文提供使用 Azure Site Recovery 進行 Hyper-V VM 內部部署對內部部署複寫之效能測試的相關資訊。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 10/30/2017
ms.author: raynew
ms.openlocfilehash: c221fe94c5301b0a36882d5ae1c57e523002ecc4
ms.sourcegitcommit: 43c3d0d61c008195a0177ec56bf0795dc103b8fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/01/2017
---
# <a name="test-results-for-on-premises-to-on-premises-hyper-v-replication-with-site-recovery"></a>使用 Site Recovery 進行內部部署對內部部署 Hyper-V 複寫的測試結果

您可以使用 Microsoft Azure Site Recovery 來協調和管理將虛擬機器與實體伺服器複寫至 Azure 或次要資料中心的複寫作業。 本文提供我們在兩個內部部署資料中心之間複寫 Hyper-V 虛擬機器時所執行之效能測試的結果。

## <a name="test-goals"></a>測試目標

測試目標是檢查 Azure Site Recovery 在穩定狀態複寫期間的執行情況。 當虛擬機器已完成初始複寫，且正在同步處理差異變更時，就會發生穩定狀態複寫。 請務必使用穩定狀態測量效能，因為除非發生非預期的中斷，否則它是大多數虛擬機器維持的狀態。

測試部署是由兩個內部部署網站所組成，且每個網站都有一個 VMM 伺服器。 此測試部署通常屬於總公司/分公司部署，以總公司做為主要站台，而分公司做為次要或復原站台。

## <a name="what-we-did"></a>我們執行的動作

以下是我們在測試階段中所執行的動作：

1. 使用 VMM 範本建立虛擬機器。
2. 啟動虛擬機器，並擷取 12 小時內的基準效能度量。
3. 在主要和復原 VMM 伺服器上建立雲端。
4. 在 Azure Site Recovery 中設定雲端保護，包括來源和復原雲端的對應。
5. 啟用虛擬機器的保護，並允許它們完成初始複寫。
6. 等待幾個小時讓系統趨於穩定。
7. 擷取 12 小時內的效能度量，以確保所有虛擬機器在這 12 小時內都維持在預期的複寫狀態。
8. 測量基準效能度量和複寫效能度量之間的差異。


## <a name="primary-server-performance"></a>主要伺服器效能

* Hyper-V 複本會使用主要伺服器上最小的儲存負荷，以非同步方式追蹤記錄檔的變更。
* Hyper-V 複本會利用自我維護的記憶體快取，以減少 IOPS 的追蹤負荷。 它會在記憶體中儲存對 VHDX 的寫入，並在記錄傳送至復原站台之前，將這些寫入排清到記錄檔中。 如果寫入達到預先決定的限制，也會發生磁碟排清。
* 下圖顯示複寫的穩定狀態 IOPS 負荷。 我們可以看到複寫的 IOPS 負荷大約是 5%，這相當低。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Hyper-V 複本會利用主要伺服器上的記憶體來最佳化磁碟效能。 如下圖所示，主要叢集中所有伺服器上的記憶體負荷都很低。 所顯示的記憶體負荷是複寫所使用的記憶體相較於 Hyper-V 伺服器上已安裝的記憶體總數的百分比。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Hyper-V 複本的 CPU 負荷最低。 如圖所示，複寫負荷位於 2-3% 的範圍內。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>次要 (復原) 伺服器效能

Hyper-V 複本會使用復原伺服器上的少量記憶體來最佳化儲存作業數目。 此圖形會摘要說明復原伺服器上的記憶體使用量。 所顯示的記憶體負荷是複寫所使用的記憶體相較於 Hyper-V 伺服器上已安裝的記憶體總數的百分比。

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

復原站台上的 I/O 作業量為主要站台上寫入作業數目的函數。 讓我們看看復原站台上的 I/O 作業總數與主要站台上的 I/O 作業和與寫入作業的總數的比較。 此圖顯示復原站台上的 IOPS 總數

* 大約是主要站台上寫入 IOPS 的 1.5 倍。
* 大約是主要站台上 IOPS 總數的 37%。

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>對網路使用率的影響

針對每秒 5 Gb 的現有頻寬，會在主要和復原節點 (已啟用壓縮) 之間使用平均每秒 275 Mb 的網路頻寬。

![結果網路使用率](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>對 VM 效能的影響

複寫對虛擬機器上執行的生產環境工作負載的影響是其中一個重要的考量。 如果主要站台已針對複寫適當地佈建，對工作負載應該不會有任何影響。 Hyper-V 複本的輕量型追蹤機制可確保虛擬機器中執行的工作負載在穩定狀態複寫期間不會受到影響。 下圖將就此說明。

此圖顯示啟用複寫之前和之後，執行不同工作負載的虛擬機器執行的 IOPS。 您可以觀察到兩者之間沒有差異。

![複本效果結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

下圖顯示啟用複寫之前和之後，執行不同工作負載的虛擬機器的輸送量。 您可以觀察到複寫沒有顯著的影響。

![結果複本效果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>結論

結果會清楚地顯示搭配 Hyper-V 複本的 Azure Site Recovery 透過最小的負荷，就可以為大型叢集妥善調整。  Azure Site Recovery 提供簡單的部署、複寫、管理和監視功能。 Hyper-V 複本提供成功調整複寫所需的基礎結構。 為規劃最佳的部署，建議您下載 [Hyper-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057)。

## <a name="test-environment-details"></a>測試環境詳細資料

### <a name="primary-site"></a>主要站台

* 主要站台所具備的叢集內含五部執行 470 個虛擬機器的 Hyper-V 伺服器。
* 虛擬機器執行不同的工作負載，而且全都有啟用 Azure Site Recovery 保護。
* 叢集節點的儲存體是由 iSCSI SAN 提供。 機型 – Hitachi HUS130。
* 每部叢集伺服器都有四張網路卡 (NIC)，每張網路卡各為 1 Gbps。
* 其中兩張網路卡會連線到 iSCSI 私人網路，另外兩張會連線到外部企業網路。 其中一個外部網路會保留為供叢集通訊專用。

![主要硬體需求](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| 伺服器 | RAM | 模型 | 處理器 | 處理器數目 | NIC | 軟體 |
| --- | --- | --- | --- | --- | --- | --- |
| 叢集中的 Hyper-V 伺服器： <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25 具備 256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| VMM 伺服器 |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>次要 (復原) 站台

* 次要站台有六個節點的容錯移轉叢集。
* 叢集節點的儲存體是由 iSCSI SAN 提供。 機型 – Hitachi HUS130。

![主要硬體規格](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| 伺服器 | RAM | 模型 | 處理器 | 處理器數目 | NIC | 軟體 |
| --- | --- | --- | --- | --- | --- | --- |
| 叢集中的 Hyper-V 伺服器： <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |Intel(R) Xeon(R) CPU E5-2630 0 @ 2.30GHz |2 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| VMM 伺服器 |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="server-workloads"></a>伺服器工作負載

* 基於測試目的，我們挑選了常用於企業客戶案例中的工作負載。
* 我們使用 [IOMeter](http://www.iometer.org) 搭配資料表中摘要說明的工作負載特性進行模擬。
* 所有 IOMeter 設定檔都設為寫入隨機位元組，以模擬最壞情況的工作負載寫入模式。

| 工作負載 | I/O 大小 (KB) | 存取百分比 | 讀取百分比 | 未完成的 I/O | I/O 模式 |
| --- | --- | --- | --- | --- | --- |
| 檔案伺服器 |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |全部 100% 隨機 |
| SQL Server (磁碟區 1) SQL Server (磁碟區 2) |864 |100%100% |70%0% |88 |100% 隨機 100% 循序 |
| Exchange |32 |100% |67% |8 |100% 隨機 |
| 工作站/VDI |464 |66%34% |70%95% |11 |兩者都 100% 隨機 |
| Web 檔案伺服器 |4864 |33%34%33% |95%95%95% |888 |全部 75% 隨機 |

### <a name="vm-configuration"></a>VM 設定

* 主要叢集上 470 個虛擬機器。
* 所有虛擬機器都搭配 VHDX 磁碟。
* 虛擬機器執行資料表中摘要說明的工作負載。 全部都使用 VMM 範本建立。

| 工作負載 | VM 數 | RAM 下限 (GB) | RAM 上限 (GB) | 每個 VM 的邏輯磁碟大小 (GB) | IOPS 上限 |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| 檔案伺服器 |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Web 伺服器 |149 |.5 |1 |80 |6 |
| 總計 |470 | | |96.83 TB |4108 |

### <a name="site-recovery-settings"></a>Site Recovery 設定

* Azure Site Recovery 設有內部部署至內部部署的保護
* VMM 伺服器已設定四個雲端，其中包含 Hyper-V 叢集伺服器及其虛擬機器。

| 主要 VMM 雲端 | 雲端中受保護的虛擬機器 | 複寫頻率 | 其他復原點 |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 分鐘 |None |
| PrimaryCloudRpo30s |47 |30 秒 |None |
| PrimaryCloudRpo30sArp1 |47 |30 秒 |1 |
| PrimaryCloudRpo5m |235 |5 分鐘 |None |

### <a name="performance-metrics"></a>效能度量

資料表摘要說明在部署中測量的效能度量和計數器。

| 度量 | 計數器 |
| --- | --- |
| CPU |\Processor(_Total)\% Processor Time |
| 可用的記憶體 |\記憶體\可用的 MB |
| IOPS |\PhysicalDisk(_Total)\每秒的磁碟傳輸數 |
| 每秒的 VM 讀取 (IOPS) 作業數 |\Hyper-V 虛擬存放裝置 (<VHD>) \每秒的讀取作業數 |
| 每秒的 VM 寫入 (IOPS) 作業數 |\Hyper-V 虛擬存放裝置 (<VHD>)\每秒的寫入作業數 |
| VM 讀取輸送量 |\Hyper-V 虛擬存放裝置 (<VHD>)\每秒的讀取位元組數 |
| VM 寫入輸送量 |\Hyper-V 虛擬存放裝置 (<VHD>)\每秒的寫入位元組數 |

## <a name="next-steps"></a>後續步驟

[設定兩個內部部署 VMM 站台之間的複寫](site-recovery-vmm-to-vmm.md)
