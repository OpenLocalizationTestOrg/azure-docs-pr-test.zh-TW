---
title: "aaaArchived 版本資訊-Azure HDInsight 上的 Hadoop 元件 |Microsoft 文件"
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
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Azure HDInsight 上 Hadoop 元件的版本資訊 (封存)

本文章提供資訊 hello**舊**Azure HDInsight 版本的更新。 如需有關最近版本的詳細資訊，請參閱 [HDInsight 版本資訊](hdinsight-release-notes.md)。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 版本控制文件](hdinsight-component-versioning.md)。



## <a name="notes-for-08302016-release-of-hdinsight"></a>HDInsight 08/30/2016 版本的相關資訊
此版本中，部署 hello 以 Linux 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

此版本中，部署 hello Windows 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>2016/8/17 - HDInsight 上的 R 伺服器版本資訊
* R 伺服器 8.0.5 - 主要為修正程式的版本。 請參閱 hello [R Server 版本資訊](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)如需詳細資訊。
* AzureML 封裝 hello 邊緣節點-[此 R 封裝](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html)啟用 R 模型 toobe 發佈及使用做為 Azure ML web 服務。  請參閱 hello [「 實施模型 」](hdinsight-hadoop-r-server-overview.md#operationalize-a-model)區段我們["概觀的 R 伺服器上 HDInsight"](hdinsight-hadoop-r-server-overview.md)發行項，如需詳細資訊。
* Linux 相依性的 hello[前 100 個最受歡迎的 R 封裝](https://github.com/metacran/cranlogs)-Linux 封裝的相依性現在預先安裝。
* 選項 toouse hello CRAN 儲存機制時新增 R 封裝 toohello 資料節點。 如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。
* R 伺服器佈建叢集建立時的 hello 改善的可靠性。

## <a name="notes-for-08012016-release-of-hdinsight"></a>HDInsight 2016/08/01 版本的相關資訊
此版本中，部署 hello 以 Linux 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

此版本中，部署 hello Windows 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 變更 tooHDInsight 3.4 叢集 |hello 預設值，如下列的 hive 組態變更更佳的效能 <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |服務 |全部 |N/A |
| 此版本包含下列修正程式 |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |服務 |全部 |N/A |

## <a name="notes-for-07142016-release-of-hdinsight"></a>HDInsight 2016/07/14 版本的相關資訊
此版本中，部署 hello 以 Linux 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 | Ambari 組建 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

此版本中，部署 hello Windows 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>HDInsight 2016/07/07 版本的相關資訊
此版本中，部署 hello 以 Linux 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

此版本中，部署 hello Windows 為基礎的 HDInsight 叢集的完整版本號碼：

| HDI | HDI 叢集版本 | HDP | HDP 組建 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| [HDInsight Tools for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式現在與適用於 IntelliJ 的 Azure 工具組整合。 它支援 Azure SDK v2.9.1，最新的 Java Sdk，並包括 hello 獨立 HDInsight IntelliJ 外掛程式的所有 hello 功能。 |工具 |Spark |N/A |
| [HDInsight Tools for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |適用於 Eclipse 的 Azure 工具組現在支援 HDInsight Spark 叢集。 它可讓 hello 下列功能： <ul><li>透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</li><li>測試本機 hello Spark 應用程式。</li><li>提交工作 tooHDInsight Spark 叢集，並擷取 hello 結果。</li><li>登入 tooAzure 和存取您的 Azure 訂用帳戶相關聯的所有 hello Spark 叢集。</li><li>瀏覽您的 HDInsight Spark 叢集的所有相關聯的 hello 儲存體資源。</li></ul> |工具 |Spark |N/A |

從這個版本開始，我們已變更為以 Linux 為基礎的 HDInsight 叢集的 hello 客體 OS 修補原則。 hello hello 新的原則目標是 toosignificantly 減少重新開機次數 hello 到期 toopatching。 hello 新原則修補程式的虛擬機器 (Vm) 上 Linux 叢集的每個星期一或星期四上午 12 utc，以交錯方式啟動任何指定的叢集節點之間。 不過，任何指定的 VM 只會重新啟動一次每 30 天到期 tooguest OS 修補程式。 此外，新建立的叢集 hello 第一次重新開機不會發生更快地從 hello 叢集建立日期的 30 天前。

> [!NOTE]
> 這些變更只會套用 toonewly 等於或大於這個發行版本建立的叢集。
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>HDInsight 2016/06/06 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

| HDP | HDI 版本 | Spark 版本 | Ambari 組建編號 | HDP 組建編號 |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDInsight 上的 Spark 已正式推出 |此版本會改善可用性、 延展性和產能 tooopen 來源 HDInsight 上的 Apache Spark 中。 <ul><li>業界領先的 99.9% 可用性 SLA，因此能應付企業要求嚴苛的工作負載。</li><li>使用 Azure Data Lake Store 的可調整儲存體層。</li><li>針對資料探索和開發的每個階段皆有相應的生產力工具。 含自訂 Spark 核心的 Jupyter 筆記本會啟用互動式資料探索，並與 BI 儀表板 (例如 Power BI、Tableau 及 Qlik) 整合，非常適合快速資料共用和連續報告；IntelliJ 外掛程式是適用於長期程式碼構件開發和偵錯的可靠方式。</li></ul> |服務 |Spark |N/A |
| HDInsight Tools for IntelliJ |這是適用於 HDInsight Spark 叢集的 IntelliJ IDEA 外掛程式。 它可讓 hello 下列功能：<ul><li>透過針對 IntelliSense 的一流撰寫支援、自動格式化、錯誤檢查等功能，在 Scala 和 Java 中輕鬆建立並撰寫 Spark 應用程式。</li><li>測試本機 hello Spark 應用程式。</li><li>提交工作 tooHDInsight Spark 叢集，並擷取 hello 結果。</li><li>登入 tooAzure 和存取您的 Azure 訂用帳戶相關聯的所有 hello Spark 叢集。</li><li>瀏覽您的 HDInsight Spark 叢集的所有相關聯的 hello 儲存體資源。</li><li>瀏覽 hello 工作歷程記錄和作業的所有資訊 HDInsight Spark 叢集。</li><li>從桌上型電腦遠端偵錯 Spark 作業。</li></ul> |工具 |Spark |N/A |

## <a name="notes-for-05132016-release-of-hdinsight"></a>HDInsight 2016/05/13 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Spark、Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| Spark 版本更新和其他錯誤修正 |此版本更新 hello Spark 版本在 HDInsight 叢集 too1.6.1，並修正其他錯誤 |服務 |Spark |N/A |

## <a name="notes-for-04112016-release-of-hdinsight"></a>HDInsight 2016/04/11 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -未變更)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDI 3.4 的自訂中繼存放區升級問題 |如果您使用先前在另一個較低版本的 HDInsight 叢集上使用的自訂中繼存放區，則叢集會建立失敗。 這是因為 tooan 升級指令碼錯誤現在已修正 |叢集建立 |全部 |N/A |
| Livy Crash 復原 |為所有已透過 Livy 提交的作業提供工作狀態復原 |可靠性 |Spark on Linux |N/A |
| Jupyter 內容 HA |提供 hello 能力 toosave 和負載 Jupyter 筆記本內容 tooand 從 hello 與 hello 叢集相關聯的儲存體帳戶。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。 |筆記本 |Spark on Linux |N/A |
| 移除 Jupyter 筆記本中的 hiveContext |使用 `%%sql` magic，而非 `%%hive` magic。 SqlContext 是相等的 toohiveContext。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md) |筆記本 |Linux 上的 Spark 叢集 |N/A |
| 取代了舊版的 Spark |從 hello 服務上 5/31 中已移除較舊版本的 Spark 1.3.1 |服務 |Windows 上的 Spark 叢集 |N/A |

## <a name="notes-for-03292016-release-of-hdinsight"></a>HDInsight 2016/03/29 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 新增 HDInsight 3.4 版並更新所有 HDInsight 叢集的 HDP 版本 |在此版本中，我們新增了 HDInsight v3.4 (以 HDP 2.4 為基礎) 並且更新了其他 HDP 版本。 HDP 2.4 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。 |服務 |所有 Linux 叢集 |N/A |
| HDInsight Premium |HDInsight 現在有兩種類別：Standard 和 Premium。 HDInsight Premium 目前為預覽版，僅適用於 Linux 上的 Hadoop 和 Spark 叢集。 如需詳細資訊，請參閱[這裡](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。 |服務 |Linux 上的 Hadoop 和 Spark |N/A |
| Microsoft R 伺服器 |HDInsight Premium 提供 Microsoft R 伺服器，它可以隨附於 Linux 上的 Hadoop 與 Spark 叢集。 如需詳細資訊，請參閱 [HDInsight 中的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)。 |服務 |Linux 上的 Hadoop 和 Spark |N/A |
| Spark 1.6.0 |HDInsight 3.4 叢集現在包含 Spark 1.6.0 |服務 |Linux 上的 Spark 叢集 |N/A |
| Jupyter Notebook 增強功能 |可用於 Spark 叢集的 Jupyter Nnotebook 現在提供額外的 Spark 核心。 其中也包括增強功能，例如使用 %%magic、自動視覺化，以及與 Python 視覺化程式庫 (例如 matplotlib) 整合。 如需詳細資訊，請參閱 [可供 Jupyter 筆記本使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。 |服務 |Linux 上的 Spark 叢集 |N/A |

## <a name="notes-for-03222016-release-of-hdinsight"></a>HDInsight 2016/03/22 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 未變更)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 未變更)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 未變更)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-03102016-release-of-hdinsight"></a>HDInsight 2016/03/10 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - 未變更)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-01272016-release-of-hdinsight"></a>HDInsight 2016/01/27 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - 未變更)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，我們已更新所有 HDInsight 叢集的 HDInsight 版本 |服務 |全部 |N/A |

## <a name="notes-for-12022015-release-of-hdinsight"></a>HDInsight 2015/12/02 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - 未變更)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - 未變更)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 新增 HDInsight 3.3 版並更新所有 HDInsight 叢集的 HDP 版本 |在此版本中，我們新增了 HDInsight v3.3 (以 HDP 2.3 為基礎) 並且更新了其他 HDP 版本。 HDP 2.3 版本附註可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。 |服務 |全部 |N/A |

## <a name="notes-for-11302015-release-of-hdinsight"></a>HDInsight 2015/11/30 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 所有 HDInsight 叢集的已更新 HDInsight 版本和 HDInsight 3.2 叢集的 HDP 版本 (Windows 和 Linux) |在此版本中，HDInsight 和 HDP 版本均已更新 |服務 |全部 |N/A |

## <a name="notes-for-10272015-release-of-hdinsight"></a>HDInsight 2015/10/27 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - 未變更)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 (Windows 和 Linux) |在此版本中，HDInsight 和 HDP 版本均已更新 |服務 |全部 |N/A |
| 修正包含大寫字母叢集之 Windows Spark 叢集的 Jupyter |必須指定以大寫字母輸入的 DNS 名稱的叢集必須 Jupyter 筆記本 tooan 原始要求檢查到期的問題。 hello 修正不 Jupyter 的組態 toolower 案例 toochange hello DNS 名稱。 |服務 |HDInsight Spark (Windows) |N/A |

## <a name="notes-for-10202015-release-of-hdinsight"></a>HDInsight 2015/10/20 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 預設 HDP 版本已變更 tooHDP 2.2 |HDInsight Windows 叢集的 hello 預設版本為變更的 tooHDP 2.2。 HDInsight 版本 3.2 (HDP 2.2) 自 2015 年 2 月已在公開上市。 這項變更只翻轉 hello 預設叢集版本，當尚未佈建 hello 叢集使用 hello Azure 入口網站、 PowerShell cmdlet 或 hello SDK 時進行明確的選取項目。 |服務 |全部 |N/A |
| 變更 VM 名稱格式以在單一虛擬網路中的 Linux 叢集上部署多個 HDInsight。 |在這個版本中已加入在單一虛擬網路中部署多個 HDInsight Linux 叢集的支援。 更新的一部分，hello hello 叢集中的虛擬機器名稱格式已從叢集前端節點\*，workernode\*和 zookeepernode\* toohn\*，wn\*，和 zk\*分別。 不建議的作法 tootake 直接相依性 hello 格式的虛擬機器名稱，因為這是主體 toochange。 使用 「 主機名稱-f"hello 本機電腦上的主機和 hello 對應的元件 toohosts Ambari Api toodetermine hello 清單。 您可以在 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) 和 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md) 找到更多資訊。 |服務 |Linux 上的 HDInsight 叢集 |N/A |
| 組態變更 |HDInsight 3.1 叢集，現在會啟用 hello 的設定： <ul><li>tez.yarn.ats.enabled 和 yarn.log.server.url。 這可讓應用程式時間軸伺服器 hello 和 hello 記錄伺服器 toobe 無法 tooserve 出記錄檔。</li></ul>HDInsight 3.2 叢集已修改 hello 的設定： <ul><li>已設定 too2 mapreduce.fileoutputcommitter.algorithm.version。 這可讓您使用 hello FileOutputCommitter hello V2 版。</li></ul> |服務 |全部 |N/A |

## <a name="notes-for-09092015-release-of-hdinsight"></a>HDInsight 2015/09/09 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，HDInsight 版本已更新 |服務 |全部 |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight 2015/07/31 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 修正 Spark 叢集節點的重新製作映像工作流程 |修正造成 Spark toonot 復原後重新安裝映像的叢集節點的 bug |服務 |Spark |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight 2015/07/31 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - 未變更)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| 更新所有 HDInsight 叢集的 HDInsight 版本 |在此版本中，HDInsight 版本已更新 |服務 |全部 |N/A |

## <a name="notes-for-07072015-release-of-hdinsight"></a>HDInsight 2015/07/07 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* SDK            1.5.8

這個版本包含下列更新的 hello:

| Title | 說明 | 受影響的區域 (例如服務、元件或 SDK) | 叢集類型 (例如 Hadoop、HBase 或 Storm) | JIRA (如果適用) |
| --- | --- | --- | --- | --- |
| HDInsight 3.2 叢集的更新後 HDP 版本 |在此版本中，HDInsight 3.2 會部署 HDP 2.2.6.1-0012 |服務 |全部 |N/A |

## <a name="notes-for-06262015-release-of-hdinsight"></a>HDInsight 2015/06/26 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - 未變更)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
<td>hello 雲端服務現在會開啟 5 連接埠 8001 too8005 hello 叢集例如上 https://<clustername>.azurehdinsight.net:8001/。 使用驗證 toothese Url 的要求 hello 相同基本驗證的密碼機制，做為連接埠 443。 這些連接埠繫結的 toohello 相同 hello 作用中叢集前端節點連接埠。 指令碼動作可以使用的 toomake 客戶服務接聽 hello 叢集前端節點和路由 toooutside hello 叢集上的這些連接埠上。</td>
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
<td>適用於 HDInsight 3.2 移動 tooLatest Azure Java SDK 2.2</td>
<td>移動 toolatest 版的 hello Azure SDK for Java hello WASB 驅動程式所使用。 hello 最新的 SDK 有幾個修正和 hello hello 版本資訊相同 https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt 在。</td>
<td>Hadoop 核心</td>
<td>全部</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>移動 tooHDP 2.1.15 HDInsight 3.1 叢集</td>
<td>Hortonworks hello 發行的版本資訊可用<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">這裡</a>。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>HDInsight 2015/06/04 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - 未變更)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
<td>此版本已修正 bug，會影響在重新開機後，向下造成 hello 網站 toobe hello 工作提交 API。</td>
<td>服務</td>
<td>Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>HDInsight 2015/06/01 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - 未變更)
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - 未變更)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
<td>此版本已修正的 bug 相關 toocluster 佈建。</td>
<td>服務</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>HDInsight 2015/05/27 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* 其他叢集版本和 SDK 不會部署為此版本的一部分。

這個版本包含下列更新的 hello:

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
<td>這一版的 HDInsight 3.2 包含 HDP 2.2.6，並將數個重要的 bug 修正 tooHDInsight。 hello 完整版本資訊位於<a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 Release Notes</a>。</td>
<td>HDP</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
<tr>
<td>變更 tooDefault Yarn 容器記憶體組態</td>
<td>在這項更新，hello 預設可用的記憶體 tooYARN 容器 （yarn.nodemanager.resource.memory mb 和 yarn.scheduler.maximum 配置 mb），啟動的節點管理員，增加的 too5632MB。 之前這是精簡的 too4608MB，但根據不同的工作執行，hello 新值必須提供更好的可靠性和效能 toomost 作業，因此更好的預設值。 像往常一樣，這個記憶體組態中有重要的相依性，如果它明確設定時建立 hello 叢集。</td>
<td>HDP</td>
<td>所有叢集類型</td>
<td>N/A</td>
</tr>
<tr>
<td>HBase 和 Storm 叢集的預設組態同位檢查</td>
<td>此更新還原 Hbase 和 Storm 叢集 toouse hello Hadoop 叢集的 YARN 組態相同值。 這是為了進行所有叢集類型的同位檢查。</td>
<td>HDP</td>
<td>HBase、Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>HDInsight 2015/05/20 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
<td>HDInsight Storm 的 hello 更新叢集封裝會將新的功能 tooSCP.NET。 您現在可以存取 toonew 應用程式開發介面，可讓您更容易 toouse EventHubSpout 或 Java Spouts 拓撲產生器中。 在更新 hello 合約，您必須更新您 SCP.NET 用戶端 SDK toowork 的新叢集。 如需詳細資訊，在 hello （包括錯誤修正） 的新 Api、 使用量和版本資訊，請參閱 toohello hello SCP.NET NuGet 封裝中包含的讀我檔案。</td>
<td>VS 工具</td>
<td>Storm HDInsight 3.2 叢集</td>
<td>N/A</td>
</tr>
<tr>
<td>JDBC 驅動程式更新</td>
<td>更新的 hello 驅動程式 toohello SQL Server 支援 sqljdbc_4.1.5605.100 版本。</td>
<td>Metastore</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>HDInsight 2015/04/27 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* SDK            1.5.8

這個版本包含下列更新的 hello:

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
<td>叢集現在對 PUT 等候要求 toobe 接受輪詢 hello 狀態之前，建立要求</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>HDInsight 2015/04/14 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* SDK            1.5.6

這個版本包含下列更新的 hello:

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
<td>Apache TEZ 2214 和 TEZ 1923 的修正包含在此版本的 HDI 3.2。 這些會需要某些 Hive 查詢上 Tez 需要 tooshuffle 大量的資料。
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>HDInsight 2015/04/06 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 未變更)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 未變更)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 未變更)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* SDK            1.5.6

