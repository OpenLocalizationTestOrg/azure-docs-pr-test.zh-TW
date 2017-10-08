---
title: "aaaManage DNS 記錄中使用 Azure PowerShell 的 Azure DNS |Microsoft 文件"
description: "將網域裝載於 Azure DNS 時，在 Azure DNS 管理 DNS 記錄集和記錄。 對記錄集和記錄執行作業的所有 PowerShell 命令。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>使用 Azure PowerShell 管理 Azure DNS 中的 DNS 記錄和記錄集

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

本文章將示範如何 toomanage DNS 記錄您的 DNS 區域使用 Azure PowerShell。 DNS 記錄也可以使用 hello 跨平台來管理[Azure CLI](dns-operations-recordsets-cli.md)或 hello [Azure 入口網站](dns-operations-recordsets-portal.md)。

本文章中的 hello 範例假設您已經有[安裝 Azure PowerShell，登入，並建立 DNS 區域](dns-operations-dnszones.md)。

## <a name="introduction"></a>簡介

Azure DNS 中建立 DNS 記錄之前, 您必須先 toounderstand Azure DNS 到 DNS 資料錄集所組織的 DNS 記錄。

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。


## <a name="create-a-new-dns-record"></a>建立新的 DNS 區域

如果您的新記錄 hello 相同的名稱和型別作為現有的記錄，您需要太[將它加入現有的資料錄集 toohello](#add-a-record-to-an-existing-record-set)。 如果您的新記錄有現有的記錄不同名稱和型別 tooall，您會需要 toocreate 新的記錄組。 

### <a name="create-a-records-in-a-new-record-set"></a>在新的記錄集中建立 'A' 記錄

您可以建立資料錄集使用 hello `New-AzureRmDnsRecordSet` cmdlet。 在建立資料錄集時，您需要 toospecify hello 記錄集名稱、 hello 區域、 建立 toolive (TTL)、 hello 記錄類型和 hello 記錄 toobe hello 時間。

新增記錄 tooa 資料錄集的 hello 參數 hello hello 資料錄集類型而有所不同。 例如，當使用類型為 'A' 的記錄集合，您需要 toospecify hello IP 位址使用 hello 參數`-IPv4Address`。 若是其他記錄類型，則使用其他變數。 請參閱[其他記錄類型範例](#additional-record-type-examples)，以了解詳細資訊。

hello 下列範例會建立之記錄集的 hello 相對名稱 'www' hello 'contoso.com' 的 DNS 區域中。 hello hello 資料錄集的完整名稱是 'www.contoso.com'。 hello 記錄類型為 'A'、 而且 hello TTL 為 3600 秒。 hello 記錄組包含單一記錄，使用 '1.2.3.4' 的 IP 位址。

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate 在 hello '' 區域的 apex 區域設定的一筆記錄 (在此情況下，'contoso.com')，使用 hello 記錄集名稱 ' @' （不含引號）：

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

如果您需要的記錄集包含多個記錄的 toocreate，先建立本機陣列並新增 hello 記錄，然後傳遞 hello 陣列太`New-AzureRmDnsRecordSet`，如下所示：

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。 hello 下列範例示範如何 toocreate 記錄設定兩個中繼資料項目，' dept = finance' 和 ' 環境 = 生產 '。

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

Azure DNS 也支援 'empty' 的資料錄集，可做為預留位置 tooreserve DNS 名稱建立 DNS 記錄之前。 空的資料錄集 hello Azure DNS 控制平面中, 會顯示，但會出現在 hello Azure DNS 名稱伺服器上。 hello 下列範例會建立空的資料錄集：

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>建立其他類型的記錄

有看到詳細 toocreate 'A' 記錄的方式，下列範例顯示如何 toocreate 記錄的其他記錄類型支援的 Azure DNS hello。

在每個案例中，我們會示範如何 toocreate 資料錄集，其中包含單一記錄。 hello 'A' 記錄先前的範例可改寫的 toocreate 資料錄集包含多個資料錄，中繼資料，與其他類型的或 toocreate 空白資料錄集。

我們不會提供範例 toocreate SOA 記錄集，因為 SOAs 會建立和刪除與每個 DNS 區域和無法建立或刪除個別。 不過， [SOA 可以修改，在稍後的範例所示的 hello](#to-modify-an-SOA-record)。

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>建立含有單一記錄的 AAAA 記錄集

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>建立含有單一記錄的 CNAME 記錄集

> [!NOTE]
> hello DNS 標準不允許在 hello 區域的區域的 apex CNAME 記錄 (`-Name '@'`)，也請勿允許包含多個記錄的資料錄集。
> 
> 如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>建立含有單一記錄的 MX 記錄集

在此範例中，我們使用 hello 記錄集名稱 ' @' hello 區域的 apex toocreate MX 記錄 (在此情況下，'contoso.com')。


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>建立含有單一記錄的 NS 記錄集

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>建立含有單一記錄的 PTR 記錄集

在此情況下，' 我-arpa-zone.com' 代表 hello ARPA 反向對應區域，表示您的 IP 範圍。 在此區域中設定每個 PTR 記錄對應 tooan 此 IP 範圍內的 IP 位址。 hello 記錄名稱 '10' 是 hello hello IP 位址，由這個記錄此 IP 範圍內的最後一個八位元。

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>建立含有單一記錄的 SRV 記錄集

建立時[SRV 記錄集](dns-zones-records.md#srv-records)，指定 hello *\_服務*和*\_通訊協定*hello 中記錄集名稱。 沒有任何需要 tooinclude ' @' 在 hello 記錄設定名稱建立一筆 SRV 記錄於 hello 區域的 apex 設定。

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>建立含有單一記錄的 TXT 記錄集

hello 下列範例顯示如何 toocreate TXT 記錄。 如需支援 TXT 記錄中的 hello 最大字串長度的詳細資訊，請參閱[TXT 記錄](dns-zones-records.md#txt-records)。

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>取得記錄集

使用現有的資料錄集，tooretrieve `Get-AzureRmDnsRecordSet`。 此 cmdlet 會傳回代表 hello 記錄 Azure DNS 中設定的本機物件。

如同`New-AzureRmDnsRecordSet`，hello 記錄集名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。 您也需要 toospecify hello 記錄類型，並包含 hello 資料錄集的 hello 區域。

hello 下列範例顯示如何 tooretrieve 記錄設定。 在此範例中，hello 區域使用指定 hello`-ZoneName`和`-ResourceGroupName`參數。

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

或者，您也可以指定使用區域物件、 使用 hello 傳遞 hello 區域`-Zone`參數。

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>列出記錄集

您也可以使用`Get-AzureRmDnsZone`toolist 記錄在區域中，設定藉由略過 hello`-Name`及/或`-RecordType`參數。

hello 下列範例會傳回所有資料錄集 hello 區域中：

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

hello 下列範例示範如何所有記錄給定類型的集合可以擷取時省略 hello 記錄集名稱指定 hello 記錄類型：

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

所有的記錄設定具有指定名稱的 tooretrieve 跨記錄類型，您需要 tooretrieve 所有資料錄集，然後篩選 hello 結果：

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

在上述範例的所有 hello，hello 區域可以指定使用 hello`-ZoneName`和`-ResourceGroupName`參數 （如所示），或藉由指定區域物件：

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>新增記錄 tooan，現有的資料錄集

tooadd 記錄 tooan 現有的記錄組，請遵循下列三個步驟的 hello:

1. 取得 hello 現有資料錄集

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. 新增 hello 新記錄 toohello 本機記錄集。 這是一種離線作業。

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. 認可 hello 變更後 toohello Azure DNS 服務。 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

使用`Set-AzureRmDnsRecordSet`*取代*hello Azure DNS （與它所包含的所有記錄） 中設定與指定的 hello 資料錄集的現有記錄。 [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。 您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。

這一系列的作業也可以是*經由管道輸出*，這表示您使用 hello 管道，而不是傳遞做為參數傳遞 hello 資料錄集物件：

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

上述的 hello 範例顯示 tooadd 'A' 記錄 tooan 現有記錄的類型為 'A' 的設定方式。 類似的作業順序是使用的 tooadd 記錄 toorecord 組的其他類型，以取代 hello`-Ipv4Address`參數`Add-AzureRmDnsRecordConfig`與其他參數 tooeach 特定記錄類型。 hello 每個記錄類型的參數是 hello 相同 hello 與`New-AzureRmDnsRecordConfig`cmdlet，如中所示[額外的記錄類型範例](#additional-record-type-examples)上方。

類型 'CNAME' 或 'SOA' 的記錄集不能包含多個記錄。 這個條件約束，就會發生來自 hello DNS 標準。 而非 Azure DNS 的限制。

## <a name="remove-a-record-from-an-existing-record-set"></a>從現有的記錄集移除記錄

hello 程序 tooremove 從資料錄集的記錄會記錄 tooan 現有類似 toohello 程序 tooadd 記錄集：

1. 取得 hello 現有資料錄集

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. 移除 hello 記錄從 hello 本機的資料錄集物件。 這是一種離線作業。 正在移除的 hello 記錄所有的參數之間必須完全符合的現有記錄。

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. 認可 hello 變更後 toohello Azure DNS 服務。 選擇性使用 hello`-Overwrite`切換 toosuppress [Etag 檢查](dns-zones-records.md#etags)並行的變更。

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

使用上述順序 tooremove hello 最後一筆記錄的記錄組從 hello 不會刪除 hello 資料錄集，而是會保留空白的資料錄集。 tooremove 記錄設定完全，請參閱[刪除記錄集](#delete-a-record-set)。

同樣地 tooadding 記錄 tooa 記錄設定，也可傳送的記錄集的作業 tooremove hello 序列：

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

支援不同的記錄類型傳遞 hello 適當的特定類型的參數太`Remove-AzureRmDnsRecordSet`。 hello 每個記錄類型的參數是 hello 相同 hello 與`New-AzureRmDnsRecordConfig`cmdlet，如中所示[額外的記錄類型範例](#additional-record-type-examples)上方。


## <a name="modify-an-existing-record-set"></a>修改現有記錄集

hello 步驟修改現有的資料錄集是從新增或移除的記錄資料錄集時所採取的類似 toohello 步驟：

1. 擷取 hello 使用設定的現有記錄`Get-AzureRmDnsRecordSet`。
2. 修改 hello 本機的資料錄集物件：
    * 新增或移除記錄
    * 變更現有記錄的 hello 參數
    * Hello 記錄變更中繼資料和 toolive 時間 (TTL) 設定
3. 認可您的變更，使用 hello `Set-AzureRmDnsRecordSet` cmdlet。 這*取代*hello Azure DNS 中設定與指定的 hello 資料錄集的現有記錄。

當使用`Set-AzureRmDnsRecordSet`， [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。 您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>tooupdate 現有記錄中的記錄設定

在此範例中，我們可以變更現有 'A' 記錄 hello IP 位址：

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify SOA 記錄

您無法加入或移除 hello 自動建立在 hello 區域的 apex 設定 SOA 記錄中的記錄 (`-Name "@"`，包括引號)。 不過，您可以修改任何 hello （除了 「 主機 」） 的 SOA 記錄中的 hello 參數，而且 hello 記錄設定的 TTL。

下列範例會示範如何 hello toochange hello*電子郵件*hello SOA 記錄的屬性：

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>在 hello 區域的 apex toomodify NS 記錄

在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。 它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。

您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。 您也可以修改 hello TTL 和此記錄集的中繼資料。 不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。

請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。 如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。

hello 下列範例顯示如何 tooadd 其他的名稱伺服器 toohello NS 記錄設定在 hello 區域的 apex:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>toomodify 記錄集的中繼資料

[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。

hello 下列範例顯示如何 toomodify hello 中繼資料的現有記錄設定：

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>刪除記錄集

使用 hello 也可以刪除資料錄集`Remove-AzureRmDnsRecordSet`cmdlet。 刪除資料錄集時，也會刪除 hello 資料錄集內的所有記錄。

> [!NOTE]
> 您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (`-Name '@'`)。  Azure DNS 時，建立這些自動 hello 區域建立，而且已刪除 hello 區域時自動刪除它們。

hello 下列範例顯示如何 toodelete 記錄設定。 在此範例中，hello 記錄集名稱、 資料錄集類型、 區域名稱和資源群組會指定每個明確。

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

或者，您可指定 hello 記錄集名稱和型別，並 hello 區域利用指定的物件：

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

做為第三個選項，以 hello 記錄集本身，都可以使用資料錄集物件來指定：

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

當您指定 hello 記錄集使用資料錄集物件，刪除 toobe [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會刪除。 您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。

也可以送 hello 資料錄集物件而不是傳遞做為參數：

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>確認提示

hello `New-AzureRmDnsRecordSet`， `Set-AzureRmDnsRecordSet`，和`Remove-AzureRmDnsRecordSet`cmdlet 都支援確認提示。

每個 cmdlet 會提示確認如果 hello `$ConfirmPreference` PowerShell 喜好設定變數的值為`Medium`或更低。 因為 hello 預設值為`$ConfirmPreference`是`High`，這些提示系統不會提供使用 hello 預設 PowerShell 設定。

您可以覆寫 hello 目前`$ConfirmPreference`設定使用 hello`-Confirm`參數。 如果您指定`-Confirm`或`-Confirm:$True`，hello cmdlet 會提示您確認再它執行。 如果您指定`-Confirm:$False`，hello cmdlet 不會提示您確認。 

如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。

## <a name="next-steps"></a>後續步驟

深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。
<br>
了解如何太[保護您的區域和記錄](dns-protect-zones-recordsets.md)時使用 Azure DNS。
<br>
檢閱 hello [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。
