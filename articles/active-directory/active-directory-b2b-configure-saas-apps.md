---
title: "在 Azure Active Directory B2B 共同作業的 aaaConfigure SaaS 應用程式 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的程式碼與 PowerShell 範例"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="5756e-103">為 B2B 共同作業設定 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="5756e-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="5756e-104">Azure Active Directory (Azure AD) B2B 共同作業可搭配與 Azure AD 整合的大部分應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="5756e-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="5756e-105">在本節中，我們將逐步說明用於設定一些常見 SaaS 應用程式以搭配 Azure AD B2B 使用的指示。</span><span class="sxs-lookup"><span data-stu-id="5756e-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="5756e-106">在您查看應用程式特定指示之前，以下是一些主要規則：</span><span class="sxs-lookup"><span data-stu-id="5756e-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="5756e-107">適用於大部分的 hello 應用程式，使用者安裝程式會以手動方式需要 toohappen。</span><span class="sxs-lookup"><span data-stu-id="5756e-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="5756e-108">亦即，使用者必須手動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5756e-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="5756e-109">支援自動安裝，例如 Dropbox 的應用程式從 hello 應用程式建立個別的邀請。</span><span class="sxs-lookup"><span data-stu-id="5756e-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="5756e-110">使用者必須確定 tooaccept 每個邀請。</span><span class="sxs-lookup"><span data-stu-id="5756e-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="5756e-111">Hello 使用者屬性，toomitigate 中來賓使用者損害的使用者設定檔磁碟 (UPD) 的所有問題都設定**使用者識別碼**太**user.mail**。</span><span class="sxs-lookup"><span data-stu-id="5756e-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="5756e-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="5756e-112">Dropbox Business</span></span>

