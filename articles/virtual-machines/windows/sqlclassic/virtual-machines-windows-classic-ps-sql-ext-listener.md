---
title: "aaaConfigure 外部 Alwayson 可用性群組接聽程式 |Microsoft 文件"
description: "此教學課程會逐步引導您完成在外部可存取所使用的 Azure 中建立一律在可用性群組接聽程式的步驟 hello 公用虛擬 IP 位址的 hello 相關聯的雲端服務。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="f4054-103">設定 Azure 中 Always On 可用性群組的外部接聽程式</span><span class="sxs-lookup"><span data-stu-id="f4054-103">Configure an external listener for Always On Availability Groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4054-104">內部接聽程式</span><span class="sxs-lookup"><span data-stu-id="f4054-104">Internal Listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="f4054-105">外部接聽程式</span><span class="sxs-lookup"><span data-stu-id="f4054-105">External Listener</span></span>](../classic/ps-sql-ext-listener.md)
> 
> 

<span data-ttu-id="f4054-106">本主題說明如何 tooconfigure Alwayson 可用性群組的外部存取上的接聽程式 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f4054-106">This topic shows you how tooconfigure a listener for an Always On Availability Group that is externally accessible on hello internet.</span></span> <span data-ttu-id="f4054-107">這樣做的原因產生關聯 hello 雲端服務的**公用虛擬 IP (VIP)** hello 接聽程式的位址。</span><span class="sxs-lookup"><span data-stu-id="f4054-107">This is made possible by associating hello cloud service's **public Virtual IP (VIP)** address with hello listener.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f4054-108">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f4054-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4054-109">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f4054-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f4054-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="f4054-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f4054-111">您的可用性群組可包含的複本為僅限內部部署、僅限 Azure，或同時跨內部部署和 Azure 的混合式組態。</span><span class="sxs-lookup"><span data-stu-id="f4054-111">Your Availability Group can contain replicas that are on-premises only, Azure only, or span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="f4054-112">Azure 複本可以位於 hello 相同區域或跨多個區域，使用多個虛擬網路 (Vnet)。</span><span class="sxs-lookup"><span data-stu-id="f4054-112">Azure replicas can reside within hello same region or across multiple regions using multiple virtual networks (VNets).</span></span> <span data-ttu-id="f4054-113">下列的 hello 步驟假設您已經有[設定可用性群組](../classic/portal-sql-alwayson-availability-groups.md)，但尚未設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f4054-113">hello steps below assume you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-external-listeners"></a><span data-ttu-id="f4054-114">外部接聽程式的指導方針和限制</span><span class="sxs-lookup"><span data-stu-id="f4054-114">Guidelines and limitations for external listeners</span></span>
<span data-ttu-id="f4054-115">請注意下列有關在 Azure 中的 hello 可用性群組接聽程式的指導方針，當您部署使用 hello 雲端服務公用 VIP 位址的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4054-115">Note hello following guidelines about hello availability group listener in Azure when you are deploying using hello cloud service pubic VIP address:</span></span>

