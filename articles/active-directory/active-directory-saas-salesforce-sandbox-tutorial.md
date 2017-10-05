---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解如何使用 Salesforce 沙箱搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="1b6f0-103">教學課程：Azure Active Directory 與 Salesforce 沙箱整合</span><span class="sxs-lookup"><span data-stu-id="1b6f0-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="1b6f0-104">本教學課程的目的是要示範 Azure 與 Salesforce 沙箱的整合。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="1b6f0-105">若要反應意見，請參閱 [Azure 支援頁面](http://go.microsoft.com/fwlink/?LinkId=521878)。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="1b6f0-106">沙箱讓您能夠針對不同用途 (例如開發、測試和訓練) 在個別環境中建立貴組織的多個複本，而不會危害 Salesforce 生產環境組織中的資料和應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="1b6f0-107">如需詳細資訊，請參閱 [沙箱概觀](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="1b6f0-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="1b6f0-108">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1b6f0-109">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="1b6f0-109">A valid Azure subscription</span></span>
* <span data-ttu-id="1b6f0-110">在 Salesforce.com 中的沙箱</span><span class="sxs-lookup"><span data-stu-id="1b6f0-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="1b6f0-111">如果您在 Salesforce.com 中還沒有有效的沙箱，則您需要連絡 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="1b6f0-112">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="1b6f0-113">啟用 Salesforce 沙箱的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="1b6f0-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="1b6f0-114">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="1b6f0-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="1b6f0-115">啟用您的網域</span><span class="sxs-lookup"><span data-stu-id="1b6f0-115">Enabling your domain</span></span>
4. <span data-ttu-id="1b6f0-116">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="1b6f0-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="1b6f0-117">指派使用者</span><span class="sxs-lookup"><span data-stu-id="1b6f0-117">Assigning users</span></span>

