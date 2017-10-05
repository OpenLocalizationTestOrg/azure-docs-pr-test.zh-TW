---
title: "在 Azure 中建立 SAP 多 SID 組態 | Microsoft Docs"
description: "Windows 虛擬機器上的 SAP NetWeaver 多 SID 組態的高可用性指南"
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
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="296d9-103">建立 SAP NetWeaver 多 SID 組態</span><span class="sxs-lookup"><span data-stu-id="296d9-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="296d9-104">Microsoft 在 2016 年 9 月發行的功能，可讓您使用 Azure 內部負載平衡器管理多個虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="296d9-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="296d9-105">這項功能已存在 Azure 外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="296d9-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="296d9-106">如果您有 SAP 部署，可以使用內部負載平衡器針對 SAP 的 ASCS/SCS 建立 Windows 叢集組態，如 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide]所述。</span><span class="sxs-lookup"><span data-stu-id="296d9-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="296d9-107">本文將著重於如何將單一 ASCS/SCS 安裝移至 SAP 多 SID 組態，方法是將其他 SAP ASCS/SCS 叢集執行個體安裝至現有 Windows Server 容錯移轉叢集 (WSFC) 叢集。</span><span class="sxs-lookup"><span data-stu-id="296d9-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="296d9-108">完成此程序之後，您將已設定 SAP 多 SID 叢集。</span><span class="sxs-lookup"><span data-stu-id="296d9-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="296d9-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="296d9-109">Prerequisites</span></span>
<span data-ttu-id="296d9-110">您已經設定用於一個 SAP ASCS/SCS 執行個體的 WSFC 叢集，如 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide]所述及如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="296d9-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="296d9-112">目標架構</span><span class="sxs-lookup"><span data-stu-id="296d9-112">Target architecture</span></span>

