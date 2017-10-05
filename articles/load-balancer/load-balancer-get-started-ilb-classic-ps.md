---
title: "建立 Azure 內部負載平衡器 - PowerShell 傳統 | Microsoft Docs"
description: "了解如何在傳統部署模型中使用 PowerShell 建立內部負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f701fb3564c62cf8088cc4362a10c5e2c2301ae6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="d1c5c-103">開始使用 PowerShell 建立內部負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="d1c5c-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1c5c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1c5c-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="d1c5c-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1c5c-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="d1c5c-106">雲端服務</span><span class="sxs-lookup"><span data-stu-id="d1c5c-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d1c5c-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d1c5c-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="d1c5c-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d1c5c-110">了解如何[使用 Resource Manager 模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="d1c5c-111">建立虛擬機器的內部負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="d1c5c-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="d1c5c-112">若要建立內部負載平衡器集，以及向其傳送流量的伺服器，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="d1c5c-113">建立將會是連入流量端點的內部負載平衡執行個體，連入流量會在負載平衡集合的不同伺服器之間進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="d1c5c-114">新增對應到虛擬機器 (將會接收連入流量) 的端點。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="d1c5c-115">設定即將傳送流量進行負荷平衡的伺服器將其流量傳送到內部負載平衡執行個體的虛擬 IP (VIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="d1c5c-116">步驟 1︰建立內部負載平衡執行個體</span><span class="sxs-lookup"><span data-stu-id="d1c5c-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="d1c5c-117">在現有的雲端服務或在區域虛擬網路下部署的雲端服務中，您可以使用下列 Windows PowerShell 命令來建立內部負載平衡執行個體：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="d1c5c-118">請注意，使用 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell Cmdlet 會使用 DefaultProbe 參數集。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="d1c5c-119">如需其他參數集的詳細資訊，請參閱 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="d1c5c-120">步驟 2：將端點加入至內部負載平衡執行個體</span><span class="sxs-lookup"><span data-stu-id="d1c5c-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="d1c5c-121">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="d1c5c-122">步驟 3：設定您的伺服器將其流量傳送到新的內部負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="d1c5c-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="d1c5c-123">您必須設定其流量即將進行負載平衡的伺服器使用內部負載平衡執行個體的新 IP 位址 (VIP)。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="d1c5c-124">這是內部負載平衡執行個體所接聽的位址。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="d1c5c-125">在大部分情況下，您只需要針對內部負載平衡執行個體的 VIP 新增或修改 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="d1c5c-126">如果您在建立內部負載平衡執行個體的過程中指定 IP 位址，則您已具有 VIP。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="d1c5c-127">否則，您可以使用下列命令查看 VIP：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="d1c5c-128">若要使用這些命令，請填入值並移除 < 和 >。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="d1c5c-129">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="d1c5c-130">在 Get-AzureInternalLoadBalancer 命令的顯示中，請記下 IP 位址，並對伺服器或 DNS 記錄進行必要的變更，以確保流量會被傳送到 VIP。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="d1c5c-131">Microsoft Azure 平台會對各種管理案例使用靜態、可公開路由傳送的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-131">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="d1c5c-132">IP 位址是 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-132">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="d1c5c-133">此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="d1c5c-134">採用 Azure 內部負載平衡，來自負載平衡器的監視探查會使用此 IP 位址，藉此判斷虛擬機器在負載平衡集的健全狀態。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-134">With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="d1c5c-135">如果網路安全性群組已用來限制傳輸至內部負載平衡集中 Azure 虛擬機器的流量，或已套用至虛擬網路子網路，請確定您已新增網路安全性規則，允許來自 168.63.129.16 的流量。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-135">If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="d1c5c-136">內部負載平衡的範例</span><span class="sxs-lookup"><span data-stu-id="d1c5c-136">Example of internal load balancing</span></span>

<span data-ttu-id="d1c5c-137">若要為兩個範例組態逐步完成建立負載平衡集合的端對端程序，請參閱下列各節。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="d1c5c-138">網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="d1c5c-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="d1c5c-139">您想要為一組網際網路面向的 Web 伺服器提供負載平衡資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="d1c5c-140">這兩組伺服器都會裝載於單一 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="d1c5c-141">進入 TCP 通訊埠 1433 的 Web 伺服器流量必須分配到資料庫層中的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="d1c5c-142">圖 1 顯示組態。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-142">Figure 1 shows the configuration.</span></span>

![資料庫層的內部負載平衡集合](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="d1c5c-144">組態包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="d1c5c-145">裝載虛擬機器的現有雲端服務會命名為 mytestcloud。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="d1c5c-146">兩個現有的資料庫伺服器會命名為 DB1、DB2。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="d1c5c-147">Web 層中的 Web 伺服器會使用私人 IP 位址連接到資料庫層中的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="d1c5c-148">另一個選項是為虛擬網路使用您自己的 DNS，並手動註冊內部負載平衡器集的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="d1c5c-149">下列命令會設定名為 **ILBset** 的新內部負載平衡執行個體，並將端點新增至對應到兩部資料庫伺服器的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="d1c5c-150">移除內部負載平衡組態</span><span class="sxs-lookup"><span data-stu-id="d1c5c-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="d1c5c-151">若要將虛擬機器從內部負載平衡器執行個體的端點中移除，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="d1c5c-152">若要使用這些命令，請填入值並移除 < 和 >。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="d1c5c-153">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="d1c5c-154">若要將內部負載平衡器執行個體從雲端服務中移除，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="d1c5c-155">若要使用這些命令，請填入值並移除 < 和 >。</span><span class="sxs-lookup"><span data-stu-id="d1c5c-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="d1c5c-156">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="d1c5c-157">內部負載平衡器 Cmdlet 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="d1c5c-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="d1c5c-158">若要取得內部負載平衡 Cmdlet 的詳細資訊，請在 Windows PowerShell 提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1c5c-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="d1c5c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1c5c-159">Next steps</span></span>

[<span data-ttu-id="d1c5c-160">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="d1c5c-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d1c5c-161">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="d1c5c-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

