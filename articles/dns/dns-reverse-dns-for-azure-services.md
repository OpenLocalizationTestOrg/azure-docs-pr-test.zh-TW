---
title: "Azure 服務的反向 DNS | Microsoft Docs"
description: "了解如何設定 Azure 託管服務的反向 DNS 對應"
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
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="398bf-103">設定 Azure 託管服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="398bf-104">本文說明如何設定 Azure 託管服務的反向 DNS 對應。</span><span class="sxs-lookup"><span data-stu-id="398bf-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="398bf-105">Azure 中的服務會使用由 Azure 指派並由 Microsoft 所擁有的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="398bf-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="398bf-106">這些反向 DNS 記錄 (PTR 記錄) 必須建立在對應的 Microsoft 擁有之反向 DNS 對應區域中。</span><span class="sxs-lookup"><span data-stu-id="398bf-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="398bf-107">本文說明如何執行此作業。</span><span class="sxs-lookup"><span data-stu-id="398bf-107">This article explains how to do this.</span></span>

<span data-ttu-id="398bf-108">請勿混淆這種情況以及[為在 Azure DNS 中指派的 IP 範圍託管反向 DNS 對應區域](dns-reverse-dns-hosting.md)的功能。</span><span class="sxs-lookup"><span data-stu-id="398bf-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="398bf-109">本例中，反向對應區域所代表的 IP 範圍必須指派給您的組織，通常由您的 ISP 指派。</span><span class="sxs-lookup"><span data-stu-id="398bf-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="398bf-110">在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="398bf-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="398bf-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="398bf-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="398bf-112">在資源管理員部署模型中，是透過 PublicIpAddress 資源公開計算資源 (例如虛擬機器、虛擬機器擴展集或 Service Fabric 叢集)。</span><span class="sxs-lookup"><span data-stu-id="398bf-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="398bf-113">反向 DNS 對應是使用 PublicIpAddress 的 'ReverseFqdn' 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="398bf-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="398bf-114">在傳統部署模型中，計算資源是使用雲端服務公開。</span><span class="sxs-lookup"><span data-stu-id="398bf-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="398bf-115">反向 DNS 對應是使用雲端服務的 'ReverseDnsFqdn' 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="398bf-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="398bf-116">目前不支援 Azure App Service 反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="398bf-117">反向 DNS 記錄的驗證</span><span class="sxs-lookup"><span data-stu-id="398bf-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="398bf-118">協力廠商應該無法為對應至您 DNS 網域的 Azure 服務建立反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="398bf-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="398bf-119">為避免這個問題，Azure 只允許建立這種條件下的反向 DNS 記錄：反向 DNS 記錄中指定的網域名稱能解析為相同 Azure 訂用帳戶中之 PublicIpAddress 或雲端服務的 DNS 名稱或 IP 位址，或和它們相同。</span><span class="sxs-lookup"><span data-stu-id="398bf-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="398bf-120">只有設定或修改反向 DNS 記錄時，才會執行這項驗證。</span><span class="sxs-lookup"><span data-stu-id="398bf-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="398bf-121">不會執行定期的重新驗證。</span><span class="sxs-lookup"><span data-stu-id="398bf-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="398bf-122">例如：假設 PublicIpAddress 資源的 DNS 名稱為 contosoapp1.northus.cloudapp.azure.com，且 IP 位址為 23.96.52.53。</span><span class="sxs-lookup"><span data-stu-id="398bf-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="398bf-123">則可將 PublicIpAddress 的 ReverseFqdn 指定為：</span><span class="sxs-lookup"><span data-stu-id="398bf-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="398bf-124">PublicIpAddress 的 DNS 名稱為 contosoapp1.northus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="398bf-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="398bf-125">相同訂用帳戶中不同 PublicIpAddress 的 DNS 名稱，例如 contosoapp2.westus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="398bf-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="398bf-126">虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是「第一次」設定為 contosoapp1.northus.cloudapp.azure.com 的 CNAME，或相同訂用帳戶中不同 PublicIpAddress 的 CNAME。</span><span class="sxs-lookup"><span data-stu-id="398bf-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="398bf-127">虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是「第一次」設定為 IP 位址 23.96.52.53 的 A 記錄，或相同訂用帳戶中不同 PublicIpAddress 之 IP 位址的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="398bf-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="398bf-128">相同的條件約束適用於雲端服務的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="398bf-129">PublicIpAddress 資源的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="398bf-130">本節會詳細說明如何在資源管理員部署模型中，使用 Azure PowerShell、Azure CLI 1.0 或 Azure CLI 2.0 為 PublicIpAddress 資源設定反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="398bf-131">目前不支援透過 Azure 入口網站為 PublicIpAddress 資源設定反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="398bf-132">Azure 目前只支援 IPv4 PublicIpAddress 資源的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="398bf-133">其不支援 IPv6。</span><span class="sxs-lookup"><span data-stu-id="398bf-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="398bf-134">將反向 DNS 新增至現有的 PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="398bf-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="398bf-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="398bf-135">PowerShell</span></span>

