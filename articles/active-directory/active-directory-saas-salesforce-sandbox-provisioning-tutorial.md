---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 沙箱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="a1b13-103">教學課程︰設定自動使用者佈建的 Salesforce 沙箱</span><span class="sxs-lookup"><span data-stu-id="a1b13-103">Tutorial: Configuring Salesforce Sandbox for Automatic User Provisioning</span></span>

<span data-ttu-id="a1b13-104">本教學課程的 hello 目標是 tooshow hello 您需要在 Salesforce 沙箱和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSalesforce 沙箱 tooperform 的步驟。</span><span class="sxs-lookup"><span data-stu-id="a1b13-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Salesforce Sandbox and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1b13-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a1b13-105">Prerequisites</span></span>

<span data-ttu-id="a1b13-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="a1b13-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="a1b13-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a1b13-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a1b13-108">您必須擁有 Salesforce Sandbox for Work 或 Salesforce Sandbox for Education 的有效租用戶。</span><span class="sxs-lookup"><span data-stu-id="a1b13-108">You must have a valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="a1b13-109">您可以使用免費試用帳戶來使用任何服務。</span><span class="sxs-lookup"><span data-stu-id="a1b13-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="a1b13-110">具有小組系統管理員權限的 Salesforce 沙箱使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1b13-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce-sandbox"></a><span data-ttu-id="a1b13-111">指派使用者 tooSalesforce 沙箱</span><span class="sxs-lookup"><span data-stu-id="a1b13-111">Assigning users tooSalesforce Sandbox</span></span>

<span data-ttu-id="a1b13-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="a1b13-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="a1b13-113">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a1b13-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="a1b13-114">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Salesforce 沙箱應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1b13-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce Sandbox app.</span></span> <span data-ttu-id="a1b13-115">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Salesforce 沙箱應用程式：</span><span class="sxs-lookup"><span data-stu-id="a1b13-115">Once decided, you can assign these users tooyour Salesforce Sandbox app by following hello instructions here:</span></span>

