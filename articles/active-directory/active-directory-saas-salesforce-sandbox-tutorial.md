---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Salesforce 沙箱的單一登入、 自動化佈建，以及更多 ！。"
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
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="185ec-103">教學課程：Azure Active Directory 與 Salesforce 沙箱整合</span><span class="sxs-lookup"><span data-stu-id="185ec-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="185ec-104">本教學課程的 hello 目標是 Azure 與 Salesforce 沙箱 tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="185ec-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="185ec-105">如需意見反應，請參閱 hello [Azure 支援頁面](http://go.microsoft.com/fwlink/?LinkId=521878)。</span><span class="sxs-lookup"><span data-stu-id="185ec-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="185ec-106">沙箱提供您將能夠 toocreate hello 的組織在不同的環境，針對各種用途，例如開發、 多個複本，測試和定型集，而不需要犧牲 hello 資料並在您的 Salesforce 生產環境中的應用程式組織。</span><span class="sxs-lookup"><span data-stu-id="185ec-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="185ec-107">如需詳細資訊，請參閱 [沙箱概觀](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="185ec-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="185ec-108">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="185ec-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="185ec-109">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="185ec-109">A valid Azure subscription</span></span>
* <span data-ttu-id="185ec-110">在 Salesforce.com 中的沙箱</span><span class="sxs-lookup"><span data-stu-id="185ec-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="185ec-111">如果您還沒有有效的沙箱在 Salesforce.com 中，您會需要 toocontact Salesforce。</span><span class="sxs-lookup"><span data-stu-id="185ec-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="185ec-112">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="185ec-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="185ec-113">啟用 Salesforce 沙箱的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="185ec-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="185ec-114">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="185ec-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="185ec-115">啟用您的網域</span><span class="sxs-lookup"><span data-stu-id="185ec-115">Enabling your domain</span></span>
4. <span data-ttu-id="185ec-116">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="185ec-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="185ec-117">指派使用者</span><span class="sxs-lookup"><span data-stu-id="185ec-117">Assigning users</span></span>

<span data-ttu-id="185ec-118">![案例](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "案例")</span><span class="sxs-lookup"><span data-stu-id="185ec-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="185ec-119">啟用 Salesforce 沙箱的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="185ec-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="185ec-120">本節 hello 目標是 toooutline 如何 Salesforce 沙箱 tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="185ec-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="185ec-121">**tooenable hello 應用程式整合 Salesforce 沙箱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="185ec-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="185ec-122">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="185ec-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="185ec-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="185ec-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="185ec-124">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="185ec-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="185ec-125">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="185ec-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="185ec-126">![應用程式](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="185ec-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="185ec-127">tooopen hello**應用程式庫**，按一下 **加入應用程式**，然後按一下**新增應用程式的 我的組織 toouse**。</span><span class="sxs-lookup"><span data-stu-id="185ec-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="185ec-128">![您該怎麼想 toodo？](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "您該怎麼想 toodo？")</span><span class="sxs-lookup"><span data-stu-id="185ec-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="185ec-129">在 hello**搜尋方塊**，型別**Salesforce 沙箱**。</span><span class="sxs-lookup"><span data-stu-id="185ec-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="185ec-130">![應用程式資源庫](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="185ec-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="185ec-131">在 hello 結果窗格中，選取  **Salesforce 沙箱**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="185ec-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="185ec-132">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="185ec-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="185ec-133">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="185ec-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="185ec-134">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSalesforce 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="185ec-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="185ec-135">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="185ec-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="185ec-136">在 Azure 傳統入口網站，在 hello hello **Salesforce 沙箱**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="185ec-137">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="185ec-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="185ec-138">在 hello**如何想您使用者 toosign tooSalesforce 沙箱上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="185ec-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="185ec-139">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="185ec-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="185ec-140">Hello 上**設定應用程式 URL**  頁面的 hello**登入 URL**文字方塊中，輸入您的 URL 使用下列模式的 hello `http://company.my.salesforce.com`，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="185ec-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="185ec-141">![設定應用程式 URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="185ec-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="185ec-142">如果您已經在您目錄中，設定單一登入另一個 Salesforce 沙箱的執行個體，則您也必須設定 hello**識別碼**toohave hello 相同的值為 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="185ec-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="185ec-143">hello**識別碼**欄位可以找到藉由檢查 hello**顯示進階設定**hello 上的核取方塊**設定應用程式 URL** hello 對話方塊頁面。</span><span class="sxs-lookup"><span data-stu-id="185ec-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="185ec-144">在 hello**於 Salesforce 沙箱設定單一登入**頁面上，按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="185ec-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="185ec-145">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="185ec-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="185ec-146">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="185ec-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="185ec-147">在 hello 最上層顯示 hello 功能表上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="185ec-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="185ec-148">![設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="185ec-149">Hello hello 左側瀏覽窗格中按一下**安全性控制**，然後按一下**單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="185ec-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="185ec-150">![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="185ec-151">在 hello 單一登入設定 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="185ec-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="185ec-152">![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="185ec-153">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="185ec-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="185ec-154">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="185ec-154">Click **New**.</span></span>
10. <span data-ttu-id="185ec-155">在 hello SAML 單一登入設定 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="185ec-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="185ec-156">![SAML 單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="185ec-157">在 [hello 名稱] 文字方塊中，輸入 hello hello 組態名稱 (例如： *SPSSOWAAD\_測試*)。</span><span class="sxs-lookup"><span data-stu-id="185ec-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="185ec-158">在 Azure 傳統入口網站，在 hello hello**於 Salesforce 沙箱設定單一登入**對話方塊頁面上，複製 hello**簽發者 URL**值並貼到 hello**簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="185ec-159">在 hello**實體識別碼**文字方塊中，輸入**https://test.salesforce.com**如果這是您要加入 tooyour 目錄 hello 第一個 Salesforce 沙箱執行個體。</span><span class="sxs-lookup"><span data-stu-id="185ec-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="185ec-160">如果您已新增執行個體的 Salesforce 沙箱則 hello**實體識別碼**hello 中的型別**登入 URL**，應該採用下列格式：`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="185ec-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="185ec-161">按一下**瀏覽**tooupload hello 下載憑證。</span><span class="sxs-lookup"><span data-stu-id="185ec-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="185ec-162">做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。</span><span class="sxs-lookup"><span data-stu-id="185ec-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="185ec-163">做為**SAML 識別位置**，選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的識別是**。</span><span class="sxs-lookup"><span data-stu-id="185ec-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="185ec-164">在 Azure 傳統入口網站，在 hello hello**於 Salesforce 沙箱設定單一登入**對話方塊頁面上，複製 hello**遠端登入 URL**值並貼到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="185ec-165">SFDC 不支援 SAML 登出。</span><span class="sxs-lookup"><span data-stu-id="185ec-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="185ec-166">因應措施是，貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello 到**身分識別提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="185ec-167">在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。</span><span class="sxs-lookup"><span data-stu-id="185ec-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="185ec-168">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="185ec-168">Click **Save**.</span></span>
11. <span data-ttu-id="185ec-169">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="185ec-170">![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="185ec-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="185ec-171">啟用網域</span><span class="sxs-lookup"><span data-stu-id="185ec-171">Enable your domain</span></span>
<span data-ttu-id="185ec-172">本節假設您已經建立了一個網域。</span><span class="sxs-lookup"><span data-stu-id="185ec-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="185ec-173">如需詳細資訊，請參閱 [定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。</span><span class="sxs-lookup"><span data-stu-id="185ec-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="185ec-174">**tooenable 您的網域，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="185ec-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="185ec-175">在 hello 左側瀏覽窗格中，按一下 **定義域管理**，然後按一下**我的網域。**</span><span class="sxs-lookup"><span data-stu-id="185ec-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="185ec-176">![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="185ec-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="185ec-177">請確定您的網域已正確設定。</span><span class="sxs-lookup"><span data-stu-id="185ec-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="185ec-178">在 hello**登入頁面設定**區段中，按一下**編輯**，然後當**驗證服務**，選取 hello 名稱從先前的 hello hello SAML 單一登入設定區段，然後按一下 最後**儲存**。</span><span class="sxs-lookup"><span data-stu-id="185ec-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="185ec-179">![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="185ec-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="185ec-180">當您設定網域之後，您的使用者應該使用 hello 網域 URL toologin toohello Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="185ec-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="185ec-181">hello URL 的 tooget hello 值，按一下您已建立 hello 前一節中的 hello SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="185ec-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="185ec-182">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="185ec-182">Configure user provisioning</span></span>
<span data-ttu-id="185ec-183">hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooSalesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="185ec-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="185ec-184">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="185ec-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="185ec-185">在 hello Salesforce 入口網站，在 hello 上方導覽列中，選取名稱 tooexpand 使用者功能表：</span><span class="sxs-lookup"><span data-stu-id="185ec-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="185ec-186">![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "我的設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="185ec-187">從使用者功能表中，選取**我的設定**tooopen 您**我的設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="185ec-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="185ec-188">在 hello 左窗格中，按一下 **個人**tooexpand hello 個人的區段，然後按一下**重設我的安全性 Token**:</span><span class="sxs-lookup"><span data-stu-id="185ec-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="185ec-189">![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "我的設定")</span><span class="sxs-lookup"><span data-stu-id="185ec-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="185ec-190">在 hello**重設我的安全性 Token**頁面上，按一下**重設安全性 Token** toorequest 包含 Salesforce.com 安全性 token 的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="185ec-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="185ec-191">![新的權杖](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "新的權杖")</span><span class="sxs-lookup"><span data-stu-id="185ec-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="185ec-192">檢查您的電子郵件收件匣，尋找來自 Salesforce.com 且主旨為「**salesforce.com.com 安全性確認**」的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="185ec-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="185ec-193">檢閱此電子郵件和複製 hello 安全性 token 值。</span><span class="sxs-lookup"><span data-stu-id="185ec-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="185ec-194">在 Azure 傳統入口網站，在 hello hello **salesforce 沙箱**應用程式整合頁面上，按一下 **設定使用者佈建**tooopen hello**設定使用者佈建**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="185ec-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="185ec-195">![設定使用者佈建](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "設定使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="185ec-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="185ec-196">在 hello**輸入您 Salesforce 沙箱認證 tooenable 自動使用者佈建**頁面上，提供下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="185ec-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="185ec-197">![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 沙箱")</span><span class="sxs-lookup"><span data-stu-id="185ec-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="185ec-198">在 hello **Salesforce 沙箱管理使用者名稱**文字方塊中，輸入的 Salesforce 帳戶名稱已 hello**系統管理員**在 Salesforce.com 被指派的設定檔。</span><span class="sxs-lookup"><span data-stu-id="185ec-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="185ec-199">在 hello **Salesforce 沙箱管理員密碼**文字方塊中，此帳戶類型 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="185ec-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="185ec-200">在 hello**使用者安全性 Token**文字方塊中，貼上 hello 安全性 token 值。</span><span class="sxs-lookup"><span data-stu-id="185ec-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="185ec-201">按一下**驗證**tooverify 您的設定。</span><span class="sxs-lookup"><span data-stu-id="185ec-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="185ec-202">按一下 hello**下一步**按鈕 tooopen hello**確認**頁面。</span><span class="sxs-lookup"><span data-stu-id="185ec-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="185ec-203">在 hello**確認**頁面上，按一下**完成**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="185ec-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="185ec-204">指派使用者</span><span class="sxs-lookup"><span data-stu-id="185ec-204">Assigning users</span></span>

<span data-ttu-id="185ec-205">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="185ec-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="185ec-206">**tooassign 使用者 tooSalesforce 沙箱，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="185ec-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="185ec-207">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="185ec-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="185ec-208">在 hello * * Salesforce 沙箱 * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="185ec-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="185ec-209">![指派使用者](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="185ec-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="185ec-210">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="185ec-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="185ec-211">![是](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="185ec-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="185ec-212">您現在應該等候 10 分鐘並驗證 hello 帳戶已同步處理的 tooSalesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="185ec-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="185ec-213">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="185ec-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="185ec-214">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="185ec-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

