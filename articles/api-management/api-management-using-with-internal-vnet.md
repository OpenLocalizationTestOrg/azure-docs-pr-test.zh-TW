---
title: "aaaHow toouse Azure API 管理與內部虛擬網路 |Microsoft 文件"
description: "深入了解如何 toosetup 和內部虛擬網路中設定 Azure API 管理。"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="5773f-103">搭配使用 Azure API 管理服務與內部虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5773f-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="5773f-104">API 管理可以使用 Azure 虛擬網路 (Vnet)，來管理應用程式開發介面無法存取 hello 網際網路上。</span><span class="sxs-lookup"><span data-stu-id="5773f-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="5773f-105">有多種 VPN 技術可提供 toomake hello 連線和 API 管理可被部署在 hello VNET 內的兩個主要模式：</span><span class="sxs-lookup"><span data-stu-id="5773f-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="5773f-106">外部</span><span class="sxs-lookup"><span data-stu-id="5773f-106">External</span></span>
* <span data-ttu-id="5773f-107">內部</span><span class="sxs-lookup"><span data-stu-id="5773f-107">Internal</span></span>

## <span data-ttu-id="5773f-108"><a name="overview"> </a>概觀</span><span class="sxs-lookup"><span data-stu-id="5773f-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="5773f-109">API 管理中的內部虛擬網路模式部署時，所有 hello 服務端點 （閘道、 開發人員入口網站、 發行者入口網站中，直接管理和 Git），才都會顯示虛擬網路內部的控制存取權。</span><span class="sxs-lookup"><span data-stu-id="5773f-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="5773f-110">無 hello 服務端點登錄在 hello 公用 DNS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5773f-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="5773f-111">使用 API 管理內部的模式中，您可以達到下列案例的 hello</span><span class="sxs-lookup"><span data-stu-id="5773f-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="5773f-112">協力廠商可在您的私人資料中心外使用站對站或 ExpressRoute VPN 連線存取資料中心時，可以安全地將 API 裝載在您的私人資料中心。</span><span class="sxs-lookup"><span data-stu-id="5773f-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="5773f-113">透過通用閘道器公開您的雲端型 API 和內部部署 API，藉此實現混合式雲端案例。</span><span class="sxs-lookup"><span data-stu-id="5773f-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="5773f-114">使用單一閘道器端點，管理裝載在多個地理位置的 API。</span><span class="sxs-lookup"><span data-stu-id="5773f-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="5773f-115"><a name="enable-vpn"> </a>在內部虛擬網路中建立 API 管理</span><span class="sxs-lookup"><span data-stu-id="5773f-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="5773f-116">hello 內部虛擬網路中的 API 管理服務是內部的負載 Balancer(ILB) 後面進行裝載。</span><span class="sxs-lookup"><span data-stu-id="5773f-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="5773f-117">hello hello ILB 的 IP 位址位於 hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html)範圍。</span><span class="sxs-lookup"><span data-stu-id="5773f-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="5773f-118">使用 Azure 入口網站啟用 VNET 連線</span><span class="sxs-lookup"><span data-stu-id="5773f-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="5773f-119">第一次使用 hello 步驟建立 hello API 管理服務[建立 API 管理服務][Create API Management service]。</span><span class="sxs-lookup"><span data-stu-id="5773f-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="5773f-120">然後設定 API 管理 toobe 部署在虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="5773f-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![在內部虛擬網路中設定 APIM 的功能表][api-management-using-internal-vnet-menu]

<span data-ttu-id="5773f-122">Hello 部署成功之後，您應該在 hello 儀表板上看到 hello 內部的虛擬 IP 位址，您的服務。</span><span class="sxs-lookup"><span data-stu-id="5773f-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![已設定內部 VNET 的 API 管理儀表板][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="5773f-124">使用 PowerShell Cmdlet 啟用 VNET 連線</span><span class="sxs-lookup"><span data-stu-id="5773f-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="5773f-125">您也可以啟用 VNET 連線使用 hello PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5773f-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="5773f-126">**建立 API 管理服務內 VNET**： 使用 hello cmdlet[新增 AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate Azure API 管理服務內的 VNET，並設定它 toouse hello 內部 VNET 類型。</span><span class="sxs-lookup"><span data-stu-id="5773f-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="5773f-127">**部署在 VNET 內現有的 API 管理服務**： 使用 hello cmdlet[更新 AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove 現有的 Azure API 管理服務的虛擬網路內，並設定它 toouse內部 VNET 型別。</span><span class="sxs-lookup"><span data-stu-id="5773f-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="5773f-128"><a name="apim-dns-configuration"></a> DNS 設定</span><span class="sxs-lookup"><span data-stu-id="5773f-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="5773f-129">使用外部虛擬網路模式的 API 管理時，DNS 是由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="5773f-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="5773f-130">內部虛擬網路模式，您必須 toomanage 自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="5773f-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="5773f-131">API 管理服務不會接聽 toorequests 即將於 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5773f-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="5773f-132">它只會回應 toorequests toohello 的服務端點上設定主機名稱 （其中包括閘道、 開發人員入口網站、 發行者入口網站中，直接管理端點和 git）。</span><span class="sxs-lookup"><span data-stu-id="5773f-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="5773f-133">預設主機名稱上的存取︰</span><span class="sxs-lookup"><span data-stu-id="5773f-133">Access on default host names:</span></span>
<span data-ttu-id="5773f-134">當您建立 API 管理服務在公用 Azure 雲端中，例如名為"contoso"時，hello 下列服務端點是預設設定。</span><span class="sxs-lookup"><span data-stu-id="5773f-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="5773f-135">閘道 / 代理程式 - contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="5773f-136">發行者入口網站和開發人員入口網站 - contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="5773f-137">直接管理端點 - contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="5773f-138">Git - contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="5773f-139">tooaccess 這些 API 管理服務端點，您可以在其中部署應用程式開發介面管理連線的子網路 toohello 虛擬網路中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5773f-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="5773f-140">假設您的服務的 hello 內部的虛擬 IP 位址 10.0.0.5，您可以執行 hello 主機檔案對應 （%systemdrive%\drivers\etc\hosts)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5773f-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="5773f-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="5773f-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="5773f-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="5773f-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="5773f-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="5773f-145">然後，您就可以存取所有 hello 服務端點從 hello 您建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5773f-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="5773f-146">如果在虛擬網路中使用自訂 DNS 伺服器，您也可以建立 A DNS 記錄，並從虛擬網路中的任何地方存取這些端點。</span><span class="sxs-lookup"><span data-stu-id="5773f-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="5773f-147">自訂網域名稱上的存取：</span><span class="sxs-lookup"><span data-stu-id="5773f-147">Access on custom domain names:</span></span>
<span data-ttu-id="5773f-148">如果您不想 tooaccess hello 與 hello 預設主控件名稱的 API 管理服務，您可以設定所有服務端點類似如下的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="5773f-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![設定 API 管理的自訂網域][api-management-custom-domain-name]

<span data-ttu-id="5773f-150">然後您可以建立 A 記錄，DNS 伺服器 tooaccess 中也就是只從您的虛擬網路中存取這些端點。</span><span class="sxs-lookup"><span data-stu-id="5773f-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="5773f-151"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="5773f-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="5773f-152">[在 VNET 中設定 APIM 常見的網路組態問題][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="5773f-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="5773f-153">虛擬網路常見問題集</span><span class="sxs-lookup"><span data-stu-id="5773f-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="5773f-154">在 DNS 中建立 A 記錄</span><span class="sxs-lookup"><span data-stu-id="5773f-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
