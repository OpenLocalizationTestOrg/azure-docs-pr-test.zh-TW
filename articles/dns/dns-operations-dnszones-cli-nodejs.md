---
title: "aaaManage DNS 區域中 Azure DNS-Azure CLI 1.0 |Microsoft 文件"
description: "您可以使用 Azure CLI 1.0 管理 DNS 區域。 本文將說明如何 tooupdate、 刪除及 Azure DNS 上建立 DNS 區域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>如何使用 Azure DNS toomanage DNS 區域 hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [入口網站](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

本指南也說明如何 toomanage 您的 DNS 區域使用 hello 跨平台 Azure CLI 1.0，這是適用於 Windows、 Mac 和 Linux。 您也可以管理您使用的 DNS 區域[Azure PowerShell](dns-operations-dnszones.md)或 hello Azure 入口網站。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。

## <a name="introduction"></a>簡介

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>取得說明

所有相關 tooAzure DNS 的 CLI 1.0 命令開頭`azure network dns`。 說明適用於每個命令使用 hello`--help`選項 (簡短形式`-h`)。  例如：

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>建立 DNS 區域

DNS 區域建立使用 hello`azure network dns zone create`命令。 如需協助，請參閱 `azure network dns zone create -h`。

hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate DNS 區域與標籤

hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*，使用 hello `--tags`參數 (簡短形式`-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>取得 DNS 區域

tooretrieve DNS 區域，使用`azure network dns zone show`。 如需協助，請參閱 `azure network dns zone show -h`。

hello 下列範例會傳回 hello DNS 區域*contoso.com*及其相關聯的資料，從資源群組*MyResourceGroup*。 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

下列範例中的 hello 是 hello 回應。

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

請注意，`azure network dns zone show` 不會傳回 DNS 記錄。 toolist DNS 記錄，使用`azure network dns record-set list`。


## <a name="list-dns-zones"></a>列出 DNS 區域

tooenumerate DNS 區域，使用`azure network dns zone list`。 如需協助，請參閱 `azure network dns zone list -h`。

指定 hello 資源群組會列出這些區域 hello 的資源群組中：

```azurecli
azure network dns zone list MyResourceGroup
```

省略 hello 資源群組列出 hello 訂用帳戶中的所有區域：

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>更新 DNS 區域

DNS 區域資源可以使用進行的變更 tooa `azure network dns zone set`。 如需協助，請參閱 `azure network dns zone set -h`。

此命令不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets-cli-nodejs.md))。 它是只使用的 tooupdate 屬性 hello 區域資源本身。 這些屬性是目前限制的 toohello [Azure 資源管理員 '標記'](dns-zones-records.md#tags) hello 區域資源。

hello 下列範例顯示如何 tooupdate hello 標記上的 DNS 區域。 所指定的 hello 值取代 hello 現有的標記。

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>刪除 DNS 區域

可以使用 `azure network dns zone delete`刪除 DNS 區域。 如需協助，請參閱 `azure network dns zone delete -h`。

> [!NOTE]
> 刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。 此作業無法復原。 如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。
>
>tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。

此命令會提示您確認。 選擇性的 hello`--quiet`切換 (簡短形式`-q`) 會隱藏此提示。

hello 下列範例示範如何 toodelete hello 區域*contoso.com*從資源群組*MyResourceGroup*。

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>後續步驟

了解如何太[管理資料錄集 」 和 「 記錄](dns-getstarted-create-recordset-cli-nodejs.md)DNS 區域中。

了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。

