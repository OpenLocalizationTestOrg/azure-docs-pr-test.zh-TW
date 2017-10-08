---
title: "aaaMonitor 和管理 Azure HDInsight 使用 Ambari Web UI |Microsoft 文件"
description: "深入了解如何 toouse Ambari toomonitor 和管理以 Linux 為基礎的 HDInsight 叢集。 在本文件中，您學會如何 toouse hello Ambari Web UI，包含與 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>使用 hello Ambari Web UI 來管理 HDInsight 叢集

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari 簡化 hello 的管理和監視 Hadoop 叢集藉由提供簡單 toouse web UI 和 REST API。 Ambari 包含以 Linux 為基礎的 HDInsight 叢集上，而且是使用的 toomonitor hello 叢集並設定變更。

在本文件中，您學會如何 toouse hello 與 HDInsight 叢集的 Ambari Web UI。

## <a id="whatis"></a>什麼是 Ambari？

[Apache Ambari](http://ambari.apache.org) 提供方便使用的 Web UI，簡化 Hadoop 管理。 您可以使用 Ambari 建立、管理及監視 Hadoop 叢集。 開發人員可以這些功能整合到應用程式使用 hello [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。

與使用 hello Linux 作業系統的 HDInsight 叢集預設會提供 hello Ambari Web UI。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 

## <a name="connectivity"></a>連線能力

hello Ambari Web UI 並用於您的 HDInsight 叢集 HTTPS://CLUSTERNAME.azurehdidnsight.net，在其中**CLUSTERNAME**是 hello 叢集的名稱。

> [!IMPORTANT]
> 連接 tooAmbari HDInsight 上的需要 HTTPS。 出現提示時進行驗證，使用 hello 管理帳戶名稱和密碼建立 hello 叢集時，您提供。

## <a name="ssh-tunnel-proxy"></a>SSH 通道 (Proxy)

Ambari 叢集可以存取直接透過網際網路 hello，而某些連結從 hello Ambari Web UI （例如 toohello JobTracker) 不會公開在 hello 網際網路。 tooaccess 這些服務，您必須建立 SSH 通道。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。

## <a name="ambari-web-ui"></a>Ambari Web UI

當連線 toohello Ambari Web UI，您會使用提示的 tooauthenticate toohello page。 使用 hello 叢集系統管理員使用者 （預設系統管理員） 和您在叢集建立期間使用的密碼。

當 hello 頁面隨即開啟時，請注意在 hello 最上方的 hello 列。 這個列中的 hello 下列資訊和控制項：

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Ambari 標誌**-開啟 hello 儀表板，它可以是使用的 toomonitor hello 叢集。

* **叢集名稱 # ops** -顯示 hello Ambari 作業數目。 選取的 hello 叢集名稱或**# ops**顯示背景作業的清單。

* **# 警示**-顯示警告或重大警示，如果有 hello 叢集。

* **儀表板**-顯示 hello 儀表板。

* **服務**-hello 叢集中的 hello 服務的資訊和組態設定。

* **主機**-hello hello 叢集中節點的資訊和組態設定。

* **警示** - 資訊、警告和重要警示的記錄。

* **系統管理員**-軟體堆疊/服務安裝在 hello 叢集、 服務帳戶資訊，以及 Kerberos 安全性。

* **系統管理員按鈕** - Ambari 管理、使用者設定和登出。

## <a name="monitoring"></a>監視

### <a name="alerts"></a>Alerts

hello 下列清單包含常見 hello 使用 Ambari 警示狀態：

* **確定**
* **警告**
* **重要**
* **未知**

警示以外**確定**導致 hello **# 警示**頂端 hello hello 頁面 toodisplay hello 警示數目的項目。 選取此項目會顯示 hello 警示和狀態。

警示會分成數個預設群組，可檢視從 hello**警示**頁面。

![警示頁面](./media/hdinsight-hadoop-manage-ambari/alerts.png)

您可以使用 hello 管理 hello 群組**動作**功能表，然後選取**管理警示的群組**。

