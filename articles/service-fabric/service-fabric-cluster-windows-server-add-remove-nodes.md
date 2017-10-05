---
title: "在獨立 Service Fabric 叢集中新增或移除節點 | Microsoft Docs"
description: "了解如何在執行 Windows Server 的實體或虛擬電腦上 (無論是在內部部署或任何雲端) 對 Azure Service Fabric 叢集新增或移除節點。"
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
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="4cb9c-103">在執行於 Windows Server 上的獨立 Service Fabric 叢集中新增或移除節點</span><span class="sxs-lookup"><span data-stu-id="4cb9c-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="4cb9c-104">[在 Windows Server 機器上建立獨立 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)之後，您的業務需求可能會改變，因此您可能需要在叢集中新增或移除節點。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="4cb9c-105">本文提供可達成此目的的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="4cb9c-106">請注意，在本機開發叢集中，不支援新增/移除節點功能。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="4cb9c-107">將節點新增至叢集</span><span class="sxs-lookup"><span data-stu-id="4cb9c-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="4cb9c-108">依照[準備機器以符合叢集部署的必要條件](service-fabric-cluster-creation-for-windows-server.md)一節所提到的步驟操作，來準備要新增至叢集的 VM/機器</span><span class="sxs-lookup"><span data-stu-id="4cb9c-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="4cb9c-109">識別要用來新增此 VM/機器的容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="4cb9c-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="4cb9c-110">透過遠端桌面 (RDP) 登入到要新增至叢集的 VM/機器</span><span class="sxs-lookup"><span data-stu-id="4cb9c-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="4cb9c-111">複製或[下載適用於 Windows Server 之 Service Fabric 的獨立套件](http://go.microsoft.com/fwlink/?LinkId=730690)到此 VM/機器，然後將套件解壓縮</span><span class="sxs-lookup"><span data-stu-id="4cb9c-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="4cb9c-112">以較高的權限 PowerShell，然後瀏覽至解壓縮套件的位置</span><span class="sxs-lookup"><span data-stu-id="4cb9c-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="4cb9c-113">使用描述要新增之新節點的參數來執行 *AddNode.ps1* 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="4cb9c-114">下列範例會將名為 VM5 的新節點 (類型為 NodeType0 且 IP 位址為 182.17.34.52) 新增至 UD1 和 fd:/dc1/r0。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="4cb9c-115">*ExistingClusterConnectionEndPoint* 是已在現有叢集中之節點的連線端點，這可以是叢集中「任何」節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="4cb9c-116">指令碼執行完成之後，您可以執行 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) Cmdlet，來檢查是否已新增新節點。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="4cb9c-117">為了確保叢集中不同節點間的一致性，您必須起始組態升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="4cb9c-118">請執行 [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) 來取得最新的組態檔，然後將剛新增的節點新增到 "Nodes" 區段。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="4cb9c-119">此外，建議您一律備妥最新的叢集組態，以因應您需要以相同組態重新部署叢集的情況。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="4cb9c-120">執行 [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) 來開始升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="4cb9c-121">您可以在 Service Fabric Explorer 中監視升級進度。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4cb9c-122">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4cb9c-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="4cb9c-123">使用 gMSA 將節點新增至已設定 Windows 安全性的叢集</span><span class="sxs-lookup"><span data-stu-id="4cb9c-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="4cb9c-124">針對已設定「群組受管理的服務帳戶」(gMSA)(https://technet.microsoft.com/library/hh831782.aspx) 的叢集，可以使用組態升級來新增新的節點：</span><span class="sxs-lookup"><span data-stu-id="4cb9c-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="4cb9c-125">在任何現有的節點上執行 [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) 來取得最新的組態檔，然後在 "Nodes" 區段中新增有關所要新增之新節點的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="4cb9c-126">請確定新節點屬於相同的群組受管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="4cb9c-127">此帳戶應該是所有機器上的「系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="4cb9c-128">執行 [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) 來開始升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="4cb9c-129">您可以在 Service Fabric Explorer 中監視升級進度。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4cb9c-130">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4cb9c-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="4cb9c-131">將節點類型新增至叢集</span><span class="sxs-lookup"><span data-stu-id="4cb9c-131">Add node types to your cluster</span></span>
<span data-ttu-id="4cb9c-132">若要新增新的節點類型，請修改您的組態以在 "Properties" 底下的 "NodeTypes" 區段中包含新節點類型，然後使用 [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) 來開始組態升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="4cb9c-133">升級完成之後，您便可以將此節點類型的新節點新增到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="4cb9c-134">從叢集移除節點</span><span class="sxs-lookup"><span data-stu-id="4cb9c-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="4cb9c-135">您可以使用組態升級，以下列方式將節點自叢集中移除：</span><span class="sxs-lookup"><span data-stu-id="4cb9c-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="4cb9c-136">執行 [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) 來取得最新的組態檔，然後將節點從 "Nodes" 區段中「移除」。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="4cb9c-137">將 "NodesToBeRemoved" 參數新增至 "FabricSettings" 區段內的 "Setup" 區段。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="4cb9c-138">"value" 應該是需要移除之節點的節點名稱清單 (以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

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
2. <span data-ttu-id="4cb9c-139">執行 [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) 來開始升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="4cb9c-140">您可以在 Service Fabric Explorer 中監視升級進度。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4cb9c-141">或者，您也可以執行 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4cb9c-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="4cb9c-142">移除節點可能會起始多個升級作業。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="4cb9c-143">有些節點帶有 `IsSeedNode=”true”` 標記標示，透過使用 `Get-ServiceFabricClusterManifest` 來查詢叢集資訊清單即可識別這些節點。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="4cb9c-144">移除這類節點所需的時間可能比移除其他節點長，因為在這類案例中，需要將種子節點四處移動。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="4cb9c-145">叢集必須至少維持 3 個主要節點類型節點。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="4cb9c-146">從叢集移除節點類型</span><span class="sxs-lookup"><span data-stu-id="4cb9c-146">Remove node types from your cluster</span></span>
<span data-ttu-id="4cb9c-147">移除節點之前，請仔細檢查是否有任何節點參考該節點類型。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="4cb9c-148">請先移除這些節點，然後才移除對應的節點類型。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="4cb9c-149">移除所有對應的節點之後，您便可以將該 NodeType 自叢集組態中移除，然後使用 [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) 來開始組態升級。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="4cb9c-150">取代您叢集的主要節點</span><span class="sxs-lookup"><span data-stu-id="4cb9c-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="4cb9c-151">應以逐一取代主要節點的方式來執行，而不是以批次方式移除後再加入。</span><span class="sxs-lookup"><span data-stu-id="4cb9c-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4cb9c-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4cb9c-152">Next steps</span></span>
* [<span data-ttu-id="4cb9c-153">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="4cb9c-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="4cb9c-154">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="4cb9c-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="4cb9c-155">建立具有執行 Windows 之 Azure VM 的獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="4cb9c-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

