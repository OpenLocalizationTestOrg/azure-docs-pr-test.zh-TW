---
title: "HDInsight 的 Azure 上的 Hadoop 服務所使用的 aaaPorts |Microsoft 文件"
description: "在 HDInsight 上執行的 Hadoop 服務所使用的連接埠清單。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>HDInsight 上 Hadoop 服務所使用的連接埠

本文件提供 hello 以 Linux 為基礎的 HDInsight 叢集上執行的 Hadoop 服務所使用的連接埠清單。 它也提供使用 tooconnect toohello 叢集使用 SSH 連接埠上的資訊。

## <a name="public-ports-vs-non-public-ports"></a>公用連接埠與非公用連接埠

以 Linux 為基礎的 HDInsight 叢集只會公開三個連接埠可公開在 hello 網際網路;22、 23、 和 443。 這些連接埠是使用 SSH 和 hello 安全的 HTTPS 通訊協定透過公開的服務使用的 toosecurely 存取 hello 叢集。

HDInsight 在內部實作由數個 Azure 虛擬機器 （hello 叢集內的 hello 節點） 的 Azure 虛擬網路上執行。 從，您也可以在 hello 虛擬網路內存取連接埠不透過 hello 公開網際網路。 例如，如果您連接的 hello 前端節點使用 SSH tooone，hello 主節點從您可以再直接存取 hello 叢集節點上執行的服務。

> [!IMPORTANT]
> 如果您沒有將 Azure 虛擬網路指定為 HDInsight 的設定選項，則會自動建立一個。 不過，您無法加入其他電腦 （例如其他 Azure 虛擬機器或用戶端開發電腦） toothis 虛擬網路。


