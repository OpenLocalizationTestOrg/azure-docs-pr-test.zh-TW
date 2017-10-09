---
title: "aaaAdd Azure 資訊安全中心中的 web 應用程式防火牆 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 加入 web 應用程式防火牆 * * 和 * * 完成應用程式保護 * *。"
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
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="d9d7c-103">在 Azure 資訊安全中心新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="d9d7c-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="d9d7c-104">Azure 資訊安全中心可能會建議您新增的 web 應用程式的防火牆 (WAF) 從 Microsoft 夥伴 toosecure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner toosecure your web applications.</span></span> <span data-ttu-id="d9d7c-105">本文件將逐步引導您透過如何的範例 tooapply 這項建議。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-105">This document walks you through an example of how tooapply this recommendation.</span></span>

<span data-ttu-id="d9d7c-106">系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="d9d7c-107">資訊安全中心建議您佈建 WAF toohelp 防禦目標 web 應用程式的 App Service 環境和虛擬機器上的攻擊。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-107">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="d9d7c-108">App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="d9d7c-109">toolearn 深入了解 ASE，請參閱 hello[應用程式服務環境的文件](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-109">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9d7c-110">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="d9d7c-111">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d9d7c-112">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="d9d7c-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="d9d7c-113">在 hello**建議**刀鋒視窗中，選取**保護 web 應用程式使用 web 應用程式防火牆**。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-113">In hello **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="d9d7c-114">![保護 Web 應用程式][1]</span><span class="sxs-lookup"><span data-stu-id="d9d7c-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="d9d7c-115">在 hello**保護您的 web 應用程式使用 web 應用程式防火牆**刀鋒視窗中，選取 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-115">In hello **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="d9d7c-116">hello**加入 Web 應用程式防火牆**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-116">hello **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="d9d7c-117">![新增 Web 應用程式防火牆][2]</span><span class="sxs-lookup"><span data-stu-id="d9d7c-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="d9d7c-118">您可以選擇 toouse 現有 web 應用程式防火牆如果有的話，或您可以建立一個新。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-118">You can choose toouse an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="d9d7c-119">此範例中沒有任何可用的現有 WAF，因此我們會建立一個 WAF。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="d9d7c-120">toocreate WAF，從 hello 整合協力電腦清單中選取方案。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-120">toocreate a WAF, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="d9d7c-121">在此範例中，我們會選取 [Barracuda Web 應用程式防火牆]。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="d9d7c-122">hello **Barracuda Web 應用程式防火牆**刀鋒視窗會開啟提供您 hello 夥伴方案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-122">hello **Barracuda Web Application Firewall** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="d9d7c-123">選取**建立**hello 資訊刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-123">Select **Create** in hello information blade.</span></span>

   ![防火牆資訊刀鋒視窗][3]

6. <span data-ttu-id="d9d7c-125">hello**新的 Web 應用程式防火牆**刀鋒視窗隨即開啟，您可以在其中執行**VM 組態**步驟並提供**WAF 資訊**。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-125">hello **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="d9d7c-126">選取 [VM 組態]。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="d9d7c-127">在 hello **VM 組態**刀鋒視窗中，輸入 hello 虛擬機器執行的必要的 toospin hello WAF 的資訊。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-127">In hello **VM Configuration** blade, you enter information required toospin up hello virtual machine that runs hello WAF.</span></span>
   <span data-ttu-id="d9d7c-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="d9d7c-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="d9d7c-129">傳回 toohello**新的 Web 應用程式防火牆**刀鋒視窗，然後選取**WAF 資訊**。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-129">Return toohello **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="d9d7c-130">在 hello **WAF 資訊**刀鋒視窗中，設定 hello WAF 本身。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-130">In hello **WAF Information** blade, you configure hello WAF itself.</span></span> <span data-ttu-id="d9d7c-131">步驟 7 可讓您在哪個 hello WAF 執行和步驟 8 可讓您 tooprovision hello WAF 本身 tooconfigure hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-131">Step 7 allows you tooconfigure hello virtual machine on which hello WAF runs and step 8 enables you tooprovision hello WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="d9d7c-132">完成應用程式保護</span><span class="sxs-lookup"><span data-stu-id="d9d7c-132">Finalize application protection</span></span>
1. <span data-ttu-id="d9d7c-133">傳回 toohello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-133">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="d9d7c-134">建立 hello WAF，呼叫後產生新的項目**完成應用程式保護**。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-134">A new entry was generated after you created hello WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="d9d7c-135">此項目可讓您知道您需要 toocomplete hello 程序實際上裝設 hello WAF hello Azure 虛擬網路內，讓它可以保護 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-135">This entry lets you know that you need toocomplete hello process of actually wiring up hello WAF within hello Azure Virtual Network so that it can protect hello application.</span></span>

   ![完成應用程式保護][5]

2. <span data-ttu-id="d9d7c-137">選取 [完成應用程式保護] 。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="d9d7c-138">此時會開啟新的分頁。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-138">A new blade opens.</span></span> <span data-ttu-id="d9d7c-139">您可以看到是需要 toohave 其流量重新路由到 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-139">You can see that there is a web application that needs toohave its traffic rerouted.</span></span>
3. <span data-ttu-id="d9d7c-140">選取 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-140">Select hello web application.</span></span> <span data-ttu-id="d9d7c-141">刀鋒視窗隨即開啟，可讓您的正在完成 hello web 應用程式防火牆安裝的步驟。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-141">A blade opens that gives you steps for finalizing hello web application firewall setup.</span></span> <span data-ttu-id="d9d7c-142">完成 hello 步驟，然後選取 **限制流量**。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-142">Complete hello steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="d9d7c-143">資訊安全中心未 hello 配線接您。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-143">Security Center then does hello wiring-up for you.</span></span>

   ![限制流量][6]

> [!NOTE]
> <span data-ttu-id="d9d7c-145">您可以藉由新增這些應用程式 tooyour 現有 WAF 部署保護的資訊安全中心中的多個 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-145">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span>
>
>

<span data-ttu-id="d9d7c-146">現在完全整合，從該 WAF hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-146">hello logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="d9d7c-147">資訊安全中心可以啟動自動收集和分析 hello 記錄檔，如此它就會出現重要的安全性警示 tooyou。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-147">Security Center can start automatically gathering and analyzing hello logs so that it can surface important security alerts tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d7c-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9d7c-148">Next steps</span></span>
<span data-ttu-id="d9d7c-149">這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 新增 web 應用程式 」。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-149">This document showed you how tooimplement hello Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="d9d7c-150">toolearn 進一步了解設定 web 應用程式防火牆，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d9d7c-150">toolearn more about configuring a web application firewall, see hello following:</span></span>

* [<span data-ttu-id="d9d7c-151">設定 App Service 環境的 Web 應用程式防火牆 (WAF)</span><span class="sxs-lookup"><span data-stu-id="d9d7c-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="d9d7c-152">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d9d7c-152">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d9d7c-153">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d9d7c-154">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d9d7c-155">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-155">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d9d7c-156">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d9d7c-157">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d9d7c-158">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="d9d7c-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
