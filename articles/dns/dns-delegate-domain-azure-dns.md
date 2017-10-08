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
# <a name="delegate-a-domain-tooazure-dns"></a>委派網域 tooAzure DNS

Azure DNS 可讓您 toohost DNS 區域，並管理網域，以在 Azure 中的 hello DNS 記錄。 為了讓網域 tooreach Azure DNS 的 DNS 查詢，hello 網域有 toobe 從 hello 父系網域委派 tooAzure DNS。 請記住 Azure DNS 不 hello 網域註冊機構。 這篇文章說明如何 toodelegate 您網域 tooAzure DNS。

網域註冊機構購買，您的註冊機構提供 hello 選項 tooset 這些 NS 記錄。 您沒有 tooown 網域 toocreate DNS 區域與該網域名稱在 Azure DNS。 不過，您需要 tooown hello 網域 tooset 向上 hello 委派 tooAzure DNS 與 hello 註冊機構。

例如，假設您購買 hello 網域 'contoso.net'，Azure DNS 中建立 hello 名稱 'contoso.net' 與區域。 做為 hello 網域 hello 擁有者，您的註冊機構會提供您的網域 hello 選項 tooconfigure hello 名稱伺服器位址 （也就是 hello NS 記錄）。 hello 註冊機構儲存在此情況下 '.net' hello 父系網域中的這些 NS 記錄。 Hello 世界各地的用戶端接著可以導向的 tooyour Azure DNS 區域中的網域時，嘗試在 'contoso.net' tooresolve DNS 記錄。

## <a name="create-a-dns-zone"></a>建立 DNS 區域

1. 登入 toohello Azure 入口網站
1. 在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. 在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:

   | **設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|contoso.net|hello hello DNS 區域名稱|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello 應用程式閘道中。|
   |**資源群組**|**建立新的︰**contosoRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

> [!NOTE]
> hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 「 全域 」，而且不會顯示。

## <a name="retrieve-name-servers"></a>擷取名稱伺服器

您可以將您的 DNS 區域 tooAzure DNS 委派之前，您必須先 tooknow hello 名稱區域的伺服器名稱。 每次建立區域時，Azure DNS 都會配置某個集區中的名稱伺服器。

1. Hello，hello Azure 入口網站中建立的 DNS 區域與**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **contoso.net** hello 中的 DNS 區域**所有資源**刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contoso.net**中依名稱 hello 篩選... 方塊 tooeasily 存取 hello 應用程式閘道。 

1. 擷取 hello DNS 區域刀鋒視窗中的 hello 名稱伺服器。 在此範例中，hello 區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'，'ns2 01.azure dns.net'、' ns3-01.azure-dns.org'，和 ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS 會自動建立您的區域，包含 hello 指派名稱伺服器中的權威 NS 記錄。  透過 Azure PowerShell 或 Azure CLI 命名 toosee hello 名稱伺服器，您只需要 tooretrieve 這些記錄。

hello 下列範例也提供 hello 步驟 tooretrieve hello 名稱伺服器中使用 PowerShell 和 Azure CLI Azure DNS 區域。

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

下列範例中的 hello 是 hello 回應。

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

### <a name="azure-cli"></a>Azure CLI

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

下列範例中的 hello 是 hello 回應。

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

## <a name="delegate-hello-domain"></a>委派 hello 網域

現在，建立 hello DNS 區域，而且您擁有 hello 名稱伺服器，需要 toobe hello Azure DNS 名稱伺服器以更新 hello 父網域。 每個註冊機構都有自己 DNS 管理工具 toochange hello 名稱伺服器記錄的網域。 在 hello 註冊機構的 DNS 管理頁面中，編輯 hello NS 記錄，以及取代的 hello 的 Azure DNS 建立 hello NS 記錄。

當委派網域 tooAzure DNS 時，您必須使用 Azure DNS 所提供的 hello 名稱伺服器名稱。 建議 toouse 所有四個名稱伺服器名稱，不論 hello 您的網域名稱。 網域委派不需要 hello 名稱伺服器名稱 toouse hello 與您的網域相同的最上層網域。

您不應該使用 '黏附記錄' toopoint toohello Azure DNS 名稱伺服器 IP 位址，因為這些 IP 位址可能會在未來變更。 Azure DNS 目前不支援使用您區域中名稱伺服器名稱的委派 (有時稱為「虛名名稱伺服器」)。

## <a name="verify-name-resolution-is-working"></a>確認名稱解析正常運作

完成之後 hello 委派，您可以確認名稱解析使用 'nslookup' tooquery hello SOA 記錄之類的工具區域 （這也會自動建立時建立 hello 區域） 正常運作。

您不需要 toospecify hello Azure DNS 名稱伺服器，如果 hello 委派已設定正確，hello 一般 DNS 解析程序會尋找 hello 名稱伺服器自動。

