---
title: "在 Azure 資訊安全中心新增 Web 應用程式防火牆 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「新增 Web 應用程式防火牆」和「完成應用程式保護」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: d04a07237029953d8a9b20704d85e852ce45d867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="cd064-103">在 Azure 資訊安全中心新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="cd064-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="cd064-104">Azure 資訊安全中心可能會建議您從 Microsoft 合作夥伴新增 Web 應用程式防火牆 (WAF)，以保護您 Web 應用程式的安全。</span><span class="sxs-lookup"><span data-stu-id="cd064-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="cd064-105">本文件逐步解說如何套用此建議的範例。</span><span class="sxs-lookup"><span data-stu-id="cd064-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="cd064-106">系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。</span><span class="sxs-lookup"><span data-stu-id="cd064-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="cd064-107">資訊安全中心建議您佈建 WAF，協助對抗以虛擬機器和 App Service 環境上的 Web 應用程式為目標的攻擊。</span><span class="sxs-lookup"><span data-stu-id="cd064-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="cd064-108">App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="cd064-109">若要深入了解 ASE，請參閱 [App Service 環境的文件](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="cd064-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cd064-110">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="cd064-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="cd064-111">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="cd064-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="cd064-112">實作建議</span><span class="sxs-lookup"><span data-stu-id="cd064-112">Implement the recommendation</span></span>
1. <span data-ttu-id="cd064-113">在 [建議] 刀鋒視窗中，選取 [使用 Web 應用程式防火牆保護 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cd064-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="cd064-114">![保護 Web 應用程式][1]</span><span class="sxs-lookup"><span data-stu-id="cd064-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="cd064-115">在 [使用 Web 應用程式防火牆保護 Web 應用程式]  刀鋒視窗中，選取 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="cd064-116">[新增 Web 應用程式防火牆]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="cd064-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="cd064-117">![Add a web application firewall][2]</span><span class="sxs-lookup"><span data-stu-id="cd064-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="cd064-118">您可以選擇使用現有的 Web 應用程式防火牆 (如果有的話)，或者您可以建立一個新的 Web 應用程式防火牆。</span><span class="sxs-lookup"><span data-stu-id="cd064-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="cd064-119">此範例中沒有任何可用的現有 WAF，因此我們會建立一個 WAF。</span><span class="sxs-lookup"><span data-stu-id="cd064-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="cd064-120">若要建立 WAF，請從整合式合作夥伴的清單中選取一個解決方案。</span><span class="sxs-lookup"><span data-stu-id="cd064-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="cd064-121">在此範例中，我們會選取 [Barracuda Web 應用程式防火牆]。</span><span class="sxs-lookup"><span data-stu-id="cd064-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="cd064-122">[Barracuda Web 應用程式防火牆]  刀鋒視窗隨即開啟，為您提供合作夥伴解決方案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cd064-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="cd064-123">選取資訊刀鋒視窗中的 [建立]  。</span><span class="sxs-lookup"><span data-stu-id="cd064-123">Select **Create** in the information blade.</span></span>

   ![防火牆資訊刀鋒視窗][3]

6. <span data-ttu-id="cd064-125">即會開啟 [新增 Web 應用程式防火牆] 刀鋒視窗，您可以在此視窗中執行 [VM 組態] 步驟並提供 [WAF 資訊]。</span><span class="sxs-lookup"><span data-stu-id="cd064-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="cd064-126">選取 [VM 組態]。</span><span class="sxs-lookup"><span data-stu-id="cd064-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="cd064-127">在 [VM 組態] 刀鋒視窗中，輸入啟動要執行 WAF 之虛擬機器所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="cd064-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="cd064-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="cd064-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="cd064-129">返回 [新增 Web 應用程式防火牆] 刀鋒視窗，然後選取 [WAF 資訊]。</span><span class="sxs-lookup"><span data-stu-id="cd064-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="cd064-130">在 [WAF 資訊] 刀鋒視窗中，設定 WAF 本身。</span><span class="sxs-lookup"><span data-stu-id="cd064-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="cd064-131">步驟 7 可讓您設定要執行 WAF 的虛擬機器，而步驟 8 則可讓您佈建 WAF 本身。</span><span class="sxs-lookup"><span data-stu-id="cd064-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="cd064-132">完成應用程式保護</span><span class="sxs-lookup"><span data-stu-id="cd064-132">Finalize application protection</span></span>
1. <span data-ttu-id="cd064-133">返回 [建議]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cd064-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="cd064-134">在您建立 WAF 之後會產生一個新項目，稱為 [完成應用程式保護] 。</span><span class="sxs-lookup"><span data-stu-id="cd064-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="cd064-135">此項目可讓您知道您需要完成實際串聯起 Azure 虛擬網路內 WAF 的程序，讓它可以保護應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>

   ![完成應用程式保護][5]

2. <span data-ttu-id="cd064-137">選取 [完成應用程式保護] 。</span><span class="sxs-lookup"><span data-stu-id="cd064-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="cd064-138">此時會開啟新的分頁。</span><span class="sxs-lookup"><span data-stu-id="cd064-138">A new blade opens.</span></span> <span data-ttu-id="cd064-139">您會看到有一個需要重新路由流量的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="cd064-140">選取 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-140">Select the web application.</span></span> <span data-ttu-id="cd064-141">將會開啟一個刀鋒視窗，其中提供完成 Web 應用程式防火牆設定的步驟。</span><span class="sxs-lookup"><span data-stu-id="cd064-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="cd064-142">完成這些步驟，然後選取 [限制流量] 。</span><span class="sxs-lookup"><span data-stu-id="cd064-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="cd064-143">接著，資訊安全中心會為您進行串聯。</span><span class="sxs-lookup"><span data-stu-id="cd064-143">Security Center then does the wiring-up for you.</span></span>

   ![限制流量][6]

> [!NOTE]
> <span data-ttu-id="cd064-145">您可以將這些應用程式加入現有的 WAF 部署，以保護資訊安全中心的多個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd064-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="cd064-146">現在已將來自該 WAF 的記錄完全整合。</span><span class="sxs-lookup"><span data-stu-id="cd064-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="cd064-147">「資訊安全中心」可以開始自動收集並分析記錄，以便對您顯示重要的安全性警示。</span><span class="sxs-lookup"><span data-stu-id="cd064-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd064-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd064-148">Next steps</span></span>
<span data-ttu-id="cd064-149">本文件說明如何實作資訊安全中心建議的「新增 Web 應用程式」。</span><span class="sxs-lookup"><span data-stu-id="cd064-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="cd064-150">若要深入了解如何設定 Web 應用程式防火牆，請參閱下列各項：</span><span class="sxs-lookup"><span data-stu-id="cd064-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="cd064-151">設定 App Service 環境的 Web 應用程式防火牆 (WAF)</span><span class="sxs-lookup"><span data-stu-id="cd064-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="cd064-152">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="cd064-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="cd064-153">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="cd064-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="cd064-154">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="cd064-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="cd064-155">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="cd064-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="cd064-156">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="cd064-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="cd064-157">[Azure 安全性中心常見問題集](security-center-faq.md) -- 尋找使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="cd064-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="cd064-158">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="cd064-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
