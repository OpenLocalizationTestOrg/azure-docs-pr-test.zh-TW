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
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="0f2ac-103">HDInsight 上的 Apache Spark 叢集上建立 Scala Maven 應用程式 toorun</span><span class="sxs-lookup"><span data-stu-id="0f2ac-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="0f2ac-104">深入了解如何 toocreate Scala Maven 使用 IntelliJ 概念中撰寫的 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="0f2ac-105">hello 發行項使用 Apache Maven hello 建置系統，並加以啟動現有的 Maven 原型 Scala IntelliJ 概念所提供的。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="0f2ac-106">IntelliJ 概念中建立 Scala 應用程式包括 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0f2ac-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="0f2ac-107">使用 Maven 做為 hello 建置系統。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="0f2ac-108">更新專案物件模型 (POM) 檔案 tooresolve Spark 模組相依性。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="0f2ac-109">以 Scala 撰寫應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-109">Write your application in Scala.</span></span>
* <span data-ttu-id="0f2ac-110">產生可以提交的 tooHDInsight Spark 叢集 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="0f2ac-111">使用晚總 Spark 叢集執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2ac-112">HDInsight 也會提供概念 IntelliJ 外掛程式工具 tooease hello 處理程序中建立並送出應用程式 tooan on Linux 的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="0f2ac-113">如需詳細資訊，請參閱[使用 HDInsight 工具適用於外掛程式 IntelliJ 概念 toocreate 提交 Spark 應用程式和](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0f2ac-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="0f2ac-114">Prerequisites</span></span>

