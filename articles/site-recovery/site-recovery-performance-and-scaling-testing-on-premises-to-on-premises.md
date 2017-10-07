---
title: "使用 Azure Site Recovery 的站台間的 HYPER-V 複寫的 aaaTest 結果 |Microsoft 文件"
description: "本文將提供使用 Azure Site Recovery 效能測試的 HYPER-V Vm 的內部部署 tooon 內部部署複寫的相關資訊。"
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
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>測試結果以進行內部 tooon 內部部署 HYPER-V 複寫與站台復原

您可以使用 Microsoft Azure Site Recovery tooorchestrate 和管理複寫的虛擬機器和實體伺服器 tooAzure 或 tooa 次要資料中心。 本文提供效能測試兩個複寫 HYPER-V 虛擬機器內部部署資料中心時，我們所做的 hello 的結果。

## <a name="test-goals"></a>測試目標

測試的 hello 目標是的 tooexamine Azure Site Recovery 在穩定狀態複寫期間執行的方式。 當虛擬機器已完成初始複寫，且正在同步處理差異變更時，就會發生穩定狀態複寫。 它是使用穩定狀態，因為它是大多數虛擬機器維持除非發生非預期的中斷 hello 狀態的重要 toomeasure 效能。

hello 測試部署是由兩個內部部署網站與 VMM 伺服器中每個站台所組成。 此測試部署是通常是總公司/分公司部署，以總公司作為主要站台 hello 和 hello 分公司與 hello 次要或復原站台。

## <a name="what-we-did"></a>我們執行的動作

以下是什麼我們未在 hello 測試中傳遞：

1. 使用 VMM 範本建立虛擬機器。
2. 啟動虛擬機器，並擷取 12 小時內的基準效能度量。
3. 在主要和復原 VMM 伺服器上建立雲端。
4. 在 Azure Site Recovery 中設定雲端保護，包括來源和復原雲端的對應。
5. 啟用虛擬機器的保護，讓他們 toocomplete 初始複寫。
6. 等待幾個小時讓系統趨於穩定。
7. 擷取 12 小時內的效能度量，以確保所有虛擬機器在這 12 小時內都維持在預期的複寫狀態。
8. 量值 hello hello 基準效能度量和 hello 複寫效能度量之間的差異。


## <a name="primary-server-performance"></a>主要伺服器效能

* HYPER-V 複本以非同步方式追蹤變更 tooa 的記錄檔以最小的儲存負擔 hello 主要伺服器上。
* HYPER-V 複本 」 會利用自我維護的記憶體快取 toominimize IOPS 負荷追蹤。 它會儲存寫入 toohello 記憶體，且其 hello hello 之前的記錄檔時間該 hello 記錄檔排清 VHDX 傳送 toohello 復原站台。 Hello 寫入達到預先決定的限制時，也會發生磁碟排清。
* hello 圖形下方會顯示複寫 hello 穩定狀態 IOPS 負荷。 我們可以看到該 hello IOPS 負荷到期 tooreplication 是大約 5%，相當低。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

HYPER-V 複本 」 會利用上 hello 主要伺服器 toooptimize 磁碟效能的記憶體。 Hello 下列圖表所示，記憶體 hello 主要叢集中的所有伺服器上的額外負荷很低。 hello 記憶體額外負荷顯示是記憶體的 hello hello HYPER-V 伺服器上的複寫比較 toohello 總安裝記憶體所使用百分比。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Hyper-V 複本的 CPU 負荷最低。 Hello 圖形中所示，複寫負荷是 2-3 %hello 範圍。

