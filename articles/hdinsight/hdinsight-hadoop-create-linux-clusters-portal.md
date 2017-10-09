---
title: "使用網頁瀏覽器-Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何 toocreate Hadoop、 HBase、 風暴或 Spark 叢集在 Linux 上使用網頁瀏覽器的 hdinsight 和 hello Azure preview 入口網站。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>HDInsight 使用 hello Azure 入口網站中建立以 Linux 為基礎的叢集
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

hello Azure 入口網站是服務和資源 hello Microsoft Azure 雲端中裝載的網頁型管理工具。 本文中，您將學習如何 toocreate 以 Linux 為基礎的 HDInsight 叢集使用 hello 入口網站。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **現代 Web 瀏覽器**。 hello Azure 入口網站會使用 HTML5 和 Javascript，並可能無法正確執行較舊的網頁瀏覽器中。

## <a name="create-clusters"></a>建立叢集
hello Azure 入口網站會公開大部分的 hello 叢集內容。 使用 Azure Resource Manager 範本，您可以隱藏許多詳細資料。 如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本在 HDInsight 中建立 Linux 型的 Hadoop 叢集](hdinsight-hadoop-create-linux-clusters-arm-templates.md)。

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 依序按一下 [+]、[智慧 + 分析] 及 [HDInsight]。
   
    ![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "hello Azure 入口網站中建立新的叢集")

3. 在 hello **HDInsight**刀鋒視窗中，按一下**（大小、 設定、 應用程式） 的自訂**，按一下**基本概念**，然後輸入下列資訊的 hello。

    ![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "hello Azure 入口網站中建立新的叢集")

    * 輸入 **叢集名稱**：此名稱必須是全域唯一的。

    * 從 hello**訂用帳戶**下拉式清單中，選取 hello hello 叢集將使用的 Azure 訂用帳戶。

    * 按一下 [叢集類型]，然後選取：
   
        * **叢集類型**： 如果您不知道哪些 toochoose，選取**Hadoop**。 它是 hello 最受歡迎的叢集類型。
     
            > [!IMPORTANT]
            > HDInsight 叢集有各種不同的類型，對應 toohello 工作負載或調整為 hello 叢集的技術。 沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。 
            > 
            > 
        
        * **作業系統**：選取 [Linux]。
        
        * **版本**： 如果您不知道哪些 toochoose 使用 hello 預設版本。 如需詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。
        * **叢集層**: Azure HDInsight 提供 hello 巨量資料雲端供應項目兩種類型： 標準層和 Premium 層。 如需詳細資訊，請參閱 [叢集層](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)。

    * 如**叢集登入使用者名稱**和**叢集登入密碼**，提供 hello 使用者名稱和密碼 hello 系統管理使用者。

    * 輸入**SSH 使用者名稱**，如果您想 toohave hello SSH 密碼相同 hello 您稍早指定的系統管理員密碼，請選取 hello**使用與叢集登入相同的密碼**核取方塊。 如果沒有，請提供**密碼**或**公開金鑰**，這將會使用的 tooauthenticate hello SSH 使用者。 使用公開金鑰為 hello 建議的方法。 按一下**選取**在 hello 底部 toosave hello 認證組態。
   
        如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

    * 如**資源群組**，指定是否要 toocreate 新的資源群組，或使用現有。

    * 指定的資料中心**位置**hello 叢集將會建立。

    * 按一下 [下一步] 。

4. 在 hello**儲存體**刀鋒視窗中，指定您是要為您的預設儲存體 Azure 儲存體 (WASB) 還是資料湖存放區。 查看 hello 下表中的詳細資訊。

    ![在 hello Azure 入口網站中建立新的叢集](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "hello Azure 入口網站中建立新的叢集")

    | 儲存體                                      | 說明 |
    |----------------------------------------------|-------------|
    | **Azure 儲存體 Blob 做為預設儲存體**   | <ul><li>對於 [主要儲存體類型]，請選取 [Azure 儲存體]。 在這之後，如**選取方法**，您可以選擇**我的訂閱**如果您想 toospecify 屬於您的 Azure 訂用帳戶的儲存體帳戶，然後選取 hello 儲存體帳戶。 否則，請按一下**便捷鍵**，並提供 hello hello 的 toochoose 從您的 Azure 訂用帳戶以外的儲存體帳戶的資訊。</li><li>如**預設容器**，您可以選擇 toogo hello hello 入口網站所建議的預設容器名稱，或指定您自己。</li><li>如果您使用 WASB 作為預設儲存體，您可以 （選擇性） 按一下 **額外的儲存體帳戶**toospecify 額外的儲存體帳戶與 hello 叢集 tooassociate。 在 hello **Azure 儲存體金鑰**刀鋒視窗中，按一下 **新增儲存體金鑰**，然後您可以提供儲存體帳戶從您的 Azure 訂用帳戶或其他訂用帳戶 （藉由提供 hello 儲存體帳戶便捷鍵）。</li><li>如果您使用 WASB 作為預設儲存體，您可以 （選擇性） 按一下 **資料湖存放區存取**toospecify 做為額外的儲存體的 Azure 資料湖存放區。 如需詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</li></ul> |
    | **Azure Data Lake Store 做為預設儲存體** | 如**主要儲存體類型**，選取**Data Lake Store**然後再參閱 toohello 文章[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)的取得指示。 |
    | **外部中繼存放區**                      | 您可以選擇性地指定 SQL 資料庫 toosave Hive 和 Oozie 中繼資料與 hello 叢集相關聯。 如**SQL database 選取的登錄區**選取 SQL 資料庫，然後再提供 hello 資料庫 hello 使用者名稱/密碼。 對 Oozie 中繼資料重複這些步驟。<br><br>針對中繼存放區使用 Azure SQL 資料庫時的一些考量。 <ul><li>hello Azure SQL database 用於 hello 中繼存放區必須允許 Azure 服務，包括 Azure HDInsight 連線 tooother。 在 hello Azure SQL database 儀表板，在 hello 右邊，按一下 hello 伺服器名稱。 這是 hello 伺服器正在執行哪些 hello SQL 資料庫執行個體。 當您在 hello 伺服器檢視，請按一下**設定**，然後**Azure 服務**，按一下**是**，然後按一下**儲存**。</li><li>在建立時的中繼存放區，請勿使用資料庫名稱包含破折號或連字號，這可能會導致 hello 叢集建立程序 toofail。</li></ul>                                                                                                                                                                       |

    按一下 [下一步] 。 

    > [!WARNING]
    > 不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。

