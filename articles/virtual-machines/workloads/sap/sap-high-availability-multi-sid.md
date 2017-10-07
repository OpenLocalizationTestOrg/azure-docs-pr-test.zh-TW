---
title: "在 Azure 中 SAP 多 SID 組態 aaaCreate |Microsoft 文件"
description: "指南 toohigh 可用性的 SAP NetWeaver Windows 虛擬機器上的多重 SID 組態"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>建立 SAP NetWeaver 多 SID 組態

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

Microsoft 在 2016 年 9 月發行的功能，可讓您使用 Azure 內部負載平衡器管理多個虛擬 IP 位址。 這項功能已存在於 hello Azure 外部負載平衡器。

如果您有 SAP 部署時，您可以使用內部負載平衡器 toocreate Windows 叢集組態中的 SAP ASCS/SCS，述 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][ sap-ha-guide].

本文著重在從單一 ASCS/SCS 安裝 tooan SAP 多 SID 組態藉由安裝其他 SAP ASCS/SCS toomove 到現有的 Windows Server 容錯移轉叢集 (WSFC) 叢集中叢集執行個體的方式。 完成此程序之後，您將已設定 SAP 多 SID 叢集。


## <a name="prerequisites"></a>必要條件
您已經設定 WSFC 叢集中使用一個 SAP ASCS/SCS 執行個體，請如所述 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][ sap-ha-guide]和此圖表中所示。

