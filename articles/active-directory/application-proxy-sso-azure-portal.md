---
title: "使用 Azure AD 應用程式 Proxy 設定應用程式的單一登入 | Microsoft Docs"
description: "在 Azure 入口網站中使用 Azure AD 應用程式 Proxy，為您已發佈的內部部署應用程式啟動單一登入。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="d7ca8-103">使用應用程式 Proxy 進行單一登入的密碼保存庫</span><span class="sxs-lookup"><span data-stu-id="d7ca8-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="d7ca8-104">Azure Active Directory 應用程式 Proxy 可發佈內部部署應用程式，讓遠端員工也可以安全地存取它們，進而幫助您改進生產力。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="d7ca8-105">在 Azure 入口網站中，您也可以設定這些應用程式的單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="d7ca8-106">您的使用者只需要向 Azure AD 驗證，便可以存取您的企業應用程式，而不必再次登入。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="d7ca8-107">應用程式 Proxy 支援數個[單一登入模式](application-proxy-sso-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="d7ca8-108">密碼型登入適用於使用使用者名稱/密碼組合進行驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="d7ca8-109">當您設定應用程式的密碼型登入您時，您的使用者必須登入一次內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="d7ca8-110">之後，Azure Active Directory 會儲存登入資訊，並且會在您的使用者從遠端存取時，自動將登入資訊提供給應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="d7ca8-111">您應該已經使用應用程式 Proxy 發行並測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="d7ca8-112">如果還沒，請依照[使用 Azure AD 應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)的步驟操作，然後回到這裡。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="d7ca8-113">為應用程式設定密碼儲存庫存</span><span class="sxs-lookup"><span data-stu-id="d7ca8-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="d7ca8-114">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="d7ca8-115">選取 [Azure Active Directory]  >  [企業應用程式]  >  [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="d7ca8-116">從清單中選取您要設定 SSO 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="d7ca8-117">選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-117">Select **Single sign-on**.</span></span>

   ![選取單一登入](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="d7ca8-119">在 SSO 模式中，選擇 [密碼型登入]。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="d7ca8-120">在登入 URL 輸入頁面 URL，使用者將在該頁面輸入其使用者名稱和密碼，以登入公司網路外部的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="d7ca8-121">這可能是您透過應用程式 Proxy 發佈應用程式時建立的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![選擇密碼型登入並輸入您的 URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="d7ca8-123">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="d7ca8-124">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="d7ca8-124">Test your app</span></span>

<span data-ttu-id="d7ca8-125">移至您設定用於遠端存取應用程式的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="d7ca8-126">使用該應用程式的認證登入 (或您設定有存取權之測試帳戶的認證)。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="d7ca8-127">一旦您成功登入，應該能夠離開應用程式後再回到應用程式，不需要再次輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="d7ca8-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d7ca8-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7ca8-128">Next steps</span></span>

- <span data-ttu-id="d7ca8-129">閱讀其他實作[使用應用程式 Proxy 進行單一登入](application-proxy-sso-overview.md)的做法</span><span class="sxs-lookup"><span data-stu-id="d7ca8-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="d7ca8-130">深入了解[使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="d7ca8-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>