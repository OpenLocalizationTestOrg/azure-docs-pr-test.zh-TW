---
title: "教學課程：Azure Active Directory 與 Cisco Webex 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Cisco Webex 的單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="3437f-103">教學課程：Azure Active Directory 與 Cisco Webex 整合</span><span class="sxs-lookup"><span data-stu-id="3437f-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="3437f-104">本教學課程的 hello 目標是 Azure 與 Cisco Webex tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="3437f-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="3437f-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="3437f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="3437f-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="3437f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3437f-107">Cisco Webex 租用戶</span><span class="sxs-lookup"><span data-stu-id="3437f-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="3437f-108">完成本教學課程之後, hello 您已指派的 tooCisco Webex 將會無法 toosingle 登入 hello 應用程式位於您 Cisco Webex 公司網站 （服務提供者起始登入），Azure AD 使用者，或使用 hello[簡介 toohello存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3437f-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="3437f-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="3437f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="3437f-110">啟用 Cisco Webex 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="3437f-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="3437f-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="3437f-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="3437f-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="3437f-112">Configuring user provisioning</span></span>
* <span data-ttu-id="3437f-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="3437f-113">Assigning users</span></span>

<span data-ttu-id="3437f-114">![案例](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "案例")</span><span class="sxs-lookup"><span data-stu-id="3437f-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="3437f-115">啟用 Cisco Webex 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="3437f-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="3437f-116">本節 hello 目標是 toooutline 如何 Cisco Webex tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="3437f-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="3437f-117">**Cisco Webex tooenable hello 應用程式整合執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3437f-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="3437f-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="3437f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3437f-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3437f-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3437f-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="3437f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="3437f-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="3437f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="3437f-122">![應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="3437f-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3437f-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="3437f-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="3437f-124">![新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="3437f-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3437f-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3437f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="3437f-126">![從資源庫新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="3437f-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3437f-127">在 hello**搜尋方塊**，型別**Cisco Webex**。</span><span class="sxs-lookup"><span data-stu-id="3437f-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="3437f-128">![應用程式資源庫](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="3437f-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="3437f-129">在 hello 結果窗格中，選取  **Cisco Webex**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3437f-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="3437f-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="3437f-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3437f-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="3437f-131">Configure single sign-on</span></span>

<span data-ttu-id="3437f-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCisco Webex 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="3437f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="3437f-133">此程序的一部分，您就需要的 toocreate base 64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="3437f-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="3437f-134">如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="3437f-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="3437f-135">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3437f-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="3437f-136">在 Azure 傳統入口網站，在 hello hello **Cisco Webex**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3437f-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3437f-137">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3437f-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="3437f-138">在 hello**方式上 tooCisco Webex 使用者 toosign 想您**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3437f-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3437f-139">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3437f-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="3437f-140">在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3437f-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="3437f-141">![設定應用程式 URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="3437f-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="3437f-142">在 hello**登入 URL**文字方塊中，輸入您的 Cisco Webex 租用戶 URL (例如： *http://contoso.webex.com*)。</span><span class="sxs-lookup"><span data-stu-id="3437f-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="3437f-143">在 hello **Cisco Webex 回覆 URL**文字方塊中，輸入您**Cisco Webex AssertionConsumerService URL** (例如： *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="3437f-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="3437f-144">在 hello**於 Cisco Webex 設定單一登入**頁面、 toodownload 憑證，請按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="3437f-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="3437f-145">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3437f-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="3437f-146">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Cisco Webex 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3437f-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="3437f-147">在 hello 最上層顯示 hello 功能表上，按一下**網站管理**。</span><span class="sxs-lookup"><span data-stu-id="3437f-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="3437f-148">![網站管理](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "網站管理")</span><span class="sxs-lookup"><span data-stu-id="3437f-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="3437f-149">在 hello**管理站台**區段中，按一下**SSO 組態**。</span><span class="sxs-lookup"><span data-stu-id="3437f-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="3437f-150">![SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="3437f-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="3437f-151">在 hello 同盟 Web SSO 組態 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3437f-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3437f-152">![同盟 SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "同盟 SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="3437f-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="3437f-153">從 hello**同盟通訊協定**清單中，選取**SAML 2.0**。</span><span class="sxs-lookup"><span data-stu-id="3437f-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="3437f-154">從您下載的憑證建立 **Base-64 編碼** 檔案。</span><span class="sxs-lookup"><span data-stu-id="3437f-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="3437f-155">如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="3437f-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="3437f-156">在 [記事本]，然後再複製 hello 它的內容中開啟您的 base-64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="3437f-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="3437f-157">按一下 [匯入 SAML 中繼資料] ，然後貼上 base-64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="3437f-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="3437f-158">在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**簽發者 URL**值並貼到 hello **(IdP ID)SAML的簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3437f-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="3437f-159">在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**遠端登入 URL**值並貼到 hello**客戶 SSO 服務登入URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3437f-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="3437f-160">從 hello **NameID 格式**清單中，選取**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3437f-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="3437f-161">在 hello **AuthnContextClassRef**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:ac:classes:Password**。</span><span class="sxs-lookup"><span data-stu-id="3437f-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="3437f-162">在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**遠端登出 URL**值並貼到 hello**客戶 SSO 服務登出URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3437f-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="3437f-163">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="3437f-163">Click **Update**.</span></span>
9. <span data-ttu-id="3437f-164">在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，選取 hello 單一登入組態確認，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="3437f-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="3437f-165">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="3437f-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="3437f-166">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="3437f-166">Configure user provisioning</span></span>

<span data-ttu-id="3437f-167">在訂單 tooenable Azure AD 使用者 toolog 到 Cisco Webex，它們必須佈建到 Cisco Webex。</span><span class="sxs-lookup"><span data-stu-id="3437f-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="3437f-168">在 Cisco Webex 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="3437f-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="3437f-169">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="3437f-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="3437f-170">登入 tooyour **Cisco Webex**租用戶。</span><span class="sxs-lookup"><span data-stu-id="3437f-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="3437f-171">跳過**管理使用者\>新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="3437f-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="3437f-172">![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="3437f-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="3437f-173">在 hello 新增使用者 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3437f-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3437f-174">![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="3437f-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="3437f-175">針對 [帳戶類型]，選取 [主機]。</span><span class="sxs-lookup"><span data-stu-id="3437f-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="3437f-176">Hello 下列文字方塊中輸入現有 Azure AD 使用者的 hello 資訊：**名字、 姓氏**，**使用者名**，**電子郵件**，**密碼**，**確認密碼**。</span><span class="sxs-lookup"><span data-stu-id="3437f-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="3437f-177">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3437f-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="3437f-178">您可以使用任何其他 Cisco Webex 使用者帳戶建立工具或 Api 提供 Cisco Webex tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3437f-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="3437f-179">指派使用者</span><span class="sxs-lookup"><span data-stu-id="3437f-179">Assign users</span></span>
<span data-ttu-id="3437f-180">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="3437f-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="3437f-181">**tooassign 使用者 tooCisco Webex 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3437f-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="3437f-182">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="3437f-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3437f-183">在 hello **Cisco Webex**應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="3437f-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3437f-184">![指派使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="3437f-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="3437f-185">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="3437f-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="3437f-186">![是](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="3437f-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3437f-187">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3437f-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="3437f-188">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3437f-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

