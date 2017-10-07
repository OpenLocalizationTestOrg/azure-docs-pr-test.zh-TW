---
title: "aaaManage DNS 區域中 Azure DNS-Azure CLI 2.0 |Microsoft 文件"
description: "您可以使用 Azure CLI 2.0 管理 DNS 區域。 本文將說明如何 tooupdate、 刪除及 Azure DNS 上建立 DNS 區域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>如何使用 Azure DNS toomanage DNS 區域 hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [入口網站](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


本指南也說明如何 toomanage 您的 DNS 區域使用 hello 跨平台 Azure CLI，這是適用於 Windows、 Mac 和 Linux。 您也可以管理您使用的 DNS 區域[Azure PowerShell](dns-operations-dnszones.md)或 hello Azure 入口網站。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。

## <a name="introduction"></a>簡介

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>設定適用於 Azure DNS 的 Azure CLI 2.0

### <a name="before-you-begin"></a>開始之前

確認您擁有 hello 開始您的組態之前，下列項目。

* Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。

* 安裝 hello hello Azure CLI 2.0，可供 Windows、 Linux 或 MAC 最新版本 詳細的資訊將會位於[安裝 hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。

### <a name="sign-in-tooyour-azure-account"></a>Azure 帳戶登入 tooyour

開啟主控台視窗，並驗證您的認證。 如需詳細資訊，請參閱記錄檔中的 hello Azure CLI tooAzure

```
az login
```

### <a name="select-hello-subscription"></a>選取 hello 訂用帳戶

請檢查 hello hello 帳戶的訂用帳戶。

```
az account list
```

選擇 Azure 訂用帳戶 toouse。

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>建立資源群組

Azure Resource Manager 需要所有的資源群組指定一個位置。 這當做 hello 預設位置，該資源群組中的資源。 不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。

如果您使用現有的資源群組，則可略過此步驟。

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>取得說明

所有相關 tooAzure DNS 的 CLI 2.0 命令開頭`az network dns`。 說明適用於每個命令使用 hello`--help`選項 (簡短形式`-h`)。  例如：

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>建立 DNS 區域

DNS 區域建立使用 hello`az network dns zone create`命令。 如需協助，請參閱 `az network dns zone create -h`。

hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate DNS 區域與標籤

hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*，使用 hello `--tags`參數 (簡短形式`-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>取得 DNS 區域

tooretrieve DNS 區域，使用`az network dns zone show`。 如需協助，請參閱 `az network dns zone show --help`。

hello 下列範例會傳回 hello DNS 區域*contoso.com*及其相關聯的資料，從資源群組*MyResourceGroup*。 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

下列範例中的 hello 是 hello 回應。

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

請注意，`az network dns zone show` 不會傳回 DNS 記錄。 toolist DNS 記錄，使用`az network dns record-set list`。


## <a name="list-dns-zones"></a>列出 DNS 區域

tooenumerate DNS 區域，使用`az network dns zone list`。 如需協助，請參閱 `az network dns zone list --help`。

指定 hello 資源群組會列出這些區域 hello 的資源群組中：

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

省略 hello 資源群組列出 hello 訂用帳戶中的所有區域：

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>更新 DNS 區域

DNS 區域資源可以使用進行的變更 tooa `az network dns zone update`。 如需協助，請參閱 `az network dns zone update --help`。

此命令不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets-cli.md))。 它是只使用的 tooupdate 屬性 hello 區域資源本身。 這些屬性是目前限制的 toohello [Azure 資源管理員 '標記'](dns-zones-records.md#tags) hello 區域資源。

hello 下列範例顯示如何 tooupdate hello 標記上的 DNS 區域。 所指定的 hello 值取代 hello 現有的標記。

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>刪除 DNS 區域

可以使用 `az network dns zone delete`刪除 DNS 區域。 如需協助，請參閱 `az network dns zone delete --help`。

> [!NOTE]
> 刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。 此作業無法復原。 如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。
>
>tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。

此命令會提示您確認。 選擇性的 hello`--yes`參數會抑制此提示。

hello 下列範例示範如何 toodelete hello 區域*contoso.com*從資源群組*MyResourceGroup*。

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>後續步驟

了解如何太[管理資料錄集 」 和 「 記錄](dns-getstarted-create-recordset-cli.md)DNS 區域中。

了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。

