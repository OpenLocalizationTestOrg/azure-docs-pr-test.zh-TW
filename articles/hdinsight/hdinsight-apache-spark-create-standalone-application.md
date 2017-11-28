---
title: "建立在 Spark 叢集上執行的 Scala 應用程式 - Azure HDInsight | Microsoft Docs"
description: "建立以 Scala 撰寫的 Spark 應用程式，搭配 Apache Maven 作為建置系統，以及由 IntelliJ IDEA 提供之適用於 Scala 的現有 Maven 原型。"
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
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="07dc7-103">建立在 HDInsight 中的 Apache Spark 叢集上執行的 Scala Maven 應用程式</span><span class="sxs-lookup"><span data-stu-id="07dc7-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="07dc7-104">了解如何使用 Maven 搭配 IntelliJ IDEA 來建立以 Scala 撰寫的 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07dc7-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="07dc7-105">本文以 Apache Maven 作為建置系統，並且以 IntelliJ IDEA 為 Scala 提供的現有 Maven 原型作為起始點。</span><span class="sxs-lookup"><span data-stu-id="07dc7-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="07dc7-106">要在 IntelliJ IDEA 中建立 Scala 應用程式，必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="07dc7-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="07dc7-107">以 Maven 做為建置系統。</span><span class="sxs-lookup"><span data-stu-id="07dc7-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="07dc7-108">更新專案物件模型 (POM) 檔案，以解析 Spark 模組相依性。</span><span class="sxs-lookup"><span data-stu-id="07dc7-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="07dc7-109">以 Scala 撰寫應用程式。</span><span class="sxs-lookup"><span data-stu-id="07dc7-109">Write your application in Scala.</span></span>
* <span data-ttu-id="07dc7-110">產生可提交至 HDInsight Spark 叢集的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="07dc7-111">使用 Livy 在 Spark 叢集上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="07dc7-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="07dc7-112">HDInsight 也提供 IntelliJ IDEA 外掛程式工具，可簡化建立和提交應用程式至 Linux 上之 HDInsight Spark 叢集的程序。</span><span class="sxs-lookup"><span data-stu-id="07dc7-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="07dc7-113">如需詳細資訊，請參閱 [使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="07dc7-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="07dc7-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="07dc7-114">Prerequisites</span></span>

* <span data-ttu-id="07dc7-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07dc7-115">An Azure subscription.</span></span> <span data-ttu-id="07dc7-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="07dc7-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="07dc7-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="07dc7-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="07dc7-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="07dc7-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="07dc7-119">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="07dc7-119">Oracle Java Development kit.</span></span> <span data-ttu-id="07dc7-120">您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。</span><span class="sxs-lookup"><span data-stu-id="07dc7-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="07dc7-121">Java IDE。</span><span class="sxs-lookup"><span data-stu-id="07dc7-121">A Java IDE.</span></span> <span data-ttu-id="07dc7-122">本文使用 IntelliJ IDEA 15.0.1。</span><span class="sxs-lookup"><span data-stu-id="07dc7-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="07dc7-123">您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。</span><span class="sxs-lookup"><span data-stu-id="07dc7-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="07dc7-124">安裝 IntelliJ IDEA 的 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="07dc7-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="07dc7-125">如果 IntelliJ IDEA 安裝未提示您啟 Scala 外掛程式，請啟動 IntelliJ IDEA，然後完成下列步驟以安裝此外掛程式：</span><span class="sxs-lookup"><span data-stu-id="07dc7-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="07dc7-126">啟動 IntelliJ IDEA，並在 [歡迎使用] 畫面中按一下 [設定]，然後按一下 [外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![啟用 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="07dc7-128">在下一個畫面中，按一下左下角的 [安裝 JetBrains 外掛程式]  。</span><span class="sxs-lookup"><span data-stu-id="07dc7-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="07dc7-129">在開啟的 [瀏覽 JetBrains 外掛程式] 對話方塊中搜尋 Scala，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![安裝 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="07dc7-131">此外掛程式安裝成功之後，請按一下 [重新啟動 IntelliJ IDEA]  按鈕，以重新啟動 IDE。</span><span class="sxs-lookup"><span data-stu-id="07dc7-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="07dc7-132">建立獨立 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="07dc7-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="07dc7-133">啟動 IntelliJ IDEA，並建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="07dc7-134">在新增專案對話方塊中選取下列選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![建立 Maven 專案](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="07dc7-136">選取 [Maven]  做為專案類型。</span><span class="sxs-lookup"><span data-stu-id="07dc7-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="07dc7-137">指定 [專案 SDK] 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="07dc7-138">按一下 [新增]，然後導覽至 Java 安裝目錄 (通常是 `C:\Program Files\Java\jdk1.8.0_66`)。</span><span class="sxs-lookup"><span data-stu-id="07dc7-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="07dc7-139">選取 [從原型建立]  選項。</span><span class="sxs-lookup"><span data-stu-id="07dc7-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="07dc7-140">從原型清單中，選取 **org.scala-tools.archetypes:scala-archetype-simple**。</span><span class="sxs-lookup"><span data-stu-id="07dc7-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="07dc7-141">這會建立正確的目錄結構，並下載撰寫 Scala 程式所需的預設相依性。</span><span class="sxs-lookup"><span data-stu-id="07dc7-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="07dc7-142">為 [GroupId]、[ArtifactId] 和 [版本] 提供相關值。</span><span class="sxs-lookup"><span data-stu-id="07dc7-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="07dc7-143">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-143">Click **Next**.</span></span>
3. <span data-ttu-id="07dc7-144">在下一個對話方塊中 (您可以在此處指定 Maven 主目錄及其他使用者設定) 接受預設值，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="07dc7-145">在最後一個對話方塊中指定專案名稱和位置，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="07dc7-146">刪除位於 **src\test\scala\com\microsoft\spark\example** 的 **MySpec.Scala** 檔案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="07dc7-147">應用程式並不需要此檔案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="07dc7-148">如有必要，請重新命名預設來源和測試檔案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="07dc7-149">在 IntelliJ IDEA 的左窗格中，導覽至 **src\main\scala\com.microsoft.spark.example**。</span><span class="sxs-lookup"><span data-stu-id="07dc7-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="07dc7-150">以滑鼠右鍵按一下 **App.scala**、按一下 [重構]、按一下 [重新命名檔案]，在對話方塊中提供應用程式的新名稱，然後按一下 [重構]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![重新命名檔案](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="07dc7-152">在後續步驟中，您將會更新 pom.xml，以定義 Spark Scala 應用程式的相依性。</span><span class="sxs-lookup"><span data-stu-id="07dc7-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="07dc7-153">若要自動下載並解析這些相依性，您必須據以設定 Maven。</span><span class="sxs-lookup"><span data-stu-id="07dc7-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![設定 Maven 以進行自動下載](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="07dc7-155">從 [檔案] 功能表中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="07dc7-156">在 [設定] 對話方塊中，導覽至 [建置、執行、部署] > [建置工具] > [Maven] > [匯入]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="07dc7-157">選取 [自動匯入 Maven 專案] 的選項。</span><span class="sxs-lookup"><span data-stu-id="07dc7-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="07dc7-158">按一下 [套用]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="07dc7-159">更新 Scala 原始程式檔，以納入您的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="07dc7-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="07dc7-160">開啟現有的範例程式碼，並將其取代為下列程式碼，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="07dc7-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="07dc7-161">此程式碼會從 HVAC.csv (所有 HDInsight Spark 叢集上均有提供) 讀取資料、擷取在第六個資料行中只有個位數的資料列，並將輸出寫入到叢集預設儲存體容器下的 **/HVACOut** 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="07dc7-162">更新 pom.xml。</span><span class="sxs-lookup"><span data-stu-id="07dc7-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="07dc7-163">在 `<project>\<properties>` 內新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="07dc7-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="07dc7-164">在 `<project>\<dependencies>` 內新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="07dc7-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="07dc7-165">儲存 pom.xml 的變更。</span><span class="sxs-lookup"><span data-stu-id="07dc7-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="07dc7-166">建立 .jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="07dc7-166">Create the .jar file.</span></span> <span data-ttu-id="07dc7-167">IntelliJ IDEA 允許將 JAR 建立為專案的構件。</span><span class="sxs-lookup"><span data-stu-id="07dc7-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="07dc7-168">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="07dc7-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="07dc7-169">在 [檔案] 功能表中，按一下 [專案結構]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="07dc7-170">在 [專案結構] 對話方塊中，按一下 [構件]，然後按一下加號。</span><span class="sxs-lookup"><span data-stu-id="07dc7-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="07dc7-171">在快顯對話方塊中按一下 [JAR]，然後按一下 [從具有相依性的模組]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="07dc7-173">在 [從模組建立 JAR] 對話方塊中，對 [主要類別] 按一下省略符號 (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png))。</span><span class="sxs-lookup"><span data-stu-id="07dc7-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="07dc7-174">在 [選取主要類別] 對話方塊中，選取依預設出現的類別，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="07dc7-176">在 [從模組建立 JAR] 對話方塊中，確定已選取 [擷取至目標 JAR]選項，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="07dc7-177">這會建立具有所有相依性的單一 JAR。</span><span class="sxs-lookup"><span data-stu-id="07dc7-177">This creates a single JAR with all dependencies.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="07dc7-179">[輸出配置] 索引標籤會列出所有納入 Maven 專案中的 jar。</span><span class="sxs-lookup"><span data-stu-id="07dc7-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="07dc7-180">您可以選取並刪除 Scala 應用程式未直接依存的 jar。</span><span class="sxs-lookup"><span data-stu-id="07dc7-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="07dc7-181">對於我們在此處建立的應用程式，您可以移除最後一個 (**SparkSimpleApp 編譯輸出**) 以外的所有 jar。</span><span class="sxs-lookup"><span data-stu-id="07dc7-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="07dc7-182">選取要刪除的 jar，然後按一下 [刪除]  圖示。</span><span class="sxs-lookup"><span data-stu-id="07dc7-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="07dc7-184">請確實選取 [在建置時建立]  方塊，以確保在每次建置或更新專案時都會建立 jar。</span><span class="sxs-lookup"><span data-stu-id="07dc7-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="07dc7-185">依序按一下 [套用] 及 [確定]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="07dc7-186">在功能表列中按一下 [建置]，然後按一下 [建立專案]。</span><span class="sxs-lookup"><span data-stu-id="07dc7-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="07dc7-187">您也可以按一下 [建置構件]，以建立 jar。</span><span class="sxs-lookup"><span data-stu-id="07dc7-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="07dc7-188">輸出 jar 會建立在 **\out\artifacts** 下。</span><span class="sxs-lookup"><span data-stu-id="07dc7-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="07dc7-190">在 Spark 叢集上執行應用程式</span><span class="sxs-lookup"><span data-stu-id="07dc7-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="07dc7-191">若要在叢集上執行應用程式，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="07dc7-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="07dc7-192">**將應用程式 jar 複製到與叢集相關聯的 Azure 儲存體 Blob** 。</span><span class="sxs-lookup"><span data-stu-id="07dc7-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="07dc7-193">您可以使用命令列公用程式 [**AzCopy**](../storage/common/storage-use-azcopy.md) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="07dc7-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="07dc7-194">另外也有很多用戶端可用來上傳資料。</span><span class="sxs-lookup"><span data-stu-id="07dc7-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="07dc7-195">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="07dc7-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="07dc7-196">**使用 Livy 從遠端提交應用程式作業至** Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="07dc7-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="07dc7-197">HDInsight 上的 Spark 叢集包含會公開 REST 端點以從遠端提交 Spark 作業的 Livy。</span><span class="sxs-lookup"><span data-stu-id="07dc7-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="07dc7-198">如需詳細資訊，請參閱 [搭配 HDInsight 上的 Spark 叢集利用 Livy 遠端提交 Spark 作業](hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="07dc7-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="07dc7-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07dc7-199">Next step</span></span>

<span data-ttu-id="07dc7-200">在本文中，您已了解如何建立 Spark Scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07dc7-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="07dc7-201">前往下篇文章，了解如何使用 Livy 在 HDInsight Spark 叢集上執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="07dc7-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="07dc7-202">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="07dc7-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

