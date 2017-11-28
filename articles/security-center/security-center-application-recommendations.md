---
title: "保護 Azure 資訊安全中心內的應用程式 | Microsoft Docs"
description: "本文件說明可協助您保護 Azure 應用程式及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: dfc7d14b95082842ba658bd94b15c8191ee5dca3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a><span data-ttu-id="16ac4-103">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="16ac4-103">Protecting your applications in Azure Security Center</span></span>
<span data-ttu-id="16ac4-104">「Azure 資訊安全中心」會分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="16ac4-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="16ac4-105">當資訊安全中心發現潛在的安全性弱點時，它會建立可引導您完成所需控制之設定程序的建議。</span><span class="sxs-lookup"><span data-stu-id="16ac4-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="16ac4-106">這些建議適用於下列 Azure 資源類型︰虛擬機器 (VM)、網路、SQL 和應用程式。</span><span class="sxs-lookup"><span data-stu-id="16ac4-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="16ac4-107">本文說明適用於應用程式的建議。</span><span class="sxs-lookup"><span data-stu-id="16ac4-107">This article addresses recommendations that apply to applications.</span></span>  <span data-ttu-id="16ac4-108">應用程式建議圍繞在 Web 應用程式防火牆的部署。</span><span class="sxs-lookup"><span data-stu-id="16ac4-108">Application recommendations center around deployment of a web application firewall.</span></span>  <span data-ttu-id="16ac4-109">請使用下表做為參考，以協助您了解可用的應用程式建議，以及如果套用建議，每一個建議將產生的作用。</span><span class="sxs-lookup"><span data-stu-id="16ac4-109">Use the table below as a reference to help you understand the available application recommendations and what each one does if you apply it.</span></span>

## <a name="available-application-recommendations"></a><span data-ttu-id="16ac4-110">可用的應用程式建議</span><span class="sxs-lookup"><span data-stu-id="16ac4-110">Available application recommendations</span></span>
| <span data-ttu-id="16ac4-111">建議</span><span class="sxs-lookup"><span data-stu-id="16ac4-111">Recommendation</span></span> | <span data-ttu-id="16ac4-112">說明</span><span class="sxs-lookup"><span data-stu-id="16ac4-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="16ac4-113">新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="16ac4-113">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md) |<span data-ttu-id="16ac4-114">建議您為 Web 端點部署「Web 應用程式防火牆」(WAF)。</span><span class="sxs-lookup"><span data-stu-id="16ac4-114">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span></span> <span data-ttu-id="16ac4-115">系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。</span><span class="sxs-lookup"><span data-stu-id="16ac4-115">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span></br></br><span data-ttu-id="16ac4-116">資訊安全中心建議您佈建 WAF，協助對抗以虛擬機器和 App Service 環境上的 Web 應用程式為目標的攻擊。</span><span class="sxs-lookup"><span data-stu-id="16ac4-116">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="16ac4-117">App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16ac4-117">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="16ac4-118">若要深入了解 ASE，請參閱 [App Service 環境的文件](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="16ac4-118">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span></br></br><span data-ttu-id="16ac4-119">您可以將這些應用程式加入現有的 WAF 部署，以保護資訊安全中心的多個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16ac4-119">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span> |
| [<span data-ttu-id="16ac4-120">完成應用程式保護</span><span class="sxs-lookup"><span data-stu-id="16ac4-120">Finalize application protection</span></span>](security-center-add-web-application-firewall.md#finalize-application-protection) |<span data-ttu-id="16ac4-121">若要完成 WAF 組態，必須將流量重新路由至 WAF 設備。</span><span class="sxs-lookup"><span data-stu-id="16ac4-121">To complete the configuration of a WAF, traffic must be rerouted to the WAF appliance.</span></span> <span data-ttu-id="16ac4-122">遵循這項建議會完成必要的設定變更。</span><span class="sxs-lookup"><span data-stu-id="16ac4-122">Following this recommendation completes the necessary setup changes.</span></span> |

## <a name="see-also"></a><span data-ttu-id="16ac4-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16ac4-123">See also</span></span>
<span data-ttu-id="16ac4-124">若要深入了解適用於其他 Azure 資源類型的建議，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="16ac4-124">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="16ac4-125">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="16ac4-125">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="16ac4-126">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="16ac4-126">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="16ac4-127">保護 Azure 資訊安全中心內的 Azure SQL 服務</span><span class="sxs-lookup"><span data-stu-id="16ac4-127">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="16ac4-128">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="16ac4-128">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="16ac4-129">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) -- 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="16ac4-129">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="16ac4-130">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="16ac4-130">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="16ac4-131">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="16ac4-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
