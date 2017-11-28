---
title: "aaaDeploy 和管理 HDInsight 上的 Apache Storm 拓撲 |Microsoft 文件"
description: "了解 toodeploy、 監視和管理 HDInsight 上使用 hello Storm 儀表板的 Apache Storm 拓撲的方式。 使用適用於 Visual Studio 的 Hadoop 工具。"
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
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="c3ff1-104">部署和管理以 Windows 為基礎的 HDInsight 上的 Apache Storm 拓撲</span><span class="sxs-lookup"><span data-stu-id="c3ff1-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="c3ff1-105">hello Storm 儀表板可讓您 tooeasily 部署和執行 Apache Storm 拓撲 tooyour HDInsight 叢集使用網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="c3ff1-106">您也可以使用 hello 儀表板 toomonitor，並管理正在執行的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="c3ff1-107">如果您使用 Visual Studio，hello HDInsight Tools for Visual Studio 會提供類似的功能，Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="c3ff1-108">hello Storm 儀表板和 hello HDInsight Tools 中的 hello Storm 功能上依賴 hello Storm REST API，可以使用的 toocreate 專屬監視和管理的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3ff1-109">本文件中的 hello 步驟需要使用 Windows 做為 hello 作業系統的 HDInsight 叢集上出現。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="c3ff1-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3ff1-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="c3ff1-112">如需透過使用 Linux 的 HDInsight 叢集來部署和管理 Storm 拓撲的詳細資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c3ff1-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3ff1-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="c3ff1-113">Prerequisites</span></span>

* <span data-ttu-id="c3ff1-114">**Apache Storm on HDInsight** - 請參閱[開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md)，以取得建立叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="c3ff1-115">Hello **Storm 儀表板**： 支援 HTML5 的現代網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="c3ff1-116">如**Visual Studio** -Azure SDK 2.5.1 或更新版本和 hello HDInsight Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="c3ff1-117">請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall 和設定 hello HDInsight tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="c3ff1-118">下列版本的 Visual Studio 中的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="c3ff1-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="c3ff1-119">Visual Studio 2012 (含 Update 4)</span><span class="sxs-lookup"><span data-stu-id="c3ff1-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="c3ff1-120">Visual Studio 2013 (含 Update 4) 或 Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="c3ff1-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="c3ff1-121">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="c3ff1-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="c3ff1-122">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="c3ff1-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="c3ff1-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="c3ff1-123">Storm Dashboard</span></span>

<span data-ttu-id="c3ff1-124">hello Storm 儀表板是在 Storm 叢集上使用的網頁。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="c3ff1-125">hello URL 是**https://&lt;clustername >.azurehdinsight.net/**，其中**clustername**是您在 HDInsight 叢集的 Storm hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="c3ff1-126">從 hello hello Storm 儀表板頂端，選取**提交拓撲**。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="c3ff1-127">遵循上 hello 頁面 toorun 拓樸範例 hello 指示或 tooupload 然後執行您所建立的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![hello 提交拓樸 頁面][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="c3ff1-129">Storm UI</span><span class="sxs-lookup"><span data-stu-id="c3ff1-129">Storm UI</span></span>

