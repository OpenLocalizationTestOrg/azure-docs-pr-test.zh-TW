---
title: "教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Citrix GoToMeeting 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="a822d-103">教學課程︰設定自動使用者佈建的 Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="a822d-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="a822d-104">本教學課程旨在說明您需要在 Citrix GoToMeeting 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Citrix GoToMeeting。</span><span class="sxs-lookup"><span data-stu-id="a822d-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a822d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a822d-105">Prerequisites</span></span>

<span data-ttu-id="a822d-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="a822d-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a822d-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a822d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a822d-108">已啟用 Citrix GoToMeeting 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a822d-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="a822d-109">具有小組系統管理員權限的 Citrix GoToMeeting 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a822d-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="a822d-110">將使用者指派給 Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="a822d-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="a822d-111">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="a822d-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a822d-112">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="a822d-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="a822d-113">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Citrix GoToMeeting 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="a822d-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="a822d-114">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Citrix GoToMeeting 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="a822d-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="a822d-115">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="a822d-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="a822d-116">將使用者指派給 Citrix GoToMeeting 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="a822d-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="a822d-117">建議將單一 Azure AD 使用者指派給 Citrix GoToMeeting，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="a822d-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="a822d-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="a822d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a822d-119">將使用者指派給 Citrix GoToMeeting 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="a822d-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="a822d-120">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="a822d-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="a822d-121">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="a822d-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="a822d-122">本節會引導您將 Azure AD 連線至 Citrix GoToMeeting 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Citrix GoToMeeting 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a822d-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a822d-123">您也可以選擇啟用 Citrix GoToMeeting 的 SAML 型單一登入，並遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="a822d-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a822d-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="a822d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="a822d-125">若要設定自動使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="a822d-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="a822d-126">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="a822d-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a822d-127">如果您已經設定 Citrix GoToMeeting 單一登入，使用 [搜尋] 欄位搜尋您的 Citrix GoToMeeting 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a822d-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="a822d-128">否則，請選取 [新增]，並在應用程式庫中搜尋 [Citrix GoToMeeting]。</span><span class="sxs-lookup"><span data-stu-id="a822d-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="a822d-129">從搜尋結果中選取 Citrix GoToMeeting，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a822d-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a822d-130">選取您的 Citrix GoToMeeting 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a822d-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a822d-131">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="a822d-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a822d-133">在 [管理員認證] 區段底下，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a822d-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="a822d-134">a.</span><span class="sxs-lookup"><span data-stu-id="a822d-134">a.</span></span> <span data-ttu-id="a822d-135">在 [Citrix GoToMeeting 管理員使用者名稱] 文字方塊中，輸入管理員的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a822d-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="a822d-136">b.</span><span class="sxs-lookup"><span data-stu-id="a822d-136">b.</span></span> <span data-ttu-id="a822d-137">在 [Citrix GoToMeeting 管理員密碼] 文字方塊中，輸入管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="a822d-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="a822d-138">在 Azure 入口網站中，按一下 [測試連線] 以確保 Azure AD 可以連線到您的 Citrix GoToMeeting 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a822d-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="a822d-139">如果連線失敗，請確定您的 Citrix GoToMeeting 帳戶具有小組系統管理員權限，並再試一次「管理員認證」步驟。</span><span class="sxs-lookup"><span data-stu-id="a822d-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="a822d-140">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a822d-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="a822d-141">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a822d-141">Click **Save.**</span></span>

9. <span data-ttu-id="a822d-142">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Citrix GoToMeeting]。</span><span class="sxs-lookup"><span data-stu-id="a822d-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="a822d-143">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Citrix GoToMeeting 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="a822d-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="a822d-144">選取為 [比對] 屬性的屬性會用來比對 Citrix GoToMeeting 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="a822d-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="a822d-145">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="a822d-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a822d-146">若要啟用 Citrix GoToMeeting 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="a822d-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="a822d-147">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a822d-147">Click **Save.**</span></span>

<span data-ttu-id="a822d-148">這會啟動在 [使用者和群組] 區段中指派給 Citrix GoToMeeting 的任何使用者和/或群組之首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="a822d-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="a822d-149">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="a822d-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a822d-150">您可以使用 [同步處理詳細資料] 區段來監視進度，並連結到佈建活動報表，該報表描述您 Citrix GoToMeeting 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="a822d-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a822d-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="a822d-151">Additional resources</span></span>

* [<span data-ttu-id="a822d-152">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="a822d-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a822d-153">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a822d-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a822d-154">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="a822d-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


