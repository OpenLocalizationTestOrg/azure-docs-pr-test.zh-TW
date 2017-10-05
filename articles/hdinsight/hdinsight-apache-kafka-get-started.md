---
title: "開始使用 Apache Kafka - Azure HDInsight | Microsoft Docs"
description: "了解如何在 Azure HDInsight 上建立 Apache Kafka 叢集。 了解如何建立主題、訂閱者和取用者。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="ec157-104">開始在 HDInsight 上使用 Apache Kafka (預覽)</span><span class="sxs-lookup"><span data-stu-id="ec157-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="ec157-105">了解如何在 Azure HDInsight 上建立和使用 [Apache Kafka](https://kafka.apache.org) 叢集。</span><span class="sxs-lookup"><span data-stu-id="ec157-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="ec157-106">Kafka 是 HDInsight 提供的開放原始碼分散式串流平台。</span><span class="sxs-lookup"><span data-stu-id="ec157-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="ec157-107">它通常作為訊息代理程式，因為它提供了類似於發佈-訂閱訊息佇列的功能。</span><span class="sxs-lookup"><span data-stu-id="ec157-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="ec157-108">HDInsight 目前提供兩個 Kafka 版本：0.9.0 (HDInsight 3.4) 和 0.10.0 (HDInsight 3.5 和 3.6)。</span><span class="sxs-lookup"><span data-stu-id="ec157-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="ec157-109">本文件中的步驟假設您使用 Kafka on HDInsight 3.6。</span><span class="sxs-lookup"><span data-stu-id="ec157-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="ec157-110">建立 Kafka 叢集</span><span class="sxs-lookup"><span data-stu-id="ec157-110">Create a Kafka cluster</span></span>

<span data-ttu-id="ec157-111">請使用下列步驟建立 Kafka on HDInsight：</span><span class="sxs-lookup"><span data-stu-id="ec157-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="ec157-112">從 [Azure 入口網站](https://portal.azure.com)選取 [+ 新增]、[情報 + 分析] 及 [HDInsight]，然後選取 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="ec157-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![建立 HDInsight 叢集](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="ec157-114">從 [基本概念]，輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="ec157-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="ec157-115">**叢集名稱**︰HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ec157-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="ec157-116">**訂用帳戶**：選取要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ec157-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="ec157-117">**叢集登入使用者名稱**和**叢集登入密碼**：透過 HTTPS 存取叢集時使用的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="ec157-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="ec157-118">您會使用這些認證來存取例如 Ambari Web UI 或 REST API 等服務。</span><span class="sxs-lookup"><span data-stu-id="ec157-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="ec157-119">**安全殼層 (SSH) 使用者名稱**：透過 SSH 存取叢集時使用的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="ec157-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="ec157-120">依預設，密碼要與叢集登入密碼相同。</span><span class="sxs-lookup"><span data-stu-id="ec157-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="ec157-121">**資源群組**：在其中建立叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ec157-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="ec157-122">**位置**：在其中建立叢集的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="ec157-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![選取訂用帳戶](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="ec157-124">選取 [叢集類型]，然後在 [叢集組態] 中設定下列值︰</span><span class="sxs-lookup"><span data-stu-id="ec157-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="ec157-125">**叢集類型**：Kafka</span><span class="sxs-lookup"><span data-stu-id="ec157-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="ec157-126">**版本**：Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="ec157-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="ec157-127">**叢集層**：標準</span><span class="sxs-lookup"><span data-stu-id="ec157-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="ec157-128">最後，使用 [選取] 按鈕來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="ec157-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![選取叢集類型](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="ec157-130">選取叢集類型之後，請使用 [選取] 按鈕來設定叢集類型。</span><span class="sxs-lookup"><span data-stu-id="ec157-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="ec157-131">接下來，使用 [下一步] 按鈕來完成基本組態。</span><span class="sxs-lookup"><span data-stu-id="ec157-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="ec157-132">從 [儲存體]，選取或建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ec157-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="ec157-133">本文件的步驟是將其他欄位保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="ec157-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="ec157-134">使用 [下一步] 按鈕以儲存儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="ec157-134">Use the __Next__ button to save storage configuration.</span></span>

    ![設定 HDInsight 的儲存體帳戶](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="ec157-136">從 [應用程式 (選擇性)]，選取 [下一步] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="ec157-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="ec157-137">這個範例不需要任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec157-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="ec157-138">從 [叢集大小]，選取 [下一步] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="ec157-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="ec157-139">若要保證 Kafka 在 HDInsight 上的可用性，您的叢集必須包含至少三個背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="ec157-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![設定 Kafka 叢集大小](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="ec157-141">[每個背景工作角色節點的磁碟數] 項目會控制 Kafka on HDInsight 的延展性。</span><span class="sxs-lookup"><span data-stu-id="ec157-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="ec157-142">如需詳細資訊，請參閱[設定 HDInsight 上 Kafka 的儲存體和延展性](hdinsight-apache-kafka-scalability.md)。</span><span class="sxs-lookup"><span data-stu-id="ec157-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="ec157-143">從 [進階設定]，選取 [下一步] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="ec157-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="ec157-144">從 [摘要] 檢閱叢集組態。</span><span class="sxs-lookup"><span data-stu-id="ec157-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="ec157-145">使用 [編輯] 連結來變更所有不正確的設定。</span><span class="sxs-lookup"><span data-stu-id="ec157-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="ec157-146">最後，使用 [建立] 按鈕來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="ec157-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![叢集組態摘要](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="ec157-148">建立叢集可能需要花費 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ec157-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="ec157-149">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="ec157-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec157-150">執行下列步驟時，您必須使用 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ec157-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="ec157-151">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="ec157-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="ec157-152">從您的用戶端，使用 SSH 連線到叢集：</span><span class="sxs-lookup"><span data-stu-id="ec157-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="ec157-153">將 **SSHUSER** 取代為您在叢集建立期間提供的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ec157-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="ec157-154">將 **CLUSTERNAME** 取代為叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ec157-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="ec157-155">出現提示時，輸入您用於 SSH 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ec157-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="ec157-156">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ec157-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="ec157-157"><a id="getkafkainfo"></a>取得 Zookeeper 和訊息代理程式主機資訊</span><span class="sxs-lookup"><span data-stu-id="ec157-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="ec157-158">使用 Kafka 時，您必須知道兩個主機值；Zookeeper 主機和訊息代理程式主機。</span><span class="sxs-lookup"><span data-stu-id="ec157-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="ec157-159">這些主機可搭配 Kafka API 以及 Kafka 隨附的許多公用程式使用。</span><span class="sxs-lookup"><span data-stu-id="ec157-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="ec157-160">使用下列步驟來建立包含主機資訊的環境變數。</span><span class="sxs-lookup"><span data-stu-id="ec157-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="ec157-161">這些環境變數使用於本文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ec157-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="ec157-162">在連往叢集的 SSH 連線中，使用下列命令來安裝 `jq` 公用程式。</span><span class="sxs-lookup"><span data-stu-id="ec157-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="ec157-163">此公用程式用來剖析 JSON 文件，而且在擷取訊息代理程式主機資訊時很有用︰</span><span class="sxs-lookup"><span data-stu-id="ec157-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="ec157-164">若要以擷取自 Ambari 的資訊設定環境變數，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec157-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ec157-165">將 `CLUSTERNAME=` 設定為 Kafka 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ec157-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="ec157-166">將 `PASSWORD=` 設定為您在建立叢集時使用的登入 (admin) 密碼。</span><span class="sxs-lookup"><span data-stu-id="ec157-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="ec157-167">以下文字是 `$KAFKAZKHOSTS` 的內容範例：</span><span class="sxs-lookup"><span data-stu-id="ec157-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="ec157-168">以下文字是 `$KAFKABROKERS` 的內容範例：</span><span class="sxs-lookup"><span data-stu-id="ec157-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="ec157-169">`cut` 命令用於將主機清單修剪為兩個主機項目。</span><span class="sxs-lookup"><span data-stu-id="ec157-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="ec157-170">建立 Kafka 取用者或產生者時，您不需要提供完整的主機清單。</span><span class="sxs-lookup"><span data-stu-id="ec157-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="ec157-171">請勿認為從此工作階段傳回的資訊永遠都正確無誤。</span><span class="sxs-lookup"><span data-stu-id="ec157-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="ec157-172">如果您調整叢集，則會新增或移除新的訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="ec157-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="ec157-173">如果發生失敗且節點被更換，則節點的主機名稱可能會變更。</span><span class="sxs-lookup"><span data-stu-id="ec157-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="ec157-174">您應在使用 Zookeeper 和訊息代理程式主機資訊不久前擷取該資訊，以確保您具備有效的資訊。</span><span class="sxs-lookup"><span data-stu-id="ec157-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="ec157-175">建立主題</span><span class="sxs-lookup"><span data-stu-id="ec157-175">Create a topic</span></span>

<span data-ttu-id="ec157-176">Kafka 會將資料串流儲存在名為 *topics* 的類別中。</span><span class="sxs-lookup"><span data-stu-id="ec157-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="ec157-177">在連往叢集前端節點的 SSH 連線中，使用 Kafka 所提供的指令碼來建立主題︰</span><span class="sxs-lookup"><span data-stu-id="ec157-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="ec157-178">此命令會使用 `$KAFKAZKHOSTS` 中儲存的主機資訊連接到 Zookeeper，然後建立名為 **test** 的 Kafka 主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="ec157-179">您可以確認使用下列指令碼建立的主題可列出主題︰</span><span class="sxs-lookup"><span data-stu-id="ec157-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="ec157-180">此命令的輸出會列出 Kafka 主題，其中包含 **test** 主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="ec157-181">產生和取用記錄</span><span class="sxs-lookup"><span data-stu-id="ec157-181">Produce and consume records</span></span>

<span data-ttu-id="ec157-182">Kafka 會在主題中儲存「記錄」。</span><span class="sxs-lookup"><span data-stu-id="ec157-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="ec157-183">記錄是由「產生者」產生，並由「取用者」取用。</span><span class="sxs-lookup"><span data-stu-id="ec157-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="ec157-184">產生者會從 Kafka「訊息代理程式」擷取記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="ec157-185">HDInsight 叢集中的每個背景工作節點都是 Kafka 訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="ec157-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="ec157-186">使用下列步驟，將記錄儲存至您稍早建立的 test 主題，然後利用取用者進行讀取︰</span><span class="sxs-lookup"><span data-stu-id="ec157-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="ec157-187">在 SSH 工作階段中，使用 Kafka 提供的指令碼將記錄寫入主題︰</span><span class="sxs-lookup"><span data-stu-id="ec157-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="ec157-188">您不會在此命令後返回提示字元。</span><span class="sxs-lookup"><span data-stu-id="ec157-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="ec157-189">反而，輸入一些文字訊息，然後使用 **Ctrl + C** 停止傳送至主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="ec157-190">每一行都會以個別的記錄傳送。</span><span class="sxs-lookup"><span data-stu-id="ec157-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="ec157-191">使用 Kafka 提供的指令碼來讀取主題中的記錄︰</span><span class="sxs-lookup"><span data-stu-id="ec157-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="ec157-192">此命令會擷取主題中的記錄並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="ec157-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="ec157-193">使用 `--from-beginning` 告知取用者從串流的開頭開始，所以會擷取所有的記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="ec157-194">使用 __Ctrl + C__ 來停止取用者。</span><span class="sxs-lookup"><span data-stu-id="ec157-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="ec157-195">產生者和取用者 API</span><span class="sxs-lookup"><span data-stu-id="ec157-195">Producer and consumer API</span></span>

<span data-ttu-id="ec157-196">您也可以利用 [Kafka API](http://kafka.apache.org/documentation#api)，以程式設計方式產生和取用記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="ec157-197">若要建立 Java 產生者和取用者，請在開發環境中使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ec157-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec157-198">您必須在開發環境中安裝下列元件：</span><span class="sxs-lookup"><span data-stu-id="ec157-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="ec157-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 或同等功能版本，例如 OpenJDK。</span><span class="sxs-lookup"><span data-stu-id="ec157-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="ec157-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="ec157-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="ec157-201">SSH 用戶端和 `scp` 命令。</span><span class="sxs-lookup"><span data-stu-id="ec157-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="ec157-202">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="ec157-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="ec157-203">從 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) 下載範例。</span><span class="sxs-lookup"><span data-stu-id="ec157-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="ec157-204">在生產者/取用者範例中，使用 `Producer-Consumer` 目錄中的專案。</span><span class="sxs-lookup"><span data-stu-id="ec157-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="ec157-205">範例包含下列類別：</span><span class="sxs-lookup"><span data-stu-id="ec157-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="ec157-206">**執行** - 由取用者或生產者開始。</span><span class="sxs-lookup"><span data-stu-id="ec157-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="ec157-207">**產生者** - 將 1,000,000 筆記錄儲存至主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="ec157-208">**取用者** - 讀取主題中的記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="ec157-209">若要建立 jar 套件，請將目錄變更為 `Producer-Consumer` 目錄的位置並使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ec157-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="ec157-210">此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-producer-consumer-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ec157-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="ec157-211">使用下列命令將 `kafka-producer-consumer-1.0-SNAPSHOT.jar` 檔案複製到 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="ec157-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="ec157-212">以叢集的 SSH 使用者取代 **USERNAME**，並以叢集的名稱取代 **CLUSTERNAME**。</span><span class="sxs-lookup"><span data-stu-id="ec157-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="ec157-213">出現提示時，請輸入 SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="ec157-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="ec157-214">`scp` 命令完成檔案複製後，請使用 SSH 連線到叢集：</span><span class="sxs-lookup"><span data-stu-id="ec157-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="ec157-215">使用下列命令將記錄寫入測試主題：</span><span class="sxs-lookup"><span data-stu-id="ec157-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="ec157-216">完成此程序後，請使用下列命令從主題讀取︰</span><span class="sxs-lookup"><span data-stu-id="ec157-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="ec157-217">已讀取的記錄以及記錄計數隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="ec157-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="ec157-218">您可能會看到已記錄 1,000,000 筆以上，因為您是使用先前步驟中的指令碼將數筆記錄傳送至主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="ec157-219">使用 __Ctrl + C__ 來結束取用者。</span><span class="sxs-lookup"><span data-stu-id="ec157-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="ec157-220">多個取用者</span><span class="sxs-lookup"><span data-stu-id="ec157-220">Multiple consumers</span></span>

<span data-ttu-id="ec157-221">Kafka 取用者會在讀取記錄時使用取用者群組。</span><span class="sxs-lookup"><span data-stu-id="ec157-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="ec157-222">多個取用者使用相同群組會導致從主題讀取負載平衡。</span><span class="sxs-lookup"><span data-stu-id="ec157-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="ec157-223">群組中的每個取用者都會收到一部分的記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="ec157-224">若要查看此程序的運作情況，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ec157-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="ec157-225">開啟連往叢集的新 SSH 工作階段，您便有兩個工作階段。</span><span class="sxs-lookup"><span data-stu-id="ec157-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="ec157-226">在每個工作階段中，使用下列命令來啟動具有相同取用者群組識別碼的取用者：</span><span class="sxs-lookup"><span data-stu-id="ec157-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="ec157-227">此命令會啟動使用群組識別碼 `mygroup` 的取用者。</span><span class="sxs-lookup"><span data-stu-id="ec157-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec157-228">使用[取得 Zookeeper 和訊息代理程式主機資訊](#getkafkainfo)一節中的命令來設定此 SSH 工作階段的 `$KAFKABROKERS`。</span><span class="sxs-lookup"><span data-stu-id="ec157-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="ec157-229">觀看每個工作階段計算其從主題接收的記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="ec157-230">這兩個工作階段的總數應該與您先前從一個取用者收到的數量相同。</span><span class="sxs-lookup"><span data-stu-id="ec157-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="ec157-231">透過主題的資料分割處理相同群組內的用戶端取用。</span><span class="sxs-lookup"><span data-stu-id="ec157-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="ec157-232">稍早建立的 `test` 主題有 8 個資料分割。</span><span class="sxs-lookup"><span data-stu-id="ec157-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="ec157-233">如果您開啟 8 個 SSH 工作階段並在所有工作階段中啟動某個取用者，則每個取用者都會從主題的單一資料分割讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec157-234">一個取用者群組中的取用者執行個體不得超過資料分割。</span><span class="sxs-lookup"><span data-stu-id="ec157-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="ec157-235">在此範例中，一個取用者群組可以包含最多 8 個取用者，因為這是主題中的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="ec157-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="ec157-236">或者，您可以有多個取用者群組，其各有不超過 8 個取用者。</span><span class="sxs-lookup"><span data-stu-id="ec157-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="ec157-237">Kafka 中儲存的記錄會依照其在資料分割內接收的順序儲存。</span><span class="sxs-lookup"><span data-stu-id="ec157-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="ec157-238">若要達到依序傳遞「資料分割內」的記錄，請建立取用者群組，其中的取用者執行個體數目與資料分割數目相符。</span><span class="sxs-lookup"><span data-stu-id="ec157-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="ec157-239">若要達到依序傳遞「主題內」的記錄，請建立只有一個取用者執行個體的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="ec157-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="ec157-240">串流 API</span><span class="sxs-lookup"><span data-stu-id="ec157-240">Streaming API</span></span>

<span data-ttu-id="ec157-241">串流 API 已新增至 0.10.0 版中的 Kafka；舊版依賴 Apache Spark 或 Storm 進行串流處理。</span><span class="sxs-lookup"><span data-stu-id="ec157-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="ec157-242">若尚未這樣做，請從 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) 將範例下載到您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="ec157-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="ec157-243">在串流範例中，使用 `streaming` 目錄中的專案。</span><span class="sxs-lookup"><span data-stu-id="ec157-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="ec157-244">此專案只包含一個類別 (`Stream`)，該類別會從先前建立的 `test` 主題讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="ec157-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="ec157-245">它會計算已讀取的字數，並發出每個單字並計入名為 `wordcounts` 的主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="ec157-246">本節中稍後的步驟會建立 `wordcounts` 主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="ec157-247">從開發環境中的命令列，將目錄變更至 `Streaming` 目錄的位置，然後使用下列命令來建立 jar 套件︰</span><span class="sxs-lookup"><span data-stu-id="ec157-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="ec157-248">此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-streaming-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ec157-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="ec157-249">使用下列命令將 `kafka-streaming-1.0-SNAPSHOT.jar` 檔案複製到 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="ec157-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="ec157-250">以叢集的 SSH 使用者取代 **USERNAME**，並以叢集的名稱取代 **CLUSTERNAME**。</span><span class="sxs-lookup"><span data-stu-id="ec157-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="ec157-251">出現提示時，請輸入 SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="ec157-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="ec157-252">`scp` 命令完成檔案複製後，請使用 SSH 連接到叢集，然後使用下列命令來建立 `wordcounts` 主題：</span><span class="sxs-lookup"><span data-stu-id="ec157-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="ec157-253">接著，使用下列命令來啟動串流程序：</span><span class="sxs-lookup"><span data-stu-id="ec157-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="ec157-254">此命令會在背景中啟動串流程序。</span><span class="sxs-lookup"><span data-stu-id="ec157-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="ec157-255">使用下列命令將訊息傳送至 `test` 主題。</span><span class="sxs-lookup"><span data-stu-id="ec157-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="ec157-256">這些訊息會依以下串流範例進行處理：</span><span class="sxs-lookup"><span data-stu-id="ec157-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="ec157-257">使用下列命令來檢視由串流程序寫入到 `wordcounts` 主題的輸出︰</span><span class="sxs-lookup"><span data-stu-id="ec157-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="ec157-258">若要檢視資料，您必須請取用者列印金鑰和金鑰與值所使用的還原序列化程式。</span><span class="sxs-lookup"><span data-stu-id="ec157-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="ec157-259">金鑰名稱為文字，而金鑰值則包含計數。</span><span class="sxs-lookup"><span data-stu-id="ec157-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="ec157-260">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="ec157-260">The output is similar to the following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="ec157-261">每次遇到一個單字，計數就會遞增。</span><span class="sxs-lookup"><span data-stu-id="ec157-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="ec157-262">使用 __Ctrl + C__ 結束取用者，然後使用 `fg` 命令將串流背景工作帶回前景。</span><span class="sxs-lookup"><span data-stu-id="ec157-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="ec157-263">使用 __Ctrl + C__ 將它結束。</span><span class="sxs-lookup"><span data-stu-id="ec157-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="ec157-264">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="ec157-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="ec157-265">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ec157-265">Troubleshoot</span></span>

<span data-ttu-id="ec157-266">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="ec157-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec157-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec157-267">Next steps</span></span>

<span data-ttu-id="ec157-268">在本文件中，您已學會使用 Apache Kafka on HDInsight 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="ec157-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="ec157-269">使用下列各項來深入了解 Kafka 的使用方式︰</span><span class="sxs-lookup"><span data-stu-id="ec157-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="ec157-270">使用 HDInsight 上的 Kafka 確保您資料的高可用性</span><span class="sxs-lookup"><span data-stu-id="ec157-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="ec157-271">使用 HDInsight 上的 Kafka 設定受控磁碟來提高延展性</span><span class="sxs-lookup"><span data-stu-id="ec157-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="ec157-272">kafka.apache.org 上的 [Apache Kafka 文件](http://kafka.apache.org/documentation.html)。</span><span class="sxs-lookup"><span data-stu-id="ec157-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="ec157-273">使用 MirrorMaker 建立 Apache Kafka on HDInsight 複本</span><span class="sxs-lookup"><span data-stu-id="ec157-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="ec157-274">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="ec157-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="ec157-275">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec157-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="ec157-276">透過 Azure 虛擬網路連線至 Kafka</span><span class="sxs-lookup"><span data-stu-id="ec157-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
