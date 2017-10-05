---
title: "為 Azure Active Directory 中的 B2B 共同作業設定 SaaS 應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="4355b-103">為 B2B 共同作業設定 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="4355b-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="4355b-104">Azure Active Directory (Azure AD) B2B 共同作業可搭配與 Azure AD 整合的大部分應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="4355b-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="4355b-105">在本節中，我們將逐步說明用於設定一些常見 SaaS 應用程式以搭配 Azure AD B2B 使用的指示。</span><span class="sxs-lookup"><span data-stu-id="4355b-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="4355b-106">在您查看應用程式特定指示之前，以下是一些主要規則：</span><span class="sxs-lookup"><span data-stu-id="4355b-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="4355b-107">大部分的應用程式都需要以手動方式進行使用者設定。</span><span class="sxs-lookup"><span data-stu-id="4355b-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="4355b-108">也就是說，必須在應用程式中手動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="4355b-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="4355b-109">若為支援自動設定的應用程式 (例如 Dropbox)，則會從應用程式建立個別的邀請。</span><span class="sxs-lookup"><span data-stu-id="4355b-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="4355b-110">使用者務必接受每個邀請。</span><span class="sxs-lookup"><span data-stu-id="4355b-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="4355b-111">在使用者屬性中，若要減少與來賓使用者中受損使用者設定檔磁碟 (UPD) 相關的任何問題，一律將 [使用者識別碼] 設定為 [user.mail]。</span><span class="sxs-lookup"><span data-stu-id="4355b-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="4355b-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="4355b-112">Dropbox Business</span></span>

