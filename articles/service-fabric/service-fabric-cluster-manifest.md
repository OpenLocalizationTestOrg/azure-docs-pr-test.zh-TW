---
title: "aaaConfigure 獨立 Azure Service Fabric 叢集 |Microsoft 文件"
description: "深入了解如何 tooconfigure 獨立] 或 [私用的 Service Fabric 叢集。"
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
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="bd88c-103">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="bd88c-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="bd88c-104">本文說明如何 tooconfigure 獨立 Service Fabric 叢集使用 hello***追蹤***檔案。</span><span class="sxs-lookup"><span data-stu-id="bd88c-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="bd88c-105">您可以使用此檔案 toospecify 資訊如 hello Service Fabric 節點和其 IP 位址、 不同類型的節點上 hello 叢集、 hello 安全性組態，以及根據錯誤/升級網域的 hello 網路拓樸您獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="bd88c-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="bd88c-106">當您[下載 hello 獨立 Service Fabric 封裝](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)，hello 追蹤檔案的一些範例僅適用於下載的 tooyour 工作電腦。</span><span class="sxs-lookup"><span data-stu-id="bd88c-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="bd88c-107">具有 hello 範例*DevCluster*名稱中將協助您建立具有 hello 相同機器類似邏輯的節點上的所有三個節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="bd88c-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="bd88c-108">在這三個節點中，至少必須將一個節點標示為主要節點。</span><span class="sxs-lookup"><span data-stu-id="bd88c-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="bd88c-109">此叢集可用於開發或測試環境，但不支援做為生產叢集。</span><span class="sxs-lookup"><span data-stu-id="bd88c-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="bd88c-110">具有 hello 範例*MultiMachine*在其名稱中，將協助您建立生產環境品質的叢集中，每個節點在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="bd88c-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="bd88c-111">*ClusterConfig.Unsecure.DevCluster.JSON*和*ClusterConfig.Unsecure.MultiMachine.JSON*顯示如何 toocreate 不安全的測試或實際執行分別的叢集。</span><span class="sxs-lookup"><span data-stu-id="bd88c-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="bd88c-112">*ClusterConfig.Windows.DevCluster.JSON*和*ClusterConfig.Windows.MultiMachine.JSON*顯示 toocreate 測試或實際執行叢集如何保護使用[Windows 安全性](service-fabric-windows-cluster-windows-security.md)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="bd88c-113">*ClusterConfig.X509.DevCluster.JSON*和*ClusterConfig.X509.MultiMachine.JSON*顯示 toocreate 測試或實際執行叢集如何保護使用[X509 憑證為基礎的安全性](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="bd88c-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="bd88c-114">現在我們將檢驗 hello 的各個不同區段***追蹤***檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd88c-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="bd88c-115">一般叢集組態</span><span class="sxs-lookup"><span data-stu-id="bd88c-115">General cluster configurations</span></span>
<span data-ttu-id="bd88c-116">這涵蓋 hello 廣泛叢集特定組態中，如以下的 hello JSON 片段所示。</span><span class="sxs-lookup"><span data-stu-id="bd88c-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="bd88c-117">您可以藉由將其指派 toohello 授予任何易記名稱 tooyour Service Fabric 叢集**名稱**變數。</span><span class="sxs-lookup"><span data-stu-id="bd88c-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="bd88c-118">hello **clusterConfigurationVersion**是 hello 版本號碼的叢集，您應該增加每次您將 Service Fabric 叢集升級。</span><span class="sxs-lookup"><span data-stu-id="bd88c-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="bd88c-119">不過，您應該保留 hello **Microsoft.authorization** toohello 預設值。</span><span class="sxs-lookup"><span data-stu-id="bd88c-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="bd88c-120">Hello 叢集上的節點</span><span class="sxs-lookup"><span data-stu-id="bd88c-120">Nodes on hello cluster</span></span>
<span data-ttu-id="bd88c-121">您也可以使用 hello Service Fabric 叢集上設定 hello 節點**節點**區段中的，為下列程式碼片段說明 hello。</span><span class="sxs-lookup"><span data-stu-id="bd88c-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

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

