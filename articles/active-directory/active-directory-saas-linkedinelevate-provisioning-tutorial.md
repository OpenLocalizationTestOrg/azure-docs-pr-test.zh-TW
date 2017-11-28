---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Elevate | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooLinkedIn 提高權限。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 08201c078ece0054e75ec0c004840e5186e0e704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="bf2ca-103">教學課程︰設定自動使用者佈建的 LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="bf2ca-103">Tutorial: Configuring LinkedIn Elevate for Automatic User Provisioning</span></span>


<span data-ttu-id="bf2ca-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform LinkedIn 提高權限與 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooLinkedIn 提高權限中的步驟。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Elevate and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bf2ca-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf2ca-105">Prerequisites</span></span>

<span data-ttu-id="bf2ca-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="bf2ca-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="bf2ca-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="bf2ca-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="bf2ca-108">LinkedIn Elevate 租用戶</span><span class="sxs-lookup"><span data-stu-id="bf2ca-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="bf2ca-109">在 LinkedIn 提升系統管理員帳戶具有存取 toohello LinkedIn 帳戶中心</span><span class="sxs-lookup"><span data-stu-id="bf2ca-109">An administrator account in LinkedIn Elevate with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="bf2ca-110">Azure Active Directory 整合與使用 hello 提升 LinkedIn [SCIM](http://www.simplecloud.info/)通訊協定。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-110">Azure Active Directory integrates with LinkedIn Elevate using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-elevate"></a><span data-ttu-id="bf2ca-111">指派使用者 tooLinkedIn 提高權限</span><span class="sxs-lookup"><span data-stu-id="bf2ca-111">Assigning users tooLinkedIn Elevate</span></span>

<span data-ttu-id="bf2ca-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="bf2ca-113">在 hello 內容中的自動帳戶佈建使用者，將同步的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bf2ca-114">在之前設定，及啟用 hello 佈建服務，您必須 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooLinkedIn 提高權限。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Elevate.</span></span> <span data-ttu-id="bf2ca-115">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooLinkedIn 提高權限：</span><span class="sxs-lookup"><span data-stu-id="bf2ca-115">Once decided, you can assign these users tooLinkedIn Elevate by following hello instructions here:</span></span>

