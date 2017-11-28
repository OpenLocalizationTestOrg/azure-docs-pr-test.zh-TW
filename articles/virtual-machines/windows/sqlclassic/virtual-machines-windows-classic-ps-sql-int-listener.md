---
title: "Always On 可用性群組在 Azure 中的 ILB 接聽程式 aaaConfigure |Microsoft 文件"
description: "本教學課程使用 hello 傳統部署模型，以建立的資源，並且會使用內部負載平衡器的 Azure 中建立 Always On 可用性群組接聽程式。"
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
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="2305e-103">在 Azure 中設定 Always On 可用性群組的 ILB 接聽程式</span><span class="sxs-lookup"><span data-stu-id="2305e-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2305e-104">內部接聽程式</span><span class="sxs-lookup"><span data-stu-id="2305e-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="2305e-105">外部接聽程式</span><span class="sxs-lookup"><span data-stu-id="2305e-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="2305e-106">概觀</span><span class="sxs-lookup"><span data-stu-id="2305e-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2305e-107">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="2305e-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2305e-108">本文涵蓋 hello hello 傳統部署模型使用。</span><span class="sxs-lookup"><span data-stu-id="2305e-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="2305e-109">建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="2305e-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="2305e-110">tooconfigure Always On 可用性群組接聽程式在 hello 資源管理員模型中，請參閱[在 Azure 中設定 Alwayson 可用性群組的負載平衡器](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="2305e-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="2305e-111">您的可用性群組可包含的複本為僅限內部部署或僅限 Azure，或同時跨內部部署和 Azure 的混合式組態。</span><span class="sxs-lookup"><span data-stu-id="2305e-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="2305e-112">Azure 複本可以位於 hello 相同區域或跨多個使用多個虛擬網路的區域。</span><span class="sxs-lookup"><span data-stu-id="2305e-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="2305e-113">hello 本文章中的程序假設您已經有[設定可用性群組](../classic/portal-sql-alwayson-availability-groups.md)但尚未設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2305e-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="2305e-114">內部接聽程式指導方針和限制</span><span class="sxs-lookup"><span data-stu-id="2305e-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="2305e-115">hello 使用可用性群組接聽程式在 Azure 中使用內部負載平衡器 (ILB) 是主體 toohello 指導方針：</span><span class="sxs-lookup"><span data-stu-id="2305e-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="2305e-116">hello 可用性群組接聽程式都支援 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="2305e-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="2305e-117">只有設定其中一種內部的可用性群組接聽程式支援每個雲端服務，因為 hello 接聽程式是 toohello ILB，且沒有每個雲端服務只能有一個 ILB。</span><span class="sxs-lookup"><span data-stu-id="2305e-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="2305e-118">不過，很可能 toocreate 多個外部接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2305e-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="2305e-119">如需詳細資訊，請參閱[在 Azure 中設定 Always On 可用性群組的外部接聽程式](../classic/ps-sql-ext-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="2305e-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="2305e-120">判斷 hello hello 接聽程式的協助工具</span><span class="sxs-lookup"><span data-stu-id="2305e-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="2305e-121">本文著重於建立使用 ILB 的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2305e-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="2305e-122">如果您需要的公用或外部的接聽程式，請參閱這篇文章討論設定總 hello 版本[外部接聽程式](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2305e-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="2305e-123">使用伺服器直接回傳建立負載平衡 VM 端點</span><span class="sxs-lookup"><span data-stu-id="2305e-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="2305e-124">您第一次建立 ILB，稍後執行本節中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2305e-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="2305e-125">為每部主控 Azure 複本的 VM 建立負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="2305e-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="2305e-126">如果您在多個地區複本，每個複本用於該區域檔案必須在相同雲端服務中的 hello hello 相同 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2305e-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="2305e-127">建立跨越多個 Azure 區域的可用性群組複本需要設定多個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2305e-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="2305e-128">如需跨虛擬網路連線設定的詳細資訊，請參閱[設定虛擬網路 toovirtual 網路連接性](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="2305e-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="2305e-129">在 hello Azure 入口網站，移 tooeach VM 主控複本 tooview hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2305e-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="2305e-130">按一下 hello**端點**每個 VM 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2305e-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="2305e-131">請確認該 hello**名稱**和**公用連接埠**的 hello toouse 不存在於使用您想要的接聽程式端點。</span><span class="sxs-lookup"><span data-stu-id="2305e-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="2305e-132">在本節中的 hello 範例，hello 名稱是*MyEndpoint*，而 hello 通訊埠是*1433年*。</span><span class="sxs-lookup"><span data-stu-id="2305e-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="2305e-133">在您的本機用戶端上下載並安裝最新的 hello [PowerShell 模組](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="2305e-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="2305e-134">啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2305e-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="2305e-135">開啟新的 PowerShell 工作階段，以 hello Azure 系統管理模組載入。</span><span class="sxs-lookup"><span data-stu-id="2305e-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="2305e-136">執行 `Get-AzurePublishSettingsFile`。</span><span class="sxs-lookup"><span data-stu-id="2305e-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="2305e-137">這個指令程式會將您導向 tooa 瀏覽器 toodownload 發行設定檔案 tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="2305e-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="2305e-138">系統可能會提示您輸入 Azure 訂用帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="2305e-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="2305e-139">執行下列 hello `Import-AzurePublishSettingsFile` hello hello 路徑的命令發行您所下載的設定檔：</span><span class="sxs-lookup"><span data-stu-id="2305e-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="2305e-140">Hello 發行之後匯入設定檔，您可以管理您的 Azure 訂閱 hello PowerShell 工作階段中。</span><span class="sxs-lookup"><span data-stu-id="2305e-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="2305e-141">針對 *ILB*，指派靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2305e-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="2305e-142">藉由執行下列命令的 hello 檢查 hello 目前的虛擬網路設定：</span><span class="sxs-lookup"><span data-stu-id="2305e-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="2305e-143">請注意 hello*子網路*hello 裝載 hello 複本 hello Vm 所在的子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="2305e-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="2305e-144">Hello 指令碼中的 hello $SubnetName 參數會使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="2305e-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="2305e-145">請注意 hello *VirtualNetworkSite*命名和 hello 啟動*AddressPrefix* hello 子網路，其中包含裝載 hello 複本 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="2305e-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="2305e-146">尋找可用的 IP 位址，藉由傳遞兩個值 toohello`Test-AzureStaticVNetIP`命令，並藉由檢查 hello *AvailableAddresses*。</span><span class="sxs-lookup"><span data-stu-id="2305e-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="2305e-147">例如，如果 hello 虛擬網路稱為*MyVNet*開始的子網路位址範圍且*172.16.0.128*，hello 下列命令會列出可用的位址：</span><span class="sxs-lookup"><span data-stu-id="2305e-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="2305e-148">選取其中一個 hello 可用的位址，並使用 hello $ILBStaticIP hello 下一個步驟中的 hello 指令碼參數中。</span><span class="sxs-lookup"><span data-stu-id="2305e-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="2305e-149">複製下列 PowerShell 指令碼 tooa 文字編輯器的 hello，並設定您的環境的 hello 變數值 toosuit。</span><span class="sxs-lookup"><span data-stu-id="2305e-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="2305e-150">某些參數已提供預設值。</span><span class="sxs-lookup"><span data-stu-id="2305e-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="2305e-151">使用同質群組的現有部署無法新增 ILB。</span><span class="sxs-lookup"><span data-stu-id="2305e-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="2305e-152">如需有關 ILB 需求的詳細資訊，請參閱[內部負載平衡器概觀](../../../load-balancer/load-balancer-internal-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2305e-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="2305e-153">此外，如果您的可用性群組跨越 Azure 地區，您必須執行 hello 指令碼一次每個資料中心 hello 雲端服務和位於該資料中心的節點。</span><span class="sxs-lookup"><span data-stu-id="2305e-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="2305e-154">設定 hello 變數之後，複本 hello 編寫指令碼從 hello 文字編輯器 tooyour PowerShell 工作階段 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="2305e-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="2305e-155">如果 hello 提示依然顯示 **>>** ，按下的 Enter 再次 toomake 確定 hello 指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="2305e-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="2305e-156">必要時，請確認已安裝 KB2854082</span><span class="sxs-lookup"><span data-stu-id="2305e-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="2305e-157">開啟可用性群組節點中的 hello 防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="2305e-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="2305e-158">建立 hello 可用性群組接聽程式</span><span class="sxs-lookup"><span data-stu-id="2305e-158">Create hello availability group listener</span></span>

<span data-ttu-id="2305e-159">兩個步驟建立 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2305e-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="2305e-160">首先，建立 hello 用戶端存取點叢集資源，並設定相依性。</span><span class="sxs-lookup"><span data-stu-id="2305e-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="2305e-161">第二，在 PowerShell 中設定 hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="2305e-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="2305e-162">建立 hello 用戶端存取點並設定 hello 叢集相依性</span><span class="sxs-lookup"><span data-stu-id="2305e-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="2305e-163">在 PowerShell 中設定 hello 叢集資源</span><span class="sxs-lookup"><span data-stu-id="2305e-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="2305e-164">對於 ILB，您必須使用 hello 的 hello 稍早建立的 ILB 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2305e-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="2305e-165">此 IP 位址在 PowerShell 中，使用下列指令碼的 hello tooobtain:</span><span class="sxs-lookup"><span data-stu-id="2305e-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="2305e-166">其中一個 hello Vm 上的作業系統 tooa 文字編輯器中，複製 hello PowerShell 指令碼，然後設定 hello 變數 toohello 您先前記下的值。</span><span class="sxs-lookup"><span data-stu-id="2305e-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="2305e-167">適用於 Windows Server 2012 或更新版本，請使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="2305e-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="2305e-168">Windows Server 2008 R2，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="2305e-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="2305e-169">設定 hello 的變數，開啟提升權限的 Windows PowerShell 視窗之後，貼上 hello 編寫指令碼從 hello 文字編輯器為您的 PowerShell 工作階段 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="2305e-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="2305e-170">如果 hello 提示依然顯示 **>>** ，按 Enter 鍵一次 toomake 確定 hello 指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="2305e-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="2305e-171">重複上述步驟，為每個 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="2305e-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="2305e-172">此指令碼以 hello hello 雲端服務 IP 位址設定 hello IP 位址資源，並設定其他參數，例如 hello 探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="2305e-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="2305e-173">當 hello IP 位址資源處於線上時，它可以回應 toohello 輪詢從 hello 負載平衡的端點，您稍早建立的 hello 探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="2305e-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="2305e-174">使 hello 接聽程式連線</span><span class="sxs-lookup"><span data-stu-id="2305e-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="2305e-175">待處理項目</span><span class="sxs-lookup"><span data-stu-id="2305e-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="2305e-176">測試 hello 可用性群組接聽程式 (在 hello 相同虛擬網路)</span><span class="sxs-lookup"><span data-stu-id="2305e-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="2305e-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2305e-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