![主要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>次要 (復原) 伺服器效能

HYPER-V 複本使用少量記憶體 hello 復原伺服器 toooptimize hello 的儲存體作業數目。 hello 圖摘要說明 hello hello 復原伺服器上的記憶體使用量。 hello 記憶體額外負荷顯示是記憶體的 hello hello HYPER-V 伺服器上的複寫比較 toohello 總安裝記憶體所使用百分比。

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

hello hello 復原站台上的 I/O 作業數量是 hello hello 主要站台上的寫入作業數目的函式。 讓我們查看 hello 相較於 hello 總 I/O 作業的復原站台上 hello 總 I/O 作業和寫入 hello 主要站台上的作業。 hello 圖形顯示 hello 復原站台 iops 該 hello 總計

* 大約 1.5 倍 hello hello 主要上寫入 IOPS。
* 大約 hello 的 37%的總 IOPS hello 主要站台上。

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![次要結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>對網路使用率的影響

每秒的網路頻寬平均為 275 Mb hello 主要和復原節點之間 （搭配使用已啟用壓縮） 針對現有的頻寬 5 Gb 每秒。

![結果網路使用率](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>對 VM 效能的影響

重要的考量是複寫的 hello 影響 hello 虛擬機器上執行的實際執行工作負載。 如果 hello 主要站台的分配適當的複寫，hello 工作負載不應該有任何影響。 HYPER-V 複本 」 的輕量型追蹤機制可確保在 hello 虛擬機器中執行的工作負載在穩定狀態複寫期間不會受到影響。 Hello 下列圖形所示。

此圖顯示啟用複寫之前和之後，執行不同工作負載的虛擬機器執行的 IOPS。 您可以觀察是 hello 兩者之間沒有差異。

![複本效果結果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

hello 下圖顯示 hello 輸送量的虛擬機器執行不同的工作負載之前和之後已啟用複寫。 您可以觀察到複寫沒有顯著的影響。

![結果複本效果](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>結論

hello 結果清楚地顯示 Azure Site Recovery 中，搭配 HYPER-V 複本縮放與最小預先配置大型叢集。  Azure Site Recovery 提供簡單的部署、複寫、管理和監視功能。 HYPER-V 複本提供複寫順利調整 hello 必要的基礎結構。 如需規劃最佳的部署，建議您下載 hello [HYPER-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057)。

## <a name="test-environment-details"></a>測試環境詳細資料

### <a name="primary-site"></a>主要站台

* hello 主要站台的叢集，其中包含五個執行 470 個虛擬機器的 HYPER-V 伺服器。
* hello 虛擬機器執行不同的工作負載，而且全都有啟用 Azure Site Recovery 保護。
* Hello 叢集節點的儲存體由 iSCSI SAN 提供。 機型 – Hitachi HUS130。
* 每部叢集伺服器都有四張網路卡 (NIC)，每張網路卡各為 1 Gbps。
* Hello 網路卡的兩個連接的 tooan iSCSI 私人網路，而兩個連接的 tooan 外部企業網路。 Hello 外部網路的其中一個被保留供叢集通訊專用。

![主要硬體需求](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| 伺服器 | RAM | 模型 | 處理器 | 處理器數目 | NIC | 軟體 |
| --- | --- | --- | --- | --- | --- | --- |
| 叢集中的 Hyper-V 伺服器： <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25 具備 256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| VMM 伺服器 |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>次要 (復原) 站台

* hello 次要站台有六個節點的容錯移轉叢集。
* Hello 叢集節點的儲存體由 iSCSI SAN 提供。 機型 – Hitachi HUS130。

![主要硬體規格](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| 伺服器 | RAM | 模型 | 處理器 | 處理器數目 | NIC | 軟體 |
| --- | --- | --- | --- | --- | --- | --- |
| 叢集中的 Hyper-V 伺服器： <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |Intel(R) Xeon(R) CPU E5-2630 0 @ 2.30GHz |2 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 @ 2.20GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V 角色 |
| VMM 伺服器 |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="server-workloads"></a>伺服器工作負載

* 基於測試目的，我們挑選了常用於企業客戶案例中的工作負載。
* 我們使用[IOMeter](http://www.iometer.org)與 hello 模擬的 hello 表中摘要說明的工作負載特性。
* 所有 IOMeter 設定檔都設定工作負載 toowrite 隨機位元組 toosimulate 最壞情況的寫入的模式。

| 工作負載 | I/O 大小 (KB) | 存取百分比 | 讀取百分比 | 未完成的 I/O | I/O 模式 |
| --- | --- | --- | --- | --- | --- |
| 檔案伺服器 |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |全部 100% 隨機 |
| SQL Server (磁碟區 1) SQL Server (磁碟區 2) |864 |100%100% |70%0% |88 |100% 隨機 100% 循序 |
| Exchange |32 |100% |67% |8 |100% 隨機 |
| 工作站/VDI |464 |66%34% |70%95% |11 |兩者都 100% 隨機 |
| Web 檔案伺服器 |4864 |33%34%33% |95%95%95% |888 |全部 75% 隨機 |

### <a name="vm-configuration"></a>VM 設定

* hello 主要叢集上 470 個虛擬機器。
* 所有虛擬機器都搭配 VHDX 磁碟。
* 執行 hello 表中摘要說明的工作負載的虛擬機器。 全部都使用 VMM 範本建立。

| 工作負載 | VM 數 | RAM 下限 (GB) | RAM 上限 (GB) | 每個 VM 的邏輯磁碟大小 (GB) | IOPS 上限 |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| 檔案伺服器 |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Web 伺服器 |149 |.5 |1 |80 |6 |
| 總計 |470 | | |96.83 TB |4108 |

### <a name="site-recovery-settings"></a>Site Recovery 設定

* Azure Site Recovery 設定為在內部部署 tooon 內部部署保護
* hello VMM 伺服器有四個雲端設定，其中包含 hello HYPER-V 叢集的伺服器和其虛擬機器。

| 主要 VMM 雲端 | 受保護的 hello 雲端中的虛擬機器 | 複寫頻率 | 其他復原點 |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 分鐘 |None |
| PrimaryCloudRpo30s |47 |30 秒 |None |
| PrimaryCloudRpo30sArp1 |47 |30 秒 |1 |
| PrimaryCloudRpo5m |235 |5 分鐘 |None |

### <a name="performance-metrics"></a>效能度量

hello 表格摘要說明 hello 效能度量和 hello 部署中測量的計數器。

| 計量 | 計數器 |
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
