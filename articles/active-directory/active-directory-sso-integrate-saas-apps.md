---
title: "將 Azure Active Directory 單一登入與 SaaS 應用程式整合 | Microsoft Docs"
description: "在 Azure Active Directory 中啟用 SaaS 應用程式的單一登入驗證和使用者佈建集中式存取管理。 如何將 Azure Active Directory 與 SaaS 應用程式整合的概觀。"
services: active-directory
keywords: "將 Azure AD 與 SaaS 應用程式整合在一起"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fc0d297598c334ca8f6f8a2bd3ae948c87956342
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a><span data-ttu-id="956fd-105">整合 Azure Active Directory 單一登入與 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="956fd-105">Integrate Azure Active Directory single sign-on with SaaS apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="956fd-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="956fd-106">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="956fd-107">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="956fd-107">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

<span data-ttu-id="956fd-108">若要開始為將於組織部署的應用程式設定單一登入，您將使用 Azure Active Directory (Azure AD) 中的現有目錄。</span><span class="sxs-lookup"><span data-stu-id="956fd-108">To get started setting up single sign-on for an app that you’re bringing into your organization, you will be using an existing directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="956fd-109">您可以使用從 Microsoft Azure、Office 365 或 Windows Intune 取得的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="956fd-109">You can use an Azure AD directory that you obtain through Microsoft Azure, Office 365, or Windows Intune.</span></span> <span data-ttu-id="956fd-110">如果您有兩個以上的項目，請參閱 [管理 Azure AD 目錄](active-directory-administer.md) 來判斷要使用哪一個。</span><span class="sxs-lookup"><span data-stu-id="956fd-110">If you have two or more of these, see [Administer your Azure AD directory](active-directory-administer.md) to determine which one to use.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="956fd-111">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="956fd-111">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="956fd-112">如需如何在 Azure AD 系統管理中心指派系統管理員角色的相關資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-enterprise-apps-manage-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-112">For how to assign administrator roles in the Azure AD admin center, see [Assigning administrator roles in Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="956fd-113">驗證</span><span class="sxs-lookup"><span data-stu-id="956fd-113">Authentication</span></span>
<span data-ttu-id="956fd-114">對於應用程式支援 SAML 2.0、WS-同盟或 OpenID Connect 通訊協定的應用程式，Azure Active Directory 使用簽章憑證來建立信任關係。</span><span class="sxs-lookup"><span data-stu-id="956fd-114">For applications that support the SAML 2.0, WS-Federation, or OpenID Connect protocols, Azure Active Directory uses signing certificates to establish trust relationships.</span></span> <span data-ttu-id="956fd-115">如需詳細資訊，請參閱 [管理同盟單一登入的憑證](active-directory-sso-certs.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-115">For more information about this, see [Managing certificates for federated single sign-on](active-directory-sso-certs.md).</span></span>

<span data-ttu-id="956fd-116">對於僅支援 HTML 表單型登入的應用程式，Azure Active Directory 使用「密碼儲存庫存」來建立信任關係。</span><span class="sxs-lookup"><span data-stu-id="956fd-116">For applications that support only HTML forms-based sign-in, Azure Active Directory uses ‘password vaulting’ to establish trust relationships.</span></span> <span data-ttu-id="956fd-117">這可讓您組織中的使用者，使用 SaaS 應用程式的使用者帳戶資訊，由 Azure AD 自動登入 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="956fd-117">This enables the users in your organization to be automatically signed in to a SaaS application by Azure AD using the user account information from the SaaS application.</span></span> <span data-ttu-id="956fd-118">Azure AD 會收集並安全地儲存使用者帳戶資訊和相關的密碼。</span><span class="sxs-lookup"><span data-stu-id="956fd-118">Azure AD collects and securely stores the user account information and the related password.</span></span> <span data-ttu-id="956fd-119">如需詳細資訊，請參閱 [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="956fd-119">For more information, see [Password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

## <a name="authorization"></a><span data-ttu-id="956fd-120">Authorization</span><span class="sxs-lookup"><span data-stu-id="956fd-120">Authorization</span></span>
<span data-ttu-id="956fd-121">佈建的帳戶可授與通過單一登入驗證的使用者使用應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="956fd-121">A provisioned account enables a user to be authorized to use an application after they have authenticated through single sign-on.</span></span> <span data-ttu-id="956fd-122">使用者佈建可以手動方式完成，或是在某些情況下，您可以依據在 Azure Active Directory 中所做的變更來新增和移除 SaaS 應用程式中的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="956fd-122">User provisioning can be done manually, or in some cases you can add and remove user information from the SaaS app based on changes made in Azure Active Directory.</span></span> <span data-ttu-id="956fd-123">如需有關使用現有的 Azure AD 連接器來進行自動化佈建的詳細資訊，請參閱[自動執行 SaaS 應用程式的使用者佈建和取消佈建](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-123">For more information on using existing Azure AD connectors for automated provisioning, see  [Automated user provisioning and de-provisioning for SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<span data-ttu-id="956fd-124">否則，您可以手動將使用者資訊新增至應用程式，或使用市集中可用的其他佈建解決方案。</span><span class="sxs-lookup"><span data-stu-id="956fd-124">Otherwise, you can manually add user information to an app, or use other provisioning solutions that are available in the marketplace.</span></span>

## <a name="access"></a><span data-ttu-id="956fd-125">Access</span><span class="sxs-lookup"><span data-stu-id="956fd-125">Access</span></span>
<span data-ttu-id="956fd-126">Azure AD 提供幾種可自訂的方式，來對您組織中的使用者部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="956fd-126">Azure AD provides several customizable ways to deploy applications to end users in your organization.</span></span> <span data-ttu-id="956fd-127">您不會受限於任一特定的部署或存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="956fd-127">You are not locked into any particular deployment or access solution.</span></span> <span data-ttu-id="956fd-128">您可以使用 [最符合您需求的解決方案](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。</span><span class="sxs-lookup"><span data-stu-id="956fd-128">You can use [the solution that best suits your needs](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

## <a name="additional-considerations-for-applications-already-in-use"></a><span data-ttu-id="956fd-129">已使用中的應用程式的其他考量</span><span class="sxs-lookup"><span data-stu-id="956fd-129">Additional considerations for applications already in use</span></span>
<span data-ttu-id="956fd-130">為組織已使用的應用程式設定單一登入是與為新應用程式建立新帳戶不同的程序。</span><span class="sxs-lookup"><span data-stu-id="956fd-130">Setting up single sign on for an application that your organization already uses is a different process from the process of creating new accounts for a new application.</span></span> <span data-ttu-id="956fd-131">有幾個基本步驟包括：將應用程式中的使用者身分識別對應到 Azure AD 身分識別，以及了解整合之後使用者如何體驗登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="956fd-131">There are a couple of preliminary steps including: mapping user identities in the application to Azure AD identities, and understanding how users will experience logging in to an application after it is integrated.</span></span>

> [!NOTE]
> <span data-ttu-id="956fd-132">若要為現有的應用程式設定 SSO，您必須在 Azure AD 和 SaaS 應用程式同時具有全域系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="956fd-132">To set up SSO for an existing application, you need to have global administrator rights in both Azure AD and the SaaS application.</span></span>
>
>

### <a name="mapping-user-accounts"></a><span data-ttu-id="956fd-133">對應使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="956fd-133">Mapping user accounts</span></span>
<span data-ttu-id="956fd-134">使用者的身分識別通常有唯一識別碼，可能是電子郵件地址或使用者主體名稱 (UPN)。</span><span class="sxs-lookup"><span data-stu-id="956fd-134">A user's identity typically has a unique identifier that could be an email address, or user principal name (UPN).</span></span> <span data-ttu-id="956fd-135">您必須將每個使用者的應用程式身分識別連結 (對應) 至其各自的 Azure AD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="956fd-135">You will need to link (map) each user's application identity to their respective Azure AD identity.</span></span> <span data-ttu-id="956fd-136">根據您的應用程式驗證的需求，有好幾種方法可完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="956fd-136">There are a couple of ways to accomplish this depending on how the requirement of your application authentication.</span></span>

<span data-ttu-id="956fd-137">如需有關將應用程式身分識別與 Azure AD 身分識別對應的詳細資訊，請參閱[自訂 SAML 權杖中發出的宣告](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx)和[自訂佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-137">For more information about mapping application identities with Azure AD identities, see [Customizing claims issued in the SAML token](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) and [Customizing attribute mappings for provisioning](active-directory-saas-customizing-attribute-mappings.md).</span></span>

### <a name="understanding-the-users-log-in-experience"></a><span data-ttu-id="956fd-138">了解使用者的登入體驗</span><span class="sxs-lookup"><span data-stu-id="956fd-138">Understanding the user's log in experience</span></span>
<span data-ttu-id="956fd-139">當您為已在使用中的應用程式整合 SSO 時，請務必了解使用者經驗將會受到影響。</span><span class="sxs-lookup"><span data-stu-id="956fd-139">When you integrate SSO for an application that’s already in use, it’s important to realize that the user experience will be affected.</span></span> <span data-ttu-id="956fd-140">對於所有應用程式，使用者將會開始使用其 Azure AD 認證來登入。</span><span class="sxs-lookup"><span data-stu-id="956fd-140">For all applications, users will start using their Azure AD credentials to sign in.</span></span> <span data-ttu-id="956fd-141">他們也可能需要使用不同的入口網站來存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="956fd-141">It could also be that they must use a different portal to access the applications.</span></span>

<span data-ttu-id="956fd-142">有些應用程式的 SSO 可在應用程式的登入介面中執行，但對於其他應用程式，使用者則必須透過中央入口網站 (例如[我的應用程式](http://myapps.microsoft.com)或 [Office365](http://portal.office.com/myapps)) 來登入。</span><span class="sxs-lookup"><span data-stu-id="956fd-142">SSO for some applications can be done on the application's sign in interface, but for other applications, the user will have to go through a central portal such as ([My Apps](http://myapps.microsoft.com) or [Office365](http://portal.office.com/myapps)) to sign in.</span></span> <span data-ttu-id="956fd-143">請在 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)中深入了解不同類型的 SSO 與其使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="956fd-143">Learn more about the different types of SSO and their user experiences in [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="956fd-144">另一個有用的資源是[引導開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)一文中的＜隱藏使用者同意＞。</span><span class="sxs-lookup"><span data-stu-id="956fd-144">Another valuable resource is *Suppressing user consent* in the [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="956fd-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="956fd-145">Next steps</span></span>
<span data-ttu-id="956fd-146">對於您在應用程式庫中找到的 SaaS 應用程式，Azure AD 提供一些 [有關如何整合 SaaS 應用程式的教學課程](active-directory-saas-tutorial-list.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-146">For SaaS apps that you find in the App Gallery, Azure AD provides a number of [tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>

<span data-ttu-id="956fd-147">如果應用程式不在應用程式庫中，您可以 [將應用程式新增至 Azure AD 應用程式庫做為自訂應用程式](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="956fd-147">If app is not in App Gallery, you can [add it to the Azure AD App Gallery as a custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

<span data-ttu-id="956fd-148">Azure.com 文件庫中還有更多關於這些議題的詳細資料，請先閱讀[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-148">There is much more detail on all of these issues in the Azure.com library, beginning with [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="956fd-149">另外，請勿錯過 [Azure Active Directory 中應用程式管理的文件索引](active-directory-apps-index.md)。</span><span class="sxs-lookup"><span data-stu-id="956fd-149">Plus, don't miss the [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md).</span></span>
