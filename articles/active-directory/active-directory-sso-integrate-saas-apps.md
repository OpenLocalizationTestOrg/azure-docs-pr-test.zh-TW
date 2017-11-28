---
title: "Azure Active Directory 單一登入具有 SaaS 應用程式的 aaaIntegrate |Microsoft 文件"
description: "在 Azure Active Directory 中啟用 SaaS 應用程式的單一登入驗證和使用者佈建集中式存取管理。 概觀 toointegrate Azure Active Directory tooSaaS 應用程式。"
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
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a><span data-ttu-id="ea7d4-105">整合 Azure Active Directory 單一登入與 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea7d4-105">Integrate Azure Active Directory single sign-on with SaaS apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea7d4-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ea7d4-106">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="ea7d4-107">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="ea7d4-107">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

<span data-ttu-id="ea7d4-108">tooget 啟動 設定單一登入帶入您的組織的應用程式，您將使用現有的目錄中 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-108">tooget started setting up single sign-on for an app that you’re bringing into your organization, you will be using an existing directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ea7d4-109">您可以使用從 Microsoft Azure、Office 365 或 Windows Intune 取得的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-109">You can use an Azure AD directory that you obtain through Microsoft Azure, Office 365, or Windows Intune.</span></span> <span data-ttu-id="ea7d4-110">如果您有兩個或多個，請參閱[管理您的 Azure AD 目錄](active-directory-administer.md)toodetermine 哪一個 toouse。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-110">If you have two or more of these, see [Administer your Azure AD directory](active-directory-administer.md) toodetermine which one toouse.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea7d4-111">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-111">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="ea7d4-112">如何置 tooassign hello Azure AD 系統管理員中的系統管理員角色，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-enterprise-apps-manage-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-112">For how tooassign administrator roles in hello Azure AD admin center, see [Assigning administrator roles in Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="ea7d4-113">驗證</span><span class="sxs-lookup"><span data-stu-id="ea7d4-113">Authentication</span></span>
<span data-ttu-id="ea7d4-114">應用程式支援 hello SAML 2.0 WS-同盟或 OpenID Connect 的通訊協定，Azure Active Directory 使用簽署憑證 tooestablish 信任關係。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-114">For applications that support hello SAML 2.0, WS-Federation, or OpenID Connect protocols, Azure Active Directory uses signing certificates tooestablish trust relationships.</span></span> <span data-ttu-id="ea7d4-115">如需詳細資訊，請參閱 [管理同盟單一登入的憑證](active-directory-sso-certs.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-115">For more information about this, see [Managing certificates for federated single sign-on](active-directory-sso-certs.md).</span></span>

