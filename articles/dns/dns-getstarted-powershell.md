---
title: "開始使用 PowerShell 的 Azure DNS aaaGet |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域，使用 PowerShell 的記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>利用 PowerShell 開始使用 Azure DNS

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

本文將指導您完成 hello 步驟 toocreate 您的第一個 DNS 區域和使用 Azure PowerShell 的記錄。 您也可以使用 hello Azure 入口網站執行這些步驟，或 hello 跨平台 Azure CLI。

DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。 toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。 接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。 最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。 以下說明上述各步驟。

這些指示假設您已經安裝並登入 tooAzure PowerShell。 如需說明，請參閱[toomanage DNS 區域使用 PowerShell](dns-operations-dnszones.md)。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

建立 hello DNS 區域之前, 建立 toocontain hello DNS 區域資源群組。 hello 下列範例示範 hello 命令。

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>建立 DNS 區域

DNS 區域由使用 hello `New-AzureRmDnsZone` cmdlet。 hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*。 使用 hello 範例 toocreate DNS 區域時，取代為您自己的 hello 值。

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>建立 DNS 記錄

您可以建立資料錄集使用 hello `New-AzureRmDnsRecordSet` cmdlet。 hello 下列範例會建立一筆記錄 hello 相對名稱"www"hello"contoso.com"，"MyResourceGroup"的資源群組中的 DNS 區域中。 hello hello 資料錄集的完整名稱是"www.contoso.com"。 hello 記錄類型為"A"，使用 IP 位址"1.2.3.4"，而且 hello TTL 為 3600 秒。

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

對於其他記錄類型，如記錄設定具有一個以上的記錄，以及 toomodify 現有的記錄，請參閱[管理 DNS 記錄和資料錄集，使用 Azure PowerShell](dns-operations-recordsets.md)。 


## <a name="view-records"></a>檢視記錄

toolist hello DNS 記錄，在您的區域，使用：

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>更新名稱伺服器

您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。 這可讓其他使用者 hello 網際網路 toofind DNS 記錄。

hello 名稱伺服器，您的區域會提供 hello `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。 您的註冊機構會提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。 如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。

## <a name="delete-all-resources"></a>刪除所有資源

toodelete 本文採用 hello 下列步驟中建立的所有資源：

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。

進一步了解管理 Azure DNS 的 DNS 區域 toolearn 看到[Azure DNS 使用 PowerShell 管理 DNS 區域](dns-operations-dnszones.md)。

進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄和記錄設定中使用 PowerShell 的 Azure DNS](dns-operations-recordsets.md)。

