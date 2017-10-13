---
title: "封存版本資訊 - Azure HDInsight 上的 Hadoop 元件 | Microsoft Docs"
description: "Azure HDInsight 之舊版 Hadoop 元件的封存版本資訊。"
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 04278aac85171601b5801b0890d14a9076060444
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Azure HDInsight 上 Hadoop 元件的版本資訊 (封存)

此文章提供有關**較舊** Azure HDInsight 版本更新的資訊。 如需有關最近版本的詳細資訊，請參閱 [HDInsight 版本資訊](hdinsight-release-notes.md)。

> [!IMPORTANT]
> Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。 如需詳細資訊，請參閱 [HDInsight 版本控制文件](hdinsight-component-versioning.md)。



## <a name="notes-for-08302016-release-of-hdinsight"></a>HDInsight 08/30/2016 版本的相關資訊
使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>2016/8/17 - HDInsight 上的 R 伺服器版本資訊
* R 伺服器 8.0.5 - 主要為修正程式的版本。 詳細資訊請參閱 [R 伺服器版本資訊](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) 。
* 邊緣節點上的 AzureML 封裝 - [此 R 封裝](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) 使 R 模型可以做為 Azure ML Web 服務來發佈和取用。  詳細資訊請參閱我們的 [HDInsight 上的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)文章中的[實作模型](hdinsight-hadoop-r-server-overview.md#operationalize-a-model)一節。
* [前 100 名熱門 R 封裝](https://github.com/metacran/cranlogs) 的 Linux 相依性 - 現在，這些 Linux 封裝相依性都是預先安裝好。
* 新增 R 封裝至資料節點時使用 CRAN 儲存機制的選項。 如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。
* 改善叢集建立時 R 伺服器佈建的可靠性。

## <a name="notes-for-08012016-release-of-hdinsight"></a>HDInsight 2016/08/01 版本的相關資訊
使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDInsight 3.4 叢集的變更 |為了提升效能，下列 Hive 組態的預設值已變更 <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |服務 |全部 |N/A |
| 此版本包含下列修正程式 |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |服務 |全部 |N/A |

## <a name="notes-for-07142016-release-of-hdinsight"></a>HDInsight 2016/07/14 版本的相關資訊
使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>HDInsight 2016/07/07 版本的相關資訊
使用此版本部署的 Linux 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

使用此版本部署的 Windows 型 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| [HDInsight Tools for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式現在與適用於 IntelliJ 的 Azure 工具組整合。 它支援 Azure SDK v2.9.1、最新的 Java SDK，以及包含獨立IntelliJ 之 HDInsight 外掛程式的所有功能。 |工具 |Spark |N/A |
| [HDInsight Tools for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |適用於 Eclipse 的 Azure 工具組現在支援 HDInsight Spark 叢集。 它可啟用下列功能： <ul><li>透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</li><li>在本機測試 Spark 應用程式。</li><li>將作業提交至 HDInsight Spark 叢集，並擷取結果。</li><li>登入 Azure，並存取與 Azure 訂用帳戶相關聯的所有 Spark 叢集。</li><li>瀏覽 HDInsight Spark 叢集的所有相關聯儲存體資源。</li></ul> |工具 |Spark |N/A |

從這個版本開始，我們針對以 Linux 為基礎的 HDInsight 叢集變更客體 OS 修補原則。 新原則的目標是大幅減少因為修補而產生的重新開機次數。 新的原則會在每個星期一或星期四 UTC 上午 12 時開始，以交錯方式在任何指定叢集的節點之間，修補 Linux 叢集上的虛擬機器 (VM)。 不過，任何指定的 VM 每隔 30 天只會因為客體 OS 修補而最多重新開機一次。 此外，新建立的叢集在叢集建立之後，也不會在 30 天內第一次重新開機。

> [!NOTE]
> 這些變更只適用於等於或大於這個發行版本的新建立叢集。
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>HDInsight 2016/06/06 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

| HDP | HDI 版本 | Spark 版本 | Ambari 組建編號 | HDP 組建編號 |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDInsight 上的 Spark 已正式推出 |此版本會針對 HDInsight 上 Apache Spark 的開放原始碼提供改良的可用性、延展性和產能。 <ul><li>業界領先的 99.9% 可用性 SLA，因此能應付企業要求嚴苛的工作負載。</li><li>使用 Azure Data Lake Store 的可調整儲存體層。</li><li>針對資料探索和開發的每個階段皆有相應的生產力工具。 含自訂 Spark 核心的 Jupyter 筆記本會啟用互動式資料探索，並與 BI 儀表板 (例如 Power BI、Tableau 及 Qlik) 整合，非常適合快速資料共用和連續報告；IntelliJ 外掛程式是適用於長期程式碼構件開發和偵錯的可靠方式。</li></ul> |服務 |Spark |N/A |
| HDInsight Tools for IntelliJ |這是適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式。 它可啟用下列功能：<ul><li>透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</li><li>在本機測試 Spark 應用程式。</li><li>將作業提交至 HDInsight Spark 叢集，並擷取結果。</li><li>登入 Azure，並存取與 Azure 訂用帳戶相關聯的所有 Spark 叢集。</li><li>瀏覽 HDInsight Spark 叢集的所有相關聯儲存體資源。</li><li>瀏覽 HDInsight Spark 叢集的所有作業歷程記錄和作業資訊。</li><li>從桌上型電腦遠端偵錯 Spark 作業。</li></ul> |工具 |Spark |N/A |

## <a name="notes-for-05132016-release-of-hdinsight"></a>HDInsight 2016/05/13 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| Spark 版本更新和其他錯誤修正 |此版本將 HDInsight 叢集中的 Spark 版本更新至 1.6.1，並修正其他錯誤 |服務 |Spark |N/A |

## <a name="notes-for-04112016-release-of-hdinsight"></a>HDInsight 2016/04/11 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -未變更)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDI 3.4 的自訂中繼存放區升級問題 |如果您使用先前在另一個較低版本的 HDInsight 叢集上使用的自訂中繼存放區，則叢集會建立失敗。 這是因為升級指令碼時發生的錯誤現在已修正 |叢集建立 |全部 |N/A |
| Livy Crash 復原 |為所有已透過 Livy 提交的作業提供工作狀態復原 |可靠性 |Spark on Linux |N/A |
| Jupyter 內容 HA |提供儲存 Jupyter 筆記本內容，以及將此內容從與叢集相關的儲存體帳戶載入的功能。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。 |筆記本 |Spark on Linux |N/A |
| 移除 Jupyter 筆記本中的 hiveContext |使用 `%%sql` magic，而非 `%%hive` magic。 SqlContext 等於 hiveContext。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md) |筆記本 |Linux 上的 Spark 叢集 |N/A |
| 取代了舊版的 Spark |舊版的 Spark 1.3.1 會於 5 月 31 日從服務中移除 |服務 |Windows 上的 Spark 叢集 |N/A |

## <a name="notes-for-03292016-release-of-hdinsight"></a>HDInsight 2016/03/29 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 新增 HDInsight 3.4 版並更新所有 HDInsight 叢集的 HDP 版本 |在此版本中，我們新增了 HDInsight v3.4 (以 HDP 2.4 為基礎) 並且更新了其他 HDP 版本。 HDP 2.4 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。 |服務 |所有 Linux 叢集 |N/A |
| HDInsight Premium |HDInsight 現在有兩種類別：Standard 和 Premium。 HDInsight Premium 目前為預覽版，僅適用於 Linux 上的 Hadoop 和 Spark 叢集。 如需詳細資訊，請參閱[這裡](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。 |服務 |Linux 上的 Hadoop 和 Spark |N/A |
| Microsoft R 伺服器 |HDInsight Premium 提供 Microsoft R 伺服器，它可以隨附於 Linux 上的 Hadoop 與 Spark 叢集。 如需詳細資訊，請參閱 [HDInsight 中的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)。 |服務 |Linux 上的 Hadoop 和 Spark |N/A |
| Spark 1.6.0 |HDInsight 3.4 叢集現在包含 Spark 1.6.0 |服務 |Linux 上的 Spark 叢集 |N/A |
| Jupyter Notebook 增強功能 |可用於 Spark 叢集的 Jupyter Nnotebook 現在提供額外的 Spark 核心。 其中也包括增強功能，例如使用 %%magic、自動視覺化，以及與 Python 視覺化程式庫 (例如 matplotlib) 整合。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。 |服務 |Linux 上的 Spark 叢集 |N/A |

## <a name="notes-for-03222016-release-of-hdinsight"></a>HDInsight 2016/03/22 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-03102016-release-of-hdinsight"></a>HDInsight 2016/03/10 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - 未變更)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-01272016-release-of-hdinsight"></a>HDInsight 2016/01/27 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - 未變更)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-12022015-release-of-hdinsight"></a>HDInsight 2015/12/02 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - 未變更)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - 未變更)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 新增 HDInsight 3.3 版並更新所有 HDInsight 叢集的 HDP 版本 |在此版本中，我們新增了 HDInsight v3.3 (以 HDP 2.3 為基礎) 並且更新了其他 HDP 版本。 HDP 2.3 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。 |服務 |全部 |N/A |

## <a name="notes-for-11302015-release-of-hdinsight"></a>HDInsight 2015/11/30 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 所有 HDInsight 叢集的已更新 HDInsight 版本和 HDInsight 3.2 叢集的 HDP 版本 (Windows 和 Linux) |在此版本中，HDInsight 和 HDP 版本均已更新 |服務 |全部 |N/A |

## <a name="notes-for-10272015-release-of-hdinsight"></a>HDInsight 2015/10/27 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 (Windows 和 Linux) |在此版本中，HDInsight 和 HDP 版本均已更新 |服務 |全部 |N/A |
| 修正包含大寫字母叢集之 Windows Spark 叢集的 Jupyter |以大寫字母指定 DNS 名稱的叢集，會因為原始要求檢查的緣故而使 Jupyter 筆記本發生問題。 此修正是要將 Jupyter 之設定的 DNS 名稱變更為小寫。 |服務 |HDInsight Spark (Windows) |N/A |

## <a name="notes-for-10202015-release-of-hdinsight"></a>HDInsight 2015/10/20 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 變更為 HDP 2.2 的預設版本 HDP |HDInsight Windows 叢集的預設版本變更為 HDP 2.2。 HDInsight 版本 3.2 (HDP 2.2) 自 2015 年 2 月已在公開上市。 這項變更只會在使用 Azure 入口網站、PowerShell Cmdlet 或 SDK 叢集佈建的同時未進行明確選擇時，翻轉預設叢集版本。 |服務 |全部 |N/A |
| 變更 VM 名稱格式以在單一虛擬網路中的 Linux 叢集上部署多個 HDInsight。 |在這個版本中已加入在單一虛擬網路中部署多個 HDInsight Linux 叢集的支援。 隨著更新，叢集的虛擬機器名稱的格式已從 headnode\*、workernode\* 和 zookeepernode\* 分別變更為 hn\*、wn\* 和 zk\*。 不建議採取虛擬機器名稱格式的直接相依性，因為這樣會受限於變更。 請使用本機機器或 Ambari API 上的 "hostname -f" 以判斷主機清單和元件到主機的對應。 您可以在 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) 和 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md) 找到更多資訊。 |服務 |Linux 上的 HDInsight 叢集 |N/A |
| 組態變更 |對於 HDInsight 3.1 叢集，現在會啟用下列組態︰ <ul><li>tez.yarn.ats.enabled 和 yarn.log.server.url。 這可讓應用程式時間軸伺服器和記錄伺服器能夠提供記錄檔。</li></ul>對於 HDInsight 3.2 叢集，已經修改下列組態： <ul><li>mapreduce.fileoutputcommitter.algorithm.version 已設為 2。 這樣就可以使用 FileOutputCommitter 的 V2 版本。</li></ul> |服務 |全部 |N/A |

## <a name="notes-for-09092015-release-of-hdinsight"></a>HDInsight 2015/09/09 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，HDInsight 版本已更新 |服務 |全部 |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight 2015/07/31 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 修正 Spark 叢集節點的重新製作映像工作流程 |修正造成 Spark 叢集節點重新製作映像後不復原的錯誤 |服務 |Spark |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight 2015/07/31 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，HDInsight 版本已更新 |服務 |全部 |N/A |

## <a name="notes-for-07072015-release-of-hdinsight"></a>HDInsight 2015/07/07 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* SDK            1.5.8

此版本包含下列更新：

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDInsight 3.2 叢集的更新後 HDP 版本 |在此版本中，HDInsight 3.2 會部署 HDP 2.2.6.1-0012 |服務 |全部 |N/A |

## <a name="notes-for-06262015-release-of-hdinsight"></a>HDInsight 2015/06/26 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>HDInsight 3.2 叢集的更新後 HDP 版本</td>
<td>在此版本中，HDInsight 3.2 會部署 HDP 2.2.6.1</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>HDInsight 2015/06/18 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>其他開啟的 HTTPS 連接埠</td>
<td>雲端服務現在會開啟叢集上的 5 個連接埠 (8001 至 8005)，例如 https://<clustername>.azurehdinsight.net:8001/。 對這些 URL 的要求會使用相同的基本驗證密碼機制驗證做為連接埠 443。 這些連接埠會繫結至作用中前端節點上的相同連接埠。 使用指令碼動作，可讓客戶服務在前端節點的這些連接埠上接聽並路由傳送到叢集外部。</td>
<td>服務雲端</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDInsight 3.2 的間歇性 MapReduce Shuffle 問題</td>
<td>修正大型叢集上 MapReduce Shuffle 的間歇性罕見情況，會導致非經常性工作失敗。 如需詳細資訊，請參閱 <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a>。</td>
<td>Hadoop 核心</td>
<td>全部</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>移至最新的 Azure Java SDK 2.2 for HDInsight 3.2</td>
<td>已移至 WASB 驅動程式所用的最新版 Azure SDK for Java。 最新的 SDK 有一些修正程式，而在 https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt 可取得相同的版本資訊。</td>
<td>Hadoop 核心</td>
<td>全部</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>移至 HDP 2.1.15 for HDInsight 3.1 叢集</td>
<td>這些版本的 Hortonworks 版本資訊位於<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">這裡</a>。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>HDInsight 2015/06/04 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - 未變更)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>修正 Storm 叢集的 502 不正確閘道器錯誤</td>
<td>此版本修正會影響工作提交 API 並導致網站在重新開機後關閉的 Bug。</td>
<td>服務</td>
<td>Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>HDInsight 2015/06/01 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - 未變更)
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - 未變更)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>各種 Bug 修正</td>
<td>此版本修正與叢集佈建相關的 Bug。</td>
<td>服務</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>HDInsight 2015/05/27 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* 其他叢集版本和 SDK 不會部署為此版本的一部分。

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>HDP 2.2 更新</td>
<td>這一版的 HDInsight 3.2 包含 HDP 2.2.6，並在 HDInsight 中加入數個重要的 Bug 修正程式。 在 <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 版本資訊</a>可取得完整的版本資訊。</td>
<td>HDP</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
<tr>
<td>變更為預設 Yarn 容器記憶體設定</td>
<td>在這項更新中，由節點管理員啟動之 YARN 容器 (yarn.nodemanager.resource.memory-mb and yarn.scheduler.maximum-allocation-mb) 的預設可用記憶體會增加至 5632MB。 先前這會縮減至 4608MB，但根據不同的工作會執行，新值必須為大部分的工作提供更佳的可靠性和效能，因此此預設值更好。 如往常一樣，如果您對此記憶體組態有重要相依性，請在建立叢集時加以明確設定。</td>
<td>HDP</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
<tr>
<td>HBase 和 Storm 叢集的預設組態同位檢查</td>
<td>此更新會將 Hbase 和 Storm 叢集還原為使用與 Hadoop 叢集相同的 YARN 組態值。 這是為了進行所有叢集類型的同位檢查。</td>
<td>HDP</td>
<td>HBase、Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>HDInsight 2015/05/20 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>SCP.NET EventHub 支援</td>
<td>HDInsight Storm 的更新叢集封裝加入 SCP.NET 的新功能。 您現在將可存取拓撲產生器中的新 API，讓您更輕鬆地使用 EventHubSpout 或 Java Spouts。 您必須更新 SCP.NET 用戶端 SDK，才能在合約更新後使用新叢集。 如需新 API、使用方式及版本資訊 (包括 Bug 修正程式) 的詳細資訊，請參閱 SCP.NET NuGet 套件中包含的 Readme 檔案。</td>
<td>VS 工具</td>
<td>Storm HDInsight 3.2 叢集</td>
<td>N/A</td>
</tr>
<tr>
<td>JDBC 驅動程式更新</td>
<td>將驅動程式更新為 sqljdbc_4.1.5605.100 中支援的 SQL Server 版本。</td>
<td>Metastore</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>HDInsight 2015/04/27 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* SDK            1.5.8

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>修正 DLL 相依性</td>
<td>移除對單位測試架構的 HDInsight 相依性。</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>競爭情形的 Bug 修正</td>
<td>叢集建立要求現正等待 PUT 要求獲得接受，然後才進行狀態的輪詢</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>HDInsight 2015/04/14 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* SDK            1.5.6

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>Tez Bug 修正</td>
<td>Apache TEZ 2214 和 TEZ 1923 的修正包含在此版本的 HDI 3.2。 Tez 上需要混和大量資料的特定 Hive 查詢需要這些修正。
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>HDInsight 2015/04/06 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* SDK            1.5.6

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>HDInsight .NET SDK 1.5.6</td>
<td>此更新可移除 Linux 上之 HDInsight 的部分內部類別。</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Avro Library 1.5.6</td>
<td>已為方法 <b>GetAllKnownTypes</b> 新增 <b>KnownTypeAttribute</b>。 當 GetAllKnownTypes 方法的類型為 Null 時已修正的 NullReferenceException。</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>錯誤修正</td>
<td>服務的各種 Bug 修正</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>HDInsight 2015/04/01 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* SDK            1.5.5

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>透過 .NET SDK 啟用/停用 Windows 叢集上的遠端桌面認證的能力</td>
<td>針對在 Windows 叢集上啟用或停用 RDP 認證的程式設計支援。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>當叢集正在佈建時啟用遠端桌面認證的能力</td>
<td>針對正在建立叢集時啟用遠端桌面認證的程式設計支援。 如此便不再需要先佈建叢集再啟用遠端桌面的兩步驟程序。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>已將 Python 升級到 2.7.8</td>
<td>已將 HDInsight 叢集上的 Python 升級到 Python 2.7.8，它包含一些 HDInsight 2.1、3.0、3.1 和 3.2 版的重要安全性修正</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>YARN 組態變更</td>
<td>已針對 HDInsight 3.1 和 3.2 版的所有叢集類型將 YARN 組態 yarn.resourcemanager.max-completed-applications 變更為 1000。 此值只會控制 YARN UI 中的已完成應用程式清單。 若要取得在 UI 上顯示應用程式清單之前提交之應用程式的相關資訊，您可以直接移至 [記錄伺服器]。</td>
<td>YARN</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>在 HBase 叢集中調整節點的大小</td>
<td>HBase 叢集現在允許針對 HDInsight 3.1 和 3.2 版 (向上及向下) 調整節點的大小</td>
<td>服務</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>JDBC 升級</td>
<td>HDInsight 3.2 版的 SQL JDBC 驅動程式已升級到 sqljdbc_4.0.2206.100 版。 此版本包含重要的安全性增強功能。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>JVM 組態更新</td>
<td>已針對 HDInsight 3.1 和 3.2 版將 JVM 組態 networkaddress.cache.ttl 從預設值 -1 更新到 300 秒。 此組態值控制來自名稱服務的成功名稱查閱快取原則。 這修正了與增大和壓縮 HBase 叢集有關的 Bug。</td>
<td>服務</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>升級到 Azure Storage SDK for Java 2.0</td>
<td>已升級 HDInsight 3.2 版以使用最新版的 Azure Storage SDK for Java。 這包含針對目前 0.6.0 版的幾項重要 Bug 修正。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>已升級到 Apache WASB 原始程式碼</td>
<td>HDInsight 3.2 版現在使用來自 Apache Hadoop 的 WASB 檔案系統驅動程式的最新程式碼。 有了這項變更，WASB 驅動程式現在封裝為獨立型 jar。 這純粹是封裝變更，不包含對 WASB 驅動程式行為的任何變更。 此 JAR 檔的名稱是 hadoop-azure-2.6.0.jar。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDInsight 3.2 中的 Jar 檔案名稱更新</td>
<td>HDInsight 3.2 版的這項更新包含數個 Bug 修正，且封裝為包含在 HDP 的一些內部 jar 也已升級。 這些 JAR 檔是 HDP 封裝內部使用，不供客戶應用程式直接使用。 應用程式應該封裝自己的 JAR 版本，如此升級 HDP 內部 JAR 時才不會中斷客戶應用程式。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>HDInsight 2015/03/03 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - 未變更)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - 未變更)
* SDK            1.5.0                (未變更)

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>可靠性的改進</td>
<td>我們做了修正，讓服務能更妥善地隨著與叢集建立時相比增加的負載而縮放。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>HDInsight 2015/02/18 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - 未變更)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* SDK            1.5.0

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>HDInsight 3.2 叢集</td>
<td>HDInsight 3.2 叢集提供 Hadoop 2.6/HDP2.2。 它包含對所有開放原始碼元件的重大更新。 如需詳細資訊，請參閱 HDInsight 的新功能和 <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 版本資訊</a>。</td>
<td>開放原始碼軟體</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>Linux 上的 HDInsight (預覽)</td>
<td>叢集可以部署在 Ubuntu Linux 上執行。 如需詳細資訊，請參閱＜開始在 Linux 上使用 HDInsight＞。</td>
<td>服務</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Storm 公開上市</td>
<td>Apache Storm 叢集已公開上市。 如需詳細資訊，請參閱＜開始在 HDInsight 中使用 Storm＞。</td>
<td>服務</td>
<td>Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>虛擬機器大小</td>
<td>Azure HDInsight 可用於更多虛擬機器類型和大小。 HDInsight 可以利用針對一般用途建置的 A2 到 A7 大小；D 系列節點的特色為固態硬碟 (SSD) 和處理器速度更快 60%；而 A8 和 A9 大小具有 InfiniBand 支援可快速進行網路連線。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>叢集縮放</td>
<td>您可以針對執行中的 HDInsight 叢集變更資料節點的數目，而不必刪除或重建它。 目前只有 Hadoop 查詢和 Apache Storm 叢集類型有此功能，但很快就會提供對 Apache HBase 叢集類型的支援。 如需詳細資訊，請參閱＜管理 HDInsight 叢集＞。</td>
<td>服務</td>
<td>Hadoop、Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Visual Studio 工具</td>
<td>除了 Apache Storm 的完整工具，Visual Studio 中的 Apache Hive 工具也已更新到包含陳述式完成、本機驗證和改進的偵錯支援。 如需詳細資訊，請參閱＜開始使用 HDInsight Tools for Visual Studio＞。</td>
<td>工具</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<td>適用於 Azure Cosmos DB 的 Hadoop Connector</td>
<td>使用適用於 Azure Cosmos DB 的 Hadoop Connector，您可以針對儲存在 Azure Cosmos DB 集合之間或資料庫帳戶之間的無結構描述 JSON 文件，執行複雜的彙總、分析與操作。 如需詳細資訊和教學課程，請參閱＜使用 Azure Cosmos DB 和 HDInsight 執行 Hadoop 作業＞。</td>
<td>服務</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>錯誤修正</td>
<td>我們為 HDInsight 服務提供了各種次要 Bug 修正。 不應有面向客戶的行為變更。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>HDInsight 2015/02/06 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* SDK            N/A

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>錯誤修正</td>
<td>我們為 HDInsight 服務提供了各種次要 Bug 修正。 不應有面向客戶的行為變更。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDP 2.1 維護更新</td>
<td>已更新 HDInsight 3.1 以部署 HDP 2.1.10.0。 如需詳細資訊，請參閱<a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">版本資訊 HDP-2.1.10</a>。 </td>
<td>開放原始碼軟體</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDP 二進位更新</td>
<td>HBase 中有一些 JAR 檔的檔案名稱已更新。 這些 JAR 檔由 HBase 做為內部使用，因此客戶不應對這些 JAR 檔的名稱有相依性。 其中包含：
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>開放原始碼軟體</td>
<td>HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>HDInsight 2015/1/29 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  未變更)
* SDK            N/A

