---
title: "aaaProtecting Azure 資訊安全中心 中的您網路 |Microsoft 文件"
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
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="50b84-103">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="50b84-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="50b84-104">Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="50b84-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="50b84-105">當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。</span><span class="sxs-lookup"><span data-stu-id="50b84-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="50b84-106">適用於建議 tooAzure 資源類型： SQL，以及應用程式網路的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="50b84-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="50b84-107">本文適用 tooyour 網路的建議。</span><span class="sxs-lookup"><span data-stu-id="50b84-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="50b84-108">網路建議圍繞在新一代防火牆、網路安全性群組、設定輸入流量規則等等。</span><span class="sxs-lookup"><span data-stu-id="50b84-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="50b84-109">使用 hello 表當做參考 toohelp 您了解 hello 可用網路的建議，每個用途如果您將其套用。</span><span class="sxs-lookup"><span data-stu-id="50b84-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="50b84-110">可用的網路建議</span><span class="sxs-lookup"><span data-stu-id="50b84-110">Available network recommendations</span></span>
| <span data-ttu-id="50b84-111">建議</span><span class="sxs-lookup"><span data-stu-id="50b84-111">Recommendation</span></span> | <span data-ttu-id="50b84-112">說明</span><span class="sxs-lookup"><span data-stu-id="50b84-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="50b84-113">新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="50b84-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="50b84-114">建議您將加入 下一步產生防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護。</span><span class="sxs-lookup"><span data-stu-id="50b84-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="50b84-115">僅透過 NGFW 路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="50b84-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="50b84-116">建議您設定網路安全性群組 (NSG) 規則強制傳入的流量 tooyour 透過您 NGFW VM。</span><span class="sxs-lookup"><span data-stu-id="50b84-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="50b84-117">啟用子網路/虛擬機器上的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="50b84-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="50b84-118">建議您在子網路或 VM 上啟用 NSG。</span><span class="sxs-lookup"><span data-stu-id="50b84-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="50b84-119">透過網際網路面向端點限制存取</span><span class="sxs-lookup"><span data-stu-id="50b84-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="50b84-120">建議您為 NSG 設定輸入流量規則。</span><span class="sxs-lookup"><span data-stu-id="50b84-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="50b84-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="50b84-121">See also</span></span>
<span data-ttu-id="50b84-122">toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="50b84-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="50b84-123">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="50b84-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="50b84-124">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="50b84-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="50b84-125">保護 Azure 資訊安全中心內的 Azure SQL 服務</span><span class="sxs-lookup"><span data-stu-id="50b84-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="50b84-126">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="50b84-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="50b84-127">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="50b84-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="50b84-128">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="50b84-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="50b84-129">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="50b84-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
