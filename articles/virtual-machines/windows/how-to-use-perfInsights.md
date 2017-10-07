---
title: "aaaHow toouse Microsoft Azure 中的 PerfInsights |Microsoft 文件"
description: "學習如何 toouse PerfInsights tootroubleshoot Windows VM 效能問題。"
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>如何 toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload)是自動化的指令碼收集診斷資訊、 執行 I/O 壓力負載，並提供分析報表 toohelp Microsoft Azure 中的 Windows VM 效能問題進行疑難排解。 

我們建議您先執行此指令碼， 再開啟 Microsoft 支援票證處理 VM 效能問題。

## <a name="supported-troubleshooting-scenarios"></a>支援的疑難排解案例

PerfInsights 可以收集並分析合併到唯一案例的多種資訊。

### <a name="collect-disk-configuration"></a>收集磁碟設定 

此案例，收集 hello 磁碟設定和其他重要的資訊，包括下列項目 hello:

-   事件記錄檔

-   所有傳入和傳出連線的網路狀態

-   網路和防火牆組態設定

-   工作清單中的 hello 系統目前正在執行的所有應用程式

-   Msinfo32 hello 虛擬機器 (VM) 所建立的資訊檔案

-   Microsoft SQL Server 資料庫組態設定 （如果 hello VM 識別為執行 SQL Server 的伺服器）

-   儲存體可靠性計數器

-   重要的 Windows Hotfix

-   已安裝的篩選器驅動程式

這是被動的集合，不應該影響 hello 系統的資訊。 

>[!Note]
>這種情況下都會自動包含在每個 hello 下列案例中。

### <a name="benchmarkstorage-performance-test"></a>基準測試/儲存體效能測試

