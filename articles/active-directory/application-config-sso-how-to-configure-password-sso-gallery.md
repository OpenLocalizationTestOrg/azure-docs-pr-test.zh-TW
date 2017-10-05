---
title: "如何為 Azure AD 資源庫應用程式設定密碼單一登入 | Microsoft Docs"
description: "當應用程式已列在 Azure AD 應用程式庫時，如何為它設定以密碼為基礎的安全單一登入"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="87e9d-103">如何為 Azure AD 資源庫應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="87e9d-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="87e9d-104">當您從 [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)新增應用程式時，您可以選擇希望使用者如何登入該應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="87e9d-105">您可以隨時在 [Azure 入口網站](https://portal.azure.com/)中選取企業應用程式的 [單一登入] 瀏覽項目，以設定這個選項。</span><span class="sxs-lookup"><span data-stu-id="87e9d-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="87e9d-106">可供您使用的其中一個單一登入方法是[以密碼為基礎的單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)選項。</span><span class="sxs-lookup"><span data-stu-id="87e9d-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="87e9d-107">這是開始將應用程式快速整合至 Azure AD 的絕佳方法，可讓您︰</span><span class="sxs-lookup"><span data-stu-id="87e9d-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="87e9d-108">針對已經與 Azure AD 整合的應用程式，安全地儲存和重播使用者名稱和密碼，以啟用**使用者的單一登入**</span><span class="sxs-lookup"><span data-stu-id="87e9d-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="87e9d-109">針對需要使用者名稱和密碼以外的更多欄位才能登入的應用程式，**支援需要多個登入欄位的應用程式**</span><span class="sxs-lookup"><span data-stu-id="87e9d-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="87e9d-110">針對使用者在[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)輸入認證時所看到的使用者名稱和密碼輸入欄位，**自訂標籤**</span><span class="sxs-lookup"><span data-stu-id="87e9d-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="87e9d-111">針對**使用者**在[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)手動輸入的任何現有應用程式帳戶，允許他們提供自己的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="87e9d-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="87e9d-112">允許**商務群組的成員**使用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)功能，指定要指派給使用者的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="87e9d-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="87e9d-113">允許**管理員**在[將使用者指派至應用程式](#assign-a-user-to-an-application-directly)時，使用更新憑證功能指定要指派給使用者的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="87e9d-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="87e9d-114">允許**管理員**在[將群組指派至應用程式](#assign-an-application-to-a-group-directly)時，使用更新憑證功能指定一群人使用的共用使用者名稱或密碼</span><span class="sxs-lookup"><span data-stu-id="87e9d-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="87e9d-115">以下說明如何為已在 [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)中的應用程式啟用[以密碼為基礎的單一登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)。</span><span class="sxs-lookup"><span data-stu-id="87e9d-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="87e9d-116">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="87e9d-116">Overview of steps required</span></span>
<span data-ttu-id="87e9d-117">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="87e9d-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="87e9d-118">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="87e9d-119">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="87e9d-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="87e9d-120">將應用程式指派至使用者或群組</span><span class="sxs-lookup"><span data-stu-id="87e9d-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="87e9d-121">將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="87e9d-122">將應用程式直接指派至群組</span><span class="sxs-lookup"><span data-stu-id="87e9d-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="87e9d-123">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="87e9d-124">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="87e9d-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="87e9d-125">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="87e9d-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="87e9d-126">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87e9d-127">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="87e9d-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87e9d-128">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87e9d-129">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="87e9d-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="87e9d-130">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="87e9d-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="87e9d-131">選取您要設為單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="87e9d-132">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="87e9d-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="87e9d-133">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="87e9d-134">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87e9d-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="87e9d-135">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="87e9d-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="87e9d-136">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="87e9d-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="87e9d-137">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="87e9d-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="87e9d-138">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87e9d-139">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="87e9d-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87e9d-140">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87e9d-141">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="87e9d-142">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87e9d-143">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="87e9d-144">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87e9d-145">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="87e9d-146">[將使用者指派至應用程式](#assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="87e9d-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="87e9d-147">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="87e9d-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="87e9d-148">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="87e9d-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="87e9d-149">將使用者直接指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-149">Assign a user to an application directly</span></span>

<span data-ttu-id="87e9d-150">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="87e9d-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="87e9d-151">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="87e9d-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87e9d-152">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87e9d-153">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="87e9d-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87e9d-154">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87e9d-155">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="87e9d-156">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87e9d-157">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="87e9d-158">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87e9d-159">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87e9d-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="87e9d-160">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="87e9d-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="87e9d-161">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="87e9d-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="87e9d-162">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="87e9d-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="87e9d-163">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="87e9d-164">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="87e9d-165">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="87e9d-166">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="87e9d-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="87e9d-167">按一下 [指派] 按鈕，將應用程式指派至選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="87e9d-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="87e9d-168">將應用程式直接指派至群組</span><span class="sxs-lookup"><span data-stu-id="87e9d-168">Assign an application to a group directly</span></span>

<span data-ttu-id="87e9d-169">若要直接將一或多個群組指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="87e9d-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="87e9d-170">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="87e9d-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87e9d-171">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87e9d-172">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="87e9d-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87e9d-173">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87e9d-174">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="87e9d-175">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87e9d-176">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="87e9d-177">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="87e9d-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87e9d-178">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87e9d-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="87e9d-179">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="87e9d-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="87e9d-180">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之群組的**完整群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="87e9d-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="87e9d-181">將滑鼠停留在清單中的**群組**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="87e9d-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="87e9d-182">按一下群組設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="87e9d-183">**選擇性︰**如果您想要**新增多個群組**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**完整群組名稱**，然後按一下核取方塊，將此群組新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="87e9d-184">當您完成選取群組時，按一下 [選取] 按鈕，將它們新增到要指派給應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="87e9d-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="87e9d-185">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取群組的角色。</span><span class="sxs-lookup"><span data-stu-id="87e9d-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="87e9d-186">按一下 [指派] 按鈕，將應用程式指派給選取的群組。</span><span class="sxs-lookup"><span data-stu-id="87e9d-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="87e9d-187">稍待片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e9d-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e9d-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87e9d-188">Next steps</span></span>
[<span data-ttu-id="87e9d-189">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="87e9d-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
