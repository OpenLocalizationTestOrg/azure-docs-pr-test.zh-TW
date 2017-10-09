---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 ZenDesk | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooZenDesk。"
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="76962-103">教學課程︰設定自動使用者佈建的 ZenDesk</span><span class="sxs-lookup"><span data-stu-id="76962-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="76962-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform ZenDesk 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooZenDesk 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="76962-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76962-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="76962-105">Prerequisites</span></span>

<span data-ttu-id="76962-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="76962-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="76962-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="76962-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="76962-108">ZenDesk 租用戶與 hello[企業計劃](https://www.zendesk.com/product/pricing/)或進一步啟用</span><span class="sxs-lookup"><span data-stu-id="76962-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="76962-109">ZenDesk 中具有系統管理員權限的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="76962-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="76962-110">hello Azure AD 佈建整合依賴 hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api)，也就是可用 tooZenDesk 小組 hello 基本計劃或更高。</span><span class="sxs-lookup"><span data-stu-id="76962-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="76962-111">指派使用者 tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="76962-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="76962-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="76962-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="76962-113">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="76962-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="76962-114">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour ZenDesk 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="76962-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="76962-115">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour ZenDesk 應用程式：</span><span class="sxs-lookup"><span data-stu-id="76962-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="76962-116">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="76962-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="76962-117">指派使用者 tooZenDesk 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="76962-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="76962-118">建議在單一 tooZenDesk tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="76962-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="76962-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="76962-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="76962-120">指派使用者 tooZenDesk 時，您必須選取其中一個 hello**使用者**角色或另一個有效應用程式特定的角色 （如果有的話） 在 hello 分派 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="76962-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="76962-121">hello**預設存取**角色不適用於佈建，以及這些使用者會略過。</span><span class="sxs-lookup"><span data-stu-id="76962-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="76962-122">做為新增的功能，佈建服務的 hello 讀取 Zendesk 中, 定義的任何自訂角色，並匯入至 Azure AD 在 hello 選取角色 對話方塊中加以選取。</span><span class="sxs-lookup"><span data-stu-id="76962-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="76962-123">啟用佈建服務的 hello 和一個同步處理循環完成之後，這些角色會顯示在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="76962-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="76962-124">設定使用者佈建 tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="76962-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="76962-125">本節會引導您完成連接您的 Azure AD tooZenDesk 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 ZenDesk 中指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="76962-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="76962-126">您也可以選擇 tooenabled SAML 型單一登入 zendesk，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="76962-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="76962-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="76962-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="76962-128">設定 Azure AD 中佈建 tooZenDesk 自動使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="76962-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="76962-129">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="76962-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="76962-130">如果您已經設定 ZenDesk 的單一登入，搜尋您的 ZenDesk 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="76962-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="76962-131">否則，請選取**新增**並搜尋**ZenDesk** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="76962-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="76962-132">從 hello 搜尋結果中，選取 ZenDesk，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="76962-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="76962-133">選取您的 ZenDesk，執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="76962-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="76962-134">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="76962-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="76962-136">在 hello**系統管理員認證**區段中，輸入的 hello**管理員使用者名稱 & tokenkey 網域**產生由您的 ZenDesk 帳戶 (您可以在您的帳戶下找到 hello 語彙基元：**系統管理員**  >  **API** > **設定**)。</span><span class="sxs-lookup"><span data-stu-id="76962-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![ZenDesk 佈建](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="76962-138">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour ZenDesk 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="76962-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="76962-139">如果 hello 連線失敗，請確定您的 ZenDesk 帳戶具有系統管理員權限，並再試一次步驟 5。</span><span class="sxs-lookup"><span data-stu-id="76962-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="76962-140">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，以及檢查 hello 核取方塊 傳送電子郵件通知發生失敗時。 」</span><span class="sxs-lookup"><span data-stu-id="76962-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="76962-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="76962-141">Click **Save**.</span></span> 

9. <span data-ttu-id="76962-142">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooZenDesk**。</span><span class="sxs-lookup"><span data-stu-id="76962-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="76962-143">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooZenDesk 同步。</span><span class="sxs-lookup"><span data-stu-id="76962-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="76962-144">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 中的使用者帳戶 ZenDesk 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="76962-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="76962-145">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="76962-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="76962-146">tooenable hello Azure AD 佈建服務 zendesk，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="76962-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="76962-147">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="76962-147">Click **Save**.</span></span> 

<span data-ttu-id="76962-148">這項作業會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooZenDesk 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="76962-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="76962-149">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="76962-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="76962-150">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="76962-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="76962-151">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="76962-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="76962-152">其他資源</span><span class="sxs-lookup"><span data-stu-id="76962-152">Additional resources</span></span>

* [<span data-ttu-id="76962-153">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="76962-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="76962-154">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="76962-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="76962-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76962-155">Next steps</span></span>

* [<span data-ttu-id="76962-156">瞭解如何 tooreview 記錄並取得上佈建活動報表</span><span class="sxs-lookup"><span data-stu-id="76962-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
