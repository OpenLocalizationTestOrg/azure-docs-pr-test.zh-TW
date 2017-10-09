---
title: "aaaAccess 和 Azure Linux Vm 範本中的安全性 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="cce61-103">適用於 Linux VM 之 Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="cce61-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="cce61-104">應用程式裝載於 Azure 可能會需要 toobe 存取 hello 透過網際網路或 VPN / 使用 Azure Express Route 連線。</span><span class="sxs-lookup"><span data-stu-id="cce61-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="cce61-105">Hello Music Store 應用程式範例中，與 hello 網站可在網際網路 hello 與公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cce61-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="cce61-106">透過建立的存取權，連線 toohello 應用程式及存取 toohello 虛擬機器資源本身應該進行保護。</span><span class="sxs-lookup"><span data-stu-id="cce61-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="cce61-107">這項存取安全性是透過「網路安全性群組」來提供。</span><span class="sxs-lookup"><span data-stu-id="cce61-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="cce61-108">這份文件詳細說明如何保護 hello 範例 Azure Resource Manager 範本中的 hello Music Store 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cce61-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="cce61-109">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="cce61-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="cce61-110">Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cce61-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="cce61-111">hello 完成範本可以在這裡 – 找到[音樂存放部署在 Ubuntu 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。</span><span class="sxs-lookup"><span data-stu-id="cce61-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="cce61-112">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="cce61-112">Public IP Address</span></span>
<span data-ttu-id="cce61-113">可以使用 tooprovide 公用存取 tooan Azure 資源，公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="cce61-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="cce61-114">您可以使用靜態或動態 IP 位址來設定公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cce61-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="cce61-115">如果使用動態位址，而且 hello 虛擬機器停止並取消配置，則會移除 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="cce61-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="cce61-116">當 hello 機器一次啟動時，它可能會指派不同的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cce61-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="cce61-117">tooprevent 的 IP 位址變更，就可以使用保留的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cce61-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="cce61-118">公用 IP 位址可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或藉由插入範本中的有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="cce61-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="cce61-119">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[公用 IP 位址](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121)。</span><span class="sxs-lookup"><span data-stu-id="cce61-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="cce61-120">「公用 IP 位址」可以與「虛擬網路介面卡」或「負載平衡器」關聯。</span><span class="sxs-lookup"><span data-stu-id="cce61-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="cce61-121">在此範例中，因為 hello Music Store 網站正進行負載平衡跨數個虛擬機器，hello 公用 IP 位址會是附加的 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="cce61-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="cce61-122">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與負載平衡器的公用 IP 位址關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208)。</span><span class="sxs-lookup"><span data-stu-id="cce61-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="cce61-123">hello 做為公用 IP 位址從看到 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cce61-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="cce61-124">請注意，hello 公用 IP 位址相關聯的 tooa 負載平衡器並不是虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cce61-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="cce61-125">網路負載平衡器的詳細 hello 本系列的下一個文件。</span><span class="sxs-lookup"><span data-stu-id="cce61-125">Network load balancers are detailed in hello next document of this series.</span></span>

![公用 IP 位址](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="cce61-127">如需有關「Azure 公用 IP 位址」的詳細資訊，請參閱 [Azure 中的 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="cce61-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="cce61-128">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="cce61-128">Network Security Group</span></span>
<span data-ttu-id="cce61-129">一旦存取已建立的 tooAzure 資源，這項存取應該限制。</span><span class="sxs-lookup"><span data-stu-id="cce61-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="cce61-130">就 Azure 虛擬機器而言，是使用「網路安全性群組」來達到保護存取的目的。</span><span class="sxs-lookup"><span data-stu-id="cce61-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="cce61-131">與 hello Music Store 應用程式範例中，所有存取 toohello 虛擬機器都是除了限制透過 http 存取的連接埠 80 和通訊埠 22 SSH 存取。</span><span class="sxs-lookup"><span data-stu-id="cce61-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="cce61-132">網路安全性群組可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或藉由插入範本中的有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="cce61-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="cce61-133">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路安全性群組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68)。</span><span class="sxs-lookup"><span data-stu-id="cce61-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

<span data-ttu-id="cce61-134">在此範例中，hello 網路安全性群組是與 hello hello 虛擬網路的資源中宣告的子網路物件相關聯。</span><span class="sxs-lookup"><span data-stu-id="cce61-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="cce61-135">請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與虛擬網路的網路安全性群組關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158)。</span><span class="sxs-lookup"><span data-stu-id="cce61-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

<span data-ttu-id="cce61-136">以下是哪個 hello 網路安全性群組看起來像 hello 從 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cce61-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="cce61-137">請注意，NSG 可以與子網路和 (或) 網路介面關聯。</span><span class="sxs-lookup"><span data-stu-id="cce61-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="cce61-138">在此情況下，hello NSG 是相關聯的 tooa 子網路。</span><span class="sxs-lookup"><span data-stu-id="cce61-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="cce61-139">在此組態中，hello 輸入的規則套用 tooall 連接虛擬機器 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="cce61-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![網路安全性群組](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="cce61-141">如需有關「網路安全性群組」的深入資訊，請參閱[什麼是網路安全性群組](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)。</span><span class="sxs-lookup"><span data-stu-id="cce61-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="cce61-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cce61-142">Next step</span></span>
<hr>

[<span data-ttu-id="cce61-143">步驟 3 - Azure Resource Manager 範本中的可用性和規模</span><span class="sxs-lookup"><span data-stu-id="cce61-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

