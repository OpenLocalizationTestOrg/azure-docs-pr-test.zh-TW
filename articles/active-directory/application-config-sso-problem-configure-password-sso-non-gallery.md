---
title: "設定密碼單一登入非組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "在 hello Azure AD 應用程式庫中設定密碼單一登入的未列出的自訂非組件庫應用程式時，了解 hello 一般問題的人臉"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4996c-103">為不在資源庫內的應用程式設定密碼單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="4996c-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4996c-104">本文協助您 toounderstand hello 一般問題的人臉設定時**密碼單一登入**與非組件庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4996c-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="4996c-105">Toocapture 登入欄位如何為應用程式</span><span class="sxs-lookup"><span data-stu-id="4996c-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="4996c-106">只有具備 HTML 功能的登入頁面支援登入欄位擷取，而**非標準的登入頁面並不支援**，例如，使用快閃記憶體或其他不具備 HTML 功能技術的頁面。</span><span class="sxs-lookup"><span data-stu-id="4996c-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="4996c-107">有兩種方式可讓您用來擷取自訂應用程式的登入欄位：</span><span class="sxs-lookup"><span data-stu-id="4996c-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="4996c-108">自動登入欄位擷取</span><span class="sxs-lookup"><span data-stu-id="4996c-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="4996c-109">手動登入欄位擷取</span><span class="sxs-lookup"><span data-stu-id="4996c-109">Manual sign-in field capture</span></span>

