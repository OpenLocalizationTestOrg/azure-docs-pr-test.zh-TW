---
title: "從存取面板登入應用程式的問題 | Microsoft Docs"
description: "如何為從 Microsoft Azure AD 存取面板 (myapps.microsoft.com) 存取應用程式時發生的問題疑難排解"
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
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="fff18-103">從存取面板登入應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="fff18-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="fff18-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="fff18-105">在 Azure AD 入口網站中可代表使用者設定這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="fff18-106">應用程式必須經過正確的設定並指派至使用者或使用者所屬的群組，才能在存取面板中顯示該應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="fff18-107">使用者能看見的應用程式類型可分為以下類別：</span><span class="sxs-lookup"><span data-stu-id="fff18-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="fff18-108">Office 365 應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-108">Office 365 Applications</span></span>

-   <span data-ttu-id="fff18-109">已設定同盟 SSO 的 Microsoft 及第三方應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="fff18-110">密碼型 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="fff18-111">含現有 SSO 解決方案的應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="fff18-112">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="fff18-112">General issues to check first</span></span>

-   <span data-ttu-id="fff18-113">請確定您使用的**瀏覽器**符合存取面板的最低需求。</span><span class="sxs-lookup"><span data-stu-id="fff18-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="fff18-114">確定使用者的瀏覽器已將應用程式的 URL 新增至其**信任的網站**。</span><span class="sxs-lookup"><span data-stu-id="fff18-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="fff18-115">檢查應用程式以確認其**設定**正確。</span><span class="sxs-lookup"><span data-stu-id="fff18-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="fff18-116">確定使用者的帳戶**已啟用**可供登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="fff18-117">確定使用者的帳戶**未鎖定**。</span><span class="sxs-lookup"><span data-stu-id="fff18-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="fff18-118">確定使用者的**密碼未過期或忘記**。</span><span class="sxs-lookup"><span data-stu-id="fff18-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="fff18-119">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="fff18-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="fff18-120">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="fff18-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="fff18-121">確定使用者的**驗證連絡資訊**為最新版本，而可強制執行 Multi-Factor Authentication 或條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fff18-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="fff18-122">也要確定嘗試清除瀏覽器的 Cookie，然後嘗試再次登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="fff18-123">符合存取面板的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="fff18-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="fff18-124">存取面板需要支援 JavaScript 且已啟用 CSS 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fff18-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="fff18-125">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fff18-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="fff18-126">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fff18-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="fff18-127">若是密碼 SSO，則使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="fff18-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="fff18-128">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fff18-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="fff18-129">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="fff18-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="fff18-130">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fff18-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="fff18-131">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fff18-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="fff18-132">如何安裝存取面板的瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="fff18-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="fff18-133">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fff18-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-134">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="fff18-135">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="fff18-136">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="fff18-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="fff18-137">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="fff18-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="fff18-138">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="fff18-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="fff18-139">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fff18-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="fff18-140">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="fff18-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="fff18-141">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="fff18-142">您可能也會從下列直接連結中下載適用於 Chrome 和 Edge 的擴充功能：</span><span class="sxs-lookup"><span data-stu-id="fff18-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="fff18-143">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="fff18-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="fff18-144">Edge 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="fff18-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="fff18-145">如何為 Azure AD 資源庫應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="fff18-146">Azure AD 資源庫中所有透過企業單一登入功能啟用的應用程式都提供逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="fff18-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="fff18-147">您可以存取[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)，以取得詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="fff18-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="fff18-148">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="fff18-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fff18-149">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="fff18-150">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="fff18-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="fff18-151">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="fff18-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="fff18-152">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="fff18-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="fff18-153">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="fff18-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="fff18-154">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="fff18-155">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="fff18-156">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-157">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fff18-158">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-159">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-160">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-161">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fff18-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fff18-162">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="fff18-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="fff18-163">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="fff18-164">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="fff18-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="fff18-165">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="fff18-166">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fff18-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="fff18-167">從 Azure AD 資源庫為應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="fff18-168">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-170">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-171">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-172">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-173">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fff18-174">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-175">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="fff18-176">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-177">從 [模式] 下拉式清單選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="fff18-178">在 [網域及 URL] 中輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="fff18-179">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="fff18-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="fff18-180">若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="fff18-181">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="fff18-182">若要將應用程式設定為 IdP 啟始的單一登入，則 [登入 URL] 為必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="fff18-183">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="fff18-184">**選擇性：**如果您想要看到非必要值，請按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="fff18-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="fff18-185">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="fff18-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="fff18-186">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="fff18-187">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="fff18-187">To add an attribute:</span></span>

   1. <span data-ttu-id="fff18-188">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="fff18-188">click **Add attribute**.</span></span> <span data-ttu-id="fff18-189">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="fff18-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="fff18-190">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="fff18-190">Click **Save.**</span></span> <span data-ttu-id="fff18-191">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="fff18-192">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="fff18-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="fff18-193">此外，您會有透過該應用程式設定 SSO 所需的中繼資料 URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="fff18-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="fff18-194">按一下 [儲存] 儲存組態。</span><span class="sxs-lookup"><span data-stu-id="fff18-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="fff18-195">將使用者指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="fff18-196">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="fff18-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="fff18-197">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-198">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-199">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-200">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-201">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-202">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fff18-203">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-204">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="fff18-205">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-206">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="fff18-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="fff18-207">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="fff18-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="fff18-208">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="fff18-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="fff18-209">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="fff18-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="fff18-210">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="fff18-211">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="fff18-211">To add an attribute:</span></span>

   1. <span data-ttu-id="fff18-212">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="fff18-212">click **Add attribute**.</span></span> <span data-ttu-id="fff18-213">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="fff18-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="fff18-214">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="fff18-214">Click **Save.**</span></span> <span data-ttu-id="fff18-215">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="fff18-216">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="fff18-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="fff18-217">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-218">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-219">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-220">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-221">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-222">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fff18-223">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-224">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="fff18-225">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-226">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="fff18-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="fff18-227">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="fff18-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="fff18-228">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="fff18-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="fff18-229">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fff18-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="fff18-230">如何為不在資源庫內的應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="fff18-231">若要設定不在資源庫內的應用程式，您必須有 Azure AD Premium，且應用程式必須支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="fff18-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="fff18-232">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="fff18-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="fff18-233">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="fff18-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="fff18-234">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="fff18-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="fff18-235">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="fff18-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="fff18-236">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="fff18-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="fff18-237">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="fff18-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="fff18-238">若要為不在 Azure AD 資源庫中的應用程式設定單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-239">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-240">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-241">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-242">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-243">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fff18-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fff18-244">按一下 [Add your own app (新增您的應用程式)] 區段中的 [Non-gallery application (非資源庫應用程式)]</span><span class="sxs-lookup"><span data-stu-id="fff18-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="fff18-245">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="fff18-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="fff18-246">按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="fff18-247">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="fff18-248">在 [模式] 下拉式清單中選取 [SAML 登入]</span><span class="sxs-lookup"><span data-stu-id="fff18-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="fff18-249">在 [網域及 URL] 中輸入必要值</span><span class="sxs-lookup"><span data-stu-id="fff18-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="fff18-250">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="fff18-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="fff18-251">若要將應用程式設定為 IdP 啟始的 SSO，請輸入回覆 URL 與識別碼。</span><span class="sxs-lookup"><span data-stu-id="fff18-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="fff18-252">**選擇性：**若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="fff18-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="fff18-253">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="fff18-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="fff18-254">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="fff18-255">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="fff18-255">To add an attribute:</span></span>

   1. <span data-ttu-id="fff18-256">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="fff18-256">click **Add attribute**.</span></span> <span data-ttu-id="fff18-257">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="fff18-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="fff18-258">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="fff18-258">Click **Save.**</span></span> <span data-ttu-id="fff18-259">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="fff18-260">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="fff18-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="fff18-261">此外，您有應用程式所需的 Azure AD URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="fff18-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="fff18-262">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="fff18-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="fff18-263">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-264">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-265">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-266">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-267">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-268">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fff18-269">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-270">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="fff18-271">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-272">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="fff18-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="fff18-273">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="fff18-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fff18-274">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="fff18-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="fff18-275">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="fff18-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="fff18-276">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="fff18-277">若要新增屬性︰</span><span class="sxs-lookup"><span data-stu-id="fff18-277">To add an attribute:</span></span>

   <span data-ttu-id="fff18-278">1. 按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="fff18-278">1.click **Add attribute**.</span></span> <span data-ttu-id="fff18-279">輸入 [名稱]，然後從下拉式清單中選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="fff18-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="fff18-280">2. 按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fff18-280">2 Click **Save.**</span></span> <span data-ttu-id="fff18-281">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="fff18-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="fff18-282">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="fff18-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="fff18-283">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-284">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-285">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-286">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-287">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-288">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fff18-289">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-290">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="fff18-291">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-292">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="fff18-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="fff18-293">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="fff18-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="fff18-294">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="fff18-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="fff18-295">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fff18-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="fff18-296">如何為 Azure AD 資源庫應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="fff18-297">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="fff18-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fff18-298">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="fff18-299">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="fff18-300">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="fff18-301">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-302">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fff18-303">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-304">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-305">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-306">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fff18-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fff18-307">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="fff18-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="fff18-308">選取您要設為單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="fff18-309">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="fff18-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="fff18-310">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="fff18-311">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fff18-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="fff18-312">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="fff18-313">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-314">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-315">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-316">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-317">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-318">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="fff18-319">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-320">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="fff18-321">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-322">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="fff18-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="fff18-323">將使用者指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-323">Assign users to the application.</span></span>

