---
title: "使用 Azure CLI 1.0 建立完整的 Linux 環境 | Microsoft Docs"
description: "使用 Azure CLI 1.0，從頭開始建立儲存體、Linux VM、虛擬網路和子網路、負載平衡器、NIC、公用 IP 以及網路安全性群組。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="f8d3b-103">使用 Azure CLI 1.0 建立完整的 Linux 環境</span><span class="sxs-lookup"><span data-stu-id="f8d3b-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="f8d3b-104">在這篇文章中，我們將建立一個簡單的網路，當中包含一個負載平衡器，以及一組對開發和簡單運算而言相當實用的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="f8d3b-105">我們將以逐個命令的方式逐步完成程序命令，直到您具備兩個可供您透過網際網路從任何地方連線的有效、安全 Linux VM 為止。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="f8d3b-106">然後您便可以繼續著手更複雜的網路和環境。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="f8d3b-107">在過程中，您將了解 Resource Manager 部署模型提供給您的相依性階層，以及它提供多少功能。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="f8d3b-108">在您了解系統建置的方式之後，您就可以使用 [Azure Resource Manager 範本](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)更快地建置系統。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f8d3b-109">此外，在您了解環境的組件彼此如何搭配運作之後，就可以更輕鬆地建立範本來將它們自動化。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="f8d3b-110">此環境包含：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-110">The environment contains:</span></span>

