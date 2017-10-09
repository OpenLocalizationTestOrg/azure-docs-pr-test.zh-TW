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
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="9103d-104">透過 Hortonworks 沙箱使用 HDInsight Tools for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="9103d-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="9103d-105">了解 toouse HDInsight Tools for IntelliJ toodevelop Apache Scala 應用程式以及測試工作流程如何 hello 應用程式上[Hortonworks 沙箱](http://hortonworks.com/products/sandbox/)在工作站上執行。</span><span class="sxs-lookup"><span data-stu-id="9103d-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="9103d-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/)是 Java 整合式開發環境 (IDE)，可用來開發電腦軟體。</span><span class="sxs-lookup"><span data-stu-id="9103d-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="9103d-107">您所開發並測試過您的應用程式上的 Hortonworks 沙箱之後，您可以將它們移過[Azure HDInsight](hdinsight-hadoop-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9103d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="9103d-108">Prerequisites</span></span>

<span data-ttu-id="9103d-109">開始進行本教學課程之前，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="9103d-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="9103d-110">在您的本機環境執行的 Hortonworks 沙箱上要有 Hortonworks Data Platform (HDP) 2.4。</span><span class="sxs-lookup"><span data-stu-id="9103d-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="9103d-111">tooconfigure HDP，請參閱[開始 hello Hadoop 生態系統，與虛擬機器上的 Hadoop 沙箱](hdinsight-hadoop-emulator-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="9103d-112">HDInsight Tools for IntelliJ 只經過 HDP 2.4 測試。</span><span class="sxs-lookup"><span data-stu-id="9103d-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="9103d-113">展開 tooget HDP 2.4 **Hortonworks 沙箱封存**上 hello [Hortonworks 沙箱下載網站](http://hortonworks.com/downloads/#sandbox)。</span><span class="sxs-lookup"><span data-stu-id="9103d-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="9103d-114">[Java Developer Kit (JDK) 1.8 版或更新版本](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。</span><span class="sxs-lookup"><span data-stu-id="9103d-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="9103d-115">如 IntelliJ 需要 hello Azure Toolkit JDK。</span><span class="sxs-lookup"><span data-stu-id="9103d-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="9103d-116">[IntelliJ 概念 community edition](https://www.jetbrains.com/idea/download)以 hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala)外掛程式和 hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md)外掛程式。</span><span class="sxs-lookup"><span data-stu-id="9103d-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="9103d-117">使用 Azure Toolkit for IntelliJ hello 的一部份 IntelliJ HDInsight 工具。</span><span class="sxs-lookup"><span data-stu-id="9103d-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="9103d-118">tooinstall hello 外掛程式，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9103d-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="9103d-119">開啟 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="9103d-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="9103d-120">在 hello ** 褖畫惎**畫面上，選取**設定**，然後選取**外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="9103d-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="9103d-121">選取**安裝 JetBrains 外掛程式**hello 左下角。</span><span class="sxs-lookup"><span data-stu-id="9103d-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="9103d-122">使用的 hello 搜尋函式 toosearch **Scala**，然後選取**安裝**。</span><span class="sxs-lookup"><span data-stu-id="9103d-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="9103d-123">選取**重新啟動 IntelliJ 概念**toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="9103d-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="9103d-124">重複步驟 4 和 5 tooinstall hello **Azure Toolkit for IntelliJ**。</span><span class="sxs-lookup"><span data-stu-id="9103d-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="9103d-125">如需詳細資訊，請參閱[安裝 hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="9103d-126">建立 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="9103d-126">Create a Spark Scala application</span></span>

<span data-ttu-id="9103d-127">在本節中，您會使用 IntelliJ IDEA 建立範例 Scala 專案。</span><span class="sxs-lookup"><span data-stu-id="9103d-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="9103d-128">Hello 下一節，您將連結 IntelliJ 概念 toohello Hortonworks 沙箱 （模擬器） 之前您送出 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="9103d-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="9103d-129">從您的工作站開啟 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="9103d-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="9103d-130">在 hello**新專案**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9103d-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="9103d-131">a.</span><span class="sxs-lookup"><span data-stu-id="9103d-131">a.</span></span> <span data-ttu-id="9103d-132">選取 [HDInsight] > [HDInsight 上的 Spark (Scala)]。</span><span class="sxs-lookup"><span data-stu-id="9103d-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="9103d-133">b.</span><span class="sxs-lookup"><span data-stu-id="9103d-133">b.</span></span> <span data-ttu-id="9103d-134">在 hello**建置工具**清單中，選取下列、 根據 tooyour 需要 hello:</span><span class="sxs-lookup"><span data-stu-id="9103d-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="9103d-135">**Maven**，以支援 Scala 專案建立精靈</span><span class="sxs-lookup"><span data-stu-id="9103d-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="9103d-136">**SBT**、 管理 hello 相依性和建置 hello Scala 專案</span><span class="sxs-lookup"><span data-stu-id="9103d-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![hello 新增專案 對話方塊](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="9103d-138">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9103d-138">Select **Next**.</span></span>

3. <span data-ttu-id="9103d-139">在 hello 下一步**新專案**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9103d-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![建立 IntelliJ Scala 專案屬性](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="9103d-141">a.</span><span class="sxs-lookup"><span data-stu-id="9103d-141">a.</span></span> <span data-ttu-id="9103d-142">在 hello**專案名稱**方塊中，輸入專案名稱。</span><span class="sxs-lookup"><span data-stu-id="9103d-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="9103d-143">b.</span><span class="sxs-lookup"><span data-stu-id="9103d-143">b.</span></span> <span data-ttu-id="9103d-144">在 hello**專案位置**方塊中，輸入專案位置。</span><span class="sxs-lookup"><span data-stu-id="9103d-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="9103d-145">c.</span><span class="sxs-lookup"><span data-stu-id="9103d-145">c.</span></span> <span data-ttu-id="9103d-146">下一步 toohello**專案 SDK**下拉式清單中，選取**新增**，選取**JDK**，然後指定 hello 的 Java JDK 1.7 版或更新版本的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9103d-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="9103d-147">選取**Java 1.8** hello Spark 2.x 叢集，或選取**Java 1.7** hello Spark 1.x 叢集。</span><span class="sxs-lookup"><span data-stu-id="9103d-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="9103d-148">hello 預設位置是 C:\Program Files\Java\jdk1.8.x_xxx。</span><span class="sxs-lookup"><span data-stu-id="9103d-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="9103d-149">d.</span><span class="sxs-lookup"><span data-stu-id="9103d-149">d.</span></span> <span data-ttu-id="9103d-150">在 hello **Spark 版本**下拉式清單中，Scala 專案建立精靈 Spark SDK 和 Scala SDK 整合 hello 正確版本。</span><span class="sxs-lookup"><span data-stu-id="9103d-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="9103d-151">如果 hello Spark 叢集版本早於 2.0，請選取**二手 1.x**。</span><span class="sxs-lookup"><span data-stu-id="9103d-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="9103d-152">否則，請選取 [Spark2.x]。</span><span class="sxs-lookup"><span data-stu-id="9103d-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="9103d-153">此範例使用 Spark 1.6.2 (Scala 2.10.5)。</span><span class="sxs-lookup"><span data-stu-id="9103d-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="9103d-154">請確定您使用 hello 儲存機制標示 Scala 2.10.x。</span><span class="sxs-lookup"><span data-stu-id="9103d-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="9103d-155">請勿使用 hello 儲存機制標示 Scala 2.11.x。</span><span class="sxs-lookup"><span data-stu-id="9103d-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="9103d-156">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="9103d-156">Select **Finish**.</span></span>

5. <span data-ttu-id="9103d-157">如果 hello**專案**檢視尚未開啟，請按**Alt + 1** tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="9103d-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="9103d-158">在**Project Explorer**，展開 hello 專案，然後選取**src**。</span><span class="sxs-lookup"><span data-stu-id="9103d-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="9103d-159">以滑鼠右鍵按一下**src**，點太**新增**，然後選取**Scala 類別**。</span><span class="sxs-lookup"><span data-stu-id="9103d-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="9103d-160">在 hello**名稱**方塊中，輸入名稱，在 hello**種類**方塊中，選取**物件**，然後選取**[確定]**。</span><span class="sxs-lookup"><span data-stu-id="9103d-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![hello 建立 Scala 類別視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="9103d-162">在 hello.scala 檔案中，貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="9103d-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="9103d-163">在 hello**建置**功能表上，選取**建置專案**。</span><span class="sxs-lookup"><span data-stu-id="9103d-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="9103d-164">請確定 hello 編譯已順利完成。</span><span class="sxs-lookup"><span data-stu-id="9103d-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="9103d-165">連結 toohello Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="9103d-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="9103d-166">您可以將連結 tooa Hortonworks 沙箱 （模擬器） 之前，您必須具有現有 IntelliJ 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9103d-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="9103d-167">toolink tooan 模擬器中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9103d-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="9103d-168">開啟 hello IntelliJ 中的專案。</span><span class="sxs-lookup"><span data-stu-id="9103d-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="9103d-169">在 hello**檢視**功能表上，選取**工具視窗**，然後選取**Azure 總管**。</span><span class="sxs-lookup"><span data-stu-id="9103d-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="9103d-170">展開 [Azure]，以滑鼠右鍵按一下 [HDInsight]，然後選取 [連結模擬器]。</span><span class="sxs-lookup"><span data-stu-id="9103d-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="9103d-171">在 hello**連結新的模擬器**視窗中，輸入您設定的 hello 根帳號的 hello Hortonworks 沙箱，hello 下列螢幕擷取畫面中輸入值類似 toothose，然後選取 hello 密碼**確定**.</span><span class="sxs-lookup"><span data-stu-id="9103d-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![hello 」 連結新的模擬器 」 視窗](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="9103d-173">tooconfigure hello 模擬器中，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="9103d-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="9103d-174">當 hello 模擬器已成功連接時，hello 模擬器 （Hortonworks 沙箱） 會列在 hello HDInsight 節點。</span><span class="sxs-lookup"><span data-stu-id="9103d-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="9103d-175">送出 hello Spark Scala 應用程式 toohello Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="9103d-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="9103d-176">您已連結 IntelliJ 概念 toohello 模擬器之後，您可以提交您的專案。</span><span class="sxs-lookup"><span data-stu-id="9103d-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="9103d-177">toosubmit 專案 tooan 模擬器中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9103d-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="9103d-178">在**Project Explorer**，hello 專案上按一下滑鼠右鍵，然後選取**提交 Spark 應用程式 tooHDInsight**。</span><span class="sxs-lookup"><span data-stu-id="9103d-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="9103d-179">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9103d-179">Do hello following:</span></span>

    <span data-ttu-id="9103d-180">a.</span><span class="sxs-lookup"><span data-stu-id="9103d-180">a.</span></span> <span data-ttu-id="9103d-181">在 hello **Spark 叢集 (僅 Linux)**下拉式清單中，選取您本機的 Hortonworks 沙箱。</span><span class="sxs-lookup"><span data-stu-id="9103d-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="9103d-182">b.</span><span class="sxs-lookup"><span data-stu-id="9103d-182">b.</span></span> <span data-ttu-id="9103d-183">在 hello**主要類別名稱**方塊中，選擇或輸入 hello 主要的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="9103d-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="9103d-184">此教學課程，hello 名稱是**GroupByTest**。</span><span class="sxs-lookup"><span data-stu-id="9103d-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="9103d-185">選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="9103d-185">Select **Submit**.</span></span> <span data-ttu-id="9103d-186">hello 作業送出記錄檔會顯示 hello Spark 提交工具視窗中。</span><span class="sxs-lookup"><span data-stu-id="9103d-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9103d-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9103d-187">Next steps</span></span>

- <span data-ttu-id="9103d-188">如何 toocreate Spark 應用程式 HDInsight 的使用 HDInsight Tools for IntelliJ，都會太 toolearn[Azure Toolkit for HDInsight Spark Linux 叢集的 IntelliJ toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-intellij-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="9103d-189">toowatch HDInsight Tools for IntelliJ，視訊跳過[導入 HDInsight Tools for Spark 開發 IntelliJ](https://www.youtube.com/watch?v=YTZzYVgut6c)。</span><span class="sxs-lookup"><span data-stu-id="9103d-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="9103d-190">toolearn toodebug Spark 應用程式使用 hello 在透過 SSH 的 HDInsight 上的遠端工具組如何移過[進行遠端偵錯 Spark 的應用程式使用 Azure Toolkit 在 HDInsight 叢集上透過 SSH IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="9103d-191">toolearn toodebug Spark 應用程式使用 hello 在透過 VPN，HDInsight 上的遠端工具組如何移過[Azure Toolkit for IntelliJ HDInsight Spark Linux 叢集上從遠端 toodebug Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="9103d-192">toolearn toouse HDInsight Tools for Eclipse toocreate Spark 應用程式如何太移[Azure Toolkit for Eclipse toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="9103d-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="9103d-193">toowatch HDInsight Tools for Eclipse，視訊跳過[Eclipse toocreate Spark 應用程式的使用 HDInsight 工具](https://mix.office.com/watch/1rau2mopb6fha)。</span><span class="sxs-lookup"><span data-stu-id="9103d-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
