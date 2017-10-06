---
title: "aaaSimulated 混合式雲端測試環境 |Microsoft 文件"
description: "使用兩個 Azure 虛擬網路和 VNet 對 VNet 連接，建立 IT 專業或開發測試的模擬混合式雲端環境。"
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="362b7-103">設定用於測試的模擬混合式雲端環境</span><span class="sxs-lookup"><span data-stu-id="362b7-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="362b7-104">本文會引導您使用兩個 Azure 虛擬網路逐步建立 Microsoft Azure 的模擬混合式雲端環境。</span><span class="sxs-lookup"><span data-stu-id="362b7-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="362b7-105">以下是 hello 產生的設定。</span><span class="sxs-lookup"><span data-stu-id="362b7-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="362b7-106">這會模擬混合式雲端生產環境，其中包括：</span><span class="sxs-lookup"><span data-stu-id="362b7-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="362b7-107">模擬和簡化內部部署網路，裝載於 Azure 的虛擬網路 （hello 測試實驗室虛擬網路）。</span><span class="sxs-lookup"><span data-stu-id="362b7-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="362b7-108">Azure (TestVNET) 代管的模擬跨單位部署虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="362b7-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="362b7-109">Hello 兩個虛擬網路之間 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="362b7-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="362b7-110">Hello TestVNET 虛擬網路中第二個網域控制站。</span><span class="sxs-lookup"><span data-stu-id="362b7-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="362b7-111">這一般可供您開始：</span><span class="sxs-lookup"><span data-stu-id="362b7-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="362b7-112">在模擬混合式雲端環境中開發和測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="362b7-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="362b7-113">建立測試設定的電腦，一些 hello 測試實驗室的虛擬網路內，一些 hello TestVNET 虛擬網路內，toosimulate 混合式雲端 IT 工作負載。</span><span class="sxs-lookup"><span data-stu-id="362b7-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="362b7-114">有四個主要階段 toosetting 這個混合式雲端測試環境：</span><span class="sxs-lookup"><span data-stu-id="362b7-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="362b7-115">Hello 測試實驗室的虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="362b7-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="362b7-116">建立 hello 跨單位虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="362b7-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="362b7-117">建立 hello VNet 對 VNet VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="362b7-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="362b7-118">設定 DC2。</span><span class="sxs-lookup"><span data-stu-id="362b7-118">Configure DC2.</span></span> 