這個版本包含下列更新的 hello:

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
<td>Linux 上的 HDInsight 更新 tooremove 某些內部的類別。</td>
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
<td>各種 bug 修正 toohello 服務</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>HDInsight 2015/04/01 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* SDK            1.5.5

這個版本包含下列更新的 hello:

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>受影響的區域 (例如服務、元件或 SDK)</p></th>
<th>叢集類型 (例如 Hadoop、HBase 或 Storm)</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>能力 tooenable/停用遠端桌面認證透過.NET SDK 的 Windows 叢集上</td>
<td>針對在 Windows 叢集上啟用或停用 RDP 認證的程式設計支援。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>能力 tooenable 遠端桌面認證到叢集，雖然它們正在佈建</td>
<td>以程式設計方式啟用遠端桌面認證，因為正在建立 hello 叢集的支援。 這會移除 hello 兩步驟程序的第一個佈建的 hello 叢集，然後啟用 遠端桌面。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>升級的 Python too2.7.8</td>
<td>升級的 Python 上的 HDInsight 叢集 tooPython 2.7.8，其中包含一些重要的安全性修正 HDInsight 版本 2.1、 3.0、 3.1 和 3.2</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>YARN 組態變更</td>
<td>變更的 YARN 組態 yarn.resourcemanager.max 完成應用 too1000 的 HDInsight 版本 3.1 和 3.2 中的所有叢集類型。 這個值只會控制 hello hello YARN UI 中的已完成應用程式清單。 應用程式的 tooget 資訊送出先前 toohello 顯示 hello UI，您可以直接移 toohello 記錄伺服器的應用程式清單。</td>
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
<td>JDBC SQL 驅動程式會升級的 tooversion sqljdbc_4.0.2206.100 hdinsight 3.2 版。 此版本包含重要的安全性增強功能。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>JVM 組態更新</td>
<td>更新的 JVM 組態 networkaddress.cache.ttl too300 hello 預設值為-1 秒為單位 3.1 和 3.2 中的 HDInsight 版本。 此設定值會控制快取原則的成功名稱查閱，從 hello 名稱服務的 hello。 這會修正 bug 相關 toogrowing 和壓縮 HBase 叢集。</td>
<td>服務</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>升級 tooAzure 儲存體 SDK for Java 2.0</td>
<td>HDInsight 3.2 版是升級的 toouse hello Azure 儲存體 SDK for Java 的 hello 最新版本。 這是透過 hello 目前 0.6.0 版本包含數個重要的 bug 修正。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>升級的 tooApache WASB 原始程式碼</td>
<td>HDInsight 現在使用 hello 最新的程式碼從 Apache Hadoop 的 hello WASB 檔案系統驅動程式 3.2 版。 透過這項變更，hello WASB 驅動程式現在會封裝為個別的 jar。 這是單純的封裝變更，而且不包含任何的變更 toobehavior hello WASB 驅動程式。 hello 這個 JAR 檔案名稱是 hadoop-azure-2.6.0.jar。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDInsight 3.2 中的 Jar 檔案名稱更新</td>
<td>此更新 tooHDInsight 版本 3.2 包含數個 bug 修正，，且已經升級幾個內部 （每瓶） 封裝為 HDP 的一部分。 這些 JAR filesare 內部 toohello HDP 封裝並不供客戶應用程式直接使用。 應用程式應該封裝 hello （每瓶） 他們自己版本，以便升級 toohello Jar HDP 內部不會中斷客戶應用程式。</td>
<td>HDP</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>HDInsight 2015/03/03 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - 未變更)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - 未變更)
* SDK            1.5.0                (未變更)

