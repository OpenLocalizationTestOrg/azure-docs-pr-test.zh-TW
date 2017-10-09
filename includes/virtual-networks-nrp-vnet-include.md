## <a name="virtual-network"></a><span data-ttu-id="4d62a-101">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4d62a-101">Virtual Network</span></span>
<span data-ttu-id="4d62a-102">虛擬網路 (VNET) 和子網路資源有助於定義在 Azure 中執行之工作負載的安全性範圍。</span><span class="sxs-lookup"><span data-stu-id="4d62a-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="4d62a-103">VNET 可由一組位址空間集合所界定 (此集合定義為 CIDR 區塊)。</span><span class="sxs-lookup"><span data-stu-id="4d62a-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d62a-104">網路管理員都熟悉 CIDR 標記法。</span><span class="sxs-lookup"><span data-stu-id="4d62a-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="4d62a-105">如果您不熟悉 CIDR，請 [深入了解](http://whatismyipaddress.com/cidr)。</span><span class="sxs-lookup"><span data-stu-id="4d62a-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![含有多個子網路的 VNET](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="4d62a-107">Vnet 包含下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d62a-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="4d62a-108">屬性</span><span class="sxs-lookup"><span data-stu-id="4d62a-108">Property</span></span> | <span data-ttu-id="4d62a-109">說明</span><span class="sxs-lookup"><span data-stu-id="4d62a-109">Description</span></span> | <span data-ttu-id="4d62a-110">範例值</span><span class="sxs-lookup"><span data-stu-id="4d62a-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d62a-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="4d62a-111">**addressSpace**</span></span> |<span data-ttu-id="4d62a-112">位址首碼 hello VNet 以 CIDR 標記法所組成的集合</span><span class="sxs-lookup"><span data-stu-id="4d62a-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="4d62a-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4d62a-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="4d62a-114">**子網路**</span><span class="sxs-lookup"><span data-stu-id="4d62a-114">**subnets**</span></span> |<span data-ttu-id="4d62a-115">組成 hello VNet 的子網路的集合</span><span class="sxs-lookup"><span data-stu-id="4d62a-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="4d62a-116">請參閱下方的 [子網路](#Subnets) 。</span><span class="sxs-lookup"><span data-stu-id="4d62a-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="4d62a-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="4d62a-117">**ipAddress**</span></span> |<span data-ttu-id="4d62a-118">Tooobject 指派 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d62a-118">IP address assigned tooobject.</span></span> <span data-ttu-id="4d62a-119">這是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="4d62a-119">This is a read-only property.</span></span> |<span data-ttu-id="4d62a-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="4d62a-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="4d62a-121">子網路</span><span class="sxs-lookup"><span data-stu-id="4d62a-121">Subnets</span></span>
<span data-ttu-id="4d62a-122">子網路是 VNET 的子資源，而且有助於使用 IP 位址首碼來定義 CIDR 區塊內位址空間的區段。</span><span class="sxs-lookup"><span data-stu-id="4d62a-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="4d62a-123">Nic 可以加入 toosubnets，並已連線的 tooVMs，提供各種工作負載的連線。</span><span class="sxs-lookup"><span data-stu-id="4d62a-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="4d62a-124">子網路包含下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d62a-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="4d62a-125">屬性</span><span class="sxs-lookup"><span data-stu-id="4d62a-125">Property</span></span> | <span data-ttu-id="4d62a-126">說明</span><span class="sxs-lookup"><span data-stu-id="4d62a-126">Description</span></span> | <span data-ttu-id="4d62a-127">範例值</span><span class="sxs-lookup"><span data-stu-id="4d62a-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d62a-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="4d62a-128">**addressPrefix**</span></span> |<span data-ttu-id="4d62a-129">Hello 子網路，以 CIDR 標記法所組成的單一位址首碼</span><span class="sxs-lookup"><span data-stu-id="4d62a-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="4d62a-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="4d62a-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="4d62a-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="4d62a-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="4d62a-132">NSG 套用 toohello 子網路</span><span class="sxs-lookup"><span data-stu-id="4d62a-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="4d62a-133">請參閱 [NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="4d62a-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="4d62a-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="4d62a-134">**routeTable**</span></span> |<span data-ttu-id="4d62a-135">路由表套用 toohello 子網路</span><span class="sxs-lookup"><span data-stu-id="4d62a-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="4d62a-136">請參閱 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="4d62a-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="4d62a-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="4d62a-137">**ipConfigurations**</span></span> |<span data-ttu-id="4d62a-138">Nic 已連線的 toohello 子網路所使用的 IP 設定物件的集合</span><span class="sxs-lookup"><span data-stu-id="4d62a-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="4d62a-139">請參閱 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="4d62a-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="4d62a-140">JSON 格式的範例 VNET：</span><span class="sxs-lookup"><span data-stu-id="4d62a-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="4d62a-141">其他資源</span><span class="sxs-lookup"><span data-stu-id="4d62a-141">Additional resources</span></span>
* <span data-ttu-id="4d62a-142">取得 [VNET](../articles/virtual-network/virtual-networks-overview.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4d62a-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="4d62a-143">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163650.aspx)vnet。</span><span class="sxs-lookup"><span data-stu-id="4d62a-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="4d62a-144">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163618.aspx)子網路。</span><span class="sxs-lookup"><span data-stu-id="4d62a-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

