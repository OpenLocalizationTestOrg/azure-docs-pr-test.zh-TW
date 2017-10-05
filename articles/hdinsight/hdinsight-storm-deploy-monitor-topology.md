---
title: "部署和管理 HDInsight 上的 Apache Storm 拓撲 | Microsoft Docs"
description: "使用 Storm Dashboard on HDInsight，了解如何部署、監視和管理 Apache Storm 拓撲。 使用適用於 Visual Studio 的 Hadoop 工具。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="a776d-104">部署和管理以 Windows 為基礎的 HDInsight 上的 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="a776d-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="a776d-105">Storm Dashboard 可讓您使用網頁瀏覽器輕鬆地部署和執行 Apache Storm 拓撲至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a776d-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="a776d-106">您也可以使用儀表板來監視和管理執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="a776d-107">如果您使用 Visual Studio，則 HDInsight Tools for Visual Studio 會提供 Visual Studio 中的類似功能。</span><span class="sxs-lookup"><span data-stu-id="a776d-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="a776d-108">HDInsight Tools 的 Storm Dashboard 和 Storm 功能依賴 Storm REST API，此 API 可用來建立您專屬的監視和管理方案。</span><span class="sxs-lookup"><span data-stu-id="a776d-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a776d-109">這份文件中的步驟需要使用 Windows 做為作業系統的 Storm on HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a776d-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="a776d-110">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a776d-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a776d-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a776d-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a776d-112">如需透過使用 Linux 的 HDInsight 叢集來部署和管理 Storm 拓撲的詳細資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="a776d-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a776d-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="a776d-113">Prerequisites</span></span>

* <span data-ttu-id="a776d-114">**Apache Storm on HDInsight** - 請參閱[開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md)，以取得建立叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="a776d-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="a776d-115">針對 **Storm Dashboard**：支援 HTML5 的新型網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a776d-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="a776d-116">針對 **Visual Studio** - Azure SDK 2.5.1 或更新版本，以及 HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a776d-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="a776d-117">請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) 以安裝及設定 HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a776d-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="a776d-118">下列其中一個 Visual Studio 版本：</span><span class="sxs-lookup"><span data-stu-id="a776d-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="a776d-119">Visual Studio 2012 (含 Update 4)</span><span class="sxs-lookup"><span data-stu-id="a776d-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="a776d-120">Visual Studio 2013 (含 Update 4) 或 Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="a776d-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="a776d-121">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="a776d-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="a776d-122">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="a776d-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="a776d-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="a776d-123">Storm Dashboard</span></span>

<span data-ttu-id="a776d-124">Storm Dashboard 是可以在 Storm 叢集上使用的網頁。</span><span class="sxs-lookup"><span data-stu-id="a776d-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="a776d-125">URL 是 **https://&lt;clustername>.azurehdinsight.net/**，其中 **clustername** 是 Storm on HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="a776d-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="a776d-126">從 Storm Dashboard 的頂端，選取 [提交拓撲] 。</span><span class="sxs-lookup"><span data-stu-id="a776d-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="a776d-127">依照頁面上的指示來執行範例拓撲，或者上傳及執行您已建立的拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![提交拓撲頁面][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="a776d-129">Storm UI</span><span class="sxs-lookup"><span data-stu-id="a776d-129">Storm UI</span></span>

<span data-ttu-id="a776d-130">從 Storm Dashboard 中選取 [Storm UI]  連結。</span><span class="sxs-lookup"><span data-stu-id="a776d-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="a776d-131">這會顯示叢集和任何執行中拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![Storm UI][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="a776d-133">在 Internet Explorer 的某些版本中，您可能會發現 Storm UI 在您最初到訪之後不會重新整理。</span><span class="sxs-lookup"><span data-stu-id="a776d-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="a776d-134">例如，可能不會顯示您提交的新拓撲，或是可能將先前已停用的拓撲顯示為使用中。</span><span class="sxs-lookup"><span data-stu-id="a776d-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="a776d-135">Microsoft 知道這個問題，並正在找出解決方案。</span><span class="sxs-lookup"><span data-stu-id="a776d-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="a776d-136">主頁面</span><span class="sxs-lookup"><span data-stu-id="a776d-136">Main page</span></span>

