---
title: "Azure 進階儲存體：專為效能而設計 | Microsoft Docs"
description: "使用 Azure 進階儲存體設計高效能應用程式。 「進階儲存體」可針對在「Azure 虛擬機器」上執行且需要大量 I/O 的工作負載，提供高效能、低延遲的磁碟支援。"
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: dde3e60ae4c8387150b65f0715166b5d549891e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Azure 進階儲存體：專為高效能而設計
## <a name="overview"></a>Overview
這篇文章提供使用 Azure 進階儲存體來建置高效能應用程式的指導方針。 您可以使用 hello 結合效能最佳作法適用於 tootechnologies 應用程式使用本文件中提供的指示。 tooillustrate hello 指導方針，我們也可以使用 SQL Server 進階儲存體上執行做為整份文件的範例。

雖然我們解決本文章中的 hello 儲存層的效能案例，您將需要 toooptimize hello 應用程式層。 比方說，如果您裝載 SharePoint 伺服器陣列在 Azure 高階儲存體上，您可以使用 hello 從這個發行項 toooptimize hello 資料庫伺服器的 SQL Server 範例。 此外，最佳化 hello SharePoint 伺服器陣列的 Web 伺服器和應用程式伺服器 tooget hello 最高效能。

關於在 Azure 進階儲存體上將應用程式效能最佳化方面，本文有助於回答以下常見的問題。

* 如何 toomeasure 您應用程式的效能？  
* 為什麼看不到預期的高效能？  
* 哪些因素會影響進階儲存體上的應用程式效能？  
* 這些因素如何影響進階儲存體上的應用程式效能？  
* 如何最佳化 IOPS、頻寬和延遲？  

我們特別針對進階儲存體提供這些指導方針，因為進階儲存體上執行的工作負載非常重視效能。 我們在適當的地方都提供範例。 您也可以套用標準儲存體磁碟與 IaaS Vm 上執行這些指導方針 tooapplications 部分。

在開始，如果您是新 tooPremium 儲存體之前，先閱讀 hello[高階儲存體： Azure 虛擬機器工作負載的高效能儲存體](../storage-premium-storage.md)和[Azure 儲存體延展性和效能目標](storage-scalability-targets.md)文件。

## <a name="application-performance-indicators"></a>應用程式效能指標
我們會評估是否正在執行應用程式，或不使用指標類似的效能、 速度應用程式會處理使用者要求時，應用程式正在處理每個要求的資料量、 多少要求正在處理中特定的應用程式停留多久，使用者擁有 toowait tooget 回應在提交要求之後的期間。 IOPS、 輸送量或頻寬和延遲是這些效能指標 hello 術語。

在本節中，我們將討論中的進階儲存體的 hello 內容 hello 一般效能指標。 在 hello 下列區段中，收集應用程式的需求，您將學習如何 toomeasure 這些應用程式的效能指標。 在最佳化應用程式效能，稍後您將了解 hello 因素會影響這些效能指標和建議 toooptimize 它們。

## <a name="iops"></a>IOPS
IOPS 是數目，您的應用程式正在傳送 toohello 存放磁碟每秒的要求。 輸入/輸出作業可能是讀取或寫入、循序或隨機。 像線上零售網站的 OLTP 應用程式需要許多並行使用者要求立即 tooprocess。 hello 使用者插入和要求更新大量的資料庫交易，哪一個 hello 應用程式必須快速處理。 因此，OLTP 應用程式需要極高的 IOPS。 這類應用程式處理數百萬個小型和隨機的 IO 要求。 如果您有這樣的應用程式，您必須設計 hello 應用程式基礎結構 toooptimize 的 IOPS。 在 hello 稍後區段，*最佳化應用程式效能*，我們探討所有 hello 因素，您必須考慮 tooget 高 IOPS。

當您附加 premium 儲存體磁碟 tooyour 高擴充能力 VM，Azure 會佈建，讓您根據 hello 磁碟規格保證的 IOPS 數字。 例如，P50 磁碟會佈建 7500 IOPS。 每個高延展性 VM 大小也有它可承受的特定 IOPS 限制。 例如，標準 GS5 VM 以 80,000 IOPS 為限。

## <a name="throughput"></a>Throughput
輸送量或頻寬是 hello 的資料量，您的應用程式正在傳送 toohello 存放磁碟中指定的時間間隔。 如果應用程式以較大 IO 單位大小執行輸入/輸出作業，則需要較高輸送量。 資料倉儲應用程式通常 tooissue 掃描需要大量的作業，一次存取大型的資料部分，並經常執行大量作業。 換句話說，這類應用程式需要較高的輸送量。 如果您有這樣的應用程式，您必須設計其基礎結構 toooptimize 的輸送量。 我們討論詳細 hello 因數 hello 下一節，您必須此微調 tooachieve。

當您附加 premium 儲存體磁碟 tooa 高擴充能力 VM，Azure 會佈建輸送量根據該磁碟規格。 例如，P50 磁碟會佈建每秒 250 MB 的磁碟輸送量。 每個高延展性 VM 大小也有它可承受的特定輸送量限制。 例如，標準 GS5 VM 的輸送量上限為每秒 2,000 MB。 

沒有之間的輸送量和 IOPS hello 公式以下所示的關聯。

![](media/storage-premium-storage-performance/image1.png)

因此，它是重要的 toodetermine hello 最佳輸送量和 IOPS 值應用程式所需。 其中一個 toooptimize 再試一次，因為其他 hello 也取得受影響。 在稍後的 *最佳化應用程式效能*一節中，我們將更詳細討論最佳化 IOPS 和輸送量。

## <a name="latency"></a>Latency
延遲是 hello 花費的時間的應用程式 tooreceive 單一要求、 將它送出 toohello 存放磁碟和傳送 hello 回應 toohello 用戶端。 這是效能的重要的量值的加法 tooIOPS 和輸送量的應用程式。 hello premium 儲存體磁碟的延遲是 hello 時間 tooretrieve hello 資訊要求並傳達回 tooyour 應用程式。 進階儲存體提供一致的低延遲。 如果在進階儲存體磁碟上啟用 ReadOnly 主機快取，讀取延遲會非常低。 在稍後的 *最佳化應用程式效能*一節中，我們將更詳細討論磁碟快取。

當您要最佳化您的應用程式 tooget 更高的 IOPS 及輸送量，它會影響您的應用程式的延遲 hello。 微調之後 hello 應用程式效能，一定要評估 hello 的 hello 應用程式 tooavoid 延遲預期有高度延遲的行為。

## <a name="gather-application-performance-requirements"></a>收集應用程式效能需求
hello 中設計高效能應用程式在 Azure 高階儲存體上執行的第一個步驟是 toounderstand hello 應用程式的效能需求。 您收集的效能需求後，您可以最佳化應用程式 tooachieve hello 最佳效能。

Hello 前一節，我們將說明 hello 一般效能指標，IOPS、 輸送量和延遲。 您必須識別哪些這些效能指標是重大 tooyour 應用程式 toodeliver hello 預期使用者體驗。 例如，高 IOPS 重要大部分 tooOLTP 應用程式的每秒處理數百萬筆的交易。 然而，就每秒處理大量資料的資料倉儲應用程式而言，高輸送量很重要。 就即時視訊串流處理網站之類的即時應用程式而言，極低的延遲非常重要。

