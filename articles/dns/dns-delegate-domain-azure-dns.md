---
title: "aaaDelegate 您網域 tooAzure DNS |Microsoft 文件"
description: "了解如何 toochange 網域委派和使用 Azure DNS 名稱伺服器 tooprovide 網域裝載。"
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="558f6-103">委派網域 tooAzure DNS</span><span class="sxs-lookup"><span data-stu-id="558f6-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="558f6-104">Azure DNS 可讓您 toohost DNS 區域，並管理網域，以在 Azure 中的 hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="558f6-105">為了讓網域 tooreach Azure DNS 的 DNS 查詢，hello 網域有 toobe 從 hello 父系網域委派 tooAzure DNS。</span><span class="sxs-lookup"><span data-stu-id="558f6-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="558f6-106">請記住 Azure DNS 不 hello 網域註冊機構。</span><span class="sxs-lookup"><span data-stu-id="558f6-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="558f6-107">這篇文章說明如何 toodelegate 您網域 tooAzure DNS。</span><span class="sxs-lookup"><span data-stu-id="558f6-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="558f6-108">網域註冊機構購買，您的註冊機構提供 hello 選項 tooset 這些 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="558f6-109">您沒有 tooown 網域 toocreate DNS 區域與該網域名稱在 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="558f6-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="558f6-110">不過，您需要 tooown hello 網域 tooset 向上 hello 委派 tooAzure DNS 與 hello 註冊機構。</span><span class="sxs-lookup"><span data-stu-id="558f6-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="558f6-111">例如，假設您購買 hello 網域 'contoso.net'，Azure DNS 中建立 hello 名稱 'contoso.net' 與區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="558f6-112">做為 hello 網域 hello 擁有者，您的註冊機構會提供您的網域 hello 選項 tooconfigure hello 名稱伺服器位址 （也就是 hello NS 記錄）。</span><span class="sxs-lookup"><span data-stu-id="558f6-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="558f6-113">hello 註冊機構儲存在此情況下 '.net' hello 父系網域中的這些 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="558f6-114">Hello 世界各地的用戶端接著可以導向的 tooyour Azure DNS 區域中的網域時，嘗試在 'contoso.net' tooresolve DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="558f6-115">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="558f6-115">Create a DNS zone</span></span>

1. <span data-ttu-id="558f6-116">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="558f6-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="558f6-117">在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="558f6-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="558f6-119">在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="558f6-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="558f6-120">**設定**</span><span class="sxs-lookup"><span data-stu-id="558f6-120">**Setting**</span></span> | <span data-ttu-id="558f6-121">**值**</span><span class="sxs-lookup"><span data-stu-id="558f6-121">**Value**</span></span> | <span data-ttu-id="558f6-122">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="558f6-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="558f6-123">**名稱**</span><span class="sxs-lookup"><span data-stu-id="558f6-123">**Name**</span></span>|<span data-ttu-id="558f6-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="558f6-124">contoso.net</span></span>|<span data-ttu-id="558f6-125">hello hello DNS 區域名稱</span><span class="sxs-lookup"><span data-stu-id="558f6-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="558f6-126">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="558f6-126">**Subscription**</span></span>|<span data-ttu-id="558f6-127">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="558f6-127">[Your subscription]</span></span>|<span data-ttu-id="558f6-128">選取的訂用帳戶 toocreate hello 應用程式閘道中。</span><span class="sxs-lookup"><span data-stu-id="558f6-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="558f6-129">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="558f6-129">**Resource group**</span></span>|<span data-ttu-id="558f6-130">**建立新的︰**contosoRG</span><span class="sxs-lookup"><span data-stu-id="558f6-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="558f6-131">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="558f6-131">Create a resource group.</span></span> <span data-ttu-id="558f6-132">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="558f6-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="558f6-133">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="558f6-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="558f6-134">**位置**</span><span class="sxs-lookup"><span data-stu-id="558f6-134">**Location**</span></span>|<span data-ttu-id="558f6-135">美國西部</span><span class="sxs-lookup"><span data-stu-id="558f6-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="558f6-136">hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="558f6-137">hello DNS 區域位置一定是 「 全域 」，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="558f6-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="558f6-138">擷取名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="558f6-138">Retrieve name servers</span></span>