* <span data-ttu-id="f4054-116">hello 可用性群組接聽程式都支援 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="f4054-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="f4054-117">hello 用戶端應用程式必須位於另一個則包含您的可用性群組 Vm 的 hello 不同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f4054-117">hello client application must reside on a different cloud service than hello one that contains your availability group VMs.</span></span> <span data-ttu-id="f4054-118">Azure 會支援伺服器直接傳回用戶端和伺服器 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f4054-118">Azure does not support direct server return with client and server in hello same cloud service.</span></span>
* <span data-ttu-id="f4054-119">根據預設，這篇文章中的 hello 步驟會顯示如何 tooconfigure 一個接聽程式 toouse hello 雲端服務的虛擬 IP (VIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="f4054-119">By default, hello steps in this article show how tooconfigure one listener toouse hello cloud service Virtual IP (VIP) address.</span></span> <span data-ttu-id="f4054-120">不過，它可能 tooreserve 而建立多個雲端服務的 VIP 位址。</span><span class="sxs-lookup"><span data-stu-id="f4054-120">However, it is possible tooreserve and create multiple VIP addresses for your cloud service.</span></span> <span data-ttu-id="f4054-121">這可讓您在此與不同的 VIP 相關聯的每個的多個接聽程式的發行項 toocreate toouse hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f4054-121">This enables you toouse hello steps in this article toocreate multiple listeners that are each associated with a different VIP.</span></span> <span data-ttu-id="f4054-122">如需有關如何 toocreate 多個 VIP 位址，請參閱詳細[每個雲端服務的多個 Vip](../../../load-balancer/load-balancer-multivip.md)。</span><span class="sxs-lookup"><span data-stu-id="f4054-122">For information on how toocreate multiple VIP addresses, see [Multiple VIPs per cloud service](../../../load-balancer/load-balancer-multivip.md).</span></span>
* <span data-ttu-id="f4054-123">如果您要建立混合式環境的接聽程式，hello 與內部網路必須有連線能力 toohello 在加法 toohello 公用網際網路以 hello Azure 虛擬網路的站台對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="f4054-123">If you are creating a listener for a hybrid environment, hello on-premises network must have connectivity toohello public Internet in addition toohello site-to-site VPN with hello Azure virtual network.</span></span> <span data-ttu-id="f4054-124">在 hello Azure 子網路，hello 可用性群組接聽程式連線到。 只有透過 hello 個別雲端服務的 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f4054-124">When in hello Azure subnet, hello availability group listener is reachable only by hello public IP address of hello respective cloud service.</span></span>
* <span data-ttu-id="f4054-125">不支援外部接聽程式在相同雲端的服務，您也可以使用的內部接聽程式的 hello toocreate hello 內部負載平衡 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="f4054-125">It is not supported toocreate an external listener in hello same cloud service where you also have an internal listener using hello Internal Load Balancer (ILB).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="f4054-126">判斷 hello hello 接聽程式的協助工具</span><span class="sxs-lookup"><span data-stu-id="f4054-126">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="f4054-127">本文著重於建立使用 **外部負載平衡**的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f4054-127">This article focuses on creating a listener that uses **external load balancing**.</span></span> <span data-ttu-id="f4054-128">如果您想要的接聽程式是私用 tooyour 虛擬網路，請參閱提供的步驟設定這篇文章 hello 版本[搭配 ILB 一起運作的接聽程式](../classic/ps-sql-int-listener.md)</span><span class="sxs-lookup"><span data-stu-id="f4054-128">If you want a listener that is private tooyour virtual network, see hello version of this article that provides steps for setting up an [listener with ILB](../classic/ps-sql-int-listener.md)</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="f4054-129">使用伺服器直接回傳建立負載平衡 VM 端點</span><span class="sxs-lookup"><span data-stu-id="f4054-129">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="f4054-130">外部負載平衡使用 hello 虛擬 hello 公用虛擬 IP 位址的 hello 裝載 Vm 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f4054-130">External load balancing uses hello virtual hello public Virtual IP address of hello cloud service that hosts your VMs.</span></span> <span data-ttu-id="f4054-131">因此您不需要 toocreate 或 hello 負載平衡器設定在此情況下。</span><span class="sxs-lookup"><span data-stu-id="f4054-131">So you do not need toocreate or configure hello load balancer in this case.</span></span>

<span data-ttu-id="f4054-132">您必須為每個主控 Azure 複本的 VM 建立負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="f4054-132">You must create a load-balanced endpoint for each VM hosting an Azure replica.</span></span> <span data-ttu-id="f4054-133">如果您在多個地區複本，每個複本用於該區域檔案必須在相同雲端服務中的 hello hello 相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="f4054-133">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same VNet.</span></span> <span data-ttu-id="f4054-134">建立跨越多個 Azure 區域的可用性群組複本需要設定多個 VNet。</span><span class="sxs-lookup"><span data-stu-id="f4054-134">Creating Availability Group replicas that span multiple Azure regions requires configuring multiple VNets.</span></span> <span data-ttu-id="f4054-135">如需有關設定跨 VNet 連線的詳細資訊，請參閱[設定 VNet tooVNet 連線](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="f4054-135">For more information on configuring cross VNet connectivity, see  [Configure VNet tooVNet Connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="f4054-136">在 hello Azure 入口網站，瀏覽 tooeach VM 裝載的複本和檢視 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f4054-136">In hello Azure portal, navigate tooeach VM hosting a replica and view hello details.</span></span>
2. <span data-ttu-id="f4054-137">按一下 hello**端點**hello Vm 的每個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f4054-137">Click hello **Endpoints** tab for each of hello VMs.</span></span>
3. <span data-ttu-id="f4054-138">請確認該 hello**名稱**和**公用連接埠**您想要的 hello 接聽程式端點 toouse 已不在使用。</span><span class="sxs-lookup"><span data-stu-id="f4054-138">Verify that hello **Name** and **Public Port** of hello listener endpoint you want toouse is not already in use.</span></span> <span data-ttu-id="f4054-139">Hello 下列範例中，在 hello 名稱是"MyEndpoint"而 hello 通訊埠是"1433"。</span><span class="sxs-lookup"><span data-stu-id="f4054-139">In hello example below, hello name is “MyEndpoint” and hello port is “1433”.</span></span>
4. <span data-ttu-id="f4054-140">在您的本機用戶端上下載並安裝[hello 最新的 PowerShell 模組](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="f4054-140">On your local client, download and install [hello latest PowerShell module](https://azure.microsoft.com/downloads/).</span></span>
5. <span data-ttu-id="f4054-141">啟動 **Azure PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="f4054-141">Launch **Azure PowerShell**.</span></span> <span data-ttu-id="f4054-142">新的 PowerShell 工作階段隨即開啟與 hello Azure 系統管理模組載入。</span><span class="sxs-lookup"><span data-stu-id="f4054-142">A new PowerShell session is opened with hello Azure administrative modules loaded.</span></span>
6. <span data-ttu-id="f4054-143">執行 **Get-AzurePublishSettingsFile**。</span><span class="sxs-lookup"><span data-stu-id="f4054-143">Run **Get-AzurePublishSettingsFile**.</span></span> <span data-ttu-id="f4054-144">這個指令程式會將您導向 tooa 瀏覽器 toodownload 發行設定檔案 tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="f4054-144">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="f4054-145">系統可能會提示您輸入 Azure 訂用帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="f4054-145">You may be prompted for your log-in credentials for your Azure subscription.</span></span>
7. <span data-ttu-id="f4054-146">執行 hello **Import-azurepublishsettingsfile** hello hello 路徑的命令發行您所下載的設定檔：</span><span class="sxs-lookup"><span data-stu-id="f4054-146">Run hello **Import-AzurePublishSettingsFile** command with hello path of hello publish settings file that you downloaded:</span></span>
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    <span data-ttu-id="f4054-147">Hello 發行設定檔匯入，您可以管理您的 Azure 訂閱 hello PowerShell 工作階段中。</span><span class="sxs-lookup"><span data-stu-id="f4054-147">Once hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>
    
1. <span data-ttu-id="f4054-148">將以下 hello PowerShell 指令碼複製到文字編輯器，並設定 hello 變數值 toosuit 環境 （某些參數已提供預設值）。</span><span class="sxs-lookup"><span data-stu-id="f4054-148">Copy hello PowerShell script below into a text editor and set hello variable values toosuit your environment (defaults have been provided for some parameters).</span></span> <span data-ttu-id="f4054-149">請注意，是否您的可用性群組跨越 Azure 地區，您必須執行 hello 指令碼一次每個資料中心 hello 雲端服務和位於該資料中心的節點。</span><span class="sxs-lookup"><span data-stu-id="f4054-149">Note that if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. <span data-ttu-id="f4054-150">一旦您已經設定 hello 變數，複製 hello 編寫指令碼從 hello 文字編輯器為您的 Azure PowerShell 工作階段 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="f4054-150">Once you have set hello variables, copy hello script from hello text editor into your Azure PowerShell session toorun it.</span></span> <span data-ttu-id="f4054-151">如果 hello 提示依然顯示 >>，輸入的 ENTER 再次 toomake 確定 hello 指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="f4054-151">If hello prompt still shows >>, type ENTER again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="f4054-152">必要時，請確認已安裝 KB2854082</span><span class="sxs-lookup"><span data-stu-id="f4054-152">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="f4054-153">開啟可用性群組節點中的 hello 防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="f4054-153">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="f4054-154">建立 hello 可用性群組接聽程式</span><span class="sxs-lookup"><span data-stu-id="f4054-154">Create hello availability group listener</span></span>

<span data-ttu-id="f4054-155">兩個步驟建立 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f4054-155">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="f4054-156">首先，建立 hello 用戶端存取點叢集資源，並設定相依性。</span><span class="sxs-lookup"><span data-stu-id="f4054-156">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="f4054-157">其次，使用 PowerShell 設定 hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="f4054-157">Second, configure hello cluster resources with PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="f4054-158">建立 hello 用戶端存取點並設定 hello 叢集相依性</span><span class="sxs-lookup"><span data-stu-id="f4054-158">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="f4054-159">在 PowerShell 中設定 hello 叢集資源</span><span class="sxs-lookup"><span data-stu-id="f4054-159">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="f4054-160">外部負載平衡，您必須取得 hello 公用虛擬 IP 位址的 hello 雲端服務，其中包含您的複本。</span><span class="sxs-lookup"><span data-stu-id="f4054-160">For external load balancing, you must obtain hello public virtual IP address of hello cloud service that contains your replicas.</span></span> <span data-ttu-id="f4054-161">登入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f4054-161">Log into hello Azure portal.</span></span> <span data-ttu-id="f4054-162">瀏覽 toohello 包含您的可用性群組 VM 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f4054-162">Navigate toohello cloud service that contains your availability group VM.</span></span> <span data-ttu-id="f4054-163">開啟 hello**儀表板**檢視。</span><span class="sxs-lookup"><span data-stu-id="f4054-163">Open hello **Dashboard** view.</span></span>
2. <span data-ttu-id="f4054-164">請注意下方顯示 hello 位址**公用虛擬 IP (VIP) 位址**。</span><span class="sxs-lookup"><span data-stu-id="f4054-164">Note hello address shown under **Public Virtual IP (VIP) Address**.</span></span> <span data-ttu-id="f4054-165">如果您的解決方案跨越多個 VNet，請針對包含主控複本之 VM 的每個雲端服務重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="f4054-165">If your solution spans VNets, repeat this step for each cloud service that contains a VM that hosts a replica.</span></span>
3. <span data-ttu-id="f4054-166">其中一個 hello Vm 上 hello 以下 PowerShell 指令碼複製到文字編輯器並設定 hello 變數 toohello 您先前記下的值。</span><span class="sxs-lookup"><span data-stu-id="f4054-166">On one of hello VMs, copy hello PowerShell script below into a text editor and set hello variables toohello values you noted earlier.</span></span>
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. <span data-ttu-id="f4054-167">之後設定 hello 變數，開啟提升權限的 Windows PowerShell 視窗，然後複製 hello 文字編輯器中的 hello 指令碼並貼到您的 Azure PowerShell 工作階段 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="f4054-167">Once you have set hello variables, open an elevated Windows PowerShell window, then copy hello script from hello text editor and paste into your Azure PowerShell session toorun it.</span></span> <span data-ttu-id="f4054-168">如果 hello 提示依然顯示 >>，輸入的 ENTER 再次 toomake 確定 hello 指令碼開始執行。</span><span class="sxs-lookup"><span data-stu-id="f4054-168">If hello prompt still shows >>, type ENTER again toomake sure hello script starts running.</span></span>
5. <span data-ttu-id="f4054-169">在每個 VM 上重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="f4054-169">Repeat this on each VM.</span></span> <span data-ttu-id="f4054-170">此指令碼與 hello hello 雲端服務 IP 位址設定 hello IP 位址資源，並且設定類似 hello 探查連接埠其他參數。</span><span class="sxs-lookup"><span data-stu-id="f4054-170">This script configures hello IP Address resource with hello IP address of hello cloud service and sets other parameters like hello probe port.</span></span> <span data-ttu-id="f4054-171">當 hello IP 位址資源處於線上時，它可以回應 toohello 輪詢 hello 從稍早在本教學課程中建立的 hello 負載平衡端點的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="f4054-171">When hello IP Address resource is brought online, it can then respond toohello polling on hello probe port from hello load-balanced endpoint created earlier in this tutorial.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="f4054-172">使 hello 接聽程式連線</span><span class="sxs-lookup"><span data-stu-id="f4054-172">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="f4054-173">待處理項目</span><span class="sxs-lookup"><span data-stu-id="f4054-173">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a><span data-ttu-id="f4054-174">測試 hello 可用性群組接聽程式 (在 hello 相同 VNet)</span><span class="sxs-lookup"><span data-stu-id="f4054-174">Test hello availability group listener (within hello same VNet)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a><span data-ttu-id="f4054-175">測試 hello 可用性群組接聽程式 (透過 hello 網際網路)</span><span class="sxs-lookup"><span data-stu-id="f4054-175">Test hello availability group listener (over hello internet)</span></span>
<span data-ttu-id="f4054-176">在順序從外部 hello 虛擬網路的 tooaccess hello 接聽程式，您必須使用外部/公用負載平衡 （如本主題所述） 而不 ILB，也就是只在 hello 內存取相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="f4054-176">In order tooaccess hello listener from outside hello virtual network, you must be using external/public load balancing (described in this topic) rather than ILB, which is only accesible within hello same VNet.</span></span> <span data-ttu-id="f4054-177">在 hello 連接字串中，您可以指定 hello 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="f4054-177">In hello connection string, you specify hello cloud service name.</span></span> <span data-ttu-id="f4054-178">例如，如果您擁有 hello 名稱的雲端服務*mycloudservice*，hello sqlcmd 陳述式將如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4054-178">For example, if you had a cloud service with hello name *mycloudservice*, hello sqlcmd statement would be as follows:</span></span>

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

<span data-ttu-id="f4054-179">與 hello 上述範例中，不同的是 SQL 驗證必須使用，因為 hello 呼叫端無法使用 windows 驗證透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f4054-179">Unlike hello previous example, SQL authentication must be used, because hello caller cannot use windows authentication over hello internet.</span></span> <span data-ttu-id="f4054-180">如需詳細資訊，請參閱 [Azure VM 中的 Always On 可用性群組：用戶端連線能力情況](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f4054-180">For more information, see [Always On Availability Group in Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx).</span></span> <span data-ttu-id="f4054-181">使用 SQL 驗證時，請確定您建立 hello 兩個複本上的相同登入。</span><span class="sxs-lookup"><span data-stu-id="f4054-181">When using SQL authentication, make sure that you create hello same login on both replicas.</span></span> <span data-ttu-id="f4054-182">如需疑難排解與可用性群組的登入的詳細資訊，請參閱[toomap 登入或使用包含 SQL 資料庫使用者 tooconnect tooother 複本和對應 tooavailability 資料庫](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f4054-182">For more information about troubleshooting logins with Availability Groups, see [How toomap logins or use contained SQL database user tooconnect tooother replicas and map tooavailability databases](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).</span></span>

<span data-ttu-id="f4054-183">如果 hello Alwayson 複本位於不同子網路中，用戶端必須指定**MultisubnetFailover = True** hello 連接字串中。</span><span class="sxs-lookup"><span data-stu-id="f4054-183">If hello Always On replicas are in different subnets, clients must specify **MultisubnetFailover=True** in hello connection string.</span></span> <span data-ttu-id="f4054-184">這會導致平行連接嘗試 tooreplicas hello 不同子網路中。</span><span class="sxs-lookup"><span data-stu-id="f4054-184">This results in parallel connection attempts tooreplicas in hello different subnets.</span></span> <span data-ttu-id="f4054-185">請注意，此情況包含跨區域的 Always On 可用性群組部署。</span><span class="sxs-lookup"><span data-stu-id="f4054-185">Note that this scenario includes a cross-region Always On Availability Group deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4054-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4054-186">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

