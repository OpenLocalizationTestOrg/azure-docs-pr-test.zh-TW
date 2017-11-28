---
title: "教學課程：Azure Active Directory 與 Box 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與方塊之間。"
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
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="0d0c0-103">教學課程︰設定自動使用者佈建的 Box</span><span class="sxs-lookup"><span data-stu-id="0d0c0-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="0d0c0-104">本教學課程的 hello 目標是在您需要在方塊和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooBox tooperform tooshow hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-104">hello objective of this tutorial is tooshow hello steps you need tooperform in Box and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooBox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d0c0-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d0c0-105">Prerequisites</span></span>

<span data-ttu-id="0d0c0-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="0d0c0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0d0c0-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0d0c0-108">已啟用 Box 單一登入功能的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="0d0c0-109">具有小組系統管理員權限的 Box 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-toobox"></a><span data-ttu-id="0d0c0-110">指派使用者 tooBox</span><span class="sxs-lookup"><span data-stu-id="0d0c0-110">Assigning users tooBox</span></span> 

<span data-ttu-id="0d0c0-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0d0c0-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0d0c0-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Box 應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Box app.</span></span> <span data-ttu-id="0d0c0-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Box 應用程式：</span><span class="sxs-lookup"><span data-stu-id="0d0c0-114">Once decided, you can assign these users tooyour Box app by following hello instructions here:</span></span>

