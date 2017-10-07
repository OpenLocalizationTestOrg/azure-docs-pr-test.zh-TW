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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="8ab0d-103">設定 Azure 託管服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="8ab0d-104">本文說明如何 tooconfigure 反向 DNS 查閱，在 Azure 中裝載的服務。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="8ab0d-105">Azure 中的服務會使用由 Azure 指派並由 Microsoft 所擁有的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="8ab0d-106">必須在 hello 對應 Microsoft 屬反向 DNS 查閱區域中建立這些反向 DNS 記錄 （PTR 記錄）。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="8ab0d-107">這篇文章說明如何 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-107">This article explains how toodo this.</span></span>

<span data-ttu-id="8ab0d-108">此案例不應混淆 hello 能力太[裝載 hello 反向 DNS 查閱區域用於您指派的 IP 範圍中 Azure DNS](dns-reverse-dns-hosting.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="8ab0d-109">在此情況下，由 hello 反向對應區域的 hello IP 範圍必須指派 tooyour 組織通常由您的 ISP。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="8ab0d-110">在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="8ab0d-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="8ab0d-112">在 hello Resource Manager 部署模型，計算資源 （例如虛擬機器、 虛擬機器擴展集或 Service Fabric 叢集） 會公開透過 PublicIpAddress 資源。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="8ab0d-113">使用 hello PublicIpAddress hello 'ReverseFqdn' 屬性所設定反向 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="8ab0d-114">在 hello 傳統部署模型中，計算資源會公開使用雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="8ab0d-115">使用雲端服務的 hello hello 'ReverseDnsFqdn' 屬性所設定反向 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="8ab0d-116">Hello Azure 應用程式服務目前不支援反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="8ab0d-117">反向 DNS 記錄的驗證</span><span class="sxs-lookup"><span data-stu-id="8ab0d-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="8ab0d-118">第三方不應該能 toocreate Azure 服務對應 tooyour DNS 網域的反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="8ab0d-119">tooprevent，但 Azure 只允許反向 DNS 記錄，其中 hello 反向 DNS 記錄中指定的網域名稱是 hello 相同，或解析，hello DNS 名稱或 IP 位址的 PublicIpAddress 或雲端服務中 hello 相同的 hello 建立 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="8ab0d-120">設定或修改 hello 反向 DNS 記錄時，才會執行這項驗證。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="8ab0d-121">不會執行定期的重新驗證。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="8ab0d-122">例如： 假設 hello PublicIpAddress 資源 hello DNS 名稱 contosoapp1.northus.cloudapp.azure.com 和 23.96.52.53 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="8ab0d-123">hello ReverseFqdn hello PublicIpAddress 可以指定為：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="8ab0d-124">hello PublicIpAddress hello DNS 名稱、 contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="8ab0d-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="8ab0d-125">hello DNS 名稱會在 hello 不同 PublicIpAddress 相同訂用帳戶，例如 contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="8ab0d-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="8ab0d-126">虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是*第一個*設定為 CNAME toocontosoapp1.northus.cloudapp.azure.com 或 tooa 不同 PublicIpAddress hello 中相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="8ab0d-127">虛名 DNS 名稱，例如 app1.contoso.com，只要這個名稱是*第一個*設定 A 記錄 toohello IP 位址 23.96.52.53 或不同的 PublicIpAddress toohello IP 位址在 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="8ab0d-128">hello 相同的條件約束套用至 tooreverse DNS 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="8ab0d-129">PublicIpAddress 資源的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="8ab0d-130">本節提供如何 tooconfigure 反向 DNS 中 hello Resource Manager 部署模型，使用 Azure PowerShell、 Azure CLI 1.0 或 Azure CLI 2.0 的 PublicIpAddress 資源的詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="8ab0d-131">設定反向 DNS PublicIpAddress 資源的目前不支援透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="8ab0d-132">Azure 目前只支援 IPv4 PublicIpAddress 資源的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="8ab0d-133">其不支援 IPv6。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="8ab0d-134">加入現有的 PublicIpAddresses 反向 DNS tooan</span><span class="sxs-lookup"><span data-stu-id="8ab0d-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ab0d-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab0d-135">PowerShell</span></span>

<span data-ttu-id="8ab0d-136">tooadd 反向 DNS tooan 現有 PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="8ab0d-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="8ab0d-137">tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ab0d-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-138">Azure CLI 1.0</span></span>

<span data-ttu-id="8ab0d-139">tooadd 反向 DNS tooan 現有 PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="8ab0d-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="8ab0d-140">tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ab0d-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-141">Azure CLI 2.0</span></span>

<span data-ttu-id="8ab0d-142">tooadd 反向 DNS tooan 現有 PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="8ab0d-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="8ab0d-143">tooadd 反向 DNS tooan 現有還沒有 DNS 名稱的 PublicIpAddress，您也必須指定 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="8ab0d-144">建立具有反向 DNS 的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8ab0d-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="8ab0d-145">新 toocreate PublicIpAddress hello 與反向 DNS 屬性已指定：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ab0d-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab0d-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ab0d-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ab0d-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="8ab0d-149">檢視現有 PublicIpAddresses 的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="8ab0d-150">tooview hello 針對現有的 PublicIpAddress 設定值：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ab0d-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab0d-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ab0d-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ab0d-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="8ab0d-154">移除現有公用 IP 位址的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="8ab0d-155">tooremove 從現有的 PublicIpAddress 反向 DNS 屬性：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ab0d-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab0d-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ab0d-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ab0d-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ab0d-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="8ab0d-159">設定雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="8ab0d-160">本節提供如何 tooconfigure 反向 DNS 雲端服務在 hello 傳統部署模型中，使用 Azure PowerShell 的詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="8ab0d-161">不支援透過 hello Azure 入口網站，Azure CLI 1.0 或 Azure CLI 2.0 設定雲端服務的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="8ab0d-162">新增反向 DNS tooexisting 雲端服務</span><span class="sxs-lookup"><span data-stu-id="8ab0d-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="8ab0d-163">tooadd 反向 DNS 記錄 tooan 現有雲端服務：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="8ab0d-164">建立具有反向 DNS 的雲端服務</span><span class="sxs-lookup"><span data-stu-id="8ab0d-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="8ab0d-165">toocreate hello 已經指定反向 DNS 內容與新的雲端服務：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="8ab0d-166">檢視現有雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="8ab0d-167">tooview hello 反向 DNS 屬性為現有的雲端服務：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="8ab0d-168">移除現有雲端服務的反向 DNS</span><span class="sxs-lookup"><span data-stu-id="8ab0d-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="8ab0d-169">tooremove 反向 DNS 屬性從現有的雲端服務：</span><span class="sxs-lookup"><span data-stu-id="8ab0d-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="8ab0d-170">常見問題集</span><span class="sxs-lookup"><span data-stu-id="8ab0d-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="8ab0d-171">反向 DNS 記錄的成本為何？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="8ab0d-172">完全免費！</span><span class="sxs-lookup"><span data-stu-id="8ab0d-172">They're free!</span></span>  <span data-ttu-id="8ab0d-173">反向 DNS 記錄或查詢不需要額外成本。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="8ab0d-174">將從我反向 DNS 記錄解析 hello 網際網路嗎？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="8ab0d-175">是。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-175">Yes.</span></span> <span data-ttu-id="8ab0d-176">一旦您設定 hello 反向 DNS 屬性為您的 Azure 服務，Azure 會管理所有 hello DNS 委派和反向 DNS 記錄的 tooensure 解析所有的網際網路使用者所需的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="8ab0d-177">我的 Azure 服務有沒有建立預設的反向 DNS 記錄？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="8ab0d-178">否。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-178">No.</span></span> <span data-ttu-id="8ab0d-179">反向 DNS 是選用的功能。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="8ab0d-180">沒有預設值，如果您選擇不 tooconfigure 建立反向 DNS 記錄它們。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="8ab0d-181">什麼是 hello hello 完整網域名稱 (FQDN) 格式？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="8ab0d-182">FQDN 是以正向順序指定，且必須以點結束 (例如，"app1.contoso.com")。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="8ab0d-183">發生什麼事如果 hello 的 hello 驗證檢查反向的 DNS 我指定失敗？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="8ab0d-184">其中 hello 反向 DNS 驗證檢查失敗，就會失敗 hello 作業 tooconfigure hello 反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="8ab0d-185">更正 hello 反向 DNS 值為必要項目，然後重試。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="8ab0d-186">Azure App Service 可以設定反向 DNS 嗎？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="8ab0d-187">否。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-187">No.</span></span> <span data-ttu-id="8ab0d-188">Hello Azure 應用程式服務不支援反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="8ab0d-189">Azure 服務可以設定多個反向 DNS 記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="8ab0d-190">否。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-190">No.</span></span> <span data-ttu-id="8ab0d-191">Azure 雲端服務或 PublicIpAddress，Azure 只支援一筆反向 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="8ab0d-192">IPv6 PublicIpAddress 資源可以設定反向 DNS嗎？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="8ab0d-193">否。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-193">No.</span></span> <span data-ttu-id="8ab0d-194">Azure 目前只支援 IPv4 PublicIpAddress 資源和雲端服務的反向 DNS。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="8ab0d-195">我可以傳送電子郵件 tooexternal 網域從我的 Azure 計算服務？</span><span class="sxs-lookup"><span data-stu-id="8ab0d-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="8ab0d-196">否。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-196">No.</span></span> [<span data-ttu-id="8ab0d-197">Azure 計算服務不支援傳送電子郵件 tooexternal 網域</span><span class="sxs-lookup"><span data-stu-id="8ab0d-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="8ab0d-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ab0d-198">Next steps</span></span>

<span data-ttu-id="8ab0d-199">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="8ab0d-200">了解如何太[主機 hello 反向對應區域，為您的 ISP 指派的 IP 範圍，在 Azure DNS](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab0d-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

