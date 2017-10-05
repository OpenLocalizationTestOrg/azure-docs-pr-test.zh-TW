---
title: "在 Azure 中設定 Always On 可用性群組的 ILB 接聽程式 | Microsoft Docs"
description: "本教學課程使用以傳統部署模型建立的資源，並在 Azure 中建立使用內部負載平衡器的 Always On 可用性群組接聽程式。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: fea70b389b1f1d6af963e3f14fdc48e8d857dd53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="9a6fe-103">在 Azure 中設定 Always On 可用性群組的 ILB 接聽程式</span><span class="sxs-lookup"><span data-stu-id="9a6fe-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a6fe-104">內部接聽程式</span><span class="sxs-lookup"><span data-stu-id="9a6fe-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="9a6fe-105">外部接聽程式</span><span class="sxs-lookup"><span data-stu-id="9a6fe-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="9a6fe-106">概觀</span><span class="sxs-lookup"><span data-stu-id="9a6fe-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a6fe-107">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9a6fe-108">本文涵蓋傳統部署模型的使用。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-108">This article covers the use of the classic deployment model.</span></span> <span data-ttu-id="9a6fe-109">我們建議讓大部分的新部署使用 Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-109">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="9a6fe-110">若要在 Resource Manager 模型中設定 Always On 可用性群組的接聽程式，請參閱[在 Azure 中設定 Always On 可用性群組的負載平衡器](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-110">To configure a listener for an Always On availability group in the Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="9a6fe-111">您的可用性群組可包含的複本為僅限內部部署或僅限 Azure，或同時跨內部部署和 Azure 的混合式組態。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="9a6fe-112">Azure 複本可位於相同區域內，或跨越使用多個虛擬網路的多個區域。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-112">Azure replicas can reside within the same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="9a6fe-113">本文中的程序假設您已經[設定可用性群組](../classic/portal-sql-alwayson-availability-groups.md)，但尚未設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-113">The procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="9a6fe-114">內部接聽程式指導方針和限制</span><span class="sxs-lookup"><span data-stu-id="9a6fe-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="9a6fe-115">在 Azure 中使用內部負載平衡器 (ILB) 搭配可用性群組接聽程式時，必須遵循下列指導方針：</span><span class="sxs-lookup"><span data-stu-id="9a6fe-115">The use of an internal load balancer (ILB) with an availability group listener in Azure is subject to the following guidelines:</span></span>

* <span data-ttu-id="9a6fe-116">可用性群組接聽程式支援 Windows Server 2008 R2、Windows Server 2012 和 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="9a6fe-117">每個雲端服務僅支援一個內部可用性群組接聽程式，因為接聽程式被設定為 ILB，且每個雲端服務僅有一個 ILB；</span><span class="sxs-lookup"><span data-stu-id="9a6fe-117">Only one internal availability group listener is supported for each cloud service, because the listener is configured to the ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="9a6fe-118">但是可以建立多個外部接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-118">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="9a6fe-119">如需詳細資訊，請參閱[在 Azure 中設定 Always On 可用性群組的外部接聽程式](../classic/ps-sql-ext-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="9a6fe-120">判斷接聽程式的存取性</span><span class="sxs-lookup"><span data-stu-id="9a6fe-120">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="9a6fe-121">本文著重於建立使用 ILB 的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="9a6fe-122">如果您需要公用或外部接聽程式，請參閱本文討論設定[外部接聽程式](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)的版本。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-122">If you need an public or external listener, see the version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="9a6fe-123">使用伺服器直接回傳建立負載平衡 VM 端點</span><span class="sxs-lookup"><span data-stu-id="9a6fe-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="9a6fe-124">藉由執行本節後面的指令碼，先建立 ILB。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-124">You first create an ILB by running the script later in this section.</span></span>

<span data-ttu-id="9a6fe-125">為每部主控 Azure 複本的 VM 建立負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="9a6fe-126">如果您的複本位於多個區域，則該區域的每個複本必須位於相同 Azure 虛擬網路中的相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-126">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same Azure virtual network.</span></span> <span data-ttu-id="9a6fe-127">建立跨越多個 Azure 區域的可用性群組複本需要設定多個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="9a6fe-128">如需設定跨虛擬網路連線的詳細資訊，請參閱[設定虛擬網路對虛擬網路連線](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network to virtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="9a6fe-129">在 Azure 入口網站中，移至每部主控複本的 VM 以檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-129">In the Azure portal, go to each VM that hosts a replica to view the details.</span></span>

2. <span data-ttu-id="9a6fe-130">按一下每部 VM 的 [端點] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-130">Click the **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="9a6fe-131">對於您想要使用的接聽程式端點，確認其 [名稱] 和 [公用連接埠] 並未使用中。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-131">Verify that the **Name** and **Public Port** of the listener endpoint that you want to use are not already in use.</span></span> <span data-ttu-id="9a6fe-132">在本節的範例中，名稱是 MyEndpoint，而通訊埠為 1433。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-132">In the example in this section, the name is *MyEndpoint*, and the port is *1433*.</span></span>

4. <span data-ttu-id="9a6fe-133">在您的本機用戶端上，下載並安裝最新的 [PowerShell 模組](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-133">On your local client, download and install the latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="9a6fe-134">啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="9a6fe-135">新的 PowerShell 工作階段隨即開啟並載入 Azure 系統管理模組。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-135">A new PowerShell session opens, with the Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="9a6fe-136">執行 `Get-AzurePublishSettingsFile`。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="9a6fe-137">這個 Cmdlet 會將您導向瀏覽器，以便將發佈設定檔案下載至本機目錄。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-137">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="9a6fe-138">系統可能會提示您輸入 Azure 訂用帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="9a6fe-139">使用您所下載發佈設定檔案的路徑來執行下列 `Import-AzurePublishSettingsFile` 命令：</span><span class="sxs-lookup"><span data-stu-id="9a6fe-139">Run the following `Import-AzurePublishSettingsFile` command with the path of the publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="9a6fe-140">匯入發佈設定檔案之後，您便可以在 PowerShell 工作階段中管理 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-140">After the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>

8. <span data-ttu-id="9a6fe-141">針對 *ILB*，指派靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="9a6fe-142">執行下列命令來檢查目前的虛擬網路組態：</span><span class="sxs-lookup"><span data-stu-id="9a6fe-142">Examine the current virtual network configuration by running the following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="9a6fe-143">請記下子網路 (其中包含主控複本的 VM) 的 *Subnet* 名稱。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-143">Note the *Subnet* name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="9a6fe-144">此名稱使用於指令碼中的 $SubnetName 參數。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-144">This name is used in the $SubnetName parameter in the script.</span></span>

10. <span data-ttu-id="9a6fe-145">記下子網路 (其中包含主控複本的 VM) 的 VirtualNetworkSite 名稱和起始的 AddressPrefix。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-145">Note the *VirtualNetworkSite* name and the starting *AddressPrefix* for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="9a6fe-146">將這兩個值傳遞至 `Test-AzureStaticVNetIP` 命令並檢查 AvailableAddresses 以尋找可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-146">Look for an available IP address by passing both values to the `Test-AzureStaticVNetIP` command and by examining the *AvailableAddresses*.</span></span> <span data-ttu-id="9a6fe-147">例如，如果虛擬網路被命名為 MyVNet 且具有以 172.16.0.128 開始的子網路位址範圍，下列命令便會列出可用的位址：</span><span class="sxs-lookup"><span data-stu-id="9a6fe-147">For example, if the virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, the following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="9a6fe-148">選取其中一個可用的位址，並將其用於下一個步驟中指令碼的 $ILBStaticIP 參數。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-148">Select one of the available addresses, and use it in the $ILBStaticIP parameter of the script in the next step.</span></span>

12. <span data-ttu-id="9a6fe-149">將下列 PowerShell 指令碼複製到文字編輯器，並設定變數值以符合您的環境。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-149">Copy the following PowerShell script to a text editor, and set the variable values to suit your environment.</span></span> <span data-ttu-id="9a6fe-150">某些參數已提供預設值。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="9a6fe-151">使用同質群組的現有部署無法新增 ILB。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="9a6fe-152">如需有關 ILB 需求的詳細資訊，請參閱[內部負載平衡器概觀](../../../load-balancer/load-balancer-internal-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="9a6fe-153">此外，如果您的可用性群組跨越 Azure 區域，您必須針對雲端服務和位於該資料中心的節點，在每個資料中心執行一次指令碼。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-153">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value

        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="9a6fe-154">設定變數之後，請從文字編輯器將指令碼複製到您的 PowerShell 工作階段來執行它。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-154">After you have set the variables, copy the script from the text editor to your PowerShell session to run it.</span></span> <span data-ttu-id="9a6fe-155">如果提示依然顯示 **>>**，請再次按 ENTER 鍵以確定指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-155">If the prompt still shows **>>**, press Enter again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="9a6fe-156">必要時，請確認已安裝 KB2854082</span><span class="sxs-lookup"><span data-stu-id="9a6fe-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="9a6fe-157">在可用性群組節點中開啟防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="9a6fe-157">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="9a6fe-158">建立可用性群組接聽程式</span><span class="sxs-lookup"><span data-stu-id="9a6fe-158">Create the availability group listener</span></span>

<span data-ttu-id="9a6fe-159">透過兩個步驟建立可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-159">Create the availability group listener in two steps.</span></span> <span data-ttu-id="9a6fe-160">首先，建立用戶端存取點叢集資源，並設定相依性。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-160">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="9a6fe-161">接著，在 PowerShell 中設定叢集資源。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-161">Second, configure the cluster resources in PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="9a6fe-162">建立用戶端存取點並設定叢集的相依性</span><span class="sxs-lookup"><span data-stu-id="9a6fe-162">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="9a6fe-163">在 PowerShell 中設定叢集資源</span><span class="sxs-lookup"><span data-stu-id="9a6fe-163">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="9a6fe-164">對於 ILB，您必須使用之前所建立 ILB 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-164">For ILB, you must use the IP address of the ILB that was created earlier.</span></span> <span data-ttu-id="9a6fe-165">若要取得 PowerShell 中的這個 IP 位址，請使用下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="9a6fe-165">To obtain this IP address in PowerShell, use the following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="9a6fe-166">在其中一部 VM 上，將適用於您作業系統的 PowerShell 指令碼複製到文字編輯器，然後將變數設定為您先前記下的值。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-166">On one of the VMs, copy the PowerShell script for your operating system to a text editor, and then set the variables to the values you noted earlier.</span></span>

    <span data-ttu-id="9a6fe-167">針對 Windows Server 2012 或更新版本，請使用下列指令碼︰</span><span class="sxs-lookup"><span data-stu-id="9a6fe-167">For Windows Server 2012 or later, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="9a6fe-168">針對 Windows Server 2008 R2，請使用下列指令碼︰</span><span class="sxs-lookup"><span data-stu-id="9a6fe-168">For Windows Server 2008 R2, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="9a6fe-169">設定變數之後，開啟提升權限的 Windows PowerShell 視窗，然後將指令碼從文字編輯器貼到您的 PowerShell 工作階段中來執行它。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-169">After you have set the variables, open an elevated Windows PowerShell window, paste the script from the text editor into your PowerShell session to run it.</span></span> <span data-ttu-id="9a6fe-170">如果提示依然顯示 **>>**，請再次按 ENTER 鍵以確定指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-170">If the prompt still shows **>>**, Press Enter again to make sure that the script starts running.</span></span>

4. <span data-ttu-id="9a6fe-171">對每部 VM 重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-171">Repeat the preceding steps for each VM.</span></span>  
    <span data-ttu-id="9a6fe-172">此指令碼會使用雲端服務的 IP 位址來設定 IP 位址資源，並設定其他參數 (例如探查連接埠)。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-172">This script configures the IP address resource with the IP address of the cloud service and sets other parameters, such as the probe port.</span></span> <span data-ttu-id="9a6fe-173">當 IP 位址資源處於線上時，它會從您稍早所建立的負載平衡端點，回應探查連接埠上的輪詢。</span><span class="sxs-lookup"><span data-stu-id="9a6fe-173">When the IP address resource is brought online, it can respond to the polling on the probe port from the load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="9a6fe-174">使接聽程式上線</span><span class="sxs-lookup"><span data-stu-id="9a6fe-174">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="9a6fe-175">待處理項目</span><span class="sxs-lookup"><span data-stu-id="9a6fe-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-virtual-network"></a><span data-ttu-id="9a6fe-176">測試可用性群組接聽程式 (位於相同的虛擬網路中)</span><span class="sxs-lookup"><span data-stu-id="9a6fe-176">Test the availability group listener (within the same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="9a6fe-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a6fe-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
