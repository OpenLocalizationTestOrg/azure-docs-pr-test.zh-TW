---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Cerner Central | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建使用者 tooa 名冊 Cerner 集中。"
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="25acf-103">教學課程︰設定自動使用者佈建的 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="25acf-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="25acf-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform Cerner 中央與 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooa 使用者名冊 Cerner 集中中的步驟。</span><span class="sxs-lookup"><span data-stu-id="25acf-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="25acf-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="25acf-105">Prerequisites</span></span>

<span data-ttu-id="25acf-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="25acf-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="25acf-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="25acf-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="25acf-108">Cerner Central 租用戶</span><span class="sxs-lookup"><span data-stu-id="25acf-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="25acf-109">Azure Active Directory 整合與使用 hello Cerner 中央[SCIM](http://www.simplecloud.info/)通訊協定。</span><span class="sxs-lookup"><span data-stu-id="25acf-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="25acf-110">指派使用者 tooCerner 中央</span><span class="sxs-lookup"><span data-stu-id="25acf-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="25acf-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="25acf-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="25acf-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="25acf-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="25acf-113">之前設定，及啟用 hello 佈建服務，您應該決定哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooCerner 中央。</span><span class="sxs-lookup"><span data-stu-id="25acf-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="25acf-114">一旦決定，您可以指派這些使用者 tooCerner 中央 hello 遵循指示：</span><span class="sxs-lookup"><span data-stu-id="25acf-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="25acf-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="25acf-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="25acf-116">指派使用者 tooCerner 中央的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="25acf-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="25acf-117">建議在單一 Azure AD 使用者被指派 tooCerner 中央 tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="25acf-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="25acf-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="25acf-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="25acf-119">一旦初始測試完成為單一使用者，Cerner 中央建議任何 Cerner 方案 （不只是 Cerner 中部） 佈建 toobe tooCerner 使用者名冊指派的使用者預期 tooaccess hello 整個清單。</span><span class="sxs-lookup"><span data-stu-id="25acf-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="25acf-120">其他 Cerner 解決方案會利用這份 hello 使用者名單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="25acf-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="25acf-121">指派使用者 tooCerner 管理中心時，您必須選取 hello**使用者**hello 分派對話方塊中的角色。</span><span class="sxs-lookup"><span data-stu-id="25acf-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="25acf-122">具有 hello 「 預設的存取 」 角色的使用者會排除佈建。</span><span class="sxs-lookup"><span data-stu-id="25acf-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="25acf-123">設定使用者佈建 tooCerner 中央</span><span class="sxs-lookup"><span data-stu-id="25acf-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="25acf-124">本節會引導您完成連接您 Azure AD tooCerner 中央使用者名單使用 Cerner 的 SCIM 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用 Cerner 管理中心中的帳戶以指派的使用者在 Azure AD 中使用者和群組指派。</span><span class="sxs-lookup"><span data-stu-id="25acf-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="25acf-125">您也可以選擇 SAML 型單一登入 tooenabled Cerner 中央，hello 指示提供在 [Azure 入口網站 (https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="25acf-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="25acf-126">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="25acf-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="25acf-127">如需詳細資訊，請參閱 hello [Cerner 中央單一登入教學課程](active-directory-saas-cernercentral-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="25acf-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="25acf-128">在 Azure AD 中佈建 tooCerner 中央 tooconfigure 自動使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="25acf-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="25acf-129">在順序 tooprovision 使用者帳戶 tooCerner 中央，您將需要 toorequest Cerner，從 Cerner 中央系統帳戶，並產生 tooconnect tooCerner SCIM 端點之後，可以使用 Azure AD 的 OAuth 承載權杖。</span><span class="sxs-lookup"><span data-stu-id="25acf-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="25acf-130">也建議 hello 整合，在之前部署 tooproduction Cerner 沙箱環境中執行。</span><span class="sxs-lookup"><span data-stu-id="25acf-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="25acf-131">hello 第一個步驟是管理 hello Cerner tooensure hello 人員，以及 Azure AD 整合擁有 CernerCare 帳戶，也就是必要的 tooaccess hello 文件必要 toocomplete hello 指示。</span><span class="sxs-lookup"><span data-stu-id="25acf-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="25acf-132">如果有必要，請使用 hello Url toocreate CernerCare 帳戶下每個適用的環境中。</span><span class="sxs-lookup"><span data-stu-id="25acf-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="25acf-133">沙箱環境：https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="25acf-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="25acf-134">生產環境：https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="25acf-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="25acf-135">接下來，必須建立 Azure AD 的系統帳戶。</span><span class="sxs-lookup"><span data-stu-id="25acf-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="25acf-136">使用 hello toorequest 系統帳戶底下的指示您沙箱和實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="25acf-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="25acf-137">指示：https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="25acf-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="25acf-138">沙箱環境：https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="25acf-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="25acf-139">生產環境：https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="25acf-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="25acf-140">接下來，產生每個系統帳戶的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="25acf-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="25acf-141">toodo，後續 hello 依照下列指示。</span><span class="sxs-lookup"><span data-stu-id="25acf-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="25acf-142">指示：https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="25acf-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="25acf-143">沙箱環境：https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="25acf-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="25acf-144">生產環境：https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="25acf-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="25acf-145">最後，您需要 tooacquire 使用者名冊領域識別碼 Cerner toocomplete hello 組態這兩種 hello 沙箱和實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="25acf-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="25acf-146">如需詳細資訊 tooacquire，請參閱： https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM。</span><span class="sxs-lookup"><span data-stu-id="25acf-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="25acf-147">現在您可以設定 Azure AD tooprovision 使用者帳戶 tooCerner。</span><span class="sxs-lookup"><span data-stu-id="25acf-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="25acf-148">登入 toohello [Azure 入口網站](https://portal.azure.com)，並瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="25acf-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="25acf-149">如果您已經設定 Cerner 中央進行單一登入，搜尋您 Cerner 中央使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="25acf-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="25acf-150">否則，請選取**新增**並搜尋**Cerner 中央**hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="25acf-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="25acf-151">從 hello 搜尋結果中，選取 Cerner 中央，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="25acf-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="25acf-152">選取您的 Cerner 中央執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="25acf-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="25acf-153">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="25acf-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Cerner Central 佈建](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="25acf-155">填寫下列欄位底下的 hello**系統管理員認證**:</span><span class="sxs-lookup"><span data-stu-id="25acf-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="25acf-156">在 hello**租用戶 URL**欄位中，輸入 「 使用者-名冊-領域-識別碼 」 取代貴用戶取得步驟 #4 中的 hello 領域識別碼 hello 格式下面 URL。</span><span class="sxs-lookup"><span data-stu-id="25acf-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="25acf-157">沙箱：https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="25acf-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="25acf-158">生產：https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="25acf-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="25acf-159">在 hello**密碼語彙基元**欄位中輸入您在步驟 3 中產生 hello OAuth 承載權杖，然後按一下**測試連接**。</span><span class="sxs-lookup"><span data-stu-id="25acf-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="25acf-160">您應該會看到您的入口網站的 hello upperright 端成功的通知。</span><span class="sxs-lookup"><span data-stu-id="25acf-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="25acf-161">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。</span><span class="sxs-lookup"><span data-stu-id="25acf-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="25acf-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="25acf-162">Click **Save**.</span></span> 

12. <span data-ttu-id="25acf-163">在 hello**屬性對應**區段中，檢閱 hello 使用者和群組屬性 toobe 從 Azure AD tooCerner 中央同步處理。</span><span class="sxs-lookup"><span data-stu-id="25acf-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="25acf-164">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 使用者帳戶和群組 Cerner 集中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="25acf-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="25acf-165">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="25acf-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="25acf-166">tooenable hello Azure AD 佈建服務 Cerner 中央，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="25acf-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="25acf-167">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="25acf-167">Click **Save**.</span></span> 

<span data-ttu-id="25acf-168">這會啟動 hello 初始同步處理的任何使用者和/或群組指派 tooCerner hello 使用者和群組 > 一節中的中央。</span><span class="sxs-lookup"><span data-stu-id="25acf-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="25acf-169">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello Azure AD 佈建服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="25acf-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="25acf-170">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Cerner 管理中心應用程式上的執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="25acf-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="25acf-171">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="25acf-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25acf-172">其他資源</span><span class="sxs-lookup"><span data-stu-id="25acf-172">Additional resources</span></span>

* [<span data-ttu-id="25acf-173">Cerner Central：使用 Azure AD 發佈身分識別資料</span><span class="sxs-lookup"><span data-stu-id="25acf-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="25acf-174">教學課程：設定 Cerner Central 搭配 Azure Active Directory 進行單一登入</span><span class="sxs-lookup"><span data-stu-id="25acf-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="25acf-175">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="25acf-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="25acf-176">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="25acf-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="25acf-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25acf-177">Next steps</span></span>
* <span data-ttu-id="25acf-178">[了解 tooreview 記錄的方式，並取得報告的佈建活動](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="25acf-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