此版本包含下列更新：

<table border="1">

<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>錯誤修正</td>
<td>我們做了一些重要 Bug 修正，可以改善 HDInsight 叢集在 Azure 升級期間的可靠性。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>HDInsight 2015/1/5 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - 未變更)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - 未變更)

此版本包含下列更新：

<table border="1">

<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>Twitter 趨勢分析及 Mahout 電影推薦的範例</td>
<td><p>在此版本中，HDInsight 查詢主控台有兩個其他範例：</p>

<p><b>Twitter 趨勢分析</b><br>
像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。 在此教學課程中，了解如何使用 Hive 取得傳送最多包含特定字之推文的 Twitter 使用者清單。 </p>

<p><b>Mahout 電影推薦</b><br>
Apache Mahout 是 Apache Hadoop 的機器學習庫。 Mahout 包含用來處理資料 (例如篩選、分類和叢集化) 的演算法。 在本教學課程中，請使用推薦引擎，根據朋友看過的電影來產生電影推薦。</p></td>
<td>查詢主控台</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>將 Hive 組態 hive.auto.convert.join.noconditionaltask.size 變更為預設值</td>
<td><p>這個大小組態適用於自動轉換的對應聯結。 值代表可以轉換成雜湊對應且可放入記憶體的資料表大小總和。 在前版中，這個值從預設值 10 MB 增加到 128 MB。 但是新的 128 MB 值因為缺乏記憶體而導致工作失敗。 此版本將預設值還原成 10MB。 客戶仍然可以依據其查詢和資料表大小選擇在叢集建立期間覆寫此值。 如需此設定和如何覆寫該設定的詳細資訊，請參閱 Hortonworks 文件中的<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">最佳化自動聯結轉換</a>。 </p></td>
<td>Hive</td>
<td>Hadoop、Hbase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>HDInsight 2014/12/23 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼為：

