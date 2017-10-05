---
title: "教學課程：Azure Active Directory 與 Cisco Webex 整合 | Microsoft Docs"
description: "了解如何使用 Cisco Webex 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="476c6-103">教學課程：Azure Active Directory 與 Cisco Webex 整合</span><span class="sxs-lookup"><span data-stu-id="476c6-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="476c6-104">本教學課程的目的是要示範 Azure 與 Cisco Webex 的整合。</span><span class="sxs-lookup"><span data-stu-id="476c6-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="476c6-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="476c6-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="476c6-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="476c6-106">A valid Azure subscription</span></span>
* <span data-ttu-id="476c6-107">Cisco Webex 租用戶</span><span class="sxs-lookup"><span data-stu-id="476c6-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="476c6-108">完成本教學課程之後，您指派給 Cisco Webex 的 Azure AD 使用者就能夠單一登入您 Cisco Webex 公司網站 (服務提供者起始登入) 的應用程式，或是使用 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="476c6-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="476c6-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="476c6-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="476c6-110">啟用 Cisco Webex 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="476c6-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="476c6-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="476c6-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="476c6-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="476c6-112">Configuring user provisioning</span></span>
* <span data-ttu-id="476c6-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="476c6-113">Assigning users</span></span>

<span data-ttu-id="476c6-114">![案例](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "案例")</span><span class="sxs-lookup"><span data-stu-id="476c6-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="476c6-115">啟用 Cisco Webex 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="476c6-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="476c6-116">本節的目的是要說明如何啟用 Cisco Webex 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="476c6-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="476c6-117">**若要啟用 Cisco Webex 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="476c6-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="476c6-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="476c6-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="476c6-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="476c6-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="476c6-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="476c6-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="476c6-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="476c6-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="476c6-122">![應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="476c6-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="476c6-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="476c6-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="476c6-124">![新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="476c6-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="476c6-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="476c6-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="476c6-126">![從資源庫新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="476c6-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="476c6-127">在**搜尋方塊**中，輸入 **Cisco Webex**。</span><span class="sxs-lookup"><span data-stu-id="476c6-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="476c6-128">![應用程式資源庫](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="476c6-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="476c6-129">在結果窗格中，選取 [Cisco Webex]，然後按一下 [完成] 以加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="476c6-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="476c6-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="476c6-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="476c6-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="476c6-131">Configure single sign-on</span></span>

<span data-ttu-id="476c6-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶在 Cisco Webex 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="476c6-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="476c6-133">在這個程序中，您必須建立 base-64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="476c6-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="476c6-134">如果您不熟悉這個程序，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="476c6-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="476c6-135">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="476c6-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="476c6-136">在 Azure 傳統入口網站的 [Cisco Webex] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="476c6-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="476c6-137">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="476c6-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="476c6-138">在 [要如何讓使用者登入 Cisco Webex] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="476c6-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="476c6-139">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="476c6-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="476c6-140">在 [設定應用程式 URL] 頁面上，執行下列步驟，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="476c6-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="476c6-141">![設定應用程式 URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="476c6-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="476c6-142">在 [登入 URL] 文字方塊中，輸入您的 Cisco Webex 租用戶 URL (例如：*http://contoso.webex.com*)。</span><span class="sxs-lookup"><span data-stu-id="476c6-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="476c6-143">在 [Cisco Webex 回覆 URL] 文字方塊中，輸入您的 **Cisco Webex AssertionConsumerService URL** (例如︰*https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*)。</span><span class="sxs-lookup"><span data-stu-id="476c6-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="476c6-144">於 [在 Cisco Webex 設定單一登入] 頁面上，按 [下載憑證] 以下載您的憑證，然後將憑證檔案儲存在您的電腦中。</span><span class="sxs-lookup"><span data-stu-id="476c6-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="476c6-145">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="476c6-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="476c6-146">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Cisco Webex 公司網站。</span><span class="sxs-lookup"><span data-stu-id="476c6-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="476c6-147">在頂端的功能表中，按一下 [網站管理] 。</span><span class="sxs-lookup"><span data-stu-id="476c6-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="476c6-148">![網站管理](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "網站管理")</span><span class="sxs-lookup"><span data-stu-id="476c6-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="476c6-149">在 [管理網站] 區段中，按一下 [SSO 組態]。</span><span class="sxs-lookup"><span data-stu-id="476c6-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="476c6-150">![SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="476c6-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="476c6-151">在 [同盟網頁 SSO 組態] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="476c6-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="476c6-152">![同盟 SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "同盟 SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="476c6-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="476c6-153">從 [同盟通訊協定] 清單中選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="476c6-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="476c6-154">從您下載的憑證建立 **Base-64 編碼** 檔案。</span><span class="sxs-lookup"><span data-stu-id="476c6-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="476c6-155">如需詳細資訊，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="476c6-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="476c6-156">在記事本中開啟 base-64 編碼的憑證，然後複製其內容。</span><span class="sxs-lookup"><span data-stu-id="476c6-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="476c6-157">按一下 [匯入 SAML 中繼資料] ，然後貼上 base-64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="476c6-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="476c6-158">在 Azure 傳統入口網站的 [在 Cisco Webex 設定單一登入] 對話頁面上，複製 [簽發者 URL] 值，然後將它貼至 [SAML 的簽發者 (IdP 識別碼)]文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="476c6-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="476c6-159">在 Azure 傳統入口網站的 [在 Cisco Webex 設定單一登入] 對話頁面上，複製 [遠端登入 URL] 值，然後將它貼至 [客戶 SSO 服務登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="476c6-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="476c6-160">從 [NameID 格式] 清單中選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="476c6-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="476c6-161">在 [AuthnContextClassRef] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**。</span><span class="sxs-lookup"><span data-stu-id="476c6-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="476c6-162">在 Azure 傳統入口網站的 [在 Cisco Webex 設定單一登入] 對話頁面上，複製 [遠端登出 URL] 值，然後將它貼至 [客戶 SSO 服務登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="476c6-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="476c6-163">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="476c6-163">Click **Update**.</span></span>
9. <span data-ttu-id="476c6-164">在 Azure 傳統入口網站的 [在 Cisco Webex 設定單一登入] 對話頁面上，選取單一登入設定確認，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="476c6-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="476c6-165">![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="476c6-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="476c6-166">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="476c6-166">Configure user provisioning</span></span>

<span data-ttu-id="476c6-167">若要讓 Azure AD 使用者可以登入 Cisco Webex，則必須將他們佈建到 Cisco Webex。</span><span class="sxs-lookup"><span data-stu-id="476c6-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="476c6-168">Cisco Webex 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="476c6-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="476c6-169">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="476c6-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="476c6-170">登入您的 **Cisco Webex** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="476c6-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="476c6-171">移至 [管理使用者] \> [加入使用者]。</span><span class="sxs-lookup"><span data-stu-id="476c6-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="476c6-172">![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="476c6-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="476c6-173">在 [加入使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="476c6-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="476c6-174">![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="476c6-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="476c6-175">針對 [帳戶類型]，選取 [主機]。</span><span class="sxs-lookup"><span data-stu-id="476c6-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="476c6-176">在下列文字方塊中，輸入現有 Azure AD 使用者的資訊：**名字、姓氏**、**使用者名稱**、**電子郵件**、**密碼**、**確認密碼**。</span><span class="sxs-lookup"><span data-stu-id="476c6-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="476c6-177">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="476c6-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="476c6-178">您可以使用任何其他的 Cisco Webex 使用者帳戶建立工具或 Cisco Webex 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="476c6-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="476c6-179">指派使用者</span><span class="sxs-lookup"><span data-stu-id="476c6-179">Assign users</span></span>
<span data-ttu-id="476c6-180">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="476c6-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="476c6-181">**若要指派使用者給 Cisco Webex，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="476c6-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="476c6-182">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="476c6-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="476c6-183">在 [Cisco Webex] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="476c6-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="476c6-184">![指派使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="476c6-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="476c6-185">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="476c6-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="476c6-186">![是](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="476c6-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="476c6-187">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="476c6-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="476c6-188">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="476c6-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

