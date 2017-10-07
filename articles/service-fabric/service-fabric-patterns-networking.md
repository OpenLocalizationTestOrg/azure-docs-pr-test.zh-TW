---
title: "適用於 Azure Service Fabric aaaNetworking 模式 |Microsoft 文件"
description: "描述常見的網路模式適用於 Service Fabric 以及 toocreate 叢集中使用 Azure 網路的功能。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="2adaa-103">Service Fabric 網路功能模式</span><span class="sxs-lookup"><span data-stu-id="2adaa-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="2adaa-104">您可以將 Azure Service Fabric 叢集與其他的 Azure 網路功能整合起來。</span><span class="sxs-lookup"><span data-stu-id="2adaa-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="2adaa-105">在本文中，我們會示範如何 toocreate 叢集該使用 hello，下列功能：</span><span class="sxs-lookup"><span data-stu-id="2adaa-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="2adaa-106">現有虛擬網路或子網路</span><span class="sxs-lookup"><span data-stu-id="2adaa-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="2adaa-107">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2adaa-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="2adaa-108">僅內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2adaa-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="2adaa-109">內部與外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2adaa-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="2adaa-110">Service Fabric 會在標準的虛擬機器擴展集內執行。</span><span class="sxs-lookup"><span data-stu-id="2adaa-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="2adaa-111">能在虛擬機器擴展集內使用的功能，就能在 Service Fabric 叢集內使用。</span><span class="sxs-lookup"><span data-stu-id="2adaa-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="2adaa-112">hello 網路區段的虛擬機器擴展集和服務網狀架構的 hello Azure Resource Manager 範本完全相同。</span><span class="sxs-lookup"><span data-stu-id="2adaa-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="2adaa-113">部署 tooan 現有的虛擬網路之後，它是簡單 tooincorporate 其他網路功能，例如 Azure ExpressRoute、 Azure VPN 閘道、 網路安全性群組，和虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="2adaa-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="2adaa-114">Service Fabric 有一個方面是其他網路功能所沒有的。</span><span class="sxs-lookup"><span data-stu-id="2adaa-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="2adaa-115">hello [Azure 入口網站](https://portal.azure.com)在內部使用 hello Service Fabric 資源提供者 toocall tooa 叢集 tooget 資訊節點和應用程式。</span><span class="sxs-lookup"><span data-stu-id="2adaa-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="2adaa-116">hello Service Fabric 資源提供者需要可公開存取的輸入的存取 toohello HTTP 閘道連接埠 （連接埠 19080，預設值） 上 hello 管理端點。</span><span class="sxs-lookup"><span data-stu-id="2adaa-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="2adaa-117">[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)使用 hello 管理端點 toomanage 您的叢集。</span><span class="sxs-lookup"><span data-stu-id="2adaa-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="2adaa-118">hello Service Fabric 資源提供者也會使用您的叢集 toodisplay hello Azure 入口網站中有關此連接埠 tooquery 資訊。</span><span class="sxs-lookup"><span data-stu-id="2adaa-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="2adaa-119">若連接埠 19080 不能從 hello Service Fabric 資源提供者存取，訊息中，例如*找不到節點*會出現在 hello 入口網站，而且節點和應用程式的清單會出現空白。</span><span class="sxs-lookup"><span data-stu-id="2adaa-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="2adaa-120">如果您想 toosee 您 hello Azure 入口網站中的叢集，您的負載平衡器必須公開公用 IP 位址，而且您的網路安全性群組必須允許 19080 的連接埠的連入流量。</span><span class="sxs-lookup"><span data-stu-id="2adaa-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="2adaa-121">如果您的設定不符合這些需求，hello Azure 入口網站不會顯示叢集的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="2adaa-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="2adaa-122">範本</span><span class="sxs-lookup"><span data-stu-id="2adaa-122">Templates</span></span>

<span data-ttu-id="2adaa-123">所有 Service Fabric 範本都位於[一個下載檔案](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)中。</span><span class="sxs-lookup"><span data-stu-id="2adaa-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="2adaa-124">您應該要能夠 toodeploy hello 範本做為使用下列 PowerShell 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="2adaa-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="2adaa-125">如果您要部署的 hello 現有 Azure 虛擬網路的範本或 hello 靜態公用 IP 範本，先閱讀 hello[初始安裝](#initialsetup)本文一節。</span><span class="sxs-lookup"><span data-stu-id="2adaa-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="2adaa-126">初始設定</span><span class="sxs-lookup"><span data-stu-id="2adaa-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="2adaa-127">現有的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2adaa-127">Existing virtual network</span></span>

<span data-ttu-id="2adaa-128">在下列範例的 hello，我們開頭現有的虛擬網路中 hello 命名 ExistingRG vnet **ExistingRG**資源群組。</span><span class="sxs-lookup"><span data-stu-id="2adaa-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="2adaa-129">hello 子網路是名為 default。</span><span class="sxs-lookup"><span data-stu-id="2adaa-129">hello subnet is named default.</span></span> <span data-ttu-id="2adaa-130">當您使用 hello Azure 入口網站 toocreate 標準的虛擬機器 (VM) 時，會建立這些預設的資源。</span><span class="sxs-lookup"><span data-stu-id="2adaa-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="2adaa-131">您可以建立 hello 虛擬網路和子網路，而不需要建立 hello VM，但 hello 新增叢集 tooan 現有虛擬網路的主要目標是 tooprovide 網路連線 tooother Vm。</span><span class="sxs-lookup"><span data-stu-id="2adaa-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="2adaa-132">建立 hello VM 提供現有的虛擬網路通常是很好範例。</span><span class="sxs-lookup"><span data-stu-id="2adaa-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="2adaa-133">如果您的 Service Fabric 叢集使用只使用內部負載平衡器，沒有公用 IP 位址，您可以使用 VM，其為安全的公用 IP hello*跳方塊*。</span><span class="sxs-lookup"><span data-stu-id="2adaa-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="2adaa-134">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2adaa-134">Static public IP address</span></span>

<span data-ttu-id="2adaa-135">靜態公用 IP 位址通常是從指派給 vm 的 hello 分開管理的專用的資源。</span><span class="sxs-lookup"><span data-stu-id="2adaa-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="2adaa-136">它是在專用的網路資源群組中提供 （做為相對於的 tooin hello Service Fabric 叢集資源群組本身）。</span><span class="sxs-lookup"><span data-stu-id="2adaa-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="2adaa-137">建立名為 staticIP1 hello 中的靜態公用 IP 位址相同 ExistingRG 資源群組中的，在 hello Azure 入口網站或 PowerShell，透過：</span><span class="sxs-lookup"><span data-stu-id="2adaa-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="2adaa-138">Service Fabric 範本</span><span class="sxs-lookup"><span data-stu-id="2adaa-138">Service Fabric template</span></span>

<span data-ttu-id="2adaa-139">在本文中的 hello 範例，我們會使用 hello Service Fabric template.json。</span><span class="sxs-lookup"><span data-stu-id="2adaa-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="2adaa-140">建立叢集之前，您可以使用 hello 標準入口網站精靈 toodownload hello 範本從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2adaa-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="2adaa-141">您也可以使用其中一個 hello 範本中 hello[範本庫](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric)，像是 hello[五個節點 Service Fabric 叢集](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="2adaa-142">現有虛擬網路或子網路</span><span class="sxs-lookup"><span data-stu-id="2adaa-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="2adaa-143">變更 hello 子網路參數 toohello hello 現有子網路名稱，並將兩個新參數 tooreference hello 現有的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="2adaa-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="2adaa-144">變更 hello`vnetID`變數 toopoint toohello 現有的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="2adaa-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="2adaa-145">從資源中移除 `Microsoft.Network/virtualNetworks`，讓 Azure 不會建立新的虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="2adaa-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="2adaa-146">註解 hello 虛擬網路從 hello`dependsOn`屬性`Microsoft.Compute/virtualMachineScaleSets`，因此您不相依於建立新的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="2adaa-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="2adaa-147">部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2adaa-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="2adaa-148">部署之後，應該包含您的虛擬網路 hello 新擴展集 Vm。</span><span class="sxs-lookup"><span data-stu-id="2adaa-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="2adaa-149">hello 虛擬機器規模集節點型別應該會顯示 hello 現有的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="2adaa-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="2adaa-150">您也可以使用遠端桌面通訊協定 (RDP) tooaccess hello 中已存在於 hello 虛擬網路的 VM 和 tooping hello 新擴展集 Vm:</span><span class="sxs-lookup"><span data-stu-id="2adaa-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="2adaa-151">如需其他範例，請參閱[而非特定 tooService 網狀架構](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="2adaa-152">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2adaa-152">Static public IP address</span></span>

1. <span data-ttu-id="2adaa-153">加入現有的靜態 IP 資源群組、 名稱和完整的網域名稱 (FQDN) 的 hello hello 名稱的參數：</span><span class="sxs-lookup"><span data-stu-id="2adaa-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="2adaa-154">移除 hello`dnsName`參數。</span><span class="sxs-lookup"><span data-stu-id="2adaa-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="2adaa-155">（hello 靜態 IP 位址已經有一個）。</span><span class="sxs-lookup"><span data-stu-id="2adaa-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="2adaa-156">加入變數 tooreference hello 現有靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="2adaa-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="2adaa-157">從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="2adaa-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="2adaa-158">註解 hello IP 位址從 hello`dependsOn`屬性`Microsoft.Network/loadBalancers`，因此您不相依於建立新的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="2adaa-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="2adaa-159">在 hello`Microsoft.Network/loadBalancers`資源、 變更 hello`publicIPAddress`的項目`frontendIPConfigurations`tooreference hello 現有靜態 IP 位址，而不是新建立的其中一個：</span><span class="sxs-lookup"><span data-stu-id="2adaa-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="2adaa-160">在 hello`Microsoft.ServiceFabric/clusters`資源，變更`managementEndpoint`toohello hello 靜態 IP 位址的 DNS FQDN。</span><span class="sxs-lookup"><span data-stu-id="2adaa-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="2adaa-161">如果您使用安全的叢集，請確定您變更*http://*太*https://*。</span><span class="sxs-lookup"><span data-stu-id="2adaa-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="2adaa-162">（請注意，這個步驟適用於 tooService 網狀架構叢集。</span><span class="sxs-lookup"><span data-stu-id="2adaa-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="2adaa-163">如果您使用虛擬機器擴展集，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="2adaa-164">部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2adaa-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="2adaa-165">部署之後，您可以看到您的負載平衡器已繫結的 toohello 公用靜態 IP 位址從 hello 其他資源群組。</span><span class="sxs-lookup"><span data-stu-id="2adaa-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="2adaa-166">hello Service Fabric 用戶端連線的端點和[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)端點點 toohello hello 靜態 IP 位址的 DNS FQDN。</span><span class="sxs-lookup"><span data-stu-id="2adaa-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="2adaa-167">僅內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2adaa-167">Internal-only load balancer</span></span>

<span data-ttu-id="2adaa-168">這種情況下，使用僅供內部使用的負載平衡器取代 hello 預設 Service Fabric 範本中的 hello 外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2adaa-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="2adaa-169">Hello Azure 入口網站和 hello Service Fabric 資源提供者的顧慮，請參閱前面一節的 hello。</span><span class="sxs-lookup"><span data-stu-id="2adaa-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="2adaa-170">移除 hello`dnsName`參數。</span><span class="sxs-lookup"><span data-stu-id="2adaa-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="2adaa-171">(不需要此參數)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="2adaa-172">(選擇性) 如果您使用靜態配置方法，則可以新增靜態 IP 位址參數。</span><span class="sxs-lookup"><span data-stu-id="2adaa-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="2adaa-173">如果您使用動態配置方法，您不需要 toodo 此步驟。</span><span class="sxs-lookup"><span data-stu-id="2adaa-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="2adaa-174">從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="2adaa-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="2adaa-175">移除 hello IP 位址`dependsOn`屬性`Microsoft.Network/loadBalancers`，因此您不相依於建立新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2adaa-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="2adaa-176">新增虛擬網路的 hello`dependsOn`屬性，因為 hello 負載平衡器現在取決於 hello hello 虛擬網路子網路：</span><span class="sxs-lookup"><span data-stu-id="2adaa-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="2adaa-177">變更 hello 負載平衡器的`frontendIPConfigurations`設定使用`publicIPAddress`，toousing 子網路和`privateIPAddress`。</span><span class="sxs-lookup"><span data-stu-id="2adaa-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="2adaa-178">`privateIPAddress` 使用預先定義的靜態內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2adaa-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="2adaa-179">toouse 動態 IP 位址，移除 hello`privateIPAddress`項目，然後再變更`privateIPAllocationMethod`太**動態**。</span><span class="sxs-lookup"><span data-stu-id="2adaa-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="2adaa-180">在 hello`Microsoft.ServiceFabric/clusters`資源，變更`managementEndpoint`toopoint toohello 內部負載平衡器位址。</span><span class="sxs-lookup"><span data-stu-id="2adaa-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="2adaa-181">如果您使用安全的叢集，請確定您變更*http://*太*https://*。</span><span class="sxs-lookup"><span data-stu-id="2adaa-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="2adaa-182">（請注意，這個步驟適用於 tooService 網狀架構叢集。</span><span class="sxs-lookup"><span data-stu-id="2adaa-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="2adaa-183">如果您使用虛擬機器擴展集，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="2adaa-184">部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2adaa-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="2adaa-185">部署之後，您的負載平衡器會使用私用靜態 10.0.0.250 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2adaa-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="2adaa-186">如果您在相同的虛擬網路的另一部電腦，您可以移 toohello 內部[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)端點。</span><span class="sxs-lookup"><span data-stu-id="2adaa-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="2adaa-187">請注意連接 tooone 的 hello hello 負載平衡器後方的節點。</span><span class="sxs-lookup"><span data-stu-id="2adaa-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="2adaa-188">內部與外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2adaa-188">Internal and external load balancer</span></span>

<span data-ttu-id="2adaa-189">在此案例中，開始與 hello 現有單一節點類型外部負載平衡器並新增 hello 內部負載平衡器相同的節點類型。</span><span class="sxs-lookup"><span data-stu-id="2adaa-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="2adaa-190">連接後端連接埠 tooa 後端位址集區可以指派只有 tooa 單一負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2adaa-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="2adaa-191">選擇要讓哪個負載平衡器擁有您的應用程式連接埠，哪個負載平衡器擁有管理端點 (連接埠 19000 和 19080)。</span><span class="sxs-lookup"><span data-stu-id="2adaa-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="2adaa-192">如果您將 hello 管理端點 hello 內部負載平衡器上，將保留在心 hello Service Fabric 資源 hello 文章中稍早討論的提供者限制。</span><span class="sxs-lookup"><span data-stu-id="2adaa-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="2adaa-193">在 hello 範例中我們使用，hello 管理端點會保留在 hello 外部負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="2adaa-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="2adaa-194">您也會新增連接埠 80 的應用程式連接埠，並將它放 hello 內部負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="2adaa-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="2adaa-195">在兩個節點型別叢集中，一種節點類型是 hello 外部負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="2adaa-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="2adaa-196">hello 其他節點型別是 hello 內部負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="2adaa-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="2adaa-197">toouse hello 入口網站建立兩個節點類型的範本 （隨附於兩個負載平衡器） 中的兩個節點型別叢集，切換 hello 第二個負載平衡器 tooan 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2adaa-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="2adaa-198">如需詳細資訊，請參閱 hello[僅供內部使用的負載平衡器](#internallb)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2adaa-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="2adaa-199">加入 hello 靜態內部負載平衡器 IP 位址參數。</span><span class="sxs-lookup"><span data-stu-id="2adaa-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="2adaa-200">（如相關 toousing 動態 IP 位址資訊，請參閱本文的稍早章節）。</span><span class="sxs-lookup"><span data-stu-id="2adaa-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="2adaa-201">新增應用程式連接埠 80 參數。</span><span class="sxs-lookup"><span data-stu-id="2adaa-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="2adaa-202">tooadd hello 現有的內部版本網路變數，複製和貼上，並新增 「-Int"toohello 名稱：</span><span class="sxs-lookup"><span data-stu-id="2adaa-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="2adaa-203">如果您啟動與 hello 入口網站所產生的範本會使用應用程式連接埠 80，hello 預設入口網站範本會加入 AppPort1 （連接埠 80） hello 外部負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="2adaa-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="2adaa-204">在此情況下，從 hello 外部負載平衡器移除 AppPort1`loadBalancingRules`和探查，因此您可以將其加入 toohello 內部負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="2adaa-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="2adaa-205">新增第二個 `Microsoft.Network/loadBalancers` 資源。</span><span class="sxs-lookup"><span data-stu-id="2adaa-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="2adaa-206">它看起來類似 hello 中建立的 toohello 內部負載平衡器[僅供內部使用的負載平衡器](#internallb) 區段中，但它會使用 hello"的 Int 」 負載平衡器變數，以及實作只有 hello 應用程式連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="2adaa-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="2adaa-207">這也會移除`inboundNatPools`，tookeep hello 公用負載平衡器上的 RDP 端點。</span><span class="sxs-lookup"><span data-stu-id="2adaa-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="2adaa-208">如果您想 RDP hello 內部負載平衡器上，移動`inboundNatPools`從 hello 外部負載平衡器 toothis 內部負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="2adaa-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="2adaa-209">在`networkProfile`hello`Microsoft.Compute/virtualMachineScaleSets`資源，新增 hello 內部的後端位址集區：</span><span class="sxs-lookup"><span data-stu-id="2adaa-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="2adaa-210">部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2adaa-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="2adaa-211">部署之後，您可以看到 hello 資源群組中的兩個負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2adaa-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="2adaa-212">如果您瀏覽 hello 負載平衡器，您可以看到 hello 公用 IP 位址和管理端點 （連接埠 19000 和 19080） 指派 toohello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2adaa-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="2adaa-213">您也可以看到 hello 靜態內部 IP 位址與應用程式端點 （連接埠 80） 指派 toohello 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2adaa-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="2adaa-214">同時指定負載平衡器使用 hello 相同虛擬機器規模集後端集區。</span><span class="sxs-lookup"><span data-stu-id="2adaa-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2adaa-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2adaa-215">Next steps</span></span>
[<span data-ttu-id="2adaa-216">建立叢集</span><span class="sxs-lookup"><span data-stu-id="2adaa-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
