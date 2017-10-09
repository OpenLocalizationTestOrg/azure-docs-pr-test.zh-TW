## <a name="nic"></a><span data-ttu-id="d8717-101">NIC</span><span class="sxs-lookup"><span data-stu-id="d8717-101">NIC</span></span>
<span data-ttu-id="d8717-102">網路介面卡 (NIC) 資源會提供網路連線 tooan 現有的子網路中的 VNet 的資源。</span><span class="sxs-lookup"><span data-stu-id="d8717-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="d8717-103">雖然您可以建立為獨立物件的 NIC，您需要 tooassociate 它 tooanother 物件 tooactually 提供連線能力。</span><span class="sxs-lookup"><span data-stu-id="d8717-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="d8717-104">NIC 可以是使用的 tooconnect，VM tooa 子網路、 公用 IP 位址或在負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d8717-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="d8717-105">屬性</span><span class="sxs-lookup"><span data-stu-id="d8717-105">Property</span></span> | <span data-ttu-id="d8717-106">說明</span><span class="sxs-lookup"><span data-stu-id="d8717-106">Description</span></span> | <span data-ttu-id="d8717-107">範例值</span><span class="sxs-lookup"><span data-stu-id="d8717-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8717-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="d8717-108">**virtualMachine**</span></span> |<span data-ttu-id="d8717-109">VM hello NIC 相關聯。</span><span class="sxs-lookup"><span data-stu-id="d8717-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="d8717-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="d8717-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="d8717-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="d8717-111">**macAddress**</span></span> |<span data-ttu-id="d8717-112">Hello NIC 的 MAC 位址</span><span class="sxs-lookup"><span data-stu-id="d8717-112">MAC address for hello NIC</span></span> |<span data-ttu-id="d8717-113">介於 4 到 30 之間的任意值</span><span class="sxs-lookup"><span data-stu-id="d8717-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="d8717-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="d8717-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="d8717-115">NSG 相關聯 toohello NIC</span><span class="sxs-lookup"><span data-stu-id="d8717-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="d8717-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="d8717-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="d8717-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="d8717-117">**dnsSettings**</span></span> |<span data-ttu-id="d8717-118">Hello NIC 的 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="d8717-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="d8717-119">請參閱 [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="d8717-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="d8717-120">網路介面卡或 NIC，表示相關聯的 tooa 虛擬機器 (VM) 網路介面。</span><span class="sxs-lookup"><span data-stu-id="d8717-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="d8717-121">一個 VM 可以有一或多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="d8717-121">A VM can have one or more NICs.</span></span>

![單一 VM 上的 NIC](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="d8717-123">IP 組態</span><span class="sxs-lookup"><span data-stu-id="d8717-123">IP configurations</span></span>
<span data-ttu-id="d8717-124">Nic 已命名的子物件**ipConfigurations**包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="d8717-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="d8717-125">屬性</span><span class="sxs-lookup"><span data-stu-id="d8717-125">Property</span></span> | <span data-ttu-id="d8717-126">說明</span><span class="sxs-lookup"><span data-stu-id="d8717-126">Description</span></span> | <span data-ttu-id="d8717-127">範例值</span><span class="sxs-lookup"><span data-stu-id="d8717-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8717-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="d8717-128">**subnet**</span></span> |<span data-ttu-id="d8717-129">子網路 hello NIC 是連接到。</span><span class="sxs-lookup"><span data-stu-id="d8717-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="d8717-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="d8717-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="d8717-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="d8717-131">**privateIPAddress**</span></span> |<span data-ttu-id="d8717-132">Hello 子網路中的 hello NIC 的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d8717-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="d8717-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="d8717-133">10.0.0.8</span></span> |
| <span data-ttu-id="d8717-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="d8717-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="d8717-135">IP 配置方法</span><span class="sxs-lookup"><span data-stu-id="d8717-135">IP allocation method</span></span> |<span data-ttu-id="d8717-136">動態或靜態</span><span class="sxs-lookup"><span data-stu-id="d8717-136">Dynamic or Static</span></span> |
| <span data-ttu-id="d8717-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="d8717-137">**enableIPForwarding**</span></span> |<span data-ttu-id="d8717-138">Hello NIC 是否可以使用的路由</span><span class="sxs-lookup"><span data-stu-id="d8717-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="d8717-139">True 或 False</span><span class="sxs-lookup"><span data-stu-id="d8717-139">true or false</span></span> |
| <span data-ttu-id="d8717-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="d8717-140">**primary**</span></span> |<span data-ttu-id="d8717-141">Hello NIC 是否 hello 主要的 NIC，供 hello VM</span><span class="sxs-lookup"><span data-stu-id="d8717-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="d8717-142">True 或 False</span><span class="sxs-lookup"><span data-stu-id="d8717-142">true or false</span></span> |
| <span data-ttu-id="d8717-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="d8717-143">**publicIPAddress**</span></span> |<span data-ttu-id="d8717-144">Hello NIC 相關聯的 PIP</span><span class="sxs-lookup"><span data-stu-id="d8717-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="d8717-145">請參閱 [DNS 設定](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="d8717-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="d8717-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="d8717-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="d8717-147">後端位址集區 hello NIC 是與相關聯</span><span class="sxs-lookup"><span data-stu-id="d8717-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="d8717-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="d8717-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="d8717-149">輸入 NIC 是與相關聯的負載平衡器 NAT 規則 hello</span><span class="sxs-lookup"><span data-stu-id="d8717-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="d8717-150">JSON 格式的範例公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="d8717-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="d8717-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="d8717-151">Additional resources</span></span>
* <span data-ttu-id="d8717-152">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163579.aspx)nic。</span><span class="sxs-lookup"><span data-stu-id="d8717-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

