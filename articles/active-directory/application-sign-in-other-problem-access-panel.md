---
title: "登入 tooan hello 存取面板應用程式的 aaaProblems |Microsoft 文件"
description: "如何從應用程式存取 tootroubleshoot 問題 hello myapps.microsoft.com Microsoft Azure AD 存取面板"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="5dbac-103">登入 tooan hello 存取面板應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="5dbac-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="5dbac-104">hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。</span><span class="sxs-lookup"><span data-stu-id="5dbac-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="5dbac-105">這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="5dbac-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="5dbac-106">hello 應用程式必須正確設定並指派的 toohello 使用者或群組 hello 使用者是 toosee hello 存取面板中的 hello 應用程式的成員。</span><span class="sxs-lookup"><span data-stu-id="5dbac-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="5dbac-107">應用程式的使用者會看見 hello 類型落在 hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="5dbac-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="5dbac-108">Office 365 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-108">Office 365 Applications</span></span>

-   <span data-ttu-id="5dbac-109">已設定同盟 SSO 的 Microsoft 及第三方應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="5dbac-110">密碼型 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="5dbac-111">含現有 SSO 解決方案的應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="5dbac-112">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="5dbac-112">General issues toocheck first</span></span>

-   <span data-ttu-id="5dbac-113">請確定您使用**瀏覽器**符合 hello hello 存取面板的最低需求。</span><span class="sxs-lookup"><span data-stu-id="5dbac-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="5dbac-114">請確定 hello 使用者的瀏覽器已新增的 hello 應用程式 tooits hello URL**信任的網站**。</span><span class="sxs-lookup"><span data-stu-id="5dbac-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="5dbac-115">請確定 toocheck hello 應用程式是**設定**正確。</span><span class="sxs-lookup"><span data-stu-id="5dbac-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="5dbac-116">請確定 hello 使用者帳戶是**啟用**的登入。</span><span class="sxs-lookup"><span data-stu-id="5dbac-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="5dbac-117">請確定 hello 使用者帳戶是**並未鎖定。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="5dbac-118">請確定 hello 使用者的**密碼未過期或遺失。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="5dbac-119">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="5dbac-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="5dbac-120">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="5dbac-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="5dbac-121">請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。</span><span class="sxs-lookup"><span data-stu-id="5dbac-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="5dbac-122">請確定 tooalso 請嘗試清除瀏覽器的 cookie，然後再試一次 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="5dbac-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="5dbac-123">會議 hello 存取面板 的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="5dbac-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="5dbac-124">存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。</span><span class="sxs-lookup"><span data-stu-id="5dbac-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="5dbac-125">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5dbac-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="5dbac-126">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5dbac-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="5dbac-127">針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="5dbac-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="5dbac-128">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5dbac-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="5dbac-129">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="5dbac-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="5dbac-130">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5dbac-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="5dbac-131">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5dbac-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="5dbac-132">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="5dbac-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="5dbac-133">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-134">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5dbac-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="5dbac-135">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="5dbac-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="5dbac-136">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="5dbac-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="5dbac-137">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="5dbac-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="5dbac-138">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5dbac-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="5dbac-139">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5dbac-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="5dbac-140">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="5dbac-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="5dbac-141">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="5dbac-142">您可能也 hello 從下載擴充功能的 Chrome 和邊緣 hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="5dbac-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="5dbac-143">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="5dbac-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="5dbac-144">Edge 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="5dbac-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5dbac-145">如何 tooconfigure 同盟單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5dbac-146">啟用具備企業單一登入功能的 hello Azure AD 資源庫中的所有應用程式有可用的逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="5dbac-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="5dbac-147">您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細資料的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="5dbac-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="5dbac-148">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="5dbac-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5dbac-149">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="5dbac-150">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="5dbac-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5dbac-151">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="5dbac-152">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="5dbac-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="5dbac-153">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="5dbac-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="5dbac-154">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="5dbac-155">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="5dbac-156">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-157">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="5dbac-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5dbac-158">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-159">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-160">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-161">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5dbac-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5dbac-162">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="5dbac-163">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="5dbac-164">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5dbac-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="5dbac-165">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="5dbac-166">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5dbac-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="5dbac-167">設定單一登入應用程式從 hello Azure AD 資源庫</span><span class="sxs-lookup"><span data-stu-id="5dbac-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="5dbac-168">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-170">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-171">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-172">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-173">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5dbac-174">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-175">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-176">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-177">選取**SAML 型登入**從 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="5dbac-178">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="5dbac-179">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="5dbac-180">tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="5dbac-181">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="5dbac-182">tooconfigure hello 應用程式做為 IdP 初始化的 SSO，hello 回覆 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="5dbac-183">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="5dbac-184">**選擇性：**按一下**顯示進階的 URL 設定**您希望 toosee hello 非必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="5dbac-185">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="5dbac-186">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="5dbac-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="5dbac-187">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="5dbac-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="5dbac-188">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-188">click **Add attribute**.</span></span> <span data-ttu-id="5dbac-189">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="5dbac-190">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-190">Click **Save.**</span></span> <span data-ttu-id="5dbac-191">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="5dbac-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="5dbac-192">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5dbac-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="5dbac-193">此外，您有 hello 中繼資料 Url 和與 hello 應用程式所需的憑證 toosetup SSO。</span><span class="sxs-lookup"><span data-stu-id="5dbac-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="5dbac-194">按一下**儲存**toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5dbac-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="5dbac-195">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="5dbac-196">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="5dbac-197">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-198">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-199">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-200">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-201">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-202">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5dbac-203">如果看不到您想 tooshow 這裡的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-204">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-205">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-206">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="5dbac-207">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5dbac-208">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="5dbac-209">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="5dbac-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="5dbac-210">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="5dbac-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="5dbac-211">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="5dbac-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="5dbac-212">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-212">click **Add attribute**.</span></span> <span data-ttu-id="5dbac-213">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="5dbac-214">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-214">Click **Save.**</span></span> <span data-ttu-id="5dbac-215">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="5dbac-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="5dbac-216">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="5dbac-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="5dbac-217">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-218">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-219">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-220">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-221">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-222">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5dbac-223">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-224">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-225">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-226">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="5dbac-227">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="5dbac-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="5dbac-228">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5dbac-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="5dbac-229">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="5dbac-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5dbac-230">如何 tooconfigure 同盟單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5dbac-231">tooconfigure 非組件庫的應用程式，您必須具備 toohave Azure AD premium 與 hello 應用程式支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="5dbac-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="5dbac-232">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="5dbac-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="5dbac-233">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="5dbac-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="5dbac-234">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="5dbac-235">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="5dbac-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="5dbac-236">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="5dbac-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="5dbac-237">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="5dbac-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="5dbac-238">tooconfigure 單一登入的應用程式不在 hello Azure AD 資源庫，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-239">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-240">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-241">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-242">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-243">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5dbac-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5dbac-244">按一下**非組件庫的應用程式**在 hello**新增您自己的應用程式**區段</span><span class="sxs-lookup"><span data-stu-id="5dbac-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="5dbac-245">輸入 hello hello 應用程式名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5dbac-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="5dbac-246">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="5dbac-247">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="5dbac-248">選取**SAML 型登入**在 hello**模式**下拉式清單</span><span class="sxs-lookup"><span data-stu-id="5dbac-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="5dbac-249">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="5dbac-250">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="5dbac-251">tooconfigure hello IdP 初始化的 SSO 應用程式輸入 hello 回覆 URL 和識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="5dbac-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="5dbac-252">**選擇性：** tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="5dbac-253">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="5dbac-254">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="5dbac-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="5dbac-255">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="5dbac-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="5dbac-256">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-256">click **Add attribute**.</span></span> <span data-ttu-id="5dbac-257">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="5dbac-258">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-258">Click **Save.**</span></span> <span data-ttu-id="5dbac-259">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="5dbac-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="5dbac-260">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5dbac-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="5dbac-261">此外，您有 Azure AD Url 和 hello 應用程式所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="5dbac-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="5dbac-262">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="5dbac-263">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-264">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-265">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-266">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-267">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-268">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5dbac-269">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-270">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-271">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-272">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="5dbac-273">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5dbac-274">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="5dbac-275">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="5dbac-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="5dbac-276">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="5dbac-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="5dbac-277">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="5dbac-277">tooadd an attribute:</span></span>

   <span data-ttu-id="5dbac-278">1. 按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-278">1.click **Add attribute**.</span></span> <span data-ttu-id="5dbac-279">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="5dbac-280">2. 按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5dbac-280">2 Click **Save.**</span></span> <span data-ttu-id="5dbac-281">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="5dbac-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="5dbac-282">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="5dbac-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="5dbac-283">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-284">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-285">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-286">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-287">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-288">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="5dbac-289">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-290">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-291">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-292">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="5dbac-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="5dbac-293">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="5dbac-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="5dbac-294">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5dbac-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="5dbac-295">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="5dbac-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5dbac-296">如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5dbac-297">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="5dbac-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5dbac-298">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="5dbac-299">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="5dbac-300">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="5dbac-301">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-302">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="5dbac-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5dbac-303">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-304">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-305">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-306">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5dbac-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5dbac-307">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="5dbac-308">選取您想 tooconfigure 進行單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="5dbac-309">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5dbac-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="5dbac-310">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="5dbac-311">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5dbac-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="5dbac-312">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="5dbac-313">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-314">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-315">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-316">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-317">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-318">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="5dbac-319">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-320">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="5dbac-321">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-322">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5dbac-323">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="5dbac-324">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5dbac-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="5dbac-325">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="5dbac-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5dbac-326">如何 tooconfigure 密碼單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5dbac-327">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="5dbac-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5dbac-328">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="5dbac-329">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="5dbac-330">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-330">Add a non-gallery application</span></span>

