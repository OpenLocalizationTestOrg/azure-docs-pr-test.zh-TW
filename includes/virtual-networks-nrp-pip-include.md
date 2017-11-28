## <a name="public-ip-address"></a><span data-ttu-id="38a43-101">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="38a43-101">Public IP address</span></span>
<span data-ttu-id="38a43-102">公用 IP 位址資源提供保留或動態的網際網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="38a43-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="38a43-103">雖然您可以將公用 IP 位址建立為獨立物件，但您必須將其關聯到另一個物件，才能實際使用該位址。</span><span class="sxs-lookup"><span data-stu-id="38a43-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="38a43-104">您可以將公用 IP 位址與負載平衡器、應用程式閘道或 NIC 建立關聯，提供以網際網路存取這些資源的能力。</span><span class="sxs-lookup"><span data-stu-id="38a43-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="38a43-105">屬性</span><span class="sxs-lookup"><span data-stu-id="38a43-105">Property</span></span> | <span data-ttu-id="38a43-106">說明</span><span class="sxs-lookup"><span data-stu-id="38a43-106">Description</span></span> | <span data-ttu-id="38a43-107">範例值</span><span class="sxs-lookup"><span data-stu-id="38a43-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38a43-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="38a43-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="38a43-109">定義 IP 位址是否為「靜態」或「動態」。</span><span class="sxs-lookup"><span data-stu-id="38a43-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="38a43-110">static、dynamic</span><span class="sxs-lookup"><span data-stu-id="38a43-110">static, dynamic</span></span> |
| <span data-ttu-id="38a43-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="38a43-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="38a43-112">定義閒置逾時，預設值為 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="38a43-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="38a43-113">如果在此時間內不再收到指定工作階段的封包，即終止工作階段。</span><span class="sxs-lookup"><span data-stu-id="38a43-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="38a43-114">介於 4 到 30 之間的任意值</span><span class="sxs-lookup"><span data-stu-id="38a43-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="38a43-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="38a43-115">**ipAddress**</span></span> |<span data-ttu-id="38a43-116">IP 位址已指派給物件。</span><span class="sxs-lookup"><span data-stu-id="38a43-116">IP address assigned to object.</span></span> <span data-ttu-id="38a43-117">這是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="38a43-117">This is a read-only property.</span></span> |<span data-ttu-id="38a43-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="38a43-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="38a43-119">DNS 設定</span><span class="sxs-lookup"><span data-stu-id="38a43-119">DNS settings</span></span>
<span data-ttu-id="38a43-120">公用 IP 位址有名為 **dnsSettings** 的子物件，其包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="38a43-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="38a43-121">屬性</span><span class="sxs-lookup"><span data-stu-id="38a43-121">Property</span></span> | <span data-ttu-id="38a43-122">說明</span><span class="sxs-lookup"><span data-stu-id="38a43-122">Description</span></span> | <span data-ttu-id="38a43-123">範例值</span><span class="sxs-lookup"><span data-stu-id="38a43-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38a43-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="38a43-124">**domainNameLabel**</span></span> |<span data-ttu-id="38a43-125">用於名稱解析的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="38a43-125">Host named used for name resolution.</span></span> |<span data-ttu-id="38a43-126">www、ftp、vm1</span><span class="sxs-lookup"><span data-stu-id="38a43-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="38a43-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="38a43-127">**fqdn**</span></span> |<span data-ttu-id="38a43-128">公用 IP 的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="38a43-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="38a43-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="38a43-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="38a43-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="38a43-130">**reverseFqdn**</span></span> |<span data-ttu-id="38a43-131">完整網域名稱，會解析成 IP 位址並在 DNS 中登錄為 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="38a43-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="38a43-132">www.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="38a43-132">www.contoso.com.</span></span> |

<span data-ttu-id="38a43-133">JSON 格式的範例公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="38a43-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="38a43-134">其他資源</span><span class="sxs-lookup"><span data-stu-id="38a43-134">Additional resources</span></span>
* <span data-ttu-id="38a43-135">取得 [公用 IP 位址](../articles/virtual-network/virtual-networks-reserved-public-ip.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38a43-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="38a43-136">了解 [執行個體層級公用 IP 位址](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="38a43-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="38a43-137">讀取公用 IP 位址的 [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163638.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="38a43-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