<span data-ttu-id="bd88c-122">Service Fabric 叢集至少必須包含 3 個節點。</span><span class="sxs-lookup"><span data-stu-id="bd88c-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="bd88c-123">根據您的設定，您可以加入多個節點 toothis 一節。</span><span class="sxs-lookup"><span data-stu-id="bd88c-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="bd88c-124">hello 下表說明每個節點的 hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="bd88c-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="bd88c-125">**節點組態**</span><span class="sxs-lookup"><span data-stu-id="bd88c-125">**Node configuration**</span></span> | <span data-ttu-id="bd88c-126">**說明**</span><span class="sxs-lookup"><span data-stu-id="bd88c-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="bd88c-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="bd88c-127">nodeName</span></span> |<span data-ttu-id="bd88c-128">您可以提供易記名稱 toohello 的任何節點。</span><span class="sxs-lookup"><span data-stu-id="bd88c-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="bd88c-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="bd88c-129">iPAddress</span></span> |<span data-ttu-id="bd88c-130">找出您節點 hello IP 位址，以開啟命令視窗並鍵入`ipconfig`。</span><span class="sxs-lookup"><span data-stu-id="bd88c-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="bd88c-131">請注意 hello IPV4 位址，並將它指派 toohello **iPAddress**變數。</span><span class="sxs-lookup"><span data-stu-id="bd88c-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="bd88c-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="bd88c-132">nodeTypeRef</span></span> |<span data-ttu-id="bd88c-133">每個節點都可以指派不同的節點類型。</span><span class="sxs-lookup"><span data-stu-id="bd88c-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="bd88c-134">hello[節點型別](#nodetypes)hello 一節中所定義。</span><span class="sxs-lookup"><span data-stu-id="bd88c-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="bd88c-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="bd88c-135">faultDomain</span></span> |<span data-ttu-id="bd88c-136">容錯網域啟用叢集系統管理員 toodefine hello 實體節點可能會在 hello 失敗的相同時間到期，tooshared 實體的相依性。</span><span class="sxs-lookup"><span data-stu-id="bd88c-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="bd88c-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="bd88c-137">upgradeDomain</span></span> |<span data-ttu-id="bd88c-138">升級網域描述都已關閉的 Service Fabric 升級在 hello 關於相同的節點集的時間。</span><span class="sxs-lookup"><span data-stu-id="bd88c-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="bd88c-139">您可以選擇哪些節點 tooassign toowhich 升級網域，如未受到任何實體的需求。</span><span class="sxs-lookup"><span data-stu-id="bd88c-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="bd88c-140">叢集屬性</span><span class="sxs-lookup"><span data-stu-id="bd88c-140">Cluster properties</span></span>
<span data-ttu-id="bd88c-141">hello**屬性**hello 追蹤 > 一節中是使用的 tooconfigure hello 叢集，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd88c-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="bd88c-142">可靠性</span><span class="sxs-lookup"><span data-stu-id="bd88c-142">Reliability</span></span>
<span data-ttu-id="bd88c-143">hello 概念**reliabilityLevel**定義 hello 複本的數目或 hello Service Fabric 系統服務可以在 hello 主要 hello 叢集節點上執行的執行個體。</span><span class="sxs-lookup"><span data-stu-id="bd88c-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="bd88c-144">它會決定這些服務的 hello 可靠性，並因此 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="bd88c-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="bd88c-145">hello 值為 hello 系統計算在叢集建立和升級時間。</span><span class="sxs-lookup"><span data-stu-id="bd88c-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="bd88c-146">診斷</span><span class="sxs-lookup"><span data-stu-id="bd88c-146">Diagnostics</span></span>
<span data-ttu-id="bd88c-147">hello **diagnosticsStore**區段可讓您 tooconfigure 參數 tooenable 診斷和疑難排解的節點或叢集失敗中 hello 下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="bd88c-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="bd88c-148">hello**中繼資料**叢集診斷的描述，且可以根據您的安裝設定。</span><span class="sxs-lookup"><span data-stu-id="bd88c-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="bd88c-149">這些變數有助於收集 ETW 追蹤記錄檔、損毀傾印，以及效能計數器。</span><span class="sxs-lookup"><span data-stu-id="bd88c-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="bd88c-150">如需 ETW 追蹤記錄檔的詳細資訊，請參閱 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 和 [ETW 追蹤](https://msdn.microsoft.com/library/ms751538.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="bd88c-151">包括的所有記錄檔[損毀傾印](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/)和[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)可以導向的 toohello **connectionString**您的電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="bd88c-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="bd88c-152">您也可以使用 *AzureStorage* 儲存診斷。</span><span class="sxs-lookup"><span data-stu-id="bd88c-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="bd88c-153">請參閱下面的範例程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="bd88c-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="bd88c-154">安全性</span><span class="sxs-lookup"><span data-stu-id="bd88c-154">Security</span></span>
<span data-ttu-id="bd88c-155">hello**安全性**區段是安全的獨立 Service Fabric 叢集所需。</span><span class="sxs-lookup"><span data-stu-id="bd88c-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="bd88c-156">hello 下列程式碼片段示範此區段的一部分。</span><span class="sxs-lookup"><span data-stu-id="bd88c-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="bd88c-157">hello**中繼資料**安全叢集的描述，且可以根據您的安裝設定。</span><span class="sxs-lookup"><span data-stu-id="bd88c-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="bd88c-158">hello **ClusterCredentialType**和**ServerCredentialType**決定 hello hello 叢集和 hello 節點將實作的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="bd88c-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="bd88c-159">您可以設定 tooeither *X509*憑證為基礎的安全性，或*Windows* Azure Active Directory 架構的安全性。</span><span class="sxs-lookup"><span data-stu-id="bd88c-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="bd88c-160">hello hello 的其餘部分**安全性**> 一節將根據 hello hello 安全性類型。</span><span class="sxs-lookup"><span data-stu-id="bd88c-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="bd88c-161">讀取[憑證為基礎的安全性，在獨立叢集中](service-fabric-windows-cluster-x509-security.md)或[獨立叢集中的 Windows 安全性](service-fabric-windows-cluster-windows-security.md)如需有關如何出 hello toofill 其餘部分的 hello 詳細**安全性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bd88c-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="bd88c-162">節點類型</span><span class="sxs-lookup"><span data-stu-id="bd88c-162">Node Types</span></span>
<span data-ttu-id="bd88c-163">hello **nodeTypes**章節描述您的叢集有的 hello 節點 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="bd88c-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="bd88c-164">至少一個節點型別必須指定叢集，hello 以下程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="bd88c-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

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