<span data-ttu-id="5dbac-331">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-332">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="5dbac-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5dbac-333">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-334">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-335">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-336">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5dbac-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5dbac-337">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="5dbac-338">輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5dbac-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="5dbac-339">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5dbac-339">Select **Add.**</span></span>

<span data-ttu-id="5dbac-340">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5dbac-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="5dbac-341">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5dbac-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="5dbac-342">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-343">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5dbac-344">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-345">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-346">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-347">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="5dbac-348">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-349">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5dbac-350">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-351">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5dbac-352">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="5dbac-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="5dbac-353">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5dbac-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="5dbac-354">請確定 hello 登入欄位會顯示在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5dbac-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="5dbac-355">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="5dbac-356">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5dbac-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="5dbac-357">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="5dbac-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="5dbac-358">如何 tooassign 使用者 tooan 應用程式直接</span><span class="sxs-lookup"><span data-stu-id="5dbac-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="5dbac-359">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5dbac-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="5dbac-360">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbac-361">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5dbac-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbac-362">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5dbac-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbac-363">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dbac-364">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5dbac-365">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5dbac-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5dbac-366">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="5dbac-367">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5dbac-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dbac-368">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5dbac-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5dbac-369">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5dbac-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5dbac-370">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="5dbac-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5dbac-371">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="5dbac-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="5dbac-372">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="5dbac-373">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="5dbac-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="5dbac-374">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5dbac-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="5dbac-375">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="5dbac-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="5dbac-376">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="5dbac-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="5dbac-377">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5dbac-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="5dbac-378">如果不執行 hello 這些疑難排解步驟解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="5dbac-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="5dbac-379">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5dbac-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="5dbac-380">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="5dbac-380">Correlation error ID</span></span>

-   <span data-ttu-id="5dbac-381">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="5dbac-381">UPN (user email address)</span></span>

-   <span data-ttu-id="5dbac-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="5dbac-382">TenantID</span></span>

-   <span data-ttu-id="5dbac-383">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="5dbac-383">Browser type</span></span>

-   <span data-ttu-id="5dbac-384">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="5dbac-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5dbac-385">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="5dbac-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dbac-386">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5dbac-386">Next steps</span></span>
[<span data-ttu-id="5dbac-387">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="5dbac-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

