---
title: "aaaDeploy 和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲 |Microsoft 文件"
description: "了解 toodeploy、 監視和管理 Apache Storm 拓撲以 Linux 為基礎的 HDInsight 上使用 hello Storm 儀表板的方式。 使用適用於 Visual Studio 的 Hadoop 工具。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="b4a94-104">部署和管理 HDInsight 上的 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="b4a94-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="b4a94-105">在本文件中，了解 hello 的管理和監視 Storm 拓撲 Storm HDInsight 叢集上執行的基本概念。</span><span class="sxs-lookup"><span data-stu-id="b4a94-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4a94-106">hello 本文章中的步驟需要以 Linux 為基礎的 Storm HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="b4a94-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="b4a94-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="b4a94-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b4a94-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="b4a94-109">如需部署和監視以 Windows 為基礎的 HDInsight 上的拓撲的詳細資訊，請參閱 [部署和管理以 Windows 為基礎的 HDInsight 上的Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="b4a94-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b4a94-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b4a94-110">Prerequisites</span></span>

* <span data-ttu-id="b4a94-111">**HDInsight 叢集上以 Linux 為基礎的 Storm**：請參閱 [開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) 以取得建立叢集的步驟</span><span class="sxs-lookup"><span data-stu-id="b4a94-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="b4a94-112">(選擇性) **熟悉 SSH 和 SCP**︰如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="b4a94-113">（選擇性）**Visual Studio**: Azure SDK 2.5.1 或更新版本和 hello Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b4a94-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="b4a94-114">如需詳細資訊，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="b4a94-115">下列版本的 Visual Studio 中的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="b4a94-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="b4a94-116">Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="b4a94-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="b4a94-117">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="b4a94-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="b4a94-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b4a94-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="b4a94-119">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="b4a94-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="b4a94-120">Visual Studio 2017 (任何版本)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="b4a94-121">資料湖 Tools for Visual Studio 2017 hello Azure 工作負載的一部分安裝。</span><span class="sxs-lookup"><span data-stu-id="b4a94-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="b4a94-122">提交拓撲︰Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4a94-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="b4a94-123">hello HDInsight 工具可以使用的 toosubmit C# 或混合式拓撲 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="b4a94-124">下列步驟的 hello 使用範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4a94-124">hello following steps use a sample application.</span></span> <span data-ttu-id="b4a94-125">如需使用 hello HDInsight Tools 來建立您自己的拓撲資訊，請參閱[開發 C# 拓撲使用 hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="b4a94-126">如果您在 Visual studio 並不安裝 hello hello Data Lake 工具最新版本，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4a94-127">hello 資料湖 Tools for Visual Studio 之前呼叫了 hello HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b4a94-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="b4a94-128">資料湖 Tools for Visual Studio 隨附的 hello __Azure 工作負載__for Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="b4a94-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="b4a94-129">開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。</span><span class="sxs-lookup"><span data-stu-id="b4a94-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="b4a94-130">在 hello**新專案**對話方塊方塊中，展開 **已安裝** > **範本**，然後選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="b4a94-131">從範本 hello 清單，選取**Storm 範例**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="b4a94-132">在 hello hello 對話方塊下方，輸入 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b4a94-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="b4a94-134">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b4a94-135">如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="b4a94-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="b4a94-136">如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。</span><span class="sxs-lookup"><span data-stu-id="b4a94-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="b4a94-137">選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="b4a94-138">您可以監視是否 hello 提交成功使用 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="b4a94-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="b4a94-139">提交拓撲： SSH 和 hello Storm 命令</span><span class="sxs-lookup"><span data-stu-id="b4a94-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="b4a94-140">使用 SSH tooconnect toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="b4a94-141">取代**USERNAME** hello SSH 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="b4a94-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="b4a94-142">將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="b4a94-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="b4a94-143">如需有關使用 SSH tooconnect tooyour HDInsight 叢集，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b4a94-144">使用下列命令 toostart 範例拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="b4a94-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="b4a94-145">此命令會啟動 hello WordCount 拓撲範例 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="b4a94-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="b4a94-146">此拓撲隨機產生的句子與每個字的計數 hello 發生 hello 句子。</span><span class="sxs-lookup"><span data-stu-id="b4a94-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b4a94-147">提交時拓撲 toohello 叢集，您必須先將 hello jar 檔案包含之前使用 hello hello 叢集`storm`命令。</span><span class="sxs-lookup"><span data-stu-id="b4a94-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="b4a94-148">toocopy hello 檔案 toohello 叢集，您可以使用 hello`scp`命令。</span><span class="sxs-lookup"><span data-stu-id="b4a94-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="b4a94-149">例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="b4a94-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="b4a94-150">hello WordCount 範例中，與其他 storm 入門範例，已包含在叢集上`/usr/hdp/current/storm-client/contrib/storm-starter/`。</span><span class="sxs-lookup"><span data-stu-id="b4a94-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="b4a94-151">提交拓撲︰以程式設計的方式</span><span class="sxs-lookup"><span data-stu-id="b4a94-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="b4a94-152">您可以與 hello Nimbus 叢集中裝載的服務進行通訊，以程式設計方式部署拓撲 tooStorm HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="b4a94-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="b4a94-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology)提供範例示範的 Java 應用程式如何 toodeploy 並開始透過 hello Nimbus 服務拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="b4a94-154">監視和管理︰Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4a94-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="b4a94-155">當您已成功提交拓撲，但是使用 Visual Studio 時，hello **Storm 拓撲**檢視會顯示 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="b4a94-156">從 hello 列出 tooview hello 執行拓撲的相關資訊，請選取 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="b4a94-158">您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="b4a94-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="b4a94-159">Hello spouts 或釘 tooview 這些元件的資訊，請選取 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="b4a94-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="b4a94-160">隨即會針對每個選取的項目開啟新的視窗。</span><span class="sxs-lookup"><span data-stu-id="b4a94-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="b4a94-161">停用和重新啟動</span><span class="sxs-lookup"><span data-stu-id="b4a94-161">Deactivate and reactivate</span></span>

<span data-ttu-id="b4a94-162">停用拓撲會暫停它，直到刪除或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b4a94-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="b4a94-163">tooperform 這些作業，使用 hello__停用__和__重新啟用__按鈕上方的 hello hello__拓撲摘要__。</span><span class="sxs-lookup"><span data-stu-id="b4a94-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="b4a94-164">重新平衡</span><span class="sxs-lookup"><span data-stu-id="b4a94-164">Rebalance</span></span>

<span data-ttu-id="b4a94-165">重新平衡的拓撲，可讓 hello 系統 toorevise hello 平行處理原則的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="b4a94-166">例如，如果您已調整大小 hello 叢集 tooadd 詳細資訊，重新平衡可讓拓樸 toosee hello 新節點。</span><span class="sxs-lookup"><span data-stu-id="b4a94-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="b4a94-167">toorebalance 拓撲中，使用 hello__重新平衡__按鈕上方的 hello hello__拓撲摘要__。</span><span class="sxs-lookup"><span data-stu-id="b4a94-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="b4a94-168">第一次重新平衡拓撲 hello 拓撲，就會停用再重新工作者平均分配 hello 叢集中，然後最後會傳回 hello 拓撲 toohello 狀態重新平衡發生之前。</span><span class="sxs-lookup"><span data-stu-id="b4a94-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="b4a94-169">因此如果 hello 拓撲是作用中，它再次變成作用中。</span><span class="sxs-lookup"><span data-stu-id="b4a94-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="b4a94-170">如果已停用，它就會保持停用。</span><span class="sxs-lookup"><span data-stu-id="b4a94-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="b4a94-171">終止拓撲</span><span class="sxs-lookup"><span data-stu-id="b4a94-171">Kill a topology</span></span>

<span data-ttu-id="b4a94-172">Storm 拓撲會繼續執行，直到已停止或刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="b4a94-173">toostop 拓撲中，使用 hello __Kill__按鈕上方的 hello hello__拓撲摘要__。</span><span class="sxs-lookup"><span data-stu-id="b4a94-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="b4a94-174">監視和管理： SSH 和 hello Storm 命令</span><span class="sxs-lookup"><span data-stu-id="b4a94-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="b4a94-175">hello`storm`公用程式可讓您從 hello 命令列執行拓樸 toowork。</span><span class="sxs-lookup"><span data-stu-id="b4a94-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="b4a94-176">使用 `storm -h` 以取得完整的命令清單。</span><span class="sxs-lookup"><span data-stu-id="b4a94-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="b4a94-177">列出拓撲</span><span class="sxs-lookup"><span data-stu-id="b4a94-177">List topologies</span></span>

<span data-ttu-id="b4a94-178">使用下列命令 toolist hello 所有正在執行的拓撲：</span><span class="sxs-lookup"><span data-stu-id="b4a94-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="b4a94-179">此命令會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="b4a94-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="b4a94-180">停用和重新啟動</span><span class="sxs-lookup"><span data-stu-id="b4a94-180">Deactivate and reactivate</span></span>

<span data-ttu-id="b4a94-181">停用拓撲會暫停它，直到刪除或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b4a94-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="b4a94-182">使用下列命令 toodeactivate hello，並重新啟動：</span><span class="sxs-lookup"><span data-stu-id="b4a94-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="b4a94-183">刪除執行中拓撲</span><span class="sxs-lookup"><span data-stu-id="b4a94-183">Kill a running topology</span></span>

<span data-ttu-id="b4a94-184">Storm 拓撲一旦啟動之後，就會繼續執行直到停止。</span><span class="sxs-lookup"><span data-stu-id="b4a94-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="b4a94-185">toostop 拓撲中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b4a94-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="b4a94-186">重新平衡</span><span class="sxs-lookup"><span data-stu-id="b4a94-186">Rebalance</span></span>

<span data-ttu-id="b4a94-187">重新平衡的拓撲，可讓 hello 系統 toorevise hello 平行處理原則的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="b4a94-188">例如，如果您已調整大小 hello 叢集 tooadd 詳細資訊，重新平衡可讓拓樸 toosee hello 新節點。</span><span class="sxs-lookup"><span data-stu-id="b4a94-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="b4a94-189">第一次重新平衡拓撲 hello 拓撲，就會停用再重新工作者平均分配 hello 叢集中，然後最後會傳回 hello 拓撲 toohello 狀態重新平衡發生之前。</span><span class="sxs-lookup"><span data-stu-id="b4a94-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="b4a94-190">因此如果 hello 拓撲是作用中，它再次變成作用中。</span><span class="sxs-lookup"><span data-stu-id="b4a94-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="b4a94-191">如果已停用，它就會保持停用。</span><span class="sxs-lookup"><span data-stu-id="b4a94-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="b4a94-192">監視和管理︰Storm UI</span><span class="sxs-lookup"><span data-stu-id="b4a94-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="b4a94-193">hello Storm UI 提供 web 介面，用於執行的拓撲，並包含在您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="b4a94-194">tooview hello Storm UI，使用 web 瀏覽器 tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**，其中**CLUSTERNAME**是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="b4a94-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a94-195">如果使用者名稱和密碼，請詢問 tooprovide，請輸入 hello 叢集系統管理員 （管理員） 和密碼時使用建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4a94-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="b4a94-196">主頁面</span><span class="sxs-lookup"><span data-stu-id="b4a94-196">Main page</span></span>

<span data-ttu-id="b4a94-197">hello Storm UI hello 主頁面上提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b4a94-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="b4a94-198">**叢集摘要**: hello Storm 叢集的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="b4a94-199">**拓撲摘要**：執行中拓撲的清單。</span><span class="sxs-lookup"><span data-stu-id="b4a94-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="b4a94-200">使用有關特定拓撲中這個區段 tooview hello 連結的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="b4a94-201">**摘要的監督員**: hello Storm 監督者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="b4a94-202">**Nimbus 組態**: Nimbus hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="b4a94-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="b4a94-203">拓撲摘要</span><span class="sxs-lookup"><span data-stu-id="b4a94-203">Topology summary</span></span>

<span data-ttu-id="b4a94-204">選取連結從 hello**拓撲摘要**區段會顯示 hello 下列 hello 拓撲的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="b4a94-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="b4a94-205">**摘要的拓樸**: hello 拓撲的相關基本資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="b4a94-206">**拓樸動作**: hello 拓撲，您可以執行管理動作。</span><span class="sxs-lookup"><span data-stu-id="b4a94-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="b4a94-207">**啟用**：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="b4a94-208">**停用**：暫停執行中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="b4a94-209">**重新平衡**： 調整 hello 拓樸的 hello 平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="b4a94-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="b4a94-210">之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="b4a94-211">這項作業允許 hello 拓撲 tooadjust 平行處理原則 toocompensate hello 增加或減少 hello 叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="b4a94-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="b4a94-212">如需詳細資訊，請參閱<a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">了解 hello 平行處理原則的 Storm 拓撲</a>。</span><span class="sxs-lookup"><span data-stu-id="b4a94-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="b4a94-213">**Kill**: hello 指定逾時之後終止 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="b4a94-214">**拓樸 stats**: hello 拓撲的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="b4a94-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="b4a94-215">tooset hello hello 剩餘項目在 hello 頁面上的時間範圍，請使用 hello hello 連結**視窗**資料行。</span><span class="sxs-lookup"><span data-stu-id="b4a94-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="b4a94-216">**Spouts**: hello spouts hello 拓撲所使用。</span><span class="sxs-lookup"><span data-stu-id="b4a94-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="b4a94-217">使用此區段 tooview 中的 hello 連結特定 spouts 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="b4a94-218">**釘**: hello hello 拓撲所使用的攻擊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="b4a94-219">使用此區段 tooview 中的 hello 連結特定攻擊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="b4a94-220">**拓撲組態**: hello 選取拓撲的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b4a94-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="b4a94-221">Spout 和 Bolt 摘要</span><span class="sxs-lookup"><span data-stu-id="b4a94-221">Spout and Bolt summary</span></span>

<span data-ttu-id="b4a94-222">選取從 hello spout **Spouts**或**釘**區段會顯示 hello 遵循 hello 選取項目的資訊：</span><span class="sxs-lookup"><span data-stu-id="b4a94-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="b4a94-223">**元件摘要**: hello spout 或閃電的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="b4a94-224">**Spout 閃電 stats**: hello 相關統計資料 spout 或閃電。</span><span class="sxs-lookup"><span data-stu-id="b4a94-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="b4a94-225">tooset hello hello 剩餘項目在 hello 頁面上的時間範圍，請使用 hello hello 連結**視窗**資料行。</span><span class="sxs-lookup"><span data-stu-id="b4a94-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="b4a94-226">**輸入 stats** （只有閃電）： hello 的相關資訊輸入 hello 閃電所耗用的資料流。</span><span class="sxs-lookup"><span data-stu-id="b4a94-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="b4a94-227">**輸出 stats**: spout 或閃電關於發出由此 hello 資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="b4a94-228">**執行程式**: hello spout 或閃電 hello 執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="b4a94-229">選取 hello**連接埠**這個執行個體所產生的項目特定的執行程式 tooview 診斷資訊的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b4a94-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="b4a94-230">**錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="b4a94-231">監視和管理︰REST API</span><span class="sxs-lookup"><span data-stu-id="b4a94-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="b4a94-232">hello REST API，乃是建立 hello Storm UI，讓您可以執行類似的管理和監視功能，可使用 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="b4a94-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="b4a94-233">您可以使用 hello REST API toocreate 自訂工具來管理和監視 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b4a94-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="b4a94-234">如需詳細資訊，請參閱 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="b4a94-235">hello 下列資訊為特定 toousing hello 與 HDInsight 上的 Apache Storm 的 REST API。</span><span class="sxs-lookup"><span data-stu-id="b4a94-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4a94-236">hello Storm REST API 未公開超過 hello 網際網路，而且必須使用 SSH 通道 toohello HDInsight 叢集前端節點存取。</span><span class="sxs-lookup"><span data-stu-id="b4a94-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="b4a94-237">如需建立及使用 SSH 通道，請參閱[使用 SSH 通道 tooaccess Ambari web UI、 ResourceManager、 JobHistory、 NameNode、 Oozie、 以及其他 web Ui](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="b4a94-238">基底 URI</span><span class="sxs-lookup"><span data-stu-id="b4a94-238">Base URI</span></span>

<span data-ttu-id="b4a94-239">hello hello REST API 以 Linux 為基礎的 HDInsight 叢集上的基底 URI 可在 hello 前端節點上**https://HEADNODEFQDN:8744/api/v1/**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="b4a94-240">hello hello 前端節點的網域名稱在叢集建立期間產生，並不是靜態。</span><span class="sxs-lookup"><span data-stu-id="b4a94-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="b4a94-241">您可以數種不同方式找到 hello 叢集前端節點的 hello 完整的網域名稱 (FQDN):</span><span class="sxs-lookup"><span data-stu-id="b4a94-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="b4a94-242">**從的 SSH 工作階段**： 使用 hello 命令`headnode -f`從 SSH 工作階段 toohello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="b4a94-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="b4a94-243">**從 Ambari Web**： 選取**服務**從 hello hello 頁面頂端，然後選取**Storm**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="b4a94-244">從 hello**摘要**索引標籤上，選取**Storm UI 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="b4a94-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="b4a94-245">hello hello Storm UI 和 REST API 執行的 hello 節點的 FQDN 是在 hello hello 頁面最上方。</span><span class="sxs-lookup"><span data-stu-id="b4a94-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="b4a94-246">**Ambari REST API 從**： 使用 hello 命令`curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"`tooretrieve 資訊 hello Storm UI 和 REST API 的 hello 節點上執行。</span><span class="sxs-lookup"><span data-stu-id="b4a94-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="b4a94-247">取代**密碼**hello hello 叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="b4a94-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="b4a94-248">取代**CLUSTERNAME**與 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b4a94-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="b4a94-249">在 hello 回應 hello"host_name"項目會包含 hello hello 節點的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="b4a94-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="b4a94-250">驗證</span><span class="sxs-lookup"><span data-stu-id="b4a94-250">Authentication</span></span>

<span data-ttu-id="b4a94-251">必須使用 REST API 的要求 toohello**基本驗證**，所以您可以使用 hello HDInsight 叢集系統管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b4a94-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a94-252">因為基本驗證會使用純文字傳送，您應該**一律**hello 叢集中使用 HTTPS toosecure 通訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="b4a94-253">傳回值</span><span class="sxs-lookup"><span data-stu-id="b4a94-253">Return values</span></span>

<span data-ttu-id="b4a94-254">只能從 hello 叢集內可使用 REST API 或虛擬機器上 hello 與 hello 叢集相同 Azure 虛擬網路從 hello 傳回的資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a94-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="b4a94-255">例如，傳回的動物園管理員伺服器 hello 完整的網域名稱 (FQDN) 是無法從 hello 網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="b4a94-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4a94-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4a94-256">Next Steps</span></span>

<span data-ttu-id="b4a94-257">既然您已經學會如何使用 toodeploy 和監視器的拓樸 hello Storm 儀表板，了解如何太[開發 Java 為基礎的拓撲使用 Maven](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="b4a94-258">若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="b4a94-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
