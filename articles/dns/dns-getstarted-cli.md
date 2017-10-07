---
title: "aaaGet 開始使用 Azure DNS 使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域和使用 Azure CLI 2.0 hello 記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>利用 Azure CLI 2.0 開始使用 Azure DNS

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

本文將引導您完成 hello 步驟 toocreate 第一次的 DNS 區域，並使用記錄 hello 跨平台 Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。 您也可以執行這些步驟使用 hello Azure 入口網站或 Azure PowerShell。

DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。 toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。 接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。 最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。 以下說明上述各步驟。

這些指示假設您已經安裝並登入 tooAzure CLI 2.0。 如需說明，請參閱[toomanage DNS 區域使用 Azure CLI 2.0](dns-operations-dnszones-cli.md)。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

建立 hello DNS 區域之前, 建立 toocontain hello DNS 區域資源群組。 hello 下列範例示範 hello 命令。

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>建立 DNS 區域

DNS 區域建立使用 hello`az network dns zone create`命令。 此命令，toosee 說明輸入`az network dns zone create -h`。

hello 下列範例會建立 DNS 區域呼叫*contoso.com* hello 資源群組中*MyResourceGroup*。 使用 hello 範例 toocreate DNS 區域時，取代為您自己的 hello 值。

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>建立 DNS 記錄

toocreate DNS 記錄，使用 hello`az network dns record-set [record type] add-record`命令。 如需說明，例如 A 記錄，請參閱 `azure network dns record-set A add-record -h`。

hello 下列範例會建立一筆記錄 hello 相對名稱"www"hello"contoso.com"，"MyResourceGroup"的資源群組中的 DNS 區域中。 hello hello 資料錄集的完整名稱是"www.contoso.com"。 hello 記錄類型是"A"，使用"1.2.3.4"的 IP 位址，則會使用預設的 TTL 為 3600 秒 （1 小時）。

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

對於其他記錄類型，如記錄設定具有一個以上的記錄，替代的 TTL 值和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure CLI 2.0](dns-operations-recordsets-cli.md)。


## <a name="view-records"></a>檢視記錄

toolist hello DNS 記錄，在您的區域，使用：

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>更新名稱伺服器

您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。 這可讓其他使用者 hello 網際網路 toofind DNS 記錄。

hello 名稱伺服器，您的區域會提供 hello`az network dns zone show`命令。 toosee hello 名稱伺服器名稱，會使用 JSON 輸出，hello 下列範例所示。

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。 您的註冊機構會提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。 如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。

## <a name="delete-all-resources"></a>刪除所有資源
 
toodelete 本文採用 hello 下列步驟中建立的所有資源：

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。

進一步了解管理 Azure DNS 的 DNS 區域 toolearn 看到[管理 DNS 區域中使用 Azure CLI 2.0 Azure DNS](dns-operations-dnszones-cli.md)。

進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄和記錄設定中使用 Azure CLI 2.0 Azure DNS](dns-operations-recordsets-cli.md)。
