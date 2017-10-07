---
title: "在 HDInsight 中使用 aaaMonitor Hadoop 叢集 hello Ambari API-Azure |Microsoft 文件"
description: "用於建立、 管理和監視 Hadoop 叢集 hello Apache Ambari 應用程式開發介面。 運算子直覺式的工具和 Api 隱藏 hello 複雜度的 Hadoop。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="0929d-104">監視使用 hello Ambari API HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="0929d-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="0929d-105">了解使用 Ambari Api toomonitor HDInsight 叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="0929d-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="0929d-106">本文章中的 hello 資訊主要是 hello 的提供唯讀 Ambari REST API 版本的 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0929d-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="0929d-107">對於 Linux 架構的叢集，請參閱 [使用 Ambari 管理 Hadoop 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="0929d-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="0929d-108">什麼是 Ambari？</span><span class="sxs-lookup"><span data-stu-id="0929d-108">What is Ambari?</span></span>
<span data-ttu-id="0929d-109">[Apache Ambari][ambari-home] 用來佈建、管理和監視 Apache Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="0929d-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="0929d-110">它包含的運算子工具的直覺式集合和一組強大的應用程式開發介面中隱藏 hello 複雜度 Hadoop，以簡化 hello 作業的叢集。</span><span class="sxs-lookup"><span data-stu-id="0929d-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="0929d-111">如需 hello 應用程式開發介面的詳細資訊，請參閱[Ambari API 參考][ambari-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="0929d-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="0929d-112">HDInsight 目前支援僅 hello Ambari 監視功能。</span><span class="sxs-lookup"><span data-stu-id="0929d-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="0929d-113">HDInsight  3.0 及 2.1 版叢集可支援 Ambari API 1.0。</span><span class="sxs-lookup"><span data-stu-id="0929d-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="0929d-114">本文涵蓋於 HDInsight 3.1 和 2.1 版叢集上存取 Ambari API。</span><span class="sxs-lookup"><span data-stu-id="0929d-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="0929d-115">hello hello 兩個之間的主要差異是，某些 hello 元件已變更的新功能 （例如 hello 作業歷程記錄的伺服器) 的 hello 簡介。</span><span class="sxs-lookup"><span data-stu-id="0929d-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="0929d-116">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="0929d-116">**Prerequisites**</span></span>

<span data-ttu-id="0929d-117">開始本教學課程之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0929d-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="0929d-118">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="0929d-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="0929d-119">(選擇性) [cURL][curl]。</span><span class="sxs-lookup"><span data-stu-id="0929d-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="0929d-120">tooinstall，請參閱[cURL 版本和下載][curl-download]。</span><span class="sxs-lookup"><span data-stu-id="0929d-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0929d-121">何時使用 hello cURL 命令在 Windows 中，使用雙引號標記，而不是 hello 選項值的單一引號括起來。</span><span class="sxs-lookup"><span data-stu-id="0929d-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="0929d-122">**Azure HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="0929d-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="0929d-123">如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="0929d-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="0929d-124">您需要下列資料 toogo hello 教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="0929d-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="0929d-125">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="0929d-125">Cluster property</span></span> | <span data-ttu-id="0929d-126">Azure PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="0929d-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="0929d-127">值</span><span class="sxs-lookup"><span data-stu-id="0929d-127">Value</span></span> | <span data-ttu-id="0929d-128">說明</span><span class="sxs-lookup"><span data-stu-id="0929d-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="0929d-129">HDInsight 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="0929d-129">HDInsight cluster name</span></span> |<span data-ttu-id="0929d-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="0929d-130">$clusterName</span></span> | |<span data-ttu-id="0929d-131">hello 的 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="0929d-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="0929d-132">叢集使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0929d-132">Cluster username</span></span> |<span data-ttu-id="0929d-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="0929d-133">$clusterUsername</span></span> | |<span data-ttu-id="0929d-134">Hello 叢集建立時所指定叢集使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0929d-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="0929d-135">叢集密碼</span><span class="sxs-lookup"><span data-stu-id="0929d-135">Cluster password</span></span> |<span data-ttu-id="0929d-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="0929d-136">$clusterPassword</span></span> | |<span data-ttu-id="0929d-137">叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="0929d-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="0929d-138">開始使用</span><span class="sxs-lookup"><span data-stu-id="0929d-138">Jump-start</span></span>
<span data-ttu-id="0929d-139">有幾種方式 toouse Ambari toomonitor HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0929d-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="0929d-140">**使用 Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0929d-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="0929d-141">下列 Azure PowerShell 指令碼的 hello 取得 hello MapReduce 作業追蹤程式資訊*HDInsight 3.5 叢集中。*</span><span class="sxs-lookup"><span data-stu-id="0929d-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="0929d-142">hello 主要差異是我們提取從 hello YARN 服務 （而非 MapReduce） 這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0929d-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="0929d-143">下列 PowerShell 指令碼的 hello 取得 hello MapReduce 作業追蹤程式資訊*HDInsight 2.1 叢集中*:</span><span class="sxs-lookup"><span data-stu-id="0929d-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="0929d-144">hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="0929d-144">hello output is:</span></span>

![Jobtracker Output][img-jobtracker-output]

