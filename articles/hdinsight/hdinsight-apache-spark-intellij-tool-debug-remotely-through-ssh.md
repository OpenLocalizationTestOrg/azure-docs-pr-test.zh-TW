---
title: "適用於 IntelliJ 的 Azure 工具組：透過 SSH 對 Spark 應用程式進行遠端偵錯 | Microsoft Docs"
description: "逐步指引如何使用適用於 IntelliJ 之 Azure 工具組中的 HDInsight 工具，透過 SSH 對 HDInsight 叢集上的應用程式進行遠端偵錯"
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
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="f0bd4-104">使用適用於 IntelliJ 的 Azure 工具組透過 SSH 對 HDInsight 叢集上的 Spark 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="f0bd4-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="f0bd4-105">本文提供的逐步指引，是關於如何使用適用於 IntelliJ 之 Azure 工具組中的 HDInsight 工具，對 HDInsight 叢集上的應用程式進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="f0bd4-106">若要對您的專案進行偵錯，您也可以觀看 [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (使用適用於 IntelliJ 的 Azure 工具組對 HDInsight Spark 應用程式進行偵錯) 影片。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="f0bd4-107">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="f0bd4-107">**Prerequisites**</span></span>

* <span data-ttu-id="f0bd4-108">**適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具**。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="f0bd4-109">此工具是適用於 IntelliJ 之 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="f0bd4-110">如需詳細資訊，請參閱[安裝適用於 IntelliJ 的 Azure 工具組](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="f0bd4-111">**適用於 IntelliJ 的 Azure 工具組**。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="f0bd4-112">使用此工具組建立適用於 HDInsight 叢集的 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="f0bd4-113">如需詳細資訊，請遵循[使用適用於 IntelliJ 的 Azure 工具組建立適用於 HDInsight 叢集的 Spark 應用程式](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="f0bd4-114">**HDInsight SSH 服務與使用者名稱和密碼管理**。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="f0bd4-115">如需詳細資訊，請參閱[使用 SSH 連線到 HDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) 和[使用 SSH 通道來存取 Ambari Web UI、JobHistory、NameNode、Oozie 及其他 Web UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="f0bd4-116">建立 Spark Scala 應用程式，並設定它以進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="f0bd4-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="f0bd4-117">啟動 IntelliJ IDEA，然後建立專案。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="f0bd4-118">在 [新增專案]  對話方塊中，執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="f0bd4-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="f0bd4-119">a.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-119">a.</span></span> <span data-ttu-id="f0bd4-120">選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="f0bd4-121">b.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-121">b.</span></span> <span data-ttu-id="f0bd4-122">根據您的喜好設定選取 Java 或 Scala 範本。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="f0bd4-123">在下列選項之間進行選取：</span><span class="sxs-lookup"><span data-stu-id="f0bd4-123">Select between the following options:</span></span>

      - <span data-ttu-id="f0bd4-124">**Spark on HDInsight (Scala) \(HDInsight 上的 Spark (Scala)\)**</span><span class="sxs-lookup"><span data-stu-id="f0bd4-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="f0bd4-125">**Spark on HDInsight (Java) \(HDInsight 上的 Spark (Java)\)**</span><span class="sxs-lookup"><span data-stu-id="f0bd4-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="f0bd4-126">Spark on HDInsight Cluster Run Sample (Scala) \(HDInsight 叢集上的 Spark 執行範例 (Scala)\)</span><span class="sxs-lookup"><span data-stu-id="f0bd4-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="f0bd4-127">此範例會使用 [Spark on HDInsight Cluster Run Sample (Scala)] \(HDInsight 叢集上的 Spark 執行範例 (Scala)) 範本。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="f0bd4-128">c.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-128">c.</span></span> <span data-ttu-id="f0bd4-129">在 [建置工具] 清單中，根據您的需求選取下列任一項目：</span><span class="sxs-lookup"><span data-stu-id="f0bd4-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="f0bd4-130">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="f0bd4-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="f0bd4-131">**SBT**，以管理相依性並建置 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="f0bd4-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![建立偵錯專案](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="f0bd4-133">d.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-133">d.</span></span> <span data-ttu-id="f0bd4-134">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="f0bd4-135">在下一個 [新增專案] 視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f0bd4-135">In the next **New Project** window, do the following:</span></span>

   ![選取 Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="f0bd4-137">a.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-137">a.</span></span> <span data-ttu-id="f0bd4-138">輸入專案名稱和專案位置。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="f0bd4-139">b.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-139">b.</span></span> <span data-ttu-id="f0bd4-140">在 [專案 SDK] 下拉式清單中，選取 [Java 1.8] \(適用於 **Spark 2.x** 叢集)，或選取 [Java 1.7] \(適用於 **Spark 1.x** 叢集)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="f0bd4-141">c.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-141">c.</span></span> <span data-ttu-id="f0bd4-142">在 [Spark 版本] 下拉式清單中，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="f0bd4-143">如果 Spark 叢集是 2.0 以前的版本，請選取 [Spark 1.x]。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="f0bd4-144">否則，請選取 **Spark 2.x**。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="f0bd4-145">此範例使用 **Spark 2.0.2 (Scala 2.11.8)**。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="f0bd4-146">d.</span><span class="sxs-lookup"><span data-stu-id="f0bd4-146">d.</span></span> <span data-ttu-id="f0bd4-147">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-147">Select **Finish**.</span></span>

4. <span data-ttu-id="f0bd4-148">選取 **src** > **main \(主要\)** > scala 以在專案中開啟您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="f0bd4-149">此範例使用 **SparkCore_wasbloTest** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="f0bd4-150">若要存取 [編輯設定] 功能表，請選取右上角的圖示。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="f0bd4-151">從這個功能表中，您可以建立或編輯遠端偵錯的設定。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![編輯設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="f0bd4-153">在 [Run/Debug Configurations] \(執行/偵錯設定) 對話方塊中，選取加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="f0bd4-154">然後選取 [Submit Spark Job] \(提交 Spark 作業\) 選項。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-154">Then select the **Submit Spark Job** option.</span></span>

   ![新增設定](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="f0bd4-156">輸入 [Name] \(名稱\)、**[Spark cluster] \(Spark 叢集\)** 和 [Main class name] \(主要類別名稱\)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="f0bd4-157">然後選取 [Advanced configuration] \(進階設定\)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-157">Then select **Advanced configuration**.</span></span> 

   ![[Run/Debug Configurations] \(執行/偵錯設定\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="f0bd4-159">在 [Spark Submission Advanced Configuration] \(Spark 提交進階設定\) 對話方塊中，選取 [Enable Spark remote debug] \(啟用 Spark 遠端偵錯\)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="f0bd4-160">輸入 SSH 使用者名稱，然後輸入密碼或使用私密金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="f0bd4-161">若要儲存設定，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-161">To save the configuration, select **OK**.</span></span>

   ![[Enable Spark remote debug] \(啟用 Spark 遠端偵錯\)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="f0bd4-163">設定現在會使用您提供的名稱儲存。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="f0bd4-164">若要檢視設定詳細資訊，請選取設定名稱。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="f0bd4-165">若要進行變更，請選取 [Edit Configurations] \(編輯設定\)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="f0bd4-166">完成組態設定之後，您可以針對遠端叢集執行專案，或執行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="f0bd4-167">了解如何執行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="f0bd4-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="f0bd4-168">案例 1：執行遠端執行</span><span class="sxs-lookup"><span data-stu-id="f0bd4-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="f0bd4-169">在本節中，我們將示範如何對驅動程式和執行程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-169">In this section, we show you how to debug drivers and executors.</span></span>

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
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="f0bd4-170">設定一個中斷點，然後選取**偵錯**圖示。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![選取偵錯圖示](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="f0bd4-172">當程式執行觸及中斷點時，您會在 [偵錯工具] 窗格中看到一個 [驅動程式] 索引標籤和兩個 [執行程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="f0bd4-173">選取**繼續程式**圖示以繼續執行程式碼，然後到達下一個中斷點並著重於對應的 [執行程式] 索引標籤。您可以在對應的 [主控台] 索引標籤中檢閱執行記錄。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![[Debug] \(偵錯\) 索引標籤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="f0bd4-175">案例 2：執行遠端偵錯和錯誤修正</span><span class="sxs-lookup"><span data-stu-id="f0bd4-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="f0bd4-176">在本節中，我們示範如何使用 IntelliJ 偵錯功能進行簡單修正，以動態更新變數值。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="f0bd4-177">在下列程式碼範例中，因為目標檔案已存在，所以會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
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


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="f0bd4-178">執行遠端偵錯和錯誤修正</span><span class="sxs-lookup"><span data-stu-id="f0bd4-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="f0bd4-179">設定兩個中斷點，然後選取**偵錯**圖示以啟動遠端偵錯程序。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="f0bd4-180">程式碼會在第一個中斷點停止，然後在 [變數] 窗格中顯示參數和變數資訊。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="f0bd4-181">選取**繼續程式**圖示以繼續。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="f0bd4-182">程式碼會在第二個點停止。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-182">The code stops at the second point.</span></span> <span data-ttu-id="f0bd4-183">正如預期，會攔截到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-183">The exception is caught as expected.</span></span>

  ![擲回錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="f0bd4-185">再次選取**繼續程式**圖示。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="f0bd4-186">[HDInsight Spark Submission] \(HDInsight Spark 提交) 視窗會顯示「作業執行失敗」錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![提交錯誤](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="f0bd4-188">若要使用 IntelliJ 偵錯功能動態更新變數值，請再次選取 [偵錯]。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="f0bd4-189">[變數] 窗格會再次出現。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="f0bd4-190">以滑鼠右鍵按一下 [Debug] \(偵錯\) 索引標籤上的目標，然後選取 [Set Value] \(設定值\)。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="f0bd4-191">接下來，輸入變數的新值。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="f0bd4-192">然後選取 **Enter** 儲存值。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-192">Then select **Enter** to save the value.</span></span> 

  ![設定值](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="f0bd4-194">選取**繼續程式**圖示以繼續執行程式。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="f0bd4-195">此時，不會攔截到任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-195">This time, no exception is caught.</span></span> <span data-ttu-id="f0bd4-196">您可以看到專案成功執行而未發生任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f0bd4-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![偵錯而未發生例外狀況](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="f0bd4-198"><a name="seealso"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="f0bd4-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="f0bd4-199">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="f0bd4-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="f0bd4-200">示範</span><span class="sxs-lookup"><span data-stu-id="f0bd4-200">Demo</span></span>
* <span data-ttu-id="f0bd4-201">建立 Scala 專案 (影片)：[Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (建立 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="f0bd4-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="f0bd4-202">遠端偵錯 (影片)：[Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (使用適用於 IntelliJ 的 Azure 工具組對 HDInsight 叢集上的 Spark 應用程式進行遠端偵錯)</span><span class="sxs-lookup"><span data-stu-id="f0bd4-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="f0bd4-203">案例</span><span class="sxs-lookup"><span data-stu-id="f0bd4-203">Scenarios</span></span>
* [<span data-ttu-id="f0bd4-204">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="f0bd4-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f0bd4-205">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="f0bd4-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f0bd4-206">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="f0bd4-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f0bd4-207">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="f0bd4-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f0bd4-208">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="f0bd4-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f0bd4-209">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f0bd4-209">Create and run applications</span></span>
* [<span data-ttu-id="f0bd4-210">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="f0bd4-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f0bd4-211">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="f0bd4-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f0bd4-212">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="f0bd4-212">Tools and extensions</span></span>
* [<span data-ttu-id="f0bd4-213">使用適用於 IntelliJ 的 Azure 工具組建立適用於 HDInsight 叢集的 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="f0bd4-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f0bd4-214">使用適用於 IntelliJ 的 Azure 工具組透過 VPN 對 Spark 應用程式進行遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="f0bd4-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f0bd4-215">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f0bd4-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="f0bd4-216">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具建立 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="f0bd4-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="f0bd4-217">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="f0bd4-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f0bd4-218">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="f0bd4-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f0bd4-219">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="f0bd4-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f0bd4-220">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="f0bd4-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f0bd4-221">管理資源</span><span class="sxs-lookup"><span data-stu-id="f0bd4-221">Manage resources</span></span>
* [<span data-ttu-id="f0bd4-222">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="f0bd4-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f0bd4-223">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="f0bd4-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
