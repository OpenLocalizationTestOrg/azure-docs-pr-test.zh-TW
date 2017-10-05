---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Cerner Central | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 以自動佈建使用者至 Cerner Central 中的名冊。"
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
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="23dad-103">教學課程︰設定自動使用者佈建的 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="23dad-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="23dad-104">本教學課程旨在說明您需要在 Cerner Central 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Cerner Central 中的使用者名冊。</span><span class="sxs-lookup"><span data-stu-id="23dad-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="23dad-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="23dad-105">Prerequisites</span></span>

<span data-ttu-id="23dad-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="23dad-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="23dad-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="23dad-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="23dad-108">Cerner Central 租用戶</span><span class="sxs-lookup"><span data-stu-id="23dad-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="23dad-109">Azure Active Directory 使用 [SCIM](http://www.simplecloud.info/) 通訊協定與 Cerner Central 整合。</span><span class="sxs-lookup"><span data-stu-id="23dad-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="23dad-110">將使用者指派給 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="23dad-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="23dad-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="23dad-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="23dad-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="23dad-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="23dad-113">在設定並啟用佈建服務之前，您應該決定 Azure AD 中的哪些使用者及/或群組代表需要 Cerner Central 存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="23dad-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="23dad-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Cerner Central：</span><span class="sxs-lookup"><span data-stu-id="23dad-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="23dad-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="23dad-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="23dad-116">將使用者指派給 Cerner Central 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="23dad-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="23dad-117">建議將單一 Azure AD 使用者指派給 Cerner Central，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="23dad-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="23dad-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="23dad-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="23dad-119">對單一使用者完成初始測試後，Cerner Central 建議指派嘗試存取要佈建至 Cerner 使用者名冊之任何 Cerner 解決方案 (不只是 Cerner Central) 的完整使用者清單。</span><span class="sxs-lookup"><span data-stu-id="23dad-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="23dad-120">其他 Cerner 解決方案會利用這份使用者名冊中的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="23dad-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="23dad-121">將使用者指派給 Cerner Central 時，您必須在 [指派] 對話方塊中選取 [使用者] 角色。</span><span class="sxs-lookup"><span data-stu-id="23dad-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="23dad-122">具有「預設存取」角色的使用者會從佈建中排除。</span><span class="sxs-lookup"><span data-stu-id="23dad-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="23dad-123">設定使用者佈建至 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="23dad-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="23dad-124">本節會引導您使用 Cerner 的 SCIM 使用者帳戶佈建 API，將 Azure AD 連線至 Cerner Central 的使用者名冊，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Cerner Central 中建立、更新和停用已指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="23dad-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="23dad-125">您也可以選擇啟用 Cerner Central 的 SAML 型單一登入，並遵循 Azure 入口網站 (https://portal.azure.com) 中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="23dad-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="23dad-126">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="23dad-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="23dad-127">如需詳細資訊，請參閱 [Cerner Central 單一登入教學課程](active-directory-saas-cernercentral-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="23dad-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="23dad-128">若要在 Azure AD 中設定自動使用者帳戶佈建至 Cerner Central：</span><span class="sxs-lookup"><span data-stu-id="23dad-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="23dad-129">為了將使用者帳戶佈建至 Cerner Central，您必須從 Cerner 要求 Cerner Central 系統帳戶，並產生 Azure AD 可用來連線到 Cerner 之 SCIM 端點的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="23dad-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="23dad-130">此外，建議在 Cerner 沙箱環境中執行整合，再部署至生產環境。</span><span class="sxs-lookup"><span data-stu-id="23dad-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="23dad-131">第一個步驟是確定管理 Cerner 與 Azure AD 整合的人員擁有 CernerCare 帳戶，必須有此帳戶才能存取完成指示所需的文件。</span><span class="sxs-lookup"><span data-stu-id="23dad-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="23dad-132">如有必要，請使用下列 URL 在每個適用的環境中建立 CernerCare 帳戶。</span><span class="sxs-lookup"><span data-stu-id="23dad-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="23dad-133">沙箱環境：https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="23dad-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="23dad-134">生產環境：https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="23dad-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="23dad-135">接下來，必須建立 Azure AD 的系統帳戶。</span><span class="sxs-lookup"><span data-stu-id="23dad-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="23dad-136">您可以使用下列指示，要求沙箱和生產環境的系統帳戶。</span><span class="sxs-lookup"><span data-stu-id="23dad-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="23dad-137">指示：https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="23dad-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="23dad-138">沙箱環境：https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="23dad-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="23dad-139">生產環境：https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="23dad-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="23dad-140">接下來，產生每個系統帳戶的 OAuth 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="23dad-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="23dad-141">若要這樣做，請遵循下列指示。</span><span class="sxs-lookup"><span data-stu-id="23dad-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="23dad-142">指示：https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="23dad-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="23dad-143">沙箱環境：https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="23dad-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="23dad-144">生產環境：https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="23dad-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="23dad-145">最後，您需要針對 Cerner 中的沙箱和生產環境取得「使用者名冊領域識別碼」，以完成設定。</span><span class="sxs-lookup"><span data-stu-id="23dad-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="23dad-146">如需如何取得此項目的資訊，請參閱：https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM。</span><span class="sxs-lookup"><span data-stu-id="23dad-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="23dad-147">現在您可以設定 Azure AD 將使用者帳戶佈建至 Cerner。</span><span class="sxs-lookup"><span data-stu-id="23dad-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="23dad-148">登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="23dad-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="23dad-149">如果您已經設定 Cerner Central 單一登入，使用 [搜尋] 欄位搜尋您的 Cerner Central 執行個體。</span><span class="sxs-lookup"><span data-stu-id="23dad-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="23dad-150">否則，請選取 [新增]，並在應用程式庫中搜尋 [Cerner Central]。</span><span class="sxs-lookup"><span data-stu-id="23dad-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="23dad-151">從搜尋結果中選取 Cerner Central，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="23dad-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="23dad-152">選取您的 Cerner Central 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="23dad-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="23dad-153">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="23dad-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Cerner Central 佈建](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="23dad-155">填寫 [系統管理員認證] 底下的下列欄位：</span><span class="sxs-lookup"><span data-stu-id="23dad-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="23dad-156">在 [租用戶 URL] 欄位中，以下列格式輸入 URL，並將 "User-Roster-Realm-ID" 取代為您在步驟 4 中取得的領域識別碼。</span><span class="sxs-lookup"><span data-stu-id="23dad-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="23dad-157">沙箱：https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="23dad-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="23dad-158">生產：https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="23dad-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="23dad-159">在 [祕密權杖] 欄位中，輸入您在步驟 3 中產生的 OAuth 持有人權杖，然後按一下 [測試連接]。</span><span class="sxs-lookup"><span data-stu-id="23dad-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="23dad-160">您應該會在入口網站的右上方看到成功通知。</span><span class="sxs-lookup"><span data-stu-id="23dad-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="23dad-161">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。</span><span class="sxs-lookup"><span data-stu-id="23dad-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="23dad-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="23dad-162">Click **Save**.</span></span> 

12. <span data-ttu-id="23dad-163">在 [屬性對應] 區段中，檢閱將從 Azure AD 同步處理至 Cerner Central 的使用者和群組屬性。</span><span class="sxs-lookup"><span data-stu-id="23dad-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="23dad-164">選取為 [比對] 屬性的屬性會用來比對 Cerner Central 中的使用者帳戶和群組以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="23dad-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="23dad-165">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="23dad-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="23dad-166">若要啟用 Cerner Central 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="23dad-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="23dad-167">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="23dad-167">Click **Save**.</span></span> 

<span data-ttu-id="23dad-168">這會啟動在 [使用者和群組] 區段中指派給 Cerner Central 的任何使用者和/或群組之首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="23dad-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="23dad-169">首次同步處理會比後續的同步處理花費較多時間執行，只要 Azure AD 佈建服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="23dad-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="23dad-170">您可以使用 [同步處理詳細資料] 區段來監視進度，並連結到佈建活動報表，該報表描述您 Cerner Central 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="23dad-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="23dad-171">如需如何讀取 Azure AD 佈建記錄的詳細資訊，請參閱[關於使用者帳戶自動佈建的報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="23dad-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23dad-172">其他資源</span><span class="sxs-lookup"><span data-stu-id="23dad-172">Additional resources</span></span>

* [<span data-ttu-id="23dad-173">Cerner Central：使用 Azure AD 發佈身分識別資料</span><span class="sxs-lookup"><span data-stu-id="23dad-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="23dad-174">教學課程：設定 Cerner Central 搭配 Azure Active Directory 進行單一登入</span><span class="sxs-lookup"><span data-stu-id="23dad-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="23dad-175">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="23dad-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="23dad-176">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="23dad-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="23dad-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23dad-177">Next steps</span></span>
* <span data-ttu-id="23dad-178">[了解如何針對佈建活動檢閱記錄和取得報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="23dad-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
