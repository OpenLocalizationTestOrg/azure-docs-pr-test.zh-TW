---
title: "教學課程：Azure Active Directory 與 Dropbox for Business 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 dropbox 企業版之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="b7fd8-103">教學課程︰設定自動使用者佈建的 Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="b7fd8-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="b7fd8-104">本教學課程的 hello 目標是 tooshow hello 商務需要在 Dropbox tooperform 商務和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooDropbox 步驟。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7fd8-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="b7fd8-105">Prerequisites</span></span>

<span data-ttu-id="b7fd8-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="b7fd8-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b7fd8-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b7fd8-108">已啟用 Dropbox for Business 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b7fd8-109">具有小組系統管理員權限的 Dropbox for Business 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="b7fd8-110">指派使用者 tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="b7fd8-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="b7fd8-111">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b7fd8-112">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b7fd8-113">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取商務應用程式的 tooyour Dropbox。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="b7fd8-114">一旦決定，您可以指派商務應用程式中的使用這些使用者 tooyour Dropbox hello 遵循指示：</span><span class="sxs-lookup"><span data-stu-id="b7fd8-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="b7fd8-115">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fd8-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="b7fd8-116">指派使用者 tooDropbox 商務的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="b7fd8-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="b7fd8-117">建議在單一 tooDropbox 商務 tootest hello 佈建組態指派給 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="b7fd8-118">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b7fd8-119">指派使用者 tooDropbox 商務時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="b7fd8-120">hello 「 預設的存取 」 角色不適用於佈建...</span><span class="sxs-lookup"><span data-stu-id="b7fd8-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b7fd8-121">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="b7fd8-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="b7fd8-122">本節會引導您完成連接您的 Azure AD tooDropbox 公司的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 在 Dropbox 企業版使用者和群組為基礎的指派的使用者帳戶Azure AD 中的指派。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b7fd8-123">您也可以選擇 tooenabled SAML 型單一登入 dropbox 企業，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b7fd8-124">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="b7fd8-125">tooconfigure 自動帳戶佈建使用者：</span><span class="sxs-lookup"><span data-stu-id="b7fd8-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="b7fd8-126">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b7fd8-127">如果您已經設定進行單一登入 dropbox 企業版，搜尋您的 Dropbox 企業版使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="b7fd8-128">否則，請選取**新增**並搜尋**dropbox 企業版**hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="b7fd8-129">從 hello 搜尋結果中，選取 dropbox 企業版，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b7fd8-130">選取您的 Dropbox 企業版，執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b7fd8-131">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b7fd8-133">在 hello**系統管理員認證**區段中，按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="b7fd8-134">會在新的瀏覽器視窗中開啟 Dropbox for Business 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="b7fd8-135">在 [hello**登入 tooDropbox toolink 與 Azure AD** ] 對話方塊中，登入 tooyour Dropbox 企業版租用戶。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="b7fd8-136">![使用者佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="b7fd8-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="b7fd8-137">確認您想要 toogive Azure Active Directory 權限 toomake 變更 tooyour Dropbox 企業版租用戶。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="b7fd8-138">按一下 [允許]。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="b7fd8-139">![使用者佈建](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="b7fd8-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="b7fd8-140">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour Dropbox 商務應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="b7fd8-141">如果 hello 連線失敗，請確定您的 Dropbox 企業帳戶有小組系統管理員權限，然後再次嘗試 hello **「 授權 」**步驟一次。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="b7fd8-142">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="b7fd8-143">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-143">Click **Save.**</span></span>

11. <span data-ttu-id="b7fd8-144">在 hello 對應區段中，選取**商務的同步處理 Azure Active Directory 使用者 tooDropbox。**</span><span class="sxs-lookup"><span data-stu-id="b7fd8-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="b7fd8-145">在 hello**屬性對應**區段中，檢閱 hello 商務從 Azure AD tooDropbox 同步的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="b7fd8-146">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 dropbox 企業版進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="b7fd8-147">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="b7fd8-148">tooenable hello Azure AD 佈建服務的 Dropbox 企業版，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="b7fd8-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="b7fd8-149">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-149">Click **Save.**</span></span>

<span data-ttu-id="b7fd8-150">它會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooDropbox 商務中 hello 使用者和群組 > 一節。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="b7fd8-151">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b7fd8-152">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建服務在您的 Dropbox 企業營運應用程式所執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="b7fd8-153">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-153">You can now create a test account.</span></span> <span data-ttu-id="b7fd8-154">等候總 tooverify hello 帳戶已經過同步處理商務 tooDropbox too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="b7fd8-155">成功完成的使用者佈建週期會以相關狀態表示。</span><span class="sxs-lookup"><span data-stu-id="b7fd8-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="b7fd8-156">![指派使用者](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="b7fd8-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b7fd8-157">其他資源</span><span class="sxs-lookup"><span data-stu-id="b7fd8-157">Additional resources</span></span>

* [<span data-ttu-id="b7fd8-158">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="b7fd8-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7fd8-159">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b7fd8-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b7fd8-160">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="b7fd8-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)