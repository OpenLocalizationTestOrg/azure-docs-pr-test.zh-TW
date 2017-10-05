---
title: "設定 Azure Service Fabric 獨立叢集 | Microsoft Docs"
description: "了解如何設定獨立或私人的 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="e696d-103">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="e696d-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="e696d-104">本文說明如何使用 ClusterConfig.JSON 檔案來設定獨立 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="e696d-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="e696d-105">您可以使用此檔案針對獨立叢集指定如下的資訊：Service Fabric 節點及其 IP 位址、叢集上不同類型的節點、安全性組態，以及關於容錯/升級網域的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="e696d-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="e696d-106">當您[下載獨立 Service Fabric 套件](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)時，即會將 ClusterConfig.JSON 檔案的一些範例下載至您的工作電腦。</span><span class="sxs-lookup"><span data-stu-id="e696d-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="e696d-107">名稱中有「DevCluster」的範例將可協助您在同一部電腦上建立三個節點皆具的叢集，例如邏輯節點。</span><span class="sxs-lookup"><span data-stu-id="e696d-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="e696d-108">在這三個節點中，至少必須將一個節點標示為主要節點。</span><span class="sxs-lookup"><span data-stu-id="e696d-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="e696d-109">此叢集可用於開發或測試環境，但不支援做為生產叢集。</span><span class="sxs-lookup"><span data-stu-id="e696d-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="e696d-110">名稱中有「MultiMachine」的範例將可協助您建立生產品質叢集，其中的每個節點會建立在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="e696d-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="e696d-111">「ClusterConfig.Unsecure.DevCluster.JSON」和「ClusterConfig.Unsecure.MultiMachine.JSON」示範如何分別建立不安全的測試或生產叢集。</span><span class="sxs-lookup"><span data-stu-id="e696d-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="e696d-112">「ClusterConfig.Windows.DevCluster.JSON」和「ClusterConfig.Windows.MultiMachine.JSON」示範如何使用 [Windows 安全性](service-fabric-windows-cluster-windows-security.md)建立受保護的測試或生產叢集。</span><span class="sxs-lookup"><span data-stu-id="e696d-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="e696d-113">「ClusterConfig.X509.DevCluster.JSON」和「ClusterConfig.X509.MultiMachine.JSON」示範如何使用 [X509 憑證型安全性](service-fabric-windows-cluster-x509-security.md)建立受保護的測試或生產叢集。</span><span class="sxs-lookup"><span data-stu-id="e696d-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="e696d-114">現在，我們將檢視 ClusterConfig.JSON 檔案的不同區段，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="e696d-115">一般叢集組態</span><span class="sxs-lookup"><span data-stu-id="e696d-115">General cluster configurations</span></span>
<span data-ttu-id="e696d-116">這涵蓋廣泛的叢集特定組態，如以下 JSON 片段所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="e696d-117">若要為 Service Fabric 叢集提供任何易記名稱，您可以將它指派給 **name** 變數。</span><span class="sxs-lookup"><span data-stu-id="e696d-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="e696d-118">**ClusterConfigurationVersion** 是叢集的版本號碼，您應該在每次升級 Service Fabric 叢集時上調此號碼。</span><span class="sxs-lookup"><span data-stu-id="e696d-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="e696d-119">不過，您應該讓 **apiVersion** 保持使用預設值。</span><span class="sxs-lookup"><span data-stu-id="e696d-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="e696d-120">叢集上的節點</span><span class="sxs-lookup"><span data-stu-id="e696d-120">Nodes on the cluster</span></span>
<span data-ttu-id="e696d-121">您可以使用 **nodes** 區段，在 Service Fabric 叢集上設定節點，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="e696d-122">Service Fabric 叢集至少必須包含 3 個節點。</span><span class="sxs-lookup"><span data-stu-id="e696d-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="e696d-123">您可以根據安裝程式，在此區段中新增更多節點。</span><span class="sxs-lookup"><span data-stu-id="e696d-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="e696d-124">下表說明每個節點的組態設定。</span><span class="sxs-lookup"><span data-stu-id="e696d-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="e696d-125">**節點組態**</span><span class="sxs-lookup"><span data-stu-id="e696d-125">**Node configuration**</span></span> | <span data-ttu-id="e696d-126">**說明**</span><span class="sxs-lookup"><span data-stu-id="e696d-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e696d-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="e696d-127">nodeName</span></span> |<span data-ttu-id="e696d-128">您可以為節點提供易記名稱。</span><span class="sxs-lookup"><span data-stu-id="e696d-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="e696d-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="e696d-129">iPAddress</span></span> |<span data-ttu-id="e696d-130">開啟命令視窗並輸入 `ipconfig`，以找出節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e696d-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="e696d-131">記下 IPV4 位址，並將它指派給 **iPAddress** 變數。</span><span class="sxs-lookup"><span data-stu-id="e696d-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="e696d-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="e696d-132">nodeTypeRef</span></span> |<span data-ttu-id="e696d-133">每個節點都可以指派不同的節點類型。</span><span class="sxs-lookup"><span data-stu-id="e696d-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="e696d-134">[節點類型](#nodetypes) 將於下一節中定義。</span><span class="sxs-lookup"><span data-stu-id="e696d-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="e696d-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="e696d-135">faultDomain</span></span> |<span data-ttu-id="e696d-136">容錯網域可讓叢集管理員定義實體節點，這類節點可能會在相同時間因為共用實體的相依性 (例如電源和網路來源) 而發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e696d-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="e696d-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="e696d-137">upgradeDomain</span></span> |<span data-ttu-id="e696d-138">升級網域說明大約會在相同時間關閉以進行 Service Fabric 升級的節點集。</span><span class="sxs-lookup"><span data-stu-id="e696d-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="e696d-139">因為它們不會受到任何實體需求所限制，您可以選擇要將哪些節點指派給哪些升級網域。</span><span class="sxs-lookup"><span data-stu-id="e696d-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="e696d-140">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="e696d-140">Cluster properties</span></span>
<span data-ttu-id="e696d-141">ClusterConfig.JSON 中的 **properties** 區段用來設定叢集，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="e696d-142">可靠性</span><span class="sxs-lookup"><span data-stu-id="e696d-142">Reliability</span></span>
<span data-ttu-id="e696d-143">**reliabilityLevel** 的概念會定義可以在叢集主要節點上執行之 Service Fabric 系統服務的複本或執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="e696d-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="e696d-144">它會決定這些服務以及叢集的可靠性。</span><span class="sxs-lookup"><span data-stu-id="e696d-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="e696d-145">其值會由系統在建立和升級叢集時計算。</span><span class="sxs-lookup"><span data-stu-id="e696d-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="e696d-146">診斷</span><span class="sxs-lookup"><span data-stu-id="e696d-146">Diagnostics</span></span>
<span data-ttu-id="e696d-147">**diagnosticsStore** 區段可讓您設定參數，以啟用診斷以及疑難排解節點或叢集的失敗，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="e696d-148">**metadata** 是叢集診斷的說明，而且可根據您的安裝程式來設定。</span><span class="sxs-lookup"><span data-stu-id="e696d-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="e696d-149">這些變數有助於收集 ETW 追蹤記錄檔、損毀傾印，以及效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e696d-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="e696d-150">如需 ETW 追蹤記錄檔的詳細資訊，請參閱 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 和 [ETW 追蹤](https://msdn.microsoft.com/library/ms751538.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e696d-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="e696d-151">包含[損毀傾印](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/)和[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)的所有記錄檔可導向至電腦上的 **connectionString** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e696d-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="e696d-152">您也可以使用 *AzureStorage* 儲存診斷。</span><span class="sxs-lookup"><span data-stu-id="e696d-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="e696d-153">請參閱下面的範例程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e696d-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="e696d-154">安全性</span><span class="sxs-lookup"><span data-stu-id="e696d-154">Security</span></span>
<span data-ttu-id="e696d-155">**security** 區段對於安全獨立的 Service Fabric 叢集是必要的項目。</span><span class="sxs-lookup"><span data-stu-id="e696d-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="e696d-156">下列程式碼片段示範此區段的一部分。</span><span class="sxs-lookup"><span data-stu-id="e696d-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="e696d-157">**metadata** 是安全叢集的說明，而且可根據您的安裝程式來設定。</span><span class="sxs-lookup"><span data-stu-id="e696d-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="e696d-158">**ClusterCredentialType** 和 **ServerCredentialType** 決定叢集和節點將實作的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="e696d-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="e696d-159">如果是憑證式安全性，可設定為 *X509*，如果是以 Azure Active Directory 為基礎的安全性，可設定為 *Windows*。</span><span class="sxs-lookup"><span data-stu-id="e696d-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="e696d-160">其餘的 **security** 區段則是根據安全性類型。</span><span class="sxs-lookup"><span data-stu-id="e696d-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="e696d-161">如需如何填滿其餘 **security** 區段的相關資訊，請參閱[獨立叢集中的憑證式安全性](service-fabric-windows-cluster-x509-security.md)或[獨立叢集中的 Windows 安全性](service-fabric-windows-cluster-windows-security.md)。</span><span class="sxs-lookup"><span data-stu-id="e696d-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="e696d-162">節點類型</span><span class="sxs-lookup"><span data-stu-id="e696d-162">Node Types</span></span>
<span data-ttu-id="e696d-163">**nodeTypes** 區段說明叢集所擁有的節點類型。</span><span class="sxs-lookup"><span data-stu-id="e696d-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="e696d-164">至少必須針對叢集指定一個節點類型，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="e696d-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="e696d-165">**name** 是此特定節點類型的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="e696d-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="e696d-166">若要建立此節點類型的節點，請將其易記名稱指派給該節點的 **nodeTypeRef** 變數，如[上面](#clusternodes)所述。</span><span class="sxs-lookup"><span data-stu-id="e696d-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="e696d-167">為每個節點類型定義將會使用的連接端點。</span><span class="sxs-lookup"><span data-stu-id="e696d-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="e696d-168">您可以為這些連接端點選擇任意的連接埠號碼，只要它們不會與此叢集中的任何其他端點發生衝突即可。</span><span class="sxs-lookup"><span data-stu-id="e696d-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="e696d-169">視 [**reliabilityLevel**](#reliability) 而定，多節點叢集中會有一或多個主要節點 (也就是 **isPrimary** 設為 *true*)。</span><span class="sxs-lookup"><span data-stu-id="e696d-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="e696d-170">如需 **nodeTypes** 和 **reliabilityLevel** 的詳細資訊，以及為了了解主要和非主要節點類型，請參閱 [Service Fabric 叢集容量規劃考量](service-fabric-cluster-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="e696d-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="e696d-171">用來設定節點類型的端點</span><span class="sxs-lookup"><span data-stu-id="e696d-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="e696d-172">clientConnectionEndpointPort 是在使用用戶端 API 時，用戶端用來連線到叢集的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="e696d-173">clusterConnectionEndpointPort 是節點用來彼此通訊的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="e696d-174">leaseDriverEndpointPort 是叢集租用驅動程式用來了解節點是否仍在作用中的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="e696d-175">serviceConnectionEndpointPort 是節點上部署的應用程式和服務用來與該特定節點的 Service Fabric 用戶端通訊的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="e696d-176">httpGatewayEndpointPort 是 Service Fabric Explorer 用來連線到叢集的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="e696d-177">ephemeralPorts 會覆寫 [OS 所使用的動態連接埠](https://support.microsoft.com/kb/929851)。</span><span class="sxs-lookup"><span data-stu-id="e696d-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="e696d-178">Service Fabric 會使用一部分連接埠做為應用程式連接埠，其餘連接埠則可供 OS 使用。</span><span class="sxs-lookup"><span data-stu-id="e696d-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="e696d-179">它也會將此範圍對應至 OS 中存在的現有範圍，因此不論用途為何，您都可以使用範例 JSON 檔案中給定的範圍。</span><span class="sxs-lookup"><span data-stu-id="e696d-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="e696d-180">您必須確保頭尾連接埠之間相差至少 255。</span><span class="sxs-lookup"><span data-stu-id="e696d-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="e696d-181">如果這項差異太低，您可能會遇到衝突，因為這個範圍會與作業系統共用。</span><span class="sxs-lookup"><span data-stu-id="e696d-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="e696d-182">請參閱設定的動態連接埠範圍，方法是執行 `netsh int ipv4 show dynamicport tcp`。</span><span class="sxs-lookup"><span data-stu-id="e696d-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="e696d-183">applicationPorts 是 Service Fabric 應用程式將使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e696d-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="e696d-184">應用程式連接埠範圍應該足以涵蓋應用程式的端點需求。</span><span class="sxs-lookup"><span data-stu-id="e696d-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="e696d-185">此範圍應該排除於電腦上的動態連接埠範圍 (也就是在組態中設定的 *ephemeralPorts* 範圍) 之外。</span><span class="sxs-lookup"><span data-stu-id="e696d-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="e696d-186">Service Fabric 會在每當需要新連接埠時使用這些連接埠，以及負責開啟這些連接埠的防火牆。</span><span class="sxs-lookup"><span data-stu-id="e696d-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="e696d-187">reverseProxyEndpointPort 是選擇性的反向 Proxy 端點。</span><span class="sxs-lookup"><span data-stu-id="e696d-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="e696d-188">如需詳細資訊，請參閱 [Service Fabric 反向 Proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="e696d-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="e696d-189">記錄設定</span><span class="sxs-lookup"><span data-stu-id="e696d-189">Log Settings</span></span>
<span data-ttu-id="e696d-190">**fabricSettings** 區段可讓您設定 Service Fabric 資料和記錄檔的根目錄。</span><span class="sxs-lookup"><span data-stu-id="e696d-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="e696d-191">您只能在初始叢集建立期間自訂這些項目。</span><span class="sxs-lookup"><span data-stu-id="e696d-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="e696d-192">如需這個區段的範例程式碼片段，請參閱下列內容。</span><span class="sxs-lookup"><span data-stu-id="e696d-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="e696d-193">建議您使用非作業系統磁碟機做為 FabricDataRoot 和 FabricLogRoot，因為這類磁碟機比較不會讓作業系統當機。</span><span class="sxs-lookup"><span data-stu-id="e696d-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="e696d-194">請注意，如果您只自訂資料根目錄，則記錄根目錄將會以資料根目錄的下一個層級來取代。</span><span class="sxs-lookup"><span data-stu-id="e696d-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="e696d-195">具狀態可靠服務設定</span><span class="sxs-lookup"><span data-stu-id="e696d-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="e696d-196">**KtlLogger** 區段可讓您設定 Reliable Services 的全域組態設定。</span><span class="sxs-lookup"><span data-stu-id="e696d-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="e696d-197">如需這些設定的詳細資訊，請參閱[設定具狀態可靠服務](service-fabric-reliable-services-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="e696d-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="e696d-198">下列範例示範如何變更所建立的共用交易記錄，以備份具狀態服務的任何可靠集合。</span><span class="sxs-lookup"><span data-stu-id="e696d-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="e696d-199">附加元件功能</span><span class="sxs-lookup"><span data-stu-id="e696d-199">Add-on features</span></span>
<span data-ttu-id="e696d-200">若要設定附加元件的功能，應將 apiVersion 設定為 ' 04-2017' 或更高版本，而且 addonFeatures 必須設定為：</span><span class="sxs-lookup"><span data-stu-id="e696d-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="e696d-201">容器支援</span><span class="sxs-lookup"><span data-stu-id="e696d-201">Container support</span></span>
<span data-ttu-id="e696d-202">若要啟用獨立叢集的 Windows Server 容器和 Hyper-V 容器的容器支援，必須啟用 'DnsService' 附加元件功能。</span><span class="sxs-lookup"><span data-stu-id="e696d-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e696d-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e696d-203">Next steps</span></span>
<span data-ttu-id="e696d-204">當您根據獨立叢集安裝程式設定完整的 ClusterConfig.JSON 檔案之後，就可以遵循[建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)一文來部署叢集，然後繼續[使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="e696d-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

