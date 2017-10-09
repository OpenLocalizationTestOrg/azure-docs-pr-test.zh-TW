## <a name="network-security-group"></a><span data-ttu-id="8a43e-101">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="8a43e-101">Network Security Group</span></span>
<span data-ttu-id="8a43e-102">NSG 資源可 hello 建立安全性界限的工作負載，藉由實作允許和拒絕規則。</span><span class="sxs-lookup"><span data-stu-id="8a43e-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="8a43e-103">這類規則可能會套用 tooa VM、 NIC 或子網路。</span><span class="sxs-lookup"><span data-stu-id="8a43e-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="8a43e-104">屬性</span><span class="sxs-lookup"><span data-stu-id="8a43e-104">Property</span></span> | <span data-ttu-id="8a43e-105">說明</span><span class="sxs-lookup"><span data-stu-id="8a43e-105">Description</span></span> | <span data-ttu-id="8a43e-106">範例值</span><span class="sxs-lookup"><span data-stu-id="8a43e-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a43e-107">**子網路**</span><span class="sxs-lookup"><span data-stu-id="8a43e-107">**subnets**</span></span> |<span data-ttu-id="8a43e-108">子網路識別碼 hello NSG 會套用至清單。</span><span class="sxs-lookup"><span data-stu-id="8a43e-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="8a43e-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="8a43e-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="8a43e-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="8a43e-110">**securityRules**</span></span> |<span data-ttu-id="8a43e-111">Hello NSG 構成安全性規則的清單</span><span class="sxs-lookup"><span data-stu-id="8a43e-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="8a43e-112">請參閱下方的 [安全性規則](#Security-rule)</span><span class="sxs-lookup"><span data-stu-id="8a43e-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="8a43e-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="8a43e-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="8a43e-114">出現在每個 NSG 中的預設安全性規則的清單</span><span class="sxs-lookup"><span data-stu-id="8a43e-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="8a43e-115">請參閱下方的 [預設安全性規則](#Default-security-rules)</span><span class="sxs-lookup"><span data-stu-id="8a43e-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="8a43e-116">**安全性規則** - NSG 可以定義多個安全性規則。</span><span class="sxs-lookup"><span data-stu-id="8a43e-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="8a43e-117">每個規則都可以允許或拒絕不同類型的流量。</span><span class="sxs-lookup"><span data-stu-id="8a43e-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="8a43e-118">安全性規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-118">Security rule</span></span>
<span data-ttu-id="8a43e-119">安全性規則是 NSG 包含 hello 屬性下方的子資源。</span><span class="sxs-lookup"><span data-stu-id="8a43e-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="8a43e-120">屬性</span><span class="sxs-lookup"><span data-stu-id="8a43e-120">Property</span></span> | <span data-ttu-id="8a43e-121">說明</span><span class="sxs-lookup"><span data-stu-id="8a43e-121">Description</span></span> | <span data-ttu-id="8a43e-122">範例值</span><span class="sxs-lookup"><span data-stu-id="8a43e-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a43e-123">**description**</span><span class="sxs-lookup"><span data-stu-id="8a43e-123">**description**</span></span> |<span data-ttu-id="8a43e-124">Hello 規則描述</span><span class="sxs-lookup"><span data-stu-id="8a43e-124">Description for hello rule</span></span> |<span data-ttu-id="8a43e-125">在子網路 X 中允許所有 VM 的輸入流量</span><span class="sxs-lookup"><span data-stu-id="8a43e-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="8a43e-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="8a43e-126">**protocol**</span></span> |<span data-ttu-id="8a43e-127">通訊協定 toomatch hello 規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-128">TCP、UDP 或 *</span><span class="sxs-lookup"><span data-stu-id="8a43e-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="8a43e-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="8a43e-129">**sourcePortRange**</span></span> |<span data-ttu-id="8a43e-130">來源連接埠範圍 toomatch hello 規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="8a43e-131">80, 100-200, *</span></span> |
| <span data-ttu-id="8a43e-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="8a43e-132">**destinationPortRange**</span></span> |<span data-ttu-id="8a43e-133">目的地連接埠範圍 toomatch hello 規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="8a43e-134">80, 100-200, *</span></span> |
| <span data-ttu-id="8a43e-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="8a43e-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="8a43e-136">來源位址前置詞 toomatch hello 規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8a43e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="8a43e-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="8a43e-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="8a43e-139">目的地位址前置詞 toomatch hello 規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8a43e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="8a43e-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="8a43e-141">**direction**</span></span> |<span data-ttu-id="8a43e-142">Hello 規則的流量 toomatch 的方向</span><span class="sxs-lookup"><span data-stu-id="8a43e-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="8a43e-143">inbound (輸入) 或 outbound (輸出)</span><span class="sxs-lookup"><span data-stu-id="8a43e-143">inbound or outbound</span></span> |
| <span data-ttu-id="8a43e-144">**優先順序**</span><span class="sxs-lookup"><span data-stu-id="8a43e-144">**priority**</span></span> |<span data-ttu-id="8a43e-145">Hello 規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="8a43e-145">Priority for hello rule.</span></span> <span data-ttu-id="8a43e-146">系統會依照規則優先順序檢查規則，一旦套用規則，就不會再測試規則是否符合。</span><span class="sxs-lookup"><span data-stu-id="8a43e-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="8a43e-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="8a43e-147">10, 100, 65000</span></span> |
| <span data-ttu-id="8a43e-148">**access**</span><span class="sxs-lookup"><span data-stu-id="8a43e-148">**access**</span></span> |<span data-ttu-id="8a43e-149">存取 tooapply 如果 hello 規則符合的型別</span><span class="sxs-lookup"><span data-stu-id="8a43e-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="8a43e-150">allow (允許) 或 deny (拒絕)</span><span class="sxs-lookup"><span data-stu-id="8a43e-150">allow or deny</span></span> |

<span data-ttu-id="8a43e-151">JSON 格式的範例 NSG：</span><span class="sxs-lookup"><span data-stu-id="8a43e-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="8a43e-152">預設安全性規則</span><span class="sxs-lookup"><span data-stu-id="8a43e-152">Default security rules</span></span>

<span data-ttu-id="8a43e-153">預設安全性規則具有 hello 安全性規則中相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="8a43e-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="8a43e-154">其存在 tooprovide 所套用的 Nsg toothem 資源之間的基本連線能力。</span><span class="sxs-lookup"><span data-stu-id="8a43e-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="8a43e-155">請確定您知道哪些[預設安全性規則](../articles/virtual-network/virtual-networks-nsg.md#default-rules)存在。</span><span class="sxs-lookup"><span data-stu-id="8a43e-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="8a43e-156">其他資源</span><span class="sxs-lookup"><span data-stu-id="8a43e-156">Additional resources</span></span>
* <span data-ttu-id="8a43e-157">取得 [NSG](../articles/virtual-network/virtual-networks-nsg.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8a43e-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="8a43e-158">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163615.aspx)的 Nsg。</span><span class="sxs-lookup"><span data-stu-id="8a43e-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="8a43e-159">讀取 hello [REST API 參考文件](https://msdn.microsoft.com/library/azure/mt163580.aspx)安全性規則。</span><span class="sxs-lookup"><span data-stu-id="8a43e-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