* HDInsight     2.1.10.420.1246783    (HDP 版本未變更)
* HDInsight     3.0.6.420.1246783    (HDP 版本未變更)
* HDInsight     3.1.1.420.1246783    (HDP 版本未變更)

此版本包含下列更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>由於負載過度而發生間歇性叢集建立失敗</td>
<td><p>改善叢集建立期間下載 HDP 封裝的演算法，以便能更強大地處理由於負載過度而發生的失敗。</p></td>
<td>服務</td>
<td>Hadoop、HBase、Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>HDInsight 2014/12/18 版本的相關資訊
此版本包含下列元件更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">叢集自訂公開上市</a></td>
<td><p>自訂可讓您使用 Apache Hadoop 生態系統可用的專案來自訂 Azure HDInsight 叢集。 有了這項新功能，您可以實驗並部署 Hadoop 專案至 Azure HDInsight。 這是透過**指令碼動作**功能而啟用，它可以使用自訂指令碼，任意修改 Hadoop 叢集。 此自訂可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。 為了示範此功能的威力，我們已記錄下安裝熱門 <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>、<a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>、<a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a> 和 <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> 模組的程序。 此版本也加入讓客戶透過 Azure 入口網站指定自訂指令碼動作的功能、提供關於如何使用協助程式方法建置自訂指令碼動作的方針和最佳實務作法，以及提供如何測試指令碼動作的方針。 </p></td>
<td>功能公開上市</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>HDInsight 2014/12/5 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼為：

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* HDInsight SDK N/A

