---
title: "如何將 Azure API 管理與內部虛擬網路搭配使用 | Microsoft Docs"
description: "了解如何在內部虛擬網路中安裝和設定 Azure API 管理。"
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
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="2348b-103">搭配使用 Azure API 管理服務與內部虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2348b-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="2348b-104">搭配 Azure 虛擬網路 (VNET)，API 管理可以管理無法在網際網路上存取的 API。</span><span class="sxs-lookup"><span data-stu-id="2348b-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="2348b-105">有多個 VPN 技術可用來進行連線，可以在 VNET 內部署兩種主要模式的 API 管理︰</span><span class="sxs-lookup"><span data-stu-id="2348b-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="2348b-106">外部</span><span class="sxs-lookup"><span data-stu-id="2348b-106">External</span></span>
* <span data-ttu-id="2348b-107">內部</span><span class="sxs-lookup"><span data-stu-id="2348b-107">Internal</span></span>

## <span data-ttu-id="2348b-108"><a name="overview"> </a>概觀</span><span class="sxs-lookup"><span data-stu-id="2348b-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="2348b-109">當 API 管理部署為「內部虛擬網路」模式時，只有在您可以控制存取的虛擬網路內部才看得到所有服務端點 (閘道器、開發人員入口網站、發行者入口網站、直接管理、Git)。</span><span class="sxs-lookup"><span data-stu-id="2348b-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="2348b-110">不會在公用 DNS 伺服器上註冊任何服務端點。</span><span class="sxs-lookup"><span data-stu-id="2348b-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="2348b-111">使用內部模式的 API 管理，您可以實現下列案例</span><span class="sxs-lookup"><span data-stu-id="2348b-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="2348b-112">協力廠商可在您的私人資料中心外使用站對站或 ExpressRoute VPN 連線存取資料中心時，可以安全地將 API 裝載在您的私人資料中心。</span><span class="sxs-lookup"><span data-stu-id="2348b-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="2348b-113">透過通用閘道器公開您的雲端型 API 和內部部署 API，藉此實現混合式雲端案例。</span><span class="sxs-lookup"><span data-stu-id="2348b-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="2348b-114">使用單一閘道器端點，管理裝載在多個地理位置的 API。</span><span class="sxs-lookup"><span data-stu-id="2348b-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="2348b-115"><a name="enable-vpn"> </a>在內部虛擬網路中建立 API 管理</span><span class="sxs-lookup"><span data-stu-id="2348b-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="2348b-116">內部虛擬網路中的 API 管理服務是裝載在內部負載平衡器 (ILB) 後。</span><span class="sxs-lookup"><span data-stu-id="2348b-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="2348b-117">ILB 的 IP 位址落在 [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) 範圍內。</span><span class="sxs-lookup"><span data-stu-id="2348b-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="2348b-118">使用 Azure 入口網站啟用 VNET 連線</span><span class="sxs-lookup"><span data-stu-id="2348b-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="2348b-119">首先，依照[建立 API 管理服務][Create API Management service]的步驟建立 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="2348b-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="2348b-120">然後，將 API 管理設定為在虛擬網路內部署。</span><span class="sxs-lookup"><span data-stu-id="2348b-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![在內部虛擬網路中設定 APIM 的功能表][api-management-using-internal-vnet-menu]

<span data-ttu-id="2348b-122">部署成功後，您應該會在儀表板上看到您的服務的內部虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2348b-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![已設定內部 VNET 的 API 管理儀表板][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="2348b-124">使用 PowerShell Cmdlet 啟用 VNET 連線</span><span class="sxs-lookup"><span data-stu-id="2348b-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="2348b-125">您也可以使用 PowerShell 來mdlet 來啟用 VNET 連線。</span><span class="sxs-lookup"><span data-stu-id="2348b-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="2348b-126">**在 VNET 內建立 API 管理服務**：使用 [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) Cmdlet 在 VNET 內建立 Azure API 管理服務，並將其設定為使用內部 VNET 類型。</span><span class="sxs-lookup"><span data-stu-id="2348b-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="2348b-127">**在 VNET 內部署現有 API 管理服務**：使用 [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) Cmdlet 移動虛擬網路內的現有 Azure API 管理服務，並將其設定為使用內部 VNET 類型。</span><span class="sxs-lookup"><span data-stu-id="2348b-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="2348b-128"><a name="apim-dns-configuration"></a> DNS 設定</span><span class="sxs-lookup"><span data-stu-id="2348b-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="2348b-129">使用外部虛擬網路模式的 API 管理時，DNS 是由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="2348b-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="2348b-130">若是內部虛擬網路模式，您必須管理您自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="2348b-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="2348b-131">API 管理服務不會接聽 IP 位址傳來的要求。</span><span class="sxs-lookup"><span data-stu-id="2348b-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="2348b-132">它只會回應對主機名稱 (在其服務端點上設定) 提出的要求；服務端點包括閘道器、開發人員入口網站、發行者入口網站、直接管理端點、Git。</span><span class="sxs-lookup"><span data-stu-id="2348b-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="2348b-133">預設主機名稱上的存取︰</span><span class="sxs-lookup"><span data-stu-id="2348b-133">Access on default host names:</span></span>
<span data-ttu-id="2348b-134">當您在公用 Azure 雲端 (假設名為「contoso」) 中建立 API 管理服務，依預設會設定下列服務端點。</span><span class="sxs-lookup"><span data-stu-id="2348b-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="2348b-135">閘道 / 代理程式 - contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="2348b-136">發行者入口網站和開發人員入口網站 - contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="2348b-137">直接管理端點 - contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="2348b-138">Git - contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="2348b-139">若要存取這些 API 管理服務端點，您可在連線到「已部署 API 管理的虛擬網路」的子網路中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2348b-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="2348b-140">假設服務的內部虛擬 IP 位址是 10.0.0.5，您可以進行主機檔案對應 (%SystemDrive%\drivers\etc\hosts)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2348b-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="2348b-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="2348b-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="2348b-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="2348b-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="2348b-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="2348b-145">然後您就可以從您建立的虛擬機器存取所有服務端點。</span><span class="sxs-lookup"><span data-stu-id="2348b-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="2348b-146">如果在虛擬網路中使用自訂 DNS 伺服器，您也可以建立 A DNS 記錄，並從虛擬網路中的任何地方存取這些端點。</span><span class="sxs-lookup"><span data-stu-id="2348b-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="2348b-147">自訂網域名稱上的存取：</span><span class="sxs-lookup"><span data-stu-id="2348b-147">Access on custom domain names:</span></span>
<span data-ttu-id="2348b-148">如果您不想要存取具有預設主機名稱的 API 管理服務，可以為您的所有服務端點設定自訂網域名稱，類似這樣：</span><span class="sxs-lookup"><span data-stu-id="2348b-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![設定 API 管理的自訂網域][api-management-custom-domain-name]

<span data-ttu-id="2348b-150">然後您可以在您的 DNS 伺服器中建立 A 記錄，用來存取這些只能從您的虛擬網路存取的端點。</span><span class="sxs-lookup"><span data-stu-id="2348b-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="2348b-151"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="2348b-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="2348b-152">[在 VNET 中設定 APIM 常見的網路組態問題][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="2348b-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="2348b-153">虛擬網路常見問題集</span><span class="sxs-lookup"><span data-stu-id="2348b-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="2348b-154">在 DNS 中建立 A 記錄</span><span class="sxs-lookup"><span data-stu-id="2348b-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
