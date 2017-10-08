---
title: "HDInsight 的 Azure 上的 Apache Storm 的 aaaStorm 入門範例 |Microsoft 文件"
description: "深入了解如何 toodo 巨量資料分析，並處理中即時的資料使用 Apache Storm 與 hello storm 入門 HDInsight 上的範例。"
keywords: "storm-starter, apache storm 範例"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="51ca8-104">開始使用 Apache Storm 上 HDInsight 使用 hello storm 入門範例</span><span class="sxs-lookup"><span data-stu-id="51ca8-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="51ca8-105">了解如何在使用 HDInsight toouse Apache Storm hello storm 入門範例。</span><span class="sxs-lookup"><span data-stu-id="51ca8-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="51ca8-106">Apache Storm 是一個可處理資料串流的分散式、容錯、即時的運算系統。</span><span class="sxs-lookup"><span data-stu-id="51ca8-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="51ca8-107">在 Storm on Azure HDInsight 中，您可以建立雲端式 Storm 叢集，以執行即時的巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="51ca8-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51ca8-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="51ca8-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="51ca8-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51ca8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="51ca8-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="51ca8-111">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="51ca8-111">**An Azure subscription**.</span></span> <span data-ttu-id="51ca8-112">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="51ca8-113">**熟悉 SSH 和 SCP**。</span><span class="sxs-lookup"><span data-stu-id="51ca8-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="51ca8-114">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="51ca8-115">建立 Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="51ca8-115">Create a Storm cluster</span></span>

