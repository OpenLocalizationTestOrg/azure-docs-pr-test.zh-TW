---
title: "aaaManage DNS 記錄，使用 Azure DNS hello Azure CLI 1.0 |Microsoft 文件"
description: "將網域裝載於 Azure DNS 時，在 Azure DNS 管理 DNS 記錄集和記錄。 對記錄集和記錄執行作業的所有 CLI 1.0 命令。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>管理 Azure DNS 使用 hello Azure CLI 1.0 中的 DNS 記錄

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

本文章將示範如何使用您的 DNS 區域的 toomanage DNS 記錄 hello 跨平台 Azure 的命令列介面 (CLI) (也就是適用於 Windows、 Mac 和 Linux。 您也可以管理您使用的 DNS 記錄[Azure PowerShell](dns-operations-recordsets.md)或 hello [Azure 入口網站](dns-operations-recordsets-portal.md)。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。

本文章中的 hello 範例假設您已經有[安裝 hello Azure CLI 1.0，登入，並建立 DNS 區域](dns-operations-dnszones-cli-nodejs.md)。

## <a name="introduction"></a>簡介

Azure DNS 中建立 DNS 記錄之前, 您必須先 toounderstand Azure DNS 到 DNS 資料錄集所組織的 DNS 記錄。

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。

## <a name="create-a-dns-record"></a>建立 DNS 記錄

toocreate DNS 記錄，使用 hello`azure network dns record-set add-record`命令。 如需協助，請參閱 `azure network dns record-set add-record -h`。

當建立記錄，您需要 toospecify hello 資源群組名稱、 區域名稱，記錄集名稱、 hello 記錄類型和正在建立 hello 記錄 hello 詳細資訊。 hello 指定的記錄集名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。

如果 hello 記錄集不存在，此命令建立它。 如果 hello 記錄集已經存在，則此命令稱之為 hello 指定 toohello 現有資料錄集的記錄。

如果建立新的記錄集，則會使用預設存留時間 (TTL) 3600。 如需有關如何 toouse 不同 TTLs，請參閱指示[建立 DNS 記錄集](#create-a-dns-record-set)。

hello 下列範例會建立稱為 「 A 記錄*www* hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*。 hello IP 位址記錄是的 hello *1.2.3.4*。

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate hello 區域的 hello 區域的 apex 中的記錄 (在此情況下，"contoso.com")，使用 hello 記錄名稱"@"，其中包括 hello 引號：

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>建立 DNS 記錄集

Hello DNS 記錄的現有資料錄集，請加入的 tooan 在上述範例 hello，或是建立 hello 記錄集*隱含*。 您也可以建立 hello 記錄集*明確*加入記錄 tooit 之前。 Azure DNS 支援 'empty' 的資料錄集，可做為預留位置 tooreserve DNS 名稱建立 DNS 記錄之前。 空的資料錄集會顯示在 hello Azure DNS 控制平面，但不是會出現在 hello Azure DNS 名稱伺服器。

資料錄集建立使用 hello`azure network dns record-set create`命令。 如需協助，請參閱 `azure network dns record-set create -h`。

建立明確設定的 hello 記錄可讓您 toospecify 記錄集屬性，例如 hello[存留時間 (TTL)](dns-zones-records.md#time-to-live)和中繼資料。 [設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。

hello 下列範例會建立空的記錄設定以 60 秒的 TTL，使用 hello`--ttl`參數 (簡短形式`-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

hello 下列範例會建立之記錄集的兩個中繼資料的項目，"dept = finance"和"環境 = 實際執行 」，利用 hello`--metadata`參數 (簡短形式`-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

建立好空白記錄集之後，可依[建立 DNS 記錄](#create-a-dns-record)所述使用 `azure network dns record-set add-record` 新增記錄。

## <a name="create-records-of-other-types"></a>建立其他類型的記錄

有看到詳細 toocreate 'A' 記錄的方式，下列範例會顯示 toocreate 記錄的其他記錄類型如何支援 Azure dns hello。

hello 參數使用 toospecify hello 記錄資料的 hello 記錄 hello 類型而有所不同。 例如，型別"A"的記錄，您指定 hello IPv4 位址搭配 hello 參數`-a <IPv4 address>`。 hello 參數，可以使用列出每個記錄類型為`azure network dns record-set add-record -h`。

在各案例中，我們會示範如何 toocreate 單一記錄。 hello 記錄加入的 toohello 現有資料錄集，或隱含建立的記錄組。 如需明確建立記錄集和定義記錄集參數的詳細資訊，請參閱[建立 DNS 記錄集](#create-a-dns-record-set)。

我們不會提供範例 toocreate SOA 記錄集，因為 SOAs 會建立和刪除與每個 DNS 區域和無法建立或刪除個別。 不過， [SOA 可以修改，在稍後的範例所示的 hello](#to-modify-an-SOA-record)。

### <a name="create-an-aaaa-record"></a>建立 AAAA 記錄

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>建立 CNAME 記錄

> [!NOTE]
> hello DNS 標準不允許在 hello 區域的區域的 apex CNAME 記錄 (`-Name "@"`)，也請勿允許包含多個記錄的資料錄集。
> 
> 如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>建立 MX 記錄

在此範例中，我們使用 hello 記錄集名稱"@"toocreate hello 在 hello 區域的 apex MX 記錄 (在此情況下，"contoso.com")。

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>建立 NS 記錄

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>建立 PTR 記錄

在此情況下，' 我-arpa-zone.com' 代表 hello ARPA 區域代表您的 IP 範圍。 在此區域中設定每個 PTR 記錄對應 tooan 此 IP 範圍內的 IP 位址。  hello 記錄名稱 '10' 是 hello hello IP 位址，由這個記錄此 IP 範圍內的最後一個八位元。

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>建立 SRV 記錄

建立時[SRV 記錄集](dns-zones-records.md#srv-records)，指定 hello *\_服務*和*\_通訊協定*hello 中記錄集名稱。 沒有任何需要 tooinclude"@"hello 記錄集中名稱建立一筆 SRV 記錄於 hello 區域的 apex 設定。

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>建立 TXT 記錄

hello 下列範例顯示如何 toocreate TXT 記錄。 如需支援 TXT 記錄中的 hello 最大字串長度的詳細資訊，請參閱[TXT 記錄](dns-zones-records.md#txt-records)。

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>取得記錄集

使用現有的資料錄集，tooretrieve `azure network dns record-set show`。 如需協助，請參閱 `azure network dns record-set show -h`。

Hello 記錄建立的記錄或資料錄集時，設定指定的名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。 您也需要 toospecify hello 記錄類型，包含 hello 記錄 hello 區域設定，並 hello 含有 hello 區域的資源群組。

hello 下列範例會擷取 hello 記錄*www*從區域類型的*contoso.com*資源群組中*MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>列出記錄集

您可以使用 hello 列出 DNS 區域中的所有記錄`azure network dns record-set list`命令。 如需協助，請參閱 `azure network dns record-set list -h`。

這個範例會傳回所有資料錄集，在 hello 區域*contoso.com*，資源群組中*MyResourceGroup*，不論名稱或記錄類型：

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

這個範例會傳回所有符合 hello 指定記錄類型 （在此情況下，'A' 記錄） 的資料錄集：

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>新增記錄 tooan，現有的資料錄集

您可以使用`azure network dns record-set add-record`同時 toocreate 新記錄中的記錄設定，或 tooadd 記錄 tooan 現有的記錄設定。

如需詳細資訊，請參閱上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)。

## <a name="remove-a-record-from-an-existing-record-set"></a>從現有的記錄集移除記錄。

tooremove DNS 記錄，從現有的資料錄集，使用`azure network dns record-set delete-record`。 如需協助，請參閱 `azure network dns record-set delete-record -h`。

此命令會刪除記錄集內的 DNS 記錄。 如果刪除資料錄集 hello 最後一筆記錄時，會將本身設 hello 記錄是**不**刪除。 反而會留下空白記錄集。 toodelete hello 記錄集相反地，請參閱[刪除記錄集](#delete-a-record-set)。

您需要 toospecify hello 記錄 toobe 刪除和 hello 區域應予以刪除，從使用 hello 相同參數做為建立記錄使用時`azure network dns record-set add-record`。 這些參數在上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)中有所說明。

此命令會提示您確認。 此提示可使用，以歸併 hello`--quiet`切換 (簡短形式`-q`)。

下列範例刪除 hello hello 的記錄中包含值 '1.2.3.4' hello 記錄從名為*www* hello 區域*contoso.com*，hello 資源群組中*MyResourceGroup*. 隱藏 hello 確認提示。

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>修改現有記錄集

每個記錄集都包含[存留時間 (TTL)](dns-zones-records.md#time-to-live)、[中繼資料](dns-zones-records.md#tags-and-metadata)和 DNS 記錄。 hello 下列各節說明如何 toomodify 每個這些屬性。

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄

toomodify 現有類型 A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄，您應該先新增新的記錄，然後刪除 hello 現有記錄。 如需有關的詳細指示 toodelete 和新增記錄，請參閱 hello 的本文稍早章節。

下列範例中的 hello 顯示 toomodify 'A' 記錄，從 IP 位址 1.2.3.4 tooIP 定址 5.6.7.8 的方式：

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify CNAME 記錄

toomodify CNAME 記錄，使用`azure network dns record-set add-record`tooadd hello 新記錄的值。 不同於其他記錄類型，CNAME 記錄集只能包含單一記錄。 因此，hello 現有的記錄是*取代*當 hello 新記錄會加入，但不需要另外刪除 toobe。  您將會提示的 tooaccept 這項取代。

hello 範例會修改 hello CNAME 記錄集*www* hello 區域*contoso.com*，資源群組中*MyResourceGroup*，toopoint 太 'www.fabrikam.net' 而不是其現有的值：

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify SOA 記錄

使用`azure network dns record-set set-soa-record`toomodify hello SOA 給定的 DNS 區域。 如需協助，請參閱 `azure network dns record-set set-soa-record -h`。

hello 下列範例示範如何 tooset hello 'email' 屬性的 hello SOA 記錄 hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>在 hello 區域的 apex toomodify NS 記錄

在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。 它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。

您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。 您也可以修改 hello TTL 和此記錄集的中繼資料。 不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。

請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。 如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。

hello 下列範例顯示如何 tooadd 其他的名稱伺服器 toohello NS 記錄設定在 hello 區域的 apex:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>toomodify hello TTL 為現有的記錄設定

toomodify hello TTL 現有記錄的設定，請使用`azure network dns record-set set`。 如需協助，請參閱 `azure network dns record-set set -h`。

hello 下列範例顯示如何 toomodify 記錄集 TTL，在此情況下 too60 秒：

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify hello 中繼資料的現有資料錄集

[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。 toomodify hello 中繼資料的現有記錄的設定，請使用`azure network dns record-set set`。 如需協助，請參閱 `azure network dns record-set set -h`。

hello 下列範例示範如何 toomodify 記錄設定兩個中繼資料的項目，"dept = finance"和"環境 = 實際執行 」，利用 hello`--metadata`參數 (簡短形式`-m`)。 請注意，任何現有的中繼資料是*取代*所指定的 hello 值。

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>刪除記錄集

使用 hello 也可以刪除資料錄集`azure network dns record-set delete`命令。 如需協助，請參閱 `azure network dns record-set delete -h`。 刪除資料錄集時，也會刪除 hello 資料錄集內的所有記錄。

> [!NOTE]
> 您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (`-Name "@"`)。  當 hello 區域建立，而且已刪除 hello 區域時自動刪除，這些會自動建立。

hello 下列範例會刪除名為 hello 記錄*www*從 hello 區域類型的*contoso.com*資源群組中*MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

您已提示的 tooconfirm hello 刪除作業。 此提示，toosuppress 使用 hello`--quiet`切換 (簡短形式`-q`)。

## <a name="next-steps"></a>後續步驟

深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。
<br>
了解如何太[保護您的區域和記錄](dns-protect-zones-recordsets.md)時使用 Azure DNS。
