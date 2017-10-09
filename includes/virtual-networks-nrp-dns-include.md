## <a name="azure-dns"></a><span data-ttu-id="11005-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="11005-101">Azure DNS</span></span>
<span data-ttu-id="11005-102">Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="11005-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="11005-103">屬性</span><span class="sxs-lookup"><span data-stu-id="11005-103">Property</span></span> | <span data-ttu-id="11005-104">說明</span><span class="sxs-lookup"><span data-stu-id="11005-104">Description</span></span> | <span data-ttu-id="11005-105">範例值</span><span class="sxs-lookup"><span data-stu-id="11005-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11005-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="11005-106">**DNSzones**</span></span> |<span data-ttu-id="11005-107">網域區域資訊 toohost DNS 記錄的特定網域</span><span class="sxs-lookup"><span data-stu-id="11005-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="11005-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="11005-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="11005-109">DNS 記錄集</span><span class="sxs-lookup"><span data-stu-id="11005-109">DNS record sets</span></span>
<span data-ttu-id="11005-110">DNS 區域擁有名為「記錄集」的子物件。</span><span class="sxs-lookup"><span data-stu-id="11005-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="11005-111">記錄集是 DNS 區域依類型分類之主機記錄的集合。</span><span class="sxs-lookup"><span data-stu-id="11005-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="11005-112">記錄類型有 A、AAAA、CNAME、MX、NS、SOA、SRV 和 TXT。</span><span class="sxs-lookup"><span data-stu-id="11005-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="11005-113">屬性</span><span class="sxs-lookup"><span data-stu-id="11005-113">Property</span></span> | <span data-ttu-id="11005-114">說明</span><span class="sxs-lookup"><span data-stu-id="11005-114">Description</span></span> | <span data-ttu-id="11005-115">範例值</span><span class="sxs-lookup"><span data-stu-id="11005-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11005-116">A</span><span class="sxs-lookup"><span data-stu-id="11005-116">A</span></span> |<span data-ttu-id="11005-117">IPv4 記錄類型</span><span class="sxs-lookup"><span data-stu-id="11005-117">IPv4 record type</span></span> |<span data-ttu-id="11005-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="11005-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="11005-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="11005-119">AAAA</span></span> |<span data-ttu-id="11005-120">IPv6 記錄類型</span><span class="sxs-lookup"><span data-stu-id="11005-120">IPv6 record type</span></span> |<span data-ttu-id="11005-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="11005-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="11005-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="11005-122">CNAME</span></span> |<span data-ttu-id="11005-123">正式名稱記錄類型 <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="11005-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="11005-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="11005-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="11005-125">MX</span><span class="sxs-lookup"><span data-stu-id="11005-125">MX</span></span> |<span data-ttu-id="11005-126">郵件記錄類型</span><span class="sxs-lookup"><span data-stu-id="11005-126">mail record type</span></span> |<span data-ttu-id="11005-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="11005-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="11005-128">NS</span><span class="sxs-lookup"><span data-stu-id="11005-128">NS</span></span> |<span data-ttu-id="11005-129">名稱伺服器記錄類型</span><span class="sxs-lookup"><span data-stu-id="11005-129">name server record type</span></span> |<span data-ttu-id="11005-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="11005-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="11005-131">SOA</span><span class="sxs-lookup"><span data-stu-id="11005-131">SOA</span></span> |<span data-ttu-id="11005-132">起始授權記錄類型 <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="11005-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="11005-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="11005-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="11005-134">SRV</span><span class="sxs-lookup"><span data-stu-id="11005-134">SRV</span></span> |<span data-ttu-id="11005-135">服務記錄類型</span><span class="sxs-lookup"><span data-stu-id="11005-135">service record type</span></span> |<span data-ttu-id="11005-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="11005-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="11005-137"><sup>1</sup> 每個記錄集僅允許一個值。</span><span class="sxs-lookup"><span data-stu-id="11005-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="11005-138"><sup>2</sup> 每個 DNS 區域僅允許一種記錄類型 SOA。</span><span class="sxs-lookup"><span data-stu-id="11005-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="11005-139">Json 格式的 DNS 區域範例：</span><span class="sxs-lookup"><span data-stu-id="11005-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="11005-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="11005-140">Additional resources</span></span>
<span data-ttu-id="11005-141">讀取 hello [DNS 區域的 REST API 文件](https://msdn.microsoft.com/library/azure/mt130626.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11005-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="11005-142">讀取 hello [DNS 資料錄集的 REST API 文件](https://msdn.microsoft.com/library/azure/mt130627.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11005-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