此版本包含下列元件更新：

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>Bug 修正：將大量分割加入 Hive DDL 中的資料表時發生間歇性的錯誤 </td>
<td><p>將大量分割加入 Hive 資料表時，如果 Hive 中繼存放區資料庫發生間歇性的連接錯誤，則 Hive DDL 可能會失敗。 如果發生此失敗，您會在 Hive 錯誤記錄中看到下列陳述式： </p><p>"錯誤 [main]：ql.Driver (SessionState.java:printError(547)) - 失敗：執行錯誤，從 org.apache.hadoop.hive.ql.exec.DDLTask 傳回代碼 1。 MetaException(message:java.lang.RuntimeException: commitTransaction 已呼叫，但 openTransactionCalls = 0。 這可能表示對 openTransaction/commitTransaction 進行不平衡的呼叫)"</p></td>
<td>Hive</td>
<td>Hadoop、Hbase</td>
<td>HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。 在此記錄供參考之用。)</td>
</tr>
<tr>
<td>Bug 修正：HDInsight 查詢主控台偶爾停止回應</td>
<td>發生此情況時，可在 WebHCat 啟動器工作的 WebHCat 記錄中看到下列陳述： <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): 無法載入歷程記錄檔 {歷程記錄檔的 wasb url}"</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。 在此記錄供參考之用。)</td>
</tr>
<tr>
<td>Bug 修正：Hbase 查詢延遲偶爾激增</td>
<td>如果發生這種情況，使用者會發現 Hbase 查詢延遲偶爾會激增 3 秒。 </td>
<td>HDInsight 叢集閘道</td>
<td>HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>HDP JAR 檔案名稱變更</td>
<td>若為 HDI 叢集 3.0 版，HDP 安裝的內部 JAR 檔案有一些變更。 jetty-6.1.26.jar 已取代為 jetty-6.1.26.hwx.jar。 jetty-util-6.1.26.jar 已取代為 jetty-util-6.1.26.hwx.jar。 這些變更適用於 Hadoop、Mahout、WebHCat 和 Oozie 專案。</td>
<td>Hadoop、Mahout、WebHCat、Oozie</td>
<td>Hadoop、HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>HDInsight 2014/11/21 版本的相關資訊
使用此版本部署的 HDInsight 叢集的完整版本號碼為：

