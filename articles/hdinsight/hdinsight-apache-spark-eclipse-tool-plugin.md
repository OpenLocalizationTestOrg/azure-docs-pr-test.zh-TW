---
title: "aaaAzure Toolkit for Eclipse-HDInsight Spark 建立 Scala 應用程式 |Microsoft 文件"
description: "使用 HDInsight Tools 在 Azure Toolkit Scala 以撰寫的 Eclipse toodevelop Spark 應用程式並將它們送出 tooan HDInsight Spark 叢集，直接從 hello Eclipse IDE。"
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
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="f19a5-103">使用 Azure Toolkit 的 HDInsight 叢集的 Eclipse toocreate Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-103">Use Azure Toolkit for Eclipse toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="f19a5-104">在 Azure Toolkit for Eclipse toodevelop 使用 HDInsight Tools 二手 Scala 中撰寫的應用程式，並將它們送出 tooan Azure HDInsight Spark 叢集，直接從 Eclipse IDE hello。</span><span class="sxs-lookup"><span data-stu-id="f19a5-104">Use HDInsight Tools in Azure Toolkit for Eclipse toodevelop Spark applications written in Scala and submit them tooan Azure HDInsight Spark cluster, directly from hello Eclipse IDE.</span></span> <span data-ttu-id="f19a5-105">您可以使用 hello HDInsight Tools 外掛程式幾個不同的方式：</span><span class="sxs-lookup"><span data-stu-id="f19a5-105">You can use hello HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="f19a5-106">toodevelop 並提交 HDInsight Spark 叢集上的 Scala Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-106">toodevelop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="f19a5-107">tooaccess Azure HDInsight Spark 叢集資源</span><span class="sxs-lookup"><span data-stu-id="f19a5-107">tooaccess your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="f19a5-108">toodevelop 和執行本機 Scala Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-108">toodevelop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f19a5-109">此工具可以使用的 toocreate 和送出應用程式僅適用於 linux 的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="f19a5-109">This tool can be used toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f19a5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f19a5-110">Prerequisites</span></span>