<span data-ttu-id="362b7-119">此組態需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="362b7-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="362b7-120">如果您有 MSDN 或 Visual Studio 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="362b7-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="362b7-121">Azure 中的虛擬機器和虛擬網路閘道會在執行時持續耗用成本。</span><span class="sxs-lookup"><span data-stu-id="362b7-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="362b7-122">這項成本是按照您的 MSDN 或付費訂用帳戶進行計算。</span><span class="sxs-lookup"><span data-stu-id="362b7-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="362b7-123">Azure VPN 閘道會實作為一組兩個的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="362b7-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="362b7-124">toominimize hello 成本，建立 hello 測試環境，並盡快執行您需要測試和示範。</span><span class="sxs-lookup"><span data-stu-id="362b7-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="362b7-125">階段 1： 設定測試實驗室虛擬網路時，hello</span><span class="sxs-lookup"><span data-stu-id="362b7-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="362b7-126">使用中 hello hello 指示[基本設定測試環境](https://technet.microsoft.com/library/mt771177.aspx)主題 tooconfigure hello DC1、 APP1 和 CLIENT1 電腦 hello Azure 虛擬網路，名為測試實驗室中的。</span><span class="sxs-lookup"><span data-stu-id="362b7-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="362b7-127">接下來，開啟 Azure PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="362b7-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="362b7-128">下列命令集的 hello 使用 Azure PowerShell 1.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="362b7-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="362b7-129">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="362b7-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="362b7-130">取得使用下列命令的 hello 您訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="362b7-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="362b7-131">設定您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="362b7-131">Set your Azure subscription.</span></span> <span data-ttu-id="362b7-132">使用 hello 相同訂用帳戶中所使用 toobuild 基底組態階段 1。</span><span class="sxs-lookup"><span data-stu-id="362b7-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="362b7-133">Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確的名稱。</span><span class="sxs-lookup"><span data-stu-id="362b7-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="362b7-134">接下來，加入基底組態，將會使用的 toohost hello Azure 閘道的閘道子網路 toohello 測試實驗室虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="362b7-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="362b7-135">接下來，要求的公用 IP 位址 tooassign toohello hello 測試實驗室虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="362b7-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="362b7-136">接下來，建立您的閘道器。</span><span class="sxs-lookup"><span data-stu-id="362b7-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="362b7-137">請注意，新的閘道可能需要 20 分鐘或更多 toocreate。</span><span class="sxs-lookup"><span data-stu-id="362b7-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="362b7-138">Hello Azure 入口網站，在本機電腦上，從連接 tooDC1 與 hello CORP\User1 認證。</span><span class="sxs-lookup"><span data-stu-id="362b7-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="362b7-139">tooconfigure hello CORP 網域，讓電腦和使用者使用其本機網域控制站進行驗證，執行這些命令從系統管理員層級 Windows PowerShell 命令提示字元在 DC1 上。</span><span class="sxs-lookup"><span data-stu-id="362b7-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="362b7-140">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="362b7-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="362b7-141">階段 2： 建立 hello TestVNET 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="362b7-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="362b7-142">首先，建立 hello TestVNET 虛擬網路，並保護與網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="362b7-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="362b7-143">接下來，要求的公用 IP 位址 toobe toohello 閘道配置 hello TestVNET 虛擬網路，並建立您的閘道。</span><span class="sxs-lookup"><span data-stu-id="362b7-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="362b7-144">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="362b7-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="362b7-145">階段 3： 建立 hello VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="362b7-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="362b7-146">首先，從您的網路或安全性管理員取得隨機且以強式密碼編譯之 32 個字元的預先共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="362b7-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="362b7-147">或者，使用在 hello 資訊[建立 IPsec 預先共用金鑰的隨機字串](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx)tooobtain 預先共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="362b7-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="362b7-148">接下來，使用這些命令 toocreate hello VNet 對 VNet VPN 連線，這可能要花費一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="362b7-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="362b7-149">在幾分鐘後應該要建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="362b7-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="362b7-150">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="362b7-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="362b7-151">第 4 階段：設定 DC2</span><span class="sxs-lookup"><span data-stu-id="362b7-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="362b7-152">首先，建立 DC2 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="362b7-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="362b7-153">Hello Azure PowerShell 命令提示字元執行這些命令在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="362b7-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="362b7-154">接下來，從 hello Azure 入口網站連接 toohello 新 DC2 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="362b7-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="362b7-155">接著，設定基本連線測試的 Windows 防火牆規則 tooallow 的流量。</span><span class="sxs-lookup"><span data-stu-id="362b7-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="362b7-156">從 DC2 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="362b7-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="362b7-157">四個來自 IP 位址 10.0.0.4 的成功回覆時產生 hello ping 命令。</span><span class="sxs-lookup"><span data-stu-id="362b7-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="362b7-158">這是資料傳輸的測試之間 hello VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="362b7-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="362b7-159">接下來，新增 hello 做為新的磁碟區與 hello 磁碟機代號 f: DC2 上額外的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="362b7-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="362b7-160">在 hello 左窗格的 伺服器管理員中，按一下 **檔案和存放服務**，然後按一下**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="362b7-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="362b7-161">在 hello 內容窗格中 hello**磁碟**群組中，按一下**磁碟 2** (以 hello**磁碟分割**設定得**未知**)。</span><span class="sxs-lookup"><span data-stu-id="362b7-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="362b7-162">按一下 工作，然後按一下新增磁碟區。</span><span class="sxs-lookup"><span data-stu-id="362b7-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="362b7-163">在 hello 開始 hello 新增磁碟區精靈頁面之前，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="362b7-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="362b7-164">在 hello 選取 hello 伺服器及磁碟 頁面上，按一下**磁碟 2**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="362b7-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="362b7-165">出現提示時，按一下 [新增功能] 架構藍圖。</span><span class="sxs-lookup"><span data-stu-id="362b7-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="362b7-166">在 hello 指定 hello 大小的 hello 磁碟區 頁面，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="362b7-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="362b7-167">在 hello 分派 tooa 磁碟機代號或資料夾 頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="362b7-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="362b7-168">Hello 選取檔案系統設定] 頁面上，按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="362b7-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="362b7-169">在 hello 確認選取項目頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="362b7-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="362b7-170">完成時，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="362b7-170">When complete, click **Close**.</span></span>

<span data-ttu-id="362b7-171">接下來，將 DC2 設定為複本網域控制站 hello corp.contoso.com 網域。</span><span class="sxs-lookup"><span data-stu-id="362b7-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="362b7-172">在 DC2 上，從 hello Windows PowerShell 命令提示字元執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="362b7-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="362b7-173">請注意，您都提示的 toosupply 兩者 hello CORP\User1 密碼的目錄服務還原模式 (DSRM) 密碼和 toorestart DC2。</span><span class="sxs-lookup"><span data-stu-id="362b7-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="362b7-174">既然 hello TestVNET 虛擬網路有自己的 DNS 伺服器 (DC2)，您必須設定 hello TestVNET 虛擬網路 toouse 此 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="362b7-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="362b7-175">Hello 左窗格中的 hello Azure 入口網站，按一下 hello 虛擬網路圖示，然後再按一下**TestVNET**。</span><span class="sxs-lookup"><span data-stu-id="362b7-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="362b7-176">在 hello**設定**索引標籤上，按一下  **DNS 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="362b7-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="362b7-177">在**主要 DNS 伺服器**，型別**已將 192.168.0.4** tooreplace 10.0.0.4。</span><span class="sxs-lookup"><span data-stu-id="362b7-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="362b7-178">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="362b7-178">Click **Save**.</span></span>

<span data-ttu-id="362b7-179">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="362b7-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="362b7-180">模擬混合式雲端環境到此準備就緒，可以進行測試。</span><span class="sxs-lookup"><span data-stu-id="362b7-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="362b7-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="362b7-181">Next step</span></span>
* <span data-ttu-id="362b7-182">在此環境中設定 [Web 型企業營運應用程式](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="362b7-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