<span data-ttu-id="5756e-113">tooenable 使用者 toosign 中使用其組織帳戶，您必須手動設定 Dropbox 商務 toouse Azure AD 做為安全性聲明標記語言 (SAML) 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="5756e-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="5756e-114">如果尚未設定的 toodo Dropbox 商務。 因此，它無法提示或否則允許使用者 toosign 中使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="5756e-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="5756e-115">tooadd hello Dropbox 商務應用程式到 Azure AD 中，選取**企業應用程式**在 hello 左的窗格，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5756e-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![hello hello 企業應用程式 頁面上的 新增 按鈕](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="5756e-117">在 hello**新增應用程式**視窗中，輸入**dropbox**在 hello 搜尋方塊，然後選取  **dropbox 企業版**hello 結果 清單中。</span><span class="sxs-lookup"><span data-stu-id="5756e-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![搜尋"dropbox"hello 上新增的應用程式頁面](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="5756e-119">在 hello**單一登入**頁面上，選取**單一登入**在 hello 左的窗格，然後輸入**user.mail**在 hello**使用者識別碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="5756e-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="5756e-120">(其預設為 UPN。)</span><span class="sxs-lookup"><span data-stu-id="5756e-120">(It's set as UPN by default.)</span></span>

  ![設定單一登入 hello 應用程式](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="5756e-122">toodownload hello 憑證 toouse Dropbox 組態選取**設定 DropBox**，然後選取**SAML 單一登入服務 URL** hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="5756e-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![下載 hello Dropbox 設定憑證](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="5756e-124">登入以 hello tooDropbox 登入 URL 從 hello**單一登入**頁面。</span><span class="sxs-lookup"><span data-stu-id="5756e-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![hello Dropbox 登入頁面](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="5756e-126">在 hello 功能表中，選取 **管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="5756e-126">On hello menu, select **Admin Console**.</span></span>

  ![hello hello Dropbox 功能表上的 「 系統管理員主控台 」 連結](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="5756e-128">在 hello**驗證**對話方塊中，選取**詳細**，hello 憑證上傳，然後在 hello**登入 URL**方塊中，輸入 hello SAML 單一登入 URL。</span><span class="sxs-lookup"><span data-stu-id="5756e-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![hello hello 摺疊 [驗證] 對話方塊中的"More"連結](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![hello 」 登入 URL"hello 中的擴充驗證 對話方塊](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="5756e-131">tooconfigure hello Azure 入口網站中的使用者自動安裝程式選取**佈建**hello 左窗格中，選取**自動**在 hello**佈建模式**方塊，並選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="5756e-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![設定自動使用者佈建在 hello Azure 入口網站](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="5756e-133">Hello Dropbox 應用程式中已設定客體或成員的使用者之後，他們會收到個別的邀請，從 Dropbox。</span><span class="sxs-lookup"><span data-stu-id="5756e-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="5756e-134">toouse Dropbox 單一登入，受邀者必須接受 hello 邀請中的連結即可。</span><span class="sxs-lookup"><span data-stu-id="5756e-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="5756e-135">Box</span><span class="sxs-lookup"><span data-stu-id="5756e-135">Box</span></span>
<span data-ttu-id="5756e-136">您可以使用 hello SAML 通訊協定為基礎的同盟，以啟用使用者 tooauthenticate 方塊 guest 使用者以 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5756e-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="5756e-137">在此程序，您上傳中繼資料 tooBox.com。</span><span class="sxs-lookup"><span data-stu-id="5756e-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="5756e-138">從 hello 企業應用程式中加入 hello Box 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5756e-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="5756e-139">在 hello 順序中，以設定單一登入：</span><span class="sxs-lookup"><span data-stu-id="5756e-139">Configure single sign-on in hello following order:</span></span>

  ![設定 Box 單一登入](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="5756e-141">a.</span><span class="sxs-lookup"><span data-stu-id="5756e-141">a.</span></span> <span data-ttu-id="5756e-142">在 hello**登入 URL**方塊中，確定 hello 登入 URL 已設定適當的方塊 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5756e-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="5756e-143">此 URL 是 hello Box.com 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5756e-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="5756e-144">它應該遵循命名慣例的 hello *https://.box.com*。</span><span class="sxs-lookup"><span data-stu-id="5756e-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="5756e-145">hello**識別碼**不適 toothis 應用程式，但它仍會顯示為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="5756e-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="5756e-146">b.</span><span class="sxs-lookup"><span data-stu-id="5756e-146">b.</span></span> <span data-ttu-id="5756e-147">在 hello**使用者識別碼**方塊中，輸入**user.mail** （適用於來賓帳戶的 SSO)。</span><span class="sxs-lookup"><span data-stu-id="5756e-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="5756e-148">c.</span><span class="sxs-lookup"><span data-stu-id="5756e-148">c.</span></span> <span data-ttu-id="5756e-149">在 [SAML 簽署憑證] 之下，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="5756e-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="5756e-150">d.</span><span class="sxs-lookup"><span data-stu-id="5756e-150">d.</span></span> <span data-ttu-id="5756e-151">設定您 Box.com 租用戶 toouse Azure AD 身分識別提供者的 toobegin 下載 hello 中繼資料檔案，並儲存它 tooyour 本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5756e-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="5756e-152">e.</span><span class="sxs-lookup"><span data-stu-id="5756e-152">e.</span></span> <span data-ttu-id="5756e-153">轉送 hello 中繼資料檔案 toohello 方塊支援小組，以單一登入您的設定。</span><span class="sxs-lookup"><span data-stu-id="5756e-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="5756e-154">Azure AD 使用者自動安裝，hello 左窗格中，選取**佈建**，然後選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="5756e-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![授權 Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="5756e-156">Dropbox 受邀者，例如方塊受邀者必須兌換邀請他們 hello Box 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5756e-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5756e-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5756e-157">Next steps</span></span>

<span data-ttu-id="5756e-158">請參閱下列 Azure AD B2B 共同作業的發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="5756e-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="5756e-159">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="5756e-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="5756e-160">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="5756e-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="5756e-161">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="5756e-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="5756e-162">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="5756e-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="5756e-163">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="5756e-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="5756e-164">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="5756e-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="5756e-165">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="5756e-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="5756e-166">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="5756e-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="5756e-167">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="5756e-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="5756e-168">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="5756e-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
