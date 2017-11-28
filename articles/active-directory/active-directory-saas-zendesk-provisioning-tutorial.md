---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 ZenDesk | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 來自動佈建並取消佈建使用者帳戶至 ZenDesk。"
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
ms.openlocfilehash: 1a1414eefd20e6d7c025da08cfd5ae7c45daad33
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="a5a45-103">教學課程︰設定自動使用者佈建的 ZenDesk</span><span class="sxs-lookup"><span data-stu-id="a5a45-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="a5a45-104">本教學課程旨在說明您需要在 ZenDesk 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 ZenDesk。</span><span class="sxs-lookup"><span data-stu-id="a5a45-104">The objective of this tutorial is to show you the steps you need to perform in ZenDesk and Azure AD to automatically provision and de-provision user accounts from Azure AD to ZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a5a45-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5a45-105">Prerequisites</span></span>

<span data-ttu-id="a5a45-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="a5a45-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a5a45-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="a5a45-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a5a45-108">已啟用 [Enterprise 方案](https://www.zendesk.com/product/pricing/)或更好方案的 ZenDesk 租用戶</span><span class="sxs-lookup"><span data-stu-id="a5a45-108">A ZenDesk tenant with the [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="a5a45-109">ZenDesk 中具有系統管理員權限的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="a5a45-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a5a45-110">Azure AD 佈建整合仰賴 [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api)，其可供 ZenDesk 小組在 Essential 方案或更好方案上使用。</span><span class="sxs-lookup"><span data-stu-id="a5a45-110">The Azure AD provisioning integration relies on the [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available to ZenDesk teams on the Essential plan or better.</span></span>

## <a name="assigning-users-to-zendesk"></a><span data-ttu-id="a5a45-111">將使用者指派給 ZenDesk</span><span class="sxs-lookup"><span data-stu-id="a5a45-111">Assigning users to ZenDesk</span></span>

<span data-ttu-id="a5a45-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="a5a45-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a5a45-113">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="a5a45-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="a5a45-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 ZenDesk 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="a5a45-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ZenDesk app.</span></span> <span data-ttu-id="a5a45-115">一旦決定後，您可以依照此處的指示，將這些使用者指派給 ZenDesk 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="a5a45-115">Once decided, you can assign these users to your ZenDesk app by following the instructions here:</span></span>

[<span data-ttu-id="a5a45-116">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="a5a45-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-zendesk"></a><span data-ttu-id="a5a45-117">將使用者指派給 ZenDesk 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="a5a45-117">Important tips for assigning users to ZenDesk</span></span>

*   <span data-ttu-id="a5a45-118">建議將單一 Azure AD 使用者指派給 ZenDesk，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="a5a45-118">It is recommended that a single Azure AD user is assigned to ZenDesk to test the provisioning configuration.</span></span> <span data-ttu-id="a5a45-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="a5a45-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a5a45-120">將使用者指派給 ZenDesk 時，您必須在 [指派] 對話方塊中選取 [使用者] 角色，或另一個有效的應用程式特有角色 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="a5a45-120">When assigning a user to ZenDesk, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="a5a45-121">[預設存取] 角色不適用於佈建，系統會略過這些使用者。</span><span class="sxs-lookup"><span data-stu-id="a5a45-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a45-122">佈建服務是一項新增功能，可讀取 Zendesk 中定義的任何自訂角色，並將它們匯入 Azure AD 中，以便在 [選取角色] 對話方塊中進行選取。</span><span class="sxs-lookup"><span data-stu-id="a5a45-122">As an added feature, the provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="a5a45-123">啟用佈建服務並完成一個同步處理週期之後，這些角色就會顯示在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a5a45-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-zendesk"></a><span data-ttu-id="a5a45-124">設定使用者佈建至 ZenDesk</span><span class="sxs-lookup"><span data-stu-id="a5a45-124">Configuring user provisioning to ZenDesk</span></span> 

<span data-ttu-id="a5a45-125">本節會引導您將 Azure AD 連線至 ZenDesk 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 ZenDesk 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5a45-125">This section guides you through connecting your Azure AD to ZenDesk's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="a5a45-126">您也可以選擇啟用 ZenDesk 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="a5a45-126">You may also choose to enabled SAML-based Single Sign-On for ZenDesk, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a5a45-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="a5a45-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-zendesk-in-azure-ad"></a><span data-ttu-id="a5a45-128">在 Azure AD 中設定自動使用者帳戶佈建至 ZenDesk</span><span class="sxs-lookup"><span data-stu-id="a5a45-128">Configure automatic user account provisioning to ZenDesk in Azure AD</span></span>


1. <span data-ttu-id="a5a45-129">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="a5a45-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a5a45-130">如果您已經設定單一登入的 ZenDesk，使用 [搜尋] 欄位搜尋您的 ZenDesk 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a5a45-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using the search field.</span></span> <span data-ttu-id="a5a45-131">否則，請選取 [新增]，並在應用程式庫中搜尋 [ZenDesk]。</span><span class="sxs-lookup"><span data-stu-id="a5a45-131">Otherwise, select **Add** and search for **ZenDesk** in the application gallery.</span></span> <span data-ttu-id="a5a45-132">從搜尋結果中選取 ZenDesk，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a5a45-132">Select ZenDesk from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a5a45-133">選取您的 ZenDesk 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a5a45-133">Select your instance of ZenDesk, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a5a45-134">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="a5a45-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="a5a45-136">在 [系統管理員認證] 區段之下，輸入您的 ZenDesk 帳戶所產生的 [系統管理員使用者名稱、權杖金鑰和網域] \(您可以在自己的帳戶之下找到權杖：[系統管理員] > [API] > [設定])。</span><span class="sxs-lookup"><span data-stu-id="a5a45-136">Under the **Admin Credentials** section, input the **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find the token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="a5a45-138">在 Azure 入口網站中，按一下 [測試連線]以確保 Azure AD 可以連線到您的 ZenDesk 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5a45-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ZenDesk app.</span></span> <span data-ttu-id="a5a45-139">如果連線失敗，請確定您的 ZenDesk 帳戶具有系統管理員權限並再試一次步驟 5。</span><span class="sxs-lookup"><span data-stu-id="a5a45-139">If the connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="a5a45-140">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選 [發生失敗時傳送電子郵件通知] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a5a45-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="a5a45-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a5a45-141">Click **Save**.</span></span> 

9. <span data-ttu-id="a5a45-142">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 ZenDesk]。</span><span class="sxs-lookup"><span data-stu-id="a5a45-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to ZenDesk**.</span></span>

10. <span data-ttu-id="a5a45-143">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 ZenDesk 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a45-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ZenDesk.</span></span> <span data-ttu-id="a5a45-144">選取為 [比對] 屬性的屬性會用來比對 ZenDesk 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="a5a45-144">The attributes selected as **Matching** properties are used to match the user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="a5a45-145">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="a5a45-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a5a45-146">若要啟用 ZenDesk 的 Azure AD 佈建服務，在 [設定]區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="a5a45-146">To enable the Azure AD provisioning service for ZenDesk, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="a5a45-147">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a5a45-147">Click **Save**.</span></span> 

<span data-ttu-id="a5a45-148">此選項會啟動在 [使用者和群組] 區段中指派給 ZenDesk 的任何使用者和/或群組之首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="a5a45-148">This operation starts the initial synchronization of any users and/or groups assigned to ZenDesk in the Users and Groups section.</span></span> <span data-ttu-id="a5a45-149">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="a5a45-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a5a45-150">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述佈建服務執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="a5a45-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="a5a45-151">如需如何讀取 Azure AD 佈建記錄的詳細資訊，請參閱[關於使用者帳戶自動佈建的報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="a5a45-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a5a45-152">其他資源</span><span class="sxs-lookup"><span data-stu-id="a5a45-152">Additional resources</span></span>

* [<span data-ttu-id="a5a45-153">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="a5a45-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a5a45-154">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a5a45-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a5a45-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5a45-155">Next steps</span></span>

* [<span data-ttu-id="a5a45-156">瞭解如何針對佈建活動檢閱記錄和取得報告</span><span class="sxs-lookup"><span data-stu-id="a5a45-156">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
