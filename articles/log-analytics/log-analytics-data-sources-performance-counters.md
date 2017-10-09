---
title: "aaaCollect 和分析 Azure 記錄分析中的效能計數器 |Microsoft 文件"
description: "記錄分析 tooanalyze 效能會收集效能計數器，Windows 和 Linux 代理程式上。  本文說明如何 tooconfigure 集合的效能計數器 Windows 和 Linux 代理程式，它們的詳細資料會儲存在 hello OMS 儲存機制，以及如何 tooanalyze hello OMS 入口網站中。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Log Analytics 中的 Windows 和 Linux 效能資料來源
在 Windows 和 Linux 的效能計數器提供深入了解 hello 的硬體元件、 作業系統和應用程式的效能。  記錄分析可供長詞彙分析及報告頻繁的近即時 (NRT) 分析加法 tooaggregating 效能資料收集效能計數器。

![效能計數器](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>設定效能計數器
從 hello hello OMS 入口網站中設定效能計數器[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。

當您先設定 Windows 或 Linux 效能計數器的新的 OMS 工作區中，您會獲得 hello 選項 tooquickly 會建立數個常用的計數器。  它們會列出核取方塊的下一個 tooeach。  請確定您想要 tooinitially 任何計數器建立簽入，然後按一下**新增 hello 選取效能計數器**。

對於 Windows 效能計數器，您可以選擇每個效能計數器的特定執行個體。 對於 Linux 效能計數器，您選擇的每個計數器執行個體 hello 適用於 tooall 的 hello 父計數器的子系計數器。 hello 下表顯示 hello 常見執行個體可用 tooboth Linux 和 Windows 效能計數器。

| 執行個體名稱 | 說明 |
| --- | --- |
| \_總計 |所有的 hello 執行個體的總數 |
| \* |所有執行個體 |
| (/&#124;/var) |比對名為 / 或 /var 的執行個體 |

### <a name="windows-performance-counters"></a>Windows 效能計數器

![設定 Windows 效能計數器](media/log-analytics-data-sources-performance-counters/configure-windows.png)

請遵循此程序 tooadd 新的 Windows 效能計數器 toocollect。

1. 在 hello hello 格式的文字方塊中的 hello 計數器類型 hello 名稱*物件 （執行個體） \counter*。  開始輸入時，您就會看到符合的常用計數器清單。  您可以選取從 hello 清單或輸入您自己的計數器。  您也可以指定 *object\counter*，以傳回特定計數器的所有執行個體。  

    當從具名執行個體中收集 SQL Server 效能計數器，所有具名執行個體的計數器開始，使用*MSSQL$* ，後面接著 hello hello 執行個體名稱。  例如，toocollect hello 記錄檔快取點擊率計數器為具名 SQL hello 資料庫效能物件中的所有資料庫執行都個體 INST2，指定`MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`。

2. 按一下 **+** 或按**Enter** tooadd hello 計數器 toohello 清單。
3. 當您新增的計數器時，它會使用 hello 預設值是 10 秒讓其**取樣間隔**。  如果您想 tooreduce hello 存放裝置需求的 hello 收集效能資料，您可以變更這個 tooa 較高值的總 too1800 秒 （30 分鐘）。
4. 完成新增計數器後，請按一下 hello**儲存**在 hello 螢幕 toosave hello 組態 hello 最上方的按鈕。

### <a name="linux-performance-counters"></a>Linux 效能計數器

![設定 Linux 效能計數器](media/log-analytics-data-sources-performance-counters/configure-linux.png)

請遵循此程序 tooadd 新增 Linux 效能計數器 toocollect。

1. 根據預設，所有的組態變更會自動推入 tooall 代理程式。  Linux 代理程式，請傳送 toohello Fluentd 資料收集器的組態檔案。  如果您想 toomodify 手動在每個 Linux 代理程式上的這個檔案，然後取消核取方塊 hello*套用下列組態 toomy Linux 電腦*並遵循下列的 hello 指引。
2. 在 hello hello 格式的文字方塊中的 hello 計數器類型 hello 名稱*物件 （執行個體） \counter*。  開始輸入時，您就會看到符合的常用計數器清單。  您可以選取從 hello 清單或輸入您自己的計數器。  
3. 按一下 **+** 或按**Enter** tooadd hello 計數器 toohello 清單中的 hello 物件的其他計數器。
4. 物件使用的所有計數器都 hello 相同**取樣間隔**。  hello 預設值為 10 秒。  如果您想 tooreduce hello 存放裝置需求的 hello 收集效能資料，您可以變更這個 tooa 較高值的總 too1800 秒 （30 分鐘）。
5. 完成新增計數器後，請按一下 hello**儲存**在 hello 螢幕 toosave hello 組態 hello 最上方的按鈕。

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>在組態檔中設定 Linux 效能計數器
您不需要設定 Linux 效能計數器使用 hello OMS 入口網站，您可以 hello 選擇編輯 hello Linux 代理程式上的設定檔。  中的 hello 組態所控制效能度量 toocollect **/等/選擇/microsoft/omsagent/\<工作區識別碼\>/conf/omsagent.conf**。

應為單一 hello 組態檔中定義每個物件或類別目錄的效能度量 toocollect`<source>`項目。 hello 語法遵循下列的 hello 模式。

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


hello 下表說明此項目中的 hello 參數。

| 參數 | 說明 |
|:--|:--|
| object\_name | Hello 集合的物件名稱。 |
| instance\_regex |  A*規則運算式*定義哪些執行個體 toocollect。 hello 值：`.*`指定所有執行個體。 toocollect 處理器校能標準只 hello\_總執行個體，您可以指定`_Total`。 toocollect 的處理序校只 hello crond 或 sshd 執行個體，您可以指定: ' (crond\|sshd)`。 |
| counter\_name\_regex | A*規則運算式*定義哪些物件的計數器 （hello） toocollect。 toocollect hello 物件的所有計數器都指定： `.*`。 toocollect 只會交換空間計數器 hello 記憶體物件，例如，您可以指定：`.+Swap.+` |
| interval | 哪些 hello 收集物件計數器的頻率。 |


hello 下表列出 hello 物件與計數器，您可以在 hello 組態檔中指定。  還有其他計數器適用於特定應用程式，如[在 Log Analytics 中收集 Linux 應用程式的效能計數器](log-analytics-data-sources-linux-applications.md)中所述。

| 物件名稱 | 計數器名稱 |
|:--|:--|
| Logical Disk | % Free Inodes |
| Logical Disk | % Free Space |
| Logical Disk | % Used Inodes |
| Logical Disk | % Used Space |
| Logical Disk | Disk Read Bytes/sec  |
| Logical Disk | Disk Reads/sec  |
| Logical Disk | Disk Transfers/sec |
| Logical Disk | Disk Write Bytes/sec |
| Logical Disk | Disk Writes/sec |
| Logical Disk | Free Megabytes |
| Logical Disk | Logical Disk Bytes/sec |
| 記憶體 | % Available Memory |
| 記憶體 | % Available Swap Space |
| 記憶體 | % Used Memory |
| 記憶體 | % Used Swap Space |
| 記憶體 | Available MBytes Memory |
| 記憶體 | Available MBytes Swap |
| 記憶體 | Page Reads/sec |
| 記憶體 | Page Writes/sec |
| 記憶體 | Pages/sec |
| 記憶體 | Used MBytes Swap Space |
| 記憶體 | Used Memory MBytes |
| 網路 | Total Bytes Transmitted |
| 網路 | Total Bytes Received |
| 網路 | Total Bytes |
| 網路 | Total Packets Transmitted |
| 網路 | Total Packets Received |
| 網路 | Total Rx Errors |
| 網路 | Total Tx Errors |
| 網路 | Total Collisions |
| Physical Disk | Avg.Disk sec/Read |
| Physical Disk | Avg.Disk sec/Transfer |
| Physical Disk | Avg.Disk sec/Write |
| Physical Disk | Physical Disk Bytes/sec |
| Process | Pct Privileged Time |
| Process | Pct User Time |
| Process | Used Memory kBytes |
| Process | Virtual Shared Memory |
| 處理器 | % DPC Time |
| 處理器 | % Idle Time |
| 處理器 | % Interrupt Time |
| 處理器 | % IO Wait Time |
| 處理器 | % Nice Time |
| 處理器 | % Privileged Time |
| 處理器 | % Processor Time |
| 處理器 | % User Time |
| 系統 | Free Physical Memory |
| 系統 | Free Space in Paging Files |
| 系統 | Free Virtual Memory |
| 系統 | 處理序 |
| 系統 | Size Stored In Paging Files |
| 系統 | Uptime |
| 系統 | 使用者 |


以下是 hello 效能標準的預設組態。

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>資料收集
只要代理程式有安裝相關計數器，Log Analytics 就會依照其指定的取樣間隔時間，收集全部代理程式上所有指定的效能計數器。  hello 資料不會彙總，而且 hello 未經處理的資料在所有的記錄搜尋檢視 hello OMS 訂用帳戶所指定的持續時間。

## <a name="performance-record-properties"></a>效能記錄屬性
效能記錄都有一種**效能**和 hello 下表中都有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 電腦 |從收集 hello 事件的電腦。 |
| CounterName |Hello 效能計數器名稱 |
| CounterPath |Hello 表單中的 hello 計數器的完整路徑\\ \\\<電腦 >\\object(instance)\\計數器。 |
| CounterValue |Hello 計數器的數值。 |
| InstanceName |Hello 事件執行個體的名稱。  如果沒有執行個體即為空白。 |
| ObjectName |Hello 效能物件的名稱 |
| SourceSystem |從已收集的代理程式 hello 資料類型。 <br><br>OpsManager – Windows 代理程式，直接連接或 SCOM <br> Linux – 所有的 Linux 代理程式  <br> AzureStorage – Azure 診斷 |
| TimeGenerated |日期和時間的 hello 資料取樣。 |

## <a name="sizing-estimates"></a>大小估計值
 特定計數器集合的約略估計是依照每個執行個體 10 秒間隔，每天約 1 MB。  您可以使用下列公式的 hello 估計 hello 存放裝置需求的特定計數器。

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>記錄搜尋與效能記錄
hello 下表提供不同範例擷取效能記錄的記錄搜尋。

| 查詢 | 說明 |
|:--- |:--- |
| Type=Perf |所有效能資料 |
| Type=Perf Computer="MyComputer" |來自特定電腦的所有效能資料 |
| Type=Perf CounterName="Current Disk Queue Length" |來自特定計數器的所有效能資料 |
| Type=Perf (ObjectName=Processor) CounterName="% Processor Time" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU  by Computer |所有電腦的平均 CPU 使用率 |
| Type=Perf (CounterName="% Processor Time") &#124;  measure max(Max) by Computer |所有電腦的最大 CPU 使用率 |
| Type=Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" &#124; measure Avg(Average) by InstanceName |所有 hello 執行個體在指定的電腦之間的平均目前磁碟佇列長度 |
| Type=Perf CounterName="DiskTransfers/sec" &#124; measure percentile95(Average) by Computer |所有電腦之第 95 個百分位數的 Disk Transfers/Sec |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |所有電腦每小時平均 CPU 使用率 |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |特定電腦每小時每個 % 百分比計數器的 70 個百分位數 |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |特定電腦每小時平均、最小、最大和 75 個百分位數的 CPU 使用量 |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | 從名為 SQL Server 執行個體 INST2 hello hello master 資料庫物件從 hello 資料庫效能的所有效能資料。  

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> | 查詢 | 說明 |
|:--- |:--- |
| Perf |所有效能資料 |
| Perf &#124; where Computer == "MyComputer" |來自特定電腦的所有效能資料 |
| Perf &#124; where CounterName == "Current Disk Queue Length" |來自特定計數器的所有效能資料 |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |所有電腦的平均 CPU 使用率 |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |所有電腦的最大 CPU 使用率 |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |所有 hello 執行個體在指定的電腦之間的平均目前磁碟佇列長度 |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |所有電腦之第 95 個百分位數的 Disk Transfers/Sec |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |所有電腦每小時平均 CPU 使用率 |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | 特定電腦每小時每個 % 百分比計數器的 70 個百分位數 |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |特定電腦每小時平均、最小、最大和 75 個百分位數的 CPU 使用量 |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | 從名為 SQL Server 執行個體 INST2 hello hello master 資料庫物件從 hello 資料庫效能的所有效能資料。  

## <a name="viewing-performance-data"></a>檢視效能資料
當您執行的效能資料記錄搜尋時，hello**清單**預設會顯示檢視。  tooview hello 資料在圖形表單中，按一下**度量**。  如需詳細的圖形化檢視，按一下 hello  **+**  tooa 計數器的下一個。  

![摺疊的計量檢視](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

tooaggregate 效能資料記錄搜尋時，請參閱 <<c0> [ 隨度量彙總並在 OMS 中的視覺效果](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/)。


## <a name="next-steps"></a>後續步驟
* [從 Linux 應用程式收集效能計數器](log-analytics-data-sources-linux-applications.md)，包括 MySQL 和 Apache HTTP Server。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。  
* 匯出收集的資料太[Power BI](log-analytics-powerbi.md)對其他視覺效果與分析。
