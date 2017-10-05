---
title: "適用於 Windows VM 之 Azure 範本中的存取和安全性 | Microsoft Docs"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ad1b5c4763cf56f681a50bb1bccc825311bbfdf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="b8bb8-103">適用於 Windows VM 之 Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="b8bb8-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="b8bb8-104">存取裝載在 Azure 中的應用程式時，可能需要透過網際網路或與 Azure 的 VPN/Express Route 連線才能存取。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="b8bb8-105">在「音樂市集」應用程式範例中，是透過公用 IP 位址讓網站在網際網路上可供使用。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="b8bb8-106">建立存取方式之後，應該保護對應用程式的連線，以及對虛擬機器資源本身的存取。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="b8bb8-107">這項存取安全性是透過「網路安全性群組」來提供。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="b8bb8-108">本文件詳細說明範例 Azure Resource Manager 範本中如何保護「音樂市集」應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="b8bb8-109">所有相依項目和獨特的設定都會以醒目提示的方式標示。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="b8bb8-110">為了獲得最佳體驗，請將一個解決方案執行個體預先部署到您的 Azure 訂用帳戶，然後與 Azure Resource Manager 範本搭配運作。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="b8bb8-111">您可以在下列連結找到完整的範本 – [Windows 上的音樂市集部署](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="b8bb8-112">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b8bb8-112">Public IP Address</span></span>
<span data-ttu-id="b8bb8-113">若要提供對 Azure 資源的公用存取，可以使用公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="b8bb8-114">您可以使用靜態或動態 IP 位址來設定公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="b8bb8-115">如果使用靜態位址，當虛擬機器被停止並解除配置時，系統就會移除該位址。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="b8bb8-116">當機器重新啟動時，系統可能會為它指派不同的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="b8bb8-117">若要防止 IP 位址變更，可以使用保留的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="b8bb8-118">您可以透過使用 Visual Studio 的「加入新資源精靈」或在範本中插入有效的 JSON，將「公用 IP 位址」新增至 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="b8bb8-119">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [公用 IP 位址](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="b8bb8-120">「公用 IP 位址」可以與「虛擬網路介面卡」或「負載平衡器」關聯。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="b8bb8-121">在此範例中，由於「音樂市集」網站的負載會在數部虛擬機器之間進行平衡，因此「公用 IP 位址」會連接至「負載平衡器」。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="b8bb8-122">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [公用 IP 位址與負載平衡器的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="b8bb8-123">Azure 入口網站中所示的公用 IP 位址樣子。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="b8bb8-124">請注意，公用 IP 位址是與負載平衡器關聯，而不是虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="b8bb8-125">本系列的下一個文件中將會詳細說明網路負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-125">Network load balancers are detailed in the next document of this series.</span></span>

![公用 IP 位址](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="b8bb8-127">如需有關「Azure 公用 IP 位址」的詳細資訊，請參閱 [Azure 中的 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="b8bb8-128">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b8bb8-128">Network Security Group</span></span>
<span data-ttu-id="b8bb8-129">建立對 Azure 資源的存取方式之後，應該對此存取進行限制。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="b8bb8-130">就 Azure 虛擬機器而言，是使用「網路安全性群組」來達到保護存取的目的。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="b8bb8-131">在「音樂市集」應用程式範例中，除了透過連接埠 80 進行的 http 存取和透過連接埠 3389 進行的 RDP 存取之外，所有對虛擬機器的存取都會受到限制。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="b8bb8-132">您可以透過使用 Visual Studio 的「加入新資源精靈」或在範本中插入有效的 JSON，將「網路安全性群組」新增至 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="b8bb8-133">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [網路安全性群組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
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
},
```

<span data-ttu-id="b8bb8-134">在此範例中，網路安全性群組是與「虛擬網路」資源中宣告的子網路物件關聯。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="b8bb8-135">請依循下列連結來查看 Resource Manager 範本內的 JSON 範例 – [網路安全性群組與虛擬網路的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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
]
```

<span data-ttu-id="b8bb8-136">以下是網路安全性群組在 Azure 入口網站中看起來的樣子。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="b8bb8-137">請注意，NSG 可以與子網路和 (或) 網路介面關聯。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="b8bb8-138">在此案例中，NSG 是與子網路關聯。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="b8bb8-139">在此組態中，輸入規則會套用至連接到子網路的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![網路安全性群組](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="b8bb8-141">如需有關「網路安全性群組」的深入資訊，請參閱[什麼是網路安全性群組](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)。</span><span class="sxs-lookup"><span data-stu-id="b8bb8-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="b8bb8-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8bb8-142">Next step</span></span>
<hr>

[<span data-ttu-id="b8bb8-143">步驟 3 - Azure Resource Manager 範本中的可用性和規模</span><span class="sxs-lookup"><span data-stu-id="b8bb8-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

