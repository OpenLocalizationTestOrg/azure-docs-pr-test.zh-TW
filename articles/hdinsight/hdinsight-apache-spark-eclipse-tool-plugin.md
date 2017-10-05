---
title: "適用於 Eclipse 的 Azure 工具組 - 建立適用於 HDInsight Spark 的 Scala 應用程式 | Microsoft Docs"
description: "使用 HDInsight 工具 (位於 Eclipse 的 Azure 工具組中) 來開發以 Scala 撰寫的 Spark 應用程式，並直接從 Eclipse IDE 將它們提交到 HDInsight Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="2d65f-103">使用適用於 Eclipse 的 Azure 工具組建立適用於 HDInsight 叢集的 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="2d65f-104">使用 HDInsight 工具 (位於適用於 Eclipse 的 Azure 工具組中) 來開發以 Scala 撰寫的 Spark 應用程式，並直接從 Eclipse IDE 將它們提交到 Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="2d65f-105">您能以數種不同的方式使用 HDInsight 工具外掛程式：</span><span class="sxs-lookup"><span data-stu-id="2d65f-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="2d65f-106">在 HDInsight Spark 叢集上開發並提交 Scala Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="2d65f-107">存取您的 Azure HDInsight Spark 叢集資源</span><span class="sxs-lookup"><span data-stu-id="2d65f-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="2d65f-108">在本機開發並執行 Scala Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d65f-109">此工具可用來只對 Linux 上的 HDInsight Spark 叢集建立並提交應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2d65f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d65f-110">Prerequisites</span></span>

