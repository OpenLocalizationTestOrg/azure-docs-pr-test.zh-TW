---
title: "教學課程︰以 Azure Active Directory 設定 LucidChart 來自動佈建使用者 | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooLucidChart。"
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="61c5a-103">教學課程︰設定 LucidChart 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="61c5a-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="61c5a-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform LucidChart 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooLucidChart 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="61c5a-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="61c5a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="61c5a-105">Prerequisites</span></span>

<span data-ttu-id="61c5a-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="61c5a-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="61c5a-107">Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="61c5a-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="61c5a-108">LucidChart 租用戶與 hello[企業計劃](https://www.lucidchart.com/user/117598685#/subscriptionLevel)或進一步啟用</span><span class="sxs-lookup"><span data-stu-id="61c5a-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="61c5a-109">LucidChart 中具有管理員權限的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="61c5a-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="61c5a-110">指派使用者 tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="61c5a-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="61c5a-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="61c5a-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="61c5a-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="61c5a-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="61c5a-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour LucidChart 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="61c5a-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="61c5a-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour LucidChart 應用程式：</span><span class="sxs-lookup"><span data-stu-id="61c5a-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="61c5a-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="61c5a-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="61c5a-116">指派使用者 tooLucidChart 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="61c5a-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="61c5a-117">建議在單一 tooLucidChart tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="61c5a-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="61c5a-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="61c5a-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="61c5a-119">指派使用者 tooLucidChart 時，您必須選取其中一個 hello**使用者**角色或另一個有效應用程式特定的角色 （如果有的話） 在 hello 分派 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="61c5a-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="61c5a-120">hello**預設存取**角色不適用於佈建，以及這些使用者會略過。</span><span class="sxs-lookup"><span data-stu-id="61c5a-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="61c5a-121">設定使用者佈建 tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="61c5a-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="61c5a-122">本節會引導您完成連接您的 Azure AD tooLucidChart 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用在 LucidChart 的 Azure AD 中的使用者和群組指派為基礎的指派的使用者帳戶.</span><span class="sxs-lookup"><span data-stu-id="61c5a-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="61c5a-123">您也可以選擇 tooenabled SAML 型單一登入 lucidchart，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="61c5a-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="61c5a-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="61c5a-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="61c5a-125">設定 Azure AD 中佈建 tooLucidChart 自動使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="61c5a-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="61c5a-126">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="61c5a-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="61c5a-127">如果您已經設定 LucidChart 的單一登入，搜尋您 LucidChart 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="61c5a-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="61c5a-128">否則，請選取**新增**並搜尋**LucidChart** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="61c5a-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="61c5a-129">從 hello 搜尋結果中，選取 LucidChart，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="61c5a-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="61c5a-130">選取您的 LucidChart，執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="61c5a-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="61c5a-131">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="61c5a-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![LucidChart 佈建](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="61c5a-133">Hello 下**系統管理員認證**區段中，輸入的 hello**密碼語彙基元**產生由您 LucidChart 帳戶 (您可以在您的帳戶下找到 hello 語彙基元：**小組** > **應用程式整合** > **SCIM**)。</span><span class="sxs-lookup"><span data-stu-id="61c5a-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart 佈建](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="61c5a-135">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour LucidChart 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="61c5a-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="61c5a-136">如果 hello 連線失敗，請確定您的 LucidChart 帳戶具有系統管理員權限，並再試一次步驟 5。</span><span class="sxs-lookup"><span data-stu-id="61c5a-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="61c5a-137">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，以及檢查 hello 核取方塊 傳送電子郵件通知發生失敗時。 」</span><span class="sxs-lookup"><span data-stu-id="61c5a-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="61c5a-138">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="61c5a-138">Click **Save**.</span></span> 

9. <span data-ttu-id="61c5a-139">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooLucidChart**。</span><span class="sxs-lookup"><span data-stu-id="61c5a-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="61c5a-140">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooLucidChart 同步。</span><span class="sxs-lookup"><span data-stu-id="61c5a-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="61c5a-141">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 中的使用者帳戶 LucidChart 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="61c5a-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="61c5a-142">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="61c5a-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="61c5a-143">tooenable hello Azure AD 佈建服務 lucidchart，變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="61c5a-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="61c5a-144">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="61c5a-144">Click **Save**.</span></span> 

<span data-ttu-id="61c5a-145">這項作業會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooLucidChart 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="61c5a-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="61c5a-146">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="61c5a-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="61c5a-147">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="61c5a-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="61c5a-148">如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。</span><span class="sxs-lookup"><span data-stu-id="61c5a-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="61c5a-149">其他資源</span><span class="sxs-lookup"><span data-stu-id="61c5a-149">Additional resources</span></span>

* [<span data-ttu-id="61c5a-150">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="61c5a-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="61c5a-151">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="61c5a-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="61c5a-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61c5a-152">Next steps</span></span>

* [<span data-ttu-id="61c5a-153">瞭解如何 tooreview 記錄並取得上佈建活動報表</span><span class="sxs-lookup"><span data-stu-id="61c5a-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
