---
title: "教學課程：Azure Active Directory 與 Coupa 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Coupa 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="3f775-103">教學課程：Azure Active Directory 與 Coupa 整合</span><span class="sxs-lookup"><span data-stu-id="3f775-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="3f775-104">本教學課程的 hello 目標是 Azure 與 Coupa tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="3f775-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="3f775-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="3f775-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="3f775-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="3f775-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3f775-107">已啟用 Coupa 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f775-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="3f775-108">完成本教學課程之後, 您已指派 tooCoupa hello Azure AD 使用者將無法 toosingle 登入 hello 應用程式使用 hello[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3f775-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3f775-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f775-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="3f775-110">啟用 Coupa 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="3f775-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="3f775-111">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="3f775-111">Configuring single sign-on</span></span>
* <span data-ttu-id="3f775-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="3f775-112">Configuring user provisioning</span></span>
* <span data-ttu-id="3f775-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="3f775-113">Assigning users</span></span>

<span data-ttu-id="3f775-114">![案例](./media/active-directory-saas-coupa-tutorial/IC791897.png "案例")</span><span class="sxs-lookup"><span data-stu-id="3f775-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="3f775-115">啟用 Coupa 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="3f775-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="3f775-116">本節 hello 目標是 toooutline 如何 Coupa tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="3f775-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="3f775-117">**tooenable hello 應用程式整合 Coupa 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3f775-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f775-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="3f775-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3f775-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3f775-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3f775-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="3f775-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="3f775-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="3f775-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="3f775-122">![應用程式](./media/active-directory-saas-coupa-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="3f775-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3f775-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="3f775-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="3f775-124">![新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="3f775-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3f775-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3f775-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="3f775-126">![從資源庫新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="3f775-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3f775-127">在 hello**搜尋方塊**，型別**Coupa**。</span><span class="sxs-lookup"><span data-stu-id="3f775-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="3f775-128">![應用程式資源庫](./media/active-directory-saas-coupa-tutorial/IC791898.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="3f775-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="3f775-129">在 hello 結果窗格中，選取  **Coupa**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f775-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="3f775-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="3f775-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3f775-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="3f775-131">Configure single sign-on</span></span>

<span data-ttu-id="3f775-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCoupa 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="3f775-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="3f775-133">設定單一登入 coupa 需要 tooretrieve 從憑證的指紋值。</span><span class="sxs-lookup"><span data-stu-id="3f775-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="3f775-134">如果您不熟悉這個程序，請參閱[如何 tooretrieve 憑證的指紋值](http://youtu.be/YKQF266SAxI)。</span><span class="sxs-lookup"><span data-stu-id="3f775-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="3f775-135">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3f775-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f775-136">登入 tooyour Coupa 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="3f775-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="3f775-137">跳過**安裝\>安全性控制**。</span><span class="sxs-lookup"><span data-stu-id="3f775-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="3f775-138">![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="3f775-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="3f775-139">toodownload hello Coupa 中繼資料檔案 tooyour，請按一下**下載並匯入 SP 中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="3f775-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="3f775-140">![Coupa 預存程序中繼資料](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa 預存程序中繼資料")</span><span class="sxs-lookup"><span data-stu-id="3f775-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="3f775-141">在不同的瀏覽器視窗中，登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="3f775-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="3f775-142">在 hello **Coupa**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3f775-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3f775-143">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791902.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3f775-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="3f775-144">在 hello**如何想您使用者 toosign tooCoupa 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3f775-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3f775-145">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791903.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3f775-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="3f775-146">在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f775-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="3f775-147">![設定應用程式 URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="3f775-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="3f775-148">在 hello**登入 URL**文字方塊中，您的使用者 toosign 上 tooyour Coupa 的應用程式所使用的型別 URL (例如:"*http://company.Coupa.com*")。</span><span class="sxs-lookup"><span data-stu-id="3f775-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="3f775-149">開啟您下載的 Coupa 中繼資料檔案，然後複製 hello **AssertionConsumerService index/URL**。</span><span class="sxs-lookup"><span data-stu-id="3f775-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="3f775-150">在 hello **coupa 轉送 URL**文字方塊中，貼上 hello **AssertionConsumerService index/URL**值。</span><span class="sxs-lookup"><span data-stu-id="3f775-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="3f775-151">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3f775-151">Click **Next**.</span></span>
8. <span data-ttu-id="3f775-152">在 hello**在 Coupa 設定單一登入**頁面、 toodownload 中繼資料檔案，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3f775-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="3f775-153">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791905.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3f775-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="3f775-154">Hello Coupa 公司網站上，前往 太**安裝\>安全性控制**。</span><span class="sxs-lookup"><span data-stu-id="3f775-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="3f775-155">![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="3f775-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="3f775-156">在 hello**使用 Coupa 認證登入**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f775-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="3f775-157">![使用 Coupa 認證登入](./media/active-directory-saas-coupa-tutorial/IC791906.png "使用 Coupa 認證登入")</span><span class="sxs-lookup"><span data-stu-id="3f775-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="3f775-158">選取 [使用 SAML 登入] 。</span><span class="sxs-lookup"><span data-stu-id="3f775-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="3f775-159">按一下**瀏覽**tooupload 您下載的 Azure Active 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3f775-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="3f775-160">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3f775-160">Click **Save**.</span></span>
11. <span data-ttu-id="3f775-161">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3f775-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="3f775-162">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791907.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3f775-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="3f775-163">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="3f775-163">Configure user provisioning</span></span>

<span data-ttu-id="3f775-164">在訂單 tooenable Azure AD 使用者 toolog 入 Coupa，它們必須佈建到 Coupa。</span><span class="sxs-lookup"><span data-stu-id="3f775-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="3f775-165">在 Coupa 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="3f775-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="3f775-166">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3f775-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f775-167">登入 tooyour **Coupa**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="3f775-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="3f775-168">在 hello 最上層顯示 hello 功能表上，按一下**安裝**，然後按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="3f775-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="3f775-169">![使用者](./media/active-directory-saas-coupa-tutorial/IC791908.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="3f775-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="3f775-170">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f775-170">Click **Create**.</span></span>
   
   <span data-ttu-id="3f775-171">![建立使用者](./media/active-directory-saas-coupa-tutorial/IC791909.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="3f775-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="3f775-172">在 hello**使用者建立**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f775-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3f775-173">![使用者詳細資料](./media/active-directory-saas-coupa-tutorial/IC791910.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="3f775-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="3f775-174">型別 hello**登入**，**名字**，**姓氏**，**單一登入識別碼**，**電子郵件**屬性您想 tooprovision 寫入 hello 的有效 Azure Active Directory 帳戶相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3f775-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="3f775-175">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f775-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="3f775-176">hello Azure Active Directory 帳戶持有者會收到含有連結 tooconfirm hello 帳戶的電子郵件之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="3f775-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="3f775-177">您可以使用任何其他 Coupa 使用者帳戶建立工具或 Api 提供 Coupa tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f775-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="3f775-178">指派使用者</span><span class="sxs-lookup"><span data-stu-id="3f775-178">Assign users</span></span>
<span data-ttu-id="3f775-179">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="3f775-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="3f775-180">**tooassign 使用者 tooCoupa，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3f775-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f775-181">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f775-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3f775-182">在 hello * * Coupa * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="3f775-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3f775-183">![指派使用者](./media/active-directory-saas-coupa-tutorial/IC791911.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="3f775-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="3f775-184">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="3f775-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="3f775-185">![是](./media/active-directory-saas-coupa-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="3f775-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3f775-186">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3f775-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="3f775-187">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3f775-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

