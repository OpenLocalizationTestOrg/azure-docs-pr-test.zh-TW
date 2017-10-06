---
title: "aaaDeploy 和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲 |Microsoft 文件"
description: "了解 toodeploy、 監視和管理 Apache Storm 拓撲以 Linux 為基礎的 HDInsight 上使用 hello Storm 儀表板的方式。 使用適用於 Visual Studio 的 Hadoop 工具。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>部署和管理 HDInsight 上的 Apache Storm 拓撲

在本文件中，了解 hello 的管理和監視 Storm 拓撲 Storm HDInsight 叢集上執行的基本概念。

> [!IMPORTANT]
> hello 本文章中的步驟需要以 Linux 為基礎的 Storm HDInsight 叢集上。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 
>
> 如需部署和監視以 Windows 為基礎的 HDInsight 上的拓撲的詳細資訊，請參閱 [部署和管理以 Windows 為基礎的 HDInsight 上的Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>必要條件

* **HDInsight 叢集上以 Linux 為基礎的 Storm**：請參閱 [開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) 以取得建立叢集的步驟

* (選擇性) **熟悉 SSH 和 SCP**︰如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

* （選擇性）**Visual Studio**: Azure SDK 2.5.1 或更新版本和 hello Data Lake Tools for Visual Studio。 如需詳細資訊，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

    下列版本的 Visual Studio 中的 hello 其中一項：

  * Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (任何版本)

  * Visual Studio 2017 (任何版本)。 資料湖 Tools for Visual Studio 2017 hello Azure 工作負載的一部分安裝。

## <a name="submit-a-topology-visual-studio"></a>提交拓撲︰Visual Studio

hello HDInsight 工具可以使用的 toosubmit C# 或混合式拓撲 tooyour Storm 叢集。 下列步驟的 hello 使用範例應用程式。 如需使用 hello HDInsight Tools 來建立您自己的拓撲資訊，請參閱[開發 C# 拓撲使用 hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

1. 如果您在 Visual studio 並不安裝 hello hello Data Lake 工具最新版本，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

    > [!NOTE]
    > hello 資料湖 Tools for Visual Studio 之前呼叫了 hello HDInsight Tools for Visual Studio。
    >
    > 資料湖 Tools for Visual Studio 隨附的 hello __Azure 工作負載__for Visual Studio 2017。

2. 開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。

3. 在 hello**新專案**對話方塊方塊中，展開 **已安裝** > **範本**，然後選取**HDInsight**。 從範本 hello 清單，選取**Storm 範例**。 在 hello hello 對話方塊下方，輸入 hello 應用程式的名稱。

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。

   > [!NOTE]
   > 如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。 如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。

5. 選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。 您可以監視是否 hello 提交成功使用 hello**輸出**視窗。

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>提交拓撲： SSH 和 hello Storm 命令

1. 使用 SSH tooconnect toohello HDInsight 叢集。 取代**USERNAME** hello SSH 登入名稱。 將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    如需有關使用 SSH tooconnect tooyour HDInsight 叢集，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用下列命令 toostart 範例拓撲 hello:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    此命令會啟動 hello WordCount 拓撲範例 hello 叢集上。 此拓撲隨機產生的句子與每個字的計數 hello 發生 hello 句子。

   > [!NOTE]
   > 提交時拓撲 toohello 叢集，您必須先將 hello jar 檔案包含之前使用 hello hello 叢集`storm`命令。 toocopy hello 檔案 toohello 叢集，您可以使用 hello`scp`命令。 例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > hello WordCount 範例中，與其他 storm 入門範例，已包含在叢集上`/usr/hdp/current/storm-client/contrib/storm-starter/`。

## <a name="submit-a-topology-programmatically"></a>提交拓撲︰以程式設計的方式

您可以與 hello Nimbus 叢集中裝載的服務進行通訊，以程式設計方式部署拓撲 tooStorm HDInsight 上。 [https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology)提供範例示範的 Java 應用程式如何 toodeploy 並開始透過 hello Nimbus 服務拓撲。

## <a name="monitor-and-manage-visual-studio"></a>監視和管理︰Visual Studio

當您已成功提交拓撲，但是使用 Visual Studio 時，hello **Storm 拓撲**檢視會顯示 hello 叢集。 從 hello 列出 tooview hello 執行拓撲的相關資訊，請選取 hello 拓撲。

![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> 您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。

Hello spouts 或釘 tooview 這些元件的資訊，請選取 hello 圖形。 隨即會針對每個選取的項目開啟新的視窗。

### <a name="deactivate-and-reactivate"></a>停用和重新啟動

停用拓撲會暫停它，直到刪除或重新啟動。 tooperform 這些作業，使用 hello__停用__和__重新啟用__按鈕上方的 hello hello__拓撲摘要__。

### <a name="rebalance"></a>重新平衡

重新平衡的拓撲，可讓 hello 系統 toorevise hello 平行處理原則的 hello 拓撲。 例如，如果您已調整大小 hello 叢集 tooadd 詳細資訊，重新平衡可讓拓樸 toosee hello 新節點。

toorebalance 拓撲中，使用 hello__重新平衡__按鈕上方的 hello hello__拓撲摘要__。

> [!WARNING]
> 第一次重新平衡拓撲 hello 拓撲，就會停用再重新工作者平均分配 hello 叢集中，然後最後會傳回 hello 拓撲 toohello 狀態重新平衡發生之前。 因此如果 hello 拓撲是作用中，它再次變成作用中。 如果已停用，它就會保持停用。

### <a name="kill-a-topology"></a>終止拓撲

Storm 拓撲會繼續執行，直到已停止或刪除 hello 叢集。 toostop 拓撲中，使用 hello __Kill__按鈕上方的 hello hello__拓撲摘要__。

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>監視和管理： SSH 和 hello Storm 命令

hello`storm`公用程式可讓您從 hello 命令列執行拓樸 toowork。 使用 `storm -h` 以取得完整的命令清單。

### <a name="list-topologies"></a>列出拓撲

使用下列命令 toolist hello 所有正在執行的拓撲：

    storm list

此命令會傳回資訊的類似 toohello 下列文字：

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>停用和重新啟動

停用拓撲會暫停它，直到刪除或重新啟動。 使用下列命令 toodeactivate hello，並重新啟動：

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>刪除執行中拓撲

Storm 拓撲一旦啟動之後，就會繼續執行直到停止。 toostop 拓撲中，使用下列命令的 hello:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>重新平衡

重新平衡的拓撲，可讓 hello 系統 toorevise hello 平行處理原則的 hello 拓撲。 例如，如果您已調整大小 hello 叢集 tooadd 詳細資訊，重新平衡可讓拓樸 toosee hello 新節點。

> [!WARNING]
> 第一次重新平衡拓撲 hello 拓撲，就會停用再重新工作者平均分配 hello 叢集中，然後最後會傳回 hello 拓撲 toohello 狀態重新平衡發生之前。 因此如果 hello 拓撲是作用中，它再次變成作用中。 如果已停用，它就會保持停用。

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>監視和管理︰Storm UI

hello Storm UI 提供 web 介面，用於執行的拓撲，並包含在您的 HDInsight 叢集。 tooview hello Storm UI，使用 web 瀏覽器 tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**，其中**CLUSTERNAME**是 hello 叢集的名稱。

> [!NOTE]
> 如果使用者名稱和密碼，請詢問 tooprovide，請輸入 hello 叢集系統管理員 （管理員） 和密碼時使用建立 hello 叢集。

### <a name="main-page"></a>主頁面

hello Storm UI hello 主頁面上提供下列資訊的 hello:

* **叢集摘要**: hello Storm 叢集的基本資訊。
* **拓撲摘要**：執行中拓撲的清單。 使用有關特定拓撲中這個區段 tooview hello 連結的詳細資訊。
* **摘要的監督員**: hello Storm 監督者的相關資訊。
* **Nimbus 組態**: Nimbus hello 叢集組態。

### <a name="topology-summary"></a>拓撲摘要

選取連結從 hello**拓撲摘要**區段會顯示 hello 下列 hello 拓撲的相關資訊：

* **摘要的拓樸**: hello 拓撲的相關基本資訊。
* **拓樸動作**: hello 拓撲，您可以執行管理動作。

  * **啟用**：繼續處理已停用的拓撲。
  * **停用**：暫停執行中的拓撲。
  * **重新平衡**： 調整 hello 拓樸的 hello 平行處理原則。 之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。 這項作業允許 hello 拓撲 tooadjust 平行處理原則 toocompensate hello 增加或減少 hello 叢集中的節點數目。

    如需詳細資訊，請參閱<a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">了解 hello 平行處理原則的 Storm 拓撲</a>。
  * **Kill**: hello 指定逾時之後終止 Storm 拓撲。
* **拓樸 stats**: hello 拓撲的相關統計資料。 tooset hello hello 剩餘項目在 hello 頁面上的時間範圍，請使用 hello hello 連結**視窗**資料行。
* **Spouts**: hello spouts hello 拓撲所使用。 使用此區段 tooview 中的 hello 連結特定 spouts 的詳細資訊。
* **釘**: hello hello 拓撲所使用的攻擊。 使用此區段 tooview 中的 hello 連結特定攻擊的詳細資訊。
* **拓撲組態**: hello 選取拓撲的 hello 設定。

### <a name="spout-and-bolt-summary"></a>Spout 和 Bolt 摘要

選取從 hello spout **Spouts**或**釘**區段會顯示 hello 遵循 hello 選取項目的資訊：

* **元件摘要**: hello spout 或閃電的基本資訊。
* **Spout 閃電 stats**: hello 相關統計資料 spout 或閃電。 tooset hello hello 剩餘項目在 hello 頁面上的時間範圍，請使用 hello hello 連結**視窗**資料行。
* **輸入 stats** （只有閃電）： hello 的相關資訊輸入 hello 閃電所耗用的資料流。
* **輸出 stats**: spout 或閃電關於發出由此 hello 資料流的資訊。
* **執行程式**: hello spout 或閃電 hello 執行個體的相關資訊。 選取 hello**連接埠**這個執行個體所產生的項目特定的執行程式 tooview 診斷資訊的記錄檔。
* **錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。

## <a name="monitor-and-manage-rest-api"></a>監視和管理︰REST API

hello REST API，乃是建立 hello Storm UI，讓您可以執行類似的管理和監視功能，可使用 hello REST API。 您可以使用 hello REST API toocreate 自訂工具來管理和監視 Storm 拓撲。

如需詳細資訊，請參閱 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)。 hello 下列資訊為特定 toousing hello 與 HDInsight 上的 Apache Storm 的 REST API。

> [!IMPORTANT]
> hello Storm REST API 未公開超過 hello 網際網路，而且必須使用 SSH 通道 toohello HDInsight 叢集前端節點存取。 如需建立及使用 SSH 通道，請參閱[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](hdinsight-linux-ambari-ssh-tunnel.md)。

### <a name="base-uri"></a>基底 URI

hello hello REST API 以 Linux 為基礎的 HDInsight 叢集上的基底 URI 可在 hello 前端節點上**https://HEADNODEFQDN:8744/api/v1/**。 hello hello 前端節點的網域名稱在叢集建立期間產生，並不是靜態。

您可以數種不同方式找到 hello 叢集前端節點的 hello 完整的網域名稱 (FQDN):

* **從的 SSH 工作階段**： 使用 hello 命令`headnode -f`從 SSH 工作階段 toohello 叢集中。
* **從 Ambari Web**： 選取**服務**從 hello hello 頁面頂端，然後選取**Storm**。 從 hello**摘要**索引標籤上，選取**Storm UI 伺服器**。 hello hello Storm UI 和 REST API 執行的 hello 節點的 FQDN 是在 hello hello 頁面最上方。
* **Ambari REST API 從**： 使用 hello 命令`curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"`tooretrieve 資訊 hello Storm UI 和 REST API 的 hello 節點上執行。 取代**密碼**hello hello 叢集系統管理員密碼。 取代**CLUSTERNAME**與 hello 叢集名稱。 在 hello 回應 hello"host_name"項目會包含 hello hello 節點的 FQDN。

### <a name="authentication"></a>驗證

必須使用 REST API 的要求 toohello**基本驗證**，所以您可以使用 hello HDInsight 叢集系統管理員名稱和密碼。

> [!NOTE]
> 因為基本驗證會使用純文字傳送，您應該**一律**hello 叢集中使用 HTTPS toosecure 通訊。

### <a name="return-values"></a>傳回值

只能從 hello 叢集內可使用 REST API 或虛擬機器上 hello 與 hello 叢集相同 Azure 虛擬網路從 hello 傳回的資訊。 例如，傳回的動物園管理員伺服器 hello 完整的網域名稱 (FQDN) 是無法從 hello 網際網路存取。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何使用 toodeploy 和監視器的拓樸 hello Storm 儀表板，了解如何太[開發 Java 為基礎的拓撲使用 Maven](hdinsight-storm-develop-java-topology.md)。

若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。
