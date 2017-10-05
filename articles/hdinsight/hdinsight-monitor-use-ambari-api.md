---
title: "使用 Ambari API 監視 HDInsight 中的 Hadoop 叢集 - Azure | Microsoft Docs"
description: "使用 Apache Ambari API 來建立、管理和監視 Hadoop 叢集。 直覺式操作工具和 API 可消除 Hadoop 的複雜性。"
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
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="f89d7-104">使用 Ambari API 監視 HDInsight 上的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="f89d7-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="f89d7-105">了解如何使用 Ambari API 監視 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f89d7-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="f89d7-106">本文中的資訊主要適用於 Windows 架構的 HDInsight 叢集，該叢集提供 Ambari REST API 的唯讀版本。</span><span class="sxs-lookup"><span data-stu-id="f89d7-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="f89d7-107">對於 Linux 架構的叢集，請參閱 [使用 Ambari 管理 Hadoop 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="f89d7-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="f89d7-108">什麼是 Ambari？</span><span class="sxs-lookup"><span data-stu-id="f89d7-108">What is Ambari?</span></span>
<span data-ttu-id="f89d7-109">[Apache Ambari][ambari-home] 用來佈建、管理和監視 Apache Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f89d7-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="f89d7-110">其中包含一組直接易懂的操作員工具和健全的 API 集，可消除 Hadoop 的複雜性，並簡化叢集作業。</span><span class="sxs-lookup"><span data-stu-id="f89d7-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="f89d7-111">如需關於 API 的詳細資訊，請參閱 [Ambari API 參考資料][ambari-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="f89d7-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="f89d7-112">HDInsight 目前僅支援 Ambari 監視功能。</span><span class="sxs-lookup"><span data-stu-id="f89d7-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="f89d7-113">HDInsight  3.0 及 2.1 版叢集可支援 Ambari API 1.0。</span><span class="sxs-lookup"><span data-stu-id="f89d7-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="f89d7-114">本文涵蓋於 HDInsight 3.1 和 2.1 版叢集上存取 Ambari API。</span><span class="sxs-lookup"><span data-stu-id="f89d7-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="f89d7-115">兩者的主要差別在於某些元件已隨著新功能引進而變更 (例如工作歷程伺服器)。</span><span class="sxs-lookup"><span data-stu-id="f89d7-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="f89d7-116">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="f89d7-116">**Prerequisites**</span></span>

<span data-ttu-id="f89d7-117">開始進行本教學課程之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="f89d7-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="f89d7-118">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="f89d7-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="f89d7-119">(選擇性) [cURL][curl]。</span><span class="sxs-lookup"><span data-stu-id="f89d7-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="f89d7-120">若要安裝此項目，請參閱 [cURL 版本和下載][curl-download]。</span><span class="sxs-lookup"><span data-stu-id="f89d7-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f89d7-121">在 Windows 上使用 cURL 命令時，請針對選項值使用雙引號，而不要使用單引號。</span><span class="sxs-lookup"><span data-stu-id="f89d7-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="f89d7-122">**Azure HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f89d7-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="f89d7-123">如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="f89d7-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="f89d7-124">進行教學課程時，您將需要以下資料：</span><span class="sxs-lookup"><span data-stu-id="f89d7-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="f89d7-125">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="f89d7-125">Cluster property</span></span> | <span data-ttu-id="f89d7-126">Azure PowerShell 變數名稱</span><span class="sxs-lookup"><span data-stu-id="f89d7-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="f89d7-127">值</span><span class="sxs-lookup"><span data-stu-id="f89d7-127">Value</span></span> | <span data-ttu-id="f89d7-128">說明</span><span class="sxs-lookup"><span data-stu-id="f89d7-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="f89d7-129">HDInsight 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="f89d7-129">HDInsight cluster name</span></span> |<span data-ttu-id="f89d7-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="f89d7-130">$clusterName</span></span> | |<span data-ttu-id="f89d7-131">您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="f89d7-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="f89d7-132">叢集使用者名稱</span><span class="sxs-lookup"><span data-stu-id="f89d7-132">Cluster username</span></span> |<span data-ttu-id="f89d7-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="f89d7-133">$clusterUsername</span></span> | |<span data-ttu-id="f89d7-134">建立叢集時指定的叢集使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f89d7-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="f89d7-135">叢集密碼</span><span class="sxs-lookup"><span data-stu-id="f89d7-135">Cluster password</span></span> |<span data-ttu-id="f89d7-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="f89d7-136">$clusterPassword</span></span> | |<span data-ttu-id="f89d7-137">叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="f89d7-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="f89d7-138">開始使用</span><span class="sxs-lookup"><span data-stu-id="f89d7-138">Jump-start</span></span>
<span data-ttu-id="f89d7-139">您可以透過數種方式使用 Ambari 監視 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f89d7-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="f89d7-140">**使用 Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f89d7-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="f89d7-141">以下 Azure PowerShell 指令碼可取得 *HDInsight 3.5 叢集*中的MapReduce 工作追蹤程式資訊。</span><span class="sxs-lookup"><span data-stu-id="f89d7-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="f89d7-142">主要差別在於我們從 YARN 服務 (而非 MapReduce) 提取這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f89d7-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="f89d7-143">以下 PowerShell 指令碼可取得「HDInsight 2.1 叢集中的」MapReduce 工作追蹤程式資訊：</span><span class="sxs-lookup"><span data-stu-id="f89d7-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="f89d7-144">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f89d7-144">The output is:</span></span>

![Jobtracker Output][img-jobtracker-output]

<span data-ttu-id="f89d7-146">**使用 cURL**</span><span class="sxs-lookup"><span data-stu-id="f89d7-146">**Use cURL**</span></span>

<span data-ttu-id="f89d7-147">以下範例使用 cURL 取得叢集資訊：</span><span class="sxs-lookup"><span data-stu-id="f89d7-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="f89d7-148">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f89d7-148">The output is:</span></span>

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

<span data-ttu-id="f89d7-149">**2014/10/8 版本的相關資訊**：</span><span class="sxs-lookup"><span data-stu-id="f89d7-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="f89d7-150">使用 Ambari 端點 "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" 時，host_name 欄位會傳回節點的完整網域名稱 (FQDN)，而不是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="f89d7-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="f89d7-151">在 2014/10/8 版本之前，此範例只會傳回 "**headnode0**"。</span><span class="sxs-lookup"><span data-stu-id="f89d7-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="f89d7-152">在 2014/10/8 版本之後，您會得到 FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**"，如先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="f89d7-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="f89d7-153">需要此變更，以便將多種叢集類型 (例如 HBase 和 Hadoop) 部屬至一個虛擬網路 (VNET) 中。</span><span class="sxs-lookup"><span data-stu-id="f89d7-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="f89d7-154">例如，使用 HBase 做為 Hadoop 的後端平台時就是這種情形。</span><span class="sxs-lookup"><span data-stu-id="f89d7-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="f89d7-155">Ambari 監視 API</span><span class="sxs-lookup"><span data-stu-id="f89d7-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="f89d7-156">下表列出部分最常用的 Ambari 監視 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f89d7-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="f89d7-157">如需 API 的詳細資訊，請參閱 [Ambari API 參考資料][ambari-api-reference]。</span><span class="sxs-lookup"><span data-stu-id="f89d7-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="f89d7-158">監視 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="f89d7-158">Monitor API call</span></span> | <span data-ttu-id="f89d7-159">URI</span><span class="sxs-lookup"><span data-stu-id="f89d7-159">URI</span></span> | <span data-ttu-id="f89d7-160">說明</span><span class="sxs-lookup"><span data-stu-id="f89d7-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f89d7-161">取得叢集</span><span class="sxs-lookup"><span data-stu-id="f89d7-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="f89d7-162">取得叢集資訊。</span><span class="sxs-lookup"><span data-stu-id="f89d7-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="f89d7-163">叢集、服務、主機</span><span class="sxs-lookup"><span data-stu-id="f89d7-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="f89d7-164">取得服務</span><span class="sxs-lookup"><span data-stu-id="f89d7-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="f89d7-165">服務包括：hdfs、mapreduce</span><span class="sxs-lookup"><span data-stu-id="f89d7-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="f89d7-166">取得服務資訊</span><span class="sxs-lookup"><span data-stu-id="f89d7-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="f89d7-167">取得服務元件</span><span class="sxs-lookup"><span data-stu-id="f89d7-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="f89d7-168">HDFS：namenode、datanodeMapReduce：jobtracker；tasktracker</span><span class="sxs-lookup"><span data-stu-id="f89d7-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="f89d7-169">取得元件資訊</span><span class="sxs-lookup"><span data-stu-id="f89d7-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="f89d7-170">ServiceComponentInfo、主機元件、度量</span><span class="sxs-lookup"><span data-stu-id="f89d7-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="f89d7-171">取得主機</span><span class="sxs-lookup"><span data-stu-id="f89d7-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="f89d7-172">headnode0、workernode0</span><span class="sxs-lookup"><span data-stu-id="f89d7-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="f89d7-173">取得主機資訊</span><span class="sxs-lookup"><span data-stu-id="f89d7-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="f89d7-174">取得主機元件</span><span class="sxs-lookup"><span data-stu-id="f89d7-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="f89d7-175">namenode、resourcemanager</span><span class="sxs-lookup"><span data-stu-id="f89d7-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="f89d7-176">取得主機元件資訊</span><span class="sxs-lookup"><span data-stu-id="f89d7-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="f89d7-177">HostRoles、元件、主機、度量</span><span class="sxs-lookup"><span data-stu-id="f89d7-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="f89d7-178">取得組態</span><span class="sxs-lookup"><span data-stu-id="f89d7-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="f89d7-179">組態類型：core-site、hdfs-site、mapred-site、hive-site</span><span class="sxs-lookup"><span data-stu-id="f89d7-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="f89d7-180">取得組態資訊</span><span class="sxs-lookup"><span data-stu-id="f89d7-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="f89d7-181">組態類型：core-site、hdfs-site、mapred-site、hive-site</span><span class="sxs-lookup"><span data-stu-id="f89d7-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f89d7-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f89d7-182">Next Steps</span></span>
<span data-ttu-id="f89d7-183">現在，您已了解如何使用 Ambari 監視 API。</span><span class="sxs-lookup"><span data-stu-id="f89d7-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="f89d7-184">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f89d7-184">To learn more, see:</span></span>

* <span data-ttu-id="f89d7-185">[使用 Azure 入口網站管理 HDInsight 叢集][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="f89d7-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="f89d7-186">[使用 Azure PowerShell 管理 HDInsight 叢集][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="f89d7-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="f89d7-187">[使用命令列介面管理 HDInsight 叢集][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="f89d7-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="f89d7-188">[HDInsight 文件][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="f89d7-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="f89d7-189">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f89d7-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
