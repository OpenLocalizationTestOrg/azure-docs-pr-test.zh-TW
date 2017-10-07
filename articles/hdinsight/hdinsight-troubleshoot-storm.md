---
title: "使用 Azure HDInsight aaaTroubleshoot Storm |Microsoft 文件"
description: "取得有關 Azure HDInsight 搭配使用 Apache Storm 的 toocommon 問題的解答。"
keywords: "Azure HDInsight, Storm, 常見問題集, 疑難排解指南, 常見問題"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="1dc55-104">使用 Azure HDInsight 為 Storm 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1dc55-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="1dc55-105">了解 hello 最常發生的問題以及其使用中 Apache Ambari Apache Storm 承載的解析度。</span><span class="sxs-lookup"><span data-stu-id="1dc55-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="1dc55-106">如何存取在叢集上的 hello Storm UI</span><span class="sxs-lookup"><span data-stu-id="1dc55-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="1dc55-107">您有兩個選項可從瀏覽器存取 hello Storm UI:</span><span class="sxs-lookup"><span data-stu-id="1dc55-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="1dc55-108">Ambari UI</span><span class="sxs-lookup"><span data-stu-id="1dc55-108">Ambari UI</span></span>
1. <span data-ttu-id="1dc55-109">移 toohello Ambari 儀表板。</span><span class="sxs-lookup"><span data-stu-id="1dc55-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="1dc55-110">在 hello 服務清單中，選取  **Storm**。</span><span class="sxs-lookup"><span data-stu-id="1dc55-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="1dc55-111">在 hello**快速連結**功能表上，選取**Storm UI**。</span><span class="sxs-lookup"><span data-stu-id="1dc55-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="1dc55-112">直接連結</span><span class="sxs-lookup"><span data-stu-id="1dc55-112">Direct link</span></span>
<span data-ttu-id="1dc55-113">您可以存取下列 URL 的 hello 在 hello Storm UI:</span><span class="sxs-lookup"><span data-stu-id="1dc55-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="1dc55-114">https://\<叢集 DNS 名稱\>/stormui</span><span class="sxs-lookup"><span data-stu-id="1dc55-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="1dc55-115">範例：</span><span class="sxs-lookup"><span data-stu-id="1dc55-115">Example:</span></span>

 <span data-ttu-id="1dc55-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="1dc55-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="1dc55-117">如何在從一個拓撲 tooanother 轉移 Storm 事件中樞 spout 檢查點資訊</span><span class="sxs-lookup"><span data-stu-id="1dc55-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="1dc55-118">在開發時從 Azure 事件中心使用 hello HDInsight Storm 事件中樞 spout 檔案的讀取的拓撲，您必須部署有相同的名稱，在新叢集的 hello 的拓撲。</span><span class="sxs-lookup"><span data-stu-id="1dc55-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="1dc55-119">不過，您必須保留 hello 已認可的 tooApache 動物園管理員 hello 舊叢集上的檢查點資料。</span><span class="sxs-lookup"><span data-stu-id="1dc55-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="1dc55-120">檢查點資料的儲存位置</span><span class="sxs-lookup"><span data-stu-id="1dc55-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="1dc55-121">位移的檢查點資料會儲存 hello 事件中樞 spout 動物園管理員在兩個根路徑中：</span><span class="sxs-lookup"><span data-stu-id="1dc55-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="1dc55-122">非交易式 Spout 檢查點會儲存在 /eventhubspout 中。</span><span class="sxs-lookup"><span data-stu-id="1dc55-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="1dc55-123">交易式 Spout 檢查點資料會儲存在 /transactional 中。</span><span class="sxs-lookup"><span data-stu-id="1dc55-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="1dc55-124">如何 toorestore</span><span class="sxs-lookup"><span data-stu-id="1dc55-124">How toorestore</span></span>
