---
title: "教學課程︰以 Azure Active Directory 設定 Samanage 來自動佈建使用者 | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooSamanage。"
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="3caae-103">教學課程︰設定 Samanage 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="3caae-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="3caae-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform Samanage 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSamanage 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="3caae-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3caae-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="3caae-105">Prerequisites</span></span>

<span data-ttu-id="3caae-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="3caae-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="3caae-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="3caae-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="3caae-108">Samanage 租用戶與 hello[專業人員的計劃](https://www.samanage.com/pricing/)或進一步啟用</span><span class="sxs-lookup"><span data-stu-id="3caae-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="3caae-109">Samanage 中具有管理員權限的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="3caae-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="3caae-110">hello Azure AD 佈建整合依賴 hello [Samanage REST API](https://www.samanage.com/api/)，也就是可用 tooSamanage hello Professional 小組計劃或更好。</span><span class="sxs-lookup"><span data-stu-id="3caae-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="3caae-111">指派使用者 tooSamanage</span><span class="sxs-lookup"><span data-stu-id="3caae-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="3caae-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="3caae-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="3caae-113">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3caae-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="3caae-114">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Samanage 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="3caae-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="3caae-115">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Samanage 應用程式：</span><span class="sxs-lookup"><span data-stu-id="3caae-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="3caae-116">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="3caae-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="3caae-117">指派使用者 tooSamanage 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="3caae-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="3caae-118">建議在單一 tooSamanage tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="3caae-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="3caae-119">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="3caae-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="3caae-120">指派使用者 tooSamanage 時，您必須選取其中一個 hello**使用者**角色或另一個有效應用程式特定的角色 （如果有的話） 在 hello 分派 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="3caae-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="3caae-121">hello**預設存取**角色不適用於佈建，以及這些使用者會略過。</span><span class="sxs-lookup"><span data-stu-id="3caae-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="3caae-122">做為新增的功能，佈建服務的 hello 讀取 Samanage 中，在定義的任何自訂角色，並匯入至 Azure AD 在 hello 選取角色 對話方塊中加以選取。</span><span class="sxs-lookup"><span data-stu-id="3caae-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="3caae-123">啟用佈建服務的 hello 和一個同步處理循環完成之後，這些角色會顯示在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3caae-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="3caae-124">設定使用者佈建 tooSamanage</span><span class="sxs-lookup"><span data-stu-id="3caae-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="3caae-125">本節會引導您完成連接您的 Azure AD tooSamanage 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Samanage 中指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3caae-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="3caae-126">您也可以選擇 tooenabled SAML 型單一登入 samanage，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3caae-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3caae-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="3caae-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="3caae-128">設定 Azure AD 中佈建 tooSamanage 自動使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="3caae-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="3caae-129">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3caae-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="3caae-130">如果您已經設定進行單一登入 Samanage，搜尋您的 Samanage 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3caae-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="3caae-131">否則，請選取**新增**並搜尋**Samanage** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="3caae-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="3caae-132">從 hello 搜尋結果中，選取 Samanage，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="3caae-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="3caae-133">選取您的 Samanage 中，執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3caae-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="3caae-134">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="3caae-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Samanage 佈建](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="3caae-136">在 hello**系統管理員認證**區段中，輸入的 hello**系統管理員使用者名稱與系統管理員密碼**的 Samanage 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3caae-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="3caae-137">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Samanage 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="3caae-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="3caae-138">如果 hello 連線失敗，請確定您的 Samanage 帳戶具有系統管理員權限，並再試一次步驟 5。</span><span class="sxs-lookup"><span data-stu-id="3caae-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="3caae-139">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，以及檢查 hello 核取方塊 傳送電子郵件通知發生失敗時。 」</span><span class="sxs-lookup"><span data-stu-id="3caae-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="3caae-140">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3caae-140">Click **Save**.</span></span> 

9. <span data-ttu-id="3caae-141">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooSamanage**。</span><span class="sxs-lookup"><span data-stu-id="3caae-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="3caae-142">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooSamanage 同步。</span><span class="sxs-lookup"><span data-stu-id="3caae-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="3caae-143">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Samanage 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="3caae-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="3caae-144">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="3caae-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="3caae-145">tooenable hello Samanage 中，變更 hello 的 Azure AD 佈建服務**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="3caae-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="3caae-146">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3caae-146">Click **Save**.</span></span> 

<span data-ttu-id="3caae-147">這項作業會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooSamanage 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="3caae-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="3caae-148">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="3caae-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="3caae-149">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="3caae-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="3caae-150">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="3caae-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3caae-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="3caae-151">Additional resources</span></span>

* [<span data-ttu-id="3caae-152">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="3caae-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="3caae-153">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3caae-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="3caae-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3caae-154">Next steps</span></span>

* [<span data-ttu-id="3caae-155">瞭解如何 tooreview 記錄並取得上佈建活動報表</span><span class="sxs-lookup"><span data-stu-id="3caae-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