<span data-ttu-id="51ca8-116">使用下列步驟 toocreate Storm HDInsight 叢集上的 hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="51ca8-117">從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增**，**智慧 + 分析**，然後選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="51ca8-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![建立 HDInsight 叢集](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="51ca8-119">從 hello**基本概念**刀鋒視窗中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="51ca8-120">**叢集名稱**: hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="51ca8-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="51ca8-121">**訂用帳戶**： 選取 hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="51ca8-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="51ca8-122">**叢集登入使用者名稱**和**叢集登入密碼**: hello 登入透過 HTTPS 存取 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="51ca8-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="51ca8-123">您使用這些認證 tooaccess 服務，例如 hello Ambari Web UI 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="51ca8-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="51ca8-124">**安全殼層 (SSH) 的使用者名稱**: hello 透過 SSH 存取 hello 叢集時使用的登入。</span><span class="sxs-lookup"><span data-stu-id="51ca8-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="51ca8-125">根據預設 hello 密碼是 hello hello 叢集登入密碼相同。</span><span class="sxs-lookup"><span data-stu-id="51ca8-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="51ca8-126">**資源群組**: hello 資源群組 toocreate hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="51ca8-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="51ca8-127">**位置**: hello Azure 地區 toocreate hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="51ca8-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![選取訂用帳戶](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="51ca8-129">選取**叢集類型**，然後組 hello 遵循值上 hello**叢集設定**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="51ca8-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="51ca8-130">**叢集類型**：Storm</span><span class="sxs-lookup"><span data-stu-id="51ca8-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="51ca8-131">**作業系統**：Linux</span><span class="sxs-lookup"><span data-stu-id="51ca8-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="51ca8-132">**版本**：Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="51ca8-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="51ca8-133">**叢集層**：標準</span><span class="sxs-lookup"><span data-stu-id="51ca8-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="51ca8-134">最後，使用 hello**選取**按鈕 toosave 設定。</span><span class="sxs-lookup"><span data-stu-id="51ca8-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![選取叢集類型](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="51ca8-136">選取 hello 叢集類型後，使用 hello__選取__按鈕 tooset hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="51ca8-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="51ca8-137">接下來，使用 hello__下一步__按鈕 toofinish 基本組態。</span><span class="sxs-lookup"><span data-stu-id="51ca8-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="51ca8-138">從 hello**儲存體**刀鋒視窗中，選取或建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51ca8-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="51ca8-139">如需本文件中的 hello 步驟，hello 預設值，此刀鋒視窗上其他欄位保留 hello。</span><span class="sxs-lookup"><span data-stu-id="51ca8-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="51ca8-140">使用 hello__下一步__按鈕 toosave 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="51ca8-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![設定 hello HDInsight 的儲存體帳戶設定](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="51ca8-142">從 hello**摘要**刀鋒視窗中，檢閱 hello hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="51ca8-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="51ca8-143">使用 hello__編輯__連結 toochange 任何不正確的設定。</span><span class="sxs-lookup"><span data-stu-id="51ca8-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="51ca8-144">最後，使用 the__Create__ 按鈕 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="51ca8-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![叢集組態摘要](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="51ca8-146">它可能會佔用 too20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="51ca8-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="51ca8-147">在 HDInsight 上執行 storm-starter 範例</span><span class="sxs-lookup"><span data-stu-id="51ca8-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="51ca8-148">連線使用 SSH toohello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="51ca8-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="51ca8-149">如果您使用密碼 toosecure SSH 使用者帳戶，則提示的 tooenter 它。</span><span class="sxs-lookup"><span data-stu-id="51ca8-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="51ca8-150">如果您使用公開金鑰，您可能需要使用 hello`-i`參數 toospecify hello 相符的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="51ca8-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="51ca8-151">例如： `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="51ca8-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="51ca8-152">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="51ca8-153">使用下列命令 toostart 範例拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="51ca8-154">在舊版的 HDInsight，hello 拓撲 hello 類別名稱是`storm.starter.WordCountTopology`而不是`org.apache.storm.starter.WordCountTopology`。</span><span class="sxs-lookup"><span data-stu-id="51ca8-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="51ca8-155">此命令會啟動在 hello 叢集上，易記名稱為 'wordcount' hello WordCount 拓撲的範例。</span><span class="sxs-lookup"><span data-stu-id="51ca8-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="51ca8-156">它 hello 句子中會隨機產生的句子與計數 hello 發生的每個字。</span><span class="sxs-lookup"><span data-stu-id="51ca8-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51ca8-157">提交時您自己的拓撲 toohello 叢集，您必須先將 hello jar 檔案包含之前使用 hello hello 叢集`storm`命令。</span><span class="sxs-lookup"><span data-stu-id="51ca8-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="51ca8-158">使用 hello`scp`命令 toocopy hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="51ca8-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="51ca8-159">例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="51ca8-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="51ca8-160">hello WordCount 範例中，與其他 storm 入門範例，已包含在叢集上`/usr/hdp/current/storm-client/contrib/storm-starter/`。</span><span class="sxs-lookup"><span data-stu-id="51ca8-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="51ca8-161">如果您有興趣檢視 hello hello storm 入門範例的來源，您可以找到 hello 程式碼在[https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="51ca8-162">這個連結是 Storm 1.1.x，隨附於 HDInsight 3.6。</span><span class="sxs-lookup"><span data-stu-id="51ca8-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="51ca8-163">對於其他版本的情況中，使用 hello__分支__按鈕上方的 hello 頁面 tooselect hello Storm 版本不同。</span><span class="sxs-lookup"><span data-stu-id="51ca8-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="51ca8-164">監視 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="51ca8-164">Monitor hello topology</span></span>

<span data-ttu-id="51ca8-165">hello Storm UI 提供 web 介面，用於執行的拓撲，並包含在您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51ca8-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="51ca8-166">使用下列步驟 toomonitor hello 拓撲使用 hello Storm UI hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="51ca8-167">toodisplay hello Storm UI 中，開啟 web 瀏覽器 toohttps://CLUSTERNAME.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="51ca8-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="51ca8-168">取代**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="51ca8-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51ca8-169">如果使用者名稱和密碼，請詢問 tooprovide，請輸入 hello 叢集系統管理員 （管理員） 和密碼時使用建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="51ca8-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="51ca8-170">在下**拓撲摘要**，選取 hello **wordcount** hello 中的項目**名稱**資料行。</span><span class="sxs-lookup"><span data-stu-id="51ca8-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="51ca8-171">會顯示 hello 拓撲的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-171">Information about hello topology is displayed.</span></span>

    ![包含 storm-starter WordCount 拓樸資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="51ca8-173">此頁面提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="51ca8-174">**拓樸 stats** -hello 拓撲效能的基本資訊組織成時段。</span><span class="sxs-lookup"><span data-stu-id="51ca8-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="51ca8-175">選取的特定時間視窗變更 hello 時間視窗 hello 網頁上的其他區段中顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="51ca8-176">**Spouts** -spouts，包括傳回每個 spout hello 最後一個錯誤的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="51ca8-177">**Bolts** ：bolt 的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="51ca8-178">**拓撲組態**-hello 拓撲組態有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="51ca8-179">此頁面也提供可以在 hello 拓撲採取的動作：</span><span class="sxs-lookup"><span data-stu-id="51ca8-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="51ca8-180">**啟用** ：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="51ca8-181">**停用** ：暫停執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="51ca8-182">**重新平衡**-調整 hello 拓樸的 hello 平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="51ca8-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="51ca8-183">之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="51ca8-184">重新平衡調整平行處理原則 toocompensate hello 增加/減少編號 hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="51ca8-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="51ca8-185">如需詳細資訊，請參閱[了解 hello 平行處理原則的 Storm 拓撲](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="51ca8-186">**Kill** -hello 指定逾時之後終止 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="51ca8-187">此頁面上，從選取的項目從 hello **Spouts**或**釘**> 一節。</span><span class="sxs-lookup"><span data-stu-id="51ca8-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="51ca8-188">會顯示 hello 選元件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-188">Information about hello selected component is displayed.</span></span>

    ![包含所選元件相關資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="51ca8-190">此頁面會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="51ca8-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="51ca8-191">**Spout 閃電 stats** -hello 元件效能的基本資訊組織成時段。</span><span class="sxs-lookup"><span data-stu-id="51ca8-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="51ca8-192">選取的特定時間視窗變更 hello 時間視窗 hello 網頁上的其他區段中顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="51ca8-193">**輸入 stats** （只有閃電）-產生 hello 閃電所耗用的資料之元件的資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="51ca8-194">**輸出統計資料 (Output stats)** ：此 bolt 發出之資料的資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="51ca8-195">**執行程式** ：此元件之執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="51ca8-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="51ca8-196">**錯誤** ：此元件產生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="51ca8-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="51ca8-197">當您檢視 spout 或閃電 hello 詳細資料，選取的項目從 hello**連接埠**hello 中的資料行**執行程式**區段 tooview hello 元件的特定執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51ca8-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="51ca8-198">在此範例中，hello word**七個**發生 1493957 的時間。</span><span class="sxs-lookup"><span data-stu-id="51ca8-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="51ca8-199">這個計數會啟動此拓撲後已發現 hello word 的次數。</span><span class="sxs-lookup"><span data-stu-id="51ca8-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="51ca8-200">停止 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="51ca8-200">Stop hello topology</span></span>

<span data-ttu-id="51ca8-201">傳回 toohello**拓撲摘要**hello 字數統計拓樸，頁面上，然後選取 hello **Kill**按鈕 hello**拓撲動作**> 一節。</span><span class="sxs-lookup"><span data-stu-id="51ca8-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="51ca8-202">出現提示時，輸入 10 hello 秒 toowait 之前停止 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="51ca8-203">Hello 逾時期限之後 hello 拓撲不會再出現當您瀏覽 hello **Storm UI** hello 儀表板的區段。</span><span class="sxs-lookup"><span data-stu-id="51ca8-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="51ca8-204">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="51ca8-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="51ca8-205">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="51ca8-206"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="51ca8-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="51ca8-207">在此 Apache Storm 教學課程中，您學到使用 Storm HDInsight 上的 hello 基本。</span><span class="sxs-lookup"><span data-stu-id="51ca8-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="51ca8-208">接下來，了解如何太[開發 Java 為基礎的拓撲使用 Maven](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="51ca8-209">如果您已經熟悉開發 Java 為基礎的拓撲，而且想 toodeploy 現存的拓撲 tooHDInsight，請參閱[部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="51ca8-210">如果您是 .NET 開發人員，您可以使用 Visual Studio 建立 C# 或混合式 C#/Java 拓撲。</span><span class="sxs-lookup"><span data-stu-id="51ca8-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="51ca8-211">如需詳細資訊，請參閱 [使用 Visual Studio 的 Hadoop 工具開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="51ca8-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="51ca8-212">如需可以搭配 Storm HDInsight 上的範例拓撲，請參閱 hello 遵循範例：</span><span class="sxs-lookup"><span data-stu-id="51ca8-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="51ca8-213">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="51ca8-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
