---
title: "教學課程：Azure Active Directory 與 Jive 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Jive 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="f3a3f-103">教學課程：設定 Jive 來佈建使用者</span><span class="sxs-lookup"><span data-stu-id="f3a3f-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="f3a3f-104">本教學課程的 hello 目標是 tooshow hello 您需要在 Jive 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooJive tooperform 的步驟。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3a3f-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="f3a3f-105">Prerequisites</span></span>

<span data-ttu-id="f3a3f-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="f3a3f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="f3a3f-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f3a3f-108">啟用 Jive 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="f3a3f-109">Jive 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="f3a3f-110">指派使用者 tooJive</span><span class="sxs-lookup"><span data-stu-id="f3a3f-110">Assigning users tooJive</span></span>

<span data-ttu-id="f3a3f-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="f3a3f-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="f3a3f-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Jive 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="f3a3f-114">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Jive 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f3a3f-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="f3a3f-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="f3a3f-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="f3a3f-116">指派使用者 tooJive 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a3f-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="f3a3f-117">建議在單一 Azure AD 使用者被指派 tooJive tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="f3a3f-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f3a3f-119">指派使用者 tooJive 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="f3a3f-120">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="f3a3f-121">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="f3a3f-121">Enable User Provisioning</span></span>

<span data-ttu-id="f3a3f-122">本節會引導您完成連接您的 Azure AD tooJive 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Jive 中指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="f3a3f-123">您也可以選擇 SAML 型單一登入 jive，遵循所提供的 hello 指示 tooenabled [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f3a3f-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="f3a3f-125">tooconfigure 使用者帳戶佈建：</span><span class="sxs-lookup"><span data-stu-id="f3a3f-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="f3a3f-126">hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooJive。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="f3a3f-127">此程序的一部分，您就需要的 tooprovide 需要向 Jive.com toorequest 的使用者安全性 token。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="f3a3f-128">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="f3a3f-129">如果您已經設定進行單一登入 Jive，搜尋您的 Jive 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="f3a3f-130">否則，請選取**新增**並搜尋**Jive** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="f3a3f-131">從 hello 搜尋結果中，選取 Jive，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="f3a3f-132">選取您的 Jive，執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="f3a3f-133">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="f3a3f-135">在 hello**系統管理員認證**區段中，提供下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3a3f-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="f3a3f-136">a.</span><span class="sxs-lookup"><span data-stu-id="f3a3f-136">a.</span></span> <span data-ttu-id="f3a3f-137">在 hello **Jive 管理使用者名稱**文字方塊中，輸入 Jive 帳戶名稱已 hello**系統管理員**在 Jive.com 中的設定檔。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="f3a3f-138">b.</span><span class="sxs-lookup"><span data-stu-id="f3a3f-138">b.</span></span> <span data-ttu-id="f3a3f-139">在 hello **Jive 管理密碼**文字方塊中，此帳戶類型 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="f3a3f-140">c.</span><span class="sxs-lookup"><span data-stu-id="f3a3f-140">c.</span></span> <span data-ttu-id="f3a3f-141">在 hello **Jive 租用戶 URL**文字方塊中，型別 hello Jive 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f3a3f-142">hello Jive 租用戶 URL 是由您的組織 toolog tooJive 中的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="f3a3f-143">一般而言，hello URL 具有下列格式的 hello: **www。\<組織\>。 jive.com**。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="f3a3f-144">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Jive 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="f3a3f-145">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="f3a3f-146">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-146">Click **Save.**</span></span>

9. <span data-ttu-id="f3a3f-147">在 hello 對應區段中，選取**tooJive 同步處理 Azure Active Directory 使用者。**</span><span class="sxs-lookup"><span data-stu-id="f3a3f-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="f3a3f-148">在 hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooJive 同步。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="f3a3f-149">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶 Jive 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="f3a3f-150">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="f3a3f-151">tooenable hello Azure AD 佈建服務 jive，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="f3a3f-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="f3a3f-152">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-152">Click **Save.**</span></span>

<span data-ttu-id="f3a3f-153">它會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooJive 在 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="f3a3f-154">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="f3a3f-155">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Jive 的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="f3a3f-156">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-156">You can now create a test account.</span></span> <span data-ttu-id="f3a3f-157">等候總 tooverify hello 帳戶已經過同步處理 tooJive too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f3a3f-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3a3f-158">其他資源</span><span class="sxs-lookup"><span data-stu-id="f3a3f-158">Additional resources</span></span>

* [<span data-ttu-id="f3a3f-159">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="f3a3f-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3a3f-160">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f3a3f-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f3a3f-161">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="f3a3f-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)