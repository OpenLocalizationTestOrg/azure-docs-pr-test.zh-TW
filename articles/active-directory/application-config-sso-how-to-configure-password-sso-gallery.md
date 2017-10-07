---
title: "aaaHow tooconfigure 密碼單一登入 Azure AD 庫應用程式 |Microsoft 文件"
description: "如何 tooconfigure 的應用程式時，使用安全密碼型單一登入已列入 hello Azure AD 應用程式庫"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="3137f-103">如何 tooconfigure 密碼單一登入 Azure AD 庫應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="3137f-104">當您新增應用程式從 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)，說明您希望您的使用者 toosign toothat 應用程式中的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="3137f-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="3137f-105">您可以設定這項選擇隨時藉由選取 hello**單一登入**瀏覽項目在企業中的應用程式 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3137f-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="3137f-106">其中一個 hello 單一登入方法提供 tooyou 為 hello[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)選項。</span><span class="sxs-lookup"><span data-stu-id="3137f-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="3137f-107">這是很好的方式 tooget 啟動快速，整合至 Azure AD 的應用程式，並可讓您：</span><span class="sxs-lookup"><span data-stu-id="3137f-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="3137f-108">啟用**單一登入您的使用者**由安全地儲存和使用者名稱和密碼的 hello 應用程式重新執行您已與 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="3137f-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="3137f-109">**支援應用程式需要多個登入欄位**需要不只是使用者名稱和密碼欄位 toosign 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="3137f-110">**自訂 hello 標籤**hello 使用者名稱和密碼輸入欄位的使用者看到上 hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)當使用者輸入其認證</span><span class="sxs-lookup"><span data-stu-id="3137f-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="3137f-111">允許您**使用者**tooprovide 他們自己的使用者名稱和它們所中手動輸入 hello 任何現有應用程式帳戶的密碼[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="3137f-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="3137f-112">允許**hello 的商務群組的成員**toospecify hello 使用者名稱和密碼使用指派給 tooa 使用者 hello[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)功能</span><span class="sxs-lookup"><span data-stu-id="3137f-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="3137f-113">允許**管理員**toospecify hello 使用者名稱和密碼使用 hello 更新認證指派給 tooa 使用者功能時[指派使用者 tooan 應用程式](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="3137f-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="3137f-114">允許**管理員**toospecify hello 共用使用者名稱或密碼一群人由使用 hello 更新認證的功能時[指派群組 tooan 應用程式](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="3137f-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="3137f-115">以下說明如何啟用[密碼型單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)tooan 應用程式已在 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)。</span><span class="sxs-lookup"><span data-stu-id="3137f-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3137f-116">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="3137f-116">Overview of steps required</span></span>
<span data-ttu-id="3137f-117">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="3137f-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="3137f-118">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="3137f-119">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="3137f-120">Hello 應用程式 tooa 使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="3137f-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="3137f-121">直接指派使用者 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="3137f-122">直接指派應用程式 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="3137f-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="3137f-123">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="3137f-124">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="3137f-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3137f-125">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="3137f-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="3137f-126">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="3137f-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3137f-127">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="3137f-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3137f-128">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3137f-129">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="3137f-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="3137f-130">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="3137f-131">選取您想 tooconfigure 進行單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="3137f-132">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3137f-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="3137f-133">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3137f-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="3137f-134">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3137f-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="3137f-135">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="3137f-136">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="3137f-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3137f-137">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="3137f-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3137f-138">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="3137f-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3137f-139">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="3137f-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3137f-140">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3137f-141">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3137f-142">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="3137f-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3137f-143">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="3137f-144">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3137f-145">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="3137f-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="3137f-146">[將使用者指派 toohello 應用程式](#assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="3137f-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="3137f-147">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="3137f-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="3137f-148">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="3137f-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="3137f-149">直接指派使用者 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="3137f-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="3137f-150">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="3137f-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3137f-151">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="3137f-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3137f-152">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="3137f-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3137f-153">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="3137f-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3137f-154">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3137f-155">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3137f-156">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="3137f-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3137f-157">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3137f-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3137f-158">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3137f-159">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3137f-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3137f-160">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3137f-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3137f-161">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="3137f-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3137f-162">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="3137f-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3137f-163">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3137f-164">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3137f-165">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3137f-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3137f-166">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="3137f-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3137f-167">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="3137f-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="3137f-168">直接指派應用程式 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="3137f-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="3137f-169">tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="3137f-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3137f-170">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="3137f-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3137f-171">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="3137f-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3137f-172">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="3137f-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3137f-173">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3137f-174">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3137f-175">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="3137f-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3137f-176">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3137f-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3137f-177">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="3137f-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3137f-178">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3137f-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3137f-179">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3137f-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3137f-180">型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="3137f-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3137f-181">將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="3137f-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3137f-182">按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3137f-183">**選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="3137f-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="3137f-184">當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3137f-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3137f-185">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。</span><span class="sxs-lookup"><span data-stu-id="3137f-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="3137f-186">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。</span><span class="sxs-lookup"><span data-stu-id="3137f-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="3137f-187">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3137f-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3137f-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3137f-188">Next steps</span></span>
[<span data-ttu-id="3137f-189">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="3137f-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
