---
title: "適用於 Vm-Azure CLI 2.0 aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解 tooconfigure 私人 IP 位址的虛擬機器使用 hello Azure 命令列介面 (CLI) 2.0 的方式。"
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="d08b4-103">設定使用 Azure CLI 2.0 hello 為虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d08b4-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d08b4-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="d08b4-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d08b4-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="d08b4-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d08b4-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="d08b4-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="d08b4-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="d08b4-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d08b4-108">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="d08b4-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d08b4-109">您也可以[管理 hello 傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="d08b4-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="d08b4-110">下列的 hello 範例 Azure CLI 2.0 命令預期簡單的環境中已經建立。</span><span class="sxs-lookup"><span data-stu-id="d08b4-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="d08b4-111">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="d08b4-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="d08b4-112">建立 VM 時指定靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d08b4-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="d08b4-113">名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*以靜態私人 ip 位址的*192.168.1.101*，請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="d08b4-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d08b4-114">如果您尚未，安裝並設定最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="d08b4-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="d08b4-115">建立 hello VM 的公用 IP 與 hello [az 網路公用 ip 建立](/cli/azure/network/public-ip#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d08b4-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="d08b4-116">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d08b4-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d08b4-117">您可能想要或需要 toouse 不同的值，在此您引數和後續的步驟，取決於您的環境而定。</span><span class="sxs-lookup"><span data-stu-id="d08b4-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="d08b4-118">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="d08b4-119">`--resource-group`: Hello toocreate hello 公用 ip 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d08b4-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="d08b4-120">`--name`: Hello 公用 IP 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d08b4-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="d08b4-121">`--location`: Azure toocreate hello 公用 ip 的區域。</span><span class="sxs-lookup"><span data-stu-id="d08b4-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="d08b4-122">執行 hello [az 網路 nic 建立](/cli/azure/network/nic#create)命令 toocreate 以靜態私人 ip 位址的 NIC。</span><span class="sxs-lookup"><span data-stu-id="d08b4-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="d08b4-123">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d08b4-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="d08b4-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="d08b4-125">參數：</span><span class="sxs-lookup"><span data-stu-id="d08b4-125">Parameters:</span></span>

    * <span data-ttu-id="d08b4-126">`--private-ip-address`： hello NIC 靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d08b4-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="d08b4-127">`--vnet-name`: Name 的 hello VNet 中哪些 toocreate hello nic。</span><span class="sxs-lookup"><span data-stu-id="d08b4-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="d08b4-128">`--subnet`： 在哪一個 toocreate hello NIC 的 hello 子網路名稱</span><span class="sxs-lookup"><span data-stu-id="d08b4-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="d08b4-129">執行 hello [azure vm 建立](/cli/azure/vm/nic#create)命令 toocreate hello 使用 hello 公用 IP 與 NIC VM 上面所建立。</span><span class="sxs-lookup"><span data-stu-id="d08b4-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="d08b4-130">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d08b4-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="d08b4-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="d08b4-132">基本的 hello 以外參數[az vm 建立](/cli/azure/vm#create)參數。</span><span class="sxs-lookup"><span data-stu-id="d08b4-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="d08b4-133">`--nics`： 附加 hello NIC toowhich hello VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="d08b4-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="d08b4-134">擷取 VM 的靜態私人 IP 位址資訊</span><span class="sxs-lookup"><span data-stu-id="d08b4-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="d08b4-135">tooview hello 靜態私人 IP 位址，在建立時，執行下列 Azure CLI 命令的 hello，並觀察 hello 值*私用 IP 配置方法*和*私人 IP 位址*:</span><span class="sxs-lookup"><span data-stu-id="d08b4-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="d08b4-136">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="d08b4-137">toodisplay 特別 hello hello NIC 的特定的 IP 資訊，該 vm，查詢 hello NIC:</span><span class="sxs-lookup"><span data-stu-id="d08b4-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="d08b4-138">hello 輸出是像這樣：</span><span class="sxs-lookup"><span data-stu-id="d08b4-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="d08b4-139">移除 VM 的靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d08b4-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="d08b4-140">您無法從 Azure CLI 的 NIC 移除資源管理員部署的靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d08b4-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="d08b4-141">您必須：</span><span class="sxs-lookup"><span data-stu-id="d08b4-141">You must:</span></span>
- <span data-ttu-id="d08b4-142">建立使用動態 IP 的新 NIC</span><span class="sxs-lookup"><span data-stu-id="d08b4-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="d08b4-143">新建立的 NIC VM 執行 hello 的 hello 上設定 hello NIC</span><span class="sxs-lookup"><span data-stu-id="d08b4-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="d08b4-144">toochange hello NIC hello VM 用於 hello 命令以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d08b4-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="d08b4-145">執行 hello **azure 網路的 nic 建立**命令 toocreate 使用動態 IP 配置新的 IP 位址的新 NIC。</span><span class="sxs-lookup"><span data-stu-id="d08b4-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="d08b4-146">請注意，因為沒有 IP 位址指定，hello 配置方法**動態**。</span><span class="sxs-lookup"><span data-stu-id="d08b4-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="d08b4-147">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-147">Expected output:</span></span>

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

2. <span data-ttu-id="d08b4-148">執行 hello **azure vm 集**命令 toochange hello hello VM 所使用的 NIC。</span><span class="sxs-lookup"><span data-stu-id="d08b4-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="d08b4-149">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d08b4-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="d08b4-150">Hello VM 是否夠大 toohave 執行 hello 的多個 NIC **azure 網路的 nic 刪除**命令 toodelete hello 舊 nic。</span><span class="sxs-lookup"><span data-stu-id="d08b4-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="d08b4-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d08b4-151">Next steps</span></span>
* <span data-ttu-id="d08b4-152">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="d08b4-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d08b4-153">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="d08b4-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d08b4-154">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d08b4-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