接下來，測量您的應用程式在其存留期 hello 最大的效能需求。 使用下面 hello 範例檢查清單是個起點。 在一般記錄 hello 最大的效能需求，尖峰和離峰時間的工作負載期間。 藉由識別所有工作負載層級的需求，您將無法 toodetermine hello 應用程式的整體效能需求。 比方說，hello 電子商務網站的一般工作負載將會是一年中大部分的指定天數內的 hello 交易。 hello 尖峰工作負載的 hello 網站將會是假日季節或特殊銷售事件期間的 hello 交易。 hello 尖峰工作負載通常有經驗的一段有限，但可能會要求您的應用程式 tooscale 兩個或多其正常作業。 了解 hello 50 個百分位數，90 個百分位數以及 99 個百分位數的需求。 這有助於篩選掉任何極端值，在 hello 效能需求，您可以專注於最佳化 hello 正確的值。

**應用程式效能需求檢查清單**

| **效能需求** | **50 百分位數** | **90 百分位數** | **99 百分位數** |
| --- | --- | --- | --- |
| 最大 每秒交易 | | | |
| % 讀取作業 | | | |
| % 寫入作業 | | | |
| % 隨機作業 | | | |
| % 循序作業 | | | |
| IO 要求大小 | | | |
| 平均輸送量 | | | |
| 最大 輸送量 | | | |
| 最小 延遲 | | | |
| 平均延遲 | | | |
| 最大 CPU | | | |
| 平均 CPU | | | |
| 最大 記憶體 | | | |
| 平均記憶體 | | | |
| 佇列深度 | | | |

> [!NOTE]
> 您應該預期應用程式未來的成長，據以調整這些數字。 因為它可能不容易 toochange hello 基礎結構，以改善之後的效能是個不錯的主意 tooplan 事先，成長。
>
>

如果您有現有的應用程式，並想 toomove tooPremium 存放裝置，請先建立 hello 的檢查清單上方 hello 現有應用程式。 接著，建立根據所述的指導方針的進階儲存體和設計 hello 應用程式上的應用程式的原型*最佳化應用程式效能*在本文件稍後的章節。 hello 下一節描述您可以使用 toogather hello 效能度量的 hello 工具。

