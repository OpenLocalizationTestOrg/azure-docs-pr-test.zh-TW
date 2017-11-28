---
title: "適用於 IntelliJ 的 Azure 工具組：建立適用於 HDInsight 叢集的 Spark 應用程式 | Microsoft Docs"
description: "使用 hello Azure Toolkit IntelliJ toodevelop Spark 應用程式撰寫的 Scala，並將它們送出 tooan HDInsight Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="563ac-103">使用 Azure Toolkit 的 HDInsight 叢集的 IntelliJ toocreate Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="563ac-104">Hello Azure Toolkit 用於 Scala，以撰寫的 IntelliJ 外掛程式 toodevelop Spark 應用程式，然後將它們送出 tooan HDInsight Spark 叢集，直接從 hello IntelliJ 整合式的開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="563ac-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="563ac-105">您可以使用一些方式外掛程式 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="563ac-106">在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="563ac-107">存取您的 Azure HDInsight Spark 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="563ac-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="563ac-108">在本機開發並執行 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="563ac-109">toocreate 您專案中，檢視 hello[建立 Spark 應用程式以 hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)視訊。</span><span class="sxs-lookup"><span data-stu-id="563ac-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="563ac-110">您可以使用這個外掛程式 toocreate 並送出應用程式僅適用於 linux 的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="563ac-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="563ac-111">Prerequisites</span></span>