<span data-ttu-id="a776d-137">Storm UI 的主頁面會提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a776d-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="a776d-138">**叢集摘要**：Storm 叢集的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="a776d-139">**拓撲摘要**：執行中拓撲的清單。</span><span class="sxs-lookup"><span data-stu-id="a776d-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="a776d-140">使用本節中的連結來檢視特定拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="a776d-141">**監督員摘要**：Storm 監督員的資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="a776d-142">**Nimbus 組態**：叢集的 Nimbus 組態。</span><span class="sxs-lookup"><span data-stu-id="a776d-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="a776d-143">拓撲摘要</span><span class="sxs-lookup"><span data-stu-id="a776d-143">Topology summary</span></span>

<span data-ttu-id="a776d-144">選取 [拓撲摘要]  區段中的連結會顯示拓撲的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a776d-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="a776d-145">**拓撲摘要**：拓撲的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="a776d-146">**拓撲動作**：您可以針對拓撲執行的管理動作。</span><span class="sxs-lookup"><span data-stu-id="a776d-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="a776d-147">**啟用**：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="a776d-148">**停用**：暫停執行中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="a776d-149">**重新平衡**：調整拓撲的平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="a776d-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="a776d-150">變更叢集中的節點數目之後，您應該重新平衡執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="a776d-151">這可讓拓撲調整平行處理原則，以彌補叢集中增加或減少的節點數目。</span><span class="sxs-lookup"><span data-stu-id="a776d-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="a776d-152">如需詳細資訊，請參閱[了解 Storm 拓撲的平行處理原則 (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (英文)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。</span><span class="sxs-lookup"><span data-stu-id="a776d-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="a776d-153">**終止**：在指定的逾時之後結束 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="a776d-154">**拓撲統計資料**：拓撲的統計資料。</span><span class="sxs-lookup"><span data-stu-id="a776d-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="a776d-155">使用 [視窗]  資料行中的連結，以設定頁面上其餘項目的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a776d-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="a776d-156">**Spout**：拓撲所使用的 Spout。</span><span class="sxs-lookup"><span data-stu-id="a776d-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="a776d-157">使用本節中的連結檢視特定 Spout 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="a776d-158">**Bolt**：拓撲所使用的 Bolt。</span><span class="sxs-lookup"><span data-stu-id="a776d-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="a776d-159">使用本節中的連結檢視特定 Bolt 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="a776d-160">**拓撲組態**：所選取拓撲的組態。</span><span class="sxs-lookup"><span data-stu-id="a776d-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="a776d-161">Spout 和 Bolt 摘要</span><span class="sxs-lookup"><span data-stu-id="a776d-161">Spout and Bolt summary</span></span>