10. <span data-ttu-id="fff18-324">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="fff18-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="fff18-325">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="fff18-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="fff18-326">如何為不在資源庫內的應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="fff18-327">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="fff18-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fff18-328">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="fff18-329">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="fff18-330">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-330">Add a non-gallery application</span></span>

<span data-ttu-id="fff18-331">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-332">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fff18-333">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-334">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-335">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-336">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="fff18-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fff18-337">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="fff18-338">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="fff18-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="fff18-339">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fff18-339">Select **Add.**</span></span>

<span data-ttu-id="fff18-340">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fff18-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="fff18-341">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="fff18-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="fff18-342">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fff18-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-343">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fff18-344">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-345">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-346">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-347">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="fff18-348">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-349">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="fff18-350">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fff18-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-351">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="fff18-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="fff18-352">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="fff18-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="fff18-353">這是使用者輸入使用者名稱和密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="fff18-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="fff18-354">確保在 URL 看得到登入欄位。</span><span class="sxs-lookup"><span data-stu-id="fff18-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="fff18-355">將使用者指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-355">Assign users to the application.</span></span>

11. <span data-ttu-id="fff18-356">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="fff18-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="fff18-357">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="fff18-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="fff18-358">如何將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="fff18-359">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="fff18-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="fff18-360">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="fff18-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fff18-361">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fff18-362">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="fff18-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fff18-363">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fff18-364">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fff18-365">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fff18-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fff18-366">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="fff18-367">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fff18-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fff18-368">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fff18-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fff18-369">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="fff18-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fff18-370">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="fff18-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fff18-371">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="fff18-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="fff18-372">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="fff18-373">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="fff18-374">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="fff18-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="fff18-375">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="fff18-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="fff18-376">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="fff18-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="fff18-377">稍待片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="fff18-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="fff18-378">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="fff18-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="fff18-379">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="fff18-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="fff18-380">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="fff18-380">Correlation error ID</span></span>

-   <span data-ttu-id="fff18-381">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="fff18-381">UPN (user email address)</span></span>

-   <span data-ttu-id="fff18-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="fff18-382">TenantID</span></span>

-   <span data-ttu-id="fff18-383">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="fff18-383">Browser type</span></span>

-   <span data-ttu-id="fff18-384">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="fff18-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="fff18-385">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="fff18-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="fff18-386">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fff18-386">Next steps</span></span>
[<span data-ttu-id="fff18-387">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="fff18-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

