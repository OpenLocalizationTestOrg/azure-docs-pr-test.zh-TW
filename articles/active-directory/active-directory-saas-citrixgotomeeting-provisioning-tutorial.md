---
title: "教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Citrix GoToMeeting 之間。"
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
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="4664d-103">教學課程︰設定自動使用者佈建的 Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="4664d-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="4664d-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform Citrix GoToMeeting 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooCitrix GoToMeeting 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="4664d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4664d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="4664d-105">Prerequisites</span></span>

<span data-ttu-id="4664d-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="4664d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4664d-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4664d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4664d-108">已啟用 Citrix GoToMeeting 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4664d-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="4664d-109">具有小組系統管理員權限的 Citrix GoToMeeting 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4664d-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="4664d-110">指派使用者 tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="4664d-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="4664d-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="4664d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4664d-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4664d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4664d-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Citrix GoToMeeting 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4664d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="4664d-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Citrix GoToMeeting 的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4664d-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="4664d-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="4664d-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="4664d-116">指派使用者 tooCitrix GoToMeeting 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="4664d-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="4664d-117">建議在單一 tooCitrix GoToMeeting tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="4664d-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="4664d-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="4664d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4664d-119">指派使用者 tooCitrix GoToMeeting 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="4664d-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="4664d-120">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="4664d-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4664d-121">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="4664d-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="4664d-122">本節會引導您完成連接您 Azure AD tooCitrix GoToMeeting 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用指派的使用者帳戶 Citrix GoToMeeting 中的根據使用者和群組Azure AD 中的指派。</span><span class="sxs-lookup"><span data-stu-id="4664d-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4664d-123">您也可以選擇 tooenabled SAML 型單一登入 Citrix gotomeeting，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4664d-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4664d-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="4664d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="4664d-125">tooconfigure 自動帳戶佈建使用者：</span><span class="sxs-lookup"><span data-stu-id="4664d-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="4664d-126">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="4664d-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="4664d-127">如果您已經設定進行單一登入 Citrix GoToMeeting，搜尋您使用 hello 搜尋欄位中的 Citrix GoToMeeting 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4664d-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="4664d-128">否則，請選取**新增**並搜尋**Citrix GoToMeeting** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="4664d-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="4664d-129">從 hello 搜尋結果中，選取 Citrix GoToMeeting，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="4664d-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4664d-130">選取您的 Citrix GoToMeeting 的執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4664d-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4664d-131">設定 hello**佈建**模式太**自動**。</span><span class="sxs-lookup"><span data-stu-id="4664d-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="4664d-133">在下 hello 系統管理員認證 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4664d-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4664d-134">a.</span><span class="sxs-lookup"><span data-stu-id="4664d-134">a.</span></span> <span data-ttu-id="4664d-135">在 hello **Citrix GoToMeeting 系統管理員使用者名稱**文字方塊中，輸入 hello 的使用者名稱的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4664d-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="4664d-136">b.</span><span class="sxs-lookup"><span data-stu-id="4664d-136">b.</span></span> <span data-ttu-id="4664d-137">在 [hello **Citrix GoToMeeting 管理員密碼**hello 系統管理員密碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4664d-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="4664d-138">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Citrix GoToMeeting 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4664d-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="4664d-139">如果 hello 連線失敗，請確定您的 Citrix GoToMeeting 帳戶具有小組系統管理員權限，然後再次嘗試 hello **[系統管理認證]**步驟一次。</span><span class="sxs-lookup"><span data-stu-id="4664d-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="4664d-140">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4664d-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="4664d-141">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4664d-141">Click **Save.**</span></span>

9. <span data-ttu-id="4664d-142">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooCitrix GoToMeeting。**</span><span class="sxs-lookup"><span data-stu-id="4664d-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="4664d-143">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooCitrix GoToMeeting 同步。</span><span class="sxs-lookup"><span data-stu-id="4664d-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="4664d-144">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Citrix GoToMeeting 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="4664d-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="4664d-145">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="4664d-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4664d-146">tooenable hello Azure AD 佈建服務 Citrix gotomeeting，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="4664d-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="4664d-147">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4664d-147">Click **Save.**</span></span>

<span data-ttu-id="4664d-148">啟動 hello 初始同步處理的任何使用者和/或群組指派 tooCitrix GoToMeeting hello 使用者和群組 區段中。</span><span class="sxs-lookup"><span data-stu-id="4664d-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="4664d-149">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="4664d-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4664d-150">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Citrix GoToMeeting 的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="4664d-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4664d-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="4664d-151">Additional resources</span></span>

* [<span data-ttu-id="4664d-152">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="4664d-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4664d-153">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4664d-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4664d-154">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="4664d-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


