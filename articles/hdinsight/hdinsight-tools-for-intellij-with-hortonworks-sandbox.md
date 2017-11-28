---
title: "透過 Hortonworks 沙箱使用 Azure Toolkit for IntelliJ | Microsoft Docs"
description: "了解如何透過 Hortonworks 沙箱使用 Azure Toolkit for IntelliJ 中的 HDInsight 工具。"
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
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="7a0a5-104">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7a0a5-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="7a0a5-105">瞭解如何使用 HDInsight Tools for IntelliJ 開發 Apache Scala 應用程式，然後在工作站上執行的 [Hortonworks 沙箱](http://hortonworks.com/products/sandbox/)上測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="7a0a5-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/)是 Java 整合式開發環境 (IDE)，可用來開發電腦軟體。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="7a0a5-107">在 Hortonworks 沙箱上開發並測試應用程式之後，您可以將它們移至 [Azure HDInsight](hdinsight-hadoop-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a0a5-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a0a5-108">Prerequisites</span></span>

<span data-ttu-id="7a0a5-109">開始進行本教學課程之前，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="7a0a5-110">在您的本機環境執行的 Hortonworks 沙箱上要有 Hortonworks Data Platform (HDP) 2.4。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="7a0a5-111">若要設定 HDP，請參閱[透過虛擬機器的 Hadoop 沙箱開始使用 Hadoop 生態系統](hdinsight-hadoop-emulator-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="7a0a5-112">HDInsight Tools for IntelliJ 只經過 HDP 2.4 測試。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="7a0a5-113">若要取得 HDP 2.4，請在 **Hortonworks 沙箱下載網站**展開 [Hortonworks 沙箱封存][](http://hortonworks.com/downloads/#sandbox)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="7a0a5-114">[Java Developer Kit (JDK) 1.8 版或更新版本](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="7a0a5-115">Azure Toolkit for IntelliJ 需要 JDK。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="7a0a5-116">[IntelliJ IDEA community 版本](https://www.jetbrains.com/idea/download)搭配使用 [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) 外掛程式與 [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="7a0a5-117">適用於 IntelliJ 的 HDInsight 工具是適用於 IntelliJ 的 Azure 工具組的一部分。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="7a0a5-118">若要安裝外掛程式，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="7a0a5-119">開啟 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="7a0a5-120">在 [歡迎使用] 畫面上，選取 [設定]，然後按一下 [外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="7a0a5-121">選取左下角的 [安裝 JetBrains 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="7a0a5-122">使用搜尋功能來搜尋 **Scala**，然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="7a0a5-123">選取 [重新啟動 IntelliJ IDEA] 以完成安裝。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="7a0a5-124">重複步驟 4 和 5 以安裝 [Azure Toolkit for IntelliJ]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="7a0a5-125">如需詳細資訊，請參閱[安裝 Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="7a0a5-126">建立 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a0a5-126">Create a Spark Scala application</span></span>

<span data-ttu-id="7a0a5-127">在本節中，您會使用 IntelliJ IDEA 建立範例 Scala 專案。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="7a0a5-128">在下節中，您要在提交專案之前，將 IntelliJ IDEA 連結至 Hortonworks 沙箱 (模擬器)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="7a0a5-129">從您的工作站開啟 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="7a0a5-130">在 [新增專案]  對話方塊中，執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="7a0a5-131">a.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-131">a.</span></span> <span data-ttu-id="7a0a5-132">選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="7a0a5-133">b.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-133">b.</span></span> <span data-ttu-id="7a0a5-134">在 [建置工具] 清單中，根據您的需求選取下列任一項目：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="7a0a5-135">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="7a0a5-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="7a0a5-136">**SBT**，以管理相依性並建置 Scala 專案</span><span class="sxs-lookup"><span data-stu-id="7a0a5-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![[新增專案] 對話方塊](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="7a0a5-138">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-138">Select **Next**.</span></span>

3. <span data-ttu-id="7a0a5-139">在下一個 [新增專案]  對話方塊中，執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-139">In the next **New Project** dialog box, do the following:</span></span>

    ![建立 IntelliJ Scala 專案屬性](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="7a0a5-141">a.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-141">a.</span></span> <span data-ttu-id="7a0a5-142">在 [專案名稱] 方塊中，輸入專案名稱。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="7a0a5-143">b.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-143">b.</span></span> <span data-ttu-id="7a0a5-144">在 [專案位置] 方塊中，輸入專案位置。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="7a0a5-145">c.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-145">c.</span></span> <span data-ttu-id="7a0a5-146">在 [專案 SDK] 下拉式清單旁邊，選取 [新增]，並選取 [JDK]，然後指定 Java JDK 1.7 版或更新版本的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="7a0a5-147">選取 [Java 1.8] (適用於 Spark 2.x 叢集)，或選取 [Java 1.7] (適用於 Spark 1.x 叢集)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="7a0a5-148">預設位置是 C:\Program Files\Java\jdk1.8.x_xxx。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="7a0a5-149">d.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-149">d.</span></span> <span data-ttu-id="7a0a5-150">在 [Spark 版本] 下拉式清單中，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="7a0a5-151">如果 Spark 叢集是 2.0 以前的版本，請選取 [Spark 1.x]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="7a0a5-152">否則，請選取 [Spark2.x]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="7a0a5-153">此範例使用 Spark 1.6.2 (Scala 2.10.5)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="7a0a5-154">確定您使用標示為 Scala 2.10.x 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="7a0a5-155">請勿使用標示為 Scala 2.11.x 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="7a0a5-156">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-156">Select **Finish**.</span></span>

5. <span data-ttu-id="7a0a5-157">如果**專案**檢視尚未開啟，請按下 **Alt + 1** 加以開啟。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="7a0a5-158">在 [專案總管] 中，展開專案，然後選取 [src]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="7a0a5-159">以滑鼠右鍵按一下 [src]，指向 [新增]，然後選取 [Scala 類別]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="7a0a5-160">在 [名稱] 方塊中輸入名稱，並且在 [種類] 方塊中選取 [物件]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![[建立新的 Scala 類別] 視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="7a0a5-162">在 .scala 檔案中，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-162">In the .scala file, paste the following code:</span></span>

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

10. <span data-ttu-id="7a0a5-163">在 [建置] 功能表上，選取 [建置專案]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="7a0a5-164">請確定已順利完成編譯。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="7a0a5-165">連結至 HortonWorks 沙箱</span><span class="sxs-lookup"><span data-stu-id="7a0a5-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7a0a5-166">您連結至 Hortonworks 沙箱 (模擬器) 前，必須有現有的 IntelliJ 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="7a0a5-167">若要連結至模擬器，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="7a0a5-168">在 IntelliJ 中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="7a0a5-169">在 [檢視] 功能表上，選取 [工具視窗]，然後選取 [Azure Explorer]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="7a0a5-170">展開 [Azure]，以滑鼠右鍵按一下 [HDInsight]，然後選取 [連結模擬器]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="7a0a5-171">在 [連結新的模擬器] 視窗中，輸入您已對於 Hortonworks 沙箱的根帳戶設定的密碼，並輸入如下列螢幕擷取畫面所示相類似的值，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![[連結新的模擬器] 視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="7a0a5-173">若要設定模擬器，請選取[是]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="7a0a5-174">成功連接模擬器時，[HDInsight] 節點會列出該模擬器 (Hortonworks 沙箱)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="7a0a5-175">將 Spark Scala 應用程式提交至 Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="7a0a5-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7a0a5-176">在將 IntelliJ IDEA 連結至模擬器之後，您就可以提交專案。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="7a0a5-177">若要將專案提交至模擬器，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="7a0a5-178">在 [專案總管] 中，以滑鼠右鍵按一下專案，然後選取 [將 Spark 應用程式提交給 HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="7a0a5-179">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7a0a5-179">Do the following:</span></span>

    <span data-ttu-id="7a0a5-180">a.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-180">a.</span></span> <span data-ttu-id="7a0a5-181">在 [Spark 叢集 (僅限 Linux)] 下拉式清單中，選取您的本機 Hortonworks 沙箱。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="7a0a5-182">b.</span><span class="sxs-lookup"><span data-stu-id="7a0a5-182">b.</span></span> <span data-ttu-id="7a0a5-183">在 [主要類別名稱] 方塊中，選擇或輸入主要類別名稱。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="7a0a5-184">在本教學課程中，名稱是 **GroupByTest**。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="7a0a5-185">選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-185">Select **Submit**.</span></span> <span data-ttu-id="7a0a5-186">Spark 提交工具視窗會顯示工作提交記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a0a5-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a0a5-187">Next steps</span></span>

- <span data-ttu-id="7a0a5-188">若要了解如何使用 HDInsight Tools for IntelliJ 建立 HDInsight 的 Spark 應用程式，請至[使用 Azure Toolkit for IntelliJ 中的 HDInsight 工具建立 HDInsight Spark Linux 叢集的 Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="7a0a5-189">若要觀看 HDInsight Tools for IntelliJ 的影片，請至[介紹用於開發 Spark 的 HDInsight Tools for IntelliJ](https://www.youtube.com/watch?v=YTZzYVgut6c)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="7a0a5-190">若要了解如何從遠端使用工具組在 HDInsight 上透過 SSH 對 Spark 應用程式進行偵錯，請至[在 HDInsight Spark Linux 叢集上從遠端使用 Azure Toolkit for IntelliJ 透過 SSH 對 Spark 應用程式進行偵錯](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="7a0a5-191">若要了解如何從遠端使用工具組在 HDInsight 上透過 VPN 對 Spark 應用程式進行偵錯，請至[在 HDInsight Spark Linux 叢集上從遠端使用 Azure Toolkit for IntelliJ 中的 HDInsight 工具對 Spark 應用程式進行偵錯](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="7a0a5-192">若要了解如何使用 HDInsight Tools for Eclipse 建立 Spark 應用程式，請至[使用 Azure Toolkit for Eclipse 中的 HDInsight 工具建立 Spark 應用程式](hdinsight-apache-spark-eclipse-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="7a0a5-193">若要觀看 HDInsight Tools for Eclipse 的影片，請至[使用 HDInsight Tool for Eclipse 建立 Spark 應用程式](https://mix.office.com/watch/1rau2mopb6fha)。</span><span class="sxs-lookup"><span data-stu-id="7a0a5-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
