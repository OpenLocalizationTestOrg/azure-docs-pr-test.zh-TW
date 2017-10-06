---
title: "適用於 IntelliJ 的 Azure 工具組：透過 SSH 對 Spark 應用程式進行遠端偵錯 | Microsoft Docs"
description: "透過 SSH toouse HDInsight Tools 在 Azure Toolkit for IntelliJ toodebug 應用程式，在 HDInsight 上的遠端叢集的方式的逐步指引"
keywords: "遠端偵錯 intellij, 進行 intellij 遠端偵錯, ssh, intellij, hdinsight, 偵錯 intellij, 偵錯"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="ee803-104">使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="ee803-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="ee803-105">這篇文章提供有關逐步指引 toouse HDInsight Tools 在 Azure Toolkit IntelliJ toodebug 上的應用程式從遠端的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ee803-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="ee803-106">toodebug 您的專案，您也可以檢視 hello[偵錯 HDInsight Spark 應用程式使用 Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)視訊。</span><span class="sxs-lookup"><span data-stu-id="ee803-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="ee803-107">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="ee803-107">**Prerequisites**</span></span>

* <span data-ttu-id="ee803-108">**適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具**。</span><span class="sxs-lookup"><span data-stu-id="ee803-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="ee803-109">此工具是適用於 IntelliJ 之 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee803-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="ee803-110">如需詳細資訊，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation)。</span><span class="sxs-lookup"><span data-stu-id="ee803-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="ee803-111">**適用於 IntelliJ 的 Azure 工具組**。</span><span class="sxs-lookup"><span data-stu-id="ee803-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="ee803-112">HDInsight 叢集使用此工具組 toocreate Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee803-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="ee803-113">如需詳細資訊，請依照下列中的 hello 指示[使用 Azure Toolkit for IntelliJ toocreate Spark 應用程式的 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin)。</span><span class="sxs-lookup"><span data-stu-id="ee803-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="ee803-114">**HDInsight SSH 服務與使用者名稱和密碼管理**。</span><span class="sxs-lookup"><span data-stu-id="ee803-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="ee803-115">如需詳細資訊，請參閱[透過 SSH 連線 tooHDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)和[使用 SSH 通道 tooaccess Ambari web UI、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel)。</span><span class="sxs-lookup"><span data-stu-id="ee803-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="ee803-116">建立 Spark Scala 應用程式，並設定它以進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="ee803-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="ee803-117">啟動 IntelliJ IDEA，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="ee803-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="ee803-118">在 hello**新專案**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ee803-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="ee803-119">a.</span><span class="sxs-lookup"><span data-stu-id="ee803-119">a.</span></span> <span data-ttu-id="ee803-120">選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="ee803-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="ee803-121">b.</span><span class="sxs-lookup"><span data-stu-id="ee803-121">b.</span></span> <span data-ttu-id="ee803-122">根據您的喜好設定選取 Java 或 Scala 範本。</span><span class="sxs-lookup"><span data-stu-id="ee803-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="ee803-123">選取下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee803-123">Select between hello following options:</span></span>

      - <span data-ttu-id="ee803-124">**Spark on HDInsight (Scala) \(HDInsight 上的 Spark (Scala)\)**</span><span class="sxs-lookup"><span data-stu-id="ee803-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="ee803-125">**Spark on HDInsight (Java) \(HDInsight 上的 Spark (Java)\)**</span><span class="sxs-lookup"><span data-stu-id="ee803-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="ee803-126">Spark on HDInsight Cluster Run Sample (Scala) \(HDInsight 叢集上的 Spark 執行範例 (Scala)\)</span><span class="sxs-lookup"><span data-stu-id="ee803-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="ee803-127">此範例會使用 [Spark on HDInsight Cluster Run Sample (Scala)] \(HDInsight 叢集上的 Spark 執行範例 (Scala)) 範本。</span><span class="sxs-lookup"><span data-stu-id="ee803-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="ee803-128">c.</span><span class="sxs-lookup"><span data-stu-id="ee803-128">c.</span></span> <span data-ttu-id="ee803-129">在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:</span><span class="sxs-lookup"><span data-stu-id="ee803-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="ee803-130">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="ee803-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="ee803-131">**SBT**、 管理 hello 相依性和建置 hello Scala 專案</span><span class="sxs-lookup"><span data-stu-id="ee803-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![建立偵錯專案](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="ee803-133">d.</span><span class="sxs-lookup"><span data-stu-id="ee803-133">d.</span></span> <span data-ttu-id="ee803-134">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="ee803-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="ee803-135">Hello 中下一步**新專案**視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="ee803-135">In hello next **New Project** window, do hello following:</span></span>

   ![選取 hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="ee803-137">a.</span><span class="sxs-lookup"><span data-stu-id="ee803-137">a.</span></span> <span data-ttu-id="ee803-138">輸入專案名稱和專案位置。</span><span class="sxs-lookup"><span data-stu-id="ee803-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="ee803-139">b.</span><span class="sxs-lookup"><span data-stu-id="ee803-139">b.</span></span> <span data-ttu-id="ee803-140">在 hello**專案 SDK**下拉式清單中，選取**Java 1.8**的**二手 2.x**叢集，或選取**Java 1.7**的**Spark 1。x**叢集。</span><span class="sxs-lookup"><span data-stu-id="ee803-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="ee803-141">c.</span><span class="sxs-lookup"><span data-stu-id="ee803-141">c.</span></span> <span data-ttu-id="ee803-142">在 hello **Spark 版本**下拉式清單中，hello Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。</span><span class="sxs-lookup"><span data-stu-id="ee803-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="ee803-143">如果 hello spark 叢集版本早於 2.0，請選取**二手 1.x**。</span><span class="sxs-lookup"><span data-stu-id="ee803-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="ee803-144">否則，請選取 **Spark 2.x**。</span><span class="sxs-lookup"><span data-stu-id="ee803-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="ee803-145">此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。</span><span class="sxs-lookup"><span data-stu-id="ee803-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="ee803-146">d.</span><span class="sxs-lookup"><span data-stu-id="ee803-146">d.</span></span> <span data-ttu-id="ee803-147">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ee803-147">Select **Finish**.</span></span>

4. <span data-ttu-id="ee803-148">選取**src** > **主要** > **scala** tooopen hello 專案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee803-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="ee803-149">這個範例會使用 hello **SparkCore_wasbloTest**指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee803-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="ee803-150">tooaccess hello**編輯組態**功能表中，選取 hello hello 右上角的圖示。</span><span class="sxs-lookup"><span data-stu-id="ee803-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="ee803-151">從這個功能表中，您可以建立或編輯 hello 組態進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="ee803-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![編輯設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="ee803-153">在 [hello**執行/偵錯組態**] 對話方塊中，選取 hello 加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="ee803-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="ee803-154">然後選取 hello**提交 Spark 作業**選項。</span><span class="sxs-lookup"><span data-stu-id="ee803-154">Then select hello **Submit Spark Job** option.</span></span>

   ![新增設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="ee803-156">輸入 [Name] \(名稱\)、**[Spark cluster] \(Spark 叢集\)** 和 [Main class name] \(主要類別名稱\)。</span><span class="sxs-lookup"><span data-stu-id="ee803-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="ee803-157">然後選取 [Advanced configuration] \(進階設定\)。</span><span class="sxs-lookup"><span data-stu-id="ee803-157">Then select **Advanced configuration**.</span></span> 

   ![[Run/Debug Configurations] \(執行/偵錯設定\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="ee803-159">在 hello **Spark 提交進階設定**對話方塊中，選取**啟用 Spark 遠端偵錯**。</span><span class="sxs-lookup"><span data-stu-id="ee803-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="ee803-160">輸入 hello SSH 使用者名稱，然後輸入密碼，或使用私用金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="ee803-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="ee803-161">toosave hello 設定，請選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="ee803-161">toosave hello configuration, select **OK**.</span></span>

   ![[Enable Spark remote debug] \(啟用 Spark 遠端偵錯\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="ee803-163">hello 組態現在是以您所提供的 hello 名稱儲存。</span><span class="sxs-lookup"><span data-stu-id="ee803-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="ee803-164">tooview hello 設定詳細資料，選取 hello 組態名稱。</span><span class="sxs-lookup"><span data-stu-id="ee803-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="ee803-165">選取 toomake 變更**編輯組態**。</span><span class="sxs-lookup"><span data-stu-id="ee803-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="ee803-166">Hello 組態設定完成之後，您可以針對 hello 遠端叢集執行 hello 專案或執行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="ee803-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="ee803-167">深入了解如何 tooperform 遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="ee803-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="ee803-168">案例 1：執行遠端執行</span><span class="sxs-lookup"><span data-stu-id="ee803-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="ee803-169">在本節中，我們會示範如何 toodebug 驅動程式和執行程式。</span><span class="sxs-lookup"><span data-stu-id="ee803-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="ee803-170">設定中斷點，然後再選取 hello**偵錯**圖示。</span><span class="sxs-lookup"><span data-stu-id="ee803-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![選取 hello 偵錯圖示](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="ee803-172">當執行 hello 程式達到 hello 重大點時，您會看到**驅動程式** 索引標籤和兩個**Executor** hello 中的索引標籤**偵錯工具**窗格。</span><span class="sxs-lookup"><span data-stu-id="ee803-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="ee803-173">選取 hello**繼續程式**執行 hello 程式碼，然後到達 hello 下一個中斷點，並著重於 hello 對應的圖示 toocontinue **Executor**  索引標籤。您可以檢閱 hello hello 對應的執行記錄**主控台** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ee803-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![[Debug] \(偵錯\) 索引標籤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="ee803-175">案例 2：執行遠端偵錯和錯誤修正</span><span class="sxs-lookup"><span data-stu-id="ee803-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="ee803-176">在本節中，我們會示範如何使用的 toodynamically 更新 hello 變數值 hello IntelliJ 偵錯功能對簡單的修正。</span><span class="sxs-lookup"><span data-stu-id="ee803-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="ee803-177">在下列程式碼範例的 hello，因為 hello 目標檔案已存在，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee803-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="ee803-178">tooperform 遠端偵錯和 bug 修正</span><span class="sxs-lookup"><span data-stu-id="ee803-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="ee803-179">設定兩個中斷點，然後再選取 hello**偵錯**圖示 toostart hello 遠端偵錯處理序。</span><span class="sxs-lookup"><span data-stu-id="ee803-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="ee803-180">hello 程式碼會停止在 hello 第一次中斷時間點，而且 hello 參數和變數的資訊會顯示 hello**變數**窗格。</span><span class="sxs-lookup"><span data-stu-id="ee803-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="ee803-181">選取 hello**繼續程式**圖示 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="ee803-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="ee803-182">hello 程式碼會在 hello 第二個點停止。</span><span class="sxs-lookup"><span data-stu-id="ee803-182">hello code stops at hello second point.</span></span> <span data-ttu-id="ee803-183">如預期般，會攔截到 hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee803-183">hello exception is caught as expected.</span></span>

  ![擲回錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="ee803-185">選取 hello**繼續程式**圖示一次。</span><span class="sxs-lookup"><span data-stu-id="ee803-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="ee803-186">hello **HDInsight Spark 提交**視窗會顯示 「 工作執行失敗 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ee803-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![提交錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="ee803-188">選取 使用 hello IntelliJ 偵錯功能的 toodynamically 更新 hello 變數值**偵錯**一次。</span><span class="sxs-lookup"><span data-stu-id="ee803-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="ee803-189">hello**變數**窗格會顯示一次。</span><span class="sxs-lookup"><span data-stu-id="ee803-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="ee803-190">以滑鼠右鍵按一下 hello 目標上 hello**偵錯**索引標籤，然後選取**設定值**。</span><span class="sxs-lookup"><span data-stu-id="ee803-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="ee803-191">接下來，輸入新的值為 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="ee803-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="ee803-192">然後選取**Enter** toosave hello 值。</span><span class="sxs-lookup"><span data-stu-id="ee803-192">Then select **Enter** toosave hello value.</span></span> 

  ![設定值](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="ee803-194">選取 hello**繼續程式**圖示 toocontinue toorun hello 程式。</span><span class="sxs-lookup"><span data-stu-id="ee803-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="ee803-195">此時，不會攔截到任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee803-195">This time, no exception is caught.</span></span> <span data-ttu-id="ee803-196">您可以看到該 hello 專案成功執行不含任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee803-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![偵錯而未發生例外狀況](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="ee803-198"><a name="seealso"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ee803-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="ee803-199">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="ee803-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="ee803-200">示範</span><span class="sxs-lookup"><span data-stu-id="ee803-200">Demo</span></span>
* <span data-ttu-id="ee803-201">建立 Scala 專案 (影片)：[Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (建立 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="ee803-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="ee803-202">遠端偵錯 （影片）：[使用 Azure Toolkit for IntelliJ toodebug Spark 應用程式，從遠端在 HDInsight 叢集上](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="ee803-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="ee803-203">案例</span><span class="sxs-lookup"><span data-stu-id="ee803-203">Scenarios</span></span>
* [<span data-ttu-id="ee803-204">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="ee803-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ee803-205">機器學習的 Spark： 使用 HDInsight tooanalyze 建置溫度使用 HVAC 資料中的 Spark</span><span class="sxs-lookup"><span data-stu-id="ee803-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ee803-206">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="ee803-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ee803-207">HDInsight toobuild 即時串流應用程式中的 Spark Streaming： 使用 Spark</span><span class="sxs-lookup"><span data-stu-id="ee803-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ee803-208">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="ee803-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ee803-209">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ee803-209">Create and run applications</span></span>
* [<span data-ttu-id="ee803-210">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="ee803-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ee803-211">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="ee803-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ee803-212">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="ee803-212">Tools and extensions</span></span>
* [<span data-ttu-id="ee803-213">使用 Azure Toolkit 的 HDInsight 叢集的 IntelliJ toocreate Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="ee803-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ee803-214">IntelliJ toodebug Spark 應用程式，透過 VPN 從遠端使用 Azure Toolkit</span><span class="sxs-lookup"><span data-stu-id="ee803-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ee803-215">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ee803-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="ee803-216">在 Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="ee803-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="ee803-217">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="ee803-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ee803-218">適用於在 hello HDInsight Spark 叢集中的 Jupyter 筆記本的核心</span><span class="sxs-lookup"><span data-stu-id="ee803-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ee803-219">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="ee803-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ee803-220">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="ee803-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ee803-221">管理資源</span><span class="sxs-lookup"><span data-stu-id="ee803-221">Manage resources</span></span>
* [<span data-ttu-id="ee803-222">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="ee803-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ee803-223">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="ee803-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