```
nslookup -type=SOA contoso.com
```

hello 下面是從 hello 前面命令的範例回應：

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

## <a name="delegate-sub-domains-in-azure-dns"></a>在 Azure DNS 中委派子網域

如果您想 tooset 組成個別的子區域，您可以委派子網域中 Azure DNS。 比方說，需設定和委派 'contoso.net' Azure DNS 中的假設您想要不同的子區域中，向上 tooset 'partners.contoso.net'。

1. 在 Azure DNS 中建立 hello 子區域 'partners.contoso.net'。
2. 查閱 hello 權威 NS 記錄 hello 子區域 tooobtain hello 名稱伺服器裝載在 Azure DNS 中的 hello 子區域中。
3. 藉由設定指向 toohello 子區域的 hello 上層區域中的 NS 記錄 hello 其子區域委派。

### <a name="create-a-dns-zone"></a>建立 DNS 區域

1. 登入 toohello Azure 入口網站
1. 在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。

    ![DNS 區域](./media/dns-domain-delegation/dns.png)

1. 在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:

   | **設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|partners.contoso.net|hello hello DNS 區域名稱|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello 應用程式閘道中。|
   |**資源群組**|**使用現有的︰**contosoRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

> [!NOTE]
> hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。 hello DNS 區域位置一定是 「 全域 」，而且不會顯示。

### <a name="retrieve-name-servers"></a>擷取名稱伺服器

1. Hello，hello Azure 入口網站中建立的 DNS 區域與**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **partners.contoso.net** hello 中的 DNS 區域**所有資源**刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**partners.contoso.net**中依名稱 hello 篩選... 方塊 tooeasily 存取 hello DNS 區域。

1. 擷取 hello DNS 區域刀鋒視窗中的 hello 名稱伺服器。 在此範例中，hello 區域 'contoso.net' 已被指派名稱伺服器 'ns1-01.azure-dns.com'，'ns2 01.azure dns.net'、' ns3-01.azure-dns.org'，和 ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS 會自動建立您的區域，包含 hello 指派名稱伺服器中的權威 NS 記錄。  透過 Azure PowerShell 或 Azure CLI 命名 toosee hello 名稱伺服器，您只需要 tooretrieve 這些記錄。

### <a name="create-name-server-record-in-parent-zone"></a>在父系區域中建立名稱伺服器記錄

1. 瀏覽 toohello **contoso.net** hello Azure 入口網站中的 DNS 區域。
1. 按一下 [+ 記錄集]
1. 在 hello**加入資料錄集**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:

   | **設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|合作夥伴|hello hello 子 DNS 區域名稱|
   |**類型**|NS|使用 NS 作為名稱伺服器記錄。|
   |**TTL**|1|Toolive 的時間。|
   |**TTL 單位**|小時|設定時間單位 toolive toohours|
   |**名稱伺服器**|{partners.contoso.net 區域中的名稱伺服器}|從 partners.contoso.net 區域輸入所有 4 hello 名稱伺服器。 |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>使用其他工具在 Azure DNS 中委派子網域

hello 下列範例提供 hello 步驟 toodelegate 子網域中使用 PowerShell 和 CLI Azure DNS:

#### <a name="powershell"></a>PowerShell

hello 下列 PowerShell 範例會示範其運作方式。 可以透過 hello Azure 入口網站執行相同的步驟，或透過 hello 跨平台 Azure CLI hello。

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

使用`nslookup`tooverify 的所有項目已正確設定時查閱 hello hello 子區域的 SOA 記錄。

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

#### <a name="azure-cli"></a>Azure CLI

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

擷取 hello 名稱伺服器 hello `partners.contoso.net` hello 輸出中的區域。

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

建立 hello 資料錄集和每個名稱伺服器 NS 記錄。

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

## <a name="delete-all-resources"></a>刪除所有資源

在本文中完成下列步驟的 hello 建立 toodelete 所有資源：

1. 在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。 按一下 hello **contosorg** hello 資源刀鋒視窗中所有資源都群組。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contosorg**在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello 資源群組。
1. 在 [hello **contosorg**刀鋒視窗中，按一下 hello**刪除**] 按鈕。
1. hello 入口網站需要您想要 toodelete hello 資源群組 tooconfirm tootype hello 名稱它。 型別*contosorg* hello 資源群組名稱，然後按一下**刪除**。 刪除資源群組會刪除 hello 資源群組中的所有資源，所以一定會確定 tooconfirm hello 內容的資源群組然後再刪除。 hello 入口網站刪除 hello 的資源群組中包含的所有資源，然後都刪除本身 hello 資源群組。 這個程序需要幾分鐘的時間。

## <a name="next-steps"></a>後續步驟

[管理 DNS 區域](dns-operations-dnszones.md)

[管理 DNS 記錄](dns-operations-recordsets.md)
