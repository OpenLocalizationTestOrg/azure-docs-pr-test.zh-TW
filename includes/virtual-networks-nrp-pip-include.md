## <a name="public-ip-address"></a><span data-ttu-id="071b9-101">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="071b9-101">Public IP address</span></span>
<span data-ttu-id="071b9-102">公用 IP 位址資源提供保留或動態的網際網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="071b9-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="071b9-103">雖然您可以建立為獨立物件的公用 IP 位址，您需要 tooassociate 它 tooanother 物件 tooactually 使用 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="071b9-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="071b9-104">您可以將公用 IP 位址 tooa 負載平衡器、 應用程式閘道或 NIC tooprovide 網際網路存取 toothose 資源建立關聯。</span><span class="sxs-lookup"><span data-stu-id="071b9-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="071b9-105">屬性</span><span class="sxs-lookup"><span data-stu-id="071b9-105">Property</span></span> | <span data-ttu-id="071b9-106">說明</span><span class="sxs-lookup"><span data-stu-id="071b9-106">Description</span></span> | <span data-ttu-id="071b9-107">範例值</span><span class="sxs-lookup"><span data-stu-id="071b9-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="071b9-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="071b9-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="071b9-109">定義 hello IP 位址是否*靜態*或*動態*。</span><span class="sxs-lookup"><span data-stu-id="071b9-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="071b9-110">static、dynamic</span><span class="sxs-lookup"><span data-stu-id="071b9-110">static, dynamic</span></span> |
| <span data-ttu-id="071b9-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="071b9-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="071b9-112">定義 hello 閒置逾時，預設值為 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="071b9-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="071b9-113">如果沒有指定工作階段的多個封包這段時間內收到，hello 工作階段已終止。</span><span class="sxs-lookup"><span data-stu-id="071b9-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="071b9-114">介於 4 到 30 之間的任意值</span><span class="sxs-lookup"><span data-stu-id="071b9-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="071b9-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="071b9-115">**ipAddress**</span></span> |<span data-ttu-id="071b9-116">Tooobject 指派 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="071b9-116">IP address assigned tooobject.</span></span> <span data-ttu-id="071b9-117">這是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="071b9-117">This is a read-only property.</span></span> |<span data-ttu-id="071b9-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="071b9-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="071b9-119">DNS 設定</span><span class="sxs-lookup"><span data-stu-id="071b9-119">DNS settings</span></span>
<span data-ttu-id="071b9-120">公用 IP 位址具有名為的子物件**dnsSettings**包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="071b9-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="071b9-121">屬性</span><span class="sxs-lookup"><span data-stu-id="071b9-121">Property</span></span> | <span data-ttu-id="071b9-122">說明</span><span class="sxs-lookup"><span data-stu-id="071b9-122">Description</span></span> | <span data-ttu-id="071b9-123">範例值</span><span class="sxs-lookup"><span data-stu-id="071b9-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="071b9-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="071b9-124">**domainNameLabel**</span></span> |<span data-ttu-id="071b9-125">用於名稱解析的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="071b9-125">Host named used for name resolution.</span></span> |<span data-ttu-id="071b9-126">www、ftp、vm1</span><span class="sxs-lookup"><span data-stu-id="071b9-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="071b9-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="071b9-127">**fqdn**</span></span> |<span data-ttu-id="071b9-128">Hello 公用 ip 的完整限定的名稱。</span><span class="sxs-lookup"><span data-stu-id="071b9-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="071b9-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="071b9-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="071b9-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="071b9-130">**reverseFqdn**</span></span> |<span data-ttu-id="071b9-131">Toohello IP 位址解析，且會註冊在 DNS PTR 記錄的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="071b9-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="071b9-132">www.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="071b9-132">www.contoso.com.</span></span> |

<span data-ttu-id="071b9-133">JSON 格式的範例公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="071b9-133">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="071b9-134">其他資源</span><span class="sxs-lookup"><span data-stu-id="071b9-134">Additional resources</span></span>
* <span data-ttu-id="071b9-135">取得 [公用 IP 位址](../articles/virtual-network/virtual-networks-reserved-public-ip.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="071b9-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="071b9-136">了解 [執行個體層級公用 IP 位址](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="071b9-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="071b9-137">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163638.aspx)公用 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="071b9-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

