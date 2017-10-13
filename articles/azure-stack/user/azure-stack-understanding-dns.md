---
title: "了解 Azure Stack 中的 DNS | Microsoft Docs"
description: "了解 Azure Stack 中的 DNS 特性與功能"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: scottnap
ms.openlocfilehash: 8c023eda179ace41a082bf4a4fadc281c14db7ba
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="69487-103">適用於 Azure Stack 的 iDNS 簡介</span><span class="sxs-lookup"><span data-stu-id="69487-103">Introducing iDNS for Azure Stack</span></span>

<span data-ttu-id="69487-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="69487-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="69487-105">iDNS 是 Azure Stack 中的一個功能，可讓您解析外部 DNS 名稱 (例如 http://www.bing.com)。</span><span class="sxs-lookup"><span data-stu-id="69487-105">iDNS is a feature in Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="69487-106">它也可以讓您登錄內部虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="69487-106">It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="69487-107">如此一來，您就可以依名稱 (而非 IP 位址) 解析相同虛擬網路上的 VM，而不需要提供自訂的 DNS 伺服器項目。</span><span class="sxs-lookup"><span data-stu-id="69487-107">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span></span>

<span data-ttu-id="69487-108">這是 Azure 中的內建功能，但是也可以在 Windows Server 2016 和 Azure Stack 中使用。</span><span class="sxs-lookup"><span data-stu-id="69487-108">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="69487-109">iDNS 的用途為何？</span><span class="sxs-lookup"><span data-stu-id="69487-109">What does iDNS do?</span></span>
<span data-ttu-id="69487-110">您可以使用 Azure Stack 中的 iDNS 取得下列功能，而不需要指定自訂的 DNS 伺服器項目。</span><span class="sxs-lookup"><span data-stu-id="69487-110">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span></span>

* <span data-ttu-id="69487-111">適用於租用戶工作負載的共用 DNS 名稱解析服務。</span><span class="sxs-lookup"><span data-stu-id="69487-111">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="69487-112">適用於租用戶虛擬網路內的名稱解析和 DNS 登錄的權威 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="69487-112">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
* <span data-ttu-id="69487-113">從租用戶 VM 解析網際網路名稱的遞迴 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="69487-113">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="69487-114">租用戶不再需要指定自訂的 DNS 項目，就可以解析網際網路名稱 (例如 www.bing.com)。</span><span class="sxs-lookup"><span data-stu-id="69487-114">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="69487-115">您仍然可以沿用您自己的 DNS，也可以使用自訂的 DNS 伺服器 (如果您想要的話)。</span><span class="sxs-lookup"><span data-stu-id="69487-115">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="69487-116">但現在，如果您只想要能夠解析網際網路 DNS 名稱，而且能夠連線到相同虛擬網路中的其他虛擬機器，則您不需要指定任何項目也能夠運作。</span><span class="sxs-lookup"><span data-stu-id="69487-116">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="69487-117">iDNS 不適用於哪些用途？</span><span class="sxs-lookup"><span data-stu-id="69487-117">What does iDNS not do?</span></span>
<span data-ttu-id="69487-118">iDNS 不允許您針對可以從虛擬網路外部解析的名稱，建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="69487-118">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="69487-119">在 Azure 中，您可以選擇指定能夠與公用 IP 位址相關聯的 DNS 名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="69487-119">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="69487-120">您可以選擇標籤 (首碼)，但 Azure 會根據您建立公用 IP 位址所在的區域，選擇尾碼。</span><span class="sxs-lookup"><span data-stu-id="69487-120">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![DNS 名稱標籤的螢幕擷取畫面](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="69487-122">在上圖中，Azure 將會在 DNS 中，為區域 **westus.cloudapp.azure.com** 底下指定的 DNS 名稱標籤，建立 “A” 記錄。首碼和尾碼可構成完整網域名稱 (FQDN)，此名稱可以從公用網際網路上的任何位置解析。</span><span class="sxs-lookup"><span data-stu-id="69487-122">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**. The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="69487-123">Azure Stack 僅支援用於內部名稱登錄的 iDNS，因此無法執行下列作業。</span><span class="sxs-lookup"><span data-stu-id="69487-123">Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span></span>

* <span data-ttu-id="69487-124">在現有的託管 DNS 區域 (例如 local.azurestack.external) 底下建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="69487-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="69487-125">建立 DNS 區域 (例如 Contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="69487-125">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="69487-126">在您自己的自訂 DNS 區域底下建立記錄。</span><span class="sxs-lookup"><span data-stu-id="69487-126">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="69487-127">支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="69487-127">Support the purchase of domain names.</span></span>

