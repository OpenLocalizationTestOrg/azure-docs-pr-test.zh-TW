## <a name="route-tables"></a><span data-ttu-id="9c456-101">路由表</span><span class="sxs-lookup"><span data-stu-id="9c456-101">Route tables</span></span>
<span data-ttu-id="9c456-102">路由表資源包含路由使用的 toodefine 流量 Azure 基礎結構中流動的方式。</span><span class="sxs-lookup"><span data-stu-id="9c456-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="9c456-103">您可以使用使用者定義的路由 (UDR) toosend 從給定的子網路 tooa 虛擬應用裝置，例如防火牆或入侵偵測系統 (ID) 的所有流量。</span><span class="sxs-lookup"><span data-stu-id="9c456-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="9c456-104">您可以將路由表 toosubnets 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9c456-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="9c456-105">路由表包含下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c456-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="9c456-106">屬性</span><span class="sxs-lookup"><span data-stu-id="9c456-106">Property</span></span> | <span data-ttu-id="9c456-107">說明</span><span class="sxs-lookup"><span data-stu-id="9c456-107">Description</span></span> | <span data-ttu-id="9c456-108">範例值</span><span class="sxs-lookup"><span data-stu-id="9c456-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c456-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="9c456-109">**routes**</span></span> |<span data-ttu-id="9c456-110">使用者的集合 hello 路由表中定義的路由</span><span class="sxs-lookup"><span data-stu-id="9c456-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="9c456-111">請參閱 [使用者定義的路由](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="9c456-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="9c456-112">**子網路**</span><span class="sxs-lookup"><span data-stu-id="9c456-112">**subnets**</span></span> |<span data-ttu-id="9c456-113">集合的子網路 hello 路由表太套用</span><span class="sxs-lookup"><span data-stu-id="9c456-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="9c456-114">請參閱 [子網路](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="9c456-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="9c456-115">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="9c456-115">User defined routes</span></span>
<span data-ttu-id="9c456-116">您可以建立 UDRs toospecify 應流量傳送到，根據其目的地位址。</span><span class="sxs-lookup"><span data-stu-id="9c456-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="9c456-117">您可以視為路由的 hello 預設閘道定義根據 hello 網路封包的目的地位址。</span><span class="sxs-lookup"><span data-stu-id="9c456-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="9c456-118">UDRs 包含下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c456-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="9c456-119">屬性</span><span class="sxs-lookup"><span data-stu-id="9c456-119">Property</span></span> | <span data-ttu-id="9c456-120">說明</span><span class="sxs-lookup"><span data-stu-id="9c456-120">Description</span></span> | <span data-ttu-id="9c456-121">範例值</span><span class="sxs-lookup"><span data-stu-id="9c456-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c456-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="9c456-122">**addressPrefix**</span></span> |<span data-ttu-id="9c456-123">位址首碼或完整 hello 目的地 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9c456-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="9c456-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="9c456-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="9c456-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="9c456-125">**nextHopType**</span></span> |<span data-ttu-id="9c456-126">將太傳送裝置 hello 流量類型</span><span class="sxs-lookup"><span data-stu-id="9c456-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="9c456-127">VirtualAppliance, VPN Gateway, Internet</span><span class="sxs-lookup"><span data-stu-id="9c456-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="9c456-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="9c456-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="9c456-129">Hello 下一個躍點 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9c456-129">IP address for hello next hop</span></span> |<span data-ttu-id="9c456-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="9c456-130">192.168.1.4</span></span> |

<span data-ttu-id="9c456-131">JSON 格式的範例路由表：</span><span class="sxs-lookup"><span data-stu-id="9c456-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="9c456-132">其他資源</span><span class="sxs-lookup"><span data-stu-id="9c456-132">Additional resources</span></span>
* <span data-ttu-id="9c456-133">取得 [UDR](../articles/virtual-network/virtual-networks-udr-overview.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9c456-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="9c456-134">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502549.aspx)的路由表。</span><span class="sxs-lookup"><span data-stu-id="9c456-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="9c456-135">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt502539.aspx)對於使用者定義的路由 (UDRs)。</span><span class="sxs-lookup"><span data-stu-id="9c456-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

