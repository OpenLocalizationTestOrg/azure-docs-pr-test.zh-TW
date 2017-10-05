---
title: "在 Azure Active Directory 中管理企業應用程式的單一登入 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory 管理企業應用程式的單一登入"
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
ms.openlocfilehash: c975428550690254ba989935fe5110c5903e7102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a><span data-ttu-id="cdcab-103">管理企業應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="cdcab-103">Managing single sign-on for enterprise apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdcab-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cdcab-104">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="cdcab-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="cdcab-105">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
> 

<span data-ttu-id="cdcab-106">本文說明如何使用 [Azure 入口網站](https://portal.azure.com)來管理企業應用程式的單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="cdcab-106">This article describes how to use the [Azure portal](https://portal.azure.com) to manage single sign-on settings for enterprise applications.</span></span> <span data-ttu-id="cdcab-107">企業應用程式是您組織內部署和使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-107">Enterprise apps are apps that are deployed and used within your organization.</span></span> <span data-ttu-id="cdcab-108">本文特別適用於從 [Azure Active Directory 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)新增的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-108">This article applies particularly to apps that were added from the [Azure Active Directory application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery).</span></span> 

## <a name="finding-your-apps-in-the-portal"></a><span data-ttu-id="cdcab-109">在入口網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="cdcab-109">Finding your apps in the portal</span></span>
<span data-ttu-id="cdcab-110">在 Azure 入口網站中可以檢視及管理針對單一登入設定的所有企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-110">All enterprise apps that are set up for single sign-on can be viewed and managed in the Azure portal.</span></span> <span data-ttu-id="cdcab-111">這些應用程式可在入口網站的 [更多服務] &gt; [企業應用程式] 區段中找到。</span><span class="sxs-lookup"><span data-stu-id="cdcab-111">The applications can be found in the **More Services** &gt; **Enterprise Applications** section of the portal.</span></span> 

![企業應用程式刀鋒視窗][1]

<span data-ttu-id="cdcab-113">選取 [所有應用程式] 以檢視已設定的所有應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="cdcab-113">Select **All applications** to view a list of all apps that have been configured.</span></span> <span data-ttu-id="cdcab-114">選取應用程式會載入該應用程式的資源刀鋒視窗，您可以在其中檢視該應用程式的報告，且可管理各種設定。</span><span class="sxs-lookup"><span data-stu-id="cdcab-114">Selecting an app loads the resource blade for that app, where reports can be viewed for that app and a variety of settings can be managed.</span></span>

<span data-ttu-id="cdcab-115">若要管理單一登入設定，請選取 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="cdcab-115">To manage single sign-on settings, select **Single sign-on**.</span></span>

![應用程式資源刀鋒視窗][2]

## <a name="single-sign-on-modes"></a><span data-ttu-id="cdcab-117">單一登入模式</span><span class="sxs-lookup"><span data-stu-id="cdcab-117">Single sign-on modes</span></span>
<span data-ttu-id="cdcab-118">[單一登入] 刀鋒視窗一開始是 [模式] 功能表，可在此設定單一登入模式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-118">The **Single sign-on** blade begins with a **Mode** menu, which allows the single sign-on mode to be configured.</span></span> <span data-ttu-id="cdcab-119">可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="cdcab-119">The available options include:</span></span>

* <span data-ttu-id="cdcab-120">**SAML 型登入** - 如果應用程式支援使用 SAML 2.0 通訊協定的 Azure Active Directory 完整同盟單一登入，便可使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cdcab-120">**SAML-based sign on** - This option is available if the application supports full federated single sign-on with Azure Active Directory using the SAML 2.0 protocol.</span></span>
* <span data-ttu-id="cdcab-121">**密碼型登入** - 如果 Azure AD 支援此應用程式的密碼表單填入，便可使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cdcab-121">**Password-based sign on** - This option is available if Azure AD supports password form filling for this application.</span></span>
* <span data-ttu-id="cdcab-122">**連結型登入** - 之前稱為「現有單一登入」，此選項可讓管理員將此應用程式的連結放在其使用者的 Azure AD 存取面板或 Office 365 應用程式啟動程式中。</span><span class="sxs-lookup"><span data-stu-id="cdcab-122">**Linked sign on** - Formerly known as "Existing single sign-on", this option allows administrators to place a link to this application in their user's Azure AD Access Panel or Office 365 application launcher.</span></span>

<span data-ttu-id="cdcab-123">如需這些模式的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="cdcab-123">For more information about these modes, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="saml-based-sign-on"></a><span data-ttu-id="cdcab-124">SAML 型登入</span><span class="sxs-lookup"><span data-stu-id="cdcab-124">SAML-based sign-on</span></span>
<span data-ttu-id="cdcab-125">選取 **SAML 型登入** 選項會顯示分成四個部分的刀鋒視窗︰</span><span class="sxs-lookup"><span data-stu-id="cdcab-125">The **SAML-based sign on** option displays a blade that is divided in four sections:</span></span>

### <a name="domains-and-urls"></a><span data-ttu-id="cdcab-126">網域和 URL</span><span class="sxs-lookup"><span data-stu-id="cdcab-126">Domains and URLs</span></span>
<span data-ttu-id="cdcab-127">這個部分顯示已加入您的 Azure AD 目錄的應用程式網域和 URL 的所有詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cdcab-127">This is where all details about the application's domain and URLs are added to your Azure AD directory.</span></span> <span data-ttu-id="cdcab-128">應用程式單一登入運作所需的所有輸入都會直接顯示在畫面上，選取 [顯示進階 URL 設定]  核取方塊可以檢視所有選擇性輸入。</span><span class="sxs-lookup"><span data-stu-id="cdcab-128">All inputs required to make single sign-on work app are displayed directly on the screen, whereas all optional inputs can be viewed by selecting the **Show advanced URL settings** checkbox.</span></span> <span data-ttu-id="cdcab-129">支援的輸入有︰</span><span class="sxs-lookup"><span data-stu-id="cdcab-129">The full list of supported inputs includes:</span></span>

* <span data-ttu-id="cdcab-130">**登入 URL** – 使用者將由此處登入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-130">**Sign On URL** – Where the user goes to sign-in to this application.</span></span> <span data-ttu-id="cdcab-131">如果應用程式設定為執行服務提供者起始單一登入，則當使用者導覽到此 URL，服務提供者會執行必要的重新導向至 Azure AD，以進行驗證並將使用者登入。</span><span class="sxs-lookup"><span data-stu-id="cdcab-131">If the application is configured to perform service provider-initiated single sign on, then when a user navigates to this URL, the service provider does the necessary redirection to Azure AD to authenticate and sign the user in.</span></span> <span data-ttu-id="cdcab-132">如果已填入此欄位，Azure AD 將使用此 URL 從 Office 365 和 Azure AD 存取面板中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-132">If this field is populated, then Azure AD will use this URL to launch the application from Office 365 and the Azure AD Access Panel.</span></span> <span data-ttu-id="cdcab-133">++如果略過這個欄位，則 Azure AD 會改為執行身分識別提供者 - 即從 Office 365、Azure AD 存取面板或 Azure AD 單一登入 URL 啟動應用程式時起始登入。</span><span class="sxs-lookup"><span data-stu-id="cdcab-133">If this field is omitted, then Azure AD instead performs identity provider -initiated sign on when the app is launched from Office 365, the Azure AD Access Panel, or from the Azure AD single sign-on URL.</span></span>
* <span data-ttu-id="cdcab-134">**識別碼** - 此 URI 應專門用於識別正在設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-134">**Identifier** - This URI should uniquely identify the application for which single sign on is being configured.</span></span> <span data-ttu-id="cdcab-135">Azure AD 會將此值傳送回應用程式做為 SAML 權杖的 Audience 參數值，應用程式預期會驗證它。</span><span class="sxs-lookup"><span data-stu-id="cdcab-135">This is the value that Azure AD sends back to application as the Audience parameter of the SAML token, and the application is expected to validate it.</span></span> <span data-ttu-id="cdcab-136">在應用程式中提供的任何 SAML 中繼資料中，此值也會顯示為實體識別碼。</span><span class="sxs-lookup"><span data-stu-id="cdcab-136">This value also appears as the Entity ID in any SAML metadata provided by the application.</span></span>
* <span data-ttu-id="cdcab-137">**回覆 URL** -回覆 URL 是應用程式預期接收 SAML 權杖的位置。</span><span class="sxs-lookup"><span data-stu-id="cdcab-137">**Reply URL** - The reply URL is where the application expects to receive the SAML token.</span></span> <span data-ttu-id="cdcab-138">這也稱為判斷提示取用者服務 (ACS) URL。</span><span class="sxs-lookup"><span data-stu-id="cdcab-138">This is also referred to as the Assertion Consumer Service (ACS) URL.</span></span> <span data-ttu-id="cdcab-139">在輸入這些資料後，請按 [下一步] 繼續前往下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="cdcab-139">After these have been entered, click Next to proceed to the next screen.</span></span> <span data-ttu-id="cdcab-140">此畫面會提供相關資訊來說明在應用程式端需要進行哪些設定，才能使應用程式接受來自於 Azure AD 的 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="cdcab-140">This screen provides information about what needs to be configured on the application side to enable it to accept a SAML token from Azure AD.</span></span>
* <span data-ttu-id="cdcab-141">**轉送狀態** - 轉送狀態是選擇性參數，可幫助告知應用程式在驗證完成後，將使用者重新導向的位置。</span><span class="sxs-lookup"><span data-stu-id="cdcab-141">**Relay State** -  The relay state is an optional parameter that can help tell the application where to redirect the user after authentication is completed.</span></span> <span data-ttu-id="cdcab-142">此值通常是對應用程式有效的 URL ，不過有些應用程式以不同方式使用此值 (詳細資訊請參閱應用程式的單一登入相關文件)。</span><span class="sxs-lookup"><span data-stu-id="cdcab-142">Typically the value is a valid URL at the application, however some applications use this field differently (see the app's single sign on documentation for details).</span></span> <span data-ttu-id="cdcab-143">設定轉送狀態的功能是新 Azure 入口網站獨有的新功能。</span><span class="sxs-lookup"><span data-stu-id="cdcab-143">The ability to set the relay state is a new feature that is unique to the new Azure portal.</span></span>

### <a name="user-attributes"></a><span data-ttu-id="cdcab-144">使用者屬性</span><span class="sxs-lookup"><span data-stu-id="cdcab-144">User Attributes</span></span>
<span data-ttu-id="cdcab-145">這個部分可供管理員檢視及編輯 SAML 權杖中傳送的屬性，而此權杖是在使用者每次登入時由 Azure AD 簽發給應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-145">This is where admins can view and edit the attributes that are sent in the SAML token that Azure AD issues to the application each time users sign in.</span></span>

<span data-ttu-id="cdcab-146">唯一支援的可編輯屬性是 **User Identifier** 屬性。</span><span class="sxs-lookup"><span data-stu-id="cdcab-146">The only editable attribute supported is the **User Identifier** attribute.</span></span> <span data-ttu-id="cdcab-147">這個屬性的值是 Azure AD 中可唯一識別應用程式中每個使用者的欄位。</span><span class="sxs-lookup"><span data-stu-id="cdcab-147">The value of this attribute is the field in Azure AD that uniquely identifies each user within the application.</span></span> <span data-ttu-id="cdcab-148">例如，如果應用程式為使用電子郵件地址做為使用者名稱和唯一識別碼，則此值會設為 Azure AD 中的 user.mail 欄位。</span><span class="sxs-lookup"><span data-stu-id="cdcab-148">For example, if the app was deployed using the "Email address" as the username and unique identifier, then the value would be set to the "user.mail" field in Azure AD.</span></span>

### <a name="saml-signing-certificate"></a><span data-ttu-id="cdcab-149">SAML 簽署憑證</span><span class="sxs-lookup"><span data-stu-id="cdcab-149">SAML Signing Certificate</span></span>
<span data-ttu-id="cdcab-150">這個部分顯示 Azure AD 用來簽署 SAML 權杖 (於每次使用者驗證時簽發給應用程式) 的憑證詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cdcab-150">This section shows the details of the certificate that Azure AD uses to sign the SAML tokens that are issued to the application each time the user authenticates.</span></span> <span data-ttu-id="cdcab-151">可用來檢查目前憑證的內容，包括到期日。</span><span class="sxs-lookup"><span data-stu-id="cdcab-151">It allows the properties of the current certificate to be inspected, including the expiration date.</span></span>

### <a name="application-configuration"></a><span data-ttu-id="cdcab-152">應用程式組態</span><span class="sxs-lookup"><span data-stu-id="cdcab-152">Application Configuration</span></span>
<span data-ttu-id="cdcab-153">最後一個部分提供文件和/或設定應用程式本身使用 Azure Active Directory 做為身分識別提供者所需的控制項。</span><span class="sxs-lookup"><span data-stu-id="cdcab-153">The final section provides the documentation and/or controls required to configure the application itself to use Azure Active Directory as an identity provider.</span></span>

<span data-ttu-id="cdcab-154">[設定應用程式]  彈出式功能表提供新的、簡潔、內嵌的應用程式設定指示。</span><span class="sxs-lookup"><span data-stu-id="cdcab-154">The **Configure Application** fly-out menu provides new concise, embedded instructions for configuring the application.</span></span> <span data-ttu-id="cdcab-155">這是新 Azure 入口網站另一個獨有的新功能。</span><span class="sxs-lookup"><span data-stu-id="cdcab-155">This is another new feature unique to the new Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cdcab-156">如需內嵌文件的完整範例，請參閱 Salesforce.com 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-156">For a complete example of embedded documentation, see the Salesforce.com application.</span></span> <span data-ttu-id="cdcab-157">將持續新增其他應用程式的文件。</span><span class="sxs-lookup"><span data-stu-id="cdcab-157">Documentation for additional apps is being continually added.</span></span>
> 
> 

![內嵌的文件][3]

## <a name="password-based-sign-on"></a><span data-ttu-id="cdcab-159">密碼型登入</span><span class="sxs-lookup"><span data-stu-id="cdcab-159">Password-based sign on</span></span>
<span data-ttu-id="cdcab-160">如果應用程式支援此種登入，選取密碼型 SSO 模式，然後選取 [儲存]  ，即可立即將它設定為進行密碼型 SSO。</span><span class="sxs-lookup"><span data-stu-id="cdcab-160">If supported for the application, selecting the password-based SSO mode and selecting **Save** instantly configures it to do password-based SSO.</span></span> <span data-ttu-id="cdcab-161">如需部署密碼型 SSO 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="cdcab-161">For more information about deploying password-based SSO, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![密碼型登入][4]

## <a name="linked-sign-on"></a><span data-ttu-id="cdcab-163">連結型登入</span><span class="sxs-lookup"><span data-stu-id="cdcab-163">Linked sign on</span></span>
<span data-ttu-id="cdcab-164">如果應用程式支援此種登入，選取連結的 SSO 模式可讓您輸入 URL，做為當使用者按一下此應用程式時您想要 Azure AD 存取面板或 Office 365 重新導向的目標。</span><span class="sxs-lookup"><span data-stu-id="cdcab-164">If supported for the application, selecting the linked SSO mode allows you to enter the URL that you want the Azure AD Access Panel or Office 365 to redirect to when users click on this app.</span></span> <span data-ttu-id="cdcab-165">如需連結型 SSO (以前稱為「現有 SSO」) 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="cdcab-165">For more information about linked SSO (formerly known as "existing SSO"), see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![連結型單一登入][5]

##<a name="feedback"></a><span data-ttu-id="cdcab-167">意見反應</span><span class="sxs-lookup"><span data-stu-id="cdcab-167">Feedback</span></span>

<span data-ttu-id="cdcab-168">我們希望您喜歡使用改進後的 Azure AD 經驗。</span><span class="sxs-lookup"><span data-stu-id="cdcab-168">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="cdcab-169">請繼續提供意見反應！</span><span class="sxs-lookup"><span data-stu-id="cdcab-169">Please keep the feedback coming!</span></span> <span data-ttu-id="cdcab-170">請將您的意見反應和改進想法張貼在我們的[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)的**管理員入口網站**區段中。</span><span class="sxs-lookup"><span data-stu-id="cdcab-170">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="cdcab-171">我們每天都很期待發展酷炫的新功能，並依照您的指導來塑造和定義我們接下來所要發展的項目。</span><span class="sxs-lookup"><span data-stu-id="cdcab-171">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
