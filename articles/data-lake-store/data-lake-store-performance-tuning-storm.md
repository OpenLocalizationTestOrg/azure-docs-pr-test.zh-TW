---
title: "aaaAzure 資料湖存放區 Storm 效能調整指導方針 |Microsoft 文件"
description: "Azure Data Lake Store Storm 效能微調方針"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>HDInsight 和 Azure Data Lake Store 上的 Storm 效能微調方針

了解 hello 微調 Azure Storm 拓樸的 hello 效能時應考慮的因素。 比方說，是工作的重要的 toounderstand hello 特性 hello 完成依 hello spouts 和 hello 攻擊 （hello 工作是否 I/O 或記憶體）。 本文探討各種效能微調指導方針，包括疑難排解方面的常見問題。

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 請確定您已啟用遠端桌面 hello 叢集。
* **在 Data Lake Store 上執行 Storm 叢集**。 如需詳細資訊，請參閱 [HDInsight 上的 Storm](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview)。
* **Data Lake Store 的效能微調指導方針**。  如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)。  

## <a name="tune-hello-parallelism-of-hello-topology"></a>微調 hello 拓樸的 hello 平行處理原則

您可能會增加資料湖存放區中的 hello I/O tooand hello 並行可以 tooimprove 效能。 Storm 拓撲具有一組決定 hello 平行處理原則的組態：
* 背景工作處理序 （hello 工作者平均分散於 hello Vm） 數目。
* Spout 執行程式執行個體數目。
* Bolt 執行程式執行個體數目。
* Spout 工作數目。
* Bolt 工作數目。

例如，在叢集上具有 4 個 Vm 和 4 的背景工作處理序、 32 spout 執行程式和 32 spout 工作和 256 閃電執行程式和 512 閃電工作，請考慮 hello 下列功能：

每個監督員 (背景工作節點) 具有單一背景工作 Java 虛擬機器 (JVM) 處理序。 此 JVM 處理序管理 4 個 Spout 執行緒和 64 個 Bolt 執行緒。 在每個執行緒內，工作會循序執行。 以上述組態的 hello，每個 spout 執行緒有 1 項工作中，而且每個閃電執行緒 2 工作。

在出現，如下 hello 相關的各種元件以及它們如何影響 hello 層級的平行處理原則，您必須：
* hello 前端節點 (稱為 Nimbus Storm 中) 是使用的 toosubmit 及管理工作。 這些節點 hello 平行處理原則程度上有任何影響。
* hello 監督員節點。 在 HDInsight，這會對應 tooa 背景工作節點 Azure VM。
* hello 工作者工作是在 hello Vm 中執行的 Storm 程序。 每個背景工作 」 工作會對應 tooa JVM 執行個體。 Storm 分散 hello 數目的工作者處理序指定 toohello 背景工作節點盡量平均。
* Spout 和 Bolt 執行程式執行個體。 每一個執行程式執行個體對應 tooa hello 工作者 (JVMs) 內執行的執行緒。
* Storm 工作。 這些工作是每個執行緒所執行的邏輯工作。 這不會變更 hello 層級的平行處理原則，因此如果您或不需要每次執行程式的多個工作，您應該評估。

### <a name="get-hello-best-performance-from-data-lake-store"></a>從資料湖存放區取得 hello 達到最佳效能

當使用資料湖存放區，如果您不要 hello 遵循發生 hello 達到最佳效能：
* 將小型附加項目聯合成為較大的大小 (最好是 4 MB)。
* 盡可能提出最多的並行要求。 因為每個閃電執行緒正在進行封鎖讀取，您會想 toohave hello 範圍的每個核心的 8-12 執行緒中的某處。 這可防止也使用 hello NIC 和 hello CPU。 較大的 VM 可允許更多的並行要求。  

### <a name="example-topology"></a>範例拓撲

假設您擁有 8 個背景工作節點的叢集，叢集中具有 D13v2 Azure VM。 此 VM 有 8 個核心，因此之間 hello 8 個背景工作節點，您有 64 核心總數。

假設我們讓每個核心執行 8 個 Bolt 執行緒。 若給定 64 個核心，這表示我們總共需要 512 個 Bolt 執行程式執行個體 (亦即執行緒)。 在此情況下，假設我們以每個 VM，一個 JVM 開頭並主要是使用內 hello JVM tooachieve 並行 hello 執行緒並行存取。 這表示我們需要 8 個背景工作的工作 (每個 Azure VM 一個工作) 和 512 個 Bolt 執行程式。 指定這個設定，嘗試 toodistribute hello 工作者背景工作節點 （也稱為監督員節點） 之間平均分配給每個背景工作節點 1 Storm JVM。 現在內 hello 監督員，Storm 嘗試監督員之間的平均 toodistribute hello 執行程式，讓每個主管 (也就是 JVM) 8 執行緒每個。