<span data-ttu-id="296d9-113">目標是在相同 WSAFC 叢集中安裝多個 SAP ABAP ASCS 或 SAP Java SCS 叢集執行個體，如這裡所詳述：</span><span class="sxs-lookup"><span data-stu-id="296d9-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Azure 中多個 SAP ASCS/SCS 叢集執行個體][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="296d9-115">每個 Azure 內部負載平衡器的私人前端 IP 有數量限制。</span><span class="sxs-lookup"><span data-stu-id="296d9-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="296d9-116">一個 WSFC 叢集中 SAP ASCS/SCS 執行個體數目上限等於每個 Azure 內部負載平衡器的私人前端 IP 數目上限。</span><span class="sxs-lookup"><span data-stu-id="296d9-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="296d9-117">如需更多有關負載平衡器限制的資訊，請參閱[網路限制：Azure Resource Manager][networking-limits-azure-resource-manager] 中的「每個負載平衡器的私人前端 IP」。</span><span class="sxs-lookup"><span data-stu-id="296d9-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="296d9-118">具有兩個高度可用 SAP 系統的完整配置畫面如下所示：</span><span class="sxs-lookup"><span data-stu-id="296d9-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![具有兩個 SAP 系統 SID 的 SAP 高可用性多 SID 設定][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="296d9-120">安裝程式必須符合下列條件︰</span><span class="sxs-lookup"><span data-stu-id="296d9-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="296d9-121">SAP ASCS / SCS 執行個體必須共用相同的 WSFC 叢集。</span><span class="sxs-lookup"><span data-stu-id="296d9-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="296d9-122">每個 DBMS SID 必須有其自己專用的 WSFC 叢集。</span><span class="sxs-lookup"><span data-stu-id="296d9-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="296d9-123">SAP 應用程式伺服器屬於必須擁有自己專用 VM 的一個 SAP 系統 SID。</span><span class="sxs-lookup"><span data-stu-id="296d9-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="296d9-124">準備基礎結構</span><span class="sxs-lookup"><span data-stu-id="296d9-124">Prepare the infrastructure</span></span>
<span data-ttu-id="296d9-125">若要準備您的基礎結構，您可以安裝額外的 SAP ASCS/SCS 執行個體，並使用下列參數︰</span><span class="sxs-lookup"><span data-stu-id="296d9-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="296d9-126">參數名稱</span><span class="sxs-lookup"><span data-stu-id="296d9-126">Parameter name</span></span> | <span data-ttu-id="296d9-127">值</span><span class="sxs-lookup"><span data-stu-id="296d9-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="296d9-128">SAP ASCS/SCS SID</span><span class="sxs-lookup"><span data-stu-id="296d9-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="296d9-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="296d9-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="296d9-130">SAP DBMS 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="296d9-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="296d9-131">PR5</span><span class="sxs-lookup"><span data-stu-id="296d9-131">PR5</span></span> |
| <span data-ttu-id="296d9-132">SAP 虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="296d9-132">SAP virtual host name</span></span> | <span data-ttu-id="296d9-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="296d9-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="296d9-134">SAP ASCS/SCS 虛擬主機 IP 位址 (其他 Azure Load Balancer IP 位址)</span><span class="sxs-lookup"><span data-stu-id="296d9-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="296d9-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="296d9-135">10.0.0.50</span></span> |
| <span data-ttu-id="296d9-136">SAP ASCS/SCS 執行個體號碼</span><span class="sxs-lookup"><span data-stu-id="296d9-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="296d9-137">50</span><span class="sxs-lookup"><span data-stu-id="296d9-137">50</span></span> |
| <span data-ttu-id="296d9-138">其他 SAP ASCS/SCS 執行個體的 ILB 探查連接埠</span><span class="sxs-lookup"><span data-stu-id="296d9-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="296d9-139">62350</span><span class="sxs-lookup"><span data-stu-id="296d9-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="296d9-140">對於 SAP ASCS/SCS 叢集執行個體，每個 IP 位址需要唯一的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="296d9-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="296d9-141">例如，如果 Azure 內部負載平衡器上有一個 IP 位址使用探查連接埠 62300，該負載平衡器上的任何其他 IP 位址就不能使用探查連接埠 62300。</span><span class="sxs-lookup"><span data-stu-id="296d9-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="296d9-142">針對本文目的，因為已保留探查連接埠 62300，我們會使用探查連接埠 62350。</span><span class="sxs-lookup"><span data-stu-id="296d9-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="296d9-143">您可以在具有兩個節點的現有 WSFC 叢集中安裝額外 SAP ASCS/SCS 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="296d9-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="296d9-144">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="296d9-144">Virtual machine role</span></span> | <span data-ttu-id="296d9-145">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="296d9-145">Virtual machine host name</span></span> | <span data-ttu-id="296d9-146">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="296d9-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="296d9-147">ASCS/SCS 執行個體的第 1 個叢集節點</span><span class="sxs-lookup"><span data-stu-id="296d9-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="296d9-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="296d9-148">pr1-ascs-0</span></span> |<span data-ttu-id="296d9-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="296d9-149">10.0.0.10</span></span> |
| <span data-ttu-id="296d9-150">ASCS/SCS 執行個體的第 2 個叢集節點</span><span class="sxs-lookup"><span data-stu-id="296d9-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="296d9-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="296d9-151">pr1-ascs-1</span></span> |<span data-ttu-id="296d9-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="296d9-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="296d9-153">在 DNS 伺服器上建立叢集 SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="296d9-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="296d9-154">您可以使用下列參數為 ASCS/SCS 執行個體的虛擬主機名稱建立 DNS 項目：</span><span class="sxs-lookup"><span data-stu-id="296d9-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="296d9-155">新的 SAP ASCS/SCS 虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="296d9-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="296d9-156">相關聯的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="296d9-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="296d9-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="296d9-157">pr5-sap-cl</span></span> |<span data-ttu-id="296d9-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="296d9-158">10.0.0.50</span></span> |

