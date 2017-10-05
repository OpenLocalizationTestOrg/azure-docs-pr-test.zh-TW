---
title: "使用 Ambari REST API 監視和管理 Hadoop - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Ambari 來監視和管理 Azure HDInsight 中的 Hadoop 叢集。 在本文件中，您將學習如何使用 HDInsight 叢集隨附的 Ambari REST API。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 7960d83bce22d4f671d61e9aaf55561bc24308f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-rest-api"></a><span data-ttu-id="f6e4c-104">使用 Ambari REST API 管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f6e4c-104">Manage HDInsight clusters by using the Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="f6e4c-105">了解如何使用 Ambari REST API 來管理和監視 Azure HDInsight 中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-105">Learn how to use the Ambari REST API to manage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="f6e4c-106">Apache Ambari 提供容易使用的 Web UI 和 REST API，可簡化 Hadoop 叢集的管理和監視。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-106">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="f6e4c-107">Ambari 會納入到使用 Linux 作業系統的 HDInsight 叢集中。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-107">Ambari is included on HDInsight clusters that use the Linux operating system.</span></span> <span data-ttu-id="f6e4c-108">您可以使用 Ambari 來監視叢集並進行設定變更。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-108">You can use Ambari to monitor the cluster and make configuration changes.</span></span>

## <span data-ttu-id="f6e4c-109"><a id="whatis"></a>什麼是 Ambari</span><span class="sxs-lookup"><span data-stu-id="f6e4c-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="f6e4c-110">[Apache Ambari](http://ambari.apache.org) 會提供 Web UI 以供用來佈建、管理及監視 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used to provision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="f6e4c-111">開發人員可以使用 [Ambari REST API](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)將這些功能整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="f6e4c-112">以 Linux 為基礎的 HDInsight 叢集預設會提供 Ambari。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-to-use-the-ambari-rest-api"></a><span data-ttu-id="f6e4c-113">如何使用 Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="f6e4c-113">How to use the Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-114">這份文件中的資訊和範例需要使用 Linux 作業系統的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-114">The information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="f6e4c-115">如需詳細資訊，請參閱[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="f6e4c-116">這份文件中的範例是針對 Bourne shell (bash) 和 PowerShell 提供。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-116">The examples in this document are provided for both the Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="f6e4c-117">bash 範例是以 GNU bash 4.3.11 進行測試，但是應該使用其他 Unix shell。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-117">The bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="f6e4c-118">PowerShell 範例是以 PowerShell 5.0 進行測試，但是應該使用 PowerShell 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-118">The PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="f6e4c-119">如果使用 __Bourne shell__ (Bash)，您必須安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-119">If using the __Bourne shell__ (Bash), you must have the following installed:</span></span>