* HDInsight 2.1.9.382.1169709 (從 2014/11/14 後未變更)
* HDInsight 3.0.5.382.1169709 (從 2014/11/14 後未變更)
* HDInsight 3.1.1.382.1169709 (從 2014/11/14 後未變更)
* HDInsight SDK 1.4.0

此版本包含下列元件更新：

<table border="1">
<tr><th>Title</th><th>說明</th><th>元件</th><th>叢集類型</th><th>JIRA (如果適用)</th></tr>
<tr>
<td>存取應用程式記錄</td>
<td>您能夠以程式設計的方式列舉在叢集上執行的應用程式，並下載相關的應用程式特定或容器特定記錄以協助偵錯有問題的應用程式。</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>在 IHdInsightClient.DeleteCluster 中指定地區名稱的能力 </td>
<td>Azure HDInsight SDK 提供在使用 **DeleteCluster** 時指定區域名稱的能力。 這有助於解除封鎖在不同地區擁有兩個同名資源且已無法刪除任一資源的客戶。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>**ClusterDetails** 物件會傳回 **DeploymentID** 欄位，它代表叢集的唯一識別項。 這可在具相同名稱跨叢集建立嘗試時，保證有唯一的名稱。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>HDInsight 2014/11/14 版本的相關資訊

使用此版本部署的 HDInsight 叢集的完整版本號碼為：

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