這個版本包含下列更新的 hello:

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
<td>我們進行了允許 hello 服務 tooscale hello 增加的負載方面 toocluster 建立較佳的修正。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>HDInsight 2015/02/18 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - 未變更)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* SDK            1.5.0

這個版本包含下列更新的 hello:

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
<td>HDInsight 3.2 叢集提供 Hadoop 2.6/HDP2.2。 它包含主要更新 tooall 的 hello 開放原始碼的元件。 如需詳細資訊，請參閱 HDInsight 的新功能和 <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 版本資訊</a>。</td>
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
<td>Azure HDInsight 可用於更多虛擬機器類型和大小。 HDInsight 可以利用內建的一般用途; A2 tooA7 大小功能固態硬碟 (Ssd) 和更快的處理器; 60%的 D 系列節點並支援快速的網路有 InfiniBand 的 A8 和 A9 的大小。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>叢集縮放</td>
<td>您可以變更 hello 資料執行的 HDInsight 叢集的節點數目，而不需要 toodelete 或重新建立它。 目前只有 Hadoop 查詢和 Apache Storm 的叢集類型具有這項能力，但支援 Apache HBase 叢集類型很快就是 toofollow。 如需詳細資訊，請參閱＜管理 HDInsight 叢集＞。</td>
<td>服務</td>
<td>Hadoop、Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Visual Studio 工具</td>
<td>此外 toocomplete tooling Apache Storm，hello 工具來 Apache Hive Visual Studio 中的已更新的 tooinclude 陳述式完成、 本機驗證，以及改善的偵錯支援。 如需詳細資訊，請參閱＜開始使用 HDInsight Tools for Visual Studio＞。</td>
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
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* SDK            N/A