## <a name="tune-additional-parameters"></a>微調其他參數
您擁有 hello 基本拓撲之後，您可以考慮是否要 tootweak 任何 hello 參數：
* **每個背景工作節點的 JVM 數目。** 如果您在記憶體中裝載了一個大型資料結構 (例如，查閱資料表)，每個 JVM 都需要個別的複本。 或者，您可以使用 hello 資料結構跨許多執行緒，如果您有較少 JVMs。 Hello 閃電 i/o hello JVMs 數目不會太多的差異，以做為 hello 加入這些 JVMs 跨執行緒數。 為了簡單起見，它是個不錯的主意 toohave 其中每個背景工作的 JVM。 根據您閃電正在進行或哪些應用程式處理中，您需要，但您可能需要 toochange 這個數字。
* **Spout 執行程式的數目。** 由於 hello 上述範例使用發射撰寫 tooData 湖存放區，但 hello spouts 數目不是直接相關 toohello 閃電效能。 不過，根據 hello 量處理或 I/O hello spout 中的情況個不錯的主意 tootune hello spouts 為了達到最佳效能。 確定您有足夠 spouts toobe 無法 tookeep hello 發射忙碌中。 hello spouts hello 輸出速率應該符合 hello 發射 hello 的輸送量。 hello 實際組態取決於 hello spout。
* **工作數目。** 每個 Bolt 都會以單一執行緒的形式來執行。 每個 Bolt 的其他工作不會提供任何額外的並行能力。 hello 唯一的時間，就會是好處的如果您的認可 hello tuple 的程序會大比例的閃電執行時間。 它是個不錯的主意 toogroup 成較大的多個 tuple 附加從 hello 閃電傳送通知之前，先。 因此，在大部分情況下，多個工作不會提供額外的好處。
* **本機或隨機群組。** 啟用此設定時，tuple 會傳送 hello 內 toobolts 相同的工作者處理序。 這可降低處理序間的通訊和網路呼叫。 這是大部分拓撲的建議作法。

這個基本案例是不錯的起點。 測試以您自己的資料 tootweak hello 前面參數 tooachieve 達到最佳效能。

## <a name="tune-hello-spout"></a>微調 hello spout

您可以修改下列設定 tootune hello spout hello。

- **Tuple 逾時︰topology.message.timeout.secs**。 此設定決定 hello 長時間的訊息會 toocomplete，並接收通知，才會視為失敗。

- **每個背景工作處理序的記憶體上限：worker.childopts**。 此設定可讓您指定其他命令列參數 toohello Java 背景工作。 hello 最常使用的設定是 XmX，決定 hello 配置的最大記憶體 tooa JVM 的堆積。

- **Spout 暫止上限：topology.max.spout.pending**。 此設定會決定 hello 隨時都可以在到飛行 （尚未認可 hello 拓撲中的所有節點），每個 spout 執行緒的 tuple 數目。

 良好的計算 toodo 是 tooestimate hello 大小每個您 tuple。 然後找出一個 Spout 執行緒有多少記憶體。 hello 配置 tooa 執行緒，此值，以分隔的記憶體總數應可提供 hello 暫止的參數的最大 spout hello 上限。

## <a name="tune-hello-bolt"></a>微調 hello 閃電
當您撰寫 tooData 湖存放區時，設定大小的同步處理原則 （hello 用戶端上的緩衝處理） too4 MB。 只有當 hello 緩衝區大小為 hello 這個值時，則執行排清或 hsync()。 hello hello 工作者 VM 上的 Data Lake Store 驅動程式會自動執行這種緩衝處理，除非您明確地執行 hsync()。

hello 預設資料湖存放區出現閃電有一個大小同步處理原則 (fileBufferSize) 的參數可以是使用的 tootune 這個參數。

在 O-大量拓撲中，它是個不錯的主意 toohave tooits 自己的檔案，tooset 每個閃電執行緒寫入檔案輪動原則 (fileRotationSize)。 Hello 檔案達到特定大小，會自動排清 hello 資料流，並寫入新的檔案。 hello 建議的輪替檔案大小為 1GB。

### <a name="handle-tuple-data"></a>處理 Tuple 資料

在出現，spout 持有 tooa tuple 直到 hello 閃電明確認可。 如果已讀取的 hello 閃電 tuple，但尚未認可，hello spout 可能不會有保存到資料湖存放區的後端。 Tuple 會在認可之後，可以保證持續性 hello 閃電 hello spout，並可接著刪除正在讀取從任何來源中的 hello 來源資料。  

