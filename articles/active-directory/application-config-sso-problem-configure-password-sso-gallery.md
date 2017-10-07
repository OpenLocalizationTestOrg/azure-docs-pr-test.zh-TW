---
title: "設定密碼單一登入 Azure AD 庫應用程式的 aaaProblem |Microsoft 文件"
description: "當您設定密碼單一登入的應用程式，已列出 hello Azure AD 應用程式庫中，了解 hello 一般問題的人臉"
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="92afe-103">為 Azure AD 資源庫應用程式設定密碼單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="92afe-103">Problem configuring password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="92afe-104">本文協助您 toounderstand hello 一般問題的人臉設定時**密碼單一登入**與 Azure AD 庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="92afe-104">This article help you toounderstand hello common problems people face when configuring **Password Single Sign-on** with an Azure AD Gallery application.</span></span>

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a><span data-ttu-id="92afe-105">認證會填入，但 hello 延伸模組未送出</span><span class="sxs-lookup"><span data-stu-id="92afe-105">Credentials are filled in, but hello extension does not submit them</span></span>

<span data-ttu-id="92afe-106">這通常發生 hello 應用程式廠商已變更其登入頁面上最近 tooadd 欄位、 變更基礎的識別項，我們使用 toodetect hello 使用者名稱和密碼欄位，或修改 hello 登入體驗運作他們的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="92afe-106">This typically happens if hello application vendor has changed their sign in page recently tooadd a field, change an underlying identifier we used toodetect hello username and password fields, or modify how hello sign in experience works for their application.</span></span> <span data-ttu-id="92afe-107">幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="92afe-107">Fortunately, in many instances, Microsoft can work with application vendors toorapidly resolve these issues.</span></span>

