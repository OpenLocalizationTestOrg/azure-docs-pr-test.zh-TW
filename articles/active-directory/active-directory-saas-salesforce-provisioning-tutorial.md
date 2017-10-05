---
title: "教學課程：Azure Active Directory 與 Salesforce 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Salesforce 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="f0278-103">教學課程︰設定自動使用者佈建的 Salesforce</span><span class="sxs-lookup"><span data-stu-id="f0278-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="f0278-104">本教學課程旨在說明您需要在 Salesforce 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="f0278-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0278-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0278-105">Prerequisites</span></span>

<span data-ttu-id="f0278-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="f0278-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f0278-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f0278-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f0278-108">您必須擁有 Salesforce for Work 或 Salesforce for Education 的有效租用戶。</span><span class="sxs-lookup"><span data-stu-id="f0278-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="f0278-109">您可以使用免費試用帳戶來使用任何服務。</span><span class="sxs-lookup"><span data-stu-id="f0278-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="f0278-110">具有小組系統管理員權限的 Salesforce 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0278-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="f0278-111">將使用者指派給 Salesforce</span><span class="sxs-lookup"><span data-stu-id="f0278-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="f0278-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="f0278-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f0278-113">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="f0278-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="f0278-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Salesforce 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0278-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="f0278-115">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Salesforce 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="f0278-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="f0278-116">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="f0278-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="f0278-117">將使用者指派給 Salesforce 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="f0278-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="f0278-118">建議將單一 Azure AD 使用者指派給 Salesforce，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="f0278-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="f0278-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="f0278-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="f0278-120">將使用者指派給 Salesforce 時，必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="f0278-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="f0278-121">「預設存取」角色不適用於佈建</span><span class="sxs-lookup"><span data-stu-id="f0278-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0278-122">此應用程式在佈建流程中，會從 Salesforce 匯入自訂角色，客戶在指派使用者時也可以選取該角色</span><span class="sxs-lookup"><span data-stu-id="f0278-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="f0278-123">啟用自動的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="f0278-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="f0278-124">本節會引導您將 Azure AD 連接至 Salesforce 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Salesforce 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0278-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="f0278-125">您也可以選擇啟用 Salesforce 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="f0278-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f0278-126">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="f0278-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="f0278-127">若要設定自動使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="f0278-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="f0278-128">本節的目的是要說明如何對 Salesforce 啟用 Active Directory 使用者帳戶的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="f0278-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="f0278-129">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="f0278-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="f0278-130">如果您已經設定單一登入的 Salesforce，請使用 [搜尋] 欄位搜尋您的 Salesforce 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f0278-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="f0278-131">否則，請選取 [新增]，並在應用程式庫中搜尋 [Salesforce]。</span><span class="sxs-lookup"><span data-stu-id="f0278-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="f0278-132">從搜尋結果中選取 Salesforce，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f0278-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="f0278-133">選取您的 Salesforce 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0278-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="f0278-134">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="f0278-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="f0278-135">![佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="f0278-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="f0278-136">在 [管理員認證] 區段下，提供下列組態設定：</span><span class="sxs-lookup"><span data-stu-id="f0278-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="f0278-137">a.</span><span class="sxs-lookup"><span data-stu-id="f0278-137">a.</span></span> <span data-ttu-id="f0278-138">在 [管理員使用者名稱] 文字方塊中，輸入已在 Salesforce.com 中指派**系統管理員**設定檔的 Salesforce 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f0278-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="f0278-139">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0278-139">b.</span></span> <span data-ttu-id="f0278-140">在 [管理員密碼] 文字方塊中，輸入這個帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="f0278-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="f0278-141">若要取得您的 Salesforce 安全性權杖，請開啟新索引標籤並登入相同的 Salesforce 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0278-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="f0278-142">在頁面右上角，按一下您的名稱，然後按一下 [我的設定]。</span><span class="sxs-lookup"><span data-stu-id="f0278-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="f0278-143">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="f0278-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="f0278-144">在左方導覽窗格上，按一下 [個人] 展開相關的區段，然後按一下 [重設我的安全性權杖]。</span><span class="sxs-lookup"><span data-stu-id="f0278-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="f0278-145">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="f0278-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="f0278-146">在 [重設我的安全性權杖] 頁面上，按一下 [重設安全性權杖] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0278-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="f0278-147">![啟用自動使用者佈建](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "啟用自動使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="f0278-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="f0278-148">檢查與此系統管理員帳戶相關聯的電子郵件收件匣。</span><span class="sxs-lookup"><span data-stu-id="f0278-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="f0278-149">尋找來自 Salesforce.com，包含新安全性權杖的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f0278-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="f0278-150">複製權杖，移至您的 Azure AD 視窗，然後將它貼到 [通訊端權杖] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f0278-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="f0278-151">在 Azure 入口網站中，按一下 [測試連接]，以確保 Azure AD 可以連接到您的 Salesforce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0278-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="f0278-152">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f0278-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="f0278-153">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f0278-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="f0278-154">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Salesforce]。</span><span class="sxs-lookup"><span data-stu-id="f0278-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="f0278-155">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Salesforce 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="f0278-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="f0278-156">請注意，選取為 [比對] 屬性的屬性會用來比對 Salesforce 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="f0278-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="f0278-157">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="f0278-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="f0278-158">若要啟用 Salesforce 的 Azure AD 佈建服務，請在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="f0278-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="f0278-159">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f0278-159">Click **Save.**</span></span>

<span data-ttu-id="f0278-160">這會啟動在 [使用者和群組] 區段中指派給 Salesforce 的任何使用者和/或群組之首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="f0278-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="f0278-161">請注意，初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，這大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="f0278-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="f0278-162">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，其會描述您 Salesforce 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="f0278-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="f0278-163">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="f0278-163">You can now create a test account.</span></span> <span data-ttu-id="f0278-164">請等候 20 分鐘以確認帳戶已同步至 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="f0278-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0278-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="f0278-165">Additional resources</span></span>

* [<span data-ttu-id="f0278-166">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="f0278-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0278-167">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f0278-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f0278-168">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="f0278-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)