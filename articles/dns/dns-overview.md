---
title: "Azure DNS 概觀 | Microsoft Docs"
description: "在 Microsoft Azure 上裝載 Azure DNS 服務的概觀。 在 Microsoft Azure 上裝載您的網域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="c9764-104">Azure DNS 概觀</span><span class="sxs-lookup"><span data-stu-id="c9764-104">Azure DNS overview</span></span>

<span data-ttu-id="c9764-105">網域名稱系統 (DNS) 負責將網站或服務名稱轉譯 (或解析) 為其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c9764-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="c9764-106">Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="c9764-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="c9764-107">只要將您的網域裝載於 Azure，就可以像管理其他 Azure 服務一樣，使用相同的認證、API、工具和計費方式來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="c9764-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS 概觀](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="c9764-109">特性</span><span class="sxs-lookup"><span data-stu-id="c9764-109">Features</span></span>

* <span data-ttu-id="c9764-110">**可靠性和效能** - Azure DNS 中的 DNS 網域是裝載於 Azure 的 DNS 名稱伺服器全球網路。</span><span class="sxs-lookup"><span data-stu-id="c9764-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="c9764-111">我們使用「任一傳播」網路，所以每個 DNS 查詢是由最接近的可用 DNS 伺服器回答。</span><span class="sxs-lookup"><span data-stu-id="c9764-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="c9764-112">這為您的網域提供快速的效能與高可用性。</span><span class="sxs-lookup"><span data-stu-id="c9764-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="c9764-113">**緊密整合** - Azure DNS 服務可用為您 Azure 服務管理 DNS 記錄，也可用來為您的外部資源提供 DNS。</span><span class="sxs-lookup"><span data-stu-id="c9764-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="c9764-114">Azure DNS 已在 Azure 入口網站中整合，並且使用與您其他 Azure 服務相同的認證、計費及支援合約。</span><span class="sxs-lookup"><span data-stu-id="c9764-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="c9764-115">**安全性** - Azure DNS 服務是以 Azure Resource Manager 為基礎。</span><span class="sxs-lookup"><span data-stu-id="c9764-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="c9764-116">因此可得益於 Resource Manager 的功能，如角色型存取控制、稽核記錄檔、資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="c9764-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="c9764-117">您可以透過 Azure 入口網站、Azure PowerShell Cmdlet 和跨平台 Azure CLI 來管理網域和記錄。</span><span class="sxs-lookup"><span data-stu-id="c9764-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="c9764-118">需要自動化 DNS 管理的應用程式可以透過 REST API 和 SDK 與服務進行整合。</span><span class="sxs-lookup"><span data-stu-id="c9764-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="c9764-119">Azure DNS 目前不支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="c9764-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="c9764-120">若想要購買網域，必須洽詢第三方網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="c9764-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="c9764-121">註冊機構通常會收取些微年費。</span><span class="sxs-lookup"><span data-stu-id="c9764-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="c9764-122">然後便可以在 Azure DNS 裝載這些網域來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="c9764-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="c9764-123">如需詳細資訊，請參閱 [將網域委派給 Azure DNS](dns-domain-delegation.md) 。</span><span class="sxs-lookup"><span data-stu-id="c9764-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="c9764-124">價格</span><span class="sxs-lookup"><span data-stu-id="c9764-124">Pricing</span></span>

<span data-ttu-id="c9764-125">DNS 的計費方式是依據 Azure 中裝載的 DNS 區域數量，以及 DNS 查詢的數量。</span><span class="sxs-lookup"><span data-stu-id="c9764-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="c9764-126">若要深入瞭解定價，請瀏覽 [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="c9764-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="c9764-127">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c9764-127">FAQ</span></span>

<span data-ttu-id="c9764-128">如需有關 Azure DNS 的常見問題集，請參閱 [Azure DNS 常見問題集](dns-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="c9764-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9764-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9764-129">Next steps</span></span>

<span data-ttu-id="c9764-130">如需深入了解 DNS 區域和記錄，請瀏覽：[DNS 區域和記錄的概觀](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="c9764-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="c9764-131">了解如何在 Azure DNS 中[建立 DNS 區域](./dns-getstarted-create-dnszone-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c9764-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="c9764-132">深入了解 Azure 的一些其他重要[網路功能](../networking/networking-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c9764-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

