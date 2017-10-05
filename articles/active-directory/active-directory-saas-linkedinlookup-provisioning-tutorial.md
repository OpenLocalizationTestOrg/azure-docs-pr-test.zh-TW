---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Lookup | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 來自動佈建並取消佈建使用者帳戶至 LinkedIn Lookup。"
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="de785-103">教學課程︰設定自動使用者佈建的 LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="de785-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="de785-104">本教學課程旨在說明您需要在 LinkedIn Lookup 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 LinkedIn Lookup。</span><span class="sxs-lookup"><span data-stu-id="de785-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Lookup and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="de785-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="de785-105">Prerequisites</span></span>

<span data-ttu-id="de785-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="de785-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="de785-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="de785-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="de785-108">LinkedIn Lookup 租用戶</span><span class="sxs-lookup"><span data-stu-id="de785-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="de785-109">LinkedIn Lookup 的系統管理員帳戶具有 LinkedIn 帳戶中心的存取權</span><span class="sxs-lookup"><span data-stu-id="de785-109">An administrator account in LinkedIn Lookup with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="de785-110">Azure Active Directory 使用 [SCIM](http://www.simplecloud.info/) 通訊協定與 LinkedIn Lookup 整合。</span><span class="sxs-lookup"><span data-stu-id="de785-110">Azure Active Directory integrates with LinkedIn Lookup using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-lookup"></a><span data-ttu-id="de785-111">將使用者指派給 LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="de785-111">Assigning users to LinkedIn Lookup</span></span>

<span data-ttu-id="de785-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="de785-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="de785-113">在自動使用者帳戶佈建的內容中，只有已「指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="de785-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="de785-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 LinkedIn Lookup 存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="de785-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Lookup.</span></span> <span data-ttu-id="de785-115">一旦決定後，您可以依照此處的指示，將這些使用者指派給 LinkedIn Lookup︰</span><span class="sxs-lookup"><span data-stu-id="de785-115">Once decided, you can assign these users to LinkedIn Lookup by following the instructions here:</span></span>

