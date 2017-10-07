---
title: "aaaCapacity 和效能 Azure 記錄分析解決方案 |Microsoft 文件"
description: "使用 hello 容量和效能方案，在您了解記錄分析 toohelp hello HYPER-V 伺服器的容量。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>規劃 HYPER-V 虛擬機器容量以 hello 容量和效能方案 （預覽）

![容量與效能符號](./media/log-analytics-capacity/capacity-solution.png)

您可以使用 hello 容量和效能方案，在您了解記錄分析 toohelp hello HYPER-V 伺服器的容量。 hello 解決方案可提供深入了解您的 HYPER-V 環境，您可以透過 hello 的整體使用情況 （CPU、 記憶體和磁碟） hello 主機和 hello 的 HYPER-V 主機上執行的 Vm。 針對 CPU、 記憶體和磁碟會收集度量，跨所有主機和 hello Vm 上執行。

hello 解決方案：

-   顯示 CPU 和記憶體使用率最高與最低的主機
-   顯示 CPU 和記憶體使用率最高與最低的 VM
-   顯示 IOPS 和輸送量使用率最高與最低的 VM
-   顯示哪些 VM 在哪些主機上執行
-   顯示 hello 高輸送量，IOPS 的最上層磁碟和延遲，在叢集共用磁碟區
- 可讓您 toocustomize 和群組為基礎的篩選

> [!NOTE]
> hello 舊版 hello 容量和效能的解決方案，稱為 容量管理需要 System Center Operations Manager 和 System Center Virtual Machine Manager。 這個經過更新的解決方案則沒有這些相依性。


## <a name="connected-sources"></a>連接的來源

hello 下表描述此解決方案所支援的 hello 連接來源。

| 連接的來源 | 支援 | 說明 |
|---|---|---|
| [Windows 代理程式](log-analytics-windows-agents.md) | 是 | hello 方案會從 Windows 代理程式收集容量和效能資料的資訊。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否    | hello 解決方案不會收集從直接 Linux 代理程式的容量和效能資料的資訊。|
| [SCOM 管理群組](log-analytics-om-agents.md) | 是 |hello 方案會從已連線的 SCOM 管理群組中的代理程式收集容量和效能資料。 不需要從 hello SCOM 代理程式 tooOMS 的直接連接。 從 hello 管理群組 toohello OMS 儲存機制，就會轉送資料。|
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | Azure 儲存體不包含容量和效能資料。|

## <a name="prerequisites"></a>必要條件

- Windows 或 Operations Manager 代理程式必須安裝在 Windows Server 2012 或更新版本的 Hyper-V 主機上，而非安裝在虛擬機器上。


## <a name="configuration"></a>組態

執行下列步驟 tooadd hello 容量和效能方案 tooyour 工作區中的 hello。

- 加入 hello 容量和效能方案 tooyour OMS 工作區中使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

## <a name="management-packs"></a>管理組件

如果您的 SCOM 管理群組連線的 tooyour OMS 工作區，然後 hello 下列管理組件將會安裝在 SCOM 中當您將加入這個方案。 這些管理組件不需要任何設定或維護。

- Microsoft.IntelligencePacks.CapacityPerformance

hello 1201 事件類似：


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

當更新 hello 容量和效能的方案時，將會變更 hello 版本號碼。

如需有關解決方案管理組件的更新方式的詳細資訊，請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。

## <a name="using-hello-solution"></a>使用 hello 解決方案

當您將 hello 容量和效能方案 tooyour 工作區時，hello 容量和效能加入 toohello 概觀儀表板。 此磚會顯示目前作用中的 HYPER-V 主機的 hello 數目以及作用中的虛擬機器受監視的 hello 選取的時間週期的 hello 數目計數。

