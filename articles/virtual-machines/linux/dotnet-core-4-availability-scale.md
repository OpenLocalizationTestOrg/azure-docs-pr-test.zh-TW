---
title: "aaaAvailability 和 Azure 資源管理員範本中的小數位數 |Microsoft 文件"
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
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="b633b-103">適用於 Linux VM 之 Azure Resource Manager 範本中的可用性和規模</span><span class="sxs-lookup"><span data-stu-id="b633b-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="b633b-104">可用性和延展性，請參閱 toouptime 且 hello 能力 toomeet 要求。</span><span class="sxs-lookup"><span data-stu-id="b633b-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="b633b-105">如果應用程式必須是 99.9%的 hello 時間，它會需要 toohave 架構，可以讓多個並行的計算資源。</span><span class="sxs-lookup"><span data-stu-id="b633b-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="b633b-106">比方說，而不是單一網站，具有高可用性的組態包含多個執行個體的 hello 相同站台，以平衡前面的技術。</span><span class="sxs-lookup"><span data-stu-id="b633b-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="b633b-107">此設定會 hello 應用程式的一個執行個體可以進行停機維護，剩餘的 hello 繼續 toofunction 時。</span><span class="sxs-lookup"><span data-stu-id="b633b-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="b633b-108">標尺上 hello 另一方面參考 tooan 應用程式的能力 tooserve 需求。</span><span class="sxs-lookup"><span data-stu-id="b633b-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="b633b-109">負載平衡應用程式，新增或移除執行個體從 hello 集區可讓應用程式 tooscale toomeet 需求。</span><span class="sxs-lookup"><span data-stu-id="b633b-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="b633b-110">本文件詳述 hello Music Store 範例部署可用性與延展性的設定方式。</span><span class="sxs-lookup"><span data-stu-id="b633b-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="b633b-111">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="b633b-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="b633b-112">Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b633b-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="b633b-113">hello 完成範本可以在這裡 – 找到[音樂存放部署在 Ubuntu 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="b633b-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="b633b-114">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="b633b-114">Availability Set</span></span>
<span data-ttu-id="b633b-115">「可用性設定組」可讓「Azure 虛擬機器」以邏輯方式跨不同的實體主機和其他基礎結構元件，例如電源供應器和實體網路硬體。</span><span class="sxs-lookup"><span data-stu-id="b633b-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="b633b-116">可用性設定組可確保在維護期間，裝置故障或其他停機狀況不會影響到所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="b633b-117">可用性設定組可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或插入範本中的有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="b633b-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="b633b-118">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[可用性設定組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387)。</span><span class="sxs-lookup"><span data-stu-id="b633b-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

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

