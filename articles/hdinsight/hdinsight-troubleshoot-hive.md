---
title: "使用 Azure HDInsight 的 Hive aaaTroubleshoot |Microsoft 文件"
description: "取得解答 toocommon 疑問使用 Apache Hive 與 Azure HDInsight。"
keywords: "Azure HDInsight, Hive, 常見問題集, 疑難排解指南, 常見問題"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="0ec78-104">使用 Azure HDInsight 為 Hive 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0ec78-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="0ec78-105">Apache Hive 承載 Apache Ambari 中工作時，了解 hello 頂端的問題和其解決方式。</span><span class="sxs-lookup"><span data-stu-id="0ec78-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="0ec78-106">如何匯出 Hive 中繼存放區並匯入另一個叢集</span><span class="sxs-lookup"><span data-stu-id="0ec78-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="0ec78-107">解決步驟</span><span class="sxs-lookup"><span data-stu-id="0ec78-107">Resolution steps</span></span>

1. <span data-ttu-id="0ec78-108">使用安全殼層 (SSH) 用戶端連接 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0ec78-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="0ec78-109">如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。</span><span class="sxs-lookup"><span data-stu-id="0ec78-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="0ec78-110">執行下列命令，在要從中 tooexport hello 中繼存放區的 hello HDInsight 叢集上的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="0ec78-111">此命令會產生名為 allatables.sql 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0ec78-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="0ec78-112">複製 hello 檔案 alltables.sql toohello 新的 HDInsight 叢集，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="0ec78-113">hello hello 解決步驟中的程式碼會假設的資料 hello 新叢集的路徑，為 hello hello 舊叢集上的資料路徑 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="0ec78-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="0ec78-114">如果 hello 資料路徑不同，您可以手動編輯產生的 hello alltables.sql 檔案 tooreflect 的任何變更。</span><span class="sxs-lookup"><span data-stu-id="0ec78-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="0ec78-115">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-115">Additional reading</span></span>