<span data-ttu-id="1b6f0-118">![案例](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "案例")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="1b6f0-119">啟用 Salesforce 沙箱的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="1b6f0-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="1b6f0-120">本節的目的是要說明如何啟用 Salesforce 沙箱的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="1b6f0-121">**若要啟用 Salesforce 沙箱的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1b6f0-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6f0-122">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1b6f0-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1b6f0-124">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1b6f0-125">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="1b6f0-126">![應用程式](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1b6f0-127">若要開啟 [應用程式庫]，請按一下 [新增應用程式]，然後按一下 [新增應用程式讓我的組織使用]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="1b6f0-128">![您要怎麼做？](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "您要怎麼做？")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="1b6f0-129">在 [搜尋方塊] 中，輸入 **Salesforce 沙箱**。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="1b6f0-130">![應用程式資源庫](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="1b6f0-131">在結果窗格中，選取 [Salesforce 沙箱]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="1b6f0-132">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="1b6f0-133">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="1b6f0-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="1b6f0-134">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶在 Salesforce 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="1b6f0-135">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1b6f0-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6f0-136">在 Azure 傳統入口網站的 [Salesforce 沙箱] 應用程式整合頁面上，按一下 [設定單一登入] 開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="1b6f0-137">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1b6f0-138">在 [要如何讓使用者登入 Salesforce 沙箱] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1b6f0-139">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="1b6f0-140">在 [設定應用程式 URL] 頁面的 [登入 URL] 文字方塊中，使用下列模式輸入您的 URL：`http://company.my.salesforce.com`，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="1b6f0-141">![設定應用程式 URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="1b6f0-142">如果您已為目錄中的另一個 Salesforce 沙箱執行個體設定單一登入，則也須將**識別碼**設定為具有與**登入 URL** 相同的值。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="1b6f0-143">您也可以在對話方塊的 [設定應用程式 URL] 頁面上核取 [顯示進階設定] 核取方塊，來尋找 [識別碼] 欄位。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="1b6f0-144">在 [設定在 Salesforce 沙箱單一登入] 頁面上，按一下 [下載憑證]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="1b6f0-145">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="1b6f0-146">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="1b6f0-147">在頂端的功能表中，按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="1b6f0-148">![設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="1b6f0-149">在左側的導覽窗格中，按一下 [安全性控制項]，然後按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="1b6f0-150">![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="1b6f0-151">在 [單一登入設定] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="1b6f0-152">![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="1b6f0-153">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="1b6f0-154">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-154">Click **New**.</span></span>
10. <span data-ttu-id="1b6f0-155">在 [SAML 單一登入設定] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="1b6f0-156">![SAML 單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="1b6f0-157">在 [名稱] 文字方塊中，輸入組態的名稱 (例如：*SPSSOWAAD\_Test*)。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="1b6f0-158">在 Azure 傳統入口網站中的 [設定在 Salesforce 沙箱單一登入] 對話方塊頁面上，複製 [簽發者 URL] 值，然後貼到 [簽發者] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="1b6f0-159">如果這是您要新增至目錄的第一個 Salesforce 沙箱執行個體，請在 [實體識別碼] 文字方塊中，輸入 **https://test.salesforce.com**。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="1b6f0-160">如果您已新增 Salesforce 沙箱的執行個體，請對 [實體識別碼] 輸入**登入 URL**，其格式如下：`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="1b6f0-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="1b6f0-161">按一下 [瀏覽] 來上傳已下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="1b6f0-162">對於 [SAML 身分識別類型]，選取 [判斷提示包含來自使用者物件的同盟識別碼]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="1b6f0-163">對於 [SAML 身分識別位置]，選取 [身分識別位於 Subject 陳述式的 NameIdentifier 元素中]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="1b6f0-164">在 Azure 傳統入口網站中的 [設定在 Salesforce 沙箱單一登入] 對話頁面上，複製 [遠端登入 URL] 值，然後貼到 [識別提供者登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="1b6f0-165">SFDC 不支援 SAML 登出。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="1b6f0-166">解決方法是在 [識別提供者登出 URL] 文字方塊中貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="1b6f0-167">在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="1b6f0-168">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-168">Click **Save**.</span></span>
11. <span data-ttu-id="1b6f0-169">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1b6f0-170">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="1b6f0-171">啟用網域</span><span class="sxs-lookup"><span data-stu-id="1b6f0-171">Enable your domain</span></span>
<span data-ttu-id="1b6f0-172">本節假設您已經建立了一個網域。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="1b6f0-173">如需詳細資訊，請參閱 [定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="1b6f0-174">**若要啟用您的網域，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1b6f0-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6f0-175">在左邊的導覽窗格中按一下 [網域管理]，然後按一下 [我的網域]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="1b6f0-176">![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1b6f0-177">請確定您的網域已正確設定。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="1b6f0-178">在 [登入頁面設定] 區段中，按一下 [編輯]，然後對於 [驗證服務]，選取來自前一區段 SAML 單一登入設定的名稱，最後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="1b6f0-179">![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="1b6f0-180">一旦您設定了網域，您的使用者便應使用該網域 URL 登入至 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="1b6f0-181">若要取得 URL 的值，請按一下您在上一區段中所建立的 SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="1b6f0-182">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="1b6f0-182">Configure user provisioning</span></span>
<span data-ttu-id="1b6f0-183">本節的目的是要說明如何對 Salesforce 沙箱啟用 Active Directory 使用者帳戶的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="1b6f0-184">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1b6f0-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6f0-185">在 Salesforce 入口網站上方的導覽列中選取您的名稱來展開使用者功能表：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="1b6f0-186">![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "我的設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="1b6f0-187">從使用者功能表中，選取 [我的設定] 來開啟 [我的設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="1b6f0-188">在左方導覽窗格中，按一下 [個人] 來展開 [個人] 區段，然後按一下 [重設我的安全性權杖]：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="1b6f0-189">![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "我的設定")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="1b6f0-190">在 [重設我的安全性權杖] 頁面上，按一下 [重設安全性權杖] 來要求包含 Salesforce.com 安全性權杖的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="1b6f0-191">![新的權杖](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "新的權杖")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="1b6f0-192">檢查您的電子郵件收件匣，尋找來自 Salesforce.com 且主旨為「**salesforce.com.com 安全性確認**」的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="1b6f0-193">檢閱這封電子郵件並複製安全性權杖值。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="1b6f0-194">在 Azure 傳統入口網站中的 [Salesforce 沙箱] 應用程式整合頁面上，按一下 [設定使用者佈建] 來開啟 [設定使用者佈建] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="1b6f0-195">![設定使用者佈建](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "設定使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="1b6f0-196">在 [輸入您的 Salesforce 沙箱認證來啟用自動使用者佈建]  頁面上，提供以下組態設定：</span><span class="sxs-lookup"><span data-stu-id="1b6f0-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="1b6f0-197">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="1b6f0-198">在 [Salesforce 沙箱管理員使用者名稱] 文字方塊中，輸入已在 Salesforce.com 中指派**系統管理員**設定檔的 Salesforce 沙箱帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="1b6f0-199">在 [Salesforce 沙箱管理員密碼] 文字方塊中，輸入這個帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="1b6f0-200">在 [使用者安全性權杖] 文字方塊中，貼上安全性權杖值。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="1b6f0-201">按一下 [驗證] 來驗證您的組態。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="1b6f0-202">按 [下一步] 按鈕以開啟 [確認] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="1b6f0-203">在 [確認] 頁面上，按一下 [完成] 來儲存您的組態。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="1b6f0-204">指派使用者</span><span class="sxs-lookup"><span data-stu-id="1b6f0-204">Assigning users</span></span>

<span data-ttu-id="1b6f0-205">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1b6f0-206">**若要將使用者指派給 Salesforce 沙箱，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1b6f0-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6f0-207">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1b6f0-208">在 [Salesforce Sandbox] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1b6f0-209">![指派使用者](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="1b6f0-210">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1b6f0-211">![是](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="1b6f0-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1b6f0-212">請等候 10 分鐘並確認帳戶已同步至 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="1b6f0-213">如果要測試您的 SSO 設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="1b6f0-214">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="1b6f0-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

