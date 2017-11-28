---
title: "aaaAdd 或移除節點 tooa 獨立 Service Fabric 叢集 |Microsoft 文件"
description: "了解 tooadd 或移除節點 tooan Azure Service Fabric 叢集化的實體或虛擬機器執行 Windows Server，可能是在內部部署上，或在任何雲端中。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="7a459-103">新增或移除 Windows Server 上執行的節點 tooa 獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7a459-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="7a459-104">之後[Windows Server 機器上建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)可能會變更您的業務需求，您可能需要 tooadd 或移除節點 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="7a459-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="7a459-105">本文章提供詳細的步驟 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="7a459-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="7a459-106">請注意，在本機開發叢集中，不支援新增/移除節點功能。</span><span class="sxs-lookup"><span data-stu-id="7a459-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="7a459-107">新增節點 tooyour 叢集</span><span class="sxs-lookup"><span data-stu-id="7a459-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="7a459-108">準備 hello 想依照 hello hello 中所述的步驟 tooadd tooyour 叢集的 VM/機器[準備 hello 的電腦上的叢集部署的 toomeet hello 必要條件](service-fabric-cluster-creation-for-windows-server.md)區段</span><span class="sxs-lookup"><span data-stu-id="7a459-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="7a459-109">識別哪些容錯網域和升級網域會持續 tooadd 此 VM/機器</span><span class="sxs-lookup"><span data-stu-id="7a459-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="7a459-110">遠端桌面 (RDP) 至 hello 您想 tooadd toohello 叢集的 VM/電腦</span><span class="sxs-lookup"><span data-stu-id="7a459-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="7a459-111">複製或[下載適用於 Windows Server 服務網狀架構 hello 獨立套件](http://go.microsoft.com/fwlink/?LinkId=730690)toohello VM/機器並將它解壓縮 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="7a459-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="7a459-112">執行 Powershell，使用提高的權限，並瀏覽 toohello hello 解壓縮封裝位置</span><span class="sxs-lookup"><span data-stu-id="7a459-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="7a459-113">執行 hello *AddNode.ps1* hello 參數所描述新節點 tooadd hello 與指令碼。</span><span class="sxs-lookup"><span data-stu-id="7a459-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="7a459-114">hello 下面範例會將新的節點稱為 VM5，與類型 NodeType0 和 IP 位址 182.17.34.52，成 UD1 和 fd: / dc1/r0。</span><span class="sxs-lookup"><span data-stu-id="7a459-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="7a459-115">hello *ExistingClusterConnectionEndPoint*節點連接端點已在 hello 現有叢集中，它可以是 IP 位址 hello*任何*hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="7a459-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="7a459-116">一旦 hello 指令碼完成執行時，您可以檢查是否已新增 hello 新節點執行 hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7a459-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="7a459-117">tooensure hello 叢集中不同節點之間的一致性，您必須起始組態升級。</span><span class="sxs-lookup"><span data-stu-id="7a459-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="7a459-118">執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 最新的組態檔，並加入 hello 新加入的節點太 「 節點 」 一節。</span><span class="sxs-lookup"><span data-stu-id="7a459-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="7a459-119">也建議 tooalways 具有 hello 最新叢集組態可用在 hello 情況下，您需要 tooredploy hello 與叢集相同的設定。</span><span class="sxs-lookup"><span data-stu-id="7a459-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="7a459-120">執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。</span><span class="sxs-lookup"><span data-stu-id="7a459-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="7a459-121">您可以監視 hello Service Fabric 總管 hello 升級進度。</span><span class="sxs-lookup"><span data-stu-id="7a459-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="7a459-122">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="7a459-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="7a459-123">新增節點 tooclusters 設定與使用 gMSA 的 Windows 安全性</span><span class="sxs-lookup"><span data-stu-id="7a459-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="7a459-124">針對已設定「群組受管理的服務帳戶」(gMSA)(https://technet.microsoft.com/library/hh831782.aspx) 的叢集，可以使用組態升級來新增新的節點：</span><span class="sxs-lookup"><span data-stu-id="7a459-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="7a459-125">執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps)上任何 hello 現有節點 tooget hello 最新的組態檔，並加入詳細資料 hello 一新節點中，您想 tooadd hello 「 節點 」 一節。</span><span class="sxs-lookup"><span data-stu-id="7a459-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="7a459-126">請確定 hello 新節點屬於相同的 hello 群組 「 受管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a459-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="7a459-127">此帳戶應該是所有機器上的「系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="7a459-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="7a459-128">執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。</span><span class="sxs-lookup"><span data-stu-id="7a459-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="7a459-129">您可以監視 hello Service Fabric 總管 hello 升級進度。</span><span class="sxs-lookup"><span data-stu-id="7a459-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="7a459-130">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="7a459-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="7a459-131">新增節點型別 tooyour 叢集</span><span class="sxs-lookup"><span data-stu-id="7a459-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="7a459-132">在排序 tooadd 新的節點類型、 修改組態 tooinclude hello 新節點類型 「 屬性 」 底下的"NodeTypes 」 一節中並開始設定升級使用[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="7a459-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="7a459-133">Hello 升級完成之後，您可以加入新的節點 tooyour 叢集與此節點類型。</span><span class="sxs-lookup"><span data-stu-id="7a459-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="7a459-134">從叢集移除節點</span><span class="sxs-lookup"><span data-stu-id="7a459-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="7a459-135">可以從組態升級時，使用下列方式 hello 中的叢集移除節點：</span><span class="sxs-lookup"><span data-stu-id="7a459-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="7a459-136">執行[Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 最新的組態檔和*移除*hello 節點，從 「 節點 」 一節。</span><span class="sxs-lookup"><span data-stu-id="7a459-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="7a459-137">新增 「 NodesToBeRemoved"hello 參數太 「 安裝 」"FabricSettings 」 區段中的區段。</span><span class="sxs-lookup"><span data-stu-id="7a459-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="7a459-138">hello"value"應該是需要 toobe 移除的節點的節點名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="7a459-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="7a459-139">執行[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 升級。</span><span class="sxs-lookup"><span data-stu-id="7a459-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="7a459-140">您可以監視 hello Service Fabric 總管 hello 升級進度。</span><span class="sxs-lookup"><span data-stu-id="7a459-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="7a459-141">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="7a459-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="7a459-142">移除節點可能會起始多個升級作業。</span><span class="sxs-lookup"><span data-stu-id="7a459-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="7a459-143">某些節點會標示`IsSeedNode=”true”`標記，並且可以由查詢 hello 叢集資訊清單使用`Get-ServiceFabricClusterManifest`。</span><span class="sxs-lookup"><span data-stu-id="7a459-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="7a459-144">因為 hello 種子節點必須在這種情況中移動 toobe，可能會超過其他這類節點移除。</span><span class="sxs-lookup"><span data-stu-id="7a459-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="7a459-145">hello 叢集必須維護 3 個主要節點類型節點的最小的值。</span><span class="sxs-lookup"><span data-stu-id="7a459-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="7a459-146">從叢集移除節點類型</span><span class="sxs-lookup"><span data-stu-id="7a459-146">Remove node types from your cluster</span></span>
<span data-ttu-id="7a459-147">然後再移除節點型別，請檢查是否有任何參考 hello 節點類型的節點。</span><span class="sxs-lookup"><span data-stu-id="7a459-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="7a459-148">移除這些節點，然後再移除 hello 對應的節點類型。</span><span class="sxs-lookup"><span data-stu-id="7a459-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="7a459-149">一旦移除所有對應的節點，您可以從 hello 叢集組態移除 hello NodeType 並開始設定升級使用[開始 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="7a459-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="7a459-150">取代您叢集的主要節點</span><span class="sxs-lookup"><span data-stu-id="7a459-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="7a459-151">hello 取代主要節點應該在另一個，而不是移除，然後將加入批次之後執行的一個節點。</span><span class="sxs-lookup"><span data-stu-id="7a459-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7a459-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a459-152">Next steps</span></span>
* [<span data-ttu-id="7a459-153">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="7a459-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="7a459-154">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="7a459-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="7a459-155">建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="7a459-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