- <span data-ttu-id="563ac-112">HDInsight Linux 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="563ac-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="563ac-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="563ac-114">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="563ac-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="563ac-115">您可以將它安裝從 hello [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。</span><span class="sxs-lookup"><span data-stu-id="563ac-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="563ac-116">IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="563ac-116">IntelliJ IDEA.</span></span> <span data-ttu-id="563ac-117">本文章使用 2017.1 版。</span><span class="sxs-lookup"><span data-stu-id="563ac-117">This article uses version 2017.1.</span></span> <span data-ttu-id="563ac-118">您可以將它安裝從 hello [JetBrains 網站](https://www.jetbrains.com/idea/download/)。</span><span class="sxs-lookup"><span data-stu-id="563ac-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="563ac-119">安裝適用於 IntelliJ 的 Azure 工具組</span><span class="sxs-lookup"><span data-stu-id="563ac-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="563ac-120">如需安裝指示，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="563ac-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="563ac-121">登入 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="563ac-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="563ac-122">啟動 hello IntelliJ IDE，並開啟 Azure 總管。</span><span class="sxs-lookup"><span data-stu-id="563ac-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="563ac-123">在 hello**檢視**功能表上，選取**工具視窗**，然後選取**Azure 總管**。</span><span class="sxs-lookup"><span data-stu-id="563ac-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![hello Azure 總管連結](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="563ac-125">以滑鼠右鍵按一下 hello **Azure**節點，然後再選取**登入**。</span><span class="sxs-lookup"><span data-stu-id="563ac-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="563ac-126">在 hello **Azure 登入**對話方塊中，選取**登入**，然後輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="563ac-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![hello Azure 登入 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="563ac-128">您已登入之後，hello**選取的訂用帳戶**對話方塊方塊中列出所有 hello Azure 訂用帳戶相關聯 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="563ac-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="563ac-129">選取 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="563ac-129">Select hello **Select** button.</span></span>

    ![hello 選取多個訂閱對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="563ac-131">在 hello **Azure 總管**索引標籤上，依序展開**HDInsight** tooview hello HDInsight Spark 叢集，您的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="563ac-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="563ac-133">tooview hello （例如，儲存體帳戶） 相關聯的資源與 hello 叢集，您可以進一步展開叢集名稱節點。</span><span class="sxs-lookup"><span data-stu-id="563ac-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![展開的叢集名稱節點](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="563ac-135">在 HDInsight Spark 叢集上執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="563ac-136">啟動 IntelliJ IDEA，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="563ac-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="563ac-137">在 hello**新專案**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="563ac-138">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-138">a.</span></span> <span data-ttu-id="563ac-139">選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="563ac-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="563ac-140">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-140">b.</span></span> <span data-ttu-id="563ac-141">在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="563ac-142">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="563ac-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="563ac-143">**SBT**、 管理 hello 相依性和建置 hello Scala 專案</span><span class="sxs-lookup"><span data-stu-id="563ac-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="563ac-145">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="563ac-145">Select **Next**.</span></span>

3. <span data-ttu-id="563ac-146">hello Scala 專案建立精靈會自動偵測您的電腦已安裝的 hello Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="563ac-147">選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="563ac-147">Select **Install**.</span></span>

   ![Scala 外掛程式檢查](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="563ac-149">toodownload hello Scala 外掛程式，請選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="563ac-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="563ac-150">請遵循 hello 指示 toorestart IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="563ac-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![hello Scala 外掛程式安裝對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="563ac-152">在 hello**新的專案**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-152">In hello **New Project** window, do hello following:</span></span>  

    ![選取 hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="563ac-154">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-154">a.</span></span> <span data-ttu-id="563ac-155">輸入專案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="563ac-155">Enter a project name and location.</span></span>

   <span data-ttu-id="563ac-156">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-156">b.</span></span> <span data-ttu-id="563ac-157">在 hello**專案 SDK**下拉式清單中，選取**Java 1.8** hello Spark 2.x 叢集，或選取**Java 1.7** hello Spark 1.x 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="563ac-158">c.</span><span class="sxs-lookup"><span data-stu-id="563ac-158">c.</span></span> <span data-ttu-id="563ac-159">在 hello **Spark 版本**下拉式清單中，Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。</span><span class="sxs-lookup"><span data-stu-id="563ac-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="563ac-160">如果 hello Spark 叢集版本早於 2.0，請選取**二手 1.x**。</span><span class="sxs-lookup"><span data-stu-id="563ac-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="563ac-161">否則，請選取 [Spark2.x]。</span><span class="sxs-lookup"><span data-stu-id="563ac-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="563ac-162">此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。</span><span class="sxs-lookup"><span data-stu-id="563ac-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="563ac-163">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="563ac-163">Select **Finish**.</span></span>

7. <span data-ttu-id="563ac-164">hello Spark 專案會自動為您建立成品。</span><span class="sxs-lookup"><span data-stu-id="563ac-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="563ac-165">tooview hello 成品，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="563ac-166">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-166">a.</span></span> <span data-ttu-id="563ac-167">在 hello**檔案**功能表上，選取**專案結構**。</span><span class="sxs-lookup"><span data-stu-id="563ac-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="563ac-168">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-168">b.</span></span> <span data-ttu-id="563ac-169">在 hello**專案結構**對話方塊中，選取**成品**tooview hello 預設成品所建立。</span><span class="sxs-lookup"><span data-stu-id="563ac-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="563ac-170">您也可以藉由選取加號 hello 建立您自己的成品 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="563ac-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![在 [hello] 對話方塊中的成品資訊](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="563ac-172">執行 hello 下列新增您的應用程式的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="563ac-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="563ac-173">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-173">a.</span></span> <span data-ttu-id="563ac-174">在 [專案總管] 中，以滑鼠右鍵按一下**src**，點太**新增**，然後選取**Scala 類別**。</span><span class="sxs-lookup"><span data-stu-id="563ac-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![從 [專案總管] 中建立 Scala 類別的命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="563ac-176">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-176">b.</span></span> <span data-ttu-id="563ac-177">在 hello**建立類別的新 Scala**對話方塊方塊中，提供的名稱，選取**物件**在 hello**種類**方塊，並選取**[確定]**。</span><span class="sxs-lookup"><span data-stu-id="563ac-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![建立新的 Scala 類別對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="563ac-179">c.</span><span class="sxs-lookup"><span data-stu-id="563ac-179">c.</span></span> <span data-ttu-id="563ac-180">在 hello **MyClusterApp.scala**檔案中，貼上下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="563ac-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="563ac-181">hello 程式碼，讀取 hello HVAC.csv （可在所有的 HDInsight Spark 叢集上），擷取 hello 資料列只有一個數字 hello 第七個資料行都在 hello CSV 檔案中，並將 hello 輸出太**/HVACOut**下 hello 預設hello 叢集的儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="563ac-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="563ac-182">藉由 hello 下列 HDInsight Spark 叢集執行 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="563ac-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="563ac-183">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-183">a.</span></span> <span data-ttu-id="563ac-184">在 專案總管 hello 專案名稱，以滑鼠右鍵按一下，然後選取**提交 Spark 應用程式 tooHDInsight**。</span><span class="sxs-lookup"><span data-stu-id="563ac-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![hello 提交 Spark 應用程式 tooHDInsight 命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="563ac-186">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-186">b.</span></span> <span data-ttu-id="563ac-187">您會提示的 tooenter 您 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="563ac-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="563ac-188">在 hello **Spark 提交**對話方塊中，提供下列值的 hello，然後選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="563ac-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="563ac-189">如**二手叢集 (僅 Linux)**，選取 hello 想 toorun HDInsight Spark 叢集應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="563ac-190">Hello IntelliJ 專案，從選取的成品，或選取從 hello 硬碟機。</span><span class="sxs-lookup"><span data-stu-id="563ac-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="563ac-191">在 hello**主要類別名稱**方塊中，選取 hello 省略符號 (**...**) 應用程式程式碼中，選取 hello 主要類別，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="563ac-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![hello 選取主要類別對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="563ac-193">因為在此範例中的 hello 應用程式程式碼不需要命令列引數或參考 （每瓶） 或檔案，您可以保留 hello 剩餘空白的方塊。</span><span class="sxs-lookup"><span data-stu-id="563ac-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="563ac-194">提供所有 hello 資訊之後，hello 對話方塊看起來應該像 hello 下列映像。</span><span class="sxs-lookup"><span data-stu-id="563ac-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![hello Spark 提交對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="563ac-196">c.</span><span class="sxs-lookup"><span data-stu-id="563ac-196">c.</span></span> <span data-ttu-id="563ac-197">hello **Spark 提交**在 hello hello 視窗底部的索引標籤應該開始顯示 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="563ac-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="563ac-198">您也可以停止 hello 應用程式藉由選取 hello 紅色按鈕在 hello **Spark 提交**視窗。</span><span class="sxs-lookup"><span data-stu-id="563ac-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![hello Spark 提交視窗](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="563ac-200">toolearn 如何 tooaccess hello 作業輸出，請參閱 hello 」 存取和管理 HDInsight Spark 叢集，請使用 Azure Toolkit for IntelliJ"本文中稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="563ac-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="563ac-201">在 HDInsight Spark 叢集上執行或偵錯 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="563ac-202">我們也建議送出 hello Spark 應用程式 toohello 叢集的另一種。</span><span class="sxs-lookup"><span data-stu-id="563ac-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="563ac-203">您可以藉由設定 hello 參數在 hello**執行/偵錯組態**IDE。</span><span class="sxs-lookup"><span data-stu-id="563ac-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="563ac-204">如需詳細資訊，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。</span><span class="sxs-lookup"><span data-stu-id="563ac-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="563ac-205">使用適用於 IntelliJ 的 Azure 工具組來存取和管理 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="563ac-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="563ac-206">您可以使用適用於 IntelliJ 的 Azure 工具組來執行各種作業。</span><span class="sxs-lookup"><span data-stu-id="563ac-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="563ac-207">存取 hello 工作檢視</span><span class="sxs-lookup"><span data-stu-id="563ac-207">Access hello job view</span></span>
1. <span data-ttu-id="563ac-208">在 Azure 總管] 中，依序展開**HDInsight**，依序展開 [hello Spark 叢集名稱，然後選取**作業**。</span><span class="sxs-lookup"><span data-stu-id="563ac-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="563ac-210">Hello 右窗格中，hello **Spark 工作檢視**索引標籤會顯示 hello 叢集所執行的所有 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="563ac-211">選取 hello hello 要 toosee 更多詳細資料的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="563ac-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="563ac-213">toodisplay 基本執行作業資訊暫留在 hello 作業圖形。</span><span class="sxs-lookup"><span data-stu-id="563ac-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="563ac-214">tooview hello 階段圖形和資訊所產生的每個工作，請選取 hello 作業圖形的節點。</span><span class="sxs-lookup"><span data-stu-id="563ac-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="563ac-216">tooview 常用的記錄檔，例如*驅動程式 Stderr*，*驅動程式 Stdout*，和*目錄資訊*，選取 hello**記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="563ac-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="563ac-218">您也可以選取 hello hello 視窗上方的連結，檢視 hello Spark 記錄 UI 和 hello YARN UI （hello 應用程式層級）。</span><span class="sxs-lookup"><span data-stu-id="563ac-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="563ac-219">存取 hello Spark 記錄伺服器</span><span class="sxs-lookup"><span data-stu-id="563ac-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="563ac-220">在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。</span><span class="sxs-lookup"><span data-stu-id="563ac-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="563ac-221">當提示您時，請輸入 hello 叢集系統管理員認證，您可以指定當您設定 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="563ac-222">Hello Spark 記錄伺服器儀表板上，您可以使用 hello 應用程式名稱 toolook hello 剛剛完成執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="563ac-223">在上述程式碼的 hello，您必須設定 hello 應用程式名稱使用`val conf = new SparkConf().setAppName("MyClusterApp")`。</span><span class="sxs-lookup"><span data-stu-id="563ac-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="563ac-224">因此，Spark 應用程式名稱為 **MyClusterApp**。</span><span class="sxs-lookup"><span data-stu-id="563ac-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="563ac-225">啟動 hello Ambari 入口網站</span><span class="sxs-lookup"><span data-stu-id="563ac-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="563ac-226">在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。</span><span class="sxs-lookup"><span data-stu-id="563ac-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="563ac-227">當提示您時，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="563ac-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="563ac-228">您可以指定這些認證 hello 叢集安裝程序期間。</span><span class="sxs-lookup"><span data-stu-id="563ac-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="563ac-229">管理 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="563ac-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="563ac-230">根據預設，Azure Toolkit for IntelliJ 會列出所有您 Azure 訂用帳戶的 hello Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="563ac-231">如有必要，您可以指定您想 tooaccess hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="563ac-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="563ac-232">在 Azure 總管 中，以滑鼠右鍵按一下 hello **Azure**根節點，然後再選取**管理訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="563ac-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="563ac-233">在 [hello] 對話方塊中，清除 hello 核取方塊下一步 toohello 訂用帳戶，您不想 tooaccess，，然後選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="563ac-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="563ac-234">您也可以選取**登出**如果想要從您的 Azure 訂用帳戶的 toosign。</span><span class="sxs-lookup"><span data-stu-id="563ac-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="563ac-235">在本機執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="563ac-236">您的工作站上，您可以在本機使用 Azure Toolkit IntelliJ toorun Spark Scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="563ac-237">hello 應用程式通常不需要存取 toocluster 資源，例如儲存體容器，您可以執行和測試它們，在本機。</span><span class="sxs-lookup"><span data-stu-id="563ac-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="563ac-238">必要條件</span><span class="sxs-lookup"><span data-stu-id="563ac-238">Prerequisite</span></span>
<span data-ttu-id="563ac-239">雖然您在 Windows 電腦上執行 hello 本機 Spark Scala 應用程式，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)。</span><span class="sxs-lookup"><span data-stu-id="563ac-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="563ac-240">因為 WinUtils.exe 遺漏 Windows 上，就會發生 hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="563ac-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="563ac-241">tooresolve 這個錯誤，[下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置，如**C:\WinUtils\bin**。</span><span class="sxs-lookup"><span data-stu-id="563ac-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="563ac-242">接著，新增 hello 環境變數**HADOOP_HOME**，並設定 hello hello 變數值太**C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="563ac-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="563ac-243">執行本機 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="563ac-244">啟動 IntelliJ IDEA 並建立專案。</span><span class="sxs-lookup"><span data-stu-id="563ac-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="563ac-245">在 hello**新專案**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="563ac-246">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-246">a.</span></span> <span data-ttu-id="563ac-247">選取 [HDInsight] > [HDInsight 上的 Spark 本機執行範例 (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="563ac-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="563ac-248">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-248">b.</span></span> <span data-ttu-id="563ac-249">在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="563ac-250">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="563ac-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="563ac-251">**SBT**、 管理 hello 相依性和建置 hello Scala 專案</span><span class="sxs-lookup"><span data-stu-id="563ac-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="563ac-253">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="563ac-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="563ac-254">在 hello 下一步 視窗中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="563ac-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="563ac-255">a.</span><span class="sxs-lookup"><span data-stu-id="563ac-255">a.</span></span> <span data-ttu-id="563ac-256">輸入專案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="563ac-256">Enter a project name and location.</span></span>

    <span data-ttu-id="563ac-257">b.</span><span class="sxs-lookup"><span data-stu-id="563ac-257">b.</span></span> <span data-ttu-id="563ac-258">在 hello**專案 SDK**下拉式清單中，選取晚於 1.7 版的 Java 版本。</span><span class="sxs-lookup"><span data-stu-id="563ac-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="563ac-259">c.</span><span class="sxs-lookup"><span data-stu-id="563ac-259">c.</span></span> <span data-ttu-id="563ac-260">在 hello **Spark 版本**下拉式清單中，您想 toouse Scala 選取 hello 版本： Scala Spark 2.0 或 Scala 2.11.x Spark 1.6 的 2.10.x。</span><span class="sxs-lookup"><span data-stu-id="563ac-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![hello 新增專案 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="563ac-262">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="563ac-262">Select **Finish**.</span></span>

6. <span data-ttu-id="563ac-263">hello 範本加入程式碼範例 (**LogQuery**) 下 hello **src**您可以在本機執行您的電腦的資料夾。</span><span class="sxs-lookup"><span data-stu-id="563ac-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="563ac-265">以滑鼠右鍵按一下 hello **LogQuery**應用程式，然後再選取**執行 'LogQuery'**。</span><span class="sxs-lookup"><span data-stu-id="563ac-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="563ac-266">在 [hello**執行**] 索引標籤底部 hello，您會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="563ac-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="563ac-268">轉換現有 IntelliJ 概念應用程式 toouse Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="563ac-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="563ac-269">您可以將轉換 hello 現有 Spark Scala 建立應用程式 IntelliJ 概念 toobe 中與 Azure Toolkit for IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="563ac-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="563ac-270">然後，您可以使用 hello 外掛程式 toosubmit hello 應用程式 tooan HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="563ac-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="563ac-271">針對現有的 Spark Scala 應用程式建立透過 IntelliJ 概念，開啟 hello 相關聯的.iml 檔案。</span><span class="sxs-lookup"><span data-stu-id="563ac-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="563ac-272">在 hello 根層級是**模組**hello 如下的項目：</span><span class="sxs-lookup"><span data-stu-id="563ac-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="563ac-273">編輯 hello 元素 tooadd`UniqueKey="HDInsightTool"`因此的 hello**模組**項目看起來類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="563ac-274">儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="563ac-274">Save hello changes.</span></span> <span data-ttu-id="563ac-275">您的應用程式現在應該可與適用於 IntelliJ 的 Azure 工具組相容。</span><span class="sxs-lookup"><span data-stu-id="563ac-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="563ac-276">您可以測試它，以滑鼠右鍵按一下 [專案總管] 中的 hello 專案名稱。</span><span class="sxs-lookup"><span data-stu-id="563ac-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="563ac-277">hello 快顯功能表現在具有 hello 選項**提交 Spark 應用程式 tooHDInsight**。</span><span class="sxs-lookup"><span data-stu-id="563ac-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="563ac-278">疑難排解</span><span class="sxs-lookup"><span data-stu-id="563ac-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="563ac-279">本機執行的錯誤：「請使用較大的堆積大小」</span><span class="sxs-lookup"><span data-stu-id="563ac-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="563ac-280">中的 Spark 1.6，如果您在本機執行，使用 32 位元 Java SDK 可能會遇到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="563ac-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="563ac-281">因為不是大型的 Spark toorun hello 堆積的大小，則會發生這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="563ac-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="563ac-282">Spark 需要至少 471 MB</span><span class="sxs-lookup"><span data-stu-id="563ac-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="563ac-283">(如需詳細資訊，請參閱 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081))。一個簡單的解決方案是 toouse 64 位元 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="563ac-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="563ac-284">您也可以藉由新增下列選項的 hello 變更 IntelliJ hello JVM 設定：</span><span class="sxs-lookup"><span data-stu-id="563ac-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![加入選項 toohello 方塊 IntelliJ 中的 「 VM 選項 」](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="563ac-286">常見問題集</span><span class="sxs-lookup"><span data-stu-id="563ac-286">FAQ</span></span>
<span data-ttu-id="563ac-287">應用程式 tooAzure 資料湖存放區，toosubmit 選擇**互動式**hello Azure 登入程序期間的模式。</span><span class="sxs-lookup"><span data-stu-id="563ac-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="563ac-288">如果您選取 [自動] 模式，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="563ac-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="563ac-290">現在，我們已解決了。</span><span class="sxs-lookup"><span data-stu-id="563ac-290">Now, we resolved it.</span></span> <span data-ttu-id="563ac-291">您可以使用任何登入方法選擇 Azure 資料湖叢集 toosubmit 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="563ac-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="563ac-292">意見反應和已知問題</span><span class="sxs-lookup"><span data-stu-id="563ac-292">Feedback and known issues</span></span>
<span data-ttu-id="563ac-293">目前，不支援直接檢視 Spark 輸出。</span><span class="sxs-lookup"><span data-stu-id="563ac-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="563ac-294">如果您有任何建議或意見反應，或使用此外掛程式時遇到任何問題，請將電子郵件傳送到 hdivstool@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="563ac-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="563ac-295"><a name="seealso"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="563ac-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="563ac-296">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="563ac-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="563ac-297">示範</span><span class="sxs-lookup"><span data-stu-id="563ac-297">Demo</span></span>
* <span data-ttu-id="563ac-298">建立 Scala 專案 (影片)：[Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (建立 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="563ac-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="563ac-299">遠端偵錯 （影片）：[使用 Azure Toolkit for IntelliJ toodebug Spark 應用程式，從遠端在 HDInsight 叢集上](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="563ac-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="563ac-300">案例</span><span class="sxs-lookup"><span data-stu-id="563ac-300">Scenarios</span></span>
* [<span data-ttu-id="563ac-301">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="563ac-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="563ac-302">機器學習的 Spark： 使用 HDInsight tooanalyze 建置溫度使用 HVAC 資料中的 Spark</span><span class="sxs-lookup"><span data-stu-id="563ac-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="563ac-303">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="563ac-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="563ac-304">HDInsight toobuild 即時串流應用程式中的 Spark Streaming： 使用 Spark</span><span class="sxs-lookup"><span data-stu-id="563ac-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="563ac-305">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="563ac-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="563ac-306">建立和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-306">Creating and running applications</span></span>
* [<span data-ttu-id="563ac-307">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="563ac-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="563ac-308">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="563ac-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="563ac-309">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="563ac-309">Tools and extensions</span></span>
* [<span data-ttu-id="563ac-310">IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="563ac-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="563ac-311">透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="563ac-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="563ac-312">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="563ac-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="563ac-313">在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="563ac-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="563ac-314">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="563ac-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="563ac-315">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="563ac-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="563ac-316">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="563ac-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="563ac-317">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="563ac-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="563ac-318">管理資源</span><span class="sxs-lookup"><span data-stu-id="563ac-318">Managing resources</span></span>
* [<span data-ttu-id="563ac-319">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="563ac-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="563ac-320">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="563ac-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

