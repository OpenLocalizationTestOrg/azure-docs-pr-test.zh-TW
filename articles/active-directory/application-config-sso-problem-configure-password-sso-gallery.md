---
title: "為 Azure AD 資源庫應用程式設定密碼單一登入時遇到的問題 | Microsoft Docs"
description: "了解使用者在為應用程式設定密碼單一登入 (這類應用程式已經列於 Azure AD 應用程式庫中) 時所面臨的常見問題"
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
ms.openlocfilehash: 58d29996a922fac6d295e753ba5d66d32e745a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="36c10-103">為 Azure AD 資源庫應用程式設定密碼單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="36c10-103">Problem configuring password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="36c10-104">本文可協助您了解使用者在搭配 Azure AD 資源庫應用程式設定**密碼單一登入**時所面臨的常見問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-104">This article help you to understand the common problems people face when configuring **Password Single Sign-on** with an Azure AD Gallery application.</span></span>

## <a name="credentials-are-filled-in-but-the-extension-does-not-submit-them"></a><span data-ttu-id="36c10-105">認證會填入，但延伸模組不會提交它們</span><span class="sxs-lookup"><span data-stu-id="36c10-105">Credentials are filled in, but the extension does not submit them</span></span>

<span data-ttu-id="36c10-106">如果應用程式廠商目前已變更他們的登入頁面來新增欄位、變更我們用來偵測使用者名稱和密碼欄位的基礎識別碼，或修改其應用程式的登入體驗運作方式，通常會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-106">This typically happens if the application vendor has changed their sign in page recently to add a field, change an underlying identifier we used to detect the username and password fields, or modify how the sign in experience works for their application.</span></span> <span data-ttu-id="36c10-107">幸運的是，在許多情況下，Microsoft 可以與應用程式廠商合作，快速解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-107">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="36c10-108">雖然 Microsoft 有技術可在這些整合中斷時進行自動偵測，但有時我們無法立即找出這些問題，或者它們需要一些時間來修正。</span><span class="sxs-lookup"><span data-stu-id="36c10-108">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away, or they take some time to fix.</span></span> <span data-ttu-id="36c10-109">萬一這其中一個整合無法正常運作，如果您開啟支援案例，我們會非常感謝您，因為如此一來，我們便能儘速修正該問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-109">In the case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="36c10-110">此外，**如果您與此應用程式的廠商聯繫，****請將我們的連絡方式傳送給他們**，讓我們能夠與他們合作，將其應用程式與 Azure Active Directory 進行原生整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-110">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="36c10-111">您可以將廠商引導到[在 Azure Active Directory 應用程式庫中列出您的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)，讓他們可以立即開始。</span><span class="sxs-lookup"><span data-stu-id="36c10-111">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="credentials-are-filled-in-and-submitted-but-the-page-indicates-the-credentials-are-incorrect"></a><span data-ttu-id="36c10-112">認證會填入並提交，但頁面指出認證不正確</span><span class="sxs-lookup"><span data-stu-id="36c10-112">Credentials are filled in and submitted, but the page indicates the credentials are incorrect</span></span>

<span data-ttu-id="36c10-113">若要解決此問題，請先檢查下列各項：</span><span class="sxs-lookup"><span data-stu-id="36c10-113">To resolve this issue, first check the following:</span></span>