![管理警示群組對話方塊](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

您也可以管理警示的方法，並從 hello 建立警示通知**動作**功能表選取__管理警示通知__。 系統會顯示任何目前的通知。 您也可以從這裡建立通知。 在發生特定警示/嚴重性組合時，便可透過**電子郵件**或 **SNMP** 傳送通知。 例如，您可以傳送 hello 的電子郵件訊息時 hello 警示的任何**YARN 預設**群組設定得**重大**。

![建立警示對話方塊](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

最後，選取__管理警示設定__從 hello__動作__功能表可讓您 tooset hello 警示必須出現次數之前，會傳送通知。 此設定可使用的 tooprevent 暫時性錯誤的通知。

### <a name="cluster"></a>叢集

hello**度量**hello 儀表板 索引標籤包含一系列，可讓您輕鬆 toomonitor hello 狀態，在叢集的一眼 widget。 [ **CPU 使用量**] 等數個 Widget 可在點按後提供其他資訊。

![儀表板與度量](./media/hdinsight-hadoop-manage-ambari/metrics.png)

hello **Heatmaps**  索引標籤會顯示為彩色 heatmaps，從綠色 toored 的度量。

![儀表板與熱圖](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

如需有關 hello 叢集內的 hello 節點的詳細資訊，請選取**主機**。 然後，選取您感興趣的 hello 特定節點。

![主機詳細資料](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>服務

hello**服務**hello 儀表板上的資訊看板提供快速了解 hello hello hello 叢集上執行的服務狀態。 不同的圖示是使用的 tooindicate 狀態或應該採取的動作。 例如，如果服務需要 toobe 回收，會顯示黃色回收符號。

![服務提要欄位](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> 顯示 hello 服務不同 HDInsight 叢集的型別和版本。 此處顯示的 hello 服務可能不同於 hello 服務顯示為您的叢集。

選取服務會更詳細的資訊顯示 hello 服務上。

![服務摘要資訊](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>快速連結

某些服務顯示**快速連結**hello hello 頁頂端的連結。 這可以是使用的 tooaccess 特定服務的 web Ui，例如：

* **作業記錄** - MapReduce 作業記錄。
* **資源管理員** - YARN ResourceManager UI。
* **NameNode** - Hadoop 分散式檔案系統 (HDFS) NameNode UI。
* **Oozie Web UI** - Oozie UI。

選取任何這些連結，則會在瀏覽器中顯示 hello 選取的頁面開啟新索引標籤。

> [!NOTE]
> 選取 hello**快速連結**服務項目可能會傳回 「 找不到伺服器 」 錯誤。 如果您遇到這個錯誤，您就必須使用 SSH 通道，當使用 hello**快速連結**這個服務項目。 如需相關資訊，請參閱[搭配 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)。

## <a name="management"></a>管理

### <a name="ambari-users-groups-and-permissions"></a>Ambari 使用者、群組和權限

使用[已加入網域](hdinsight-domain-joined-introduction.md)的 HDInsight 叢集時，支援處理使用者、群組和權限。 如需使用 hello Ambari 管理 UI 已加入網域的叢集上的資訊，請參閱[管理已加入網域的 HDInsight 叢集](hdinsight-domain-joined-introduction.md)。

> [!WARNING]
> 請勿變更 hello 以 Linux 為基礎的 HDInsight 叢集上的 hello Ambari 監視 (hdinsightwatchdog) 密碼。 變更 hello 密碼符號 hello 能力 toouse 指令碼動作，或執行與您的叢集的調整作業。

### <a name="hosts"></a>主機

hello**主機**頁面會列出 hello 叢集中所有主機。 toomanage 主機，請遵循下列步驟。

![主機頁面](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> 使用 HDInsight 叢集時，請勿新增、解除委任或重新委任主機。

1. 選取您想 toomanage hello 主機。

2. 使用 hello**動作**想 tooperform 功能表 tooselect hello 動作：

   * **啟動所有元件**-hello 主機上都啟動所有元件。

   * **停止所有元件**-hello 主機上都停止所有元件。

   * **重新啟動所有元件**-停止並啟動 hello 主機上的所有元件。

   * **啟動維護模式**-會歸併警示 hello 主機。 如果您執行的動作會產生警示，則應該啟用此模式。 例如，停止和啟動服務。

   * **將維護模式關閉**-傳回 hello 主機 toonormal 警示。

   * **停止**-停駐點 DataNode 或 NodeManagers hello 主機上的。

   * **啟動**-啟動 DataNode 或 NodeManagers hello 主機上的。

   * **重新啟動**-停止或啟動 DataNode 或 NodeManagers hello 主機上的。

   * **解除委任**-從 hello 叢集移除主機。

     > [!NOTE]
     > 請勿在 HDInsight 叢集上使用此動作。

   * **Recommission** -新增先前已解除委任的主機 toohello 叢集。

     > [!NOTE]
     > 請勿在 HDInsight 叢集上使用此動作。

### <a id="service"></a>服務

從 hello**儀表板**或**服務**頁面上，使用 hello**動作**在 hello 服務 toostop hello 清單底部的按鈕，並啟動所有服務。

![服務動作](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> 雖然**加入服務**會列在這個功能表中，不應該使用的 tooadd 服務 toohello HDInsight 叢集。 您應該在叢集佈建期間，使用指令碼動作加入新服務。 如需使用指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

Hello 時**動作**按鈕可以重新啟動所有服務，通常您會想 toostart、 停止或重新都啟動特定的服務。 使用下列步驟 tooperform 動作上的個別服務的 hello:

1. 從 hello**儀表板**或**服務**頁面上，選取服務。

2. 從 hello 頂端 hello**摘要**索引標籤上，使用 hello**服務動作**按鈕並選取 hello 動作 tootake。 這會重新啟動所有節點上的 hello 服務。

    ![服務動作](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Hello 叢集正在執行，請重新啟動某些服務可能會產生警示。 tooavoid 發出警示通知，您可以使用 hello**服務動作**按鈕 tooenable**維護模式**hello 服務，然後再執行 hello 重新啟動。

3. 一旦選取動作，hello **# op**在背景作業發生的 hello 頁面遞增 tooshow hello 最上方的項目。 如果設定 toodisplay，會顯示 hello 背景作業清單。

   > [!NOTE]
   > 如果您啟用**維護模式**hello 服務，請記住 toodisable 它使用 hello**服務動作**按鈕一旦 hello 作業已完成。

tooconfigure 服務時，使用下列步驟的 hello:

1. 從 hello**儀表板**或**服務**頁面上，選取服務。

2. 選取 hello **Configs**  索引標籤 hello 的目前組態會顯示。 同時也會顯示先前組態的清單。

    ![組態](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. 使用 hello 顯示欄位 toomodify hello 組態，然後選取**儲存**。 或選取先前的設定，然後選取**設為現用**tooroll 回 toohello 先前的設定。

## <a name="ambari-views"></a>Ambari 檢視

Ambari 檢視可讓開發人員 tooplug UI 項目到 hello Ambari Web UI 使用 hello [Ambari 檢視 Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views)。 HDInsight 提供下列檢視與 Hadoop 叢集類型的 hello:

* Yarn 佇列管理員： hello 佇列管理員提供的簡單 UI 的檢視和修改 YARN 佇列。

* 登錄區檢視： hello hive 控制檔的檢視可讓您直接從您網頁瀏覽器 toorun Hive 查詢。 您可以儲存查詢、 檢視結果、 將結果儲存 toohello 叢集存放裝置，或下載結果 tooyour 本機系統。 如需有關使用 Hive 檢視的詳細資訊，請參閱 [在 HDInsight 上使用 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md)。

* Tez 檢視： hello Tez 檢視可讓您 toobetter 了解並最佳化作業。 您可以檢視有關 Tez 工作執行方式及使用哪些資源的資訊。