[<span data-ttu-id="bf2ca-116">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="bf2ca-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-elevate"></a><span data-ttu-id="bf2ca-117">指派使用者 tooLinkedIn 提高權限的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="bf2ca-117">Important tips for assigning users tooLinkedIn Elevate</span></span>

*   <span data-ttu-id="bf2ca-118">建議在單一 Azure AD 使用者被指派 tooLinkedIn 提高權限 tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Elevate tootest hello provisioning configuration.</span></span> <span data-ttu-id="bf2ca-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bf2ca-120">指派使用者 tooLinkedIn 提高權限時，您必須選取 hello**使用者**hello 分派對話方塊中的角色。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-120">When assigning a user tooLinkedIn Elevate, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="bf2ca-121">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-elevate"></a><span data-ttu-id="bf2ca-122">設定使用者佈建 tooLinkedIn 提高權限</span><span class="sxs-lookup"><span data-stu-id="bf2ca-122">Configuring user provisioning tooLinkedIn Elevate</span></span>

<span data-ttu-id="bf2ca-123">本節會引導您完成連接您 Azure AD tooLinkedIn 提高權限的 SCIM 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新並停用在 LinkedIn 提高的使用者和群組為基礎的指派的使用者帳戶Azure AD 中的指派。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-123">This section guides you through connecting your Azure AD tooLinkedIn Elevate's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="bf2ca-124">**提示：**您也可以選擇 tooenabled SAML 型單一登入的 LinkedIn 提升，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Elevate, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bf2ca-125">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-elevate-in-azure-ad"></a><span data-ttu-id="bf2ca-126">tooconfigure 自動使用者帳戶在 Azure AD 中佈建 tooLinkedIn 提高權限：</span><span class="sxs-lookup"><span data-stu-id="bf2ca-126">tooconfigure automatic user account provisioning tooLinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="bf2ca-127">hello 第一個步驟是 tooretrieve LinkedIn 的存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="bf2ca-128">如果您是企業版系統管理員，可以自我佈建存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="bf2ca-129">在您的帳戶中心移過**設定&gt;通用設定**和開啟 hello **SCIM 安裝**面板。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="bf2ca-130">如果直接而不是透過連結存取 hello 帳戶中心，您可以使用下列步驟的 hello 到達。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="bf2ca-131">登入 tooAccount 中心。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="bf2ca-132">選取 [系統管理員] > [系統管理員設定]**&gt;**。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="bf2ca-133">按一下**進階整合**hello 左提要欄位上。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="bf2ca-134">您已有向的 toohello 帳戶中心。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="bf2ca-135">按一下**+ 加入新的 SCIM 組態**遵循 hello 程序來填入每個欄位。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="bf2ca-136">若未啟用自動指派授權，表示只有使用者資料會同步處理。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Elevate 佈建](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="bf2ca-138">啟用 autolicense 指派時，您需要 toonote 應用程式執行個體及授權類型。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="bf2ca-139">第一個伴隨指派授權，先做為基礎，直到所有 hello 授權會都取用。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![LinkedIn Elevate 佈建](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="bf2ca-141">按一下 [產生權杖]。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-141">Click **Generate token**.</span></span> <span data-ttu-id="bf2ca-142">您應該會看到您的存取權杖顯示在 [hello] 下**存取權杖**欄位。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="bf2ca-143">離開 hello 頁面之前，儲存您的存取語彙基元 tooyour 剪貼簿或電腦。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="bf2ca-144">接下來，登入 toohello [Azure 入口網站](https://portal.azure.com)，並瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="bf2ca-145">如果您已經設定 LinkedIn 提高權限的單一登入，搜尋您的使用 hello 搜尋欄位 LinkedIn 提升執行個體。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using hello search field.</span></span> <span data-ttu-id="bf2ca-146">否則，請選取**新增**並搜尋**LinkedIn 提高**hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in hello application gallery.</span></span> <span data-ttu-id="bf2ca-147">從 hello 搜尋結果中，選取 [LinkedIn 提高權限，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-147">Select LinkedIn Elevate from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="bf2ca-148">選取執行個體 LinkedIn 提高權限，然後選取 hello**佈建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-148">Select your instance of LinkedIn Elevate, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="bf2ca-149">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![LinkedIn Elevate 佈建](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="bf2ca-151">填寫下列欄位底下的 hello**系統管理員認證**:</span><span class="sxs-lookup"><span data-stu-id="bf2ca-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="bf2ca-152">在 [hello**租用戶 URL**欄位中，輸入 https://api.linkedin.com。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="bf2ca-153">在 [hello**密碼語彙基元**欄位中輸入您在步驟 1 中產生的 hello 存取權杖，然後按一下**測試連接**。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="bf2ca-154">您應該會看到您的入口網站的 hello upperright 端成功的通知。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="bf2ca-155">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="bf2ca-156">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-156">Click **Save**.</span></span> 

14) <span data-ttu-id="bf2ca-157">在 [hello**屬性對應**區段中，檢閱將會同步處理從 Azure AD tooLinkedIn 提高權限的 hello 使用者和群組屬性。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Elevate.</span></span> <span data-ttu-id="bf2ca-158">請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 使用者帳戶和更新作業中 LinkedIn 提高權限的群組。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="bf2ca-159">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-159">Select hello Save button toocommit any changes.</span></span>

![LinkedIn Elevate 佈建](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="bf2ca-161">tooenable hello Azure AD 佈建服務 LinkedIn 提升，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="bf2ca-161">tooenable hello Azure AD provisioning service for LinkedIn Elevate, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="bf2ca-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-162">Click **Save**.</span></span> 

<span data-ttu-id="bf2ca-163">這會啟動 hello 初始同步處理的任何使用者和/或群組指派 tooLinkedIn hello 使用者和群組 > 一節中的提高權限。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Elevate in hello Users and Groups section.</span></span> <span data-ttu-id="bf2ca-164">請注意，hello 初始同步處理會花費較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="bf2ca-165">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 LinkedIn 提高應用程式上的執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="bf2ca-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Elevate app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bf2ca-166">其他資源</span><span class="sxs-lookup"><span data-stu-id="bf2ca-166">Additional Resources</span></span>

* [<span data-ttu-id="bf2ca-167">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="bf2ca-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="bf2ca-168">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bf2ca-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