<span data-ttu-id="4355b-113">若要讓使用者使用其組織帳戶登入，您必須手動設定 Dropbox Business，才能使用 Azure AD 做為安全性聲明標記語言 (SAML) 識別提供者。</span><span class="sxs-lookup"><span data-stu-id="4355b-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="4355b-114">如果 Dropbox Business 已這樣設定，則無法顯示提示或允許使用者使用 Azure AD 進行登入。</span><span class="sxs-lookup"><span data-stu-id="4355b-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="4355b-115">若要將 Dropbox Business 應用程式新增至 Azure AD，請選取左的窗格中的 [企業應用程式]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4355b-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![企業應用程式頁面上的 [新增] 按鈕](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="4355b-117">在 [加入應用程式] 視窗的搜尋方塊中輸入 **dropbox**，然後選取結果清單中的 [商務用 Dropbox]。</span><span class="sxs-lookup"><span data-stu-id="4355b-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![在 [加入應用程式] 頁面上搜尋 "dropbox"](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="4355b-119">在 [單一登入] 頁面上，選取左窗格中的 [單一登入]，然後在 [使用者識別碼] 方塊中輸入 **user.mail**。</span><span class="sxs-lookup"><span data-stu-id="4355b-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="4355b-120">(其預設為 UPN。)</span><span class="sxs-lookup"><span data-stu-id="4355b-120">(It's set as UPN by default.)</span></span>

  ![為應用程式設定單一登入](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="4355b-122">若要下載憑證以用於 Dropbox 設定，請選取 [設定 DropBox]，然後選取清單中的 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4355b-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![下載可用於 Dropbox 設定的憑證](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="4355b-124">從 [單一登入] 頁面，使用登入 URL 登入 Dropbox。</span><span class="sxs-lookup"><span data-stu-id="4355b-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Dropbox 登入頁面](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="4355b-126">在功能表上，選取 [系統管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="4355b-126">On the menu, select **Admin Console**.</span></span>

  ![Dropbox 功能表上的 [系統管理員主控台] 連結](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="4355b-128">在 [驗證] 對話方塊中，選取 [更多]上傳憑證，然後在 [登入 URL] 方塊中，輸入 SAML 單一登入 URL。</span><span class="sxs-lookup"><span data-stu-id="4355b-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![摺疊的 [驗證] 對話方塊中的 [更多] 連結](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![展開的 [驗證] 對話方塊中的 [登入 URL]](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="4355b-131">若要在 Azure 入口網站中設定自動使用者設定，請選取左窗格中的 [佈建]、選取 [佈建模式] 方塊中的 [自動]，然後選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="4355b-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![在 Azure 入口網站中設定自動使用者佈建](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="4355b-133">在 Dropbox 應用程式中設定來賓或成員使用者之後，他們就會收到來自 Dropbox 的個別邀請。</span><span class="sxs-lookup"><span data-stu-id="4355b-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="4355b-134">若要使用 Dropbox 單一登入，受邀者必須藉由按一下邀請中的連結來接受邀請。</span><span class="sxs-lookup"><span data-stu-id="4355b-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="4355b-135">Box</span><span class="sxs-lookup"><span data-stu-id="4355b-135">Box</span></span>
<span data-ttu-id="4355b-136">使用以 SAML 通訊協定為基礎的同盟，即可讓使用者使用其 Azure AD 帳戶來驗證 Box 來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="4355b-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="4355b-137">在此程序中，您會將中繼資料上傳至 Box.com。</span><span class="sxs-lookup"><span data-stu-id="4355b-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="4355b-138">從企業應用程式新增 Box 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4355b-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="4355b-139">請依下列順序設定單一登入：</span><span class="sxs-lookup"><span data-stu-id="4355b-139">Configure single sign-on in the following order:</span></span>

  ![設定 Box 單一登入](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="4355b-141">a.</span><span class="sxs-lookup"><span data-stu-id="4355b-141">a.</span></span> <span data-ttu-id="4355b-142">在 [登入 URL] 方塊中，確定已在 Azure 入口網站中針對 Box 適當設定登入 URL。</span><span class="sxs-lookup"><span data-stu-id="4355b-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="4355b-143">此 URL 是 Box.com 租用戶的 URL。</span><span class="sxs-lookup"><span data-stu-id="4355b-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="4355b-144">它應該遵循命名慣例 https://.box.com。</span><span class="sxs-lookup"><span data-stu-id="4355b-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="4355b-145">[識別碼] 不適用於此應用程式，但它仍會顯示為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="4355b-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="4355b-146">b.</span><span class="sxs-lookup"><span data-stu-id="4355b-146">b.</span></span> <span data-ttu-id="4355b-147">在 [使用者識別碼] 方塊中，輸入 **user.mail** (適用於來賓帳戶的 SSO)。</span><span class="sxs-lookup"><span data-stu-id="4355b-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="4355b-148">c.</span><span class="sxs-lookup"><span data-stu-id="4355b-148">c.</span></span> <span data-ttu-id="4355b-149">在 [SAML 簽署憑證] 之下，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="4355b-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="4355b-150">d.</span><span class="sxs-lookup"><span data-stu-id="4355b-150">d.</span></span> <span data-ttu-id="4355b-151">若要開始將 Box.com 租用戶設定成使用 Azure AD 做為識別提供者，請下載中繼資料檔案，然後將它儲存到本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="4355b-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="4355b-152">e.</span><span class="sxs-lookup"><span data-stu-id="4355b-152">e.</span></span> <span data-ttu-id="4355b-153">將設定單一登入的中繼資料檔案轉寄給 Box 支援小組。</span><span class="sxs-lookup"><span data-stu-id="4355b-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="4355b-154">若要進行 Azure AD 自動使用者設定，請在左窗格中選取 [佈建]，然後選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="4355b-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![授權 Azure AD 以連線到 Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="4355b-156">如同 Dropbox 受邀者，Box 受邀者也必須從 Box 應用程式兌換其邀請。</span><span class="sxs-lookup"><span data-stu-id="4355b-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4355b-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4355b-157">Next steps</span></span>

<span data-ttu-id="4355b-158">請參閱下列有關 Azure AD B2B 共同作業的文章：</span><span class="sxs-lookup"><span data-stu-id="4355b-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4355b-159">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="4355b-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4355b-160">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="4355b-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4355b-161">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="4355b-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4355b-162">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="4355b-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4355b-163">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="4355b-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4355b-164">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="4355b-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4355b-165">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="4355b-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4355b-166">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="4355b-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4355b-167">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="4355b-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="4355b-168">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="4355b-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
