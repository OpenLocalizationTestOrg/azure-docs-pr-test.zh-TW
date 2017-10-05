---
title: "將網域委派給 Azure DNS |Microsoft Docs"
description: "了解如何變更網域委派及使用 Azure DNS 名稱伺服器提供網域主機代管。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="67465-103">將網域委派給 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="67465-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="67465-104">Azure DNS 可讓您裝載 DNS 區域，並在 Azure 中管理網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="67465-105">網域必須從父系網域委派給 Azure DNS，該網域的 DNS 查詢才能送達 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="67465-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="67465-106">請記住，Azure DNS 不是網域註冊機構。</span><span class="sxs-lookup"><span data-stu-id="67465-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="67465-107">本文說明如何將您的網域委派給 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="67465-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="67465-108">如果是從註冊機構購買網域，註冊機構會提供選項來設定這些 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="67465-109">您不必擁有網域，也能在 Azure DNS 中以該網域名稱建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="67465-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="67465-110">不過，您必須擁有網域，才能在註冊機構中設定委派給 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="67465-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="67465-111">例如，假設您購買網域 'contoso.net'，並在 Azure DNS 中建立名稱為 'contoso.net' 的區域。</span><span class="sxs-lookup"><span data-stu-id="67465-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="67465-112">身為網域的擁有者，註冊機構會提供選項，讓您設定網域的名稱伺服器位址 (亦即 NS 記錄)。</span><span class="sxs-lookup"><span data-stu-id="67465-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="67465-113">註冊機構會將這些 NS 記錄儲存在父系網域中，在此範例中為 '.net'。</span><span class="sxs-lookup"><span data-stu-id="67465-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="67465-114">然後，當世界各地的用戶端嘗試解析 'contoso.net' 中的 DNS 記錄時，系統會將他們導向至您在 Azure DNS 區域中的網域。</span><span class="sxs-lookup"><span data-stu-id="67465-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="67465-115">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="67465-115">Create a DNS zone</span></span>

1. <span data-ttu-id="67465-116">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="67465-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="67465-117">在 [中樞] 功能表上，按一下 [新增] > [網路] > [DNS 區域] 以開啟 [建立 DNS 區域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="67465-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="67465-119">在 [建立 DNS 區域] 刀鋒視窗中輸入下列的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="67465-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="67465-120">**設定**</span><span class="sxs-lookup"><span data-stu-id="67465-120">**Setting**</span></span> | <span data-ttu-id="67465-121">**值**</span><span class="sxs-lookup"><span data-stu-id="67465-121">**Value**</span></span> | <span data-ttu-id="67465-122">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="67465-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="67465-123">**名稱**</span><span class="sxs-lookup"><span data-stu-id="67465-123">**Name**</span></span>|<span data-ttu-id="67465-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="67465-124">contoso.net</span></span>|<span data-ttu-id="67465-125">DNS 區域的名稱</span><span class="sxs-lookup"><span data-stu-id="67465-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="67465-126">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="67465-126">**Subscription**</span></span>|<span data-ttu-id="67465-127">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="67465-127">[Your subscription]</span></span>|<span data-ttu-id="67465-128">選取要在其中建立應用程式閘道的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="67465-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="67465-129">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="67465-129">**Resource group**</span></span>|<span data-ttu-id="67465-130">**建立新的︰**contosoRG</span><span class="sxs-lookup"><span data-stu-id="67465-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="67465-131">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="67465-131">Create a resource group.</span></span> <span data-ttu-id="67465-132">資源群組名稱在您選取的訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="67465-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="67465-133">若要深入了解資源群組，請閱讀 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 概觀。</span><span class="sxs-lookup"><span data-stu-id="67465-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="67465-134">**位置**</span><span class="sxs-lookup"><span data-stu-id="67465-134">**Location**</span></span>|<span data-ttu-id="67465-135">美國西部</span><span class="sxs-lookup"><span data-stu-id="67465-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="67465-136">資源群組是指資源群組的位置，不會對 DNS 區域有任何影響。</span><span class="sxs-lookup"><span data-stu-id="67465-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="67465-137">DNS 區域一定是「全域」位置，並不會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="67465-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="67465-138">擷取名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="67465-138">Retrieve name servers</span></span>

