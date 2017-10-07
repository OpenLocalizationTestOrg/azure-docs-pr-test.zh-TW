---
title: "Azure 虛擬機器規模集的 aaaNetworking |Microsoft 文件"
description: "設定 Azure 虛擬機器擴展集的網路屬性。"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="283ab-103">Azure 虛擬機器擴展集的網路</span><span class="sxs-lookup"><span data-stu-id="283ab-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="283ab-104">當您部署透過 hello 入口網站設定 Azure 虛擬機器比例時，某些網路內容的預設，例如 Azure 負載平衡器輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="283ab-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="283ab-105">本文說明如何 toouse hello 的某些更進階的小數位數，您可以設定的網路功能設定。</span><span class="sxs-lookup"><span data-stu-id="283ab-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="283ab-106">您可以設定所有 hello 功能涵蓋在本文中使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="283ab-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="283ab-107">選取的功能也會包含 Azure CLI 和 PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="283ab-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="283ab-108">使用 CLI 2.10 和 PowerShell 4.2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="283ab-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="283ab-109">加速網路</span><span class="sxs-lookup"><span data-stu-id="283ab-109">Accelerated Networking</span></span>
<span data-ttu-id="283ab-110">Azure[加速網路](../virtual-network/virtual-network-create-vm-accelerated-networking.md)藉由啟用單一根目錄 I/O 虛擬化 (SR-IOV) tooa 虛擬機器可以改善網路效能。</span><span class="sxs-lookup"><span data-stu-id="283ab-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="283ab-111">toouse 加速與規模集網路功能、 設定得 enableAcceleratedNetworking**true**規模集的 networkInterfaceConfigurations 設定中。</span><span class="sxs-lookup"><span data-stu-id="283ab-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="283ab-112">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="283ab-113">建立參考現有 Azure Load Balancer 的擴展集</span><span class="sxs-lookup"><span data-stu-id="283ab-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="283ab-114">使用 hello Azure 入口網站建立規模集時，大部分的設定選項建立新的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="283ab-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="283ab-115">如果您使用現有的負載平衡器建立需要 tooreference 的小數位數集合，您可以使用 CLI。</span><span class="sxs-lookup"><span data-stu-id="283ab-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="283ab-116">下列範例指令碼的 hello 建立負載平衡器，然後建立 小數位數組，即在參考它：</span><span class="sxs-lookup"><span data-stu-id="283ab-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="283ab-117">可設定的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="283ab-117">Configurable DNS Settings</span></span>
<span data-ttu-id="283ab-118">根據預設，規模集採取 hello VNET 和子網路中建立 hello 特定 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="283ab-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="283ab-119">不過，您可以設定直接設定的標尺的 hello DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="283ab-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="283ab-120">使用可設定的 DNS 伺服器建立擴展集</span><span class="sxs-lookup"><span data-stu-id="283ab-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="283ab-121">小數位數設定自訂 DNS 設定，使用 CLI 2.0 toocreate 新增 hello **-dns 伺服器**引數 toohello **vmss 建立**命令，後面接空格分隔的伺服器 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="283ab-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="283ab-122">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="283ab-123">tooconfigure 自訂 DNS 伺服器在 Azure 範本中，加入 dnsSettings 屬性 toohello 規模調整集合 networkInterfaceConfigurations > 一節。</span><span class="sxs-lookup"><span data-stu-id="283ab-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="283ab-124">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="283ab-125">使用可設定的虛擬機器網域名稱建立擴展集</span><span class="sxs-lookup"><span data-stu-id="283ab-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="283ab-126">規模調整集合以自訂的 DNS 名稱的虛擬機器使用 CLI 2.0 toocreate 新增 hello **-vm 網域名稱**引數 toohello **vmss 建立**命令，後面接著代表 hello 網域名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="283ab-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="283ab-127">tooset hello 網域名稱在 Azure 範本中，加入**dnsSettings**屬性 toohello 規模集**networkInterfaceConfigurations** > 一節。</span><span class="sxs-lookup"><span data-stu-id="283ab-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="283ab-128">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="283ab-129">hello 輸出，個別的虛擬機器的 dns 名稱會在下列形式的 hello:</span><span class="sxs-lookup"><span data-stu-id="283ab-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="283ab-130">每個虛擬機器的公用 IPv4</span><span class="sxs-lookup"><span data-stu-id="283ab-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="283ab-131">一般情況下，Azure 擴展集虛擬機器不需要自己的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="283ab-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="283ab-132">大部分的情況下，它是更經濟及安全 tooassociate 公用 IP 位址 tooa 負載平衡器或 tooan 個別虛擬機器 (也稱為 jumpbox)，然後路由傳送內送連接 tooscale 組虛擬機器，視需要 （例如，透過輸入的 NAT 規則）。</span><span class="sxs-lookup"><span data-stu-id="283ab-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="283ab-133">但是，某些情況下確實需要小數位數設定的虛擬機器 toohave 他們自己的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="283ab-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="283ab-134">範例遊戲，亦即主控台需要 toomake 直接連線 tooa 雲端虛擬機器，進行遊戲物理處理。</span><span class="sxs-lookup"><span data-stu-id="283ab-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="283ab-135">另一個例子是需要虛擬機器 toomake 外部連接 tooone 另一個分散式資料庫中的區域。</span><span class="sxs-lookup"><span data-stu-id="283ab-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="283ab-136">使用公用 IP 每虛擬機器建立擴展集</span><span class="sxs-lookup"><span data-stu-id="283ab-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="283ab-137">toocreate 公用 IP 位址 tooeach 將虛擬機器指派 CLI 2.0 規模集新增 hello **-公用-ip-vm**參數 toohello **vmss 建立**命令。</span><span class="sxs-lookup"><span data-stu-id="283ab-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="283ab-138">toocreate 在擴展集使用 Azure 的範本，請確定至少是 hello API 版的 hello Microsoft.Compute/virtualMachineScaleSets 資源**2017年-03-30**，並加入**publicIpAddressConfiguration**JSON 屬性 toohello 規模調整集合 ipConfigurations > 一節。</span><span class="sxs-lookup"><span data-stu-id="283ab-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="283ab-139">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="283ab-140">範本範例：[201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="283ab-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="283ab-141">查詢 hello 公用 IP 位址 hello 中的虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="283ab-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="283ab-142">toolist hello 公用 IP 位址指派 tooscale 使用 CLI 2.0 組虛擬機器，請使用 hello **az vmss 清單的執行個體-公用-ip**命令。</span><span class="sxs-lookup"><span data-stu-id="283ab-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="283ab-143">toolist 規模調整集合使用 PowerShell 的公用 IP 位址，請使用 hello _Get AzureRmPublicIpAddress_命令。</span><span class="sxs-lookup"><span data-stu-id="283ab-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="283ab-144">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="283ab-145">您也可以直接參考 hello hello 公用 IP 位址設定的資源識別碼查詢 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="283ab-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="283ab-146">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="283ab-147">tooquery hello 公用 IP 位址指派 tooscale 組虛擬機器使用 hello [Azure 資源總管](https://resources.azure.com)，或 hello Azure REST API 版本**2017年-03-30**或更高版本。</span><span class="sxs-lookup"><span data-stu-id="283ab-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="283ab-148">tooview 公用 IP 位址使用 hello 資源總管 中，設定標尺的查看 hello **publicipaddresses**規模集下的一節。</span><span class="sxs-lookup"><span data-stu-id="283ab-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="283ab-149">例如：https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="283ab-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="283ab-150">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="283ab-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="283ab-151">每個 NIC 的多個 IP 位址</span><span class="sxs-lookup"><span data-stu-id="283ab-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="283ab-152">每個 NIC 附加的 tooa VM 規模集中可以有一或多個與其相關聯的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="283ab-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="283ab-153">每個組態會獲派一個私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="283ab-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="283ab-154">每個組態可能也會有一個關聯的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="283ab-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="283ab-155">toounderstand 多少 IP 位址可以指派 tooa NIC，而且您可以使用 Azure 訂用帳戶中的多少公用 IP 位址太參考[Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)。</span><span class="sxs-lookup"><span data-stu-id="283ab-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="283ab-156">每個虛擬機器的多個 NIC</span><span class="sxs-lookup"><span data-stu-id="283ab-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="283ab-157">您可以向上 too8 Nic，每個虛擬機器，視機器大小而定。</span><span class="sxs-lookup"><span data-stu-id="283ab-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="283ab-158">hello 最大的 Nic 數目每台電腦位於 hello [VM 大小文章](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="283ab-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="283ab-159">hello 下列範例是規模調整集合網路設定檔顯示多個 NIC 項目，以及每個虛擬機器的多個公用 Ip:</span><span class="sxs-lookup"><span data-stu-id="283ab-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="283ab-160">每個擴展集的 NSG</span><span class="sxs-lookup"><span data-stu-id="283ab-160">NSG per scale set</span></span>
<span data-ttu-id="283ab-161">直接 tooa 規模集，藉由新增參考 toohello 網路介面組態區段的 hello 小數位數設定虛擬機器的內容，可以套用網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="283ab-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="283ab-162">例如：</span><span class="sxs-lookup"><span data-stu-id="283ab-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="283ab-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="283ab-163">Next steps</span></span>
<span data-ttu-id="283ab-164">如需有關 Azure 虛擬網路的詳細資訊，請參閱太[這份文件](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="283ab-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