這個版本包含下列更新的 hello:

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
<td>HDInsight 3.1 是更新的 toodeploy HDP 2.1.10.0。 如需詳細資訊，請參閱<a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">版本資訊 HDP-2.1.10</a>。 </td>
<td>開放原始碼軟體</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>HDP 二進位更新</td>
<td>HBase 中有一些 JAR 檔的檔案名稱已更新。 這些 JAR 檔案可供在內部 HBase，因此不預期客戶具有下列 JAR 檔案 hello 名稱的相依性。 其中包含：
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
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  未變更)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  未變更)
* SDK            N/A

這個版本包含下列更新的 hello:

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
<td>我們進行了幾個重要的 bug 修正，改善 Azure 升級期間的 hello 可靠性 hello HDInsight 叢集。</td>
<td>服務</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>HDInsight 2015/1/5 版本的相關資訊
hello 與這一版一起部署的 HDInsight 叢集的完整版本號碼：

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - 未變更)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - 未變更)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - 未變更)

這個版本包含下列更新的 hello:

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
<td><p>在此版本中，hello HDInsight 查詢主控台有兩個其他範例：</p>

<p><b>Twitter 趨勢分析</b><br>
像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。 在本教學課程，了解如何 toouse hive 控制檔 tooget 傳送嗨大部分推文含有特定單字的 Twitter 使用者的清單。 </p>