<span data-ttu-id="296d9-159">新的主機名稱和 IP 位址會顯示在 DNS 管理員中，如下列螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="296d9-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![DNS 管理員清單反白顯示已定義之新的 SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-6004]

<span data-ttu-id="296d9-161">建立 DNS 項目的程序在主要的 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide-9.1.1]中也有詳細說明。</span><span class="sxs-lookup"><span data-stu-id="296d9-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="296d9-162">您指派給 ASCS/SCS 執行個體之虛擬主機名稱的新 IP 位址必須與指派給 SAP Azure Load Balancer 的新 IP 位址相同。</span><span class="sxs-lookup"><span data-stu-id="296d9-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="296d9-163">在我們的案例中，IP 位址是 10.0.0.50。</span><span class="sxs-lookup"><span data-stu-id="296d9-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="296d9-164">使用 PowerShell 將 IP 位址新增至現有的 Azure 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="296d9-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="296d9-165">若要在相同的 WSFC 叢集中建立多個 SAP ASCS/SCS 執行個體，請使用 PowerShell 將 IP 位址新增至現有的 Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="296d9-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="296d9-166">每個 IP 位址都需要有自己的負載平衡規則、探查連接埠、前端 IP 集區和後端集區。</span><span class="sxs-lookup"><span data-stu-id="296d9-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="296d9-167">下列指令碼會將新的 IP 位址新增至現有的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="296d9-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="296d9-168">請更新您環境的 PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="296d9-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="296d9-169">指令碼會為所有 SAP ASCS/SCS 通訊埠建立所有必要的負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="296d9-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get the Azure VNet and subnet
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

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="296d9-170">在執行指令碼之後，結果會顯示在 Azure 入口網站中，如下列螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="296d9-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Azure 入口網站中新的前端 IP 集區][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="296d9-172">將磁碟新增至叢集機器，並設定 SIOS 叢集共用磁碟</span><span class="sxs-lookup"><span data-stu-id="296d9-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="296d9-173">對於每個額外 SAP ASCS/SCS 執行個體，您必須新增叢集共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="296d9-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="296d9-174">針對 Windows Server 2012 R2，目前使用的 WSFC 叢集共用磁碟是 SIOS DataKeeper 軟體解決方案。</span><span class="sxs-lookup"><span data-stu-id="296d9-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="296d9-175">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="296d9-175">Do the following:</span></span>
1. <span data-ttu-id="296d9-176">將額外磁碟或大小相同的磁碟 (您需要等量的磁碟) 新增至每個叢集節點中，並將其格式化。</span><span class="sxs-lookup"><span data-stu-id="296d9-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="296d9-177">使用 SIOS DataKeeper 設定儲存體複寫。</span><span class="sxs-lookup"><span data-stu-id="296d9-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="296d9-178">此程序假設您已在 WSFC 叢集機器上安裝了 SIOS DataKeeper。</span><span class="sxs-lookup"><span data-stu-id="296d9-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="296d9-179">如果已經安裝，您現在必須在電腦之間設定複寫。</span><span class="sxs-lookup"><span data-stu-id="296d9-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="296d9-180">如需此程序的詳細說明，請參閱主要的 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide-8.12.3.3]。</span><span class="sxs-lookup"><span data-stu-id="296d9-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![新的 SAP ASCS/SCS 共用磁碟的 DataKeeper 同步鏡像][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="296d9-182">針對 SAP 應用程式伺服器和 DBMS 叢集部署 VM</span><span class="sxs-lookup"><span data-stu-id="296d9-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="296d9-183">若要完成第二個 SAP 系統的基礎結構準備，執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="296d9-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="296d9-184">為 SAP 應用程式伺服器部署專用 VM，並將它們放在其自己專用的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="296d9-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="296d9-185">為 DBMS 叢集部署專用 VM，並將它們放在其自己專用的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="296d9-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="296d9-186">安裝第二個 SAP SID2 NetWeaver 系統</span><span class="sxs-lookup"><span data-stu-id="296d9-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="296d9-187">如需有關安裝第二個 SAP SID2 系統的完整程序說明，請參閱主要的 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide-9]。</span><span class="sxs-lookup"><span data-stu-id="296d9-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="296d9-188">高階程序如下所示︰</span><span class="sxs-lookup"><span data-stu-id="296d9-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="296d9-189">[安裝 SAP 的第一個叢集節點][sap-ha-guide-9.1.2]。</span><span class="sxs-lookup"><span data-stu-id="296d9-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="296d9-190">在此步驟中，您要在**現有 WSFC 叢集節點 1** 上使用高可用性 ASCS/SCS 執行個體安裝 SAP。</span><span class="sxs-lookup"><span data-stu-id="296d9-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="296d9-191">[修改 ASCS/SCS 執行個體的 SAP 設定檔][sap-ha-guide-9.1.3]。</span><span class="sxs-lookup"><span data-stu-id="296d9-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="296d9-192">[設定探查連接埠][sap-ha-guide-9.1.4]。</span><span class="sxs-lookup"><span data-stu-id="296d9-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="296d9-193">在此步驟中，您要使用 PowerShell 設定 SAP 叢集資源 SAP SID2 IP 探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="296d9-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="296d9-194">在其中一個 SAP ASCS/SCS 叢集節點上執行此組態。</span><span class="sxs-lookup"><span data-stu-id="296d9-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="296d9-195">[安裝資料庫執行個體][sap-ha-guide-9.2]。</span><span class="sxs-lookup"><span data-stu-id="296d9-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="296d9-196">在此步驟中，您要在專用的 WSFC 叢集上安裝 DBMS。</span><span class="sxs-lookup"><span data-stu-id="296d9-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="296d9-197">[安裝第二個叢集節點][sap-ha-guide-9.3]。</span><span class="sxs-lookup"><span data-stu-id="296d9-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="296d9-198">在此步驟中，您要在現有 WSFC 叢集節點 2 上使用高可用性 ASCS/SCS 執行個體安裝 SAP。</span><span class="sxs-lookup"><span data-stu-id="296d9-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="296d9-199">開啟 SAP ASCS/SCS 執行個體和 ProbePort 的 Windows 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="296d9-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="296d9-200">在用於 SAP ASCS/SCS 執行個體的兩個叢集節點上，您要開啟 SAP ASCS/SCS 所使用的所有 Windows 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="296d9-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="296d9-201">如需這些連接埠的清單，請參閱 [Windows VM 上的高可用性 SAP NetWeaver 指南][sap-ha-guide-8.8]。</span><span class="sxs-lookup"><span data-stu-id="296d9-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="296d9-202">此外，開啟 Azure 內部負載平衡器探查連接埠，在我們的案例中為 62350。</span><span class="sxs-lookup"><span data-stu-id="296d9-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="296d9-203">[變更 SAP ERS Windows 服務執行個體的啟動類型][sap-ha-guide-9.4]。</span><span class="sxs-lookup"><span data-stu-id="296d9-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="296d9-204">在新的專用 VM 上[安裝 SAP 主要應用程式伺服器][sap-ha-guide-9.5]。</span><span class="sxs-lookup"><span data-stu-id="296d9-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="296d9-205">在新的專用 VM 上[安裝 SAP 額外應用程式伺服器][sap-ha-guide-9.6]。</span><span class="sxs-lookup"><span data-stu-id="296d9-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="296d9-206">[測試 SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫][sap-ha-guide-10]。</span><span class="sxs-lookup"><span data-stu-id="296d9-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="296d9-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="296d9-207">Next steps</span></span>

- <span data-ttu-id="296d9-208">[網路限制：Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="296d9-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="296d9-209">[Azure Load Balancer 的多個 VIP][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="296d9-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="296d9-210">[Windows VM 上的 SAP NetWeaver 高可用性指南][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="296d9-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