[<span data-ttu-id="a1b13-116">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="a1b13-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a><span data-ttu-id="a1b13-117">指派使用者 tooSalesforce 沙箱的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="a1b13-117">Important tips for assigning users tooSalesforce Sandbox</span></span>

* <span data-ttu-id="a1b13-118">建議在單一 tooSalesforce 沙箱 tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="a1b13-118">It is recommended that a single Azure AD user is assigned tooSalesforce Sandbox tootest hello provisioning configuration.</span></span> <span data-ttu-id="a1b13-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="a1b13-119">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="a1b13-120">指派使用者 tooSalesforce 沙箱時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="a1b13-120">When assigning a user tooSalesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="a1b13-121">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="a1b13-121">hello "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="a1b13-122">此應用程式會從 Salesforce 沙箱的佈建程序，將使用者指派時，哪個 hello 客戶可能會想 tooselect hello 一部分匯入自訂的角色。</span><span class="sxs-lookup"><span data-stu-id="a1b13-122">This app imports custom roles from Salesforce Sandbox as part of hello provisioning process, which hello customer may want tooselect when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="a1b13-123">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="a1b13-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="a1b13-124">本節引導您連接您 Azure AD tooSalesforce 沙箱的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用指派的使用者帳戶，在 Salesforce 沙箱根據使用者和群組Azure AD 中的指派。</span><span class="sxs-lookup"><span data-stu-id="a1b13-124">This section guides you through connecting your Azure AD tooSalesforce Sandbox's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="a1b13-125">您也可以選擇 tooenabled SAML 型單一登入 Salesforce 沙箱，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a1b13-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce Sandbox, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a1b13-126">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="a1b13-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="a1b13-127">tooconfigure 自動帳戶佈建使用者：</span><span class="sxs-lookup"><span data-stu-id="a1b13-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="a1b13-128">hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooSalesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="a1b13-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

1. <span data-ttu-id="a1b13-129">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="a1b13-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a1b13-130">如果您已經設定進行單一登入 Salesforce 沙箱，搜尋您的 Salesforce 沙箱使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1b13-130">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using hello search field.</span></span> <span data-ttu-id="a1b13-131">否則，請選取**新增**並搜尋**Salesforce 沙箱**hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="a1b13-131">Otherwise, select **Add** and search for **Salesforce Sandbox** in hello application gallery.</span></span> <span data-ttu-id="a1b13-132">從 hello 搜尋結果中，選取 Salesforce 沙箱，並將它加入 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="a1b13-132">Select Salesforce Sandbox from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="a1b13-133">選取您的 Salesforce 沙箱的執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a1b13-133">Select your instance of Salesforce Sandbox, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="a1b13-134">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="a1b13-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
    <span data-ttu-id="a1b13-135">![佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="a1b13-135">![provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="a1b13-136">在 hello**系統管理員認證**區段中，提供下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1b13-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="a1b13-137">a.</span><span class="sxs-lookup"><span data-stu-id="a1b13-137">a.</span></span> <span data-ttu-id="a1b13-138">在 hello**系統管理員使用者名稱**文字方塊中，輸入的 Salesforce 帳戶名稱已 hello**系統管理員**在 Salesforce.com 被指派的設定檔。</span><span class="sxs-lookup"><span data-stu-id="a1b13-138">In hello **Admin User Name** textbox, type a Salesforce Sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="a1b13-139">b.</span><span class="sxs-lookup"><span data-stu-id="a1b13-139">b.</span></span> <span data-ttu-id="a1b13-140">在 hello**系統管理員密碼**文字方塊中，此帳戶類型 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="a1b13-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="a1b13-141">tooget Salesforce 沙箱安全性權杖中，開啟新索引標籤，並登入 hello 相同 Salesforce 沙箱管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1b13-141">tooget your Salesforce Sandbox security token, open a new tab and sign into hello same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="a1b13-142">Hello 右上角的 hello 頁面上，按一下您的名稱，然後**我的設定**。</span><span class="sxs-lookup"><span data-stu-id="a1b13-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="a1b13-143">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="a1b13-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="a1b13-144">在 hello 左側瀏覽窗格中，按一下 **個人**tooexpand hello 相關的區段，然後按一下**重設我的安全性 Token**。</span><span class="sxs-lookup"><span data-stu-id="a1b13-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="a1b13-145">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="a1b13-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="a1b13-146">在 [hello**重設我的安全性 Token**頁面上，按一下 hello**重設安全性 Token** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1b13-146">On hello **Reset My Security Token** page, click hello **Reset Security Token** button.</span></span>

    <span data-ttu-id="a1b13-147">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="a1b13-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="a1b13-148">請檢查與此系統管理員帳戶相關聯 hello 電子郵件收件匣。</span><span class="sxs-lookup"><span data-stu-id="a1b13-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="a1b13-149">從包含 hello 新的安全性權杖的 Salesforce Sandbox.com 尋找電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a1b13-149">Look for an email from Salesforce Sandbox.com that contains hello new security token.</span></span>
10. <span data-ttu-id="a1b13-150">複製 hello 語彙基元，請移 tooyour Azure AD 視窗中，並將它貼到 hello**通訊端語彙基元**欄位。</span><span class="sxs-lookup"><span data-stu-id="a1b13-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="a1b13-151">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Salesforce 沙箱應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1b13-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce Sandbox app.</span></span>

12. <span data-ttu-id="a1b13-152">在 hello**通知電子郵件**欄位中，輸入 hello 電子郵件地址的個人或群組應該收到佈建錯誤通知，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a1b13-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

13. <span data-ttu-id="a1b13-153">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a1b13-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="a1b13-154">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooSalesforce 沙箱。**</span><span class="sxs-lookup"><span data-stu-id="a1b13-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce Sandbox.**</span></span>

15. <span data-ttu-id="a1b13-155">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooSalesforce 沙箱同步。</span><span class="sxs-lookup"><span data-stu-id="a1b13-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce Sandbox.</span></span> <span data-ttu-id="a1b13-156">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Salesforce 沙箱進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="a1b13-156">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="a1b13-157">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="a1b13-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="a1b13-158">tooenable hello Azure AD 佈建服務的 Salesforce 沙箱，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="a1b13-158">tooenable hello Azure AD provisioning service for Salesforce Sandbox, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="a1b13-159">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a1b13-159">Click **Save.**</span></span>


<span data-ttu-id="a1b13-160">啟動 hello 初始同步處理的任何使用者和/或群組指派 tooSalesforce hello 使用者和群組 > 一節中的沙箱。</span><span class="sxs-lookup"><span data-stu-id="a1b13-160">It starts hello initial synchronization of any users and/or groups assigned tooSalesforce Sandbox in hello Users and Groups section.</span></span> <span data-ttu-id="a1b13-161">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="a1b13-161">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="a1b13-162">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Salesforce 沙箱應用程式上的執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="a1b13-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="a1b13-163">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="a1b13-163">You can now create a test account.</span></span> <span data-ttu-id="a1b13-164">等候總 tooverify hello 帳戶已經過同步處理 toosalesforce too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a1b13-164">Wait for up too20 minutes tooverify that hello account has been synchronized toosalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1b13-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="a1b13-165">Additional resources</span></span>

* [<span data-ttu-id="a1b13-166">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="a1b13-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1b13-167">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a1b13-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a1b13-168">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="a1b13-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforcesandbox-tutorial.md)