<p><b>Mahout 電影推薦</b><br>
Apache Mahout 是 Apache Hadoop 的機器學習庫。 Mahout 包含用來處理資料 (例如篩選、分類和叢集化) 的演算法。 在本教學課程中，使用 根據您的朋友看過的電影建議引擎 toogenerate 影片建議。</p></td>
<td>查詢主控台</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>變更 toodefault Hive 組態值： hive.auto.convert.join.noconditionaltask.size</td>
<td><p>此大小設定套用轉換 tooautomatically 對應聯結。 hello 值代表 hello 大小的資料表可放入記憶體中的轉換的 toohash 對應 hello 總和。 在先前的版本中，此值會增加從 hello 預設值是 10 MB too128 MB。 不過，hello 128 mb 的新值導致工作 toofail 到期 toolack 的記憶體。 此版本中還原 hello 預設值回 too10 MB。 客戶仍然可以選擇 toooverride 該值叢集建立期間，指定其查詢和資料表的大小。 如需這項設定的詳細資訊及如何 toooverride，請參閱<a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">最佳化自動聯結轉換</a>Hortonworks 文件中。 </p></td>
<td>Hive</td>
<td>Hadoop、Hbase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>HDInsight 2014/12/23 版本的相關資訊
HDInsight 叢集部署此版本中的 hello 完整版本號碼為：

* HDInsight     2.1.10.420.1246783    (HDP 版本未變更)
* HDInsight     3.0.6.420.1246783    (HDP 版本未變更)
* HDInsight     3.1.1.420.1246783    (HDP 版本未變更)

這個版本包含下列更新的 hello:

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>由於 tooexcessive 負載間歇性的叢集建立失敗</td>
<td><p>改善的演算法在叢集建立期間下載 HDP 封裝可讓更穩固處理的失敗，因為 tooexcessive 負載。</p></td>
<td>服務</td>
<td>Hadoop、HBase、Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>HDInsight 2014/12/18 版本的相關資訊
這個版本包含下列元件更新 hello:

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
<td><p>自訂 hello 功能為您提供的 toocustomize Azure HDInsight 叢集，都是從 hello Apache Hadoop 生態系統的專案。 使用這項新功能，您可以試驗並部署 Hadoop 專案 tooAzure HDInsight。 啟用此選項透過 hello**指令碼動作**功能，可以修改 Hadoop 叢集以任意方式使用自訂指令碼。 此自訂可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。 這項功能的 toodemonstrate hello 電源，我們記載的 hello 受歡迎的程序 tooinstall hello <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>， <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>， <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>，和<a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a>模組。 此版本也加入 hello 功能，提供客戶 toospecify hello Azure 入口網站透過自訂指令碼動作、 提供指導方針和最佳作法，關於如何 toobuild 自訂指令碼動作使用的 helper 方法，並提供有關如何指導方針 tootesthello 指令碼動作。 </p></td>
<td>功能公開上市</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>HDInsight 2014/12/5 版本的相關資訊
HDInsight 叢集部署此版本中的 hello 完整版本號碼為：

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* HDInsight SDK N/A

這個版本包含下列元件更新 hello:

<table border="1">
<tr>
<th>Title</th>
<th>說明</th>
<th>元件</th>
<th>叢集類型</th>
<th>JIRA (如果適用)</th>
</tr>
<tr>
<td>Bug 修正： hive 控制檔的 DDL 中新增大量的資料分割 tooa 資料表時發生的間歇性錯誤 </td>
<td><p>如果有間歇性連線錯誤與 hello Hive 中繼存放區資料庫加入大量資料分割 tooa Hive 資料表時，可能會失敗 hello Hive DDL。 如果此失敗，就會發生下列陳述式 isseen hello Hive 錯誤記錄檔中的 hello: </p><p>"錯誤 [main]：ql.Driver (SessionState.java:printError(547)) - 失敗：執行錯誤，從 org.apache.hadoop.hive.ql.exec.DDLTask 傳回代碼 1。 MetaException(message:java.lang.RuntimeException: commitTransaction 已呼叫，但 openTransactionCalls = 0。 這可能表示有不對稱的呼叫 tooopenTransaction/commitTransaction） 」</p></td>
<td>Hive</td>
<td>Hadoop、Hbase</td>
<td>HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。 在此記錄供參考之用。)</td>
</tr>
<tr>
<td>Bug 修正： hello HDInsight 查詢主控台中的不定期停止回應</td>
<td>當發生這種情況時，hello 下列陳述式中可以看到 hello WebHCat 記錄檔中的 hello WebHCat 啟動器作業： <p>「 org.apache.hive.hcatalog.templeton.CatchallExceptionMapper |org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException)： 無法載入記錄檔 {wasb url toohello 歷程記錄檔案}"</p></td>
<td>WebHCat</td>
<td>Hadoop</td>
<td>HIVE-482 (這是內部 JIRA，因此不可在外部加上引號。 在此記錄供參考之用。)</td>
</tr>
<tr>
<td>Bug 修正：Hbase 查詢延遲偶爾激增</td>
<td>如果發生這種情況，使用者將會注意到 3 秒偶爾突然增加 hello 延遲的 Hbase 查詢。 </td>
<td>HDInsight 叢集閘道</td>
<td>HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>HDP JAR 檔案名稱變更</td>
<td>HDI 叢集 3.0 版，那里幾個變更 toohello 內部 JAR 檔案 HDP 所安裝。 jetty-6.1.26.jar 已取代為 jetty-6.1.26.hwx.jar。 jetty-util-6.1.26.jar 已取代為 jetty-util-6.1.26.hwx.jar。 這些變更將套用 tooHadoop，砲象兵，WebHCat 和 Oozie 專案。</td>
<td>Hadoop、Mahout、WebHCat、Oozie</td>
<td>Hadoop、HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>HDInsight 2014/11/21 版本的相關資訊
HDInsight 叢集部署此版本中的 hello 完整版本號碼為：

* HDInsight 2.1.9.382.1169709 (從 2014/11/14 後未變更)
* HDInsight 3.0.5.382.1169709 (從 2014/11/14 後未變更)
* HDInsight 3.1.1.382.1169709 (從 2014/11/14 後未變更)
* HDInsight SDK 1.4.0

這個版本包含下列元件更新 hello:

