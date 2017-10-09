---
title: "aaaGet 入門 Hadoop 和 Azure HDInsight 中的登錄區 |Microsoft 文件"
description: "了解如何 toocreate HDInsight 叢集，以及使用 Hive 查詢資料。"
keywords: "開始使用,hadoop linux,hadoop 快速入門,開始使用 hive,hive 快速入門"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Hadoop 教學課程：開始在 HDInsight 中使用 Hadoop

深入了解如何 toocreate [Hadoop](http://hadoop.apache.org/) HDInsight 及 toorun Hive HDInsight 中的工作中的叢集。 [Apache Hive](https://hive.apache.org/)是 hello hello Hadoop 生態系統中最受歡迎的元件。 HDInsight 目前隨附 [7 個不同的叢集類型](hdinsight-hadoop-introduction.md#overview)。 每種叢集類型都支援一組不同的元件。 所有叢集類型都支援 Hive。 如需支援的元件，在 HDInsight 中的清單，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備：

* **Azure 訂用帳戶**: toocreate 免費的一個月試用版帳戶，瀏覽過[azure.microsoft.com/free](https://azure.microsoft.com/free)。

## <a name="create-cluster"></a>建立叢集

大部分 Hadoop 作業都是批次作業。 您會建立叢集，執行某些作業，然後再刪除 hello 叢集。 在本節中，您會在 HDInsight 中使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)建立 Hadoop 叢集。 進行本教學課程並不需要具備 Resource Manager 範本經驗。 適用於其他叢集建立方法，並了解本教學課程中使用的 hello 內容，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 使用 hello 選取器 hello hello 頁面 toochoose 頂端上您的叢集建立選項。

在本教學課程中使用的 hello Resource Manager 範本位於[GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)。 

1. 按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 輸入或選取下列值的 hello:
   
    ![HDInsight Linux get 入口網站上啟動資源管理員範本](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "部署 Hadoop 叢集中使用 HDInsigut hello Azure 入口網站和資源群組管理員範本")。
   
    * **訂用帳戶**：選取您的 Azure 訂用帳戶。
    * **資源群組**：建立資源群組，或選取現有的資源群組。  資源群組是 Azure 元件的容器。  在此情況下，hello 資源群組包含 hello HDInsight 叢集和 hello 相依的 Azure 儲存體帳戶。 
    * **位置**： 選取您想 toocreate 您叢集的 Azure 位置。  選擇位置較接近 tooyou 以提升效能。 
    * **叢集類型**：請為本教學課程選取 [hadoop]。
    * **叢集名稱**： 輸入 hello Hadoop 叢集的名稱。
    * **叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。
    * **SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。  您可以將它重新命名。 
     
    某些屬性已被硬式編碼 hello 範本中。  您可以設定這些值從 hello 範本。

    * **位置**: hello hello 叢集的位置和 hello 相依的儲存體帳戶共用 hello 與 hello 資源群組相同的位置。
    * **叢集版本**：3.5
    * **OS 類型**：Linux
    * **背景工作節點數目**：2

     每個叢集都具備 [Azure 儲存體帳戶](hdinsight-hadoop-use-blob-storage.md)或 [Azure Data Lake 帳戶](hdinsight-hadoop-use-data-lake-store.md)相依性。 它會稱為 hello 預設儲存體帳戶。 HDInsight 叢集和其預設儲存體帳戶必須共置於 hello 中相同的 Azure 區域。 刪除叢集不會刪除 hello 儲存體帳戶。 
     
     如需這些屬性的詳細說明，請參閱[在 HDInsight 中建立Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

3. 選取**toohello 條款和條件前面所述，即表示我同意**和**Pin toodashboard**，然後按一下**購買**。 您應該會看到標題為新的圖格**部署範本部署**hello 入口網站儀表板上。 大約需要約 20 分鐘 toocreate 叢集。 一旦建立 hello 叢集後，hello 磚的 hello 標題是變更的 toohello 您指定的資源群組名稱。 和 hello 入口網站會自動開啟 hello 資源群組中的新刀鋒視窗。 您可以看到 hello 叢集和 hello 所列的預設儲存體。
   
    ![HDInsight Linux 開始使用的資源群組](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight 叢集資源群組")。

4. 按一下 hello 叢集名稱 tooopen hello 叢集的新刀鋒視窗中。

   ![HDInsight Linux 開始使用的叢集設定](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Azure HDInsight 屬性")


## <a name="run-hive-queries"></a>執行 Hive 查詢
[Apache Hive](hdinsight-use-hive.md)是 hello 最受歡迎使用 HDInsight 中的元件。 有很多種 toorun Hive 工作在 HDInsight 中。 在本教學課程中，您可以使用 hello Ambari Hive 檢視從 hello 入口網站。 如需提交 Hive 工作的其他方法，請參閱 [在 HDInsight 中使用 Hive](hdinsight-use-hive.md)。

1. 從 hello 上一個螢幕擷取畫面，按一下 **叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。  您也可以瀏覽過**https://&lt;ClusterName >。.azurehdinsight.net**，其中&lt;ClusterName > 是您在前一個區段 tooopen hello Ambari 建立 hello 叢集。
2. 輸入 hello Hadoop 使用者名稱和您在 hello 上一節中指定的密碼。 hello 預設使用者名稱是**admin**。
3. 開啟**Hive 檢視**hello 下列螢幕擷取畫面所示：
   
    ![選取 Ambari 檢視](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive 檢視器功能表")。
4. 在 [hello**查詢編輯器**hello] 頁面上，貼上下列 HiveQL 陳述式 hello 工作表中的 hello 區段：
   
        SHOW TABLES;
   
   > [!NOTE]
   > Hive 需要分號。       
   > 
   > 
5. 按一下 [Execute (執行)] 。 A**查詢程序結果**區段應該會顯示在底下 hello 查詢編輯器，並顯示 hello 工作的相關資訊。 
   
    Hello 查詢完成時，一旦 hello**查詢程序結果**區段會顯示 hello hello 作業結果。 您應該會看到一個名為 hivesampletable 的資料表。 此範例的 Hive 資料表隨附於所有的 hello HDInsight 叢集。
   
    ![HDInsight Hive 檢視](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive 檢視查詢編輯器")。
6. 重複步驟 4 和 5 步驟 toorun hello 下列查詢：
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > 請注意 hello**將結果儲存**下拉式清單中 hello 右上方 hello**查詢程序結果**區段; 您可以使用這個 tooeither 下載 hello 的結果，或將它們儲存 tooHDInsight 儲存成 CSV 檔案。
   > 
   > 
7. 按一下**記錄**tooget hello 工作清單。

您已完成的 Hive 工作之後，您可以[hello 結果 tooAzure SQL 資料庫或 SQL Server 資料庫匯出](hdinsight-use-sqoop-mac-linux.md)，您也可以[將使用 Excel 的 hello 結果視覺化](hdinsight-connect-excel-power-query.md)。 如需使用 HDInsight 中的登錄區的詳細資訊，請參閱[使用 Hive 和 HiveQL HDInsight tooanalyze 範例 Apache log4j 檔案中的 Hadoop](hdinsight-use-hive.md)。

## <a name="clean-up-hello-tutorial"></a>清除 hello 教學課程
完成 hello 教學課程之後，您可能想 toodelete hello 叢集。 利用 HDInsight，您的資料會儲存在 Azure 儲存體中，以便您在未使用叢集時安全地進行刪除。 您也需支付 HDInsight 叢集的費用 (即使未使用)。 由於 hello 叢集 hello 費用的次數超過儲存體的 hello 費用，經濟效益 toodelete 叢集時未使用。 

> [!NOTE]
> 使用[Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md)，您可以視情況下，需要建立 HDInsight 叢集並設定 TimeToLive 設定太 hello 叢集自動刪除。 
> 
> 

**toodelete hello 叢集及/或 hello 預設儲存體帳戶**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從 hello 入口網站儀表板，按一下 hello 磚 hello 建立 hello 叢集時，使用的資源群組名稱。
3. 按一下**刪除**在 hello 資源刀鋒視窗 toodelete hello 資源群組，其中包含 hello 叢集和 hello 預設儲存體帳戶，或按一下 hello 叢集名稱上 hello**資源**磚，然後按一下**刪除**hello 叢集刀鋒視窗上。 請注意，刪除 hello 資源群組中刪除 hello 儲存體帳戶。 如果您想 tookeep hello 儲存體帳戶，請選擇 toodelete hello 叢集中。

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已經學會如何 toocreate 以 Linux 為基礎的 HDInsight 叢集使用資源管理員範本，以及如何 tooperform 基本 Hive 查詢。

toolearn 有關使用 HDInsight，分析資料的詳細資訊，請參閱下列文章 hello:

* toolearn 更多有關搭配使用 Hive 與 HDInsight，包括如何 tooperform Hive 查詢從 Visual Studio，請參閱[使用 Hive 與 HDInsight][hdinsight-use-hive]。
* 關於 Pig toolearn，使用語言 tootransform 資料，請參閱[與 HDInsight 搭配使用 Pig][hdinsight-use-pig]。
* toolearn 有關 MapReduce，方式 toowrite 程式的處理資料的 Hadoop，請參閱[與 HDInsight 的使用 MapReduce][hdinsight-use-mapreduce]。
* 請參閱有關使用 hello HDInsight Tools for Visual Studio tooanalyze 資料在 HDInsight 上 toolearn[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)。

如果您是使用您自己的資料準備 toostart，且需要深入了解 tooknow HDInsight 儲存資料的方式，或如何 tooget 資料 HDInsight，請參閱下列資訊 hello:

* 如需有關 HDInsight 如何使用 Azure 儲存體的資訊，請參閱 [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)。
* 如需詳細資訊 tooupload 資料 tooHDInsight，請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。

如果您想要 toolearn 深入了解建立或管理的 HDInsight 叢集，請參閱 hello 下列資訊：

* toolearn 關於管理您的 Linux 為基礎的 HDInsight 叢集，請參閱[使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。
* toolearn 進一步了解 hello 選項，您可以選取當建立 HDInsight 叢集，請參閱[建立使用自訂選項的 Linux 的 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)。
* 如果您熟悉 Linux 及 Hadoop，但是想 tooknow 特點 Hadoop hello HDInsight 上的時，請參閱[Linux 上使用 HDInsight](hdinsight-hadoop-linux-information.md)。 本文提供的資訊如下：
  
  * 裝載在 hello 叢集上，例如 Ambari 和 WebHCat 服務的 Url
  * hello 位置的 Hadoop 檔案與 hello 本機檔案系統上的範例
  * hello 使用的 Azure 儲存體 (WASB) 而不是 HDFS 做 hello 預設資料存放區

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