* <span data-ttu-id="f8d3b-111">兩個位於可用性設定組內的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="f8d3b-112">一個在連接埠 80 有負載平衡規則的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="f8d3b-113">可保護 VM 防止不必要流量的網路安全性群組 (NSG) 規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="f8d3b-114">若要建立此自訂環境，您需要處於 Resource Manager 模式 (`azure config mode arm`) 的最新 [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="f8d3b-115">您也需要 JSON 剖析工具。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="f8d3b-116">此範例使用 [jq](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f8d3b-117">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="f8d3b-117">CLI versions to complete the task</span></span>
<span data-ttu-id="f8d3b-118">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f8d3b-119">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="f8d3b-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f8d3b-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="f8d3b-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="f8d3b-121">快速命令</span><span class="sxs-lookup"><span data-stu-id="f8d3b-121">Quick commands</span></span>
<span data-ttu-id="f8d3b-122">如果您需要快速完成工作，下列章節詳細說明上傳 VM 至 Azure 的基本命令。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="f8d3b-123">每個步驟的詳細資訊和內容可在文件其他地方找到，從[這裡](#detailed-walkthrough)開始。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="f8d3b-124">確定您已登入 [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，並且使用的是 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f8d3b-125">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f8d3b-126">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="f8d3b-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-127">Create the resource group.</span></span> <span data-ttu-id="f8d3b-128">下列範例會在 `westeurope` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="f8d3b-129">使用 JSON 剖析器來確認資源群組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="f8d3b-130">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-130">Create the storage account.</span></span> <span data-ttu-id="f8d3b-131">下列範例會建立名為 `mystorageaccount` 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="f8d3b-132">(儲存體帳戶名稱必須是唯一的，因此請提供您自己的唯一名稱。)</span><span class="sxs-lookup"><span data-stu-id="f8d3b-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="f8d3b-133">使用 JSON 剖析器來確認儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="f8d3b-134">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f8d3b-134">Create the virtual network.</span></span> <span data-ttu-id="f8d3b-135">下列範例會建立名為 `myVnet`的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="f8d3b-136">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-136">Create a subnet.</span></span> <span data-ttu-id="f8d3b-137">下列範例會建立名為 `mySubnet`的子網路：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="f8d3b-138">使用 JSON 剖析器來確認虛擬網路和子網路：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="f8d3b-139">建立公用 IP。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-139">Create a public IP.</span></span> <span data-ttu-id="f8d3b-140">下列範例會建立名為 `myPublicIP` 的公用 IP，DNS 名稱為`mypublicdns`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="f8d3b-141">(DNS 名稱必須是唯一的，因此請提供您自己的唯一名稱。)</span><span class="sxs-lookup"><span data-stu-id="f8d3b-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="f8d3b-142">建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-142">Create the load balancer.</span></span> <span data-ttu-id="f8d3b-143">下列範例會建立名為 `myLoadBalancer` 的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="f8d3b-144">建立負載平衡器的前端 IP 集區，並與公用 IP 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="f8d3b-145">下列範例會建立名為 `mySubnetPool` 的前端 IP 集區：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="f8d3b-146">建立負載平衡器的後端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="f8d3b-147">下列範例會建立名為 `myBackEndPool` 的後端 IP 集區：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="f8d3b-148">建立負載平衡器的 SSH 輸入網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="f8d3b-149">下列範例會建立兩個負載平衡器，`myLoadBalancerRuleSSH1` 和 `myLoadBalancerRuleSSH2`：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="f8d3b-150">建立負載平衡器的 Web 輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="f8d3b-151">下列範例會建立名為 `myLoadBalancerRuleWeb` 的負載平衡器規則：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="f8d3b-152">建立負載平衡器健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-152">Create the load balancer health probe.</span></span> <span data-ttu-id="f8d3b-153">下列範例會建立名為 `myHealthProbe` 的 TCP 探查：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="f8d3b-154">使用 JSON 剖析器來確認負載平衡器、IP 集區及 NAT 規則：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="f8d3b-155">建立第一個網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="f8d3b-156">使用您自己的 Azure 訂用帳戶識別碼取代 `#####-###-###` 區段。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="f8d3b-157">當檢查您建立的資源時，會在 **jq** 的輸出中註明您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="f8d3b-158">您也可以使用 `azure account list`來檢視您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="f8d3b-159">下列範例會建立名為 `myNic1` 的 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="f8d3b-160">建立第二個 NIC。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-160">Create the second NIC.</span></span> <span data-ttu-id="f8d3b-161">下列範例會建立名為 `myNic2` 的 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="f8d3b-162">使用 JSON 剖析器來確認兩個 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="f8d3b-163">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-163">Create the network security group.</span></span> <span data-ttu-id="f8d3b-164">下列範例會建立名為 `myNetworkSecurityGroup` 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="f8d3b-165">新增兩個網路安全性群組的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="f8d3b-166">下列範例會建立兩個規則，名為 `myNetworkSecurityGroupRuleSSH` 和 `myNetworkSecurityGroupRuleHTTP`：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="f8d3b-167">使用 JSON 剖析器來確認網路安全性群組和輸入規則：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="f8d3b-168">將網路安全性群組繫結至兩個 NIC︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="f8d3b-169">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-169">Create the availability set.</span></span> <span data-ttu-id="f8d3b-170">下列範例會建立名為 `myAvailabilitySet` 的可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="f8d3b-171">建立第一個 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-171">Create the first Linux VM.</span></span> <span data-ttu-id="f8d3b-172">下列範例會建立名為 `myVM1` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="f8d3b-173">建立第二個 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-173">Create the second Linux VM.</span></span> <span data-ttu-id="f8d3b-174">下列範例會建立名為 `myVM2` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="f8d3b-175">使用 JSON 剖析器來確認已建置的所有項目︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="f8d3b-176">將您的新環境匯出成範本，以便快速重新建立新的執行個體：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f8d3b-177">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="f8d3b-177">Detailed walkthrough</span></span>
<span data-ttu-id="f8d3b-178">接下來的詳細步驟將說明您建置環境時每個命令的功能。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="f8d3b-179">當您建置自己的自訂開發環境或生產環境時，這些概念會相當有用。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="f8d3b-180">確定您已登入 [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，並且使用的是 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f8d3b-181">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f8d3b-182">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="f8d3b-183">建立資源群組並選擇部署位置</span><span class="sxs-lookup"><span data-stu-id="f8d3b-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="f8d3b-184">Azure 資源群組是邏輯部署實體，當中包含用來啟用資源部署邏輯管理的組態資訊和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="f8d3b-185">下列範例會在 `westeurope` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f8d3b-186">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f8d3b-187">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f8d3b-187">Create a storage account</span></span>
<span data-ttu-id="f8d3b-188">您需要儲存體帳戶來用於您的 VM 磁碟和任何您想要新增的額外資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="f8d3b-189">您幾乎是在建立資源群組之後立即建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="f8d3b-190">在這裡，我們使用 `azure storage account create` 命令，其中會傳遞帳戶的位置、控制它的資源群組，以及您想要的儲存體支援類型。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="f8d3b-191">下列範例會建立名為 `mystorageaccount` 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="f8d3b-192">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="f8d3b-193">若要使用 `azure group show` 命令來檢查我們的資源群組，讓我們使用 [jq](https://stedolan.github.io/jq/) 工具來搭配 `--json` Azure CLI 選項。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="f8d3b-194">(您可以使用 **jsawk** 或任何您慣用的語言程式庫來剖析 JSON。)</span><span class="sxs-lookup"><span data-stu-id="f8d3b-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="f8d3b-195">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="f8d3b-196">若要使用 CLI 來調查儲存體帳戶，您必須先設定帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="f8d3b-197">以您選擇的名稱取代下列範例中的儲存體帳戶名稱︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="f8d3b-198">然後您就可以輕鬆地檢視您的儲存體資訊︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="f8d3b-199">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="f8d3b-200">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="f8d3b-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="f8d3b-201">接著，您將需要建立一個在 Azure 中執行的虛擬網路，以及一個可供您建立 VM 的子網路。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="f8d3b-202">下列範例會建立名為 `myVnet` 的虛擬網路，位址首碼為 `192.168.0.0/16`：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="f8d3b-203">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="f8d3b-204">同樣地，讓我們使用 --json 選項 `azure group show` 和 `jq` 來查看我們如何建置資源。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="f8d3b-205">我們現在有 `storageAccounts` 資源和 `virtualNetworks` 資源。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="f8d3b-206">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="f8d3b-207">現在讓我們在要於其中部署 VM 的 `myVnet` 虛擬網路中建立子網路。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="f8d3b-208">我們將使用 `azure network vnet subnet create` 命令搭配我們已經建立的資源︰`myResourceGroup` 資源群組和 `myVnet` 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="f8d3b-209">在下列範例中，我們會新增名為 `mySubnet` 的子網路，子網路位址首碼為 `192.168.1.0/24`：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="f8d3b-210">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="f8d3b-211">由於子網路是以邏輯方式位於虛擬網路內，因此我們將使用略為不同的命令來尋找子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="f8d3b-212">我們使用的命令是 `azure network vnet show`，但是我們將繼續使用 `jq`來檢查 JSON 輸出。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="f8d3b-213">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="f8d3b-214">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f8d3b-214">Create a public IP address</span></span>
<span data-ttu-id="f8d3b-215">現在，讓我們建立將指派給您負載平衡器的公用 IP 位址 (PIP)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="f8d3b-216">它可讓您使用 `azure network public-ip create` 命令從網際網路連線到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="f8d3b-217">由於預設位址是動態位址，因此我們將使用 `--domain-name-label` 選項在 **cloudapp.azure.com** 網域中建立具名的 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="f8d3b-218">下列範例會建立名為 `myPublicIP` 的公用 IP，DNS 名稱為`mypublicdns`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="f8d3b-219">因為 DNS 名稱必須是唯一的，因此請提供您自己的唯一 DNS 名稱︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="f8d3b-220">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="f8d3b-221">公用 IP 位址也是最上層資源，因此您可以使用 `azure group show`來查看它。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="f8d3b-222">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="f8d3b-223">您可以使用完整的 `azure network public-ip show` 命令來調查更多資源詳細資料，包括子網域的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="f8d3b-224">公用 IP 位址資源已經以邏輯方式配置，但尚未指派特定位址。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="f8d3b-225">若要取得 IP 位址，您將需要一個負載平衡器，而我們尚未建立此負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="f8d3b-226">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="f8d3b-227">建立負載平衡器和 IP 集區</span><span class="sxs-lookup"><span data-stu-id="f8d3b-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="f8d3b-228">在建立負載平衡器的情況下，您將可以把流量分散到多個 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="f8d3b-229">它也會藉由執行多個 VM 以在進行維護或發生大量負載時回應使用者要求，為您的應用程式提供備援。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="f8d3b-230">下列範例會建立名為 `myLoadBalancer` 的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="f8d3b-231">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="f8d3b-232">我們的負載平衡器很空，因此讓我們建立一些 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="f8d3b-233">我們想要為負載平衡器建立兩個 IP 集區，一個用於前端，一個用於後端。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="f8d3b-234">前端 IP 集區會公開顯示。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="f8d3b-235">它也是我們指派稍早所建立 PIP 的位置。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="f8d3b-236">然後，我們將使用後端集區作為我們 VM 要連接的位置。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="f8d3b-237">這樣一來，流量便可以經由負載平衡器流向 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="f8d3b-238">首先，讓我們建立前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="f8d3b-239">下列範例會建立名為 `myFrontEndPool` 的前端集區：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="f8d3b-240">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="f8d3b-241">請注意我們如何使用 `--public-ip-name` 參數來傳入我們稍早建立的 `myPublicIP`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="f8d3b-242">將公用 IP 位址指派給負載平衡器可讓您透過網際網路連線到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="f8d3b-243">接下來，讓我們建立第二個 IP 集區，這次是針對我們的後端流量。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="f8d3b-244">下列範例會建立名為 `myBackEndPool` 的後端集區：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="f8d3b-245">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="f8d3b-246">我們可以使用 `azure network lb show` 並檢查 JSON 輸出，來查看負載平衡器的執行情況：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="f8d3b-247">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="f8d3b-248">建立負載平衡器 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="f8d3b-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="f8d3b-249">若要讓流量流經負載平衡器，我們需要建立指定輸入或輸出動作的網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="f8d3b-250">您可以指定要使用的通訊協定，然後依需要將外部連接埠對應到內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="f8d3b-251">在我們的環境中，建立一些規則以允許 SSH 透過負載平衡器流向 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="f8d3b-252">我們將設定 TCP 連接埠 4222 和 4223 以導向 VM 上的 TCP 連接埠 22 (我們會在稍後建立)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="f8d3b-253">下列範例會建立名為 `myLoadBalancerRuleSSH1` 的規則以將 TCP 連接埠 4222 對應至連接埠 22：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="f8d3b-254">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="f8d3b-255">針對進行 SSH 的第二個 NAT 規則，重複此程序。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="f8d3b-256">下列範例會建立名為 `myLoadBalancerRuleSSH2` 的規則以將 TCP 連接埠 4223 對應至連接埠 22：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="f8d3b-257">讓我們繼續進行，並針對 web 流量建立 TCP 連接埠 80 的 NAT 規則，以將規則連結到我們的 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="f8d3b-258">如果我們將規則連結到 IP 集區，而不是將規則個別連結到 VM，則我們可在 IP 集區中新增或移除 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="f8d3b-259">負載平衡器會自動調整流量的流動。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="f8d3b-260">下列範例會建立名為 `myLoadBalancerRuleWeb` 的規則以將 TCP 連接埠 80 對應至連接埠 80：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="f8d3b-261">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="f8d3b-262">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="f8d3b-262">Create a load balancer health probe</span></span>
<span data-ttu-id="f8d3b-263">健全狀況探查會定期檢查受負載平衡器保護的 VM，以確定它們依定義的方式運作及回應要求。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="f8d3b-264">否則，就從將它們從作業中移除，以確保不會將使用者導向到它們。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="f8d3b-265">您可以定義健全狀況探查的自訂檢查，以及間隔和逾時值。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="f8d3b-266">如需有關健全狀況探查的詳細資訊，請參閱 [負載平衡器探查](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f8d3b-267">下列範例會建立名為 `myHealthProbe` 的 TCP 健全狀況探查：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="f8d3b-268">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="f8d3b-269">在這裡，我們指定了 15 秒的健全狀況檢查間隔。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="f8d3b-270">最多可錯過 4 次探查 (1 分鐘)，負載平衡器才會將該主機視為已不再運作。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="f8d3b-271">確認負載平衡器</span><span class="sxs-lookup"><span data-stu-id="f8d3b-271">Verify the load balancer</span></span>
<span data-ttu-id="f8d3b-272">現在，負載平衡器設定已完成。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="f8d3b-273">以下是您所採取的步驟：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="f8d3b-274">您建立了負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-274">You created a load balancer.</span></span>
2. <span data-ttu-id="f8d3b-275">您建立了前端 IP 集區並為它指派公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="f8d3b-276">您建立了 VM 可以連接的後端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="f8d3b-277">您建立了可允許透過 SSH 連接到 VM 以進行管理的 NAT 規則，以及可允許將 TCP 連接埠 80 用於 Web 應用程式的規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="f8d3b-278">您新增了健全狀況探查來定期檢查 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="f8d3b-279">這個健全狀況探查可確保使用者不會嘗試存取已不再運作或提供內容的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="f8d3b-280">讓我們檢閱您負載平衡器現在的樣子︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="f8d3b-281">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="f8d3b-282">建立要與 Linux VM 搭配使用的 NIC</span><span class="sxs-lookup"><span data-stu-id="f8d3b-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="f8d3b-283">您可以透過程式設計方式提供 NIC，因為您可以將規則套用到 NIC 的使用上。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="f8d3b-284">您也可以有多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-284">You can also have more than one.</span></span> <span data-ttu-id="f8d3b-285">在下列 `azure network nic create` 命令中，您會將 NIC 連結到負載後端 IP 集區，並將它與 NAT 規則建立關聯以允許 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="f8d3b-286">使用您自己的 Azure 訂用帳戶識別碼取代 `#####-###-###` 區段。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="f8d3b-287">當檢查您建立的資源時，會在 `jq` 的輸出中註明您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="f8d3b-288">您也可以使用 `azure account list`來檢視您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="f8d3b-289">下列範例會建立名為 `myNic1` 的 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="f8d3b-290">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="f8d3b-291">您可以直接檢查資源來查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="f8d3b-292">您可以使用 `azure network nic show` 命令來檢查資源︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="f8d3b-293">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="f8d3b-294">現在，我們將建立的第二個 NIC，其中會再次將它連結到我們的後端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="f8d3b-295">這一次，第二個 NAT 規則將允許 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="f8d3b-296">下列範例會建立名為 `myNic2` 的 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="f8d3b-297">建立網路安全性群組和規則</span><span class="sxs-lookup"><span data-stu-id="f8d3b-297">Create a network security group and rules</span></span>
<span data-ttu-id="f8d3b-298">我們現在會建立網路安全性群組和管理 NIC 存取權的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="f8d3b-299">網路安全性群組可以套用至 NIC 或子網路。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="f8d3b-300">您要定義規則以控制進出 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="f8d3b-301">下列範例會建立名為 `myNetworkSecurityGroup` 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="f8d3b-302">讓我們加入 NSG 的輸入規則以允許連接埠 22 上的輸入連線 (以支援 SSH)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="f8d3b-303">下列範例會建立名為 `myNetworkSecurityGroupRuleSSH` 的規則以允許連接埠 22 上的 TCP︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="f8d3b-304">現在讓我們加入 NSG 的輸入規則以允許連接埠 80 上的輸入連線 (以支援 web 流量)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="f8d3b-305">下列範例會建立名為 `myNetworkSecurityGroupRuleHTTP` 的規則以允許連接埠 80 上的 TCP︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="f8d3b-306">輸入規則是輸入網路連線的篩選器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="f8d3b-307">在此範例中，我們將 NSG 繫結至 VM 虛擬 NIC，這意謂著任何傳送給連接埠 22 的要求都會傳遞到 VM 上的 NIC。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="f8d3b-308">這個輸入規則與網路連線相關，而不是與端點 (在傳統部署中會相關的對象) 相關。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="f8d3b-309">若要開啟連接埠，您必須將 `--source-port-range` 保留設定為 '\*' (預設)，才能接受來自**「任何」**要求連接埠的輸入要求。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="f8d3b-310">連接埠通常是動態的。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="f8d3b-311">繫結至 NIC</span><span class="sxs-lookup"><span data-stu-id="f8d3b-311">Bind to the NIC</span></span>
<span data-ttu-id="f8d3b-312">將 NSG 繫結至 NIC。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="f8d3b-313">我們需要將 NIC 與我們的網路安全性群組連線。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="f8d3b-314">執行這兩個命令來連結我們的兩個 NIC：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="f8d3b-315">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="f8d3b-315">Create an availability set</span></span>
<span data-ttu-id="f8d3b-316">可用性設定組可協助將 VM 分散到容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="f8d3b-317">為 VM 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="f8d3b-318">下列範例會建立名為 `myAvailabilitySet` 的可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="f8d3b-319">容錯網域定義一個虛擬機器群組，且群組內的虛擬機器會共用通用電源和網路交換器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="f8d3b-320">根據預設，可用性設定組內設定的虛擬機器最多可分散到三個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="f8d3b-321">這裡的概念是，其中一個容錯網域中的硬體問題將不會影響每個執行您應用程式的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="f8d3b-322">將多個 VM 放在一個可用性設定組中時，Azure 會自動將它們分散到容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="f8d3b-323">升級網域表示虛擬機器群組和可同時重新啟動的基礎實體硬體。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="f8d3b-324">在計劃性維護期間，可能不會循序重新啟動升級網域，而只會一次重新啟動一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="f8d3b-325">同樣地，將多個 VM 放在一個可用性設定網站中時，Azure 會自動將它們分散到升級網域。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="f8d3b-326">深入了解 [管理 VM 的可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="f8d3b-327">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f8d3b-327">Create the Linux VMs</span></span>
<span data-ttu-id="f8d3b-328">您已建立儲存體和網路資源來支援可存取網際網路的 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="f8d3b-329">現在，讓我們建立這些 VM，並利用沒有密碼的 SSH 金鑰來保障其安全。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="f8d3b-330">在此情況下，我們要根據最新的 LTS 建立 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="f8d3b-331">我們會使用 `azure vm image list`來找出該映像資訊 (如 [尋找 Azure VM 映像](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)所述)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f8d3b-332">我們之前使用 `azure vm image list westeurope canonical | grep LTS`命令來選取映像。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="f8d3b-333">在此案例中，我們會使用 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="f8d3b-334">針對最後一個欄位，我們會傳遞 `latest` ，如此在未來我們就一律會取得最新的組建。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="f8d3b-335">(我們使用的字串是 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="f8d3b-336">對於任何已經使用 **ssh-keygen -t rsa -b 2048**在 Linux 或 Mac 上建立 ssh rsa 公用和私密金鑰組的人來說，這下一個步驟都是相當熟悉的步驟。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="f8d3b-337">如果您的 `~/.ssh` 目錄中沒有任何憑證金鑰組，您可以建立它們︰</span><span class="sxs-lookup"><span data-stu-id="f8d3b-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="f8d3b-338">藉由使用 `azure vm create --generate-ssh-keys` 選項來自動建立。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="f8d3b-339">藉由使用 [自行建立的指示](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來手動建立。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f8d3b-340">或者，您也可以使用 `--admin-password` 方法，在 VM 建立後驗證 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="f8d3b-341">這個方法通常較不安全。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-341">This method is typically less secure.</span></span>

<span data-ttu-id="f8d3b-342">我們會使用 `azure vm create` 命令將所有資源和資訊結合在一起來建立 VM：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="f8d3b-343">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="f8d3b-344">您可以使用預設 SSH 金鑰來立即連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="f8d3b-345">請確定您指定的連接埠正確，因為我們要通過的是負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="f8d3b-346">(針對第一個 VM，我們設定了將連接埠 4222 轉送到 VM 的 NAT 規則。)</span><span class="sxs-lookup"><span data-stu-id="f8d3b-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="f8d3b-347">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="f8d3b-348">繼續進行，並以相同方式建立第二個 VM：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="f8d3b-349">您現在可以使用 `azure vm show myResourceGroup myVM1` 命令來檢查您已建立的項目。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="f8d3b-350">此時，您的 Ubuntu VM 是在 Azure 中的負載平衡器後方執行，您只能利用 SSH 金鑰組來登入 (因為密碼已被停用)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="f8d3b-351">您可以安裝 nginx 或 httpd、部署 Web 應用程式，然後查看經由負載平衡器流向兩個 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="f8d3b-352">輸出：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="f8d3b-353">將環境匯出為範本</span><span class="sxs-lookup"><span data-stu-id="f8d3b-353">Export the environment as a template</span></span>
<span data-ttu-id="f8d3b-354">您現在已經建立這個環境，如果您想要使用相同的參數來建立其他開發環境，或想要建立與其相符的生產環境時，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="f8d3b-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="f8d3b-355">Resource Manager 可使用定義了所有環境參數的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="f8d3b-356">您可以藉由參考此 JSON 範本來建置整個環境。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="f8d3b-357">您可以 [手動建立 JSON 範本](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，或將現有的環境匯出來為您建立 JSON 範本：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="f8d3b-358">此命令會在您目前的工作目錄中建立 `myResourceGroup.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="f8d3b-359">當您從這個範本建立環境時，系統會提示您輸入所有資源名稱，包括負載平衡器、網路介面或 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="f8d3b-360">您可以藉由將 `-p` 或 `--includeParameterDefaultValue` 參數新增至稍早所示的 `azure group export` 命令中，在您的範本檔案中填入這些名稱。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="f8d3b-361">請編輯您的 JSON 範本以指定資源名稱，或 [建立 parameters.json 檔案](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來指定資源名稱。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="f8d3b-362">從範本建立環境：</span><span class="sxs-lookup"><span data-stu-id="f8d3b-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="f8d3b-363">您可以 [深入了解如何從範本進行部署](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f8d3b-364">請了解如何以累加方式更新環境、使用參數檔案，以及從單一儲存體位置存取範本。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8d3b-365">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8d3b-365">Next steps</span></span>
<span data-ttu-id="f8d3b-366">現在您已準備好開始使用多個網路元件和 VM。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="f8d3b-367">您可以利用這裡介紹的核心元件，使用這個範例環境來建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8d3b-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
