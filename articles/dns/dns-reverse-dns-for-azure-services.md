---
title: "Azure 服務的 DNS aaaReverse |Microsoft 文件"
description: "了解如何 tooconfigure 反向 DNS 查閱，在 Azure 中裝載的服務"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>設定 Azure 託管服務的反向 DNS

本文說明如何 tooconfigure 反向 DNS 查閱，在 Azure 中裝載的服務。

Azure 中的服務會使用由 Azure 指派並由 Microsoft 所擁有的 IP 位址。 必須在 hello 對應 Microsoft 屬反向 DNS 查閱區域中建立這些反向 DNS 記錄 （PTR 記錄）。 這篇文章說明如何 toodo 這。

此案例不應混淆 hello 能力太[裝載 hello 反向 DNS 查閱區域用於您指派的 IP 範圍中 Azure DNS](dns-reverse-dns-hosting.md)。 在此情況下，由 hello 反向對應區域的 hello IP 範圍必須指派 tooyour 組織通常由您的 ISP。

在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。

Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。
* 在 hello Resource Manager 部署模型，計算資源 （例如虛擬機器、 虛擬機器擴展集或 Service Fabric 叢集） 會公開透過 PublicIpAddress 資源。 使用 hello PublicIpAddress hello 'ReverseFqdn' 屬性所設定反向 DNS 查閱。
* 在 hello 傳統部署模型中，計算資源會公開使用雲端服務。 使用雲端服務的 hello hello 'ReverseDnsFqdn' 屬性所設定反向 DNS 查閱。

Hello Azure 應用程式服務目前不支援反向 DNS。

## <a name="validation-of-reverse-dns-records"></a>反向 DNS 記錄的驗證

第三方不應該能 toocreate Azure 服務對應 tooyour DNS 網域的反向 DNS 記錄。 tooprevent，但 Azure 只允許反向 DNS 記錄，其中 hello 反向 DNS 記錄中指定的網域名稱是 hello 相同，或解析，hello DNS 名稱或 IP 位址的 PublicIpAddress 或雲端服務中 hello 相同的 hello 建立 Azure 訂用帳戶。

設定或修改 hello 反向 DNS 記錄時，才會執行這項驗證。 不會執行定期的重新驗證。

例如： 假設 hello PublicIpAddress 資源 hello DNS 名稱 contosoapp1.northus.cloudapp.azure.com 和 23.96.52.53 的 IP 位址。 hello ReverseFqdn hello PublicIpAddress 可以指定為：
* hello PublicIpAddress hello DNS 名稱、 contosoapp1.northus.cloudapp.azure.com
* hello DNS 名稱會在 hello 不同 PublicIpAddress 相同訂用帳戶，例如 contosoapp2.westus.cloudapp.azure.com
* 虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是*第一個*設定為 CNAME toocontosoapp1.northus.cloudapp.azure.com 或 tooa 不同 PublicIpAddress hello 中相同的訂用帳戶。
* 虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是*第一個*設定 A 記錄 toohello IP 位址 23.96.52.53 或不同的 PublicIpAddress toohello IP 位址在 hello 相同訂用帳戶。

hello 相同的條件約束套用至 tooreverse DNS 雲端服務。


## <a name="reverse-dns-for-publicipaddress-resources"></a>PublicIpAddress 資源的反向 DNS

本節提供如何 tooconfigure 反向 DNS 中 hello Resource Manager 部署模型，使用 Azure PowerShell、 Azure CLI 1.0 或 Azure CLI 2.0 的 PublicIpAddress 資源的詳細的指示。 設定反向 DNS PublicIpAddress 資源的目前不支援透過 hello Azure 入口網站。

Azure 目前只支援 IPv4 PublicIpAddress 資源的反向 DNS。 其不支援 IPv6。

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>加入現有的 PublicIpAddresses 反向 DNS tooan

#### <a name="powershell"></a>PowerShell

tooadd 反向 DNS tooan 現有 PublicIpAddress:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

tooadd 反向 DNS tooan 現有 PublicIpAddress:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

tooadd 反向 DNS tooan 現有 PublicIpAddress:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>建立具有反向 DNS 的公用 IP 位址

新 toocreate PublicIpAddress hello 與反向 DNS 屬性已指定：

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>檢視現有 PublicIpAddresses 的反向 DNS

tooview hello 針對現有的 PublicIpAddress 設定值：

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>移除現有公用 IP 位址的反向 DNS

tooremove 從現有的 PublicIpAddress 反向 DNS 屬性：

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>設定雲端服務的反向 DNS

本節提供如何 tooconfigure 反向 DNS 雲端服務在 hello 傳統部署模型中，使用 Azure PowerShell 的詳細的指示。 不支援透過 hello Azure 入口網站，Azure CLI 1.0 或 Azure CLI 2.0 設定雲端服務的反向 DNS。

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>新增反向 DNS tooexisting 雲端服務

tooadd 反向 DNS 記錄 tooan 現有雲端服務：

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>建立具有反向 DNS 的雲端服務

toocreate hello 已經指定反向 DNS 內容與新的雲端服務：

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>檢視現有雲端服務的反向 DNS

tooview hello 反向 DNS 屬性為現有的雲端服務：

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>移除現有雲端服務的反向 DNS

tooremove 反向 DNS 屬性從現有的雲端服務：

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>常見問題集

### <a name="how-much-do-reverse-dns-records-cost"></a>反向 DNS 記錄的成本為何？

完全免費！  反向 DNS 記錄或查詢不需要額外成本。

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>將從我反向 DNS 記錄解析 hello 網際網路嗎？

是。 一旦您設定 hello 反向 DNS 屬性為您的 Azure 服務，Azure 會管理所有 hello DNS 委派和反向 DNS 記錄的 tooensure 解析所有的網際網路使用者所需的 DNS 區域。

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>我的 Azure 服務有沒有建立預設的反向 DNS 記錄？

否。 反向 DNS 是選用的功能。 沒有預設值，如果您選擇不 tooconfigure 建立反向 DNS 記錄它們。

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>什麼是 hello hello 完整網域名稱 (FQDN) 格式？

FQDN 是以正向順序指定，且必須以點結束 (例如，"app1.contoso.com")。

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>發生什麼事如果 hello 的 hello 驗證檢查反向的 DNS 我指定失敗？

其中 hello 反向 DNS 驗證檢查失敗，就會失敗 hello 作業 tooconfigure hello 反向 DNS 記錄。 更正 hello 反向 DNS 值為必要項目，然後重試。

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Azure App Service 可以設定反向 DNS 嗎？

否。 Hello Azure 應用程式服務不支援反向 DNS。

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Azure 服務可以設定多個反向 DNS 記錄嗎？

否。 Azure 雲端服務或 PublicIpAddress，Azure 只支援一筆反向 DNS 記錄。

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>IPv6 PublicIpAddress 資源可以設定反向 DNS嗎？

否。 Azure 目前只支援 IPv4 PublicIpAddress 資源和雲端服務的反向 DNS。

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>我可以傳送電子郵件 tooexternal 網域從我的 Azure 計算服務？

否。 [Azure 計算服務不支援傳送電子郵件 tooexternal 網域](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>後續步驟

如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。
<br>
了解如何太[主機 hello 反向對應區域，為您的 ISP 指派的 IP 範圍，在 Azure DNS](dns-reverse-dns-for-azure-services.md)。

