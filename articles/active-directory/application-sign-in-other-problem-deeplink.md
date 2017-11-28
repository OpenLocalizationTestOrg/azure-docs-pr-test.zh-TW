---
title: "aaaProblems 登入 tooan 應用程式使用深層連結 |Microsoft 文件"
description: "如何從使用 Azure AD 的深層連結 URL 存取的應用程式的 tootroubleshoot 問題"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="e4e8a-103">登入使用深層連結 tooan 應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="e4e8a-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="e4e8a-104">hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="e4e8a-105">這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="e4e8a-106">hello 應用程式必須正確設定並指派的 toohello 使用者或群組 hello 使用者是 toosee hello 存取面板中的 hello 應用程式的成員。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="e4e8a-107">深層連結或使用者的存取 Url 將是您的使用者可能會使用其密碼 SSO 應用程式直接從他們的瀏覽器的 URL 列的 tooaccess 的連結。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="e4e8a-108">瀏覽 toothis 連結，使用者會自動登入 hello 應用程式，而不需要 toogo toohello 存取面板的第一次。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="e4e8a-109">這是 hello 使用者使用 tooaccess hello Office 365 應用程式啟動程式從這些應用程式的相同連結。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="e4e8a-110">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="e4e8a-110">General issues toocheck first</span></span>

-   <span data-ttu-id="e4e8a-111">請確定您使用**瀏覽器**符合 hello hello 存取面板的最低需求。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="e4e8a-112">請確定 hello 使用者的瀏覽器已新增的 hello 應用程式 tooits hello URL**信任的網站**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="e4e8a-113">請確定 toocheck hello 應用程式是**設定**正確。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="e4e8a-114">請確定 hello 使用者帳戶是**啟用**的登入。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="e4e8a-115">請確定 hello 使用者帳戶是**並未鎖定。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="e4e8a-116">請確定 hello 使用者的**密碼未過期或遺失。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="e4e8a-117">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="e4e8a-118">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="e4e8a-119">請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="e4e8a-120">請確定 tooalso 請嘗試清除瀏覽器的 cookie，然後再試一次 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="e4e8a-121">檢查 hello 深層連結</span><span class="sxs-lookup"><span data-stu-id="e4e8a-121">Checking hello deeplink</span></span>

<span data-ttu-id="e4e8a-122">toocheck，如果您擁有 hello 正確深層連結，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-123">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e4e8a-124">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-125">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-126">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-127">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e4e8a-128">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e4e8a-129">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="e4e8a-130">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="e4e8a-131">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="e4e8a-132">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="e4e8a-133">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e4e8a-134">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="e4e8a-135">選取您想要的 hello 核取 hello 深層連結的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="e4e8a-136">找出 hello 標籤**使用者存取 URL**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="e4e8a-137">您的深層連結應符合此 URL。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="e4e8a-138">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="e4e8a-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="e4e8a-139">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-140">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="e4e8a-141">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="e4e8a-142">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="e4e8a-143">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="e4e8a-144">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="e4e8a-145">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="e4e8a-146">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="e4e8a-147">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="e4e8a-148">您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="e4e8a-149">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="e4e8a-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="e4e8a-150">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="e4e8a-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="e4e8a-151">如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="e4e8a-152">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e4e8a-153">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="e4e8a-154">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e4e8a-155">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e4e8a-156">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-157">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="e4e8a-158">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-159">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-160">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-161">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="e4e8a-162">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="e4e8a-163">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="e4e8a-164">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="e4e8a-165">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="e4e8a-166">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="e4e8a-167">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="e4e8a-168">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-169">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e4e8a-170">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-171">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-172">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-173">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e4e8a-174">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e4e8a-175">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e4e8a-176">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e4e8a-177">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e4e8a-178">[將使用者指派 toohello 應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="e4e8a-179">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="e4e8a-180">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e4e8a-181">如何 tooconfigure 密碼單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e4e8a-182">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e4e8a-183">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="e4e8a-184">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="e4e8a-185">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-185">Add a non-gallery application</span></span>

<span data-ttu-id="e4e8a-186">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-187">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="e4e8a-188">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-189">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-190">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-191">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="e4e8a-192">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="e4e8a-193">輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="e4e8a-194">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-194">Select **Add.**</span></span>

<span data-ttu-id="e4e8a-195">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="e4e8a-196">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4e8a-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="e4e8a-197">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-198">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e4e8a-199">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-200">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-201">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-202">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="e4e8a-203">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e4e8a-204">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e4e8a-205">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e4e8a-206">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e4e8a-207">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e4e8a-208">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e4e8a-209">請確定 hello 登入欄位會顯示在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="e4e8a-210">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="e4e8a-211">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="e4e8a-212">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="e4e8a-213">如何 tooassign 使用者 tooan 應用程式直接</span><span class="sxs-lookup"><span data-stu-id="e4e8a-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="e4e8a-214">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4e8a-215">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e4e8a-216">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4e8a-217">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4e8a-218">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4e8a-219">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e4e8a-220">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e4e8a-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e4e8a-221">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e4e8a-222">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e4e8a-223">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e4e8a-224">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e4e8a-225">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e4e8a-226">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e4e8a-227">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e4e8a-228">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e4e8a-229">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e4e8a-230">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e4e8a-231">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="e4e8a-232">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="e4e8a-233">如果不執行 hello 這些疑難排解步驟解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="e4e8a-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="e4e8a-234">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e4e8a-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="e4e8a-235">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="e4e8a-235">Correlation error ID</span></span>

-   <span data-ttu-id="e4e8a-236">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="e4e8a-236">UPN (user email address)</span></span>

-   <span data-ttu-id="e4e8a-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="e4e8a-237">TenantID</span></span>

-   <span data-ttu-id="e4e8a-238">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="e4e8a-238">Browser type</span></span>

-   <span data-ttu-id="e4e8a-239">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="e4e8a-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="e4e8a-240">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="e4e8a-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4e8a-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4e8a-241">Next steps</span></span>
[<span data-ttu-id="e4e8a-242">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="e4e8a-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
