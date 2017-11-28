---
title: "aaaUnderstanding Azure 堆疊中的 DNS |Microsoft 文件"
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
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="b8828-103">適用於 Azure Stack 的 iDNS 簡介</span><span class="sxs-lookup"><span data-stu-id="b8828-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="b8828-104">Idn 是 tooresolve 外部 DNS 名稱 （例如 http://www.bing.com) 可讓您的 Azure 堆疊中的功能。</span><span class="sxs-lookup"><span data-stu-id="b8828-104">iDNS is a feature in Azure Stack that allows you tooresolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="b8828-105">它也可讓您 tooregister 內部虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="b8828-105">It also allows you tooregister internal virtual network names.</span></span> <span data-ttu-id="b8828-106">如此一來，您可以在相同的虛擬網路名稱，而不是 IP 位址，而不需要自訂 DNS 伺服器項目 tooprovide hello 解決 Vm。</span><span class="sxs-lookup"><span data-stu-id="b8828-106">By doing so, you can resolve VMs on hello same virtual network by name rather than IP address, without having tooprovide custom DNS server entries.</span></span>

<span data-ttu-id="b8828-107">這是 Azure 中的內建功能，但是也可以在 Windows Server 2016 和 Azure Stack 中使用。</span><span class="sxs-lookup"><span data-stu-id="b8828-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="b8828-108">iDNS 的用途為何？</span><span class="sxs-lookup"><span data-stu-id="b8828-108">What does iDNS do?</span></span>
<span data-ttu-id="b8828-109">透過 Azure 堆疊中的 Idn，您可以取得下列功能，而不需要自訂 DNS 伺服器項目 toospecify hello。</span><span class="sxs-lookup"><span data-stu-id="b8828-109">With iDNS in Azure Stack, you get hello following capabilities, without having toospecify custom DNS server entries.</span></span>

* <span data-ttu-id="b8828-110">適用於租用戶工作負載的共用 DNS 名稱解析服務。</span><span class="sxs-lookup"><span data-stu-id="b8828-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="b8828-111">名稱解析和 hello 租用戶虛擬網路內的 DNS 登錄的授權 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="b8828-111">Authoritative DNS service for name resolution and DNS registration within hello tenant virtual network.</span></span>
* <span data-ttu-id="b8828-112">從租用戶 VM 解析網際網路名稱的遞迴 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="b8828-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="b8828-113">租用戶不再需要 toospecify 自訂 DNS 項目 tooresolve 網際網路名稱 (例如，www.bing.com)。</span><span class="sxs-lookup"><span data-stu-id="b8828-113">Tenants no longer need toospecify custom DNS entries tooresolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="b8828-114">您仍然可以沿用您自己的 DNS，也可以使用自訂的 DNS 伺服器 (如果您想要的話)。</span><span class="sxs-lookup"><span data-stu-id="b8828-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="b8828-115">但現在，如果您只想 toobe 無法 tooresolve 網際網路 DNS 名稱，而且可以 tooconnect tooother 虛擬機器中的 hello 相同虛擬網路，您不需要 toospecify 任何項目而且也能夠運作。</span><span class="sxs-lookup"><span data-stu-id="b8828-115">But now, if you just want toobe able tooresolve Internet DNS names and be able tooconnect tooother virtual machines in hello same virtual network, you don’t need toospecify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="b8828-116">iDNS 不適用於哪些用途？</span><span class="sxs-lookup"><span data-stu-id="b8828-116">What does iDNS not do?</span></span>
<span data-ttu-id="b8828-117">哪些 Idn 不允許您 toodo 是建立可從外部 hello 虛擬網路解析的名稱的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="b8828-117">What iDNS does not allow you toodo is create a DNS record for a name that can be resolved from outside hello virtual network.</span></span>

<span data-ttu-id="b8828-118">在 Azure 中，您可以 hello 選擇指定的公用 IP 位址與相關聯的 DNS 名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="b8828-118">In Azure, you have hello option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="b8828-119">您可以選擇 hello 標籤 （前置詞），但 Azure 選擇 hello 後置詞，您可以在其中建立 hello 公用 IP 位址的 hello 區域為基礎。</span><span class="sxs-lookup"><span data-stu-id="b8828-119">You can choose hello label (prefix), but Azure chooses hello suffix, which is based on hello region in which you create hello public IP address.</span></span>

![DNS 名稱標籤的螢幕擷取畫面](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="b8828-121">Hello 在圖中，Azure 會建立"A"記錄在 DNS 中的 hello hello 區域底下指定的 DNS 名稱標籤**westus.cloudapp.azure.com**。前置詞和 hello 尾碼一起構成完整限定網域名稱 (FQDN)，可以從任何地方解決的 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="b8828-121">In hello image above, Azure will create an “A” record in DNS for hello DNS name label specified under hello zone **westus.cloudapp.azure.com**. The prefix and hello suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on hello public Internet.</span></span>

<span data-ttu-id="b8828-122">Azure 堆疊只支援 Idn 的內部名稱登錄，因此無法 hello 遵循。</span><span class="sxs-lookup"><span data-stu-id="b8828-122">Azure Stack only supports iDNS for internal name registration, so it cannot do hello following.</span></span>

* <span data-ttu-id="b8828-123">在現有的託管 DNS 區域 (例如 local.azurestack.external) 底下建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="b8828-123">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="b8828-124">建立 DNS 區域 (例如 Contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="b8828-124">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="b8828-125">在您自己的自訂 DNS 區域底下建立記錄。</span><span class="sxs-lookup"><span data-stu-id="b8828-125">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="b8828-126">支援 hello 購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b8828-126">Support hello purchase of domain names.</span></span>

