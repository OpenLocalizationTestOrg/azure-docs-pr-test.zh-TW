---
title: "教學課程：Azure Active Directory 與 Concur 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Concur 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="a36b1-103">教學課程：設定 Concur 的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="a36b1-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="a36b1-104">本教學課程旨在說明您需要在 Concur 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Concur。</span><span class="sxs-lookup"><span data-stu-id="a36b1-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a36b1-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a36b1-105">Prerequisites</span></span>

<span data-ttu-id="a36b1-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="a36b1-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a36b1-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a36b1-108">已啟用 Concur 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="a36b1-109">具有小組系統管理員權限的 Concur 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="a36b1-110">將使用者指派給 Concur</span><span class="sxs-lookup"><span data-stu-id="a36b1-110">Assigning users to Concur</span></span>

<span data-ttu-id="a36b1-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="a36b1-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a36b1-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="a36b1-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="a36b1-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Concur 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="a36b1-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="a36b1-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Concur 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="a36b1-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="a36b1-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="a36b1-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="a36b1-116">將使用者指派給 Concur 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="a36b1-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="a36b1-117">建議將單一 Azure AD 使用者指派給 Concur，以測試佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="a36b1-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="a36b1-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="a36b1-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a36b1-119">將使用者指派給 Concur 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="a36b1-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="a36b1-120">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="a36b1-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a36b1-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="a36b1-121">Enable user provisioning</span></span>

<span data-ttu-id="a36b1-122">本節會引導您將 Azure AD 連接至 Concur 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Concur 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="a36b1-123">您也可以選擇啟用 Concur 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="a36b1-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a36b1-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="a36b1-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="a36b1-125">若要設定使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="a36b1-125">To configure user account provisioning:</span></span>

<span data-ttu-id="a36b1-126">本節的目的是要說明如何對 Concur 啟用 Active Directory 使用者帳戶的佈建。</span><span class="sxs-lookup"><span data-stu-id="a36b1-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="a36b1-127">若要啟用 Expense Service 中的應用程式，您必須適當地設定及使用 Web 服務系統管理員設定檔，</span><span class="sxs-lookup"><span data-stu-id="a36b1-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="a36b1-128">而不要將 WS 系統管理員角色加入用於 T&E 系統管理功能的現有系統管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a36b1-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="a36b1-129">Concur 顧問或用戶端系統管理員必須建立不同的 Web 服務系統管理員設定檔，而且用戶端系統管理員必須使用這個設定檔來執行 Web 服務系統管理員功能 (例如，啟用應用程式)。</span><span class="sxs-lookup"><span data-stu-id="a36b1-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="a36b1-130">這些設定檔必須與用戶端系統管理員的每日 T&E 系統管理員設定檔分開保存 (T&E 系統管理員設定檔不應該指派 WS 系統管理員角色)。</span><span class="sxs-lookup"><span data-stu-id="a36b1-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="a36b1-131">當您建立要用於啟用應用程式的設定檔時，請在使用者設定檔欄位中，輸入用戶端系統管理員的名稱。</span><span class="sxs-lookup"><span data-stu-id="a36b1-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="a36b1-132">這會對設定檔指派擁有權。</span><span class="sxs-lookup"><span data-stu-id="a36b1-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="a36b1-133">在建立一或多個設定檔之後，用戶端必須使用這個設定檔登入，並針對合作夥伴應用程式，按一下 [Web 服務] 功能表中的 [啟用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36b1-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="a36b1-134">基於下列原因，不應該透過用於一般 T&E 系統管理的設定檔完成這項動作。</span><span class="sxs-lookup"><span data-stu-id="a36b1-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="a36b1-135">用戶端必須在啟用應用程式之後所顯示的對話視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="a36b1-136">這個點選動作可確認用戶端是否願意讓合作夥伴應用程式存取其資料，因此您或合作夥伴無法按 [是] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a36b1-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="a36b1-137">如果使用 T&E 系統管理員設定檔啟用應用程式的用戶端系統管理員已離職 (導致設定檔被停用)，在使用另一個現用 WS 系統管理員設定檔啟用應用程式之前，使用該設定檔啟用的所有應用程式都無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="a36b1-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="a36b1-138">因此，您必須建立不同的 WS 系統管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a36b1-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="a36b1-139">如果系統管理員離職，與 WS 系統管理員設定檔關聯的名稱可視需要變更為續任的系統管理員，由於不需要停用該設定檔，因此不會影響已啟用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36b1-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="a36b1-140">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a36b1-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a36b1-141">登入您的 **Concur** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="a36b1-142">從 [管理] 功能表中，選取 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="a36b1-143">![Concur 租用戶](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur 租用戶")</span><span class="sxs-lookup"><span data-stu-id="a36b1-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="a36b1-144">從左側的 [Web 服務] 窗格中，選取 [啟用合作夥伴應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="a36b1-145">![啟用合作夥伴應用程式](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "啟用合作夥伴應用程式")</span><span class="sxs-lookup"><span data-stu-id="a36b1-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="a36b1-146">從 [啟用應用程式] 清單中選取 [Azure Active Directory]，然後按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="a36b1-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a36b1-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="a36b1-148">按一下 [是] 關閉 [確認動作] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a36b1-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="a36b1-149">![確認動作](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "確認動作")</span><span class="sxs-lookup"><span data-stu-id="a36b1-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="a36b1-150">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="a36b1-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="a36b1-151">如果您已經設定單一登入的 Concur，使用 [搜尋] 欄位搜尋您的 Concur 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a36b1-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="a36b1-152">否則，請選取 [新增]，並在應用程式庫中搜尋 [Concur]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="a36b1-153">從搜尋結果中選取 Concur，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a36b1-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="a36b1-154">選取您的 Concur 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a36b1-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="a36b1-155">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![佈建](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="a36b1-157">在 [管理員認證] 區段下，輸入 Concur 系統管理員的**使用者名稱**和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a36b1-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="a36b1-158">在 Azure 入口網站中，按一下 [測試連接]以確保 Azure AD 可以連接到您的 Concur 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a36b1-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="a36b1-159">如果連接失敗，請確定您的 Concur 帳戶具有小組系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="a36b1-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="a36b1-160">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a36b1-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="a36b1-161">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-161">Click **Save.**</span></span>

14. <span data-ttu-id="a36b1-162">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Concur]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="a36b1-163">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Concur 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="a36b1-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="a36b1-164">選取為 [比對] 屬性的屬性會用來比對 Concur 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="a36b1-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="a36b1-165">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="a36b1-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="a36b1-166">若要啟用 Concur 的 Azure AD 佈建服務，在 [設定]區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="a36b1-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="a36b1-167">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a36b1-167">Click **Save.**</span></span>

<span data-ttu-id="a36b1-168">您現在可以建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="a36b1-168">You can now create a test account.</span></span> <span data-ttu-id="a36b1-169">請等候 20 分鐘以確認帳戶已同步至 Concur。</span><span class="sxs-lookup"><span data-stu-id="a36b1-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a36b1-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="a36b1-170">Additional resources</span></span>

* [<span data-ttu-id="a36b1-171">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="a36b1-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a36b1-172">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a36b1-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a36b1-173">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="a36b1-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