![[容量和效能] 圖格](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>檢閱使用率

按一下 hello 容量和效能磚 tooopen hello 容量和效能儀表板。 hello 儀表板會納入 hello 下表中的 hello 資料行。 每個資料行列出 tooten 比對資料行的準則 hello 指定領域和時間範圍的項目。 您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello hello 資料行，或按一下 hello 資料行標頭。

- **主機**
    - **主機 CPU 使用率**顯示 hello CPU 使用率，主機電腦以及一份主機，根據選取的時間週期的 hello 的圖形化趨勢。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何主控件名稱 tooopen 記錄搜尋，並檢視託管 Vm 的 CPU 計數器詳細資料。
    - **主機記憶體使用率**顯示 hello 的主機電腦的記憶體使用量和根據選取的時間週期的 hello 的主機清單的圖形化趨勢。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何主控件名稱 tooopen 記錄搜尋和檢視記憶體計數器詳細資料對於託管的 Vm。
- **虛擬機器**
    - **VM 的 CPU 使用率**顯示 hello CPU 使用量的虛擬機器和虛擬機器，根據選取的時間週期的 hello 清單的圖形化趨勢。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間的 hello 前 3 個 Vm。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何 VM 名稱 tooopen 記錄搜尋，並檢視彙總的 hello VM 的 CPU 計數器詳細資料。
    - **VM 記憶體使用率**顯示 hello 記憶體使用量的虛擬機器和虛擬機器，根據選取的時間週期的 hello 清單的圖形化趨勢。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間的 hello 前 3 個 Vm。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何 VM 名稱 tooopen 記錄搜尋，然後檢視 hello VM 的彙總的記憶體計數器詳細資料。
    - **VM 磁碟 IOPS 總數**顯示 hello 的圖形化趨勢總磁碟 IOPS 的虛擬機器和虛擬機器，以針對每個，hello IOPS 的清單會根據選取的時間週期的 hello。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間的 hello 前 3 個 Vm。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何 VM 名稱 tooopen 記錄搜尋並檢視彙總的磁碟 IOPS 計數器 hello VM 的詳細資料。
    - **VM 的總磁碟輸送量**顯示虛擬機器和與 hello 總磁碟輸送量為每個虛擬機器的清單，根據的 hello hello 總磁碟輸送量的圖形化趨勢選取時間週期。 將滑鼠停留在 hello 行圖表 tooview 詳細資料的特定點的時間的 hello 前 3 個 Vm。 按一下 hello 圖表 tooview 在記錄搜尋中的更多詳細資料。 按一下任何 VM 名稱 tooopen 記錄搜尋，並檢視彙總 hello VM 的總磁碟輸送量計數器詳細資料。
- **叢集共用磁碟區**
    - **總輸送量**顯示 hello 總和兩者的讀取和寫入在叢集共用磁碟區上。
    - **總 IOPS**顯示 hello 總和的叢集共用磁碟區上每秒輸入/輸出作業。
    - **延遲總計**叢集共用磁碟區上會顯示 hello 總延遲時間。
- **裝載密度**hello 頂端磚會顯示的主機和虛擬機器可用的 toohello 方案 hello 總數。 按一下 記錄搜尋中的 hello 頂端的圖格 tooview 其他詳細資料。 也會列出所有主機和 hello 所裝載的虛擬機器數目。 按一下主機 toodrill 到 hello，VM 會記錄搜尋中。


![儀表板主機刀鋒視窗](./media/log-analytics-capacity/dashboard-hosts.png)

![儀表板虛擬機器刀鋒視窗](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>評估效能

從一個組織 tooanother 實際執行運算環境中則有明顯的差異。 此外，容量和效能的工作負載可能會取決於 VM 的執行方式以及您認為平常的事項。 特定程序 toohelp 測量效能可能不會套用 tooyour 環境。 讓多個一般化指引是更適合的 toohelp。 Microsoft 發行的各種不同的規範指引文章 toohelp 您衡量效能。

toosummarize，hello 解決方案從各種不同的來源包括效能計數器收集容量和效能資料。 使用 hello 方案中的各種介面中呈現該容量和效能資料，並比較您的結果 toothose 在 hello[測量的效能，在 HYPER-V 上](https://msdn.microsoft.com/library/cc768535.aspx)發行項。 雖然 hello 發行項已發行之前，都仍然有效 hello 度量、 考量和指導方針。 hello 發行項包含連結 tooother 實用資源。


## <a name="sample-log-searches"></a>記錄檔搜尋範例

下表中的 hello 提供容量和效能資料收集，並計算此解決方案的範例記錄搜尋。

| 查詢 | 說明 |
|---|---|
| 所有主機記憶體組態 | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| 所有 VM 記憶體組態 | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| 所有 VM 的磁碟 IOPS 總數細目 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 所有 VM 的磁碟輸送量總數細目 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 所有 CSV 的 IOPS 總數細目 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 所有 CSV 的輸送量總數細目 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 所有 CSV 的延遲總數細目 | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> | 查詢 | 說明 |
|:--- |:--- |
| 所有主機記憶體組態 | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| 所有 VM 記憶體組態 | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| 所有 VM 的磁碟 IOPS 總數細目 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 所有 VM 的磁碟輸送量總數細目 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 所有 CSV 的 IOPS 總數細目 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 所有 CSV 的輸送量總數細目 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 所有 CSV 的延遲總數細目 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細容量和效能資料。