<span data-ttu-id="4996c-110">**自動登入欄位擷取**適用於大部分 HTML 啟用登入頁面，如果他們使用**已知 DIV 識別碼 hello 使用者名稱和密碼輸入**欄位。</span><span class="sxs-lookup"><span data-stu-id="4996c-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="4996c-111">hello 這個運作的方式是透過抓取 hello HTML hello 頁面 toofind DIV 識別碼符合特定準則的上，然後儲存此應用程式的中繼資料，因此我們可以稍後重新執行密碼 tooit。</span><span class="sxs-lookup"><span data-stu-id="4996c-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="4996c-112">**手動登入欄位擷取**可用在 hello 應用程式的 hello 案例**供應商並未標示**hello 輸入用來登入的欄位。</span><span class="sxs-lookup"><span data-stu-id="4996c-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="4996c-113">手動登入欄位擷取也可用在 hello 情況下，如果 hello**廠商呈現多個欄位**無法自動偵測。</span><span class="sxs-lookup"><span data-stu-id="4996c-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="4996c-114">Azure AD 可以儲存資料所多少個欄位上 hello 登入頁面上，只要您告訴我們，這些欄位位於 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="4996c-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="4996c-115">一般情況下，**如果自動登入欄位擷取無法運作，我們建議嘗試 hello 手動選項。**</span><span class="sxs-lookup"><span data-stu-id="4996c-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="4996c-116">Tooautomatically 如何擷取登入應用程式的欄位</span><span class="sxs-lookup"><span data-stu-id="4996c-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="4996c-117">tooconfigure**密碼型單一登入**應用程式使用**自動登入欄位擷取**，依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="4996c-118">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="4996c-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4996c-119">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="4996c-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4996c-120">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="4996c-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4996c-121">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="4996c-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4996c-122">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="4996c-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4996c-123">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="4996c-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4996c-124">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4996c-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="4996c-125">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="4996c-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4996c-126">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="4996c-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4996c-127">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="4996c-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="4996c-128">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="4996c-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="4996c-129">**確認 hello 登入欄位是否顯示在您提供的 hello URL**。</span><span class="sxs-lookup"><span data-stu-id="4996c-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="4996c-130">按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4996c-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="4996c-131">一旦您這樣做，我們會自動將消除該 URL 的使用者名稱和密碼輸入方塊，並且可讓您 toouse Azure AD toosecurely 傳輸密碼 toothat 應用程式使用 hello 存取面板瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4996c-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="4996c-132">Toomanually 如何擷取登入應用程式的欄位</span><span class="sxs-lookup"><span data-stu-id="4996c-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="4996c-133">toomanually 擷取登入欄位，您必須先安裝 hello 存取面板瀏覽器延伸模組和**inPrivate、 incognito，或私用模式中不在執行。**</span><span class="sxs-lookup"><span data-stu-id="4996c-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="4996c-134">tooinstall hello 瀏覽器延伸模組，後續的 hello 步驟在 hello [tooinstall hello 存取面板瀏覽器延伸模組的方式](#i-cannot-manually-detect-sign-in-fields-for-my-application)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4996c-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="4996c-135">tooconfigure**密碼型單一登入**應用程式使用**手動登入欄位擷取**，依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="4996c-136">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="4996c-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4996c-137">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="4996c-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4996c-138">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="4996c-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4996c-139">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="4996c-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4996c-140">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="4996c-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="4996c-141">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="4996c-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4996c-142">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4996c-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="4996c-143">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="4996c-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4996c-144">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="4996c-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4996c-145">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="4996c-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="4996c-146">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="4996c-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="4996c-147">**確認 hello 登入欄位是否顯示在您提供的 hello URL**。</span><span class="sxs-lookup"><span data-stu-id="4996c-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="4996c-148">按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4996c-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="4996c-149">一旦您這樣做，我們會自動將消除該 URL 的使用者名稱和密碼輸入方塊，並且可讓您 toouse Azure AD toosecurely 傳輸密碼 toothat 應用程式使用 hello 存取面板瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4996c-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="4996c-150">您可以在 hello 失敗的情況下，**異動 hello 登入模式 toouse 手動登入欄位擷取**繼續 toostep 12。</span><span class="sxs-lookup"><span data-stu-id="4996c-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="4996c-151">按一下 [設定 &lt;appname&gt; 密碼單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="4996c-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="4996c-152">選取 hello**手動偵測登入欄位**組態選項。</span><span class="sxs-lookup"><span data-stu-id="4996c-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="4996c-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4996c-153">Click **Ok**.</span></span>

15. <span data-ttu-id="4996c-154">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4996c-154">Click **Save**.</span></span>

16. <span data-ttu-id="4996c-155">依照畫面指示 toouse hello 存取面板中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4996c-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="4996c-156">我看到「在該 URL 找不到任何登入欄位」的錯誤</span><span class="sxs-lookup"><span data-stu-id="4996c-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="4996c-157">當自動偵測登入欄位失敗時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4996c-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="4996c-158">此問題，請嘗試手動登入欄位偵測所遵循的 hello 步驟 hello tooresolve [toomanually 如何擷取應用程式的登入欄位](#how-to-manually-capture-sign-in-fields-for-an-application)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4996c-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="4996c-159">我看到 「 無法 toosave 單一登入設定 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="4996c-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="4996c-160">在某些罕見的情況下，更新 hello 單一登入組態可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4996c-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="4996c-161">tooresolve 這重試儲存 hello 單一登入組態一次。</span><span class="sxs-lookup"><span data-stu-id="4996c-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="4996c-162">如果此問題持續 toofail 一致的方式，提交支援案例，並提供 hello 蒐集在 hello[如何 toosee hello 詳細資料的入口網站的通知](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[tooget 如何藉由傳送通知的詳細資料 tooa 協助支援工程師](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)區段。</span><span class="sxs-lookup"><span data-stu-id="4996c-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="4996c-163">我無法手動偵測應用程式的登入欄位</span><span class="sxs-lookup"><span data-stu-id="4996c-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="4996c-164">手動偵測為不使用時，您可能會看到 hello 行為的部分包括：</span><span class="sxs-lookup"><span data-stu-id="4996c-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="4996c-165">hello 手動擷取程序 toowork，但未正確擷取 hello 欄位</span><span class="sxs-lookup"><span data-stu-id="4996c-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="4996c-166">hello 右側欄位未取得反白顯示執行 hello 擷取程序時</span><span class="sxs-lookup"><span data-stu-id="4996c-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="4996c-167">hello 擷取程序接受我 toohello 應用程式的登入頁面如預期般，但會發生任何事</span><span class="sxs-lookup"><span data-stu-id="4996c-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="4996c-168">手動擷取出現 toowork，但我的使用者瀏覽 toohello hello 存取面板應用程式時，不會發生 SSO。</span><span class="sxs-lookup"><span data-stu-id="4996c-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="4996c-169">如果您遇到任何問題，請檢查下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="4996c-170">確定您已擁有 hello hello 存取面板瀏覽器延伸模組最新版本**安裝**和**啟用**hello 中的 hello 步驟[tooinstall 如何 hello 存取面板瀏覽器延伸模組](#how-to-install-the-access-panel-browser-extension)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4996c-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="4996c-171">請確定您未在您的瀏覽器中時嘗試 hello 擷取處理序**incognito、 inPrivate，或私用模式**。</span><span class="sxs-lookup"><span data-stu-id="4996c-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="4996c-172">hello 存取面板延伸模組不支援這些模式中。</span><span class="sxs-lookup"><span data-stu-id="4996c-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="4996c-173">請確定您的使用者沒有 toosign toohello hello 存取面板時在應用程式**incognito、 inPrivate，或私用模式**。</span><span class="sxs-lookup"><span data-stu-id="4996c-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="4996c-174">hello 存取面板延伸模組不支援這些模式中。</span><span class="sxs-lookup"><span data-stu-id="4996c-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="4996c-175">再試一次 hello 手動擷取程序，確保 hello 紅色標記透過 hello 正確的欄位。</span><span class="sxs-lookup"><span data-stu-id="4996c-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="4996c-176">Hello 手動擷取程序看起來 toohang，則不會執行 hello 登入頁面上的任何項目 （情況 3 以上），hello 手動擷取處理序再試一次。</span><span class="sxs-lookup"><span data-stu-id="4996c-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="4996c-177">但是，此時間之後完成 hello 程序，請按 hello **F12**按鈕 tooopen 瀏覽器的開發人員主控台。</span><span class="sxs-lookup"><span data-stu-id="4996c-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="4996c-178">一次，開啟 hello**主控台**和型別**window.location="&lt;輸入設定 hello 應用程式時，您指定的 url 中的 hello 登&gt;"** ，然後按**輸入**。</span><span class="sxs-lookup"><span data-stu-id="4996c-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="4996c-179">此強制頁面重新導向的結束 hello 擷取程序，並儲存已擷取的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="4996c-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="4996c-180">如果這其中沒有任何一種方式適合您，我們很樂意提供協助。</span><span class="sxs-lookup"><span data-stu-id="4996c-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="4996c-181">Hello 詳細資料，來嘗試什麼方法，以及所蒐集 hello 中的 hello 資訊提交支援案例[如何 toosee hello 詳細資料的入口網站的通知](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[tooget 如何協助 tooa 支援傳送通知的詳細資料工程](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)區段 （如果適用）。</span><span class="sxs-lookup"><span data-stu-id="4996c-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="4996c-182">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="4996c-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="4996c-183">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="4996c-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="4996c-184">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4996c-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="4996c-185">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="4996c-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="4996c-186">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="4996c-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="4996c-187">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="4996c-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="4996c-188">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4996c-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="4996c-189">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4996c-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="4996c-190">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="4996c-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="4996c-191">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4996c-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="4996c-192">您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="4996c-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="4996c-193">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="4996c-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="4996c-194">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="4996c-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="4996c-195">如何 toosee hello 詳細資料的入口網站的通知</span><span class="sxs-lookup"><span data-stu-id="4996c-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="4996c-196">您可以依照以下 hello 步驟看到 hello 詳細資料的任何入口網站的通知：</span><span class="sxs-lookup"><span data-stu-id="4996c-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="4996c-197">按一下 hello**通知**hello Azure 入口網站的 hello 右上角的圖示 （hello 鈴聲）</span><span class="sxs-lookup"><span data-stu-id="4996c-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="4996c-198">選取中的任何通知**錯誤**狀態 （紅色 （！） 的 下一步 toothem 與那些）。</span><span class="sxs-lookup"><span data-stu-id="4996c-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="4996c-199">!NOTE] 您無法按一下處於**成功**或**進行中**狀態的通知。</span><span class="sxs-lookup"><span data-stu-id="4996c-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="4996c-200">這個開啟 hello**通知的詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4996c-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="4996c-201">使用此資訊自行 toounderstand 更多有關 hello 問題詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4996c-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="4996c-202">如果您仍需要協助，您也可以與您的問題共用與支援工程師或 hello 產品群組 tooget 說明這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4996c-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="4996c-203">按一下 hello**複製****圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 通知詳細資料 tooshare 與支援或產品的群組工程師。</span><span class="sxs-lookup"><span data-stu-id="4996c-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="4996c-204">藉由傳送通知的詳細資料 tooa 支援工程師 tooget 的說明</span><span class="sxs-lookup"><span data-stu-id="4996c-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="4996c-205">它是非常重要，共用**所有 hello 下面所列的詳細資料**支援工程師，如果您需要協助，以便它們可以協助您快速。</span><span class="sxs-lookup"><span data-stu-id="4996c-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="4996c-206">您可以輕鬆**擷取螢幕畫面，**或按一下 hello**複製錯誤圖示**，找到 toohello 右邊 hello**複製錯誤**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4996c-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="4996c-207">說明通知詳細資料</span><span class="sxs-lookup"><span data-stu-id="4996c-207">Notification Details Explained</span></span>

<span data-ttu-id="4996c-208">hello 以下說明更每一項 hello 通知項目表示，以及每個提供範例。</span><span class="sxs-lookup"><span data-stu-id="4996c-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="4996c-209">必要通知項目</span><span class="sxs-lookup"><span data-stu-id="4996c-209">Essential Notification Items</span></span>

-   <span data-ttu-id="4996c-210">**標題**– hello hello 通知的描述性標題</span><span class="sxs-lookup"><span data-stu-id="4996c-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="4996c-211">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="4996c-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="4996c-212">**描述**– hello 所發生的 hello 運算結果的描述</span><span class="sxs-lookup"><span data-stu-id="4996c-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="4996c-213">範例 - **輸入的內部 URL 正由另一個應用程式使用中**</span><span class="sxs-lookup"><span data-stu-id="4996c-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="4996c-214">**通知識別碼**– hello 的 hello 通知的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4996c-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="4996c-215">範例 - **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="4996c-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="4996c-216">**用戶端要求 Id** – 您的瀏覽器所做的 hello 特定要求識別碼</span><span class="sxs-lookup"><span data-stu-id="4996c-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="4996c-217">範例 - **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="4996c-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="4996c-218">**時間戳記 UTC** – hello 期間 hello 通知發生，以 UTC 時間戳記</span><span class="sxs-lookup"><span data-stu-id="4996c-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="4996c-219">範例 - **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="4996c-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="4996c-220">**內部交易識別碼**– hello 我們可能佔用 toolook hello 錯誤，我們系統中的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="4996c-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="4996c-221">範例 - **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="4996c-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="4996c-222">**UPN** – 執行 hello 作業的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="4996c-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="4996c-223">範例 - **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="4996c-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="4996c-224">**租用戶識別碼**– hello 唯一 hello 租用戶識別碼 hello 使用者執行 hello 作業人員是的成員</span><span class="sxs-lookup"><span data-stu-id="4996c-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="4996c-225">範例 - **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="4996c-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="4996c-226">**使用者物件識別碼**– hello 執行 hello 作業的 hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4996c-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="4996c-227">範例 - **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="4996c-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="4996c-228">詳細通知項目</span><span class="sxs-lookup"><span data-stu-id="4996c-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="4996c-229">**顯示名稱**– **（可以是空的）** hello 錯誤的更詳細的顯示名稱</span><span class="sxs-lookup"><span data-stu-id="4996c-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="4996c-230">範例 *- **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="4996c-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="4996c-231">**狀態**– hello hello 通知的特定狀態</span><span class="sxs-lookup"><span data-stu-id="4996c-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="4996c-232">範例 *- **失敗**</span><span class="sxs-lookup"><span data-stu-id="4996c-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="4996c-233">**物件識別碼**– **（可以是空的）** hello 的 hello 針對已執行作業的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="4996c-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="4996c-234">範例 - **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="4996c-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="4996c-235">**詳細資料**– hello 的詳細描述所發生的 hello 運算結果</span><span class="sxs-lookup"><span data-stu-id="4996c-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="4996c-236">範例 - **內部 url 'http://bing.com/' 無效，因為已在使用中**</span><span class="sxs-lookup"><span data-stu-id="4996c-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="4996c-237">**複製錯誤**– 按一下 hello**複製圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 與支援或產品的群組工程師通知詳細資料 tooshare</span><span class="sxs-lookup"><span data-stu-id="4996c-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="4996c-238">範例 - ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="4996c-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="4996c-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4996c-239">Next steps</span></span>
[<span data-ttu-id="4996c-240">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="4996c-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

