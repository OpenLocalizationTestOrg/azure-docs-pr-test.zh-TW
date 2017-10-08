---
title: "使用 Apache Kafka-Azure HDInsight aaaStart |Microsoft 文件"
description: "了解 toocreate Apache Kafka Azure HDInsight 上的叢集化。 深入了解如何 toocreate 主題、 訂閱者與取用者。"
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
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="0e79f-104">開始在 HDInsight 上使用 Apache Kafka (預覽)</span><span class="sxs-lookup"><span data-stu-id="0e79f-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="0e79f-105">深入了解如何 toocreate 並用[Apache Kafka](https://kafka.apache.org)上 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0e79f-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="0e79f-106">Kafka 是 HDInsight 提供的開放原始碼分散式串流平台。</span><span class="sxs-lookup"><span data-stu-id="0e79f-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="0e79f-107">通常是當做訊息仲介，因為它提供了類似的功能 tooa 發行-訂閱訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="0e79f-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="0e79f-108">HDInsight 目前提供兩個 Kafka 版本：0.9.0 (HDInsight 3.4) 和 0.10.0 (HDInsight 3.5 和 3.6)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="0e79f-109">本文件中的 hello 步驟假設您使用 Kafka HDInsight 3.6 上。</span><span class="sxs-lookup"><span data-stu-id="0e79f-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="0e79f-110">建立 Kafka 叢集</span><span class="sxs-lookup"><span data-stu-id="0e79f-110">Create a Kafka cluster</span></span>