<table border="1">
<tr><th>Title</th><th>說明</th><th>元件</th><th>叢集類型</th><th>JIRA (如果適用)</th></tr>
<tr>
<td>存取應用程式記錄</td>
<td>能力 tooprogrammatically 列舉您的叢集執行的應用程式和 toodownload 相關的特定應用程式或特定容器的記錄檔 toohelp 偵錯問題的應用程式。</td>
<td>SDK</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>在 IHdInsightClient.DeleteCluster 能力 toospecify 區域名稱 </td>
<td>hello Azure HDInsight SDK 提供 hello 能力 toospecify 地區名稱，使用時**DeleteCluster**。 這可協助客戶不同的區域中都有兩個具有相同名稱的資源，並已無法 toodelete 解除封鎖其中。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>hello **ClusterDetails**物件會傳回**DeploymentID**代表 hello 叢集的唯一識別碼的欄位。 這樣會保證唯一的叢集建立 toobe 嘗試以 hello 相同名稱。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>HDInsight 2014/11/14 版本的相關資訊

HDInsight 叢集部署此版本中的 hello 完整版本號碼為：

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

這個版本包含下列新功能、 元件更新和錯誤修正 hello。

<table border="1">
<tr><th>Title</th><th>說明</th><th>元件</th><th>叢集類型</th><th>JIRA (如果適用)</th></tr>
<tr>
<td>指令碼動作 (預覽)</td>
<td>預覽的 hello 叢集中自訂功能，可修改的 Hadoop 叢集以任意方式使用自訂指令碼。 利用此功能，使用者可以試驗一下，部署專案，您可以從 hello Apache Hadoop 生態系統 tooAzure HDInsight 叢集。 此自訂功能可在所有類型的 HDInsight 叢集上使用，包括 Hadoop、HBase 和 Storm。</td>
<td>新功能</td>
<td>全部</td>
<td>N/A</td>
</tr>
<tr>
<td>為 Azure 網站與儲存體記錄分析先行建置的工作</td>
<td>hello HDInsight 查詢主控台都有支援工作的解決方案，對您的資料，或針對取樣資料入門圖庫。
<p>**在您資料上運作的方案**：<br>
我們建立了一些 hello 最常見的資料分析案例 tooprovide 建立您自己的方案的起始點的作業。 您可以使用您的資料與 hello 作業 toosee 它的運作方式。 接著當您準備好時，使用已學 toocreate hello 預先建立作業之後所建立的解決方案。</p>
<p>**在資料範例上運作的方案**：<br>
深入了解如何藉由查核透過某些基本的情況下 （例如 web 記錄檔和感應器資料分析） 與 HDInsight toowork。 您了解如何 toouse HDInsight tooanalyze 這類資料和連線的其他應用程式和服務 toothis 資料的方式。 視覺化資料，藉由連接 tooMicrosoft Excel 提供的 hello 電源，這種方法的範例。</p></td>
<td>查詢主控台</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Templeton 中的記憶體遺漏修正</td>
<td>已解決 Templeton 中的記憶體流失，該問題會影響已長期執行叢集的客戶，或每秒提交數百次工作要求的客戶。 hello： 認定為 Templeton 5xx 錯誤和 hello 因應措施的問題是 toorestart hello 服務。 不再需要 hello 因應措施。</td>
<td>Templeton</td>
<td>全部</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> 沒有記載 toodemonstrate hello 新功能所提供叢集自訂程序，在叢集上使用指令碼動作 tooinstall Spark 和 R 模組的 hello 程序。 如需詳細資訊，請參閱：

* [在 HDInsight 叢集上安裝和使用 Spark 1.0](hdinsight-hadoop-spark-install.md)
* [在 HDInsight Hadoop 叢集上安裝和使用 R](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>HDInsight 2014/11/07 版本的相關資訊

在此版本部署的 HDInsight 叢集的 hello 完整版本號碼為：

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

這個版本包含下列元件更新 hello:

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
<td>根據預設，已啟用 hello YARN 時間表伺服器 (也稱為 hello 泛型應用程式記錄的伺服器)。 hello 時間表伺服器提供已完成的應用程式 （例如應用程式識別碼、 應用程式名稱、 應用程式狀態、 應用程式送出時間和應用程式完成時間） 的一般資訊。

藉由存取 hello URI http://headnodehost:8188 或是執行 hello YARN 命令，可以從 hello 前端節點擷取此應用程式資訊： yarn 應用程式的清單-appStates 所有。

此資訊也可以透過 REST API 從 https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/ 遠端擷取。

如需詳細資訊，請參閱 <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>。</td>
<td>服務、YARN</td>
<td>Hadoop、HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>叢集部署 ID</td>
<td>從 SDK 1.3.3.1.5426.29232 版開始，使用者可存取 HDInsight 發行給每個叢集的唯一 ID。 此可讓客戶 toofigure，唯一的執行個體的叢集 DNS 名稱在重複使用時建立或卸除的案例。</td>
<td>SDK</td>
<td>全部</td>
<td>N/A</td>
</tr>
</table>

> [!NOTE]
> 防止 hello 完整版本號碼，從顯示 hello 入口網站中，或傳回 hello SDK 或 Windows PowerShell 的 hello bug 已修正在此版本中。

## <a name="notes-for-10152014-release"></a>2014/10/15 版本的相關資訊

此 hotfix 版本中受影響的 Templeton hello 重負荷使用者 Templeton 修正記憶體流失。 在某些情況下，運用 Templeton 大量的使用者會看到錯誤： 在因為 hello 要求不會有足夠的記憶體 toorun 認定為 500 錯誤碼。 此問題的因應措施 hello was toorestart hello Templeton 服務。 已修正此問題。

## <a name="notes-for-1072014-release"></a>2014/10/7 版本的相關資訊

* 當使用 Ambari 端點，「 https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}"，hello *host_name*欄位會傳回hello 完整網域名稱 (FQDN) 的 hello 節點，而不是 hello 主機名稱。 例如，而不是傳回"**headnode0**」，您會收到 hello FQDN"**headnode0。 {ClusterDNS}.azurehdinsight.net**"。 一個虛擬網路中進行此變更，需要的 toofacilitate 案例可以部署多個叢集類型 （例如 HBase 和 Hadoop） 的位置。 例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。

* 我們已提供 hello 預設部署的 hello HDInsight 叢集的新記憶體設定。 先前的預設記憶體設定未充分負責處理 hello 指導 hello 正在部署的 CPU 核心的數目。 根據 Hortonworks 建議，這些新的記憶體設定應該提供更佳的預設值。 toochange 這些項目，請參閱 toohello 變更叢集設定的相關 SDK 參考文件。 hello 新記憶體設定，可供 hello 預設 4 CPU 核心 （8 容器） HDInsight 叢集會分項 hello 下表中。 （hello 用值 toothis 先前版本中也提供併入。）

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

