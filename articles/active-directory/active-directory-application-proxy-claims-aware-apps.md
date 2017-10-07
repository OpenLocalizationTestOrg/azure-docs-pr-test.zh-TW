---
title: "aaaClaims 感知應用程式的 Azure AD 應用程式 Proxy |Microsoft 文件"
description: "如何 toopublish 內部接受您的使用者的安全遠端存取的 ADFS 宣告的 ASP.NET 應用程式。"
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="95c86-103">在應用程式 Proxy 中使用宣告感知應用程式</span><span class="sxs-lookup"><span data-stu-id="95c86-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="95c86-104">[宣告感知應用程式](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx)執行重新導向 toohello 安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="95c86-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="95c86-105">hello STS hello 使用者，但是也會語彙基元要求認證，然後重新導向 hello 使用者 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95c86-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="95c86-106">有幾個方式 tooenable 應用程式 Proxy toowork，與這些重新導向。</span><span class="sxs-lookup"><span data-stu-id="95c86-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="95c86-107">針對宣告感知應用程式使用此發行項 tooconfigure 您的部署。</span><span class="sxs-lookup"><span data-stu-id="95c86-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="95c86-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="95c86-108">Prerequisites</span></span>
<span data-ttu-id="95c86-109">請確定該 hello 宣告感知應用程式的 hello STS 重新導向 toois 與內部網路之外使用。</span><span class="sxs-lookup"><span data-stu-id="95c86-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="95c86-110">您可以提供 hello STS 公開透過 proxy，或允許外部連接。</span><span class="sxs-lookup"><span data-stu-id="95c86-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="95c86-111">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="95c86-111">Publish your application</span></span>

1. <span data-ttu-id="95c86-112">將根據 toohello 指示中所述的應用程式發行[發行應用程式 Proxy](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="95c86-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="95c86-113">瀏覽 toohello 應用程式頁面上，在入口網站，並選取 hello**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="95c86-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="95c86-114">如果您選擇 [Azure Active Directory] 作為您的 [預先驗證方法]，請選取 [Azure AD 單一登入已停用] 作為您的 [內部驗證方法]。</span><span class="sxs-lookup"><span data-stu-id="95c86-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="95c86-115">如果您選擇**通過**做為您**預先驗證方法**，您不需要 toochange 任何項目。</span><span class="sxs-lookup"><span data-stu-id="95c86-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="95c86-116">設定 ADFS</span><span class="sxs-lookup"><span data-stu-id="95c86-116">Configure ADFS</span></span>

<span data-ttu-id="95c86-117">您可以使用以下兩種方式之一為宣告感知應用程式設定 ADFS。</span><span class="sxs-lookup"><span data-stu-id="95c86-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="95c86-118">hello 第一個是使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="95c86-118">hello first is by using custom domains.</span></span> <span data-ttu-id="95c86-119">WS-同盟與第二個是 hello。</span><span class="sxs-lookup"><span data-stu-id="95c86-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="95c86-120">選項 1：自訂網域</span><span class="sxs-lookup"><span data-stu-id="95c86-120">Option 1: Custom domains</span></span>

<span data-ttu-id="95c86-121">如果所有 hello 內部 Url，您的應用程式的完整網域名稱 (Fqdn)，則您可以設定[自訂網域](active-directory-application-proxy-custom-domains.md)應用程式。</span><span class="sxs-lookup"><span data-stu-id="95c86-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="95c86-122">使用 hello 自訂網域 toocreate 外部 Url hello 與 hello 內部 Url 相同。</span><span class="sxs-lookup"><span data-stu-id="95c86-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="95c86-123">當您的外部 Url 符合您的內部 Url 時，hello STS 重新導向會使用您的使用者是否在內部部署或遠端。</span><span class="sxs-lookup"><span data-stu-id="95c86-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="95c86-124">選項 2：WS-同盟</span><span class="sxs-lookup"><span data-stu-id="95c86-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="95c86-125">開啟 [ADFS 管理]。</span><span class="sxs-lookup"><span data-stu-id="95c86-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="95c86-126">跳過**信賴憑證者信任**，以滑鼠右鍵按一下您要發行應用程式 proxy 的 hello 應用程式，然後選擇 **屬性**。</span><span class="sxs-lookup"><span data-stu-id="95c86-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![信賴憑證者信任 - 以滑鼠右鍵按一下應用程式名稱 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="95c86-128">在 hello**端點**索引標籤，在**端點類型**，選取**WS-同盟**。</span><span class="sxs-lookup"><span data-stu-id="95c86-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="95c86-129">下**信任 URL**，輸入您在輸入 hello 下的應用程式 Proxy 的 hello URL**外部 URL**按一下**[確定]**。</span><span class="sxs-lookup"><span data-stu-id="95c86-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![新增端點 - 設定 [信任的 URL] 值 - 螢幕擷取畫面](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="95c86-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95c86-131">Next steps</span></span>
* <span data-ttu-id="95c86-132">對於非宣告感知的應用程式，請[啟用單一登入](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="95c86-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="95c86-133">啟用原生用戶端應用程式 toointeract 與 proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="95c86-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