<span data-ttu-id="b633b-119">「可用性設定組」會宣告為「虛擬機器」資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="b633b-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="b633b-120">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與虛擬機器的可用性設定組關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313)。</span><span class="sxs-lookup"><span data-stu-id="b633b-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="b633b-121">hello 可用性設定組如同 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b633b-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="b633b-122">此處所述每個虛擬機器以及 hello 設定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b633b-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![可用性設定組](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="b633b-124">如需有關「可用性設定組」的深入資訊，請參閱 [管理虛擬機器的可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b633b-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="b633b-125">網路負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b633b-125">Network Load Balancer</span></span>
<span data-ttu-id="b633b-126">可用性設定組會提供應用程式容錯移轉，而負載平衡器讓 hello 應用程式的許多執行個體上可使用單一網路位址。</span><span class="sxs-lookup"><span data-stu-id="b633b-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="b633b-127">應用程式的多個執行個體可以裝載多個虛擬機器，每個連接 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b633b-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="b633b-128">存取 hello 應用程式時，則 hello 負載平衡器路由 hello hello 附加成員之間連入要求。</span><span class="sxs-lookup"><span data-stu-id="b633b-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="b633b-129">負載平衡器可以使用 hello Visual Studio 新增資源精靈，加入或插入正確格式化 JSON 資源到 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b633b-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="b633b-130">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路負載平衡器](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208)。</span><span class="sxs-lookup"><span data-stu-id="b633b-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="b633b-131">因為 hello 範例應用程式公開的 toohello 網際網路的公用 IP 位址，此位址是 hello 負載平衡器相關聯。</span><span class="sxs-lookup"><span data-stu-id="b633b-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="b633b-132">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[公用 IP 位址的網路負載平衡器關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221)。</span><span class="sxs-lookup"><span data-stu-id="b633b-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="b633b-133">Hello Azure 入口網站，從 hello 網路負載平衡器概觀會顯示 hello 和 hello 公用 IP 位址之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="b633b-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![網路負載平衡器](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="b633b-135">負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="b633b-135">Load Balancer Rule</span></span>
<span data-ttu-id="b633b-136">使用負載平衡器，當規則被設定可控制流量如何平衡 hello 適合資源。</span><span class="sxs-lookup"><span data-stu-id="b633b-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="b633b-137">Hello 範例 Music Store 應用程式時，流量會到達連接埠 80 的公用 IP 位址 hello 和分散到所有虛擬機器的通訊埠 80。</span><span class="sxs-lookup"><span data-stu-id="b633b-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="b633b-138">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[負載平衡器規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。</span><span class="sxs-lookup"><span data-stu-id="b633b-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="b633b-139">檢視 hello 網路負載平衡器規則從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b633b-139">A view of hello network load balancer rule from hello portal.</span></span>

![網路負載平衡器規則](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="b633b-141">負載平衡器探查</span><span class="sxs-lookup"><span data-stu-id="b633b-141">Load Balancer Probe</span></span>
<span data-ttu-id="b633b-142">hello 負載平衡器也需要 toomonitor 每部虛擬機器，以便要求是只有 toorunning 系統。</span><span class="sxs-lookup"><span data-stu-id="b633b-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="b633b-143">這項監視會透過經常探查預先定義的連接埠來進行。</span><span class="sxs-lookup"><span data-stu-id="b633b-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="b633b-144">hello Music Store 部署是設定的 tooprobe 連接埠 80 上所有包含虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="b633b-145">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[負載平衡器探查](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257)。</span><span class="sxs-lookup"><span data-stu-id="b633b-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="b633b-146">從 hello Azure 入口網站看到 hello 負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="b633b-146">hello load balancer probe seen from hello Azure portal.</span></span>

![網路負載平衡器探查](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="b633b-148">輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="b633b-148">Inbound NAT Rules</span></span>
<span data-ttu-id="b633b-149">當使用負載平衡器時，需要 toobe 規則放置提供非負載平衡的存取 tooeach 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="b633b-150">例如，建立與每個虛擬機器的 SSH 連線時，不應該對此流量進行負載平衡，而是應該設定一個預先決定的路徑。</span><span class="sxs-lookup"><span data-stu-id="b633b-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="b633b-151">設定預先決定的路徑時是使用「輸入 NAT 規則」資源來設定。</span><span class="sxs-lookup"><span data-stu-id="b633b-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="b633b-152">輸入的通訊使用這項資源，可以是對應的 tooindividual 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="b633b-153">以 hello Music Store 應用程式，開始 5000 連接埠會是對應的 tooport 22 每部虛擬機器上進行 SSH 存取。</span><span class="sxs-lookup"><span data-stu-id="b633b-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="b633b-154">hello`copyindex()`函式是使用的 tooincrement hello 連入通訊埠，例如 hello 第二個虛擬機器接收 5001 連入通訊埠、 hello 第三個 5002，依此類推。</span><span class="sxs-lookup"><span data-stu-id="b633b-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="b633b-155">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[輸入 NAT 規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。</span><span class="sxs-lookup"><span data-stu-id="b633b-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

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

<span data-ttu-id="b633b-156">其中一個範例中所見 hello Azure 入口網站與輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="b633b-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="b633b-157">SSH NAT 規則會建立 hello 部署中每部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![輸入 NAT 規則](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="b633b-159">深入了解 hello Azure 網路負載平衡器的詳細資訊，請參閱[Azure 基礎結構服務部署的負載平衡](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b633b-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="b633b-160">部署多個 VM</span><span class="sxs-lookup"><span data-stu-id="b633b-160">Deploy multiple VMs</span></span>
<span data-ttu-id="b633b-161">最後，可用性設定組或負載平衡器 tooeffectively 函式，就需要多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b633b-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="b633b-162">可以使用 hello Azure Resource Manager 範本複製功能來部署多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="b633b-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="b633b-163">使用 hello 複製函式，不需要 toodefine 有限數目的虛擬機器，而不是此值可以為部署的 hello 次動態提供。</span><span class="sxs-lookup"><span data-stu-id="b633b-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="b633b-164">hello 複製函式會消耗 hello toocreated 執行個體和部署 hello 適當數目的虛擬機器和相關聯的資源控制代碼數目。</span><span class="sxs-lookup"><span data-stu-id="b633b-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="b633b-165">在 hello 音樂存放區範例範本，參數會定義在執行個體計數會採用。</span><span class="sxs-lookup"><span data-stu-id="b633b-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="b633b-166">建立虛擬機器和相關的資源時，此編號用整個 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="b633b-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="b633b-167">在 hello 虛擬機器資源，hello 複製迴圈會給予的名稱，hello 的執行個體參數用產生複本 toocontrol hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b633b-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="b633b-168">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器複製函式](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300)。</span><span class="sxs-lookup"><span data-stu-id="b633b-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

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

<span data-ttu-id="b633b-169">hello hello 複製函式的 目前反覆項目可以存取以 hello`copyIndex()`函式。</span><span class="sxs-lookup"><span data-stu-id="b633b-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="b633b-170">hello hello 複製索引函式值可以是使用的 tooname 虛擬機器和其他資源。</span><span class="sxs-lookup"><span data-stu-id="b633b-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="b633b-171">例如，如果部署兩個虛擬機器執行個體，它們將需要不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="b633b-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="b633b-172">hello`copyIndex()`函式可以做為屬於 hello 虛擬機器名稱 toocreate 唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="b633b-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="b633b-173">舉例來說，hello `copyindex()` hello 虛擬機器資源中可以看到用來命名之用的函式。</span><span class="sxs-lookup"><span data-stu-id="b633b-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="b633b-174">此處 hello 電腦名稱是串連的 hello`vmName`參數和 hello`copyIndex()`函式。</span><span class="sxs-lookup"><span data-stu-id="b633b-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="b633b-175">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[複製索引功能](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319)。</span><span class="sxs-lookup"><span data-stu-id="b633b-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

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

<span data-ttu-id="b633b-176">hello`copyIndex`函式 hello Music Store 範例範本中使用多次。</span><span class="sxs-lookup"><span data-stu-id="b633b-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="b633b-177">資源和函式，利用`copyIndex`包含任何項目特定 tooa hello 虛擬機器網路介面，負載平衡器規則，例如單一執行個體和任何相依於函式。</span><span class="sxs-lookup"><span data-stu-id="b633b-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="b633b-178">如需有關 hello 複製功能的詳細資訊，請參閱[Azure 資源管理員中建立資源的多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="b633b-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="b633b-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b633b-179">Next step</span></span>
<hr>

[<span data-ttu-id="b633b-180">步驟 4 - 使用 Azure Resource Manager 範本進行應用程式部署</span><span class="sxs-lookup"><span data-stu-id="b633b-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

