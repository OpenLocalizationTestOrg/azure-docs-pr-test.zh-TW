---
title: "aaaOpen 連接埠 tooa VM 使用 Azure PowerShell |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Windows VM / 使用 hello Azure 資源管理員部署模式和 Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="5a251-103">如何 tooopen 連接埠和端點 tooa 使用 PowerShell 在 Azure 中的 VM</span><span class="sxs-lookup"><span data-stu-id="5a251-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="5a251-104">快速命令</span><span class="sxs-lookup"><span data-stu-id="5a251-104">Quick commands</span></span>
<span data-ttu-id="5a251-105">toocreate 網路安全性的群組和 ACL 規則您需要[hello 最新版本的 Azure PowerShell 安裝](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="5a251-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="5a251-106">您也可以[使用 hello Azure 入口網站執行這些步驟](nsg-quickstart-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5a251-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="5a251-107">Azure 帳戶登入 tooyour 中：</span><span class="sxs-lookup"><span data-stu-id="5a251-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5a251-108">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5a251-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5a251-109">範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。</span><span class="sxs-lookup"><span data-stu-id="5a251-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="5a251-110">使用 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) 建立規則。</span><span class="sxs-lookup"><span data-stu-id="5a251-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="5a251-111">hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow *tcp*連接埠的流量*80*:</span><span class="sxs-lookup"><span data-stu-id="5a251-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="5a251-112">接下來，建立您的網路安全性群組與[新增 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)和指派 hello HTTP 規則您剛剛建立，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5a251-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="5a251-113">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5a251-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="5a251-114">現在讓我們將您的網路安全性群組 tooa 子網路指派。</span><span class="sxs-lookup"><span data-stu-id="5a251-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="5a251-115">hello 下列範例會將指派現有的虛擬網路，名為*myVnet* toohello 變數*$vnet*與[Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="5a251-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="5a251-116">使用 [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) 將網路安全性群組與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="5a251-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="5a251-117">hello 下列範例將名為 「 hello 」 子網路*mySubnet*與您的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="5a251-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="5a251-118">最後，更新虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)為了讓您變更 tootake 效果：</span><span class="sxs-lookup"><span data-stu-id="5a251-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="5a251-119">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="5a251-119">More information on Network Security Groups</span></span>
<span data-ttu-id="5a251-120">這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。</span><span class="sxs-lookup"><span data-stu-id="5a251-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="5a251-121">網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="5a251-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="5a251-122">您可以深入了解 [建立網路安全性群組和 ACL 規則](tutorial-virtual-network.md#manage-internal-traffic)。</span><span class="sxs-lookup"><span data-stu-id="5a251-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="5a251-123">針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。</span><span class="sxs-lookup"><span data-stu-id="5a251-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="5a251-124">hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5a251-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="5a251-125">如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="5a251-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a251-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a251-126">Next steps</span></span>
<span data-ttu-id="5a251-127">在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="5a251-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="5a251-128">您可以找到有關 hello 下列文件中建立更詳細的環境：</span><span class="sxs-lookup"><span data-stu-id="5a251-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="5a251-129">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="5a251-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="5a251-130">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="5a251-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="5a251-131">負載平衡器的 Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="5a251-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