<span data-ttu-id="bd88c-165">hello**名稱**是 hello 此特定節點類型的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="bd88c-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="bd88c-166">toocreate 此節點類型節點，將指派其好記名稱 toohello **nodeTypeRef**變數對於該節點，如所述[上方](#clusternodes)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="bd88c-167">每個節點類型，定義將用於 hello 連接端點。</span><span class="sxs-lookup"><span data-stu-id="bd88c-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="bd88c-168">您可以為這些連接端點選擇任意的連接埠號碼，只要它們不會與此叢集中的任何其他端點發生衝突即可。</span><span class="sxs-lookup"><span data-stu-id="bd88c-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="bd88c-169">在多節點叢集中，會有一或多個主要節點 (也就是**isPrimary**設定得*true*)，端視 hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="bd88c-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="bd88c-170">讀取[Service Fabric 叢集的容量規劃考量](service-fabric-cluster-capacity.md)有關**nodeTypes**和**reliabilityLevel**，和 tooknow 哪些主要或 hello非主要節點類型。</span><span class="sxs-lookup"><span data-stu-id="bd88c-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="bd88c-171">使用端點 tooconfigure hello 節點型別</span><span class="sxs-lookup"><span data-stu-id="bd88c-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="bd88c-172">*clientConnectionEndpointPort*是 hello 使用 hello 用戶端應用程式開發介面時，hello 用戶端 tooconnect toohello 叢集所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd88c-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="bd88c-173">*clusterConnectionEndpointPort* hello hello 節點彼此通訊的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="bd88c-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="bd88c-174">*leaseDriverEndpointPort*是使用 hello 叢集租用驅動程式 toofind 出 hello 節點是否仍在作用中的 hello 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="bd88c-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="bd88c-175">*serviceConnectionEndpointPort* hello hello 應用程式所使用的連接埠及 toocommunicate hello Service Fabric 用戶端上該特定節點的節點上部署的服務。</span><span class="sxs-lookup"><span data-stu-id="bd88c-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="bd88c-176">*httpGatewayEndpointPort*是 hello hello Service Fabric 總管 tooconnect toohello 叢集所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd88c-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="bd88c-177">*ephemeralPorts*覆寫 hello [hello 作業系統所使用的動態連接埠](https://support.microsoft.com/kb/929851)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="bd88c-178">Service Fabric 將使用這些應用程式連接埠的一部分，而且可供 hello OS hello 剩餘。</span><span class="sxs-lookup"><span data-stu-id="bd88c-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="bd88c-179">它也會對應此範圍 toohello 現有範圍中 hello OS，因此所有進行中，您可以使用已知 hello 範例 JSON 檔案中的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="bd88c-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="bd88c-180">您必須確定 hello 開始與 hello 端通訊埠的 hello 差異至少 255 toomake。</span><span class="sxs-lookup"><span data-stu-id="bd88c-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="bd88c-181">如果這項差異太低，因為與 hello 作業系統共用此範圍，則可能會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="bd88c-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="bd88c-182">請參閱 hello 設定動態連接埠範圍，藉由執行`netsh int ipv4 show dynamicport tcp`。</span><span class="sxs-lookup"><span data-stu-id="bd88c-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="bd88c-183">*applicationPorts* hello hello Service Fabric 應用程式將使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd88c-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="bd88c-184">hello 應用程式連接埠範圍應夠大 toocover hello 端點需求的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd88c-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="bd88c-185">此範圍應 hello 在電腦上，也就是 hello hello 動態連接埠範圍排除*ephemeralPorts* hello 組態中所設定的範圍。</span><span class="sxs-lookup"><span data-stu-id="bd88c-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="bd88c-186">服務網狀架構會使用這些新的連接埠為必要欄位，以及負責開啟這些連接埠的 hello 防火牆時。</span><span class="sxs-lookup"><span data-stu-id="bd88c-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="bd88c-187">reverseProxyEndpointPort 是選擇性的反向 Proxy 端點。</span><span class="sxs-lookup"><span data-stu-id="bd88c-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="bd88c-188">如需詳細資訊，請參閱 [Service Fabric 反向 Proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="bd88c-189">記錄設定</span><span class="sxs-lookup"><span data-stu-id="bd88c-189">Log Settings</span></span>
<span data-ttu-id="bd88c-190">hello **fabricSettings**區段可讓您 tooset hello 根 hello Service Fabric 資料與記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="bd88c-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="bd88c-191">您可以自訂這些只在 hello 最初的叢集建立期間。</span><span class="sxs-lookup"><span data-stu-id="bd88c-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="bd88c-192">如需這個區段的範例程式碼片段，請參閱下列內容。</span><span class="sxs-lookup"><span data-stu-id="bd88c-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="bd88c-193">我們建議使用 hello FabricDataRoot 非作業系統磁碟機和 Clusterconfig.json，因為它提供更多的可靠性，對作業系統當機。</span><span class="sxs-lookup"><span data-stu-id="bd88c-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="bd88c-194">請注意，是否您自訂 hello 資料根目錄，然後 hello 記錄根將放置 hello 資料根目錄下的一個層級。</span><span class="sxs-lookup"><span data-stu-id="bd88c-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="bd88c-195">具狀態可靠服務設定</span><span class="sxs-lookup"><span data-stu-id="bd88c-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="bd88c-196">hello **KtlLogger**區段可讓您的可靠服務 tooset hello 全域組態設定。</span><span class="sxs-lookup"><span data-stu-id="bd88c-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="bd88c-197">如需這些設定的詳細資訊，請參閱[設定具狀態可靠服務](service-fabric-reliable-services-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="bd88c-198">hello 以下範例顯示如何 toochange hello hello 共用的交易記錄檔，取得會建立 tooback 可設定狀態服務的任何可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="bd88c-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="bd88c-199">附加元件功能</span><span class="sxs-lookup"><span data-stu-id="bd88c-199">Add-on features</span></span>
<span data-ttu-id="bd88c-200">tooconfigure 附加元件的功能，hello api 版本應該是設定為 ' 04-2017' 或更高版本，而且 addonFeatures 需要 toobe 設定：</span><span class="sxs-lookup"><span data-stu-id="bd88c-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="bd88c-201">容器支援</span><span class="sxs-lookup"><span data-stu-id="bd88c-201">Container support</span></span>
<span data-ttu-id="bd88c-202">windows server 容器和 hyper-v 容器的獨立式叢集 tooenable 容器支援，必須啟用 toobe hello 'DnsService' 附加元件功能。</span><span class="sxs-lookup"><span data-stu-id="bd88c-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd88c-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd88c-203">Next steps</span></span>
<span data-ttu-id="bd88c-204">一旦您擁有完整的追蹤檔案，根據獨立的叢集安裝程式設定，您可以部署下列 hello 發行項所叢集[建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)，然後再繼續太[視覺化您的叢集，利用 Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="bd88c-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