如需 hello YARN 和 MapReduce hello Hortonworks Data Platform 使用 HDInsight 上使用的記憶體組態設定的詳細資訊，請參閱[判斷 HDP 記憶體組態設定](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html)。 Hortonworks 也提供工具 toocalculate 適當的記憶體設定。

關於 hello Azure PowerShell 和 hello HDInsight SDK 的錯誤訊息: 「*叢集未設定為使用 HTTP 服務存取*":

* 這個錯誤是已知[相容性問題](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight)，可能是因為 tooa hello 版的 hello HDInsight SDK 或 Azure PowerShell 和 hello hello 叢集的版本中的差異。 在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。 但是，這項功能不會正確解譯舊版 hello HDInsight SDK 或 Azure PowerShell。 hello 結果是某些工作提交作業失敗。 如果您使用 HDInsight SDK Api 或 Azure PowerShell cmdlet (**使用 AzureRmHDInsightCluster**或**Invoke AzureRmHDInsightHiveJob**) toosubmit 工作，這些作業可能會失敗並 hello 錯誤訊息 」*叢集<clustername>未針對 HTTP 服務存取*。 」 或者 （hello 視作業而定），您可能會收到其他錯誤訊息，例如"*無法連接 toocluster*"。
* Hello 的 hello HDInsight SDK 和 Azure PowerShell 的最新版本中解決這些相容性問題。 我們建議您更新 hello HDInsight SDK tooversion 1.3.1.6 或更新版本以及 Azure PowerShell 工具 tooversion 0.8.8 或更新版本。 您可以取得存取 toohello 從最新的 HDInsight SDK [NugGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) hello Azure PowerShell 工具和[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>HDInsight 3.1 2014/9/12 版本的相關資訊
* 此版本根據 Hortonworks Data Platform (HDP) 2.1.5。 如需此版本中修正的 hello bug 的清單，請參閱 hello[此版本中修正](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html)hello Hortonworks 站台上的頁面。
* Hello"avro-mapred-1.7.4.jar"檔案已在 hello Pig 文件庫資料夾中，變更太"avro-mapred-1.7.4-hadoop2.jar。 」 此檔案的 hello 內容包含次要的 bug 修正非中斷程式。 建議客戶請勿直接相依性的 hello hello 名稱時重新命名檔案的 JAR 檔案 tooavoid 符號。

## <a name="notes-for-8212014-release"></a>2014/8/21 版本的相關資訊
* 我們會加入下列 WebHCat 組態 (HIVE-7155)，設定作業 too1 GB hello Templeton 控制站的預設記憶體限制的 hello。 （hello 先前的預設值為 512 MB）。

     templeton.mapper.memory.mb (=1024)

  * 這項變更位址 hello 下列與特定的 Hive 查詢因為 toolower 記憶體限制的錯誤: 「 容器以外的實體記憶體限制執行 」。
  * toorevert toohello 舊預設值，您可以設定 Azure PowerShell 透過此組態值 too512 在叢集建立期間使用 hello 下列命令：

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* hello 的 hello 動物園管理員角色的主機名稱已變更過*動物園管理員*。 這會影響 hello 叢集內的名稱解析，但它並不會影響外部 REST Api。 如果您的元件，使用 hello *zookeepernode*主機名稱，您需要 tooupdate 它們 toouse 新名稱。 hello hello 三個動物園管理員節點的新名稱是：

  * zookeeper0
  * zookeeper1
  * zookeeper2
* 已更新 HBase 版本支援矩陣。 只有 HBase 工作負載的生產才能支援 HDInsight 3.1 版 (HBase 0.98 版)。 將不再支援 3.0 版(之前可用於預覽)。

## <a name="notes-about-clusters-created-prior-too8152014"></a>叢集的相關注意事項建立先前 too8/15/2014
Azure PowerShell 或 HDInsight SDK 的錯誤訊息，"叢集<clustername>未針對 HTTP 服務的存取權 」 (或根據 hello 作業其他錯誤訊息如: 「 無法連接 toocluster 」) 可能會遇到因為 tooa 版本差異Azure PowerShell 或 hello HDInsight SDK 和一個叢集。 在 8/15 或之後建立的叢集支援佈建到虛擬網路的這項新功能。 Hello Azure PowerShell 或 hello HDInsight SDK，會導致失敗的工作提交作業的舊版本不正確地解譯這項功能。 如果您使用 HDInsight SDK Api 或 Azure PowerShell cmdlet （例如使用 AzureRmHDInsightCluster 或叫用 AzureRmHDInsightHiveJob） toosubmit 工作，這些作業可能會因 hello 錯誤訊息所述的其中一個。

Hello 的 hello HDInsight SDK 和 Azure PowerShell 的最新版本中解決這些相容性問題。 我們建議您更新 hello HDInsight SDK tooversion 1.3.1.6 或更新版本以及 Azure PowerShell 工具 tooversion 0.8.8 或更新版本。 您可以取得存取 toohello 從最新的 HDInsight SDK [NuGet][nuget-link]。 您可以使用來存取 hello Azure PowerShell 工具[Microsoft Web Platform Installer][webpi-link]。

## <a name="notes-for-7282014-release"></a>2014/7/28 版本的相關資訊
* **在新的區域中可用的 HDInsight**： 我們擴大 HDInsight 地理存在 toothree 區域。 HDInsight 客戶可以在這三個區域建立叢集：
  * 東亞
  * 美國中北部
  * 美國中南部
* 正在從 hello Azure 入口網站移除 HDInsight （HDP 1.1 和 Hadoop 1.0.3） 1.6 版和 HDInsight 版本 2.1 （HDP1.3 和 Hadoop 1.2）。 您可以使用這些版本 hello Azure PowerShell cmdlet，持續 toocreate Hadoop 叢集[新增 AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx)或使用 hello [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx)。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md)。
* 此版本中的 Hortonworks Data Platform (HDP) 變更：

<table border="1">
<tr><th>HDP</th><th>變更</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>沒有變更</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>沒有變更</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>2014/6/24 版本的相關資訊
這一版包含增強功能 toohello HDInsight 服務：

* **HDP 2.1 可用性**: HDInsight 3.1 （其中包含 HDP 2.1） 是通常也是 hello 新叢集的預設版本。
* **HBase - Azure 入口網站改進**：我們正使 HBase 叢集可用於預覽版。 您可以從按幾下滑鼠的 hello 入口網站建立 HBase 叢集。

