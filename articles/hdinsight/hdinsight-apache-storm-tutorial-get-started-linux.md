---
title: "HDInsight 上 Apache Storm 的 Storm-starter 範例 | Microsoft Docs"
description: "了解如何使用 Apache Storm 和 HDInsight 上的 storm-starter 範例來執行巨量資料分析及處理資料。"
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
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="f4a88-104">使用 storm-starter 範例在 HDInsight 上開始使用 Apache Storm</span><span class="sxs-lookup"><span data-stu-id="f4a88-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="f4a88-105">了解如何使用 storm-starter 範例，在 HDInsight 中使用 Apache Storm。</span><span class="sxs-lookup"><span data-stu-id="f4a88-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="f4a88-106">Apache Storm 是一個可處理資料串流的分散式、容錯、即時的運算系統。</span><span class="sxs-lookup"><span data-stu-id="f4a88-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="f4a88-107">在 Storm on Azure HDInsight 中，您可以建立雲端式 Storm 叢集，以執行即時的巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="f4a88-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4a88-108">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="f4a88-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f4a88-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4a88-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f4a88-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="f4a88-111">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f4a88-111">**An Azure subscription**.</span></span> <span data-ttu-id="f4a88-112">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f4a88-113">**熟悉 SSH 和 SCP**。</span><span class="sxs-lookup"><span data-stu-id="f4a88-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="f4a88-114">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="f4a88-115">建立 Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="f4a88-115">Create a Storm cluster</span></span>