5. （選擇性） 按一下**應用程式**tooinstall 應用程式使用的 HDInsight 叢集。 Microsoft 獨立軟體廠商 (ISV) 或您可以自己開發這些應用程式。 如需詳細資訊，請參閱[安裝 HDInsight 應用程式](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)。


6. 按一下**叢集大小**toodisplay hello 節點將會建立此叢集的資訊。 設定 hello hello 叢集所需的背景工作節點數。 hello 估計成本的 hello 叢集將會顯示 hello 刀鋒視窗中。
   
    ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "指定叢集節點的數目")
   
   > [!IMPORTANT]
   > 如果您計劃 32 個以上的背景工作節點，在叢集建立，或建立之後，調整 hello 叢集，則您必須選取前端節點大小至少為 8 個核心，14 GB ram。
   > 
   > 如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。
   > 
   > 
   
   按一下**下一步**toosave hello 節點定價組態。

7. 按一下**進階設定**tooconfigure 其他選擇性設定，例如使用**指令碼動作**toocustomize 叢集 tooinstall 自訂元件，或加入**的虛擬網路**. 查看 hello 下表中的詳細資訊。

    ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "指定叢集節點的數目")

    | 選項 | 說明 |
    |--------|-------------|
    | **指令碼動作** | 如果您想 toouse 自訂指令碼 toocustomize 叢集中，正在建立 hello 叢集時，使用此選項。 如需指令碼動作的詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。 |
    | **虛擬網路** | 如果您想要在虛擬網路的 tooplace hello 叢集，請選取 Azure 虛擬網路和 hello 子網路。 如需使用 HDInsight 與虛擬網路，包括特定組態需求的 hello 虛擬網路，請參閱[擴充 HDInsight 功能，方法是使用 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。 |

    按一下 [下一步] 。

8. 在 hello**摘要**刀鋒視窗中，確認您先前輸入的 hello 資訊，然後按一下**建立**。

    ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "指定叢集節點的數目")
    
    > [!NOTE]
    > 它將需要一些時間 hello 叢集 toobe 建立，通常大約 15 分鐘。 使用 hello 磚上 hello 開始面板，或 hello**通知**hello 上的項目上佈建程序的 hello 方 hello 頁面 toocheck。
    > 
    > 
12. Hello 建立程序完成之後，請按一下 hello 磚 hello 叢集 hello 開始面板 toolaunch hello 叢集刀鋒視窗。 hello 叢集刀鋒視窗會提供下列資訊的 hello。
    
    ![叢集刀鋒視窗](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "叢集屬性")
    
    使用下列 toounderstand hello 圖示在 hello 這個刀鋒視窗頂端的 hello。
    
    * **概觀**索引標籤會提供有關 hello 叢集例如 hello 名稱、 其所屬 hello 位置，hello 作業系統中，URL hello 叢集儀表板等 hello 資源群組的 hello 基本資訊。
    * **儀表板**會將您導向 toohello Ambari 入口網站與 hello 叢集相關聯。
    * **安全殼層**： 需要使用 SSH tooaccess hello 叢集的資訊。
    * **延展叢集**可讓您增加 hello 與 hello 叢集相關聯的背景工作節點數。
    * **刪除**： 刪除 hello HDInsight 叢集。
    

## <a name="customize-clusters"></a>自訂叢集
* 請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。
* 請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟
既然您已成功建立的 HDInsight 叢集，請使用 hello 如何遵循 toolearn toowork 與您的叢集：

### <a name="hadoop-clusters"></a>Hadoop 叢集
* [〈搭配 HDInsight 使用 Hivet〉](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase 叢集
* [開始在 HDInsight 上使用 HBase](hdinsight-hbase-tutorial-get-started-linux.md)
* [在 HDInsight 上開發適用於 HBase 的 Java 應用程式](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm 叢集
* [在 HDInsight 上開發適用於 Storm 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)
* [在 HDInsight 上的 Storm 中使用 Python 元件](hdinsight-storm-develop-python-topology.md)
* [在 HDInsight 上使用 Storm 部署和監視拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark 叢集
* [使用 Scala 來建立獨立的應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行工作](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)

