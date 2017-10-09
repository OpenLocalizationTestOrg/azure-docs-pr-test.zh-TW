---
title: "Azure Toolkit for IntelliJ 與 Hortonworks 沙箱 aaaUse |Microsoft 文件"
description: "深入了解如何 toouse HDInsight Tools 在 Azure Toolkit for IntelliJ 與 Hortonworks 沙箱。"
keywords: "hadoop 工具,hive 查詢,intellij,hortonworks 沙箱,azure toolkit for intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ

了解 toouse HDInsight Tools for IntelliJ toodevelop Apache Scala 應用程式以及測試工作流程如何 hello 應用程式上[Hortonworks 沙箱](http://hortonworks.com/products/sandbox/)在工作站上執行。 

[IntelliJ IDEA](https://www.jetbrains.com/idea/)是 Java 整合式開發環境 (IDE)，可用來開發電腦軟體。 您所開發並測試過您的應用程式上的 Hortonworks 沙箱之後，您可以將它們移過[Azure HDInsight](hdinsight-hadoop-introduction.md)。

## <a name="prerequisites"></a>必要條件

開始進行本教學課程之前，您必須具備：

- 在您的本機環境執行的 Hortonworks 沙箱上要有 Hortonworks Data Platform (HDP) 2.4。 tooconfigure HDP，請參閱[開始 hello Hadoop 生態系統，與虛擬機器上的 Hadoop 沙箱](hdinsight-hadoop-emulator-get-started.md)。 
    >[!NOTE]
    >HDInsight Tools for IntelliJ 只經過 HDP 2.4 測試。 展開 tooget HDP 2.4 **Hortonworks 沙箱封存**上 hello [Hortonworks 沙箱下載網站](http://hortonworks.com/downloads/#sandbox)。

- [Java Developer Kit (JDK) 1.8 版或更新版本](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。 如 IntelliJ 需要 hello Azure Toolkit JDK。

- [IntelliJ 概念 community edition](https://www.jetbrains.com/idea/download)以 hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala)外掛程式和 hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md)外掛程式。 使用 Azure Toolkit for IntelliJ hello 的一部份 IntelliJ HDInsight 工具。 

  tooinstall hello 外掛程式，請勿 hello 遵循：

  1. 開啟 IntelliJ IDEA。
  2. 在 hello ** 褖畫惎**畫面上，選取**設定**，然後選取**外掛程式**。
  3. 選取**安裝 JetBrains 外掛程式**hello 左下角。
  4. 使用的 hello 搜尋函式 toosearch **Scala**，然後選取**安裝**。
  5. 選取**重新啟動 IntelliJ 概念**toocomplete hello 安裝。
  6. 重複步驟 4 和 5 tooinstall hello **Azure Toolkit for IntelliJ**。 如需詳細資訊，請參閱[安裝 hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。

## <a name="create-a-spark-scala-application"></a>建立 Spark Scala 應用程式

在本節中，您會使用 IntelliJ IDEA 建立範例 Scala 專案。 Hello 下一節，您將連結 IntelliJ 概念 toohello Hortonworks 沙箱 （模擬器） 之前您送出 hello 專案。

1. 從您的工作站開啟 IntelliJ IDEA。 在 hello**新專案**對話方塊方塊中，執行下列 hello:

   a. 選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。

   b. 在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:

    * **Maven**，以支援 Scala 專案建立精靈
    * **SBT**、 管理 hello 相依性和建置 hello Scala 專案

   ![hello 新增專案 對話方塊](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. 選取 [下一步] 。

3. 在 hello 下一步**新專案**對話方塊方塊中，執行下列 hello:

    ![建立 IntelliJ Scala 專案屬性](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. 在 hello**專案名稱**方塊中，輸入專案名稱。

    b. 在 hello**專案位置**方塊中，輸入專案位置。

    c. 下一步 toohello**專案 SDK**下拉式清單中，選取**新增**，選取**JDK**，然後指定 hello 的 Java JDK 1.7 版或更新版本的資料夾。 選取**Java 1.8** hello Spark 2.x 叢集，或選取**Java 1.7** hello Spark 1.x 叢集。 hello 預設位置是 C:\Program Files\Java\jdk1.8.x_xxx。

    d. 在 hello **Spark 版本**下拉式清單中，Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。 如果 hello Spark 叢集版本早於 2.0，請選取**二手 1.x**。 否則，請選取 [Spark2.x]。 此範例使用 Spark 1.6.2 (Scala 2.10.5)。 請確定您使用 hello 儲存機制標示 Scala 2.10.x。 請勿使用 hello 儲存機制標示 Scala 2.11.x。

4. 選取 [完成]。

5. 如果 hello**專案**檢視尚未開啟，請按**Alt + 1** tooopen 它。

6. 在**Project Explorer**，展開 hello 專案，然後選取**src**。

7. 以滑鼠右鍵按一下**src**，點太**新增**，然後選取**Scala 類別**。

8. 在 hello**名稱**方塊中，輸入名稱，在 hello**種類**方塊中，選取**物件**，然後選取**[確定]**。

    ![hello 建立 Scala 類別視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. 在 hello.scala 檔案中，貼上下列程式碼的 hello:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. 在 hello**建置**功能表上，選取**建置專案**。 請確定 hello 編譯已順利完成。


## <a name="link-toohello-hortonworks-sandbox"></a>連結 toohello Hortonworks 沙箱

您可以將連結 tooa Hortonworks 沙箱 （模擬器） 之前，您必須具有現有 IntelliJ 應用程式。

toolink tooan 模擬器中，執行下列 hello:

1. 開啟 hello IntelliJ 中的專案。

2. 在 hello**檢視**功能表上，選取**工具視窗**，然後選取**Azure 總管**。

3. 展開 [Azure]，以滑鼠右鍵按一下 [HDInsight]，然後選取 [連結模擬器]。

4. 在 hello**連結新的模擬器**視窗中，輸入您設定的 hello 根帳號的 hello Hortonworks 沙箱，hello 下列螢幕擷取畫面中輸入值類似 toothose，然後選取 hello 密碼**確定**. 

   ![hello 」 連結新的模擬器 」 視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. tooconfigure hello 模擬器中，選取**是**。

當 hello 模擬器已成功連接時，hello 模擬器 （Hortonworks 沙箱） 會列在 hello HDInsight 節點。

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>送出 hello Spark Scala 應用程式 toohello Hortonworks 沙箱

您已連結 IntelliJ 概念 toohello 模擬器之後，您可以提交您的專案。

toosubmit 專案 tooan 模擬器中，請勿 hello 遵循：

1. 在**Project Explorer**，hello 專案上按一下滑鼠右鍵，然後選取**提交 Spark 應用程式 tooHDInsight**。

2. 請勿 hello 遵循：

    a. 在 hello **Spark 叢集 (僅 Linux)**下拉式清單中，選取您本機的 Hortonworks 沙箱。

    b. 在 hello**主要類別名稱**方塊中，選擇或輸入 hello 主要的類別名稱。 此教學課程，hello 名稱是**GroupByTest**。

3. 選取 [提交]。 hello 作業送出記錄檔會顯示 hello Spark 提交工具視窗中。

## <a name="next-steps"></a>後續步驟

- 如何 toocreate Spark 應用程式 HDInsight 的使用 HDInsight Tools for IntelliJ，都會太 toolearn[Azure Toolkit for HDInsight Spark Linux 叢集的 IntelliJ toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-intellij-tool-plugin.md)。

- toowatch HDInsight Tools for IntelliJ，視訊跳過[導入 HDInsight Tools for Spark 開發 IntelliJ](https://www.youtube.com/watch?v=YTZzYVgut6c)。

- toolearn toodebug Spark 應用程式使用 hello 在透過 SSH 的 HDInsight 上的遠端工具組如何移過[進行遠端偵錯 Spark 的應用程式使用 Azure Toolkit 在 HDInsight 叢集上透過 SSH IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)。

- toolearn toodebug Spark 應用程式使用 hello 在透過 VPN，HDInsight 上的遠端工具組如何移過[Azure Toolkit for IntelliJ HDInsight Spark Linux 叢集上從遠端 toodebug Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)。

- toolearn toouse HDInsight Tools for Eclipse toocreate Spark 應用程式如何太移[Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)。

- toowatch HDInsight Tools for Eclipse，視訊跳過[Eclipse toocreate Spark 應用程式的使用 HDInsight 工具](https://mix.office.com/watch/1rau2mopb6fha)。