* <span data-ttu-id="f19a5-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="f19a5-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f19a5-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="f19a5-113">Oracle Java Development Kit 第 8 版，以用於 hello Eclipse IDE 執行階段。</span><span class="sxs-lookup"><span data-stu-id="f19a5-113">Oracle Java Development Kit version 8, which is used for hello Eclipse IDE runtime.</span></span> <span data-ttu-id="f19a5-114">您可以從 hello [Oracle 網站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-114">You can download it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="f19a5-115">Eclipse IDE。</span><span class="sxs-lookup"><span data-stu-id="f19a5-115">Eclipse IDE.</span></span> <span data-ttu-id="f19a5-116">本文使用的是 Eclipse Neon。</span><span class="sxs-lookup"><span data-stu-id="f19a5-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="f19a5-117">您可以將它安裝從 hello [Eclipse 網站](https://www.eclipse.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-117">You can install it from hello [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="f19a5-118">Spark SDK。</span><span class="sxs-lookup"><span data-stu-id="f19a5-118">Spark SDK.</span></span> <span data-ttu-id="f19a5-119">您可以從 [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409) 下載。</span><span class="sxs-lookup"><span data-stu-id="f19a5-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="f19a5-120">在 Azure Toolkit 安裝 HDInsight Tools Eclipse 和 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="f19a5-121">安裝 HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="f19a5-121">Install HDInsight Tools</span></span>
<span data-ttu-id="f19a5-122">適用於 Eclipse 的 HDInsight 工具是適用於 Eclipse 的 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="f19a5-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="f19a5-123">如需安裝指示，請參閱[安裝適用於 Eclipse 的 Azure 工具組](../azure-toolkit-for-eclipse-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="f19a5-124">安裝 Scala 外掛程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-124">Install Scala Plugin</span></span>
<span data-ttu-id="f19a5-125">當您開啟 hello Intellij 時，hello HDInsight Tools 自動偵測是否或不安裝 Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-125">When you open hello Intellij, hello HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="f19a5-126">按一下**確定**toocontinue 然後遵循 hello 指示 tooinstall 由 hello Eclipse Marketplace。</span><span class="sxs-lookup"><span data-stu-id="f19a5-126">Click **OK** toocontinue and follow hello instructions tooinstall by hello Eclipse Marketplace.</span></span>

 ![自動安裝 Scala 外掛程式](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="f19a5-128">登入 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f19a5-128">Sign in tooyour Azure subscription</span></span>
1. <span data-ttu-id="f19a5-129">啟動 hello Eclipse IDE，並開啟 Azure 總管。</span><span class="sxs-lookup"><span data-stu-id="f19a5-129">Start hello Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="f19a5-130">在 hello**視窗**功能表上，按一下 **顯示檢視**，然後按一下**其他**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-130">On hello **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="f19a5-131">在開啟的 hello 對話方塊中，依序展開**Azure**，按一下**Azure 總管**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-131">In hello dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![顯示檢視對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="f19a5-133">以滑鼠右鍵按一下 hello **Azure**節點，然後再按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-133">Right-click hello **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="f19a5-134">在 hello **Azure 登入**對話方塊方塊中，選擇 hello 驗證方法中，按一下**登入**，並輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="f19a5-134">In hello **Azure Sign In** dialog box, choose hello authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![[Azure 登入] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="f19a5-136">您已登入之後，hello**選取的訂用帳戶**對話方塊方塊中列出所有 hello 與 hello 認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f19a5-136">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions associated with hello credentials.</span></span> <span data-ttu-id="f19a5-137">按一下**選取**tooclose hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f19a5-137">Click **Select** tooclose hello dialog box.</span></span>

    ![[選取訂用帳戶] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="f19a5-139">在 hello **Azure 總管**索引標籤上，依序展開**HDInsight** toosee hello HDInsight Spark 叢集，您的訂用帳戶底下。</span><span class="sxs-lookup"><span data-stu-id="f19a5-139">On hello **Azure Explorer** tab, expand **HDInsight** toosee hello HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure Explorer 中的 HDInsight Spark 叢集](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="f19a5-141">您可以進一步展開叢集名稱節點 toosee hello （例如，儲存體帳戶） 相關聯的資源與 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f19a5-141">You can further expand a cluster name node toosee hello resources (for example, storage accounts) associated with hello cluster.</span></span>
   
    ![展開叢集名稱 toosee 資源](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="f19a5-143">設定 HDInsight Spark 叢集的 Spark Scala 專案</span><span class="sxs-lookup"><span data-stu-id="f19a5-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="f19a5-144">在 hello Eclipse IDE 工作區中，按一下 **檔案**，按一下**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-144">In hello Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="f19a5-145">在 hello 新專案精靈 中，展開**HDInsight**，選取**HDInsight (Scala) 上的 Spark**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-145">In hello New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![選取 HDInsight (Scala) 專案上的 Spark hello](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="f19a5-147">hello Scala 專案建立精靈自動偵測是否或不安裝 Scala 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-147">hello Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="f19a5-148">按一下**確定**toocontinue 下載 hello Scala 外掛程式，然後遵循 hello 指示 toorestart Eclipse。</span><span class="sxs-lookup"><span data-stu-id="f19a5-148">Click **OK** toocontinue downloading hello Scala plugin, then follow hello instructions toorestart Eclipse.</span></span>

    ![Scala 檢查](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="f19a5-150">在 hello**新 HDInsight Scala 專案**對話方塊中，提供 hello 下列值，然後再按一下**下一步**:</span><span class="sxs-lookup"><span data-stu-id="f19a5-150">In hello **New HDInsight Scala Project** dialog box, provide hello following values, and then click **Next**:</span></span>
   * <span data-ttu-id="f19a5-151">輸入 hello 專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="f19a5-151">Enter a name for hello project.</span></span>
   * <span data-ttu-id="f19a5-152">在 hello **JRE**區域中，請確定**使用執行環境 JRE**設定得**JavaSE 1.7**或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f19a5-152">In hello **JRE** area, make sure that **Use an execution environment JRE** is set too**JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="f19a5-153">請確定 Spark SDK 下載 hello SDK 組 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="f19a5-153">Make sure that Spark SDK is set toohello location where you downloaded hello SDK.</span></span> <span data-ttu-id="f19a5-154">hello 連結 toohello 下載中包含位置 hello[必要條件](#prerequisites)稍早在本文章。</span><span class="sxs-lookup"><span data-stu-id="f19a5-154">hello link toohello download location is included in hello [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="f19a5-155">您也可以從 hello 下載 hello SDK 包含 hello 對話方塊中的連結。</span><span class="sxs-lookup"><span data-stu-id="f19a5-155">You can also download hello SDK from hello link included in hello dialog box.</span></span>

    ![[新增 HDInsight Scala 專案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="f19a5-157">在 hello 下一步 對話方塊中，按一下 hello**文件庫**索引標籤上，並保留 hello 的預設值，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-157">In hello next dialog box, click hello **Libraries** tab and keep hello defaults, and then click **Finish**.</span></span> 
   
    ![[程式庫] 索引標籤](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="f19a5-159">建立 HDInsight Spark 叢集的 Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="f19a5-160">在 hello Eclipse IDE 中，從 封裝總管 中，展開您稍早建立的 hello 專案，以滑鼠右鍵按一下**src**，點太**新增**，然後按一下**其他**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-160">In hello Eclipse IDE, from Package Explorer, expand hello project that you created earlier, right-click **src**, point too**New**, and then click **Other**.</span></span>
2. <span data-ttu-id="f19a5-161">在 hello**選取精靈**對話方塊方塊中，展開  **Scala 精靈**，按一下  **Scala 物件**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-161">In hello **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![選取精靈對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="f19a5-163">在 hello**開新檔案**對話方塊中，輸入 hello 物件的名稱，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-163">In hello **Create New File** dialog box, enter a name for hello object, and then click **Finish**.</span></span>
   
    ![[建立新檔案] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="f19a5-165">貼上下列程式碼 hello 文字編輯器中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f19a5-165">Paste hello following code in hello text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="f19a5-166">HDInsight Spark 叢集上執行 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f19a5-166">Run hello application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="f19a5-167">封裝總管 中，從 hello 專案名稱，以滑鼠右鍵按一下，然後選取**提交 Spark 應用程式 tooHDInsight**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-167">From Package Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>        
   2. <span data-ttu-id="f19a5-168">在 hello **Spark 提交**對話方塊中，提供 hello 下列值，然後再按一下**送出**:</span><span class="sxs-lookup"><span data-stu-id="f19a5-168">In hello **Spark Submission** dialog box, provide hello following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="f19a5-169">如**叢集名稱**，選取 hello 想 toorun HDInsight Spark 叢集應用程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-169">For **Cluster Name**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>
      * <span data-ttu-id="f19a5-170">Hello Eclipse 的專案，從選取的成品，或選取從硬碟機。</span><span class="sxs-lookup"><span data-stu-id="f19a5-170">Select an artifact from hello Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="f19a5-171">hello 預設值取決於您以滑鼠右鍵按一下封裝總管 中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="f19a5-171">hello default value depends on hello item you right-click from package explorer.</span></span>
      * <span data-ttu-id="f19a5-172">在 hello**主要類別名稱**dropdownlist，精靈會顯示從選定專案的所有物件名稱的提交。</span><span class="sxs-lookup"><span data-stu-id="f19a5-172">In hello **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="f19a5-173">選取或輸入一個您要 toorun。</span><span class="sxs-lookup"><span data-stu-id="f19a5-173">Select or input one that you want toorun.</span></span> <span data-ttu-id="f19a5-174">如果您從硬碟選取構件，您必須自行輸入主要類別名稱。</span><span class="sxs-lookup"><span data-stu-id="f19a5-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="f19a5-175">因為在此範例中的 hello 應用程式程式碼不需要任何命令列引數或參考 （每瓶） 或檔案，您可以保留 hello 剩餘的空文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f19a5-175">Because hello application code in this example does not require any command-line arguments or reference JARs or files, you can leave hello remaining text boxes empty.</span></span>
        
       ![[提交 Spark] 對話方塊](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="f19a5-177">hello **Spark 提交** 索引標籤應該開始顯示 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="f19a5-177">hello **Spark Submission** tab should start displaying hello progress.</span></span> <span data-ttu-id="f19a5-178">您可以在 hello hello 紅色按鈕，即可停止 hello 應用程式**Spark 提交**視窗。</span><span class="sxs-lookup"><span data-stu-id="f19a5-178">You can stop hello application by clicking hello red button in hello **Spark Submission** window.</span></span> <span data-ttu-id="f19a5-179">您也可以檢視 hello hello 地球圖示 （hello 映像中的 hello 藍色方塊以表示），即可執行此特定應用程式的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f19a5-179">You can also view hello logs for this specific application run by clicking hello globe icon (denoted by hello blue box in hello image).</span></span>
      
       ![[提交 Spark] 視窗](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="f19a5-181">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具來存取和管理 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="f19a5-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="f19a5-182">您可以使用 HDInsight 工具，包括存取 hello 工作輸出執行各種作業。</span><span class="sxs-lookup"><span data-stu-id="f19a5-182">You can perform various operations by using HDInsight Tools, including accessing hello job output.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="f19a5-183">存取 hello 工作檢視</span><span class="sxs-lookup"><span data-stu-id="f19a5-183">Access hello job view</span></span>
1. <span data-ttu-id="f19a5-184">在 Azure 總管] 中，依序展開**HDInsight**，依序展開 [hello Spark 叢集名稱，然後按一下**作業**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-184">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then click **Jobs**.</span></span> 

    ![作業檢視節點](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="f19a5-186">按一下 hello**作業**節點。</span><span class="sxs-lookup"><span data-stu-id="f19a5-186">Click on hello **Jobs** node.</span></span> <span data-ttu-id="f19a5-187">hello HDInsight Tools 自動偵測是否或不安裝 hello E (fx) clipse 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-187">hello HDInsight Tools auto-detects whether you installed hello E(fx)clipse plugin or not.</span></span> <span data-ttu-id="f19a5-188">按一下**確定**toocontinue 與後續 hello 指示 tooinstall hello Eclipse Marketplace 並重新啟動 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="f19a5-188">Click **OK** toocontinue and follow hello instructions tooinstall hello Eclipse Marketplace and restart Eclipse.</span></span>

    ![安裝 E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="f19a5-190">開啟 hello 工作檢視從 hello**作業**節點。</span><span class="sxs-lookup"><span data-stu-id="f19a5-190">Open hello Job View from hello **Jobs** node.</span></span> <span data-ttu-id="f19a5-191">Hello 右窗格中，hello **Spark 工作檢視**索引標籤會顯示 hello 叢集所執行的所有 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-191">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="f19a5-192">按一下 hello hello 要 toosee 更多詳細資料的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f19a5-192">Click hello name of hello application for which you want toosee more details.</span></span>

    ![應用程式詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="f19a5-194">如果您將滑鼠停留在 hello 作業圖形，它會顯示基本執行的作業資訊。</span><span class="sxs-lookup"><span data-stu-id="f19a5-194">If you hover on hello job graph, it displays basic running job info.</span></span> <span data-ttu-id="f19a5-195">按一下即可在 hello 作業圖形顯示 hello 階段圖形和每項工作產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="f19a5-195">Clicking on hello job graph shows hello stages graph and info that every job generates.</span></span>

    ![作業階段詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="f19a5-197">常用的記錄檔，包括驅動程式 Stderr、 驅動程式 Stdout 和目錄資訊會列在 hello**記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f19a5-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in hello **Log** tab.</span></span>

    ![記錄詳細資料](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="f19a5-199">您也可以按一下 hello 視窗頂端的 hello hello 各自的超連結，開啟 hello Spark 記錄 UI 和 hello YARN UI （hello 應用程式層級）。</span><span class="sxs-lookup"><span data-stu-id="f19a5-199">You can also open hello Spark history UI and hello YARN UI (at hello application level) by clicking hello respective hyperlink at hello top of hello window.</span></span>

### <a name="access-hello-storage-container-for-hello-cluster"></a><span data-ttu-id="f19a5-200">Hello 叢集存取 hello 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="f19a5-200">Access hello storage container for hello cluster</span></span>
1. <span data-ttu-id="f19a5-201">在 Azure 總管] 中，展開 [hello **HDInsight**根節點 toosee HDInsight Spark 叢集可用的清單。</span><span class="sxs-lookup"><span data-stu-id="f19a5-201">In Azure Explorer, expand hello **HDInsight** root node toosee a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="f19a5-202">展開 hello 叢集名稱 toosee hello 儲存體帳戶與 hello hello 叢集的預設儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="f19a5-202">Expand hello cluster name toosee hello storage account and hello default storage container for hello cluster.</span></span>
   
    ![儲存體帳戶和預設儲存體容器](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="f19a5-204">按一下 hello 與 hello 叢集相關聯的儲存體容器名稱。</span><span class="sxs-lookup"><span data-stu-id="f19a5-204">Click hello storage container name associated with hello cluster.</span></span> <span data-ttu-id="f19a5-205">Hello 右窗格中，按兩下 hello **HVACOut**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f19a5-205">In hello right pane, double-click hello **HVACOut** folder.</span></span> <span data-ttu-id="f19a5-206">開啟其中一個 hello**一部分-**檔案 toosee hello hello 應用程式輸出。</span><span class="sxs-lookup"><span data-stu-id="f19a5-206">Open one of hello **part-** files toosee hello output of hello application.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="f19a5-207">存取 hello Spark 記錄伺服器</span><span class="sxs-lookup"><span data-stu-id="f19a5-207">Access hello Spark history server</span></span>
1. <span data-ttu-id="f19a5-208">在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟 Spark 歷程記錄 UI]。</span><span class="sxs-lookup"><span data-stu-id="f19a5-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="f19a5-209">當提示您時，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f19a5-209">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="f19a5-210">您必須指定這些佈建 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="f19a5-210">You must have specified these while provisioning hello cluster.</span></span>
2. <span data-ttu-id="f19a5-211">Hello Spark 記錄伺服器儀表板 中，您可以使用 hello 應用程式名稱 toolook hello 剛剛完成執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-211">In hello Spark history server dashboard, you use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="f19a5-212">在上述程式碼的 hello，您必須設定 hello 應用程式名稱使用`val conf = new SparkConf().setAppName("MyClusterApp")`。</span><span class="sxs-lookup"><span data-stu-id="f19a5-212">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="f19a5-213">因此，Spark 應用程式名稱為 **MyClusterApp**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="f19a5-214">啟動 hello Ambari 入口網站</span><span class="sxs-lookup"><span data-stu-id="f19a5-214">Start hello Ambari portal</span></span>
1. <span data-ttu-id="f19a5-215">在 [Azure Explorer] 中，以滑鼠右鍵按一下您的 Spark 叢集名稱，然後選取 [開啟叢集管理入口網站 (Ambari)]。</span><span class="sxs-lookup"><span data-stu-id="f19a5-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="f19a5-216">當提示您時，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f19a5-216">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="f19a5-217">您必須指定這些佈建 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="f19a5-217">You must have specified these while provisioning hello cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="f19a5-218">管理 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f19a5-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="f19a5-219">根據預設，在 Azure Toolkit for Eclipse HDInsight 工具會列出所有您 Azure 訂用帳戶的 hello Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="f19a5-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="f19a5-220">如有必要，您可以指定要 tooaccess hello 叢集 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f19a5-220">If necessary, you can specify hello subscriptions for which you want tooaccess hello cluster.</span></span> 

1. <span data-ttu-id="f19a5-221">在 Azure 總管 中，以滑鼠右鍵按一下 hello **Azure**根節點，然後**管理訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-221">In Azure Explorer, right-click hello **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="f19a5-222">在 [hello] 對話方塊中，清除 hello hello 訂用帳戶，您不想 tooaccess，，然後按一下核取方塊**關閉**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-222">In hello dialog box, clear hello check boxes for hello subscription that you don't want tooaccess, and then click **Close**.</span></span> <span data-ttu-id="f19a5-223">您也可以按一下**登出**如果想要從您的 Azure 訂用帳戶的 toosign。</span><span class="sxs-lookup"><span data-stu-id="f19a5-223">You can also click **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="f19a5-224">在本機執行 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="f19a5-225">您可以使用 HDInsight Tools 在 Azure Toolkit Eclipse toorun Spark Scala 應用程式在本機工作站上。</span><span class="sxs-lookup"><span data-stu-id="f19a5-225">You can use HDInsight Tools in Azure Toolkit for Eclipse toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="f19a5-226">一般而言，這些應用程式不需要存取 toocluster 資源，例如儲存體容器，而且您可以執行，並在本機測試它們。</span><span class="sxs-lookup"><span data-stu-id="f19a5-226">Typically, these applications don't need access toocluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="f19a5-227">必要條件</span><span class="sxs-lookup"><span data-stu-id="f19a5-227">Prerequisite</span></span>
<span data-ttu-id="f19a5-228">雖然您在 Windows 電腦上執行 hello 本機 Spark Scala 應用程式，您可能會收到例外狀況中所述[SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-228">While you're running hello local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="f19a5-229">發生這個例外狀況是因為 Windows 中遺失 **WinUtils.exe**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="f19a5-230">tooresolve 這個錯誤，您必須[下載可執行檔的 hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 位置**C:\WinUtils\bin**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-230">tooresolve this error, you must [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="f19a5-231">然後，您必須加入 hello 環境變數**HADOOP_HOME**並設定 hello hello 變數值太**C\WinUtils**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-231">You must then add hello environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="f19a5-232">執行本機 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="f19a5-233">啟動 Eclipse，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="f19a5-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="f19a5-234">在 hello**新專案**對話方塊中，請 hello 下列選項，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-234">In hello **New Project** dialog box, make hello following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="f19a5-235">Hello 左窗格中，選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-235">In hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="f19a5-236">Hello 右窗格中，選取**HDInsight 本機執行範例 (Scala) 上的 Spark**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-236">In hello right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![New Project dialog box](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="f19a5-238">tooprovide hello 專案詳細資料，遵循步驟 3 到 6 從 hello 前一節[設定 Spark Scala 專案 HDInsight Spark 叢集](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster)。</span><span class="sxs-lookup"><span data-stu-id="f19a5-238">tooprovide hello project details, follow steps 3 through 6 from hello earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="f19a5-239">hello 範本加入程式碼範例 (**LogQuery**) 下 hello **src**您可以在本機執行您的電腦的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f19a5-239">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 的位置](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="f19a5-241">以滑鼠右鍵按一下 hello **LogQuery**應用程式中，點太**執行身分**，然後按一下 **1 個 Scala 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f19a5-241">Right-click hello **LogQuery** application, point too**Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="f19a5-242">您會看到如下輸出中 hello**主控台**hello 底部的索引標籤：</span><span class="sxs-lookup"><span data-stu-id="f19a5-242">You will see an output like this in hello **Console** tab at hello bottom:</span></span>
   
   ![Spark 應用程式本機執行結果](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="f19a5-244">常見問題集</span><span class="sxs-lookup"><span data-stu-id="f19a5-244">FAQ</span></span>
<span data-ttu-id="f19a5-245">應用程式 tooAzure 資料湖存放區，toosubmit 選擇**互動式**hello Azure 登入程序期間的模式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-245">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="f19a5-246">如果您選取 [自動] 模式，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f19a5-246">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="f19a5-248">現在，我們已解決了。</span><span class="sxs-lookup"><span data-stu-id="f19a5-248">Now, we resolved it.</span></span> <span data-ttu-id="f19a5-249">您可以使用任何登入方法選擇 Azure 資料湖叢集 toosubmit 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f19a5-249">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="f19a5-250">意見反應和已知問題</span><span class="sxs-lookup"><span data-stu-id="f19a5-250">Feedback and known issues</span></span>
<span data-ttu-id="f19a5-251">目前，不支援直接檢視 Spark 輸出。</span><span class="sxs-lookup"><span data-stu-id="f19a5-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="f19a5-252">如果您有任何建議或意見反應，或使用此工具時，遇到任何問題，您可用 toosend 我們在電子郵件hdivstool@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="f19a5-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free toosend us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="f19a5-253"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="f19a5-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f19a5-254">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="f19a5-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f19a5-255">案例</span><span class="sxs-lookup"><span data-stu-id="f19a5-255">Scenarios</span></span>
* [<span data-ttu-id="f19a5-256">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="f19a5-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f19a5-257">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="f19a5-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f19a5-258">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="f19a5-258">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f19a5-259">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f19a5-260">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="f19a5-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="f19a5-261">建立和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-261">Creating and running applications</span></span>
* [<span data-ttu-id="f19a5-262">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f19a5-263">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="f19a5-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f19a5-264">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="f19a5-264">Tools and extensions</span></span>
* [<span data-ttu-id="f19a5-265">使用 Azure Toolkit for IntelliJ toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="f19a5-265">Use Azure Toolkit for IntelliJ toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f19a5-266">IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="f19a5-266">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f19a5-267">透過 SSH 遠端 IntelliJ toodebug Spark 應用程式使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="f19a5-267">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="f19a5-268">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f19a5-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="f19a5-269">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="f19a5-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f19a5-270">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="f19a5-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f19a5-271">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="f19a5-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f19a5-272">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="f19a5-272">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="f19a5-273">管理資源</span><span class="sxs-lookup"><span data-stu-id="f19a5-273">Managing resources</span></span>
* [<span data-ttu-id="f19a5-274">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="f19a5-274">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f19a5-275">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="f19a5-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