使用 HBase，您可以在 HDInsight 上建立各種不同的即時工作負載從互動使用大型資料集 tooservices 儲存感應器和遙測資料從數百萬個結束點的網站。 hello 下一個步驟就是 tooanalyze hello 資料在 Hadoop 工作進行，這些工作負載，這可能 HDInsight 透過 Azure PowerShell 和 hello Hive 叢集儀表板中。

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout 預先安裝在 HDInsight 3.1
 [砲象兵](http://hortonworks.com/hadoop/mahout/)是預先安裝在 HDInsight 3.1 Hadoop 叢集上，因此您可以執行砲象兵工作而 hello 需要在其他叢集組態。 例如，您可以從遠端存取 Hadoop 叢集使用遠端桌面通訊協定 (RDP)，而不需要額外的步驟，您可以執行下列命令 Hello World 砲象兵的 hello:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

如需此程序的更完整說明，請參閱 hello 文件以 hello [Breiman 範例](https://mahout.apache.org/users/classification/breiman-example.html)hello Apache 砲象兵網站上。

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Hive 查詢可在 HDinsight 3.1 中使用 Tez
Hive 0.13 可在 HDInsight 3.1 中使用，且能夠使用 Tez 來執行查詢，妥善運用可大幅提升效能。
依預設不會對 Hive 查詢啟用 Tez。 toouse，您必須選擇加入。 您可以啟用 Tez 藉由執行下列程式碼片段的 hello:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks 在標準效能評比中，已發表一份關於 Hive 查詢搭配 Tez 而提升效能的詳細數據。 如需詳細資訊，請參閱 [Apache Hive 13 for Enterprise Hadoop 效能評比](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/)(英文)。

如需詳細資訊，請參閱 [Tez 上的 Hive](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)。

### <a name="global-availability"></a>正式上市
與 HDInsight Hadoop 2.2 hello 發行，Microsoft 已做出 HDInsight 可用在所有 Azure 所在的主要地理位置。 具體來說，hello 西歐洲和東南亞資料中心有已上線。 這可讓客戶 toolocate 叢集已關閉的資料中心，以及可能類似的相容性需求的區域中。

### <a name="dos--donts-between-cluster-versions"></a>叢集版本之間的注意事項
**與 HDInsight 3.1 叢集搭配使用的 Oozie 中繼存放區與舊版的 HDInsight 2.1 叢集無法回溯相容，且兩者無法與此舊版本搭配使用**。

與 HDInsight 3.1 叢集一起部署的自訂 Oozie metastore 資料庫，無法在 HDInsight 2.1 叢集上重複使用。 這是 hello 情況下，即使 hello 中繼存放區產生與 HDInsight 2.1 叢集。 不支援這種情況下，因為搭配 HDInsight 3.1 叢集，使它不再與 hello hello HDInsight 2.1 叢集所需的中繼存放區相容時，取得升級 hello 中繼存放區結構描述。 任何嘗試 tooreuse 搭配 HDInsight 3.1 叢集的 Oozie 中繼存放區會呈現無用 hello HDInsight 2.1 叢集。

**叢集之間無法共用 Oozie 中繼存放區。**

Oozie 中繼存放區是附加的 toospecific 群集，而不能在叢集中共用它們。

### <a name="breaking-changes"></a>重大變更
**前置詞語法**： 只有 hello"wasb: / /"HDInsight 3.1 與 3.0 叢集中的支援語法。 較舊的 hello"asv: / /"語法支援 HDInsight 2.1 和 1.6 的叢集，但它不支援 HDInsight 3.1 或 3.0 的叢集。 這表示任何工作提交 tooan HDInsight 3.1 或叢集的明確 3.0，會使用 「 hello 」 asv: / /"語法將會失敗。 hello"wasb: / /"應該改為使用語法。 此外，工作提交 tooany HDInsight 3.1 或 3.0 建立的叢集，其中包含現有中繼存放區與明確參考使用 hello tooresources"asv: / /"語法將會失敗。 這些中繼存放區需要重建使用 hello toobe"wasb: / /"語法 tooaddress 資源。

**連接埠**: hello hello HDInsight 服務所使用的連接埠已變更。 hello 連接埠號碼已使用了 hello Windows 作業系統的 hello 暫時連接埠範圍內。 對於短期的網際網路通訊協定通訊，會自動從預設定義的暫時範圍中配置連接埠。 hello 組新的 Hortonworks Data Platform (HDP) 允許的服務連接埠號碼會發生衝突時的 hello hello 前端節點上執行的服務所使用的連接埠可能會發生此範圍 tooavoid 之外。 hello 新的連接埠號碼，應該不會造成任何重大變更。 如下所示為 hello 所使用的數字：

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
hello 下列相依性中所加入 HDInsight 3.x (HDP2.x):

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

hello 下列相依性不存在於 HDInsight 3.x (HDP2.x):

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
HDInsight 之間所做的下列版本變更的 hello 2.x (HDP1.x) 和 HDInsight 3.x (HDP2.x):

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
hello Java Database Connectivity (JDBC) 驅動程式，適用於 SQL Server HDInsight 內部使用，並不會用於外部作業。 如果您想 tooconnect tooHDInsight 使用開放式資料庫連接 (ODBC) 時，請使用 hello Microsoft Hive ODBC 驅動程式。 如需詳細資訊，請參閱[以 hello Microsoft Hive ODBC 驅動程式連接的 Excel tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md)。

### <a name="bug-fixes"></a>錯誤修正
在此版本中，我們已重新整理 hello 遵循數個 bug 修正的 HDInsight 版本：

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Hortonworks 版本資訊
Hello Hortonworks 資料平台 (HDPs) 版本的 HDInsight 叢集所使用的版本資訊位於下列位置的 hello:

* HDInsight 3.1 版會使用為基礎的 hello Hadoop 散發[Hortonworks Data Platform 2.1.7][hdp-2-1-7]。 這是使用 2014 年 11 月 7 日之後的 hello Azure 入口網站時，建立 hello 預設 Hadoop 叢集。 2014 年 11 月 7 日依據 hello 之前建立的 HDInsight 3.1 叢集[Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight 3.0 版會使用為基礎的 hello Hadoop 散發[Hortonworks 資料平台 2.0][hdp-2-0-8]。
* HDInsight 2.1 版會使用為基礎的 hello Hadoop 散發[Hortonworks 資料平台 1.3][hdp-1-3-0]。
* HDInsight 1.6 版會使用為基礎的 hello Hadoop 散發[Hortonworks 資料平台 1.1][hdp-1-1-0]。

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
