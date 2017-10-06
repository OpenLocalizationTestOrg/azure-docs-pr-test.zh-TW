---
title: "在 Azure HDInsight 叢集 aaaCreate Apache Spark |Microsoft 文件"
description: "如何 toocreate Apache Spark 叢集在 HDInsight 上的 HDInsight Spark 快速入門。"
keywords: "spark 快速入門, 互動式 spark, 互動式查詢, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>在 Azure HDInsight 中建立 Apache Spark 叢集

在本文中，您學會 toocreate Apache Spark 中 Azure HDInsight 叢集的方式。 如需 Spark on HDInsight 相關資訊，請參閱[概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)。

   ![快速入門步驟 toocreate Apache Spark 叢集描述 Azure HDInsight 上的圖表](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "使用 Apache Spark 中 HDInsight Spark 快速入門。說明的步驟︰建立叢集；執行 Spark 互動式查詢")

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。 請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。

## <a name="create-hdinsight-spark-cluster"></a>建立 HDInsight Spark 叢集

在本節中，您會使用 [Azure Resource Manager 範本](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/)來建立 HDInsight Spark 叢集。 如需其他叢集建立方法，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

1. 按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. 輸入下列值的 hello:

    ![使用 Azure Resource Manager 範本建立 HDInsight Spark 叢集](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "在 HDInsight 中使用 Azure Resource Manager 範本建立 Spark 叢集")

    * **訂用帳戶**：針對此叢集選取您的 Azure 訂用帳戶。
    * **資源群組**：建立資源群組，或選取現有的資源群組。 資源群組是使用的 toomanage 專案的 Azure 資源。
    * **位置**： 選取 hello 資源群組的位置。 hello 範本會使用這個位置建立 hello 叢集也與 hello 預設叢集存放區。
    * **ClusterName**： 輸入您想 toocreate hello HDInsight 叢集的名稱。
    * **Spark 版本**： 選取**2.0**做為您想 tooinstall hello 叢集上的 hello 版本。
    * **叢集登入名稱和密碼**: hello 預設登入名稱是系統管理員。
    * SSH 使用者名稱和密碼。

   請記下這些值。  您稍後在 hello 教學課程需要它們。

3. 選取**toohello 條款和條件前面所述，即表示我同意**，選取**Pin toodashboard**，然後按一下**購買**。 您可以看到新的圖格，標題為「提交範本部署的部署」。 它會採用約 20 分鐘 toocreate hello 叢集。

如果您遇到的問題建立 HDInsight 叢集時，可能是，您不需要 hello 正確的權限 toodo 因此。 如需詳細資訊，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

> [!NOTE]
> 這篇文章建立 Spark 叢集，以使用[hello 與 Azure 儲存體 Blob 叢集儲存體](hdinsight-hadoop-use-blob-storage.md)。 您也可以建立使用的 Spark 叢集[Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)為 hello 預設儲存體。 如需指示，請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>執行使用 Spark SQL 的 Hive 查詢

當您使用 HDInsight Spark 叢集設定 Jupyter 筆記本時，您會取得預設`sqlContext`可讓您使用 Spark SQL toorun Hive 查詢。 在本節中，您學會如何 toostart Jupyter 筆記本，然後執行基本的 Hive 查詢。

1. 開啟 hello [Azure 入口網站](https://portal.azure.com/)。

2. 如果您選擇 toopin hello 叢集 toohello 儀表板，按一下 hello 叢集磚的 hello 儀表板 toolaunch hello 叢集刀鋒視窗。

    如果您沒有不固定 hello 叢集 toohello 儀表板，從 hello 左窗格中，按一下**HDInsight 叢集**，然後按一下您所建立的 hello 叢集。

3. 從 快速連結，按一下 叢集儀表板，然後按一下Jupyter Notebook。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   ![開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")

   > [!NOTE]
   > 您也可以透過下列 URL 在瀏覽器中開啟 hello 叢集存取 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. 建立 Notebook。 按一下 新增，然後按一下PySpark。

   ![建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")

   建立新的記事本，並開啟 hello 名稱 Untitled(Untitled.pynb)。

4. 按一下頂端 hello hello 筆記本名稱，然後輸入易記的名稱，如果您想。

    ![提供查詢的名稱 hello Jupter 筆記本 toorun 互動式 Spark 從](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "提供 hello Jupter 筆記本 toorun 互動式 Spark 中查詢的名稱")

5.  貼上 hello 下列空的資料格中的程式碼，然後按下**SHIFT + ENTER** toorun hello 程式碼。 下列程式碼 hello `%%sql` (稱為的 hello sql magic) 會告知 Jupyter 筆記本 toouse hello 預設`sqlContext`toorun hello Hive 查詢。 hello 查詢擷取 Hive 資料表中的 hello 前 10 個資料列 (**hivesampletable**)，而且可根據預設，所有的 HDInsight 叢集上。

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![HDInsight Spark 中的 Hive 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark 中的 Hive 查詢")

    如需有關 hello`%%sql`魔法與 hello 預先設定的內容，請參閱[Jupyter 核心的 HDInsight 叢集供](hdinsight-apache-spark-jupyter-notebook-kernels.md)。

    > [!NOTE]
    > 每次您在 Jupyter 執行查詢，會顯示您的 web 瀏覽器視窗標題**（忙碌）**狀態以及 hello 筆記本標題。 另請參閱實心圓的下一個 toohello **PySpark** hello 右上角中的文字。 Hello 作業完成之後，它會變更 tooa 空心圓圈。
    >
    >
    
6. 囉 」 畫面應該重新整理 tooshow hello 查詢輸出。

    ![HDInsight Spark 中的 Hive 查詢輸出](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark 中的 Hive 查詢輸出")

7. 您完成執行後，hello 應用程式，請關閉 hello 筆記本 toorelease hello 叢集資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。

8. 如果您稍後打算 toocomplete hello 接下來的步驟，請確定刪除在這篇文章中所建立的 hello HDInsight 叢集。 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>後續步驟 

在本文，您學到如何 toocreate HDInsight Spark 叢集，並執行基本的 Spark SQL 查詢。 前進 toohello toouse HDInsight Spark 叢集的方式下一個發行項 toolearn toorun 互動式查詢針對取樣資料。

> [!div class="nextstepaction"]
>[在 HDInsight Spark 叢集上執行互動查詢](hdinsight-apache-spark-load-data-run-query.md)



