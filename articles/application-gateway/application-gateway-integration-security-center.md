---
title: "應用程式閘道與 Azure 資訊安全中心整合 | Microsoft Docs"
description: "此頁面提供如何將應用程式閘道整合到 Azure 資訊安全中心的相關資訊。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="c0fd9-103">應用程式閘道與 Azure 資訊安全中心整合概觀</span><span class="sxs-lookup"><span data-stu-id="c0fd9-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="c0fd9-104">了解如何使用應用程式閘道和資訊安全中心如何保護您的 Web 應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="c0fd9-105">應用程式閘道 Web 應用程式防火牆 (WAF) 與[資訊安全中心](../security-center/security-center-intro.md)整合可提供無落差的檢視，以防止、偵測及回應環境中針對未受保護 Web 應用程式的威脅。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="c0fd9-106">概觀</span><span class="sxs-lookup"><span data-stu-id="c0fd9-106">Overview</span></span>

<span data-ttu-id="c0fd9-107">建議在資訊安全中心使用應用程式閘道 WAF，以保護 Web 應用程式議抵禦入侵和弱點。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="c0fd9-108">已啟用 Web 的資源若沒有受到 WAF 的保護，資訊安全中心會建議它是高嚴重性。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="c0fd9-109">使用 Web 應用程式防火牆的建議會出現在 [概觀] 頁面的 [應用程式] 底下。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![與資訊安全中心整合][1]

<span data-ttu-id="c0fd9-111">按一下任何與 Web 應用程式防火牆相關的建議會開啟新的刀鋒視窗，其中顯示建議的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="c0fd9-112">將 Web 應用程式防火牆新增至現有資源</span><span class="sxs-lookup"><span data-stu-id="c0fd9-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="c0fd9-113">瀏覽至 [更多服務]  >  [安全性 + 身分識別]  >  [資訊安全中心]，在 [資訊安全中心-概觀] 刀鋒視窗中按一下 [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="c0fd9-114">在 [資訊安全中心 - 應用程式] 刀鋒視窗中，資料表包含資訊安全中心在您的訂用帳戶中偵測到的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![Web 應用程式][3]

<span data-ttu-id="c0fd9-116">按一下有嚴重問題的 Web 應用程式，您會看到 [應用程式安全性健康情況] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="c0fd9-117">在下圖中，Web 應用程式沒有 Web 應用程式防火牆的保護。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![未受保護的 Web 資源][2]

<span data-ttu-id="c0fd9-119">按一下 [建議] 底下的 [新增 Web 應用程式防火牆] 以開啟 [新增 Web 應用程式防火牆] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="c0fd9-120">如果您還沒有應用程式閘道或想要建立新的，按一下 [新建]，在 [建立新的 Web 應用程式防火牆] 刀鋒視窗中，按一下 [Microsoft - 應用程式閘道]。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="c0fd9-121">這會帶您開始建立應用程式閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="c0fd9-122">此時，您的 Web 應用程式已新增為受保護的資源，資訊安全中心現在會追蹤這個受到 Web 應用程式防火牆保護的資源。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="c0fd9-123">這不會將它新增為後端集區的成員。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="c0fd9-124">如果您有現有的應用程式閘道，您可以在 [使用現有的解決方案] 中選擇它。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![新增 Web 應用程式防火牆刀鋒視窗][4]

<span data-ttu-id="c0fd9-126">透過資訊安全中心將 Web 應用程式新增至應用程式閘道，不會將此資源新增為後端集區成員，這必須在應用程式閘道資源上直接設定。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="c0fd9-127">將資源新增至現有 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="c0fd9-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="c0fd9-128">瀏覽至 [更多服務]  >  [安全性 + 身分識別]  >  [資訊安全中心]，在 [資訊安全中心-概觀] 刀鋒視窗中按一下 [合作夥伴解決方案]。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="c0fd9-129">在 [合作夥伴解決方案] 刀鋒視窗中會顯示現有的資訊安全中心感知應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![合作夥伴解決方案][7]

<span data-ttu-id="c0fd9-131">按一下 [連結應用程式] 開啟 [連結應用程式] 刀鋒視窗，您可以在此選取現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="c0fd9-132">選擇要保護的應用程式，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="c0fd9-133">這不會將 Web 應用程式新增至應用程式閘道的後端集區。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="c0fd9-134">這會將資源設定為受保護的資源，讓資訊安全中心能夠追蹤它。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="c0fd9-135">若要將資源新增為後端集區成員，必須在應用程式閘道上完成，在眼前的刀鋒視窗中按一下 [解決方案主控台] 會帶您前往此應用程式閘道資源，讓您將 Web 應用程式新增至後端集區。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![合作夥伴解決方案應用程式][6]

## <a name="finalize-configuration"></a><span data-ttu-id="c0fd9-137">完成設定</span><span class="sxs-lookup"><span data-stu-id="c0fd9-137">Finalize configuration</span></span>

<span data-ttu-id="c0fd9-138">資訊安全中心會追蹤已新增至應用程式閘道成為受保護資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="c0fd9-139">它會監視此資源的健康情況，確保它受到應用程式閘道的保護。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="c0fd9-140">下一個步驟是將虛耗網路的私人 IP、公用 IP 或 NIC 新增至應用程式閘道的後端集區。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="c0fd9-141">若不這麼做，會顯示另一個 [完成應用程式保護] 建議，直到新增資源。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![新增 Web 應用程式防火牆刀鋒視窗][5]

## <a name="security-alerts"></a><span data-ttu-id="c0fd9-143">安全性警示</span><span class="sxs-lookup"><span data-stu-id="c0fd9-143">Security Alerts</span></span>

<span data-ttu-id="c0fd9-144">在資訊安全中心內瀏覽至 [偵測]  >  [安全性警示]。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="c0fd9-145">在這裡可以找到您的應用程式閘道的 WAF 警示。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="c0fd9-146">警示是依 WAF 規則細分。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-146">Alerts are broken down by WAF rule.</span></span>

![安全性警示][8]

<span data-ttu-id="c0fd9-148">按一下規則會提供該特定 WAF 規則的警示清單。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="c0fd9-149">每個警示會顯示找到項目的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="c0fd9-150">詳細資料會提供連結至應用程式閘道的連結。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-150">The details provide a link to the application gateway.</span></span>
 
![警示詳細資料][9]

## <a name="next-steps"></a><span data-ttu-id="c0fd9-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0fd9-152">Next steps</span></span>

<span data-ttu-id="c0fd9-153">若要了解如何在現有應用程式閘道上啟用 Web 應用程式防火牆，請參閱[建立或更新具有 Web 應用程式防火牆的 Azure 應用程式閘道](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)。</span><span class="sxs-lookup"><span data-stu-id="c0fd9-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png