<span data-ttu-id="0e79f-111">使用下列步驟 toocreate Kafka HDInsight 叢集上的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="0e79f-112">從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增**，**智慧 + 分析**，然後選取**HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="0e79f-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![建立 HDInsight 叢集](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="0e79f-114">從**基本概念**，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="0e79f-115">**叢集名稱**: hello hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="0e79f-116">**訂用帳戶**： 選取 hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="0e79f-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="0e79f-117">**叢集登入使用者名稱**和**叢集登入密碼**: hello 登入透過 HTTPS 存取 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="0e79f-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="0e79f-118">您使用這些認證 tooaccess 服務，例如 hello Ambari Web UI 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="0e79f-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="0e79f-119">**安全殼層 (SSH) 的使用者名稱**: hello 透過 SSH 存取 hello 叢集時使用的登入。</span><span class="sxs-lookup"><span data-stu-id="0e79f-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="0e79f-120">根據預設 hello 密碼是 hello hello 叢集登入密碼相同。</span><span class="sxs-lookup"><span data-stu-id="0e79f-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="0e79f-121">**資源群組**: hello 資源群組 toocreate hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="0e79f-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="0e79f-122">**位置**: hello Azure 地區 toocreate hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="0e79f-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![選取訂用帳戶](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="0e79f-124">選取**叢集類型**，然後組 hello 遵循值**叢集設定**:</span><span class="sxs-lookup"><span data-stu-id="0e79f-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="0e79f-125">**叢集類型**：Kafka</span><span class="sxs-lookup"><span data-stu-id="0e79f-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="0e79f-126">**版本**：Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="0e79f-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="0e79f-127">**叢集層**：標準</span><span class="sxs-lookup"><span data-stu-id="0e79f-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="0e79f-128">最後，使用 hello**選取**按鈕 toosave 設定。</span><span class="sxs-lookup"><span data-stu-id="0e79f-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![選取叢集類型](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="0e79f-130">選取 hello 叢集類型後，使用 hello__選取__按鈕 tooset hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="0e79f-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="0e79f-131">接下來，使用 hello__下一步__按鈕 toofinish 基本組態。</span><span class="sxs-lookup"><span data-stu-id="0e79f-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="0e79f-132">從 [儲存體]，選取或建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e79f-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="0e79f-133">如需本文件中的 hello 步驟，hello 其他欄位保留在 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="0e79f-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="0e79f-134">使用 hello__下一步__按鈕 toosave 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="0e79f-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![設定 hello HDInsight 的儲存體帳戶設定](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="0e79f-136">從__應用程式 （選擇性）__，選取__下一步__toocontinue。</span><span class="sxs-lookup"><span data-stu-id="0e79f-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="0e79f-137">這個範例不需要任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e79f-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="0e79f-138">從__叢集大小__，選取__下一步__toocontinue。</span><span class="sxs-lookup"><span data-stu-id="0e79f-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0e79f-139">HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="0e79f-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![設定 hello Kafka 叢集大小](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="0e79f-141">hello**磁碟每個背景工作節點**項目控制項 hello Kafka HDInsight 上的延展性。</span><span class="sxs-lookup"><span data-stu-id="0e79f-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="0e79f-142">如需詳細資訊，請參閱[設定 HDInsight 上 Kafka 的儲存體和延展性](hdinsight-apache-kafka-scalability.md)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="0e79f-143">從__進階設定__，選取__下一步__toocontinue。</span><span class="sxs-lookup"><span data-stu-id="0e79f-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="0e79f-144">從 hello**摘要**，檢閱 hello hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="0e79f-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="0e79f-145">使用 hello__編輯__連結 toochange 任何不正確的設定。</span><span class="sxs-lookup"><span data-stu-id="0e79f-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="0e79f-146">最後，使用 the__Create__ 按鈕 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="0e79f-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![叢集組態摘要](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="0e79f-148">它可能會佔用 too20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="0e79f-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="0e79f-149">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="0e79f-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e79f-150">在執行下列步驟的 hello 時，您必須使用 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="0e79f-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="0e79f-151">如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0e79f-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="0e79f-152">從您的用戶端使用 SSH tooconnect toohello 叢集：</span><span class="sxs-lookup"><span data-stu-id="0e79f-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="0e79f-153">取代**SSHUSER**與 hello 您在叢集建立期間所提供的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="0e79f-154">取代**CLUSTERNAME** hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="0e79f-155">出現提示時，輸入您所使用的 hello SSH 帳戶的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0e79f-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="0e79f-156">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="0e79f-157"><a id="getkafkainfo"></a>取得 hello 動物園管理員和代理人主機資訊</span><span class="sxs-lookup"><span data-stu-id="0e79f-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="0e79f-158">當使用 Kafka，您必須知道兩個主機的值;hello*動物園管理員*主機和 hello *Broker*主機。</span><span class="sxs-lookup"><span data-stu-id="0e79f-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="0e79f-159">這些主控件用於 Kafka 有 hello Kafka API 和出貨的 hello 公用程式的許多。</span><span class="sxs-lookup"><span data-stu-id="0e79f-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="0e79f-160">使用下列步驟 toocreate 環境變數包含 hello 主機資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="0e79f-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="0e79f-161">本文件中的 hello 步驟中使用這些環境變數。</span><span class="sxs-lookup"><span data-stu-id="0e79f-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="0e79f-162">SSH 連線 toohello 叢集中，從使用 hello 下列的命令 tooinstall hello`jq`公用程式。</span><span class="sxs-lookup"><span data-stu-id="0e79f-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="0e79f-163">此公用程式是使用的 tooparse JSON 文件，並在擷取 hello broker 主機資訊非常有用：</span><span class="sxs-lookup"><span data-stu-id="0e79f-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="0e79f-164">從 Ambari，下列命令使用 hello 擷取 tooset hello 環境變數的資訊：</span><span class="sxs-lookup"><span data-stu-id="0e79f-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0e79f-165">設定`CLUSTERNAME=`toohello hello Kafka 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="0e79f-166">設定`PASSWORD=`toohello （管理員） 登入密碼時建立 hello 叢集所使用。</span><span class="sxs-lookup"><span data-stu-id="0e79f-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="0e79f-167">hello 下列文字是 hello 內容的範例`$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="0e79f-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="0e79f-168">hello 下列文字是 hello 內容的範例`$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="0e79f-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="0e79f-169">hello`cut`命令是使用的 tootrim hello 份主機 tootwo 主機項目。</span><span class="sxs-lookup"><span data-stu-id="0e79f-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="0e79f-170">建立 Kafka 取用者或生產者時不需要主機 tooprovide hello 完整的清單。</span><span class="sxs-lookup"><span data-stu-id="0e79f-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="0e79f-171">請勿依賴 hello 資訊從這個工作階段傳回 tooalways 會精確。</span><span class="sxs-lookup"><span data-stu-id="0e79f-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="0e79f-172">如果您調整 hello 叢集時，新的代理程式加入或移除。</span><span class="sxs-lookup"><span data-stu-id="0e79f-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="0e79f-173">如果發生失敗且節點更換時，可能會變更 hello hello 節點的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="0e79f-174">使用具有有效的資訊 tooensure 的不久之前，您應該擷取 hello 動物園管理員和代理人主機資訊。</span><span class="sxs-lookup"><span data-stu-id="0e79f-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="0e79f-175">建立主題</span><span class="sxs-lookup"><span data-stu-id="0e79f-175">Create a topic</span></span>

<span data-ttu-id="0e79f-176">Kafka 會將資料串流儲存在名為 *topics* 的類別中。</span><span class="sxs-lookup"><span data-stu-id="0e79f-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="0e79f-177">SSH 連線 tooa 叢集前端節點，從使用 Kafka toocreate 主題所提供的指令碼：</span><span class="sxs-lookup"><span data-stu-id="0e79f-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="0e79f-178">此命令會連線使用 hello 主機資訊儲存在 tooZookeeper `$KAFKAZKHOSTS`，然後建立名為 Kafka 主題**測試**。</span><span class="sxs-lookup"><span data-stu-id="0e79f-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="0e79f-179">您可以確認該 hello 主題建立使用下列指令碼 toolist 主題 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="0e79f-180">hello 輸出此命令會列出 Kafka 主題，其中包含 hello**測試**主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="0e79f-181">產生和取用記錄</span><span class="sxs-lookup"><span data-stu-id="0e79f-181">Produce and consume records</span></span>

<span data-ttu-id="0e79f-182">Kafka 會在主題中儲存「記錄」。</span><span class="sxs-lookup"><span data-stu-id="0e79f-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="0e79f-183">記錄是由「產生者」產生，並由「取用者」取用。</span><span class="sxs-lookup"><span data-stu-id="0e79f-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="0e79f-184">產生者會從 Kafka「訊息代理程式」擷取記錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="0e79f-185">HDInsight 叢集中的每個背景工作節點都是 Kafka 訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="0e79f-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="0e79f-186">使用您先前建立並使用取用者讀取 hello 測試主題到下列步驟 toostore 記錄 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="0e79f-187">從 hello SSH 工作階段，使用 Kafka toowrite 記錄 toohello 主題所提供的指令碼：</span><span class="sxs-lookup"><span data-stu-id="0e79f-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="0e79f-188">您不會傳回 toohello 提示這個命令之後。</span><span class="sxs-lookup"><span data-stu-id="0e79f-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="0e79f-189">相反地，輸入一些文字訊息，然後使用**Ctrl + C** toostop 傳送 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="0e79f-190">每一行都會以個別的記錄傳送。</span><span class="sxs-lookup"><span data-stu-id="0e79f-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="0e79f-191">使用 Kafka tooread 記錄從 hello 主題所提供的指令碼：</span><span class="sxs-lookup"><span data-stu-id="0e79f-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="0e79f-192">此命令會擷取 hello 主題中的 hello 記錄，並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="0e79f-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="0e79f-193">使用`--from-beginning`hello 開頭 hello 資料流，從告訴 hello 消費者 toostart，因此會擷取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="0e79f-194">使用__Ctrl + C__ toostop hello 取用者。</span><span class="sxs-lookup"><span data-stu-id="0e79f-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="0e79f-195">產生者和取用者 API</span><span class="sxs-lookup"><span data-stu-id="0e79f-195">Producer and consumer API</span></span>

<span data-ttu-id="0e79f-196">您也以程式設計方式產生並使用記錄使用 hello [Kafka Api](http://kafka.apache.org/documentation#api)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="0e79f-197">toobuild Java 生產者和取用者，請使用下列步驟，從您的開發環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="0e79f-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e79f-198">您必須擁有下列元件安裝在您的開發環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="0e79f-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 或同等功能版本，例如 OpenJDK。</span><span class="sxs-lookup"><span data-stu-id="0e79f-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="0e79f-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="0e79f-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="0e79f-201">SSH 用戶端與 hello`scp`命令。</span><span class="sxs-lookup"><span data-stu-id="0e79f-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="0e79f-202">如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0e79f-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="0e79f-203">下載從 hello 範例[https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="0e79f-204">Hello 生產者/消費者使用範例的 hello 專案在 hello`Producer-Consumer`目錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="0e79f-205">這個範例包含下列類別的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="0e79f-206">**執行**-啟動 hello 取用者或產生者。</span><span class="sxs-lookup"><span data-stu-id="0e79f-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="0e79f-207">**生產者**-存放區 1,000,000 個記錄 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="0e79f-208">**取用者**-hello 主題會讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="0e79f-209">toocreate jar 封裝時，變更目錄 toohello 位置 hello`Producer-Consumer`目錄，並使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="0e79f-210">此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-producer-consumer-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0e79f-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="0e79f-211">使用 hello 下列命令 toocopy hello`kafka-producer-consumer-1.0-SNAPSHOT.jar`檔案 tooyour HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="0e79f-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="0e79f-212">取代**SSHUSER**與您的叢集，以及取代 hello SSH 使用者**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="0e79f-213">出現提示時輸入 hello SSH 使用者 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0e79f-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="0e79f-214">一次 hello`scp`命令完成複製 hello 檔案中，使用 SSH toohello 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="0e79f-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="0e79f-215">使用下列命令 toowrite 記錄 toohello 測試主題 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="0e79f-216">一旦完成 hello 程序，使用 hello 主題中的下列命令 tooread hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="0e79f-217">會顯示 hello 記錄讀取，以及記錄的計數。</span><span class="sxs-lookup"><span data-stu-id="0e79f-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="0e79f-218">您可能會看到幾個以上的 1000000 記錄，因為傳送數個記錄 toohello 主題在先前步驟中使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="0e79f-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="0e79f-219">使用__Ctrl + C__ tooexit hello 取用者。</span><span class="sxs-lookup"><span data-stu-id="0e79f-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="0e79f-220">多個取用者</span><span class="sxs-lookup"><span data-stu-id="0e79f-220">Multiple consumers</span></span>

<span data-ttu-id="0e79f-221">Kafka 取用者會在讀取記錄時使用取用者群組。</span><span class="sxs-lookup"><span data-stu-id="0e79f-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="0e79f-222">搭配多個取用者使用相同群組中的 hello 導致負載平衡主題的讀取次數。</span><span class="sxs-lookup"><span data-stu-id="0e79f-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="0e79f-223">Hello 群組中的每一個取用者會收到 hello 記錄的一部分。</span><span class="sxs-lookup"><span data-stu-id="0e79f-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="0e79f-224">toosee 在動作中，使用 hello 遵循此程序的步驟：</span><span class="sxs-lookup"><span data-stu-id="0e79f-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="0e79f-225">開啟新的 SSH 工作階段 toohello 叢集，讓您有兩個。</span><span class="sxs-lookup"><span data-stu-id="0e79f-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="0e79f-226">在每個工作階段中，使用 hello toostart 下列與取用者 hello 相同取用者群組識別碼：</span><span class="sxs-lookup"><span data-stu-id="0e79f-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="0e79f-227">此命令會啟動使用 hello 群組識別碼的消費者`mygroup`。</span><span class="sxs-lookup"><span data-stu-id="0e79f-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e79f-228">使用中 hello hello 指令[取得 hello 動物園管理員和代理人主機資訊](#getkafkainfo)區段 tooset`$KAFKABROKERS`此 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="0e79f-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="0e79f-229">觀看為在收到 hello 主題的每個工作階段計數 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="0e79f-230">兩個工作階段的 hello 總數應該 hello 相同一個取用者從先前接收。</span><span class="sxs-lookup"><span data-stu-id="0e79f-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="0e79f-231">用戶端 hello 相同的群組透過 hello 主題的 hello 資料分割內的耗用量。</span><span class="sxs-lookup"><span data-stu-id="0e79f-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="0e79f-232">Hello`test`稍早建立的主題有八個資料分割。</span><span class="sxs-lookup"><span data-stu-id="0e79f-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="0e79f-233">如果您開啟八個的 SSH 工作階段，並在所有工作階段中啟動取用者，每一個取用者會從 hello 主題的單一資料分割讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e79f-234">一個取用者群組中的取用者執行個體不得超過資料分割。</span><span class="sxs-lookup"><span data-stu-id="0e79f-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="0e79f-235">在此範例中，一個取用者群組可以包含總 tooeight 取用者，因為這是 hello hello 主題中的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="0e79f-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="0e79f-236">或者，您可以有多個取用者群組，其各有不超過 8 個取用者。</span><span class="sxs-lookup"><span data-stu-id="0e79f-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="0e79f-237">Kafka 中儲存的記錄會儲存在資料分割內收到 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="0e79f-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="0e79f-238">受 tooachieve 中排序的傳遞記錄*資料分割內*，建立取用者群組取用者執行個體的 hello 數目要比對資料分割的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="0e79f-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="0e79f-239">受 tooachieve 中排序的傳遞記錄*hello 主題內*，使用只有一個取用者執行個體建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="0e79f-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="0e79f-240">串流 API</span><span class="sxs-lookup"><span data-stu-id="0e79f-240">Streaming API</span></span>

<span data-ttu-id="0e79f-241">資料流 API hello 版已加入 tooKafka 在 0.10.0;舊版依賴 Apache Spark 或 Storm 進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="0e79f-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="0e79f-242">如果您尚未這樣做，請下載 hello 範例從[https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour 開發環境。</span><span class="sxs-lookup"><span data-stu-id="0e79f-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="0e79f-243">Hello 串流範例，請同時使用 hello 專案 hello`streaming`目錄。</span><span class="sxs-lookup"><span data-stu-id="0e79f-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="0e79f-244">此專案包含一個類別， `Stream`，記錄讀取從 hello`test`先前建立的主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="0e79f-245">它會計算 hello 字讀取，而發出名為每個 word 和計數 tooa 主題`wordcounts`。</span><span class="sxs-lookup"><span data-stu-id="0e79f-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="0e79f-246">hello`wordcounts`建立稍後的步驟，本節中的主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="0e79f-247">從開發環境中的 hello 命令列，變更目錄 toohello 位置 hello`Streaming`目錄，然後使用下列命令 toocreate jar 封裝的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="0e79f-248">此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-streaming-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0e79f-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="0e79f-249">使用 hello 下列命令 toocopy hello`kafka-streaming-1.0-SNAPSHOT.jar`檔案 tooyour HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="0e79f-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="0e79f-250">取代**SSHUSER**與您的叢集，以及取代 hello SSH 使用者**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e79f-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="0e79f-251">出現提示時輸入 hello SSH 使用者 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0e79f-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="0e79f-252">一次 hello`scp`命令完成 hello 檔案複製，toohello 叢集使用 SSH 連線，並接著使用下列命令 toocreate hello hello`wordcounts`主題：</span><span class="sxs-lookup"><span data-stu-id="0e79f-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="0e79f-253">接下來，啟動串流處理程序使用下列命令的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="0e79f-254">此命令啟動 hello 串流中 hello 背景處理程序。</span><span class="sxs-lookup"><span data-stu-id="0e79f-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="0e79f-255">使用 hello 下列命令 toosend 訊息 toohello`test`主題。</span><span class="sxs-lookup"><span data-stu-id="0e79f-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="0e79f-256">Hello 串流範例處理這些訊息：</span><span class="sxs-lookup"><span data-stu-id="0e79f-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="0e79f-257">使用下列命令 tooview hello 輸出寫入 toohello 的 hello `wordcounts` hello 串流處理程序的主題：</span><span class="sxs-lookup"><span data-stu-id="0e79f-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="0e79f-258">tooview hello 資料，您必須告訴 hello 消費者 tooprint hello 索引鍵和 hello 還原序列化程式 toouse hello 索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="0e79f-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="0e79f-259">hello 索引鍵名稱是 hello 單字，而 hello 索引鍵值包含 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="0e79f-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="0e79f-260">hello 輸出是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="0e79f-260">hello output is similar toohello following text:</span></span>
   
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
    > <span data-ttu-id="0e79f-261">hello 計數會遞增每次遇到一個字。</span><span class="sxs-lookup"><span data-stu-id="0e79f-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="0e79f-262">使用 hello __Ctrl + C__ tooexit hello 取用者，然後使用 hello `fg` toobring hello 串流處理的背景工作後 toohello 前景的命令。</span><span class="sxs-lookup"><span data-stu-id="0e79f-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="0e79f-263">使用__Ctrl + C__ tooexit 它也。</span><span class="sxs-lookup"><span data-stu-id="0e79f-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="0e79f-264">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="0e79f-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="0e79f-265">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0e79f-265">Troubleshoot</span></span>

<span data-ttu-id="0e79f-266">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e79f-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e79f-267">Next steps</span></span>

<span data-ttu-id="0e79f-268">在本文件中，您已經學會使用 Apache Kafka HDInsight 上的 hello 基本。</span><span class="sxs-lookup"><span data-stu-id="0e79f-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="0e79f-269">使用下列詳細資料使用 Kafka toolearn hello:</span><span class="sxs-lookup"><span data-stu-id="0e79f-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="0e79f-270">使用 HDInsight 上的 Kafka 確保您資料的高可用性</span><span class="sxs-lookup"><span data-stu-id="0e79f-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="0e79f-271">使用 HDInsight 上的 Kafka 設定受控磁碟來提高延展性</span><span class="sxs-lookup"><span data-stu-id="0e79f-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="0e79f-272">kafka.apache.org 上的 [Apache Kafka 文件](http://kafka.apache.org/documentation.html)。</span><span class="sxs-lookup"><span data-stu-id="0e79f-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="0e79f-273">在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本</span><span class="sxs-lookup"><span data-stu-id="0e79f-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="0e79f-274">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="0e79f-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="0e79f-275">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e79f-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="0e79f-276">透過 Azure 虛擬網路連線 tooKafka</span><span class="sxs-lookup"><span data-stu-id="0e79f-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
