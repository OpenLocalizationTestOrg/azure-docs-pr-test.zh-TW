---
title: "使用深層連結登入應用程式的問題 | Microsoft Docs"
description: "如何為使用 Azure AD 從深層連結 URL 存取應用程式的問題疑難排解"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="b2492-103">使用深層連結登入應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="b2492-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="b2492-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="b2492-105">在 Azure AD 入口網站中可代表使用者設定這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="b2492-106">應用程式必須經過正確的設定並指派至使用者或使用者所屬的群組，才能在存取面板中顯示該應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="b2492-107">深層連結或使用者存取 URL 是一種連結，您的使用者可使用此種連結直接從其瀏覽器網址列存取其密碼 SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="b2492-108">透過瀏覽到此連結，使用者不必先移至存取面板，便會自動登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="b2492-109">這是使用者用來從 Office 365 應用程式啟動程式存取這些應用程式的相同連結。</span><span class="sxs-lookup"><span data-stu-id="b2492-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="b2492-110">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="b2492-110">General issues to check first</span></span>

-   <span data-ttu-id="b2492-111">請確定您使用的**瀏覽器**符合存取面板的最低需求。</span><span class="sxs-lookup"><span data-stu-id="b2492-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="b2492-112">確定使用者的瀏覽器已將應用程式的 URL 新增至其**信任的網站**。</span><span class="sxs-lookup"><span data-stu-id="b2492-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="b2492-113">檢查應用程式以確認其**設定**正確。</span><span class="sxs-lookup"><span data-stu-id="b2492-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="b2492-114">確定使用者的帳戶**已啟用**可供登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="b2492-115">確定使用者的帳戶**未鎖定**。</span><span class="sxs-lookup"><span data-stu-id="b2492-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="b2492-116">確定使用者的**密碼未過期或忘記**。</span><span class="sxs-lookup"><span data-stu-id="b2492-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="b2492-117">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="b2492-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="b2492-118">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="b2492-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="b2492-119">確定使用者的**驗證連絡資訊**為最新版本，而可強制執行 Multi-Factor Authentication 或條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="b2492-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="b2492-120">也要確定嘗試清除瀏覽器的 Cookie，然後嘗試再次登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="b2492-121">檢查深層連結</span><span class="sxs-lookup"><span data-stu-id="b2492-121">Checking the deeplink</span></span>

<span data-ttu-id="b2492-122">若要檢查您是否擁有正確的深層連結，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b2492-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-123">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b2492-124">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-125">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-126">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-127">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b2492-128">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b2492-129">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="b2492-130">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="b2492-131">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="b2492-132">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="b2492-133">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b2492-134">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="b2492-135">選取您想要檢查深層連結的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="b2492-136">尋找 [使用者存取 URL] 標籤。</span><span class="sxs-lookup"><span data-stu-id="b2492-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="b2492-137">您的深層連結應符合此 URL。</span><span class="sxs-lookup"><span data-stu-id="b2492-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="b2492-138">如何安裝存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="b2492-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="b2492-139">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b2492-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-140">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b2492-141">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="b2492-142">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="b2492-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b2492-143">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="b2492-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="b2492-144">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="b2492-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="b2492-145">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="b2492-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="b2492-146">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="b2492-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b2492-147">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b2492-148">您可能也會從下列直接連結中下載適用於 Chrome 和 Firefox 的延伸模組：</span><span class="sxs-lookup"><span data-stu-id="b2492-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="b2492-149">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="b2492-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b2492-150">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="b2492-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b2492-151">如何為 Azure AD 資源庫應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="b2492-152">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="b2492-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b2492-153">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="b2492-154">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="b2492-155">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="b2492-156">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b2492-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-157">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="b2492-158">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-159">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-160">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-161">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2492-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="b2492-162">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="b2492-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="b2492-163">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="b2492-164">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="b2492-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="b2492-165">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="b2492-166">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2492-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="b2492-167">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="b2492-168">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b2492-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-169">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b2492-170">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-171">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-172">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-173">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b2492-174">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b2492-175">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b2492-176">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b2492-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b2492-177">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="b2492-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b2492-178">[將使用者指派至應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="b2492-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="b2492-179">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="b2492-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="b2492-180">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="b2492-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b2492-181">如何為不在資源庫內的應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b2492-182">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="b2492-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b2492-183">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="b2492-184">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="b2492-185">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-185">Add a non-gallery application</span></span>

<span data-ttu-id="b2492-186">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b2492-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-187">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="b2492-188">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-189">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-190">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-191">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2492-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="b2492-192">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="b2492-193">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b2492-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="b2492-194">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b2492-194">Select **Add.**</span></span>

<span data-ttu-id="b2492-195">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2492-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="b2492-196">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="b2492-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="b2492-197">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b2492-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-198">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b2492-199">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-200">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-201">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-202">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="b2492-203">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b2492-204">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b2492-205">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b2492-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b2492-206">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="b2492-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b2492-207">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="b2492-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="b2492-208">這是使用者輸入使用者名稱和密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="b2492-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="b2492-209">確保在 URL 看得到登入欄位。</span><span class="sxs-lookup"><span data-stu-id="b2492-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="b2492-210">將使用者指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-210">Assign users to the application.</span></span>

11. <span data-ttu-id="b2492-211">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="b2492-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="b2492-212">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="b2492-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="b2492-213">如何將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="b2492-214">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="b2492-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b2492-215">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b2492-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b2492-216">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b2492-217">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b2492-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b2492-218">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b2492-219">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b2492-220">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2492-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b2492-221">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b2492-222">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b2492-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b2492-223">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2492-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b2492-224">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="b2492-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b2492-225">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b2492-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b2492-226">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="b2492-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b2492-227">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b2492-228">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="b2492-229">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="b2492-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b2492-230">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="b2492-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="b2492-231">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="b2492-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="b2492-232">稍待片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2492-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="b2492-233">如果這些疑難排解步驟無法解決問題。</span><span class="sxs-lookup"><span data-stu-id="b2492-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="b2492-234">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="b2492-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="b2492-235">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="b2492-235">Correlation error ID</span></span>

-   <span data-ttu-id="b2492-236">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="b2492-236">UPN (user email address)</span></span>

-   <span data-ttu-id="b2492-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="b2492-237">TenantID</span></span>

-   <span data-ttu-id="b2492-238">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="b2492-238">Browser type</span></span>

-   <span data-ttu-id="b2492-239">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="b2492-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b2492-240">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="b2492-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2492-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2492-241">Next steps</span></span>
[<span data-ttu-id="b2492-242">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="b2492-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