<span data-ttu-id="0929d-146">**使用 cURL**</span><span class="sxs-lookup"><span data-stu-id="0929d-146">**Use cURL**</span></span>

<span data-ttu-id="0929d-147">hello 下列範例會取得叢集資訊使用 cURL:</span><span class="sxs-lookup"><span data-stu-id="0929d-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="0929d-148">hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="0929d-148">hello output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="0929d-149">**Hello 2014 年 10 月 8 日發行的**:</span><span class="sxs-lookup"><span data-stu-id="0929d-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="0929d-150">當使用 hello Ambari 端點，「 https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}"，hello *host_name*欄位傳回 hello 節點，而不是 hello 主機名稱的 hello 完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="0929d-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="0929d-151">之前 hello 2014 年 10 月 8 日發行，此範例只是傳回"**headnode0**"。</span><span class="sxs-lookup"><span data-stu-id="0929d-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="0929d-152">之後 hello 2014 年 10 月 8 日版本中，您會收到 hello FQDN"**headnode0。 {ClusterDNS}.azurehdinsight.net**"，hello 先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="0929d-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="0929d-153">一個虛擬網路 (VNET) 中進行此變更，需要的 toofacilitate 案例可以部署多個叢集類型 （例如 HBase 和 Hadoop） 的位置。</span><span class="sxs-lookup"><span data-stu-id="0929d-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="0929d-154">例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。</span><span class="sxs-lookup"><span data-stu-id="0929d-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="0929d-155">Ambari 監視 API</span><span class="sxs-lookup"><span data-stu-id="0929d-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="0929d-156">hello 下表列出一些 hello 最常見 Ambari 監視 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="0929d-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="0929d-157">如需 hello API 的詳細資訊，請參閱[Ambari API 參考][ambari-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="0929d-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="0929d-158">監視 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="0929d-158">Monitor API call</span></span> | <span data-ttu-id="0929d-159">URI</span><span class="sxs-lookup"><span data-stu-id="0929d-159">URI</span></span> | <span data-ttu-id="0929d-160">說明</span><span class="sxs-lookup"><span data-stu-id="0929d-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0929d-161">取得叢集</span><span class="sxs-lookup"><span data-stu-id="0929d-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="0929d-162">取得叢集資訊。</span><span class="sxs-lookup"><span data-stu-id="0929d-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="0929d-163">叢集、服務、主機</span><span class="sxs-lookup"><span data-stu-id="0929d-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="0929d-164">取得服務</span><span class="sxs-lookup"><span data-stu-id="0929d-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="0929d-165">服務包括：hdfs、mapreduce</span><span class="sxs-lookup"><span data-stu-id="0929d-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="0929d-166">取得服務資訊</span><span class="sxs-lookup"><span data-stu-id="0929d-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="0929d-167">取得服務元件</span><span class="sxs-lookup"><span data-stu-id="0929d-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="0929d-168">HDFS：namenode、datanodeMapReduce：jobtracker；tasktracker</span><span class="sxs-lookup"><span data-stu-id="0929d-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="0929d-169">取得元件資訊</span><span class="sxs-lookup"><span data-stu-id="0929d-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="0929d-170">ServiceComponentInfo、主機元件、度量</span><span class="sxs-lookup"><span data-stu-id="0929d-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="0929d-171">取得主機</span><span class="sxs-lookup"><span data-stu-id="0929d-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="0929d-172">headnode0、workernode0</span><span class="sxs-lookup"><span data-stu-id="0929d-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="0929d-173">取得主機資訊</span><span class="sxs-lookup"><span data-stu-id="0929d-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="0929d-174">取得主機元件</span><span class="sxs-lookup"><span data-stu-id="0929d-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="0929d-175">namenode、resourcemanager</span><span class="sxs-lookup"><span data-stu-id="0929d-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="0929d-176">取得主機元件資訊</span><span class="sxs-lookup"><span data-stu-id="0929d-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="0929d-177">HostRoles、元件、主機、度量</span><span class="sxs-lookup"><span data-stu-id="0929d-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="0929d-178">取得組態</span><span class="sxs-lookup"><span data-stu-id="0929d-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="0929d-179">組態類型：core-site、hdfs-site、mapred-site、hive-site</span><span class="sxs-lookup"><span data-stu-id="0929d-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="0929d-180">取得組態資訊</span><span class="sxs-lookup"><span data-stu-id="0929d-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="0929d-181">組態類型：core-site、hdfs-site、mapred-site、hive-site</span><span class="sxs-lookup"><span data-stu-id="0929d-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0929d-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0929d-182">Next Steps</span></span>
<span data-ttu-id="0929d-183">現在您已經學會如何 toouse Ambari 監視應用程式開發介面呼叫。</span><span class="sxs-lookup"><span data-stu-id="0929d-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="0929d-184">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0929d-184">toolearn more, see:</span></span>

* <span data-ttu-id="0929d-185">[管理 HDInsight 叢集使用 hello Azure 入口網站][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0929d-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0929d-186">[使用 Azure PowerShell 管理 HDInsight 叢集][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="0929d-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="0929d-187">[使用命令列介面管理 HDInsight 叢集][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="0929d-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="0929d-188">[HDInsight 文件][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="0929d-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="0929d-189">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0929d-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
