---
title: "教學課程：Azure Active Directory 與 Box 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Box 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="9dfdb-103">教學課程︰設定自動使用者佈建的 Box</span><span class="sxs-lookup"><span data-stu-id="9dfdb-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="9dfdb-104">本教學課程旨在說明您需要在 Box 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dfdb-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="9dfdb-105">Prerequisites</span></span>

<span data-ttu-id="9dfdb-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="9dfdb-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9dfdb-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9dfdb-108">已啟用 Box 單一登入功能的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="9dfdb-109">具有小組系統管理員權限的 Box 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="9dfdb-110">將使用者指派給 Box</span><span class="sxs-lookup"><span data-stu-id="9dfdb-110">Assigning users to Box</span></span> 

<span data-ttu-id="9dfdb-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9dfdb-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9dfdb-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Box 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="9dfdb-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Box 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9dfdb-114">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="9dfdb-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="9dfdb-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="9dfdb-116">指派使用者和群組</span><span class="sxs-lookup"><span data-stu-id="9dfdb-116">Assign users and groups</span></span>
<span data-ttu-id="9dfdb-117">Azure 入口網站的 [Box] > [使用者和群組] 索引標籤可讓您指定應該授與哪些使用者和群組 Box 的存取權。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-117">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="9dfdb-118">指派使用者或群組會導致下列事項發生︰</span><span class="sxs-lookup"><span data-stu-id="9dfdb-118">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="9dfdb-119">Azure AD 允許指派的使用者 (直接指派或群組成員資格) 驗證 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-119">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="9dfdb-120">如果使用者未經指派，則 Azure AD 不會允許他們登入 Box，並會在 Azure AD 登入分頁傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-120">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="9dfdb-121">Box 的應用程式圖格會加入使用者的 [應用程式啟動程式](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)中。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-121">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="9dfdb-122">如已啟用自動佈建，則指派的使用者及/或群組就會加入佈建佇列進行自動佈建。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-122">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="9dfdb-123">如果只設定要佈建使用者物件，則所有直接指派的使用者都會放在佈建佇列中，而任何指派群組成員的所有使用者也會放在佈建佇列中。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-123">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="9dfdb-124">如果設定要佈建的是群組物件，則所有指派的群組物件以及這些群組成員的所有使用者都會佈建到 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-124">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="9dfdb-125">群組和使用者成員資格都會保留寫入 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-125">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="9dfdb-126">您可以使用 [屬性] > [單一登入] 索引標籤來設定，在 SAML 驗證期間，要向 Box 呈現哪些使用者屬性 (或宣告)；使用 [屬性] > [佈建] 索引標籤來設定，在佈建作業期間，使用者及群組屬性如何從 Azure AD 流向 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-126">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="9dfdb-127">將使用者指派給 Box 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="9dfdb-127">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="9dfdb-128">建議將單一 Azure AD 使用者指派給 Box，以測試佈建的設定。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-128">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="9dfdb-129">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9dfdb-130">將使用者指派給 Box 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-130">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="9dfdb-131">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-131">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9dfdb-132">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="9dfdb-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="9dfdb-133">本節會引導您將 Azure AD 連線至 Box 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Box 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-133">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="9dfdb-134">如已啟用自動佈建，則指派的使用者及/或群組就會加入佈建佇列進行自動佈建。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-134">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="9dfdb-135">如果只設定要佈建使用者物件，則直接指派的使用者會放在佈建佇列中，而任何指派群組成員的所有使用者也會放在佈建佇列中。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-135">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="9dfdb-136">如果設定要佈建的是群組物件，則所有指派的群組物件以及這些群組成員的所有使用者都會佈建到 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-136">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="9dfdb-137">群組和使用者成員資格都會保留寫入 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-137">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="9dfdb-138">您也可以選擇啟用 Box 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-138">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9dfdb-139">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="9dfdb-140">若要設定自動使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="9dfdb-140">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="9dfdb-141">本節的目的是要說明如何對 Box 啟用 Active Directory 使用者帳戶的佈建。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-141">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="9dfdb-142">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-142">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9dfdb-143">如果您已經設定單一登入的 Box，使用 [搜尋] 欄位搜尋您的 Box 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-143">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="9dfdb-144">否則，請選取 [新增]，並在應用程式庫中搜尋 [Box]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-144">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="9dfdb-145">從搜尋結果中選取 Box，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-145">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9dfdb-146">選取您的 Box 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-146">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9dfdb-147">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-147">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9dfdb-149">在 [管理員認證] 區段底下，按一下 [授權] 以在新的瀏覽器視窗中開啟 Box 登入對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-149">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="9dfdb-150">在 [登入以授與 Box 存取權] 頁面上，提供必要的認證，然後按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-150">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="9dfdb-151">![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="9dfdb-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="9dfdb-152">按一下 [授與 Box 存取權]  ，以授權進行此作業並返回 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-152">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="9dfdb-153">![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="9dfdb-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="9dfdb-154">在 Azure 入口網站中，按一下 [測試連線] 以確保 Azure AD 可以連線到您的 Box 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-154">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="9dfdb-155">如果連線失敗，請確定您的 Box 帳戶具有小組系統管理員權限，並再試一次「授權」步驟。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-155">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="9dfdb-156">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-156">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="9dfdb-157">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-157">Click **Save.**</span></span>

11. <span data-ttu-id="9dfdb-158">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Box]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="9dfdb-159">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Box 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="9dfdb-160">選取為 [比對] 屬性的屬性會用來比對 Box 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-160">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="9dfdb-161">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-161">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="9dfdb-162">若要啟用 Box 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="9dfdb-162">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="9dfdb-163">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-163">Click **Save.**</span></span>

<span data-ttu-id="9dfdb-164">這會對 [使用者和群組] 區段中指派給 Box 的任何使用者和/或群組，啟動首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-164">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="9dfdb-165">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-165">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9dfdb-166">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，其會描述您 Box 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="9dfdb-167">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-167">You can now create a test account.</span></span> <span data-ttu-id="9dfdb-168">請等候 20 分鐘以確認帳戶已同步至 Box。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-168">Wait for up to 20 minutes to verify that the account has been synchronized to box.</span></span>

<span data-ttu-id="9dfdb-169">在 Box 租用戶中，已同步處理的使用者會列在 [管理主控台] 的 [管理使用者] 之下。</span><span class="sxs-lookup"><span data-stu-id="9dfdb-169">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="9dfdb-170">![整合狀態](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "整合狀態")</span><span class="sxs-lookup"><span data-stu-id="9dfdb-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9dfdb-171">其他資源</span><span class="sxs-lookup"><span data-stu-id="9dfdb-171">Additional resources</span></span>

* [<span data-ttu-id="9dfdb-172">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="9dfdb-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9dfdb-173">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9dfdb-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9dfdb-174">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="9dfdb-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)