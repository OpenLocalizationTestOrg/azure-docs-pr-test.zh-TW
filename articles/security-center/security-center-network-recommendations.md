---
title: "保護 Azure 資訊安全中心內的網路 | Microsoft Docs"
description: "本文件說明可協助您保護 Azure 網路及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="bf974-103">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="bf974-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="bf974-104">「Azure 資訊安全中心」會分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="bf974-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="bf974-105">當資訊安全中心發現潛在的安全性弱點時，它會建立可引導您完成所需控制之設定程序的建議。</span><span class="sxs-lookup"><span data-stu-id="bf974-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="bf974-106">這些建議適用於下列 Azure 資源類型︰虛擬機器 (VM)、網路、SQL 和應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf974-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="bf974-107">本文說明適用於網路的建議。</span><span class="sxs-lookup"><span data-stu-id="bf974-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="bf974-108">網路建議圍繞在新一代防火牆、網路安全性群組、設定輸入流量規則等等。</span><span class="sxs-lookup"><span data-stu-id="bf974-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="bf974-109">請使用下表做為參考，以協助您了解可用的網路建議，以及如果套用建議，每一個建議將產生的作用。</span><span class="sxs-lookup"><span data-stu-id="bf974-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="bf974-110">可用的網路建議</span><span class="sxs-lookup"><span data-stu-id="bf974-110">Available network recommendations</span></span>
| <span data-ttu-id="bf974-111">建議</span><span class="sxs-lookup"><span data-stu-id="bf974-111">Recommendation</span></span> | <span data-ttu-id="bf974-112">說明</span><span class="sxs-lookup"><span data-stu-id="bf974-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bf974-113">新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="bf974-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="bf974-114">建議您新增由 Microsoft 合作夥伴提供的新一代防火牆 (NGFW)，以提升您的安全防護。</span><span class="sxs-lookup"><span data-stu-id="bf974-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="bf974-115">僅透過 NGFW 路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="bf974-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="bf974-116">建議您設定網路安全性群組 (NSG) 規則，強制透過您的 NGFW 傳送內送流量到 VM。</span><span class="sxs-lookup"><span data-stu-id="bf974-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="bf974-117">啟用子網路/虛擬機器上的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="bf974-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="bf974-118">建議您在子網路或 VM 上啟用 NSG。</span><span class="sxs-lookup"><span data-stu-id="bf974-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="bf974-119">透過網際網路面向端點限制存取</span><span class="sxs-lookup"><span data-stu-id="bf974-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="bf974-120">建議您為 NSG 設定輸入流量規則。</span><span class="sxs-lookup"><span data-stu-id="bf974-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="bf974-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bf974-121">See also</span></span>
<span data-ttu-id="bf974-122">若要深入了解適用於其他 Azure 資源類型的建議，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="bf974-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="bf974-123">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bf974-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="bf974-124">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="bf974-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="bf974-125">保護 Azure 資訊安全中心內的 Azure SQL 服務</span><span class="sxs-lookup"><span data-stu-id="bf974-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="bf974-126">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="bf974-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="bf974-127">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) -- 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="bf974-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bf974-128">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="bf974-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="bf974-129">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="bf974-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
