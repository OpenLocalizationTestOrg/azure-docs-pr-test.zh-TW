---
title: "教學課程：Azure Active Directory 與 Replicon 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Replicon 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="b752e-103">教學課程：Azure Active Directory 與 Replicon 整合</span><span class="sxs-lookup"><span data-stu-id="b752e-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="b752e-104">本教學課程的 hello 目標是 Azure 與 Replicon tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="b752e-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="b752e-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="b752e-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="b752e-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="b752e-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b752e-107">Replicon 租用戶</span><span class="sxs-lookup"><span data-stu-id="b752e-107">A Replicon tenant</span></span>

<span data-ttu-id="b752e-108">完成本教學課程之後, 您已指派 tooReplicon hello Azure AD 使用者將能夠 toosingle 登入位於您 Replicon 公司網站 （服務提供者起始登入），或使用 hello 的 hello 應用程式[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b752e-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="b752e-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b752e-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="b752e-110">啟用 Replicon 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="b752e-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="b752e-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="b752e-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b752e-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="b752e-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="b752e-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="b752e-113">Assigning users</span></span>

<span data-ttu-id="b752e-114">![案例](./media/active-directory-saas-replicon-tutorial/IC777798.png "案例")</span><span class="sxs-lookup"><span data-stu-id="b752e-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="b752e-115">啟用 Replicon 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="b752e-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="b752e-116">本節 hello 目標是 toooutline 如何 Replicon tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="b752e-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="b752e-117">**tooenable hello 應用程式整合 Replicon 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b752e-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="b752e-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="b752e-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="b752e-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b752e-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b752e-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="b752e-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="b752e-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="b752e-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="b752e-122">![應用程式](./media/active-directory-saas-replicon-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="b752e-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b752e-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="b752e-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="b752e-124">![新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="b752e-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="b752e-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b752e-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="b752e-126">![從資源庫新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="b752e-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="b752e-127">在 hello**搜尋方塊**，型別**Replicon**。</span><span class="sxs-lookup"><span data-stu-id="b752e-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="b752e-128">![應用程式資源庫](./media/active-directory-saas-replicon-tutorial/IC777799.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="b752e-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="b752e-129">在 hello 結果窗格中，選取  **Replicon**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b752e-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="b752e-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="b752e-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="b752e-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="b752e-131">Configure single sign-on</span></span>

<span data-ttu-id="b752e-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooReplicon 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="b752e-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="b752e-133">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b752e-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="b752e-134">在 Azure 傳統入口網站，在 hello hello **Replicon**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b752e-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b752e-135">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777801.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="b752e-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="b752e-136">在 hello**如何想您使用者 toosign tooReplicon 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b752e-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b752e-137">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777802.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="b752e-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="b752e-138">在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b752e-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b752e-139">![設定應用程式 URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="b752e-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="b752e-140">在 hello **Replicon 登入 URL**文字方塊中，輸入 Replicon 租用戶 URL (例如： *https://na2.replicon.com/company/saml2/sp-sso/post*)。</span><span class="sxs-lookup"><span data-stu-id="b752e-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="b752e-141">在 hello **Replicon 回覆 URL**文字方塊中，輸入 Replicon **AssertionConsumerService** URL (例如： *https://global.replicon.com/ ！saml2/公司/sso/post/*)。</span><span class="sxs-lookup"><span data-stu-id="b752e-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="b752e-142">您可以從 hello Replicon 中繼資料取得 hello URL: **https://global.replicon.com/ ！ /saml2/\<YourCompanyKey\>**。</span><span class="sxs-lookup"><span data-stu-id="b752e-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="b752e-143">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b752e-143">Click **Next**.</span></span>

4. <span data-ttu-id="b752e-144">在 hello**在 Replicon 設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b752e-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="b752e-145">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777804.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="b752e-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="b752e-146">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b752e-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="b752e-147">tooconfigure SAML 2.0 執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b752e-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="b752e-148">![啟用 SAML 驗證](./media/active-directory-saas-replicon-tutorial/IC777805.png "啟用 SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="b752e-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="b752e-149">toodisplay hello **EnableSAML Authentication2**  對話方塊中，新增下列 tooyour URL，公司金鑰 hello: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="b752e-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="b752e-150">hello 下列範例示範 hello hello 完整的 URL 結構描述：</span><span class="sxs-lookup"><span data-stu-id="b752e-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="b752e-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="b752e-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="b752e-152">按一下 hello  **+**  tooexpand hello **v20Configuration** > 一節。</span><span class="sxs-lookup"><span data-stu-id="b752e-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="b752e-153">按一下 hello  **+**  tooexpand hello **metaDataConfiguration** > 一節。</span><span class="sxs-lookup"><span data-stu-id="b752e-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="b752e-154">按一下**選擇檔案**，tooselect 您的身分識別提供者中繼資料 XML 檔案，然後按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="b752e-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="b752e-155">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b752e-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="b752e-156">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC778418.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="b752e-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="b752e-157">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="b752e-157">Configure user provisioning</span></span>

<span data-ttu-id="b752e-158">在訂單 tooenable Azure AD 使用者 toolog 入 Replicon，它們必須佈建到 Replicon。</span><span class="sxs-lookup"><span data-stu-id="b752e-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="b752e-159">在 Replicon 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="b752e-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="b752e-160">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b752e-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b752e-161">在 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b752e-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="b752e-162">跳過**管理\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="b752e-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="b752e-163">![使用者](./media/active-directory-saas-replicon-tutorial/IC777806.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="b752e-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="b752e-164">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b752e-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="b752e-165">![新增使用者](./media/active-directory-saas-replicon-tutorial/IC777807.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="b752e-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="b752e-166">在 hello**使用者設定檔**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b752e-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b752e-167">![使用者設定檔](./media/active-directory-saas-replicon-tutorial/IC777808.png "使用者設定檔")</span><span class="sxs-lookup"><span data-stu-id="b752e-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="b752e-168">在 hello**登入名稱**文字方塊中，型別 hello Azure AD 電子郵件地址的 hello Azure AD 使用者要 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="b752e-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="b752e-169">針對 [驗證類型] 選取 [SSO]。</span><span class="sxs-lookup"><span data-stu-id="b752e-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="b752e-170">在 hello**部門**文字方塊中，輸入 hello 使用者的部門。</span><span class="sxs-lookup"><span data-stu-id="b752e-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="b752e-171">針對 [員工類型] 選取 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="b752e-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="b752e-172">按一下 [儲存使用者設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="b752e-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="b752e-173">您可以使用任何其他 Replicon 使用者帳戶建立工具或 Api 提供 Replicon tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b752e-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="b752e-174">指派使用者</span><span class="sxs-lookup"><span data-stu-id="b752e-174">Assign users</span></span>
<span data-ttu-id="b752e-175">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="b752e-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="b752e-176">**tooassign 使用者 tooReplicon，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b752e-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="b752e-177">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="b752e-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="b752e-178">在 hello **Replicon**應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="b752e-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="b752e-179">![指派使用者](./media/active-directory-saas-replicon-tutorial/IC777809.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="b752e-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="b752e-180">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="b752e-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="b752e-181">![是](./media/active-directory-saas-replicon-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="b752e-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b752e-182">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b752e-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="b752e-183">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b752e-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