* <span data-ttu-id="f6e4c-120">[cURL](http://curl.haxx.se/)：cURL 是公用程式，可以用來從命令列使用 REST API。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used to work with REST APIs from the command line.</span></span> <span data-ttu-id="f6e4c-121">在本文件中，它用來與 Ambari REST API 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-121">In this document, it is used to communicate with the Ambari REST API.</span></span>

<span data-ttu-id="f6e4c-122">無論是使用 Bash 或 PowerShell，您也必須安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="f6e4c-123">Jq 是用來使用 JSON 文件的公用程式。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="f6e4c-124">它用在**所有** Bash 範例中，以及**其中一個** PowerShell 範例中。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-124">It is used in **all** the Bash examples, and **one** of the PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="f6e4c-125">Ambari REST API 的基底 URI</span><span class="sxs-lookup"><span data-stu-id="f6e4c-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="f6e4c-126">HDInsight 上 Ambari REST API 的基底 URI 是 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME，其中 **CLUSTERNAME** 是叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-126">The base URI for the Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-127">URI (CLUSTERNAME.azurehdinsight.net) 完整網域名稱 (FQDN) 部分中的叢集名稱區分大小寫，URI 中的其他部分也區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-127">While the cluster name in the fully qualified domain name (FQDN) part of the URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in the URI are case-sensitive.</span></span> <span data-ttu-id="f6e4c-128">例如，如果您的叢集名稱為 `MyCluster`，有效的 URI 如下：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-128">For example, if your cluster is named `MyCluster`, the following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="f6e4c-129">下列 URI 會傳回錯誤，因為名稱的第二個項目不是正確的大小寫。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-129">The following URIs return an error because the second occurrence of the name is not the correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="f6e4c-130">驗證</span><span class="sxs-lookup"><span data-stu-id="f6e4c-130">Authentication</span></span>

<span data-ttu-id="f6e4c-131">連線到 HDInsight 上的 Ambari 需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-131">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="f6e4c-132">請使用您在叢集建立期間所提供的管理帳戶名稱 (預設值是 **admin**) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-132">Use the admin account name (the default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="f6e4c-133">範例︰驗證和剖析 JSON</span><span class="sxs-lookup"><span data-stu-id="f6e4c-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="f6e4c-134">下列範例示範如何針對基底 Ambari REST API 進行 GET 要求︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-134">The following examples demonstrate how to make a GET request against the base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-135">這份文件中的 Bash 範例進行下列假設︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-135">The Bash examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="f6e4c-136">叢集的登入名稱是 `admin` 的預設值。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-136">The login name for the cluster is the default value of `admin`.</span></span>
> * <span data-ttu-id="f6e4c-137">`$PASSWORD` 包含 HDInsight 登入命令的密碼。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-137">`$PASSWORD` contains the password for the HDInsight login command.</span></span> <span data-ttu-id="f6e4c-138">您可以藉由使用 `PASSWORD='mypassword'` 來設定此值。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="f6e4c-139">`$CLUSTERNAME` 包含叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-139">`$CLUSTERNAME` contains the name of the cluster.</span></span> <span data-ttu-id="f6e4c-140">您可以藉由使用 `set CLUSTERNAME='clustername'` 來設定此值</span><span class="sxs-lookup"><span data-stu-id="f6e4c-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-141">這份文件中的 PowerShell 範例進行下列假設︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-141">The PowerShell examples in this document make the following assumptions:</span></span>
>
> * <span data-ttu-id="f6e4c-142">`$creds` 是認證物件，包含叢集的系統管理員登入和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-142">`$creds` is a credential object that contains the admin login and password for the cluster.</span></span> <span data-ttu-id="f6e4c-143">您可以藉由使用 `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` 來設定此值，並且在系統提示時提供認證。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"` and providing the credentials when prompted.</span></span>
> * <span data-ttu-id="f6e4c-144">`$clusterName` 是字串，包含叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-144">`$clusterName` is a string that contains the name of the cluster.</span></span> <span data-ttu-id="f6e4c-145">您可以藉由使用 `$clusterName="clustername"` 來設定此值。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="f6e4c-146">兩個範例都會傳回開頭資訊類似下列內容的 JSON 文件︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-146">Both examples return a JSON document that begins with information similar to the following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="f6e4c-147">剖析 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="f6e4c-147">Parsing JSON data</span></span>

<span data-ttu-id="f6e4c-148">下列範例會使用 `jq` 來剖析 JSON 回應文件，並且只顯示結果的 `health_report` 資訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-148">The following example uses `jq` to parse the JSON response document and display only the `health_report` information from the results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="f6e4c-149">PowerShell 3.0 版和更新版本提供 `ConvertFrom-Json` Cmdlet，將 JSON 文件轉換成更容易從 PowerShell 使用的物件。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-149">PowerShell 3.0 and higher provides the `ConvertFrom-Json` cmdlet, which converts the JSON document into an object that is easier to work with from PowerShell.</span></span> <span data-ttu-id="f6e4c-150">下列範例會使用 `ConvertFrom-Json`，僅顯示結果的 `health_report` 資訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-150">The following example uses `ConvertFrom-Json` to display only the `health_report` information from the results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="f6e4c-151">雖然此文件的大多數範例使用 `ConvertFrom-Json` 來顯示回應文件的元素，而[更新 Ambari 組態](#example-update-ambari-configuration)範例會使用 jq。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-151">While most examples in this document use `ConvertFrom-Json` to display elements from the response document, the [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="f6e4c-152">此範例使用 jq，從 JSON 回應文件建構新的範本。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-152">Jq is used in this example to construct a new template from the JSON response document.</span></span>

<span data-ttu-id="f6e4c-153">如需 REST API 的完整參考，請參閱 [Ambari API 參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-153">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-the-fqdn-of-cluster-nodes"></a><span data-ttu-id="f6e4c-154">範例：取得叢集節點的 FQDN</span><span class="sxs-lookup"><span data-stu-id="f6e4c-154">Example: Get the FQDN of cluster nodes</span></span>

<span data-ttu-id="f6e4c-155">使用 HDInsight 時，您可能需要知道叢集節點的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-155">When working with HDInsight, you may need to know the fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="f6e4c-156">您可以使用下列範例，輕鬆地擷取叢集中不同節點的 FQDN：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-156">You can easily retrieve the FQDN for the various nodes in the cluster using the following examples:</span></span>

* <span data-ttu-id="f6e4c-157">**所有節點**</span><span class="sxs-lookup"><span data-stu-id="f6e4c-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="f6e4c-158">**前端節點**：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="f6e4c-159">**背景工作節點**</span><span class="sxs-lookup"><span data-stu-id="f6e4c-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="f6e4c-160">**Zookeeper 節點**</span><span class="sxs-lookup"><span data-stu-id="f6e4c-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-the-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="f6e4c-161">範例︰取得叢集節點的內部 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f6e4c-161">Example: Get the internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-162">本章節中的範例所傳回的 IP 位址無法直接透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-162">The IP addresses returned by the examples in this section are not directly accessible over the internet.</span></span> <span data-ttu-id="f6e4c-163">它們只能在包含 HDInsight 叢集的 Azure 虛擬網路內存取。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-163">They are only accessible within the Azure Virtual Network that contains the HDInsight cluster.</span></span>
>
> <span data-ttu-id="f6e4c-164">如需使用 HDInsight 和虛擬網路的詳細資訊，請參閱[使用自訂 Azure 虛擬網路擴充 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="f6e4c-165">若要尋找 IP 位址，您必須知道叢集節點的內部完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-165">To find the IP address, you must know the internal fully qualified domain name (FQDN) of the cluster nodes.</span></span> <span data-ttu-id="f6e4c-166">一旦您擁有 FQDN，就可以取得主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-166">Once you have the FQDN, you can then get the IP address of the host.</span></span> <span data-ttu-id="f6e4c-167">下列範例會先查詢所有主機節點之 FQDN 的 Ambari，然後查詢每部主機之 IP 位址的 Ambari。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-167">The following examples first query Ambari for the FQDN of all the host nodes, then query Ambari for the IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-the-default-storage"></a><span data-ttu-id="f6e4c-168">範例：取得預設儲存體</span><span class="sxs-lookup"><span data-stu-id="f6e4c-168">Example: Get the default storage</span></span>

<span data-ttu-id="f6e4c-169">建立 HDInsight 叢集時，您必須使用 Azure 儲存體帳戶或 Data Lake Store 做為叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as the default storage for the cluster.</span></span> <span data-ttu-id="f6e4c-170">在建立叢集之後，您可以使用 Ambari 來擷取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-170">You can use Ambari to retrieve this information after the cluster has been created.</span></span> <span data-ttu-id="f6e4c-171">例如，如果您想要讀取/寫入資料至 HDInsight 以外的容器。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-171">For example, if you want to read/write data to the container outside HDInsight.</span></span>

<span data-ttu-id="f6e4c-172">下列範例會從叢集擷取預設儲存體組態：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-172">The following examples retrieve the default storage configuration from the cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="f6e4c-173">這些範例會傳回套用至伺服器的第一個組態 (`service_config_version=1`)，其包含這項資訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-173">These examples return the first configuration applied to the server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="f6e4c-174">如果您擷取在叢集建立後已修改過的值，您可能需要列出組態版本並擷取最新的版本。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-174">If you retrieve a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="f6e4c-175">傳回值會類似下列其中一個範例︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-175">The return value is similar to one of the following examples:</span></span>

* <span data-ttu-id="f6e4c-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - 這個值表示叢集是使用 Azure 儲存體帳戶做為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that the cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="f6e4c-177">`ACCOUNTNAME` 值是儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-177">The `ACCOUNTNAME` value is the name of the storage account.</span></span> <span data-ttu-id="f6e4c-178">`CONTAINER` 部分是儲存體帳戶中 blob 容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-178">The `CONTAINER` portion is the name of the blob container in the storage account.</span></span> <span data-ttu-id="f6e4c-179">容器是叢集的 HDFS 相容儲存體的根目錄。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-179">The container is the root of the HDFS compatible storage for the cluster.</span></span>

* <span data-ttu-id="f6e4c-180">`adl://home` - 這個值表示叢集是使用 Azure Data Lake Store 做為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-180">`adl://home` - This value indicates that the cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="f6e4c-181">若要尋找 Data Lake Store 帳戶名稱，請使用下列範例︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-181">To find the Data Lake Store account name, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="f6e4c-182">傳回值類似 `ACCOUNTNAME.azuredatalakestore.net`，其中 `ACCOUNTNAME` 是 Data Lake Store 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-182">The return value is similar to `ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is the name of the Data Lake Store account.</span></span>

    <span data-ttu-id="f6e4c-183">若要尋找包含叢集儲存體的 Data Lake Store 內的目錄，請使用下列範例︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-183">To find the directory within Data Lake Store that contains the storage for the cluster, use the following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="f6e4c-184">傳回值類似 `/clusters/CLUSTERNAME/`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-184">The return value is similar to `/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="f6e4c-185">這個值是 Data Lake Store 帳戶內的路徑。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-185">This value is a path within the Data Lake Store account.</span></span> <span data-ttu-id="f6e4c-186">這個路徑是叢集的 HDFS 相容檔案系統的根目錄。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-186">This path is the root of the HDFS compatible file system for the cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6e4c-187">[Azure PowerShell](/powershell/azure/overview) 提供的 `Get-AzureRmHDInsightCluster` Cmdlet 也會傳回叢集的儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-187">The `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns the storage information for the cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="f6e4c-188">範例：取得組態</span><span class="sxs-lookup"><span data-stu-id="f6e4c-188">Example: Get configuration</span></span>

1. <span data-ttu-id="f6e4c-189">取得可供您的叢集使用的組態。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-189">Get the configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="f6e4c-190">此範例會傳回 JSON 文件，其中包含叢集上安裝之元件的目前組態 (由「tag」值識別)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-190">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="f6e4c-191">下列範例是從 Spark 叢集類型傳回之資料的摘要。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-191">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="f6e4c-192">取得您感興趣之元件的組態。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-192">Get the configuration for the component that you are interested in.</span></span> <span data-ttu-id="f6e4c-193">在下列範例中，以前一個要求傳回的標記值取代 `INITIAL`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-193">In the following example, replace `INITIAL` with the tag value returned from the previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="f6e4c-194">此範例會傳回 JSON 文件，其中包含 `core-site` 元件的目前組態。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-194">This example returns a JSON document containing the current configuration for the `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="f6e4c-195">範例︰更新組態</span><span class="sxs-lookup"><span data-stu-id="f6e4c-195">Example: Update configuration</span></span>

1. <span data-ttu-id="f6e4c-196">取得目前的組態，Ambari 會將其儲存為「所需的組態」:</span><span class="sxs-lookup"><span data-stu-id="f6e4c-196">Get the current configuration, which Ambari stores as the "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="f6e4c-197">此範例會傳回 JSON 文件，其中包含叢集上安裝之元件的目前組態 (由「tag」值識別)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-197">This example returns a JSON document containing the current configuration (identified by the *tag* value) for the components installed on the cluster.</span></span> <span data-ttu-id="f6e4c-198">下列範例是從 Spark 叢集類型傳回之資料的摘要。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-198">The following example is an excerpt from the data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="f6e4c-199">您需要從此清單中複製元件的名稱 (例如，**spark\_thrift\_sparkconf** 和 **tag** 值。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-199">From this list, you need to copy the name of the component (for example, **spark\_thrift\_sparkconf** and the **tag** value.</span></span>

2. <span data-ttu-id="f6e4c-200">使用下列命令以擷取元件和標記的組態：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-200">Retrieve the configuration for the component and tag by using the following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="f6e4c-201">將 **spark-thrift-sparkconf** 和 **INITIAL** 取代為您想要擷取其組態的元件和標籤。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-201">Replace **spark-thrift-sparkconf** and **INITIAL** with the component and tag that you want to retrieve the configuration for.</span></span>
   
    <span data-ttu-id="f6e4c-202">Jq 是用來將從 HDInsight 擷取到的資料轉換至新的組態範本。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-202">Jq is used to turn the data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="f6e4c-203">具體來說，這些範例會執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="f6e4c-203">Specifically, these examples perform the following actions:</span></span>
   
    * <span data-ttu-id="f6e4c-204">建立唯一的值，其中包含字串 "version" 和日期，會儲存在 `newtag`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-204">Creates a unique value containing the string "version" and the date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="f6e4c-205">建立新的所需組態的根文件。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-205">Creates a root document for the new desired configuration.</span></span>

    * <span data-ttu-id="f6e4c-206">取得 `.items[]` 陣列的內容，並且新增在 **desired_config** 元素下。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-206">Gets the contents of the `.items[]` array and adds it under the **desired_config** element.</span></span>

    * <span data-ttu-id="f6e4c-207">刪除 `href`、`version` 和 `Config` 元素，因為提交新組態時不需要這些元素。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-207">Deletes the `href`, `version`, and `Config` elements, as these elements aren't needed to submit a new configuration.</span></span>

    * <span data-ttu-id="f6e4c-208">使用 `version#################` 的值新增 `tag` 元素。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="f6e4c-209">數字部分是根據目前的日期。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-209">The numeric portion is based on the current date.</span></span> <span data-ttu-id="f6e4c-210">每個組態都必須有唯一的標記。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="f6e4c-211">最後，將資料儲存至 `newconfig.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-211">Finally, the data is saved to the `newconfig.json` document.</span></span> <span data-ttu-id="f6e4c-212">此文件結構應會顯示為類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-212">The document structure should appear similar to the following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="f6e4c-213">開啟 `newconfig.json` 文件，並且在 `properties` 物件中修改/新增值。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-213">Open the `newconfig.json` document and modify/add values in the `properties` object.</span></span> <span data-ttu-id="f6e4c-214">下列範例會將 `"spark.yarn.am.memory"`的值從 `"1g"`變更為 `"3g"`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-214">The following example changes the value of `"spark.yarn.am.memory"` from `"1g"` to `"3g"`.</span></span> <span data-ttu-id="f6e4c-215">它也會使用 `"256m"` 的值新增 `"spark.kryoserializer.buffer.max"`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="f6e4c-216">完成修改之後，請儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-216">Save the file once you are done making modifications.</span></span>

4. <span data-ttu-id="f6e4c-217">使用以下命令將更新的組態提交至 Ambari。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-217">Use the following commands to submit the updated configuration to Ambari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="f6e4c-218">這些命令會將 **newconfig.json** 檔案的內容提交至叢集，做為新的所需組態。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-218">These commands submit the contents of the **newconfig.json** file to the cluster as the new desired configuration.</span></span> <span data-ttu-id="f6e4c-219">要求會傳回 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-219">The request returns a JSON document.</span></span> <span data-ttu-id="f6e4c-220">這份文件中的 **versionTag** 元素應符合您所提交的版本，**configs** 物件將會包含您所要求的組態變更。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-220">The **versionTag** element in this document should match the version you submitted, and the **configs** object contains the configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="f6e4c-221">範例︰重新啟動服務元件</span><span class="sxs-lookup"><span data-stu-id="f6e4c-221">Example: Restart a service component</span></span>

<span data-ttu-id="f6e4c-222">此時，如果您看一下 Ambari Web UI，Spark 服務就會指出它需要重新啟動，新組態才會生效。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-222">At this point, if you look at the Ambari web UI, the Spark service indicates that it needs to be restarted before the new configuration can take effect.</span></span> <span data-ttu-id="f6e4c-223">使用下列步驟重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-223">Use the following steps to restart the service.</span></span>

1. <span data-ttu-id="f6e4c-224">使用以下命令以啟用 Spark 服務的維護模式：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-224">Use the following to enable maintenance mode for the Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="f6e4c-225">這些命令會將 JSON 文件傳送至伺服器，該伺服器以維護模式開啟。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-225">These commands send a JSON document to the server that turns on maintenance mode.</span></span> <span data-ttu-id="f6e4c-226">您可以使用下列要求驗證服務現在處於維護模式中：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-226">You can verify that the service is now in maintenance mode using the following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="f6e4c-227">傳回值是 `ON`。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-227">The return value is `ON`.</span></span>

2. <span data-ttu-id="f6e4c-228">接下來，使用下列命令來關閉服務：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-228">Next, use the following to turn off the service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="f6e4c-229">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-229">The response is similar to the following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="f6e4c-230">這個 URI 所傳回的 `href` 值會使用叢集節點的內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-230">The `href` value returned by this URI is using the internal IP address of the cluster node.</span></span> <span data-ttu-id="f6e4c-231">若要從叢集之外使用它，請將 '10.0.0.18:8080' 部分取代為叢集的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-231">To use it from outside the cluster, replace the \`10.0.0.18:8080' portion with the FQDN of the cluster.</span></span> 
    
    <span data-ttu-id="f6e4c-232">下列命令會擷取要求的狀態：</span><span class="sxs-lookup"><span data-stu-id="f6e4c-232">The following commands retrieve the status of the request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="f6e4c-233">`COMPLETED` 的回應表示要求已完成。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-233">A response of `COMPLETED` indicates that the request has finished.</span></span>

3. <span data-ttu-id="f6e4c-234">前一個要求完成後，使用以下命令來啟動服務。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-234">Once the previous request completes, use the following to start the service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="f6e4c-235">服務現在使用新的組態。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-235">The service is now using the new configuration.</span></span>

4. <span data-ttu-id="f6e4c-236">最後，使用以下命令來關閉維護模式。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-236">Finally, use the following to turn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="f6e4c-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6e4c-237">Next steps</span></span>

<span data-ttu-id="f6e4c-238">如需 REST API 的完整參考，請參閱 [Ambari API 參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="f6e4c-238">For a complete reference of the REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

