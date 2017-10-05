---
title: "Azure Service Fabric 的網路功能模式 | Microsoft Docs"
description: "描述 Service Fabric 常見的網路功能模式，以及如何使用 Azure 網路功能建立叢集。"
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
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="c8e70-103">Service Fabric 網路功能模式</span><span class="sxs-lookup"><span data-stu-id="c8e70-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="c8e70-104">您可以將 Azure Service Fabric 叢集與其他的 Azure 網路功能整合起來。</span><span class="sxs-lookup"><span data-stu-id="c8e70-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="c8e70-105">本文說明如何建立使用下列功能的叢集︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="c8e70-106">現有虛擬網路或子網路</span><span class="sxs-lookup"><span data-stu-id="c8e70-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="c8e70-107">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c8e70-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="c8e70-108">僅內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c8e70-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="c8e70-109">內部與外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c8e70-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="c8e70-110">Service Fabric 會在標準的虛擬機器擴展集內執行。</span><span class="sxs-lookup"><span data-stu-id="c8e70-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="c8e70-111">能在虛擬機器擴展集內使用的功能，就能在 Service Fabric 叢集內使用。</span><span class="sxs-lookup"><span data-stu-id="c8e70-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="c8e70-112">虛擬機器擴展集和 Service Fabric 之 Azure Resource Manager 範本中的網路區段完全相同。</span><span class="sxs-lookup"><span data-stu-id="c8e70-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="c8e70-113">在部署至現有虛擬網路後，即可輕鬆地納入其他網路功能，例如 Azure ExpressRoute、Azure VPN 閘道、網路安全性群組和虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="c8e70-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="c8e70-114">Service Fabric 有一個方面是其他網路功能所沒有的。</span><span class="sxs-lookup"><span data-stu-id="c8e70-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="c8e70-115">[Azure 入口網站](https://portal.azure.com)在內部會使用 Service Fabric 資源提供者來呼叫叢集，以取得節點和應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c8e70-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="c8e70-116">Service Fabric 資源提供者對管理端點上的 HTTP 閘道連接埠 (預設為連接埠 19080) 需具備可公開存取的輸入存取權。</span><span class="sxs-lookup"><span data-stu-id="c8e70-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="c8e70-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 會使用此管理端點來管理您的叢集。</span><span class="sxs-lookup"><span data-stu-id="c8e70-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="c8e70-118">Service Fabric 資源提供者也會使用此連接埠來查詢您叢集的相關資訊，以顯示在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c8e70-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="c8e70-119">如果無法從 Service Fabric 資源提供者存取連接埠 19080，入口網站中會出現「找不到節點」之類的訊息，而且您的節點和應用程式清單會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="c8e70-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="c8e70-120">如果您想在 Azure 入口網站看到您的叢集，負載平衡器必須公開公用 IP 位址，且您的網路安全性群組必須允許連入的連接埠 19080 流量。</span><span class="sxs-lookup"><span data-stu-id="c8e70-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="c8e70-121">如果您的設定不符合這些需求，Azure 入口網站就不會顯示叢集的狀態。</span><span class="sxs-lookup"><span data-stu-id="c8e70-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="c8e70-122">範本</span><span class="sxs-lookup"><span data-stu-id="c8e70-122">Templates</span></span>

<span data-ttu-id="c8e70-123">所有 Service Fabric 範本都位於[一個下載檔案](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)中。</span><span class="sxs-lookup"><span data-stu-id="c8e70-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="c8e70-124">使用下列 Powershell 命令應該可以依原樣部署範本。</span><span class="sxs-lookup"><span data-stu-id="c8e70-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="c8e70-125">如果您要部署現有 Azure 虛擬網路範本或靜態公用 IP 範本，請先閱讀本文的[初始設定](#initialsetup)一節。</span><span class="sxs-lookup"><span data-stu-id="c8e70-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="c8e70-126">初始設定</span><span class="sxs-lookup"><span data-stu-id="c8e70-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="c8e70-127">現有的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c8e70-127">Existing virtual network</span></span>

<span data-ttu-id="c8e70-128">在下列範例中，我們會從 **ExistingRG** 資源群組中名為 ExistingRG-vnet 的現有虛擬網路來開始。</span><span class="sxs-lookup"><span data-stu-id="c8e70-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="c8e70-129">子網路名為 default。</span><span class="sxs-lookup"><span data-stu-id="c8e70-129">The subnet is named default.</span></span> <span data-ttu-id="c8e70-130">這些預設資源會在您使用 Azure 入口網站來建立標準虛擬機器 (VM) 時建立。</span><span class="sxs-lookup"><span data-stu-id="c8e70-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="c8e70-131">您可以建立虛擬網路和子網路而不建立 VM，但將叢集新增至現有虛擬網路的主要目標是要提供對其他 VM 的網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="c8e70-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="c8e70-132">建立 VM 可為現有虛擬網路一般是如何使用的提供良好範例。</span><span class="sxs-lookup"><span data-stu-id="c8e70-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="c8e70-133">如果 Service Fabric 叢集只使用內部負載平衡器而不使用公用 IP 位址，您可以使用 VM 和其公用 IP 來做為安全的「跳躍箱」。</span><span class="sxs-lookup"><span data-stu-id="c8e70-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="c8e70-134">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c8e70-134">Static public IP address</span></span>

<span data-ttu-id="c8e70-135">靜態公用 IP 位址一般是會與 VM 或其指派到之 VM 分開管理的專用資源。</span><span class="sxs-lookup"><span data-stu-id="c8e70-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="c8e70-136">它會佈建在專用的網路資源群組中 (而非在 Service Fabric 叢集資源群組本身)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="c8e70-137">請透過 Azure 入口網站或 Powershell，在同一個 ExistingRG 資源群組中建立名為 staticIP1 的靜態公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="c8e70-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="c8e70-138">Service Fabric 範本</span><span class="sxs-lookup"><span data-stu-id="c8e70-138">Service Fabric template</span></span>

<span data-ttu-id="c8e70-139">在本文的範例中，我們會使用 Service Fabric template.json。</span><span class="sxs-lookup"><span data-stu-id="c8e70-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="c8e70-140">您可以先使用標準入口網站精靈從入口網站下載範本，再建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c8e70-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="c8e70-141">您也可以使用[範本庫 (英文)](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric) 中的其中一個範本，例如[五個節點的 Service Fabric 叢集 (英文)](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="c8e70-142">現有虛擬網路或子網路</span><span class="sxs-lookup"><span data-stu-id="c8e70-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="c8e70-143">將子網路參數變更為現有子網路的名稱，然後新增兩個新的參數以參考現有虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="c8e70-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

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


2. <span data-ttu-id="c8e70-144">變更 `vnetID` 變數以指向現有虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="c8e70-145">從資源中移除 `Microsoft.Network/virtualNetworks`，讓 Azure 不會建立新的虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="c8e70-146">從 `Microsoft.Compute/virtualMachineScaleSets` 的 `dependsOn` 屬性將虛擬網路註解化，以便不需依賴建立新的虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="c8e70-147">部署範本：</span><span class="sxs-lookup"><span data-stu-id="c8e70-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="c8e70-148">在部署之後，您的虛擬網路應該會包含新的擴展集 VM。</span><span class="sxs-lookup"><span data-stu-id="c8e70-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="c8e70-149">虛擬機器擴展集節點類型應該會顯示現有虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="c8e70-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="c8e70-150">您也可以使用遠端桌面通訊協定 (RDP) 來存取已存在於虛擬網路的 VM，以及 ping 新的擴展集 VM：</span><span class="sxs-lookup"><span data-stu-id="c8e70-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="c8e70-151">如需其他範例，請參閱[非 Service Fabric 專屬的範例](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="c8e70-152">靜態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c8e70-152">Static public IP address</span></span>

1. <span data-ttu-id="c8e70-153">新增現有靜態 IP 資源群組名稱、名稱和完整網域名稱 (FQDN) 的參數︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="c8e70-154">移除 `dnsName` 參數 </span><span class="sxs-lookup"><span data-stu-id="c8e70-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="c8e70-155">(靜態 IP 位址已經有一個)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="c8e70-156">新增變數來參考現有靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="c8e70-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="c8e70-157">從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="c8e70-158">從 `Microsoft.Network/loadBalancers` 的 `dependsOn` 屬性將 IP 位址註解化，以便不需依賴建立新的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="c8e70-159">在 `Microsoft.Network/loadBalancers` 資源中，變更 `frontendIPConfigurations` 的 `publicIPAddress` 元素來參考現有靜態 IP 位址，而非參考新建立的位址︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="c8e70-160">在 `Microsoft.ServiceFabric/clusters` 資源中，將 `managementEndpoint` 變更為靜態 IP 位址的 DNS FQDN。</span><span class="sxs-lookup"><span data-stu-id="c8e70-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="c8e70-161">如果您使用安全的叢集，請務必將 http:// 變更為 https:// </span><span class="sxs-lookup"><span data-stu-id="c8e70-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="c8e70-162">(請注意，此步驟僅適用於 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c8e70-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="c8e70-163">如果您使用虛擬機器擴展集，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="c8e70-164">部署範本：</span><span class="sxs-lookup"><span data-stu-id="c8e70-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="c8e70-165">在部署後，您會看到負載平衡器繫結至另一個資源群組中的公用靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c8e70-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="c8e70-166">Service Fabric 用戶端連線端點和 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 端點會指向靜態 IP 位址的 DNS FQDN。</span><span class="sxs-lookup"><span data-stu-id="c8e70-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="c8e70-167">僅內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c8e70-167">Internal-only load balancer</span></span>

<span data-ttu-id="c8e70-168">此案例使用僅內部負載平衡器取代預設 Service Fabric 範本中的外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="c8e70-169">若要了解這對 Azure 入口網站和 Service Fabric 資源提供者的影響，請參閱上一節。</span><span class="sxs-lookup"><span data-stu-id="c8e70-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="c8e70-170">移除 `dnsName` 參數 </span><span class="sxs-lookup"><span data-stu-id="c8e70-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="c8e70-171">(不需要此參數)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="c8e70-172">(選擇性) 如果您使用靜態配置方法，則可以新增靜態 IP 位址參數。</span><span class="sxs-lookup"><span data-stu-id="c8e70-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="c8e70-173">如果您使用動態配置方法，則不需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="c8e70-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="c8e70-174">從資源中移除 `Microsoft.Network/publicIPAddresses`，讓 Azure 不會建立新的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="c8e70-175">從 `Microsoft.Network/loadBalancers` 的 `dependsOn` 屬性中移除 IP 位址，以便不需依賴建立新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c8e70-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="c8e70-176">新增虛擬網路 `dependsOn` 屬性，因為負載平衡器現在仰賴虛擬網路中的子網路︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

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

5. <span data-ttu-id="c8e70-177">將負載平衡器的 `frontendIPConfigurations` 設定從使用 `publicIPAddress` 變更為使用子網路和 `privateIPAddress`。</span><span class="sxs-lookup"><span data-stu-id="c8e70-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="c8e70-178">`privateIPAddress` 使用預先定義的靜態內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c8e70-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="c8e70-179">若要使用動態 IP 位址，請移除 `privateIPAddress` 元素，然後將 `privateIPAllocationMethod` 變更為 **Dynamic**。</span><span class="sxs-lookup"><span data-stu-id="c8e70-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

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

6. <span data-ttu-id="c8e70-180">在 `Microsoft.ServiceFabric/clusters` 資源中，變更 `managementEndpoint` 以指向內部負載平衡器位址。</span><span class="sxs-lookup"><span data-stu-id="c8e70-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="c8e70-181">如果您使用安全的叢集，請務必將 http:// **變更為 https://** </span><span class="sxs-lookup"><span data-stu-id="c8e70-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="c8e70-182">(請注意，此步驟僅適用於 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c8e70-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="c8e70-183">如果您使用虛擬機器擴展集，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="c8e70-184">部署範本：</span><span class="sxs-lookup"><span data-stu-id="c8e70-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="c8e70-185">在部署後，負載平衡器會使用私用靜態 IP 位址 10.0.0.250。</span><span class="sxs-lookup"><span data-stu-id="c8e70-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="c8e70-186">如果您在相同的虛擬網路中有另一部電腦，您可以移至內部 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 端點。</span><span class="sxs-lookup"><span data-stu-id="c8e70-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="c8e70-187">請注意，它會連線至負載平衡器後的其中一個節點。</span><span class="sxs-lookup"><span data-stu-id="c8e70-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="c8e70-188">內部與外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c8e70-188">Internal and external load balancer</span></span>

<span data-ttu-id="c8e70-189">在此案例中，您會從現有的單一節點類型外部負載平衡器來開始，然後新增同一節點類型的內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="c8e70-190">連結到後端位址集區的後端連接埠只能指派給單一負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="c8e70-191">選擇要讓哪個負載平衡器擁有您的應用程式連接埠，哪個負載平衡器擁有管理端點 (連接埠 19000 和 19080)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="c8e70-192">如果您將管理端點放在內部負載平衡器，請記住本文稍早討論過的 Service Fabric 資源提供者限制。</span><span class="sxs-lookup"><span data-stu-id="c8e70-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="c8e70-193">在我們使用的範例中，管理端點會留在外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="c8e70-194">您也會新增連接埠 80 應用程式連接埠，並將它放在內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="c8e70-195">在雙節點類型的叢集中，一個節點類型位於外部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="c8e70-196">另一個節點類型則位於內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="c8e70-197">若要使用雙節點類型的叢集，請在入口網站中建立雙節點類型的範本 (隨附兩個負載平衡器)，並將第二個負載平衡器切換至內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="c8e70-198">如需詳細資訊，請參閱[僅內部負載平衡器](#internallb)一節。</span><span class="sxs-lookup"><span data-stu-id="c8e70-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="c8e70-199">新增靜態內部負載平衡器 IP 位址參數 </span><span class="sxs-lookup"><span data-stu-id="c8e70-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="c8e70-200">(如需使用動態 IP 位址的相關注意事項，請參閱本文前面幾節)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="c8e70-201">新增應用程式連接埠 80 參數。</span><span class="sxs-lookup"><span data-stu-id="c8e70-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="c8e70-202">若要新增現有網路變數的內部版本，請將變數複製並貼上，然後在名稱中新增「-Int」︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

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

4. <span data-ttu-id="c8e70-203">如果您從使用應用程式連接埠 80 的入口網站所產生範本來開始，預設入口網站範本會在外部負載平衡器上新增 AppPort1 (連接埠 80)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="c8e70-204">在此情況下，請將 AppPort1 從外部負載平衡器 `loadBalancingRules` 和探查中移除，以將它新增至內部負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="c8e70-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

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
        } /* Remove AppPort1 from the external load balancer.
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
        } /* Remove AppPort1 from the external load balancer.
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

5. <span data-ttu-id="c8e70-205">新增第二個 `Microsoft.Network/loadBalancers` 資源。</span><span class="sxs-lookup"><span data-stu-id="c8e70-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="c8e70-206">此資源類似[僅內部負載平衡器](#internallb)一節中建立的內部負載平衡器，但它會使用「-Int」負載平衡器變數，並只實作應用程式連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="c8e70-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="c8e70-207">這也會移除 `inboundNatPools`，以將 RDP 端點保留在公用負載平衡器上。</span><span class="sxs-lookup"><span data-stu-id="c8e70-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="c8e70-208">如果您想讓 RDP 位於內部負載平衡器上，請將 `inboundNatPools` 從外部負載平衡器移動到這個內部負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
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
                                /* Switch from Public to Private IP address
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
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
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
                    /* Add the probe for the app port. */
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

6. <span data-ttu-id="c8e70-209">在 `Microsoft.Compute/virtualMachineScaleSets` 資源的 `networkProfile` 上，新增內部後端位址集區︰</span><span class="sxs-lookup"><span data-stu-id="c8e70-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

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

7. <span data-ttu-id="c8e70-210">部署範本：</span><span class="sxs-lookup"><span data-stu-id="c8e70-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="c8e70-211">在部署後，您會看到資源群組中有兩個負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c8e70-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="c8e70-212">如果您瀏覽負載平衡器，您會看到公用 IP 位址和指派給公用 IP 位址的管理端點 (連接埠 19000 和 19080)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="c8e70-213">您也會看到靜態內部 IP 位址和指派給內部負載平衡器的應用程式端點 (連接埠 80)。</span><span class="sxs-lookup"><span data-stu-id="c8e70-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="c8e70-214">這兩個負載平衡器會使用相同的虛擬機器擴展集後端集區。</span><span class="sxs-lookup"><span data-stu-id="c8e70-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e70-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8e70-215">Next steps</span></span>
[<span data-ttu-id="c8e70-216">建立叢集</span><span class="sxs-lookup"><span data-stu-id="c8e70-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