<span data-ttu-id="67465-139">在委派 DNS 區域給 Azure DNS 之前，您必須先知道區域的名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="67465-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="67465-140">每次建立區域時，Azure DNS 都會配置某個集區中的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="67465-141">建立 DNS 區域之後，在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="67465-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="67465-142">在 [所有資源] 刀鋒視窗中，按一下 [contoso.net] DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="67465-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="67465-143">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選...] 方塊中輸入 **contoso.net**，</span><span class="sxs-lookup"><span data-stu-id="67465-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="67465-144">輕鬆地存取應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="67465-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="67465-145">從 DNS 區域刀鋒視窗中擷取名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="67465-146">在此範例引，區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'、'ns2-01.azure-dns.net'、'ns3-01.azure-dns.org' 和 'ns4-01.azure-dns.info'：</span><span class="sxs-lookup"><span data-stu-id="67465-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="67465-148">Azure DNS 會自動在包含指派的名稱伺服器的區域中，建立權威 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="67465-149">您只需要擷取這些記錄，就能透過 Azure PowerShell 或 Azure CLI 查看名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="67465-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="67465-150">下列範例也會提供使用 PowerShell 和 Azure CLI 擷取 Azure DNS 中區域之名稱伺服器的步驟。</span><span class="sxs-lookup"><span data-stu-id="67465-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="67465-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67465-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="67465-152">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="67465-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="67465-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67465-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="67465-154">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="67465-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="67465-155">委派網域</span><span class="sxs-lookup"><span data-stu-id="67465-155">Delegate the domain</span></span>

<span data-ttu-id="67465-156">現已建立 DNS 區域且您擁有名稱伺服器，必須使用 Azure DNS 名稱伺服器來更新父系網域。</span><span class="sxs-lookup"><span data-stu-id="67465-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="67465-157">每個註冊機構都有自己的 DNS 管理工具，可變更網域的名稱伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="67465-158">在註冊機構的 DNS 管理頁面中，請編輯 NS 記錄，並將 NS 記錄取代為 Azure DNS 建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="67465-159">委派網域給 Azure DNS 時，您必須使用 Azure DNS 提供的名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="67465-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="67465-160">不論您的網域名稱為何，建議將名稱伺服器的 4 個名稱全部用上。</span><span class="sxs-lookup"><span data-stu-id="67465-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="67465-161">網域委派不需要名稱伺服器名稱，即可使用相同的最上層網域作為您的網域。</span><span class="sxs-lookup"><span data-stu-id="67465-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="67465-162">您不應該使用「黏附記錄」指向 Azure DNS 名稱伺服器 IP 位址，因為這些 IP 位址日後可能變更。</span><span class="sxs-lookup"><span data-stu-id="67465-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="67465-163">Azure DNS 目前不支援使用您區域中名稱伺服器名稱的委派 (有時稱為「虛名名稱伺服器」)。</span><span class="sxs-lookup"><span data-stu-id="67465-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="67465-164">確認名稱解析正常運作</span><span class="sxs-lookup"><span data-stu-id="67465-164">Verify name resolution is working</span></span>

<span data-ttu-id="67465-165">完成委派之後，您可以使用 'nslookup' 之類的工具來查詢您區域的 SOA 記錄 (這也是在建立區域時自動建立)，以確認名稱解析正常運作。</span><span class="sxs-lookup"><span data-stu-id="67465-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="67465-166">您不必指定 Azure DNS 名稱伺服器，如果已正確設定委派，正常的 DNS 解析程序會自動尋找名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="67465-167">以下是上述命令的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="67465-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="67465-168">在 Azure DNS 中委派子網域</span><span class="sxs-lookup"><span data-stu-id="67465-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="67465-169">如果您想要設定個別的子區域，您可以在 Azure DNS 中委派子網域。</span><span class="sxs-lookup"><span data-stu-id="67465-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="67465-170">例如，假設您想要設定個別的子區域 'partners.contoso.net'，請在 Azure DNS 中設定及委派 'contoso.net'。</span><span class="sxs-lookup"><span data-stu-id="67465-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="67465-171">在 Azure DNS 中建立子區域 'partners.contoso.net'。</span><span class="sxs-lookup"><span data-stu-id="67465-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="67465-172">查閱子區域中的權威 NS 記錄，來取得在 Azure DNS 中裝載子區域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="67465-173">在指向子區域的上層區域中設定 NS 記錄，以委派子區域。</span><span class="sxs-lookup"><span data-stu-id="67465-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="67465-174">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="67465-174">Create a DNS zone</span></span>