toojoin 其他機器 toohello 虛擬網路，您就必須 hello 虛擬網路，請先建立，然後指定它，建立您的 HDInsight 叢集時。 如需詳細資訊，請參閱 [使用 Azure 虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>公用連接埠

HDInsight 叢集中的節點位於 Azure 虛擬網路，而且不能直接從存取的所有都 hello 都 hello 網際網路。 公用閘道提供網際網路存取 toohello 下列連接埠，是通用的 HDInsight 叢集的所有類型。

| 服務 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |連接的用戶端 toosshd hello 主要叢集前端節點上。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。 |
| sshd |22 |SSH |連接的用戶端 toosshd hello 邊緣節點上。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。 |
| sshd |23 |SSH |連接的用戶端 toosshd hello 次要叢集前端節點上。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。 |
| Ambari |443 |HTTPS |Ambari Web UI。 請參閱[管理 HDInsight 使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |Ambari REST API。 請參閱[管理 HDInsight 使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |HCatalog REST API。 請參閱[搭配使用 Hive 與 Curl](hdinsight-hadoop-use-pig-curl.md)、[搭配使用 Pig 與 Curl](hdinsight-hadoop-use-pig-curl.md)、[搭配使用 MapReduce 與 Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |會使用 ODBC tooHive 的連接。 請參閱[hello Microsoft ODBC 驅動程式連接的 Excel tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md)。 |
| HiveServer2 |443 |JDBC |會使用 JDBC tooHive 的連接。 請參閱[tooHive hello Hive JDBC 驅動程式使用的 HDInsight 上的連接](hdinsight-connect-hive-jdbc-driver.md) |

hello 以下是適用於特定的叢集類型：

| 服務 | 連接埠 | 通訊協定 | 叢集類型 | 說明 |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |HBase REST API。 請參閱 [開始使用 HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |Spark REST API。 請參閱 [使用 Livy 從遠端提交 Spark 作業](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Storm Web UI。 請參閱 [部署和管理 HDInsight 上的 Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>驗證

Hello 必須驗證網際網路上公開的所有服務：

| Port | 認證 |
| --- | --- |
| 22 或 23 |在叢集建立期間指定的 hello SSH 使用者認證 |
| 443 |hello 登入名稱 (預設： 系統管理員) 和叢集建立期間所設定的密碼 |

## <a name="non-public-ports"></a>非公用連接埠

> [!NOTE]
> 部分服務只能在特定叢集類型上使用。 例如，HBase 只能在 HBase 叢集類型上使用。

> [!IMPORTANT]
> 某些服務一次只能在一個前端節點上執行。 如果您嘗試在 hello 主要叢集前端節點上的 tooconnect toohello 服務，並傳回 404 錯誤，重試一次使用 hello 次要叢集前端節點。

### <a name="ambari"></a>Ambari

| 服務 | 節點 | Port | URL 路徑 | 通訊協定 | 
| --- | --- | --- | --- | --- |
| Ambari Web UI | 前端節點 | 8080 | / | HTTP |
| Ambari REST API | 前端節點 | 8080 | /api/v1 | HTTP |

範例：

* Ambari REST API：`curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>HDFS 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| NameNode Web UI |前端節點 |30070 |HTTPS |Web UI tooview 狀態 |
| NameNode 中繼資料服務 |前端節點 |8020 |IPC |檔案系統中繼資料 |
| DataNode |所有背景工作節點 |30075 |HTTPS |Web UI tooview 狀態、 記錄檔等。 |
| DataNode |所有背景工作節點 |30010 |&nbsp; |資料傳輸 |
| DataNode |所有背景工作節點 |30020 |IPC |中繼資料作業 |
| 次要 NameNode |前端節點 |50090 |HTTP |NameNode 中繼資料的檢查點 |

### <a name="yarn-ports"></a>YARN 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| Resource Manager |前端節點 |8088 |HTTP |適用於 Resource Manager 的 Web UI |
| Resource Manager |前端節點 |8090 |HTTPS |適用於 Resource Manager 的 Web UI |
| Resource Manager 系統管理介面 |前端節點 |8141 |IPC |適用於應用程式提交 (Hive、Hive 伺服器、Pig 等) |
| Resource Manager 排程器 |前端節點 |8030 |HTTP |系統管理介面 |
| Resource Manager 應用程式介面 |前端節點 |8050 |HTTP |Hello 應用程式管理員 介面的地址 |
| NodeManager |所有背景工作節點 |30050 |&nbsp; |hello 容器管理員 hello 地址 |
| NodeManager Web UI |所有背景工作節點 |30060 |HTTP |Resource Manager 介面 |
| Timeline 位址 |前端節點 |10200 |RPC |hello 時間表 RPC 服務。 |
| Timeline Web UI |前端節點 |8181 |HTTP |hello 時間表服務 web UI |

### <a name="hive-ports"></a>Hive 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| HiveServer2 |前端節點 |10001 |Thrift |服務連接 tooHive (Thrift/JDBC) |
| Hive 中繼存放區 |前端節點 |9083 |Thrift |服務連接 tooHive 中繼資料 (Thrift/JDBC) |

### <a name="webhcat-ports"></a>WebHCat 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| WebHCat 伺服器 |前端節點 |30111 |HTTP |以 HCatalog 和其他 Hadoop 服務為基礎的 Web API |

### <a name="mapreduce-ports"></a>MapReduce 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| JobHistory |前端節點 |19888 |HTTP |MapReduce JobHistory Web UI |
| JobHistory |前端節點 |10020 |&nbsp; |MapReduce JobHistory 伺服器 |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |傳輸中繼對應輸出 toorequesting Reducers |

### <a name="oozie"></a>Oozie

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| Oozie 伺服器 |前端節點 |11000 |HTTP |Oozie 服務的 URL |
| Oozie 伺服器 |前端節點 |11001 |HTTP |Oozie 系統管理的連接埠 |

### <a name="ambari-metrics"></a>Ambari 度量

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| TimeLine (應用程式歷程記錄) |前端節點 |6188 |HTTP |hello 時間表服務 web UI |
| TimeLine (應用程式歷程記錄) |前端節點 |30200 |RPC |hello 時間表服務 web UI |

### <a name="hbase-ports"></a>HBase 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| HMaster |前端節點 |16000 |&nbsp; |&nbsp; |
| HMaster 資訊 Web UI |前端節點 |16010 |HTTP |hello HBase 主版網頁 UI 的 hello 連接埠 |
| 區域伺服器 |所有背景工作節點 |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |用戶端使用 tooconnect tooZooKeeper hello 連接埠 |

### <a name="kafka-ports"></a>Kafka 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | 說明 |
| --- | --- | --- | --- | --- |
| Broker |背景工作節點 |9092 |[Kafka Wire Protocol (Kafka 有線通訊協定)](http://kafka.apache.org/protocol.html) |用於用戶端通訊 |
| &nbsp; |Zookeeper 節點 |2181 |&nbsp; |用戶端使用 tooconnect tooZookeeper hello 連接埠 |

### <a name="spark-ports"></a>Spark 連接埠

| 服務 | 節點 | 連接埠 | 通訊協定 | URL 路徑 | 說明 |
| --- | --- | --- | --- | --- | --- |
| Spark Thrift 伺服器 |前端節點 |10002 |Thrift | &nbsp; | 服務連接 tooSpark SQL (Thrift/JDBC) |
| Livy 伺服器 | 前端節點 | 8998 | HTTP | /batches | 要執行陳述式、作業和應用程式的服務 |

範例：

* Livy：`curl "http://10.0.0.11:8998/batches"`。 在此範例中，`10.0.0.11`是 hello hello 叢集前端節點裝載 hello 晚總服務 IP 位址。
