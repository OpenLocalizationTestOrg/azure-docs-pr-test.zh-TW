---
title: "教學課程︰以 Azure Active Directory 設定 Samanage 來自動佈建使用者 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 將使用者帳戶自動佈建和取消佈建至 Samanage。"
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="c964a-103">教學課程︰設定 Samanage 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="c964a-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="c964a-104">本教學課程旨在說明您需要在 Samanage 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Samanage。</span><span class="sxs-lookup"><span data-stu-id="c964a-104">The objective of this tutorial is to show you the steps you need to perform in Samanage and Azure AD to automatically provision and de-provision user accounts from Azure AD to Samanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c964a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="c964a-105">Prerequisites</span></span>

<span data-ttu-id="c964a-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="c964a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="c964a-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="c964a-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="c964a-108">已啟用[專業方案](https://www.samanage.com/pricing/)或更好方案的 Samanage 租用戶</span><span class="sxs-lookup"><span data-stu-id="c964a-108">A Samanage tenant with the [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="c964a-109">Samanage 中具有管理員權限的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="c964a-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="c964a-110">Azure AD 佈建整合仰賴 [Samanage REST API](https://www.samanage.com/api/)，這在專業方案或更好方案中可供 Samanage 小組使用。</span><span class="sxs-lookup"><span data-stu-id="c964a-110">The Azure AD provisioning integration relies on the [Samanage REST API](https://www.samanage.com/api/), which is available to Samanage teams on the Professional plan or better.</span></span>

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="c964a-111">將使用者指派給 Samanage</span><span class="sxs-lookup"><span data-stu-id="c964a-111">Assigning users to Samanage</span></span>

<span data-ttu-id="c964a-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="c964a-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="c964a-113">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="c964a-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="c964a-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Samanage 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="c964a-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Samanage app.</span></span> <span data-ttu-id="c964a-115">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Samanage 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="c964a-115">Once decided, you can assign these users to your Samanage app by following the instructions here:</span></span>

[<span data-ttu-id="c964a-116">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="c964a-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="c964a-117">將使用者指派給 Samanage 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="c964a-117">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="c964a-118">建議將單一 Azure AD 使用者指派給 Samanage，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="c964a-118">It is recommended that a single Azure AD user is assigned to Samanage to test the provisioning configuration.</span></span> <span data-ttu-id="c964a-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="c964a-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="c964a-120">將使用者指派給 Samanage 時，您必須在 [指派] 對話方塊中選取 [使用者] 角色，或另一個有效的應用程式特有角色 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="c964a-120">When assigning a user to Samanage, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="c964a-121">[預設存取] 角色不適用於佈建，系統會略過這些使用者。</span><span class="sxs-lookup"><span data-stu-id="c964a-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="c964a-122">佈建服務是一項新增功能，可讀取 Samanage 中定義的任何自訂角色，並將它們匯入 Azure AD 中，以便在 [選取角色] 對話方塊中進行選取。</span><span class="sxs-lookup"><span data-stu-id="c964a-122">As an added feature, the provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="c964a-123">啟用佈建服務並完成一個同步處理週期之後，這些角色就會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c964a-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-samanage"></a><span data-ttu-id="c964a-124">設定將使用者佈建至 Samanage</span><span class="sxs-lookup"><span data-stu-id="c964a-124">Configuring user provisioning to Samanage</span></span> 

<span data-ttu-id="c964a-125">本節會引導您將 Azure AD 連線至 Samanage 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Samanage 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c964a-125">This section guides you through connecting your Azure AD to Samanage's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="c964a-126">您也可以選擇啟用 Samanage 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="c964a-126">You may also choose to enabled SAML-based Single Sign-On for Samanage, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c964a-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="c964a-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a><span data-ttu-id="c964a-128">在 Azure AD 中設定將使用者帳戶自動佈建至 Samanage：</span><span class="sxs-lookup"><span data-stu-id="c964a-128">Configure automatic user account provisioning to Samanage in Azure AD:</span></span>


1. <span data-ttu-id="c964a-129">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="c964a-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="c964a-130">如果您已將 Samanage 設定為單一登入，請使用 [搜尋] 欄位搜尋您的 Samanage 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c964a-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using the search field.</span></span> <span data-ttu-id="c964a-131">否則，請選取 [新增]，並在應用程式庫中搜尋 [Samanage]。</span><span class="sxs-lookup"><span data-stu-id="c964a-131">Otherwise, select **Add** and search for **Samanage** in the application gallery.</span></span> <span data-ttu-id="c964a-132">從搜尋結果中選取 Samanage，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="c964a-132">Select Samanage from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="c964a-133">選取您的 Samanage 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c964a-133">Select your instance of Samanage, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="c964a-134">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="c964a-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Samanage 佈建](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="c964a-136">在 [管理員認證] 區段下，輸入 Samanage 帳戶的 [管理員使用者名稱和管理員密碼]。</span><span class="sxs-lookup"><span data-stu-id="c964a-136">Under the **Admin Credentials** section, input the **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="c964a-137">在 Azure 入口網站中，按一下 [測試連線]，以確保 Azure AD 可以連線至您的 Samanage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c964a-137">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Samanage app.</span></span> <span data-ttu-id="c964a-138">如果連線失敗，請確定您的 Samanage 帳戶具有管理員權限，然後再試一次步驟 5。</span><span class="sxs-lookup"><span data-stu-id="c964a-138">If the connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="c964a-139">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選 [發生失敗時傳送電子郵件通知] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c964a-139">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="c964a-140">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c964a-140">Click **Save**.</span></span> 

9. <span data-ttu-id="c964a-141">在 [對應] 區段下，選取 [同步處理 Azure Active Directory 使用者至 Samanage]。</span><span class="sxs-lookup"><span data-stu-id="c964a-141">Under the Mappings section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

10. <span data-ttu-id="c964a-142">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Samanage 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="c964a-142">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Samanage.</span></span> <span data-ttu-id="c964a-143">選取為 [比對] 屬性的屬性會用來比對 Samanage 中的使用者帳戶，以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="c964a-143">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="c964a-144">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="c964a-144">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="c964a-145">若要對 Samanage 啟用 Azure AD 佈建服務，請在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="c964a-145">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="c964a-146">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c964a-146">Click **Save**.</span></span> 

<span data-ttu-id="c964a-147">此作業會對 [使用者和群組] 區段中指派給 Samanage 的任何使用者和/或群組，啟動首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="c964a-147">This operation starts the initial synchronization of any users and/or groups assigned to Samanage in the Users and Groups section.</span></span> <span data-ttu-id="c964a-148">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="c964a-148">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="c964a-149">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述佈建服務執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="c964a-149">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="c964a-150">如需如何讀取 Azure AD 佈建記錄的詳細資訊，請參閱[關於使用者帳戶自動佈建的報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="c964a-150">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c964a-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="c964a-151">Additional resources</span></span>

* [<span data-ttu-id="c964a-152">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="c964a-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="c964a-153">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c964a-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="c964a-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c964a-154">Next steps</span></span>

* [<span data-ttu-id="c964a-155">瞭解如何針對佈建活動檢閱記錄和取得報告</span><span class="sxs-lookup"><span data-stu-id="c964a-155">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
