---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Netsuite 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="7b2bc-103">教學課程︰設定 Netsuite 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="7b2bc-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="7b2bc-104">本教學課程旨在說明您需要在 Netsuite 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Netsuite。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b2bc-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b2bc-105">Prerequisites</span></span>

<span data-ttu-id="7b2bc-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="7b2bc-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="7b2bc-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="7b2bc-108">啟用 Netsuite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7b2bc-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="7b2bc-109">Netsuite 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="7b2bc-110">將使用者指派給 Netsuite</span><span class="sxs-lookup"><span data-stu-id="7b2bc-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="7b2bc-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="7b2bc-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="7b2bc-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Netsuite 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="7b2bc-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Netsuite 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="7b2bc-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="7b2bc-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="7b2bc-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="7b2bc-116">將使用者指派給 Netsuite 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="7b2bc-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="7b2bc-117">建議將單一 Azure AD 使用者指派給 Netsuite，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="7b2bc-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7b2bc-119">將使用者指派給 Netsuite 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="7b2bc-120">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="7b2bc-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="7b2bc-121">Enable User Provisioning</span></span>

<span data-ttu-id="7b2bc-122">本節會引導您將 Azure AD 連線至 Netsuite 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Netsuite 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="7b2bc-123">您也可以選擇啟用 Netsuite 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7b2bc-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="7b2bc-125">若要設定使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="7b2bc-125">To configure user account provisioning:</span></span>

<span data-ttu-id="7b2bc-126">本節的目的是要說明如何對 Netsuite 啟用 Active Directory 使用者帳戶的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="7b2bc-127">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="7b2bc-128">如果您已將 Netsuite 設定為單一登入，請使用 [搜尋] 欄位搜尋您的 Netsuite 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="7b2bc-129">否則，請選取 [新增]，並在應用程式庫中搜尋 [Netsuite]。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="7b2bc-130">從搜尋結果中選取 Netsuite，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="7b2bc-131">選取您的 Netsuite 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="7b2bc-132">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="7b2bc-134">在 [管理員認證] 區段下，提供下列組態設定：</span><span class="sxs-lookup"><span data-stu-id="7b2bc-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="7b2bc-135">a.</span><span class="sxs-lookup"><span data-stu-id="7b2bc-135">a.</span></span> <span data-ttu-id="7b2bc-136">在 [管理員使用者名稱] 文字方塊中，輸入已在 Netsuite.com 指派**系統管理員**設定檔的 Netsuite 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="7b2bc-137">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-137">b.</span></span> <span data-ttu-id="7b2bc-138">在 [管理員密碼] 文字方塊中，輸入這個帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="7b2bc-139">在 Azure 入口網站中，按一下 [測試連線]，以確保 Azure AD 可以連線至您的 Netsuite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="7b2bc-140">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選 [發生失敗時傳送電子郵件通知] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="7b2bc-141">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-141">Click **Save.**</span></span>

9. <span data-ttu-id="7b2bc-142">在 [對應] 區段下，選取 [同步處理 Azure Active Directory 使用者至 Netsuite]。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="7b2bc-143">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Netsuite 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="7b2bc-144">請注意，選取為 [比對] 屬性的屬性會用來比對 Netsuite 中的使用者帳戶，以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="7b2bc-145">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="7b2bc-146">若要對 Netsuite 啟用 Azure AD 佈建服務，請在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="7b2bc-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="7b2bc-147">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-147">Click **Save.**</span></span>

<span data-ttu-id="7b2bc-148">這會對 [使用者和群組] 區段中指派給 Netsuite 的任何使用者和/或群組，啟動首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="7b2bc-149">請注意，初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，這大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="7b2bc-150">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述佈建服務在您的 Netsuite 應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="7b2bc-151">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-151">You can now create a test account.</span></span> <span data-ttu-id="7b2bc-152">請等候 20 分鐘以確認帳戶已同步至 Netsuite。</span><span class="sxs-lookup"><span data-stu-id="7b2bc-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b2bc-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="7b2bc-153">Additional resources</span></span>

* [<span data-ttu-id="7b2bc-154">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="7b2bc-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b2bc-155">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7b2bc-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7b2bc-156">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="7b2bc-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)