---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Slack | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 來自動佈建並取消佈建使用者帳戶至 Slack。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="bb27c-103">教學課程︰設定自動使用者佈建的 Slack</span><span class="sxs-lookup"><span data-stu-id="bb27c-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="bb27c-104">本教學課程旨在說明您需要在 Slack 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Slack。</span><span class="sxs-lookup"><span data-stu-id="bb27c-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb27c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="bb27c-105">Prerequisites</span></span>

<span data-ttu-id="bb27c-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="bb27c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bb27c-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="bb27c-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="bb27c-108">已啟用具有 [Plus 方案](https://aadsyncfabric.slack.com/pricing)或更高方案的 Slack</span><span class="sxs-lookup"><span data-stu-id="bb27c-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="bb27c-109">具有小組系統管理員權限的 Slack 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="bb27c-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="bb27c-110">注意︰Azure AD 佈建整合仰賴 [Slack SCIM API](https://api.slack.com/scim)，其可在 Plus 方案或更高方案中提供 Slack 小組。</span><span class="sxs-lookup"><span data-stu-id="bb27c-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="bb27c-111">將使用者指派給 Slack</span><span class="sxs-lookup"><span data-stu-id="bb27c-111">Assigning users to Slack</span></span>

<span data-ttu-id="bb27c-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="bb27c-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bb27c-113">在自動使用者帳戶佈建的內容中，只有已「指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="bb27c-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bb27c-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Slack 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb27c-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="bb27c-115">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Slack 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="bb27c-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="bb27c-116">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="bb27c-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="bb27c-117">將使用者指派給 Slack 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="bb27c-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="bb27c-118">建議將單一 Azure AD 使用者指派給 Slack，以測試佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="bb27c-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="bb27c-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="bb27c-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bb27c-120">將使用者指派給 Slack 時，您必須在指派對話方塊中選取**使用者**或「群組」角色。</span><span class="sxs-lookup"><span data-stu-id="bb27c-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="bb27c-121">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="bb27c-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="bb27c-122">設定使用者佈建至 Slack</span><span class="sxs-lookup"><span data-stu-id="bb27c-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="bb27c-123">本節會引導您將 Azure AD 連接至 Slack 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Slack 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb27c-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="bb27c-124">**提示︰**您也可以選擇啟用 Slack 的 SAML 型單一登入，遵循 (Azure 入口網站) 中提供的指示 [ https://portal.azure.com ] 。</span><span class="sxs-lookup"><span data-stu-id="bb27c-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="bb27c-125">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="bb27c-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="bb27c-126">若要在 Azure AD 中設定自動使用者帳戶佈建至 Slack︰</span><span class="sxs-lookup"><span data-stu-id="bb27c-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="bb27c-127">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="bb27c-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="bb27c-128">如果您已經設定單一登入的 Slack，使用 [搜尋] 欄位搜尋您的 Slack 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bb27c-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="bb27c-129">否則，請選取 [新增]，並在應用程式庫中搜尋 [Slack]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="bb27c-130">從搜尋結果中選取 Slack，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="bb27c-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="bb27c-131">選取您的 Slack 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bb27c-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="bb27c-132">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Slack 佈建](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="bb27c-134">在 [系統管理員認證] 區段下，按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="bb27c-135">這會在新的瀏覽器視窗中開啟 Slack 授權對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bb27c-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="bb27c-136">在新視窗中，使用您的小組系統管理帳戶登入 Slack。</span><span class="sxs-lookup"><span data-stu-id="bb27c-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="bb27c-137">在產生的授權對話方塊中，選取您想要啟用佈建的 Slack 小組，然後選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="bb27c-138">一旦完成後，回到 Azure 入口網站以完成佈建組態。</span><span class="sxs-lookup"><span data-stu-id="bb27c-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![授權對話方塊](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="bb27c-140">在 Azure 入口網站中，按一下 [測試連接]以確保 Azure AD 可以連接到您的 Slack 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb27c-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="bb27c-141">如果連接失敗，請確定您的 Slack 帳戶具有小組系統管理員權限，並再試一次「授權」步驟。</span><span class="sxs-lookup"><span data-stu-id="bb27c-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="bb27c-142">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bb27c-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="bb27c-143">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb27c-143">Click **Save**.</span></span> 

10) <span data-ttu-id="bb27c-144">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Slack]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="bb27c-145">在 [屬性對應] 區段中，檢閱將從 Azure AD 同步至 Slack 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="bb27c-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="bb27c-146">請注意，選取為 [比對] 屬性的屬性會用來比對 Slack 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="bb27c-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="bb27c-147">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="bb27c-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="bb27c-148">若要啟用 Slack 的 Azure AD 佈建服務，在 [設定]區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="bb27c-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="bb27c-149">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb27c-149">Click **Save**.</span></span> 

<span data-ttu-id="bb27c-150">這會啟動在 [使用者和群組] 區段中指派給 Slack 的任何使用者和/或群組之初始同步處理。</span><span class="sxs-lookup"><span data-stu-id="bb27c-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="bb27c-151">請注意，初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，這大約每 10 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="bb27c-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="bb27c-152">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，其會描述您 Slack 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="bb27c-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="bb27c-153">[選用] 設定群組物件佈建至 Slack</span><span class="sxs-lookup"><span data-stu-id="bb27c-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="bb27c-154">您可以選擇性地啟用從 Azure AD 佈建群組物件至 Slack。</span><span class="sxs-lookup"><span data-stu-id="bb27c-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="bb27c-155">這不同於「指派使用者群組」，因為除了其成員之外，實際群組物件會從 Azure AD 複寫至 Slack。</span><span class="sxs-lookup"><span data-stu-id="bb27c-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="bb27c-156">例如，如果您在 Azure AD 中有名為「我的群組」的群組，則會在 Slack 內建立名為「我的群組」的完全相同群組。</span><span class="sxs-lookup"><span data-stu-id="bb27c-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="bb27c-157">若要啟用群組物件的佈建︰</span><span class="sxs-lookup"><span data-stu-id="bb27c-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="bb27c-158">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 群組至 Slack]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="bb27c-159">在 [屬性對應] 刀鋒視窗中，將 [已啟用] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="bb27c-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="bb27c-160">在 [屬性對應] 區段中，檢閱將從 Azure AD 同步至 Slack 的群組屬性。</span><span class="sxs-lookup"><span data-stu-id="bb27c-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="bb27c-161">請注意，選取為 [比對] 屬性的屬性會用來比對 Slack 中的群組以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="bb27c-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="bb27c-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb27c-162">Click **Save**.</span></span>

<span data-ttu-id="bb27c-163">這會造成在 [使用者和群組] 區段中指派至 Slack 的任何群組物件完全從 Azure AD 同步至 Slack。</span><span class="sxs-lookup"><span data-stu-id="bb27c-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="bb27c-164">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，其會描述您 Slack 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="bb27c-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bb27c-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="bb27c-165">Additional Resources</span></span>

* [<span data-ttu-id="bb27c-166">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="bb27c-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="bb27c-167">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bb27c-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
