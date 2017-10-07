---
title: "在 HDInsight 中使用 aaaManage Windows 為基礎的 Hadoop 叢集 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 tooadminister HDInsight 服務。 建立 HDInsight 叢集、 開啟 hello 互動式 JavaScript 主控台與開啟的 hello Hadoop 命令主控台。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>透過 hello Azure 入口網站來管理 HDInsight 中的 Windows 架構的 Hadoop 叢集

使用 hello [Azure 入口網站][azure-portal]，您可以在 Azure HDInsight 中建立 Windows 架構的 Hadoop 叢集變更 Hadoop 使用者的密碼，以及啟用遠端桌面通訊協定 (RDP) 讓您能夠存取 hello Hadoophello 叢集上的命令主控台。

本文章中的 hello 資訊僅適用於 tooWindow 為基礎的 HDInsight 叢集。 如需管理以 Linux 為基礎的叢集資訊，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站](hdinsight-administer-use-portal-linux.md)。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。


## <a name="prerequisites"></a>必要條件

在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **Azure 儲存體帳戶**-HDInsight 叢集會為 hello 預設檔案系統中使用 Azure Blob 儲存體容器。 如需 Azure Blob 儲存體如何提供順暢 HDInsight 叢集使用體驗的詳細資訊，請參閱 [搭配使用 Azure Blob 儲存體與 HDInsight](hdinsight-hadoop-use-blob-storage.md)。 如需有關建立 Azure 儲存體帳戶的詳細資訊，請參閱[如何 tooCreate 儲存體帳戶](../storage/common/storage-create-storage-account.md)。