<span data-ttu-id="398bf-136">將反向 DNS 新增至現有的 PublicIpAddresses：</span><span class="sxs-lookup"><span data-stu-id="398bf-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="398bf-137">若要將反向 DNS 新增至尚未有 DNS 名稱的現有 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="398bf-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="398bf-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="398bf-138">Azure CLI 1.0</span></span>

<span data-ttu-id="398bf-139">將反向 DNS 新增至現有的 PublicIpAddresses：</span><span class="sxs-lookup"><span data-stu-id="398bf-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="398bf-140">若要將反向 DNS 新增至尚未有 DNS 名稱的現有 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="398bf-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="398bf-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="398bf-141">Azure CLI 2.0</span></span>

<span data-ttu-id="398bf-142">將反向 DNS 新增至現有的 PublicIpAddresses：</span><span class="sxs-lookup"><span data-stu-id="398bf-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="398bf-143">若要將反向 DNS 新增至尚未有 DNS 名稱的現有 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="398bf-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="398bf-144">建立具有反向 DNS 的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="398bf-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="398bf-145">建立已指定反向 DNS 屬性的新 PublicIpAddress：</span><span class="sxs-lookup"><span data-stu-id="398bf-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="398bf-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="398bf-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="398bf-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="398bf-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="398bf-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="398bf-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="398bf-149">檢視現有 PublicIpAddresses 的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="398bf-150">檢視現有 PublicIpAddress 已設定的值：</span><span class="sxs-lookup"><span data-stu-id="398bf-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="398bf-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="398bf-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="398bf-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="398bf-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="398bf-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="398bf-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="398bf-154">移除現有公用 IP 位址的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="398bf-155">從現有的 PublicIpAddress 移除反向 DNS 屬性：</span><span class="sxs-lookup"><span data-stu-id="398bf-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="398bf-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="398bf-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="398bf-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="398bf-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="398bf-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="398bf-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="398bf-159">設定雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="398bf-160">本節會詳細說明如何在傳統部署模型中，使用 Azure PowerShell 為雲端服務設定反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="398bf-161">不支援透過 Azure 入口網站、Azure CLI 1.0 或 Azure CLI 2.0 為雲端服務設定反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="398bf-162">將反向 DNS 新增至現有的雲端服務</span><span class="sxs-lookup"><span data-stu-id="398bf-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="398bf-163">將反向 DNS 記錄新增至雲端服務：</span><span class="sxs-lookup"><span data-stu-id="398bf-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="398bf-164">建立具有反向 DNS 的雲端服務</span><span class="sxs-lookup"><span data-stu-id="398bf-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="398bf-165">建立已指定反向 DNS 屬性的新雲端服務：</span><span class="sxs-lookup"><span data-stu-id="398bf-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="398bf-166">檢視現有雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="398bf-167">檢視現有雲端服務的反向 DNS 屬性：</span><span class="sxs-lookup"><span data-stu-id="398bf-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="398bf-168">移除現有雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="398bf-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="398bf-169">從現有的雲端服務移除反向 DNS 屬性：</span><span class="sxs-lookup"><span data-stu-id="398bf-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="398bf-170">常見問題集</span><span class="sxs-lookup"><span data-stu-id="398bf-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="398bf-171">反向 DNS 記錄的成本為何？</span><span class="sxs-lookup"><span data-stu-id="398bf-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="398bf-172">完全免費！</span><span class="sxs-lookup"><span data-stu-id="398bf-172">They're free!</span></span>  <span data-ttu-id="398bf-173">反向 DNS 記錄或查詢不需要額外成本。</span><span class="sxs-lookup"><span data-stu-id="398bf-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="398bf-174">我的反向 DNS 記錄會從網際網路解析嗎？</span><span class="sxs-lookup"><span data-stu-id="398bf-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="398bf-175">是。</span><span class="sxs-lookup"><span data-stu-id="398bf-175">Yes.</span></span> <span data-ttu-id="398bf-176">在您為 Azure 服務設定反向 DNS 屬性之後，Azure 會管理所有必要的 DNS 委派和 DNS 區域，以確保反向 DNS 記錄可以為所有網際網路使用者解析。</span><span class="sxs-lookup"><span data-stu-id="398bf-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="398bf-177">我的 Azure 服務有沒有建立預設的反向 DNS 記錄？</span><span class="sxs-lookup"><span data-stu-id="398bf-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="398bf-178">否。</span><span class="sxs-lookup"><span data-stu-id="398bf-178">No.</span></span> <span data-ttu-id="398bf-179">反向 DNS 是選用的功能。</span><span class="sxs-lookup"><span data-stu-id="398bf-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="398bf-180">如果您選擇不設定，則不會建立任何預設反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="398bf-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="398bf-181">完整網域名稱 (FQDN) 的格式為何？</span><span class="sxs-lookup"><span data-stu-id="398bf-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="398bf-182">FQDN 是以正向順序指定，且必須以點結束 (例如，"app1.contoso.com")。</span><span class="sxs-lookup"><span data-stu-id="398bf-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="398bf-183">如果我指定的反向 DNS 驗證檢查失敗，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="398bf-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="398bf-184">當反向 DNS 驗證檢查失敗時，設定反向 DNS 記錄的作業也會失敗。</span><span class="sxs-lookup"><span data-stu-id="398bf-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="398bf-185">請依要求更正反向 DNS 值，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="398bf-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="398bf-186">Azure App Service 可以設定反向 DNS 嗎？</span><span class="sxs-lookup"><span data-stu-id="398bf-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="398bf-187">否。</span><span class="sxs-lookup"><span data-stu-id="398bf-187">No.</span></span> <span data-ttu-id="398bf-188">目前不支援 Azure App Service 反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="398bf-189">Azure 服務可以設定多個反向 DNS 記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="398bf-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="398bf-190">否。</span><span class="sxs-lookup"><span data-stu-id="398bf-190">No.</span></span> <span data-ttu-id="398bf-191">Azure 雲端服務或 PublicIpAddress，Azure 只支援一筆反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="398bf-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="398bf-192">IPv6 PublicIpAddress 資源可以設定反向 DNS嗎？</span><span class="sxs-lookup"><span data-stu-id="398bf-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="398bf-193">否。</span><span class="sxs-lookup"><span data-stu-id="398bf-193">No.</span></span> <span data-ttu-id="398bf-194">Azure 目前只支援 IPv4 PublicIpAddress 資源和雲端服務的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="398bf-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="398bf-195">我可以從我的 Azure 計算服務將電子郵件傳送至外部網域嗎？</span><span class="sxs-lookup"><span data-stu-id="398bf-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="398bf-196">否。</span><span class="sxs-lookup"><span data-stu-id="398bf-196">No.</span></span> [<span data-ttu-id="398bf-197">Azure 計算服務不支援將電子郵件傳送至外部網域</span><span class="sxs-lookup"><span data-stu-id="398bf-197">Azure Compute services do not support sending emails to external domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="398bf-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="398bf-198">Next steps</span></span>

<span data-ttu-id="398bf-199">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="398bf-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="398bf-200">了解如何[在 Azure DNS 中為您 ISP 指派的 IP 範圍託管反向對應區域](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="398bf-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

