---
title: "為不在資源庫內的應用程式設定密碼單一登入時遇到的問題 | Microsoft Docs"
description: "了解使用者在為不在資源庫內的自訂應用程式設定密碼單一登入 (這類應用程式不會列於 Azure AD 應用程式庫中) 時所面臨的常見問題"
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e0a9b-103">為不在資源庫內的應用程式設定密碼單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="e0a9b-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e0a9b-104">本文可協助您了解使用者在搭配不在資源庫內的應用程式設定**密碼單一登入**時所面臨的常見問題。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e0a9b-105">如何擷取應用程式的登入欄位</span><span class="sxs-lookup"><span data-stu-id="e0a9b-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="e0a9b-106">只有具備 HTML 功能的登入頁面支援登入欄位擷取，而**非標準的登入頁面並不支援**，例如，使用快閃記憶體或其他不具備 HTML 功能技術的頁面。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="e0a9b-107">有兩種方式可讓您用來擷取自訂應用程式的登入欄位：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="e0a9b-108">自動登入欄位擷取</span><span class="sxs-lookup"><span data-stu-id="e0a9b-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="e0a9b-109">手動登入欄位擷取</span><span class="sxs-lookup"><span data-stu-id="e0a9b-109">Manual sign-in field capture</span></span>

<span data-ttu-id="e0a9b-110">**自動登入欄位擷取**適用於大部分具備 HTML 功能的登入頁面，但前提是這些頁面會**針對使用者名稱和密碼輸入欄位使用已知的 DIV 識別碼**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="e0a9b-111">其運作方式是藉由消除頁面上的 HTML 來尋找符合特定準則的 DIV 識別碼，然後儲存此應用程式的中繼資料，如此便能在稍後重新執行密碼給它。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="e0a9b-112">**手動登入欄位擷取**的適用情況是，應用程式**廠商並未標示**用來登入的輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="e0a9b-113">手動登入欄位擷取也可適用於下列情況：當**廠商呈現多個無法自動偵測的欄位**時。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="e0a9b-114">Azure AD 能在登入頁面上盡可能儲存最多欄位的資料，只要您告知我們那些欄位在頁面上的位置即可。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="e0a9b-115">一般而言，**如果自動登入欄位擷取無法運作，我們一律建議嘗試手動選項。**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e0a9b-116">如何自動擷取應用程式的登入欄位</span><span class="sxs-lookup"><span data-stu-id="e0a9b-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="e0a9b-117">若要為使用**自動登入欄位擷取**的應用程式設定**密碼單一登入**，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="e0a9b-118">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e0a9b-119">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e0a9b-120">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e0a9b-121">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e0a9b-122">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e0a9b-123">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e0a9b-124">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="e0a9b-125">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e0a9b-126">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e0a9b-127">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="e0a9b-128">這是使用者輸入其使用者名稱及密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="e0a9b-129">**確定在您提供的 URL 上看得到登入欄位**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="e0a9b-130">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="e0a9b-131">這麼做之後，我們會自動擷取使用者名稱和密碼輸入方塊的該 URL，並可讓您使用 Azure AD 並利用存取面板瀏覽器擴充功能將密碼安全地傳輸到該應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e0a9b-132">如何手動擷取應用程式的登入欄位</span><span class="sxs-lookup"><span data-stu-id="e0a9b-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="e0a9b-133">若要手動擷取登入欄位，您必須先安裝存取面板的瀏覽器延伸模組，而且**不能在 InPrivate、incognito 或私人模式中執行**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="e0a9b-134">若要安裝瀏覽器延伸模組，請依照[如何安裝存取面板的瀏覽器延伸模組](#i-cannot-manually-detect-sign-in-fields-for-my-application)一節中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="e0a9b-135">若要為使用**手動登入欄位擷取**的應用程式設定**密碼單一登入**，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="e0a9b-136">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e0a9b-137">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e0a9b-138">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e0a9b-139">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e0a9b-140">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="e0a9b-141">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e0a9b-142">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="e0a9b-143">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e0a9b-144">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e0a9b-145">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="e0a9b-146">這是使用者輸入其使用者名稱及密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="e0a9b-147">**確定在您提供的 URL 上看得到登入欄位**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="e0a9b-148">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="e0a9b-149">這麼做之後，我們會自動擷取使用者名稱和密碼輸入方塊的該 URL，並可讓您使用 Azure AD 並利用存取面板瀏覽器擴充功能將密碼安全地傳輸到該應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="e0a9b-150">萬一此作業失敗，您可以藉由繼續執行步驟 12 來**變更登入模式以使用手動登入欄位擷取**。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="e0a9b-151">按一下 [設定 &lt;appname&gt; 密碼單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="e0a9b-152">選取 [手動偵測登入欄位] 設定選項。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="e0a9b-153">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-153">Click **Ok**.</span></span>

15. <span data-ttu-id="e0a9b-154">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-154">Click **Save**.</span></span>

16. <span data-ttu-id="e0a9b-155">依照畫面指示來使用存取面板。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="e0a9b-156">我看到「在該 URL 找不到任何登入欄位」的錯誤</span><span class="sxs-lookup"><span data-stu-id="e0a9b-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="e0a9b-157">當自動偵測登入欄位失敗時，您就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="e0a9b-158">若要解決此問題，請依照[如何手動擷取應用程式的登入欄位](#how-to-manually-capture-sign-in-fields-for-an-application)一節中的步驟，嘗試執行手動登入欄位偵測。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="e0a9b-159">我看到「無法儲存單一登入設定」錯誤</span><span class="sxs-lookup"><span data-stu-id="e0a9b-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="e0a9b-160">在某些罕見的情況下，更新單一登入設定可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="e0a9b-161">若要解決此錯誤，請再次嘗試儲存單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="e0a9b-162">如果這持續不斷失敗，請開啟一個支援案例，並提供[如何查看入口網站通知的詳細資料](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[如何將通知詳細資料傳送給支援工程師以取得協助](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)小節中所收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="e0a9b-163">我無法手動偵測應用程式的登入欄位</span><span class="sxs-lookup"><span data-stu-id="e0a9b-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="e0a9b-164">當手動偵測無法運作時，您可能看到某些行為，包括：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="e0a9b-165">手動擷取程序看似正常運作，但擷取的欄位不正確</span><span class="sxs-lookup"><span data-stu-id="e0a9b-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="e0a9b-166">在執行擷取程序時並未反白顯示適當的欄位</span><span class="sxs-lookup"><span data-stu-id="e0a9b-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="e0a9b-167">擷取程序如預期般將我帶到應用程式的登入頁面，但什麼事也沒發生</span><span class="sxs-lookup"><span data-stu-id="e0a9b-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="e0a9b-168">手動擷取看似正常運作，但是，當我的使用者從存取面板瀏覽至應用程式，SSO 不會發生。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="e0a9b-169">如果您遇到這其中任一個問題，請檢查下列內容：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="e0a9b-170">確定您已依照[如何安裝存取面板的瀏覽器延伸模組](#how-to-install-the-access-panel-browser-extension)一節中的步驟，**安裝**並**啟用**最新版本的存取面板瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="e0a9b-171">確定您未在瀏覽器處於 **incognito、InPrivate 或私人模式**時嘗試擷取程序。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e0a9b-172">這些模式不支援存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e0a9b-173">確定您的使用者未在 **incognito、InPrivate 或私人模式**中，嘗試從存取面板登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e0a9b-174">這些模式不支援存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e0a9b-175">再次嘗試手動擷取程序，確保正確的欄位上都有紅色標記。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="e0a9b-176">如果手動擷取程序看起來沒有回應，或者登入頁面不會執行任何動作 (上述的案例 3)，請再試一次手動擷取程序。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="e0a9b-177">但這次已完成此程序，請按 **F12** 按鈕，以開啟瀏覽器的開發人員主控台。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="e0a9b-178">位於該處之後，開啟**主控台**並輸入 **window.location="&lt;輸入您在設定應用程式時所指定的登入 url&gt;"**，然後按 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="e0a9b-179">這樣會強制執行頁面重新導向，以結束擷取程序並儲存已擷取的欄位。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="e0a9b-180">如果這其中沒有任何一種方式適合您，我們很樂意提供協助。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="e0a9b-181">請開啟一個支援案例，並提供您所嘗試動作的詳細資料，以及[如何查看入口網站通知的詳細資料](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[如何將通知詳細資料傳送給支援工程師以取得協助](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)小節 (如果適用) 中所收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="e0a9b-182">如何安裝存取面板的瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="e0a9b-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="e0a9b-183">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="e0a9b-184">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="e0a9b-185">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="e0a9b-186">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="e0a9b-187">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="e0a9b-188">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="e0a9b-189">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="e0a9b-190">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="e0a9b-191">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="e0a9b-192">您可能也會從下列直接連結中下載適用於 Chrome 和 Firefox 的延伸模組：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="e0a9b-193">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="e0a9b-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="e0a9b-194">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="e0a9b-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="e0a9b-195">如何查看入口網站通知的詳細資料</span><span class="sxs-lookup"><span data-stu-id="e0a9b-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="e0a9b-196">您可以依照下列步驟來查看任何入口網站通知的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="e0a9b-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="e0a9b-197">按一下 Azure 入口網站右上方的 [通知] 圖示 (鐘)。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="e0a9b-198">選取處於**錯誤**狀態的任何通知 (旁邊有紅色 (!))。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="e0a9b-199">!NOTE] 您無法按一下處於**成功**或**進行中**狀態的通知。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="e0a9b-200">這會開啟 [通知詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="e0a9b-201">請自行利用這項資訊來了解更多問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="e0a9b-202">如果您仍然需要協助，您也可以將這項資訊分享給支援工程師或產品群組，以取得協助來解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="e0a9b-203">按一下 [複製錯誤] 文字方塊右邊的**複製****圖示**，以複製所有通知詳細資料來分享給支援工程師或產品群組工程師。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="e0a9b-204">如何將通知詳細資料傳送給支援工程師以取得協助</span><span class="sxs-lookup"><span data-stu-id="e0a9b-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="e0a9b-205">如果您需要協助，一定要與支援工程師分享**下列所有詳細資料**，好讓他們儘快幫助您。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="e0a9b-206">只要**擷取螢幕畫面**，或按一下 [複製錯誤] 文字方塊右邊的**複製錯誤圖示**，輕鬆就能這樣做。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="e0a9b-207">說明通知詳細資料</span><span class="sxs-lookup"><span data-stu-id="e0a9b-207">Notification Details Explained</span></span>

<span data-ttu-id="e0a9b-208">以下詳細說明每個通知項目的意義，並提供個別的範例。</span><span class="sxs-lookup"><span data-stu-id="e0a9b-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="e0a9b-209">必要通知項目</span><span class="sxs-lookup"><span data-stu-id="e0a9b-209">Essential Notification Items</span></span>

-   <span data-ttu-id="e0a9b-210">**標題** - 通知的描述性標題</span><span class="sxs-lookup"><span data-stu-id="e0a9b-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="e0a9b-211">範例 - **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="e0a9b-212">**描述** - 作業所產生之結果的描述</span><span class="sxs-lookup"><span data-stu-id="e0a9b-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="e0a9b-213">範例 - **輸入的內部 URL 正由另一個應用程式使用中**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="e0a9b-214">**通知識別碼** - 通知的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="e0a9b-215">範例 - **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="e0a9b-216">**用戶端要求識別碼** - 瀏覽器所產生的特定要求識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="e0a9b-217">範例 - **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="e0a9b-218">**時間戳記 UTC** - 發生通知期間的時間戳記 (UTC)</span><span class="sxs-lookup"><span data-stu-id="e0a9b-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="e0a9b-219">範例 - **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="e0a9b-220">**內部交易識別碼** - 可用來在系統中查閱錯誤的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="e0a9b-221">範例 - **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="e0a9b-222">**UPN** - 執行作業的使用者</span><span class="sxs-lookup"><span data-stu-id="e0a9b-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="e0a9b-223">範例 - **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="e0a9b-224">**租用戶識別碼** - 作業執行使用者所屬之租用戶的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="e0a9b-225">範例 - **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="e0a9b-226">**使用者物件識別碼** - 執行作業之使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="e0a9b-227">範例 - **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="e0a9b-228">詳細通知項目</span><span class="sxs-lookup"><span data-stu-id="e0a9b-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="e0a9b-229">**顯示名稱** - **(可以是空白)** 錯誤的更詳細顯示名稱</span><span class="sxs-lookup"><span data-stu-id="e0a9b-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="e0a9b-230">範例 *- **應用程式 Proxy 設定**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="e0a9b-231">**狀態** - 通知的特定狀態</span><span class="sxs-lookup"><span data-stu-id="e0a9b-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="e0a9b-232">範例 *- **失敗**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="e0a9b-233">**物件識別碼** - **(可以是空白)** 據以執行作業的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="e0a9b-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="e0a9b-234">範例 - **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="e0a9b-235">**詳細資料** - 作業所產生之結果的詳細描述</span><span class="sxs-lookup"><span data-stu-id="e0a9b-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="e0a9b-236">範例 - **內部 url 'http://bing.com/' 無效，因為已在使用中**</span><span class="sxs-lookup"><span data-stu-id="e0a9b-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="e0a9b-237">**複製錯誤** - 按一下 [複製錯誤] 文字方塊右邊的**複製圖示**，以複製所有通知詳細資料來分享給支援工程師或產品群組工程師</span><span class="sxs-lookup"><span data-stu-id="e0a9b-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="e0a9b-238">範例 - ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="e0a9b-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0a9b-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0a9b-239">Next steps</span></span>
[<span data-ttu-id="e0a9b-240">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="e0a9b-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

