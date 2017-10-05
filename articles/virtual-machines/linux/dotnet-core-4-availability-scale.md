---
title: "Azure Resource Manager 範本中的可用性和規模 | Microsoft Docs"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0250b8152ed31b9a5d8b42ae139c9b38da0984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="f39ed-103">適用於 Linux VM 之 Azure Resource Manager 範本中的可用性和規模</span><span class="sxs-lookup"><span data-stu-id="f39ed-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="f39ed-104">可用性和規模是指滿足需求的執行時間和能力。</span><span class="sxs-lookup"><span data-stu-id="f39ed-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="f39ed-105">如果應用程式必須 99.9% 的時間都處於執行狀態，它就需要一個可允許多個並行計算資源的架構。</span><span class="sxs-lookup"><span data-stu-id="f39ed-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="f39ed-106">例如，具有較高層級可用性的組態不會包含單一網站，而是會包含相同網站的多個執行個體，其中前端會有平衡技術。</span><span class="sxs-lookup"><span data-stu-id="f39ed-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="f39ed-107">在此組態中，可以讓一個應用程式執行個體停機來進行維護，而剩下的執行個體則繼續運作。</span><span class="sxs-lookup"><span data-stu-id="f39ed-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="f39ed-108">另一方面，規模則是指應用程式為需求提供服務的能力。</span><span class="sxs-lookup"><span data-stu-id="f39ed-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="f39ed-109">使用已負載平衡的應用程式時，在集區中新增或移除執行個體，即可讓應用程式調整來滿足需求。</span><span class="sxs-lookup"><span data-stu-id="f39ed-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="f39ed-110">本文件詳細說明如何針對可用性和規模設定「音樂市集」範例部署。</span><span class="sxs-lookup"><span data-stu-id="f39ed-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="f39ed-111">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="f39ed-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f39ed-112">為了獲得最佳體驗，請將一個解決方案執行個體預先部署到您的 Azure 訂用帳戶，然後與 Azure Resource Manager 範本搭配運作。</span><span class="sxs-lookup"><span data-stu-id="f39ed-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="f39ed-113">您可以在下列連結找到完整的範本 – [Ubuntu 上的音樂市集部署](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="f39ed-114">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="f39ed-114">Availability Set</span></span>
<span data-ttu-id="f39ed-115">「可用性設定組」可讓「Azure 虛擬機器」以邏輯方式跨不同的實體主機和其他基礎結構元件，例如電源供應器和實體網路硬體。</span><span class="sxs-lookup"><span data-stu-id="f39ed-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="f39ed-116">可用性設定組可確保在維護期間，裝置故障或其他停機狀況不會影響到所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f39ed-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="f39ed-117">您可以透過使用 Visual Studio 的「加入新資源精靈」或在範本中插入有效的 JSON，將「可用性設定組」新增至 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f39ed-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="f39ed-118">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [可用性設定組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="f39ed-119">「可用性設定組」會宣告為「虛擬機器」資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="f39ed-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="f39ed-120">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [可用性設定組與虛擬機器的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="f39ed-121">Azure 入口網站中所示的可用性設定組樣子。</span><span class="sxs-lookup"><span data-stu-id="f39ed-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="f39ed-122">以下詳細顯示每個虛擬機器及組態的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f39ed-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![可用性設定組](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="f39ed-124">如需有關「可用性設定組」的深入資訊，請參閱 [管理虛擬機器的可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="f39ed-125">網路負載平衡器</span><span class="sxs-lookup"><span data-stu-id="f39ed-125">Network Load Balancer</span></span>
<span data-ttu-id="f39ed-126">可用性設定組可提供應用程式容錯移轉，而負載平衡器則是讓單一網路位址上有許多應用程式執行個體可供使用。</span><span class="sxs-lookup"><span data-stu-id="f39ed-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="f39ed-127">多個應用程式執行個體可以裝載在多個虛擬機器上，每個虛擬機器皆連接到負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f39ed-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="f39ed-128">當應用程式被存取時，負載平衡器會將連入要求路由傳送至各個連接的成員。</span><span class="sxs-lookup"><span data-stu-id="f39ed-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="f39ed-129">您可以透過使用 Visual Studio 的「加入新資源精靈」或在 Azure Resource Manager 範本中插入格式正確的 JSON 資源，來新增「負載平衡器」。</span><span class="sxs-lookup"><span data-stu-id="f39ed-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="f39ed-130">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [網路負載平衡器](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="f39ed-131">由於範例應用程式是透過公用 IP 位址對網際網路公開，因此這個位址會與負載平衡器關聯。</span><span class="sxs-lookup"><span data-stu-id="f39ed-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="f39ed-132">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [網路負載平衡器與公用 IP 位址的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="f39ed-133">在 Azure 入口網站中，網路負載平衡器概觀會顯示與公用 IP 位址的關聯。</span><span class="sxs-lookup"><span data-stu-id="f39ed-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![網路負載平衡器](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="f39ed-135">負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="f39ed-135">Load Balancer Rule</span></span>
<span data-ttu-id="f39ed-136">使用負載平衡器時，會設定規則來控制如何在各個預期的資源之間平衡流量。</span><span class="sxs-lookup"><span data-stu-id="f39ed-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="f39ed-137">在範例「音樂市集」應用程式中，流量會抵達公用 IP 位址的連接埠 80，然後分散到所有虛擬機器的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="f39ed-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="f39ed-138">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [負載平衡器規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="f39ed-139">入口網站中所示的網路負載平衡器規則樣子。</span><span class="sxs-lookup"><span data-stu-id="f39ed-139">A view of the network load balancer rule from the portal.</span></span>

![網路負載平衡器規則](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="f39ed-141">負載平衡器探查</span><span class="sxs-lookup"><span data-stu-id="f39ed-141">Load Balancer Probe</span></span>
<span data-ttu-id="f39ed-142">負載平衡器也需要監視每個虛擬機器，以便只將要求提供給執行中的系統。</span><span class="sxs-lookup"><span data-stu-id="f39ed-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="f39ed-143">這項監視會透過經常探查預先定義的連接埠來進行。</span><span class="sxs-lookup"><span data-stu-id="f39ed-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="f39ed-144">「音樂市集」部署是設定為探查所有包含的虛擬機器上的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="f39ed-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="f39ed-145">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [負載平衡器探查](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="f39ed-146">Azure 入口網站中所示的負載平衡器探查樣子。</span><span class="sxs-lookup"><span data-stu-id="f39ed-146">The load balancer probe seen from the Azure portal.</span></span>

![網路負載平衡器探查](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="f39ed-148">輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="f39ed-148">Inbound NAT Rules</span></span>
<span data-ttu-id="f39ed-149">使用「負載平衡器」時，必須有適當規則來提供對每個「虛擬機器」的非負載平衡存取。</span><span class="sxs-lookup"><span data-stu-id="f39ed-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="f39ed-150">例如，建立與每個虛擬機器的 SSH 連線時，不應該對此流量進行負載平衡，而是應該設定一個預先決定的路徑。</span><span class="sxs-lookup"><span data-stu-id="f39ed-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="f39ed-151">設定預先決定的路徑時是使用「輸入 NAT 規則」資源來設定。</span><span class="sxs-lookup"><span data-stu-id="f39ed-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="f39ed-152">透過使用這項資源，便可將輸入通訊對應到個別的「虛擬機器」。</span><span class="sxs-lookup"><span data-stu-id="f39ed-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="f39ed-153">在「音樂市集」應用程式中，從 5000 開始的連接埠會對應到每個「虛擬機器」上的連接埠 22 以進行 SSH 存取。</span><span class="sxs-lookup"><span data-stu-id="f39ed-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="f39ed-154">`copyindex()` 函式可用來遞增連入連接埠，讓第二個「虛擬機器」接收連入接埠 5001，第三個則接收 5002，依此類推。</span><span class="sxs-lookup"><span data-stu-id="f39ed-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="f39ed-155">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [輸入 NAT 規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="f39ed-156">Azure 入口網站中所示的一個範例輸入 NAT 規則樣子。</span><span class="sxs-lookup"><span data-stu-id="f39ed-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="f39ed-157">在部署中會為每個虛擬機器建立一個 SSH NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="f39ed-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![輸入 NAT 規則](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="f39ed-159">如需有關「Azure 網路負載平衡器」的深入資訊，請參閱 [Azure 基礎結構服務的負載平衡](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="f39ed-160">部署多個 VM</span><span class="sxs-lookup"><span data-stu-id="f39ed-160">Deploy multiple VMs</span></span>
<span data-ttu-id="f39ed-161">最後，為了讓「可用性設定組」或「負載平衡器」有效地運作，必須要有多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f39ed-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="f39ed-162">您可以使用 Azure Resource Manager 範本複製函式來部署多個 VM。</span><span class="sxs-lookup"><span data-stu-id="f39ed-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="f39ed-163">使用複製函式時，並不需要定義有限數量的「虛擬機器」，而是可以在部署時動態提供這個值。</span><span class="sxs-lookup"><span data-stu-id="f39ed-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="f39ed-164">複製函式會取用要建立的執行個體數目，以及處理部署適當數目之虛擬機器及相關資源的作業。</span><span class="sxs-lookup"><span data-stu-id="f39ed-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="f39ed-165">在「音樂市集」範本中，已定義一個會擷取執行個體計數的參數。</span><span class="sxs-lookup"><span data-stu-id="f39ed-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="f39ed-166">在範本中，當建立虛擬機器及相關資源時，會全程使用這個數字。</span><span class="sxs-lookup"><span data-stu-id="f39ed-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

<span data-ttu-id="f39ed-167">在「虛擬機器」資源上，會為複製迴圈提供名稱及參數用來控制產生之複本數目的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="f39ed-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="f39ed-168">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [虛擬機器複製函式](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="f39ed-169">存取目前的複製函式反覆項目時，可以透過 `copyIndex()` 函式來存取。</span><span class="sxs-lookup"><span data-stu-id="f39ed-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="f39ed-170">複製索引函式的值可用來命名虛擬機器和其他資源。</span><span class="sxs-lookup"><span data-stu-id="f39ed-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="f39ed-171">例如，如果部署兩個虛擬機器執行個體，它們將需要不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="f39ed-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="f39ed-172">`copyIndex()` 函式可用來作為虛擬機器名稱的一部分，以建立一個唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="f39ed-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="f39ed-173">在「虛擬機器」資源中可以看到用於命名用途的 `copyindex()` 函式範例。</span><span class="sxs-lookup"><span data-stu-id="f39ed-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="f39ed-174">這裡的電腦名稱是由 `vmName` 參數和 `copyIndex()` 函式串連而成。</span><span class="sxs-lookup"><span data-stu-id="f39ed-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="f39ed-175">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [複製索引函式](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="f39ed-176">在「音樂市集」範例範本中使用 `copyIndex` 函式多次。</span><span class="sxs-lookup"><span data-stu-id="f39ed-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="f39ed-177">利用 `copyIndex` 的資源和函式會包括單一虛擬機器執行個體的所有特定項目，例如網路介面、負載平衡器規則及與函式相依的任何項目。</span><span class="sxs-lookup"><span data-stu-id="f39ed-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="f39ed-178">如需有關有關複製函式的詳細資訊，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="f39ed-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="f39ed-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f39ed-179">Next step</span></span>
<hr>

[<span data-ttu-id="f39ed-180">步驟 4 - 使用 Azure Resource Manager 範本進行應用程式部署</span><span class="sxs-lookup"><span data-stu-id="f39ed-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

