---
title: "適用於 IntelliJ 的 Azure 工具組：建立適用於 HDInsight 叢集的 Spark 應用程式 | Microsoft Docs"
description: "使用適用於 IntelliJ 的 Azure 工具組來開發以 Scala 撰寫的 Spark 應用程式，並將它們提交到 HDInsight Spark 叢集。"
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="56ea8-103">使用適用於 IntelliJ 的 Azure 工具組建立適用於 HDInsight 叢集的 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="56ea8-104">使用適用於 IntelliJ 外掛程式的 Azure 工具組來開發以 Scala 撰寫的 Spark 應用程式，然後直接從 IntelliJ 整合式開發環境 (IDE) 將它們提交到 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="56ea8-105">您可以利用數個方式來使用此外掛程式：</span><span class="sxs-lookup"><span data-stu-id="56ea8-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="56ea8-106">在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="56ea8-107">存取您的 Azure HDInsight Spark 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="56ea8-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="56ea8-108">在本機開發並執行 Scala Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="56ea8-109">若要建立您的專案，請觀看 [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (使用適用於 IntelliJ 的 Azure 工具組建立 Spark 應用程式) 影片。</span><span class="sxs-lookup"><span data-stu-id="56ea8-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56ea8-110">您可以使用此外掛程式僅針對 Linux 上的 HDInsight Spark 叢集建立並提交應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="56ea8-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="56ea8-111">Prerequisites</span></span>

- <span data-ttu-id="56ea8-112">HDInsight Linux 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="56ea8-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="56ea8-114">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="56ea8-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="56ea8-115">您可以從 [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下載。</span><span class="sxs-lookup"><span data-stu-id="56ea8-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="56ea8-116">IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="56ea8-116">IntelliJ IDEA.</span></span> <span data-ttu-id="56ea8-117">本文章使用 2017.1 版。</span><span class="sxs-lookup"><span data-stu-id="56ea8-117">This article uses version 2017.1.</span></span> <span data-ttu-id="56ea8-118">您可以從 [JetBrains 網站](https://www.jetbrains.com/idea/download/)下載。</span><span class="sxs-lookup"><span data-stu-id="56ea8-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="56ea8-119">安裝適用於 IntelliJ 的 Azure 工具組</span><span class="sxs-lookup"><span data-stu-id="56ea8-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="56ea8-120">如需安裝指示，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="56ea8-121">登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="56ea8-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="56ea8-122">啟動 IntelliJ IDE，然後開啟 [Azure Explorer]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="56ea8-123">在 [檢視] 功能表上，選取 [工具視窗]，然後選取 [Azure Explorer]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![[Azure Explorer] 連結](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="56ea8-125">以滑鼠右鍵按一下 [Azure] 節點，然後選取 [登入]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="56ea8-126">在 [Azure 登入] 對話方塊中，選取 [登入]，然後輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="56ea8-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![[Azure 登入] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="56ea8-128">登入之後，[選取訂用帳戶] 對話方塊會列出與認證建立關聯的所有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56ea8-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="56ea8-129">選取 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56ea8-129">Select the **Select** button.</span></span>

    ![[選取訂用帳戶] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="56ea8-131">在 [Azure Explorer] 索引標籤中展開 [HDInsight]，可檢視您訂用帳戶中的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="56ea8-133">若要檢視與叢集建立關聯的資源 (例如儲存體帳戶)，您可以進一步展開叢集名稱節點。</span><span class="sxs-lookup"><span data-stu-id="56ea8-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![展開的叢集名稱節點](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="56ea8-135">在 HDInsight Spark 叢集上執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="56ea8-136">啟動 IntelliJ IDEA，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="56ea8-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="56ea8-137">在 [新增專案]  對話方塊中，執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="56ea8-138">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-138">a.</span></span> <span data-ttu-id="56ea8-139">選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="56ea8-140">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-140">b.</span></span> <span data-ttu-id="56ea8-141">在 [建置工具] 清單中，根據您的需求選取下列任一項目：</span><span class="sxs-lookup"><span data-stu-id="56ea8-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="56ea8-142">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="56ea8-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="56ea8-143">**SBT**，以管理相依性並建置 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="56ea8-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![[新增專案] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="56ea8-145">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="56ea8-145">Select **Next**.</span></span>

3. <span data-ttu-id="56ea8-146">Scala 專案建立精靈會自動偵測您是否已安裝 Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="56ea8-147">選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-147">Select **Install**.</span></span>

   ![Scala 外掛程式檢查](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="56ea8-149">若要下載 Scala 外掛程式，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="56ea8-150">依指示重新啟動 IntelliJ。</span><span class="sxs-lookup"><span data-stu-id="56ea8-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Scala 外掛程式安裝對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="56ea8-152">在 [新增專案] 視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-152">In the **New Project** window, do the following:</span></span>  

    ![選取 Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="56ea8-154">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-154">a.</span></span> <span data-ttu-id="56ea8-155">輸入專案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="56ea8-155">Enter a project name and location.</span></span>

   <span data-ttu-id="56ea8-156">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-156">b.</span></span> <span data-ttu-id="56ea8-157">在 [專案 SDK] 下拉式清單中，選取 [Java 1.8] \(適用於 Spark 2.x 叢集)，或選取 [Java 1.7] \(適用於 Spark 1.x 叢集)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="56ea8-158">c.</span><span class="sxs-lookup"><span data-stu-id="56ea8-158">c.</span></span> <span data-ttu-id="56ea8-159">在 [Spark 版本] 下拉式清單中，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。</span><span class="sxs-lookup"><span data-stu-id="56ea8-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="56ea8-160">如果 Spark 叢集是 2.0 以前的版本，請選取 [Spark 1.x]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="56ea8-161">否則，請選取 [Spark2.x]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="56ea8-162">此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。</span><span class="sxs-lookup"><span data-stu-id="56ea8-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="56ea8-163">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-163">Select **Finish**.</span></span>

7. <span data-ttu-id="56ea8-164">Spark 專案會自動為您建立構件。</span><span class="sxs-lookup"><span data-stu-id="56ea8-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="56ea8-165">若要檢視構件，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="56ea8-166">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-166">a.</span></span> <span data-ttu-id="56ea8-167">在 [檔案] 功能表上，選取 [專案結構]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="56ea8-168">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-168">b.</span></span> <span data-ttu-id="56ea8-169">在 [專案結構] 對話方塊中，選取 [構件]，以檢視建立的預設構件。</span><span class="sxs-lookup"><span data-stu-id="56ea8-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="56ea8-170">您也可以建立自己的構件，方法是選取加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![對話方塊中的構件資訊](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="56ea8-172">若要新增應用程式的原始程式碼，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="56ea8-173">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-173">a.</span></span> <span data-ttu-id="56ea8-174">在專案總管中，以滑鼠右鍵按一下 [src]、指向 [新增]，然後選取 [Scala 類別]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![從 [專案總管] 中建立 Scala 類別的命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="56ea8-176">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-176">b.</span></span> <span data-ttu-id="56ea8-177">在 [建立新的 Scala 類別] 對話方塊中，提供一個名稱，並在 [種類] 方塊中選取 [物件]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![建立新的 Scala 類別對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="56ea8-179">c.</span><span class="sxs-lookup"><span data-stu-id="56ea8-179">c.</span></span> <span data-ttu-id="56ea8-180">在 **MyClusterApp.scala** 檔案中，貼入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="56ea8-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="56ea8-181">此程式碼會從 HVAC.csv (所有 HDInsight Spark 叢集上均提供) 讀取資料、擷取在 CSV 檔案的第七個資料行中只有一個位數的資料列，並將輸出寫入叢集預設儲存體容器下的 **/HVACOut** 。</span><span class="sxs-lookup"><span data-stu-id="56ea8-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="56ea8-182">若要在 HDInsight Spark 叢集上執行應用程式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="56ea8-183">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-183">a.</span></span> <span data-ttu-id="56ea8-184">在 [專案總管] 中，以滑鼠右鍵按一下專案名稱，然後選取 [將 Spark 應用程式提交給 HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![[將 Spark 應用程式提交給 HDInsight] 命令](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="56ea8-186">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-186">b.</span></span> <span data-ttu-id="56ea8-187">系統會提示您輸入 Azure 訂用帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="56ea8-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="56ea8-188">在 [提交 Spark] 對話方塊中，提供下列值，然後選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="56ea8-189">針對 [Spark clusters (Linux only) (Spark 叢集 (僅限 Linux))] ，選取您要在其上執行應用程式的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="56ea8-190">從 IntelliJ 專案中選取構件，或從硬碟中選取一個。</span><span class="sxs-lookup"><span data-stu-id="56ea8-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="56ea8-191">在 [主要類別名稱] 方塊中，選取省略符號 (**...**)，並在應用程式的原始程式碼中選取主要類別，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![[選取主要類別] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="56ea8-193">此範例中的應用程式程式碼不需要命令列引數或是參考 JAR 或檔案，因此您可以將其餘的方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="56ea8-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="56ea8-194">提供所有資訊之後，對話方塊應該如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="56ea8-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![[提交 Spark] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="56ea8-196">c.</span><span class="sxs-lookup"><span data-stu-id="56ea8-196">c.</span></span> <span data-ttu-id="56ea8-197">視窗底部的 [Spark Submission (提交 Spark)]  索引標籤應會開始顯示進度。</span><span class="sxs-lookup"><span data-stu-id="56ea8-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="56ea8-198">您也可以選取 [提交 Spark] 視窗中的紅色按鈕，即可將應用程式停止。</span><span class="sxs-lookup"><span data-stu-id="56ea8-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![[提交 Spark] 視窗](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="56ea8-200">若要了解如何存取作業輸出，請參閱本文稍後的＜使用適用於 IntelliJ 的 Azure 工具組來存取和管理 HDInsight Spark 叢集＞一節。</span><span class="sxs-lookup"><span data-stu-id="56ea8-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="56ea8-201">在 HDInsight Spark 叢集上執行或偵錯 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="56ea8-202">我們也建議另一種將 Spark 應用程式提交至叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="56ea8-203">做法是在 [執行/偵錯設定] IDE 中設定參數。</span><span class="sxs-lookup"><span data-stu-id="56ea8-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="56ea8-204">如需詳細資訊，請參閱[使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="56ea8-205">使用適用於 IntelliJ 的 Azure 工具組來存取和管理 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="56ea8-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="56ea8-206">您可以使用適用於 IntelliJ 的 Azure 工具組來執行各種作業。</span><span class="sxs-lookup"><span data-stu-id="56ea8-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="56ea8-207">存取作業檢視</span><span class="sxs-lookup"><span data-stu-id="56ea8-207">Access the job view</span></span>
1. <span data-ttu-id="56ea8-208">在 [Azure Explorer] 中，依序展開 [HDInsight] 和 Spark 叢集名稱，然後選取 [作業]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="56ea8-210">在右窗格中，[Spark 作業檢視]  索引標籤會顯示已在叢集上執行的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="56ea8-211">選取您想要查看更多詳細資料的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="56ea8-211">Select the name of the application for which you want to see more details.</span></span>

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="56ea8-213">若要顯示基本的執行作業資訊，請將滑鼠停留在作業圖形上。</span><span class="sxs-lookup"><span data-stu-id="56ea8-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="56ea8-214">若要檢視每項作業產生的階段圖形和資訊，請選取作業圖形上的節點。</span><span class="sxs-lookup"><span data-stu-id="56ea8-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="56ea8-216">若要檢視經常使用的記錄 (例如「驅動程式 Stderr」、「驅動程式 Stdout」和「目錄資訊」)，請選取 [記錄] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="56ea8-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="56ea8-218">您也可以選取視窗頂端的連結，在應用程式層級檢視 Spark 歷程記錄 UI 和 YARN UI。</span><span class="sxs-lookup"><span data-stu-id="56ea8-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="56ea8-219">存取 Spark 歷程記錄伺服器</span><span class="sxs-lookup"><span data-stu-id="56ea8-219">Access the Spark history server</span></span>
1. <span data-ttu-id="56ea8-220">在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="56ea8-221">出現提示時，輸入叢集的系統管理員認證，也就是您在設定叢集時所指定的認證。</span><span class="sxs-lookup"><span data-stu-id="56ea8-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="56ea8-222">在 [Spark 歷程記錄伺服器] 儀表板上，您可以使用應用程式名稱，尋找您剛完成執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="56ea8-223">在上述程式碼中，您可以使用 `val conf = new SparkConf().setAppName("MyClusterApp")`來設定應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="56ea8-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="56ea8-224">因此，Spark 應用程式名稱為 **MyClusterApp**。</span><span class="sxs-lookup"><span data-stu-id="56ea8-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="56ea8-225">啟動 Ambari 入口網站</span><span class="sxs-lookup"><span data-stu-id="56ea8-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="56ea8-226">在 [Azure Explorer] 中，展開 [HDInsight]、以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="56ea8-227">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="56ea8-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="56ea8-228">您在叢集設定程序期間已指定這些認證。</span><span class="sxs-lookup"><span data-stu-id="56ea8-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="56ea8-229">管理 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56ea8-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="56ea8-230">根據預設，適用於 IntelliJ 的 Azure 工具組會列出您所有 Azure 訂用帳戶中的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="56ea8-231">如有必要，您可以指定要存取的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56ea8-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="56ea8-232">在 [Azure Explorer] 中，以滑鼠右鍵按一下 [Azure] 根節點，然後選取 [管理訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="56ea8-233">在對話方塊中，清除您不想要存取之訂用帳戶旁的核取方塊，然後選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="56ea8-234">如果您想要登出 Azure 訂用帳戶，也可以選取 [登出]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="56ea8-235">在本機執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="56ea8-236">您可以使用適用於 IntelliJ 的 Azure 工具組，在工作站上本機執行 Spark Scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="56ea8-237">這些應用程式通常不需要存取叢集資源 (例如儲存體容器)，而且您可在本機上執行並測試。</span><span class="sxs-lookup"><span data-stu-id="56ea8-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="56ea8-238">必要條件</span><span class="sxs-lookup"><span data-stu-id="56ea8-238">Prerequisite</span></span>
<span data-ttu-id="56ea8-239">在 Windows 電腦上執行本機 Spark Scala 應用程式時，可能會發生如 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) 中所述的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="56ea8-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="56ea8-240">發生這個例外狀況是因為 Windows 上遺失 WinUtils.exe。</span><span class="sxs-lookup"><span data-stu-id="56ea8-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="56ea8-241">若要解決這個錯誤，請[下載可執行檔](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)，並將其放在 **C:\WinUtils\bin** 之類的位置。</span><span class="sxs-lookup"><span data-stu-id="56ea8-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="56ea8-242">然後，新增環境變數 **HADOOP_HOME**，並將變數的值設為 **C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="56ea8-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="56ea8-243">執行本機 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="56ea8-244">啟動 IntelliJ IDEA 並建立專案。</span><span class="sxs-lookup"><span data-stu-id="56ea8-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="56ea8-245">在 [新增專案]  對話方塊中，執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="56ea8-246">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-246">a.</span></span> <span data-ttu-id="56ea8-247">選取 [HDInsight] > [HDInsight 上的 Spark 本機執行範例 (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="56ea8-248">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-248">b.</span></span> <span data-ttu-id="56ea8-249">在 [建置工具] 清單中，根據您的需求選取下列任一項目：</span><span class="sxs-lookup"><span data-stu-id="56ea8-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="56ea8-250">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="56ea8-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="56ea8-251">**SBT**，以管理相依性並建置 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="56ea8-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![[新增專案] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="56ea8-253">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="56ea8-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="56ea8-254">在下一個視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="56ea8-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="56ea8-255">a.</span><span class="sxs-lookup"><span data-stu-id="56ea8-255">a.</span></span> <span data-ttu-id="56ea8-256">輸入專案名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="56ea8-256">Enter a project name and location.</span></span>

    <span data-ttu-id="56ea8-257">b.</span><span class="sxs-lookup"><span data-stu-id="56ea8-257">b.</span></span> <span data-ttu-id="56ea8-258">在 [專案 SDK] 下拉式清單中，選取 1.7 版以後的 Java 版本。</span><span class="sxs-lookup"><span data-stu-id="56ea8-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="56ea8-259">c.</span><span class="sxs-lookup"><span data-stu-id="56ea8-259">c.</span></span> <span data-ttu-id="56ea8-260">在 [Spark 版本] 下拉式清單中，選取您想要使用的 Scala 版本：Scala 2.11.x (適用於 Spark 2.0) 或 Scala 2.10.x (適用於 Spark 1.6)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![[新增專案] 對話方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="56ea8-262">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="56ea8-262">Select **Finish**.</span></span>

6. <span data-ttu-id="56ea8-263">範本會在 **src** 資料夾下方新增可在電腦本機執行的程式碼範例 (**LogQuery**)。</span><span class="sxs-lookup"><span data-stu-id="56ea8-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="56ea8-265">以滑鼠右鍵按一下 [LogQuery] 應用程式，然後選取 [執行 'LogQuery']。</span><span class="sxs-lookup"><span data-stu-id="56ea8-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="56ea8-266">您會在底部的 [執行] 索引標籤上看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="56ea8-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="56ea8-268">轉換現有的 IntelliJ IDEA 應用程式，來使用適用於 IntelliJ 的 Azure 工具組</span><span class="sxs-lookup"><span data-stu-id="56ea8-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="56ea8-269">您可以將 IntelliJ IDEA 中建立的現有 Spark Scala 應用程式轉換成與適用於 IntelliJ 的 Azure 工具組相容。</span><span class="sxs-lookup"><span data-stu-id="56ea8-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="56ea8-270">然後您可以使用外掛程式，將應用程式提交給 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="56ea8-271">對於透過 IntelliJ IDEA 建立的現有 Spark Scala 應用程式，請開啟關聯的 .iml 檔案。</span><span class="sxs-lookup"><span data-stu-id="56ea8-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="56ea8-272">根層級中有 **module** 項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="56ea8-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="56ea8-273">編輯該元素以加入 `UniqueKey="HDInsightTool"` ，使 **module** 元素看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="56ea8-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="56ea8-274">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="56ea8-274">Save the changes.</span></span> <span data-ttu-id="56ea8-275">您的應用程式現在應該可與適用於 IntelliJ 的 Azure 工具組相容。</span><span class="sxs-lookup"><span data-stu-id="56ea8-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="56ea8-276">您可以滑鼠右鍵按一下 [專案總管] 中的專案名稱來進行測試。</span><span class="sxs-lookup"><span data-stu-id="56ea8-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="56ea8-277">現在，快顯功能表提供 [將 Spark 應用程式提交給 HDInsight] 的選項。</span><span class="sxs-lookup"><span data-stu-id="56ea8-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="56ea8-278">疑難排解</span><span class="sxs-lookup"><span data-stu-id="56ea8-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="56ea8-279">本機執行的錯誤：「請使用較大的堆積大小」</span><span class="sxs-lookup"><span data-stu-id="56ea8-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="56ea8-280">在 Spark 1.6 中，如果您在本機執行期間是使用 32 位元的 Java SDK，可能會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="56ea8-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="56ea8-281">會發生這些錯誤是因為堆積大小不足，使 Spark 無法執行。</span><span class="sxs-lookup"><span data-stu-id="56ea8-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="56ea8-282">Spark 需要至少 471 MB</span><span class="sxs-lookup"><span data-stu-id="56ea8-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="56ea8-283">(如需詳細資訊，請參閱 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081))。其中一個簡單的解決方案就是使用 64 位元的 Java SDK。</span><span class="sxs-lookup"><span data-stu-id="56ea8-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="56ea8-284">您也可以新增下列選項來變更 IntelliJ 中的 JVM 設定：</span><span class="sxs-lookup"><span data-stu-id="56ea8-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![IntelliJ 中的將選項新增至 [VM 選項] 方塊](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="56ea8-286">常見問題集</span><span class="sxs-lookup"><span data-stu-id="56ea8-286">FAQ</span></span>
<span data-ttu-id="56ea8-287">若要將應用程式提交至 Azure Data Lake Store，請在 Azure 登入程序期間，選擇 [互動] 模式。</span><span class="sxs-lookup"><span data-stu-id="56ea8-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="56ea8-288">如果您選取 [自動] 模式，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="56ea8-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="56ea8-290">現在，我們已解決了。</span><span class="sxs-lookup"><span data-stu-id="56ea8-290">Now, we resolved it.</span></span> <span data-ttu-id="56ea8-291">您可以選擇要使用任何登入方法提交您應用程式的 Azure Data Lake 叢集。</span><span class="sxs-lookup"><span data-stu-id="56ea8-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="56ea8-292">意見反應和已知問題</span><span class="sxs-lookup"><span data-stu-id="56ea8-292">Feedback and known issues</span></span>
<span data-ttu-id="56ea8-293">目前，不支援直接檢視 Spark 輸出。</span><span class="sxs-lookup"><span data-stu-id="56ea8-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="56ea8-294">如果您有任何建議或意見反應，或使用此外掛程式時遇到任何問題，請將電子郵件傳送到 hdivstool@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="56ea8-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="56ea8-295"><a name="seealso"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="56ea8-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="56ea8-296">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="56ea8-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="56ea8-297">示範</span><span class="sxs-lookup"><span data-stu-id="56ea8-297">Demo</span></span>
* <span data-ttu-id="56ea8-298">建立 Scala 專案 (影片)：[Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (建立 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="56ea8-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="56ea8-299">遠端偵錯 (影片)：[Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (使用適用於 IntelliJ 的 Azure 工具組對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯)</span><span class="sxs-lookup"><span data-stu-id="56ea8-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="56ea8-300">案例</span><span class="sxs-lookup"><span data-stu-id="56ea8-300">Scenarios</span></span>
* [<span data-ttu-id="56ea8-301">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="56ea8-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="56ea8-302">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="56ea8-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="56ea8-303">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="56ea8-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="56ea8-304">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="56ea8-305">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="56ea8-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="56ea8-306">建立和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-306">Creating and running applications</span></span>
* [<span data-ttu-id="56ea8-307">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="56ea8-308">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="56ea8-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="56ea8-309">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="56ea8-309">Tools and extensions</span></span>
* [<span data-ttu-id="56ea8-310">使用適用於 IntelliJ 的 Azure 工具組透過 VPN 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="56ea8-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="56ea8-311">使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="56ea8-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="56ea8-312">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="56ea8-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="56ea8-313">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具建立 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="56ea8-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="56ea8-314">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="56ea8-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="56ea8-315">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="56ea8-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="56ea8-316">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="56ea8-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="56ea8-317">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="56ea8-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="56ea8-318">管理資源</span><span class="sxs-lookup"><span data-stu-id="56ea8-318">Managing resources</span></span>
* [<span data-ttu-id="56ea8-319">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="56ea8-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="56ea8-320">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="56ea8-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

