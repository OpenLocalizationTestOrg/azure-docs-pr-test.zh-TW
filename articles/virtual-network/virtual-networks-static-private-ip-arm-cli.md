---
title: "設定 VM 的私人 IP 位址 - Azure CLI 2.0 | Microsoft Docs"
description: "了解如何使用 Azure 命令列介面 (CLI) 2.0 設定虛擬機器的私人 IP 位址。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="7ed68-103">使用 Azure CLI 2.0 設定虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ed68-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7ed68-104">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="7ed68-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="7ed68-105">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="7ed68-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="7ed68-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – 適用於傳統和資源管理部署模型的 CLI</span><span class="sxs-lookup"><span data-stu-id="7ed68-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="7ed68-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - 適用於資源管理部署模型的新一代 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="7ed68-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7ed68-108">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="7ed68-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="7ed68-109">您也可以 [管理傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7ed68-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="7ed68-110">下列範例 Azure CLI 2.0 命令會預期已經建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="7ed68-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="7ed68-111">如果您想要執行如本文件中所顯示的命令，請先建置 [建立 vnet](virtual-networks-create-vnet-arm-cli.md)中所說明的測試環境。</span><span class="sxs-lookup"><span data-stu-id="7ed68-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="7ed68-112">建立 VM 時指定靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ed68-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="7ed68-113">若要在名為 TestVNet 之 VNet 的FrontEnd子網路中建立名為 DNS01 且其靜態私人 IP 為 192.168.1.101 的 VM，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ed68-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="7ed68-114">安裝及設定最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) (若您尚未這麼做)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ed68-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="7ed68-115">使用 [az network public-ip create](/cli/azure/network/public-ip#create) 命令來建立 VM 的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="7ed68-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="7ed68-116">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="7ed68-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ed68-117">視您的環境而定，您可能會想要或需要為此步驟和後續步驟中的引數使用不同的值。</span><span class="sxs-lookup"><span data-stu-id="7ed68-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="7ed68-118">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="7ed68-119">`--resource-group`︰要在其中建立公用 IP 之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed68-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="7ed68-120">`--name`：公用 IP 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed68-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="7ed68-121">`--location`：要在其中建立公用 IP 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="7ed68-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="7ed68-122">執行 [az network nic create](/cli/azure/network/nic#create) 命令以建立具有靜態私人 IP 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="7ed68-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="7ed68-123">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="7ed68-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="7ed68-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="7ed68-125">參數：</span><span class="sxs-lookup"><span data-stu-id="7ed68-125">Parameters:</span></span>

    * <span data-ttu-id="7ed68-126">`--private-ip-address`：NIC 的靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ed68-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="7ed68-127">`--vnet-name`：要在其中建立 NIC 之 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed68-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="7ed68-128">`--subnet`：要在其中建立 NIC 之子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed68-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="7ed68-129">執行 [azure vm create](/cli/azure/vm/nic#create) 命令來使用上面建立的公用 IP 和 NIC 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7ed68-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="7ed68-130">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="7ed68-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="7ed68-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="7ed68-132">基本 [az vm create](/cli/azure/vm#create) 參數以外的參數。</span><span class="sxs-lookup"><span data-stu-id="7ed68-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="7ed68-133">`--nics`︰VM 所連接至之 NIC 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ed68-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="7ed68-134">擷取 VM 的靜態私人 IP 位址資訊</span><span class="sxs-lookup"><span data-stu-id="7ed68-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="7ed68-135">若要檢視所建立的靜態私人 IP 位址，請執行下列 Azure CLI 命令並觀察 Private IP alloc-method 和 Private IP address 的值：</span><span class="sxs-lookup"><span data-stu-id="7ed68-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="7ed68-136">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="7ed68-137">若要顯示該 VM 之 NIC 的特定 IP 資訊，請查詢 NIC，特別是：</span><span class="sxs-lookup"><span data-stu-id="7ed68-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="7ed68-138">輸出會像這樣：</span><span class="sxs-lookup"><span data-stu-id="7ed68-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="7ed68-139">移除 VM 的靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ed68-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="7ed68-140">您無法從 Azure CLI 的 NIC 移除資源管理員部署的靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ed68-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="7ed68-141">您必須：</span><span class="sxs-lookup"><span data-stu-id="7ed68-141">You must:</span></span>
- <span data-ttu-id="7ed68-142">建立使用動態 IP 的新 NIC</span><span class="sxs-lookup"><span data-stu-id="7ed68-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="7ed68-143">在新建立 NIC 的 VM 上設定 NIC。</span><span class="sxs-lookup"><span data-stu-id="7ed68-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="7ed68-144">若要變更上述命令中使用之 VM 的 NIC，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="7ed68-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="7ed68-145">執行 **azure network nic create** 命令來建立使用新 IP 位址動態配置 IP 的新 NIC。</span><span class="sxs-lookup"><span data-stu-id="7ed68-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="7ed68-146">請注意，因為未指定任何 IP 位址，配置方法為**動態**。</span><span class="sxs-lookup"><span data-stu-id="7ed68-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="7ed68-147">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="7ed68-148">執行 **azure vm set** 命令來變更 VM 所使用的 NIC。</span><span class="sxs-lookup"><span data-stu-id="7ed68-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="7ed68-149">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7ed68-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="7ed68-150">如果 VM 夠大而可容納多個 NIC，請執行 **azure network nic delete** 命令，以刪除舊 NIC。</span><span class="sxs-lookup"><span data-stu-id="7ed68-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="7ed68-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ed68-151">Next steps</span></span>
* <span data-ttu-id="7ed68-152">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="7ed68-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7ed68-153">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="7ed68-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7ed68-154">請參閱 [保留 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ed68-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

