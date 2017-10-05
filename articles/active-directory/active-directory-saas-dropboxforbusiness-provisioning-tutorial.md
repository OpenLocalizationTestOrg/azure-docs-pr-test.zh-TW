---
title: "教學課程：Azure Active Directory 與 Dropbox for Business 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Dropbox for Business 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="889a5-103">教學課程︰設定自動使用者佈建的 Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="889a5-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="889a5-104">本教學課程旨在說明您需要在 Dropbox for Business 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Dropbox for Business。</span><span class="sxs-lookup"><span data-stu-id="889a5-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="889a5-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="889a5-105">Prerequisites</span></span>

<span data-ttu-id="889a5-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="889a5-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="889a5-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="889a5-108">已啟用 Dropbox for Business 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="889a5-109">具有小組系統管理員權限的 Dropbox for Business 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="889a5-110">將使用者指派至 Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="889a5-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="889a5-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="889a5-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="889a5-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="889a5-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="889a5-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Dropbox for Business 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="889a5-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="889a5-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Dropbox for Business 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="889a5-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="889a5-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="889a5-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="889a5-116">將使用者指派給 Dropbox for Business 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="889a5-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="889a5-117">建議將單一 Azure AD 使用者指派給 Dropbox for Business，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="889a5-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="889a5-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="889a5-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="889a5-119">將使用者指派給 Dropbox for Business 時，必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="889a5-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="889a5-120">「預設存取」角色不適用於佈建..</span><span class="sxs-lookup"><span data-stu-id="889a5-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="889a5-121">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="889a5-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="889a5-122">本節會引導您將 Azure AD 連線至 Dropbox for Business 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Dropbox for Business 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="889a5-123">您也可以選擇啟用 Dropbox for Business 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="889a5-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="889a5-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="889a5-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="889a5-125">若要設定自動使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="889a5-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="889a5-126">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="889a5-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="889a5-127">如果您已經設定單一登入的 Dropbox for Business，請使用 [搜尋] 欄位搜尋您的 Dropbox for Business 執行個體。</span><span class="sxs-lookup"><span data-stu-id="889a5-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="889a5-128">否則，請選取 [新增]，並在應用程式庫中搜尋 [Dropbox for Business]。</span><span class="sxs-lookup"><span data-stu-id="889a5-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="889a5-129">從搜尋結果中選取 Dropbox for Business，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="889a5-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="889a5-130">選取您的 Dropbox for Business 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="889a5-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="889a5-131">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="889a5-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="889a5-133">在 [系統管理員認證] 區段下，按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="889a5-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="889a5-134">會在新的瀏覽器視窗中開啟 Dropbox for Business 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="889a5-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="889a5-135">在 [登入 Dropbox 來與 Azure AD 連結]  對話方塊上，登入您的 Dropbox for Business 租用戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="889a5-136">![使用者佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="889a5-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="889a5-137">確認您需要授與 Azure Active Directory 權限來變更您的 Dropbox for Business 租用戶。</span><span class="sxs-lookup"><span data-stu-id="889a5-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="889a5-138">按一下 [允許]。</span><span class="sxs-lookup"><span data-stu-id="889a5-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="889a5-139">![使用者佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="889a5-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="889a5-140">在 Azure 入口網站中，按一下 [測試連線]以確保 Azure AD 可以連線到您的 Dropbox for Business 應用程式。</span><span class="sxs-lookup"><span data-stu-id="889a5-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="889a5-141">如果連線失敗，請確定您的 Dropbox for Business 帳戶具有小組系統管理員權限，並再試一次**「授權」**步驟。</span><span class="sxs-lookup"><span data-stu-id="889a5-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="889a5-142">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="889a5-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="889a5-143">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="889a5-143">Click **Save.**</span></span>

11. <span data-ttu-id="889a5-144">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Dropbox for Business]。</span><span class="sxs-lookup"><span data-stu-id="889a5-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="889a5-145">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Dropbox for Business 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="889a5-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="889a5-146">選取為 [比對] 屬性的屬性會用來比對 Dropbox for Business 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="889a5-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="889a5-147">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="889a5-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="889a5-148">若要啟用 Dropbox for Business 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="889a5-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="889a5-149">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="889a5-149">Click **Save.**</span></span>

<span data-ttu-id="889a5-150">這會啟動在 [使用者和群組] 區段中指派給 Dropbox for Business 的任何使用者和/或群組之首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="889a5-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="889a5-151">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="889a5-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="889a5-152">您可以使用 [同步處理詳細資料] 區段來監視進度，並連結到佈建活動報告，該報告描述您 Dropbox for Business 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="889a5-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="889a5-153">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="889a5-153">You can now create a test account.</span></span> <span data-ttu-id="889a5-154">請等候 20 分鐘以驗證帳戶已同步至 Dropbox for Business。</span><span class="sxs-lookup"><span data-stu-id="889a5-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="889a5-155">成功完成的使用者佈建週期會以相關狀態表示。</span><span class="sxs-lookup"><span data-stu-id="889a5-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="889a5-156">![指派使用者](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="889a5-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="889a5-157">其他資源</span><span class="sxs-lookup"><span data-stu-id="889a5-157">Additional resources</span></span>

* [<span data-ttu-id="889a5-158">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="889a5-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="889a5-159">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="889a5-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="889a5-160">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="889a5-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)