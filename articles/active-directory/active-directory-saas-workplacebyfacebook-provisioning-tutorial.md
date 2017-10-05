---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workplace by Facebook 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="57891-103">教學課程：設定使用者佈建的 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="57891-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="57891-104">本教學課程旨在說明您需要在 Workplace by Facebook 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Workplace by Facebook。</span><span class="sxs-lookup"><span data-stu-id="57891-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57891-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="57891-105">Prerequisites</span></span>

<span data-ttu-id="57891-106">若要設定 Azure AD 與 Workplace by Facebook 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="57891-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="57891-107">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="57891-107">An Azure AD subscription</span></span>
- <span data-ttu-id="57891-108">已啟用 Workplace by Facebook 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="57891-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57891-109">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="57891-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57891-110">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="57891-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57891-111">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="57891-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57891-112">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="57891-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="57891-113">將使用者指派給 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="57891-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="57891-114">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="57891-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="57891-115">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="57891-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="57891-116">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Workplace by Facebook 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="57891-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="57891-117">一旦決定後，您可以依照此處的指示，將這些使用者指派給 Workplace by Facebook 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="57891-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="57891-118">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="57891-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="57891-119">將使用者指派給 Workplace by Facebook 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="57891-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="57891-120">建議將單一 Azure AD 使用者指派給 Workplace by Facebook，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="57891-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="57891-121">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="57891-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="57891-122">將使用者指派給 Workplace by Facebook 時，必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="57891-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="57891-123">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="57891-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="57891-124">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="57891-124">Enable User Provisioning</span></span>

<span data-ttu-id="57891-125">本節會引導您將 Azure AD 連線至 Workplace by Facebook 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Workplace by Facebook 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="57891-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="57891-126">您也可以選擇啟用 Workplace by Facebook 的 SAML 型單一登入，並遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="57891-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="57891-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="57891-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="57891-128">若要在 Azure AD 中設定要佈建到 Workplace by Facebook 的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="57891-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="57891-129">本節旨在說明如何對 Workplace by Facebook 啟用 Active Directory 使用者帳戶的佈建。</span><span class="sxs-lookup"><span data-stu-id="57891-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="57891-130">Azure AD 支援將指派之使用者的帳戶詳細資料自動同步處理至 Workplace by Facebook 的功能。</span><span class="sxs-lookup"><span data-stu-id="57891-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="57891-131">這個自動同步處理可讓 Workplace by Facebook 在使用者嘗試第一次登入之前，取得授權使用者存取所需的資料。</span><span class="sxs-lookup"><span data-stu-id="57891-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="57891-132">當存取在 Azure AD 中被撤銷時，它也會從 Workplace by Facebook 取消佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="57891-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="57891-133">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="57891-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="57891-134">如果您已經設定單一登入的 Workplace by Facebook，使用 [搜尋] 欄位搜尋您的 Workplace by Facebook 執行個體。</span><span class="sxs-lookup"><span data-stu-id="57891-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="57891-135">否則，請選取 [新增]，並在應用程式庫中搜尋 [Workplace by Facebook]。</span><span class="sxs-lookup"><span data-stu-id="57891-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="57891-136">從搜尋結果中選取 Workplace by Facebook，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="57891-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="57891-137">選取您的 Workplace by Facebook 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57891-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="57891-138">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="57891-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="57891-140">在 [管理員認證] 區段下，輸入 Workplace by Facebook 系統管理員的祕密權杖和租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="57891-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="57891-141">在 Azure 入口網站中，按一下 [測試連線]以確保 Azure AD 可以連線到您的 Workplace by Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57891-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="57891-142">如果連線失敗，請確定您的 Workplace by Facebook 帳戶具有小組系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="57891-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="57891-143">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="57891-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="57891-144">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="57891-144">Click **Save.**</span></span>

9. <span data-ttu-id="57891-145">在 [對應] 區段中，選取 [同步處理 Azure Active Directory 使用者至 Workplace by Facebook]。</span><span class="sxs-lookup"><span data-stu-id="57891-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="57891-146">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Workplace by Facebook 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="57891-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="57891-147">選取為 [比對] 屬性的屬性會用來比對 Workplace by Facebook 中的使用者帳戶以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="57891-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="57891-148">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="57891-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="57891-149">若要啟用 Workplace by Facebook 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="57891-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="57891-150">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="57891-150">Click **Save.**</span></span>

<span data-ttu-id="57891-151">如需如何設定自動佈建的詳細資訊，請參閱 [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="57891-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="57891-152">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="57891-152">You can now create a test account.</span></span> <span data-ttu-id="57891-153">請等候 20 分鐘以驗證帳戶已同步至 Workplace by Facebook。</span><span class="sxs-lookup"><span data-stu-id="57891-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57891-154">其他資源</span><span class="sxs-lookup"><span data-stu-id="57891-154">Additional resources</span></span>

* [<span data-ttu-id="57891-155">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="57891-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57891-156">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="57891-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="57891-157">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="57891-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

