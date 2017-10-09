## <a name="traffic-manager-profile"></a><span data-ttu-id="d7830-101">流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="d7830-101">Traffic Manager Profile</span></span>
<span data-ttu-id="d7830-102">Traffic manager，且其子 endpoint 資源可讓在 Azure 和 Azure 外部 DNS 路由 tooendpoints。</span><span class="sxs-lookup"><span data-stu-id="d7830-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="d7830-103">這類流量分配是由路由原則方法所管理。</span><span class="sxs-lookup"><span data-stu-id="d7830-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="d7830-104">Traffic manager 也可讓您監視端點健全狀況 toobe，並被導向適當的流量會根據 hello 健全狀況的端點。</span><span class="sxs-lookup"><span data-stu-id="d7830-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="d7830-105">屬性</span><span class="sxs-lookup"><span data-stu-id="d7830-105">Property</span></span> | <span data-ttu-id="d7830-106">說明</span><span class="sxs-lookup"><span data-stu-id="d7830-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7830-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="d7830-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="d7830-108">可能的值為 *Performance*、*Weighted* 和 *Priority*</span><span class="sxs-lookup"><span data-stu-id="d7830-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="d7830-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="d7830-109">**dnsConfig**</span></span> |<span data-ttu-id="d7830-110">Hello 設定檔的 FQDN</span><span class="sxs-lookup"><span data-stu-id="d7830-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="d7830-111">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="d7830-111">**Protocol**</span></span> |<span data-ttu-id="d7830-112">監視通訊協定，可能的值為 *HTTP* 和 *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="d7830-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="d7830-113">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="d7830-113">**Port**</span></span> |<span data-ttu-id="d7830-114">監視連接埠</span><span class="sxs-lookup"><span data-stu-id="d7830-114">monitoring port</span></span> |
| <span data-ttu-id="d7830-115">**路徑**</span><span class="sxs-lookup"><span data-stu-id="d7830-115">**Path**</span></span> |<span data-ttu-id="d7830-116">監視路徑</span><span class="sxs-lookup"><span data-stu-id="d7830-116">monitoring path</span></span> |
| <span data-ttu-id="d7830-117">**Endpoints**</span><span class="sxs-lookup"><span data-stu-id="d7830-117">**Endpoints**</span></span> |<span data-ttu-id="d7830-118">端點資源的容器</span><span class="sxs-lookup"><span data-stu-id="d7830-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="d7830-119">端點</span><span class="sxs-lookup"><span data-stu-id="d7830-119">Endpoint</span></span>
<span data-ttu-id="d7830-120">端點是流量管理員設定檔的子資源。</span><span class="sxs-lookup"><span data-stu-id="d7830-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="d7830-121">它代表服務或 web 端點 toowhich 使用者流量分散根據 hello Traffic Manager 設定檔的資源中的 hello 設定原則。</span><span class="sxs-lookup"><span data-stu-id="d7830-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="d7830-122">屬性</span><span class="sxs-lookup"><span data-stu-id="d7830-122">Property</span></span> | <span data-ttu-id="d7830-123">說明</span><span class="sxs-lookup"><span data-stu-id="d7830-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7830-124">**類型**</span><span class="sxs-lookup"><span data-stu-id="d7830-124">**Type**</span></span> |<span data-ttu-id="d7830-125">hello 類型可能的值為 hello 端點的*Azure 結束點*，*外部端點*，和*巢狀的端點*</span><span class="sxs-lookup"><span data-stu-id="d7830-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="d7830-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="d7830-126">**targetResourceId**</span></span> |<span data-ttu-id="d7830-127">服務或 Web 端點的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d7830-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="d7830-128">這可以是 Azure 或外部端點。</span><span class="sxs-lookup"><span data-stu-id="d7830-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="d7830-129">**重量**</span><span class="sxs-lookup"><span data-stu-id="d7830-129">**Weight**</span></span> |<span data-ttu-id="d7830-130">用於流量管理的端點加權。</span><span class="sxs-lookup"><span data-stu-id="d7830-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="d7830-131">**優先順序**</span><span class="sxs-lookup"><span data-stu-id="d7830-131">**Priority**</span></span> |<span data-ttu-id="d7830-132">hello 端點，使用 toodefine 容錯移轉動作的優先順序</span><span class="sxs-lookup"><span data-stu-id="d7830-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="d7830-133">JSON 格式的流量管理員範例：</span><span class="sxs-lookup"><span data-stu-id="d7830-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="d7830-134">其他資源</span><span class="sxs-lookup"><span data-stu-id="d7830-134">Additional resources</span></span>
<span data-ttu-id="d7830-135">如需詳細資訊，請閱讀 [流量管理員的 REST API 文件](https://msdn.microsoft.com/library/azure/mt163664.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d7830-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