* <span data-ttu-id="2d65f-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2d65f-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="2d65f-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="2d65f-113">Oracle Java Development Kit 第 8 版，可用於 Eclipse IDE 執行階段。</span><span class="sxs-lookup"><span data-stu-id="2d65f-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="2d65f-114">您可以從 [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下載。</span><span class="sxs-lookup"><span data-stu-id="2d65f-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="2d65f-115">Eclipse IDE。</span><span class="sxs-lookup"><span data-stu-id="2d65f-115">Eclipse IDE.</span></span> <span data-ttu-id="2d65f-116">本文使用的是 Eclipse Neon。</span><span class="sxs-lookup"><span data-stu-id="2d65f-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="2d65f-117">您可以從 [Eclipse 網站](https://www.eclipse.org/downloads/)下載。</span><span class="sxs-lookup"><span data-stu-id="2d65f-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="2d65f-118">Spark SDK。</span><span class="sxs-lookup"><span data-stu-id="2d65f-118">Spark SDK.</span></span> <span data-ttu-id="2d65f-119">您可以從 [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409) 下載。</span><span class="sxs-lookup"><span data-stu-id="2d65f-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="2d65f-120">在 Azure Toolkit 安裝 HDInsight Tools Eclipse 和 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="2d65f-121">安裝 HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="2d65f-121">Install HDInsight Tools</span></span>
<span data-ttu-id="2d65f-122">適用於 Eclipse 的 HDInsight 工具是適用於 Eclipse 的 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="2d65f-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="2d65f-123">如需安裝指示，請參閱[安裝適用於 Eclipse 的 Azure 工具組](../azure-toolkit-for-eclipse-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="2d65f-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="2d65f-124">安裝 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-124">Install Scala Plugin</span></span>
<span data-ttu-id="2d65f-125">當您開啟 Intellij 時，HDInsight Tools 自動偵測是否或不安裝 Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-125">When you open the Intellij, the HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="2d65f-126">按一下**確定**若要繼續，然後依照指示安裝 Eclipse Marketplace。</span><span class="sxs-lookup"><span data-stu-id="2d65f-126">Click **OK** to continue and follow the instructions to install by the Eclipse Marketplace.</span></span>

 ![自動安裝 Scala 外掛程式](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="2d65f-128">登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="2d65f-128">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="2d65f-129">啟動 Eclipse IDE，然後開啟 [Azure Explorer]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-129">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="2d65f-130">在 [視窗] 功能表上，按一下 [顯示檢視]，然後按一下 [其他]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-130">On the **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="2d65f-131">在開啟的對話方塊中展開 [Azure]，然後依序按一下 [Azure Explorer] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-131">In the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![顯示檢視對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="2d65f-133">以滑鼠右鍵按一下 [Azure] 節點，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-133">Right-click the **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="2d65f-134">在 [Azure 登入] 對話方塊中，選擇 [驗證模式]、按一下 [登入] 並輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="2d65f-134">In the **Azure Sign In** dialog box, choose the authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![[Azure 登入] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="2d65f-136">登入之後，[選取訂用帳戶] 對話方塊會列出與認證相關聯的所有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d65f-136">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="2d65f-137">按一下 [選取] 以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2d65f-137">Click **Select** to close the dialog box.</span></span>

    ![[選取訂用帳戶] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="2d65f-139">在 [Azure Explorer] 索引標籤中展開 [HDInsight]，可查看您訂用帳戶下的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-139">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="2d65f-141">您可以進一步展開叢集名稱節點，查看與叢集相關聯的資源 (例如，儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="2d65f-141">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
    ![展開叢集名稱以查看資源](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="2d65f-143">設定 HDInsight Spark 叢集的 Spark Scala 專案</span><span class="sxs-lookup"><span data-stu-id="2d65f-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="2d65f-144">在 Eclipse IDE 工作區中，依序按一下 [檔案]、[新增] 及 [專案]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-144">In the Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="2d65f-145">在 [新增專案] 精靈中展開 [HDInsight]、選取 [HDInsight 上的 Spark (Scala)]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-145">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![選取 Spark HDInsight (Scala) 專案](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="2d65f-147">Scala 專案建立精靈會自動偵測您是否已安裝 Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-147">The Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="2d65f-148">按一下**確定**繼續下載 Scala 外掛程式，然後依照指示來重新啟動 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="2d65f-148">Click **OK** to continue downloading the Scala plugin, then follow the instructions to restart Eclipse.</span></span>

    ![Scala 檢查](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="2d65f-150">在 [新增 HDInsight Scala 專案] 對話方塊中，提供下列值，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="2d65f-150">In the **New HDInsight Scala Project** dialog box, provide the following values, and then click **Next**:</span></span>
   * <span data-ttu-id="2d65f-151">輸入專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-151">Enter a name for the project.</span></span>
   * <span data-ttu-id="2d65f-152">在 [JRE] 區域中，請確定已將 [使用執行環境 JRE] 設為 [JavaSE-1.7] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2d65f-152">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="2d65f-153">請確定已將 Spark SDK 設為您下載 SDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="2d65f-153">Make sure that Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="2d65f-154">下載位置的連結已包含於本文稍早的[必要條件](#prerequisites)中。</span><span class="sxs-lookup"><span data-stu-id="2d65f-154">The link to the download location is included in the [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="2d65f-155">您也可以從此對話方塊中包含的連結下載 SDK。</span><span class="sxs-lookup"><span data-stu-id="2d65f-155">You can also download the SDK from the link included in the dialog box.</span></span>

    ![[新增 HDInsight Scala 專案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="2d65f-157">在下一個對話方塊中，按一下 [程式庫] 索引標籤並保留預設值，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-157">In the next dialog box, click the **Libraries** tab and keep the defaults, and then click **Finish**.</span></span> 
   
    ![[程式庫] 索引標籤](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="2d65f-159">建立 HDInsight Spark 叢集的 Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="2d65f-160">在 Eclipse IDE 中，從 [封裝總管] 將您稍早建立的專案展開，以滑鼠右鍵按一下 [src]、指向 [新增]，然後按一下 [其他]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-160">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="2d65f-161">在 [選取精靈] 對話方塊方塊中，展開 [Scala 精靈]、按一下 [Scala 物件]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-161">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![選取精靈對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="2d65f-163">在 [建立新檔案] 對話方塊中輸入物件的名稱，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-163">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![[建立新檔案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="2d65f-165">在文字編輯器中貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="2d65f-165">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="2d65f-166">在 HDInsight Spark 叢集上執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="2d65f-166">Run the application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="2d65f-167">從 [封裝總管] 中，以滑鼠右鍵按一下專案名稱，然後選取 [將 Spark 應用程式提交給 HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-167">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="2d65f-168">在 [提交 Spark] 對話方塊中，提供下列值，然後按一下 [提交]：</span><span class="sxs-lookup"><span data-stu-id="2d65f-168">In the **Spark Submission** dialog box, provide the following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="2d65f-169">針對 **叢集名稱**，選取您要在其上執行應用程式的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-169">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="2d65f-170">從 Eclipse 專案中選取構件，或從硬碟中選取一個。</span><span class="sxs-lookup"><span data-stu-id="2d65f-170">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="2d65f-171">預設值取決於您在套件總管中以滑鼠右鍵按一下的項目。</span><span class="sxs-lookup"><span data-stu-id="2d65f-171">The default value depends on the item you right-click from package explorer.</span></span>
      * <span data-ttu-id="2d65f-172">在 [主要類別名稱] 下拉式清單中，提交精靈會顯示您所選專案的所有物件名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-172">In the **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="2d65f-173">選取或輸入您想要執行的物件名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-173">Select or input one that you want to run.</span></span> <span data-ttu-id="2d65f-174">如果您從硬碟選取構件，您必須自行輸入主要類別名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="2d65f-175">因為此範例中的應用程式程式碼不需要任何命令列引數，或是參考 JAR 或檔案，所以您可以將其餘的文字方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="2d65f-175">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
       ![[提交 Spark] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="2d65f-177">[Spark Submission (提交 Spark)]  索引標籤應會開始顯示進度。</span><span class="sxs-lookup"><span data-stu-id="2d65f-177">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="2d65f-178">您可以按一下 [提交 Spark] 視窗中的紅色按鈕，即可將應用程式停止。</span><span class="sxs-lookup"><span data-stu-id="2d65f-178">You can stop the application by clicking the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="2d65f-179">您也可以按一下全球圖示 (以映像中的藍色方塊表示)，檢視此特定應用程式執行的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d65f-179">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![[提交 Spark] 視窗](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="2d65f-181">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具來存取和管理 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="2d65f-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="2d65f-182">您可以使用 HDInsight 工具來執行各種作業，包括存取作業輸出。</span><span class="sxs-lookup"><span data-stu-id="2d65f-182">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="2d65f-183">存取作業檢視</span><span class="sxs-lookup"><span data-stu-id="2d65f-183">Access the job view</span></span>
1. <span data-ttu-id="2d65f-184">在 [Azure Explorer] 中，依序展開 [HDInsight] 和 Spark 叢集名稱，然後按一下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-184">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span> 

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="2d65f-186">按一下**作業**節點。</span><span class="sxs-lookup"><span data-stu-id="2d65f-186">Click on the **Jobs** node.</span></span> <span data-ttu-id="2d65f-187">HDInsight 工具自動偵測是否或不安裝 E (fx) clipse 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-187">The HDInsight Tools auto-detects whether you installed the E(fx)clipse plugin or not.</span></span> <span data-ttu-id="2d65f-188">按一下**確定**若要繼續，請依照指示安裝 Eclipse Marketplace 並重新啟動 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="2d65f-188">Click **OK** to continue and follow the instructions to install the Eclipse Marketplace and restart Eclipse.</span></span>

    ![安裝 E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="2d65f-190">從 [作業] 節點開啟 [作業] 檢視。</span><span class="sxs-lookup"><span data-stu-id="2d65f-190">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="2d65f-191">在右窗格中，[Spark 作業檢視]  索引標籤會顯示已在叢集上執行的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-191">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="2d65f-192">按一下您想要查看更多詳細資料的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-192">Click the name of the application for which you want to see more details.</span></span>

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="2d65f-194">如果您將滑鼠停留在作業圖形，它會顯示基本執行的作業資訊。</span><span class="sxs-lookup"><span data-stu-id="2d65f-194">If you hover on the job graph, it displays basic running job info.</span></span> <span data-ttu-id="2d65f-195">按一下即可在作業圖形顯示階段圖形和每項工作產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="2d65f-195">Clicking on the job graph shows the stages graph and info that every job generates.</span></span>

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="2d65f-197">包括 Stderr 驅動程式、 驅動程式 Stdout 和目錄資訊的常用記錄檔中所列**記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2d65f-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in the **Log** tab.</span></span>

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="2d65f-199">您也可以按一下視窗頂端的個別超連結，開啟 [Spark history UI] \(Spark 歷程記錄 UI\) 和 [YARN UI] \(應用程式層級)。</span><span class="sxs-lookup"><span data-stu-id="2d65f-199">You can also open the Spark history UI and the YARN UI (at the application level) by clicking the respective hyperlink at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="2d65f-200">存取叢集的儲存體容器</span><span class="sxs-lookup"><span data-stu-id="2d65f-200">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="2d65f-201">在 [Azure Explorer] 中展開 [HDInsight] 根節點，查看可用的 HDInsight Spark 叢集清單。</span><span class="sxs-lookup"><span data-stu-id="2d65f-201">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="2d65f-202">展開叢集名稱以查看叢集的儲存體帳戶和預設儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="2d65f-202">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![儲存體帳戶和預設儲存體容器](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="2d65f-204">按一下與叢集相關聯的儲存體容器名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-204">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="2d65f-205">在右窗格中，按兩下 **HVACOut** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d65f-205">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="2d65f-206">開啟其中一個 **part-** 檔案，可查看應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="2d65f-206">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="2d65f-207">存取 Spark 歷程記錄伺服器</span><span class="sxs-lookup"><span data-stu-id="2d65f-207">Access the Spark history server</span></span>
1. <span data-ttu-id="2d65f-208">在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="2d65f-209">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="2d65f-209">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="2d65f-210">在佈建叢集時，您必須已指定這些項目。</span><span class="sxs-lookup"><span data-stu-id="2d65f-210">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="2d65f-211">在 [Spark 歷程記錄伺服器] 儀表板中，您可以使用應用程式名稱，尋找您剛完成執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-211">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="2d65f-212">在上述程式碼中，您可以使用 `val conf = new SparkConf().setAppName("MyClusterApp")`來設定應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="2d65f-212">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="2d65f-213">因此，Spark 應用程式名稱為 **MyClusterApp**。</span><span class="sxs-lookup"><span data-stu-id="2d65f-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="2d65f-214">啟動 Ambari 入口網站</span><span class="sxs-lookup"><span data-stu-id="2d65f-214">Start the Ambari portal</span></span>
1. <span data-ttu-id="2d65f-215">在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="2d65f-216">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="2d65f-216">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="2d65f-217">在佈建叢集時，您必須已指定這些項目。</span><span class="sxs-lookup"><span data-stu-id="2d65f-217">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="2d65f-218">管理 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2d65f-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="2d65f-219">根據預設，適用於 Eclipse 的 Azure 工具組中之 HDInsight 工具會列出您所有 Azure 訂用帳戶中的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="2d65f-220">如有必要，您可以指定要存取其叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d65f-220">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="2d65f-221">在 [Azure Explorer] 中，以滑鼠右鍵按一下 [Azure] 根節點，然後按一下 [管理訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-221">In Azure Explorer, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="2d65f-222">在對話方塊中，清除您不想要存取的訂用帳戶核取方塊，然後按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-222">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then click **Close**.</span></span> <span data-ttu-id="2d65f-223">如果您想要登出 Azure 訂用帳戶，也可以按一下 [登出]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-223">You can also click **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="2d65f-224">在本機執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="2d65f-225">您可以使用適用於 Eclipse 的 Azure 工具組中之 HDInsight 工具，在工作站上本機執行 Spark Scala 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-225">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="2d65f-226">一般而言，這些應用程式不需要存取叢集資源 (例如儲存體容器)，而且您可在本機上執行並測試。</span><span class="sxs-lookup"><span data-stu-id="2d65f-226">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="2d65f-227">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d65f-227">Prerequisite</span></span>
<span data-ttu-id="2d65f-228">在 Windows 電腦上執行本機 Spark Scala 應用程式時，可能會發生如 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) 中所述的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2d65f-228">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="2d65f-229">發生這個例外狀況是因為 Windows 中遺失 **WinUtils.exe**。</span><span class="sxs-lookup"><span data-stu-id="2d65f-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="2d65f-230">若要解決這個錯誤，您必須[下載可執行檔](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)，並將其放在 **C:\WinUtils\bin** 之類的位置。</span><span class="sxs-lookup"><span data-stu-id="2d65f-230">To resolve this error, you must [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="2d65f-231">然後，您必須新增環境變數 **HADOOP_HOME**，並將變數的值設為 **C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="2d65f-231">You must then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="2d65f-232">執行本機 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="2d65f-233">啟動 Eclipse，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="2d65f-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="2d65f-234">在 [新增專案] 對話方塊中選取下列選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-234">In the **New Project** dialog box, make the following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="2d65f-235">在左窗格中，選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-235">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="2d65f-236">在右窗格中，選取 [HDInsight 上的 Spark 本機執行範例 (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-236">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![New Project dialog box](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="2d65f-238">若要提供專案的詳細資料，請遵循稍早的[設定 HDInsight Spark 叢集的 Spark Scala 專案](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster)一節中的步驟 3 到 6。</span><span class="sxs-lookup"><span data-stu-id="2d65f-238">To provide the project details, follow steps 3 through 6 from the earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="2d65f-239">範本會在 **src** 資料夾下方新增可在電腦本機執行的程式碼範例 (**LogQuery**)。</span><span class="sxs-lookup"><span data-stu-id="2d65f-239">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="2d65f-241">以滑鼠右鍵按一下 **LogQuery** 應用程式、指向 [執行身分]，然後按一下 [1 Scala 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2d65f-241">Right-click the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="2d65f-242">您將在底部的 [主控台] 索引標籤中看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="2d65f-242">You will see an output like this in the **Console** tab at the bottom:</span></span>
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="2d65f-244">常見問題集</span><span class="sxs-lookup"><span data-stu-id="2d65f-244">FAQ</span></span>
<span data-ttu-id="2d65f-245">若要將應用程式提交至 Azure Data Lake Store，請在 Azure 登入程序期間，選擇 [互動] 模式。</span><span class="sxs-lookup"><span data-stu-id="2d65f-245">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="2d65f-246">如果您選取 [自動] 模式，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2d65f-246">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="2d65f-248">現在，我們已解決了。</span><span class="sxs-lookup"><span data-stu-id="2d65f-248">Now, we resolved it.</span></span> <span data-ttu-id="2d65f-249">您可以選擇要使用任何登入方法提交您應用程式的 Azure Data Lake 叢集。</span><span class="sxs-lookup"><span data-stu-id="2d65f-249">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="2d65f-250">意見反應和已知問題</span><span class="sxs-lookup"><span data-stu-id="2d65f-250">Feedback and known issues</span></span>
<span data-ttu-id="2d65f-251">目前，不支援直接檢視 Spark 輸出。</span><span class="sxs-lookup"><span data-stu-id="2d65f-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="2d65f-252">如果您有任何建議或意見反應，或使用此工具時遇到任何問題，歡迎將電子郵件傳送到 hdivstool@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="2d65f-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to send us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="2d65f-253"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="2d65f-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="2d65f-254">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="2d65f-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="2d65f-255">案例</span><span class="sxs-lookup"><span data-stu-id="2d65f-255">Scenarios</span></span>
* [<span data-ttu-id="2d65f-256">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="2d65f-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2d65f-257">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="2d65f-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2d65f-258">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="2d65f-258">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2d65f-259">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="2d65f-260">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="2d65f-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="2d65f-261">建立和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-261">Creating and running applications</span></span>
* [<span data-ttu-id="2d65f-262">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2d65f-263">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="2d65f-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2d65f-264">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="2d65f-264">Tools and extensions</span></span>
* [<span data-ttu-id="2d65f-265">使用適用於 IntelliJ 的 Azure 工具組中來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="2d65f-265">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2d65f-266">使用適用於 IntelliJ 的 Azure 工具組透過 VPN 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="2d65f-266">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2d65f-267">使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="2d65f-267">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="2d65f-268">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2d65f-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="2d65f-269">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="2d65f-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2d65f-270">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="2d65f-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2d65f-271">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="2d65f-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2d65f-272">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="2d65f-272">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="2d65f-273">管理資源</span><span class="sxs-lookup"><span data-stu-id="2d65f-273">Managing resources</span></span>
* [<span data-ttu-id="2d65f-274">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="2d65f-274">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2d65f-275">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="2d65f-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

