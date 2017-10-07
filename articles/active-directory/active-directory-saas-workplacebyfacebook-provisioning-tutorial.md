---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
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
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="5f1bc-103">教學課程：設定使用者佈建的 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="5f1bc-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="5f1bc-104">本教學課程 hello 目標是 tooshow hello 需要 tooperform 工作地點中的 Facebook 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooWorkplace 由 Facebook 的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f1bc-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f1bc-105">Prerequisites</span></span>

<span data-ttu-id="5f1bc-106">tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5f1bc-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="5f1bc-107">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5f1bc-107">An Azure AD subscription</span></span>
- <span data-ttu-id="5f1bc-108">已啟用 Workplace by Facebook 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5f1bc-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f1bc-109">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f1bc-110">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5f1bc-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f1bc-111">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f1bc-112">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="5f1bc-113">由 Facebook 指派的使用者 tooWorkplace</span><span class="sxs-lookup"><span data-stu-id="5f1bc-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="5f1bc-114">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5f1bc-115">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="5f1bc-116">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour 工作地點的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="5f1bc-117">一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour 工作地點的 Facebook 應用程式：</span><span class="sxs-lookup"><span data-stu-id="5f1bc-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="5f1bc-118">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="5f1bc-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="5f1bc-119">指派由 Facebook 使用者 tooWorkplace 的重要秘訣</span><span class="sxs-lookup"><span data-stu-id="5f1bc-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="5f1bc-120">建議在單一 Azure AD 使用者指派 tooWorkplace Facebook tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="5f1bc-121">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5f1bc-122">由 Facebook 使用者 tooWorkplace 指派時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="5f1bc-123">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="5f1bc-124">啟用使用者佈建</span><span class="sxs-lookup"><span data-stu-id="5f1bc-124">Enable User Provisioning</span></span>

<span data-ttu-id="5f1bc-125">本節將引導您透過 Azure AD tooWorkplace 連接 Facebook 的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用在工作地點的使用者和群組為基礎的 Facebook 指派的使用者帳戶Azure AD 中的指派。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="5f1bc-126">您也可以選擇 tooenabled SAML 型單一登入的 Facebook、 hello 指示中所提供的工作場所[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5f1bc-127">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="5f1bc-128">在 Azure AD 中佈建由 Facebook tooWorkplace tooconfigure 使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="5f1bc-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="5f1bc-129">hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="5f1bc-130">Azure AD 支援 hello 能力 tooautomatically 同步處理的 hello 帳戶詳細資料指派給使用者 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="5f1bc-131">此自動同步處理工作地點啟用 Facebook tooget hello 資料之前需要 tooauthorize 使用者進行存取，這些嘗試 toosign 中的 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="5f1bc-132">當存取在 Azure AD 中被撤銷時，它也會從 Workplace by Facebook 取消佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="5f1bc-133">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory** > **企業應用程式** > **的所有應用程式** > 一節。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="5f1bc-134">如果您已經設定工作地點的 Facebook 進行單一登入，則會搜尋執行個體的 Facebook 使用 hello 搜尋欄位中的工作場所。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="5f1bc-135">否則，請選取**新增**並搜尋**工作地點的 Facebook** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="5f1bc-136">從 hello 搜尋結果中，選取由 Facebook 的工作地點，並將它新增 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="5f1bc-137">選取您的工作地點的 Facebook、 執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="5f1bc-138">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![佈建](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="5f1bc-140">在 hello**系統管理員認證**區段中，輸入 hello 密碼語彙基元，hello Facebook 管理員工作地點的租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="5f1bc-141">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour 工作地點的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="5f1bc-142">如果 hello 連線失敗，請確定您的工作場所的 Facebook 帳戶有小組系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="5f1bc-143">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="5f1bc-144">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-144">Click **Save.**</span></span>

9. <span data-ttu-id="5f1bc-145">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooWorkplace 由 Facebook。**</span><span class="sxs-lookup"><span data-stu-id="5f1bc-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="5f1bc-146">在 hello**屬性對應**區段中，檢閱 hello 從 Azure AD tooWorkplace Facebook 會同步處理的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="5f1bc-147">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在工作地點的 Facebook 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="5f1bc-148">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="5f1bc-149">tooenable hello Azure AD 佈建服務工作場所的 Facebook、 變更 hello**佈建狀態**太**上**在 hello**設定**區段</span><span class="sxs-lookup"><span data-stu-id="5f1bc-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="5f1bc-150">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-150">Click **Save.**</span></span>

<span data-ttu-id="5f1bc-151">如需有關如何 tooconfigure 自動佈建，請參閱[https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="5f1bc-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="5f1bc-152">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-152">You can now create a test account.</span></span> <span data-ttu-id="5f1bc-153">等候總 tooverify hello 帳戶已經過同步處理由 Facebook tooWorkplace too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5f1bc-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f1bc-154">其他資源</span><span class="sxs-lookup"><span data-stu-id="5f1bc-154">Additional resources</span></span>

* [<span data-ttu-id="5f1bc-155">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="5f1bc-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f1bc-156">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5f1bc-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5f1bc-157">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="5f1bc-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