這種情況下執行 hello [diskspd](https://github.com/Microsoft/diskspd)針對所有的磁碟機附加 toohello VM 建立基準測試 （IOPS 和 MBPS）。 

> [!Note]
> 此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。 必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。 增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。
>

### <a name="general-vm-slow-analysis"></a>一般 VM Slow 分析 

這種情況下執行[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx)使用 hello 計數器 hello Generalcounters.txt 檔案中指定的追蹤。 如果 hello VM 識別為執行 SQL Server 的伺服器，它會執行使用 hello Sqlcounters.txt 檔中找到的 hello 計數器的效能計數器追蹤。 它也包含效能診斷資料。

### <a name="vm-slow-analysis-and-benchmark"></a>VM Slow 分析和基準測試

此案例會執行[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx)追蹤，後面接著 [diskspd](https://github.com/Microsoft/diskspd) 基準測試。 

> [!Note]
> 此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。 必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。 增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。
>

### <a name="azure-files-analysis"></a>Azure 檔案分析 

此案例會同時執行特殊的效能計數器擷取與網路追蹤。 擷取包含所有的 hello [SMB 用戶端共用] 計數器。 hello 下面是一些索引鍵的 SMB 用戶端共用效能計數器屬於 hello 擷取：

| **類型**     | **SMB 用戶端共用計數器** |
|--------------|-------------------------------|
| IOPS         | 資料要求/秒             |
|              | 讀取要求/秒             |
|              | 寫入要求/秒            |
| Latency      | 平均秒/資料要求         |
|              | 平均秒/讀取                 |
|              | 平均秒/寫入                |
| IO 大小      | Avg.位元組/資料要求       |
|              | Avg.位元組/讀取               |
|              | Avg.位元組/寫入              |
| 輸送量   | 資料位元組/秒                |
|              | 讀取位元組/秒                |
|              | 寫入位元組/秒               |
| 佇列長度 | Avg.讀取佇列長度        |
|              | Avg.寫入佇列長度       |
|              | Avg.資料佇列長度        |

### <a name="custom-configuration"></a>自訂組態 

當您執行自訂設定時，您是以平行方式執行所有的追蹤 (效能診斷、效能計數器、xperf、網路、storport)，視您選取多少不同的追蹤而定。 完成追蹤之後，hello 工具會執行 hello diskspd benchmark 中，如果已選取。 

> [!Note]
> 此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。 必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。 增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Hello 指令碼所收集的資訊類型為何？

資訊的 Windows VM、 磁碟或儲存集區組態、 收集效能計數器、 記錄檔和各種追蹤視使用的 hello 效能案例而定：

|收集的資料                              |  |  | 效能測試案例 |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | 收集磁碟設定 | 基準測試/儲存體效能測試 | 一般 VM Slow 分析 | VM Slow 分析和基準測試 | Azure 檔案分析 | 自訂組態 |
| 來自事件記錄檔的資訊      | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 系統資訊               | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 磁碟區對應                       | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 磁碟對應                         | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 正在執行的工作                    | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 儲存體可靠性計數器     | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 儲存體資訊              | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| Fsutil 輸出                    | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 篩選器驅動程式資訊               | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| Netstat 輸出                   | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 網路組態            | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 防火牆設定           | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| SQL Server 設定         | 是                        | 是                                | 是                      | 是                            | 是                  | 是                  |
| 效能診斷追蹤 * |                            |                                    | 是                      |                                |                      | 是                  |
| 效能計數器追蹤 **     |                            |                                    |                          |                                |                      | 是                  |
| SMB 計數器追蹤 **             |                            |                                    |                          |                                | 是                  |                      |
| SQL Server 計數器追蹤 **      |                            |                                    |                          |                                |                      | 是                  |
| XPerf 追蹤                      |                            |                                    |                          |                                |                      | 是                  |
| StorPort 追蹤                   |                            |                                    |                          |                                |                      | 是                  |
| 網路追蹤                    |                            |                                    |                          |                                | 是                  | 是                  |
| Diskspd 基準追蹤 ***      |                            | 是                                |                          | 是                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>效能診斷追蹤 (*)

執行規則引擎在 hello 背景 toocollect 資料和診斷進行中的效能問題。 目前支援下列規則的 hello:

- HighCpuUsage 規則： 偵測到高 CPU 使用量的期間，並在這些時間週期期間顯示 hello 頂端 CPU 使用量取用者。
- HighDiskUsage 規則： 偵測到的實體磁碟上的高磁碟使用量期間，並在這些時間週期期間顯示 hello 最大的磁碟使用量取用者。
- HighResolutionDiskMetric 規則： 顯示每部實體磁碟每 50 毫秒的 IOPS、輸送量和 IO 延遲計量。 它會協助 tooquickly 識別節流週期的磁碟。
- HighMemoryUsage 規則： 偵測到高記憶體使用量的期間，並在這些時間週期期間顯示 hello 最多記憶體的使用方式取用者。

> [!NOTE] 
> 目前支援 Windows 版本，包括 hello.NET Framework 3.5 或更新版本。

### <a name="performance-counter-trace-"></a>效能計數器追蹤 (**)

會收集下列效能計數器的 hello:

- \Process、\Processor、\Memory、\Thread、\PhysicalDisk、\LogicalDisk
- \Cache\Dirty Pages、\Cache\Lazy Write Flushes/sec、\Server\Pool Nonpaged、Failures、\Server\Pool Paged Failures
- \Network Interface、\IPv4\Datagrams、\IPv6\Datagrams、\TCPv4\Segments、\TCPv6\Segments、\Network Adapter、\WFPv4\Packets、\WFPv6\Packets、\UDPv4\Datagrams、\UDPv6\Datagrams、\TCPv4\Connection、\TCPv6\Connection、\Network QoS Policy\Packets、\Per Processor Network Interface Card Activity、\Microsoft Winsock BSP 下的已選取計數器

#### <a name="for-sql-server-instances"></a>SQL Server 執行個體
- \SQL Server:Buffer Manager、\SQLServer:Resource Pool Stats、\SQLServer:SQL Statistics\
- \SQLServer:Locks、\SQLServer:General、Statistics
- \SQLServer:Access 方法

#### <a name="for-azure-files"></a>Azure 檔案
\SMB 用戶端共用

### <a name="diskspd-benchmark-trace-"></a>Diskspd 基準追蹤 (***)
Diskspd IO 工作負載測試 [OS 磁碟 (寫入) 和集區磁碟 (讀取/寫入)]

## <a name="run-hello-perfinsights-on-your-vm"></a>在您的 VM 上執行 hello PerfInsights

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>為什麼應該 tooknow 之前我要執行 hello 指令碼？ 

**指令碼需求**

1.  此指令碼必須 hello 發生 hello 效能問題的 VM 上執行。 

2.  hello 支援下列作業系統： Windows Server 2008 R2、 2012、 2012 R2、 2016。Windows 8.1 和 Windows 10。

**當您在實際執行的 Vm 上執行 hello 指令碼的可能問題：**

1.  hello 指令碼與已使用 XPerf 或 DiskSpd hello 「 基準 」 或 「 自訂 」 案例一起使用時，可能產生不良影響 hello 的 hello VM 的效能。 當您在生產環境中執行 hello 指令碼，請格外小心。

2.  當您使用 hello 指令碼，以及已使用 DiskSpd 的 hello 「 基準 」 或 「 自訂 」 案例時，請確定沒有其他背景活動干擾 hello hello 測試磁碟上的 I/O 工作負載。

3.  根據預設，hello 指令碼會使用 hello 暫存磁碟機 toocollect 資料。 如果追蹤會保持啟用更長的時間，可能是相關 hello 收集的資料數量。 這可以降低 hello 可用性 hello 暫存磁碟，因此會影響依賴此磁碟機的任何應用程式上的空間。

### <a name="how-do-i-run-perfinsights"></a>如何執行 PerfInsights？ 

toorun hello 指令碼，請遵循下列步驟：

1. 下載 [PerfInsights.zip](http://aka.ms/perfinsightsdownload)。

2. 解除封鎖 hello PerfInsights.zip 檔案。 這樣，以滑鼠右鍵按一下 hello PerfInsights.zip 檔案中，選取 toodo**屬性**。 在 hello**一般**索引標籤上，選取**解除封鎖**，然後選取 **確定**。 如此可確保 hello 指令碼會在沒有任何額外的安全性會提示執行。  

    ![解除鎖定 hello zip 檔案](media/how-to-use-perfInsights/unlock-file.png)

3.  展開壓縮的 hello PerfInsights.zip 檔案至暫存磁碟機 （依預設，通常是 hello D 磁碟機）。 hello 壓縮的檔案應包含 hello 下列檔案和資料夾：

    ![hello zip 資料夾中的檔案](media/how-to-use-perfInsights/file-folder.png)

4.  系統管理員身分開啟 Windows PowerShell，然後執行 hello PerfInsights.ps1 指令碼。

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    您可能必須 tooenter"y"tooif 您詢問 tooconfirm 想 toochange hello 執行原則。

    在 hello 免責聲明對話方塊方塊中，您可以向 Microsoft 支援的 hello 選項 tooshare 診斷資訊。 您也必須同意 toohello 授權合約 toocontinue。 確認選項後按一下 [執行指令碼]。

    ![[免責聲明] 方塊](media/how-to-use-perfInsights/disclaimer.png)

5.  如果可用的話，當您執行 hello 指令碼 （這是我們的統計資料） 時，請送出 hello 案例數目。 然後按 [下一步] 。
    
    ![輸入支援識別碼](media/how-to-use-perfInsights/enter-support-number.png)

6.  選取暫存磁碟機。 hello 指令碼可以自動偵測 hello hello 磁碟機的磁碟機代號。 如果在這個階段中發生任何問題，您可能會提示您 tooselect hello 磁碟機 （hello 預設磁碟機是 D）。 產生的記錄檔會儲存在這裡 hello 記錄檔中\_集合資料夾。 您輸入或接受 hello 磁碟機代號後，按一下**確定**。

    ![輸入磁碟機](media/how-to-use-perfInsights/enter-drive.png)

7.  從 hello 提供清單中，選取疑難排解的情況。

       ![選取支援案例](media/how-to-use-perfInsights/select-scenarios.png)

8.  您也可以執行 PerfInsights 不顯示 UI。

    hello 下列命令執行 hello 「 一般 VM 慢分析 」 疑難排解案例，而無 UI 提示，或為 30 秒內擷取資料。 它會提示您 tooconsent toohello 相同免責聲明和步驟 4 中所述的使用者授權合約。

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    如果您想 PerfInsights toorun 以無訊息模式時，使用**-AcceptDisclaimerAndShareDiagnostics**參數。 例如，使用下列命令的 hello:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>如何疑難排解執行 hello 指令碼時的問題？

如果不正常終止 hello 指令碼，您可以清除不一致的狀態執行 hello 指令碼，並搭配 hello-清除參數，如下所示：

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

如果 hello 自動偵測 hello 暫存磁碟機的期間發生任何問題，您可能會提示您 tooselect hello 磁碟機 （hello 預設磁碟機是 D）。

![enter-drive](media/how-to-use-perfInsights/enter-drive.png)

hello 指令碼解除安裝 hello 公用程式工具，並會移除暫存資料夾。

### <a name="troubleshooting-other-script-issues"></a>對其他指令碼問題進行疑難排解 

如果您執行 hello 指令碼時，就會發生任何問題，請按 Ctrl + C toointerrupt hello 指令碼執行。 tooremove 暫存物件，請參閱 hello 「 清除異常終止之後 」 一節。

如果您嘗試幾次之後，即使持續 tooexperience 指令碼失敗，我們建議您以 「 偵錯模式 」 執行 hello 指令碼使用 hello"為偵錯 」 參數選項，在啟動時。

Hello 失敗發生時，複製 hello 完整輸出的 hello PowerShell 主控台中，並將它傳送 toohello Microsoft 支援服務代理程式的使用者您的協助之後 toohelp 會對 hello 問題進行疑難排解。

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>如何在自訂組態模式下執行 hello 指令碼？

藉由選取 hello**自訂**組態中，您可以啟用數個追蹤，以平行方式 （使用 shift 鍵 toomulti 選取）：

![選取案例](media/how-to-use-perfInsights/select-scenario.png)

當您選取 hello 效能診斷時，效能計數器追蹤、 XPerf 追蹤、 網路追蹤或 Storport 追蹤案例中，遵循 hello hello 對話方塊中，再次嘗試 tooreproduce hello 效能緩慢的問題之後啟動 hello 追蹤。

下列對話方塊中的 hello 可讓您啟動追蹤：

![start-trace](media/how-to-use-perfInsights/start-trace-message.png)

toostop hello 追蹤，tooconfirm hello 命令中有第二個對話方塊。

![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)

當 hello 追蹤或作業都完成後，新的檔案會產生在 d:\\記錄\_集合 （或 hello 暫存磁碟機），名稱為**CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip。** 您可以傳送分析此檔案 toohello 支援代理程式。

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>檢閱 hello PerfInsights 所建立的診斷報告

Hello 內**CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip 檔案**PerfInsights 產生，則可以找到詳細資料的 hello 發現 HTML 報表PerfInsights。 tooreview hello 報表中，展開 hello **CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip**檔案，然後再開啟 hello **PerfInsights Report.html**檔案。

選取 hello**發現** 索引標籤。

![[尋找] 索引標籤](media/how-to-use-perfInsights/findingtab.png)

**注意事項**

-   紅色訊息是已知的設定問題，可能會導致效能問題。

-   黃色訊息是警告，表示不一定會造成效能問題的非最佳化設定。

-   藍色訊息僅為資訊聲明。

檢閱 hello 紅色 tooget 中的所有錯誤訊息的 HTTP 連結更詳細的 hello 發現與它們可能會如何影響 hello 效能最佳化組態的最佳作法的相關資訊。

### <a name="disk-configuration-tab"></a>[磁碟設定] 索引標籤

hello**概觀**區段會顯示 hello 存放裝置設定，包括從 Diskpart 與儲存空間資訊的不同檢視

hello **DiskMap**和**VolumeMap**各節說明如何邏輯雙重檢視方塊上的磁碟區和實體磁碟都是相關的 tooeach 其他。

Hello PhysicalDisk 檢視方塊 (DiskMap)，在 hello 資料表會顯示 hello 磁碟上執行的所有邏輯磁碟區。 在下列範例的 hello，PhysicalDrive2 執行 2 邏輯磁碟區建立多個資料分割 （J 和 H）：

![[資料] 索引標籤](media/how-to-use-perfInsights/disktab.png)

在 hello 磁碟區的檢視方塊中 (*VolumeMap*)，hello 表格顯示在每個邏輯磁碟區下的 hello 實體磁碟。 請注意，對於 RAID/動態磁碟，您可能會在多個實體磁碟上執行邏輯磁碟區。 在下列範例中的 hello *c:\\掛接*是設定為掛接點*SpannedDisk*上 PhysicalDisks \#2 和\#3:

![[磁碟區] 索引標籤](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>[SQL Server] 索引標籤

如果 hello 目標 VM 裝載任何 SQL Server 執行個體，您會看到 [其他] 索引標籤中名為 hello 報表**SQL Server**:

![[SQL] 索引標籤](media/how-to-use-perfInsights/sqltab.png)

本節包含 「 概觀 」 和其他的子索引標籤，每個 hello hello VM 上裝載的 SQL Server 執行個體。

hello < 概觀 > 一節包含很有幫助的資料表，可總結所有 hello 實體磁碟 （系統和資料磁碟） 正在執行，且包含混合資料檔和交易記錄檔。

在下列範例，hello *PhysicalDrive0* （執行 hello C 磁碟機） 會顯示，因為兩者 hello *modeldev*和*modellog*檔案位於 hello C 磁碟機，並他們屬於不同類型 (例如資料檔案和交易記錄檔，分別):

![loginfo](media/how-to-use-perfInsights/loginfo.png)

hello SQL Server 執行個體特有的索引標籤包含一般的區段會顯示 hello 選執行個體的基本資訊以及進階的資訊，包括設定、 組態和使用者選項的其他章節。

## <a name="references-toohello-external-tools-used"></a>參考用 toohello 外部工具

### <a name="diskspd"></a>Diskspd

DISKSPD 是儲存體負載產生器和效能測試工具從 hello Windows 和 Windows Server 和雲端伺服器基礎結構工程團隊。 如需詳細資訊，請參閱 [Diskspd](https://github.com/Microsoft/diskspd)。

### <a name="xperf"></a>XPerf

Xperf 是從 Windows 效能工具套件 hello 命令列工具 toocapture 追蹤。

如需詳細資訊，請參閱 [Windows 效能工具組 – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/)。

## <a name="next-steps"></a>後續步驟

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>上傳診斷記錄和報告 tooMicrosoft 支援供進一步檢閱

當您使用 hello Microsoft 支援人員時，您可能要求的 tootransmit hello 輸出 PerfInsights tooassist hello 疑難排解程序所產生。

hello 支援代理程式會建立 DTM 工作區，而且您會收到電子郵件訊息，其中包含連結 toohello [DTM 入口網站 (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) 以及唯一的使用者識別碼和密碼。

此訊息會從 **CTS 自動化診斷服務** (ctsadiag@microsoft.com) 傳送。

![Hello 訊息的範例](media/how-to-use-perfInsights/supportemail.png)

為了增加安全性，您將會需要的 toochange 您密碼上的第一次使用。

在您登入 tooDTM 之後，您會發現對話方塊方塊 tooupload hello **CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip** PerfInsights 收集的檔案。
