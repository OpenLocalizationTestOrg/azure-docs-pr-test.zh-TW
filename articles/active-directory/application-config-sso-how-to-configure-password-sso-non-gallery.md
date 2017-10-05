---
title: "如何為不在資源庫內的應用程式設定密碼單一登入 | Microsoft Docs"
description: "當不在資源庫內的自訂應用程式未列在 Azure AD 應用程式庫時，如何為它設定以密碼為基礎的安全單一登入"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ee7a3-103">如何為不在資源庫內的應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="ee7a3-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ee7a3-104">除了 Azure AD 應用程式庫中找到的選項，當您想要的應用程式未在此處列出時，您也可以選擇新增**不在資源庫內的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="ee7a3-105">使用這項功能，您可以新增任何已存在於組織中的應用程式，或您可能從尚不屬於 [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)的供應商取得的任何第三方應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="ee7a3-106">當您新增不在資源庫內的應用程式之後，接著就可以在 [Azure 入口網站](https://portal.azure.com/)中選取企業應用程式的 [單一登入] 瀏覽項目，以設定此應用程式使用的單一登入方法。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="ee7a3-107">可供您使用的其中一個單一登入方法是[以密碼為基礎的單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)選項。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="ee7a3-108">透過**新增不在資源庫內的應用程式**經驗，您可以整合任何呈現 HTML 使用者名稱和密碼輸入欄位的應用程式 (即使它不在我們預先整合的應用程式集之內)。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="ee7a3-109">運作方式是採用存取面板擴充中的頁面抓取技術，這可讓我們自動偵測使用者名稱和密碼輸入欄位，安全地儲存這些欄位供您的特定應用程式執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="ee7a3-110">然後，當使用者在應用程式存取面板上瀏覽至該應用程式時，就安全地將使用者名稱和密碼重播給這些欄位。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="ee7a3-111">這是開始將任何一種應用程式快速整合至 Azure AD 的絕佳方法，可讓您︰</span><span class="sxs-lookup"><span data-stu-id="ee7a3-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="ee7a3-112">整合**坊間任何應用程式**和您的 Azure AD 租用戶 (只要應用程式會呈現 HTML 使用者名稱和密碼輸入欄位)</span><span class="sxs-lookup"><span data-stu-id="ee7a3-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="ee7a3-113">針對已經與 Azure AD 整合的應用程式，安全地儲存和重播使用者名稱和密碼，以啟用**使用者的單一登入**</span><span class="sxs-lookup"><span data-stu-id="ee7a3-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="ee7a3-114">針對任何應用程式**自動偵測輸入**欄位，萬一自動偵測找不到這些欄位，您還可以使用存取面板瀏覽器擴充來手動偵測</span><span class="sxs-lookup"><span data-stu-id="ee7a3-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="ee7a3-115">針對需要使用者名稱和密碼以外的更多欄位才能登入的應用程式，**支援需要多個登入欄位的應用程式**</span><span class="sxs-lookup"><span data-stu-id="ee7a3-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="ee7a3-116">針對使用者在[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)輸入認證時所看到的使用者名稱和密碼輸入欄位，**自訂標籤**</span><span class="sxs-lookup"><span data-stu-id="ee7a3-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="ee7a3-117">針對**使用者**在[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)手動輸入的任何現有應用程式帳戶，允許他們提供自己的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="ee7a3-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="ee7a3-118">允許**商務群組的成員**使用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)功能，指定要指派給使用者的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="ee7a3-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="ee7a3-119">允許**管理員**在[將使用者指派至應用程式](#_How_to_configure_1)時，使用更新憑證功能指定要指派給使用者的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="ee7a3-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="ee7a3-120">允許**管理員**在[將群組指派至應用程式](#assign-an-application-to-a-group-directly)時，使用更新憑證功能指定一群人使用的共用使用者名稱或密碼</span><span class="sxs-lookup"><span data-stu-id="ee7a3-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="ee7a3-121">以下說明如何針對您使用**新增不在資源庫內的應用程式**經驗所新增的任何應用程式，啟用[以密碼為基礎的單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="ee7a3-122">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="ee7a3-122">Overview of steps required</span></span>

<span data-ttu-id="ee7a3-123">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="ee7a3-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ee7a3-124">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7a3-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ee7a3-125">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="ee7a3-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="ee7a3-126">將應用程式指派至使用者或群組</span><span class="sxs-lookup"><span data-stu-id="ee7a3-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="ee7a3-127">將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7a3-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="ee7a3-128">將應用程式直接指派至群組</span><span class="sxs-lookup"><span data-stu-id="ee7a3-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="ee7a3-129">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7a3-129">Add a non-gallery application</span></span>

<span data-ttu-id="ee7a3-130">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="ee7a3-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="ee7a3-131">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ee7a3-132">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ee7a3-133">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ee7a3-134">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ee7a3-135">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="ee7a3-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ee7a3-136">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="ee7a3-137">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="ee7a3-138">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-138">Select **Add.**</span></span>

<span data-ttu-id="ee7a3-139">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="ee7a3-140">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="ee7a3-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="ee7a3-141">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="ee7a3-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="ee7a3-142">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ee7a3-143">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ee7a3-144">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ee7a3-145">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ee7a3-146">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ee7a3-147">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ee7a3-148">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ee7a3-149">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ee7a3-150">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ee7a3-151">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ee7a3-152">這是使用者輸入使用者名稱和密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ee7a3-153">確保在 URL 看得到登入欄位。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="ee7a3-154">將使用者指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-154">Assign users to the application.</span></span>

11. <span data-ttu-id="ee7a3-155">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="ee7a3-156">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="ee7a3-157">將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7a3-157">Assign a user to an application directly</span></span>

<span data-ttu-id="ee7a3-158">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="ee7a3-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="ee7a3-159">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ee7a3-160">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ee7a3-161">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ee7a3-162">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ee7a3-163">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ee7a3-164">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ee7a3-165">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="ee7a3-166">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ee7a3-167">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ee7a3-168">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ee7a3-169">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ee7a3-170">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="ee7a3-171">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="ee7a3-172">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="ee7a3-173">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="ee7a3-174">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="ee7a3-175">按一下 [指派] 按鈕，將應用程式指派至選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="ee7a3-176">將應用程式直接指派至群組</span><span class="sxs-lookup"><span data-stu-id="ee7a3-176">Assign an application to a group directly</span></span>

<span data-ttu-id="ee7a3-177">若要直接將一或多個群組指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="ee7a3-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="ee7a3-178">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ee7a3-179">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ee7a3-180">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ee7a3-181">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ee7a3-182">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ee7a3-183">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ee7a3-184">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="ee7a3-185">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ee7a3-186">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ee7a3-187">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ee7a3-188">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之群組的**完整群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ee7a3-189">將滑鼠停留在清單中的**群組**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="ee7a3-190">按一下群組設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="ee7a3-191">**選擇性︰**如果您想要**新增多個群組**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**完整群組名稱**，然後按一下核取方塊，將此群組新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="ee7a3-192">當您完成選取群組時，按一下 [選取] 按鈕，將它們新增到要指派給應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="ee7a3-193">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取群組的角色。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="ee7a3-194">按一下 [指派] 按鈕，將應用程式指派給選取的群組。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="ee7a3-195">稍待片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7a3-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee7a3-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee7a3-196">Next steps</span></span>
[<span data-ttu-id="ee7a3-197">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7a3-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
