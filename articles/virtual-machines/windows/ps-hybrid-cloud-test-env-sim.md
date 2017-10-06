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
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>設定用於測試的模擬混合式雲端環境
本文會引導您使用兩個 Azure 虛擬網路逐步建立 Microsoft Azure 的模擬混合式雲端環境。 以下是 hello 產生的設定。

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

這會模擬混合式雲端生產環境，其中包括：

* 模擬和簡化內部部署網路，裝載於 Azure 的虛擬網路 （hello 測試實驗室虛擬網路）。
* Azure (TestVNET) 代管的模擬跨單位部署虛擬網路。
* Hello 兩個虛擬網路之間 VNet 對 VNet 連線。
* Hello TestVNET 虛擬網路中第二個網域控制站。

這一般可供您開始：

* 在模擬混合式雲端環境中開發和測試應用程式。
* 建立測試設定的電腦，一些 hello 測試實驗室的虛擬網路內，一些 hello TestVNET 虛擬網路內，toosimulate 混合式雲端 IT 工作負載。

有四個主要階段 toosetting 這個混合式雲端測試環境：

1. Hello 測試實驗室的虛擬網路設定。
2. 建立 hello 跨單位虛擬網路。
3. 建立 hello VNet 對 VNet VPN 連線。
4. 設定 DC2。 

此組態需要 Azure 訂用帳戶。 如果您有 MSDN 或 Visual Studio 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。

> [!NOTE]
> Azure 中的虛擬機器和虛擬網路閘道會在執行時持續耗用成本。 這項成本是按照您的 MSDN 或付費訂用帳戶進行計算。 Azure VPN 閘道會實作為一組兩個的 Azure 虛擬機器。 toominimize hello 成本，建立 hello 測試環境，並盡快執行您需要測試和示範。
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>階段 1： 設定測試實驗室虛擬網路時，hello
使用中 hello hello 指示[基本設定測試環境](https://technet.microsoft.com/library/mt771177.aspx)主題 tooconfigure hello DC1、 APP1 和 CLIENT1 電腦 hello Azure 虛擬網路，名為測試實驗室中的。 

接下來，開啟 Azure PowerShell 提示字元。

> [!NOTE]
> 下列命令集的 hello 使用 Azure PowerShell 1.0 和更新版本。
> 
> 

登入 tooyour 帳戶。

    Login-AzureRMAccount

取得使用下列命令的 hello 您訂用帳戶名稱。

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

設定您的 Azure 訂用帳戶 使用 hello 相同訂用帳戶中所使用 toobuild 基底組態階段 1。 Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確的名稱。

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

接下來，加入基底組態，將會使用的 toohost hello Azure 閘道的閘道子網路 toohello 測試實驗室虛擬網路。

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

接下來，要求的公用 IP 位址 tooassign toohello hello 測試實驗室虛擬網路閘道。

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

接下來，建立您的閘道器。

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

請注意，新的閘道可能需要 20 分鐘或更多 toocreate。

Hello Azure 入口網站，在本機電腦上，從連接 tooDC1 與 hello CORP\User1 認證。 tooconfigure hello CORP 網域，讓電腦和使用者使用其本機網域控制站進行驗證，執行這些命令從系統管理員層級 Windows PowerShell 命令提示字元在 DC1 上。

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>階段 2： 建立 hello TestVNET 虛擬網路
首先，建立 hello TestVNET 虛擬網路，並保護與網路安全性群組。

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

接下來，要求的公用 IP 位址 toobe toohello 閘道配置 hello TestVNET 虛擬網路，並建立您的閘道。

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>階段 3： 建立 hello VNet 對 VNet 連線
首先，從您的網路或安全性管理員取得隨機且以強式密碼編譯之 32 個字元的預先共用金鑰。 或者，使用在 hello 資訊[建立 IPsec 預先共用金鑰的隨機字串](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx)tooobtain 預先共用金鑰。

接下來，使用這些命令 toocreate hello VNet 對 VNet VPN 連線，這可能要花費一些時間 toocomplete。

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

在幾分鐘後應該要建立 hello 連線。

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>第 4 階段：設定 DC2
首先，建立 DC2 的虛擬機器。 Hello Azure PowerShell 命令提示字元執行這些命令在本機電腦上。

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

接下來，從 hello Azure 入口網站連接 toohello 新 DC2 的虛擬機器。

接著，設定基本連線測試的 Windows 防火牆規則 tooallow 的流量。 從 DC2 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

四個來自 IP 位址 10.0.0.4 的成功回覆時產生 hello ping 命令。 這是資料傳輸的測試之間 hello VNet 對 VNet 連線。

接下來，新增 hello 做為新的磁碟區與 hello 磁碟機代號 f: DC2 上額外的資料磁碟。

1. 在 hello 左窗格的 伺服器管理員中，按一下 **檔案和存放服務**，然後按一下**磁碟**。
2. 在 hello 內容窗格中 hello**磁碟**群組中，按一下**磁碟 2** (以 hello**磁碟分割**設定得**未知**)。
3. 按一下 工作，然後按一下新增磁碟區。
4. 在 hello 開始 hello 新增磁碟區精靈頁面之前，請按一下**下一步**。
5. 在 hello 選取 hello 伺服器及磁碟 頁面上，按一下**磁碟 2**，然後按一下**下一步**。 出現提示時，按一下 [新增功能] 架構藍圖。
6. 在 hello 指定 hello 大小的 hello 磁碟區 頁面，按一下 **下一步**。
7. 在 hello 分派 tooa 磁碟機代號或資料夾 頁面上，按一下 **下一步**。
8. Hello 選取檔案系統設定] 頁面上，按一下 [**下一步**。
9. 在 hello 確認選取項目頁面上，按一下 **建立**。
10. 完成時，按一下 [關閉] 。

接下來，將 DC2 設定為複本網域控制站 hello corp.contoso.com 網域。 在 DC2 上，從 hello Windows PowerShell 命令提示字元執行這些命令。

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

請注意，您都提示的 toosupply 兩者 hello CORP\User1 密碼的目錄服務還原模式 (DSRM) 密碼和 toorestart DC2。

既然 hello TestVNET 虛擬網路有自己的 DNS 伺服器 (DC2)，您必須設定 hello TestVNET 虛擬網路 toouse 此 DNS 伺服器。

1. Hello 左窗格中的 hello Azure 入口網站，按一下 hello 虛擬網路圖示，然後再按一下**TestVNET**。
2. 在 hello**設定**索引標籤上，按一下  **DNS 伺服器**。
3. 在**主要 DNS 伺服器**，型別**已將 192.168.0.4** tooreplace 10.0.0.4。
4. 按一下 [儲存] 。

這是您目前的組態。 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

模擬混合式雲端環境到此準備就緒，可以進行測試。

## <a name="next-step"></a>後續步驟
* 在此環境中設定 [Web 型企業營運應用程式](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