## <a name="open-hello-portal"></a>開啟 hello 入口網站
1. 登入太[https://portal.azure.com](https://portal.azure.com)。
2. 開啟 hello 入口網站之後，您可以：

   * 按一下**新增**從 hello 左側的功能表 toocreate 新叢集：

       ![新的 HDInsight 叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * 按一下**HDInsight 叢集**hello 左側功能表中。

       ![Azure 入口網站 HDInsight 叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     如果**HDInsight**未出現在 hello 左側功能表中，按一下**瀏覽**。

     ![Azure 入口網站瀏覽叢集按鈕](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>建立叢集
Hello 建立指示使用 hello 入口網站，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

HDInsight 可以與很多 Hadoop 元件搭配使用。 Hello 驗證以及支援 hello 元件清單，請參閱[的 Hadoop 版本是在 Azure HDInsight](hdinsight-component-versioning.md)。 您可以自訂 HDInsight 使用其中一種 hello 下列選項：

* 使用指令碼動作 toorun 自訂指令碼，可以自訂叢集 tooeither 變更叢集設定，或安裝自訂元件，例如 Giraph 或 Solr。 如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md)。
* 在叢集建立期間使用 hello HDInsight.NET SDK 或 Azure PowerShell 中的 hello 叢集自訂參數。 這些組態變更再透過 hello 存留期的 hello 叢集保留，並不會受到 Azure 平台會定期執行維護的叢集節點 reimages。 如需有關使用 hello 叢集自訂參數的詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。
* 某些原生 Java 元件，例如砲象兵和 Cascading，可以當做 JAR 檔案 hello 叢集上執行。 這些 JAR 檔案可以是分散式的 tooAzure Blob 儲存體，並透過 Hadoop 工作提交機制提交 tooHDInsight 叢集。 如需詳細資訊，請參閱 [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。

  > [!NOTE]
  > 如果您有部署 JAR 檔案 tooHDInsight 叢集的問題，或呼叫 JAR 檔案，在 HDInsight 叢集，請連絡[Microsoft 支援服務](https://azure.microsoft.com/support/options/)。
  >
  > Cascading 不受 HDInsight 支援，而且不符合「Microsoft 支援」的資格。 支援的元件清單中，請參閱[hello 叢集版本 HDInsight 所提供的新](hdinsight-component-versioning.md)。
  >
  >

不支援使用遠端桌面連線的 hello 叢集上的自訂軟體安裝。 您應該避免儲存 hello hello 前端節點之後，磁碟機上的任何檔案因為它們將會遺失如果您需要 toore-建立 hello 叢集。 建議您將檔案儲存至 Azure Blob 儲存體。 Blob 儲存體是持續性的。

## <a name="list-and-show-clusters"></a>列出和顯示叢集
1. 登入太[https://portal.azure.com](https://portal.azure.com)。
2. 按一下**HDInsight 叢集**hello 左側功能表中。
3. 按一下 hello 叢集名稱。 如果 hello 叢集清單很長，您可以使用篩選器上 hello hello 頁面的頂端。
4. 按兩下叢集 hello 清單 tooshow hello 詳細資料。

    **功能表和基本功能**：

    ![Azure portal HDInsight cluster essentials](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello 功能表上，hello 功能表上按一下滑鼠右鍵，然後按一下**自訂**。
   * **設定**和**所有設定**： 顯示 hello**設定**刀鋒視窗中的，可讓您 tooaccess hello 叢集組態的詳細資訊 hello 叢集。
   * **儀表板**，**叢集儀表板**和**URL： 這些是所有方法 tooaccess hello 叢集儀表板，也就是 Ambari Web linux 叢集。-**安全殼層 * *: 顯示 hello 指示 tooconnect toohello 叢集使用安全殼層 (SSH) 連線。
   * **調整叢集**： 可讓您對此叢集的背景工作節點 toochange hello 數。
   * **刪除**： 刪除 hello 叢集。
   * **快速啟動**：顯示可協助您開始使用 HDInsight 的資訊。
   * * * 使用者： 可讓您 tooset 權限*入口網站管理*此叢集的其他使用者 Azure 訂用帳戶。

     > [!IMPORTANT]
     > 這*只*影響 hello Azure 入口網站中的存取和權限 toothis 叢集，以及誰可以連線 tooor 送出工作 toohello HDInsight 叢集上沒有作用。
     >
     >
   * **標記**： 標記可讓您 tooset 索引鍵/值組 toodefine 自訂您的雲端服務的分類。 例如，您可建立名為 **project**的索引鍵，然後使用與特定專案相關聯之所有服務的通用值。
   * **Ambari 檢視**： 連結 tooAmbari Web。

     > [!IMPORTANT]
     > toomanage hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。 如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。
     >
     >

     **使用量**：

     ![Azure 入口網站 HDInsight 叢集使用量](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. 按一下 [設定] 。

    ![Azure 入口網站 HDInsight 叢集使用量](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **屬性**： 檢視 hello 叢集內容。
   * **叢集 AAD 身分識別**：
   * **Azure 儲存體金鑰**： 檢視 hello 預設儲存體帳戶和它的索引鍵。 hello 叢集建立程序期間設定 hello 儲存體帳戶。
   * **叢集登入**: hello 叢集 HTTP 使用者名稱和密碼變更。
   * **外部中繼存放區**： 檢視 hello Hive 和 Oozie 中繼存放區。 只能在 hello 叢集建立程序期間設定 hello 中繼存放區。
   * **調整叢集**： 增減 hello 叢集背景工作節點數。
   * **遠端桌面**： 啟用和停用遠端桌面 (RDP) 存取和設定 hello RDP 使用者名稱。  hello RDP 使用者名稱必須不同於 hello HTTP 使用者名稱。
   * **記錄可查夥伴**：

     > [!NOTE]
     > 這是可用設定的泛型清單，並不會針對所有叢集類型顯示所有的可用設定。
     >
     >
6. 按一下 [屬性] ：

    hello 屬性區段會列出 hello 下列：

   * **主機名稱**：叢集名稱。
   * **叢集 URL**。
   * **狀態**：包括Aborted、Accepted、ClusterStorageProvisioned、AzureVMConfiguration、HDInsightConfiguration、Operational、Running、Error、Deleting、Deleted、Timedout、DeleteQueued、DeleteTimedout、DeleteError、PatchQueued、CertRolloverQueued、ResizeQueued、ClusterCustomization
   * **區域**：Azure 位置。 如需支援的 Azure 位置的清單，請參閱 hello**區域**下拉式清單方塊上的[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。
   * **資料已建立**。
   * **作業系統**：**Windows** 或 **Linux**。
   * **類型**：Hadoop、HBase、Storm、Spark。
   * **版本**。 請參閱 [HDInsight 版本](hdinsight-component-versioning.md)
   * **訂用帳戶**︰訂用帳戶名稱。
   * **訂用帳戶識別碼**。
   * **主要資料來源**。 hello Azure Blob 儲存體帳戶做為 hello 預設 Hadoop 檔案系統。
   * **背景工作節點定價層**。
   * **前端節點定價層**。

## <a name="delete-clusters"></a>刪除叢集
刪除叢集時，不會刪除 hello 預設儲存體帳戶或任何連結儲存體帳戶。 您可以使用，以重新建立 hello 叢集 hello 相同的儲存體帳戶和 hello 相同中繼存放區。

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**刪除**從 hello 上方功能表中，然後再遵循 hello 的指示。

另請參閱 [暫停/關閉叢集](#pauseshut-down-clusters)。

## <a name="scale-clusters"></a>調整叢集
hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。

> [!NOTE]
> 只支援使用 HDInsight 3.1.3 版或更高版本的叢集。 如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。  請參閱[列出和顯示叢集](#list-and-show-clusters)。
>
>

hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：

* Hadoop

    您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。 Hello 作業正在進行時，也可以提交新的作業。 使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。

    當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。 這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。 您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。
* HBase

    順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。 完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。 不過，您就可以手動平衡 hello 地區的伺服器登入 hello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    如需有關使用 hello HBase 殼層的詳細資訊，請參閱]
* Storm

    順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。 但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。

    您可以使用兩種方式來完成重新平衡作業：

  * Storm Web UI
  * 命令列介面 (CLI) 工具

    請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。

    hello Storm web UI 是在 hello HDInsight 叢集上使用：

    ![hdinsight storm scale rebalance](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale 叢集**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**設定**從 hello 最上層功能表，然後再按一下**延展叢集**。
4. 輸入 **背景工作節點的數目**。 hello hello 叢集節點數目限制會因 Azure 訂用帳戶而異。 您可以連絡帳務支援 tooincrease hello 限制。  hello 成本資訊將會反映您所做的節點 toohello 數目的 hello 變更。

    ![HDInsight Hadoop HBase Storm Spark scale](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>暫停/關閉叢集
大部分 Hadoop 工作是只會偶爾執行的批次工作。 對於大多數的 Hadoop 叢集有長時間的過 hello 叢集不正進行處理。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。
您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。

有許多方法，您可以程式設計 hello 程序：

* 使用 Azure Data Factory。 請參閱 [Azure HDInsight 連結服務](../data-factory/data-factory-compute-linked-services.md)和[使用 Azure Data Factory 進行轉換和分析](../data-factory/data-factory-data-transformation-activities.md)，以取得隨選和自行定義的 HDInsight 連結服務。
* 使用 Azure PowerShell。  請參閱 [分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)。
* 使用 Azure CLI。 請參閱 [使用 Azure CLI 管理 HDInsight 叢集](hdinsight-administer-use-command-line.md)。
* 使用 HDInsight .NET SDK。 請參閱 [提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。

Hello 定價資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。 請參閱 toodelete hello 入口網站中，從叢集[刪除叢集](#delete-clusters)

## <a name="change-cluster-username"></a>變更叢集使用者名稱
HDInsight 叢集可以有兩個使用者帳戶。 hello 建立程序期間建立的 hello HDInsight 叢集的使用者帳戶。 您也可以建立存取透過 RDP hello 叢集的 RDP 使用者帳戶。 請參閱 [啟用遠端桌面](#connect-to-hdinsight-clusters-by-using-rdp)。

**toochange hello HDInsight 叢集使用者名稱和密碼**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**設定**從 hello 最上層功能表，然後再按一下**叢集登入**。
4. 如果**叢集登入**已啟用，您必須按一下**停用**，然後按一下**啟用**hello 使用者名稱和密碼，您可以變更之前...
5. 變更 hello**叢集登入名稱**及/或 hello**叢集登入密碼**，然後按一下**儲存**。

    ![HDInsight change cluster user username password http user](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>授與/撤銷存取權
HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

預設會授與這些服務的存取權。 您可以撤銷/授與 hello 存取從 hello Azure 入口網站。

> [!NOTE]
> 授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。
>
>

**toogrant/revoke HTTP web 服務存取**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**設定**從 hello 最上層功能表，然後再按一下**叢集登入**。
4. 如果**叢集登入**已啟用，您必須按一下**停用**，然後按一下**啟用**hello 使用者名稱和密碼，您可以變更之前...
5. 如**叢集登入使用者名稱**和**叢集登入密碼**，hello 叢集分別輸入 hello 新的使用者名稱和密碼。
6. 按一下 [儲存] 。

    ![HDInsight grand remove http web service access](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>找不到 hello 預設儲存體帳戶
每個 HDInsight 叢集都有預設的儲存體帳戶。 叢集會顯示在 hello 預設儲存體帳戶，而且其索引鍵**設定**/**屬性**/**Azure 儲存體金鑰**。 請參閱[列出和顯示叢集](#list-and-show-clusters)。

## <a name="find-hello-resource-group"></a>找不到 hello 資源群組
在 hello Azure Resource Manager 模式中，每個 HDInsight 叢集建立 Azure 資源群組。 叢集所屬 tooappears 中的 hello Azure 資源群組：

* hello 叢集清單有**資源群組**資料行。
* 叢集 [基本資料]  磚。  

請參閱 [列出和顯示叢集](#list-and-show-clusters)。

## <a name="open-hdinsight-query-console"></a>開啟 HDInsight 查詢主控台
hello HDInsight 查詢主控台包含下列功能的 hello:

* **Hive 編輯器**：用於提交 Hive 工作的 GUI Web 介面。  請參閱[執行 Hive 查詢使用 hello 查詢主控台](hdinsight-hadoop-use-hive-query-console.md)。

    ![HDInsight portal hive editor](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **工作歷程記錄**：監視 Hadoop 工作。  

    ![HDInsight portal job history](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    按一下**查詢名稱**tooshow hello 詳細資料，包括工作屬性**工作查詢**，和 * * 作業輸出。 您也可以下載 hello 查詢與 hello 輸出 tooyour 工作站。
* **檔案瀏覽器**： 瀏覽 hello 預設儲存體帳戶和 hello 連結儲存體帳戶。

    ![HDInsight portal file browser browse](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    在 hello 螢幕擷取畫面，hello  **<Account>** 類型表示 hello 項目是 Azure 儲存體帳戶。  按一下 hello 帳戶名稱 toobrowse hello 檔案。
* **Hadoop UI**。

    ![HDInsight portal Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    從「Hadoop UI」，您可以瀏覽檔案，並檢查記錄檔。
* **Yarn UI**。

    ![HDInsight portal YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>執行 Hive 查詢
tooran Hive 工作從 hello 入口網站中，按一下**登錄區編輯器**主控台 hello HDInsight 查詢中。 請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

## <a name="monitor-jobs"></a>監視工作
toomonitor 工作，從 hello 入口網站中，按一下**作業歷程記錄**主控台 hello HDInsight 查詢中。 請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

## <a name="browse-files"></a>瀏覽檔案
toobrowse 檔案儲存在 hello 預設儲存體帳戶及 hello 連結儲存體帳戶，請按一下**檔案瀏覽器**主控台 hello HDInsight 查詢中。 請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

您也可以使用 hello**瀏覽檔案系統中 hello**公用程式的 hello **Hadoop UI** hello HDInsight 主控台中。  請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

## <a name="monitor-cluster-usage"></a>監視叢集使用量
hello**使用量**hello HDInsight 叢集刀鋒視窗的區段會顯示 hello 核心可用 tooyour HDInsight，搭配使用的訂用帳戶數目，以及 hello toothis 叢集以及其同時配置的核心數目的相關資訊配置給 hello 此叢集中的節點。 請參閱[列出和顯示叢集](#list-and-show-clusters)。

> [!IMPORTANT]
> toomonitor hello 服務提供 hello HDInsight 叢集，您必須使用 Ambari Web 或 hello Ambari REST API。 如需使用 Ambari 的詳細資訊，請參閱 [使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>開啟 Hadoop UI
toomonitor hello 叢集、 瀏覽 hello 檔案系統，並檢查記錄檔中，按一下**Hadoop UI**主控台 hello HDInsight 查詢中。 請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

## <a name="open-yarn-ui"></a>開啟 Yarn UI
toouse Yarn 使用者介面中，按一下**Yarn UI**主控台 hello HDInsight 查詢中。 請參閱 [開啟 HDInsight 查詢主控台](#open-hdinsight-query-console)。

## <a name="connect-tooclusters-using-rdp"></a>Tooclusters 使用 RDP 的連接
為您提供在其建立 hello 叢集 hello 認證提供 toohello hello 叢集中，但不是 toohello 叢集本身透過遠端桌面服務的存取權。 當您佈建叢集時或叢集佈建完成後，可以開啟遠端桌面存取。 有關建立時啟用遠端桌面的 hello 指示，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

**tooenable 遠端桌面**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**設定**從 hello 最上層功能表，然後再按一下**遠端桌面**。
4. 輸入 到期日、遠端桌面使用者名稱 和 遠端桌面密碼，然後按一下啟用。

    ![HDInsight 啟用停用設定遠端桌面](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    hello 的到期日的預設值是一週。

   > [!NOTE]
   > 您也可以在叢集上使用 hello HDInsight.NET SDK tooenable 遠端桌面。 使用 hello **EnableRdp** hello 下列方式中的 hello HDInsight 用戶端物件上的方法：**用戶端。EnableRdp (clustername、 位置、"rdpuser"、"rdppassword"，DateTime.Now.AddDays(6))**。 同樣地，toodisable 遠端桌面 hello 叢集上的，您可以使用**用戶端。DisableRdp （clustername、 位置）**。 如需這些方法的詳細資訊，請參閱 [HDInsight .NET SDK 參考](http://go.microsoft.com/fwlink/?LinkId=529017)。 這僅適用於在 Windows 上執行的 HDInsight 叢集。
   >
   >

**使用 RDP tooconnect tooa 叢集**

1. 登入 toohello[入口網站][azure-portal]。
2. 按一下**瀏覽所有**從 hello 左窗格中，按一下  **HDInsight 叢集**，按一下叢集名稱。
3. 按一下**設定**從 hello 最上層功能表，然後再按一下**遠端桌面**。
4. 按一下**連接**並遵循 hello 指示。 如果 [連接] 已停用，您必須先加以啟用。 請確定使用 hello 遠端桌面使用者使用者名稱和密碼。  您無法使用 hello 叢集使用者認證。

## <a name="open-hadoop-command-line"></a>開啟 Hadoop 命令列
tooconnect toohello 叢集中，使用遠端桌面和使用 hello Hadoop 命令列，您必須先啟用遠端桌面存取 toohello 叢集 hello 上一節中所述。

**tooopen Hadoop 命令列**

1. Toohello 叢集使用遠端桌面連線。
2. 從 hello 桌面按兩下**Hadoop 命令列**。

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    如需 Hadoop 命令的詳細資訊，請參閱 [Hadoop 命令參考](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)。

在 hello 上一個螢幕擷取畫面，hello 資料夾名稱會有內嵌的 hello Hadoop 版本號碼。 hello 版本號碼可以變更根據的 hello hello 叢集上安裝的 hello Hadoop 元件版本。 您可以使用 Hadoop 環境變數 toorefer toothose 資料夾。 例如：

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何使用的 HDInsight 叢集 toocreate hello 入口網站，和如何 tooopen hello Hadoop 命令列工具。 toolearn 詳細資訊，請參閱下列文章 hello:

* [使用 Azure PowerShell 管理 HDInsight](hdinsight-administer-use-powershell.md)
* [使用 Azure CLI 管理 HDInsight](hdinsight-administer-use-command-line.md)
* [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)
* [開始使用 Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure HDInsight 提供 Hadoop 的什麼版本？](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop 命令列"
