---
title: "教學課程︰在 Azure 中設定 Google Apps 來自動佈建使用者 | Microsoft Docs"
description: "了解如何將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Google Apps。"
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="4adc8-103">教學課程︰設定 Google Apps 來自動佈建使用者</span><span class="sxs-lookup"><span data-stu-id="4adc8-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="4adc8-104">本教學課程旨在說明您需要在 Google Apps 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 Google Apps。</span><span class="sxs-lookup"><span data-stu-id="4adc8-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4adc8-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="4adc8-105">Prerequisites</span></span>

<span data-ttu-id="4adc8-106">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="4adc8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4adc8-107">Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4adc8-108">您必須擁有 Google Apps for Work 或 Google Apps for Education 的有效租用戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="4adc8-109">您可以使用免費試用帳戶來使用任何服務。</span><span class="sxs-lookup"><span data-stu-id="4adc8-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="4adc8-110">Google Apps 中具有小組管理員權限的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="4adc8-111">將使用者指派給 Google Apps</span><span class="sxs-lookup"><span data-stu-id="4adc8-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="4adc8-112">Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="4adc8-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4adc8-113">在自動使用者帳戶佈建的內容中，只有「已指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="4adc8-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4adc8-114">在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 Google Apps 應用程式存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="4adc8-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="4adc8-115">一旦決定後，您可以將這些使用者指派給 Google Apps 應用程式，方法是遵循以下指示：[將使用者或群組指派給企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="4adc8-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="4adc8-116">建議將單一 Azure AD 使用者指派給 Google Apps，以測試佈建設定。</span><span class="sxs-lookup"><span data-stu-id="4adc8-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="4adc8-117">其他使用者及/或群組可能會稍後再指派。</span><span class="sxs-lookup"><span data-stu-id="4adc8-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="4adc8-118">將使用者指派給 Google Apps 時，您必須在指派對話方塊中選取 [使用者] 或 [群組] 角色。</span><span class="sxs-lookup"><span data-stu-id="4adc8-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="4adc8-119">「預設存取」角色不適用於佈建。</span><span class="sxs-lookup"><span data-stu-id="4adc8-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4adc8-120">啟用自動使用者佈建</span><span class="sxs-lookup"><span data-stu-id="4adc8-120">Enable automated user provisioning</span></span>

<span data-ttu-id="4adc8-121">本節會引導您將 Azure AD 連線至 Google Apps 的使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 Google Apps 中建立、更新和停用指派的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4adc8-122">您也可以選擇啟用 Google Apps 的 SAML 型單一登入，請遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。</span><span class="sxs-lookup"><span data-stu-id="4adc8-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4adc8-123">可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。</span><span class="sxs-lookup"><span data-stu-id="4adc8-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="4adc8-124">設定使用者帳戶自動佈建</span><span class="sxs-lookup"><span data-stu-id="4adc8-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="4adc8-125">自動化使用者佈建至 Google Apps 另一個可行的選項是使用 [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) ，這會將您的內部部署 Active Directory 身分識別佈建至 Google Apps。</span><span class="sxs-lookup"><span data-stu-id="4adc8-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="4adc8-126">但是，本教學課程中的解決方案則會將您的 Azure Active Directory (雲端) 使用者和啟用郵件功能的群組佈建至 Google Apps。</span><span class="sxs-lookup"><span data-stu-id="4adc8-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="4adc8-127">使用您的系統管理員帳戶登入 [Google Apps 管理控制台](http://admin.google.com/)，然後按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="4adc8-128">如果您沒有看到連結，它可能隱藏在畫面底部的 [其他控制項]  功能表之下。</span><span class="sxs-lookup"><span data-stu-id="4adc8-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![按一下 [安全性]。][10]

2. <span data-ttu-id="4adc8-130">在 [安全性] 頁面上，按一下 [API 參考]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![按一下 [API 參考]。][15]

3. <span data-ttu-id="4adc8-132">選取 [啟用 API 存取] 。</span><span class="sxs-lookup"><span data-stu-id="4adc8-132">Select **Enable API access**.</span></span>
   
    ![按一下 [API 參考]。][16]

    > [!IMPORTANT]
    > <span data-ttu-id="4adc8-134">對於您想要佈建至 Google Apps 的每位使用者，其使用者名稱在 Azure Active Directory 中*必須*繫結至自訂網域。</span><span class="sxs-lookup"><span data-stu-id="4adc8-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="4adc8-135">例如，Google Apps 不會接受 bob@contoso.onmicrosoft.com 這樣的使用者名稱，但是會接受 bob@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="4adc8-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="4adc8-136">您可以在 Azure AD 中編輯現有使用者的內容，來變更其網域。</span><span class="sxs-lookup"><span data-stu-id="4adc8-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="4adc8-137">下列步驟包含如何為 Azure Active Directory 與 Google Apps 兩者設定自訂網域的指示。</span><span class="sxs-lookup"><span data-stu-id="4adc8-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="4adc8-138">如果您尚未將自訂網域名稱新增至 Azure Active Directory，請按照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4adc8-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="4adc8-139">a.</span><span class="sxs-lookup"><span data-stu-id="4adc8-139">a.</span></span> <span data-ttu-id="4adc8-140">在 [Azure 入口網站](https://portal.azure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="4adc8-141">在目錄清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="4adc8-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="4adc8-142">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4adc8-142">b.</span></span> <span data-ttu-id="4adc8-143">在左方瀏覽窗格中，按一下 [網域名稱]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![新增網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="4adc8-146">c.</span><span class="sxs-lookup"><span data-stu-id="4adc8-146">c.</span></span> <span data-ttu-id="4adc8-147">在 [網域名稱]  欄位中輸入您的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4adc8-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="4adc8-148">這個網域名稱應該與您要用於 Google Apps 的網域名稱相同。</span><span class="sxs-lookup"><span data-stu-id="4adc8-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="4adc8-149">準備好時，按一下 [新增網域] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4adc8-149">When ready, click the **Add Domain** button.</span></span>
     
     ![網域名稱](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="4adc8-151">d.</span><span class="sxs-lookup"><span data-stu-id="4adc8-151">d.</span></span> <span data-ttu-id="4adc8-152">按 [下一步]  移至驗證頁面。</span><span class="sxs-lookup"><span data-stu-id="4adc8-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="4adc8-153">若要確認您擁有此網域，您必須根據此頁面提供的值，編輯網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4adc8-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="4adc8-154">您可以選擇使用 [MX 記錄] 或 [TXT 記錄] 進行確認，視您選取的 [記錄類型] 選項而定。</span><span class="sxs-lookup"><span data-stu-id="4adc8-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="4adc8-155">如需有關如何向 Azure AD 驗證網域名稱的更完整指示，請參閱[將您自己的網域名稱新增至 Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="4adc8-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="4adc8-157">e.</span><span class="sxs-lookup"><span data-stu-id="4adc8-157">e.</span></span> <span data-ttu-id="4adc8-158">對於所有您想要新增至目錄的網域，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="4adc8-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="4adc8-159">您已經向 Azure AD 驗證所有網域，但是您還必須向 Google Apps 再驗證一次。</span><span class="sxs-lookup"><span data-stu-id="4adc8-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="4adc8-160">對於尚未向 Google Apps 註冊的每個網域，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4adc8-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="4adc8-161">a.</span><span class="sxs-lookup"><span data-stu-id="4adc8-161">a.</span></span> <span data-ttu-id="4adc8-162">在 [Google Apps 管理控制台](http://admin.google.com/)中，按一下 [網域]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![按一下 [網域]][20]

    <span data-ttu-id="4adc8-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4adc8-164">b.</span></span> <span data-ttu-id="4adc8-165">按一下 [新增網域或網域別名] 。</span><span class="sxs-lookup"><span data-stu-id="4adc8-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![新增網域][21]

    <span data-ttu-id="4adc8-167">c.</span><span class="sxs-lookup"><span data-stu-id="4adc8-167">c.</span></span> <span data-ttu-id="4adc8-168">選取 [新增另一個網域] ，並輸入您想要新增的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4adc8-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![輸入您的網域名稱][22]

    <span data-ttu-id="4adc8-170">d.</span><span class="sxs-lookup"><span data-stu-id="4adc8-170">d.</span></span> <span data-ttu-id="4adc8-171">按一下 [繼續並驗證網域擁有權]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="4adc8-172">然後依照步驟以驗證您擁有網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4adc8-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="4adc8-173">如需有關如何向 Google Apps 驗證您的網域的完整指示，請參閱</span><span class="sxs-lookup"><span data-stu-id="4adc8-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="4adc8-174">[向 Google Apps 驗證網站擁有權](https://support.google.com/webmasters/answer/35179)。</span><span class="sxs-lookup"><span data-stu-id="4adc8-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="4adc8-175">e.</span><span class="sxs-lookup"><span data-stu-id="4adc8-175">e.</span></span> <span data-ttu-id="4adc8-176">對於您想要新增至 Google Apps 的任何其他網域，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="4adc8-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="4adc8-177">如果您變更 Google Apps 租用戶的主要網域，而且如果您已經使用 Azure AD 來設定單一登入，則必須重複[步驟 2：啟用單一登入](#step-two-enable-single-sign-on)下的步驟 #3。</span><span class="sxs-lookup"><span data-stu-id="4adc8-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="4adc8-178">在 [Google Apps 管理控制台](http://admin.google.com/)中，按一下 [管理角色]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![按一下 [Google Apps]][26]

7. <span data-ttu-id="4adc8-180">決定您想要用來管理使用者佈建的管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="4adc8-181">對於該帳戶的 [管理角色]，編輯該角色的 [權限]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="4adc8-182">確定它已啟用所有 [管理 API 權限]，以便讓此帳戶可以用來佈建。</span><span class="sxs-lookup"><span data-stu-id="4adc8-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![按一下 [Google Apps]][27]
   
    > [!NOTE]
    > <span data-ttu-id="4adc8-184">如果您要設定生產環境，最佳做法是特別針對此步驟在 Google Apps 中建立管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="4adc8-185">這些帳戶必須有相關聯的管理角色，該角色還要具備必要的 API 權限。</span><span class="sxs-lookup"><span data-stu-id="4adc8-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="4adc8-186">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory > 企業應用程式 > 所有應用程式] 區段。</span><span class="sxs-lookup"><span data-stu-id="4adc8-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="4adc8-187">如果您已將 Google Apps 設定為單一登入，請使用 [搜尋] 欄位搜尋您的 Google Apps 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4adc8-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="4adc8-188">否則，請選取 [新增]，並在應用程式庫中搜尋 [Google Apps]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="4adc8-189">從搜尋結果中選取 Google Apps，並將它新增至您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4adc8-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="4adc8-190">選取您的 Google Apps 執行個體，然後選取 [佈建] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4adc8-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="4adc8-191">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![佈建](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="4adc8-193">在 [系統管理員認證] 區段下，按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="4adc8-194">這會在新的瀏覽器視窗中開啟 Google Apps 授權對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4adc8-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="4adc8-195">確認您想要授與 Azure Active Directory 權限來變更您的 Google Apps 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4adc8-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="4adc8-196">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-196">Click **Accept**.</span></span>
    
     ![確認權限。][28]

14. <span data-ttu-id="4adc8-198">在 Azure 入口網站中，按一下 [測試連線]，以確保 Azure AD 可以連線至您的 Google Apps 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4adc8-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="4adc8-199">如果連線失敗，請確定您的 Google Apps 帳戶具有小組管理員權限，然後再試一次**「授權」**步驟。</span><span class="sxs-lookup"><span data-stu-id="4adc8-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="4adc8-200">在 [通知電子郵件] 欄位中，輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4adc8-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="4adc8-201">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-201">Click **Save.**</span></span>

17. <span data-ttu-id="4adc8-202">在 [對應] 區段下，選取 [同步處理 Azure Active Directory 使用者至 Google Apps]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="4adc8-203">在 [屬性對應] 區段中，檢閱從 Azure AD 同步至 Google Apps 的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="4adc8-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="4adc8-204">選取為 [比對] 屬性的屬性會用來比對 Google Apps 中的使用者帳戶，以進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="4adc8-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="4adc8-205">選取 [儲存] 按鈕以認可任何變更。</span><span class="sxs-lookup"><span data-stu-id="4adc8-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="4adc8-206">若要對 Google Apps 啟用 Azure AD 佈建服務，請在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]</span><span class="sxs-lookup"><span data-stu-id="4adc8-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="4adc8-207">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4adc8-207">Click **Save.**</span></span>

<span data-ttu-id="4adc8-208">這會對 [使用者和群組] 區段中指派給 Google Apps 的任何使用者和/或群組，啟動首次同步處理。</span><span class="sxs-lookup"><span data-stu-id="4adc8-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="4adc8-209">初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，大約每 20 分鐘便會發生一次。</span><span class="sxs-lookup"><span data-stu-id="4adc8-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="4adc8-210">您可以使用 [同步處理詳細資料] 區段來監視進度，並遵循連結來佈建活動報告，報告中會描述佈建服務在您的 Google Apps 應用程式上執行的所有動作。</span><span class="sxs-lookup"><span data-stu-id="4adc8-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4adc8-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="4adc8-211">Additional resources</span></span>

* [<span data-ttu-id="4adc8-212">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="4adc8-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4adc8-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4adc8-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4adc8-214">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="4adc8-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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