[<span data-ttu-id="0d0c0-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="0d0c0-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="0d0c0-116">指派使用者和群組</span><span class="sxs-lookup"><span data-stu-id="0d0c0-116">Assign users and groups</span></span>
<span data-ttu-id="0d0c0-117">hello**方塊 > 使用者和群組**hello Azure 入口網站中的索引標籤可讓您的使用者和群組應該被授與存取 tooBox toospecify。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-117">hello **Box > Users and Groups** tab in hello Azure portal allows you toospecify which users and groups should be granted access tooBox.</span></span> <span data-ttu-id="0d0c0-118">使用者或群組的指派會導致下列項目 toooccur hello:</span><span class="sxs-lookup"><span data-stu-id="0d0c0-118">Assignment of a user or group causes hello following things toooccur:</span></span>

* <span data-ttu-id="0d0c0-119">Azure AD 可允許 hello 指派使用者 （無論是直接指派或群組成員資格） tooauthenticate tooBox。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-119">Azure AD permits hello assigned user (either by direct assignment or group membership) tooauthenticate tooBox.</span></span> <span data-ttu-id="0d0c0-120">如果未指派使用者，Azure AD 不允許它們 toosign tooBox 中，並在 hello Azure AD 登入頁面上會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-120">If a user is not assigned, then Azure AD does not permit them toosign in tooBox and returns an error on hello Azure AD sign-in page.</span></span>
* <span data-ttu-id="0d0c0-121">方塊的應用程式磚加入 toohello 使用者[應用程式啟動器](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-121">An app tile for Box is added toohello user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="0d0c0-122">如果已啟用自動佈建，然後 hello 指派使用者和/或群組加入 toohello 佈建佇列 toobe 自動佈建。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-122">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
  
  * <span data-ttu-id="0d0c0-123">如果只有使用者物件已設定的 toobe 佈建，然後在 hello 佈建佇列中，位於所有直接指派的使用者和任何指派的群組成員的所有使用者會都放在 hello 佈建佇列。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-123">If only user objects were configured toobe provisioned, then all directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
  * <span data-ttu-id="0d0c0-124">如果已設定的 toobe 佈建群組物件，然後所有指派的群組物件是佈建的 tooBox 和群組成員的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-124">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="0d0c0-125">hello 群組和使用者成員資格會保留在時寫入 tooBox。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-125">hello group and user memberships are preserved upon being written tooBox.</span></span>

<span data-ttu-id="0d0c0-126">您可以使用 hello**屬性 > 單一登入**索引標籤上的使用者屬性 （或宣告） 會呈現在 SAML 為基礎的驗證和 hello tooBox tooconfigure**屬性 > 佈建**從 Azure AD tooBox 使用者和群組屬性流程佈建作業期間如何 tooconfigure 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-126">You can use hello **Attributes > Single Sign-On** tab tooconfigure which user attributes (or claims) are presented tooBox during SAML-based authentication, and hello **Attributes > Provisioning** tab tooconfigure how user and group attributes flow from Azure AD tooBox during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-toobox"></a><span data-ttu-id="0d0c0-127">指派使用者 tooBox 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="0d0c0-127">Important tips for assigning users tooBox</span></span> 

*   <span data-ttu-id="0d0c0-128">建議單一 Azure AD 使用者指派 tooBox tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-128">It is recommended that a single Azure AD user assigned tooBox tootest hello provisioning configuration.</span></span> <span data-ttu-id="0d0c0-129">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0d0c0-130">指派使用者 toobox 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-130">When assigning a user toobox, you must select a valid user role.</span></span> <span data-ttu-id="0d0c0-131">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-131">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0d0c0-132">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="0d0c0-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="0d0c0-133">本節引導連接您的 Azure AD tooBox 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用根據 Azure AD 中的使用者和群組指派 方塊中的指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-133">This section guides through connecting your Azure AD tooBox's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="0d0c0-134">如果已啟用自動佈建，然後 hello 指派使用者和/或群組加入 toohello 佈建佇列 toobe 自動佈建。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-134">If automatic provisioning is enabled, then hello assigned users and/or groups are added toohello provisioning queue toobe automatically provisioned.</span></span>
    
 * <span data-ttu-id="0d0c0-135">如果只有使用者物件設定的 toobe 佈建，然後直接指派的使用者會放入 hello 佈建的佇列，並置於 hello 佈建佇列的任何指派的群組成員的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-135">If only user objects are configured toobe provisioned, then directly assigned users are placed in hello provisioning queue, and all users that are members of any assigned groups are placed in hello provisioning queue.</span></span> 
    
 * <span data-ttu-id="0d0c0-136">如果已設定的 toobe 佈建群組物件，然後所有指派的群組物件是佈建的 tooBox 和群組成員的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-136">If group objects were configured toobe provisioned, then all assigned group objects are provisioned tooBox, and all users that are members of those groups.</span></span> <span data-ttu-id="0d0c0-137">hello 群組和使用者成員資格會保留在時寫入 tooBox。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-137">hello group and user memberships are preserved upon being written tooBox.</span></span>

> [!TIP] 
> <span data-ttu-id="0d0c0-138">您也可以選擇 SAML 型單一登入方塊中，遵循所提供的 hello 指示 tooenabled [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-138">You may also choose tooenabled SAML-based Single Sign-On for Box, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0d0c0-139">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="0d0c0-140">tooconfigure 自動帳戶佈建使用者：</span><span class="sxs-lookup"><span data-stu-id="0d0c0-140">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="0d0c0-141">hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooBox。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-141">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooBox.</span></span>

1. <span data-ttu-id="0d0c0-142">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-142">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="0d0c0-143">如果您已經進行單一登入設定 方塊中，搜尋方塊中，使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-143">If you have already configured Box for single sign-on, search for your instance of Box using hello search field.</span></span> <span data-ttu-id="0d0c0-144">否則，請選取**新增**並搜尋**方塊**hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-144">Otherwise, select **Add** and search for **Box** in hello application gallery.</span></span> <span data-ttu-id="0d0c0-145">從 hello 搜尋結果中，選取方塊，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-145">Select Box from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0d0c0-146">選取您的執行個體的方塊，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-146">Select your instance of Box, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0d0c0-147">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-147">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0d0c0-149">在 hello**系統管理員認證**區段中，按一下**授權**tooopen 新的瀏覽器視窗中的登入對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-149">Under hello **Admin Credentials** section, click **Authorize** tooopen a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="0d0c0-150">在 hello**登入 toogrant 存取 tooBox**頁面上，提供所需的 hello 認證，然後按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-150">On hello **Login toogrant access tooBox** page, provide hello required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="0d0c0-151">![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="0d0c0-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="0d0c0-152">按一下**授與存取 tooBox** tooauthorize 此作業並 tooreturn toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-152">Click **Grant access tooBox** tooauthorize this operation and tooreturn toohello Azure portal.</span></span> 
   
    <span data-ttu-id="0d0c0-153">![啟用自動使用者佈建](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="0d0c0-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="0d0c0-154">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Box 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-154">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Box app.</span></span> <span data-ttu-id="0d0c0-155">如果 hello 連線失敗，請確定您的 Box 帳戶具有小組系統管理員權限，然後再次嘗試 hello **「 授權 」**步驟一次。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-155">If hello connection fails, ensure your Box account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="0d0c0-156">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-156">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="0d0c0-157">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-157">Click **Save.**</span></span>

11. <span data-ttu-id="0d0c0-158">在 hello 對應區段中，選取**tooBox 同步處理 Azure Active Directory 使用者。**</span><span class="sxs-lookup"><span data-stu-id="0d0c0-158">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooBox.**</span></span>

12. <span data-ttu-id="0d0c0-159">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooBox 同步。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-159">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooBox.</span></span> <span data-ttu-id="0d0c0-160">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶 方塊中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-160">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Box for update operations.</span></span> <span data-ttu-id="0d0c0-161">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-161">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="0d0c0-162">tooenable hello Azure AD 佈建服務 方塊中，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="0d0c0-162">tooenable hello Azure AD provisioning service for Box, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="0d0c0-163">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-163">Click **Save.**</span></span>

<span data-ttu-id="0d0c0-164">啟動 hello 初始同步任何的處理使用者和/或群組指派 tooBox 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-164">That starts hello initial synchronization of any users and/or groups assigned tooBox in hello Users and Groups section.</span></span> <span data-ttu-id="0d0c0-165">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-165">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="0d0c0-166">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務應用程式 方塊上的所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-166">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Box app.</span></span>

<span data-ttu-id="0d0c0-167">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-167">You can now create a test account.</span></span> <span data-ttu-id="0d0c0-168">等候總 tooverify hello 帳戶已經過同步處理 toobox too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-168">Wait for up too20 minutes tooverify that hello account has been synchronized toobox.</span></span>

<span data-ttu-id="0d0c0-169">Box 租用戶中已同步處理的使用者會列在**受管理的使用者**在 hello**管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="0d0c0-169">In your Box tenant, synchronized users are listed under **Managed Users** in hello **Admin Console**.</span></span>

<span data-ttu-id="0d0c0-170">![整合狀態](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "整合狀態")</span><span class="sxs-lookup"><span data-stu-id="0d0c0-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0d0c0-171">其他資源</span><span class="sxs-lookup"><span data-stu-id="0d0c0-171">Additional resources</span></span>

* [<span data-ttu-id="0d0c0-172">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="0d0c0-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d0c0-173">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0d0c0-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0d0c0-174">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="0d0c0-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)