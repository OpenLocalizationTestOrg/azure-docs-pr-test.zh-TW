---
title: "在 HDInsight 中使用 aaaMonitor Hadoop 叢集 hello Ambari API-Azure |Microsoft 文件"
description: "用於建立、 管理和監視 Hadoop 叢集 hello Apache Ambari 應用程式開發介面。 運算子直覺式的工具和 Api 隱藏 hello 複雜度的 Hadoop。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>監視使用 hello Ambari API HDInsight 中的 Hadoop 叢集
了解使用 Ambari Api toomonitor HDInsight 叢集的方式。

> [!NOTE]
> 本文章中的 hello 資訊主要是 hello 的提供唯讀 Ambari REST API 版本的 Windows 為基礎的 HDInsight 叢集。 對於 Linux 架構的叢集，請參閱 [使用 Ambari 管理 Hadoop 叢集](hdinsight-hadoop-manage-ambari.md)。
> 
> 

## <a name="what-is-ambari"></a>什麼是 Ambari？
[Apache Ambari][ambari-home] 用來佈建、管理和監視 Apache Hadoop 叢集。 它包含的運算子工具的直覺式集合和一組強大的應用程式開發介面中隱藏 hello 複雜度 Hadoop，以簡化 hello 作業的叢集。 如需 hello 應用程式開發介面的詳細資訊，請參閱[Ambari API 參考][ambari-api-reference]。 

HDInsight 目前支援僅 hello Ambari 監視功能。 HDInsight  3.0 及 2.1 版叢集可支援 Ambari API 1.0。 本文涵蓋於 HDInsight 3.1 和 2.1 版叢集上存取 Ambari API。 hello hello 兩個之間的主要差異是，某些 hello 元件已變更的新功能 （例如 hello 作業歷程記錄的伺服器) 的 hello 簡介。 

**必要條件**

開始本教學課程之前，您必須具備下列項目 hello:

* **具有 Azure PowerShell 的工作站**。
* (選擇性) [cURL][curl]。 tooinstall，請參閱[cURL 版本和下載][curl-download]。
  
  > [!NOTE]
  > 何時使用 hello cURL 命令在 Windows 中，使用雙引號標記，而不是 hello 選項值的單一引號括起來。
  > 
  > 
* **Azure HDInsight 叢集**。 如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。 您需要下列資料 toogo hello 教學課程的 hello:
  
  | 叢集屬性 | Azure PowerShell 變數名稱 | 值 | 說明 |
  | --- | --- | --- | --- |
  |   HDInsight 叢集名稱 |$clusterName | |hello 的 HDInsight 叢集的名稱。 |
  |   叢集使用者名稱 |$clusterUsername | |Hello 叢集建立時所指定叢集使用者名稱。 |
  |   叢集密碼 |$clusterPassword | |叢集使用者密碼。 |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>開始使用
有幾種方式 toouse Ambari toomonitor HDInsight 叢集。

**使用 Azure PowerShell**

下列 Azure PowerShell 指令碼的 hello 取得 hello MapReduce 作業追蹤程式資訊*HDInsight 3.5 叢集中。*  hello 主要差異是我們提取從 hello YARN 服務 （而非 MapReduce） 這些詳細資料。

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

下列 PowerShell 指令碼的 hello 取得 hello MapReduce 作業追蹤程式資訊*HDInsight 2.1 叢集中*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

hello 輸出為：

![Jobtracker Output][img-jobtracker-output]

**使用 cURL**

hello 下列範例會取得叢集資訊使用 cURL:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

hello 輸出為：

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

**Hello 2014 年 10 月 8 日發行的**:

當使用 hello Ambari 端點，「 https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}"，hello *host_name*欄位傳回 hello 節點，而不是 hello 主機名稱的 hello 完整的網域名稱 (FQDN)。 之前 hello 2014 年 10 月 8 日發行，此範例只是傳回"**headnode0**"。 之後 hello 2014 年 10 月 8 日版本中，您會收到 hello FQDN"**headnode0。 {ClusterDNS}.azurehdinsight.net**"，hello 先前範例所示。 一個虛擬網路 (VNET) 中進行此變更，需要的 toofacilitate 案例可以部署多個叢集類型 （例如 HBase 和 Hadoop） 的位置。 例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。

## <a name="ambari-monitoring-apis"></a>Ambari 監視 API
hello 下表列出一些 hello 最常見 Ambari 監視 API 呼叫。 如需 hello API 的詳細資訊，請參閱[Ambari API 參考][ambari-api-reference]。

| 監視 API 呼叫 | URI | 說明 |
| --- | --- | --- |
| 取得叢集 |`/api/v1/clusters` | |
| 取得叢集資訊。 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |叢集、服務、主機 |
| 取得服務 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |服務包括：hdfs、mapreduce |
| 取得服務資訊 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| 取得服務元件 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS：namenode、datanodeMapReduce：jobtracker；tasktracker |
| 取得元件資訊 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo、主機元件、度量 |
| 取得主機 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0、workernode0 |
| 取得主機資訊 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| 取得主機元件 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode、resourcemanager |
| 取得主機元件資訊 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles、元件、主機、度量 |
| 取得組態 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |組態類型：core-site、hdfs-site、mapred-site、hive-site |
| 取得組態資訊 |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |組態類型：core-site、hdfs-site、mapred-site、hive-site |

## <a name="next-steps"></a>後續步驟
現在您已經學會如何 toouse Ambari 監視應用程式開發介面呼叫。 toolearn 詳細資訊，請參閱：

* [管理 HDInsight 叢集使用 hello Azure 入口網站][hdinsight-admin-portal]
* [使用 Azure PowerShell 管理 HDInsight 叢集][hdinsight-admin-powershell]
* [使用命令列介面管理 HDInsight 叢集][hdinsight-admin-cli]
* [HDInsight 文件][hdinsight-documentation]
* [開始使用 HDInsight][hdinsight-get-started]

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