此版本包含下列新功能、元件更新和 Bug 修正。

<table border="1">
<tr><th>課程名稱</th><th>說明</th><th>元件</th><th>叢集類型</th><th>JIRA (如果適用)</th></tr>
<tr>
<td>指令碼動作 (預覽)</td>
<td>叢集自訂功能的預覽，可使用自訂指令碼以任意方式來修改 Hadoop 叢集。 有了此功能，使用者可實驗從 Apache Hadoop 生態系統取得的專案，以及將專案部署到 Azure HDInsight 叢集。 此自訂功能可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。</td>
<td>新功能</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>為 Azure 網站與儲存體記錄分析先行建置的工作</td>
<td>HDInsight 查詢主控台具有使用者入門庫，其支援在您的資料或資料範例上運作的方案。
<p>**在您資料上運作的方案**：<br>
我們已經為部分最常見的資料分析案例建立工作，以做為建立您自己的方案的起點。 您可以執行工作來使用您的資料，以查看其運作方式。 接著在就緒時，使用已學得的知識來建立您在預先建立工作後所製作的方案模型。</p>
<p>**在資料範例上運作的方案**：<br>
逐步執行部分基本案例 (例如分析 Web 記錄和感應器資料) 來了解如何使用 HDInsight。 您會了解如何使用 HDInsight 來分析此類資料，以及如何將其他應用程式和服務連線至此資料。 藉由連線至 Microsoft Excel 來提供此強大方案範例，藉此視覺化資料。</p></td>
<td>查詢主控台</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Templeton 中的記憶體遺漏修正</td>
<td>已解決 Templeton 中的記憶體流失，該問題會影響已長期執行叢集的客戶，或每秒提交數百次工作要求的客戶。 此問題會顯示為 Templeton 5xx 錯誤，且因應措施為重新啟動服務。 不再需要此因應措施。</td>
<td>Templeton</td>
<td>全部</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> 為了示範叢集自訂所提供的新功能，已記錄使用指令碼動作在叢集上安裝 Spark 和 R 模組的程序。 如需詳細資訊，請參閱：

