---
title: "aaaMonitor 和管理與 Ambari REST API Azure HDInsight Hadoop |Microsoft 文件"
description: "深入了解如何 toouse Ambari toomonitor 和管理 Azure HDInsight 中的 Hadoop 叢集。 在本文件中，您將學習如何 toouse hello Ambari REST API 包含與 HDInsight 叢集。"
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
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="4f679-104">使用 hello Ambari REST API 來管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="4f679-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="4f679-105">了解如何 toouse hello Ambari REST API toomanage 和監視 Azure HDInsight 中的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="4f679-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="4f679-106">Apache Ambari 簡化 hello 的管理和監視 Hadoop 叢集藉由提供簡單 toouse web UI 和 REST API。</span><span class="sxs-lookup"><span data-stu-id="4f679-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="4f679-107">Ambari 包含在使用 hello Linux 作業系統的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="4f679-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="4f679-108">您可以使用 Ambari toomonitor hello 叢集，並進行組態變更。</span><span class="sxs-lookup"><span data-stu-id="4f679-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="4f679-109"><a id="whatis"></a>什麼是 Ambari</span><span class="sxs-lookup"><span data-stu-id="4f679-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="4f679-110">[Apache Ambari](http://ambari.apache.org)提供 web UI，它可以是使用的 tooprovision、 管理及監視 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="4f679-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="4f679-111">開發人員可以這些功能整合到應用程式使用 hello [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4f679-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="4f679-112">以 Linux 為基礎的 HDInsight 叢集預設會提供 Ambari。</span><span class="sxs-lookup"><span data-stu-id="4f679-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="4f679-113">如何 toouse hello Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="4f679-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f679-114">hello 資訊與本文件中的範例需要使用 Linux 作業系統的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4f679-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="4f679-115">如需詳細資訊，請參閱[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4f679-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="4f679-116">這份文件中的 hello 範例提供 hello 信瑜殼層 (bash) 和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4f679-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="4f679-117">範例測試與 GNU hello bash 撞 4.3.11，但應搭配其他 Unix 殼層。</span><span class="sxs-lookup"><span data-stu-id="4f679-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="4f679-118">hello PowerShell 範例與 PowerShell 5.0 中測試，但應該使用 PowerShell 3.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4f679-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="4f679-119">如果使用 hello__信瑜殼層__(Bash)，您必須擁有 hello 安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="4f679-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="4f679-120">[cURL](http://curl.haxx.se/): cURL 是可以使用 REST Api 的使用的 toowork 從 hello 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="4f679-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="4f679-121">在本文件中，會使用的 toocommunicate 以 hello Ambari REST API。</span><span class="sxs-lookup"><span data-stu-id="4f679-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="4f679-122">無論是使用 Bash 或 PowerShell，您也必須安裝 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="4f679-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="4f679-123">Jq 是用來使用 JSON 文件的公用程式。</span><span class="sxs-lookup"><span data-stu-id="4f679-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="4f679-124">它用於**所有**hello Bash 範例和**一個**的 hello PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="4f679-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="4f679-125">Ambari REST API 的基底 URI</span><span class="sxs-lookup"><span data-stu-id="4f679-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="4f679-126">hello hello Ambari REST API，在 HDInsight 上的基底 URI 是 https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME，其中**CLUSTERNAME**是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4f679-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f679-127">雖然在 hello hello 叢集名稱完整限定 hello URI (CLUSTERNAME.azurehdinsight.net) 網域名稱 (FQDN) 部分不區分大小寫，出現在其他位置中 hello URI 有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4f679-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="4f679-128">例如，如果您的叢集的名稱為`MyCluster`，hello 下列是有效的 Uri:</span><span class="sxs-lookup"><span data-stu-id="4f679-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="4f679-129">hello 下列 Uri 會傳回錯誤，因為不是 hello hello hello 名稱的第二次出現修正案例。</span><span class="sxs-lookup"><span data-stu-id="4f679-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="4f679-130">驗證</span><span class="sxs-lookup"><span data-stu-id="4f679-130">Authentication</span></span>

<span data-ttu-id="4f679-131">連接 tooAmbari HDInsight 上的需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4f679-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="4f679-132">使用 hello 管理帳戶的名稱 (hello 預設值是**admin**) 和您在叢集建立期間所提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="4f679-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="4f679-133">範例︰驗證和剖析 JSON</span><span class="sxs-lookup"><span data-stu-id="4f679-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="4f679-134">hello 遵循範例示範如何針對 hello GET 要求 toomake 基底 Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="4f679-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="4f679-135">本文件中的 hello Bash 範例進行下列假設 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="4f679-136">hello 叢集 hello 登入名稱是 hello 預設值是`admin`。</span><span class="sxs-lookup"><span data-stu-id="4f679-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="4f679-137">`$PASSWORD`包含 hello 密碼 hello HDInsight 登入的命令。</span><span class="sxs-lookup"><span data-stu-id="4f679-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="4f679-138">您可以藉由使用 `PASSWORD='mypassword'` 來設定此值。</span><span class="sxs-lookup"><span data-stu-id="4f679-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="4f679-139">`$CLUSTERNAME`包含 hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4f679-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="4f679-140">您可以藉由使用 `set CLUSTERNAME='clustername'` 來設定此值</span><span class="sxs-lookup"><span data-stu-id="4f679-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="4f679-141">本文件中的 hello PowerShell 範例進行下列假設 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="4f679-142">`$creds`是包含 hello 系統管理員登入和密碼 hello 叢集的認證物件。</span><span class="sxs-lookup"><span data-stu-id="4f679-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="4f679-143">您可以使用來設定此值`$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"`提供 hello 提示的認證。</span><span class="sxs-lookup"><span data-stu-id="4f679-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="4f679-144">`$clusterName`是包含 hello hello 叢集名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="4f679-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="4f679-145">您可以藉由使用 `$clusterName="clustername"` 來設定此值。</span><span class="sxs-lookup"><span data-stu-id="4f679-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="4f679-146">這兩個範例會傳回開頭為下列範例的資訊類似 toohello 的 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="4f679-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="4f679-147">剖析 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="4f679-147">Parsing JSON data</span></span>

<span data-ttu-id="4f679-148">hello 下列範例會使用`jq`tooparse hello JSON 回應文件，並顯示只有 hello `health_report` hello 結果中的資訊。</span><span class="sxs-lookup"><span data-stu-id="4f679-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="4f679-149">PowerShell 3.0 和更新版本提供 hello `ConvertFrom-Json` cmdlet，將 hello JSON 文件轉換成更容易 toowork 與從 PowerShell 的物件。</span><span class="sxs-lookup"><span data-stu-id="4f679-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="4f679-150">hello 下列範例會使用`ConvertFrom-Json`toodisplay 只有 hello `health_report` hello 結果中的資訊。</span><span class="sxs-lookup"><span data-stu-id="4f679-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="4f679-151">雖然大部分的範例，在此文件使用`ConvertFrom-Json`toodisplay 項目從 hello 回應文件，hello[更新 Ambari 組態](#example-update-ambari-configuration)範例會使用 jq。</span><span class="sxs-lookup"><span data-stu-id="4f679-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="4f679-152">用於此範例 tooconstruct Jq hello JSON 回應文件的新範本。</span><span class="sxs-lookup"><span data-stu-id="4f679-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="4f679-153">Hello REST API 的完整參考，請參閱[Ambari 應用程式開發介面參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4f679-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="4f679-154">範例： 取得 hello 的叢集節點 FQDN</span><span class="sxs-lookup"><span data-stu-id="4f679-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="4f679-155">當使用 HDInsight，您可能需要 tooknow hello 完整的網域名稱 (FQDN) 的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="4f679-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="4f679-156">您可以輕鬆地擷取 hello FQDN hello 叢集使用 hello 遵循範例中的，各種節點：</span><span class="sxs-lookup"><span data-stu-id="4f679-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="4f679-157">**所有節點**</span><span class="sxs-lookup"><span data-stu-id="4f679-157">**All nodes**</span></span>

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

* <span data-ttu-id="4f679-158">**前端節點**：</span><span class="sxs-lookup"><span data-stu-id="4f679-158">**Head nodes**</span></span>

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

* <span data-ttu-id="4f679-159">**背景工作節點**</span><span class="sxs-lookup"><span data-stu-id="4f679-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="4f679-160">**Zookeeper 節點**</span><span class="sxs-lookup"><span data-stu-id="4f679-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="4f679-161">範例： 取得 hello 內部 IP 位址的叢集節點</span><span class="sxs-lookup"><span data-stu-id="4f679-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f679-162">本節中的 hello 範例所傳回的 hello IP 位址是無法直接存取 over hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="4f679-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="4f679-163">它們只會在 hello 包含 hello HDInsight 叢集的 Azure 虛擬網路中存取。</span><span class="sxs-lookup"><span data-stu-id="4f679-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="4f679-164">如需使用 HDInsight 和虛擬網路的詳細資訊，請參閱[使用自訂 Azure 虛擬網路擴充 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="4f679-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="4f679-165">toofind hello IP 位址，您必須知道 hello 內部的完整的網域名稱 (FQDN 的 hello 叢集節點)。</span><span class="sxs-lookup"><span data-stu-id="4f679-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="4f679-166">一旦您擁有 hello FQDN，然後就可以 hello hello 主機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f679-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="4f679-167">hello 下列範例先查詢 Ambari hello FQDN，所有的 hello 主機節點，然後查詢 Ambari hello 的每一部主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f679-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="4f679-168">範例： 取得 hello 預設儲存體</span><span class="sxs-lookup"><span data-stu-id="4f679-168">Example: Get hello default storage</span></span>

<span data-ttu-id="4f679-169">當您建立的 HDInsight 叢集時，您必須使用 Azure 儲存體帳戶或資料湖存放區作為 hello 預設儲存體 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="4f679-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="4f679-170">建立 hello 叢集後，您可以使用指定 Ambari tooretrieve 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4f679-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="4f679-171">例如，如果您想外 HDInsight tooread/寫入資料 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="4f679-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="4f679-172">hello 下列範例擷取 hello 預設儲存體設定 hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="4f679-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="4f679-173">這些範例會傳回第一次套用設定 toohello 伺服器 hello (`service_config_version=1`) 包含這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4f679-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="4f679-174">如果您擷取在叢集建立後已修改的值，您可能需要在 toolist hello 組態版本，並擷取 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="4f679-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="4f679-175">hello 傳回值會是 hello 的類似 tooone 遵循範例：</span><span class="sxs-lookup"><span data-stu-id="4f679-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="4f679-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`為這個值表示該 hello 叢集使用的是 Azure 儲存體帳戶預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="4f679-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="4f679-177">hello`ACCOUNTNAME`值為 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4f679-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="4f679-178">hello`CONTAINER`部分是 hello hello 儲存體帳戶中的 hello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="4f679-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="4f679-179">hello 容器是 hello 根 hello hello 叢集的 HDFS 相容的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="4f679-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="4f679-180">`adl://home`為這個值表示該 hello 叢集使用預設儲存體的 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="4f679-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="4f679-181">toofind hello Data Lake Store 帳戶名稱，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="4f679-182">hello 傳回值就會類似太`ACCOUNTNAME.azuredatalakestore.net`，其中`ACCOUNTNAME`hello hello Data Lake Store 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4f679-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="4f679-183">資料湖存放區，其中包含 hello 叢集的存放裝置 hello，下列範例使用 hello 內 toofind hello 目錄：</span><span class="sxs-lookup"><span data-stu-id="4f679-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="4f679-184">hello 傳回值就會類似太`/clusters/CLUSTERNAME/`。</span><span class="sxs-lookup"><span data-stu-id="4f679-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="4f679-185">此值為 hello Data Lake Store 帳戶內的路徑。</span><span class="sxs-lookup"><span data-stu-id="4f679-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="4f679-186">這個路徑是 hello hello hello 叢集的 HDFS 相容的檔案系統根目錄。</span><span class="sxs-lookup"><span data-stu-id="4f679-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="4f679-187">hello`Get-AzureRmHDInsightCluster`所提供的 cmdlet [Azure PowerShell](/powershell/azure/overview)也傳回 hello hello 叢集的儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="4f679-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="4f679-188">範例：取得組態</span><span class="sxs-lookup"><span data-stu-id="4f679-188">Example: Get configuration</span></span>

1. <span data-ttu-id="4f679-189">取得可供您的叢集 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="4f679-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="4f679-190">這個範例會傳回包含 hello 目前組態的 JSON 文件 (由 hello*標記*值) hello hello 叢集上安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="4f679-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="4f679-191">hello 下列範例是摘錄自 hello Spark 叢集類型所傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="4f679-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="4f679-192">取得您感興趣的 hello 元件的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="4f679-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="4f679-193">下列範例，取代在 hello`INITIAL`與 hello hello 前一個要求所傳回的標記值。</span><span class="sxs-lookup"><span data-stu-id="4f679-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="4f679-194">這個範例會傳回包含 hello hello 目前組態的 JSON 文件`core-site`元件。</span><span class="sxs-lookup"><span data-stu-id="4f679-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="4f679-195">範例︰更新組態</span><span class="sxs-lookup"><span data-stu-id="4f679-195">Example: Update configuration</span></span>

1. <span data-ttu-id="4f679-196">收到 hello 目前組態，Ambari 將儲存為 hello 」 所需組態 >:</span><span class="sxs-lookup"><span data-stu-id="4f679-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="4f679-197">這個範例會傳回包含 hello 目前組態的 JSON 文件 (由 hello*標記*值) hello hello 叢集上安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="4f679-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="4f679-198">hello 下列範例是摘錄自 hello Spark 叢集類型所傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="4f679-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="4f679-199">從這個清單中，您需要 toocopy hello hello 元件名稱 (例如， **spark\_thrift\_sparkconf**和 hello**標記**值。</span><span class="sxs-lookup"><span data-stu-id="4f679-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="4f679-200">使用下列命令的 hello 擷取 hello 元件和標記的 hello 組態：</span><span class="sxs-lookup"><span data-stu-id="4f679-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="4f679-201">取代**spark-thrift-sparkconf**和**初始**hello 元件與您想要針對 tooretrieve hello 設定的標記。</span><span class="sxs-lookup"><span data-stu-id="4f679-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="4f679-202">Jq 是使用的 tooturn hello 資料從 HDInsight 擷取至新的組態範本。</span><span class="sxs-lookup"><span data-stu-id="4f679-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="4f679-203">具體來說，這些範例會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="4f679-204">建立唯一的值，其中包含 hello 字串 「 版本 」 和 hello 日期，儲存在`newtag`。</span><span class="sxs-lookup"><span data-stu-id="4f679-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="4f679-205">建立 hello 新想要設定根文件。</span><span class="sxs-lookup"><span data-stu-id="4f679-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="4f679-206">取得 hello 的 hello 內容`.items[]`陣列，並將它加入下 hello **desired_config**項目。</span><span class="sxs-lookup"><span data-stu-id="4f679-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="4f679-207">刪除 hello `href`， `version`，和`Config`項目，做為這些項目不是所需的 toosubmit 新組態。</span><span class="sxs-lookup"><span data-stu-id="4f679-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="4f679-208">使用 `version#################` 的值新增 `tag` 元素。</span><span class="sxs-lookup"><span data-stu-id="4f679-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="4f679-209">hello 數值部分根據 hello 目前的日期。</span><span class="sxs-lookup"><span data-stu-id="4f679-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="4f679-210">每個組態都必須有唯一的標記。</span><span class="sxs-lookup"><span data-stu-id="4f679-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="4f679-211">最後，hello 資料會儲存 toohello`newconfig.json`文件。</span><span class="sxs-lookup"><span data-stu-id="4f679-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="4f679-212">hello 文件結構應該會出現類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="4f679-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="4f679-213">開啟 hello`newconfig.json`中 hello 的文件和修改/加入值`properties`物件。</span><span class="sxs-lookup"><span data-stu-id="4f679-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="4f679-214">hello 下列範例會變更 hello 值`"spark.yarn.am.memory"`從`"1g"`太`"3g"`。</span><span class="sxs-lookup"><span data-stu-id="4f679-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="4f679-215">它也會使用 `"256m"` 的值新增 `"spark.kryoserializer.buffer.max"`。</span><span class="sxs-lookup"><span data-stu-id="4f679-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="4f679-216">Hello 檔案儲存在您完成後的修改。</span><span class="sxs-lookup"><span data-stu-id="4f679-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="4f679-217">使用下列命令 toosubmit hello 更新組態 tooAmbari hello。</span><span class="sxs-lookup"><span data-stu-id="4f679-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="4f679-218">這些命令送出 hello hello 內容**newconfig.json**檔 toohello 叢集為 hello 新增所需的組態。</span><span class="sxs-lookup"><span data-stu-id="4f679-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="4f679-219">hello 要求會傳回 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="4f679-219">hello request returns a JSON document.</span></span> <span data-ttu-id="4f679-220">hello **versionTag**這份文件中的項目應符合 hello 版本，將它送出，然後再 hello **configs**物件包含您所要求的 hello 組態變更。</span><span class="sxs-lookup"><span data-stu-id="4f679-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="4f679-221">範例︰重新啟動服務元件</span><span class="sxs-lookup"><span data-stu-id="4f679-221">Example: Restart a service component</span></span>

<span data-ttu-id="4f679-222">此時，如果您看一下 hello Ambari web UI，hello 的 Spark 服務會指出它需要 toobe 重新啟動 hello 新設定才會生效。</span><span class="sxs-lookup"><span data-stu-id="4f679-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="4f679-223">使用下列步驟 toorestart hello 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="4f679-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="4f679-224">使用下列 tooenable hello 的 Spark 服務在維護模式下的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="4f679-225">這些命令會傳送 JSON 文件 toohello 伺服器，以維護模式開啟。</span><span class="sxs-lookup"><span data-stu-id="4f679-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="4f679-226">您可以確認 hello 服務目前處於維護模式使用 hello 下列要求：</span><span class="sxs-lookup"><span data-stu-id="4f679-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="4f679-227">hello 傳回值是`ON`。</span><span class="sxs-lookup"><span data-stu-id="4f679-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="4f679-228">接下來，使用下列 tooturn hello 服務關閉的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f679-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="4f679-229">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="4f679-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="4f679-230">hello`href`這個 URI 所傳回的值使用 hello 叢集節點的 hello 內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f679-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="4f679-231">toouse 外部 hello 叢集中，從 hello '10.0.0.18:8080' 部分取代 hello hello 叢集的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="4f679-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="4f679-232">下列命令的 hello 擷取 hello hello 要求狀態：</span><span class="sxs-lookup"><span data-stu-id="4f679-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="4f679-233">回應`COMPLETED`表示該 hello 要求已完成。</span><span class="sxs-lookup"><span data-stu-id="4f679-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="4f679-234">Hello 前一個要求完成之後，請使用下列 toostart hello 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="4f679-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="4f679-235">hello 服務正在使用 hello 新組態。</span><span class="sxs-lookup"><span data-stu-id="4f679-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="4f679-236">最後，使用下列維護模式關閉 tooturn hello。</span><span class="sxs-lookup"><span data-stu-id="4f679-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="4f679-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f679-237">Next steps</span></span>

<span data-ttu-id="4f679-238">Hello REST API 的完整參考，請參閱[Ambari 應用程式開發介面參考 V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4f679-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