1. <span data-ttu-id="67465-175">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="67465-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="67465-176">在 [中樞] 功能表上，按一下 [新增] > [網路] > [DNS 區域] 以開啟 [建立 DNS 區域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="67465-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="67465-178">在 [建立 DNS 區域] 刀鋒視窗中輸入下列的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="67465-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="67465-179">**設定**</span><span class="sxs-lookup"><span data-stu-id="67465-179">**Setting**</span></span> | <span data-ttu-id="67465-180">**值**</span><span class="sxs-lookup"><span data-stu-id="67465-180">**Value**</span></span> | <span data-ttu-id="67465-181">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="67465-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="67465-182">**名稱**</span><span class="sxs-lookup"><span data-stu-id="67465-182">**Name**</span></span>|<span data-ttu-id="67465-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="67465-183">partners.contoso.net</span></span>|<span data-ttu-id="67465-184">DNS 區域的名稱</span><span class="sxs-lookup"><span data-stu-id="67465-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="67465-185">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="67465-185">**Subscription**</span></span>|<span data-ttu-id="67465-186">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="67465-186">[Your subscription]</span></span>|<span data-ttu-id="67465-187">選取要在其中建立應用程式閘道的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="67465-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="67465-188">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="67465-188">**Resource group**</span></span>|<span data-ttu-id="67465-189">**使用現有的︰**contosoRG</span><span class="sxs-lookup"><span data-stu-id="67465-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="67465-190">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="67465-190">Create a resource group.</span></span> <span data-ttu-id="67465-191">資源群組名稱在您選取的訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="67465-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="67465-192">若要深入了解資源群組，請閱讀 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 概觀。</span><span class="sxs-lookup"><span data-stu-id="67465-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="67465-193">**位置**</span><span class="sxs-lookup"><span data-stu-id="67465-193">**Location**</span></span>|<span data-ttu-id="67465-194">美國西部</span><span class="sxs-lookup"><span data-stu-id="67465-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="67465-195">資源群組是指資源群組的位置，不會對 DNS 區域有任何影響。</span><span class="sxs-lookup"><span data-stu-id="67465-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="67465-196">DNS 區域一定是「全域」位置，並不會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="67465-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="67465-197">擷取名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="67465-197">Retrieve name servers</span></span>

