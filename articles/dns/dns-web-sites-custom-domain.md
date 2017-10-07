---
title: "aaaCreate web 應用程式的自訂 DNS 記錄 |Microsoft 文件"
description: "Toocreate 自訂網域 DNS 資料錄的方式使用 Azure DNS 的 web 應用程式。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>在自訂網域中建立 Web 應用程式的 DNS 記錄

您可以使用 Azure DNS toohost 自訂網域，您的 web 應用程式。 比方說，您所建立的 Azure web 應用程式，而且您想要使用者 tooaccess 它透過使用 contoso.com 或 www.contoso.com 當做 FQDN。

toodo，您有 toocreate 兩筆記錄：

* 根"A"的記錄指標 toocontoso.com
* "CNAME"hello www 名稱指向 toohello 記錄記錄

請注意，如果您在 Azure 中建立 web 應用程式的 A 記錄，記錄必須手動更新，如果 hello hello hello web 應用程式變更為基礎的 IP 位址。

## <a name="before-you-begin"></a>開始之前

在開始之前，必須首先 Azure DNS 中建立 DNS 區域，並在您的註冊機構 tooAzure DNS 委派 hello 區域。

1. toocreate DNS 區域，請依照下列中的 hello 步驟[建立 DNS 區域](dns-getstarted-create-dnszone.md)。
2. toodelegate 您 DNS tooAzure DNS，請依照下列中的 hello 步驟[DNS 網域委派](dns-domain-delegation.md)。

之後建立區域委派它 tooAzure DNS，然後您可以建立記錄的自訂網域。

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1.建立自訂網域的 A 記錄

A 記錄是使用的 toomap 名稱 tooits IP 位址。 Hello 下列範例中我們將會為 IPv4 位址的 A 記錄 tooan 指派:

### <a name="step-1"></a>步驟 1

建立 A 記錄，並指派 tooa 變數 $rs

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>步驟 2

新增 hello IPv4 值 toohello 先前建立的記錄組"@"使用 hello $rs 變數指派。 hello 指派的 IPv4 值將是 hello web 應用程式的 IP 位址。

toofind hello IP 位址，web 應用程式中，請依照下列中的 hello 步驟[Azure App Service 中設定自訂網域名稱](../app-service-web/app-service-web-tutorial-custom-domain.md)。

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>步驟 3

認可 hello 變更 toohello 記錄集。 使用`Set-AzureRMDnsRecordSet`tooupload hello 變更 toohello 記錄集 tooAzure DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2.建立自訂網域的 CNAME 記錄

如果您的網域已經受 Azure DNS (請參閱[DNS 網域委派](dns-domain-delegation.md)，您可以使用 hello 遵循 hello 範例 toocreate: contoso.azurewebsites.net 的 CNAME 記錄。

### <a name="step-1"></a>步驟 1

開啟 PowerShell 並建立新的 CNAME 記錄集並指派 tooa 變數 $rs。 這個範例會建立 「 時間 toolive 」 為 600 秒 DNS 區域中名為"contoso.com"的資料錄集類型 CNAME。

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

下列範例中的 hello 是 hello 回應。

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>步驟 2

Hello CNAME 記錄組建立之後，您需要 toocreate 將會為 toohello web 應用程式的別名值。

使用先前指派變數"$rs"hello 您可以使用以下 toocreate hello 別名 hello PowerShell 命令的 hello web 應用程式： contoso.azurewebsites.net。

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

下列範例中的 hello 是 hello 回應。

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>步驟 3

認可使用 hello hello 變更`Set-AzureRMDnsRecordSet`cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

您可以驗證 hello 記錄已正確建立藉由查詢 hello"www.contoso.com"使用 nslookup，如下所示：

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>建立 Web Apps 的 awverify 記錄

如果您決定 toouse A 記錄 web 應用程式時，您必須通過驗證程序 tooensure 您自己的 hello 自訂網域。 此驗證步驟可透過建立名為 "awverify" 的特殊 CNAME 記錄來完成。 本節適用於僅 tooA 記錄。

### <a name="step-1"></a>步驟 1

建立 hello"awverify 」 記錄。 在 [hello 下列範例中，我們將建立 hello 自訂網域為 contoso.com tooverify 擁有權的 hello"aweverify 」 記錄。

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

下列範例中的 hello 是 hello 回應。

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>步驟 2

一旦建立資料錄集 」 awverify"hello，指派別名設定 hello CNAME 記錄。 在 [hello 下列範例中，我們將會指派 hello CNAMe 記錄集別名 tooawverify.contoso.azurewebsites.net。

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

下列範例中的 hello 是 hello 回應。

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>步驟 3

認可使用 hello hello 變更`Set-AzureRMDnsRecordSet cmdlet`下方的 hello 命令所示。

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>後續步驟

中的 hello 步驟[設定應用程式服務的自訂網域名稱](../app-service-web/web-sites-custom-domain-name.md)tooconfigure 您 web 應用程式 toouse 自訂網域。
