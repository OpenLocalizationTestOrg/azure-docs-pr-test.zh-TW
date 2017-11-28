---
title: "教學課程：設定使用者佈建的 Workplace by Facebook | Microsoft Docs"
description: "了解如何 tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooWorkplace 由 Facebook。"
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="9e05e-103">教學課程：設定使用者佈建的 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="9e05e-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="9e05e-104">此教學課程會顯示 hello 步驟需要 tooautomatically 佈建和解除佈建的 Azure Active Directory (Azure AD) tooWorkplace 由 Facebook 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e05e-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e05e-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e05e-105">Prerequisites</span></span>

<span data-ttu-id="9e05e-106">tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9e05e-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="9e05e-107">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e05e-107">An Azure AD subscription</span></span>
- <span data-ttu-id="9e05e-108">已啟用 Workplace by Facebook (SSO) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e05e-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9e05e-109">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="9e05e-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9e05e-110">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9e05e-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e05e-111">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9e05e-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="9e05e-112">指派由 Facebook 使用者 tooWorkplace</span><span class="sxs-lookup"><span data-stu-id="9e05e-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="9e05e-113">Azure AD 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="9e05e-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9e05e-114">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已指派 Azure AD 中的 tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e05e-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9e05e-115">設定及啟用 hello 佈建服務，決定哪些使用者和群組在 Azure AD 中之前代表 hello 使用者需要存取 tooyour 工作地點的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e05e-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9e05e-116">然後您可以指派這些使用者 tooyour 工作地點的 Facebook 應用程式遵循 hello 中的指示[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="9e05e-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="9e05e-117">藉由指派單一佈建組態的測試 hello Azure AD 使用者 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="9e05e-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="9e05e-118">稍後指派額外的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="9e05e-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="9e05e-119">當您將指派由 Facebook 使用者 tooWorkplace 時，您必須選取有效的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="9e05e-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="9e05e-120">hello 預設存取角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="9e05e-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9e05e-121">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="9e05e-121">Enable automated user provisioning</span></span>

<span data-ttu-id="9e05e-122">本節將引導您完成連線 Azure AD toohello 使用者帳戶佈建應用程式開發介面的工作地點的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="9e05e-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="9e05e-123">此外，您也會學習如何 tooconfigure hello 佈建服務 toocreate、 更新和停用在工作地點的 Facebook 指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e05e-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="9e05e-124">這是以 Azure AD 中的使用者和群組指派為基礎。</span><span class="sxs-lookup"><span data-stu-id="9e05e-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9e05e-125">您也可以選擇 tooenabled SAML 單一登入工作場所的 Facebook，藉由遵循 hello 中提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9e05e-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9e05e-126">您可以獨立設定自動佈建的 SSO，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="9e05e-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="9e05e-127">設定 Azure AD 中佈建 tooWorkplace 由 Facebook 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="9e05e-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="9e05e-128">Azure AD 支援 hello 能力 tooautomatically 同步處理的 hello 帳戶詳細資料指派給使用者 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="9e05e-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="9e05e-129">此自動同步處理工作地點啟用 Facebook tooget hello 資料之前需要 tooauthorize 使用者進行存取，這些嘗試 toosign 中的 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="9e05e-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="9e05e-130">當存取在 Azure AD 中被撤銷時，它也會從 Workplace by Facebook 取消佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="9e05e-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="9e05e-131">在 hello [Azure 入口網站](https://portal.azure.com)，選取**Azure Active Directory** > **企業應用程式** > **所有應用程式**.</span><span class="sxs-lookup"><span data-stu-id="9e05e-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="9e05e-132">如果您已經為 SSO 設定由 Facebook 的工作場所，請利用 hello 搜尋欄位中搜尋執行個體的 Facebook 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="9e05e-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="9e05e-133">否則，請選取**新增**並搜尋**工作地點的 Facebook** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="9e05e-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="9e05e-134">選取**工作地點的 Facebook** hello 從搜尋結果，並將它加入 tooyour 的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="9e05e-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9e05e-135">選取您的工作地點的 Facebook、 執行個體，然後選取 [hello**佈建**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9e05e-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9e05e-136">設定**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="9e05e-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Workplace by Facebook 佈建選項的螢幕擷取畫面](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9e05e-138">在 hello**系統管理員認證**區段中，輸入 hello**密碼語彙基元**和 hello**租用戶 URL** Facebook 管理員工作地點。</span><span class="sxs-lookup"><span data-stu-id="9e05e-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="9e05e-139">在 hello Azure 入口網站，選取 **測試連接**tooensure Azure AD 可連接 tooyour 工作地點的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e05e-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9e05e-140">如果 hello 連線失敗，請確定您的工作場所的 Facebook 帳戶具有小組系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="9e05e-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="9e05e-141">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，然後 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="9e05e-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="9e05e-142">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9e05e-142">Select **Save**.</span></span>

9. <span data-ttu-id="9e05e-143">在 hello 對應區段中，選取**由 Facebook 的同步處理 Azure Active Directory 使用者 tooWorkplace**。</span><span class="sxs-lookup"><span data-stu-id="9e05e-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="9e05e-144">在 hello**屬性對應**區段中，檢閱 hello 從 Azure AD tooWorkplace Facebook 會同步處理的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="9e05e-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="9e05e-145">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在工作地點的 Facebook 進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="9e05e-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="9e05e-146">任何變更，請選取 toocommit**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9e05e-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="9e05e-147">tooenable hello Azure AD 佈建服務的 Facebook 的工作場所中 hello**設定**區段中，變更 hello**佈建狀態**太**上**。</span><span class="sxs-lookup"><span data-stu-id="9e05e-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="9e05e-148">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9e05e-148">Select **Save**.</span></span>

<span data-ttu-id="9e05e-149">如需有關如何 tooconfigure 自動佈建，請參閱[hello Facebook 文件](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)。</span><span class="sxs-lookup"><span data-stu-id="9e05e-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="9e05e-150">您現在可以建立測試帳戶了。</span><span class="sxs-lookup"><span data-stu-id="9e05e-150">You can now create a test account.</span></span> <span data-ttu-id="9e05e-151">等候總 tooverify hello 帳戶已經過同步處理由 Facebook tooWorkplace too20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9e05e-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e05e-152">其他資源</span><span class="sxs-lookup"><span data-stu-id="9e05e-152">Additional resources</span></span>

* [<span data-ttu-id="9e05e-153">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="9e05e-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e05e-154">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9e05e-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9e05e-155">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="9e05e-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