1. <span data-ttu-id="67465-198">建立 DNS 區域之後，在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="67465-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="67465-199">在 [所有資源] 刀鋒視窗中，按一下 [partners.contoso.net] DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="67465-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="67465-200">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選...] 方塊中輸入 **partners.contoso.net**，</span><span class="sxs-lookup"><span data-stu-id="67465-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="67465-201">輕鬆地存取 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="67465-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="67465-202">從 DNS 區域刀鋒視窗中擷取名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="67465-203">在此範例引，區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'、'ns2-01.azure-dns.net'、'ns3-01.azure-dns.org' 和 'ns4-01.azure-dns.info'：</span><span class="sxs-lookup"><span data-stu-id="67465-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="67465-205">Azure DNS 會自動在包含指派的名稱伺服器的區域中，建立權威 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="67465-206">您只需要擷取這些記錄，就能透過 Azure PowerShell 或 Azure CLI 查看名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="67465-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="67465-207">在父系區域中建立名稱伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="67465-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="67465-208">瀏覽至 Azure 入口網站中的 **contoso.net** DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="67465-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="67465-209">按一下 [+ 記錄集]</span><span class="sxs-lookup"><span data-stu-id="67465-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="67465-210">在 [新增記錄集] 刀鋒視窗上，輸入下列值，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="67465-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="67465-211">**設定**</span><span class="sxs-lookup"><span data-stu-id="67465-211">**Setting**</span></span> | <span data-ttu-id="67465-212">**值**</span><span class="sxs-lookup"><span data-stu-id="67465-212">**Value**</span></span> | <span data-ttu-id="67465-213">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="67465-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="67465-214">**名稱**</span><span class="sxs-lookup"><span data-stu-id="67465-214">**Name**</span></span>|<span data-ttu-id="67465-215">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="67465-215">partners</span></span>|<span data-ttu-id="67465-216">子 DNS 區域的名稱</span><span class="sxs-lookup"><span data-stu-id="67465-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="67465-217">**類型**</span><span class="sxs-lookup"><span data-stu-id="67465-217">**Type**</span></span>|<span data-ttu-id="67465-218">NS</span><span class="sxs-lookup"><span data-stu-id="67465-218">NS</span></span>|<span data-ttu-id="67465-219">使用 NS 作為名稱伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="67465-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="67465-220">**TTL**</span></span>|<span data-ttu-id="67465-221">1</span><span class="sxs-lookup"><span data-stu-id="67465-221">1</span></span>|<span data-ttu-id="67465-222">存留時間。</span><span class="sxs-lookup"><span data-stu-id="67465-222">Time to live.</span></span>|
   |<span data-ttu-id="67465-223">**TTL 單位**</span><span class="sxs-lookup"><span data-stu-id="67465-223">**TTL unit**</span></span>|<span data-ttu-id="67465-224">小時</span><span class="sxs-lookup"><span data-stu-id="67465-224">Hours</span></span>|<span data-ttu-id="67465-225">將存留時間單位設定為小時</span><span class="sxs-lookup"><span data-stu-id="67465-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="67465-226">**名稱伺服器**</span><span class="sxs-lookup"><span data-stu-id="67465-226">**NAME SERVER**</span></span>|<span data-ttu-id="67465-227">{partners.contoso.net 區域中的名稱伺服器}</span><span class="sxs-lookup"><span data-stu-id="67465-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="67465-228">輸入 partners.contoso.net 區域中的 4 個名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="67465-230">使用其他工具在 Azure DNS 中委派子網域</span><span class="sxs-lookup"><span data-stu-id="67465-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="67465-231">下列範例會提供使用 PowerShell 和 CLI 在 Azure DNS 中委派子網域的步驟︰</span><span class="sxs-lookup"><span data-stu-id="67465-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="67465-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67465-232">PowerShell</span></span>

<span data-ttu-id="67465-233">下列 PowerShell 範例將示範其運作方式。</span><span class="sxs-lookup"><span data-stu-id="67465-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="67465-234">透過 Azure 入口網站或跨平台 Azure CLI 也可執行相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="67465-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="67465-235">使用 `nslookup` 透過查閱子區域的 SOA 記錄，確認一切都已正確設定。</span><span class="sxs-lookup"><span data-stu-id="67465-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="67465-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67465-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="67465-237">從輸出擷取 `partners.contoso.net` 區域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="67465-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="67465-238">建立每部名稱伺服器的記錄集和 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="67465-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="67465-239">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="67465-239">Delete all resources</span></span>

<span data-ttu-id="67465-240">若要刪除這篇文章中建立的所有資源，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="67465-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="67465-241">在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="67465-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="67465-242">在 [所有資源] 刀鋒視窗中，按一下 [contosorg] 資源群組。</span><span class="sxs-lookup"><span data-stu-id="67465-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="67465-243">如果您選取的訂用帳戶已有幾個資源，可以在 [依名稱篩選...] 方塊中輸入 **contosorg**，</span><span class="sxs-lookup"><span data-stu-id="67465-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="67465-244">輕鬆地存取資源群組。</span><span class="sxs-lookup"><span data-stu-id="67465-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="67465-245">在 [contosorg] 刀鋒視窗中，按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="67465-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="67465-246">入口網站會要求您輸入資源群組的名稱，以確認您想要刪除它。</span><span class="sxs-lookup"><span data-stu-id="67465-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="67465-247">輸入 contosorg 作為資源群組名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="67465-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="67465-248">刪除資源群組會刪除資源群組內的所有資源，所以務必確認資源群組的內容，然後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="67465-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="67465-249">入口網站會刪除資源群組內包含的所有資源，然後刪除資源群組本身。</span><span class="sxs-lookup"><span data-stu-id="67465-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="67465-250">這個程序需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="67465-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67465-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67465-251">Next steps</span></span>

[<span data-ttu-id="67465-252">管理 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="67465-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="67465-253">管理 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="67465-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