<span data-ttu-id="92afe-108">Microsoft 有技術 tooautomatically 這些整合中斷，但有時候我們不能 toofind 時偵測到這些問題右離開，或者它們需要一些時間 toofix。</span><span class="sxs-lookup"><span data-stu-id="92afe-108">While Microsoft has technologies tooautomatically detect when these integrations break, but sometimes we are not able toofind these issues right away, or they take some time toofix.</span></span> <span data-ttu-id="92afe-109">萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝如果您開啟支援案例，以便我們可以盡快修正。</span><span class="sxs-lookup"><span data-stu-id="92afe-109">In hello case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="92afe-110">在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="92afe-110">In addition toothis, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them toonatively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="92afe-111">您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。</span><span class="sxs-lookup"><span data-stu-id="92afe-111">You can send hello vendor toohello [Listing your application in hello Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget them started.</span></span>

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a><span data-ttu-id="92afe-112">認證會填入與提交，但 hello 頁面會指出 hello 認證不正確</span><span class="sxs-lookup"><span data-stu-id="92afe-112">Credentials are filled in and submitted, but hello page indicates hello credentials are incorrect</span></span>

<span data-ttu-id="92afe-113">這個問題，第一個核取 hello 下列 tooresolve:</span><span class="sxs-lookup"><span data-stu-id="92afe-113">tooresolve this issue, first check hello following:</span></span>

-   <span data-ttu-id="92afe-114">擁有 hello 使用者首次試用過**直接登入 toohello 應用程式網站**hello 認證儲存它們。</span><span class="sxs-lookup"><span data-stu-id="92afe-114">Have hello user first try too**sign in toohello application website directly** with hello credentials stored for them.</span></span>

  * <span data-ttu-id="92afe-115">如果此作業有效，則有 hello 使用者按一下 hello**更新認證**hello 按鈕**應用程式磚**在 hello**應用程式**區段 hello[應用程式存取面板](https://myapps.microsoft.com/)tooupdate 它們 toohello 最新已知使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="92afe-115">If that works, then have hello user click hello **Update credentials** button on hello **Application Tile** in hello **Apps** section of hello [Application Access Panel](https://myapps.microsoft.com/) tooupdate them toohello latest known working username and password.</span></span>

   * <span data-ttu-id="92afe-116">如果您或其他系統管理員指派 hello 認證對這個使用者而言尋找 hello 使用者或群組的應用程式指派瀏覽 toohello**使用者和群組**hello 應用程式中，選取 hello 分派 索引標籤和按一下 hello**更新認證** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92afe-116">If you, or another administrator assigned hello credentials for this user, find hello user or group’s application assignment by navigating toohello **Users & Groups** tab of hello application, selecting hello assignment and clicking hello **Update Credentials** button.</span></span>

-   <span data-ttu-id="92afe-117">如果 hello 使用者指派自己的認證，擁有 hello 使用者**檢查確定他們的密碼尚未過期 hello 應用程式中的 toobe**而且如果是，**更新過期的密碼**登入 toohello應用程式直接。</span><span class="sxs-lookup"><span data-stu-id="92afe-117">If hello user assigned their own credentials, have hello user **check toobe sure that their password has not expired in hello application** and if so, **update their expired password** by signing in toohello application directly.</span></span>

   * <span data-ttu-id="92afe-118">已更新 hello 應用程式中的 hello 密碼之後，要求 hello 使用者 tooclick hello**更新認證**按鈕 hello**應用程式磚**在 hello**應用程式**區段的 hello[應用程式存取面板](https://myapps.microsoft.com/)tooupdate 它們 toohello 最新已知使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="92afe-118">After hello password has been updated in hello application, request hello user tooclick hello **Update credentials** button on hello **Application Tile** in hello **Apps** section of hello [Application Access Panel](https://myapps.microsoft.com/) tooupdate them toohello latest known working username and password.</span></span>

   * <span data-ttu-id="92afe-119">如果您或其他系統管理員指派 hello 認證對這個使用者而言尋找 hello 使用者或群組的應用程式指派瀏覽 toohello**使用者和群組**hello 應用程式中，選取 hello 分派 索引標籤和按一下 hello**更新認證** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92afe-119">If you, or another administrator assigned hello credentials for this user, find hello user or group’s application assignment by navigating toohello **Users & Groups** tab of hello application, selecting hello assignment and clicking hello **Update Credentials** button.</span></span>

-   <span data-ttu-id="92afe-120">Hello 使用者更新 hello 存取面板瀏覽器延伸模組已依照 hello 執行下列步驟在 hello [tooinstall hello 存取面板瀏覽器延伸模組的方式](#how-to-install-the-access-panel-browser-extension)> 一節。</span><span class="sxs-lookup"><span data-stu-id="92afe-120">Have hello user update hello access panel browser extension by following hello steps below in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="92afe-121">請確認正在執行且已啟用使用者的瀏覽器 hello 存取面板瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="92afe-121">Ensure that hello access panel browser extension is running and enabled in your user’s browser.</span></span>

-   <span data-ttu-id="92afe-122">請確定您的使用者沒有 toosign toohello hello 存取面板時在應用程式**incognito、 inPrivate，或私用模式**。</span><span class="sxs-lookup"><span data-stu-id="92afe-122">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="92afe-123">hello 存取面板延伸模組不支援這些模式中。</span><span class="sxs-lookup"><span data-stu-id="92afe-123">hello access panel extension is not supported in these modes.</span></span>

<span data-ttu-id="92afe-124">如果這無法運作，它可能已經變更。 已暫時中斷與 Azure AD 的 hello 應用程式整合 hello 應用程式端的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="92afe-124">In case this does not work, it could be hello case that a change has occurred on hello application side which has temporarily broken hello application’s integration with Azure AD.</span></span> <span data-ttu-id="92afe-125">例如，發生這個問題 hello 應用程式廠商導入了其具有不同行為手動 vs 頁面上的指令碼自動化的輸入，這會導致自動化整合，我們自己，toobreak 類似。</span><span class="sxs-lookup"><span data-stu-id="92afe-125">For example, this can occur when hello application vendor introduces a script on their page which behaves differently for manual vs automated input, which causes automated integration, like our own, toobreak.</span></span> <span data-ttu-id="92afe-126">幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="92afe-126">Fortunately, in many instances, Microsoft can work with application vendors toorapidly resolve these issues.</span></span>

<span data-ttu-id="92afe-127">Microsoft 有技術 tooautomatically 這些整合中斷，但有時候我們不能 toofind 時偵測到這些問題右離開，或者它們需要一些時間 toofix。</span><span class="sxs-lookup"><span data-stu-id="92afe-127">While Microsoft has technologies tooautomatically detect when these integrations break, but sometimes we are not able toofind these issues right away, or they take some time toofix.</span></span> <span data-ttu-id="92afe-128">萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝如果您開啟支援案例，以便我們可以盡快修正。</span><span class="sxs-lookup"><span data-stu-id="92afe-128">In hello case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="92afe-129">在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="92afe-129">In addition toothis, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them toonatively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="92afe-130">您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。</span><span class="sxs-lookup"><span data-stu-id="92afe-130">You can send hello vendor toohello [Listing your application in hello Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget them started.</span></span>

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a><span data-ttu-id="92afe-131">在 Chrome 和 Firefox，但不是在 Internet Explorer hello 擴充功能的運作方式</span><span class="sxs-lookup"><span data-stu-id="92afe-131">hello extension works in Chrome and Firefox, but not in Internet Explorer</span></span>

<span data-ttu-id="92afe-132">有兩個主要原因 toothis 問題：</span><span class="sxs-lookup"><span data-stu-id="92afe-132">There are two main causes toothis issue:</span></span>

-   <span data-ttu-id="92afe-133">根據 hello 如果 hello 網站不是，在 Internet Explorer 中啟用的安全性設定的一部分**信任區域**，有時候我們的指令碼遭到封鎖而無法執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="92afe-133">Depending on hello security settings enabled in Internet Explorer, if hello website is not part of a **Trusted Zone**, sometimes our script be blocked from executing for hello application.</span></span>

  *  <span data-ttu-id="92afe-134">tooresolve，太指示 hello 使用者**新增 hello 應用程式的網站**toohello**信任的網站**清單中其**Internet Explorer 安全性設定**。</span><span class="sxs-lookup"><span data-stu-id="92afe-134">tooresolve this, instruct hello user too**Add hello application’s website** toohello **Trusted Sites** list within their **Internet Explorer security settings**.</span></span> <span data-ttu-id="92afe-135">您可以傳送使用者 toohello[如何 tooadd 網站 toomy 受信任的網站清單](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5)文件以取得詳細指示。</span><span class="sxs-lookup"><span data-stu-id="92afe-135">You can send your users toohello [How tooadd a site toomy trusted sites list](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) article for detailed instructions.</span></span>

-   <span data-ttu-id="92afe-136">在極少數的情況下，Internet Explorer 的安全性驗證可能有時會造成 hello 頁面 tooload 比 hello 指令碼執行更慢。</span><span class="sxs-lookup"><span data-stu-id="92afe-136">In rare circumstances, Internet Explorer’s security validation can sometimes cause hello page tooload more slowly than hello execution of our script.</span></span>

   * <span data-ttu-id="92afe-137">不幸的是，這種情況可能會改變 hello 瀏覽器版本、 電腦的速度或瀏覽的站台而定。</span><span class="sxs-lookup"><span data-stu-id="92afe-137">Unfortunately, this situation can vary depending on hello browser version, computer speed, or site visited.</span></span> <span data-ttu-id="92afe-138">在此情況下，我們建議您連絡支援部門，以便我們可以修正 hello 這個特定的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="92afe-138">In this case, we suggest that you contact support so we can fix hello integration for this specific application.</span></span>

<span data-ttu-id="92afe-139">在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="92afe-139">In addition toothis, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them toonatively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="92afe-140">您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。</span><span class="sxs-lookup"><span data-stu-id="92afe-140">You can send hello vendor toohello [Listing your application in hello Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget them started.</span></span>

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a><span data-ttu-id="92afe-141">請檢查是否 hello 應用程式的登入頁面最近已變更或需要額外的欄位</span><span class="sxs-lookup"><span data-stu-id="92afe-141">Check if hello application’s login page has changed recently or requires an additional field</span></span>

<span data-ttu-id="92afe-142">如果已大幅變更 hello 應用程式的登入頁面，有時候這會導致我們整合 toobreak。</span><span class="sxs-lookup"><span data-stu-id="92afe-142">If hello application’s login page has changed drastically, sometimes this causes our integrations toobreak.</span></span> <span data-ttu-id="92afe-143">舉例來說，這是應用程式廠商在欄位中，captcha，加入正負號，或多重要素驗證 tootheir 發生。</span><span class="sxs-lookup"><span data-stu-id="92afe-143">An example of this is when an application vendor adds a sign in field, a captcha, or multi-factor authentication tootheir experiences.</span></span> <span data-ttu-id="92afe-144">幸運的是，在許多情況下，Microsoft 可與應用程式廠商 toorapidly 解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="92afe-144">Fortunately, in many instances, Microsoft can work with application vendors toorapidly resolve these issues.</span></span>

<span data-ttu-id="92afe-145">Microsoft 有技術 tooautomatically 偵測這些整合中斷，但有時候我們不能 toofind 時立即問題。</span><span class="sxs-lookup"><span data-stu-id="92afe-145">While Microsoft has technologies tooautomatically detect when these integrations break, but sometimes we are not able toofind these issues right away.</span></span> <span data-ttu-id="92afe-146">否則，這些會需要一些時間 toofix。</span><span class="sxs-lookup"><span data-stu-id="92afe-146">Otherwise they take some time toofix.</span></span> <span data-ttu-id="92afe-147">萬一 hello 當其中一個這些整合功能無法正常運作，我們非常感謝開啟支援案例，以便我們可以盡快修正。</span><span class="sxs-lookup"><span data-stu-id="92afe-147">In hello case when one of these integrations does not work correctly, we would appreciate opening a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="92afe-148">在加法 toothis**是否中斷此應用程式的廠商與連線****傳送我們**以便讓我們可以搭配它們 toonatively 會將其應用程式整合與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="92afe-148">In addition toothis, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them toonatively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="92afe-149">您可以傳送嗨廠商 toohello[列出 hello Azure Active Directory 應用程式庫中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)tooget 加以啟動。</span><span class="sxs-lookup"><span data-stu-id="92afe-149">You can send hello vendor toohello [Listing your application in hello Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget them started.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="92afe-150">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="92afe-150">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="92afe-151">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="92afe-151">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="92afe-152">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="92afe-152">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="92afe-153">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="92afe-153">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="92afe-154">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="92afe-154">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="92afe-155">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="92afe-155">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="92afe-156">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="92afe-156">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="92afe-157">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="92afe-157">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="92afe-158">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="92afe-158">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="92afe-159">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="92afe-159">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="92afe-160">您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="92afe-160">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="92afe-161">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="92afe-161">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="92afe-162">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="92afe-162">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a><span data-ttu-id="92afe-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92afe-163">Next steps</span></span>
[<span data-ttu-id="92afe-164">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="92afe-164">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

