---
title: "在多個 IP 組態中使用 Azure CLI 平衡 aaaLoad |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址使用 Azure CLI tooa 虛擬機器 |資源管理員。"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="2eb91-103">在多個 IP 組態上進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="2eb91-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2eb91-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="2eb91-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="2eb91-105">CLI</span><span class="sxs-lookup"><span data-stu-id="2eb91-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="2eb91-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2eb91-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="2eb91-107">本文說明如何 toouse Azure 負載平衡器與多個 IP 位址上的次要網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="2eb91-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="2eb91-108">在此案例中，我們有兩部執行 Windows 的 VM，每部各有一個主要和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="2eb91-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="2eb91-109">每個次要 hello Nic 有兩個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="2eb91-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="2eb91-110">每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站會繫結的 tooone 的 hello hello 次要 NIC 上的 IP 組態</span><span class="sxs-lookup"><span data-stu-id="2eb91-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="2eb91-111">我們使用 Azure 負載平衡器 tooexpose 兩個前端 IP 位址，一個用於每個網站，toodistribute 流量 toohello 個別的 IP 組態 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="2eb91-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="2eb91-112">這種情況下使用 hello 跨前端，以及兩個後端集區 IP 位址相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="2eb91-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="2eb91-114">多個 IP 組態步驟 tooload 餘額</span><span class="sxs-lookup"><span data-stu-id="2eb91-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="2eb91-115">請遵循下面這篇文章所述的 tooachieve hello 案例 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2eb91-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="2eb91-116">[安裝和設定 hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI 依照 hello 連結的發行項和記錄檔中的 hello 步驟新增到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2eb91-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="2eb91-117">如上所述[建立資源群組](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) (稱為 contosofabrikam)。</span><span class="sxs-lookup"><span data-stu-id="2eb91-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="2eb91-118">[建立可用性設定組](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set)toofor hello 兩個 Vm。</span><span class="sxs-lookup"><span data-stu-id="2eb91-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="2eb91-119">此案例中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2eb91-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="2eb91-120">[建立虛擬網路](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) (稱為 myVNet) 和子網路 (稱為 mySubnet)：</span><span class="sxs-lookup"><span data-stu-id="2eb91-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="2eb91-121">[建立 hello 負載平衡器](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json)呼叫*mylb*:</span><span class="sxs-lookup"><span data-stu-id="2eb91-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="2eb91-122">建立兩個動態公用 IP 位址 hello 前端 IP 組態，您的負載平衡器的：</span><span class="sxs-lookup"><span data-stu-id="2eb91-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="2eb91-123">建立 hello 兩個前端 IP 組態*contosofe*和*fabrikamfe*分別：</span><span class="sxs-lookup"><span data-stu-id="2eb91-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="2eb91-124">建立後端位址集區 - contosopool 和 fabrikampool、[探查](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - HTTP，和負載平衡規則 - HTTPc 和 HTTPf：</span><span class="sxs-lookup"><span data-stu-id="2eb91-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="2eb91-125">執行的 hello 下列以下命令，然後核取 hello 輸出太[確認您的負載平衡器](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json)已正確建立：</span><span class="sxs-lookup"><span data-stu-id="2eb91-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="2eb91-126">為第一個虛擬機器 VM1 [建立公用 IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address) (myPublicIp) 和[儲存體帳戶](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (mystorageaccont1)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2eb91-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="2eb91-127">[網路介面建立 hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) VM1 的並加入第二個 IP 組態， *VM1 ipconfig2*，和[建立 hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms)如下所示：</span><span class="sxs-lookup"><span data-stu-id="2eb91-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="2eb91-128">為第二個 VM 重複步驟 10 至 11：</span><span class="sxs-lookup"><span data-stu-id="2eb91-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="2eb91-129">最後，您必須設定 DNS 資源記錄 toopoint toohello 各自的前端 IP 位址的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2eb91-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="2eb91-130">您可以在 Azure DNS 中裝載網域。</span><span class="sxs-lookup"><span data-stu-id="2eb91-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="2eb91-131">如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2eb91-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2eb91-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2eb91-132">Next steps</span></span>
- <span data-ttu-id="2eb91-133">深入了解如何 toocombine 負載平衡服務在 Azure 中[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="2eb91-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="2eb91-134">了解如何在 Azure toomanage 中使用不同類型的記錄檔，以及疑難排解負載平衡器中的[Azure 負載平衡器的記錄分析](../load-balancer/load-balancer-monitor-log.md)。</span><span class="sxs-lookup"><span data-stu-id="2eb91-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