<span data-ttu-id="558f6-139">您可以將您的 DNS 區域 tooAzure DNS 委派之前，您必須先 tooknow hello 名稱區域的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="558f6-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="558f6-140">每次建立區域時，Azure DNS 都會配置某個集區中的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="558f6-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="558f6-141">Hello，hello Azure 入口網站中建立的 DNS 區域與**我的最愛**] 窗格中，按一下 [**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="558f6-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="558f6-142">按一下 hello **contoso.net** hello 中的 DNS 區域**所有資源**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="558f6-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="558f6-143">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contoso.net**中依名稱 hello 篩選...</span><span class="sxs-lookup"><span data-stu-id="558f6-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="558f6-144">方塊 tooeasily 存取 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="558f6-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="558f6-145">擷取 hello DNS 區域刀鋒視窗中的 hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="558f6-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="558f6-146">在此範例中，hello 區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'，'ns2 01.azure dns.net'、' ns3-01.azure-dns.org'，和 ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="558f6-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="558f6-148">Azure DNS 會自動建立您的區域，包含 hello 指派名稱伺服器中的權威 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="558f6-149">透過 Azure PowerShell 或 Azure CLI 命名 toosee hello 名稱伺服器，您只需要 tooretrieve 這些記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="558f6-150">hello 下列範例也提供 hello 步驟 tooretrieve hello 名稱伺服器中使用 PowerShell 和 Azure CLI Azure DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="558f6-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="558f6-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="558f6-152">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="558f6-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="558f6-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="558f6-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="558f6-154">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="558f6-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="558f6-155">委派 hello 網域</span><span class="sxs-lookup"><span data-stu-id="558f6-155">Delegate hello domain</span></span>

<span data-ttu-id="558f6-156">現在，建立 hello DNS 區域，而且您擁有 hello 名稱伺服器，需要 toobe hello Azure DNS 名稱伺服器以更新 hello 父網域。</span><span class="sxs-lookup"><span data-stu-id="558f6-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="558f6-157">每個註冊機構都有自己 DNS 管理工具 toochange hello 名稱伺服器記錄的網域。</span><span class="sxs-lookup"><span data-stu-id="558f6-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="558f6-158">在 hello 註冊機構的 DNS 管理頁面中，編輯 hello NS 記錄，以及取代的 hello 的 Azure DNS 建立 hello NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="558f6-159">當委派網域 tooAzure DNS 時，您必須使用 Azure DNS 所提供的 hello 名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="558f6-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="558f6-160">建議 toouse 所有四個名稱伺服器名稱，不論 hello 您的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="558f6-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="558f6-161">網域委派不需要 hello 名稱伺服器名稱 toouse hello 與您的網域相同的最上層網域。</span><span class="sxs-lookup"><span data-stu-id="558f6-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="558f6-162">您不應該使用 '黏附記錄' toopoint toohello Azure DNS 名稱伺服器 IP 位址，因為這些 IP 位址可能會在未來變更。</span><span class="sxs-lookup"><span data-stu-id="558f6-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="558f6-163">Azure DNS 目前不支援使用您區域中名稱伺服器名稱的委派 (有時稱為「虛名名稱伺服器」)。</span><span class="sxs-lookup"><span data-stu-id="558f6-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="558f6-164">確認名稱解析正常運作</span><span class="sxs-lookup"><span data-stu-id="558f6-164">Verify name resolution is working</span></span>

<span data-ttu-id="558f6-165">完成之後 hello 委派，您可以確認名稱解析使用 'nslookup' tooquery hello SOA 記錄之類的工具區域 （這也會自動建立時建立 hello 區域） 正常運作。</span><span class="sxs-lookup"><span data-stu-id="558f6-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="558f6-166">您不需要 toospecify hello Azure DNS 名稱伺服器，如果 hello 委派已設定正確，hello 一般 DNS 解析程序會尋找 hello 名稱伺服器自動。</span><span class="sxs-lookup"><span data-stu-id="558f6-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="558f6-167">hello 下面是從 hello 前面命令的範例回應：</span><span class="sxs-lookup"><span data-stu-id="558f6-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="558f6-168">在 Azure DNS 中委派子網域</span><span class="sxs-lookup"><span data-stu-id="558f6-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="558f6-169">如果您想 tooset 組成個別的子區域，您可以委派子網域中 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="558f6-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="558f6-170">比方說，需設定和委派 'contoso.net' Azure DNS 中的假設您想要不同的子區域中，向上 tooset 'partners.contoso.net'。</span><span class="sxs-lookup"><span data-stu-id="558f6-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="558f6-171">在 Azure DNS 中建立 hello 子區域 'partners.contoso.net'。</span><span class="sxs-lookup"><span data-stu-id="558f6-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="558f6-172">查閱 hello 權威 NS 記錄 hello 子區域 tooobtain hello 名稱伺服器裝載在 Azure DNS 中的 hello 子區域中。</span><span class="sxs-lookup"><span data-stu-id="558f6-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="558f6-173">藉由設定指向 toohello 子區域的 hello 上層區域中的 NS 記錄 hello 其子區域委派。</span><span class="sxs-lookup"><span data-stu-id="558f6-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="558f6-174">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="558f6-174">Create a DNS zone</span></span>

1. <span data-ttu-id="558f6-175">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="558f6-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="558f6-176">在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="558f6-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="558f6-178">在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="558f6-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="558f6-179">**設定**</span><span class="sxs-lookup"><span data-stu-id="558f6-179">**Setting**</span></span> | <span data-ttu-id="558f6-180">**值**</span><span class="sxs-lookup"><span data-stu-id="558f6-180">**Value**</span></span> | <span data-ttu-id="558f6-181">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="558f6-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="558f6-182">**名稱**</span><span class="sxs-lookup"><span data-stu-id="558f6-182">**Name**</span></span>|<span data-ttu-id="558f6-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="558f6-183">partners.contoso.net</span></span>|<span data-ttu-id="558f6-184">hello hello DNS 區域名稱</span><span class="sxs-lookup"><span data-stu-id="558f6-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="558f6-185">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="558f6-185">**Subscription**</span></span>|<span data-ttu-id="558f6-186">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="558f6-186">[Your subscription]</span></span>|<span data-ttu-id="558f6-187">選取的訂用帳戶 toocreate hello 應用程式閘道中。</span><span class="sxs-lookup"><span data-stu-id="558f6-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="558f6-188">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="558f6-188">**Resource group**</span></span>|<span data-ttu-id="558f6-189">**使用現有的︰**contosoRG</span><span class="sxs-lookup"><span data-stu-id="558f6-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="558f6-190">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="558f6-190">Create a resource group.</span></span> <span data-ttu-id="558f6-191">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="558f6-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="558f6-192">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="558f6-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="558f6-193">**位置**</span><span class="sxs-lookup"><span data-stu-id="558f6-193">**Location**</span></span>|<span data-ttu-id="558f6-194">美國西部</span><span class="sxs-lookup"><span data-stu-id="558f6-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="558f6-195">hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="558f6-196">hello DNS 區域位置一定是 「 全域 」，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="558f6-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="558f6-197">擷取名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="558f6-197">Retrieve name servers</span></span>

1. <span data-ttu-id="558f6-198">Hello，hello Azure 入口網站中建立的 DNS 區域與**我的最愛**] 窗格中，按一下 [**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="558f6-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="558f6-199">按一下 hello **partners.contoso.net** hello 中的 DNS 區域**所有資源**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="558f6-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="558f6-200">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**partners.contoso.net**中依名稱 hello 篩選...</span><span class="sxs-lookup"><span data-stu-id="558f6-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="558f6-201">方塊 tooeasily 存取 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="558f6-202">擷取 hello DNS 區域刀鋒視窗中的 hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="558f6-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="558f6-203">在此範例中，hello 區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'，'ns2 01.azure dns.net'、' ns3-01.azure-dns.org'，和 ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="558f6-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="558f6-205">Azure DNS 會自動建立您的區域，包含 hello 指派名稱伺服器中的權威 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="558f6-206">透過 Azure PowerShell 或 Azure CLI 命名 toosee hello 名稱伺服器，您只需要 tooretrieve 這些記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="558f6-207">在父系區域中建立名稱伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="558f6-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="558f6-208">瀏覽 toohello **contoso.net** hello Azure 入口網站中的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="558f6-209">按一下 [+ 記錄集]</span><span class="sxs-lookup"><span data-stu-id="558f6-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="558f6-210">在 hello**加入資料錄集**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="558f6-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="558f6-211">**設定**</span><span class="sxs-lookup"><span data-stu-id="558f6-211">**Setting**</span></span> | <span data-ttu-id="558f6-212">**值**</span><span class="sxs-lookup"><span data-stu-id="558f6-212">**Value**</span></span> | <span data-ttu-id="558f6-213">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="558f6-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="558f6-214">**名稱**</span><span class="sxs-lookup"><span data-stu-id="558f6-214">**Name**</span></span>|<span data-ttu-id="558f6-215">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="558f6-215">partners</span></span>|<span data-ttu-id="558f6-216">hello hello 子 DNS 區域名稱</span><span class="sxs-lookup"><span data-stu-id="558f6-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="558f6-217">**類型**</span><span class="sxs-lookup"><span data-stu-id="558f6-217">**Type**</span></span>|<span data-ttu-id="558f6-218">NS</span><span class="sxs-lookup"><span data-stu-id="558f6-218">NS</span></span>|<span data-ttu-id="558f6-219">使用 NS 作為名稱伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="558f6-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="558f6-220">**TTL**</span></span>|<span data-ttu-id="558f6-221">1</span><span class="sxs-lookup"><span data-stu-id="558f6-221">1</span></span>|<span data-ttu-id="558f6-222">Toolive 的時間。</span><span class="sxs-lookup"><span data-stu-id="558f6-222">Time toolive.</span></span>|
   |<span data-ttu-id="558f6-223">**TTL 單位**</span><span class="sxs-lookup"><span data-stu-id="558f6-223">**TTL unit**</span></span>|<span data-ttu-id="558f6-224">小時</span><span class="sxs-lookup"><span data-stu-id="558f6-224">Hours</span></span>|<span data-ttu-id="558f6-225">設定時間單位 toolive toohours</span><span class="sxs-lookup"><span data-stu-id="558f6-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="558f6-226">**名稱伺服器**</span><span class="sxs-lookup"><span data-stu-id="558f6-226">**NAME SERVER**</span></span>|<span data-ttu-id="558f6-227">{partners.contoso.net 區域中的名稱伺服器}</span><span class="sxs-lookup"><span data-stu-id="558f6-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="558f6-228">從 partners.contoso.net 區域輸入所有 4 hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="558f6-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="558f6-230">使用其他工具在 Azure DNS 中委派子網域</span><span class="sxs-lookup"><span data-stu-id="558f6-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="558f6-231">hello 下列範例提供 hello 步驟 toodelegate 子網域中使用 PowerShell 和 CLI Azure DNS:</span><span class="sxs-lookup"><span data-stu-id="558f6-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="558f6-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="558f6-232">PowerShell</span></span>

<span data-ttu-id="558f6-233">hello 下列 PowerShell 範例會示範其運作方式。</span><span class="sxs-lookup"><span data-stu-id="558f6-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="558f6-234">可以透過 hello Azure 入口網站執行相同的步驟，或透過 hello 跨平台 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="558f6-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="558f6-235">使用`nslookup`tooverify 的所有項目已正確設定時查閱 hello hello 子區域的 SOA 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="558f6-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="558f6-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="558f6-237">擷取 hello 名稱伺服器 hello `partners.contoso.net` hello 輸出中的區域。</span><span class="sxs-lookup"><span data-stu-id="558f6-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="558f6-238">建立 hello 資料錄集和每個名稱伺服器 NS 記錄。</span><span class="sxs-lookup"><span data-stu-id="558f6-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="558f6-239">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="558f6-239">Delete all resources</span></span>

<span data-ttu-id="558f6-240">在本文中完成下列步驟的 hello 建立 toodelete 所有資源：</span><span class="sxs-lookup"><span data-stu-id="558f6-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="558f6-241">在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="558f6-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="558f6-242">按一下 hello **contosorg** hello 資源刀鋒視窗中所有資源都群組。</span><span class="sxs-lookup"><span data-stu-id="558f6-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="558f6-243">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contosorg**在 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="558f6-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="558f6-244">方塊 tooeasily 存取 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="558f6-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="558f6-245">在 [hello **contosorg**刀鋒視窗中，按一下 hello**刪除**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="558f6-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="558f6-246">hello 入口網站需要您想要 toodelete hello 資源群組 tooconfirm tootype hello 名稱它。</span><span class="sxs-lookup"><span data-stu-id="558f6-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="558f6-247">型別*contosorg* hello 資源群組名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="558f6-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="558f6-248">刪除資源群組會刪除 hello 資源群組中的所有資源，所以一定會確定 tooconfirm hello 內容的資源群組然後再刪除。</span><span class="sxs-lookup"><span data-stu-id="558f6-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="558f6-249">hello 入口網站刪除 hello 的資源群組中包含的所有資源，然後都刪除本身 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="558f6-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="558f6-250">這個程序需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="558f6-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="558f6-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="558f6-251">Next steps</span></span>

[<span data-ttu-id="558f6-252">管理 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="558f6-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="558f6-253">管理 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="558f6-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
