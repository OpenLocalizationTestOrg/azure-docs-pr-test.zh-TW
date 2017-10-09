---
title: "上的 Spark 叢集-Azure HDInsight aaaCreate Scala 應用程式 toorun |Microsoft 文件"
description: "建立 Spark 撰寫的應用程式使用 Apache Maven Scala hello Scala IntelliJ 概念所提供的建置系統及現有的 Maven 原型。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>HDInsight 上的 Apache Spark 叢集上建立 Scala Maven 應用程式 toorun

深入了解如何 toocreate Scala Maven 使用 IntelliJ 概念中撰寫的 Spark 應用程式。 hello 發行項使用 Apache Maven hello 建置系統，並加以啟動現有的 Maven 原型 Scala IntelliJ 概念所提供的。  IntelliJ 概念中建立 Scala 應用程式包括 hello 下列步驟：

* 使用 Maven 做為 hello 建置系統。
* 更新專案物件模型 (POM) 檔案 tooresolve Spark 模組相依性。
* 以 Scala 撰寫應用程式。
* 產生可以提交的 tooHDInsight Spark 叢集 jar 檔案。
* 使用晚總 Spark 叢集執行 hello 應用程式。

> [!NOTE]
> HDInsight 也會提供概念 IntelliJ 外掛程式工具 tooease hello 處理程序中建立並送出應用程式 tooan on Linux 的 HDInsight Spark 叢集。 如需詳細資訊，請參閱[使用 HDInsight 工具適用於外掛程式 IntelliJ 概念 toocreate 提交 Spark 應用程式和](hdinsight-apache-spark-intellij-tool-plugin.md)。
> 
> 

## <a name="prerequisites"></a>必要條件

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。
* Oracle Java Development Kit。 您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。
* Java IDE。 本文使用 IntelliJ IDEA 15.0.1。 您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。

## <a name="install-scala-plugin-for-intellij-idea"></a>安裝 IntelliJ IDEA 的 Scala 外掛程式
如果 IntelliJ 概念安裝沒有啟用 Scala 外掛程式不提示，啟動 IntelliJ 概念，並瀏覽下列步驟 tooinstall hello 外掛程式 hello:

1. 啟動 IntelliJ IDEA，並在 歡迎使用 畫面中按一下 設定，然後按一下外掛程式。
   
    ![啟用 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. 在 hello 下一個畫面中，按一下 **安裝 JetBrains 外掛程式**從 hello 左下角。 在 hello**瀏覽 JetBrains 外掛程式**對話方塊隨即開啟，Scala 搜尋，然後再按一下**安裝**。
   
    ![安裝 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. 已成功安裝 hello 外掛程式之後，請按一下 hello**重新啟動 IntelliJ 概念按鈕**toorestart hello IDE。

## <a name="create-a-standalone-scala-project"></a>建立獨立 Scala 專案
1. 啟動 IntelliJ IDEA，並建立新的專案。 在 hello 新專案 對話方塊進行 hello 下列選項，然後按一下**下一步**。
   
    ![建立 Maven 專案](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * 選取**Maven** hello 專案類型。
   * 指定 [專案 SDK] 。 按一下 [新增] 並瀏覽 toohello Java 安裝目錄時，通常`C:\Program Files\Java\jdk1.8.0_66`。
   * 選取 hello**從原型建立**選項。
   * 從 hello archetypes 清單選取**org.scala tools.archetypes:scala 原型-簡單**。 這會建立 hello 正確的目錄結構，並下載所需的 hello 預設相依性 toowrite Scala 程式。
2. 為 [GroupId]、[ArtifactId] 和 [版本] 提供相關值。 按一下 [下一步] 。
3. Hello 下一步 對話方塊，讓您指定 Maven 主目錄及其他使用者設定，在接受 hello 預設值然後按**下一步**。
4. 在 hello 最後一個對話方塊，指定專案名稱和位置，然後按一下**完成**。
5. 刪除 hello **MySpec.Scala**檔案**src\test\scala\com\microsoft\spark\example**。 您不需要這個 hello 應用程式。
6. 如有需要，重新命名 hello 預設來源和測試檔案。 從 hello IntelliJ 概念 hello 左窗格，瀏覽過**src\main\scala\com.microsoft.spark.example**。 以滑鼠右鍵按一下**App.scala**，按一下 **重構**、 按一下 重新命名檔案，並在 hello 對話方塊中，提供 hello hello 應用程式的新名稱，然後按一下**重構**。
   
    ![重新命名檔案](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. 在 hello 後續步驟中，您將更新 hello pom.xml toodefine hello 相依性 hello Spark Scala 應用程式。 這些相依性 toobe 下載，並自動解決，您必須據此設定 Maven。
   
    ![設定 Maven 以進行自動下載](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. 從 hello**檔案**功能表上，按一下 **設定**。
   2. 在 hello**設定**對話方塊方塊中，瀏覽過**建置、 執行、 部署** > **建置工具** > **Maven** > **匯入**。
   3. 選取 hello 選項太**匯入 Maven 專案自動**。
   4. 按一下 套用，然後按一下確定。
8. 更新 hello Scala 來源檔案 tooinclude 應用程式程式碼。 開啟並取代現有範例程式碼以下列程式碼的 hello hello 並儲存 hello 變更。 此程式碼，讀取 hello hello HVAC.csv （可在所有的 HDInsight Spark 叢集上）、 擷取 hello hello 第六個資料行中只有一個數字的資料列和 hello 會將輸出寫入太**/HVACOut**下 hello 預設儲存體hello 叢集的容器。
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. 更新 hello pom.xml。
   
   1. 內`<project>\<properties>`新增 hello 下列：
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. 內`<project>\<dependencies>`新增 hello 下列：
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      儲存變更 toopom.xml。
10. 建立 hello 檔案。 IntelliJ IDEA 允許將 JAR 建立為專案的構件。 執行下列步驟的 hello。
    
    1. 從 hello**檔案**功能表上，按一下 **專案結構**。
    2. 在 hello**專案結構**對話方塊中，按一下 **成品**hello 加上符號，然後按一下。 Hello 快顯對話方塊方塊中，按一下  **JAR**，然後按一下**具有相依性的模組從**。
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. 在 hello**從模組建立 JAR**對話方塊方塊中，按一下 hello 省略符號 (![省略](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) 針對 hello**主要類別**。
    4. 在 hello**選取主要類別**對話方塊中，依預設會出現，然後按一下選取 hello 類別**確定**。
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. 在 hello**從模組建立 JAR**對話方塊方塊中，請確定該 hello 選項太**擷取 toohello 目標 JAR**已選取，然後按一下**確定**。 這會建立具有所有相依性的單一 JAR。
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. hello 輸出版面配置 索引標籤會列出所有 hello （每瓶） 的 hello Maven 專案的一部分。 您可以選取和刪除 hello 所在的 hello Scala 應用程式並沒有直接相依。 對於此建立 hello 應用程式，您可以移除以外的所有 hello 最後一個 (**SparkSimpleApp 編譯輸出**)。 選取 hello （每瓶) toodelete，然後按一下hello**刪除**圖示。
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        請確定**上進行建置**選取方塊，以確保每次建立或更新 hello 專案建立該 hello jar。 依序按一下 [套用] 及 [確定]。
    7. 在 hello 功能表列中，按一下**建置**，然後按一下**進行專案**。 您也可以按一下**組建成品**toocreate hello jar。 hello 輸出 jar 下方會建立**\out\artifacts**。
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Hello Spark 叢集上執行 hello 應用程式
hello 叢集上的 toorun hello 應用程式，您必須執行下列 hello:

* **複製 hello 應用程式 jar toohello Azure 儲存體 blob** hello 叢集相關聯。 您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式，toodo 因此。 有很多其他用戶端以及您可以使用 tooupload 資料。 您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。
* **從遠端使用晚總 toosubmit 應用程式工作**toohello Spark 叢集。 HDInsight 上的 Spark 叢集包含晚總公開 REST 端點 tooremotely 送出 Spark 作業。 如需詳細資訊，請參閱 [搭配 HDInsight 上的 Spark 叢集利用 Livy 遠端提交 Spark 作業](hdinsight-apache-spark-livy-rest-interface.md)。

## <a name="next-step"></a>後續步驟

在這個發行項您學到如何 toocreate Spark scala 應用程式。 進階 toohello 下一個發行項 toolearn 如何 toorun 這個應用程式的 HDInsight Spark 叢集使用晚總。

> [!div class="nextstepaction"]
>[利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

