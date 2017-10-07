---
title: "aaaHow tooconfigure 密碼單一登入的非組件庫的應用程式 |Microsoft 文件"
description: "如何 tooconfigure 自訂非組件庫的應用程式時，使用安全密碼型單一登入它將不會列在 hello Azure AD 應用程式庫"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e619b-103">如何 tooconfigure 密碼單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e619b-104">此外 toohello 選擇找到 hello Azure AD 應用程式庫，您也可以 hello 選項 tooadd**非組件庫的應用程式**當您想要的 hello 應用程式未在此處列出。</span><span class="sxs-lookup"><span data-stu-id="e619b-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="e619b-105">使用這項功能，您可以新增任何應用程式已存在於您的組織或您可能會使用任何協力廠商應用程式廠商還不屬於 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)。</span><span class="sxs-lookup"><span data-stu-id="e619b-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="e619b-106">一旦您加入非組件庫的應用程式，您可以設定 hello 單一登入此應用程式使用的方法藉由選取 hello**單一登入**瀏覽項目在企業中的應用程式 hello [Azure 入口網站](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e619b-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="e619b-107">其中一個 hello 單一登入方法提供 tooyou 為 hello[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)選項。</span><span class="sxs-lookup"><span data-stu-id="e619b-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="e619b-108">以 hello**加入非組件庫的應用程式**體驗，您可以整合任何應用程式可呈現 HTML 為基礎的使用者名稱和密碼會輸入欄位，即使它不在我們一組預先整合應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="e619b-109">抓取的 hello 技術的頁面存取面板延伸模組，讓我們 tooauto hello 其運作的方式就是-偵測使用者名稱和密碼的輸入的欄位，並安全地儲存特定應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="e619b-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="e619b-110">然後安全地重新執行的使用者名稱，並在使用者的密碼 toothose 欄位巡覽 toothat hello 應用程式存取面板上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="e619b-111">這是很好的方式 tooget 啟動快速，將任何種類的應用程式整合至 Azure AD，並可讓您：</span><span class="sxs-lookup"><span data-stu-id="e619b-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="e619b-112">整合**任何應用程式中的 hello world**與 Azure AD 租用戶，因此只要它們呈現 HTML 使用者名稱和密碼輸入的欄位</span><span class="sxs-lookup"><span data-stu-id="e619b-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="e619b-113">啟用**單一登入您的使用者**由安全地儲存和使用者名稱和密碼的 hello 應用程式重新執行您已與 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="e619b-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="e619b-114">**自動偵測輸入**欄位的任何應用程式，並可讓您 toomanually 偵測使用 hello 存取面板瀏覽器延伸模組，這些欄位，萬一自動偵測不到它們</span><span class="sxs-lookup"><span data-stu-id="e619b-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="e619b-115">**支援應用程式需要多個登入欄位**需要不只是使用者名稱和密碼欄位 toosign 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="e619b-116">**自訂 hello 標籤**hello 使用者名稱和密碼輸入欄位的使用者看到上 hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)當使用者輸入其認證</span><span class="sxs-lookup"><span data-stu-id="e619b-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="e619b-117">允許您**使用者**tooprovide 他們自己的使用者名稱和它們所中手動輸入 hello 任何現有應用程式帳戶的密碼[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="e619b-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="e619b-118">允許**hello 的商務群組的成員**toospecify hello 使用者名稱和密碼使用指派給 tooa 使用者 hello[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)功能</span><span class="sxs-lookup"><span data-stu-id="e619b-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="e619b-119">允許**管理員**toospecify hello 使用者名稱和密碼使用 hello 更新認證指派給 tooa 使用者功能時[指派使用者 tooan 應用程式](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="e619b-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="e619b-120">允許**管理員**toospecify hello 共用使用者名稱或密碼一群人由使用 hello 更新認證的功能時[指派群組 tooan 應用程式](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="e619b-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="e619b-121">以下說明如何啟用[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)tooany 應用程式，您將使用 hello**加入非組件庫的應用程式**體驗。</span><span class="sxs-lookup"><span data-stu-id="e619b-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="e619b-122">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="e619b-122">Overview of steps required</span></span>

<span data-ttu-id="e619b-123">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e619b-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e619b-124">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="e619b-125">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="e619b-126">Hello 應用程式 tooa 使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="e619b-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="e619b-127">直接指派使用者 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="e619b-128">直接指派應用程式 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="e619b-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="e619b-129">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-129">Add a non-gallery application</span></span>

<span data-ttu-id="e619b-130">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e619b-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e619b-131">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="e619b-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e619b-132">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e619b-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e619b-133">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e619b-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e619b-134">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e619b-135">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e619b-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e619b-136">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e619b-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="e619b-137">輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e619b-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="e619b-138">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e619b-138">Select **Add.**</span></span>

<span data-ttu-id="e619b-139">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e619b-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="e619b-140">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="e619b-141">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e619b-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e619b-142">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e619b-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e619b-143">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e619b-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e619b-144">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e619b-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e619b-145">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e619b-146">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e619b-147">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e619b-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e619b-148">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e619b-149">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e619b-150">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="e619b-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e619b-151">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="e619b-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e619b-152">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e619b-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e619b-153">請確定 hello 登入欄位會顯示在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e619b-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="e619b-154">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="e619b-155">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e619b-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="e619b-156">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="e619b-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="e619b-157">直接指派使用者 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="e619b-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="e619b-158">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e619b-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e619b-159">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e619b-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e619b-160">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e619b-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e619b-161">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e619b-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e619b-162">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e619b-163">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e619b-164">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e619b-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e619b-165">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e619b-166">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e619b-167">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e619b-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e619b-168">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e619b-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e619b-169">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="e619b-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e619b-170">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="e619b-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e619b-171">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e619b-172">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e619b-173">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e619b-174">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="e619b-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e619b-175">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="e619b-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="e619b-176">直接指派應用程式 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="e619b-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="e619b-177">tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e619b-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e619b-178">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e619b-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e619b-179">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e619b-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e619b-180">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e619b-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e619b-181">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e619b-182">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e619b-183">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e619b-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e619b-184">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e619b-185">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e619b-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e619b-186">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e619b-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e619b-187">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e619b-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e619b-188">型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="e619b-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e619b-189">將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="e619b-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e619b-190">按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e619b-191">**選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e619b-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="e619b-192">當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e619b-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e619b-193">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。</span><span class="sxs-lookup"><span data-stu-id="e619b-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="e619b-194">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。</span><span class="sxs-lookup"><span data-stu-id="e619b-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="e619b-195">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e619b-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e619b-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e619b-196">Next steps</span></span>
[<span data-ttu-id="e619b-197">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="e619b-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
