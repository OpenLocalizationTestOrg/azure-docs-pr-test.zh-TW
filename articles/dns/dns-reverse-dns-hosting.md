---
title: "aaaHosting 反向 DNS 對應區域，在 Azure DNS |Microsoft 文件"
description: "了解如何 toouse Azure DNS toohost hello 反向 DNS 對應區域的 IP 範圍"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>在 Azure DNS 中託管反向 DNS 對應區域

本文說明如何 toohost hello 反轉您指派的 IP 範圍中 Azure DNS 的 DNS 對應區域。 hello IP 範圍由 hello 反向對應區域，必須指派 tooyour 組織通常由您的 ISP。

tooconfigure 反向 DNS Azure 擁有 IP 位址指派 tooyour Azure 服務，請參閱[hello IP 位址配置 tooyour Azure 服務設定 hello 反向對應](dns-reverse-dns-for-azure-services.md)。

在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。

這篇文章會引導您透過 hello 步驟 toocreate 您的第一個反向對應 DNS 區域與記錄使用 hello Azure 入口網站，Azure PowerShell、 Azure CLI 1.0 或 Azure CLI 2.0。

## <a name="create-a-reverse-lookup-dns-zone"></a>建立反向對應 DNS 區域

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)
1. 在 hello 中樞功能表中，按一下，然後按一下**新增** > **網路**>，然後按一下 **DNS 區域**tooopen hello**建立 DNS 區域**刀鋒視窗。

   ![DNS 區域](./media/dns-reverse-dns-hosting/figure1.png)