<span data-ttu-id="ea7d4-116">對於支援僅 HTML 表單型登入的應用程式，Azure Active Directory 使用 '密碼儲存庫存' tooestablish 信任關係。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-116">For applications that support only HTML forms-based sign-in, Azure Active Directory uses ‘password vaulting’ tooestablish trust relationships.</span></span> <span data-ttu-id="ea7d4-117">這可讓 hello 中的使用者組織 toobe 自動登入 tooa hello SaaS 應用程式中的 hello 使用者帳戶資訊，使用 Azure AD SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-117">This enables hello users in your organization toobe automatically signed in tooa SaaS application by Azure AD using hello user account information from hello SaaS application.</span></span> <span data-ttu-id="ea7d4-118">Azure AD 會收集並安全地儲存 hello 使用者帳戶資訊和 hello 相關的密碼。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-118">Azure AD collects and securely stores hello user account information and hello related password.</span></span> <span data-ttu-id="ea7d4-119">如需詳細資訊，請參閱 [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-119">For more information, see [Password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

## <a name="authorization"></a><span data-ttu-id="ea7d4-120">Authorization</span><span class="sxs-lookup"><span data-stu-id="ea7d4-120">Authorization</span></span>
<span data-ttu-id="ea7d4-121">佈建的帳戶它們透過單一登入已驗證之後，可讓使用者獲得授權的 toobe toouse 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-121">A provisioned account enables a user toobe authorized toouse an application after they have authenticated through single sign-on.</span></span> <span data-ttu-id="ea7d4-122">使用者佈建即可手動方式或在某些情況下，您可以新增和移除 Azure Active Directory 中所做的變更所根據的 hello SaaS 應用程式的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-122">User provisioning can be done manually, or in some cases you can add and remove user information from hello SaaS app based on changes made in Azure Active Directory.</span></span> <span data-ttu-id="ea7d4-123">如需有關使用現有的 Azure AD 連接器來進行自動化佈建的詳細資訊，請參閱[自動執行 SaaS 應用程式的使用者佈建和取消佈建](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-123">For more information on using existing Azure AD connectors for automated provisioning, see  [Automated user provisioning and de-provisioning for SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<span data-ttu-id="ea7d4-124">否則，您可以手動新增使用者資訊 tooan 應用程式，或使用其他佈建的解決方案，可在 hello marketplace 中。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-124">Otherwise, you can manually add user information tooan app, or use other provisioning solutions that are available in hello marketplace.</span></span>

## <a name="access"></a><span data-ttu-id="ea7d4-125">Access</span><span class="sxs-lookup"><span data-stu-id="ea7d4-125">Access</span></span>
<span data-ttu-id="ea7d4-126">Azure AD 提供數個可自訂的方式 toodeploy 您組織中的應用程式 tooend 使用者。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-126">Azure AD provides several customizable ways toodeploy applications tooend users in your organization.</span></span> <span data-ttu-id="ea7d4-127">您不會受限於任一特定的部署或存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-127">You are not locked into any particular deployment or access solution.</span></span> <span data-ttu-id="ea7d4-128">您可以使用[hello 最適合您需求的解決方案](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-128">You can use [hello solution that best suits your needs](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

## <a name="additional-considerations-for-applications-already-in-use"></a><span data-ttu-id="ea7d4-129">已使用中的應用程式的其他考量</span><span class="sxs-lookup"><span data-stu-id="ea7d4-129">Additional considerations for applications already in use</span></span>
<span data-ttu-id="ea7d4-130">設定單一登入您的組織已使用的應用程式是從建立新應用程式的新帳戶的 hello 程序在不同處理序。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-130">Setting up single sign on for an application that your organization already uses is a different process from hello process of creating new accounts for a new application.</span></span> <span data-ttu-id="ea7d4-131">有幾個基本步驟包括： 對應中 hello 應用程式 tooAzure AD 身分識別的使用者識別，以及了解使用者如何體驗之後整合 tooan 應用程式中的記錄。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-131">There are a couple of preliminary steps including: mapping user identities in hello application tooAzure AD identities, and understanding how users will experience logging in tooan application after it is integrated.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7d4-132">tooset 上現有的應用程式的 SSO，這兩個 Azure AD 中需要 toohave 全域系統管理員權限和 hello SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-132">tooset up SSO for an existing application, you need toohave global administrator rights in both Azure AD and hello SaaS application.</span></span>
>
>

### <a name="mapping-user-accounts"></a><span data-ttu-id="ea7d4-133">對應使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="ea7d4-133">Mapping user accounts</span></span>
<span data-ttu-id="ea7d4-134">使用者的身分識別通常有唯一識別碼，可能是電子郵件地址或使用者主體名稱 (UPN)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-134">A user's identity typically has a unique identifier that could be an email address, or user principal name (UPN).</span></span> <span data-ttu-id="ea7d4-135">您將需要 toolink (map) 每個使用者的應用程式識別 tootheir 各自的 Azure AD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-135">You will need toolink (map) each user's application identity tootheir respective Azure AD identity.</span></span> <span data-ttu-id="ea7d4-136">有幾個方式 tooaccomplish 這如何根據 hello 需求的應用程式驗證。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-136">There are a couple of ways tooaccomplish this depending on how hello requirement of your application authentication.</span></span>

<span data-ttu-id="ea7d4-137">如需對應應用程式識別與 Azure AD 識別身分的詳細資訊，請參閱[自訂 hello SAML 權杖中發出的宣告](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx)和[自訂屬性對應的佈建](active-directory-saas-customizing-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-137">For more information about mapping application identities with Azure AD identities, see [Customizing claims issued in hello SAML token](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) and [Customizing attribute mappings for provisioning](active-directory-saas-customizing-attribute-mappings.md).</span></span>

### <a name="understanding-hello-users-log-in-experience"></a><span data-ttu-id="ea7d4-138">了解 hello 使用者的登入體驗</span><span class="sxs-lookup"><span data-stu-id="ea7d4-138">Understanding hello user's log in experience</span></span>
<span data-ttu-id="ea7d4-139">當您將 SSO 整合的應用程式已在使用時，務必 toorealize hello 使用者體驗，將會受到影響。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-139">When you integrate SSO for an application that’s already in use, it’s important toorealize that hello user experience will be affected.</span></span> <span data-ttu-id="ea7d4-140">所有應用程式，使用者將使用在其 Azure AD 認證 toosign 來開始。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-140">For all applications, users will start using their Azure AD credentials toosign in.</span></span> <span data-ttu-id="ea7d4-141">它也可能是它們必須使用不同的入口網站 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-141">It could also be that they must use a different portal tooaccess hello applications.</span></span>

<span data-ttu-id="ea7d4-142">SSO 對於某些應用程式可以對 hello 應用程式的登入介面，但其他應用程式，hello 使用者會有 toogo 透過中央入口網站例如 ([我的應用程式](http://myapps.microsoft.com)或[Office365](http://portal.office.com/myapps)) toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-142">SSO for some applications can be done on hello application's sign in interface, but for other applications, hello user will have toogo through a central portal such as ([My Apps](http://myapps.microsoft.com) or [Office365](http://portal.office.com/myapps)) toosign in.</span></span> <span data-ttu-id="ea7d4-143">深入了解 hello 不同類型的 SSO 和使用者經驗[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-143">Learn more about hello different types of SSO and their user experiences in [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="ea7d4-144">另一個重要的資源是*隱藏使用者同意*在 hello [Guiding 開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-144">Another valuable resource is *Suppressing user consent* in hello [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea7d4-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea7d4-145">Next steps</span></span>
<span data-ttu-id="ea7d4-146">針對您在 hello 應用程式庫中找到的 SaaS 應用程式，Azure AD 提供數個[教學課程有關 toointegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-146">For SaaS apps that you find in hello App Gallery, Azure AD provides a number of [tutorials on how toointegrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>

<span data-ttu-id="ea7d4-147">如果應用程式不會在應用程式庫中，您可以[將它做為自訂應用程式加入 Azure AD App 資源庫 toohello](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-147">If app is not in App Gallery, you can [add it toohello Azure AD App Gallery as a custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

<span data-ttu-id="ea7d4-148">沒有更多詳細資料，從這些問題 hello Azure.com 文件庫中的所有[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-148">There is much more detail on all of these issues in hello Azure.com library, beginning with [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="ea7d4-149">此外，不會錯過 hello [Azure Active Directory 中的應用程式管理的文件索引](active-directory-apps-index.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-149">Plus, don't miss hello [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md).</span></span>
