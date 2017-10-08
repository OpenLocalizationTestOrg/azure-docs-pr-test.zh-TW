---
title: "HDInsight 的 Azure 上的 Apache Storm 的 aaaStorm 入門範例 |Microsoft 文件"
description: "深入了解如何 toodo 巨量資料分析，並處理中即時的資料使用 Apache Storm 與 hello storm 入門 HDInsight 上的範例。"
keywords: "storm-starter, apache storm 範例"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>開始使用 Apache Storm 上 HDInsight 使用 hello storm 入門範例

了解如何在使用 HDInsight toouse Apache Storm hello storm 入門範例。

Apache Storm 是一個可處理資料串流的分散式、容錯、即時的運算系統。 在 Storm on Azure HDInsight 中，您可以建立雲端式 Storm 叢集，以執行即時的巨量資料分析。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="prerequisites"></a>必要條件

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

* **熟悉 SSH 和 SCP**。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="create-a-storm-cluster"></a>建立 Storm 叢集

使用下列步驟 toocreate Storm HDInsight 叢集上的 hello:

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增**，**智慧 + 分析**，然後選取**HDInsight**。

    ![建立 HDInsight 叢集](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. 從 hello**基本概念**刀鋒視窗中，輸入下列資訊的 hello:

    * **叢集名稱**: hello hello HDInsight 叢集名稱。
    * **訂用帳戶**： 選取 hello 訂用帳戶 toouse。
    * **叢集登入使用者名稱**和**叢集登入密碼**: hello 登入透過 HTTPS 存取 hello 叢集時。 您使用這些認證 tooaccess 服務，例如 hello Ambari Web UI 或 REST API。
    * **安全殼層 (SSH) 的使用者名稱**: hello 透過 SSH 存取 hello 叢集時使用的登入。 根據預設 hello 密碼是 hello hello 叢集登入密碼相同。
    * **資源群組**: hello 資源群組 toocreate hello 叢集中。
    * **位置**: hello Azure 地區 toocreate hello 叢集中。

    ![選取訂用帳戶](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. 選取**叢集類型**，然後組 hello 遵循值上 hello**叢集設定**刀鋒視窗中：

    * **叢集類型**：Storm

    * **作業系統**：Linux

    * **版本**：Storm 1.1.0 (HDI 3.6)

    * **叢集層**：標準

    最後，使用 hello**選取**按鈕 toosave 設定。

    ![選取叢集類型](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. 選取 hello 叢集類型後，使用 hello__選取__按鈕 tooset hello 叢集類型。 接下來，使用 hello__下一步__按鈕 toofinish 基本組態。

5. 從 hello**儲存體**刀鋒視窗中，選取或建立儲存體帳戶。 如需本文件中的 hello 步驟，hello 預設值，此刀鋒視窗上其他欄位保留 hello。 使用 hello__下一步__按鈕 toosave 存放裝置設定。

    ![設定 hello HDInsight 的儲存體帳戶設定](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. 從 hello**摘要**刀鋒視窗中，檢閱 hello hello 叢集組態。 使用 hello__編輯__連結 toochange 任何不正確的設定。 最後，使用 the__Create__ 按鈕 toocreate hello 叢集。

    ![叢集組態摘要](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > 它可能會佔用 too20 分鐘 toocreate hello 叢集。

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>在 HDInsight 上執行 storm-starter 範例

1. 連線使用 SSH toohello HDInsight 叢集：

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    如果您使用密碼 toosecure SSH 使用者帳戶，則提示的 tooenter 它。 如果您使用公開金鑰，您可能需要使用 hello`-i`參數 toospecify hello 相符的私密金鑰。 例如： `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`。

    如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用下列命令 toostart 範例拓撲 hello:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > 在舊版的 HDInsight，hello 拓撲 hello 類別名稱是`storm.starter.WordCountTopology`而不是`org.apache.storm.starter.WordCountTopology`。

    此命令會啟動在 hello 叢集上，易記名稱為 'wordcount' hello WordCount 拓撲的範例。 它 hello 句子中會隨機產生的句子與計數 hello 發生的每個字。

    > [!NOTE]
    > 提交時您自己的拓撲 toohello 叢集，您必須先將 hello jar 檔案包含之前使用 hello hello 叢集`storm`命令。 使用 hello`scp`命令 toocopy hello 檔案。 例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > hello WordCount 範例中，與其他 storm 入門範例，已包含在叢集上`/usr/hdp/current/storm-client/contrib/storm-starter/`。

如果您有興趣檢視 hello hello storm 入門範例的來源，您可以找到 hello 程式碼在[https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter)。 這個連結是 Storm 1.1.x，隨附於 HDInsight 3.6。 對於其他版本的情況中，使用 hello__分支__按鈕上方的 hello 頁面 tooselect hello Storm 版本不同。

## <a name="monitor-hello-topology"></a>監視 hello 拓樸

hello Storm UI 提供 web 介面，用於執行的拓撲，並包含在您的 HDInsight 叢集。

使用下列步驟 toomonitor hello 拓撲使用 hello Storm UI hello:

1. toodisplay hello Storm UI 中，開啟 web 瀏覽器 toohttps://CLUSTERNAME.azurehdinsight.net/stormui。 取代**CLUSTERNAME**與 hello 叢集的名稱。

    > [!NOTE]
    > 如果使用者名稱和密碼，請詢問 tooprovide，請輸入 hello 叢集系統管理員 （管理員） 和密碼時使用建立 hello 叢集。

2. 在下**拓撲摘要**，選取 hello **wordcount** hello 中的項目**名稱**資料行。 會顯示 hello 拓撲的相關資訊。

    ![包含 storm-starter WordCount 拓樸資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    此頁面提供下列資訊的 hello:

    * **拓樸 stats** -hello 拓撲效能的基本資訊組織成時段。

        > [!NOTE]
        > 選取的特定時間視窗變更 hello 時間視窗 hello 網頁上的其他區段中顯示的資訊。

    * **Spouts** -spouts，包括傳回每個 spout hello 最後一個錯誤的基本資訊。

    * **Bolts** ：bolt 的基本資訊。

    * **拓撲組態**-hello 拓撲組態有關的詳細資訊。

    此頁面也提供可以在 hello 拓撲採取的動作：

    * **啟用** ：繼續處理已停用的拓撲。

    * **停用** ：暫停執行中拓撲。

    * **重新平衡**-調整 hello 拓樸的 hello 平行處理原則。 之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。 重新平衡調整平行處理原則 toocompensate hello 增加/減少編號 hello 叢集中的節點。 如需詳細資訊，請參閱[了解 hello 平行處理原則的 Storm 拓撲](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。

    * **Kill** -hello 指定逾時之後終止 Storm 拓撲。

3. 此頁面上，從選取的項目從 hello **Spouts**或**釘**> 一節。 會顯示 hello 選元件的相關資訊。

    ![包含所選元件相關資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    此頁面會顯示下列資訊的 hello:

    * **Spout 閃電 stats** -hello 元件效能的基本資訊組織成時段。

        > [!NOTE]
        > 選取的特定時間視窗變更 hello 時間視窗 hello 網頁上的其他區段中顯示的資訊。

    * **輸入 stats** （只有閃電）-產生 hello 閃電所耗用的資料之元件的資訊。

    * **輸出統計資料 (Output stats)** ：此 bolt 發出之資料的資訊。

    * **執行程式** ：此元件之執行個體的資訊。

    * **錯誤** ：此元件產生的錯誤。

4. 當您檢視 spout 或閃電 hello 詳細資料，選取的項目從 hello**連接埠**hello 中的資料行**執行程式**區段 tooview hello 元件的特定執行個體的詳細資料。

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    在此範例中，hello word**七個**發生 1493957 的時間。 這個計數會啟動此拓撲後已發現 hello word 的次數。

## <a name="stop-hello-topology"></a>停止 hello 拓樸

傳回 toohello**拓撲摘要**hello 字數統計拓樸，頁面上，然後選取 hello **Kill**按鈕 hello**拓撲動作**> 一節。 出現提示時，輸入 10 hello 秒 toowait 之前停止 hello 拓撲。 Hello 逾時期限之後 hello 拓撲不會再出現當您瀏覽 hello **Storm UI** hello 儀表板的區段。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a id="next"></a>接續步驟

在此 Apache Storm 教學課程中，您學到使用 Storm HDInsight 上的 hello 基本。 接下來，了解如何太[開發 Java 為基礎的拓撲使用 Maven](hdinsight-storm-develop-java-topology.md)。

如果您已經熟悉開發 Java 為基礎的拓撲，而且想 toodeploy 現存的拓撲 tooHDInsight，請參閱[部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)。

如果您是 .NET 開發人員，您可以使用 Visual Studio 建立 C# 或混合式 C#/Java 拓撲。 如需詳細資訊，請參閱 [使用 Visual Studio 的 Hadoop 工具開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

如需可以搭配 Storm HDInsight 上的範例拓撲，請參閱 hello 遵循範例：

* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