* [在 HDInsight 叢集上安裝和使用 Spark 1.0](hdinsight-hadoop-spark-install.md)
* [在 HDInsight Hadoop 叢集上安裝和使用 R](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>HDInsight 2014/11/07 版本的相關資訊

使用此版本部署的 HDInsight 叢集的完整版本號碼為：

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

此版本包含下列元件更新：

<table border="1">
<tr><th>Title</th><th>說明</th><th>元件</th><th>叢集類型</th><th>JIRA (如果適用)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>此版本根據 Hortonworks Data Platform (HDP) 2.1.7。 如需詳細資訊，請參閱 <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">HDP 2.1.7 的版本資訊</a>。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>YARN Timeline Server</td>
<td>YARN Timeline Server (也稱為 Generic Application History Server) 預設已啟用。 Timeline Server 提供已完成應用程式的泛型資訊 (例如應用程式 ID、應用程式名稱、應用程式狀態、應用程式提交時間及應用程式完成時間)。

可透過存取 URI http://headnodehost:8188 或執行 YARN 命令：yarn application -list -appStates ALL，從前端節點擷取此應用程式資訊。

此資訊也可以透過 REST API 從 https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/ 遠端擷取。

如需詳細資訊，請參閱 <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>。</td>
<td>服務、YARN</td>
<td>Hadoop、HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>叢集部署 ID</td>
<td>從 SDK 1.3.3.1.5426.29232 版開始，使用者可存取 HDInsight 發行給每個叢集的唯一 ID。 這能讓客戶在跨建立/捨棄案例重複使用 DNS 名稱時，找出叢集的唯一執行個體。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

> [!NOTE]
> 這個版本已修正防止入口網站顯示及防止 SDK 或 Windows PowerShell 傳回完整版本號碼的 Bug。

## <a name="notes-for-10152014-release"></a>2014/10/15 版本的相關資訊

此 Hotfix 版本修復 Templeton 中影響 Templeton 重度使用者的記憶體遺漏。 在某些情況下，Templeton 的重度使用者會看到以 500 錯誤碼表示的錯誤，因為要求沒有足夠的記憶體可執行。 重新啟動 Templeton 服務就能解決此問題。 已修正此問題。

## <a name="notes-for-1072014-release"></a>2014/10/7 版本的相關資訊

* 使用 Ambari 端點 "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" 時，*host_name* 欄位會傳回節點的完整網域名稱 (FQDN)，而不只是主機名稱。 例如，不是傳回 "**headnode0**"，而是傳回 FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**"。 需要此變更才能協助在一個虛擬網路中部署多種叢集類型 (例如 HBase 和 Hadoop) 的情況。 例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。

* 我們為 HDInsight 叢集的預設部署提供新的記憶體設定。 先前的預設記憶體設定並未充分考量所部署 CPU 核心數目的方針。 根據 Hortonworks 建議，這些新的記憶體設定應該提供更佳的預設值。 若要變更，請參閱關於變更叢集組態的 SDK 參考文件。 下表列舉預設 4 CPU 核心 (8 容器) HDInsight 叢集所使用的新記憶體設定。 (同時也附帶提供此版本之前使用的值。)

<table border="1">
<tr><th>元件</th><th>記憶體配置</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768 MB (先前是 512 MB)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6144 MB (未變更)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6144 MB (未變更)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768 MB (先前是 512 MB)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m (先前是 -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1536 MB (先前是 1024 MB)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m (先前是 -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768 MB (先前是 1024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m (先前是 -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256 MB (先前是 200 MB)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1536 MB (未變更)</td></tr>
</table>

如需 HDInsight 使用的 Hortonworks Data Platform 上供 YARN 和 MapReduce 使用的記憶體組態設定的詳細資訊，請參閱 [決定 HDP 記憶體組態設定](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html)。 Hortonworks 也提供工具來計算適當的記憶體設定。

關於 Azure PowerShell 和 HDInsight SDK 的錯誤訊息：「叢集未設定 HTTP 服務存取」：

* 此錯誤是已知的[相容性問題](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight)，起因可能是 HDInsight 或 Azure PowerShell 版本和叢集版本的差異。 在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。 但舊版的 HDInsight SDK 或 Azure PowerShell 無法正確解譯此功能。 結果造成某些工作提交作業失敗。 如果您使用 HDInsight SDK API 或 Azure PowerShell Cmdlet (**Use-AzureRmHDInsightCluster** 或 **Invoke-AzureRmHDInsightHiveJob**) 來提交工作，這些作業可能會失敗並傳回錯誤訊息「叢集 <clustername> 未設定 HTTP 服務存取」。 或者 (根據作業而定) 傳回其他錯誤訊息，例如「無法連接到叢集」。
* 最新版的 HDInsight SDK 和 Azure PowerShell 中已解決這些相容性問題。 建議將 HDInsight SDK 更新到 1.3.1.6 版或更新版本，並將 Azure PowerShell 工具更新到 0.8.8 版或更新版本。 您可以從 [NuGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) 取得最新的 HDInsight SDK，並從[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 取得 Azure PowerShell 工具。

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>HDInsight 3.1 2014/9/12 版本的相關資訊
* 此版本根據 Hortonworks Data Platform (HDP) 2.1.5。 如需此版本中修正的 Bug 清單，請參閱 Hortonworks 網站上的 [已在此版本修正](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) 頁面。
* 在 Pig 程式庫資料夾中，"avro-mapred-1.7.4.jar" 檔案已變更為 "avro-mapred-1.7.4-hadoop2.jar"。 此檔案的內容包含非中斷的次要 Bug 修正。 建議客戶不要直接依賴 JAR 檔案的名稱，以避免檔案重新命名時中斷。

## <a name="notes-for-8212014-release"></a>2014/8/21 版本的相關資訊
* 我們加入下列 WebHCat 組態 (HIVE-7155)，其將 Templeton 控制器工作的預設記憶體限制設為 1GB。 (先前的預設值是 512 MB。)

     templeton.mapper.memory.mb (=1024)

  * 此變更解決了某些 Hive 查詢因為記憶體限制較低而發生的下列錯誤：「容器超過實體記憶體限制」。
  * 若要還原成舊的預設值，您可以在建立叢集時使用下列命令以透過 Azure PowerShell 將此組態值設為 512：

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* Zookeeper 角色的主機名稱已變更為 *zookeeper*。 這會影響叢集內的名稱解析，但不影響外部 REST API。 如果您有元件使用 *zookeepernode* 主機名稱，則必須更新元件以改用新名稱。 三個 zookeeper 節點的新名稱如下：

  * zookeeper0
  * zookeeper1
  * zookeeper2
* 已更新 HBase 版本支援矩陣。 只有 HBase 工作負載的生產才能支援 HDInsight 3.1 版 (HBase 0.98 版)。 將不再支援 3.0 版(之前可用於預覽)。

## <a name="notes-about-clusters-created-prior-to-8152014"></a>2014/8/15 之前所建立之叢集的附註
因為 Azure PowerShell 或 HDInsight SDK 的版本與叢集版本不同，而可能遇到 Azure PowerShell 或 HDInsight SDK 錯誤訊息：「HTTP 服務存取未設定叢集 <clustername>」(或者根據作業而定，可能遇到其他錯誤訊息，例如「*無法連接到叢集*」)。 在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。 舊版的 Azure PowerShell 或 HDInsight SDK 無法正確解譯此功能，導致工作提交作業失敗。 如果您使用 HDInsight SDK API 或 Azure PowerShell Cmdlet (例如 Use-AzureRmHDInsightCluster 或 Invoke-AzureRmHDInsightHiveJob) 來提交工作，這些作業可能會失敗並傳回上述其中一個錯誤訊息。

最新版的 HDInsight SDK 和 Azure PowerShell 中已解決這些相容性問題。 建議將 HDInsight SDK 更新到 1.3.1.6 版或更新版本，並將 Azure PowerShell 工具更新到 0.8.8 版或更新版本。 您可以從 [NuGet][nuget-link] 存取最新的 HDInsight SDK。 您可以使用 [Microsoft Web Platform Installer][webpi-link] 存取 Azure PowerShell 工具。

## <a name="notes-for-7282014-release"></a>2014/7/28 版本的相關資訊
* **新區域可用 HDInsight**：我們將 HDInsight 的地理位置據點擴展到三個區域。 HDInsight 客戶可以在這三個區域建立叢集：
  * 東亞
  * 美國中北部
  * 美國中南部
* 正在將 HDInsight 1.6 版 (HDP 1.1 和 Hadoop 1.0.3) 和 HDInsight 2.1 版 (HDP1.3 和 Hadoop 1.2) 從 Azure 入口網站移除。 您可以繼續使用 Azure PowerShell Cmdlet、[New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) 或使用 [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx) 來建立這些版本的 Hadoop 叢集。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。
* 此版本中的 Hortonworks Data Platform (HDP) 變更：

<table border="1">
<tr><th>HDP</th><th>變更</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>沒有變更</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>沒有變更</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>2014/6/24 版本的相關資訊
此版本包含 HDInsight 服務的增強功能：

* **HDP 2.1 可用性**：HDInsight 3.1 (內含 HDP 2.1) 已公開上市，且為新叢集的預設版本。
* **HBase - Azure 入口網站改進**：我們正使 HBase 叢集可用於預覽版。 您可以從入口網站建立 HBase 叢集，只要按幾下滑鼠即可。

HBase 可讓您在 HDInsight 上建置各種即時工作負載，包括處理大型資料集的互動式網站，甚至是將數百萬個端點的感應器和遙測資料儲存起來的服務，都沒問題。 下一步是使用 Hadoop 工作來分析這些工作負載中的資料，而透過 Azure PowerShell 和 Hive 叢集儀表板，就能在 HDInsight 中進行此分析。

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout 預先安裝在 HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) 已預先安裝在 HDInsight 3.1 Hadoop 叢集，因此您可以執行 Mahout 工作，而不需要其他叢集組態。 例如，您可以使用遠端桌面通訊協定 (RDP) 從遠端進入 Hadoop 叢集，且不需要額外的步驟就能執行下列 Hello World Mahout 命令：

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

如需此程序更完整的說明，請參閱 Apache Mahout 網站上關於 [Breiman 範例](https://mahout.apache.org/users/classification/breiman-example.html) 的文件。

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Hive 查詢可在 HDinsight 3.1 中使用 Tez
Hive 0.13 可在 HDInsight 3.1 中使用，且能夠使用 Tez 來執行查詢，妥善運用可大幅提升效能。
依預設不會對 Hive 查詢啟用 Tez。 若要使用，您必須自行啟用。 您可以執行下列程式碼片段來啟用 Tez：

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks 在標準效能評比中，已發表一份關於 Hive 查詢搭配 Tez 而提升效能的詳細數據。 如需詳細資訊，請參閱 [Apache Hive 13 for Enterprise Hadoop 效能評比](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/)(英文)。

如需詳細資訊，請參閱 [Tez 上的 Hive](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)。

### <a name="global-availability"></a>正式上市
隨著 HDInsight 在 Hadoop 2.2 上推出，Microsoft 已在所有主要的 Azure 提供地理區提供 HDInsight。 尤其，西歐和東南亞資料中心已上線運作。 這可讓客戶將叢集配置在鄰近且可能位於相似符合性需求區域中的資料中心。

### <a name="dos--donts-between-cluster-versions"></a>叢集版本之間的注意事項
**與 HDInsight 3.1 叢集搭配使用的 Oozie 中繼存放區與舊版的 HDInsight 2.1 叢集無法回溯相容，且兩者無法與此舊版本搭配使用**。

與 HDInsight 3.1 叢集一起部署的自訂 Oozie metastore 資料庫，無法在 HDInsight 2.1 叢集上重複使用。 即使是源自 HDInsight 2.1 叢集的中繼存放區也是如此。 不支援此案例，因為中繼存放區結構描述與 HDInsight 3.1 叢集一起使用時會升級，所以與 HDInsight 2.1 叢集所需的中繼存放區就不再相容。 嘗試重複使用已在 HDInsight 3.1 叢集上使用過的 Oozie 中繼存放區，將會使 HDInsight 2.1 叢集變得無法使用。

**叢集之間無法共用 Oozie 中繼存放區。**

Oozie 中繼存放區會連接到特定叢集，且兩者無法在叢集之間共用。

### <a name="breaking-changes"></a>重大變更
**前置詞語法**：HDInsight 3.1 和 3.0 叢集僅支援 "wasb://" 語法。 HDInsight 2.1 和 1.6 叢集支援舊的 "asv://" 語法，但在 HDInsight 3.1 或 3.0 叢集中不支援。 這表示任何提交至 HDInsight 3.1 或 3.0 叢集且明確使用 “asv://” 語法的工作將會失敗。 應該改用 "wasb://" 語法。 此外，如果工作提交至任何以現有中繼存放區建立的 HDInsight 3.1 或 3.0 叢集，且中繼存放區中使用 asv:// 語法來明確參考資源，則也會失敗。 必須使用 "wasb://" 語法來定址資源以重新建立這些中繼存放區。

**連接埠**：已變更 HDInsight 服務所使用的連接埠。 以前所使用的連接埠號碼都在 Windows 作業系統暫時連接埠範圍內。 對於短期的網際網路通訊協定通訊，會自動從預設定義的暫時範圍中配置連接埠。 新的一組允許的 Hortonworks Data Platform (HDP) 服務連接埠號碼不在此範圍內，以避免與前端節點上執行的服務所使用的連接埠發生衝突。 新的連接埠號碼應該不會引起任何重大變更。 使用的號碼如下：

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>名稱</th><th>值</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 和 3.0 (HDP 2.1 和 2.0)**

<table border="1">
<tr><th>名稱</th><th>值</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>相依項目
HDInsight 3.x (HDP2.x) 加入下列相依項目：

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

HDInsight 3.x (HDP2.x) 中已不存在下列相依項目：

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>版本變更
HDInsight 2.x (HDP1.x) 與 HDInsight 3.x (HDP2.x) 之間有下列版本變更：

* metrics-core: ['2.1.2'] -> ['3.0.0']
* derbynet: ['10.4.2.0'] -> ['10.10.1.1']
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper-compiler: ['5.5.12'] -> ['5.5.23']
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] -> ['10.10.1.1']
* httpcore: ['4.2.4'] -> ['4.2.5']
* hsqldb: ['1.8.0.10'] -> ['2.0.0']
* jets3t: ['0.6.1'] -> ['0.9.0']
* protobuf-java: ['2.4.1'] -> ['2.5.0']
* derby: ['10.4.2.0'] -> ['10.10.1.1']
* jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* commons-daemon: ['1.0.1'] -> ['1.0.13']
* datanucleus-core: ['3.0.9'] -> ['3.2.10']
* datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']
* zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>驅動程式
SQL Server 的 Java 資料庫連接 (JDBC) 驅動程式僅供 HDInsight 內部使用，且不適用於外部作業。 如果您想要使用開放式資料庫連接 (ODBC) 連線至 HDInsight，請使用 Microsoft Hive ODBC 驅動程式。 如需詳細資訊，請參閱 [使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 HDInsight](hdinsight-connect-excel-hive-odbc-driver.md)。

### <a name="bug-fixes"></a>錯誤修正
在此版本中，我們使用幾個 Bug 修正來重新整理下列 HDInsight 版本：

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Hortonworks 版本資訊
下列位置提供 HDInsight 版本叢集使用的 Hortonworks Data Platform (HDP) 的版本資訊：

* HDInsight 3.1 版採用以 [Hortonworks Data Platform 2.1.7][hdp-2-1-7] 為基礎的 Hadoop 散發。 這是在 2014/11/7 之後使用 Azure 入口網站時所建立的預設 Hadoop 叢集。 在 2014/11/7 之前建立的 HDInsight 3.1 叢集是以 [Hortonworks Data Platform 2.1.1][hdp-2-1-1] 為基礎。
* HDInsight 3.0 版採用以 [Hortonworks Data Platform 2.0][hdp-2-0-8] 為基礎的 Hadoop 散發。
* HDInsight 2.1 版採用以 [Hortonworks Data Platform 1.3][hdp-1-3-0] 為基礎的 Hadoop 散發。
* HDInsight 1.6 版採用以 [Hortonworks Data Platform 1.1][hdp-1-1-0] 為基礎的 Hadoop 散發。

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