* <span data-ttu-id="0f2ac-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-115">An Azure subscription.</span></span> <span data-ttu-id="0f2ac-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0f2ac-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0f2ac-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="0f2ac-119">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-119">Oracle Java Development kit.</span></span> <span data-ttu-id="0f2ac-120">您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="0f2ac-121">Java IDE。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-121">A Java IDE.</span></span> <span data-ttu-id="0f2ac-122">本文使用 IntelliJ IDEA 15.0.1。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="0f2ac-123">您可以從[這裡](https://www.jetbrains.com/idea/download/)安裝它。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="0f2ac-124">安裝 IntelliJ IDEA 的 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="0f2ac-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="0f2ac-125">如果 IntelliJ 概念安裝沒有啟用 Scala 外掛程式不提示，啟動 IntelliJ 概念，並瀏覽下列步驟 tooinstall hello 外掛程式 hello:</span><span class="sxs-lookup"><span data-stu-id="0f2ac-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="0f2ac-126">啟動 IntelliJ IDEA，並在 歡迎使用 畫面中按一下 設定，然後按一下外掛程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![啟用 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="0f2ac-128">在 hello 下一個畫面中，按一下 **安裝 JetBrains 外掛程式**從 hello 左下角。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="0f2ac-129">在 hello**瀏覽 JetBrains 外掛程式**對話方塊隨即開啟，Scala 搜尋，然後再按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![安裝 Scala 外掛程式](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="0f2ac-131">已成功安裝 hello 外掛程式之後，請按一下 hello**重新啟動 IntelliJ 概念按鈕**toorestart hello IDE。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="0f2ac-132">建立獨立 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="0f2ac-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="0f2ac-133">啟動 IntelliJ IDEA，並建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="0f2ac-134">在 hello 新專案 對話方塊進行 hello 下列選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![建立 Maven 專案](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="0f2ac-136">選取**Maven** hello 專案類型。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="0f2ac-137">指定 [專案 SDK] 。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="0f2ac-138">按一下 [新增] 並瀏覽 toohello Java 安裝目錄時，通常`C:\Program Files\Java\jdk1.8.0_66`。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="0f2ac-139">選取 hello**從原型建立**選項。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="0f2ac-140">從 hello archetypes 清單選取**org.scala tools.archetypes:scala 原型-簡單**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="0f2ac-141">這會建立 hello 正確的目錄結構，並下載所需的 hello 預設相依性 toowrite Scala 程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="0f2ac-142">為 [GroupId]、[ArtifactId] 和 [版本] 提供相關值。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="0f2ac-143">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-143">Click **Next**.</span></span>
3. <span data-ttu-id="0f2ac-144">Hello 下一步 對話方塊，讓您指定 Maven 主目錄及其他使用者設定，在接受 hello 預設值然後按**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="0f2ac-145">在 hello 最後一個對話方塊，指定專案名稱和位置，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="0f2ac-146">刪除 hello **MySpec.Scala**檔案**src\test\scala\com\microsoft\spark\example**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="0f2ac-147">您不需要這個 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="0f2ac-148">如有需要，重新命名 hello 預設來源和測試檔案。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="0f2ac-149">從 hello IntelliJ 概念 hello 左窗格，瀏覽過**src\main\scala\com.microsoft.spark.example**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="0f2ac-150">以滑鼠右鍵按一下**App.scala**，按一下 **重構**、 按一下 重新命名檔案，並在 hello 對話方塊中，提供 hello hello 應用程式的新名稱，然後按一下**重構**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![重新命名檔案](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="0f2ac-152">在 hello 後續步驟中，您將更新 hello pom.xml toodefine hello 相依性 hello Spark Scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="0f2ac-153">這些相依性 toobe 下載，並自動解決，您必須據此設定 Maven。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![設定 Maven 以進行自動下載](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="0f2ac-155">從 hello**檔案**功能表上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="0f2ac-156">在 hello**設定**對話方塊方塊中，瀏覽過**建置、 執行、 部署** > **建置工具** > **Maven** > **匯入**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="0f2ac-157">選取 hello 選項太**匯入 Maven 專案自動**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="0f2ac-158">按一下 套用，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="0f2ac-159">更新 hello Scala 來源檔案 tooinclude 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="0f2ac-160">開啟並取代現有範例程式碼以下列程式碼的 hello hello 並儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="0f2ac-161">此程式碼，讀取 hello hello HVAC.csv （可在所有的 HDInsight Spark 叢集上）、 擷取 hello hello 第六個資料行中只有一個數字的資料列和 hello 會將輸出寫入太**/HVACOut**下 hello 預設儲存體hello 叢集的容器。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
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
9. <span data-ttu-id="0f2ac-162">更新 hello pom.xml。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="0f2ac-163">內`<project>\<properties>`新增 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0f2ac-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="0f2ac-164">內`<project>\<dependencies>`新增 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0f2ac-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="0f2ac-165">儲存變更 toopom.xml。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="0f2ac-166">建立 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-166">Create hello .jar file.</span></span> <span data-ttu-id="0f2ac-167">IntelliJ IDEA 允許將 JAR 建立為專案的構件。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="0f2ac-168">執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="0f2ac-169">從 hello**檔案**功能表上，按一下 **專案結構**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="0f2ac-170">在 hello**專案結構**對話方塊中，按一下 **成品**hello 加上符號，然後按一下。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="0f2ac-171">Hello 快顯對話方塊方塊中，按一下  **JAR**，然後按一下**具有相依性的模組從**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="0f2ac-173">在 hello**從模組建立 JAR**對話方塊方塊中，按一下 hello 省略符號 (![省略](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) 針對 hello**主要類別**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="0f2ac-174">在 hello**選取主要類別**對話方塊中，依預設會出現，然後按一下選取 hello 類別**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="0f2ac-176">在 hello**從模組建立 JAR**對話方塊方塊中，請確定該 hello 選項太**擷取 toohello 目標 JAR**已選取，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="0f2ac-177">這會建立具有所有相依性的單一 JAR。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-177">This creates a single JAR with all dependencies.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="0f2ac-179">hello 輸出版面配置 索引標籤會列出所有 hello （每瓶） 的 hello Maven 專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="0f2ac-180">您可以選取和刪除 hello 所在的 hello Scala 應用程式並沒有直接相依。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="0f2ac-181">對於此建立 hello 應用程式，您可以移除以外的所有 hello 最後一個 (**SparkSimpleApp 編譯輸出**)。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="0f2ac-182">選取 hello （每瓶) toodelete，然後按一下hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="0f2ac-184">請確定**上進行建置**選取方塊，以確保每次建立或更新 hello 專案建立該 hello jar。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="0f2ac-185">依序按一下 [套用] 及 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="0f2ac-186">在 hello 功能表列中，按一下**建置**，然後按一下**進行專案**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="0f2ac-187">您也可以按一下**組建成品**toocreate hello jar。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="0f2ac-188">hello 輸出 jar 下方會建立**\out\artifacts**。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![建立 JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="0f2ac-190">Hello Spark 叢集上執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f2ac-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="0f2ac-191">hello 叢集上的 toorun hello 應用程式，您必須執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="0f2ac-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="0f2ac-192">**複製 hello 應用程式 jar toohello Azure 儲存體 blob** hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="0f2ac-193">您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式，toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="0f2ac-194">有很多其他用戶端以及您可以使用 tooupload 資料。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="0f2ac-195">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="0f2ac-196">**從遠端使用晚總 toosubmit 應用程式工作**toohello Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="0f2ac-197">HDInsight 上的 Spark 叢集包含晚總公開 REST 端點 tooremotely 送出 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="0f2ac-198">如需詳細資訊，請參閱 [搭配 HDInsight 上的 Spark 叢集利用 Livy 遠端提交 Spark 作業](hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="0f2ac-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f2ac-199">Next step</span></span>

<span data-ttu-id="0f2ac-200">在這個發行項您學到如何 toocreate Spark scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="0f2ac-201">進階 toohello 下一個發行項 toolearn 如何 toorun 這個應用程式的 HDInsight Spark 叢集使用晚總。</span><span class="sxs-lookup"><span data-stu-id="0f2ac-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="0f2ac-202">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="0f2ac-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