<span data-ttu-id="a776d-162">從 [Spout] 或 [Bolt] 區段中選取 Spout 會顯示所選取項目的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a776d-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="a776d-163">**元件摘要**：Spout 或 Bolt 的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="a776d-164">**Spout/Bolt 統計資料**：Spout 或 Bolt 的統計資料。</span><span class="sxs-lookup"><span data-stu-id="a776d-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="a776d-165">使用 [視窗]  資料行中的連結，以設定頁面上其餘項目的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a776d-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="a776d-166">**輸入統計資料** (僅限 Bolt)：Bolt 所使用輸入資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="a776d-167">**輸出統計資料**：此 Spout 或 Bolt 所發出資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="a776d-168">**執行程式**：Spout 或 Bolt 執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="a776d-169">選取特定執行程式的 [連接埠]  項目，以檢視針對此執行個體所產生之診斷資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="a776d-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="a776d-170">**錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="a776d-171">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a776d-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="a776d-172">HDInsight Tools 可以用來將 C# 或混合式拓撲提交至 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="a776d-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="a776d-173">下列步驟使用範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a776d-173">The following steps use a sample application.</span></span> <span data-ttu-id="a776d-174">如需使用 HDInsight Tools 建立您專屬拓撲的詳細資訊，請參閱 [使用 HDInsight Tools for Visual Studio 開發 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="a776d-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="a776d-175">使用下列步驟，將範例部署至 Storm on HDInsight 叢集，然後檢視和管理拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="a776d-176">如果您尚未安裝最新版本的 HDInsight Tools for Visual Studio，請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a776d-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="a776d-177">開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。</span><span class="sxs-lookup"><span data-stu-id="a776d-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="a776d-178">在 [新增專案] 對話方塊中，依序展開 [已安裝]  >  [範本]，然後選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="a776d-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="a776d-179">從範本清單中，選取 [Storm 範例] 。</span><span class="sxs-lookup"><span data-stu-id="a776d-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="a776d-180">在對話方塊底部，輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="a776d-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="a776d-182">在 [方案總管] 中，於專案上按一下滑鼠右鍵，然後選取 [提交至 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="a776d-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a776d-183">如果出現提示，請輸入您 Azure 訂閱的登入認證。</span><span class="sxs-lookup"><span data-stu-id="a776d-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="a776d-184">如果您有多個訂用帳戶，請登入包含 Storm on HDInsight 叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a776d-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="a776d-185">從 [Storm 叢集] 下拉式清單中選取 Storm on HDInsight 叢集，然後選取 [提交]。</span><span class="sxs-lookup"><span data-stu-id="a776d-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="a776d-186">您可以使用 [輸出]  視窗監視提交是否成功。</span><span class="sxs-lookup"><span data-stu-id="a776d-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="a776d-187">順利提交拓撲時，應該會出現叢集的 [Storm 拓撲]  。</span><span class="sxs-lookup"><span data-stu-id="a776d-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="a776d-188">從清單中選取拓撲，以檢視執行中拓撲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-188">Select the topology from the list to view information about the running topology.</span></span>

    ![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="a776d-190">您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="a776d-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="a776d-191">選取 Spout 或 Bolt 的圖形以檢視這些元件的資訊。</span><span class="sxs-lookup"><span data-stu-id="a776d-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="a776d-192">隨即會針對每個選取的項目開啟新的視窗。</span><span class="sxs-lookup"><span data-stu-id="a776d-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a776d-193">拓撲的名稱是拓撲的類別名稱 (在此案例中為 `HelloWord`) 加上時間戳記。</span><span class="sxs-lookup"><span data-stu-id="a776d-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="a776d-194">從 [拓撲摘要] 檢視中，選取 [終止] 停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a776d-195">除非停止 Storm 拓撲或刪除叢集，否則 Storm 拓撲會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="a776d-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="a776d-196">REST API</span><span class="sxs-lookup"><span data-stu-id="a776d-196">REST API</span></span>

<span data-ttu-id="a776d-197">Storm UI 是以 REST API 為建置基礎，因此您可以使用 REST API 執行類似的管理和監視功能。</span><span class="sxs-lookup"><span data-stu-id="a776d-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="a776d-198">您可以使用 REST API 建立自訂工具來管理和監視 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="a776d-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="a776d-199">如需詳細資訊，請參閱 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)。</span><span class="sxs-lookup"><span data-stu-id="a776d-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="a776d-200">下列資訊專用於搭配使用 REST API 與 Apache Storm on HDInsight。</span><span class="sxs-lookup"><span data-stu-id="a776d-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="a776d-201">基底 URI</span><span class="sxs-lookup"><span data-stu-id="a776d-201">Base URI</span></span>

<span data-ttu-id="a776d-202">REST API on HDInsight 叢集的基底 URI 是 **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**，其中 **clustername** 是 Storm on HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="a776d-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="a776d-203">驗證</span><span class="sxs-lookup"><span data-stu-id="a776d-203">Authentication</span></span>

<span data-ttu-id="a776d-204">REST API 的要求必須使用 **基本驗證**，因此請使用 HDInsight 叢集管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a776d-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="a776d-205">因為使用純文字傳送基本驗證，所以您應該 **一律** 使用 HTTPS 來保護與叢集通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="a776d-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="a776d-206">傳回值</span><span class="sxs-lookup"><span data-stu-id="a776d-206">Return values</span></span>

<span data-ttu-id="a776d-207">從 REST API 傳回的資訊只能從叢集或與叢集相同之 Azure 虛擬網路上的虛擬機器內使用。</span><span class="sxs-lookup"><span data-stu-id="a776d-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="a776d-208">例如，無法從網際網路存取針對 Zookeeper 伺服器所傳回的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="a776d-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a776d-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a776d-209">Next Steps</span></span>

<span data-ttu-id="a776d-210">現在，您已了解如何使用 Storm Dashboard 部署和監視拓撲，接著請了解如何：</span><span class="sxs-lookup"><span data-stu-id="a776d-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="a776d-211">使用 HDInsight Tools for Visual Studio 開發 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="a776d-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="a776d-212">使用 Maven 開發 Java 型拓撲</span><span class="sxs-lookup"><span data-stu-id="a776d-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="a776d-213">若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="a776d-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
