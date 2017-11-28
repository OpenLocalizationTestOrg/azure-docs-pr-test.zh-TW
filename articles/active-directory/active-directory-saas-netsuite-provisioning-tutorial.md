---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Netsuite 之間。"
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
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="62f3f-103">教學課程︰設定 Netsuite 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="62f3f-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="62f3f-104">本教學課程的 hello 目標是 tooshow hello 需要 tooperform Netsuite 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooNetsuite 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="62f3f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62f3f-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="62f3f-105">Prerequisites</span></span>

<span data-ttu-id="62f3f-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="62f3f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="62f3f-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="62f3f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="62f3f-108">啟用 Netsuite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="62f3f-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="62f3f-109">Netsuite 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="62f3f-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="62f3f-110">指派使用者 tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="62f3f-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="62f3f-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="62f3f-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="62f3f-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="62f3f-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="62f3f-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Netsuite 的應用程式中的群組。</span><span class="sxs-lookup"><span data-stu-id="62f3f-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="62f3f-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Netsuite 應用程式：</span><span class="sxs-lookup"><span data-stu-id="62f3f-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="62f3f-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="62f3f-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="62f3f-116">指派使用者 tooNetsuite 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="62f3f-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="62f3f-117">建議在單一 tooNetsuite tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="62f3f-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="62f3f-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="62f3f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="62f3f-119">指派使用者 tooNetsuite 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="62f3f-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="62f3f-120">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="62f3f-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="62f3f-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="62f3f-121">Enable User Provisioning</span></span>

<span data-ttu-id="62f3f-122">本節會引導您完成連接您的 Azure AD tooNetsuite 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用在 Netsuite 的 Azure AD 中的使用者和群組指派為基礎的指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="62f3f-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="62f3f-123">您也可以選擇 tooenabled SAML 型單一登入 netsuite，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="62f3f-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="62f3f-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="62f3f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="62f3f-125">tooconfigure 使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="62f3f-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="62f3f-126">hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooNetsuite。</span><span class="sxs-lookup"><span data-stu-id="62f3f-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="62f3f-127">在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="62f3f-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="62f3f-128">如果您已經設定 Netsuite 的單一登入，搜尋您 Netsuite 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="62f3f-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="62f3f-129">否則，請選取**新增**並搜尋**Netsuite** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="62f3f-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="62f3f-130">從 hello 搜尋結果中，選取 Netsuite，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="62f3f-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="62f3f-131">選取您的 Netsuite，執行個體，然後選取 hello**佈建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="62f3f-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="62f3f-132">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="62f3f-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="62f3f-134">在 [hello**系統管理員認證**區段中，提供下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="62f3f-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="62f3f-135">a.</span><span class="sxs-lookup"><span data-stu-id="62f3f-135">a.</span></span> <span data-ttu-id="62f3f-136">在 hello**系統管理員使用者名稱**文字方塊中，輸入 Netsuite 帳戶名稱已 hello**系統管理員**Netsuite.com 指派中的設定檔。</span><span class="sxs-lookup"><span data-stu-id="62f3f-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="62f3f-137">b.</span><span class="sxs-lookup"><span data-stu-id="62f3f-137">b.</span></span> <span data-ttu-id="62f3f-138">在 [hello**系統管理員密碼**文字方塊中，此帳戶類型 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="62f3f-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="62f3f-139">在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Netsuite 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="62f3f-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="62f3f-140">在 [hello**通知電子郵件**欄位中，輸入 hello 電子郵件地址的個人或群組應該收到佈建錯誤通知，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="62f3f-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="62f3f-141">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="62f3f-141">Click **Save.**</span></span>

9. <span data-ttu-id="62f3f-142">在 [hello 對應區段中，選取**tooNetsuite 同步處理 Azure Active Directory 使用者。**</span><span class="sxs-lookup"><span data-stu-id="62f3f-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="62f3f-143">在 [hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooNetsuite 同步。</span><span class="sxs-lookup"><span data-stu-id="62f3f-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="62f3f-144">請注意，hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 中的使用者帳戶 Netsuite 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="62f3f-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="62f3f-145">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="62f3f-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="62f3f-146">tooenable hello Azure AD 佈建服務 netsuite，變更 hello**佈建狀態**太**上**hello 設定] 區段中</span><span class="sxs-lookup"><span data-stu-id="62f3f-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="62f3f-147">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="62f3f-147">Click **Save.**</span></span>

<span data-ttu-id="62f3f-148">它會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooNetsuite 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="62f3f-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="62f3f-149">請注意 hello 初始同步處理所花費的時間 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="62f3f-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="62f3f-150">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建您 Netsuite 的應用程式上的服務所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="62f3f-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="62f3f-151">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="62f3f-151">You can now create a test account.</span></span> <span data-ttu-id="62f3f-152">等候總 tooverify hello 帳戶已經過同步處理 tooNetsuite too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="62f3f-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62f3f-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="62f3f-153">Additional resources</span></span>

* [<span data-ttu-id="62f3f-154">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="62f3f-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62f3f-155">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="62f3f-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="62f3f-156">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="62f3f-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)