1. 在 hello**建立 DNS 區域**刀鋒視窗中，命名您的 DNS 區域。 hello hello 區域名稱是以不同的方式製作的 IPv4 和 IPv6 首碼。 使用任一個 hello 指示[IPV4](#ipv4)或[IPv6](#ipv6) tooname 您的區域。 當完成時按一下**建立**toocreate hello 區域。

### <a name="ipv4"></a>IPv4

IPv4 反向對應區域的 hello 名稱根據它所代表的 hello IP 範圍。 應為下列格式的 hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`。 如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv4)。

> [!NOTE]
> 當 Azure DNS 中建立 classless inter-domain routing 反向 DNS 查閱區域，您必須使用連字號 (`-`) 而不是正斜線 （'/') 在 hello 區域名稱。
>
> 例如，針對 hello IP 範圍 192.0.2.128/26，您必須使用`128-26.2.0.192.in-addr.arpa`hello 區域名稱，而不是為`128/26.2.0.192.in-addr.arpa`。
>
> 這是因為雖然兩者 hello DNS 標準的支援，DNS 區域名稱中包含 hello 正斜線 (`/`) Azure DNS 中不支援的字元。

hello 下列範例示範如何 toocreate ' 類別 C' 反向 DNS 區域命名為`2.0.192.in-addr.arpa`Azure DNS 透過 hello Azure 入口網站中：

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure2.png)

hello '資源群組位置' 定義 hello 位置 hello 資源群組，且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 'global'，而且不會顯示。

hello 下列範例顯示如何 toocomplete 此工作使用 Azure PowerShell 和 hello Azure CLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

IPv6 反向對應區域的 hello 名稱應為下列格式的 hello: `<IPv6 network prefix in reverse order>.ip6.arpa`。  如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv6)。


hello 下列範例示範如何 toocreate IPv6 反向 DNS 查閱區域命名`0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa`Azure DNS 透過 hello Azure 入口網站中：

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure3.png)

hello '資源群組位置' 定義 hello 位置 hello 資源群組，且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 'global'，而且不會顯示。

hello 下列範例顯示如何 toocomplete 此工作使用 Azure PowerShell 和 hello Azure CLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>委派反向 DNS 對應區域

一旦建立 DNS 反向查閱區域，您必須確定該 hello 區域會從 hello 父區域委派。 DNS 委派可讓 hello DNS 名稱解析程序 toofind hello 名稱伺服器裝載 DNS 反向查閱區域。 這可讓這些名稱伺服器 tooanswer DNS 反向查詢 hello 中的 IP 位址的位址範圍。

正向對應區域的委派 DNS 區域的 hello 程序所述[委派您網域 tooAzure DNS](dns-delegate-domain-azure-dns.md)。 反向對應區域的委派 hello 的運作方式相同。 hello 唯一的差別是您需要以提供您的 IP 範圍，而不是網域名稱註冊機構的 ISP hello tooconfigure hello 名稱伺服器。

## <a name="create-a-dns-ptr-record"></a>建立 DNS PTR 記錄

### <a name="ipv4"></a>IPv4

hello 下列範例將引導您 hello 程序建立反向 DNS 區域中 Azure DNS PTR 記錄。 其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。

1.  頂端的 hello hello **DNS 區域**刀鋒視窗中，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。

 ![DNS 區域](./media/dns-reverse-dns-hosting/figure4.png)

1. 在 hello**加入資料錄集**刀鋒視窗。 
1. 選取**PTR** hello 記錄 」**類型**」 功能表。  
1. hello PTR 記錄 hello 資料錄集的名稱必須 toobe hello rest hello IPv4 位址的反向順序。 在此範例中，hello 前三個八位元都已填入 hello 區域名稱 (.2.0.192) 的一部分。 因此，只有 hello 最後一個八位元會提供 hello 名稱 欄位中。 例如，您可以將 IP 位址是 192.0.2.15 的資源記錄集命名為 "**15**"。  
1. 在 hello"**網域名稱**」 欄位中，輸入 hello 資源使用 hello IP 的 hello 完整的網域名稱 (FQDN)。
1. 選取**確定**底部 hello hello 刀鋒視窗 toocreate hello DNS 記錄。

 ![新增記錄集](./media/dns-reverse-dns-hosting/figure5.png)

hello 以下舉例說明幾如何 toocomplete 使用 PowerShell 和 hello AzureCLI 這項工作：

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

下列範例中的 hello 會引導您建立新的 'PTR' 記錄的 hello 程序。 其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。

1. 頂端的 hello hello **DNS 區域刀鋒視窗**，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。

  ![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure6.png)

2. 在 hello**加入資料錄集**刀鋒視窗。 
3. 選取**PTR** hello 記錄 」**類型**」 功能表。  
4. hello PTR 記錄 hello 資料錄集的名稱必須 toobe hello rest hello IPv6 位址的反向順序。 它絕不能包含任何零壓縮。 在此範例中，hello 的 hello IPv6 都已填入 hello 區域名稱 (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa) 的一部分的第一個 64 位元。 因此，hello 最後的 64 位元 hello 名稱 欄位中提供。 hello hello IP 位址的最後一個 64 位元會輸入以相反順序中，使用句號做為每個十六進位數字之間的 hello 分隔符號。 例如，您可以將 IP 位址是 2001:0db8:abdc:0000:f524:10bc:1af9:405e 的資源記錄集命名為 "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**"。  
5. 在 hello"**網域名稱**」 欄位中，輸入 hello 資源使用 hello IP 的 hello 完整的網域名稱 (FQDN)。
6. 選取**確定**底部 hello hello 刀鋒視窗 toocreate hello DNS 記錄。

![新增記錄集刀鋒視窗](./media/dns-reverse-dns-hosting/figure7.png)

hello 以下舉例說明幾如何 toocomplete 使用 PowerShell 和 hello AzureCLI 這項工作：

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>檢視記錄

tooview hello 記錄建立時，瀏覽 tooyour hello Azure 入口網站中的 DNS 區域。 Hello 中較低的 hello 一部分**DNS 區域**刀鋒視窗中，您可以看到 hello hello DNS 區域的記錄。 您應該會看到 hello 預設 NS 與 SOA 記錄，也就建立在每個區域中加上您建立任何新記錄。

### <a name="ipv4"></a>IPv4

[DNS 區域] 刀鋒視窗，顯示 IPv4 PTR 記錄：

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure8.png)

hello 下列範例顯示如何 tooview hello PTR 記錄使用 PowerShell 或 hello Azure CLI:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

[DNS 區域] 刀鋒視窗，顯示 IPv6 PTR 記錄：

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure9.png)

hello 以下是範例上 tooview hello 使用 PowerShell 和 hello AzureCLI 資料錄的方式：

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>常見問題集

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>我可以在 Azure DNS 上，為 ISP 指派的 IP 區塊託管反向 DNS 對應區域嗎？

是。 完全支援裝載您自己的 IP 範圍，在 Azure DNS 中的 hello (ARPA) 的反向對應區域。

在本文中，將會有說明，在 Azure DNS 中建立 hello 反向對應區域，然後使用您的 ISP 太[委派 hello 區域](dns-domain-delegation.md)。  接著，您可以管理 hello PTR 記錄 hello 中每個反向對應的相同方式其他記錄類型。

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>託管反向 DNS 對應區域的費用如何？

裝載 hello 反向 DNS 對應區域的 Azure DNS 在您的 ISP 指派的 IP 區塊收費[標準 Azure DNS 費率](https://azure.microsoft.com/pricing/details/dns/)。

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>我可以同時在 Azure DNS 中為 IPv4 和 IPv6 位址託管反向 DNS 對應區域嗎？

是。 這篇文章說明如何 toocreate IPv4 和 IPv6 反向 DNS 查閱 Azure DNS 區域。

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>可以匯入現有的反向 DNS 對應區域嗎？

是。 您可以使用 hello Azure CLI tooimport 現有 DNS 區域，將 Azure DNS。 正向對應區域和反向對應區域都適用。

如需詳細資訊，請參閱[匯入和匯出 DNS 區域檔案使用 hello Azure CLI](dns-import-export.md)。

## <a name="next-steps"></a>後續步驟

如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。
<br>
了解如何太[管理您的 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。