資料湖存放區的最佳效能，有 hello 閃電 4 MB 的 tuple 資料的緩衝區。 接著，撰寫的 toohello 回資料湖存放區端一個 4 MB 寫入。 Hello 資料已成功寫入的 toohello 存放區之後 （所呼叫的 hflush()) hello 閃電可以了解 hello 資料回復 toohello spout。 這是什麼 hello 範例閃電提供這裡沒有。 它也是可接受 toohold 更大量的 tuple 之前進行 hello hflush() 呼叫與 hello 認可的 tuple。 不過，這會增加 hello 傳送 hello spout 需要 toohold，，因此會增加 hello 的每個 JVM 所需的記憶體數量的 tuple 數目。

> [!NOTE]
基於其他非效能，應用程式可能有更頻繁地 （在資料大小小於 4 MB） 的需求 tooacknowledge tuple。 不過，可能會影響 hello I/O 輸送量 toohello 存放裝置後端。 請仔細權衡 hello 閃電 I/O 效能對這些權衡取捨。

如果 tuple 的 hello 內送速率不高，因此 hello 4 MB 緩衝區會很長的時間 toofill，請考慮緩和這由：
* 減少攻擊的 hello 數量，因此會有較少的緩衝區 toofill。
* 具有以時間為基礎或以計數為基礎的原則，其中 hflush() 觸發每隔 x 排清或每個 y 毫秒，並累積到目前為止的 hello tuple 都已認可後。

請注意，在此情況下 hello 輸送量較低，事件的速度變慢，最大輸送量並非 hello 最大目標還是。 這些防護功能，幫助您減少 hello 透過 toohello 存放區 tuple tooflow 所花費的總時間。 如果您無論如何都想要即時管線 (即使事件速率會偏低)，這一點可能就很重要。 另外請注意，如果內送的 tuple 速率過低時，應調整 hello topology.message.timeout_secs 參數，因此 hello tuple 不會逾時取得經過緩衝處理或處理。

## <a name="monitor-your-topology-in-storm"></a>監視 Storm 中的拓撲  
執行您的拓撲時，您可以在 hello Storm 使用者介面來進行監視。 以下是在 hello 主要參數 toolook:

* **總處理序執行延遲。** 這是一個 tuple 所需 toobe hello spout 所發出、 處理 hello 閃電和認可的 hello 平均時間。

* **總 Bolt 處理序延遲。** 這是 hello 直到其接收到通知，在 hello 閃電 hello tuple 所花費的平均時間。

* **總 Bolt 執行延遲。** 這是 hello 平均 hello 閃電 hello 中所花費的時間執行的方法。

* **失敗次數。** 這是指 toohello 失敗 toobe 完全處理這些逾時之前的 tuple 數目。

* **容量。** 這是系統忙碌程度的量值。 如果這個數字為 1，Bolt 會以它最快的速度工作。 如果是小於 1，增加 hello 平行處理原則。 如果是大於 1，減少 hello 平行處理原則。

## <a name="troubleshoot-common-problems"></a>針對常見問題進行疑難排解
以下是一些常見的疑難排解案例。
* **許多 Tuple 逾時。**查看 hello 瓶頸何在 hello 拓撲 toodetermine 的每個節點。 hello 最常見的原因是 hello 發射並不能 tookeep 向上與 hello spouts。 這會導致 tootuples 繼續 hello 等候 toobe 處理時的內部緩衝區。 請考慮增加 hello 逾時值或減少 hello max spout 暫止。

* **總處理序執行延遲很高，但 Bolt 處理序延遲卻很低。** 在此情況下，很可能的 hello tuple 都尚未被認可速度夠快。 請確認認可者的數量足夠。 另一個可能性是，它們會 hello 在佇列中等待太久之前 hello 釘開始處理它們。 減少 hello max spout 暫止。

* **Bolt 執行延遲很高。** 這表示您閃電 hello execute （） 方法時間太長。 最佳化 hello 程式碼，或查看寫入大小，排清的行為。

### <a name="data-lake-store-throttling"></a>Data Lake Store 節流
如果您遇到 hello 限制的資料湖存放區所提供的頻寬，您可能會看到工作失敗。 請檢查工作記錄中的節流錯誤。 您可以藉由增加容器大小減少 hello 平行處理原則。    

如果您節流，toocheck 啟用 hello 偵錯 hello 用戶端記錄：

1. 在**Ambari** > **Storm** > **Config** > **進階 storm-背景工作層 log4j**，變更**&lt;根層級 ="info"&gt;** 太**&lt;根層級 ="debug"&gt;**。 重新啟動所有 hello 節點/服務 hello 組態 tootake 效果。
2. 監視 hello Storm 拓撲登入的背景工作節點 (在 /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;連接埠&gt;/worker.log) 節流例外狀況的資料湖存放區。

## <a name="next-steps"></a>後續步驟
Storm 的其他效能微調請參考[此部落格](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/)。

其他範例 toorun，請參閱[GitHub 上的此一](https://github.com/hdinsight/storm-performance-automation)。
