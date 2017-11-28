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
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="cca99-103">建立 SAP NetWeaver 多 SID 組態</span><span class="sxs-lookup"><span data-stu-id="cca99-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="cca99-104">Microsoft 在 2016 年 9 月發行的功能，可讓您使用 Azure 內部負載平衡器管理多個虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cca99-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="cca99-105">這項功能已存在於 hello Azure 外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="cca99-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="cca99-106">如果您有 SAP 部署時，您可以使用內部負載平衡器 toocreate Windows 叢集組態中的 SAP ASCS/SCS，述 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="cca99-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="cca99-107">本文著重在從單一 ASCS/SCS 安裝 tooan SAP 多 SID 組態藉由安裝其他 SAP ASCS/SCS toomove 到現有的 Windows Server 容錯移轉叢集 (WSFC) 叢集中叢集執行個體的方式。</span><span class="sxs-lookup"><span data-stu-id="cca99-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="cca99-108">完成此程序之後，您將已設定 SAP 多 SID 叢集。</span><span class="sxs-lookup"><span data-stu-id="cca99-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cca99-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="cca99-109">Prerequisites</span></span>
<span data-ttu-id="cca99-110">您已經設定 WSFC 叢集中使用一個 SAP ASCS/SCS 執行個體，請如所述 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][ sap-ha-guide]和此圖表中所示。</span><span class="sxs-lookup"><span data-stu-id="cca99-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="cca99-112">目標架構</span><span class="sxs-lookup"><span data-stu-id="cca99-112">Target architecture</span></span>

<span data-ttu-id="cca99-113">hello 的目標是的 tooinstall 多個 SAP ABAP ASCS 或 SAP Java SCS 叢集執行個體 hello 相同 WSFC 叢集中，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="cca99-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Azure 中多個 SAP ASCS/SCS 叢集執行個體][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="cca99-115">沒有為每個 Azure 內部負載平衡器的私用前端 Ip 限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="cca99-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="cca99-116">hello 一個 WSFC 叢集中的 SAP ASCS/SCS 執行個體數目上限是相等的 toohello 的每個 Azure 內部負載平衡器的私用前端 Ip 數目上限。</span><span class="sxs-lookup"><span data-stu-id="cca99-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="cca99-117">如需更多有關負載平衡器限制的資訊，請參閱[網路限制：Azure Resource Manager][networking-limits-azure-resource-manager] 中的「每個負載平衡器的私人前端 IP」。</span><span class="sxs-lookup"><span data-stu-id="cca99-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="cca99-118">hello 與兩個高可用性的 SAP 系統的完整說明看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="cca99-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![具有兩個 SAP 系統 SID 的 SAP 高可用性多 SID 設定][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="cca99-120">hello 安裝程式必須符合下列條件的 hello:</span><span class="sxs-lookup"><span data-stu-id="cca99-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="cca99-121">hello SAP ASCS/SCS 執行個體必須共用 hello 相同 WSFC 叢集。</span><span class="sxs-lookup"><span data-stu-id="cca99-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="cca99-122">每個 DBMS SID 必須有其自己專用的 WSFC 叢集。</span><span class="sxs-lookup"><span data-stu-id="cca99-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="cca99-123">屬於 tooone SAP 系統 SID 的 SAP 應用程式伺服器必須有自己專用的 Vm。</span><span class="sxs-lookup"><span data-stu-id="cca99-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="cca99-124">準備 hello 基礎結構</span><span class="sxs-lookup"><span data-stu-id="cca99-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="cca99-125">tooprepare 您基礎結構，您可以使用下列參數的 hello 安裝額外的 SAP ASCS/SCS 執行個體：</span><span class="sxs-lookup"><span data-stu-id="cca99-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="cca99-126">參數名稱</span><span class="sxs-lookup"><span data-stu-id="cca99-126">Parameter name</span></span> | <span data-ttu-id="cca99-127">值</span><span class="sxs-lookup"><span data-stu-id="cca99-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cca99-128">SAP ASCS/SCS SID</span><span class="sxs-lookup"><span data-stu-id="cca99-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="cca99-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="cca99-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="cca99-130">SAP DBMS 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="cca99-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="cca99-131">PR5</span><span class="sxs-lookup"><span data-stu-id="cca99-131">PR5</span></span> |
| <span data-ttu-id="cca99-132">SAP 虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="cca99-132">SAP virtual host name</span></span> | <span data-ttu-id="cca99-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="cca99-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="cca99-134">SAP ASCS/SCS 虛擬主機 IP 位址 (其他 Azure Load Balancer IP 位址)</span><span class="sxs-lookup"><span data-stu-id="cca99-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="cca99-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="cca99-135">10.0.0.50</span></span> |
| <span data-ttu-id="cca99-136">SAP ASCS/SCS 執行個體號碼</span><span class="sxs-lookup"><span data-stu-id="cca99-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="cca99-137">50</span><span class="sxs-lookup"><span data-stu-id="cca99-137">50</span></span> |
| <span data-ttu-id="cca99-138">其他 SAP ASCS/SCS 執行個體的 ILB 探查連接埠</span><span class="sxs-lookup"><span data-stu-id="cca99-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="cca99-139">62350</span><span class="sxs-lookup"><span data-stu-id="cca99-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="cca99-140">對於 SAP ASCS/SCS 叢集執行個體，每個 IP 位址需要唯一的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="cca99-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="cca99-141">例如，如果 Azure 內部負載平衡器上有一個 IP 位址使用探查連接埠 62300，該負載平衡器上的任何其他 IP 位址就不能使用探查連接埠 62300。</span><span class="sxs-lookup"><span data-stu-id="cca99-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="cca99-142">針對本文目的，因為已保留探查連接埠 62300，我們會使用探查連接埠 62350。</span><span class="sxs-lookup"><span data-stu-id="cca99-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="cca99-143">您可以在 hello 現有 WSFC 叢集包含兩個節點中安裝額外的 SAP ASCS/SCS 執行個體：</span><span class="sxs-lookup"><span data-stu-id="cca99-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="cca99-144">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="cca99-144">Virtual machine role</span></span> | <span data-ttu-id="cca99-145">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="cca99-145">Virtual machine host name</span></span> | <span data-ttu-id="cca99-146">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="cca99-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cca99-147">ASCS/SCS 執行個體的第 1 個叢集節點</span><span class="sxs-lookup"><span data-stu-id="cca99-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="cca99-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="cca99-148">pr1-ascs-0</span></span> |<span data-ttu-id="cca99-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="cca99-149">10.0.0.10</span></span> |
| <span data-ttu-id="cca99-150">ASCS/SCS 執行個體的第 2 個叢集節點</span><span class="sxs-lookup"><span data-stu-id="cca99-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="cca99-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="cca99-151">pr1-ascs-1</span></span> |<span data-ttu-id="cca99-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="cca99-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="cca99-153">Hello DNS 伺服器上建立叢集的 hello SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="cca99-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="cca99-154">您可以使用下列參數的 hello 建立 hello hello ASCS/SCS 執行個體的虛擬主機名稱的 DNS 項目：</span><span class="sxs-lookup"><span data-stu-id="cca99-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="cca99-155">新的 SAP ASCS/SCS 虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="cca99-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="cca99-156">相關聯的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="cca99-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="cca99-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="cca99-157">pr5-sap-cl</span></span> |<span data-ttu-id="cca99-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="cca99-158">10.0.0.50</span></span> |