<span data-ttu-id="f4a88-116">請使用下列步驟建立 Storm on HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="f4a88-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="f4a88-117">從 [Azure 入口網站](https://portal.azure.com)選取 [+ 新增]、[情報 + 分析] 及 [HDInsight]，然後選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="f4a88-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![建立 HDInsight 叢集](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="f4a88-119">在 [基本概念] 刀鋒視窗中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f4a88-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="f4a88-120">**叢集名稱**︰HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f4a88-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="f4a88-121">**訂用帳戶**：選取要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4a88-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="f4a88-122">**叢集登入使用者名稱**和**叢集登入密碼**：透過 HTTPS 存取叢集時使用的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="f4a88-123">您會使用這些認證來存取例如 Ambari Web UI 或 REST API 等服務。</span><span class="sxs-lookup"><span data-stu-id="f4a88-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="f4a88-124">**安全殼層 (SSH) 使用者名稱**：透過 SSH 存取叢集時使用的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="f4a88-125">依預設，密碼要與叢集登入密碼相同。</span><span class="sxs-lookup"><span data-stu-id="f4a88-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="f4a88-126">**資源群組**：在其中建立叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f4a88-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="f4a88-127">**位置**：在其中建立叢集的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="f4a88-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![選取訂用帳戶](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="f4a88-129">選取 [叢集類型]，並且在 [叢集組態] 刀鋒視窗中設定下列值︰</span><span class="sxs-lookup"><span data-stu-id="f4a88-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="f4a88-130">**叢集類型**：Storm</span><span class="sxs-lookup"><span data-stu-id="f4a88-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="f4a88-131">**作業系統**：Linux</span><span class="sxs-lookup"><span data-stu-id="f4a88-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="f4a88-132">**版本**：Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="f4a88-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="f4a88-133">**叢集層**：標準</span><span class="sxs-lookup"><span data-stu-id="f4a88-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="f4a88-134">最後，使用 [選取] 按鈕來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="f4a88-134">Finally, use the **Select** button to save settings.</span></span>

    ![選取叢集類型](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="f4a88-136">選取叢集類型之後，請使用 [選取] 按鈕來設定叢集類型。</span><span class="sxs-lookup"><span data-stu-id="f4a88-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="f4a88-137">接下來，使用 [下一步] 按鈕來完成基本組態。</span><span class="sxs-lookup"><span data-stu-id="f4a88-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="f4a88-138">從 [儲存體] 刀鋒視窗中，選取或建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4a88-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="f4a88-139">本文件的步驟是，將此刀鋒視窗中的其他欄位保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="f4a88-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="f4a88-140">使用 [下一步] 按鈕以儲存儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="f4a88-140">Use the __Next__ button to save storage configuration.</span></span>

    ![設定 HDInsight 的儲存體帳戶](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="f4a88-142">從 [摘要] 刀鋒視窗中，檢閱叢集組態。</span><span class="sxs-lookup"><span data-stu-id="f4a88-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="f4a88-143">使用 [編輯] 連結來變更所有不正確的設定。</span><span class="sxs-lookup"><span data-stu-id="f4a88-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="f4a88-144">最後，使用 [建立] 按鈕來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="f4a88-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![叢集組態摘要](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="f4a88-146">建立叢集可能需要花費 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="f4a88-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="f4a88-147">在 HDInsight 上執行 storm-starter 範例</span><span class="sxs-lookup"><span data-stu-id="f4a88-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="f4a88-148">使用 SSH 連線到 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f4a88-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="f4a88-149">如果您已經使用密碼保護您 SSH 使用者帳戶的安全，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="f4a88-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="f4a88-150">如果您使用的是公開金鑰，您需要使用 `-i` 參數來指定對應的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4a88-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="f4a88-151">例如， `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="f4a88-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="f4a88-152">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f4a88-153">使用下列命令以啟動範例拓撲：</span><span class="sxs-lookup"><span data-stu-id="f4a88-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="f4a88-154">在舊版 HDInsight 上，拓撲的類別名稱是 `storm.starter.WordCountTopology` 而不是 `org.apache.storm.starter.WordCountTopology`。</span><span class="sxs-lookup"><span data-stu-id="f4a88-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="f4a88-155">此命令會在叢集上使用 'wordcount' 的易記名稱，啟動範例 WordCount 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="f4a88-156">命令會隨機產生句子，並計算句子中每個字詞的出現次數。</span><span class="sxs-lookup"><span data-stu-id="f4a88-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f4a88-157">將您自己的拓撲提交至叢集時，必須先複製包含叢集的 jar 檔案，再使用 `storm` 命令。</span><span class="sxs-lookup"><span data-stu-id="f4a88-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="f4a88-158">使用 `scp` 命令來複製檔案。</span><span class="sxs-lookup"><span data-stu-id="f4a88-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="f4a88-159">例如， `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="f4a88-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="f4a88-160">WordCount 範例和其他 storm-starter 範例都已經包含在叢集中，位置是 `/usr/hdp/current/storm-client/contrib/storm-starter/`。</span><span class="sxs-lookup"><span data-stu-id="f4a88-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="f4a88-161">如果您有興趣檢視 storm-starter 範例的來源，可以在 [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter) 找到程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4a88-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="f4a88-162">這個連結是 Storm 1.1.x，隨附於 HDInsight 3.6。</span><span class="sxs-lookup"><span data-stu-id="f4a88-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="f4a88-163">如需其他 Storm 版本，請使用頁面頂端的 __Branch__ 分支 按鈕來選取其他 Storm 版本。</span><span class="sxs-lookup"><span data-stu-id="f4a88-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="f4a88-164">監視拓撲</span><span class="sxs-lookup"><span data-stu-id="f4a88-164">Monitor the topology</span></span>

<span data-ttu-id="f4a88-165">Storm UI 提供 Web 介面來處理執行中的拓撲，包含在您的 HDInsight 叢集中。</span><span class="sxs-lookup"><span data-stu-id="f4a88-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="f4a88-166">使用下列步驟以 Storm UI 監視拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="f4a88-167">若要顯示 Storm UI，請開啟網頁瀏覽器並前往 https://CLUSTERNAME.azurehdinsight.net/stormui。</span><span class="sxs-lookup"><span data-stu-id="f4a88-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="f4a88-168">將 **CLUSTERNAME** 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f4a88-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f4a88-169">如果要求您提供使用者名稱和密碼，請輸入叢集系統管理員 (admin) 和建立叢集時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f4a88-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="f4a88-170">在 [拓撲摘要] 下，選取 [名稱] 欄中的 [wordcount] 項目。</span><span class="sxs-lookup"><span data-stu-id="f4a88-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="f4a88-171">關於拓撲的詳細資訊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f4a88-171">Information about the topology is displayed.</span></span>

    ![包含 storm-starter WordCount 拓樸資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="f4a88-173">此頁面提供以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f4a88-173">This page provides the following information:</span></span>

    * <span data-ttu-id="f4a88-174">**拓撲統計資料 (Topology stats)** ：拓撲效能的基本資訊，已整理為時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f4a88-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f4a88-175">選取特定的時間範圍，可以變更頁面中其他區段所顯示之資訊的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f4a88-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="f4a88-176">**Spouts** ：spout 的基本資訊，包括每個 spout 傳回的最後一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="f4a88-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="f4a88-177">**Bolts** ：bolt 的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="f4a88-178">**拓撲組態 (Topology configuration)** ：拓撲組態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="f4a88-179">此頁面也提供可對拓撲採取的動作：</span><span class="sxs-lookup"><span data-stu-id="f4a88-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="f4a88-180">**啟用** ：繼續處理已停用的拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="f4a88-181">**停用** ：暫停執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="f4a88-182">**重新平衡** ：調整拓撲的平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="f4a88-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="f4a88-183">變更叢集中的節點數目之後，您應該重新平衡執行中拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="f4a88-184">重新平衡調整平行處理原則，以彌補叢集中增加/減少的節點數目。</span><span class="sxs-lookup"><span data-stu-id="f4a88-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="f4a88-185">如需詳細資訊，請參閱[了解 Storm 拓撲的平行處理原則](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="f4a88-186">**終止 (Kill)** ：在指定的逾時之後終止 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="f4a88-187">在此頁面中，選取 [Spouts] 或 [Bolts] 區段中的一個項目。</span><span class="sxs-lookup"><span data-stu-id="f4a88-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="f4a88-188">關於所選元件的詳細資訊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f4a88-188">Information about the selected component is displayed.</span></span>

    ![包含所選元件相關資訊的 Storm 儀表板。](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="f4a88-190">此頁面會顯示以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f4a88-190">This page displays the following information:</span></span>

    * <span data-ttu-id="f4a88-191">**Spout/Bolt 統計資料 (Spout/Bolt stats)** ：元件效能的基本資訊，已整理為時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f4a88-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f4a88-192">選取特定的時間範圍，可以變更頁面中其他區段所顯示之資訊的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f4a88-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="f4a88-193">**輸入統計資料 (Input stats)** (僅 bolt)：提供的資訊是關於產生 bolt 所使用之資料的元件。</span><span class="sxs-lookup"><span data-stu-id="f4a88-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="f4a88-194">**輸出統計資料 (Output stats)** ：此 bolt 發出之資料的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="f4a88-195">**執行程式** ：此元件之執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4a88-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="f4a88-196">**錯誤** ：此元件產生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f4a88-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="f4a88-197">檢視 spout 或 bolt 的詳細資料時，請在 [執行程式] 區段的 [連接埠] 欄中選取一個項目，以檢視特定元件執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f4a88-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="f4a88-198">在此範例中，「七」這個字出現 1493957 次。</span><span class="sxs-lookup"><span data-stu-id="f4a88-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="f4a88-199">此計數就是啟動拓撲後，該字所出現的次數。</span><span class="sxs-lookup"><span data-stu-id="f4a88-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="f4a88-200">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="f4a88-200">Stop the topology</span></span>

<span data-ttu-id="f4a88-201">返回 word-count 拓撲的 [拓撲摘要] 頁面，然後選取 [拓撲動作] 區段中的 [終止] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f4a88-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="f4a88-202">出現提示時，請先輸入要等候 10 秒，再停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="f4a88-203">逾時期限過後，當您瀏覽儀表板的 [Storm UI]  區段時，就不會再看到拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="f4a88-204">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="f4a88-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f4a88-205">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="f4a88-206"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="f4a88-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="f4a88-207">在本 Apache Storm 教學課程中，您已了解使用 Storm on HDInsight 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="f4a88-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="f4a88-208">接下來，了解如何 [使用 Maven 開發 Java 型拓撲](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="f4a88-209">如果您已熟悉開發 Java 型拓撲，而且想要將現有的拓撲部署至 HDInsight，請參閱 [部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="f4a88-210">如果您是 .NET 開發人員，您可以使用 Visual Studio 建立 C# 或混合式 C#/Java 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f4a88-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="f4a88-211">如需詳細資訊，請參閱 [使用 Visual Studio 的 Hadoop 工具開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a88-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="f4a88-212">如需可搭配 Storm on HDInsight 使用的拓撲範例，請參閱下列範例︰</span><span class="sxs-lookup"><span data-stu-id="f4a88-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="f4a88-213">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="f4a88-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
