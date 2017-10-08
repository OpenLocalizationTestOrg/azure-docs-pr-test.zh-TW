---
title: "Azure AD Application Proxy 的 SSO aaaManage |Microsoft 文件"
description: "深入了解的單一登入應用程式 proxy 的 hello 基本概念"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="8262c-103">Azure AD 應用程式 Proxy 如何提供單一登入？</span><span class="sxs-lookup"><span data-stu-id="8262c-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="8262c-104">單一登入是 Azure AD 應用程式 Proxy 的重要元素。</span><span class="sxs-lookup"><span data-stu-id="8262c-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="8262c-105">因為您的使用者只能有 toosign tooAzure hello 雲端中的 Active Directory 中，它會提供 hello 最佳使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="8262c-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="8262c-106">一旦驗證 tooAzure Active Directory hello 應用程式 Proxy 連接器處理 hello 驗證 toohello 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8262c-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="8262c-107">hello 後端應用程式無法分辨 hello 遠端使用者透過應用程式 Proxy 與一般情況下使用已加入網域的裝置上登入之間的差異。</span><span class="sxs-lookup"><span data-stu-id="8262c-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="8262c-108">toouse Azure Active Directory 的單一登入 tooyour 應用程式，您需要 tooselect **Azure Active Directory** hello 預先驗證方法。</span><span class="sxs-lookup"><span data-stu-id="8262c-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="8262c-109">如果您選取**通過**則您的使用者未完全驗證 tooAzure Active Directory，但是會導向直線 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8262c-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="8262c-110">當您第一次發行的應用程式，或瀏覽 tooyour hello Azure 入口網站中的應用程式編輯 hello 應用程式 Proxy 設定，您可以設定這項設定。</span><span class="sxs-lookup"><span data-stu-id="8262c-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="8262c-111">toosee 單一登入選項，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8262c-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="8262c-112">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8262c-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8262c-113">瀏覽過**Azure Active Directory** > **企業應用程式** > **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8262c-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="8262c-114">選取 hello 應用程式的單一登入選項想 toomanage。</span><span class="sxs-lookup"><span data-stu-id="8262c-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="8262c-115">選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8262c-115">Select **Single sign-on**.</span></span>

   ![SSO 下拉式功能表](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="8262c-117">hello 下拉式清單中的功能表會顯示為單一登入 tooyour 應用程式的五個選項：</span><span class="sxs-lookup"><span data-stu-id="8262c-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="8262c-118">已啟用 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8262c-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="8262c-119">密碼型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-119">Password-based sign-on</span></span>
* <span data-ttu-id="8262c-120">連結型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-120">Linked sign-on</span></span>
* <span data-ttu-id="8262c-121">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8262c-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="8262c-122">標頭型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="8262c-123">已啟用 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8262c-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="8262c-124">如果您不想 toouse 單一登入 tooyour 應用程式的 Azure Active Directory 整合，請選擇**Azure AD 單一登入已停用**。</span><span class="sxs-lookup"><span data-stu-id="8262c-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="8262c-125">選取此選項後，使用者可能會進行兩次驗證。</span><span class="sxs-lookup"><span data-stu-id="8262c-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="8262c-126">首先，它們會驗證 tooAzure Active Directory，並再登入 toohello 應用程式本身。</span><span class="sxs-lookup"><span data-stu-id="8262c-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="8262c-127">如果在內部部署應用程式不需要使用者 tooauthenticate，但是您想要 tooadd Azure Active Directory 安全性層級為遠端存取，此選項是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="8262c-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="8262c-128">密碼型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-128">Password-based sign-on</span></span>

<span data-ttu-id="8262c-129">如果您想要 toouse Azure Active Directory 與密碼保存庫在內部部署應用程式，選擇**密碼式登入**。</span><span class="sxs-lookup"><span data-stu-id="8262c-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="8262c-130">如果您的應用程式使用使用者名稱/密碼組合 (而不是存取權杖或標頭) 進行驗證，此選項是個不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="8262c-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="8262c-131">使用密碼型登入，您的使用者需要 toosign toohello 應用程式 hello 中的第一次存取它。</span><span class="sxs-lookup"><span data-stu-id="8262c-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="8262c-132">在這之後，Azure Active Directory 會代表 hello 使用者提供 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8262c-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="8262c-133">如需設定密碼型登入的詳細資訊，請參閱[使用應用程式 Proxy 單一登入的密碼保存庫](application-proxy-sso-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8262c-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="8262c-134">連結型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-134">Linked sign-on</span></span>

<span data-ttu-id="8262c-135">如果您已經有為您的內部部署身分識別設定的單一登入解決方案，請選擇 [連結型登入]。</span><span class="sxs-lookup"><span data-stu-id="8262c-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="8262c-136">此選項可讓 Azure Active Directory tooleverage 現有 SSO 解決方案，但是遠端存取 toohello 應用程式仍可讓您的使用者。</span><span class="sxs-lookup"><span data-stu-id="8262c-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="8262c-137">如需連結登入 (先前稱為現有單一登入) 的詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="8262c-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="8262c-138">整合式 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="8262c-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="8262c-139">如果您在內部部署應用程式使用整合式 Windows Authentication(IWA) 或您想 toouse Kerberos 限制委派 (KCD) 的單一登入，選擇 **整合式 Windows 驗證**。</span><span class="sxs-lookup"><span data-stu-id="8262c-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="8262c-140">使用此選項，您的使用者只需要 tooauthenticate tooAzure Active Directory，並接著 hello 應用程式 Proxy 連接器模擬 hello 使用者 tooget Kerberos 權杖並 toohello 應用程式中的登入。</span><span class="sxs-lookup"><span data-stu-id="8262c-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="8262c-141">如需設定整合式 Windows 驗證的詳細資訊，請參閱 [使用應用程式 Proxy 單一登入的 Kerberos 限制委派](active-directory-application-proxy-sso-using-kcd.md)。</span><span class="sxs-lookup"><span data-stu-id="8262c-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="8262c-142">標頭型登入</span><span class="sxs-lookup"><span data-stu-id="8262c-142">Header-based sign-on</span></span> 

<span data-ttu-id="8262c-143">如果應用程式使用標頭進行驗證，請選擇 [標頭型登入]。</span><span class="sxs-lookup"><span data-stu-id="8262c-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="8262c-144">使用此選項，您的使用者只需要 tooauthentication hello Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="8262c-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="8262c-145">與協力廠商驗證服務的 Microsoft 合作夥伴呼叫 PingAccess，轉譯成 hello 應用程式標頭格式的 hello Azure Active Directory 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="8262c-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="8262c-146">如需設定標頭型驗證的相關資訊，請參閱[使用應用程式 Proxy 單一登入的標頭型驗證](application-proxy-ping-access.md)。</span><span class="sxs-lookup"><span data-stu-id="8262c-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8262c-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8262c-147">Next steps</span></span>

- [<span data-ttu-id="8262c-148">使用應用程式 Proxy 進行單一登入的密碼保存庫</span><span class="sxs-lookup"><span data-stu-id="8262c-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="8262c-149">可供使用應用程式 Proxy 單一登入的 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="8262c-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="8262c-150">使用應用程式 Proxy 單一登入的標頭型驗證</span><span class="sxs-lookup"><span data-stu-id="8262c-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
