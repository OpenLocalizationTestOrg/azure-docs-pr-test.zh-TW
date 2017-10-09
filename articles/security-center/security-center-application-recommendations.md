---
title: "aaaProtecting Azure 資訊安全中心中的應用程式 |Microsoft 文件"
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
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a><span data-ttu-id="8da57-103">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="8da57-103">Protecting your applications in Azure Security Center</span></span>
<span data-ttu-id="8da57-104">Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="8da57-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="8da57-105">當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。</span><span class="sxs-lookup"><span data-stu-id="8da57-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="8da57-106">適用於建議 tooAzure 資源類型： SQL，以及應用程式網路的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="8da57-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="8da57-107">本文適用 tooapplications 的建議。</span><span class="sxs-lookup"><span data-stu-id="8da57-107">This article addresses recommendations that apply tooapplications.</span></span>  <span data-ttu-id="8da57-108">應用程式建議圍繞在 Web 應用程式防火牆的部署。</span><span class="sxs-lookup"><span data-stu-id="8da57-108">Application recommendations center around deployment of a web application firewall.</span></span>  <span data-ttu-id="8da57-109">使用 hello 表當做參考 toohelp 您了解 hello 可用的應用程式的建議，每個用途如果您將其套用。</span><span class="sxs-lookup"><span data-stu-id="8da57-109">Use hello table below as a reference toohelp you understand hello available application recommendations and what each one does if you apply it.</span></span>

## <a name="available-application-recommendations"></a><span data-ttu-id="8da57-110">可用的應用程式建議</span><span class="sxs-lookup"><span data-stu-id="8da57-110">Available application recommendations</span></span>
| <span data-ttu-id="8da57-111">建議</span><span class="sxs-lookup"><span data-stu-id="8da57-111">Recommendation</span></span> | <span data-ttu-id="8da57-112">說明</span><span class="sxs-lookup"><span data-stu-id="8da57-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="8da57-113">新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="8da57-113">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md) |<span data-ttu-id="8da57-114">建議您為 Web 端點部署「Web 應用程式防火牆」(WAF)。</span><span class="sxs-lookup"><span data-stu-id="8da57-114">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span></span> <span data-ttu-id="8da57-115">系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。</span><span class="sxs-lookup"><span data-stu-id="8da57-115">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span></br></br><span data-ttu-id="8da57-116">資訊安全中心建議您佈建 WAF toohelp 防禦目標 web 應用程式的 App Service 環境和虛擬機器上的攻擊。</span><span class="sxs-lookup"><span data-stu-id="8da57-116">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="8da57-117">App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8da57-117">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="8da57-118">toolearn 深入了解 ASE，請參閱 hello[應用程式服務環境的文件](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="8da57-118">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span></br></br><span data-ttu-id="8da57-119">您可以藉由新增這些應用程式 tooyour 現有 WAF 部署保護的資訊安全中心中的多個 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8da57-119">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span> |
| [<span data-ttu-id="8da57-120">完成應用程式保護</span><span class="sxs-lookup"><span data-stu-id="8da57-120">Finalize application protection</span></span>](security-center-add-web-application-firewall.md#finalize-application-protection) |<span data-ttu-id="8da57-121">toocomplete hello 的 WAF，流量必須路由的 toohello WAF 應用裝置。</span><span class="sxs-lookup"><span data-stu-id="8da57-121">toocomplete hello configuration of a WAF, traffic must be rerouted toohello WAF appliance.</span></span> <span data-ttu-id="8da57-122">遵循這個建議完成 hello 必要的設定變更。</span><span class="sxs-lookup"><span data-stu-id="8da57-122">Following this recommendation completes hello necessary setup changes.</span></span> |

## <a name="see-also"></a><span data-ttu-id="8da57-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8da57-123">See also</span></span>
<span data-ttu-id="8da57-124">toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8da57-124">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="8da57-125">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8da57-125">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="8da57-126">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="8da57-126">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="8da57-127">保護 Azure 資訊安全中心內的 Azure SQL 服務</span><span class="sxs-lookup"><span data-stu-id="8da57-127">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="8da57-128">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8da57-128">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="8da57-129">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="8da57-129">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8da57-130">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="8da57-130">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8da57-131">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="8da57-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
