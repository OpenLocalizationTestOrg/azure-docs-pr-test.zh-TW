---
title: "R 伺服器 HDInsight 的 Azure 上的 aaaCompute 內容選項 |Microsoft 文件"
description: "深入了解 hello 不同的計算內容選項可用 toousers 與 HDInsight 上的 R 伺服器"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>適用於 HDInsight 上 R 伺服器的計算內容選項

Azure HDInsight 上的 Microsoft R Server 控制設定 hello 計算內容執行呼叫的方式。 本文概述 hello 選項可用 toospecify 是否及如何執行平行處理跨 hello 邊緣節點或 HDInsight 叢集的核心。

hello 邊緣節點的叢集提供方便的位置 tooconnect toohello 叢集和 toorun R 指令碼。 邊緣節點之後，您有 hello 選項執行 hello 平行處理的分散式函式的 ScaleR 跨 hello 核心的 hello 邊緣節點伺服器。 您也可以執行這些 hello hello 叢集節點之間使用 ScaleR 的 Hadoop 對應減少或 Spark 計算內容。

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Azure HDInsight 上的 Microsoft R 伺服器
[Azure HDInsight 上的 Microsoft R Server](hdinsight-hadoop-r-server-overview.md) hello 最新功能，提供 R 為基礎的分析。 它可以使用儲存在 HDFS 容器中的資料您[Azure Blob](../storage/common/storage-introduction.md "Azure Blob 儲存體")儲存體帳戶、 資料湖存放區或 hello 本機 Linux 檔案系統。 因為 R Server 根據開放原始碼 R，hello R 為基礎的應用程式建置可以套用的任何 hello 8000 + 開放原始碼 R 封裝。 他們也可以使用中的 hello 常式[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)，隨附於 R Server 的 Microsoft 的巨量資料分析封裝。  

## <a name="compute-contexts-for-an-edge-node"></a>邊緣節點的計算內容
一般情況下，在 hello 邊緣節點 R 伺服器中執行 R 指令碼 hello R 解譯器中執行，該節點上。 hello 例外狀況是呼叫 ScaleR 函式的步驟。 hello ScaleR 呼叫都取決於您如何設定 hello ScaleR 計算內容的運算環境中執行。  當您從邊緣節點執行 R 指令碼時，hello 的 hello 可能的值會計算內容是：

- 本機循序 (*‘local’*)
- 本機平行 (*‘localpar’*)
- Map Reduce
- Spark

hello *'local'*和*'localpar'*選項的差異只在於如何**rxExec**執行呼叫。 這些兩個其他 rx 函式呼叫中執行以平行方式分散到所有可用的核心除非另行指定，藉由使用 hello ScaleR **numCoresToUse**選項，例如`rxOptions(numCoresToUse=6)`。 平行執行選項提供最佳效能。

hello 下表摘要說明各種計算如何執行呼叫的內容選項 tooset hello:

| 計算內容  | 如何 tooset                      | 執行內容                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| 本機循序 | rxSetComputeContext(‘local’)    | 平行化的執行跨 hello 核心 hello 邊緣節點伺服器，會循序執行的 rxExec 呼叫除外 |
| 本機平行   | rxSetComputeContext(‘localpar’) | 平行化的執行跨 hello 核心 hello 邊緣節點伺服器 |
| Spark            | RxSpark()                       | 平行處理分散式經由執行 Spark hello 節點之間的 hello HDI 叢集 |
| Map Reduce       | RxHadoopMR()                    | 平行處理分散式的執行透過對應減少 hello 節點之間的 hello HDI 叢集 |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>用於決定計算內容的指導方針

其中一個 hello 的三個選項選擇提供平行化的執行取決於 hello 本質的分析工作、 hello 大小和 hello 資料的位置。 沒有任何簡單的公式，告訴您的計算內容 toouse。 有，不過，有些可協助您進行 hello 正確的選擇，或至少，幫助您縮小您的選擇，然後再執行基準測試的指導原則。 這些指導原則包括︰

- hello 本機 Linux 檔案系統的速度比 HDFS。
- 如果 hello 資料在本機，而且如果它是在 XDF 重複的分析時，速度加快。
- 它是比 toostream 少量的文字資料來源的資料。 如果 hello 資料量大，請將它轉換 tooXDF 分析之前。
- hello 的複製或資料流分析的 hello 資料 toohello 邊緣節點的額外負荷變得難以管理的非常大量的資料。
- Spark 在 Hadoop 中的分析速度較 Map Reduce 快。

指定這些原則，hello 下列各節提供一些一般法則選取的計算內容。

### <a name="local"></a>本機
* 如果資料 tooanalyze hello 量小，而不需要重複的分析，然後進行串流處理它直接在 hello 分析常式使用*'local'*或*'localpar'*。
* 如果 hello 資料 tooanalyze 數量是小型或中型大小，且需要重複的分析，然後將它複製 toohello 本機檔案系統、 匯入它 tooXDF，以及分析透過*'local'*或*'localpar'*。

### <a name="hadoop-spark"></a>Hadoop Spark
* 如果 hello 資料 tooanalyze 數量很大，將它匯入 tooa Spark 資料框架使用**RxHiveData**或**RxParquetData**，或在 HDFS tooXDF （除非儲存體問題），並進行分析使用 hello Spark計算內容。

### <a name="hadoop-map-reduce"></a>Hadoop Map Reduce
* 如果您遇到 hello Spark 計算內容是無法克服問題，因為它是速度較慢，請使用 hello 對應減少的計算內容。  

## <a name="inline-help-on-rxsetcomputecontext"></a>rxSetComputeContext 的內嵌說明
如需詳細資訊和範例 ScaleR 的計算內容，請參閱 hello 內嵌在 R 中的說明 hello rxSetComputeContext 方法，例如：

    > ?rxSetComputeContext

您也可以參考 toohello"[ScaleR 分散式運算指南](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)"，而且可從 hello [R 伺服器 MSDN](https://msdn.microsoft.com/library/mt674634.aspx "MSDN 上的 R 伺服器")程式庫。

## <a name="next-steps"></a>後續步驟
在本文中，您學可用 toospecify hello 選項是否及如何執行進行平行處理跨 hello 邊緣節點或 HDInsight 叢集的核心。 toolearn 深入了解如何 toouse R 伺服器與 HDInsight 叢集，請參閱下列主題中的 hello:

* [適用於 Hadoop 的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)
* [開始使用適用於 Hadoop 的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)
* [新增 RStudio 伺服器 tooHDInsight （如果不在叢集建立期間新增）](hdinsight-hadoop-r-server-install-r-studio.md)
* [適用於 HDInsight R 伺服器的 Azure 儲存體選項](hdinsight-hadoop-r-server-storage.md)