![高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>目標架構

hello 的目標是的 tooinstall 多個 SAP ABAP ASCS 或 SAP Java SCS 叢集執行個體 hello 相同 WSFC 叢集中，如下圖所示：

![Azure 中多個 SAP ASCS/SCS 叢集執行個體][sap-ha-guide-figure-6002]

> [!NOTE]
>沒有為每個 Azure 內部負載平衡器的私用前端 Ip 限制 toohello 數目。
>
>hello 一個 WSFC 叢集中的 SAP ASCS/SCS 執行個體數目上限是相等的 toohello 的每個 Azure 內部負載平衡器的私用前端 Ip 數目上限。
>

如需更多有關負載平衡器限制的資訊，請參閱[網路限制：Azure Resource Manager][networking-limits-azure-resource-manager] 中的「每個負載平衡器的私人前端 IP」。

hello 與兩個高可用性的 SAP 系統的完整說明看起來會像這樣：

![具有兩個 SAP 系統 SID 的 SAP 高可用性多 SID 設定][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> hello 安裝程式必須符合下列條件的 hello:
> - hello SAP ASCS/SCS 執行個體必須共用 hello 相同 WSFC 叢集。
> - 每個 DBMS SID 必須有其自己專用的 WSFC 叢集。
> - 屬於 tooone SAP 系統 SID 的 SAP 應用程式伺服器必須有自己專用的 Vm。


## <a name="prepare-hello-infrastructure"></a>準備 hello 基礎結構
tooprepare 您基礎結構，您可以使用下列參數的 hello 安裝額外的 SAP ASCS/SCS 執行個體：

| 參數名稱 | 值 |
| --- | --- |
| SAP ASCS/SCS SID |pr1-lb-ascs |
| SAP DBMS 內部負載平衡器 | PR5 |
| SAP 虛擬主機名稱 | pr5-sap-cl |
| SAP ASCS/SCS 虛擬主機 IP 位址 (其他 Azure Load Balancer IP 位址) | 10.0.0.50 |
| SAP ASCS/SCS 執行個體號碼 | 50 |
| 其他 SAP ASCS/SCS 執行個體的 ILB 探查連接埠 | 62350 |

> [!NOTE]
> 對於 SAP ASCS/SCS 叢集執行個體，每個 IP 位址需要唯一的探查連接埠。 例如，如果 Azure 內部負載平衡器上有一個 IP 位址使用探查連接埠 62300，該負載平衡器上的任何其他 IP 位址就不能使用探查連接埠 62300。
>
>針對本文目的，因為已保留探查連接埠 62300，我們會使用探查連接埠 62350。

您可以在 hello 現有 WSFC 叢集包含兩個節點中安裝額外的 SAP ASCS/SCS 執行個體：

| 虛擬機器角色 | 虛擬機器主機名稱 | 靜態 IP 位址 |
| --- | --- | --- |
| ASCS/SCS 執行個體的第 1 個叢集節點 |pr1-ascs-0 |10.0.0.10 |
| ASCS/SCS 執行個體的第 2 個叢集節點 |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Hello DNS 伺服器上建立叢集的 hello SAP ASCS/SCS 執行個體的虛擬主機名稱

您可以使用下列參數的 hello 建立 hello hello ASCS/SCS 執行個體的虛擬主機名稱的 DNS 項目：

| 新的 SAP ASCS/SCS 虛擬主機名稱 | 相關聯的 IP 位址 |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

hello 新的主機名稱和 IP 位址會顯示 hello DNS 管理員 中，在 hello 下列螢幕擷取畫面所示：

![DNS 管理員 清單中反白顯示 hello 定義 hello 新 SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-6004]

建立 DNS 項目 hello 程序也說明 hello 主要詳細[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-9.1.1]。

> [!NOTE]
> hello 您指派 toohello hello 其他 ASCS/SCS 執行個體的虛擬主機名稱的新 IP 位址必須是 hello 與 hello 新的 IP 位址指派給 toohello SAP 的 Azure 負載平衡器相同。
>
>在我們的案例所 10.0.0.50 hello IP 位址。

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>使用 PowerShell 新增 IP 位址 tooan 現有 Azure 內部負載平衡器

以上一個 SAP ASCS/SCS 執行個體中的 toocreate hello 相同 WSFC 叢集，請使用 PowerShell tooadd 現有 Azure 內部負載平衡器 IP 位址 tooan。 每個 IP 位址都需要有自己的負載平衡規則、探查連接埠、前端 IP 集區和後端集區。

hello 下列指令碼會新增新 IP 位址 tooan 現有負載平衡器。 更新您的環境的 hello PowerShell 變數。 hello 指令碼會建立所需的所有負載平衡規則的所有 SAP ASCS/SCS 連接埠。

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
Hello 指令碼執行之後，結果會顯示在 hello hello Azure 入口網站，hello 下列螢幕擷取畫面所示：

![前端 IP 集區中 hello Azure 入口網站][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>新增磁碟 toocluster 機器，並設定 hello SIOS 叢集共用磁碟

對於每個額外 SAP ASCS/SCS 執行個體，您必須新增叢集共用磁碟。 Windows Server 2012 R2，hello WSFC 叢集共用磁碟目前正在使用中的 hello SIOS DataKeeper 軟體解決方案。

請勿 hello 遵循：
1. 新增其他磁碟或磁碟的 hello 相同的大小 (您需要 toostripe) tooeach hello 的叢集節點，然後將它們格式化。
2. 使用 SIOS DataKeeper 設定儲存體複寫。

此程序假設您已經有安裝 SIOS DataKeeper hello WSFC 叢集的電腦上。 如果您已安裝它，您現在必須設定 hello 機器之間的複寫。 hello 程序中有詳細說明在 hello 主要[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-8.12.3.3]。  

![DataKeeper 同步鏡像 hello 新 SAP ASCS/SCS 共用磁碟][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>針對 SAP 應用程式伺服器和 DBMS 叢集部署 VM

第二個 SAP 系統 hello，toocomplete hello 基礎結構準備 hello 遵循：

1. 為 SAP 應用程式伺服器部署專用 VM，並將它們放在其自己專用的可用性群組。
2. 為 DBMS 叢集部署專用 VM，並將它們放在其自己專用的可用性群組。


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>安裝第二個 SID2 的 SAP NetWeaver 系統 hello

hello 安裝的第二個 SAP SID2 系統的完整程序所述 hello 主要[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-9]。

hello 高階程序如下所示：

1. [安裝 hello SAP 第一個叢集節點][sap-ha-guide-9.1.2]。  
 在此步驟中，您要安裝 SAP 與高可用性 ASCS/SCS 執行個體上 hello**現有的 WSFC 叢集節點 1**。

2. [修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔][sap-ha-guide-9.1.3]。

3. [設定探查連接埠][sap-ha-guide-9.1.4]。  
 在此步驟中，您要使用 PowerShell 設定 SAP 叢集資源 SAP SID2 IP 探查連接埠。 其中一個 hello SAP ASCS/SCS 叢集節點上執行這項設定。

4. [安裝 hello 資料庫執行個體][sap-ha-快速入門-9.2]。  
 在此步驟中，您要在專用的 WSFC 叢集上安裝 DBMS。

5. [安裝 hello 第二個叢集節點][sap-ha-快速入門-9.3]。  
 在此步驟中，您要安裝 SAP 與現有 WSFC 叢集節點 hello 2 上的高可用性 ASCS/SCS 執行個體。

6. 開啟 Windows 防火牆連接埠 hello SAP ASCS/SCS 執行個體或甚至 ProbePort。  
 在用於 SAP ASCS/SCS 執行個體的兩個叢集節點上，您要開啟 SAP ASCS/SCS 所使用的所有 Windows 防火牆連接埠。 這些連接埠會列在 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-8.8]。  
 也開啟 hello Azure 內部負載平衡器探查連接埠，也就是 62350 在我們的案例。

7. [變更 hello hello SAP 端 Windows 服務執行個體的啟動類型][sap-ha-guide-9.4]。

8. [安裝 hello SAP 主應用程式伺服器][ sap-ha-guide-9.5]上新的 hello 專用 VM。

9. [安裝 hello SAP 其他應用程式伺服器][ sap-ha-guide-9.6]上新的 hello 專用 VM。

10. [測試 hello SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫][sap-ha-guide-10]。

## <a name="next-steps"></a>後續步驟

- [網路限制：Azure Resource Manager][networking-limits-azure-resource-manager]
- [Azure Load Balancer 的多個 VIP][load-balancer-multivip-overview]
- [Windows VM 上的 SAP NetWeaver 高可用性指南][sap-ha-guide]