-   <span data-ttu-id="36c10-114">讓使用者先嘗試使用為他們儲存的認證，**直接登入應用程式網站**。</span><span class="sxs-lookup"><span data-stu-id="36c10-114">Have the user first try to **sign in to the application website directly** with the credentials stored for them.</span></span>

  * <span data-ttu-id="36c10-115">如果可行，接著讓使用者在[應用程式存取面板](https://myapps.microsoft.com/)的 [應用程式] 區段中，按一下 [應用程式磚] 上的 [更新認證] 按鈕，以將他們更新至最新已知的有效使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="36c10-115">If that works, then have the user click the **Update credentials** button on the **Application Tile** in the **Apps** section of the [Application Access Panel](https://myapps.microsoft.com/) to update them to the latest known working username and password.</span></span>

   * <span data-ttu-id="36c10-116">如果您或其他系統管理員已為此使用者指派認證，請尋找使用者或群組的應用程式指派，方法是瀏覽至應用程式的 [使用者和群組] 索引標籤、選取指派，然後按一下 [更新認證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36c10-116">If you, or another administrator assigned the credentials for this user, find the user or group’s application assignment by navigating to the **Users & Groups** tab of the application, selecting the assignment and clicking the **Update Credentials** button.</span></span>

-   <span data-ttu-id="36c10-117">如果使用者已指派他們自己的認證，讓使用者**檢查以確定他們的密碼在應用程式中尚未過期**，如果過期，請直接登入應用程式，以**更新他們過期的密碼**。</span><span class="sxs-lookup"><span data-stu-id="36c10-117">If the user assigned their own credentials, have the user **check to be sure that their password has not expired in the application** and if so, **update their expired password** by signing in to the application directly.</span></span>

   * <span data-ttu-id="36c10-118">在應用程式中更新密碼之後，要求使用者在[應用程式存取面板](https://myapps.microsoft.com/)的 [應用程式] 區段中，按一下 [應用程式磚] 上的 [更新認證] 按鈕，以將他們更新至最新已知的有效使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="36c10-118">After the password has been updated in the application, request the user to click the **Update credentials** button on the **Application Tile** in the **Apps** section of the [Application Access Panel](https://myapps.microsoft.com/) to update them to the latest known working username and password.</span></span>

   * <span data-ttu-id="36c10-119">如果您或其他系統管理員已為此使用者指派認證，請尋找使用者或群組的應用程式指派，方法是瀏覽至應用程式的 [使用者和群組] 索引標籤、選取指派，然後按一下 [更新認證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36c10-119">If you, or another administrator assigned the credentials for this user, find the user or group’s application assignment by navigating to the **Users & Groups** tab of the application, selecting the assignment and clicking the **Update Credentials** button.</span></span>

-   <span data-ttu-id="36c10-120">讓使用者依照[如何安裝存取面板的瀏覽器延伸模組](#how-to-install-the-access-panel-browser-extension)一節中的下列步驟，來更新存取面板的瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="36c10-120">Have the user update the access panel browser extension by following the steps below in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="36c10-121">確定存取面板的瀏覽器延伸模組正在使用者的瀏覽器中執行且已啟用。</span><span class="sxs-lookup"><span data-stu-id="36c10-121">Ensure that the access panel browser extension is running and enabled in your user’s browser.</span></span>

-   <span data-ttu-id="36c10-122">確定您的使用者未在 **incognito、InPrivate 或私人模式**中，嘗試從存取面板登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="36c10-122">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="36c10-123">這些模式不支援存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="36c10-123">The access panel extension is not supported in these modes.</span></span>

<span data-ttu-id="36c10-124">萬一這不可行，可能是因為應用程式端發生了變更，暫時中斷了應用程式與 Azure AD 的整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-124">In case this does not work, it could be the case that a change has occurred on the application side which has temporarily broken the application’s integration with Azure AD.</span></span> <span data-ttu-id="36c10-125">例如，這可能發生在下列情況中：當應用程式廠商在其頁面上引進了一個指令碼，而其行為在手動與自動輸入時極為不同，這可能導致自動整合 (就像我們自己的) 中斷。</span><span class="sxs-lookup"><span data-stu-id="36c10-125">For example, this can occur when the application vendor introduces a script on their page which behaves differently for manual vs automated input, which causes automated integration, like our own, to break.</span></span> <span data-ttu-id="36c10-126">幸運的是，在許多情況下，Microsoft 可以與應用程式廠商合作，快速解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-126">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="36c10-127">雖然 Microsoft 有技術可在這些整合中斷時進行自動偵測，但有時我們無法立即找出這些問題，或者它們需要一些時間來修正。</span><span class="sxs-lookup"><span data-stu-id="36c10-127">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away, or they take some time to fix.</span></span> <span data-ttu-id="36c10-128">萬一這其中一個整合無法正常運作，如果您開啟支援案例，我們會非常感謝您，因為如此一來，我們便能儘速修正該問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-128">In the case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="36c10-129">此外，**如果您與此應用程式的廠商聯繫，****請將我們的連絡方式傳送給他們**，讓我們能夠與他們合作，將其應用程式與 Azure Active Directory 進行原生整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-129">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="36c10-130">您可以將廠商引導到[在 Azure Active Directory 應用程式庫中列出您的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)，讓他們可以立即開始。</span><span class="sxs-lookup"><span data-stu-id="36c10-130">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="the-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a><span data-ttu-id="36c10-131">延伸模組可在 Chrome 和 Firefox 中運作，但無法在 Internet Explorer 中運作</span><span class="sxs-lookup"><span data-stu-id="36c10-131">The extension works in Chrome and Firefox, but not in Internet Explorer</span></span>

<span data-ttu-id="36c10-132">這個問題有兩個主要原因：</span><span class="sxs-lookup"><span data-stu-id="36c10-132">There are two main causes to this issue:</span></span>

-   <span data-ttu-id="36c10-133">根據已在 Internet Explorer 中啟用的安全性設定而定，如果網站不屬於**信任的區域**，有時我們的指令碼會被中斷而無法針對應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="36c10-133">Depending on the security settings enabled in Internet Explorer, if the website is not part of a **Trusted Zone**, sometimes our script be blocked from executing for the application.</span></span>

  *  <span data-ttu-id="36c10-134">若要解決此問題，指示使用者**新增應用程式的網站**至其 **Internet Explorer 安全性設定**內的**信任的網站**清單。</span><span class="sxs-lookup"><span data-stu-id="36c10-134">To resolve this, instruct the user to **Add the application’s website** to the **Trusted Sites** list within their **Internet Explorer security settings**.</span></span> <span data-ttu-id="36c10-135">您可以將使用者引導至[如何將網站新增到信任的網站清單](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5)一文，以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="36c10-135">You can send your users to the [How to add a site to my trusted sites list](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) article for detailed instructions.</span></span>

-   <span data-ttu-id="36c10-136">在很罕見的情況下，Internet Explorer 的安全性驗證有時會造成頁面載入速度比我們指令碼執行的速度還慢。</span><span class="sxs-lookup"><span data-stu-id="36c10-136">In rare circumstances, Internet Explorer’s security validation can sometimes cause the page to load more slowly than the execution of our script.</span></span>

   * <span data-ttu-id="36c10-137">不幸的是，這種情況會根據瀏覽器版本、電腦速度或瀏覽過的網站而有所不同。</span><span class="sxs-lookup"><span data-stu-id="36c10-137">Unfortunately, this situation can vary depending on the browser version, computer speed, or site visited.</span></span> <span data-ttu-id="36c10-138">在此情況下，我們建議您連絡支援人員，讓我們能夠修正這個特定應用程式的整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-138">In this case, we suggest that you contact support so we can fix the integration for this specific application.</span></span>

<span data-ttu-id="36c10-139">此外，**如果您與此應用程式的廠商聯繫，****請將我們的連絡方式傳送給他們**，讓我們能夠與他們合作，將其應用程式與 Azure Active Directory 進行原生整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-139">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="36c10-140">您可以將廠商引導到[在 Azure Active Directory 應用程式庫中列出您的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)，讓他們可以立即開始。</span><span class="sxs-lookup"><span data-stu-id="36c10-140">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="check-if-the-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a><span data-ttu-id="36c10-141">檢查應用程式的登入頁面最近是否已變更或需要額外的欄位</span><span class="sxs-lookup"><span data-stu-id="36c10-141">Check if the application’s login page has changed recently or requires an additional field</span></span>

<span data-ttu-id="36c10-142">如果應用程式的登入頁面已大幅變更，有時這會導致我們的整合中斷。</span><span class="sxs-lookup"><span data-stu-id="36c10-142">If the application’s login page has changed drastically, sometimes this causes our integrations to break.</span></span> <span data-ttu-id="36c10-143">當應用程式廠商將登入欄位、Captcha 或多重要素驗證新增至他們的體驗時，即為一例。</span><span class="sxs-lookup"><span data-stu-id="36c10-143">An example of this is when an application vendor adds a sign in field, a captcha, or multi-factor authentication to their experiences.</span></span> <span data-ttu-id="36c10-144">幸運的是，在許多情況下，Microsoft 可以與應用程式廠商合作，快速解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-144">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="36c10-145">雖然 Microsoft 有技術可在這些整合中斷時進行自動偵測，但有時我們無法立即找出這些問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-145">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away.</span></span> <span data-ttu-id="36c10-146">不然就是它們需要一些時間來修正。</span><span class="sxs-lookup"><span data-stu-id="36c10-146">Otherwise they take some time to fix.</span></span> <span data-ttu-id="36c10-147">萬一這其中一個整合無法正常運作，如果您開啟支援案例，我們會非常感謝您，因為如此一來，我們便能儘速修正該問題。</span><span class="sxs-lookup"><span data-stu-id="36c10-147">In the case when one of these integrations does not work correctly, we would appreciate opening a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="36c10-148">此外，**如果您與此應用程式的廠商聯繫，****請將我們的連絡方式傳送給他們**，讓我們能夠與他們合作，將其應用程式與 Azure Active Directory 進行原生整合。</span><span class="sxs-lookup"><span data-stu-id="36c10-148">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="36c10-149">您可以將廠商引導到[在 Azure Active Directory 應用程式庫中列出您的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)，讓他們可以立即開始。</span><span class="sxs-lookup"><span data-stu-id="36c10-149">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="36c10-150">如何安裝存取面板的瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="36c10-150">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="36c10-151">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36c10-151">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="36c10-152">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="36c10-152">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="36c10-153">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="36c10-153">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="36c10-154">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="36c10-154">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="36c10-155">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="36c10-155">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="36c10-156">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="36c10-156">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="36c10-157">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="36c10-157">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="36c10-158">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="36c10-158">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="36c10-159">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="36c10-159">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="36c10-160">您可能也會從下列直接連結中下載適用於 Chrome 和 Firefox 的延伸模組：</span><span class="sxs-lookup"><span data-stu-id="36c10-160">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="36c10-161">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="36c10-161">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="36c10-162">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="36c10-162">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a><span data-ttu-id="36c10-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36c10-163">Next steps</span></span>
[<span data-ttu-id="36c10-164">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="36c10-164">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

