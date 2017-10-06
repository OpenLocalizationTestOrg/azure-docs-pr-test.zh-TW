---
title: "教學課程：Azure Active Directory 與 Concur 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Concur 之間。"
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
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="32274-103">教學課程：設定 Concur 的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="32274-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="32274-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform Concur 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooConcur 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="32274-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32274-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="32274-105">Prerequisites</span></span>

<span data-ttu-id="32274-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="32274-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="32274-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="32274-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="32274-108">已啟用 Concur 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32274-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="32274-109">具有小組系統管理員權限的 Concur 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="32274-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="32274-110">指派使用者 tooConcur</span><span class="sxs-lookup"><span data-stu-id="32274-110">Assigning users tooConcur</span></span>

<span data-ttu-id="32274-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="32274-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="32274-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="32274-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="32274-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Concur 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="32274-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="32274-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Concur 應用程式：</span><span class="sxs-lookup"><span data-stu-id="32274-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="32274-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="32274-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="32274-116">指派使用者 tooConcur 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="32274-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="32274-117">建議在單一 Azure AD 使用者被指派 tooConcur tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="32274-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="32274-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="32274-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="32274-119">指派使用者 tooConcur 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="32274-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="32274-120">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="32274-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="32274-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="32274-121">Enable user provisioning</span></span>

<span data-ttu-id="32274-122">本節會引導您完成連接您的 Azure AD tooConcur 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Concur 中指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="32274-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="32274-123">您也可以選擇 tooenabled SAML 型單一登入 concur，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="32274-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="32274-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="32274-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="32274-125">tooconfigure 使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="32274-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="32274-126">hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooConcur。</span><span class="sxs-lookup"><span data-stu-id="32274-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="32274-127">tooenable 應用程式在 hello 費用的服務，有 toobe 適當設定並使用 Web 服務系統管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="32274-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="32274-128">請勿將加入 hello WS 管理員角色 tooyour 現有系統管理員設定檔，您用於 t&e 管理功能。</span><span class="sxs-lookup"><span data-stu-id="32274-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="32274-129">Concur 顧問或 hello 用戶端系統管理員必須建立不同的 Web 服務系統管理員設定檔和 hello 用戶端系統管理員必須使用此設定檔的 hello Web 服務系統管理員的功能 （例如，啟用應用程式）。</span><span class="sxs-lookup"><span data-stu-id="32274-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="32274-130">這些設定檔必須有所區隔 hello 用戶端系統管理員的每日 t&e 系統管理員設定檔 （hello T & 電子管理員設定檔不應該有 hello T&e 角色指派）。</span><span class="sxs-lookup"><span data-stu-id="32274-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="32274-131">當您建立 hello 設定檔 toobe 用於啟用 hello 應用程式時，輸入 hello 使用者設定檔欄位 hello 用戶端系統管理員的名稱。</span><span class="sxs-lookup"><span data-stu-id="32274-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="32274-132">這會指派擁有權 toohello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="32274-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="32274-133">一旦建立一或多個設定檔，hello 用戶端必須登入這個設定檔 tooclick hello"*啟用*"合作夥伴應用程式內 hello Web 服務] 功能表上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="32274-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="32274-134">Hello 下列原因，此動作不應該與用於一般 t&e 管理 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="32274-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="32274-135">hello 用戶端有 toobe hello 按下的其中一個"*是*"上的應用程式啟用後會顯示 hello 對話方塊視窗。</span><span class="sxs-lookup"><span data-stu-id="32274-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="32274-136">此點選動作 hello 用戶端願意 hello 協力廠商應用程式 tooaccess 針對其資料，讓您或使用 hello 夥伴不能按一下 [是] 按鈕，可確認。</span><span class="sxs-lookup"><span data-stu-id="32274-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="32274-137">如果已啟用使用 hello T & 電子管理員設定檔的應用程式的用戶端系統管理員離開 hello 公司 （導致 hello 設定檔正在停用狀態），使用該設定檔啟用任何應用程式無法運作 hello 應用程式啟用與另一個使用中的 WS 管理員之前設定檔。</span><span class="sxs-lookup"><span data-stu-id="32274-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="32274-138">這就是為什麼您應該 toocreate 相異 WS 管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="32274-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="32274-139">如果系統管理員離開 hello 公司，hello 名稱相關聯的 toohello WS 管理員設定檔可以變更的 toohello 取代系統管理員，視需要而不會影響 hello 啟用應用程式因為該設定檔不需要停用狀態。</span><span class="sxs-lookup"><span data-stu-id="32274-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="32274-140">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="32274-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="32274-141">登入 tooyour **Concur**租用戶。</span><span class="sxs-lookup"><span data-stu-id="32274-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="32274-142">從 hello**管理**功能表上，選取**Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="32274-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="32274-143">![Concur 租用戶](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur 租用戶")</span><span class="sxs-lookup"><span data-stu-id="32274-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="32274-144">在左方、 從 hello hello **Web 服務**窗格中，選取**啟用夥伴應用程式**。</span><span class="sxs-lookup"><span data-stu-id="32274-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="32274-145">![啟用合作夥伴應用程式](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "啟用合作夥伴應用程式")</span><span class="sxs-lookup"><span data-stu-id="32274-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="32274-146">從 hello**啟用應用程式**清單中，選取**Azure Active Directory**，然後按一下 [**啟用**。</span><span class="sxs-lookup"><span data-stu-id="32274-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="32274-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="32274-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="32274-148">按一下**是**tooclose hello**確認動作**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="32274-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="32274-149">![確認動作](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "確認動作")</span><span class="sxs-lookup"><span data-stu-id="32274-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="32274-150">在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="32274-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="32274-151">如果您已經設定進行單一登入 Concur，搜尋您的 Concur 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="32274-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="32274-152">否則，請選取**新增**並搜尋**Concur** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="32274-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="32274-153">從 hello 搜尋結果中，選取 [Concur，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="32274-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="32274-154">選取您的 Concur，執行個體，然後選取 hello**佈建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="32274-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="32274-155">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="32274-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![佈建](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="32274-157">在 hello**系統管理員認證**區段中，輸入 hello**使用者名**和 hello**密碼**Concur 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="32274-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="32274-158">在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Concur 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="32274-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="32274-159">如果 hello 連線失敗，請確定您的 Concur 帳戶具有小組系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="32274-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="32274-160">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="32274-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="32274-161">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="32274-161">Click **Save.**</span></span>

14. <span data-ttu-id="32274-162">在 [hello 對應區段中，選取**tooConcur 同步處理 Azure Active Directory 使用者。**</span><span class="sxs-lookup"><span data-stu-id="32274-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="32274-163">在 [hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooConcur 同步。</span><span class="sxs-lookup"><span data-stu-id="32274-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="32274-164">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Concur 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="32274-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="32274-165">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="32274-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="32274-166">tooenable hello Azure AD 佈建服務 concur，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="32274-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="32274-167">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="32274-167">Click **Save.**</span></span>

<span data-ttu-id="32274-168">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="32274-168">You can now create a test account.</span></span> <span data-ttu-id="32274-169">等候總 tooverify hello 帳戶已經過同步處理 tooConcur too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="32274-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32274-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="32274-170">Additional resources</span></span>

* [<span data-ttu-id="32274-171">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="32274-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32274-172">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="32274-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="32274-173">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="32274-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

