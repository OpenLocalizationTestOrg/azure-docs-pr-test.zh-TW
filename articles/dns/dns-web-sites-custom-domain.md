---
title: "建立 Web 應用程式的自訂 DNS 記錄 | Microsoft Docs"
description: "如何使用 Azure DNS 來建立 Web 應用程式的自訂網域 DNS 記錄。"
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
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="9791c-103">在自訂網域中建立 Web 應用程式的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="9791c-104">您可以使用 Azure DNS 來裝載 Web 應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9791c-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="9791c-105">例如，您正在建立 Azure Web 應用程式，而且想要讓使用者使用 contoso.com 或 www.contoso.com 做為 FQDN 來存取它。</span><span class="sxs-lookup"><span data-stu-id="9791c-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="9791c-106">若要這樣做，您必須建立兩筆記錄︰</span><span class="sxs-lookup"><span data-stu-id="9791c-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="9791c-107">指向 contoso.com 的根 "A" 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="9791c-108">指向 A 記錄之 www 名稱的 "CNAME" 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="9791c-109">請記住，如果您在 Azure 中建立 Web 應用程式的 A 記錄，如果 Web 應用程式的基礎 IP 位址變更，則您必須手動更新 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="9791c-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9791c-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="9791c-110">Before you begin</span></span>

<span data-ttu-id="9791c-111">開始之前，您必須先在 Azure DNS 中建立 DNS 區域，並將註冊機構中的區域委派給 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="9791c-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="9791c-112">若要建立 DNS 區域，請依照 [建立 DNS 區域](dns-getstarted-create-dnszone.md)的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="9791c-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="9791c-113">若要將 DNS 委派給 Azure DNS，請依照 [DNS 網域委派](dns-domain-delegation.md)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="9791c-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="9791c-114">建立區域並委派給 Azure DNS 之後，便可以為您的自訂網域建立記錄。</span><span class="sxs-lookup"><span data-stu-id="9791c-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="9791c-115">1.建立自訂網域的 A 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="9791c-116">A 記錄可用來將名稱對應到其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9791c-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="9791c-117">在下列範例中，我們會將 @ 當成 A 記錄指派給 IPv4 位址：</span><span class="sxs-lookup"><span data-stu-id="9791c-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="9791c-118">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9791c-118">Step 1</span></span>

<span data-ttu-id="9791c-119">建立 A 記錄，並指派給變數 $rs</span><span class="sxs-lookup"><span data-stu-id="9791c-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="9791c-120">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9791c-120">Step 2</span></span>

<span data-ttu-id="9791c-121">使用指派的 $rs 變數，將 IPv4 值新增至先前建立的記錄集 "@"。</span><span class="sxs-lookup"><span data-stu-id="9791c-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="9791c-122">指派的 IPv4 值將是您 Web 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9791c-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="9791c-123">若要尋找 Web 應用程式的 IP 位址，請依照[在 Azure App Service 中設定自訂網域名稱](../app-service-web/app-service-web-tutorial-custom-domain.md)的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="9791c-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="9791c-124">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9791c-124">Step 3</span></span>

<span data-ttu-id="9791c-125">認可對記錄集所做的變更。</span><span class="sxs-lookup"><span data-stu-id="9791c-125">Commit the changes to the record set.</span></span> <span data-ttu-id="9791c-126">使用 `Set-AzureRMDnsRecordSet` 將記錄集的變更上傳到 Azure DNS：</span><span class="sxs-lookup"><span data-stu-id="9791c-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="9791c-127">2.建立自訂網域的 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="9791c-128">如果您的網域已受 Azure DNS 管理 (請參閱 [DNS 網域委派](dns-domain-delegation.md))，您可以使用下列範例，建立 contoso.azurewebsites.net 的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="9791c-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="9791c-129">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9791c-129">Step 1</span></span>

<span data-ttu-id="9791c-130">開啟 PowerShell 並建立新的 CNAME 記錄集，然後指派給變數 $rs。</span><span class="sxs-lookup"><span data-stu-id="9791c-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="9791c-131">此範例會在名為 "contoso.com" 的DNS 區域中建立一個「存留時間」為 600 秒的記錄集類型 CNAME。</span><span class="sxs-lookup"><span data-stu-id="9791c-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9791c-132">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="9791c-132">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="9791c-133">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9791c-133">Step 2</span></span>

<span data-ttu-id="9791c-134">一旦建立 CNAME 記錄集，您需要建立將指向 Web 應用程式的別名值。</span><span class="sxs-lookup"><span data-stu-id="9791c-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="9791c-135">使用先前指派的變數 "$rs"，您可以使用下列 PowerShell 命令來建立 Web 應用程式 contoso.azurewebsites.net 的別名。</span><span class="sxs-lookup"><span data-stu-id="9791c-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="9791c-136">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="9791c-136">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="9791c-137">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9791c-137">Step 3</span></span>

<span data-ttu-id="9791c-138">使用 `Set-AzureRMDnsRecordSet` Cmdlet 來認可所做的變更：</span><span class="sxs-lookup"><span data-stu-id="9791c-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="9791c-139">您可以使用 nslookup 來驗證由查詢 "www.contoso.com" 正確建立的記錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9791c-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="9791c-140">建立 Web Apps 的 awverify 記錄</span><span class="sxs-lookup"><span data-stu-id="9791c-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="9791c-141">如果您決定使用 Web 應用程式的 A 記錄，您必須通過驗證程序，才能確保您擁有自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9791c-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="9791c-142">此驗證步驟可透過建立名為 "awverify" 的特殊 CNAME 記錄來完成。</span><span class="sxs-lookup"><span data-stu-id="9791c-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="9791c-143">本節適用於僅限 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="9791c-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="9791c-144">步驟 1</span><span class="sxs-lookup"><span data-stu-id="9791c-144">Step 1</span></span>

<span data-ttu-id="9791c-145">建立 awverify 記錄。</span><span class="sxs-lookup"><span data-stu-id="9791c-145">Create the "awverify" record.</span></span> <span data-ttu-id="9791c-146">在以下範例中，我們將建立 contoso.com 的 "awverify" 記錄，以驗證自訂網域的擁有權。</span><span class="sxs-lookup"><span data-stu-id="9791c-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9791c-147">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="9791c-147">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="9791c-148">步驟 2</span><span class="sxs-lookup"><span data-stu-id="9791c-148">Step 2</span></span>

<span data-ttu-id="9791c-149">一旦建立 "awverify" 記錄集，請指派 CNAME 記錄集別名。</span><span class="sxs-lookup"><span data-stu-id="9791c-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="9791c-150">在以下範例中，我們會將 CNAME 記錄集別名指派為 awverify.contoso.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="9791c-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="9791c-151">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="9791c-151">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="9791c-152">步驟 3</span><span class="sxs-lookup"><span data-stu-id="9791c-152">Step 3</span></span>

<span data-ttu-id="9791c-153">使用 `Set-AzureRMDnsRecordSet cmdlet`認可所做的變更，如下列命令所示。</span><span class="sxs-lookup"><span data-stu-id="9791c-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="9791c-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9791c-154">Next steps</span></span>

<span data-ttu-id="9791c-155">依照 [設定 App Service 的自訂網域名稱](../app-service-web/web-sites-custom-domain-name.md) 中的步驟設定 Web 應用程式使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9791c-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