<span data-ttu-id="1dc55-125">tooget hello 指令碼和程式庫使用 tooexport 動物園管理員中的資料，然後匯入 hello 資料回復 tooZooKeeper 以新名稱，請參閱[HDInsight Storm 範例](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0)。</span><span class="sxs-lookup"><span data-stu-id="1dc55-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="1dc55-126">hello lib 資料夾有包含 hello hello 匯出/匯入作業之實作的 d 檔案。</span><span class="sxs-lookup"><span data-stu-id="1dc55-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="1dc55-127">hello bash 資料夾已經示範如何從 tooexport 資料 hello 動物園管理員伺服器 hello 舊叢集上的範例指令碼，並將它匯入後 toohello 動物園管理員伺服器 hello 新叢集上。</span><span class="sxs-lookup"><span data-stu-id="1dc55-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="1dc55-128">執行 hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello 動物園管理員節點 tooexport 從指令碼，然後匯入資料。</span><span class="sxs-lookup"><span data-stu-id="1dc55-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="1dc55-129">更新 hello 指令碼 toohello 正確 Hortonworks Data Platform (HDP) 版本。</span><span class="sxs-lookup"><span data-stu-id="1dc55-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="1dc55-130">(我們正致力於讓這些指令碼在 HDInsight 中成為泛型。</span><span class="sxs-lookup"><span data-stu-id="1dc55-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="1dc55-131">泛型指令碼可以從任何節點上執行而不需修改 hello 使用者 hello 叢集。）</span><span class="sxs-lookup"><span data-stu-id="1dc55-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="1dc55-132">hello 匯出命令寫入 hello 中繼資料 tooan Apache Hadoop 分散式檔案系統 (HDFS) 路徑 （在 Azure Blob 儲存體或 Azure Data Lake Store 市集中） 在您設定的位置。</span><span class="sxs-lookup"><span data-stu-id="1dc55-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="1dc55-133">範例</span><span class="sxs-lookup"><span data-stu-id="1dc55-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="1dc55-134">匯出位移中繼資料</span><span class="sxs-lookup"><span data-stu-id="1dc55-134">Export offset metadata</span></span>
1. <span data-ttu-id="1dc55-135">從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。</span><span class="sxs-lookup"><span data-stu-id="1dc55-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="1dc55-136">Hello 執行的下列命令 （在您更新 HDP 版本字串 hello） 之後 tooexport 動物園管理員位移資料 toohello /stormmetadta/zkdata HDFS 路徑：</span><span class="sxs-lookup"><span data-stu-id="1dc55-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="1dc55-137">匯入位移中繼資料</span><span class="sxs-lookup"><span data-stu-id="1dc55-137">Import offset metadata</span></span>
1. <span data-ttu-id="1dc55-138">從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。</span><span class="sxs-lookup"><span data-stu-id="1dc55-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="1dc55-139">執行 hello 下列命令 （在您更新 hello HDP 版本字串） 之後 tooimport 動物園管理員位移 hello HDFS 路徑/stormmetadata/zkdata toohello 動物園管理員伺服器 hello 目標叢集上的資料：</span><span class="sxs-lookup"><span data-stu-id="1dc55-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="1dc55-140">刪除位移的中繼資料，以便拓撲可以開始處理 hello 開頭的資料，或該 hello 使用者選擇的時間戳記</span><span class="sxs-lookup"><span data-stu-id="1dc55-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="1dc55-141">從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。</span><span class="sxs-lookup"><span data-stu-id="1dc55-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="1dc55-142">執行 hello 下列命令 （在您更新 hello HDP 版本字串） 之後所有 toodelete 動物園管理員位移 hello 目前叢集中的資料：</span><span class="sxs-lookup"><span data-stu-id="1dc55-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="1dc55-143">如何找出叢集上的 Storm 二進位檔</span><span class="sxs-lookup"><span data-stu-id="1dc55-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="1dc55-144">Hello 目前 HDP 堆疊的 storm 二進位檔位於 /usr/hdp/current/storm-client。</span><span class="sxs-lookup"><span data-stu-id="1dc55-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="1dc55-145">hello 位置是 hello 相同的前端節點和背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="1dc55-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="1dc55-146">/usr/hdp 中可能會有特定 HDP 版本的多個二進位檔 (例如 /usr/hdp/2.5.0.1233/storm)。</span><span class="sxs-lookup"><span data-stu-id="1dc55-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="1dc55-147">hello /usr/hdp/current/storm-client 資料夾是 symlinked toohello 最新版本 hello 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="1dc55-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="1dc55-148">如需詳細資訊，請參閱[使用 SSH 連線 tooan HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)和[Storm](http://storm.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="1dc55-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="1dc55-149">我要如何判斷 hello Storm 叢集部署拓撲</span><span class="sxs-lookup"><span data-stu-id="1dc55-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="1dc55-150">首先，找出所有與 HDInsight Storm 一起安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="1dc55-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="1dc55-151">Storm 叢集包含四個節點類別：</span><span class="sxs-lookup"><span data-stu-id="1dc55-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="1dc55-152">閘道節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-152">Gateway nodes</span></span>
* <span data-ttu-id="1dc55-153">前端節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-153">Head nodes</span></span>
* <span data-ttu-id="1dc55-154">ZooKeeper 節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="1dc55-155">背景工作節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="1dc55-156">閘道節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-156">Gateway nodes</span></span>
<span data-ttu-id="1dc55-157">閘道節點是閘道和反向 proxy 服務，可讓公用存取 tooan active Ambari 管理服務。</span><span class="sxs-lookup"><span data-stu-id="1dc55-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="1dc55-158">它也可以處理 Ambari 前置選擇。</span><span class="sxs-lookup"><span data-stu-id="1dc55-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="1dc55-159">前端節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-159">Head nodes</span></span>
<span data-ttu-id="1dc55-160">Storm 前端節點執行下列服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc55-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="1dc55-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="1dc55-161">Nimbus</span></span>
* <span data-ttu-id="1dc55-162">Ambari 伺服器</span><span class="sxs-lookup"><span data-stu-id="1dc55-162">Ambari server</span></span>
* <span data-ttu-id="1dc55-163">Ambari 計量伺服器</span><span class="sxs-lookup"><span data-stu-id="1dc55-163">Ambari Metrics server</span></span>
* <span data-ttu-id="1dc55-164">Ambari 計量收集器</span><span class="sxs-lookup"><span data-stu-id="1dc55-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="1dc55-165">ZooKeeper 節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-165">ZooKeeper nodes</span></span>
<span data-ttu-id="1dc55-166">HDInsight 隨附一個三節點的 ZooKeeper 仲裁。</span><span class="sxs-lookup"><span data-stu-id="1dc55-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="1dc55-167">hello 仲裁大小固定，且無法重新設定。</span><span class="sxs-lookup"><span data-stu-id="1dc55-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="1dc55-168">Hello 叢集中的 storm 服務是設定的 tooautomatically 使用 hello 動物園管理員仲裁。</span><span class="sxs-lookup"><span data-stu-id="1dc55-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="1dc55-169">背景工作節點</span><span class="sxs-lookup"><span data-stu-id="1dc55-169">Worker nodes</span></span>
<span data-ttu-id="1dc55-170">Storm 背景工作節點執行下列服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc55-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="1dc55-171">監督員</span><span class="sxs-lookup"><span data-stu-id="1dc55-171">Supervisor</span></span>
* <span data-ttu-id="1dc55-172">背景工作 Java 虛擬機器 (JVM)，用於執行拓樸</span><span class="sxs-lookup"><span data-stu-id="1dc55-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="1dc55-173">Ambari 代理程式</span><span class="sxs-lookup"><span data-stu-id="1dc55-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="1dc55-174">如何找出用於開發的 Storm 事件中樞 Spout 二進位檔</span><span class="sxs-lookup"><span data-stu-id="1dc55-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="1dc55-175">如需搭配使用 Storm 事件中樞 spout d 檔案與您的拓撲的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="1dc55-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="1dc55-176">Java 型拓撲</span><span class="sxs-lookup"><span data-stu-id="1dc55-176">Java-based topology</span></span>
[<span data-ttu-id="1dc55-177">使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)</span><span class="sxs-lookup"><span data-stu-id="1dc55-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="1dc55-178">C# 型拓撲 (HDInsight 3.4+ Linux Storm 叢集上的 Mono)</span><span class="sxs-lookup"><span data-stu-id="1dc55-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="1dc55-179">利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)</span><span class="sxs-lookup"><span data-stu-id="1dc55-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="1dc55-180">適用於 HDInsight 3.5+ Linux Storm 叢集的最新 Storm 事件中樞 Spout 二進位檔</span><span class="sxs-lookup"><span data-stu-id="1dc55-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="1dc55-181">toolearn 如何 toouse hello 最新出現事件中樞 spout HDInsight 3.5 + 適用於 Linux Storm 叢集，請參閱 hello mvn 儲存機制[讀我檔案](https://github.com/hdinsight/mvn-repo/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc55-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="1dc55-182">原始程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1dc55-182">Source code examples</span></span>
<span data-ttu-id="1dc55-183">請參閱[範例](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)方式的 tooread 從 Azure 事件中心的 Azure HDInsight 叢集上使用 （以 Java 撰寫的） Apache Storm 拓樸和寫入。</span><span class="sxs-lookup"><span data-stu-id="1dc55-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="1dc55-184">如何找出叢集上的 Storm Log4J 設定檔</span><span class="sxs-lookup"><span data-stu-id="1dc55-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="1dc55-185">tooidentify Apache Log4J Storm 服務的組態檔。</span><span class="sxs-lookup"><span data-stu-id="1dc55-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="1dc55-186">在前端節點上</span><span class="sxs-lookup"><span data-stu-id="1dc55-186">On head nodes</span></span>
<span data-ttu-id="1dc55-187">讀取 hello Nimbus Log4J 組態 libodbc/hdp/\<HDP 版本\>/storm/log4j2/cluster.xml。</span><span class="sxs-lookup"><span data-stu-id="1dc55-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="1dc55-188">在背景工作節點上</span><span class="sxs-lookup"><span data-stu-id="1dc55-188">On worker nodes</span></span>
<span data-ttu-id="1dc55-189">讀取 hello 監督員 Log4J 組態 libodbc/hdp/\<HDP 版本\>/storm/log4j2/cluster.xml。</span><span class="sxs-lookup"><span data-stu-id="1dc55-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="1dc55-190">讀取 hello 工作者 Log4J 組態檔 libodbc/hdp/\<HDP 版本\>/storm/log4j2/worker.xml。</span><span class="sxs-lookup"><span data-stu-id="1dc55-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="1dc55-191">範例：/usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="1dc55-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

