---
title: "aaaSingle 登入的 hello Azure Active Directory 中的企業應用程式管理 |Microsoft 文件"
description: "了解如何 toomanage 單一登入企業應用程式使用 hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a><span data-ttu-id="0ff86-103">管理企業應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="0ff86-103">Managing single sign-on for enterprise apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ff86-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0ff86-104">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="0ff86-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="0ff86-105">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
> 

<span data-ttu-id="0ff86-106">本文說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)toomanage 單一登入企業應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="0ff86-106">This article describes how toouse hello [Azure portal](https://portal.azure.com) toomanage single sign-on settings for enterprise applications.</span></span> <span data-ttu-id="0ff86-107">企業應用程式是您組織內部署和使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-107">Enterprise apps are apps that are deployed and used within your organization.</span></span> <span data-ttu-id="0ff86-108">本文件適用於特別 hello 從已加入的 tooapps [Azure Active Directory 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)。</span><span class="sxs-lookup"><span data-stu-id="0ff86-108">This article applies particularly tooapps that were added from hello [Azure Active Directory application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery).</span></span> 

## <a name="finding-your-apps-in-hello-portal"></a><span data-ttu-id="0ff86-109">在 [hello 入口網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="0ff86-109">Finding your apps in hello portal</span></span>
<span data-ttu-id="0ff86-110">您已設定單一登入的所有企業應用程式可以檢視及管理 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0ff86-110">All enterprise apps that are set up for single sign-on can be viewed and managed in hello Azure portal.</span></span> <span data-ttu-id="0ff86-111">hello 應用程式可以在 hello**更服務** &gt; **企業應用程式**hello 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="0ff86-111">hello applications can be found in hello **More Services** &gt; **Enterprise Applications** section of hello portal.</span></span> 

![企業應用程式刀鋒視窗][1]

<span data-ttu-id="0ff86-113">選取**所有應用程式**tooview 已設定的所有應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0ff86-113">Select **All applications** tooview a list of all apps that have been configured.</span></span> <span data-ttu-id="0ff86-114">選取應用程式載入 hello 資源刀鋒視窗，該應用程式，其中可以檢視報告，該應用程式，且可管理各種不同的設定。</span><span class="sxs-lookup"><span data-stu-id="0ff86-114">Selecting an app loads hello resource blade for that app, where reports can be viewed for that app and a variety of settings can be managed.</span></span>

<span data-ttu-id="0ff86-115">toomanage 單一登入設定，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0ff86-115">toomanage single sign-on settings, select **Single sign-on**.</span></span>

![應用程式資源刀鋒視窗][2]

## <a name="single-sign-on-modes"></a><span data-ttu-id="0ff86-117">單一登入模式</span><span class="sxs-lookup"><span data-stu-id="0ff86-117">Single sign-on modes</span></span>
<span data-ttu-id="0ff86-118">hello**單一登入**刀鋒視窗開頭**模式**功能表上，可讓 hello 單一登入模式 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="0ff86-118">hello **Single sign-on** blade begins with a **Mode** menu, which allows hello single sign-on mode toobe configured.</span></span> <span data-ttu-id="0ff86-119">hello 可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="0ff86-119">hello available options include:</span></span>

* <span data-ttu-id="0ff86-120">**SAML 型登入**-這個選項才可以使用 hello 應用程式與 Azure Active Directory 使用 hello SAML 2.0 通訊協定支援完整同盟單一登入。</span><span class="sxs-lookup"><span data-stu-id="0ff86-120">**SAML-based sign on** - This option is available if hello application supports full federated single sign-on with Azure Active Directory using hello SAML 2.0 protocol.</span></span>
* <span data-ttu-id="0ff86-121">**密碼型登入** - 如果 Azure AD 支援此應用程式的密碼表單填入，便可使用此選項。</span><span class="sxs-lookup"><span data-stu-id="0ff86-121">**Password-based sign on** - This option is available if Azure AD supports password form filling for this application.</span></span>
* <span data-ttu-id="0ff86-122">**連結登入**-稱為 [現有單一登入 」，此選項可讓系統管理員 tooplace 連結 toothis 應用程式中使用者的 Azure AD 存取面板或 Office 365 應用程式的啟動程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-122">**Linked sign on** - Formerly known as "Existing single sign-on", this option allows administrators tooplace a link toothis application in their user's Azure AD Access Panel or Office 365 application launcher.</span></span>

<span data-ttu-id="0ff86-123">如需這些模式的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="0ff86-123">For more information about these modes, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="saml-based-sign-on"></a><span data-ttu-id="0ff86-124">SAML 型登入</span><span class="sxs-lookup"><span data-stu-id="0ff86-124">SAML-based sign-on</span></span>
<span data-ttu-id="0ff86-125">hello **SAML 型登入**選項會顯示分成四個區段的刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="0ff86-125">hello **SAML-based sign on** option displays a blade that is divided in four sections:</span></span>

### <a name="domains-and-urls"></a><span data-ttu-id="0ff86-126">網域和 URL</span><span class="sxs-lookup"><span data-stu-id="0ff86-126">Domains and URLs</span></span>
<span data-ttu-id="0ff86-127">這是加入 hello 應用程式網域和 Url 的所有詳細 tooyour Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="0ff86-127">This is where all details about hello application's domain and URLs are added tooyour Azure AD directory.</span></span> <span data-ttu-id="0ff86-128">所有輸入所都需 toomake 單一登入工作的應用程式會顯示直接在 hello 畫面上，而選取 hello 也可以檢視所有選擇性輸入**顯示進階的 URL 設定**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0ff86-128">All inputs required toomake single sign-on work app are displayed directly on hello screen, whereas all optional inputs can be viewed by selecting hello **Show advanced URL settings** checkbox.</span></span> <span data-ttu-id="0ff86-129">支援輸入 hello 完整清單包括：</span><span class="sxs-lookup"><span data-stu-id="0ff86-129">hello full list of supported inputs includes:</span></span>

* <span data-ttu-id="0ff86-130">**登入 URL** – 其中 hello 使用者進入 toosign 中 toothis 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-130">**Sign On URL** – Where hello user goes toosign-in toothis application.</span></span> <span data-ttu-id="0ff86-131">如果當使用者瀏覽 toothis URL，hello 服務提供者未 hello 必要則 hello 應用程式設定的 tooperform 服務提供者起始單一登入，重新導向 tooAzure AD tooauthenticate 並登入 hello 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="0ff86-131">If hello application is configured tooperform service provider-initiated single sign on, then when a user navigates toothis URL, hello service provider does hello necessary redirection tooAzure AD tooauthenticate and sign hello user in.</span></span> <span data-ttu-id="0ff86-132">如果已填入此欄位，Azure AD 會使用 Office 365 和 Azure AD 存取面板 hello 這個 URL toolaunch hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-132">If this field is populated, then Azure AD will use this URL toolaunch hello application from Office 365 and hello Azure AD Access Panel.</span></span> <span data-ttu-id="0ff86-133">如果省略此欄位，則 Azure AD 會改為執行身分識別提供者-初始的登入 hello 應用程式啟動時從 Office 365、 Azure AD 存取面板 hello 或 hello Azure AD 單一登入 URL。</span><span class="sxs-lookup"><span data-stu-id="0ff86-133">If this field is omitted, then Azure AD instead performs identity provider -initiated sign on when hello app is launched from Office 365, hello Azure AD Access Panel, or from hello Azure AD single sign-on URL.</span></span>
* <span data-ttu-id="0ff86-134">**識別項**-這個 URI 應專門用於識別 hello 應用程式所設定的單一登入。</span><span class="sxs-lookup"><span data-stu-id="0ff86-134">**Identifier** - This URI should uniquely identify hello application for which single sign on is being configured.</span></span> <span data-ttu-id="0ff86-135">這是 Azure AD 會傳送後 tooapplication hello hello SAML 權杖中，對象參數時，和 hello 應用程式是預期的 toovalidate hello 值它。</span><span class="sxs-lookup"><span data-stu-id="0ff86-135">This is hello value that Azure AD sends back tooapplication as hello Audience parameter of hello SAML token, and hello application is expected toovalidate it.</span></span> <span data-ttu-id="0ff86-136">這個值也會顯示為 hello 應用程式所提供的任何 SAML 中繼資料中的實體識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="0ff86-136">This value also appears as hello Entity ID in any SAML metadata provided by hello application.</span></span>
* <span data-ttu-id="0ff86-137">**回覆 URL** -hello 回覆 URL 是 hello 應用程式預期 tooreceive hello SAML 權杖中的位置。</span><span class="sxs-lookup"><span data-stu-id="0ff86-137">**Reply URL** - hello reply URL is where hello application expects tooreceive hello SAML token.</span></span> <span data-ttu-id="0ff86-138">這也是參考的 tooas hello 判斷提示取用者服務 (ACS) URL。</span><span class="sxs-lookup"><span data-stu-id="0ff86-138">This is also referred tooas hello Assertion Consumer Service (ACS) URL.</span></span> <span data-ttu-id="0ff86-139">這些輸入之後，畫面上，按 [下一步 tooproceed toohello 下一步]。</span><span class="sxs-lookup"><span data-stu-id="0ff86-139">After these have been entered, click Next tooproceed toohello next screen.</span></span> <span data-ttu-id="0ff86-140">此畫面會提供哪些需求 toobe 上設定 hello 應用程式端 tooenable 它 tooaccept 來自 Azure AD SAML 權杖的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0ff86-140">This screen provides information about what needs toobe configured on hello application side tooenable it tooaccept a SAML token from Azure AD.</span></span>
* <span data-ttu-id="0ff86-141">**轉送狀態**-hello 轉送狀態是選擇性參數，可協助分辨 hello 應用程式其中 tooredirect hello 使用者驗證完成後。</span><span class="sxs-lookup"><span data-stu-id="0ff86-141">**Relay State** -  hello relay state is an optional parameter that can help tell hello application where tooredirect hello user after authentication is completed.</span></span> <span data-ttu-id="0ff86-142">Hello 值通常是在 hello 應用程式中，有效的 URL，不過有些應用程式以不同的方式使用此欄位 （在文件，如需詳細資訊，請參閱 hello 應用程式的單一登）。</span><span class="sxs-lookup"><span data-stu-id="0ff86-142">Typically hello value is a valid URL at hello application, however some applications use this field differently (see hello app's single sign on documentation for details).</span></span> <span data-ttu-id="0ff86-143">hello 能力 tooset hello 轉送狀態會是唯一的 toohello 新版 Azure 入口網站的新功能。</span><span class="sxs-lookup"><span data-stu-id="0ff86-143">hello ability tooset hello relay state is a new feature that is unique toohello new Azure portal.</span></span>

### <a name="user-attributes"></a><span data-ttu-id="0ff86-144">使用者屬性</span><span class="sxs-lookup"><span data-stu-id="0ff86-144">User Attributes</span></span>
<span data-ttu-id="0ff86-145">這是系統管理員可以檢視和編輯 hello 屬性傳送嗨 SAML 權杖中，Azure AD 會發出 toohello 應用程式每次使用者登入位置。</span><span class="sxs-lookup"><span data-stu-id="0ff86-145">This is where admins can view and edit hello attributes that are sent in hello SAML token that Azure AD issues toohello application each time users sign in.</span></span>

<span data-ttu-id="0ff86-146">僅支援可編輯的屬性為 hello hello**使用者識別碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="0ff86-146">hello only editable attribute supported is hello **User Identifier** attribute.</span></span> <span data-ttu-id="0ff86-147">hello 這個屬性的值是唯一識別 hello 應用程式中的每個使用者的 Azure AD 中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="0ff86-147">hello value of this attribute is hello field in Azure AD that uniquely identifies each user within hello application.</span></span> <span data-ttu-id="0ff86-148">例如，如果 hello 應用程式已部署為 hello 使用者名稱和唯一識別碼使用 hello 」 電子郵件地址 」，然後 hello 值會設定 toohello"user.mail"欄位在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0ff86-148">For example, if hello app was deployed using hello "Email address" as hello username and unique identifier, then hello value would be set toohello "user.mail" field in Azure AD.</span></span>

### <a name="saml-signing-certificate"></a><span data-ttu-id="0ff86-149">SAML 簽署憑證</span><span class="sxs-lookup"><span data-stu-id="0ff86-149">SAML Signing Certificate</span></span>
<span data-ttu-id="0ff86-150">此區段會顯示 hello hello Azure AD 使用 toosign hello SAML 權杖 toohello 應用程式會驗證每個時間 hello 使用者發出的憑證詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ff86-150">This section shows hello details of hello certificate that Azure AD uses toosign hello SAML tokens that are issued toohello application each time hello user authenticates.</span></span> <span data-ttu-id="0ff86-151">它可讓 hello hello 目前憑證 toobe 檢查，包括 hello 到期日屬性。</span><span class="sxs-lookup"><span data-stu-id="0ff86-151">It allows hello properties of hello current certificate toobe inspected, including hello expiration date.</span></span>

### <a name="application-configuration"></a><span data-ttu-id="0ff86-152">應用程式組態</span><span class="sxs-lookup"><span data-stu-id="0ff86-152">Application Configuration</span></span>
<span data-ttu-id="0ff86-153">hello 最後一節提供 hello 文件及/或控制項需要的 tooconfigure hello 應用程式本身 toouse Azure Active Directory 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="0ff86-153">hello final section provides hello documentation and/or controls required tooconfigure hello application itself toouse Azure Active Directory as an identity provider.</span></span>

<span data-ttu-id="0ff86-154">hello**設定應用程式**出現的功能表提供新簡潔的內嵌設定指示 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-154">hello **Configure Application** fly-out menu provides new concise, embedded instructions for configuring hello application.</span></span> <span data-ttu-id="0ff86-155">這是另一個新功能唯一 toohello 新版 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0ff86-155">This is another new feature unique toohello new Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0ff86-156">針對內嵌文件的完整範例，請參閱 hello Salesforce.com 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-156">For a complete example of embedded documentation, see hello Salesforce.com application.</span></span> <span data-ttu-id="0ff86-157">將持續新增其他應用程式的文件。</span><span class="sxs-lookup"><span data-stu-id="0ff86-157">Documentation for additional apps is being continually added.</span></span>
> 
> 

![內嵌的文件][3]

## <a name="password-based-sign-on"></a><span data-ttu-id="0ff86-159">密碼型登入</span><span class="sxs-lookup"><span data-stu-id="0ff86-159">Password-based sign on</span></span>
<span data-ttu-id="0ff86-160">如果支援 hello 應用程式，則選取 hello 密碼型 SSO 模式，然後選取**儲存**立即將它設定 toodo 密碼登入。</span><span class="sxs-lookup"><span data-stu-id="0ff86-160">If supported for hello application, selecting hello password-based SSO mode and selecting **Save** instantly configures it toodo password-based SSO.</span></span> <span data-ttu-id="0ff86-161">如需部署密碼型 SSO 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="0ff86-161">For more information about deploying password-based SSO, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![密碼型登入][4]

## <a name="linked-sign-on"></a><span data-ttu-id="0ff86-163">連結型登入</span><span class="sxs-lookup"><span data-stu-id="0ff86-163">Linked sign on</span></span>
<span data-ttu-id="0ff86-164">如果支援 hello 應用程式，則選取連結的 hello SSO 模式可讓您 tooenter hello URL 想 hello Azure AD 存取面板或 Office 365 tooredirect toowhen 使用者按一下此應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ff86-164">If supported for hello application, selecting hello linked SSO mode allows you tooenter hello URL that you want hello Azure AD Access Panel or Office 365 tooredirect toowhen users click on this app.</span></span> <span data-ttu-id="0ff86-165">如需連結型 SSO (以前稱為「現有 SSO」) 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="0ff86-165">For more information about linked SSO (formerly known as "existing SSO"), see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![連結型單一登入][5]

##<a name="feedback"></a><span data-ttu-id="0ff86-167">意見反應</span><span class="sxs-lookup"><span data-stu-id="0ff86-167">Feedback</span></span>

<span data-ttu-id="0ff86-168">我們希望您希望使用 hello 改善 Azure AD 的體驗。</span><span class="sxs-lookup"><span data-stu-id="0ff86-168">We hope you like using hello improved Azure AD experience.</span></span> <span data-ttu-id="0ff86-169">請保留來自 hello 意見反應 ！</span><span class="sxs-lookup"><span data-stu-id="0ff86-169">Please keep hello feedback coming!</span></span> <span data-ttu-id="0ff86-170">將張貼到您的意見反應與改進的想法 hello**管理入口**區段我們[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)。</span><span class="sxs-lookup"><span data-stu-id="0ff86-170">Post your feedback and ideas for improvement in hello **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="0ff86-171">我們正在興奮每一天，建置新很棒的相關指引 tooshape 和使用什麼接下來要建立的定義。</span><span class="sxs-lookup"><span data-stu-id="0ff86-171">We’re excited about building cool new stuff every day, and use your guidance tooshape and define what we build next.</span></span>

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
