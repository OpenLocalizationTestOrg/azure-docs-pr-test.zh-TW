---
title: "使用 Azure HDInsight 的 Hive aaaTroubleshoot |Microsoft 文件"
description: "取得解答 toocommon 疑問使用 Apache Hive 與 Azure HDInsight。"
keywords: "Azure HDInsight, Hive, 常見問題集, 疑難排解指南, 常見問題"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>使用 Azure HDInsight 為 Hive 進行疑難排解

Apache Hive 承載 Apache Ambari 中工作時，了解 hello 頂端的問題和其解決方式。


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>如何匯出 Hive 中繼存放區並匯入另一個叢集


### <a name="resolution-steps"></a>解決步驟

1. 使用安全殼層 (SSH) 用戶端連接 toohello HDInsight 叢集。 如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。

2. 執行下列命令，在要從中 tooexport hello 中繼存放區的 hello HDInsight 叢集上的 hello:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  此命令會產生名為 allatables.sql 的檔案。

3. 複製 hello 檔案 alltables.sql toohello 新的 HDInsight 叢集，並執行下列命令的 hello:

  ```apache
  hive -f alltables.sql
  ```

hello hello 解決步驟中的程式碼會假設的資料 hello 新叢集的路徑，為 hello hello 舊叢集上的資料路徑 hello 相同。 如果 hello 資料路徑不同，您可以手動編輯產生的 hello alltables.sql 檔案 tooreflect 的任何變更。

### <a name="additional-reading"></a>其他閱讀資料

- [透過 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>如何在叢集上尋找 Hive 記錄

### <a name="resolution-steps"></a>解決步驟

1. 使用 SSH 連線 toohello HDInsight 叢集。 如需詳細資訊，請參閱**其他閱讀資料**。

2. tooview Hive 用戶端記錄檔，請使用下列命令的 hello:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. tooview Hive 中繼存放區記錄檔，會使用下列命令的 hello:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver 記錄檔，會使用下列命令的 hello:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>其他閱讀資料

- [透過 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>我要如何啟動 hello 與叢集上的特定組態的登錄區殼層

### <a name="resolution-steps"></a>解決步驟

1. 當您啟動 hello Hive 殼層，請指定組態機碼值組。 如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist Hive shell 之上，使用 hello 遵循所有有效的組態命令：

  ```apache
  hive> set;
  ```

  例如，使用偵錯記錄在 hello 主控台上啟用具備下列命令 toostart Hive 殼層 hello:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>其他閱讀資料

- [Hive 設定屬性](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>如何分析叢集關鍵路徑上的 Tez DAG 資料


### <a name="resolution-steps"></a>解決步驟
 
1. tooanalyze Apache Tez 導向非循環圖 (DAG) 關鍵叢集的圖形上，透過 SSH 連線 toohello HDInsight 叢集。 如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。

2. 在命令提示字元執行下列命令的 hello:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist 可以是使用的 tooanalyze Tez DAG 其他分析器使用 hello 下列命令：

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  您必須提供範例程式為 hello 第一個引數。

  有效的程式名稱包括：
    - **ContainerReuseAnalyzer**：列印 DAG 中的容器重複使用詳細資料
    - **CriticalPath**： 尋找 DAG 的 hello 關鍵路徑
    - **LocalityAnalyzer**：列印 DAG 中的位置詳細資料
    - **ShuffleTimeAnalyzer**： 分析在 DAG 中的 hello 隨機播放時間詳細資料
    - **SkewAnalyzer**： 分析 DAG 中的 hello 誤差詳細資料
    - **SlowNodeAnalyzer**：列印 DAG 中的節點詳細資料
    - **SlowTaskIdentifier**：列印 DAG 中的低速工作詳細資料
    - **SlowestVertexAnalyzer**：列印 DAG 中最慢頂點詳細資料
    - **SpillAnalyzer**：列印 DAG 中的溢出詳細資料
    - **TaskConcurrencyAnalyzer**： 列印在 DAG 中的 hello 工作並行詳細資料
    - **VertexLevelCriticalPathAnalyzer**： 尋找 hello 關鍵路徑中 DAG 的頂點層級


### <a name="additional-reading"></a>其他閱讀資料

- [透過 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>如何從叢集下載 Tez DAG 資料


#### <a name="resolution-steps"></a>解決步驟

有兩種方式 toocollect hello Tez DAG 資料：

- 從 hello 命令列：
 
    使用 SSH 連線 toohello HDInsight 叢集。 在 hello 命令提示字元中執行下列命令的 hello:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- 使用 hello Ambari Tez 檢視：
   
  1. 移 tooAmbari。 
  2. 移 tooTez 檢視 （在 hello 右上角中的 hello 磚圖示）。 
  3. 選取您想要 tooview DAG hello。
  4. 選取 [下載資料]。

### <a name="additional-reading-end"></a>其他閱讀資料

[透過 SSH 連線 tooan HDInsight 叢集](hdinsight-hadoop-linux-use-ssh-unix.md)






