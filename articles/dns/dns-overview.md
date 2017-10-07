---
title: "Azure DNS 的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="4bc01-104">Azure DNS 概觀</span><span class="sxs-lookup"><span data-stu-id="4bc01-104">Azure DNS overview</span></span>

<span data-ttu-id="4bc01-105">hello 網域名稱系統或 DNS，負責將轉譯 （或解決） 的網站或服務名稱 tooits IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4bc01-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="4bc01-106">Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="4bc01-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="4bc01-107">裝載您在 Azure 中的網域，您可以管理您的 DNS 記錄使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4bc01-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS 概觀](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="4bc01-109">特性</span><span class="sxs-lookup"><span data-stu-id="4bc01-109">Features</span></span>

* <span data-ttu-id="4bc01-110">**可靠性和效能** - Azure DNS 中的 DNS 網域是裝載於 Azure 的 DNS 名稱伺服器全球網路。</span><span class="sxs-lookup"><span data-stu-id="4bc01-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="4bc01-111">我們使用任一傳播網路，讓每個 DNS 查詢由 hello 最接近可用 DNS 伺服器回應。</span><span class="sxs-lookup"><span data-stu-id="4bc01-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="4bc01-112">這為您的網域提供快速的效能與高可用性。</span><span class="sxs-lookup"><span data-stu-id="4bc01-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="4bc01-113">**緊密整合**-hello Azure DNS 服務可以使用的 toomanage Azure 服務的 DNS 記錄，而且可以是使用的 tooprovide DNS，針對您外部的資源。</span><span class="sxs-lookup"><span data-stu-id="4bc01-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="4bc01-114">Azure DNS 整合 hello Azure 入口網站中，而且會使用相同的認證、 帳單和支援合約 hello 與其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4bc01-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="4bc01-115">**安全性**-hello Azure DNS 服務採用 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="4bc01-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="4bc01-116">因此可得益於 Resource Manager 的功能，如角色型存取控制、稽核記錄檔、資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="4bc01-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="4bc01-117">您的網域和記錄可以透過 hello Azure 入口網站，Azure PowerShell cmdlet，管理和 hello 跨平台 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="4bc01-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="4bc01-118">需要 DNS 的自動管理的應用程式可以整合透過 hello hello 服務 REST API 和 Sdk。</span><span class="sxs-lookup"><span data-stu-id="4bc01-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="4bc01-119">Azure DNS 目前不支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4bc01-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="4bc01-120">如果您想 toopurchase 網域時，您會需要 toouse 第三方網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="4bc01-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="4bc01-121">hello 註冊機構通常費用小年費。</span><span class="sxs-lookup"><span data-stu-id="4bc01-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="4bc01-122">hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="4bc01-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="4bc01-123">請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4bc01-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="4bc01-124">價格</span><span class="sxs-lookup"><span data-stu-id="4bc01-124">Pricing</span></span>

<span data-ttu-id="4bc01-125">DNS 計費根據裝載在 Azure 中並以 hello 的 DNS 查詢的 DNS 區域的 hello 數目而定。</span><span class="sxs-lookup"><span data-stu-id="4bc01-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="4bc01-126">深入了解定價，請造訪 toolearn [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="4bc01-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="4bc01-127">常見問題集</span><span class="sxs-lookup"><span data-stu-id="4bc01-127">FAQ</span></span>

<span data-ttu-id="4bc01-128">常見問題集疑問 Azure DNS 的詳細資訊，請參閱 hello [Azure DNS 常見問題集](dns-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="4bc01-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bc01-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bc01-129">Next steps</span></span>

<span data-ttu-id="4bc01-130">如需深入了解 DNS 區域和記錄，請瀏覽：[DNS 區域和記錄的概觀](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="4bc01-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="4bc01-131">了解如何太[建立 DNS 區域](./dns-getstarted-create-dnszone-portal.md)Azure DNS 中。</span><span class="sxs-lookup"><span data-stu-id="4bc01-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="4bc01-132">深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。</span><span class="sxs-lookup"><span data-stu-id="4bc01-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