<span data-ttu-id="c3ff1-130">從 hello Storm 儀表板，選取 hello **Storm UI**連結。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="c3ff1-131">這在加法 tooany 執行拓樸中顯示 hello 叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![hello storm ui][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="c3ff1-133">使用 Internet Explorer 的某些版本中，您可能會發現 Storm UI 不會重新整理之後，您必須先瀏覽該 hello。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="c3ff1-134">例如，它可能不會顯示 hello 新拓撲您上傳，或您先前停用時，它可能會顯示為作用中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="c3ff1-135">Microsoft 知道這個問題，並正在找出解決方案。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="c3ff1-136">主頁面</span><span class="sxs-lookup"><span data-stu-id="c3ff1-136">Main page</span></span>

<span data-ttu-id="c3ff1-137">hello Storm UI hello 主頁面上提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3ff1-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="c3ff1-138">**叢集摘要**: hello Storm 叢集的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="c3ff1-139">**拓撲摘要**：執行中拓撲的清單。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="c3ff1-140">使用有關特定拓撲中這個區段 tooview hello 連結的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="c3ff1-141">**摘要的監督員**: hello Storm 監督者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="c3ff1-142">**Nimbus 組態**: Nimbus hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="c3ff1-143">拓撲摘要</span><span class="sxs-lookup"><span data-stu-id="c3ff1-143">Topology summary</span></span>

<span data-ttu-id="c3ff1-144">選取連結從 hello**拓撲摘要**區段會顯示 hello 下列 hello 拓撲的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="c3ff1-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="c3ff1-145">**摘要的拓樸**: hello 拓撲的相關基本資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="c3ff1-146">**拓樸動作**: hello 拓撲，您可以執行管理動作。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="c3ff1-147">**啟用**：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="c3ff1-148">**停用**：暫停執行中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="c3ff1-149">**重新平衡**： 調整 hello 拓樸的 hello 平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="c3ff1-150">之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="c3ff1-151">這可讓 hello 拓撲 tooadjust 平行處理原則 toocompensate hello 增加或減少 hello 叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="c3ff1-152">如需詳細資訊，請參閱[了解 hello 平行處理原則的 Storm 拓撲 (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="c3ff1-153">**Kill**: hello 指定逾時之後終止 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="c3ff1-154">**拓樸 stats**: hello 拓撲的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="c3ff1-155">使用中 hello hello 連結**視窗**hello 剩餘項目在 hello 頁面上的資料行 tooset hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="c3ff1-156">**Spouts**: hello spouts hello 拓撲所使用。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="c3ff1-157">使用此區段 tooview 中的 hello 連結特定 spouts 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="c3ff1-158">**釘**: hello hello 拓撲所使用的攻擊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="c3ff1-159">使用此區段 tooview 中的 hello 連結特定攻擊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="c3ff1-160">**拓撲組態**: hello 選取拓撲的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="c3ff1-161">Spout 和 Bolt 摘要</span><span class="sxs-lookup"><span data-stu-id="c3ff1-161">Spout and Bolt summary</span></span>

<span data-ttu-id="c3ff1-162">選取從 hello spout **Spouts**或**釘**區段會顯示 hello 遵循 hello 選取項目的資訊：</span><span class="sxs-lookup"><span data-stu-id="c3ff1-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="c3ff1-163">**元件摘要**: hello spout 或閃電的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="c3ff1-164">**Spout 閃電 stats**: hello 相關統計資料 spout 或閃電。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="c3ff1-165">使用中 hello hello 連結**視窗**hello 剩餘項目在 hello 頁面上的資料行 tooset hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="c3ff1-166">**輸入 stats** （只有閃電）： hello 的相關資訊輸入 hello 閃電所耗用的資料流。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="c3ff1-167">**輸出 stats**: spout 或閃電關於發出由此 hello 資料流的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="c3ff1-168">**執行程式**: hello spout 或閃電 hello 執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="c3ff1-169">選取 hello**連接埠**這個執行個體所產生的項目特定的執行程式 tooview 診斷資訊的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="c3ff1-170">**錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="c3ff1-171">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3ff1-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="c3ff1-172">hello HDInsight 工具可以使用的 toosubmit C# 或混合式拓撲 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="c3ff1-173">下列步驟的 hello 使用範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-173">hello following steps use a sample application.</span></span> <span data-ttu-id="c3ff1-174">如需使用 hello HDInsight Tools 來建立您自己的拓撲資訊，請參閱[開發 C# 拓撲使用 hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="c3ff1-175">使用下列步驟 toodeploy 範例 tooyour Storm HDInsight 叢集上的 hello 然後檢視和管理 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="c3ff1-176">如果您有尚未安裝 hello 最新版 hello HDInsight Tools for Visual Studio，請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="c3ff1-177">開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="c3ff1-178">在 hello**新專案**對話方塊方塊中，展開 **已安裝** > **範本**，然後選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="c3ff1-179">從範本 hello 清單，選取**Storm 範例**。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="c3ff1-180">在 hello hello 對話方塊下方，輸入 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="c3ff1-182">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3ff1-183">如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="c3ff1-184">如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="c3ff1-185">選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="c3ff1-186">您可以監視是否 hello 提交成功使用 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="c3ff1-187">已成功送出 hello 拓樸，當 hello **Storm 拓撲**hello 叢集應該會出現。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="c3ff1-188">從 hello 列出 tooview hello 執行拓撲的相關資訊，請選取 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="c3ff1-190">您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="c3ff1-191">Hello spouts 或釘 tooview 這些元件的資訊，請選取 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="c3ff1-192">隨即會針對每個選取的項目開啟新的視窗。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3ff1-193">hello hello 拓撲檔案名 hello 拓樸的 hello 類別名稱 (在此情況下， `HelloWord`，) 附加時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="c3ff1-194">從 hello**拓撲摘要**檢視中，選取**Kill** toostop hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3ff1-195">Storm 拓撲會繼續執行，直到已停止或刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="c3ff1-196">REST API</span><span class="sxs-lookup"><span data-stu-id="c3ff1-196">REST API</span></span>

<span data-ttu-id="c3ff1-197">hello REST API，乃是建立 hello Storm UI，讓您可以執行類似的管理和監視功能，可使用 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="c3ff1-198">您可以使用 hello REST API toocreate 自訂工具來管理和監視 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="c3ff1-199">如需詳細資訊，請參閱 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="c3ff1-200">hello 下列資訊為特定 toousing hello 與 HDInsight 上的 Apache Storm 的 REST API。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="c3ff1-201">基底 URI</span><span class="sxs-lookup"><span data-stu-id="c3ff1-201">Base URI</span></span>

<span data-ttu-id="c3ff1-202">hello hello REST API 在 HDInsight 叢集上的基底 URI 是**https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**，其中**clustername**位於您 Storm hello 名稱HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="c3ff1-203">驗證</span><span class="sxs-lookup"><span data-stu-id="c3ff1-203">Authentication</span></span>

<span data-ttu-id="c3ff1-204">必須使用 REST API 的要求 toohello**基本驗證**，所以您可以使用 hello HDInsight 叢集系統管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="c3ff1-205">因為基本驗證會使用純文字傳送，您應該**一律**hello 叢集中使用 HTTPS toosecure 通訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="c3ff1-206">傳回值</span><span class="sxs-lookup"><span data-stu-id="c3ff1-206">Return values</span></span>

<span data-ttu-id="c3ff1-207">只能從 hello 叢集內可使用 REST API 或虛擬機器上 hello 與 hello 叢集相同 Azure 虛擬網路從 hello 傳回的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="c3ff1-208">例如，傳回的動物園管理員伺服器 hello 完整的網域名稱 (FQDN) 是無法從 hello 網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ff1-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3ff1-209">Next Steps</span></span>

<span data-ttu-id="c3ff1-210">既然您已經學會如何使用 toodeploy 和監視器的拓樸 hello Storm 儀表板，了解如何：</span><span class="sxs-lookup"><span data-stu-id="c3ff1-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="c3ff1-211">開發使用 hello HDInsight Tools for Visual Studio C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="c3ff1-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="c3ff1-212">使用 Maven 開發 Java 型拓撲</span><span class="sxs-lookup"><span data-stu-id="c3ff1-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="c3ff1-213">若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ff1-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