建立的檢查清單類似 tooyour 現有應用程式 hello 原型。 您可以使用 Benchmarking 工具模擬 hello 工作負載及測量 hello 原型應用程式的效能。 請參閱 hello 章節[Benchmarking](#benchmarking) toolearn 更多。 這樣做可讓您判斷進階儲存體是否符合或超越應用程式效能需求。 然後您可以實作 hello 實際執行應用程式的相同指導方針。

### <a name="counters-toomeasure-application-performance-requirements"></a>計數器 toomeasure 應用程式效能需求
hello 應用程式的最佳方式 toomeasure 效能需求，hello 伺服器 hello 作業系統所提供的 toouse 效能監視工具。 您可以使用 Windows 的 PerfMon 和 Linux 的 iostat。 這些工具會擷取對應 tooeach 量值 hello 區段上面所述的計數器。 您的應用程式執行其一般、 尖峰和離峰時間的工作負載時，您必須擷取 hello 這些計數器的值。

hello PerfMon 計數器可用的處理器、 記憶體和，每個邏輯磁碟和實體磁碟，您的伺服器。 當您使用進階儲存體磁碟 vm 時，hello 實體磁碟計數器每個 premium 儲存體磁碟，而邏輯磁碟計數器 hello premium 儲存磁碟上建立的每個磁碟區。 您必須擷取 hello 裝載您的應用程式工作負載的 hello 磁碟的值。 如果有一個 tooone 之間的對應邏輯與實體磁碟，您可以參考 toophysical 磁碟計數器;否則，請參閱 toohello 邏輯磁碟計數器。 在 Linux 上 hello iostat 命令會產生的 CPU 和磁碟使用報告。 hello 磁碟使用量報表會提供每個實體裝置或分割區的統計資料。 如果資料庫伺服器的資料和記錄位於不同磁碟上，請同時從這兩個磁碟中收集這項資料。 下表說明磁碟、處理器和記憶體的計數器：

| 計數器 | 說明 | PerfMon | Iostat |
| --- | --- | --- | --- |
| **IOPS 或每秒交易數** |I/O 要求數目發出 toohello 存放裝置磁碟每秒。 |Disk Reads/sec  <br> Disk Writes/sec |tps  <br> r/s  <br> w/s |
| **磁碟讀取和寫入** |%的讀取和寫入 hello 磁碟上執行的作業。 |% Disk Read Time  <br> % Disk Write Time |r/s  <br> w/s |
| **輸送量** |讀取或寫入 toohello 磁碟每秒資料量。 |Disk Read Bytes/sec  <br> Disk Write Bytes/sec |kB_read/s <br> kB_wrtn/s |
| **延遲** |總時間 toocomplete 磁碟 IO 要求。 |Average Disk sec/Read  <br> Average disk sec/Write |await  <br> svctm |
| **IO 大小** |hello 大小的 I/O 要求發出 toohello 存放磁碟。 |Average Disk Bytes/Read  <br> Average Disk Bytes/Write |avgrq-sz |
| **佇列深度** |等候 toobe 讀取表單或寫入 toohello 存放裝置磁碟要求的未處理 I/O 數目。 |目前磁碟佇列長度 |avgqu-sz |
| **最大記憶體** |所需記憶體數量 toorun 應用程式順暢 |% Committed Bytes in Use |Use vmstat |
| **最大CPU** |CPU 數量順暢需要 toorun 應用程式 |% Processor time |%util |

深入了解 [iostat](http://linuxcommand.org/man_pages/iostat1.html) 和 [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx)。

## <a name="optimizing-application-performance"></a>最佳化應用程式效能
hello 影響效能的高階儲存體上執行的應用程式的主要因素是本質的 IO 要求，VM 大小、 磁碟大小、 磁碟、 磁碟快取、 執行緒和佇列深度的數字。 您可以控制這些因素與 hello 系統所提供的參數。 大部分的應用程式可能無法提供您選項 tooalter hello IO 大小和佇列深度直接。 例如，如果您使用 SQL Server，您無法選擇 hello IO 大小和佇列深度。 SQL Server 會選擇 hello 最佳 IO 大小和佇列深度值 tooget hello 最高效能。 它是重要 toounderstand hello 這兩種因素對效能的影響您應用程式，以便您可以提供適當的資源 toomeet 效能需求。

在本章節中，請參閱 toohello 應用程式需求檢查清單，讓您建立，tooidentify 需要多少 toooptimize 應用程式效能。 為基礎，您將會無法 toodetermine 其中的因素本節中您將需要 tootune。 toowitness hello 每個因素對效能的影響您應用程式，執行效能評定，在您的應用程式設定的工具。 請參閱 toohello [Benchmarking](#Benchmarking) hello 本文章最後的步驟 toorun 一般效能評定工具在 Windows 和 Linux Vm 上的一節。

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>最佳化 IOPS、輸送量和延遲的速覽
hello 下表摘要列出所有 hello 效能因素和 hello 步驟 toooptimize IOPS、 輸送量和延遲。 hello 後面此摘要的章節將說明每個因素是更深度。

| &nbsp; | **IOPS** | **輸送量** | **延遲** |
| --- | --- | --- | --- |
| **範例案例** |需要極高每秒交易速率的企業 OLTP 應用程式。 |處理大量資料的企業資料倉儲應用程式。 |接近即時的應用程式需要即時回應 toouser 要求，例如線上遊戲。 |
| 效能因素 | &nbsp; | &nbsp; | &nbsp; |
| **IO 大小** |較小 IO 大小會產生較高的 IOPS。 |較大 IO 大小 tooyields 較高的輸送量。 | &nbsp;|
| **VM 大小** |使用 IOPS 大於應用程式需求的 VM 大小。 請參閱這裡的 VM 大小及其 IOPS 限制。 |使用輸送量限制大於應用程式需求的 VM 大小。 請參閱這裡的 VM 大小及其輸送量限制。 |使用調整限制大於應用程式需求的 VM 大小。 請參閱這裡的 VM 大小及其限制。 |
| **磁碟大小** |使用 IOPS 大於應用程式需求的磁碟大小。 請參閱這裡的磁碟大小及其 IOPS。 |使用輸送量限制大於應用程式需求的磁碟大小。 請參閱這裡的磁碟大小及其輸送量限制。 |使用調整限制大於應用程式需求的磁碟大小。 請參閱這裡的磁碟大小及其限制。 |
| **VM 和磁碟調整限制** |應大於驅動的高階儲存體磁碟的 IOPS 總數附加 tooit hello VM 大小所選的 IOPS 限制。 |應大於總輸送量受到高階儲存體磁碟附加 tooit hello VM 大小所選的輸送量限制。 |Hello VM 大小所選的小數位數限制必須大於附加的高階儲存體磁碟的總小數位數限制。 |
| **磁碟快取** |與讀取大量作業 tooget 高階儲存體磁碟上啟用唯讀快取較高的讀取 IOPS。 | &nbsp; |啟用 premium 準備的大量作業 tooget 非常低的讀取延遲的儲存磁碟上的唯讀快取。 |
| **磁碟串接** |使用多個磁碟和等量磁碟區它們一起 tooget 合併的更高 IOPS 及輸送量限制。 請注意，hello 結合的限制每個 VM 應高於 hello 附加的高階磁碟的結合的限制。 | &nbsp; | &nbsp; |
| **等量大小** |在 OLTP 應用程式中，隨機小型 IO 模式使用較小的等量大小。 例如，SQL Server OLTP 應用程式使用等量大小 64KB。 |在資料倉儲應用程式中，循序大型 IO 模式使用較大的等量大小。 例如，SQL Server 資料倉儲應用程式使用 256KB 等量大小。 | &nbsp; |
| **多執行緒處理** |使用多執行緒 toopush 高的數字的要求 tooPremium 存放裝置，將會導致 toohigher IOPS 及輸送量。 例如，SQL Server 上設定高的 MAXDOP 值 tooallocate 更多的 Cpu tooSQL 伺服器。 | &nbsp; | &nbsp; |
| **佇列深度** |較大佇列深度會產生較高的 IOPS。 |較大佇列深度會產生較高的輸送量。 |較小佇列深度會產生較低的延遲。 |

## <a name="nature-of-io-requests"></a>IO 要求的本質
IO 要求是指應用程式執行的輸入/輸出作業單位。 識別 hello 本質的 IO 要求，隨機或循序讀取或寫入，小型或大型的可協助您判斷 hello 應用程式的效能需求。 它是非常重要的 toounderstand hello 性質的 IO 要求，toomake hello 正確決策設計您的應用程式基礎結構時。

IO 大小是 hello 的其中一個更重要的因素。 hello IO 大小是由您的應用程式所產生的 hello 輸入/輸出作業要求 hello 大小。 hello IO 大小會影響效能，尤其是在 hello IOPS 和 hello 應用程式的頻寬能夠 tooachieve。 hello 下列公式會顯示 hello 關係 IOPS、 IO 大小和頻寬/輸送量。  
    ![](media/storage-premium-storage-performance/image1.png)

某些應用程式可讓您 tooalter 其 IO 大小，但在某些應用程式不需要。 例如，SQL Server 判斷 hello 最佳 IO 大小本身，和不為使用者提供任何參數 toochange 它。 在 hello 另一方面，Oracle 提供呼叫的參數[DB\_封鎖\_大小](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815)使用您可以設定 hello hello 資料庫的 I/O 要求的大小。

如果您使用的應用程式不允許您 toochange hello IO 大小，用於這個發行項 toooptimize hello 效能是最相關的 tooyour 應用程式的 KPI hello 指導方針。 例如，

* OLTP 應用程式會產生數百萬個小型和隨機的 IO 要求。 toohandle 這些類型的 IO 要求，您必須設計您的應用程式基礎結構 tooget 高 IOPS。  
* 資料倉儲應用程式會產生大型和循序的 IO 要求。 toohandle 這些類型的 IO 要求，您必須設計您的應用程式基礎結構 tooget 較高的頻寬或輸送量。

如果您使用應用程式，可讓您 toochange hello IO 大小、 使用此規則的捲動方塊的 hello IO 此外大小 tooother 效能指導方針，

* 較小 IO 大小 tooget 高 IOPS。 例如，OLTP 應用程式使用 8 KB。  
* 較大 IO 大小 tooget 較高的頻寬輸送量。 例如，資料倉儲應用程式使用 1024 KB。

以下是範例上如何計算 hello IOPS 及輸送量/頻寬應用程式。 假設應用程式使用 P30 磁碟。 hello 的最大 IOPS 及輸送量/頻寬 P30 磁碟可以達到是 5000 IOPS 和 200 MB 秒分別。 現在，如果您的應用程式需要的 hello 的 hello P30 磁碟和您的最大 IOPS 使用 IO 小 8 kb 為單位，例如 hello 產生的頻寬，您將會無法 tooget 會是 40 MB 每秒。 不過，如果您的應用程式需要 hello 最大輸送量/頻寬從 P30 磁碟，而且您使用較大的 IO 大小類似 1024 KB，hello 產生 IOPS 將會更少 200 的 IOPS。 因此，微調 hello IO 大小，使其符合這兩個應用程式的 IOPS 及輸送量/頻寬需求。 下表摘要說明不同 IO 大小 hello 和其相對應 IOPS 及輸送量 P30 磁碟。

| 應用程式需求 | I/O 大小 | IOPS | 輸送量/頻寬 |
| --- | --- | --- | --- |
| 最大 IOPS |8 KB |5,000 |每秒 40 MB |
| 最大輸送量 |1024 KB |200 |每秒 200 MB |
| 最大輸送量 + 高 IOPS |64 KB |3,200 |每秒 200 MB |
| 最大 IOPS + 高輸送量 |32 KB |5,000 |每秒 160 MB |

tooget IOPS 與頻寬高於 hello 最大值的單一高階儲存體磁碟時，使用多個一起的高階磁碟。 例如，等量分割兩個 P30 磁碟 tooget 10000 IOPS 結合的 IOPS 或合併的輸送量為 400 MB 每秒。 Hello 下一節所述，您必須使用支援 hello 結合磁碟 IOPS 及輸送量的 VM 大小。

> [!NOTE]
> 隨著您增加任一 IOPS 或輸送量 hello 其他也會增加，請確定您不觸及輸送量或 hello 磁碟或 VM 的 IOPS 限制時增加其中一個。
>
>

toowitness hello 的 IO 大小對應用程式效能的影響，您可以執行您的 VM 和磁碟上的效能評定工具。 建立多個測試回合，並針對每個執行的 toosee hello 影響使用不同的 IO 大小。 請參閱 toohello [Benchmarking](#Benchmarking) hello 結尾這篇文章以取得詳細資料 > 一節。

## <a name="high-scale-vm-sizes"></a>高延展性 VM 大小
當您開始設計的應用程式時，其中第一個項目 toodo hello 是，選擇您的應用程式的 VM toohost。 進階儲存體提供高延展性 VM 大小，可以執行需要更高計算能力和較高本機磁碟 I/O 效能的應用程式。 這些 Vm 提供更快的處理器、 記憶體-核心比率較高，以及 Solid-State 磁碟機 (SSD) hello 本機磁碟。 高比例 Vm 支援進階儲存體的範例包括 hello DS、 DSv2 及 GS 系列 Vm。

高延展性 VM 有各種不同大小，以及不同數目的 CPU 核心、記憶體、作業系統和暫存磁碟大小。 每個 VM 的大小也會有資料磁碟，您可以連接 toohello VM 的最大數目。 因此，選擇 hello VM 大小會影響多少處理、 記憶體和儲存體容量可供您的應用程式。 它也會影響 hello 計算和儲存成本。 例如，以下是 hello 最大 VM 大小 DS 系列、 DSv2 系列和 GS 系列中的 hello 規格：

| VM 大小 | CPU 核心 | 記憶體 | VM 磁碟大小 | 最大 資料磁碟 | 快取大小 | IOPS | 頻寬快取 IO 限制 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |作業系統 = 1023 GB  <br> 本機 SSD = 224 GB |32 |576 GB |50,000 IOPS  <br> 每秒 512 MB |4,000 IOPS 和每秒 33 MB |
| Standard_GS5 |32 |448 GB |作業系統 = 1023 GB  <br> 本機 SSD = 896 GB |64 |4224 GB |80,000 IOPS  <br> 每秒 2,000 MB |5,000 IOPS 和每秒 50 MB |

tooview 的所有可用的 Azure VM 大小，完整清單，請參閱太[Windows VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[Linux VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 選擇符合的 VM 大小和小數位數 tooyour 預期應用程式效能需求。 此外 toothis，考慮下列情況選擇 VM 大小的重要考量。

*調整限制*  
hello 最大 IOPS 限制每個 VM 和每個磁碟都不同，且彼此獨立。 請確定 hello 應用程式正在推動 IOPS，hello VM 以及 hello premium 磁碟附加的 tooit hello 限制範圍內。 否則，應用程式效能會發生節流現象。

例如，假設應用程式需求是最高 4,000 IOPS。 tooachieve 此，您佈建 P30 磁碟 DS1 VM 上。 hello P30 磁碟可以 too5，000 IOPS 向上傳遞。 不過，hello DS1 VM 是有限的 too3，200 的 IOPS。 因此，hello 應用程式的效能會受到 hello VM 3,200 IOPS 限制，而且會降低的效能。 tooprevent 這種情況下，選擇 VM 和磁碟大小，將這兩個符合應用程式的需求。

*作業成本*  
在許多情況下，使用進階儲存體的整體作業成本，可能會低於使用標準儲存體。

例如，假設應用程式需要 16,000 IOPS。 tooachieve 這種效能，您將需要標準\_D14 Azure IaaS VM，而可再提供使用 32 標準儲存體 1 TB 磁碟 16000 最大值 IOPS。 每個 1TB 標準儲存體磁碟最高可達到 500 IOPS。 hello 估計 $1,570 進行的每月 VM 的成本。 $1,638 進行 hello 32 個標準儲存體磁碟的每月成本。 hello 預估每月成本的總計會是 $3,208。

相同但是 hello 如果您裝載高階儲存體上的應用程式，您將需要較小的 VM 大小和較少的高階儲存體磁碟，進而降低整體成本的 hello。 標準\_DS13 VM 可以符合 hello 16000 IOPS 需求使用四個 P30 磁碟。 hello DS13 VM 25,600 最大 IOPS，每個 P30 磁碟 5,000 最大值 IOPS。 整體來說，這項設定可以達到 5,000 x 4 = 20,000 IOPS。 hello 估計 $1,003 進行的每月 VM 的成本。 $544.34 進行 hello 的四個 P30 高階儲存體磁碟的每月成本。 hello 預估每月成本的總計會是 $1,544。

下表摘要說明 hello 成本分解的這種情況下，Standard 和 Premium 儲存體。

| &nbsp; | **標準** | **高級** |
| --- | --- | --- |
| **每月的 VM 成本** |$1,570.58 (Standard\_D14) |$1,003.66 (Standard\_DS13) |
| **每月的磁碟成本** |$1,638.40 (32 x 1 TB 磁碟) |$544.34 (4 x P30 磁碟) |
| **每月的整體成本** |$3,208.98 |$1,544.34 |

*Linux 散發版本*  

透過 Azure 高階儲存體，您可以取得 hello 相同的 Vm 執行 Windows 和 Linux 的效能層級。 我們支援許多種 Linux 散發版本，而您可以看到 hello 完成清單[這裡](../../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 請務必不同的散發版本是較佳的 toonote 適合不同類型的工作負載。 您會看到不同層級的效能視 hello distro 執行您的工作負載而定。 測試您的應用程式的 hello Linux 散發版本，然後選擇最適合的其中一個 hello。

當執行 Linux 與高階儲存體時，請檢查 hello 必要的驅動程式 tooensure 高效能的相關最新的更新。

## <a name="premium-storage-disk-sizes"></a>進階儲存體磁碟大小
Azure 進階儲存體目前提供七種磁碟大小。 對於 IOPS、頻寬和儲存體，每個磁碟大小各有不同的調整限制。 選擇 hello 正確 Premium 儲存體磁碟的大小視 hello 應用程式需求和 hello 高擴充能力的 VM 大小。 hello 下表顯示 hello 七個磁碟大小及其功能。 受控磁碟目前僅支援 P4 和 P6 大小。

| 進階磁碟類型  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 磁碟大小           | 32 GB | 64 GB | 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| 每一磁碟的 IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| 每一磁碟的輸送量 | 每秒 25 MB  | 每秒 50 MB  | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB | 


所選大小的選擇取決於 hello 磁碟的磁碟數目。 您可以使用單一 P50 磁碟或多個 P10 磁碟 toomeet 您應用程式的需求。 請考慮進行 hello 選擇時下, 面所列的帳戶考量。

*調整限制 (IOPS 和輸送量)*  
hello IOPS 及輸送量限制每個 Premium 磁碟大小是不同，不受影響從 hello VM 規模限制。 確定 hello IOPS 總數，而且從 hello 磁碟輸送量的 hello 的小數位數限制範圍內選擇的 VM 大小。

例如，如果應用程式需求是輸送量上限 250 MB/秒，而且您使用 DS4 VM 搭配單一 P30 磁碟。 hello DS4 VM 可以放棄 too256 MB/sec 輸送量。 不過，單一 P30 磁碟有 200 MB/秒的輸送量限制。因此，hello 應用程式將會限制在 200 MB/秒到期 toohello 磁碟的限制。 tooovercome 此限制，佈建多個資料磁碟 toohello VM 或調整您的磁碟 tooP40 或 P50。

> [!NOTE]
> Hello 磁碟 IOPS 及輸送量中不包含由 hello 快取的讀取，因此沒有主體 toodisk 限制。 對於每個 VM，快取有其個別的 IOPS 和輸送量限制。
>
> 例如，剛開始時，讀取和寫入分別為 60 MB/秒和 40 MB/秒。 經過一段時間，hello 快取 warms 並且提供越來越多的 hello 讀取 hello 快取中使用。 然後，您可以從 hello 磁碟取得更高版本寫入輸送量。
>
>

*磁碟數量*  
判斷的磁碟，您必須透過評估應用程式需求的 hello 數目。 每個 VM 的大小也會具有 hello 數目，您可以附加 toohello VM 的磁碟上的限制。 一般而言，這是兩次 hello 核心數目。 請確定該 hello 您選擇可以支援所需的磁碟的 hello 數目的 VM 大小。

請記住，hello Premium 儲存體磁碟有較高的效能比較功能 tooStandard 存放磁碟。 因此，如果您要移轉您的應用程式，從使用標準儲存體 tooPremium 儲存體的 Azure IaaS VM，您可能需要較少的高階磁碟 tooachieve hello 應用程式的相同或更高的效能。

## <a name="disk-caching"></a>磁碟快取
採用 Azure 進階儲存體的高延展性 VM 有一項稱為 BlobCache 的多層快取技術。 BlobCache 結合了 hello 虛擬機器的 RAM 與 SSD 本機快取。 此快取可用 hello 高階儲存體持續性及 hello VM 本機磁碟。 根據預設，此快取設定為 tooRead 寫 OS 磁碟和 ReadOnly，進階儲存體上裝載的資料磁碟。 與 hello Premium 儲存體磁碟上啟用快取的磁碟，hello 高擴充能力 Vm 可以達到非常高的效能超過 hello 基礎磁碟效能。

> [!WARNING]
> 變更 hello Azure 磁碟快取設定卸離及重新附加 hello 目標磁碟。 如果它是 hello 作業系統磁碟時，會重新啟動 hello VM。 停止所有應用程式/服務，可能會受到此中斷作業再變更 hello 磁碟快取設定。
>
>

toolearn 有關 BlobCache 的運作方式的詳細資訊，請參閱內部 toohello [Azure 高階儲存體](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)部落格文章。

重要 tooenable hello 右一組磁碟上的快取它。 您應該啟用 premium 磁碟上的磁碟快取，或不將取決於 hello 工作負載模式的磁碟將會處理。 下表顯示 hello 預設 OS 和資料磁碟的快取設定。

| **磁碟類型** | **預設快取設定** |
| --- | --- |
| 作業系統磁碟 |讀寫 |
| 資料磁碟 |None |

下列是 hello 建議的磁碟快取設定的資料磁碟

| **磁碟快取設定** | **建議何時 toouse 這項設定** |
| --- | --- |
| None |針對唯寫和大量寫入的磁碟，將主機快取設定為「無」。 |
| 唯讀 |針對唯讀和讀寫的磁碟，將主機快取設定為「唯讀」。 |
| 讀寫 |依照 ReadWrite 只有當應用程式適當地處理寫入快取資料 toopersistent 磁碟需要時，請設定主機快取。 |

*唯讀*  
您可以在進階儲存體資料磁碟上設定「唯讀」快取，讓應用程式達到較低的讀取延遲，以及非常高的讀取 IOPS 和輸送量。 這是基於兩個理由，

1. 從快取，位於 hello VM 記憶體和本機 SSD 執行讀取，速度比在 hello Azure blob 儲存體 hello 資料磁碟的讀取次數。  
2. 高階儲存體不會計算的 hello 讀取由快取中，向 hello 磁碟 IOPS 及輸送量。 因此，您的應用程式是可以 tooachieve 較高的總 IOPS 及輸送量。

*讀寫*  
根據預設，hello OS 磁碟會有啟用 ReadWrite 快取。 我們最近也已在資料磁碟上增加支援「讀寫」快取。 如果您使用 ReadWrite 快取，您必須從快取 toopersistent 磁碟的正確方式 toowrite hello 資料。 例如，SQL Server 撰寫的控點快取資料 toohello 永續性儲存體磁碟本身。 不會處理保存的 hello 的應用程式中使用 ReadWrite 快取資料可能會導致 toodata 遺失，如果需要 hello VM 損毀。

例如，您可以套用這些指導方針 tooSQL 伺服器進行 hello 下列高階儲存體上執行

1. 在裝載資料檔的進階儲存體磁碟上設定「唯讀」快取。  
   a.  hello 快速讀取快取較低 hello SQL Server 查詢時，因為從 hello 從 hello 資料磁碟的快取比較 toodirectly 更快速擷取資料頁。  
   b.  由快取來服務讀取，表示高階資料磁碟會有額外的輸送量可用。 SQL Server 可以使用這個額外的輸送量來擷取更多資料頁和執行其他作業，例如備份/還原、批次載入和索引重建。  
2. 設定"None"高階儲存體上的快取磁碟裝載 hello 記錄檔。  
   a.  記錄檔以大量寫入的作業為主。 因此，它們不會受益於 hello 唯讀快取。

## <a name="disk-striping"></a>磁碟串接
當 VM 連接的數個 premium 儲存體永續性磁碟，hello 磁碟高擴充能力可以是等量一起 tooaggregate 其 IOPs、 頻寬和儲存體容量。

在 Windows 中，您可以一起使用儲存空間 toostripe 磁碟。 您必須為集區中的每個磁碟設定一欄。 否則，hello 的等量磁碟區的整體效能可能低數目超出預期，因為 toouneven hello 磁碟之間的流量分散。

重要事項： 使用伺服器管理員 」 UI，您可以設定 hello 總數 too8 等量磁碟區上的資料行。 在附加時 8 個以上的磁碟，請使用 PowerShell toocreate hello 磁碟區。 使用 PowerShell，您可以設定資料行的 hello 數目等於 toohello 磁碟數目。 例如，如果有 16 個磁碟，在單一的等量集;指定 16 個資料行中 hello *NumberOfColumns* hello 參數*New-virtualdisk* PowerShell cmdlet。

On Linux，請同時使用 hello MDADM 公用程式 toostripe 磁碟。 如需在 Linux 上的等量磁碟的詳細的步驟，請參閱太[Linux 上的 設定軟體 RAID](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

*等量大小*  
磁碟條狀配置中的重要組態是 hello 等量磁碟區大小。 hello 等量磁碟區大小或區塊大小是 hello 最小區塊的應用程式可以解決在等量磁碟區的資料。 您所設定的 hello 等量磁碟區大小取決於 hello 類型的應用程式和它的要求模式。 如果您選擇 hello 錯誤等量磁碟區大小，它可能會導致 tooIO 對齊錯誤，導致 toodegraded 應用程式的效能。

例如，如果您的應用程式所產生的 IO 要求大於 hello 磁碟等量磁碟區大小，hello 儲存系統將它寫入之間 stripe 單元界限在多個磁碟上。 當它是時間 tooaccess 該資料時，它會有 tooseek 跨越一個以上的等量磁碟區單位 toocomplete hello 要求。 這類行為的 hello 累加的效果可能會導致 toosubstantial 效能降低。 在 hello 另一方面，如果 hello IO 要求的大小會小於等量磁碟區大小，而且如果它是隨機的 hello 的 IO 要求可能會加總 hello 上相同磁碟造成瓶頸和最終降低 hello IO 效能。

根據您的應用程式正在執行的工作負載 hello 類型，選擇適當的等量磁碟區大小。 對於隨機小型 IO 要求，請使用較小的等量大小。 對於大型循序 IO 要求，請使用較大的等量大小。 找出 hello 等量磁碟區大小 hello 應用程式建議您將在高階儲存體上執行。 對於 SQL Server 而言，請將 OLTP 工作負載的等量大小設定為 64KB，而資料倉儲工作負載則設定為 256KB。 請參閱[Azure Vm 上的 SQL Server 的效能最佳做法](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance)toolearn 更多。

> [!NOTE]
> 在 DS 系列 VM 上，最多可以串接 32 個進階儲存體磁碟，而在 GS 系列 VM 上，最多可以串接 64 個進階儲存體磁碟。
>
>

## <a name="multi-threading"></a>多執行緒處理
設計 azure 高階儲存體的平台 toobe 大量平行。 因此，多執行緒應用程式可達到的效能遠高於單一執行緒應用程式。 多執行緒應用程式跨多個執行緒會分割其工作，並提升其利用 hello VM 所執行的效率與最大的磁碟資源 toohello。

例如，如果您的應用程式在單一核心 VM 使用兩個執行緒上執行，hello CPU 可以 hello 兩個執行緒 tooachieve 效率之間切換。 當一個執行緒正在等候磁碟 IO toocomplete 時，hello CPU 可以在另一個執行緒切換 toohello。 如此一來，兩個執行緒可以完成比單一執行緒更多的工作。 如果 hello VM 有多個核心，進一步減少執行時間，因為每個核心可以平行執行的工作。

您可能不是能 toochange hello 方式現成的應用程式實作單一執行緒或多執行緒處理。 例如，SQL Server 能夠處理多 CPU 與多核心。 不過，SQL Server 會決定在哪些情況下，它將會利用一個或多個執行緒 tooprocess 查詢。 它可以使用多執行緒來執行查詢和建立索引。 包含的查詢，聯結大型資料表和排序資料，傳回 toohello 使用者之前，SQL Server 將可能使用多個執行緒。 但是，使用者無法控制 SQL Server 使用單一執行緒或多個執行緒來執行查詢。

沒有組態設定，您可以更改 tooinfluence 此多執行緒處理或平行處理的應用程式。 例如，如果 SQL Server 是 hello 最大 Degree of Parallelism 組態。 呼叫 MAXDOP，此設定可讓您 tooconfigure hello 最大處理器數目平行處理時，可以使用 SQL Server。 您可以為個別的查詢或索引作業設定 MAXDOP。 當您需要 toobalance 資源系統的效能關鍵應用程式時，這是有幫助。

例如，假設您使用 SQL Server 的應用程式正在執行大型查詢和索引的作業在 hello 相同的時間。 讓我們假設您想 hello 索引作業 toobe 詳細比較高效能 toohello 大型查詢。 在這種情況下，您可以設定 hello 高於 hello hello 查詢 MAXDOP 值的索引作業 toobe MAXDOP 的值。 如此一來，SQL Server 有更多數目的供 hello 索引作業比較 toohello 數目它可以設定專用的處理器的處理器 toohello 大型查詢。 請記住，您無法控制 hello SQL Server 會使用每個作業的執行緒數目。 您可以控制 hello 正在專用的處理器數目上限多執行緒處理。

深入了解 SQL Server 中的 [平行處理原則的程度](https://technet.microsoft.com/library/ms188611.aspx) 。 了解這類設定會影響您的應用程式和其組態 toooptimize 效能，多執行緒處理。

## <a name="queue-depth"></a>佇列深度
hello 佇列深度或佇列長度，或佇列大小是 hello 數暫止的 IO 要求 hello 系統中。 佇列深度 hello 值決定多少 IO 作業可以對齊您的應用程式，將處理哪些 hello 存放磁碟。 它會影響所有 hello 三個應用程式效能指標，此文章 viz.IOPS、 輸送量和延遲所述。

佇列深度與多執行緒處理密切相關。 hello 佇列深度的值會指出多少多執行緒處理可以達成 hello 應用程式。 Hello 佇列深度很大，如果應用程式可以執行更多作業同時，亦即，更多執行緒處理。 如果 hello 佇列深度小，即使應用程式為多執行緒，它將會沒有足夠的請求，並行執行的方式。

一般而言，關閉 hello 放到書架應用程式不允許您 toochange hello 佇列深度，因為如果設定不正確，它會執行弊多於利。 應用程式會設定佇列深度 tooget hello 達到最佳效能的 hello 右值。 不過，它是重要 toounderstand 這個概念，以便疑難排解您的應用程式的效能問題。 您也可以觀察 hello 效果佇列深度的系統上執行效能評定工具。

某些應用程式提供設定 tooinfluence hello 佇列深度。 例如，SQL Server 中的 hello MAXDOP （最大平行處理原則程度） 設定先前一節所述。 MAXDOP 是方式 tooinfluence 佇列深度和多執行緒處理，雖然它不會直接變更的 SQL Server hello 佇列深度的值。

*高佇列深度*  
高佇列深度排列 hello 磁碟上的更多作業。 hello 磁碟知道 hello 事先其佇列中的下一個要求。 因此，hello 磁碟可以排程作業事先，而且最佳的順序處理它們。 Hello 應用程式傳送多個要求 toohello 磁碟，因為 hello 磁碟可以處理多個平行 IOs。 最後，hello 應用程式將會無法 tooachieve 高 IOPS。 應用程式正在處理其他要求，因為 hello hello 應用程式的總輸送量也會增加。

通常，當每個連接的磁碟上有 8-16+ 個未完成的 IO 時，應用程式可以達到最大輸送量。 如果佇列深度是其中一個，應用程式不會將推送足夠 IOs toohello 系統，並會在指定時間處理較少數量。 換句話說，輸送量較少。

例如，在 SQL Server，設定 hello MAXDOP 值的查詢太"4"會通知它 toofour 核心 tooexecute hello 查詢可以使用的 SQL Server。 SQL Server 將會決定最佳佇列深度值和 hello 的核心數目為 hello 查詢執行。

*最佳佇列深度*  
佇列深度值太高也有其缺點。 如果佇列深度的值太高，hello 應用程式會嘗試 toodrive 非常高 IOPS。 除非應用程式的永續性磁碟已佈建足夠的 IOPS，否則這可能對應用程式延遲造成負面影響。 下列公式會顯示 hello IOPS、 延遲和佇列深度之間的關聯性。  
    ![](media/storage-premium-storage-performance/image6.png)

您不應該設定佇列深度 tooany 高價值，但 tooan 最佳值，可以提供足夠的 IOPS 供 hello 應用程式，而不會影響延遲。 比方說，如果 hello 應用程式的延遲需要 toobe 1 毫秒，hello 佇列深度所需的 tooachieve 5,000 IOPS 即 QD = 5000 x 0.001 = 5。

*等量磁碟區的佇列深度*  
對於等量磁碟區，應該維持夠高的佇列深度，讓每個磁碟有各自的尖峰佇列深度。 例如，請考慮推播通知的佇列深度為 2 的應用程式和 hello 等量磁碟區中有 4 個磁碟。 hello 兩個的 IO 要求將會移 tootwo 磁碟，而剩餘的兩個磁碟會處於閒置狀態。 因此，設定 hello 佇列深度，使所有 hello 磁碟可以都是忙碌中。 下列公式會顯示如何 toodetermine hello 的等量磁碟區的佇列深度。  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>節流
Azure 高階儲存體佈建指定數目的 IOPS 及輸送量視 hello VM 大小和您所選擇的磁碟大小而定。 每當您的應用程式會嘗試 toodrive IOPS 或輸送量上方的哪一個 hello VM 或磁碟可以處理這些限制，進階儲存體便會進行節流。 這會表示 hello 表單的應用程式中的效能降低的問題。 這可能表示延遲較高、輸送量較低或 IOPS 較低。 如果進階儲存體不會節流，應用程式可能會超出其資源的能力負荷而完全失敗。 因此，tooavoid 效能發出到期 toothrottling，一律佈建足夠的資源應用程式。 請考量前述 hello VM 大小和上述的磁碟大小章節中。 效能評定，是最佳方式 toofigure hello 出哪些資源要 toohost 您的應用程式。

## <a name="benchmarking"></a>效能評定
效能評定，是模擬您的應用程式上的不同工作負載，以及測量 hello 應用程式效能，每個工作負載的 hello 程序。 使用前一節中所述的 hello 步驟，您已經收集 hello 應用程式效能需求。 藉由執行效能評定 hello hello 應用程式裝載的 Vm 上的工具，您可以判斷您的應用程式可以達到進階儲存體的 hello 效能層級。 在本節中，我們針對以 Azure 進階儲存體佈建的標準 DS14 VM，提供效能評定範例。

我們分別在 Windows 和 Linux 上使用一般效能評定工具 Iometer 和 FIO。 這些工具會繁衍多個執行緒模擬實際執行類似工作負載，以及測量 hello 系統效能。 使用 hello 工具您也可以設定的參數如區塊大小和佇列深度，您通常不能變更應用程式。 這可讓您更大的彈性 toodrive hello 最高效能大規模使用不同類型的應用程式工作負載的高階磁碟佈建的 VM 上。 有關每個效能評定的工具，請瀏覽的 toolearn [Iometer](http://www.iometer.org/)和[FIO](http://freecode.com/projects/fio)。

toofollow hello 以下範例中，建立標準的 DS14 VM，並附加 11 高階儲存體磁碟 toohello VM。 Hello 11 磁碟、 設定 10 個磁碟具有主機快取為"None"和 stripe 它們入呼叫 NoCacheWrites 磁碟區。 設定為"ReadOnly"hello 剩餘磁碟的快取的主機，並建立呼叫 CacheReads 與此磁碟的磁碟區。 使用此安裝程式，您將無法 toosee hello 最大讀取和寫入效能標準的 DS14 VM。 如需使用高階磁碟建立 DS14 VM 的詳細步驟，請移至太[建立和使用進階儲存體帳戶的虛擬機器資料磁碟](../storage-premium-storage.md)。

*暖機 hello 快取*  
ReadOnly 主機快取與 hello 磁碟是可以 toogive hello 磁碟限制比高 IOPS。 tooget 此上限值讀取效能 hello 主機快取，首先您必須準備此磁碟的 hello 快取。 這可確保該 hello 哪一種效能評定工具將 CacheReads 磁碟區的磁碟機讀取 IOs 實際叫用 hello 快取而且不 hello 磁碟直接。 hello 快取命中結果中的 hello 單一快取的其他 IOPS 啟用磁碟。

> **重要事項：**  
> 您必須準備 hello 快取，然後再執行效能評定，每次重新啟動 VM。
>
>

#### <a name="iometer"></a>Iometer
[下載 hello Iometer 工具](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download)hello VM 上。

*測試檔案*  
Iometer 使用，您會在其執行效能測試的 hello hello 磁碟區儲存的測試檔案。 它在磁碟機讀取和寫入這個測試檔案 toomeasure hello 磁碟 IOPS 及輸送量。 如果您沒有提供此測試檔案，Iometer 會建立測試檔案。 建立 hello CacheReads 和 NoCacheWrites 磁碟區上呼叫 iobw.tst 200 GB 測試檔案。

*存取規格*  
hello 規格，要求 IO 大小，%讀取/寫入，%隨機/循序未設定使用中 Iometer hello 」 的存取規格 」 索引標籤。 每個 hello 案例，如下所述建立存取規格。 建立 hello 存取規格，並 [儲存] 以適當命名像 RandomWrites\_8k RandomReads\_8k。 執行 hello 測試案例時，請選取 hello 對應規格。

以下顯示最大寫入 IOPS 案例的存取規格範例，  
    ![](media/storage-premium-storage-performance/image8.png)

*最大 IOPS 測試規格*  
toodemonstrate 最大 IOPs，使用較小的要求大小。 使用 8K 要求大小，並建立隨機寫入和讀取的規格。

| 存取規格 | 要求大小 | 隨機 % | 讀取 % |
| --- | --- | --- | --- |
| RandomWrites\_8K |8K |100 |0 |
| RandomReads\_8K |8K |100 |100 |

*最大輸送量測試規格*  
toodemonstrate 最大的輸送量，使用較大要求大小。 使用 64K 要求大小，並建立隨機寫入和讀取的規格。

| 存取規格 | 要求大小 | 隨機 % | 讀取 % |
| --- | --- | --- | --- |
| RandomWrites\_64K |64K |100 |0 |
| RandomReads\_64K |64K |100 |100 |

*執行 hello Iometer 測試*  
執行下列 toowarm 快取的 hello 步驟

1. 使用如下所示的值建立兩個存取規格

   | 名稱 | 要求大小 | 隨機 % | 讀取 % |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1MB |100 |0 |
   | RandomReads\_1MB |1MB |100 |100 |
2. 執行 hello Iometer 測試初始化快取磁碟，並指定下列參數。 使用三個背景工作執行緒 hello 目標磁碟區，以及 128 的佇列深度。 設定 hello hello 測試 too2hrs hello [測試 Setup] 索引標籤上的 「 執行時間 」 的持續時間。

   | 案例 | 目標磁碟區 | 名稱 | 持續時間 |
   | --- | --- | --- | --- |
   | 初始化快取磁碟 |CacheReads |RandomWrites\_1MB |2 小時 |
3. 執行 hello Iometer 測試暖機使用下列參數的快取磁碟。 使用三個背景工作執行緒 hello 目標磁碟區，以及 128 的佇列深度。 設定 hello hello 測試 too2hrs hello [測試 Setup] 索引標籤上的 「 執行時間 」 的持續時間。

   | 案例 | 目標磁碟區 | 名稱 | 持續時間 |
   | --- | --- | --- | --- |
   | 準備快取磁碟 |CacheReads |RandomReads\_1MB |2 小時 |

快取磁碟就緒之後，繼續下面所列的 hello 測試案例。 toorun hello Iometer 測試使用至少三個工作者執行緒**每個**目標磁碟區。 每個背景工作執行緒，選取 hello 目標磁碟區、 設定佇列深度並選取一個 hello 儲存測試規格，hello 資料表 toorun hello 對應的測試案例如下所示。 hello 資料表也會顯示預期的結果的 IOPS 及輸送量時執行這些測試。 在所有案例中，都使用較小的 IO 大小 8 KB 和較高的佇列深度 128。

| 測試案例 | 目標磁碟區 | 名稱 | 結果 |
| --- | --- | --- | --- |
| 最大 讀取 IOPS |CacheReads |RandomWrites\_8K |50,000 IOPS  |
| 最大 寫入 IOPS |NoCacheWrites |RandomReads\_8K |64,000 IOPS |
| 最大 結合的 IOPS |CacheReads |RandomWrites\_8K |100,000 IOPS |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| 最大 讀取 MB/秒 |CacheReads |RandomWrites\_64K |524 MB/秒 |
| 最大 寫入 MB/秒 |NoCacheWrites |RandomReads\_64K |524 MB/秒 |
| 結合的 MB/秒 |CacheReads |RandomWrites\_64K |1000 MB/秒 |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

以下是 hello 的螢幕擷取畫面 Iometer 結合的 IOPS 及輸送量案例的測試結果。

*結合的讀取和寫入最大 IOPS*  
![](media/storage-premium-storage-performance/image9.png)

*結合的讀取和寫入最大輸送量*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO 為普遍使用的工具 toobenchmark 儲存 hello Linux Vm 上。 它擁有 hello 彈性 tooselect IO 大小不同，連續或隨機讀取和寫入。 它會產生背景工作執行緒或處理程序 tooperform hello 指定 I/O 作業。 您可以指定 hello 類型的 I/O 作業每個工作者執行緒必須使用工作檔案執行。 我們建立一個工作檔案，每個以下的 hello 範例中所述的案例。 您可以變更這些工作檔案 toobenchmark 不同工作負載在高階儲存體上執行中的 hello 規格。 在 hello 範例中，我們會使用標準的 DS 14 VM 執行**Ubuntu**。 使用相同的安裝程式所述的 hello hello 開頭的 hello[效能評定區段](#Benchmarking)和熱機 hello 快取，才能執行效能測試的 hello。

開始進行之前，請先在虛擬機器上 [下載 FIO](https://github.com/axboe/fio) 並安裝。

執行 hello Ubuntu，如下列命令

```
apt-get install fio
```

我們將使用來推動寫入作業的四個工作者執行緒和四個背景工作執行緒驅動 hello 磁碟上的讀取作業。 hello 寫入背景工作將會推動流量具有 10 的磁碟快取設定太 hello 「 無 」 磁碟區上 「 無 」。 hello 讀取背景工作將會推動流量 hello"readcache 「 磁碟區，也有 1 個磁碟快取設定"ReadOnly"。

*最大寫入 IOPS*  
建立具有下列規格 tooget hello 工作檔案寫入的最大 IOPS。 將它命名為 "fiowrite.ini"。

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

請注意 hello 遵循遵循先前章節所述的 hello 設計指導方針的重要事情。 這些規格是不可或缺的 toodrive 最大 IOPS  

* 較高的佇列深度 256。  
* 較小的區塊大小 8KB。  
* 執行隨機寫入的多個執行緒。

執行下列的 hello FIO 測試 30 秒，關閉命令 tookick hello  

```
sudo fio --runtime 30 fiowrite.ini
```

雖然 hello 測試執行時，您會無法 toosee hello 數目寫入 IOPS hello VM 和 Premium 磁碟傳遞。 Hello 以下範例所示，hello DS14 VM 會將其最大寫入 IOPS 限制的 50,000 的 IOPS。  
    ![](media/storage-premium-storage-performance/image11.png)

*最大讀取 IOPS*  
建立具有下列規格 tooget hello 工作檔案讀取的最大 IOPS。 將它命名為 "fioread.ini"。

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

請注意 hello 遵循遵循先前章節所述的 hello 設計指導方針的重要事情。 這些規格是不可或缺的 toodrive 最大 IOPS

* 較高的佇列深度 256。  
* 較小的區塊大小 8KB。  
* 執行隨機寫入的多個執行緒。

執行下列的 hello FIO 測試 30 秒，關閉命令 tookick hello

```
sudo fio --runtime 30 fioread.ini
```

Hello 測試執行時，您將會是能 toosee hello 數讀取 IOPS hello VM，並提供高階磁碟。 Hello 以下範例所示，hello DS14 VM 會將超過 64000 讀取 IOPS。 這是 hello 磁碟和 hello 快取效能的組合。  
    ![](media/storage-premium-storage-performance/image12.png)

*最大讀取和寫入 IOPS*  
建立 hello 工作檔案的最大的下列規格 tooget 結合讀取和寫入的 IOPS。 將它命名為 "fioreadwrite.ini"。

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

請注意 hello 遵循遵循先前章節所述的 hello 設計指導方針的重要事情。 這些規格是不可或缺的 toodrive 最大 IOPS

* 較高的佇列深度 128。  
* 較小的區塊大小 4KB。  
* 執行隨機讀取和寫入的多個執行緒。

執行下列的 hello FIO 測試 30 秒，關閉命令 tookick hello

```
sudo fio --runtime 30 fioreadwrite.ini
```

Hello 測試執行時，您將無法 toosee hello 數目結合讀取和寫入 IOPS hello VM 提供高階磁碟。 Hello 以下範例所示，hello DS14 VM 會將 100,000 個以上的組合的讀取和寫入的 IOPS。 這是 hello 磁碟和 hello 快取效能的組合。  
    ![](media/storage-premium-storage-performance/image13.png)

*結合的最大輸送量*  
最大 tooget hello 組合讀取和寫入的輸送量，請使用較大的區塊大小和大佇列深度具有多個執行緒執行讀取和寫入。 您可以使用 64KB 的區塊大小和 128 的佇列深度。

## <a name="next-steps"></a>後續步驟
深入了解 Azure 進階儲存體：

* [Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../storage-premium-storage.md)  

若為 SQL Server 使用者，請參閱「SQL Server 的效能最佳作法」文章：

* [Azure 虛擬機器中的 SQL Server 效能最佳作法](../../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Azure 進階儲存體為 Azure VM 中的 SQL Server 提供最高效能](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
