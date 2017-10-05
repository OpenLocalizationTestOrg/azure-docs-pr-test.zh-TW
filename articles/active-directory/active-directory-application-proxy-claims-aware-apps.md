---
title: "宣告感知應用程式 - Azure AD 應用程式 Proxy | Microsoft Docs"
description: "如何發佈接受 ADFS 宣告的內部部署 ASP.NET 應用程式，讓您的使用者安全地進行遠端存取。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="df853-103">在應用程式 Proxy 中使用宣告感知應用程式</span><span class="sxs-lookup"><span data-stu-id="df853-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="df853-104">[宣告感知應用程式](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx)會執行重新導向至 Security Token Service (STS)。</span><span class="sxs-lookup"><span data-stu-id="df853-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="df853-105">STS 會向使用者要求認證以交換權杖，然後將使用者重新導向至應用程式。</span><span class="sxs-lookup"><span data-stu-id="df853-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="df853-106">有幾種方法可以讓應用程式 Proxy 進行這些重新導向。</span><span class="sxs-lookup"><span data-stu-id="df853-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="df853-107">請按照本文的說明來設定對宣告感知應用程的部署。</span><span class="sxs-lookup"><span data-stu-id="df853-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="df853-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="df853-108">Prerequisites</span></span>
<span data-ttu-id="df853-109">確定宣告感知應用程式重新導向的 STS 可從內部部署網路外部使用。</span><span class="sxs-lookup"><span data-stu-id="df853-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="df853-110">您可以透過 Proxy 將 STS 公開或是允許外部連接，讓 STS 可供使用。</span><span class="sxs-lookup"><span data-stu-id="df853-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="df853-111">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="df853-111">Publish your application</span></span>

1. <span data-ttu-id="df853-112">根據 [使用應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)中的所述指示來發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="df853-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="df853-113">瀏覽至入口網站中的應用程式頁面，然後選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="df853-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="df853-114">如果您選擇 [Azure Active Directory] 作為您的 [預先驗證方法]，請選取 [Azure AD 單一登入已停用] 作為您的 [內部驗證方法]。</span><span class="sxs-lookup"><span data-stu-id="df853-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="df853-115">如果您選擇 [傳遞] 作為您的 [預先驗證方法]，則無需進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="df853-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="df853-116">設定 ADFS</span><span class="sxs-lookup"><span data-stu-id="df853-116">Configure ADFS</span></span>

<span data-ttu-id="df853-117">您可以使用以下兩種方式之一為宣告感知應用程式設定 ADFS。</span><span class="sxs-lookup"><span data-stu-id="df853-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="df853-118">第一種方式是使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="df853-118">The first is by using custom domains.</span></span> <span data-ttu-id="df853-119">第二種方式是使用 WS-同盟。</span><span class="sxs-lookup"><span data-stu-id="df853-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="df853-120">選項 1：自訂網域</span><span class="sxs-lookup"><span data-stu-id="df853-120">Option 1: Custom domains</span></span>

<span data-ttu-id="df853-121">如果您應用程式的所有內部 URL 皆為完整網域名稱 (FQDN)，則您可為您的應用程式設定[自訂網域](active-directory-application-proxy-custom-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="df853-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="df853-122">請使用自訂網域建立與內部 URL 相同的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="df853-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="df853-123">當您的外部 URL 與內部 URL 相符時，無論使用者是在內部部署或遠端，STS 重新導向都會運作。</span><span class="sxs-lookup"><span data-stu-id="df853-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="df853-124">選項 2：WS-同盟</span><span class="sxs-lookup"><span data-stu-id="df853-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="df853-125">開啟 [ADFS 管理]。</span><span class="sxs-lookup"><span data-stu-id="df853-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="df853-126">移至 [信賴憑證者信任]，並在您要使用「應用程式 Proxy 」來發佈的應用程式上按一下滑鼠右鍵，然後選擇 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="df853-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![信賴憑證者信任 - 以滑鼠右鍵按一下應用程式名稱 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="df853-128">在 [端點] 索引標籤的 [端點類型] 底下，選取 [WS-同盟]。</span><span class="sxs-lookup"><span data-stu-id="df853-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="df853-129">在 [信任的 URL] 底下，輸入您在「應用程式 Proxy」的 [外部 URL] 底下輸入的 URL，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="df853-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![新增端點 - 設定 [信任的 URL] 值 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="df853-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df853-131">Next steps</span></span>
* <span data-ttu-id="df853-132">對於非宣告感知的應用程式，請[啟用單一登入](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="df853-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="df853-133">啟用原生用戶端應用程式以與 Proxy 應用程式互動</span><span class="sxs-lookup"><span data-stu-id="df853-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


