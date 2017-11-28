---
title: "aaaCreate Azure 內部負載平衡器-PowerShell 傳統 |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器在 hello 傳統部署模型中使用 PowerShell 的方式"
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
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="8fca9-103">開始使用 PowerShell 建立內部負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="8fca9-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fca9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fca9-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="8fca9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fca9-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="8fca9-106">雲端服務</span><span class="sxs-lookup"><span data-stu-id="8fca9-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="8fca9-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8fca9-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8fca9-108">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="8fca9-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8fca9-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="8fca9-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8fca9-110">了解如何太[使用 hello 資源管理員的模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="8fca9-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="8fca9-111">建立虛擬機器的內部負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="8fca9-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="8fca9-112">內部負載平衡器設定和 hello 伺服器，則會傳送其流量 tooit toocreate，您有 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8fca9-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="8fca9-113">建立執行個體的內部負載平衡一組負載平衡的 hello 伺服器之間取得平衡的連入流量 toobe 負載 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="8fca9-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="8fca9-114">新增對應 toohello 將接收 hello 連入流量的虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="8fca9-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="8fca9-115">設定將用來傳送嗨流量 toobe 負載平衡 toosend 其流量 toohello 虛擬 IP (VIP) 位址 hello 內部負載平衡的執行個體的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8fca9-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="8fca9-116">步驟 1︰建立內部負載平衡執行個體</span><span class="sxs-lookup"><span data-stu-id="8fca9-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="8fca9-117">對於現有的雲端服務或部署在區域虛擬網路的雲端服務，您可以建立內部負載平衡的執行個體，以下列 Windows PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8fca9-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="8fca9-118">請注意，這種使用 hello [Add-azureendpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet 會使用 hello DefaultProbe 參數集。</span><span class="sxs-lookup"><span data-stu-id="8fca9-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="8fca9-119">如需其他參數集的詳細資訊，請參閱 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8fca9-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="8fca9-120">步驟 2： 新增端點 toohello 內部負載平衡執行個體</span><span class="sxs-lookup"><span data-stu-id="8fca9-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="8fca9-121">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="8fca9-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="8fca9-122">步驟 3： 設定伺服器 toosend 其流量 toohello 新內部負載平衡的端點</span><span class="sxs-lookup"><span data-stu-id="8fca9-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="8fca9-123">您有太設定 hello 伺服器的流量是進行 toobe 負載平衡 toouse hello 新 IP 位址 (hello VIP) hello 內部負載平衡的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8fca9-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="8fca9-124">這是內部負載平衡的 hello 執行個體所接聽的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="8fca9-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="8fca9-125">在大部分情況下，您需要 toojust 加入或修改 hello 內部負載平衡的執行個體的 hello VIP 的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="8fca9-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="8fca9-126">如果您指定 hello IP 位址 hello hello 內部負載平衡的執行個體建立期間，您已經有 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="8fca9-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="8fca9-127">否則，您可以看到 hello VIP 從 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8fca9-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="8fca9-128">toouse 這些命令中，填寫 hello 值，然後移除 hello < 和 >。</span><span class="sxs-lookup"><span data-stu-id="8fca9-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="8fca9-129">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="8fca9-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="8fca9-130">從 hello 顯示 hello Get-azureinternalloadbalancer 命令，記下 hello IP 位址以 hello 必要的變更 tooyour 伺服器或資料流取得傳送 toohello VIP 的 DNS 記錄 tooensure。</span><span class="sxs-lookup"><span data-stu-id="8fca9-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="8fca9-131">hello Microsoft Azure 平台會使用各種不同的系統管理情況靜態、 可公開路由傳送的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="8fca9-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="8fca9-132">hello IP 位址是 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="8fca9-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="8fca9-133">此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="8fca9-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="8fca9-134">內部負載平衡尊重 tooAzure，此 IP 位址會使用藉由監視 hello 負載平衡器 toodetermine hello 健全狀況狀態的虛擬機器負載平衡集的探查。</span><span class="sxs-lookup"><span data-stu-id="8fca9-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="8fca9-135">如果網路安全性小組使用的 toorestrict 內部負載平衡集內的流量 tooAzure 虛擬機器或套用的 tooa 虛擬網路子網路，請確定網路安全性規則從 168.63.129.16 加入 tooallow 流量。</span><span class="sxs-lookup"><span data-stu-id="8fca9-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="8fca9-136">內部負載平衡的範例</span><span class="sxs-lookup"><span data-stu-id="8fca9-136">Example of internal load balancing</span></span>

<span data-ttu-id="8fca9-137">您完成 hello 結束 tooend 程序建立一組負載平衡的兩個範例設定，請參閱 toostep hello 下列各節。</span><span class="sxs-lookup"><span data-stu-id="8fca9-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="8fca9-138">網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="8fca9-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="8fca9-139">您想 tooprovide 一組網際網路對向 web 伺服器的負載平衡資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="8fca9-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="8fca9-140">這兩組伺服器都會裝載於單一 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8fca9-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="8fca9-141">網頁伺服器流量 tooTCP 連接埠 1433年必須分散 hello 資料庫層中的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fca9-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="8fca9-142">圖 1 顯示 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="8fca9-142">Figure 1 shows hello configuration.</span></span>

![Hello 資料庫層的內部負載平衡集](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="8fca9-144">hello 設定包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="8fca9-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="8fca9-145">hello 現有的雲端服務裝載 hello 虛擬機器名為 mytestcloud。</span><span class="sxs-lookup"><span data-stu-id="8fca9-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="8fca9-146">hello 兩個現有資料庫伺服器則命名為 DB1 中，DB2。</span><span class="sxs-lookup"><span data-stu-id="8fca9-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="8fca9-147">Hello web 層中的 web 伺服器連接 toohello hello 資料庫層中的資料庫伺服器使用 hello 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8fca9-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="8fca9-148">另一個選項是 toouse hello 虛擬網路的 DNS，並以手動方式註冊 hello 內部負載平衡器集 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="8fca9-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="8fca9-149">hello comandos siguientes configuran 新內部負載平衡的執行個體名為**ILBset**加入對應 toohello 兩個資料庫伺服器的端點 toohello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="8fca9-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="8fca9-150">移除內部負載平衡組態</span><span class="sxs-lookup"><span data-stu-id="8fca9-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="8fca9-151">tooremove 為內部負載平衡器執行個體，下列命令使用 hello 從端點的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="8fca9-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="8fca9-152">toouse 這些命令中，填寫 hello 值，並移除 hello < 和 >。</span><span class="sxs-lookup"><span data-stu-id="8fca9-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="8fca9-153">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="8fca9-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="8fca9-154">tooremove 內部負載平衡器執行個體從雲端服務，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="8fca9-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="8fca9-155">這些命令，toouse 填入 hello 值，並移除 hello < 和 >。</span><span class="sxs-lookup"><span data-stu-id="8fca9-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="8fca9-156">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="8fca9-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="8fca9-157">內部負載平衡器 Cmdlet 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="8fca9-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="8fca9-158">tooobtain 內部負載平衡 cmdlet，執行下列命令在 Windows PowerShell 提示字元中的 hello 相關的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="8fca9-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="8fca9-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fca9-159">Next steps</span></span>

[<span data-ttu-id="8fca9-160">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="8fca9-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8fca9-161">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="8fca9-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

