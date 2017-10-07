---
title: "教學課程︰在 Azure 中設定 Google Apps 來自動佈建使用者 | Microsoft Docs"
description: "了解如何 tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooGoogle 應用程式。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="087f5-103">教學課程︰設定 Google Apps 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="087f5-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="087f5-104">本教學課程的 hello 目標是的 tooshow hello 您需要在 Google Apps 與 Azure AD tooautomatically 規定 tooperform 和解除佈建使用者帳戶從 Azure AD tooGoogle 應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="087f5-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="087f5-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="087f5-105">Prerequisites</span></span>

<span data-ttu-id="087f5-106">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="087f5-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="087f5-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="087f5-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="087f5-108">您必須擁有 Google Apps for Work 或 Google Apps for Education 的有效租用戶。</span><span class="sxs-lookup"><span data-stu-id="087f5-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="087f5-109">您可以使用免費試用帳戶來使用任何服務。</span><span class="sxs-lookup"><span data-stu-id="087f5-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="087f5-110">Google Apps 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="087f5-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="087f5-111">將使用者指派 tooGoogle 應用程式</span><span class="sxs-lookup"><span data-stu-id="087f5-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="087f5-112">Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。</span><span class="sxs-lookup"><span data-stu-id="087f5-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="087f5-113">在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="087f5-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="087f5-114">之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Google Apps 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="087f5-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="087f5-115">一旦決定，您可以將這些使用者 tooyour Google Apps 應用程式指派 hello 遵循指示：[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="087f5-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="087f5-116">建議在單一 Azure AD 使用者被指派 tooGoogle 應用程式 tootest hello 佈建的組態。</span><span class="sxs-lookup"><span data-stu-id="087f5-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="087f5-117">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="087f5-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="087f5-118">指派使用者 tooGoogle 應用程式時，您必須在 hello 分派 對話方塊中選取 hello 使用者或 「 群組 」 角色。</span><span class="sxs-lookup"><span data-stu-id="087f5-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="087f5-119">hello 「 預設的存取 」 角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="087f5-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="087f5-120">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="087f5-120">Enable automated user provisioning</span></span>

<span data-ttu-id="087f5-121">本節會引導您完成連接您的 Azure AD tooGoogle 應用程式的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Google Apps 中指派的使用者帳戶.</span><span class="sxs-lookup"><span data-stu-id="087f5-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="087f5-122">您也可以選擇 tooenabled SAML 型單一登入 Google 應用程式，請遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="087f5-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="087f5-123">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="087f5-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="087f5-124">設定使用者帳戶自動佈建</span><span class="sxs-lookup"><span data-stu-id="087f5-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="087f5-125">自動化使用者佈建 tooGoogle 應用程式的另一個可行選項是 toouse [Google 應用程式目錄同步處理 (GADS)](https://support.google.com/a/answer/106368?hl=en)的佈建您的內部部署 Active Directory 身分識別 tooGoogle 應用程式。</span><span class="sxs-lookup"><span data-stu-id="087f5-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="087f5-126">相反地，在此教學課程中的 hello 方案佈建您的 Azure Active Directory （雲端） 使用者和群組已啟用郵件 tooGoogle 應用程式。</span><span class="sxs-lookup"><span data-stu-id="087f5-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="087f5-127">登入 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)使用您的系統管理員帳戶，然後按一下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="087f5-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="087f5-128">如果您沒有看到 hello 連結，它可能會隱藏在 hello**其他控制項**功能表底部 hello 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="087f5-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![按一下 [安全性]。][10]

2. <span data-ttu-id="087f5-130">在 hello**安全性**頁面上，按一下**API 參考**。</span><span class="sxs-lookup"><span data-stu-id="087f5-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![按一下 [API 參考]。][15]

3. <span data-ttu-id="087f5-132">選取 [啟用 API 存取] 。</span><span class="sxs-lookup"><span data-stu-id="087f5-132">Select **Enable API access**.</span></span>
   
    ![按一下 [API 參考]。][16]

    > [!IMPORTANT]
    > <span data-ttu-id="087f5-134">針對您想 tooprovision tooGoogle 應用程式，其使用者名稱在 Azure Active Directory 中的每個使用者*必須*是 tooa 繫結的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="087f5-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="087f5-135">例如，Google Apps 不會接受 bob@contoso.onmicrosoft.com 這樣的使用者名稱，但是會接受 bob@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="087f5-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="087f5-136">您可以在 Azure AD 中編輯現有使用者的內容，來變更其網域。</span><span class="sxs-lookup"><span data-stu-id="087f5-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="087f5-137">指示 tooset Azure Active Directory 與 Google Apps 的自訂網域如何在中包含下列步驟。</span><span class="sxs-lookup"><span data-stu-id="087f5-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="087f5-138">如果您尚未加入自訂網域名稱 tooyour Azure Active Directory，然後依照下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="087f5-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="087f5-139">a.</span><span class="sxs-lookup"><span data-stu-id="087f5-139">a.</span></span> <span data-ttu-id="087f5-140">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="087f5-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="087f5-141">在 hello 目錄清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="087f5-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="087f5-142">b.</span><span class="sxs-lookup"><span data-stu-id="087f5-142">b.</span></span> <span data-ttu-id="087f5-143">按一下**網域名稱**在 hello 左側瀏覽窗格，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="087f5-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![新增網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="087f5-146">c.</span><span class="sxs-lookup"><span data-stu-id="087f5-146">c.</span></span> <span data-ttu-id="087f5-147">您的網域名稱輸入 hello**網域名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="087f5-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="087f5-148">此網域名稱應該是 hello 想要 Google Apps toouse 相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="087f5-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="087f5-149">準備就緒時，按一下 hello**新增網域** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="087f5-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![網域名稱](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="087f5-151">d.</span><span class="sxs-lookup"><span data-stu-id="087f5-151">d.</span></span> <span data-ttu-id="087f5-152">按一下**下一步**toogo toohello 驗證 頁面。</span><span class="sxs-lookup"><span data-stu-id="087f5-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="087f5-153">tooverify 您擁有此網域，您必須編輯根據 toohello 值在此頁面提供的 hello 網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="087f5-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="087f5-154">您可以選擇使用 tooverify **MX 記錄**或**TXT 記錄**，視您選取的 hello**記錄類型**選項。</span><span class="sxs-lookup"><span data-stu-id="087f5-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="087f5-155">如需有關如何 tooverify 網域名稱與 Azure AD 的更完整指示，請參閱[加入您自己的網域名稱 tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="087f5-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="087f5-157">e.</span><span class="sxs-lookup"><span data-stu-id="087f5-157">e.</span></span> <span data-ttu-id="087f5-158">重複上述步驟，針對您想 tooadd tooyour 目錄的所有 hello 定義域 hello。</span><span class="sxs-lookup"><span data-stu-id="087f5-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="087f5-159">您已經向 Azure AD 驗證所有網域，但是您還必須向 Google Apps 再驗證一次。</span><span class="sxs-lookup"><span data-stu-id="087f5-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="087f5-160">未與 Google Apps 註冊每個網域，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="087f5-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="087f5-161">a.</span><span class="sxs-lookup"><span data-stu-id="087f5-161">a.</span></span> <span data-ttu-id="087f5-162">在 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)，按一下 **網域**。</span><span class="sxs-lookup"><span data-stu-id="087f5-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![按一下 [網域]][20]

    <span data-ttu-id="087f5-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="087f5-164">b.</span></span> <span data-ttu-id="087f5-165">按一下 [新增網域或網域別名] 。</span><span class="sxs-lookup"><span data-stu-id="087f5-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![新增網域][21]

    <span data-ttu-id="087f5-167">c.</span><span class="sxs-lookup"><span data-stu-id="087f5-167">c.</span></span> <span data-ttu-id="087f5-168">選取**新增另一個網域**，然後輸入您想要 tooadd hello 網域之 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="087f5-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![輸入您的網域名稱][22]

    <span data-ttu-id="087f5-170">d.</span><span class="sxs-lookup"><span data-stu-id="087f5-170">d.</span></span> <span data-ttu-id="087f5-171">按一下 [繼續並驗證網域擁有權]。</span><span class="sxs-lookup"><span data-stu-id="087f5-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="087f5-172">然後，遵循 hello 步驟 tooverify 您擁有 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="087f5-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="087f5-173">如需如何 tooverify 與 Google Apps 網域查看全方位指示。</span><span class="sxs-lookup"><span data-stu-id="087f5-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="087f5-174">[向 Google Apps 驗證網站擁有權](https://support.google.com/webmasters/answer/35179)。</span><span class="sxs-lookup"><span data-stu-id="087f5-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="087f5-175">e.</span><span class="sxs-lookup"><span data-stu-id="087f5-175">e.</span></span> <span data-ttu-id="087f5-176">重複上述步驟，針對您想 tooadd tooGoogle 應用程式的任何其他網域的 hello。</span><span class="sxs-lookup"><span data-stu-id="087f5-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="087f5-177">如果您變更您的 Google Apps 租用戶 hello 主要網域，而且如果已經設定單一登入與 Azure AD，則有 toorepeat 步驟 #3 下的[兩個步驟： 啟用單一登入](#step-two-enable-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="087f5-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="087f5-178">在 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)，按一下 **系統管理員角色**。</span><span class="sxs-lookup"><span data-stu-id="087f5-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![按一下 [Google Apps]][26]

7. <span data-ttu-id="087f5-180">判斷哪一個系統管理員希望 toouse toomanage 使用者佈建的帳戶。</span><span class="sxs-lookup"><span data-stu-id="087f5-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="087f5-181">Hello**系統管理員角色**該帳戶中，編輯 hello**權限**該角色。</span><span class="sxs-lookup"><span data-stu-id="087f5-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="087f5-182">請確定它擁有所有 hello**管理員 API 的權限**啟用，所以此帳戶可以用於佈建。</span><span class="sxs-lookup"><span data-stu-id="087f5-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![按一下 [Google Apps]][27]
   
    > [!NOTE]
    > <span data-ttu-id="087f5-184">如果您要設定的實際執行環境，hello 最佳作法是 toocreate Google Apps 中系統管理員帳戶，特別針對此步驟。</span><span class="sxs-lookup"><span data-stu-id="087f5-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="087f5-185">這些帳戶必須具備 hello 必要 API 權限系統管理員角色與其相關聯。</span><span class="sxs-lookup"><span data-stu-id="087f5-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="087f5-186">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="087f5-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="087f5-187">如果您已經設定 Google Apps 的單一登入，搜尋您的 Google Apps 使用 hello 搜尋欄位中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="087f5-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="087f5-188">否則，請選取**新增**並搜尋**Google Apps** hello 應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="087f5-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="087f5-189">從 hello 搜尋結果中，選取 Google Apps，並將它加入 tooyour 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="087f5-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="087f5-190">選取您的 Google Apps 的執行個體，然後選取 hello**佈建** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="087f5-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="087f5-191">設定 hello**佈建模式**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="087f5-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![佈建](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="087f5-193">在 hello**系統管理員認證**區段中，按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="087f5-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="087f5-194">這會在新的瀏覽器視窗中開啟 Google Apps 授權對話方塊。</span><span class="sxs-lookup"><span data-stu-id="087f5-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="087f5-195">確認您想要 toogive Azure Active Directory 權限 toomake 變更 tooyour Google Apps 租用戶。</span><span class="sxs-lookup"><span data-stu-id="087f5-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="087f5-196">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="087f5-196">Click **Accept**.</span></span>
    
     ![確認權限。][28]

14. <span data-ttu-id="087f5-198">在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Google Apps 的應用程式可以連接。</span><span class="sxs-lookup"><span data-stu-id="087f5-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="087f5-199">如果 hello 連線失敗，請確定您的 Google Apps 帳戶已小組系統管理員權限，然後再次嘗試 hello **「 授權 」**步驟一次。</span><span class="sxs-lookup"><span data-stu-id="087f5-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="087f5-200">輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="087f5-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="087f5-201">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="087f5-201">Click **Save.**</span></span>

17. <span data-ttu-id="087f5-202">在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooGoogle 應用程式。**</span><span class="sxs-lookup"><span data-stu-id="087f5-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="087f5-203">在 hello**屬性對應**區段中，檢閱已從 Azure AD tooGoogle 應用程式同步處理的 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="087f5-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="087f5-204">hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Google Apps 中進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="087f5-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="087f5-205">選取 hello 儲存按鈕 toocommit 任何變更。</span><span class="sxs-lookup"><span data-stu-id="087f5-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="087f5-206">tooenable hello Azure AD 佈建服務，針對 Google 應用程式，變更 hello**佈建狀態**太**上**hello 設定 區段中</span><span class="sxs-lookup"><span data-stu-id="087f5-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="087f5-207">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="087f5-207">Click **Save.**</span></span>

<span data-ttu-id="087f5-208">啟動 hello 初始同步處理的任何使用者和/或群組指派 tooGoogle hello 使用者和群組 > 一節中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="087f5-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="087f5-209">hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。</span><span class="sxs-lookup"><span data-stu-id="087f5-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="087f5-210">您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Google Apps 的應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="087f5-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="087f5-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="087f5-211">Additional resources</span></span>

* [<span data-ttu-id="087f5-212">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="087f5-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="087f5-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="087f5-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="087f5-214">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="087f5-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png