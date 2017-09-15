## <a name="route-tables"></a><span data-ttu-id="76844-101">路由表</span><span class="sxs-lookup"><span data-stu-id="76844-101">Route tables</span></span>
<span data-ttu-id="76844-102">路由表資源包含路由，用來定義流量如何在 Azure 基礎結構內流動。</span><span class="sxs-lookup"><span data-stu-id="76844-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="76844-103">您可以使用使用者定義的路由 (UDR) 將所有流量從給定的子網路傳送到虛擬應用裝置，例如防火牆或入侵偵測系統 (IDS)。</span><span class="sxs-lookup"><span data-stu-id="76844-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="76844-104">您可以將路由表與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="76844-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="76844-105">路由表包含下列屬性。</span><span class="sxs-lookup"><span data-stu-id="76844-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="76844-106">屬性</span><span class="sxs-lookup"><span data-stu-id="76844-106">Property</span></span> | <span data-ttu-id="76844-107">說明</span><span class="sxs-lookup"><span data-stu-id="76844-107">Description</span></span> | <span data-ttu-id="76844-108">範例值</span><span class="sxs-lookup"><span data-stu-id="76844-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76844-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="76844-109">**routes**</span></span> |<span data-ttu-id="76844-110">路由表中使用者定義的路由的集合</span><span class="sxs-lookup"><span data-stu-id="76844-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="76844-111">請參閱 [使用者定義的路由](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="76844-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="76844-112">**子網路**</span><span class="sxs-lookup"><span data-stu-id="76844-112">**subnets**</span></span> |<span data-ttu-id="76844-113">路由表套用的子網路的集合</span><span class="sxs-lookup"><span data-stu-id="76844-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="76844-114">請參閱 [子網路](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="76844-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="76844-115">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="76844-115">User defined routes</span></span>
<span data-ttu-id="76844-116">您可以根據流量的目的地位址建立 UDR 以指定流量應傳送到何處。</span><span class="sxs-lookup"><span data-stu-id="76844-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="76844-117">您可以將路由想成是根據網路封包的目的地位址定義的預設閘道。</span><span class="sxs-lookup"><span data-stu-id="76844-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="76844-118">UDR 包含下列屬性。</span><span class="sxs-lookup"><span data-stu-id="76844-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="76844-119">屬性</span><span class="sxs-lookup"><span data-stu-id="76844-119">Property</span></span> | <span data-ttu-id="76844-120">說明</span><span class="sxs-lookup"><span data-stu-id="76844-120">Description</span></span> | <span data-ttu-id="76844-121">範例值</span><span class="sxs-lookup"><span data-stu-id="76844-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76844-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="76844-122">**addressPrefix**</span></span> |<span data-ttu-id="76844-123">目的地的位址首碼或完整 IP 位址</span><span class="sxs-lookup"><span data-stu-id="76844-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="76844-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="76844-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="76844-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="76844-125">**nextHopType**</span></span> |<span data-ttu-id="76844-126">流量將傳送的目標裝置類型。</span><span class="sxs-lookup"><span data-stu-id="76844-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="76844-127">VirtualAppliance, VPN Gateway, Internet</span><span class="sxs-lookup"><span data-stu-id="76844-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="76844-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="76844-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="76844-129">下個躍點的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="76844-129">IP address for the next hop</span></span> |<span data-ttu-id="76844-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="76844-130">192.168.1.4</span></span> |

<span data-ttu-id="76844-131">JSON 格式的範例路由表：</span><span class="sxs-lookup"><span data-stu-id="76844-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="76844-132">其他資源</span><span class="sxs-lookup"><span data-stu-id="76844-132">Additional resources</span></span>
* <span data-ttu-id="76844-133">取得 [UDR](../articles/virtual-network/virtual-networks-udr-overview.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="76844-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="76844-134">閱讀關於路由表的 [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502549.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="76844-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="76844-135">閱讀關於使用者定義路由的 [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502539.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="76844-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

