---
title: "aaaAzure HDInsight 疑難排解指南 |Microsoft 文件"
description: "使用 Azure HDInsight 進行 Hadoop 工作負載的疑難排解。 逐步文件會顯示您如何 toouse HDInsight toosolve Hive、 Spark、 YARN、 HBase、 HDFS 及常見問題出現。"
services: hdinsight
author: arijitt
manager: arijitt
layout: LandingPage
ms.assetid: 
ms.service: hdinsight
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing - page
ms.date: 7/06/2017
ms.author: arijitt
ms.openlocfilehash: 6d801389cba738345b36364302c62008b8318018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-by-using-azure-hdinsight"></a>使用 Azure HDInsight 進行疑難排解

| Apache 工作負載 | 最常見問題 |
|---|---|
|![HBase](./media/hdinsight-troubleshoot-guide/HBASE.png)<br>[進行 HBase 的疑難排解](hdinsight-troubleshoot-hbase.md)|<br>[如何執行回報多個未指派區域的 hbck 命令](hdinsight-troubleshoot-hbase.md#how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions)<br><br>[如何修正使用區域指派的 hbck 命令時發生的逾時問題](hdinsight-troubleshoot-hbase.md#how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments)<br><br>[如何在叢集中強制停用 HDFS 安全模式](hdinsight-troubleshoot-hbase.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)<br><br>[如何使用 Apache Phoenix 修正 JDBC 或 sqlline 連線問題](hdinsight-troubleshoot-hbase.md#how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix)<br><br>[什麼情況會讓主要伺服器 toofail toostart](hdinsight-troubleshoot-hbase.md#what-causes-a-master-server-to-fail-to-start)<br><br>[什麼情況導致區域伺服器上的重新啟動失敗](hdinsight-troubleshoot-hbase.md#what-causes-a-restart-failure-on-a-region-server)|
|![HDFS](./media/hdinsight-troubleshoot-guide/HDFS.png)<br>[進行 HDFS 的疑難排解](hdinsight-troubleshoot-hdfs.md)|<br>[如何從叢集內部存取本機 HDFS](hdinsight-troubleshoot-hdfs.md#how-do-i-access-local-hdfs-from-inside-a-cluster)<br><br>[如何在叢集中強制停用 HDFS 安全模式](hdinsight-troubleshoot-hdfs.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)|
|![Hive](./media/hdinsight-troubleshoot-guide/HIVE.png)<br>[進行 HBase 的疑難排解](hdinsight-troubleshoot-hive.md)|<br>[如何匯出 Hive 中繼存放區並匯入另一個叢集](hdinsight-troubleshoot-hive.md#how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster)<br><br>[如何在叢集上尋找 Hive 記錄](hdinsight-troubleshoot-hive.md#how-do-i-locate-hive-logs-on-a-cluster)<br><br>[我要如何啟動 hello 與叢集上的特定組態的登錄區殼層](hdinsight-troubleshoot-hive.md#how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster)<br><br>[如何分析叢集關鍵路徑上的 Tez DAG 資料](hdinsight-troubleshoot-hive.md#how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path)<br><br>[如何從叢集下載 Tez DAG 資料](hdinsight-troubleshoot-hive.md#how-do-i-download-tez-dag-data-from-a-cluster)|
|![Spark](./media/hdinsight-troubleshoot-guide/SPARK.png)<br>[進行 Spark 的疑難排解](hdinsight-troubleshoot-SPARK.md)|<br>[如何使用 Ambari 在叢集上設定 Spark 應用程式](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-ambari-on-clusters)<br><br>[如何使用 Jupyter 筆記本在叢集上設定 Spark 應用程式](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters)<br><br>[如何使用 Livy 在叢集上設定 Spark 應用程式](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-livy-on-clusters)<br><br>[如何使用 spark-submit 在叢集上設定 Spark 應用程式](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters)<br><br>[造成 Spark 應用程式 OutOfMemoryError 例外狀況的原因](hdinsight-troubleshoot-spark.md#what-causes-a-spark-application-outofmemoryerror-exception)|
|![Storm](./media/hdinsight-troubleshoot-guide/STORM.png)<br>[進行 Storm 的疑難排解](hdinsight-troubleshoot-STORM.md)|<br>[如何存取在叢集上的 hello Storm UI](hdinsight-troubleshoot-storm.md#how-do-i-access-the-storm-ui-on-a-cluster)<br><br>[如何在從一個拓撲 tooanother 轉移 Storm 事件中樞 spout 檢查點資訊](hdinsight-troubleshoot-storm.md#how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another)<br><br>[如何找出叢集上的 Storm 二進位檔](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-binaries-on-a-cluster)<br><br>[我要如何判斷 hello Storm 叢集部署拓撲](hdinsight-troubleshoot-storm.md#how-do-i-determine-the-deployment-topology-of-a-storm-cluster)<br><br>[如何找出用於開發的 Storm 事件中樞 Spout 二進位檔](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-event-hub-spout-binaries-for-development)<br><br>[如何找出叢集上的 Storm Log4J 組態檔](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-log4j-configuration-files-on-clusters)|
|![YARN](./media/hdinsight-troubleshoot-guide/YARN.png)<br>[進行 YARN 的疑難排解](hdinsight-troubleshoot-YARN.md)|<br>[如何在叢集上建立新的 YARN 佇列](hdinsight-troubleshoot-yarn.md#how-do-i-create-a-new-yarn-queue-on-a-cluster)<br><br>[如何下載叢集的 YARN 記錄](hdinsight-troubleshoot-yarn.md#how-do-i-download-yarn-logs-from-a-cluster)|

## <a name="hdinsight-troubleshooting-resources"></a>HDInsight 疑難排解資源

| 如需下列資訊 | 請參閱以下文章 |
| --- | --- |
| Linux 上的 HDInsight 與最佳化 | - [在 Linux 上使用 HDInsight 的相關資訊](hdinsight-hadoop-linux-information.md)<br>- [Hadoop 記憶體和效能疑難排解](hdinsight-hadoop-stack-trace-error-messages.md)<br>- [Hive 查詢效能](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/) |
| 記錄和傾印 | - [存取 Linux 上的 YARN 應用程式記錄](hdinsight-hadoop-access-yarn-app-logs-linux.md)<br>- [啟用適用於 Linux 上的 Hadoop 服務進行的堆積傾印](hdinsight-hadoop-collect-debug-heap-dump-linux.md)<br>- [分析 HDInsight 記錄檔](hdinsight-debug-jobs.md)|
| Errors | - [了解並解決 WebHCat 錯誤](hdinsight-hadoop-templeton-webhcat-debug-errors.md)<br>- [設定 toofix OutofMemory 錯誤 hive 控制檔](hdinsight-hadoop-hive-out-of-memory-error-oom.md) |
| 工具 | - [使用 Ambari 檢視 toodebug Tez 作業](hdinsight-debug-ambari-tez-view.md)<br>- [最佳化 Hive 查詢](hdinsight-hadoop-optimize-hive-query.md) |
