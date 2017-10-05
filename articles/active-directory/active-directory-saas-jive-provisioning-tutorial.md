---
title: "教學課程：Azure Active Directory 與 Jive 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Jive 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="07eac-103">教學課程：設定 Jive 來佈建使用者</span><span class="sxs-lookup"><span data-stu-id="07eac-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="07eac-104">本教學課程旨在說明您需要在 Jive 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Jive。</span><span class="sxs-lookup"><span data-stu-id="07eac-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07eac-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="07eac-105">Prerequisites</span></span>

<span data-ttu-id="07eac-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="07eac-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="07eac-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="07eac-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="07eac-108">啟用 Jive 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07eac-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="07eac-109">Jive 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="07eac-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="07eac-110">將使用者指派給 Jive</span><span class="sxs-lookup"><span data-stu-id="07eac-110">Assigning users to Jive</span></span>

<span data-ttu-id="07eac-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="07eac-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="07eac-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="07eac-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="07eac-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Jive 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="07eac-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="07eac-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Jive 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="07eac-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="07eac-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="07eac-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="07eac-116">將使用者指派給 Jive 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="07eac-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="07eac-117">建議將單一 Azure AD 使用者指派給 Jive，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="07eac-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="07eac-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="07eac-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="07eac-119">將使用者指派給 Jive 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="07eac-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="07eac-120">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="07eac-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="07eac-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="07eac-121">Enable User Provisioning</span></span>

<span data-ttu-id="07eac-122">本節會引導您將 Azure AD 連線至 Jive 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Jive 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="07eac-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="07eac-123">您也可以選擇啟用 Jive 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="07eac-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="07eac-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="07eac-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="07eac-125">若要設定使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="07eac-125">To configure user account provisioning:</span></span>

<span data-ttu-id="07eac-126">本節的目的是要說明如何對 Jive 啟用 Active Directory 使用者帳戶的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="07eac-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="07eac-127">在此程序中，您必須提供從 Jive.com 要求所需的使用者安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="07eac-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="07eac-128">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="07eac-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="07eac-129">如果您已將 Jive 設定為單一登入，請使用 [搜尋] 欄位搜尋您的 Jive 執行個體。</span><span class="sxs-lookup"><span data-stu-id="07eac-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="07eac-130">否則，請選取 [新增]，並在應用程式庫中搜尋 [Jive]。</span><span class="sxs-lookup"><span data-stu-id="07eac-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="07eac-131">從搜尋結果中選取 Jive，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="07eac-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="07eac-132">選取您的 Jive 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="07eac-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="07eac-133">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="07eac-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="07eac-135">在 [管理員認證] 區段下，提供下列組態設定：</span><span class="sxs-lookup"><span data-stu-id="07eac-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="07eac-136">a.</span><span class="sxs-lookup"><span data-stu-id="07eac-136">a.</span></span> <span data-ttu-id="07eac-137">在 [Jive 管理員使用者名稱] 文字方塊中，輸入在 Jive.com 已指派 **System Administrator** 設定檔的 Jive 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="07eac-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="07eac-138">b.</span><span class="sxs-lookup"><span data-stu-id="07eac-138">b.</span></span> <span data-ttu-id="07eac-139">在 [Jive 管理員密碼]  文字方塊中，輸入這個帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="07eac-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="07eac-140">c.</span><span class="sxs-lookup"><span data-stu-id="07eac-140">c.</span></span> <span data-ttu-id="07eac-141">在 [Jive 租用戶 URL]  文字方塊中，輸入 Jive 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="07eac-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="07eac-142">Jive 租用戶 URL 是您的組織登入 Jive 所使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="07eac-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="07eac-143">一般來說，該 URL 的格式如下：**www.\<organization\>.jive.com**。</span><span class="sxs-lookup"><span data-stu-id="07eac-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="07eac-144">在 Azure 入口網站中，按一下 [測試連線]，以確保 Azure AD 可以連線至您的 Jive 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07eac-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="07eac-145">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。</span><span class="sxs-lookup"><span data-stu-id="07eac-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="07eac-146">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="07eac-146">Click **Save.**</span></span>

9. <span data-ttu-id="07eac-147">在 [對應] 區段下，選取 [同步處理 Azure Active Directory 使用者至 Jive]。</span><span class="sxs-lookup"><span data-stu-id="07eac-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="07eac-148">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Jive 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="07eac-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="07eac-149">選取為 [比對] 屬性的屬性會用來比對 Jive 中的使用者帳戶，以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="07eac-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="07eac-150">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="07eac-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="07eac-151">若要對 Jive 啟用 Azure AD 佈建服務，請在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="07eac-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="07eac-152">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="07eac-152">Click **Save.**</span></span>

<span data-ttu-id="07eac-153">這會對 [使用者和群組] 區段中指派給 Jive 的任何使用者和/或群組，啟動首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="07eac-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="07eac-154">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="07eac-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="07eac-155">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述佈建服務在您的 Jive 應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="07eac-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="07eac-156">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="07eac-156">You can now create a test account.</span></span> <span data-ttu-id="07eac-157">請等候 20 分鐘以確認帳戶已同步至 Jive。</span><span class="sxs-lookup"><span data-stu-id="07eac-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07eac-158">其他資源</span><span class="sxs-lookup"><span data-stu-id="07eac-158">Additional resources</span></span>

* [<span data-ttu-id="07eac-159">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="07eac-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07eac-160">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="07eac-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="07eac-161">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="07eac-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)