- [<span data-ttu-id="0ec78-116">透過 SSH 連線 tooan HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="0ec78-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="0ec78-117">如何在叢集上尋找 Hive 記錄</span><span class="sxs-lookup"><span data-stu-id="0ec78-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0ec78-118">解決步驟</span><span class="sxs-lookup"><span data-stu-id="0ec78-118">Resolution steps</span></span>

1. <span data-ttu-id="0ec78-119">使用 SSH 連線 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0ec78-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="0ec78-120">如需詳細資訊，請參閱**其他閱讀資料**。</span><span class="sxs-lookup"><span data-stu-id="0ec78-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="0ec78-121">tooview Hive 用戶端記錄檔，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="0ec78-122">tooview Hive 中繼存放區記錄檔，會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="0ec78-123">tooview Hiveserver 記錄檔，會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="0ec78-124">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-124">Additional reading</span></span>

- [<span data-ttu-id="0ec78-125">透過 SSH 連線 tooan HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="0ec78-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="0ec78-126">我要如何啟動 hello 與叢集上的特定組態的登錄區殼層</span><span class="sxs-lookup"><span data-stu-id="0ec78-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0ec78-127">解決步驟</span><span class="sxs-lookup"><span data-stu-id="0ec78-127">Resolution steps</span></span>

1. <span data-ttu-id="0ec78-128">當您啟動 hello Hive 殼層，請指定組態機碼值組。</span><span class="sxs-lookup"><span data-stu-id="0ec78-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="0ec78-129">如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。</span><span class="sxs-lookup"><span data-stu-id="0ec78-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="0ec78-130">toolist Hive shell 之上，使用 hello 遵循所有有效的組態命令：</span><span class="sxs-lookup"><span data-stu-id="0ec78-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="0ec78-131">例如，使用偵錯記錄在 hello 主控台上啟用具備下列命令 toostart Hive 殼層 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="0ec78-132">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-132">Additional reading</span></span>

- [<span data-ttu-id="0ec78-133">Hive 設定屬性</span><span class="sxs-lookup"><span data-stu-id="0ec78-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="0ec78-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>如何分析叢集關鍵路徑上的 Tez DAG 資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="0ec78-135">解決步驟</span><span class="sxs-lookup"><span data-stu-id="0ec78-135">Resolution steps</span></span>
 
1. <span data-ttu-id="0ec78-136">tooanalyze Apache Tez 導向非循環圖 (DAG) 關鍵叢集的圖形上，透過 SSH 連線 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0ec78-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="0ec78-137">如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-end)。</span><span class="sxs-lookup"><span data-stu-id="0ec78-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="0ec78-138">在命令提示字元執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="0ec78-139">toolist 可以是使用的 tooanalyze Tez DAG 其他分析器使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="0ec78-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="0ec78-140">您必須提供範例程式為 hello 第一個引數。</span><span class="sxs-lookup"><span data-stu-id="0ec78-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="0ec78-141">有效的程式名稱包括：</span><span class="sxs-lookup"><span data-stu-id="0ec78-141">Valid program names include:</span></span>
    - <span data-ttu-id="0ec78-142">**ContainerReuseAnalyzer**：列印 DAG 中的容器重複使用詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="0ec78-143">**CriticalPath**： 尋找 DAG 的 hello 關鍵路徑</span><span class="sxs-lookup"><span data-stu-id="0ec78-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="0ec78-144">**LocalityAnalyzer**：列印 DAG 中的位置詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="0ec78-145">**ShuffleTimeAnalyzer**： 分析在 DAG 中的 hello 隨機播放時間詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="0ec78-146">**SkewAnalyzer**： 分析 DAG 中的 hello 誤差詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="0ec78-147">**SlowNodeAnalyzer**：列印 DAG 中的節點詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="0ec78-148">**SlowTaskIdentifier**：列印 DAG 中的低速工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="0ec78-149">**SlowestVertexAnalyzer**：列印 DAG 中最慢頂點詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="0ec78-150">**SpillAnalyzer**：列印 DAG 中的溢出詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="0ec78-151">**TaskConcurrencyAnalyzer**： 列印在 DAG 中的 hello 工作並行詳細資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="0ec78-152">**VertexLevelCriticalPathAnalyzer**： 尋找 hello 關鍵路徑中 DAG 的頂點層級</span><span class="sxs-lookup"><span data-stu-id="0ec78-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="0ec78-153">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-153">Additional reading</span></span>

- [<span data-ttu-id="0ec78-154">透過 SSH 連線 tooan HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="0ec78-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="0ec78-155">如何從叢集下載 Tez DAG 資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="0ec78-156">解決步驟</span><span class="sxs-lookup"><span data-stu-id="0ec78-156">Resolution steps</span></span>

<span data-ttu-id="0ec78-157">有兩種方式 toocollect hello Tez DAG 資料：</span><span class="sxs-lookup"><span data-stu-id="0ec78-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="0ec78-158">從 hello 命令列：</span><span class="sxs-lookup"><span data-stu-id="0ec78-158">From hello command line:</span></span>
 
    <span data-ttu-id="0ec78-159">使用 SSH 連線 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0ec78-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="0ec78-160">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ec78-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="0ec78-161">使用 hello Ambari Tez 檢視：</span><span class="sxs-lookup"><span data-stu-id="0ec78-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="0ec78-162">移 tooAmbari。</span><span class="sxs-lookup"><span data-stu-id="0ec78-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="0ec78-163">移 tooTez 檢視 （在 hello 右上角中的 hello 磚圖示）。</span><span class="sxs-lookup"><span data-stu-id="0ec78-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="0ec78-164">選取您想要 tooview DAG hello。</span><span class="sxs-lookup"><span data-stu-id="0ec78-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="0ec78-165">選取 [下載資料]。</span><span class="sxs-lookup"><span data-stu-id="0ec78-165">Select **Download data**.</span></span>

### <span data-ttu-id="0ec78-166"><a name="additional-reading-end"></a>其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="0ec78-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="0ec78-167">透過 SSH 連線 tooan HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="0ec78-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






