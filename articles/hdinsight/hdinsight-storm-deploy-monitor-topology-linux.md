---
title: "在以 Linux 為基礎的 HDInsight 上部署與管理 Apache Storm 拓撲 | Microsoft Docs"
description: "了解如何使用以 Linux 為基礎 HDInsight 上的 Storm Dashboard 部署、監視和管理 Apache Storm 拓撲。 使用適用於 Visual Studio 的 Hadoop 工具。"
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="3fce8-104">部署和管理 HDInsight 上的 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="3fce8-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="3fce8-105">在本文件中，您可以了解管理和監視在 Storm on HDInsight 叢集上執行之 Storm 拓撲的基本概念。</span><span class="sxs-lookup"><span data-stu-id="3fce8-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fce8-106">本文中的步驟需要 HDInsight 叢集上以 Linux 為基礎的 Storm。</span><span class="sxs-lookup"><span data-stu-id="3fce8-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="3fce8-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="3fce8-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3fce8-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="3fce8-109">如需部署和監視以 Windows 為基礎的 HDInsight 上的拓撲的詳細資訊，請參閱 [部署和管理以 Windows 為基礎的 HDInsight 上的Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="3fce8-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3fce8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fce8-110">Prerequisites</span></span>

* <span data-ttu-id="3fce8-111">**HDInsight 叢集上以 Linux 為基礎的 Storm**：請參閱 [開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) 以取得建立叢集的步驟</span><span class="sxs-lookup"><span data-stu-id="3fce8-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="3fce8-112">(選擇性) **熟悉 SSH 和 SCP**︰如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="3fce8-113">(選擇性) **Visual Studio**：Azure SDK 2.5.1 或更新版本，以及 Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3fce8-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="3fce8-114">如需詳細資訊，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="3fce8-115">下列其中一個 Visual Studio 版本：</span><span class="sxs-lookup"><span data-stu-id="3fce8-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="3fce8-116">Visual Studio 2012 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="3fce8-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="3fce8-117">Visual Studio 2013 [(含 Update 4)](http://www.microsoft.com/download/details.aspx?id=44921) 或 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="3fce8-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="3fce8-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3fce8-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="3fce8-119">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="3fce8-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="3fce8-120">Visual Studio 2017 (任何版本)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="3fce8-121">Data Lake Tools for Visual Studio 2017 會安裝為 Azure 工作負載的一部分。</span><span class="sxs-lookup"><span data-stu-id="3fce8-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="3fce8-122">提交拓撲︰Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fce8-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="3fce8-123">HDInsight Tools 可以用來將 C# 或混合式拓撲提交至 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="3fce8-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="3fce8-124">下列步驟使用範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fce8-124">The following steps use a sample application.</span></span> <span data-ttu-id="3fce8-125">如需使用 HDInsight Tools 建立您專屬拓撲的詳細資訊，請參閱 [使用 HDInsight Tools for Visual Studio 開發 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="3fce8-126">如果您尚未安裝最新版的 Data Lake Tools for Visual Studio，請參閱[開始使用 Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3fce8-127">Data Lake Tools for Visual Studio 先前稱為 HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3fce8-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="3fce8-128">Data Lake Tools for Visual Studio 隨附於適用於 Visual Studio 2017 的 __Azure 工作負載__中。</span><span class="sxs-lookup"><span data-stu-id="3fce8-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="3fce8-129">開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="3fce8-130">在 [新增專案] 對話方塊中，依序展開 [已安裝]  >  [範本]，然後選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="3fce8-131">從範本清單中，選取 [Storm 範例] 。</span><span class="sxs-lookup"><span data-stu-id="3fce8-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="3fce8-132">在對話方塊底部，輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fce8-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="3fce8-134">在 [方案總管] 中，於專案上按一下滑鼠右鍵，然後選取 [提交至 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fce8-135">如果出現提示，請輸入您 Azure 訂閱的登入認證。</span><span class="sxs-lookup"><span data-stu-id="3fce8-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="3fce8-136">如果您有多個訂用帳戶，請登入包含 Storm on HDInsight 叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fce8-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="3fce8-137">從 [Storm 叢集] 下拉式清單中選取 Storm on HDInsight 叢集，然後選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="3fce8-138">您可以使用 [輸出]  視窗監視提交是否成功。</span><span class="sxs-lookup"><span data-stu-id="3fce8-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="3fce8-139">提交拓撲︰SSH 和 Storm 命令</span><span class="sxs-lookup"><span data-stu-id="3fce8-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="3fce8-140">使用 SSH 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3fce8-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="3fce8-141">使用您的 SSH 登入名稱來取代 **USERNAME**。</span><span class="sxs-lookup"><span data-stu-id="3fce8-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="3fce8-142">將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="3fce8-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="3fce8-143">如需使用 SSH 連線至 HDInsight 叢集的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3fce8-144">使用下列命令以啟動範例拓撲：</span><span class="sxs-lookup"><span data-stu-id="3fce8-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="3fce8-145">這個命令會在叢集上啟動範例 WordCount 拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="3fce8-146">這個拓撲會隨機產生句子，並計算句子中每個字詞的出現次數。</span><span class="sxs-lookup"><span data-stu-id="3fce8-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fce8-147">將拓撲提交至叢集時，您必須先複製包含叢集的 jar 檔案，再使用 `storm` 命令。</span><span class="sxs-lookup"><span data-stu-id="3fce8-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="3fce8-148">若要將檔案複製到叢集，您可以使用 `scp` 命令。</span><span class="sxs-lookup"><span data-stu-id="3fce8-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="3fce8-149">例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="3fce8-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="3fce8-150">WordCount 範例和其他 Storm 入門範例都已經包含在叢集中，位置是 `/usr/hdp/current/storm-client/contrib/storm-starter/`。</span><span class="sxs-lookup"><span data-stu-id="3fce8-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="3fce8-151">提交拓撲︰以程式設計的方式</span><span class="sxs-lookup"><span data-stu-id="3fce8-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="3fce8-152">您可以用程式設計方式與裝載於叢集中的 Nimbus 服務進行通訊，以對 Storm on HDInsight 部署拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="3fce8-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) 提供範例 Java 應用程式，以示範如何透過 Nimbus 服務部署和啟動拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="3fce8-154">監視和管理︰Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fce8-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="3fce8-155">使用 Visual Studio 順利提交拓撲之後，隨即會出現叢集的 [Storm 拓撲] 檢視。</span><span class="sxs-lookup"><span data-stu-id="3fce8-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="3fce8-156">從清單中選取拓撲，以檢視執行中拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-156">Select the topology from the list to view information about the running topology.</span></span>

![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="3fce8-158">您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="3fce8-159">選取 Spout 或 Bolt 的圖形以檢視這些元件的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="3fce8-160">隨即會針對每個選取的項目開啟新的視窗。</span><span class="sxs-lookup"><span data-stu-id="3fce8-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="3fce8-161">停用和重新啟動</span><span class="sxs-lookup"><span data-stu-id="3fce8-161">Deactivate and reactivate</span></span>

<span data-ttu-id="3fce8-162">停用拓撲會暫停它，直到刪除或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3fce8-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="3fce8-163">若要執行這些作業，請使用 [拓撲摘要] 頂端的 [停用] 和 [重新啟用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fce8-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="3fce8-164">重新平衡</span><span class="sxs-lookup"><span data-stu-id="3fce8-164">Rebalance</span></span>

<span data-ttu-id="3fce8-165">重新平衡拓撲可以讓系統修訂拓撲的平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="3fce8-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="3fce8-166">例如，如果您已調整叢集的大小來新增更多節點，重新平衡可讓拓撲看見新的節點。</span><span class="sxs-lookup"><span data-stu-id="3fce8-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="3fce8-167">若要重新平衡拓撲，請使用 [拓撲摘要] 頂端的 [重新平衡] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fce8-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="3fce8-168">重新平衡拓撲首先會停用拓撲，然後跨叢集平均重新分佈背景工作角色，最後讓拓撲返回發生重新平衡之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="3fce8-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="3fce8-169">因此，如果拓撲是作用中，它會再次變成作用中。</span><span class="sxs-lookup"><span data-stu-id="3fce8-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="3fce8-170">如果已停用，它就會保持停用。</span><span class="sxs-lookup"><span data-stu-id="3fce8-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="3fce8-171">終止拓撲</span><span class="sxs-lookup"><span data-stu-id="3fce8-171">Kill a topology</span></span>

<span data-ttu-id="3fce8-172">除非停止 Storm 拓撲或刪除叢集，否則 Storm 拓撲會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="3fce8-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="3fce8-173">若要停止拓撲，請使用 [拓撲摘要] 頂端的 [終止] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fce8-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="3fce8-174">監視和管理：SSH 和 Storm 命令</span><span class="sxs-lookup"><span data-stu-id="3fce8-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="3fce8-175">`storm` 公用程式可讓您從命令列使用執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="3fce8-176">使用 `storm -h` 以取得完整的命令清單。</span><span class="sxs-lookup"><span data-stu-id="3fce8-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="3fce8-177">列出拓撲</span><span class="sxs-lookup"><span data-stu-id="3fce8-177">List topologies</span></span>

<span data-ttu-id="3fce8-178">使用下列命令來列出所有執行中拓撲：</span><span class="sxs-lookup"><span data-stu-id="3fce8-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="3fce8-179">此命令會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="3fce8-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="3fce8-180">停用和重新啟動</span><span class="sxs-lookup"><span data-stu-id="3fce8-180">Deactivate and reactivate</span></span>

<span data-ttu-id="3fce8-181">停用拓撲會暫停它，直到刪除或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3fce8-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="3fce8-182">使用下列命令來停用和重新啟動：</span><span class="sxs-lookup"><span data-stu-id="3fce8-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="3fce8-183">刪除執行中拓撲</span><span class="sxs-lookup"><span data-stu-id="3fce8-183">Kill a running topology</span></span>

<span data-ttu-id="3fce8-184">Storm 拓撲一旦啟動之後，就會繼續執行直到停止。</span><span class="sxs-lookup"><span data-stu-id="3fce8-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="3fce8-185">若要停止拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3fce8-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="3fce8-186">重新平衡</span><span class="sxs-lookup"><span data-stu-id="3fce8-186">Rebalance</span></span>

<span data-ttu-id="3fce8-187">重新平衡拓撲可以讓系統修訂拓撲的平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="3fce8-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="3fce8-188">例如，如果您已調整叢集的大小來新增更多節點，重新平衡可讓拓撲看見新的節點。</span><span class="sxs-lookup"><span data-stu-id="3fce8-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="3fce8-189">重新平衡拓撲首先會停用拓撲，然後跨叢集平均重新分佈背景工作角色，最後讓拓撲返回發生重新平衡之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="3fce8-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="3fce8-190">因此，如果拓撲是作用中，它會再次變成作用中。</span><span class="sxs-lookup"><span data-stu-id="3fce8-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="3fce8-191">如果已停用，它就會保持停用。</span><span class="sxs-lookup"><span data-stu-id="3fce8-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="3fce8-192">監視和管理︰Storm UI</span><span class="sxs-lookup"><span data-stu-id="3fce8-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="3fce8-193">Storm UI 提供 Web 介面來處理執行中的拓撲，包含在您的 HDInsight 叢集中。</span><span class="sxs-lookup"><span data-stu-id="3fce8-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="3fce8-194">若要檢視 Storm UI，請使用網頁瀏覽器開啟 **https://CLUSTERNAME.azurehdinsight.net/stormui**，其中 **CLUSTERNAME** 是叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fce8-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3fce8-195">如果要求您提供使用者名稱和密碼，請輸入叢集系統管理員 (admin) 和建立叢集時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="3fce8-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="3fce8-196">主頁面</span><span class="sxs-lookup"><span data-stu-id="3fce8-196">Main page</span></span>

<span data-ttu-id="3fce8-197">Storm UI 的主頁面會提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3fce8-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="3fce8-198">**叢集摘要**：Storm 叢集的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="3fce8-199">**拓撲摘要**：執行中拓撲的清單。</span><span class="sxs-lookup"><span data-stu-id="3fce8-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="3fce8-200">使用本節中的連結來檢視特定拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="3fce8-201">**監督員摘要**：Storm 監督員的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="3fce8-202">**Nimbus 組態**：叢集的 Nimbus 組態。</span><span class="sxs-lookup"><span data-stu-id="3fce8-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="3fce8-203">拓撲摘要</span><span class="sxs-lookup"><span data-stu-id="3fce8-203">Topology summary</span></span>

<span data-ttu-id="3fce8-204">選取 [拓撲摘要]  區段中的連結會顯示拓撲的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3fce8-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="3fce8-205">**拓撲摘要**：拓撲的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="3fce8-206">**拓撲動作**：您可以針對拓撲執行的管理動作。</span><span class="sxs-lookup"><span data-stu-id="3fce8-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="3fce8-207">**啟用**：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="3fce8-208">**停用**：暫停執行中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="3fce8-209">**重新平衡**：調整拓撲的平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="3fce8-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="3fce8-210">變更叢集中的節點數目之後，您應該重新平衡執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="3fce8-211">這個作業可讓拓撲調整平行處理原則，以彌補叢集中增加或減少的節點數目。</span><span class="sxs-lookup"><span data-stu-id="3fce8-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="3fce8-212">如需詳細資訊，請參閱<a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">了解 Storm 拓撲的平行處理原則</a>。</span><span class="sxs-lookup"><span data-stu-id="3fce8-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="3fce8-213">**終止**：在指定的逾時之後結束 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="3fce8-214">**拓撲統計資料**：拓撲的統計資料。</span><span class="sxs-lookup"><span data-stu-id="3fce8-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="3fce8-215">若要設定頁面上其餘項目的時間範圍，請使用 [視窗] 資料行中的連結。</span><span class="sxs-lookup"><span data-stu-id="3fce8-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="3fce8-216">**Spout**：拓撲所使用的 Spout。</span><span class="sxs-lookup"><span data-stu-id="3fce8-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="3fce8-217">使用本節中的連結檢視特定 Spout 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="3fce8-218">**Bolt**：拓撲所使用的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="3fce8-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="3fce8-219">使用本節中的連結檢視特定 Bolt 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="3fce8-220">**拓撲組態**：所選取拓撲的組態。</span><span class="sxs-lookup"><span data-stu-id="3fce8-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="3fce8-221">Spout 和 Bolt 摘要</span><span class="sxs-lookup"><span data-stu-id="3fce8-221">Spout and Bolt summary</span></span>

<span data-ttu-id="3fce8-222">從 [Spout] 或 [Bolt] 區段中選取 Spout 會顯示所選取項目的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3fce8-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="3fce8-223">**元件摘要**：Spout 或 Bolt 的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="3fce8-224">**Spout/Bolt 統計資料**：Spout 或 Bolt 的統計資料。</span><span class="sxs-lookup"><span data-stu-id="3fce8-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="3fce8-225">若要設定頁面上其餘項目的時間範圍，請使用 [視窗] 資料行中的連結。</span><span class="sxs-lookup"><span data-stu-id="3fce8-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="3fce8-226">**輸入統計資料** (僅限 Bolt)：Bolt 所使用輸入資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="3fce8-227">**輸出統計資料**：此 Spout 或 Bolt 所發出資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="3fce8-228">**執行程式**：Spout 或 Bolt 執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="3fce8-229">選取特定執行程式的 [連接埠]  項目，以檢視針對此執行個體所產生之診斷資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="3fce8-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="3fce8-230">**錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="3fce8-231">監視和管理︰REST API</span><span class="sxs-lookup"><span data-stu-id="3fce8-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="3fce8-232">Storm UI 是以 REST API 為建置基礎，因此您可以使用 REST API 執行類似的管理和監視功能。</span><span class="sxs-lookup"><span data-stu-id="3fce8-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="3fce8-233">您可以使用 REST API 建立自訂工具來管理和監視 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="3fce8-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="3fce8-234">如需詳細資訊，請參閱 [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="3fce8-235">下列資訊專用於搭配使用 REST API 與 Apache Storm on HDInsight。</span><span class="sxs-lookup"><span data-stu-id="3fce8-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fce8-236">Storm REST API 不是透過網際網路公開可用，而是必須使用 HDInsight 叢集前端節點的 SSH 通道來存取。</span><span class="sxs-lookup"><span data-stu-id="3fce8-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="3fce8-237">如需建立及使用 SSH 通道的詳細資訊，請參閱[使用 SSH 通道來存取 Ambari Web UI、ResourceManager、JobHistory、NameNode、Oozie 及其他 Web UI](hdinsight-linux-ambari-ssh-tunnel.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="3fce8-238">基底 URI</span><span class="sxs-lookup"><span data-stu-id="3fce8-238">Base URI</span></span>

<span data-ttu-id="3fce8-239">以 Linux 為基礎的 HDInsight 叢集上 REST API 的基底 URI 可在前端節點 (位於 **https://HEADNODEFQDN:8744/api/v1/**) 上取得。</span><span class="sxs-lookup"><span data-stu-id="3fce8-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="3fce8-240">前端節點的網域名稱是在叢集建立期間產生，而不是靜態的。</span><span class="sxs-lookup"><span data-stu-id="3fce8-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="3fce8-241">您可以用幾種不同的方式尋找叢集前端節點的完整網域名稱 (FQDN)：</span><span class="sxs-lookup"><span data-stu-id="3fce8-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="3fce8-242">**從 SSH 工作階段**：使用命令 `headnode -f` (從 SSH 工作階段到叢集)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="3fce8-243">**從 Ambari Web**：從頁面頂端選取 [服務]，然後選取 [Storm]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="3fce8-244">從 [摘要] 索引標籤，選取 [Storm UI 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="3fce8-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="3fce8-245">Storm UI 和 REST API 執行所在節點的 FQDN 位於頁面頂端。</span><span class="sxs-lookup"><span data-stu-id="3fce8-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="3fce8-246">**從 Ambari REST API**：使用命令 `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` 來擷取 Storm UI 和 REST API 執行所在節點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3fce8-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="3fce8-247">將 **PASSWORD** 取代為叢集的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="3fce8-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="3fce8-248">將 **CLUSTERNAME** 取代為叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="3fce8-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="3fce8-249">在回應中，"host_name" 項目包含節點的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="3fce8-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="3fce8-250">驗證</span><span class="sxs-lookup"><span data-stu-id="3fce8-250">Authentication</span></span>

<span data-ttu-id="3fce8-251">REST API 的要求必須使用 **基本驗證**，因此請使用 HDInsight 叢集管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="3fce8-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="3fce8-252">因為使用純文字傳送基本驗證，所以您應該 **一律** 使用 HTTPS 來保護與叢集通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="3fce8-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="3fce8-253">傳回值</span><span class="sxs-lookup"><span data-stu-id="3fce8-253">Return values</span></span>

<span data-ttu-id="3fce8-254">從 REST API 傳回的資訊只能從叢集或與叢集相同之 Azure 虛擬網路上的虛擬機器內使用。</span><span class="sxs-lookup"><span data-stu-id="3fce8-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="3fce8-255">例如，無法從網際網路存取針對 Zookeeper 伺服器所傳回的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fce8-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fce8-256">Next Steps</span></span>

<span data-ttu-id="3fce8-257">現在，您已經了解如何使用 Storm 儀表板來部署和監視拓撲、了解如何 [使用 Maven 來開發以 Java 為基礎的拓撲](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="3fce8-258">若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="3fce8-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
