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
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="82ef1-103">在自訂網域中建立 Web 應用程式的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="82ef1-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="82ef1-104">您可以使用 Azure DNS toohost 自訂網域，您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="82ef1-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="82ef1-105">比方說，您所建立的 Azure web 應用程式，而且您想要使用者 tooaccess 它透過使用 contoso.com 或 www.contoso.com 當做 FQDN。</span><span class="sxs-lookup"><span data-stu-id="82ef1-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="82ef1-106">toodo，您有 toocreate 兩筆記錄：</span><span class="sxs-lookup"><span data-stu-id="82ef1-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="82ef1-107">根"A"的記錄指標 toocontoso.com</span><span class="sxs-lookup"><span data-stu-id="82ef1-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="82ef1-108">"CNAME"hello www 名稱指向 toohello 記錄記錄</span><span class="sxs-lookup"><span data-stu-id="82ef1-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="82ef1-109">請注意，如果您在 Azure 中建立 web 應用程式的 A 記錄，記錄必須手動更新，如果 hello hello hello web 應用程式變更為基礎的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82ef1-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="82ef1-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="82ef1-110">Before you begin</span></span>

<span data-ttu-id="82ef1-111">在開始之前，必須首先 Azure DNS 中建立 DNS 區域，並在您的註冊機構 tooAzure DNS 委派 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="82ef1-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="82ef1-112">toocreate DNS 區域，請依照下列中的 hello 步驟[建立 DNS 區域](dns-getstarted-create-dnszone.md)。</span><span class="sxs-lookup"><span data-stu-id="82ef1-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="82ef1-113">toodelegate 您 DNS tooAzure DNS，請依照下列中的 hello 步驟[DNS 網域委派](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="82ef1-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="82ef1-114">之後建立區域委派它 tooAzure DNS，然後您可以建立記錄的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="82ef1-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="82ef1-115">1.建立自訂網域的 A 記錄</span><span class="sxs-lookup"><span data-stu-id="82ef1-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="82ef1-116">A 記錄是使用的 toomap 名稱 tooits IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82ef1-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="82ef1-117">Hello 下列範例中我們將會為 IPv4 位址的 A 記錄 tooan 指派:</span><span class="sxs-lookup"><span data-stu-id="82ef1-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="82ef1-118">步驟 1</span><span class="sxs-lookup"><span data-stu-id="82ef1-118">Step 1</span></span>

<span data-ttu-id="82ef1-119">建立 A 記錄，並指派 tooa 變數 $rs</span><span class="sxs-lookup"><span data-stu-id="82ef1-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="82ef1-120">步驟 2</span><span class="sxs-lookup"><span data-stu-id="82ef1-120">Step 2</span></span>

<span data-ttu-id="82ef1-121">新增 hello IPv4 值 toohello 先前建立的記錄組"@"使用 hello $rs 變數指派。</span><span class="sxs-lookup"><span data-stu-id="82ef1-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="82ef1-122">hello 指派的 IPv4 值將是 hello web 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82ef1-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="82ef1-123">toofind hello IP 位址，web 應用程式中，請依照下列中的 hello 步驟[Azure App Service 中設定自訂網域名稱](../app-service-web/app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="82ef1-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="82ef1-124">步驟 3</span><span class="sxs-lookup"><span data-stu-id="82ef1-124">Step 3</span></span>

<span data-ttu-id="82ef1-125">認可 hello 變更 toohello 記錄集。</span><span class="sxs-lookup"><span data-stu-id="82ef1-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="82ef1-126">使用`Set-AzureRMDnsRecordSet`tooupload hello 變更 toohello 記錄集 tooAzure DNS:</span><span class="sxs-lookup"><span data-stu-id="82ef1-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="82ef1-127">2.建立自訂網域的 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="82ef1-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="82ef1-128">如果您的網域已經受 Azure DNS (請參閱[DNS 網域委派](dns-domain-delegation.md)，您可以使用 hello 遵循 hello 範例 toocreate: contoso.azurewebsites.net 的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="82ef1-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="82ef1-129">步驟 1</span><span class="sxs-lookup"><span data-stu-id="82ef1-129">Step 1</span></span>

<span data-ttu-id="82ef1-130">開啟 PowerShell 並建立新的 CNAME 記錄集並指派 tooa 變數 $rs。</span><span class="sxs-lookup"><span data-stu-id="82ef1-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="82ef1-131">這個範例會建立 「 時間 toolive 」 為 600 秒 DNS 區域中名為"contoso.com"的資料錄集類型 CNAME。</span><span class="sxs-lookup"><span data-stu-id="82ef1-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="82ef1-132">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="82ef1-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="82ef1-133">步驟 2</span><span class="sxs-lookup"><span data-stu-id="82ef1-133">Step 2</span></span>

<span data-ttu-id="82ef1-134">Hello CNAME 記錄組建立之後，您需要 toocreate 將會為 toohello web 應用程式的別名值。</span><span class="sxs-lookup"><span data-stu-id="82ef1-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="82ef1-135">使用先前指派變數"$rs"hello 您可以使用以下 toocreate hello 別名 hello PowerShell 命令的 hello web 應用程式： contoso.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="82ef1-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="82ef1-136">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="82ef1-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="82ef1-137">步驟 3</span><span class="sxs-lookup"><span data-stu-id="82ef1-137">Step 3</span></span>

<span data-ttu-id="82ef1-138">認可使用 hello hello 變更`Set-AzureRMDnsRecordSet`cmdlet:</span><span class="sxs-lookup"><span data-stu-id="82ef1-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="82ef1-139">您可以驗證 hello 記錄已正確建立藉由查詢 hello"www.contoso.com"使用 nslookup，如下所示：</span><span class="sxs-lookup"><span data-stu-id="82ef1-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="82ef1-140">建立 Web Apps 的 awverify 記錄</span><span class="sxs-lookup"><span data-stu-id="82ef1-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="82ef1-141">如果您決定 toouse A 記錄 web 應用程式時，您必須通過驗證程序 tooensure 您自己的 hello 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="82ef1-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="82ef1-142">此驗證步驟可透過建立名為 "awverify" 的特殊 CNAME 記錄來完成。</span><span class="sxs-lookup"><span data-stu-id="82ef1-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="82ef1-143">本節適用於僅 tooA 記錄。</span><span class="sxs-lookup"><span data-stu-id="82ef1-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="82ef1-144">步驟 1</span><span class="sxs-lookup"><span data-stu-id="82ef1-144">Step 1</span></span>

<span data-ttu-id="82ef1-145">建立 hello"awverify 」 記錄。</span><span class="sxs-lookup"><span data-stu-id="82ef1-145">Create hello "awverify" record.</span></span> <span data-ttu-id="82ef1-146">在 [hello 下列範例中，我們將建立 hello 自訂網域為 contoso.com tooverify 擁有權的 hello"aweverify 」 記錄。</span><span class="sxs-lookup"><span data-stu-id="82ef1-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="82ef1-147">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="82ef1-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="82ef1-148">步驟 2</span><span class="sxs-lookup"><span data-stu-id="82ef1-148">Step 2</span></span>

<span data-ttu-id="82ef1-149">一旦建立資料錄集 」 awverify"hello，指派別名設定 hello CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="82ef1-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="82ef1-150">在 [hello 下列範例中，我們將會指派 hello CNAMe 記錄集別名 tooawverify.contoso.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="82ef1-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="82ef1-151">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="82ef1-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="82ef1-152">步驟 3</span><span class="sxs-lookup"><span data-stu-id="82ef1-152">Step 3</span></span>

<span data-ttu-id="82ef1-153">認可使用 hello hello 變更`Set-AzureRMDnsRecordSet cmdlet`下方的 hello 命令所示。</span><span class="sxs-lookup"><span data-stu-id="82ef1-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="82ef1-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82ef1-154">Next steps</span></span>

<span data-ttu-id="82ef1-155">中的 hello 步驟[設定應用程式服務的自訂網域名稱](../app-service-web/web-sites-custom-domain-name.md)tooconfigure 您 web 應用程式 toouse 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="82ef1-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