<span data-ttu-id="cca99-159">hello 新的主機名稱和 IP 位址會顯示 hello DNS 管理員 中，在 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="cca99-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![DNS 管理員 清單中反白顯示 hello 定義 hello 新 SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-6004]

<span data-ttu-id="cca99-161">建立 DNS 項目 hello 程序也說明 hello 主要詳細[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-9.1.1]。</span><span class="sxs-lookup"><span data-stu-id="cca99-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="cca99-162">hello 您指派 toohello hello 其他 ASCS/SCS 執行個體的虛擬主機名稱的新 IP 位址必須是 hello 與 hello 新的 IP 位址指派給 toohello SAP 的 Azure 負載平衡器相同。</span><span class="sxs-lookup"><span data-stu-id="cca99-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="cca99-163">在我們的案例所 10.0.0.50 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cca99-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="cca99-164">使用 PowerShell 新增 IP 位址 tooan 現有 Azure 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="cca99-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="cca99-165">以上一個 SAP ASCS/SCS 執行個體中的 toocreate hello 相同 WSFC 叢集，請使用 PowerShell tooadd 現有 Azure 內部負載平衡器 IP 位址 tooan。</span><span class="sxs-lookup"><span data-stu-id="cca99-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="cca99-166">每個 IP 位址都需要有自己的負載平衡規則、探查連接埠、前端 IP 集區和後端集區。</span><span class="sxs-lookup"><span data-stu-id="cca99-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="cca99-167">hello 下列指令碼會新增新 IP 位址 tooan 現有負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="cca99-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="cca99-168">更新您的環境的 hello PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="cca99-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="cca99-169">hello 指令碼會建立所需的所有負載平衡規則的所有 SAP ASCS/SCS 連接埠。</span><span class="sxs-lookup"><span data-stu-id="cca99-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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
<span data-ttu-id="cca99-170">Hello 指令碼執行之後，結果會顯示在 hello hello Azure 入口網站，hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="cca99-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![前端 IP 集區中 hello Azure 入口網站][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="cca99-172">新增磁碟 toocluster 機器，並設定 hello SIOS 叢集共用磁碟</span><span class="sxs-lookup"><span data-stu-id="cca99-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="cca99-173">對於每個額外 SAP ASCS/SCS 執行個體，您必須新增叢集共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="cca99-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="cca99-174">Windows Server 2012 R2，hello WSFC 叢集共用磁碟目前正在使用中的 hello SIOS DataKeeper 軟體解決方案。</span><span class="sxs-lookup"><span data-stu-id="cca99-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="cca99-175">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="cca99-175">Do hello following:</span></span>
1. <span data-ttu-id="cca99-176">新增其他磁碟或磁碟的 hello 相同的大小 (您需要 toostripe) tooeach hello 的叢集節點，然後將它們格式化。</span><span class="sxs-lookup"><span data-stu-id="cca99-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="cca99-177">使用 SIOS DataKeeper 設定儲存體複寫。</span><span class="sxs-lookup"><span data-stu-id="cca99-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="cca99-178">此程序假設您已經有安裝 SIOS DataKeeper hello WSFC 叢集的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cca99-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="cca99-179">如果您已安裝它，您現在必須設定 hello 機器之間的複寫。</span><span class="sxs-lookup"><span data-stu-id="cca99-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="cca99-180">hello 程序中有詳細說明在 hello 主要[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-8.12.3.3]。</span><span class="sxs-lookup"><span data-stu-id="cca99-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper 同步鏡像 hello 新 SAP ASCS/SCS 共用磁碟][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="cca99-182">針對 SAP 應用程式伺服器和 DBMS 叢集部署 VM</span><span class="sxs-lookup"><span data-stu-id="cca99-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="cca99-183">第二個 SAP 系統 hello，toocomplete hello 基礎結構準備 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="cca99-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="cca99-184">為 SAP 應用程式伺服器部署專用 VM，並將它們放在其自己專用的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="cca99-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="cca99-185">為 DBMS 叢集部署專用 VM，並將它們放在其自己專用的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="cca99-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="cca99-186">安裝第二個 SID2 的 SAP NetWeaver 系統 hello</span><span class="sxs-lookup"><span data-stu-id="cca99-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="cca99-187">hello 安裝的第二個 SAP SID2 系統的完整程序所述 hello 主要[Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-9]。</span><span class="sxs-lookup"><span data-stu-id="cca99-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="cca99-188">hello 高階程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="cca99-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="cca99-189">[安裝 hello SAP 第一個叢集節點][sap-ha-guide-9.1.2]。</span><span class="sxs-lookup"><span data-stu-id="cca99-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="cca99-190">在此步驟中，您要安裝 SAP 與高可用性 ASCS/SCS 執行個體上 hello**現有的 WSFC 叢集節點 1**。</span><span class="sxs-lookup"><span data-stu-id="cca99-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="cca99-191">[修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔][sap-ha-guide-9.1.3]。</span><span class="sxs-lookup"><span data-stu-id="cca99-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="cca99-192">[設定探查連接埠][sap-ha-guide-9.1.4]。</span><span class="sxs-lookup"><span data-stu-id="cca99-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="cca99-193">在此步驟中，您要使用 PowerShell 設定 SAP 叢集資源 SAP SID2 IP 探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="cca99-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="cca99-194">其中一個 hello SAP ASCS/SCS 叢集節點上執行這項設定。</span><span class="sxs-lookup"><span data-stu-id="cca99-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="cca99-195">[安裝 hello 資料庫執行個體][sap-ha-快速入門-9.2]。</span><span class="sxs-lookup"><span data-stu-id="cca99-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="cca99-196">在此步驟中，您要在專用的 WSFC 叢集上安裝 DBMS。</span><span class="sxs-lookup"><span data-stu-id="cca99-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="cca99-197">[安裝 hello 第二個叢集節點][sap-ha-快速入門-9.3]。</span><span class="sxs-lookup"><span data-stu-id="cca99-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="cca99-198">在此步驟中，您要安裝 SAP 與現有 WSFC 叢集節點 hello 2 上的高可用性 ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="cca99-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="cca99-199">開啟 Windows 防火牆連接埠 hello SAP ASCS/SCS 執行個體或甚至 ProbePort。</span><span class="sxs-lookup"><span data-stu-id="cca99-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="cca99-200">在用於 SAP ASCS/SCS 執行個體的兩個叢集節點上，您要開啟 SAP ASCS/SCS 所使用的所有 Windows 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="cca99-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="cca99-201">這些連接埠會列在 hello [Windows Vm 上的高可用性的 SAP NetWeaver 指南][sap-ha-guide-8.8]。</span><span class="sxs-lookup"><span data-stu-id="cca99-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="cca99-202">也開啟 hello Azure 內部負載平衡器探查連接埠，也就是 62350 在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="cca99-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="cca99-203">[變更 hello hello SAP 端 Windows 服務執行個體的啟動類型][sap-ha-guide-9.4]。</span><span class="sxs-lookup"><span data-stu-id="cca99-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="cca99-204">[安裝 hello SAP 主應用程式伺服器][ sap-ha-guide-9.5]上新的 hello 專用 VM。</span><span class="sxs-lookup"><span data-stu-id="cca99-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="cca99-205">[安裝 hello SAP 其他應用程式伺服器][ sap-ha-guide-9.6]上新的 hello 專用 VM。</span><span class="sxs-lookup"><span data-stu-id="cca99-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="cca99-206">[測試 hello SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫][sap-ha-guide-10]。</span><span class="sxs-lookup"><span data-stu-id="cca99-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cca99-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cca99-207">Next steps</span></span>

- <span data-ttu-id="cca99-208">[網路限制：Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="cca99-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="cca99-209">[Azure Load Balancer 的多個 VIP][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="cca99-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="cca99-210">[Windows VM 上的 SAP NetWeaver 高可用性指南][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="cca99-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
