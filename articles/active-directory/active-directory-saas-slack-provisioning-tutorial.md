---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Slack | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooSlack。"
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
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="2883d-103">教學課程︰設定自動使用者佈建的 Slack</span><span class="sxs-lookup"><span data-stu-id="2883d-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="2883d-104">hello 這個教學課程的目標是 tooshow hello 需要 tooperform Slack 和 Azure 中的步驟 AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSlack。</span><span class="sxs-lookup"><span data-stu-id="2883d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2883d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="2883d-105">Prerequisites</span></span>

<span data-ttu-id="2883d-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="2883d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="2883d-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="2883d-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="2883d-108">Slack 租用戶以 hello[再加上計劃](https://aadsyncfabric.slack.com/pricing)或進一步啟用</span><span class="sxs-lookup"><span data-stu-id="2883d-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="2883d-109">具有小組系統管理員權限的 Slack 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="2883d-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="2883d-110">注意： hello Azure AD 佈建整合依賴 hello [Slack SCIM API](https://api.slack.com/scim)也就是可用 tooSlack 小組 hello 再加上計劃或更高。</span><span class="sxs-lookup"><span data-stu-id="2883d-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="2883d-111">指派使用者 tooSlack</span><span class="sxs-lookup"><span data-stu-id="2883d-111">Assigning users tooSlack</span></span>

<span data-ttu-id="2883d-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="2883d-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="2883d-113">在 hello 內容中的自動帳戶佈建使用者，將同步的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="2883d-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="2883d-114">在之前設定，及啟用 hello 佈建服務，您必須 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Slack 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="2883d-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="2883d-115">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Slack 應用程式：</span><span class="sxs-lookup"><span data-stu-id="2883d-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="2883d-116">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="2883d-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="2883d-117">指派使用者 tooSlack 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="2883d-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="2883d-118">建議在單一 Azure AD 使用者被指派 tooSlack tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="2883d-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="2883d-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="2883d-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="2883d-120">指派使用者 tooSlack 時，您必須選取 hello**使用者**或 hello 分派對話方塊中的 「 群組 」 角色。</span><span class="sxs-lookup"><span data-stu-id="2883d-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="2883d-121">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="2883d-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="2883d-122">設定使用者佈建 tooSlack</span><span class="sxs-lookup"><span data-stu-id="2883d-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="2883d-123">本節會引導您完成連接您的 Azure AD tooSlack 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新並停用在 Slack 的 Azure AD 中的使用者和群組指派為基礎的指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2883d-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="2883d-124">**提示：**您也可以選擇 tooenabled SAML 型單一登入 slack，hello 指示 （Azure 入口網站） 中提供 [https://portal.azure.com]。</span><span class="sxs-lookup"><span data-stu-id="2883d-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="2883d-125">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="2883d-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="2883d-126">在 Azure AD 中佈建 tooSlack tooconfigure 自動使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="2883d-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="2883d-127">在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="2883d-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="2883d-128">如果您已經設定進行單一登入 Slack，搜尋您的 Slack 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="2883d-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="2883d-129">否則，請選取**新增**並搜尋**Slack** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="2883d-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="2883d-130">從 hello 搜尋結果中，選取 [Slack，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="2883d-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="2883d-131">選取您的 Slack，執行個體，然後選取 hello**佈建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2883d-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="2883d-132">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="2883d-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Slack 佈建](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="2883d-134">在 [hello**系統管理員認證**區段中，按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="2883d-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="2883d-135">這會在新的瀏覽器視窗中開啟 Slack 授權對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2883d-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="2883d-136">在 hello 新視窗中，登入 Slack 使用您的小組系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="2883d-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="2883d-137">在 hello 產生授權對話方塊中，選取 hello Slack 的小組，您想要佈建 tooenable，然後選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="2883d-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="2883d-138">一旦完成，則傳回 toohello Azure 入口網站 toocomplete hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="2883d-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![授權對話方塊](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="2883d-140">在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Slack 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="2883d-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="2883d-141">如果 hello 連線失敗，請確定您的 Slack 帳戶具有小組系統管理員權限，然後再次嘗試的 hello 「 授權 」 步驟一次。</span><span class="sxs-lookup"><span data-stu-id="2883d-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="2883d-142">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。</span><span class="sxs-lookup"><span data-stu-id="2883d-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="2883d-143">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2883d-143">Click **Save**.</span></span> 

10) <span data-ttu-id="2883d-144">在 [hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooSlack**。</span><span class="sxs-lookup"><span data-stu-id="2883d-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="2883d-145">在 [hello**屬性對應**區段中，檢閱將會從 Azure AD tooSlack 同步處理的 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="2883d-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="2883d-146">請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 中的使用者帳戶 Slack 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="2883d-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="2883d-147">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="2883d-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="2883d-148">tooenable hello Azure AD 佈建服務 slack，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="2883d-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="2883d-149">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2883d-149">Click **Save**.</span></span> 

<span data-ttu-id="2883d-150">這會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooSlack 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2883d-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="2883d-151">請注意，hello 初始同步處理會花費較長的 tooperform 比發生大約每 10 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="2883d-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="2883d-152">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Slack 的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="2883d-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="2883d-153">[選用]設定佈建 tooSlack 群組物件</span><span class="sxs-lookup"><span data-stu-id="2883d-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="2883d-154">（選擇性） 您可以啟用群組物件，從 Azure AD tooSlack hello 佈建。</span><span class="sxs-lookup"><span data-stu-id="2883d-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="2883d-155">這是不同的 「 指派的使用者群組 」，該 hello 實際群組物件中除了 tooits 成員將會複寫從 Azure AD tooSlack。</span><span class="sxs-lookup"><span data-stu-id="2883d-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="2883d-156">例如，如果您在 Azure AD 中有名為「我的群組」的群組，則會在 Slack 內建立名為「我的群組」的完全相同群組。</span><span class="sxs-lookup"><span data-stu-id="2883d-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="2883d-157">tooenable 佈建群組物件：</span><span class="sxs-lookup"><span data-stu-id="2883d-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="2883d-158">在 [hello 對應區段中，選取**同步處理 Azure Active Directory 群組 tooSlack**。</span><span class="sxs-lookup"><span data-stu-id="2883d-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="2883d-159">在屬性對應的 hello 刀鋒視窗中，會設定已啟用 tooYes。</span><span class="sxs-lookup"><span data-stu-id="2883d-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="2883d-160">在 [hello**屬性對應**區段中，檢閱將會從 Azure AD tooSlack 同步處理的 hello 群組屬性。</span><span class="sxs-lookup"><span data-stu-id="2883d-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="2883d-161">請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 群組 Slack 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="2883d-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="2883d-162">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2883d-162">Click **Save**.</span></span>

<span data-ttu-id="2883d-163">這個結果中的 hello 任何群組指派物件 tooSlack**使用者和群組**區段從 Azure AD tooSlack 完整同步處理。</span><span class="sxs-lookup"><span data-stu-id="2883d-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="2883d-164">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Slack 的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="2883d-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2883d-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="2883d-165">Additional Resources</span></span>

* [<span data-ttu-id="2883d-166">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="2883d-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="2883d-167">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="2883d-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