[<span data-ttu-id="de785-116">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="de785-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a><span data-ttu-id="de785-117">將使用者指派給 LinkedIn Lookup 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="de785-117">Important tips for assigning users to LinkedIn Lookup</span></span>

*   <span data-ttu-id="de785-118">建議將單一 Azure AD 使用者指派給 LinkedIn Lookup，以測試佈建的設定。</span><span class="sxs-lookup"><span data-stu-id="de785-118">It is recommended that a single Azure AD user be assigned to LinkedIn Lookup to test the provisioning configuration.</span></span> <span data-ttu-id="de785-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="de785-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="de785-120">將使用者指派給 LinkedIn Lookup 時，您必須在指派對話方塊中選取**使用者**角色。</span><span class="sxs-lookup"><span data-stu-id="de785-120">When assigning a user to LinkedIn Lookup, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="de785-121">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="de785-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a><span data-ttu-id="de785-122">設定使用者佈建至 LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="de785-122">Configuring user provisioning to LinkedIn Lookup</span></span>

<span data-ttu-id="de785-123">本節會引導您將 Azure AD 連接至 LinkedIn Lookup 的 SCIM 使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 LinkedIn Lookup 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="de785-123">This section guides you through connecting your Azure AD to LinkedIn Lookup's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="de785-124">您也可以選擇啟用 LinkedIn Lookup 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="de785-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Lookup, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="de785-125">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="de785-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a><span data-ttu-id="de785-126">若要在 Azure AD 中設定自動使用者帳戶佈建至 LinkedIn Lookup︰</span><span class="sxs-lookup"><span data-stu-id="de785-126">To configure automatic user account provisioning to LinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="de785-127">第一步是擷取您的 LinkedIn Elevate 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="de785-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="de785-128">如果您是企業版系統管理員，可以自我佈建存取權杖。</span><span class="sxs-lookup"><span data-stu-id="de785-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="de785-129">在帳戶中心，移至 [設定]> [通用設定]**&gt;**，開啟 [SCIM 安裝] 面板。</span><span class="sxs-lookup"><span data-stu-id="de785-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="de785-130">如果您是直接存取帳戶中心，而不是透過連結，可以使用下列步驟開啟面板。</span><span class="sxs-lookup"><span data-stu-id="de785-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="de785-131">登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="de785-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="de785-132">選取 [系統管理員] > [系統管理員設定]**&gt;**。</span><span class="sxs-lookup"><span data-stu-id="de785-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="de785-133">按一下左欄中的 [進階整合]。</span><span class="sxs-lookup"><span data-stu-id="de785-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="de785-134">系統會將您導向帳戶中心。</span><span class="sxs-lookup"><span data-stu-id="de785-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="de785-135">按一下 [+ 新增 SCIM 組態]，遵循程序填寫每個欄位。</span><span class="sxs-lookup"><span data-stu-id="de785-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="de785-136">若未啟用自動指派授權，表示只有使用者資料會同步處理。</span><span class="sxs-lookup"><span data-stu-id="de785-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Lookup 佈建](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="de785-138">若啟用自動指派授權，您需要記下應用程式執行個體及授權類型。</span><span class="sxs-lookup"><span data-stu-id="de785-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="de785-139">授權的指派採取先到先拿原則，一直到所有授權都指派完為止。</span><span class="sxs-lookup"><span data-stu-id="de785-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![LinkedIn Lookup 佈建](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="de785-141">按一下 [產生權杖]。</span><span class="sxs-lookup"><span data-stu-id="de785-141">Click **Generate token**.</span></span> <span data-ttu-id="de785-142">您應該會看到您的存取權杖顯示在存取權杖 欄位下。</span><span class="sxs-lookup"><span data-stu-id="de785-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="de785-143">離開頁面之前，將您的存取權杖儲存至剪貼簿或電腦。</span><span class="sxs-lookup"><span data-stu-id="de785-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="de785-144">接下來，登入 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="de785-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="de785-145">如果您已經設定 LinkedIn Lookup 單一登入，請使用 [搜尋] 欄位搜尋您的 LinkedIn Lookup 執行個體。</span><span class="sxs-lookup"><span data-stu-id="de785-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using the search field.</span></span> <span data-ttu-id="de785-146">否則，請選取 [新增]，並在應用程式庫中搜尋 [LinkedIn Lookup]。</span><span class="sxs-lookup"><span data-stu-id="de785-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in the application gallery.</span></span> <span data-ttu-id="de785-147">從搜尋結果中選取 LinkedIn Lookup，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="de785-147">Select LinkedIn Lookup from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="de785-148">選取您的 LinkedIn Lookup 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="de785-148">Select your instance of LinkedIn Lookup, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="de785-149">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="de785-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![LinkedIn Lookup 佈建](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="de785-151">填寫 [系統管理員認證] 底下的下列欄位：</span><span class="sxs-lookup"><span data-stu-id="de785-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="de785-152">在 [租用戶 URL] 欄位中輸入 https://api.linkedin.com。</span><span class="sxs-lookup"><span data-stu-id="de785-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="de785-153">在 [祕密權杖] 欄位中，輸入在步驟 1 產生的存取權杖，然後按一下 [測試連線]。</span><span class="sxs-lookup"><span data-stu-id="de785-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="de785-154">您應該會在入口網站的右上角看到成功通知。</span><span class="sxs-lookup"><span data-stu-id="de785-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="de785-155">在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。</span><span class="sxs-lookup"><span data-stu-id="de785-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="de785-156">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de785-156">Click **Save**.</span></span> 

14) <span data-ttu-id="de785-157">在 [屬性對應] 區段中，檢閱將從 Azure AD 同步至 LinkedIn Lookup 的使用者和群組屬性。</span><span class="sxs-lookup"><span data-stu-id="de785-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Lookup.</span></span> <span data-ttu-id="de785-158">請注意，選取為 [比對] 屬性的屬性會用來比對 LinkedIn Lookup 中的使用者帳戶和群組以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="de785-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="de785-159">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="de785-159">Select the Save button to commit any changes.</span></span>

![LinkedIn Lookup 佈建](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="de785-161">若要啟用 LinkedIn Lookup 的 Azure AD 佈建服務，在 [設定]區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="de785-161">To enable the Azure AD provisioning service for LinkedIn Lookup, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="de785-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de785-162">Click **Save**.</span></span> 

<span data-ttu-id="de785-163">這會啟動在 [使用者和群組] 區段中指派給 LinkedIn Lookup 之任何使用者和/或群組初始的同步處理。</span><span class="sxs-lookup"><span data-stu-id="de785-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Lookup in the Users and Groups section.</span></span> <span data-ttu-id="de785-164">請注意，初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，這大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="de785-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="de785-165">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述您的 LinkedIn Lookup 應用程式上的佈建服務所執行之所有動作。</span><span class="sxs-lookup"><span data-stu-id="de785-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="de785-166">其他資源</span><span class="sxs-lookup"><span data-stu-id="de785-166">Additional Resources</span></span>

* [<span data-ttu-id="de785-167">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="de785-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="de785-168">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de785-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
